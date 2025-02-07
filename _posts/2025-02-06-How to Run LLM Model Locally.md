---
layout: single 
classes: 
title: "How to Run LLM Model Locally" 
last_modified_at:
---

In this guide, I will walk through the steps to run large language models (LLMs) on your local machine using Ollama and Open WebUI.

## Setting Up Ollama
1. **Install Ollama**: Ollama (Open Source Large Language Model Meta AI) is an open source platform that allow you to run LLMs on a local machine. You can download and install it from their [website](https://ollama.com/)
2. **Choose a Model**: Ollama offers various LLM model that you can choose from. I choose [phi4 model](https://ollama.com/library/phi4).
3. **Run the Model**: Open commend prompt and run:

``` sh
ollama run phi4
```
4.  That's all!

## Setting Up Open WebUI
Open WebUI is an extensible, feature-rich AI platform that operates offline with an OpenAI-compatible interface. It's recommended to use Docker for running Open WebUI.
1. **Install Docker** : If you haven't already, download and install [Docker](https://www.docker.com/).
2. **Run Open-WebUI** : In my case, I will run Open-WebUI with Nvidia GPU, so use this commend:

``` sh
docker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:cuda
```
Alternatively, you can install Open WebUI bundled with Ollama with GPU support:

``` sh
docker run -d -p 3000:8080 --gpus=all -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:ollama
```
3.  **Access Open WebUI** : Navigate to `localhost:3000` in your web browser.

## Nvidia CUDA Toolkit

To monitor GPU usage, use the Nvidia command-line utility:

``` sh
nvidia-smi -l 1
```

This will display information like GPU utilization and power usage at specified intervals (e.g., every 1 second). If your LLM isn't utilizing the GPU, consider installing the [Nvidia CUDA toolkit](https://developer.nvidia.com/cuda-downloads) .
\## Integration with Continue VSCode Plugin
You can integrate a local LLM into the [Continue](https://www.continue.dev/) VSCode Plugin as an AI code assistant. Detailed instructions are available in the [Open WebUI documentation](https://docs.openwebui.com/tutorials/integrations/continue-dev) .
Here is an example of `config.json`

``` json
  "models": [
    {
      "title": "qwen:14b",
      "provider": "openai",
      "model": "qwen2.5-coder:14b",
      "apiBase": "http://localhost:3000/ollama/v1",
      "apiKey": "sk-YOUR-API-KEY"
    }
  ],
```

The API key can be found in Open WebUI under Settings \> Account.