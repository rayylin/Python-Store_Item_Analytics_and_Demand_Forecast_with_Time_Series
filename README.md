# Store-Item-Demand-Forecast
In this project, we will use several models to conduct demand forecast, models including Time Series
Demand forecast is an important issue in supply chain. With forecast of good accuracy, we can better schedule our material and capacity planning.

# Raw data
we have 5 years of transaction data (930,000 observasions) of 10 stores and 10 items they sell.
![image](https://user-images.githubusercontent.com/58899897/195485834-fa88a5ee-a0a9-4b8c-bd0b-bcd2871a7369.png)

#EDA
We can check the seasonality of data first. To do so, we use resample method and with different length, such as a week, a month, or a season (3 months).

![image](https://user-images.githubusercontent.com/58899897/195486593-29ae77b0-4889-4958-ac54-9f3457f93acd.png)

#Time Series Model

The Additive Model it is a model of data in which the effects of the individual factors are differentiated and added to model the data. 
y(t) = Level + Trend + Seasonality + Noise
In the additive model, the behavior is linear where changes over time are consistently made by the same amount, like a linear trend. 

The Multiplicative Model
In this situation, trend and seasonal components are multiplied and then added to the error component. 
y(t) = Level * Trend * Seasonality * Noise
Different from the additive model, the multiplicative model has an increasing or decreasing amplitude and/or frequency over time.

![image](https://user-images.githubusercontent.com/58899897/195490332-2de48110-8b48-4020-acfd-1b1a00a60ee2.png)

In the Time Series model, the “frequency” is the number of observations before the seasonal pattern repeats.
(If you are using tsa.seasonal_decompose, it is recommended to use "period" rather than "freq".)



References:
https://sigmundojr.medium.com/seasonality-in-python-additive-or-multiplicative-model-d4b9cf1f48a7
