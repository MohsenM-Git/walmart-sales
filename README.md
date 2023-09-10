# Walmart Sales: A Time Series Analysis

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/logo.jpg" width="800"/>



Periodic sales are among the most important business indicators so much so that many corporations usually set public targets for thier quarterly and annual sales. Sales influence profit margins -by reducing logistic costs associated with under- and over-purchases, and improve customer satisfaction. However, sales data show different features that make predicting them a challenge. On the one hand, sales have strong relationships with general economic factros such as inflation and job market conditions, and consumer sentiment. On the other hand, sale series typically show seasonality effect and contain various deterministic and stochastic trends.Therefore, forecasting sales data is of both business and technical importance. In this project, I analyze Walmart's sales data and build a model to predict its sales. 



## A Quick Look

**Data Preprocessing**
I start by merging all datasets, cleaning them, and setting the time-index appropriately.

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/prep-2.png" width="450"/> <img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/prep-1.png" width="450"/>

**Data Exploration**
Then, I explore the both the fearures and the sales data with visualization tools in `Python`. These include:
* feature analysis
 
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/unemp.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/gasprice.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/unemp-inf.png" width="650"/>

* characteristics of stores

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/size-type.png" width="450"/> <img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/type.png" width="450"/>


* correlations
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/pair-plot.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/corr.png" width="650"/>



* tiem series of sales
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/acf.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/pacf.png" width="650"/>

and,

* Seasonal Decompisiton
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/temp.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/decomp.png" width="650"/>

Understainding the data better helps the desing of farcasting models. It seems that determinsitic trends are the most important factors. 

**Forecasting**

I start by simulating a white noise to match and predict the sales series. Although, a white noise, by definition, is impossible to predit, as we see in the graph, it matches the data fairly well. I also use a number of `rolling-average` models. 

* White Noise
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/wn.png" width="650"/>



* Exponential Smoothing
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/smooth-1.png" width="650"/>

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/smooth-2.png" width="650"/>

  
* Time Series Models
Lstly, I forecast the sales series using standard time series models. In addition to predictive power, I run diagnostic tests on the residuals to ensure the validity of my estimates. 

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/SAR-1.png" width="650"/>
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/sarimax-1.png" width="650"/> 
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/diags.png" width="650"/> 


**Comparing Forecasts**

This notebook ends with comparing various predicitive models. Four metrics that I use to compare out-of-smaple (train-test) accuracy of forecasts are: `RMSE`, `Normalized RMSE`, `MAE`, and `MAPE`.

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/rmse.png" width="650"/> 

It is also helpful to compare these models visually.


<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/comp-1.png" width="650"/> 
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/comp-2.png" width="650"/> 
<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/comp-3.png" width="650"/> 

**Conclusion**
An interesting finding of this exercise is that the SARIMAX model does not have the best out-of-sample performance. To find-out why, I further explore the fitted values and forecasted values with the original seris. It seems that inclduing *CPI* as a feature is the reason for the inaccurate forecasts of the SARIMAX model. It is important to note that in my split, it just so happens that there are no holiday weeks in the test set. Therefore, incorporating features does not improve the forecasts. 

<img src="https://github.com/MohsenM-Git/walmart-sales/blob/main/Images/comp-4.png" width="650"/> 

My `naive` forecast, which only considers last year sales in the same week is one of the top 5 most accurate predictions. Also, the `weighted rolling average` model outperforms most sophisticated time series models. Alternatively, simply including seasonal pattern in the AR framework significantly imporves the accuracy of forecasts. Therefore, his exercise, in my opinion, above all, emphasizes the importance of determinisitc trends in forecasting future sales.

## Content
[Part I: Data Exploration ](#1) 
- [Data Preprocessing](#1.1)
    * [Merging Datasets](#1.1.1)
    * [TimeStamps and Frequencies](#1.1.2)
- [Data Visualization](#1.2)
    * [Economic Factors](#1.2.1)
    * [Store Characteristics](#1.2.2)
    * [Holidays](#1.2.3)
- [Relations and Correlations](#1.3)

[Part II: Forecasting ](#2) 
- [Train-Test Split](#2.1) 
- [Diagnostic Plots and Trend Analysis](#2.2)
    * [QQ, ACF, PACF Plots](#2.2.1)
    * [Seasonal Decompisiton and Unit Root Tests](#2.2.2)
   
   
- [Forecasting Models](#2.3)
    * [White Noise](#2.3.1)
    * [Random Walk](#2.3.2)
    * [Weighted and Rolling Averages](#2.3.3)
    * [Exponential Smoothing](#2.3.4)
    * [Time Series Models](#2.3.5)
    
- [Comparing Forecasts](#2.4)
    * [Accuracy Measures](#2.4.1)
    * [Visual Comparison](#2.4.2)
- [Concluding Remarks](#2.5)


## Data
Walmart's weekly sales data obtaind from a `Kaggle` project [(Link)](https://www.kaggle.com/datasets/aslanahmedov/walmart-sales-forecast).
All data used are available in the "Data" folder of this repository.

 ## Code
 "WalmarSales.ipynb".
 
