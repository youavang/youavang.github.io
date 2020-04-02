---
title: "Stock Market Prediction with LSTM"
dateL: 2020-03-28
tags: [LSTM, data science, artificial recurrent neural network, stock market prediction, closing price prediction, Jupyter Notebook]
header:
  image: 
excerpt: "Stock market closing price prediction with LSTM."
mathjax: "true"
---
The program use Long Short Term Memory (LSTM) to predict the stock closing price of a company by analysing the past 60 days. LSTM is an artificial recurrent neural network achitecture used in deep learning. Also, this program is written in Jupyter Notebook.

Why use LSTM?
* Has feedback connections that allows it to process single both single data points, such as images, and an entire sequence data points, such as speech or videos.
+ It is highly effective when used for sequence prediction problem due to its capability to store past information that is important and forget information that is not important.

Before coding the program, import labraries required for the program.
Note: below is a few libriaries as an example. Check this [link](https://github.com/youavang/LSTM-Closing-Stock-Price-Prediction/blob/master/LSTM%20Closing%20Stock%20Price%20Prediction.ipynb) for the full list.

```python
# Import libraries
import pandas as pd
import pandas_datareader as web
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler
from keras.models import Sequential
from keras.layers import Dense, LSTM
```
Extract data of stock closing price of a company with pandas data reader for analysis and plot the closing price.
<img src="{{ site.url }}{{ site.baseurl }}/images/stock/stock.png" alt="linearly separable data" height="48">

Next the data is scaled with min-max scaler to fit within a range from 0 to 1, then it is plit into training and testing sets. The training data set is turned into a numpy array, then reshaped into the deminsional before the LSTM model is trained on them. The testing data set also gets transformed and plugged into the LSTM model.

The root mean squared error (rmse) of the training and testing data sets is used to measure the performance of the LSTM model in predicting the stock closing price. A low rmse value indicates low error rates and higher accuracy at prediction. In our case, the rmse = 1.08.

Here is the plot of the training data set (blue), the predicted data set (yellow) and the actual data set (red).
<img src="{{ site.url }}{{ site.baseurl }}/images/stock/stockpredict.png" alt="linearly separable data" height="48">

Overall, the LSTM did well at predicting the stock closing price. I hope you enjoyed this short summary of this project. You can view the enitre codes at this [link](https://github.com/youavang/LSTM-Closing-Stock-Price-Prediction/blob/master/LSTM%20Closing%20Stock%20Price%20Prediction.ipynb).
