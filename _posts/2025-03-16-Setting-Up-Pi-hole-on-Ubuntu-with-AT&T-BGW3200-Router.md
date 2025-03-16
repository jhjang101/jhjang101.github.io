---
layout: single 
classes: wide
title: "Setting Up Pi-hole on Ubuntu with AT&T BGW320 Router" 
last_modified_at:
---

Pi-hole is a free and open-source network-wide DNS sinkhole that acts as a highly effective ad blocker and privacy tool. It intercepts DNS requests, filtering them against lists of known ad-serving domains.

While the most straightforward method of installing Pi-hole is on a raspberry Pi, I happened to have an HP microcomputer that I repurposed into a Linux toy server. So I chose to run Pi-hole in a Docker container for flexibility.

To use Pi-hole as you private DNS server, you need to configure your router to use Pi-hole's IP address as their DNS server. Unfortunately, my AT&T Fiber's BGW320-505 router does not allow changing DNS settings. While Pi-hole's DHCP server could be a solution, I instead chose to manually configure the DNS settings on devices where I wanted ad-blocking enabled.


##  **Step 1: Assign a Static IP to the Ubuntu Server**

Before setting up Pi-hole and other services, it's important to assign a **static IP address** to the Ubuntu server. This ensures that the server always has the same IP address, preventing connectivity issues.

1. Open a web browser and go to the **router web interface** at [http://192.168.1.254](http://192.168.1.254)
2. Go to **Home Network > IP Allocation**
3. Enter the **device access code** (found on the router label)
4. Locate the Ubuntu server in the device list
5. Assign it a **static IP (192.168.1.100)** or which ever you prefer


## **Step 2: Install Pi-hole in Docker**

Installing Pi-hole within an isolated Docker environment simplifies its management. If Docker isn't already installed, the [official Docker documentation provides an installation guide](https://docs.docker.com/engine/install/ubuntu/).   
Assuming Docker is set up, this section will guide you through the process of installing Pi-hole as a Docker container.

1. Create a directory for Pi-hole.  
```bash
sudo mkdir -p docker/pihole
```

2. Move to the directory.  
```bash
cd docker/pihole
```

3. Create a `compose.yaml` file.
```bash
sudo nano docker-compose.yml
```

4. Add the following configuration file.  
  ```yaml
  services:
    pihole:
      container_name: pihole
      image: pihole/pihole:latest
      ports:
        - "53:53/tcp"
        - "53:53/udp"
        - "80:80/tcp"
        - "443:443/tcp"
      environment:
        TZ: 'America/Chicago'
        FTLCONF_webserver_api_password: 'mypassword'
        FTLCONF_dns_listeningMode: 'all'
      volumes:
        - './etc-pihole:/etc/pihole'
      restart: unless-stopped
  ```
  Set the appropriate timezone for your location and replace `mypassword` with a password for the Pi-hole admin panel.  

  5. Start Pi-hole using Docker Compose.  
  ```bash
  docker compose up -d
  ```

6. Verify that Pi-hole is running.  
```bash
 docker ps
 ```

7. Access the Pi-hole admin interface.  
	- Open a browser and go to: [http://192.168.1.100/admin/](http://192.168.1.100/admin/)
	- Log in using the password set earlier.


## **Step 3: Disable systemd-resolved and Set Pi-hole as DNS**

Ubuntu and Fedora use `systemd-resolved`, which includes a **DNS Stub Listener** that listens on **port 53** to speed up DNS queries.

However, **Pi-hole also runs its own DNS server on port 53**, which conflicts with `systemd-resolved`’s DNS stub listener.  To resolve this, we need to disable the stub resolver and configure the system to use Pi-hole directly.

1. Disable the stub resolver.
```bash
sudo sed -r -i.orig 's/#?DNSStubListener=yes/DNSStubListener=no/g' /etc/systemd/resolved.conf
```

2. Remove existing `/etc/resolv.conf`
```bash
sudo rm /etc/resolv.conf
```

3. Manually set `/etc/resolv.conf` to point to your Pi-hole server. While Pi-hole documentation often recommends creating a symlink to `/run/systemd/resolve/resolv.conf` for automatic DNS updates based on `netplan` settings, this is not ideal in my situation due to the AT&T router's limitations. Therefore, we will directly set Pi-hole as the DNS server:
```bash
echo "nameserver 192.168.1.100" | sudo tee /etc/resolv.conf
``` 
This still might be a temporally solution, as `systemd-resolved` may regenerate `/etc/resolv.conf` and overwrite your manual changes on system reboot. Optionally, you can prevent the system overwrites.  
```bash
sudo chattr +i /etc/resolv.conf
```

**Warning:**  
Setting the immutable attribute will prevent any modifications to `/etc/resolv.conf` until you explicitly remove it using `sudo chattr -i /etc/resolv.conf`.
{: .notice--warning}



## **Step 4: Disable IPv6 on the AT&T BGW320 Router**

Disabling IPv6 prevents devices from bypassing Pi-hole by using external IPv6 DNS servers.  
To disable IPv6 on the AT&T BGW320 router:

1. Log into the **router settings** [http://192.168.1.254](http://192.168.1.254)
2. Navigate to **Home Network > IPv6**.
3. Set **IPv6** to **Off** and save changes.


## **Step 5: Manually Set DNS to Pi-hole on Each Device**

Since AT&T does not allow changing the router’s DNS settings, I chose to manually configure the DNS settings on devices where I wanted ad-blocking enabled.  

- **Windows:** Go to **Network Settings > Change Adapter Options > Properties > IPv4 > Properties**, set DNS to **192.168.1.100**.
- **Linux:** As demonstrated in Step 3, modify the `/etc/resolv.conf` file.
- **Phones & Tablets:** Typically, you can find DNS settings within the Wi-Fi connection details. Look for advanced options or IP settings and manually enter **192.168.1.100** as the DNS server.


## **What's Next?**

I've already updated my Pi-hole blocklists using the excellent resource at [https://github.com/hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists).

This is temporary setup to address the limitation of my AT&T router, which doesn't allow custom DNS configuration. My next step is to buy a router that will allow me to deploy Pi-hole across my entire home network and integrate a VPN.