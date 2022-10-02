# trading_simulation_using_brownian_motion

* Explored the stochastic dealer model from a [paper](https://www.researchgate.net/publication/26284556_Solvable_stochastic_dealer_models_for_financial_markets) published on Physical Review E in 2008 during an global economical recession. The study aim for understanding the economical impacts of different trading behaviors. 
* Fetched real-time stock data from Yahoo using pandas_datareader API. Calculated statistical properties of 1-, 30-, 90-, and 180-day logistic change in Price. Forecast future stock prices using Regression and LSTM.
* Portfolio Optimization using 2000 Monte Carlo Simulations.
* Optimize arbitrary initial portfolio weights by maximizing sharpe_ratio using SLSQP (Sequential Least Squares Programming). 
* On average, the optimizer increased expected annual return by 73.99%, and increase expected sharpe ratio by 25.40%, making the investment more profitable and less violatile at the same time.

## Code and Resources Used 
**Python Version:** 3.7  
**Packages:** pandas, numpy, scipy, sklearn, matplotlib, seaborn, plotly

## [Exploratory Data Analysis and Simple Portfolio Statistics](https://github.com/XYU1204/trading_using_brownian_motion/blob/main/EDA.ipynb)
We fetched recent 10 years of stock data for S&P500 from Yahoo using pandas_datareader API. We used S&P500 instead of stocks from specific companies because S&P500 is more representative of the global economics.

![image](https://user-images.githubusercontent.com/56236129/193451197-ced0b604-1061-4803-b55f-4918c9c1b633.png)

Stock price and trading volume over time.

Next, we calculated the 1-, 30-, 90-, and 180- day return rate for the stock using logistic change $G_\tau(t) \equiv \log{P(t+\tau)} - \log{P(t)}$. Where $P(t)$ is the price on day t, and $P(t+\tau)$ is the price on day $t+\tau$.

![image](https://user-images.githubusercontent.com/56236129/193451219-555b4b9a-5f88-4a42-b307-c969dbd0aa99.png)

Distribution of 1-, 30-,  90-, and 180-day return rate.

![image](https://user-images.githubusercontent.com/56236129/193451566-ac95ef38-febf-4995-aa22-03296dd8a561.png)

Probability density function for 1-, 30-, 90-, and 180-day return rate. The probability density follows Gaussian distribution.

## [Stock price prediction using Regression and LSTM](https://github.com/XYU1204/portfolio_optimization/blob/main/portfolio_optimization.ipynb)

We divided the 10 year stock data into 80% training and 20% testing. We aim for finding a way to predict future days stock prices using stock data from past days. To do this, we tried both simple regression model and LSTM algorithm.

![image](https://user-images.githubusercontent.com/56236129/193452277-2e90e44a-103d-4e12-9b41-51f51d485191.png)

Here, we don't see much a difference between the performance of a simple regression model and LSTM algorithm.

![image](https://user-images.githubusercontent.com/56236129/193452436-18b5855e-275b-4680-88c6-da46f9f1473b.png)

We plot the difference between predicted price and real stock closing price. It turned out simple regression model works better than LSTM algorithm. This tells us more complex model doesn't necessarily model data better than simple physical models. Data insights are important!

## [Building a Stochastic Dealer using Brownian Motion](https://github.com/XYU1204/trading_using_brownian_motion/blob/main/stochastic_trader.ipynb)
To evaluate the performance of the optimizer we created, we randomly generated 50 initialization feed to the optimizer. We compared the percentage increase in annual return and in sharpe ratio before and after optimization. On average, our optimizer shows 73.99% increase in expected annual return, and 25.40% increase in expected sharpe ratio. 
