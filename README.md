# NGX-STOCK-MARKOV-MODEL3
Statistical modelling  of the Nigerian stock market (NGX) Using Discrete time Markov chains To predict State transitions and market stability 
Modelling Stock Market State Transitions: A Case Study of the NGX
Project Overview
This project applies Stochastic Processes  to the Nigerian financial market. By utilizing  Discrete Time Markov Chains (DTMC) I analyzed historical stock data to calculate the probability of the market transitioning between three specific states Bull,Bear, and Stable.
Key Features
Data Cleaning: Processed raw NGX historical data using  SQL and Python.
State Classification: Developed an algorithm to categorize daily market returns based on volatility thresholds.
Transition Matrix: Constructed a probability matrix ($P$) to visualize the likelihood of market shifts.
Steady State Analysis: Calculated the long run Stationary Distribution of the market.
 Mathematical Model
The model assumes the Markov Property, where the probability of tomorrow's state depends solely on today's closing price.
P(X_{n+1} = j | X_n = i) = p_{ij}
