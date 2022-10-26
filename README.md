# Store-Item-Demand-Forecast
In this project, we will use several models to conduct demand forecast, models including Time Series
Demand forecast is an important issue in supply chain. With forecast of good accuracy, we can better schedule our material and capacity planning.

# Raw data
we have 5 years of transaction data (930,000 observasions) of 10 stores and 10 items they sell.
![image](https://user-images.githubusercontent.com/58899897/197666799-017afbca-5bdd-488c-8ae2-660ce1835cc6.png)



# EDA
First we can use info() function to have a basic understanding of the data.

![image](https://user-images.githubusercontent.com/58899897/197666672-c42fb2ca-d277-4e62-86ab-edaf49d76acb.png)

We focus only on the sales data, so we can use sotre and date to group the data. unstack is used to switch the x and y axis.

![image](https://user-images.githubusercontent.com/58899897/197673847-08c17238-4939-4bd7-a72e-61a80216e854.png)


We can use resample method tp visualize the performance of different length, such as a week, a month, or a season (3 months).  Resample is a convenient method for frequency conversion and resampling of time series.

![image](https://user-images.githubusercontent.com/58899897/197670269-6f7906d0-c7e9-4e2f-8ee1-81e4247fe931.png)
![image](https://user-images.githubusercontent.com/58899897/197670298-40bf035e-62af-46e3-a9ab-7fb888c8489d.png)

Now we have a basic understanding of the weekly, montly, and seasonal sales performance, but what if we want to know the performance of average trend or the 25 quartile? We could use the quantitle method to do this!

![image](https://user-images.githubusercontent.com/58899897/197674075-1e9a79c0-c515-4587-8d5c-79f7842ff1fa.png)

From the pictures we could see that stores share a general pattern and have highs and lows during the same periods of time.

We can check the seasonality of data. To do so,  we can use tsa.seasonal_decompose

![image](https://user-images.githubusercontent.com/58899897/197676103-93a7b2a6-3d73-47f9-8a72-d5fa0867b879.png)


we can also review the week-to-week difference by using diff function, which calculates the difference of a DataFrame element compared with another element in the DataFrame. There is a Nan in the first row, so we need to use iloc to remove that.

![image](https://user-images.githubusercontent.com/58899897/197677875-f9fe2160-e049-437d-b50e-072f3cf26ca8.png)

In the Time Series model, the “frequency” is the number of observations before the seasonal pattern repeats.
(If you are using tsa.seasonal_decompose, it is recommended to use "period" rather than "freq".)

Before applying the ARIMA model, we should make sure that the time series data is stationary. Stationary means that properties do not depend on the time at which the series is observed. Thus, time series with trends, or with seasonality, are not stationary — the trend and seasonality will affect the value of the time series at different times. To test that, we can use Augmented Dickey-Fuller unit root test. The Augmented Dickey-Fuller test can be used to test for a unit root in a univariate process in the presence of serial correlation.

![image](https://user-images.githubusercontent.com/58899897/197680849-d54af743-e087-4c8e-a146-781bc45c1658.png)

We can also use heat map to visualize the performances of items in each store. The greener color means the item accounts for more percentage of sales

![image](https://user-images.githubusercontent.com/58899897/197683721-89ff7549-cc2c-4a25-bda7-ae27a50af6de.png)

To better manage our inventory, we might want to know the performance of each day of the week, so we know how many items we should order. 

![image](https://user-images.githubusercontent.com/58899897/198027366-eeeac162-bec7-4e32-88ee-b67a13dc2a05.png)

If we want to know the performance of each item, we just need to use store to group data rather than store.

![image](https://user-images.githubusercontent.com/58899897/198028001-d6ffadb1-c52b-4380-90fc-ebe97cedbb48.png)

We could also use boxplot, but the result is not easy to interpret in this case.

![image](https://user-images.githubusercontent.com/58899897/198041196-0b7dd616-798a-4cac-a2b7-a34463021c74.png)


# Time Series Model

The Additive Model it is a model of data in which the effects of the individual factors are differentiated and added to model the data. 
y(t) = Trend + Seasonality + Noise

In the additive model, the behavior is linear where changes over time are consistently made by the same amount, like a linear trend. 

The Multiplicative Model
In this situation, trend and seasonal components are multiplied and then added to the error component. 
y(t) = Trend * Seasonality * Noise

Different from the additive model, the multiplicative model has an increasing or decreasing amplitude and/or frequency over time.

# ACF & PACF
Autocorrelation intends to measure the relationship between a variable’s present value and any past values. It’s a good idea to make an autocorrelation plot to compare the values of the autocorrelation function (ACF) against different lag sizes.

![image](https://user-images.githubusercontent.com/58899897/198070542-b9b503d9-6790-4898-be24-dbfca079806f.png)

![image](https://user-images.githubusercontent.com/58899897/198070637-95b7219f-ed89-4e71-b605-24fda482712d.png)

# Arima Model with p, d, q
We could use sta
For the ARIMA model, p is the number of autoregressive terms, d is the number of nonseasonal differences needed for stationarity, and. q is the number of lagged forecast errors in the prediction equation. We are going to use Time Series analysis (tsa) of Statsmodels with p = 6, d =1, and q =0.

![image](https://user-images.githubusercontent.com/58899897/198098390-928ecb5c-81df-462a-a8d1-ed7721e0aad6.png)

![image](https://user-images.githubusercontent.com/58899897/198100259-df8cd470-b90d-4a52-a86d-b5e123c73d3c.png)

As the figure shows that the performance is not very good, we could import more information to improve the performance.

![image](https://user-images.githubusercontent.com/58899897/198102831-20bcde2b-a127-41a5-99eb-c424e4efb7b2.png)


References:
https://sigmundojr.medium.com/seasonality-in-python-additive-or-multiplicative-model-d4b9cf1f48a7
