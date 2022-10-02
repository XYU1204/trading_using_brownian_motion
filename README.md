# trading_simulation_using_random_walk

* Explored the stochastic dealer model from a [paper](https://www.researchgate.net/publication/26284556_Solvable_stochastic_dealer_models_for_financial_markets) published on Physical Review E in 2008 during an global economical recession. The study aim for understanding the economical impacts of different trading behaviors. 
* Fetched real-time stock data from Yahoo using pandas_datareader API. Calculated statistical properties of 1-, 30-, 90-, and 180-day logistic change in Price. Forecast future stock prices using Regression and LSTM.
* 

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

## Building a Stochastic Dealer using Brownian Motion: Theory

The detailed theory on the stochastic dealer model can be found in the  [paper](https://www.researchgate.net/publication/26284556_Solvable_stochastic_dealer_models_for_financial_markets). Here, we brief summarize the idea on how to perform the dealer simulation. 

![image](https://user-images.githubusercontent.com/56236129/193455291-ce818f12-81ff-4208-8ce6-aecb6933e423.png)

We have two dealers $p_1(t)$ and $p_2(t)$ buying and selling a stock with each other. We characterize their positions through their mid-price, which is the average of their bid and ask prices. The price of each dealer follows an independent 1D random walk in time until the transaction condition, one dealer's bid price (minimum price willing to sell) is higher than the other deadler's ask price (maximum price willing to buy), is met (equation L1 shown in figure above). At this point, they exchange one unit of stock at a market price given by the average of the mid-prices (equation L2). Their mid-prices are then reset to this new Market price, and they start a new random walk.

![image](https://user-images.githubusercontent.com/56236129/193455405-51ccf0b4-13ab-47f2-b915-acd97e6581c6.png)

For each of the 1D random walk, the dealers make decision stochastically based on previous impression of the stock. The previous impression times behavior term is captured on the second term of L4. The previous impression is calculated in L6 as the moving average over the previous price changes. Here, $M$ represents how many previous price changes we are considering. The constant $d$ capture the behavior of the dealer: whether the dealer follow the previous trend (d>0), or trade contrary to the previous trend (d<0). 

![image](https://user-images.githubusercontent.com/56236129/193455715-63d7c2e6-aef4-439c-8f74-7b9171e658f6.png)

To capture the stochastic behavior between the two dealers and to make our calculation easier, we can simulate and visualize the trading process as a 2D random walk instead of two interative 1D random walk. D(t) in L7 represent the differences in the mid-price between the two dealers, and A(t) in L8 calculates the average of the mid-prices of the two dealers. For each move in 2D random walk, D(t) can be bootstrapped from the joint distribution of the steps from two dealers as shown in L9, and A(t) can be bootstrapped from the joint distribution plus the impression*behavior term. For simplicity of the study, we assume the two dealers have the exact same behavior, and same previous behavior about the stock.

## [Building a Stochastic Dealer using Brownian Motion: Simulation](https://github.com/XYU1204/trading_using_brownian_motion/blob/main/stochastic_trader.ipynb)

![image](https://user-images.githubusercontent.com/56236129/193456553-b188dc81-3e7e-4f60-9aab-f70ca96cab36.png)


## Future Work

There are few possible extensions to this project to make the dealer model simulation more close to real life stock exchange behavior:

1. In our model, we used only two dealers. However, in real stock exchange market, scalability
2. We assume both dealers in our simulation has the same behavior, either they are both trend followers, or both contratrians. However, in 


