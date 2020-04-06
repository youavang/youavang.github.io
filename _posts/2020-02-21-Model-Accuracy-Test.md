---
title: "Model Accuracy Test"
dateL: 2020-02-24
tags: [machine learning, logistric regression, svm, linear kernel, poly kernel, rbf, kNN, naive bayes, decision tree, random forest, classification, accuracy score]
header:
  image: 
excerpt: "Train multiple machine learning models on classification dataset."
mathjax: "true"
---
In this program, eight different machine learning models are trained on the same data. The data consist of different writings of numbers from 0 to 9. Each model will be tested on how well they can predict the number. The machine learning models being tested are:
  1. logistic regression
  2. svm with linear kernel
  3. svm with poly kernel
  4. svm with rbf kernel
  5. k-NN
  6. naive bayes
  7. decision tree classification
  8. random forest classification

Start by importing the required libraries and download the data:
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
```
Next, create a dataframe, then split the dataset into training (75%) and testing set and normalize the features.
```python
df = load_digits()
X = df.data
y = df.target

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 0)

from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)
```
Now train each model and calculate their accuracy score. For Svm poly kernel model, k-NN model and random forest model are train with different values of their respective hyperparameter in a loop to determine which values result in the highest accuracy score. Also, graph each of these models to visually assist in analyzing the trend.

For svm poly kernel model, degree = 3 gives the best accuracy score.
<img src="{{ site.url }}{{ site.baseurl }}/images/models/svm-kernel.png" alt="linearly separable data" height="25">

For k-NN model, k = 1 and k = 5 gives the best accuracy score.
<img src="{{ site.url }}{{ site.baseurl }}/images/models/kNN.png" height="25" width = "25">

For random forest model, estimator = 72, 73, 77, 78 gives the best accuracy score.
<img src="{{ site.url }}{{ site.baseurl }}/images/models/estimators.png" alt="linearly separable data" height="30">

Here are the best accuracy score for each models:
  1. Logistic Regression = 0.9622222222222222
  2. SVM with linear kernel = 0.9733333333333334
  3. SVM with poly kernel = 0.9822222222222222
  4. SVM with rbf kernerl = 0.9844444444444445
  5. k-NN = 0.9733333333333334
  6. Naive Bayes = 0.7733333333333333
  7. Decision Tree Classification = 0.8488888888888889
  8.  Random Forest Classification = 0.9822222222222222
  
When comparing the accuracy scores of all the models, SVM with rbf kernel produced the highest accuracy score for this dataset.

You can view the enitre codes at this [link](https://github.com/youavang/Model-Accuracy-Test/Model Accuracy Test.ipynb).
