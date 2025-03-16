---
layout: single 
classes: 
title: "Standardization of Datasets" 
last_modified_at:
---

Data standardization is a crucial for machine learning algorithms. For instance, let us think the two features have different scales or units:

- Range of Feature A: 0 - 25
- Range of Feature B: 500 - 25000

The feature B will most likely dominate the model with the large ranges.
The data standardization rescale the data to ensure the that features contribute proportionately.
In scikit-learn, `sklearn.preprocessing` module provides various scalers.

``` python
from sklearn.preprocessing import (
    StandardScaler,
    MinMaxScaler,
    MaxAbsScaler,
    RobustScaler,
    PowerTransformer,
    QuantileTransformer,
    )
```

## Linear scalers

### StandardScaler: `StandardScaler()`

StandardScaler scales a features by removing the mean and scaling to unit variance.

$$ X_{std} = \frac{X - \overline{X}} {\sigma} $$

where $ \overline{X} $ is the mean of the feature and $\sigma$ is the standard deviation.


``` python
from sklearn.preprocessing import StandardScaler

X = np.array([[4, -4, -9],
              [2, -1,  0],
              [4,  2,  2],
              [2,  5,  3]])
              
StandardScaler().fit_transform(X)
```

    [[ 1.         -1.34164079 -1.68654809]
     [-1.         -0.4472136   0.21081851]
     [ 1.          0.4472136   0.63245553]
     [-1.          1.34164079  0.84327404]]

- **Sensitive to outliers:** It uses the mean and standard deviation to center and scale the data.
- **Assumes normal distribution:** It works best when the data is normally distributed.
- **Can be influenced by outliers:** Outliers can significantly affect the mean and standard deviation, leading to suboptimal scaling.

### MinMaxScaler: `MinMaxScaler()`

MinMaxScaler rescales a feature to a specific range, typically between 0 and 1.

$$X_{std} = \frac{X - min(X)} {max(X) - min(X)}$$

``` python
from sklearn.preprocessing import MinMaxScaler

X = np.array([[4, -4, -9],
              [2, -1,  0],
              [4,  2,  2],
              [2,  5,  3]])
              
MinMaxScaler().fit_transform(X)
```

    [[1.         0.         0.        ]
     [0.         0.33333333 0.75      ]
     [1.         0.66666667 0.91666667]
     [0.         1.         1.        ]]

- **Preserves original distribution:** MinMaxScaler doesn't change the shape of the original distribution.
- **Sensitive to outliers:** Outliers can significantly affect the scaling, as they can influence the minimum and maximum values.
- **Suitable for neural networks:** It's often used in neural networks where inputs are expected to be in a specific range.

### MaxAbsScaler: `MaxAbsScaler()`

MaxAbsScaler rescales a feature by its maximum absolute value.

$$X_{std} = \frac{X} {max(|X|)}$$

``` python
from sklearn.preprocessing import MaxAbsScaler

X = np.array([[4, -4, -9],
              [2, -1,  0],
              [4,  2,  2],
              [2,  5,  3]])
              
MaxAbsScaler().fit_transform(X)
```

    [[ 1.         -0.8        -1.        ]
     [ 0.5        -0.2         0.        ]
     [ 1.          0.4         0.22222222]
     [ 0.5         1.          0.33333333]]

- **Preserves sparsity:** It doesn't shift or center the data, so it's ideal for sparse datasets.
- **Simple scaling:** It's a straightforward scaling technique that doesn't involve complex calculations.
- **Suitable for specific scenarios:** It's particularly useful when you want to scale features without affecting their zero-centered nature.

### RobustScaler: `RobustScaler()`

RobustScaler rescales a feature by removing the median and scaling it by the interquartile range.

$$X_{std} = \frac{X - \tilde{X}} {IQR}$$

where $\tilde{X}$ is the median of the feature and $IQR$ is The interquartile range (Q3 - Q1).

``` python
from sklearn.preprocessing import RobustScaler

X = np.array([[4, -4, -9],
              [2, -1,  0],
              [4,  2,  2],
              [2,  5,  3]])
              
RobustScaler().fit_transform(X)
```

    [[ 0.5        -1.         -2.22222222]
     [-0.5        -0.33333333 -0.22222222]
     [ 0.5         0.33333333  0.22222222]
     [-0.5         1.          0.44444444]]

- **Robust to outliers:** It uses the median and interquartile range (IQR) to center and scale the data.
- **Less affected by outliers:** The median and IQR are less sensitive to extreme values, making it more robust to outliers.
- **Suitable for non-normally distributed data:** It can handle skewed distributions more effectively.

## Non-linear scalers

### PowerTransformer: `PowerTransformer()`

**PowerTransformer** transform a features to a more Gaussian-like distribution.

1. **Skewness and Kurtosis:** The distribution of the features is analyzed to identify skewness and kurtosis.
2. **Parameter Estimation:** The optimal power parameter (lambda) is estimated using maximum likelihood estimation.
3. **Transformation:** The data is transformed using the estimated lambda.

![](/assets/images/PowerTransformer.png)

- **Parametric:** It assumes a specific parametric distribution (e.g., Box-Cox or Yeo-Johnson).
- **Distribution-based:** It transforms data to a specific distribution, often a normal distribution.
- **Sensitive to Outliers:** While less sensitive than some other methods, outliers can still influence the transformation.
- **May Distort Rank Order:** The relative order of data points might change after transformation.

### QuantileTransformer: `QuantileTransformer()`

**QuantileTransformer** transform a features to a specified distribution, typically a uniform or normal distribution.

1. **Rank-based Transformation:** Each data point is assigned a rank based on its position in the sorted list.
2. **Quantile Mapping:** The ranks are then mapped to quantiles of the desired distribution (uniform or normal).
3. **Transformation:** The data is transformed with their corresponding quantile map.

![](/assets/images/QuantileTransformer.png)

- **Non-parametric:** It doesn't assume a specific distribution for the data.
- **Rank-based:** It maps data points to quantiles of a desired distribution (uniform or normal).
- **Robust to Outliers:** It's less sensitive to outliers as it focuses on the relative ranks of data points.
- **Preserves Rank Order:** The relative order of data points remains unchanged after transformation.

## External Link

[Jupyter notebook](https://github.com/jhjang101/blog-nookbook/blob/1948cb7fc94706f2f736a5b3fa8a3444ec426fcc/scalers.ipynb)