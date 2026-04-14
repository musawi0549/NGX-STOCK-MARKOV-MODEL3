# Stock Market State Transition Analysis
## Using Discrete-Time Markov Chains (DTMC)

This repository contains a Python implementation of a First-Order Markov Chain used to model and predict stock market state transitions (Bull, Bear, and Stable regimes).

### 🚀 Overview
The model discretizes historical price returns into categorical states based on a volatility threshold. It then computes a transition probability matrix to estimate the likelihood of future market states.

### 🛠️ Key Features
- **Object-Oriented Design**: Encapsulated in a reusable `MarkovStockModel` class.
- **Robustness**: Handles sparse data using reindexing to ensure matrix consistency.
- **Flexibility**: Adjustable return thresholds for different asset classes.

### 📈 Future Research Directions
I am currently exploring ways to expand this model for my MSc research, including:
- **Hidden Markov Models (HMM)** to identify latent market regimes.
- **GARCH Integration** for dynamic volatility thresholding.
- **Bayesian Inference** for real-time probability updates.

### 📂 How to Run
1. Ensure you have `pandas` and `numpy` installed.
2. Clone this repo: `git clone <your-repo-link>`
3. Run the model: `python markov_model.py`
