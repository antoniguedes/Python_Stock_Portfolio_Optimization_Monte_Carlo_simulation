# Python_Stock_Portfolio_Optimization_Monte_Carlo_simulation

## 1. Presentation of the Project Overview
In this completion project, we perform portfolio analysis, visualization and optimization.
A portfolio is a collection of financial assets such as stocks, bonds, cash & real estate.
The purpose of a portfolio is to diversify the investments and manage risks.
Portfolio optimization is the process of selecting the optimal portfolio out a universe of possible portfolios with various asset allocations. The goal is to maximize risk-adjusted return of the portfolio, aka Maximize return for the lowest given risk (these portfolio possibilities can be plotted on a (x,y) diagram with x being risk, y being return: the most efficient portfolios for every given risk in x form a scatter line called the Markowitz efficient frontier, by the name of its inventor.
<img width="1193" height="319" alt="image" src="https://github.com/user-attachments/assets/3e775576-c1b7-4996-bdd6-d68040748587" />


## 2. Project steps
<img width="1282" height="568" alt="image" src="https://github.com/user-attachments/assets/74f812b4-fa72-4de3-95a8-e278527aba6d" />


## 3. Presentation of the dataset
The dataset is composed of 10 stocks of the US S&P500 index, with raw data as their daily stock prices from 2014 – 2022. 
The stock prices are composed of different prices throughout the day: Open High Low Close Ajusted Close. For the purpose of analysis we will use the Adjusted Close price, after considering  stock splits and dividends.
- AMZN: Amazon Inc. - Multinational tech company focusing on e-commerce, cloud computing, and artificial intelligence
- JPM: JPMorgan Chase and Co. - Multinational investment bank and financial services holding company
- META: Meta Platforms, formerly named Facebook Inc. - META owns Facebook, Instagram, and WhatsApp
- PG: Procter and Gamble (P&G) - Multinational consumer goods corporation
- GOOG: Google (Alphabet Inc.) - Multinational company that focuses on search engine tech, e-commerce, Cloud and AI 
- CAT: Caterpillar - World's largest construction-equipment manufacturer
- PFE: Pfizer Inc. - Multinational pharmaceutical and biotechnology corporation
- EXC: Exelon - An American Fortune 100 energy company 
- DE: Deere & Company (John Deere) - Manufactures agricultural machinery and heavy equipment
- JNJ: Johnson & Johnson - A multinational corporation that develops medical devices and pharmaceuticals

In the first part of the project, we will uses only AMZN for the showcase of the visualization power of Python and its libraries like matplotlib, plotly express, seaborn.
Then for the portfolio simulation engine and optimization runs, we will come back to the 10 stocks portfolio.

## Chapter 4. Python Libraries used in the project for computation and visualization
`import np as numpy  
import pd as pandas`  
import datetime module that comes pre-installed in Python   
`datetime offers classes that work with date & time information  
import datetime as dt`  

For example use the info() methode to obtain information about the Pandas DataFrame such as data types, memory utilization...    
`stock_df.info()`   
Use the describe() method to obtain a statistical summary about the data: average, median, min, max ...    
`stock_df.describe().round(2)` 

<img width="1303" height="547" alt="image" src="https://github.com/user-attachments/assets/395fa2fc-c634-4c07-b0f7-f29f405464dc" />

Matplotlib is a comprehensive data visualization library in Python 
Seaborn is a visualization library that sits on top of matplotlib and offers enhanced features 
plotly.express module contains functions that can create interactive figures using a few lines of code

`import matplotlib.pyplot as plt  
!pip install seaborn  
import seaborn as sns  
import plotly.express as px`

Link to Matplotlib Documentation: https://matplotlib.org/   
Link to Seaborn Documentation: https://seaborn.pydata.org/   
Link to Plotly Documentation: https://plotly.com/python/  


<img width="1303" height="696" alt="image" src="https://github.com/user-attachments/assets/e0fbe33e-a4c7-4c7c-8724-40f35d2d5f37" />


# 5. Use of visualizations in this project
- Plot a Line Plot Using Plotly Express  
`fig = px.line(title = 'Amazon.com, Inc. (AMZN) Adjusted Closing Price [$]')
fig.add_scatter(x = stock_df['Date'], y = stock_df['Adj Close'], name = 'Adj Close')`

- Plot trading volume 
plot_financial_data(stock_df.iloc[:,[0,5]], 'Amazon.com, Inc. (AMZN) Trading Volume')

<img width="1763" height="264" alt="image" src="https://github.com/user-attachments/assets/37fb9fed-6327-400d-ae0a-e7416ad1fe50" />

<img width="1315" height="700" alt="image" src="https://github.com/user-attachments/assets/6924ac2e-f954-45b3-b46f-a35f1348d8c4" />


- Plot heatmap for stocks daily returns using plotly express    
Compare META to JNJ daily returns histograms  
`fig = px.histogram(daily_returns_df.drop(columns = ['Date']))  
fig.update_layout({'plot_bgcolor': "white"})`

<img width="777" height="665" alt="image" src="https://github.com/user-attachments/assets/991c0d89-b00a-437f-a2d9-b4b0fdc66c9e" />

- Plot the Pairplot between stocks daily returns
sns.pairplot(daily_returns_df);
<img width="2469" height="2455" alt="image" src="https://github.com/user-attachments/assets/3bbe78fc-bf4f-445c-8ad0-fa7ea57e9dbb" />

 
- Function to scale stock prices based on their initial starting price
The objective of this function is to set all prices to start at a value of 1 
`def price_scaling(raw_prices_df):
    scaled_prices_df = raw_prices_df.copy()
    for i in raw_prices_df.columns[1:]:
          scaled_prices_df[i] = raw_prices_df[i]/raw_prices_df[i][0]
    return scaled_prices_df`


# 6. DEFINE A FUNCTION THAT GENERATES RANDOM PORTFOLIO WEIGHTS

Let's create an array that holds random portfolio weights
Note that portfolio weights must add up to 1 
'import random

def generate_portfolio_weights(n):  '
<img width="872" height="428" alt="image" src="https://github.com/user-attachments/assets/e3d8842e-b939-4909-a5ac-8bc88312e2de" />


#7.PERFORM ASSET ALLOCATION & CALCULATE PORTFOLIO DAILY VALUE/RETURN

<img width="855" height="412" alt="image" src="https://github.com/user-attachments/assets/e05600cd-6536-41e0-962c-970c84e69410" />

<img width="865" height="449" alt="image" src="https://github.com/user-attachments/assets/0a110534-c304-4b86-8df9-dab2567a8e03" />

<img width="851" height="398" alt="image" src="https://github.com/user-attachments/assets/20442329-ffc3-4b66-a7a9-785a876bc85c" />

<img width="851" height="398" alt="image" src="https://github.com/user-attachments/assets/9a9ded81-cb1f-4762-9cc9-bbae4e824422" />


- Let's define the "weights" list similar to the slides
weights = [0.032266, 0.094461, 0.117917, 0.132624, 0.145942, 0.128299, 0.10009, 0.007403, 0.088581, 0.152417]
weights

Assume that we have $1,000,000 that we would like to invest in one or more of the selected stocks  
Let's create a function that receives the following arguments:   
      # (1) Stocks closing prices  
      # (2) Random weights   
      # (3) Initial investment amount   
The function will return a DataFrame that contains the following:
      # (1) Daily value (position) of each individual stock over the specified time period   
      # (2) Total daily value of the portfolio    
      # (3) Percentage daily return   
                
    def asset_allocation(df, weights, initial_investment):
    portfolio_df = df.copy()

    Scale stock prices using the "price_scaling" function that we defined earlier (Make them all start at 1)
    scaled_df = price_scaling(df)
  
    for i, stock in enumerate(scaled_df.columns[1:]):
        portfolio_df[stock] = scaled_df[stock] * weights[i] * initial_investment

    Sum up all values and place the result in a new column titled "portfolio value [$]" 
   Note that we excluded the date column from this calculation
    portfolio_df['Portfolio Value [$]'] = portfolio_df[portfolio_df != 'Date'].sum(axis = 1, numeric_only = True)
            
    # Calculate the portfolio percentage daily return and replace NaNs with zeros
    portfolio_df['Portfolio Daily Return [%]'] = portfolio_df['Portfolio Value [$]'].pct_change(1) * 100 
    portfolio_df.replace(np.nan, 0, inplace = True)
    return portfolio_df

<img width="839" height="452" alt="image" src="https://github.com/user-attachments/assets/7b544f5f-c467-4341-8f3b-14370bad5972" />


8. DEFINE THE "SIMULATION" FUNCTION THAT PERFORMS ASSET ALLOCATION, AND CALCULATES KEY PORTFOLIO METRICS

<img width="839" height="452" alt="image" src="https://github.com/user-attachments/assets/1e6cc378-6e37-448c-9858-9c2b8656ca4f" />

<img width="829" height="433" alt="image" src="https://github.com/user-attachments/assets/93be1f99-6331-470d-a4aa-588d8d52cd27" />

<img width="749" height="429" alt="image" src="https://github.com/user-attachments/assets/e0f6dfcb-5082-4a98-b64b-657a5949dbfa" />

This is the core function of the project in Pyton

This is the core of the code for making the MC simulation:

Let's define the simulation engine function 
The function receives: 
    # (1) portfolio weights
    # (2) initial investment amount
The function performs asset allocation and calculates portfolio statistical metrics including Sharpe ratio
The function returns: 
    # (1) Expected portfolio return 
    # (2) Expected volatility 
    # (3) Sharpe ratio 
    # (4) Return on investment 
    # (5) Final portfolio value in dollars


`def simulation_engine(weights, initial_investment):
    # Perform asset allocation using the random weights (sent as arguments to the function)
    portfolio_df = asset_allocation(close_price_df, weights, initial_investment)
  
    # Calculate the return on the investment 
    # Return on investment is calculated using the last final value of the portfolio compared to its initial value
    return_on_investment = ((portfolio_df['Portfolio Value [$]'][-1:] - 
                             portfolio_df['Portfolio Value [$]'][0])/ 
                             portfolio_df['Portfolio Value [$]'][0]) * 100
  
    # Daily change of every stock in the portfolio (Note that we dropped the date, portfolio daily worth and daily % returns) 
    portfolio_daily_return_df = portfolio_df.drop(columns = ['Date', 'Portfolio Value [$]', 'Portfolio Daily Return [%]'])
    portfolio_daily_return_df = portfolio_daily_return_df.pct_change(1) 
  
    # Portfolio Expected Return formula
    expected_portfolio_return = np.sum(weights * portfolio_daily_return_df.mean() ) * 252
  
    # Portfolio volatility (risk) formula
    # The risk of an asset is measured using the standard deviation which indicates the dispertion away from the mean
    # The risk of a portfolio is not a simple sum of the risks of the individual assets within the portfolio
    # Portfolio risk must consider correlations between assets within the portfolio which is indicated by the covariance 
    # The covariance determines the relationship between the movements of two random variables
    # When two stocks move together, they have a positive covariance when they move inversely, the have a negative covariance 

    covariance = portfolio_daily_return_df.cov() * 252 
    expected_volatility = np.sqrt(np.dot(weights.T, np.dot(covariance, weights)))`

    # Check out the chart for the 10-years U.S. treasury at https://ycharts.com/indicators/10_year_treasury_rate
   ` rf = 0.03 # Try to set the risk free rate of return to 1% (assumption)`

    # Calculate Sharpe ratio
   ` sharpe_ratio = (expected_portfolio_return - rf)/expected_volatility 
    return expected_portfolio_return, expected_volatility, sharpe_ratio, portfolio_df['Portfolio Value [$]'][-1:].values[0], return_on_investment.values[0]`

9. RUN MONTE CARLO SIMULATIONS

<img width="819" height="427" alt="image" src="https://github.com/user-attachments/assets/74db577f-5b91-40f1-8b6d-cd68bcc716ea" />

10. PERFORM PORTFOLIO OPTIMIZATION, BY DRAWING MARKOWITZ EFFICIENT FRONTIER 

<img width="838" height="449" alt="image" src="https://github.com/user-attachments/assets/c7cdca74-6078-4a11-8bb5-9d17255c4dcf" />

print('Best Portfolio Metrics Based on {} Monte Carlo Simulation Runs:'.format(sim_runs))
print('  - Portfolio Expected Annual Return = {:.02f}%'.format(optimal_portfolio_return * 100))
print('  - Portfolio Standard Deviation (Volatility) = {:.02f}%'.format(optimal_volatility * 100))
print('  - Sharpe Ratio = {:.02f}'.format(optimal_sharpe_ratio))
print('  - Final Value = ${:.02f}'.format(highest_final_value))
print('  - Return on Investment = {:.02f}%'.format(optimal_return_on_investment))

**Here are the results of the 10,000 MC simulations:
Best Portfolio Metrics Based on 10000 Monte Carlo Simulation Runs:
  - Portfolio Expected Annual Return = 18.05%
  - Portfolio Standard Deviation (Volatility) = 18.50%
  - Sharpe Ratio = 0.81
  - Final Value = $3,792,621.73
  - Return on Investment = 279.26% from 2014 to 2022**


Plot volatility vs. return for all simulation runs
Highlight the volatility and return that corresponds to the highest Sharpe ratio
import plotly.graph_objects as go
fig = px.scatter(sim_out_df, x = 'Volatility', y = 'Portfolio_Return', color = 'Sharpe_Ratio', size = 'Sharpe_Ratio', hover_data = ['Sharpe_Ratio'] )
fig.update_layout({'plot_bgcolor': "white"})
fig.show()


Use this code if Sharpe ratio is negative  
fig = px.scatter(sim_out_df, x = 'Volatility', y = 'Portfolio_Return', color = 'Sharpe_Ratio', hover_data = ['Sharpe_Ratio'] )  

Use this code if Sharpe ratio is negative 
fig = px.scatter(sim_out_df, x = 'Volatility', y = 'Portfolio_Return', color = 'Sharpe_Ratio', hover_data = ['Sharpe_Ratio'] )  


<img width="899" height="256" alt="image" src="https://github.com/user-attachments/assets/6695eac1-cbc0-410e-a237-f1b9acc0a0f5" />




























































