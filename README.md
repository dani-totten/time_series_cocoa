# time series analysis of cocoa futures prices

# Summary
- Data collected from Yahoo! Finance, Jan 2010-February 2020 with ~250 trading days per year
- Models attempted include ARIMA, dynamic regression, neural net, random walk, time series + ARIMA and random walk
- identified strong autocorrelation, high volatility and a small but statistically significant effect of El Nino/La Nina on cocoa priced

# Main Findings
1) The adjusted closing price for each day is dependent upon the daily price of the previous trading day. The change in adjusted closing price from day to day is close to random.
2) El Niño and La Niña events have a moderately small but significant effect on the price of cocoa due to their impact on cocoa production.
3) There is volatility in the data and so large changes are more likely to occur in close proximity to one another.

These three findings together mean that it is difficult to accurately predict the future price of cocoa futures because the price at any given time is highly dependently on the price in the period before. Furthermore, the day to day change is more or less random but large changes, either positive or negative, are likely to follow large changes. Therefore, it can be difficult to try to determine if a price increase will be followed by additional price increases, or a large drop. This makes purchasing futures at a time of change difficult. However, since El Niño and La Niña can impact cocoa prices by impacting crop yields and forecasts for these patterns are often made far in advance, it could be prudent perform further research into purchasing cocoa futures when a strong El Niño effect is likely because the price of cocoa may rise as a consequence of warmer weather and stronger storms in equatorial regions.

Model			RMSE-train	RMSE-test	Passes model selection
Monthly	ARIMA(1,1,0)	135	       	  499	         Yes
Monthly	Dynamic Reg	134	          518	         Yes
Monthly	Neural Network	107	          310	         Yes
				
Daily	Random walk	        43	          263	         Yes
Daily	Reg + ARIMA	        43	          357	         Yes
Daily	Exp Smoothing 	    52	          177	         No


# Data - 3 ways
The data for July 2020 cocoa futures contracts came from Yahoo! Finance and included data from January 3, 2010 through February 26th, 2020. Only data after 2010 was ultimately used. Data only came from active trading days, of which there are approximately 250 per year because trading does not occur on weekends or holidays. Data cleansing was performed, and no anomolies were detected.

1) Daily adjusted closing price
Looking at the daily adjusted closing price shows day-to-day changes

2) Log returns
Log returns helps to show volatility in the data

3) Monthly average closing price
Taking the monthly average closing price can help to show long-term trends that may not be clear in noisy daily data. Additionally, I was interested in looking at the impact of El Nino and La Nina, which effect oceanic temperature and weather patterns for a period, on cocoa prices by impacting production
