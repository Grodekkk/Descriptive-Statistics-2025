---
jupyter:
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 5
---

::: {#3359dc4d .cell .markdown}
# Data visualization in Python (`pyplot`)
:::

::: {#493aa2b2 .cell .markdown}
## Looking ahead: April, Weeks 1-2

-   In April, weeks 1-2, we\'ll dive deep into **data visualization**.
    -   How do we make visualizations in Python?
    -   What principles should we keep in mind?
:::

::: {#95104c93 .cell .markdown}
## Goals of this exercise

-   What *is* data visualization and why is it important?
-   Introducing `matplotlib`.
-   Univariate plot types:
    -   **Histograms** (univariate).
    -   **Scatterplots** (bivariate).
    -   **Bar plots** (bivariate).
:::

::: {#90a907b9 .cell .markdown}
## Introduction: data visualization
:::

::: {#f6b285c0 .cell .markdown}
### What is data visualization?

[Data visualization](https://en.wikipedia.org/wiki/Data_visualization)
refers to the process (and result) of representing data graphically.

For our purposes today, we\'ll be talking mostly about common methods of
**plotting** data, including:

-   Histograms\
-   Scatterplots\
-   Line plots
-   Bar plots
:::

::: {#decf9c5d .cell .markdown}
### Why is data visualization important?

-   Exploratory data analysis
-   Communicating insights
-   Impacting the world
:::

::: {#be8ed6cf .cell .markdown}
### Exploratory Data Analysis: Checking your assumptions

[Anscombe\'s
Quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)

![title](img/anscombe.png)
:::

::: {#715bf72c .cell .markdown}
### Communicating Insights

[Reference: Full Stack
Economics](https://fullstackeconomics.com/18-charts-that-explain-the-american-economy/)

![title](img/work.png)
:::

::: {#2f256b36 .cell .markdown}
### Impacting the world

[Florence
Nightingale](https://en.wikipedia.org/wiki/Florence_Nightingale)
(1820-1910) was a social reformer, statistician, and founder of modern
nursing.

![title](img/polar.jpeg)
:::

::: {#352cb9d0 .cell .markdown}
### Impacting the world (pt. 2) {#impacting-the-world-pt-2}

[John Snow](https://en.wikipedia.org/wiki/John_Snow) (1813-1858) was a
physician whose visualization of cholera outbreaks helped identify the
source and spreading mechanism (water supply).

![title](img/cholera.jpeg)
:::

::: {#97728b3d .cell .markdown}
## Introducing `matplotlib`
:::

::: {#7133db85 .cell .markdown}
### Loading packages

Here, we load the core packages we\'ll be using.

We also add some lines of code that make sure our visualizations will
plot \"inline\" with our code, and that they\'ll have nice, crisp
quality.
:::

::: {#b7669446 .cell .code}
``` python
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import scipy.stats as ss
```
:::

::: {#c4ba3d85 .cell .code}
``` python
%matplotlib inline 
%config InlineBackend.figure_format = 'retina'
```
:::

::: {#90b2a3f8 .cell .markdown}
### What is `matplotlib`?

> [`matplotlib`](https://matplotlib.org/) is a **plotting library** for
> Python.

-   Many [tutorials](https://matplotlib.org/stable/tutorials/index.html)
    available online.\
-   Also many [examples](https://matplotlib.org/stable/gallery/index) of
    `matplotlib` in use.

Note that [`seaborn`](https://seaborn.pydata.org/) (which we\'ll cover
soon) uses `matplotlib` \"under the hood\".
:::

::: {#8967f67a .cell .markdown}
### What is `pyplot`?

> [`pyplot`](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)
> is a collection of functions *within* `matplotlib` that make it really
> easy to plot data.

With `pyplot`, we can easily plot things like:

-   Histograms (`plt.hist`)
-   Scatterplots (`plt.scatter`)
-   Line plots (`plt.plot`)
-   Bar plots (`plt.bar`)
:::

::: {#123e44ca .cell .markdown}
### Example dataset

Let\'s load our familiar Pokemon dataset, which can be found in
`data/pokemon.csv`.
:::

::: {#2f8e7d3a .cell .code}
``` python
df_pokemon = pd.read_csv("data/pokemon.csv")
df_pokemon.head(10)
```

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>405</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>534</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>634</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>634</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>314</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#c2bee9eb .cell .markdown}
## Histograms
:::

::: {#6ab51c38 .cell .markdown}
### What are histograms?

> A **histogram** is a visualization of a single continuous,
> quantitative variable (e.g., income or temperature).

-   Histograms are useful for looking at how a variable
    **distributes**.\
-   Can be used to determine whether a distribution is **normal**,
    **skewed**, or **bimodal**.

A histogram is a **univariate** plot, i.e., it displays only a single
variable.
:::

::: {#fa3335fe .cell .markdown}
### Histograms in `matplotlib`

To create a histogram, call `plt.hist` with a **single column** of a
`DataFrame` (or a `numpy.ndarray`).

**Check-in**: What is this graph telling us?
:::

::: {#403ba6c0 .cell .code}
``` python
p = plt.hist(df_pokemon['Attack'])

#histograms show how often some values are occuring in dataset, in this example how pokemon attack statistic is distributed
#we see that most of pokemons have atk stat between 50 and 100, and very few of them less than 25 and even less have more than 175
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/c6d1a408be56fba6b567467e1d86dc8c1e3cbee0.png)
:::
:::

::: {#93af995b .cell .markdown}
#### Changing the number of bins

A histogram puts your continuous data into **bins** (e.g., 1-10, 11-20,
etc.).

-   The height of each bin reflects the number of observations within
    that interval.\
-   Increasing or decreasing the number of bins gives you more or less
    granularity in your distribution.
:::

::: {#afa8db7e .cell .code}
``` python
### This has lots of bins
p = plt.hist(df_pokemon['Attack'], bins = 30)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/7d43aada9732ddcaad4b5b08b95edf51a3ea96d6.png)
:::
:::

::: {#6d419dbc .cell .code}
``` python
### This has fewer bins
p = plt.hist(df_pokemon['Attack'], bins = 5)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/768ca3deceabcdc78b01fb01c28fb1f5e257a6ce.png)
:::
:::

::: {#4c7896bf .cell .markdown}
#### Changing the `alpha` level

The `alpha` level changes the **transparency** of your figure.
:::

::: {#f010d5bf .cell .code}
``` python
### This has fewer bins
p = plt.hist(df_pokemon['Attack'], alpha = .6)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/da199d3b86f076a5828af54bf98b7c3e4519e3c0.png)
:::
:::

::: {#4718c6cf .cell .markdown}
#### Check-in:

How would you make a histogram of the scores for `Defense`?
:::

::: {#b6c13c35 .cell .code}
``` python
### Your code here
p = plt.hist(df_pokemon['Defense'], bins = 30, alpha = 0.8)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/f5ee4925f195ccb2590439953c3a49a4c5d39f8b.png)
:::
:::

::: {#bc47549d .cell .markdown}
#### Check-in: {#check-in}

Could you make a histogram of the scores for `Type 1`?
:::

::: {#9d110b61 .cell .code}
``` python
### Your code here
#get counts of each type and do barplot of it
df_pokemon['Type 1'].value_counts().plot(kind='bar', alpha=0.8)
```

::: {.output .display_data}
    <Axes: xlabel='Type 1'>
:::

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/fd99ab0fa003e6965aa33a6379bdc07ee067ac1d.png)
:::
:::

::: {#e626ac25 .cell .markdown}
### Learning from histograms

Histograms are incredibly useful for learning about the **shape** of our
distribution. We can ask questions like:

-   Is this distribution relatively
    [normal](https://en.wikipedia.org/wiki/Normal_distribution)?
-   Is the distribution
    [skewed](https://en.wikipedia.org/wiki/Skewness)?
-   Are there [outliers](https://en.wikipedia.org/wiki/Outlier)?
:::

::: {#a0b905e1 .cell .markdown}
#### Normally distributed data

We can use the `numpy.random.normal` function to create a **normal
distribution**, then plot it.

A normal distribution has the following characteristics:

-   Classic \"bell\" shape (**symmetric**).\
-   Mean, median, and mode are all identical.
:::

::: {#331ffb62 .cell .code}
``` python
norm = np.random.normal(loc = 10, scale = 1, size = 1000)
p = plt.hist(norm, alpha = .6)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/e100d1e06e7036c185bc615e8c130280c7bd64cf.png)
:::
:::

::: {#17e9ed65 .cell .markdown}
#### Skewed data

> **Skew** means there are values *elongating* one of the \"tails\" of a
> distribution.

-   Positive/right skew: the tail is pointing to the right.\
-   Negative/left skew: the tail is pointing to the left.
:::

::: {#3c04f3c1 .cell .code}
``` python
rskew = ss.skewnorm.rvs(20, size = 1000) # make right-skewed data
lskew = ss.skewnorm.rvs(-20, size = 1000) # make left-skewed data
fig, axes = plt.subplots(1, 2)
axes[0].hist(rskew)
axes[0].set_title("Right-skewed")
axes[1].hist(lskew)
axes[1].set_title("Left-skewed")
```

::: {.output .display_data}
    Text(0.5, 1.0, 'Left-skewed')
:::

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/9f266a19618a0f96c72dc615aaafa6ce0cf81813.png)
:::
:::

::: {#12bef073 .cell .markdown}
#### Outliers

> **Outliers** are data points that differ significantly from other
> points in a distribution.

-   Unlike skewed data, outliers are generally **discontinuous** with
    the rest of the distribution.
-   Next week, we\'ll talk about more ways to **identify** outliers; for
    now, we can rely on histograms.
:::

::: {#3937ac58 .cell .code}
``` python
norm = np.random.normal(loc = 10, scale = 1, size = 1000)
upper_outliers = np.array([21, 21, 21, 21]) ## some random outliers
data = np.concatenate((norm, upper_outliers))
p = plt.hist(data, alpha = .6)
plt.arrow(20, 100, dx = 0, dy = -50, width = .3, head_length = 10, facecolor = "red");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/7ceaea4cccde5fe85306cd7939612f9ed20e60b6.png)
:::
:::

::: {#cdbe0c05 .cell .markdown}
#### Check-in {#check-in}

How would you describe the following distribution?

-   Normal vs. skewed?\
-   With or without outliers?
:::

::: {#d71b9eac .cell .code}
``` python
#im guessing we're talking about upper distribution, then it has outlier, there is value 20 much bigger than all of data, and there is no 
# values between 14-20

#distribution is skewed because it doesnt follow normal distribution pattern
```
:::

::: {#c56cccb1 .cell .markdown}
#### Check-in {#check-in}

In a somewhat **right-skewed distribution** (like below), what\'s
larger----the `mean` or the `median`?
:::

::: {#4258e674 .cell .code}
``` python
mean1=np.mean(data)
median1=np.median(data)
print(mean1)
print(median1)

#mean is slightly bigger, but difference is small
```

::: {.output .stream .stdout}
    10.154714535915247
    10.08105391070858
:::
:::

::: {#5ce387eb .cell .markdown}
### Modifying our plot

-   A good data visualization should also make it *clear* what\'s being
    plotted.
    -   Clearly labeled `x` and `y` axes, title.
-   Sometimes, we may also want to add **overlays**.
    -   E.g., a dashed vertical line representing the `mean`.
:::

::: {#e8a17923 .cell .markdown}
#### Adding axis labels
:::

::: {#4b488eaa .cell .code}
``` python
p = plt.hist(df_pokemon['Attack'], alpha = .6)
plt.xlabel("Attack")
plt.ylabel("Count")
plt.title("Distribution of Attack Scores");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/d9e6f61a2ed9e77c8b4afabc55ee77606eaf78b2.png)
:::
:::

::: {#ca982ace .cell .markdown}
#### Adding a vertical line

The `plt.axvline` function allows us to draw a vertical line at a
particular position, e.g., the `mean` of the `Attack` column.
:::

::: {#fc8013c1 .cell .code}
``` python
p = plt.hist(df_pokemon['Attack'], alpha = .6)
plt.xlabel("Attack")
plt.ylabel("Count")
plt.title("Distribution of Attack Scores")
plt.axvline(df_pokemon['Attack'].mean(), linestyle = "dotted");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/ab32d993f0c5404096d76ae1dd25cac0c6d0f0d5.png)
:::
:::

::: {#283eaaae .cell .markdown}
## Faceting for histograms
:::

::: {#f7675978 .cell .markdown}
Let\'s try to group by our no. of Attacks by Pokemon Types looking at
many histograms at a time:
:::

::: {#fd514671 .cell .code}
``` python
import plotly.express as px
fig = px.histogram(df_pokemon,x='Attack', color="Legendary", facet_col='Generation')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=1<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":true,"type":"histogram","x":{"bdata":"MQA+AFIAZAA0AEAAVACCAGgAMAA/AFMAZwAeABQALQAjABkAWgCWAC0APABQAFAAOABRADwAWgA8AFUANwBaAEsAZAAvAD4AXAA5AEgAZgAtAEYAKQBMAC0ARgAtAFAAMgBBAFAARgBfADcAQQA3AFAALQBGADQAUgBQAGkARgBuADIAQQBfABQAIwAyADIAUABkAIIASwBaAGkAKABGAFAAXwB4AFUAZABBAEsASwAjADwAQQBVAG4ALQBGAFAAaQBBAF8AIwAyAEEAQQAtADAASQBpAIIAHgAyACgAXwAyAFAAeABpADcAQQBaAFUAggAFADcAXwB9ACgAQQBDAFwALQBLAC0AbgAyAFMAXwB9AJsAZAAKAH0AmwBVADAANwBBAEEAggA8ACgAPABQAHMAaQCHAG4AQABUAIYAZAA=","dtype":"i2"},"xaxis":"x","yaxis":"y"},{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=2<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"MQA+AFIANABAAFQAQQBQAGkALgBMAB4AMgAUACMAPABaAFoAJgA6ACgAGQAeABQAKAAyAEsAKAA3AEsAXwBQABQAMgBkAEsAIwAtADcARgAeAEsAQQAtAFUAQQBBAFUASwA8AEgAIQBQAEEAWgBGAEsAVQB9AFAAeABfAIIAlgAKAH0AuQBfAFAAggAoADIAMgBkADcAQQBpADcAKABQADwAWgBaAF8APAB4AFAAXwAUACMAXwAeAD8ASwBQAAoAQABUAIYApABkAA==","dtype":"i2"},"xaxis":"x2","yaxis":"y2"},{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=3<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"LQBBAFUAbgA8AFUAeACgAEYAVQBuAJYANwBaAB4ARgAtACMARgAjADIAHgAyAEYAKABGAGQANwBVAB4AMgAZACMAQQBVAB4APAAoAIIAPABQAKAALQBaAFoAMwBHAFsAPAB4ABQALQAtAEEASwBVAFUAaQBGAFoAbgCMACgAPABkAC0ASwBLADIAKABJAC8APAArAEkAWgB4AIwARgBaADwAZAB4AFUAGQAtADwAZABGAGQAVQBzACgARgBuAHMAZAA3AF8AMABOAFAAeAAoAEYAKQBRAF8AfQAPADwARgBaAEsAcwClACgARgBEADIAggCWABcAMgBQAHgAKAA8AFAAQABoAFQAWgAeAEsAXwCHAJEANwBLAIcAkQA=","dtype":"i2"},"xaxis":"x3","yaxis":"y3"},{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=4<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"RABZAG0AOgBOAGgAMwBCAFYANwBLAHgALQBVABkAVQBBAFUAeAAeAEYAfQClACoANAAdADsATwBFAF4AHgBQAC0AQQBpACMAPAAwAFMAZAAyAFAAQgBMAIgAPAB9ADcAUgAeAD8AXQAYAFkAUAAZAAUAQQBcAEYAWgCCAKoAVQBGAG4AkQBIAHAAMgBaAD0AagBkADEARQAUAD4AXACEAHgARgBVAIwAZAB7AF8AMgBMAG4APABfAIIAUAB9AKUANwBkAFAAMgBBAEEAQQBBAEEARgBQAGQA","dtype":"i2"},"xaxis":"x4","yaxis":"y4"},{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=5<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"LQA8AEsAPwBdAHsANwBLAGQANwBVADwAUABuADIAWAA1AGIANQBiADUAYgAZADcANwBNAHMAPABkAEsAaQCHAC0AOQBVAIcAPAA8AFAAaQCMADIAQQBfAGQAfQA1AD8AZwAtADcAZAAbAEMAIwA8AFwASABSAHUAWgCMAB4AVgBBAF8ASwBaADoAHgAyAE4AbABwAIwAMgBfAEEAaQAyAF8AHgAtADcAHgAoAEEALABXADIAQQBfADwAZABLAEsAhwA3AFUAKAA8AEsALwBNADIAXgA3AFAAZAA3AFUAcwA3AEsAHgAoADcAVwB1AJMARgBuADIAKABGAEIAVQB9AHgASgB8AFUAfQBuAFMAewA3AEEAYQBtAEEAVQBpAFUAPABIAEgATQCAAHgA","dtype":"i2"},"xaxis":"x5","yaxis":"y5"},{"bingroup":"x","hovertemplate":"Legendary=False<br>Generation=6<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"False","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"False","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"PQBOAGsALQA7AEUAOAA/AF8AJAA4ADIASQBRACMAFgA0ADIARAAmAC0AQQBBAGQAUgB8AFAAMAAwADAAUABuAJYAMgA0AEgAMABQADYAXAA0AGkAPABLADUASQAmADcAWQB5ADsATQBBAFwAOgAyADIASwBkAFAARgBuAEIAQgBCAEIAWgBVAF8AZABFAHUAHgBGAA==","dtype":"i2"},"xaxis":"x6","yaxis":"y6"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=1<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":true,"type":"histogram","x":{"bdata":"VQBaAGQAbgC+AJYA","dtype":"i2"},"xaxis":"x","yaxis":"y"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=2<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"VQBzAEsAWgCCAA==","dtype":"i2"},"xaxis":"x2","yaxis":"y2"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=3<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"ZAAyAEsAUABkAFoAggBkAJYAlgC0AJYAtABkAJYAtABGAF8A","dtype":"i2"},"xaxis":"x3","yaxis":"y3"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=4<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"SwBpAH0AeAB4AFoAoABkAHgAWgBkAGcAeAA=","dtype":"i2"},"xaxis":"x4","yaxis":"y4"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=5<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"ZABaAIEAWgBzAGQAcwBpAHgAlgB9AJEAggCqAHgA","dtype":"i2"},"xaxis":"x5","yaxis":"y5"},{"bingroup":"x","hovertemplate":"Legendary=True<br>Generation=6<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"True","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"True","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"gwCDAGQAZACgAG4AoABuAA==","dtype":"i2"},"xaxis":"x6","yaxis":"y6"}],"layout":{"annotations":[{"font":{},"showarrow":false,"text":"Generation=1","x":7.5e-2,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=2","x":0.24499999999999997,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=3","x":0.415,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=4","x":0.585,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=5","x":0.7549999999999999,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=6","x":0.925,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"}],"barmode":"relative","legend":{"title":{"text":"Legendary"},"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,0.15],"title":{"text":"Attack"}},"xaxis2":{"anchor":"y2","domain":[0.16999999999999998,0.31999999999999995],"matches":"x","title":{"text":"Attack"}},"xaxis3":{"anchor":"y3","domain":[0.33999999999999997,0.49],"matches":"x","title":{"text":"Attack"}},"xaxis4":{"anchor":"y4","domain":[0.51,0.66],"matches":"x","title":{"text":"Attack"}},"xaxis5":{"anchor":"y5","domain":[0.6799999999999999,0.83],"matches":"x","title":{"text":"Attack"}},"xaxis6":{"anchor":"y6","domain":[0.85,1],"matches":"x","title":{"text":"Attack"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"count"}},"yaxis2":{"anchor":"x2","domain":[0,1],"matches":"y","showticklabels":false},"yaxis3":{"anchor":"x3","domain":[0,1],"matches":"y","showticklabels":false},"yaxis4":{"anchor":"x4","domain":[0,1],"matches":"y","showticklabels":false},"yaxis5":{"anchor":"x5","domain":[0,1],"matches":"y","showticklabels":false},"yaxis6":{"anchor":"x6","domain":[0,1],"matches":"y","showticklabels":false}}}
```
:::
:::

::: {#9f8bce26 .cell .markdown}
## Scatterplots
:::

::: {#db6ebae0 .cell .markdown}
### What are scatterplots?

> A **scatterplot** is a visualization of how two different continuous
> distributions relate to each other.

-   Each individual point represents an observation.
-   Very useful for **exploratory data analysis**.
    -   Are these variables positively or negatively correlated?

A scatterplot is a **bivariate** plot, i.e., it displays at least two
variables.
:::

::: {#a51b8245 .cell .markdown}
### Scatterplots with `matplotlib`

We can create a scatterplot using `plt.scatter(x, y)`, where `x` and `y`
are the two variables we want to visualize.
:::

::: {#e39d3b6e .cell .code}
``` python
x = np.arange(1, 10)
y = np.arange(11, 20)
p = plt.scatter(x, y)
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/b461d74ab52494c5002552d4df61eb8e4e6d6b47.png)
:::
:::

::: {#914ce21b .cell .markdown}
#### Check-in {#check-in}

Are these variables related? If so, how?
:::

::: {#1344c5b4 .cell .code}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = x * 2 + np.random.normal(loc = 0, scale = 2, size = 100)
plt.scatter(x, y, alpha = .6);

#yes, I think they are related. we can obserwe that as x increases, y value increases also
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/7778ac5b4d2dcb8cb79d8e450237072604d02934.png)
:::
:::

::: {#dc6220ad .cell .markdown}
#### Check-in {#check-in}

Are these variables related? If so, how?
:::

::: {#f61c92b0 .cell .code}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = -x * 2 + np.random.normal(loc = 0, scale = 2, size = 100)
plt.scatter(x, y, alpha = .6);

#yes It's simmilar case but this time they are decreasing
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/a452388bf2537b7bc1d09013ab9c2d8095088096.png)
:::
:::

::: {#6f93979f .cell .markdown}
#### Scatterplots are useful for detecting non-linear relationships
:::

::: {#a40d5ef3 .cell .code}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = np.sin(x)
plt.scatter(x, y, alpha = .6);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/d6f530c54514f7df2172f2e5e15d4c384fff4703.png)
:::
:::

::: {#b149414e .cell .markdown}
#### Check-in {#check-in}

How would we visualize the relationship between `Attack` and `Speed` in
our Pokemon dataset?
:::

::: {#b5351725 .cell .code}
``` python
x = df_pokemon["Attack"]
y = df_pokemon["Speed"]
plt.scatter(x, y,  alpha = .7);
plt.title('Relationship between Attack and Speed, each dot is pokemon')
plt.xlabel("Attack")
plt.ylabel("Speed")
plt.axvline(df_pokemon['Attack'].mean(), linestyle = "dotted");
plt.axhline(df_pokemon['Speed'].mean(), linestyle = "dotted");
plt.show()

```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/416d13db7e8b0a42352c350e17d1140fffbe5d7f.png)
:::
:::

::: {#e00dcff6 .cell .markdown}
## Scatterplots with `pyplot express`
:::

::: {#f881f378 .cell .markdown}
With pyplot express we can play with scatterplots even further - we can
create `bubble plots`!
:::

::: {#07325f96 .cell .code}
``` python
import plotly.express as px
bubble=px.scatter(df_pokemon, x='Attack', y='Speed', color='Generation', size='HP');
bubble.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<br>Generation=%{marker.color}<extra></extra>","legendgroup":"","marker":{"color":{"bdata":"AQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgY=","dtype":"i1"},"coloraxis":"coloraxis","size":{"bdata":"LQA8AFAAUAAnADoATgBOAE4ALAA7AE8ATwAtADIAPAAoAC0AQQBBACgAPwBTAFMAHgA3ACgAQQAjADwAIwA8ADIASwA3AEYAWgAuAD0AUQBGAF8AJgBJAHMAjAAoAEsALQA8AEsAIwA8ADwARgAKACMAKABBADIAUAAoAEEANwBaACgAQQBaABkAKAA3ADcARgBQAFoAMgBBAFAAKABQACgANwBQADIAQQBaAF8AXwAZADIANAAjADwAQQBaAFAAaQAeADIAHgAtADwAPAAjADwAVQAeADcAKAA8ADwAXwAyADwAMgAyAFoAKABBAFAAaQD6AEEAaQBpAB4ANwAtAFAAHgA8ACgARgBBAEEAQQBBAEEASwAUAF8AXwCCADAANwCCAEEAQQBBACMARgAeADwAUABQAKAAWgBaAFoAKQA9AFsAagBqAGoAZAAtADwAUAAnADoATgAyAEEAVQAjAFUAPABkACgANwAoAEYAVQBLAH0AFAAyAFoAIwA3ACgAQQA3AEYAWgBaAEsARgBkAEYAWgAjADcASwA3AB4ASwBBADcAXwBBAF8APABfADwAMAC+AEYAMgBLAGQAQQBLAEsAPABaAEEARgBGABQAUABQADcAPABaACgAMgAyAGQANwAjAEsALQBBAEEALQBLAEsASwBaAFoAVQBJADcAIwAyAC0ALQAtAF8A/wBaAHMAZAAyAEYAZABkAGoAagBkACgAMgBGAEYALQA8AFAAUAAyAEYAZABkACMARgAmAE4ALQAyADwAMgA8ACgAPABQACgARgBaACgAPAAoADwAHAAmAEQARAAoAEYAPAA8ADwAUACWAB8APQABAEAAVABoAEgAkAAyAB4AMgBGADIAMgAyADIAMgA8AEYARgAeADwAPAAoAEYARgA8ADwAQQBBADIARgBkAC0ARgBGAIIAqgA8AEYARgBGADwAUAA8AC0AMgBQADIARgAtAEsASwBJAEkARgBGADIAbgArAD8AKAA8AEIAVgAtAEsAFABfAEYAPAAsAEAAQAAUACgAYwBBAEEAQQBfADIAUABQAEYAWgBuACMANwA3AGQAKwAtAEEAXwBfACgAPABQAFAAUABQAFAAUABQAFAAUABkAGQAZABkAGkAaQBkADIAMgAyADIANwBLAF8ALABAAEwANQBAAFQAKAA3AFUAOwBPACUATQAtADwAUAAoADwAQwBhAB4APAAoADwAPAA8AEYAHgBGADwANwBVAC0ARgBMAG8ASwBaAJYANwBBAEEAPABkADEARwAtAD8AZwA5AEMAMgAUAGQATAAyADoARABsAGwAhwAoAEYARgBEAGwAKABGADAAUwBKADEARQAtADwAWgBaAEYARgBuAHMAZABLAEsAVQBWAEEAQQBLAG4AVQBEAEQAPAAtAEYAMgAyADIAMgAyADIASwBQAEsAZABaAFsAbgCWAJYAeABQAGQARgBkAGQAeABkAC0APABLAEEAWgBuADcASwBfAC0APAAtAEEAVQApAEAAMgBLADIASwAyAEsATAB0ADIAPgBQAC0ASwA3AEYAVQA3AEMAPABuAGcAZwBLAFUAaQAyAEsAaQB4AEsALQA3AEsAHgAoADwAKAA8AC0ARgBGADIAPABfAEYAaQBpAEsAMgBGADIAQQBIACYAOgA2AEoANwBLADIAUAAoADwANwBLAC0APABGAC0AQQBuAD4ASwAkADMARwA8AFAANwAyAEYARQByADcAZAClADIARgAsAEoAKAA8ADwAIwBBAFUANwBLADIAPAA8AC4AQgBMADcAXwBGADIAUABtAC0AQQBNADsAWQAtAEEAXwBGAGQARgBuAFUAOgA0AEgAXAA3AFUAWwBbAFsATwBPAE8ATwBkAGQAWQBZAH0AfQB9AFsAWwBkAGQARwA4AD0AWAAoADsASwApADYASAAmAFUALQA+AE4AJgAtAFAAPgBWACwANgBOAEIAewBDAF8ASwA+AEoASgAtADsAPAA8AE4AZQA+AFIANQBWACoASAAyAEEAMgBHACwAPgA6AFIATQB7AF8ATgBDADIALQBEAFoAOQArAFUAMQAsADYAOwBBADcASwBVADcAXwAoAFUAfgB+AGwAMgAyAFAAUABQAA==","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"","orientation":"v","showlegend":false,"type":"scatter","x":{"bdata":"MQA+AFIAZAA0AEAAVACCAGgAMAA/AFMAZwAeABQALQAjABkAWgCWAC0APABQAFAAOABRADwAWgA8AFUANwBaAEsAZAAvAD4AXAA5AEgAZgAtAEYAKQBMAC0ARgAtAFAAMgBBAFAARgBfADcAQQA3AFAALQBGADQAUgBQAGkARgBuADIAQQBfABQAIwAyADIAUABkAIIASwBaAGkAKABGAFAAXwB4AFUAZABBAEsASwAjADwAQQBVAG4ALQBGAFAAaQBBAF8AIwAyAEEAQQAtADAASQBpAIIAHgAyACgAXwAyAFAAeABpADcAQQBaAFUAggAFADcAXwB9ACgAQQBDAFwALQBLAC0AbgAyAFMAXwB9AJsAZAAKAH0AmwBVADAANwBBAEEAggA8ACgAPABQAHMAaQCHAG4AVQBaAGQAQABUAIYAbgC+AJYAZAAxAD4AUgA0AEAAVABBAFAAaQAuAEwAHgAyABQAIwA8AFoAWgAmADoAKAAZAB4AFAAoADIASwAoADcASwBfAFAAFAAyAGQASwAjAC0ANwBGAB4ASwBBAC0AVQBBAEEAVQBLADwASAAhAFAAQQBaAEYASwBVAH0AUAB4AF8AggCWAAoAfQC5AF8AUACCACgAMgAyAGQANwBBAGkANwAoAFAAPABaAFoAXwA8AHgAUABfABQAIwBfAB4APwBLAFAACgBVAHMASwBAAFQAhgCkAFoAggBkAC0AQQBVAG4APABVAHgAoABGAFUAbgCWADcAWgAeAEYALQAjAEYAIwAyAB4AMgBGACgARgBkADcAVQAeADIAGQAjAEEAVQAeADwAKACCADwAUACgAC0AWgBaADMARwBbADwAeAAUAC0ALQBBAEsAVQBVAGkARgBaAG4AjAAoADwAZAAtAEsASwAyACgASQAvADwAKwBJAFoAeACMAEYAWgA8AGQAeABVABkALQA8AGQARgBkAFUAcwAoAEYAbgBzAGQANwBfADAATgBQAHgAKABGACkAUQBfAH0ADwA8AEYAWgBLAHMApQAoAEYARAAyAIIAlgAXADIAUAB4ACgAPABQAEAAaABUAFoAHgBLAF8AhwCRADcASwCHAJEAZAAyAEsAUABkAFoAggBkAJYAlgC0AJYAtABkAJYAtABGAF8ARABZAG0AOgBOAGgAMwBCAFYANwBLAHgALQBVABkAVQBBAFUAeAAeAEYAfQClACoANAAdADsATwBFAF4AHgBQAC0AQQBpACMAPAAwAFMAZAAyAFAAQgBMAIgAPAB9ADcAUgAeAD8AXQAYAFkAUAAZAAUAQQBcAEYAWgCCAKoAVQBGAG4AkQBIAHAAMgBaAD0AagBkADEARQAUAD4AXACEAHgARgBVAIwAZAB7AF8AMgBMAG4APABfAIIAUAB9AKUANwBkAFAAMgBBAEEAQQBBAEEASwBpAH0AeAB4AFoAoABkAHgARgBQAGQAWgBkAGcAeABkAC0APABLAD8AXQB7ADcASwBkADcAVQA8AFAAbgAyAFgANQBiADUAYgA1AGIAGQA3ADcATQBzADwAZABLAGkAhwAtADkAVQCHADwAPABQAGkAjAAyAEEAXwBkAH0ANQA/AGcALQA3AGQAGwBDACMAPABcAEgAUgB1AFoAjAAeAFYAQQBfAEsAWgA6AB4AMgBOAGwAcACMADIAXwBBAGkAMgBfAB4ALQA3AB4AKABBACwAVwAyAEEAXwA8AGQASwBLAIcANwBVACgAPABLAC8ATQAyAF4ANwBQAGQANwBVAHMANwBLAB4AKAA3AFcAdQCTAEYAbgAyACgARgBCAFUAfQB4AEoAfABVAH0AbgBTAHsANwBBAGEAbQBBAFUAaQBVADwAWgCBAFoAcwBkAHMAaQB4AJYAfQCRAIIAqgB4AEgASABNAIAAeAA9AE4AawAtADsARQA4AD8AXwAkADgAMgBJAFEAIwAWADQAMgBEACYALQBBAEEAZABSAHwAUAAwADAAMABQAG4AlgAyADQASAAwAFAANgBcADQAaQA8AEsANQBJACYANwBZAHkAOwBNAEEAXAA6ADIAMgBLAGQAUABGAG4AQgBCAEIAQgBaAFUAXwBkAEUAdQAeAEYAgwCDAGQAZACgAG4AoABuAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"LQA8AFAAUABBAFAAZABkAGQAKwA6AE4ATgAtAB4ARgAyACMASwCRADgARwBlAHkASABhAEYAZAA3AFAAWgBuACgAQQApADgATAAyAEEAVQAjADwAQQBkABQALQA3AFoAHgAoADIAGQAeAC0AWgBfAHgAWgBzADcAVQBGAF8APABfAFoAWgBGAFoAaQB4AJYAIwAtADcAKAA3AEYARgBkABQAIwAtAFoAaQAPAB4AHgAtAEYAPABLAGQALQBGABkAMgAoAEYAUABfAG4AggBGACoAQwAyAEsAZACMACgANwAjAC0AVwBMAB4AIwA8ABkAKAAyADwAWgBkADwAVQA/AEQAVQBzAFoAaQBfAGkAXQBVAGkAbgBQAFEAUQA8ADAANwBBAIIAQQAoACMANwA3AFAAggCWAB4AVQBkAFoAMgBGAFAAggCCAIwAZAAtADwAUABBAFAAZAArADoATgAUAFoAMgBGADcAVQAeACgAggBDAEMAPAAPAA8AFAAoAEYAXwAjAC0ANwAtADIAKAAyAB4ARgAyAFAAbgBVAB4AHgBfAA8AIwBuAEEAWwAeAFUAMAAhAFUADwAoAC0AVQAeAB4AHgAtAFUAQQBLAAUAVQBLAHMAKAA3ABQAHgAyADIAIwBBAC0ASwBGAEYAQQBfAHMAVQAoADIAPABVAEsAIwBGAEEAXwBTAGQANwBzAGQAVQApADMAPQBHAG4AWgBkAEYAXwB4AJEALQA3AFAAZAAoADIAPABGACMARgA8AGQAFAAPAEEADwBBAB4AMgBGAB4APABQAFUAfQBVAEEAKAAyAFAAZABBADwAIwBGAB4AWgBkACgAoAAoABwAMABEABkAMgAUAB4AMgBGADIAFAAyADIAHgAoADIAMgA8AFAAZABBAGkAhwBfAF8AVQBVAEEAKAA3AEEAXwBpADwAPAAjACgAFAAUADwAUAA8AAoARgBkACMANwAyAFAAUABaAEEARgBGADwAPAAjADcANwBLABcAKwBLAC0AUABRAEYAKAAtAEEASwAZABkAMwBBAEsAcwAXADIAUABkABkALQBBACAANAA0ADcAYQAyADIAZAB4AB4AMgBGAG4AMgAyADIAbgBuAG4AbgBaAFoAWgBaAF8AcwBkAJYAlgBaALQAHwAkADgAPQBRAGwAKAAyADwAPABQAGQAHwBHABkAQQAtADwARgA3AFoAOgA6AB4AHgAkACQAJAAkAEIARgAoAF8AVQBzACMAVQAiACcAcwBGAFAAVQBpAIcAaQBHAFUAcAAtAEoAVAAXACEACgA8AB4AWwAjACoAUgBmAFwABQA8AFoAcAAgAC8AQQBfADIAVQAuAEIAWwAyACgAPAAeAH0APAAyACgAMgBfAFMAUABfAF8AQQBfAFAAWgBQAG4AKAAtAG4AWwBWAFYAVgBWAFYAXwBQAHMAWgBkAE0AZABaAFoAVQBQAGQAfQBkAH8AeABkAD8AUwBxAC0ANwBBAC0APABGACoATQA3ADwAUABCAGoAQABlAEAAZQBAAGUAGAAdACsAQQBdAEwAdAAPABQAGQBIAHIARABYADIAMgAjACgALQBAAEUASgAtAFUAKgAqAFwAOQAvAHAAQgB0AB4AWgBiAEEASgBcADIAXwA3ADwANwAtADAAOgBhAB4AHgAWACAARgBuAEEASwBBAGkASwBzAC0ANwBBABQAHgAeADcAYgAsADsATwBLAF8AZwA8ABQADwAeACgAPABBAEEAbAAKABQAHgAyAFoAPAAoADIAHgAoABQANwBQADkAQwBhACgAMgBpABkAkQAgAEEAaQAwACMANwA8AEYANwA8AFAAPABQAEEAbQAmADoAYgA8AGQAbABsAGwAbwB5AG8AZQBaAFoAZQBbAF8AXwBfAGwAbABaAIAAYwAmADkAQAA8AEkAaABHAGEAegA5AE4APgBUAH4AIwAdAFkASABqACoANABLADQARAArADoAZgBEAGgAaAAcACMAPAA8ABcAHQAxAEgALQBJADIARAAeACwALAA7AEYAbQAwAEcALgA6ADwAdgBlADIAKAA8AFAASwAmADgAMwA4AC4AKQBUAGMARQA2ABwAHAA3AHsAYwBjAF8AMgBuAEYAUABGAA==","dtype":"i2"},"yaxis":"y"}],"layout":{"coloraxis":{"colorbar":{"title":{"text":"Generation"}},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"legend":{"itemsizing":"constant","tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Attack"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Speed"}}}}
```
:::
:::

::: {#15cbf769 .cell .markdown}
## Barplots
:::

::: {#99fac95b .cell .markdown}
### What is a barplot?

> A **barplot** visualizes the relationship between one *continuous*
> variable and a *categorical* variable.

-   The *height* of each bar generally indicates the mean of the
    continuous variable.
-   Each bar represents a different *level* of the categorical variable.

A barplot is a **bivariate** plot, i.e., it displays at least two
variables.
:::

::: {#7bc3d8c1 .cell .markdown}
### Barplots with `matplotlib`

`plt.bar` can be used to create a **barplot** of our data.

-   E.g., average `Attack` by `Legendary` status.
-   However, we first need to use `groupby` to calculate the mean
    `Attack` per level.
:::

::: {#6f9bc2a1 .cell .markdown}
#### Step 1: Using `groupby`
:::

::: {#90845f24 .cell .code}
``` python
summary = df_pokemon[['Legendary', 'Attack']].groupby("Legendary").mean().reset_index()
summary
```

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Legendary</th>
      <th>Attack</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>75.669388</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>116.676923</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#2532e0a4 .cell .code}
``` python
### Turn Legendary into a str
summary['Legendary'] = summary['Legendary'].apply(lambda x: str(x))
summary
```

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Legendary</th>
      <th>Attack</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>75.669388</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>116.676923</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#c1aaac87 .cell .markdown}
#### Step 2: Pass values into `plt.bar` {#step-2-pass-values-into-pltbar}

**Check-in**:

-   What do we learn from this plot?\
-   What is this plot missing?
:::

::: {#e6b03730 .cell .code}
``` python
plt.bar(x = summary['Legendary'],height = summary['Attack'],alpha = .6);
plt.xlabel("Legendary status");
plt.ylabel("Attack");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/be1628ee1d8f6a28c9a0a3f9a779ba7b6ad84154.png)
:::
:::

::: {#288e6096 .cell .markdown}
## Barplots in `plotly.express` {#barplots-in-plotlyexpress}
:::

::: {#30a16f8b .cell .code}
``` python
import plotly.express as px
data_canada = px.data.gapminder().query("country == 'Canada'")
fig = px.bar(data_canada, x='year', y='pop')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"year=%{x}<br>pop=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":{"bdata":"oAelB6oHrwe0B7kHvgfDB8gHzQfSB9cH","dtype":"i2"},"xaxis":"x","y":{"bdata":"MJzhAOqNAwF5syEBN689AdQIVAGwGmsB7IyAAcQdlQHuO7MBM27OATzK5gE9fv0B","dtype":"i4"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"pop"}}}}
```
:::
:::

::: {#37062b25 .cell .code}
``` python
data_canada.head(3)
```

::: {.output .display_data}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"country","rawType":"object","type":"string"},{"name":"continent","rawType":"object","type":"string"},{"name":"year","rawType":"int64","type":"integer"},{"name":"lifeExp","rawType":"float64","type":"float"},{"name":"pop","rawType":"int64","type":"integer"},{"name":"gdpPercap","rawType":"float64","type":"float"},{"name":"iso_alpha","rawType":"object","type":"string"},{"name":"iso_num","rawType":"int64","type":"integer"}],"conversionMethod":"pd.DataFrame","ref":"e76665fe-6095-4c4f-9e10-4f4a70e23cbe","rows":[["240","Canada","Americas","1952","68.75","14785584","11367.16112","CAN","124"],["241","Canada","Americas","1957","69.96","17010154","12489.95006","CAN","124"],["242","Canada","Americas","1962","71.3","18985849","13462.48555","CAN","124"]],"shape":{"columns":8,"rows":3}}
```
:::
:::

::: {#d890c8bf .cell .code}
``` python
long_df = px.data.medals_long()

fig = px.bar(long_df, x="nation", y="count", color="medal", title="Long format of data")
fig.show()

long_df.head(3)
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"medal=gold<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"gold","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"gold","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"GAoJ","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"medal=silver<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"silver","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"silver","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"DQ8M","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"medal=bronze<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"bronze","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"bronze","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"CwgM","dtype":"i1"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"medal"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Long format of data"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"nation"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"count"}}}}
```
:::

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>nation</th>
      <th>medal</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>South Korea</td>
      <td>gold</td>
      <td>24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>China</td>
      <td>gold</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Canada</td>
      <td>gold</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#1519cb26 .cell .code}
``` python
wide_df = px.data.medals_wide()

fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide format of data")
fig.show()

wide_df.head(3)
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"variable=gold<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"gold","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"gold","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"GAoJ","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"variable=silver<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"silver","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"silver","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"DQ8M","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"variable=bronze<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"bronze","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"bronze","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"CwgM","dtype":"i1"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"variable"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Wide format of data"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"nation"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"value"}}}}
```
:::

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>nation</th>
      <th>gold</th>
      <th>silver</th>
      <th>bronze</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>South Korea</td>
      <td>24</td>
      <td>13</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>China</td>
      <td>10</td>
      <td>15</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Canada</td>
      <td>9</td>
      <td>12</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#d503f844 .cell .markdown}
## Faceting barplots

Please use faceting for the Pokemon data with barplots:
:::

::: {#952324be .cell .code}
``` python
fig = px.bar(df_pokemon, x='Type 1', facet_row='Legendary')
fig.show()
 
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Legendary=False<br>Type 1=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":["Grass","Grass","Grass","Grass","Fire","Fire","Fire","Fire","Fire","Water","Water","Water","Water","Bug","Bug","Bug","Bug","Bug","Bug","Bug","Normal","Normal","Normal","Normal","Normal","Normal","Normal","Normal","Poison","Poison","Electric","Electric","Ground","Ground","Poison","Poison","Poison","Poison","Poison","Poison","Fairy","Fairy","Fire","Fire","Normal","Normal","Poison","Poison","Grass","Grass","Grass","Bug","Bug","Bug","Bug","Ground","Ground","Normal","Normal","Water","Water","Fighting","Fighting","Fire","Fire","Water","Water","Water","Psychic","Psychic","Psychic","Psychic","Fighting","Fighting","Fighting","Grass","Grass","Grass","Water","Water","Rock","Rock","Rock","Fire","Fire","Water","Water","Water","Electric","Electric","Normal","Normal","Normal","Water","Water","Poison","Poison","Water","Water","Ghost","Ghost","Ghost","Ghost","Rock","Psychic","Psychic","Water","Water","Electric","Electric","Grass","Grass","Ground","Ground","Fighting","Fighting","Normal","Poison","Poison","Ground","Ground","Normal","Grass","Normal","Normal","Water","Water","Water","Water","Water","Water","Psychic","Bug","Ice","Electric","Fire","Bug","Bug","Normal","Water","Water","Water","Water","Normal","Normal","Water","Electric","Fire","Normal","Rock","Rock","Rock","Rock","Rock","Rock","Normal","Dragon","Dragon","Dragon","Psychic","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Bug","Bug","Bug","Bug","Poison","Water","Water","Electric","Fairy","Normal","Fairy","Fairy","Psychic","Psychic","Electric","Electric","Electric","Electric","Grass","Water","Water","Rock","Water","Grass","Grass","Grass","Normal","Grass","Grass","Bug","Water","Water","Psychic","Dark","Dark","Water","Ghost","Psychic","Psychic","Normal","Bug","Bug","Normal","Ground","Steel","Steel","Fairy","Fairy","Water","Bug","Bug","Bug","Bug","Bug","Dark","Normal","Normal","Fire","Fire","Ice","Ice","Water","Water","Water","Ice","Water","Steel","Dark","Dark","Dark","Water","Ground","Ground","Normal","Normal","Normal","Fighting","Fighting","Ice","Electric","Fire","Normal","Normal","Rock","Rock","Rock","Rock","Psychic","Grass","Grass","Grass","Grass","Fire","Fire","Fire","Fire","Water","Water","Water","Water","Dark","Dark","Normal","Normal","Bug","Bug","Bug","Bug","Bug","Water","Water","Water","Grass","Grass","Grass","Normal","Normal","Water","Water","Psychic","Psychic","Psychic","Psychic","Bug","Bug","Grass","Grass","Normal","Normal","Normal","Bug","Bug","Bug","Normal","Normal","Normal","Fighting","Fighting","Normal","Rock","Normal","Normal","Dark","Dark","Steel","Steel","Steel","Steel","Steel","Steel","Fighting","Fighting","Fighting","Electric","Electric","Electric","Electric","Electric","Bug","Bug","Grass","Poison","Poison","Water","Water","Water","Water","Water","Fire","Fire","Fire","Fire","Psychic","Psychic","Normal","Ground","Ground","Ground","Grass","Grass","Normal","Dragon","Dragon","Normal","Poison","Rock","Rock","Water","Water","Water","Water","Ground","Ground","Rock","Rock","Rock","Rock","Water","Water","Normal","Normal","Ghost","Ghost","Ghost","Ghost","Ghost","Grass","Psychic","Dark","Dark","Psychic","Ice","Ice","Ice","Ice","Ice","Ice","Water","Water","Water","Water","Water","Dragon","Dragon","Dragon","Dragon","Steel","Steel","Steel","Steel","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Normal","Bug","Bug","Electric","Electric","Electric","Grass","Grass","Rock","Rock","Rock","Rock","Bug","Bug","Bug","Bug","Bug","Bug","Bug","Electric","Water","Water","Grass","Grass","Water","Water","Normal","Ghost","Ghost","Normal","Normal","Normal","Ghost","Dark","Normal","Normal","Psychic","Poison","Poison","Steel","Steel","Rock","Psychic","Normal","Normal","Ghost","Dragon","Dragon","Dragon","Dragon","Normal","Fighting","Fighting","Fighting","Ground","Ground","Poison","Poison","Poison","Poison","Grass","Water","Water","Water","Grass","Grass","Grass","Dark","Electric","Normal","Ground","Grass","Electric","Fire","Fairy","Bug","Grass","Ice","Ground","Ice","Normal","Psychic","Psychic","Rock","Ghost","Ice","Electric","Electric","Electric","Electric","Electric","Electric","Psychic","Water","Water","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Normal","Dark","Dark","Grass","Grass","Fire","Fire","Water","Water","Psychic","Psychic","Normal","Normal","Normal","Electric","Electric","Rock","Rock","Rock","Psychic","Psychic","Ground","Ground","Normal","Normal","Fighting","Fighting","Fighting","Water","Water","Water","Fighting","Fighting","Bug","Bug","Bug","Bug","Bug","Bug","Grass","Grass","Grass","Grass","Water","Ground","Ground","Ground","Fire","Fire","Fire","Grass","Bug","Bug","Dark","Dark","Psychic","Ghost","Ghost","Water","Water","Rock","Rock","Poison","Poison","Dark","Dark","Normal","Normal","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Water","Water","Ice","Ice","Ice","Normal","Normal","Electric","Bug","Bug","Grass","Grass","Water","Water","Water","Bug","Bug","Grass","Grass","Steel","Steel","Steel","Electric","Electric","Electric","Psychic","Psychic","Ghost","Ghost","Ghost","Dragon","Dragon","Dragon","Ice","Ice","Ice","Bug","Bug","Ground","Fighting","Fighting","Dragon","Ground","Ground","Dark","Dark","Normal","Normal","Normal","Dark","Dark","Fire","Bug","Dark","Dark","Dark","Bug","Bug","Water","Water","Normal","Normal","Bug","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Fire","Fire","Bug","Bug","Bug","Fire","Fire","Fairy","Fairy","Fairy","Grass","Grass","Fighting","Fighting","Normal","Psychic","Psychic","Psychic","Steel","Steel","Steel","Steel","Fairy","Fairy","Fairy","Fairy","Dark","Dark","Rock","Rock","Poison","Poison","Water","Water","Electric","Electric","Rock","Rock","Rock","Rock","Fairy","Fighting","Electric","Rock","Dragon","Dragon","Dragon","Steel","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ice","Ice","Flying","Flying"],"xaxis":"x2","y":{"bdata":"AQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEB","dtype":"i1"},"yaxis":"y2"},{"hovertemplate":"Legendary=True<br>Type 1=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":["Ice","Electric","Fire","Psychic","Psychic","Psychic","Electric","Fire","Water","Psychic","Fire","Rock","Ice","Steel","Dragon","Dragon","Dragon","Dragon","Water","Water","Ground","Ground","Dragon","Dragon","Steel","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Steel","Water","Fire","Normal","Ghost","Ghost","Dark","Grass","Grass","Normal","Psychic","Steel","Rock","Grass","Flying","Flying","Electric","Electric","Dragon","Dragon","Ground","Ground","Dragon","Dragon","Dragon","Fairy","Dark","Dragon","Rock","Rock","Psychic","Psychic","Fire"],"xaxis":"x","y":{"bdata":"AQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQE=","dtype":"i1"},"yaxis":"y"}],"layout":{"annotations":[{"font":{},"showarrow":false,"text":"Legendary=True","textangle":90,"x":0.98,"xanchor":"left","xref":"paper","y":0.2425,"yanchor":"middle","yref":"paper"},{"font":{},"showarrow":false,"text":"Legendary=False","textangle":90,"x":0.98,"xanchor":"left","xref":"paper","y":0.7575000000000001,"yanchor":"middle","yref":"paper"}],"barmode":"relative","legend":{"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,0.98],"title":{"text":"Type 1"}},"xaxis2":{"anchor":"y2","domain":[0,0.98],"matches":"x","showticklabels":false},"yaxis":{"anchor":"x","domain":[0,0.485],"title":{"text":"count"}},"yaxis2":{"anchor":"x2","domain":[0.515,1],"matches":"y","title":{"text":"count"}}}}
```
:::
:::

::: {#90aea62d .cell .markdown}
For more information please go to the tutorial [Plotly Express Wide-Form
Support in Python](https://plotly.com/python/wide-form/).
:::

::: {#3354adc8 .cell .markdown}
## Conclusion

This concludes our first introduction to **data visualization**:

-   Working with `matplotlib.pyplot`.\
-   Working with more convenient version of `pyplot.express`.
-   Creating basic plots: histograms, scatterplots, and barplots.

Next time, we\'ll move onto discussing `seaborn`, another very useful
package for data visualization.
:::

::: {#1ce46c35 .cell .markdown}
:::

::: {#37df836b .cell .markdown}
# Data visualization, pt. 2 (`seaborn`) {#data-visualization-pt-2-seaborn}
:::

::: {#a0c713dc .cell .markdown}
## Goals of this exercise {#goals-of-this-exercise}

-   Introducting `seaborn`.
-   Putting `seaborn` into practice:
    -   **Univariate** plots (histograms).\
    -   **Bivariate** continuous plots (scatterplots and line plots).
    -   **Bivariate** categorical plots (bar plots, box plots, and strip
        plots).
:::

::: {#f03cbd26 .cell .markdown}
## Introducing `seaborn`
:::

::: {#9ef901fb .cell .markdown}
### What is `seaborn`?

> [`seaborn`](https://seaborn.pydata.org/) is a data visualization
> library based on `matplotlib`.

-   In general, it\'s easier to make nice-looking graphs with `seaborn`.
-   The trade-off is that `matplotlib` offers more flexibility.
:::

::: {#489354b0 .cell .code}
``` python
import seaborn as sns ### importing seaborn
import pandas as pd
import matplotlib.pyplot as plt ## just in case we need it
import numpy as np
```
:::

::: {#c2ef2d36 .cell .code}
``` python
%matplotlib inline 
%config InlineBackend.figure_format = 'retina'
```
:::

::: {#b014f804 .cell .markdown}
### The `seaborn` hierarchy of plot types

We\'ll learn more about exactly what this hierarchy means today (and in
next lecture).

![title](img/seaborn_library.png)
:::

::: {#a7635f4e .cell .markdown}
### Example dataset {#example-dataset}

Today we\'ll work with a new dataset, from
[Gapminder](https://www.gapminder.org/data/documentation/).

-   **Gapminder** is an independent Swedish foundation dedicated to
    publishing and analyzing data to correct misconceptions about the
    world.
-   Between 1952-2007, has data about `life_exp`, `gdp_cap`, and
    `population`.
:::

::: {#0903ed20 .cell .code}
``` python
df_gapminder = pd.read_csv("data/gapminder_full.csv")
```
:::

::: {#c598f7d5 .cell .code}
``` python
df_gapminder.head(2)
```

::: {.output .display_data}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1952</td>
      <td>8425333</td>
      <td>Asia</td>
      <td>28.801</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>1957</td>
      <td>9240934</td>
      <td>Asia</td>
      <td>30.332</td>
      <td>820.853030</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#8f3b8d83 .cell .code}
``` python
df_gapminder.shape
```

::: {.output .display_data}
    (1704, 6)
:::
:::

::: {#588bce4b .cell .markdown}
## Univariate plots

> A **univariate plot** is a visualization of only a *single* variable,
> i.e., a **distribution**.

![title](img/displot.png)
:::

::: {#c3f6917c .cell .markdown}
### Histograms with `sns.histplot` {#histograms-with-snshistplot}

-   We\'ve produced histograms with `plt.hist`.\
-   With `seaborn`, we can use `sns.histplot(...)`.

Rather than use `df['col_name']`, we can use the syntax:

``` python
sns.histplot(data = df, x = col_name)
```

This will become even more useful when we start making **bivariate
plots**.
:::

::: {#fb2c9dc7 .cell .code}
``` python
# Histogram of life expectancy
sns.histplot(data = df_gapminder, x = "life_exp");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/0bcd2126b69fb18a157cd2488f141e049b7f4d2a.png)
:::
:::

::: {#5a5313a5 .cell .markdown}
#### Modifying the number of bins

As with `plt.hist`, we can modify the number of *bins*.
:::

::: {#148e3f48 .cell .code}
``` python
# Fewer bins
sns.histplot(data = df_gapminder, x = 'life_exp', bins = 10, alpha = .6);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/d91700846e76f9f0dc30e61331819ad460e44d3f.png)
:::
:::

::: {#f9950d2e .cell .code}
``` python
# Many more bins!
sns.histplot(data = df_gapminder, x = 'life_exp', bins = 100, alpha = .6);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/80156289178c9b97a55a087c296dfa2e0841b1f6.png)
:::
:::

::: {#bcc2af69 .cell .markdown}
#### Modifying the y-axis with `stat`

By default, `sns.histplot` will plot the **count** in each bin. However,
we can change this using the `stat` parameter:

-   `probability`: normalize such that bar heights sum to `1`.
-   `percent`: normalize such that bar heights sum to `100`.
-   `density`: normalize such that total *area* sums to `1`.
:::

::: {#071bbbc0 .cell .code}
``` python
# Note the modified y-axis!
sns.histplot(data = df_gapminder, x = 'life_exp', stat = "probability", alpha = .6);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/08bdcf328460d1371c4e98654fcbffad816821b5.png)
:::
:::

::: {#c7858b5c .cell .markdown}
### Check-in {#check-in}

How would you make a histogram showing the distribution of `population`
values in `2007` alone?

-   Bonus 1: Modify this graph to show `probability`, not `count`.
-   Bonus 2: What do you notice about this graph, and how might you
    change it?
:::

::: {#c1eb1320 .cell .code}
``` python
### Your code here
year = 2007
sns.histplot(data = df_gapminder[df_gapminder['year'] == year], x = "population", stat = "probability", log_scale=(True, False))

# for bonus 2; without log_scale the very tall pillar at 0 sticks out and looks bad, hence log_scale
# but log_scale disappears the population numbers, so plt.xticks() is needed
plt.xticks([1e6, 1e7, 1e8, 1e9, 1e10], ["1M", "10M", "100M", "1B", "10B"])  #M and B are more legible than exponents, in my opinion
plt.show()
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/32caba197aeb5c46d9656ed1eab8b40ec9b3799e.png)
:::
:::

::: {#14f61beb .cell .markdown}
## Bivariate continuous plots

> A **bivariate continuous plot** visualizes the relationship between
> *two continuous variables*.

![title](img/seaborn_relplot.png)
:::

::: {#37b12e06 .cell .markdown}
### Scatterplots with `sns.scatterplot` {#scatterplots-with-snsscatterplot}

> A **scatterplot** visualizes the relationship between two continuous
> variables.

-   Each observation is plotted as a single dot/mark.
-   The position on the `(x, y)` axes reflects the value of those
    variables.

One way to make a scatterplot in `seaborn` is using `sns.scatterplot`.
:::

::: {#eeebe6ff .cell .markdown}
#### Showing `gdp_cap` by `life_exp`

What do we notice about `gdp_cap`?
:::

::: {#301b6675 .cell .code}
``` python
sns.scatterplot(data = df_gapminder, x = 'gdp_cap',
               y = 'life_exp', alpha = .3);

# we can observe a good share of gdp_cap is comparably low regardless of life_exp,
# but has a tendency to rise with life_exp, save few outliers
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/299fbc63118ece85f2da388250a15509604905a9.png)
:::
:::

::: {#e92d1159 .cell .markdown}
#### Showing `gdp_cap_log` by `life_exp`
:::

::: {#de9becb2 .cell .code}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder, x = 'gdp_cap_log', y = 'life_exp', alpha = .3);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/9ca96da96bb703875bc18b34fc81610da2acec65.png)
:::
:::

::: {#3aaf4f35 .cell .markdown}
#### Adding a `hue`

-   What if we want to add a *third* component that\'s categorical, like
    `continent`?
-   `seaborn` allows us to do this with `hue`.
:::

::: {#be64e906 .cell .code}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp', hue = "continent", alpha = .7);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/c70fe4f7213fb6a078ba921450269848457d1e16.png)
:::
:::

::: {#b8088781 .cell .markdown}
#### Adding a `size`

-   What if we want to add a *fourth* component that\'s continuous, like
    `population`?
-   `seaborn` allows us to do this with `size`.
:::

::: {#5c445c72 .cell .code}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp',
                hue = "continent", size = 'population', alpha = .7);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/de5b91c1ed61ee659a7f996c0b8f16899f3d47bb.png)
:::
:::

::: {#3fc2e86e .cell .markdown}
#### Changing the position of the legend
:::

::: {#747f04da .cell .code}
``` python
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp',
                hue = "continent", size = 'population', alpha = .7);

plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/05d3dfd47f4ecabbc4f8b183cc92636e8f0cd518.png)
:::
:::

::: {#650e228c .cell .markdown}
### Lineplots with `sns.lineplot` {#lineplots-with-snslineplot}

> A **lineplot** also visualizes the relationship between two continuous
> variables.

-   Typically, the position of the line on the `y` axis reflects the
    *mean* of the `y`-axis variable for that value of `x`.
-   Often used for plotting **change over time**.

One way to make a lineplot in `seaborn` is using
[`sns.lineplot`](https://seaborn.pydata.org/generated/seaborn.lineplot.html).
:::

::: {#d2fb03c2 .cell .markdown}
#### Showing `life_exp` by `year`

What general trend do we notice?
:::

::: {#e793e9da .cell .code}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp');

# we can see life expectancy has been growing every year
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/e4eb56bff0c18a55433304cc4c092f9fed1e3630.png)
:::
:::

::: {#9aed5261 .cell .markdown}
#### Modifying how error/uncertainty is displayed

-   By default, `seaborn.lineplot` will draw **shading** around the line
    representing a confidence interval.
-   We can change this with `errstyle`.
:::

::: {#d8200ed3 .cell .code}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp',
            err_style = "bars");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/f68abafc56721fdde1e1676baa34a0a8a4fae780.png)
:::
:::

::: {#b6430661 .cell .markdown}
#### Adding a `hue` {#adding-a-hue}

-   We could also show this by `continent`.\
-   There\'s (fortunately) a positive trend line for each `continent`.
:::

::: {#11c7da9b .cell .code}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp',
            hue = "continent")
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/f34429863310ad645942a0ed6f27fdc91ad622fd.png)
:::
:::

::: {#f9798fd6 .cell .markdown}
#### Check-in {#check-in}

How would you plot the relationship between `year` and `gdp_cap` for
countries in the `Americas` only?
:::

::: {#7e133b8c .cell .code}
``` python
### Your code here
sns.lineplot(data = df_gapminder[df_gapminder['continent'] == 'Americas'],
             x = 'year',
             y = 'gdp_cap');
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/b92ffd41580085ab347b2093abd5445298202b06.png)
:::
:::

::: {#2051330e .cell .markdown}
#### Heteroskedasticity in `gdp_cap` by `year`

-   [**Heteroskedasticity**](https://en.wikipedia.org/wiki/Homoscedasticity_and_heteroscedasticity)
    is when the *variance* in one variable (e.g., `gdp_cap`) changes as
    a function of another variable (e.g., `year`).
-   In this case, why do you think that is?
-   Likely because, over time, richer and more peaceful countries (i.e.
    USA) prospered and grew much faster than poorer regions, often
    dealing with unrest and civil wars
:::

::: {#93dff0da .cell .markdown}
#### Plotting by country

-   There are too many countries to clearly display in the `legend`.
-   But the top two lines are the `United States` and `Canada`.
    -   I.e., two countries have gotten much wealthier per capita, while
        the others have not seen the same economic growth.
:::

::: {#1f9c11fa .cell .code}
``` python
sns.lineplot(data = df_gapminder[df_gapminder['continent']=="Americas"],
             x = 'year', y = 'gdp_cap', hue = "country", legend = None);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/315d747a133525817630fef45c2b8303c5e000ba.png)
:::
:::

::: {#c44e3787 .cell .markdown}
### Using `replot`

-   `relplot` allows you to plot either line plots or scatter plots
    using `kind`.
-   `relplot` also makes it easier to `facet` (which we\'ll discuss
    momentarily).
:::

::: {#ef638f45 .cell .code}
``` python
sns.relplot(data = df_gapminder, x = "year", y = "life_exp", kind = "line");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/b848b36ba9e1d84a8e077bc94183ee2eeef051ed.png)
:::
:::

::: {#74a9cfeb .cell .markdown}
#### Faceting into `rows` and `cols`

We can also plot the same relationship across multiple \"windows\" or
**facets** by adding a `rows`/`cols` parameter.
:::

::: {#82ae41ef .cell .code}
``` python
sns.relplot(data = df_gapminder, x = "year", y = "life_exp", kind = "line", col = "continent");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/59c2be5c7c26e1a2d9d49cc79d8867090c4265b5.png)
:::
:::

::: {#0bfda82c .cell .markdown}
## Bivariate categorical plots

> A **bivariate categorical plot** visualizes the relationship between
> one categorical variable and one continuous variable.

![title](img/seaborn_catplot.png)
:::

::: {#98aced57 .cell .markdown}
### Example dataset {#example-dataset}

Here, we\'ll return to our Pokemon dataset, which has more examples of
categorical variables.
:::

::: {#3fcdb89d .cell .code}
``` python
df_pokemon = pd.read_csv("data/pokemon.csv")
```
:::

::: {#f7796540 .cell .markdown}
### Barplots with `sns.barplot` {#barplots-with-snsbarplot}

> A **barplot** visualizes the relationship between one *continuous*
> variable and a *categorical* variable.

-   The *height* of each bar generally indicates the mean of the
    continuous variable.
-   Each bar represents a different *level* of the categorical variable.

With `seaborn`, we can use the function `sns.barplot`.
:::

::: {#9c9c6fa2 .cell .markdown}
#### Average `Attack` by `Legendary` status
:::

::: {#6c432a87 .cell .code}
``` python
sns.barplot(data = df_pokemon,
           x = "Legendary", y = "Attack");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/53a0676e1012190e35a43f168915719edf5c6575.png)
:::
:::

::: {#7ecdf6f1 .cell .markdown}
#### Average `Attack` by `Type 1`

Here, notice that I make the figure *bigger*, to make sure the labels
all fit.
:::

::: {#6f0b890d .cell .code}
``` python
plt.figure(figsize=(15,4))
sns.barplot(data = df_pokemon,
           x = "Type 1", y = "Attack");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/9c486ce49109cae2ba86cbe095459c592e7decbc.png)
:::
:::

::: {#79fb95bf .cell .markdown}
#### Check-in {#check-in}

How would you plot `HP` by `Type 1`?
:::

::: {#11cc3fe4 .cell .code}
``` python
plt.figure(figsize=(15,4))
sns.barplot(data = df_pokemon,
           x = "Type 1", y = "HP");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/416b779d7384602f298c55fdb3aaaca12ee63728.png)
:::
:::

::: {#f9dbcdcc .cell .markdown}
#### Modifying `hue`

As with `scatterplot` and `lineplot`, we can change the `hue` to give
further granularity.

-   E.g., `HP` by `Type 1`, further divided by `Legendary` status.
:::

::: {#fc2612f3 .cell .code}
``` python
plt.figure(figsize=(15,4))
sns.barplot(data = df_pokemon,
           x = "Type 1", y = "HP", hue = "Legendary");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/29efa038b3a52c1061c5d833556b426a2a261dc7.png)
:::
:::

::: {#03b58212 .cell .markdown}
### Using `catplot`

> `seaborn.catplot` is a convenient function for plotting bivariate
> categorical data using a range of plot types (`bar`, `box`, `strip`).
:::

::: {#7890e17e .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "bar");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/856d635d7638220d0968149bf555d818f1c19455.png)
:::
:::

::: {#cac8e4fb .cell .markdown}
#### `strip` plots

> A `strip` plot shows each individual point (like a scatterplot),
> divided by a **category label**.
:::

::: {#809e429a .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "strip", alpha = .5);
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/fc6c13a4bd3277f5258d254849f07d1395a94bc6.png)
:::
:::

::: {#3662d04a .cell .markdown}
#### Adding a `mean` to our `strip` plot

We can plot *two graphs* at the same time, showing both the individual
points and the means.
:::

::: {#9e4c0184 .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "strip", alpha = .1)
sns.pointplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", hue = "Legendary");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/c3d5dcf1120871237526de3b4c693fc87ffbb830.png)
:::
:::

::: {#ba96735f .cell .markdown}
#### `box` plots

> A `box` plot shows the interquartile range (the middle 50% of the
> data), along with the minimum and maximum.
:::

::: {#c1c14414 .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "box");
```

::: {.output .display_data}
![](vertopal_e7e159d639df4aa58bd01e86d9b446d3/49e0bd0363950302ce57fe8d26061d14c9f80300.png)
:::
:::

::: {#84f11a8e .cell .markdown}
## Conclusion {#conclusion}

As with our lecture on `pyplot`, this just scratches the surface.

But now, you\'ve had an introduction to:

-   The `seaborn` package.
-   Plotting both **univariate** and **bivariate** data.
-   Creating plots with multiple layers.
:::
