---
layout: single 
classes: 
title: "Core Types of Machine Learning" 
last_modified_at:
---

## 1. Supervised Learning

Supervised Learning uses labeled data, making predictions based on **known input-output pairs**.
Each row in the training set includes both the input data and the desired output, or "label," allowing the model to learn the relationship between inputs and outputs. By observing these pairs, the model develops an understanding of how the inputs correlate with the outputs and uses this to make predictions on new, unseen data.

### 1.1. Regression
Predicting continuous values, where the output can take on a range of values. For example, predicting housing prices based on features like location, size, and amenities.
- **Linear Regression**: Suitable for straightforward, linear relationships (e.g., sales forecasting).
- **Polynomial Regression**: Handles non-linear relationships by fitting polynomial curves to the data.
- **Support Vector Regression (SVR)**: Adaptation of SVM for continuous predictions, good for smaller datasets.
- **Decision Tree Regressor**: Flexible model that can capture complex relationships.
- **Random Forest Regressor**: An ensemble of decision trees used for regression tasks, averaging the predictions from multiple trees.
- **Gradient Boosting Regressor**: A boosting method that sequentially builds weak models, typically decision trees, correcting errors from the previous models.

### 1.2. Classification
Predicting discrete labels, where the output falls into one of several predefined categories.
For instance, classifying emails as "spam" or "not spam" is a classification problem.
- **Logistic Regression**: Great for binary classification (e.g., churn prediction).
- **Naïve Bayes**: Common in text classification (e.g., sentiment analysis, spam detection).
- **Support Vector Machine (SVM)**: Powerful for high-dimensional data like image recognition.
- **Decision Tree**: Intuitive model useful for both binary and multi-class classification.
- **K-Nearest Neighbors (KNN)**: Simple, non-parametric method that is effective on smaller datasets.
- **Random Forest**: An ensemble method that uses multiple decision trees to vote on the final prediction, reducing the likelihood of overfitting.

## 2. Unsupervised Learning
Unsupervised Learning discovers patterns or structure in data **without labeled outcomes**.
The training data has no predefined output labels or categories. The model attempts to find hidden patterns, structures, or relationships within the data by grouping similar data points or identifying underlying features. Without any guidance on what the correct outputs should be, the model learns independently by exploring the dataset's inherent structure.

### 2.1. Clustering
Grouping similar data points together. For example, in customer segmentation, a clustering algorithm can analyze customer behaviors and identify distinct customer groups, helping companies personalize marketing efforts for each group.
- **K-Means**: Commonly used in customer segmentation.
- **Hierarchical Clustering**: Useful for datasets with natural, hierarchical groupings (e.g., biological data).
- **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)**: Good for clustering spatial data or data with noise.
- **Gaussian Mixture Models (GMM)**: A probabilistic model, useful when clusters have different shapes and sizes.

### 2.2. Dimensionality Reduction
Simplifying high-dimensional data by reducing the number of features while retaining important information. For instance, dimensionality reduction techniques like Principal Component Analysis (PCA) can condense large, complex datasets into a more manageable size, making visualization or further analysis easier.
- **Principal Component Analysis (PCA)**: Effective for feature reduction in high-dimensional datasets (e.g., image and gene data).
- **t-Distributed Stochastic Neighbor Embedding (t-SNE)**: Often used for visualizing high-dimensional data, such as word embeddings.
- **Autoencoders**: Neural network-based approach often used for complex data compression and anomaly detection.
- **Linear Discriminant Analysis (LDA)**: Primarily for dimensionality reduction with labeled data, also useful for feature extraction in supervised tasks.
