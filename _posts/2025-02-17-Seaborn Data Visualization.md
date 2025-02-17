---
layout: single 
classes: wide
title: "Seaborn Data Visualization " 
last_modified_at:
---

When it comes to data visualization in Python, **Matplotlib** is powerful but often requires extra effort to make plots look polished. **Seaborn**, built on top of Matplotlib, simplifies this process by providing a high-level interface for drawing attractive and informative statistical graphics.

It integrates well with **Pandas** data structures, making it easy to visualize data directly from DataFrames without needing to manually extract columns.

In this post, we’ll explore how to get started with Seaborn, create great-looking visualizations with minimal effort.

Import required libraries.
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

We will use iris dataset to create plots.
```python
df = sns.load_dataset('iris')
df.head()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>
</div>

## Set seaborn style theme

Parameters: [Seaborn link](https://seaborn.pydata.org/generated/seaborn.set_theme.html)
- **context**: changes label size, line thickness, etc  
  options: 'paper', 'notebook', 'talk', 'poster'
- **style**: changes plot styles  
  options: 'darkgrid', 'whitegrid', 'dark', 'white', 'ticks'
- **palette**: Choose color palette, see color palettes section for detail
  options: 'deep', 'muted', 'bright', 'pastel', 'dark', 'colorblind'
- **rc**: Dictionary of rc parameter mappings to override

```python
# default
sns.set_theme()
sns.set_theme(context='notebook', style='darkgrid', palette='deep', font='sans-serif', font_scale=1, color_codes=True, rc=None)

# custom example
custom_params = {"axes.spines.right": False, "axes.spines.top": False}
sns.set_theme(context='paper', style='darkgrid', palette='Pastel1', font='century gothic', rc=custom_params)
```

## Axes-level

Seaborn has two ways of functions to plot. **Figure-level** function generates `seaborn.FacetGrid` object and **Axes-level** function generate `matplotlib.pyplot.Axes` object.  
For better control, it is better to use **Axes-level** functions.  

![](/assets/images/Seaborn%20Data%20Visualization.png)

## List plots

[scatterplot](https://seaborn.pydata.org/generated/seaborn.scatterplot.html)
```python
# scatterplot
sns.scatterplot(data=df, x='sepal_length', y='sepal_width', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-1.png)

[lineplot](https://seaborn.pydata.org/generated/seaborn.lineplot.html)
```python
# lineplot
sns.lineplot(data=df, x='sepal_length', y='sepal_width', hue='species', estimator=None)
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-2.png)

## Histogram

[histplot](https://seaborn.pydata.org/generated/seaborn.histplot.html)
```python
# histplot
sns.histplot(data=df, x='sepal_length', hue='species', stat='count', bins=20, kde=True)
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-3.png)

[kdeplot](https://seaborn.pydata.org/generated/seaborn.kdeplot.html)
```python
# kdeplot
sns.kdeplot(data=df, x='sepal_length', hue='species', log_scale=(False,True))
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-4.png)

[ecdfplot](https://seaborn.pydata.org/generated/seaborn.ecdfplot.html)
```python
# ecdfplot
sns.ecdfplot(data=df, x='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-5.png)

[rugplot](https://seaborn.pydata.org/generated/seaborn.rugplot.html)
```python
# rugplot
sns.kdeplot(data=df, x='sepal_length')
sns.rugplot(data=df, x='sepal_length')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-6.png)

## Categorical plot

[stripplot](https://seaborn.pydata.org/generated/seaborn.stripplot.html)
```python
# stripplot
sns.stripplot(data=df, x='species', y='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-7.png)

[swarmplot](https://seaborn.pydata.org/generated/seaborn.swarmplot.html)
```python
# swarmplot
sns.swarmplot(data=df, x='species', y='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-8.png)

[boxplot](https://seaborn.pydata.org/generated/seaborn.boxplot.html)
```python
# boxplot
sns.boxplot(data=df, x='species', y='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-9.png)

[violinplot](https://seaborn.pydata.org/generated/seaborn.violinplot.html)
```python
# violinplot
sns.violinplot(data=df, x='species', y='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-10.png)

[barplot](https://seaborn.pydata.org/generated/seaborn.barplot.html)
```python
# barplot![](99_Attachments/sns_16_0.png)
sns.barplot(data=df, x='species', y='sepal_length', hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-11.png)
## Multiple plots in one axes

```python
# create a single grid figure using plt.subplots - default size (width, height) is 6.4 and 4.8 inches
fig, ax = plt.subplots(figsize=(4,3))

# add sns plots to the axes
sns.scatterplot(data=df, x='sepal_length', y='sepal_width', ax=ax, label='to be override')
sns.lineplot(data=df, x='sepal_length', y='sepal_width', color='r', ax=ax, label='to be override')

# add title, legend and label - will override sns plot parameters
ax.set_title('sepal_width by sepal_length', {'fontsize': 12, 'fontweight':'bold'})
ax.legend(title="Plots", labels=['scatter','line'])
ax.set_xlabel('sepal_length, cm', {'fontweight':'bold'})
ax.set_ylabel('sepal_width, cm', {'fontweight':'bold'})
# ax.set(xlabel='sepal_length, cm', ylabel='sepal_width, cm')

plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-12.png)

## Multiple plot in a figure

```python
# create a grid using plt.subplots - default size (width, height) is 6.4 and 4.8 inches
fig, ax = plt.subplots(1,4,figsize=(12,3), sharey=True)

# first plot
sns.stripplot(ax=ax[0], data=df, x='species', y='sepal_length', hue='species')
sns.violinplot(ax=ax[0], data=df, x='species', y='sepal_length', hue='species', fill=False)
ax[0].set(ylabel='cm')
ax[0].set_title('sepal_length')

# second plot
sns.scatterplot(ax=ax[1], data=df, x='sepal_length', y='petal_length', color=sns.color_palette()[5])
ax[1].legend(labels=['petal_length'])
ax[1].set(xlabel='sepal_length, cm')

# third plot
sns.scatterplot(ax=ax[2], data=df, x='petal_length', y='petal_width', color='k', alpha = 0.5, label='all species')
ax[2].legend(title='petal_width', labels=['all species'])

# fourth plot
sns.scatterplot(ax=ax[3], data=df, x='petal_length', y='petal_width', hue='species')
ax[3].set_title('petal_width')

# adjust the padding between and around subplots.
plt.tight_layout()
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-13.png)

## Matrix plot

```python
# create a grid using plt.subplots
fig, ax = plt.subplots(4,4,figsize=(10,10),sharex=True, sharey=True)

# generate matrix plot(pairplot in seaborn)
for row, col_y in enumerate(df.columns[0:4]):
    for col, col_x in enumerate(df.columns[0:4]):
        # generate legend at [0,0] plot
        if row==0 and col==0:
            sns.scatterplot(ax=ax[row,col], data=df, x=col_x, y=col_y, hue='species')
        else:
            sns.scatterplot(ax=ax[row,col], data=df, x=col_x, y=col_y, hue='species', legend=False)

        # optional location id
        ax[row,col].set_title(f"[{row},{col}]")
        # optional plot position and axis
        print(f"[{row},{col}]",f"x={col_x}", f"y={col_y}")
        
# adjust the padding between and around subplots.
plt.tight_layout()
plt.show()
```

    [0,0] x=sepal_length y=sepal_length
    [0,1] x=sepal_width y=sepal_length
    [0,2] x=petal_length y=sepal_length
    [0,3] x=petal_width y=sepal_length
    [1,0] x=sepal_length y=sepal_width
    [1,1] x=sepal_width y=sepal_width
    [1,2] x=petal_length y=sepal_width
    [1,3] x=petal_width y=sepal_width
    [2,0] x=sepal_length y=petal_length
    [2,1] x=sepal_width y=petal_length
    [2,2] x=petal_length y=petal_length
    [2,3] x=petal_width y=petal_length
    [3,0] x=sepal_length y=petal_width
    [3,1] x=sepal_width y=petal_width
    [3,2] x=petal_length y=petal_width
    [3,3] x=petal_width y=petal_width

![](/assets/images/Seaborn%20Data%20Visualization-14.png)

```python
sns.pairplot(data=df, hue='species')
plt.show()
```

![](/assets/images/Seaborn%20Data%20Visualization-15.png)

## Color palettes
There are two ways to set color palette.

```python
# set theme - default color palette is 'deep'
sns.set_theme(context='paper', style='white', palette='Set3', color_codes=True, font='century gothic')

# set color palette
sns.set_palette(palette='pastel', n_colors=None, desat=None, color_codes=False)
```

Possible palette values include:
- [Seaborn palette](https://seaborn.pydata.org/tutorial/color_palettes.html) ('deep', 'muted', 'bright', 'pastel', 'dark', 'colorblind')
- [Matplotlib colormap](https://matplotlib.org/stable/gallery/color/colormap_reference.html)
- ‘husl’ or ‘hls’

color_codes: bool
- If `True` and `palette` is a seaborn palette, remap the [shorthand color codes](https://matplotlib.org/stable/gallery/color/named_colors.html#base-colors) (e.g. “b”, “g”, “r”, etc.) to the colors from this palette.

```python
# set theme with color_code = False
sns.set_theme(palette='deep', color_codes=False)
# Current color palettes
current_palette = sns.color_palette()
sns.palplot(current_palette)
# single letter color codes stays
sns.palplot(['b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'])

```

![](/assets/images/Seaborn%20Data%20Visualization-16.png)

![](/assets/images/Seaborn%20Data%20Visualization-17.png)

```python
# set theme with color_code = True
sns.set_theme(palette='deep', color_codes=True)
# Current color palettes
current_palette = sns.color_palette()
sns.palplot(current_palette)
# single letter color codes remap
sns.palplot(['b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'])
```

![](/assets/images/Seaborn%20Data%20Visualization-18.png)

![](/assets/images/Seaborn%20Data%20Visualization-19.png)

