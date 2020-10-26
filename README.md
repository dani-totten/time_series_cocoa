# Time Series Analysis of Cocoa Futures Prices

# Summary
- Daily Data, 2493 data points from Jan. 3, 2010 – Feb. 26, 2020 from Yahoo! Finance
- Train: 2455 observation, Jan 3, 2010- Dec 31, 2019
- Test: 38 observations, Jan 2, 2020 – Feb. 26, 2020
- Models attempted include ARIMA, dynamic regression, neural net, random walk, time series + ARIMA and random walk
- identified strong autocorrelation, high volatility and a small but statistically significant effect of El Nino/La Nina on cocoa priced

# Main Findings
1) The adjusted closing price for each day is dependent upon the daily price of the previous trading day. The change in adjusted closing price from day to day is close to random.
2) El Niño and La Niña events have a moderately small but significant effect on the price of cocoa due to their impact on cocoa production.
3) There is volatility in the data and so large changes are more likely to occur in close proximity to one another.
4) There was a sharp increase in price during the test period, so testing reflected a particularly difficult time period for models to predict

These three findings together mean that it is difficult to accurately predict the future price of cocoa futures because the price at any given time is highly dependently on the price in the period before. Furthermore, the day to day change is more or less random but large changes, either positive or negative, are likely to follow large changes. Therefore, it can be difficult to try to determine if a price increase will be followed by additional price increases, or a large drop. This makes purchasing futures at a time of change difficult. However, since El Niño and La Niña can impact cocoa prices by impacting crop yields and forecasts for these patterns are often made far in advance, it could be prudent perform further research into purchasing cocoa futures when a strong El Niño effect is likely because the price of cocoa may rise as a consequence of warmer weather and stronger storms in equatorial regions.

|Model	|RMSE-train	|RMSE-test	|Passes model selection|
|:---	|:---		|:---		|:---		|
|Monthly|	ARIMA(1,1,0)	|135|499 Yes|
|Monthly	Dynamic Regression + ARIMA(1,1,0) |134|518|Yes|
|Monthly	Neural Network	|107|310|Yes|
|Daily	Random walk	|43|263	|Yes|
|Daily	Dynamic Regression + ARIMA	|43|357|Yes|
|Daily	Exponential Smoothing|52|177|No|


# Data - 3 ways
The data for July 2020 cocoa futures contracts came from Yahoo! Finance and included data from January 3, 2010 through February 26th, 2020. Only data after 2010 was ultimately used. Data only came from active trading days, of which there are approximately 250 per year because trading does not occur on weekends or holidays. Data cleansing was performed, and no anomolies were detected.

1) Daily adjusted closing price

Looking at the daily adjusted closing price shows day-to-day changes.

![](https://github.com/dani-totten/time_series_cocoa/blob/main/daily_adj_closing_price.png)

Methods for looking at daily adjusted closing price
- random walk
- exponential smoothing
- time series regression with ARIMA to model residual autocorrelation.

No model did a particularly good job of forecasting futures pricing. A first difference yielded a fairly noisy plot, so a random walk was attempted. This had one of the lowest RMSE for the training set, but performed poorly on the test set. Exponential smoothing captured the sharp increase, but weakened as model forecasted further into the future. 3rd order trend in time series regression best captured the series in training and performed reasonably well, but the model incorrectly predicted a decline in the test period, rather than an increase.

![](https://github.com/dani-totten/time_series_cocoa/blob/main/forecast_daily.png)

2) Monthly average closing price

Taking the monthly average closing price can help to show long-term trends that may not be clear in noisy daily data. Additionally, I was interested in looking at the impact of El Nino and La Nina, which effect oceanic temperature and weather patterns for a period, on cocoa prices by impacting production. El Niño and la Niña data were added to the monthly data based on research that the temperamental cocoa plant can be significantly impacted by weather changes. El Niño  events are marked by warmer water in the Pacific and La Niña events are marked by cooler water in the Pacific. The data came from The data came from Golden Gate Weather Services and is based on the Oceanic Nino Index to classify periods of El Niño  and La Niña weather events into weak (1), moderate (2), strong (3) and very strong (4). Periods without these events are marked with a 0.  This data was added to the monthly data as an ordered factor with El Niño  and La Niña considered as separate variables than cannot occur concurrently.

![](https://github.com/dani-totten/time_series_cocoa/blob/main/monthly_avg_closing.png)

Methods for average monthly closing price
- ARIMA(1,1,0)
- ARIMA(1,1,0) with dynamic regression
- Recurrent Neural Network

The ARIMA(1,1,0) aka first-differenced autoregressive model adequately accounted for all residual autocorrelation (based on Box-Ljung test of residuals) with moderate training set RMSE, but was poor at predicting the test set. Since regression analysis showed a statistically significant relationship between prices and El Nino/La Nina months (El Nino causing slight increase in price, La Nina causing slight decrease in price). Layering these two models had almost no impact on RMSE in the trianing set, but had a slightly higher RMSE in the test set. A neural network that included El Nino/La Nina was overall better than either of the previous two models with lower training and test RMSE.

![](https://github.com/dani-totten/time_series_cocoa/blob/main/monthly_forecast.png)

2) Log returns

Log returns helps to show volatility in the data. Strong autocorrelation can be seen in the ACF plot, indicating volatility in the model.

![](https://github.com/dani-totten/time_series_cocoa/blob/main/sqd_log_ret.png)

