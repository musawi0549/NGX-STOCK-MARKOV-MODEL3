import pandas as pd
import numpy as np

class MarkovStockModel:
    """
    A professional-grade implementation for estimating state transitions
    in financial time series using Discrete Time Markov Chains (DTMC).
    """
    def __init__(self, threshold=0.002):
        """
        Initialize the model parameters.
        :param threshold: The percentage change threshold to define Bull/Bear states.
        """
        self.threshold = threshold
        self.transition_matrix = None
        self.states = ['Bear', 'Stable', 'Bull']

    def _classify_state(self, return_val):
        """
        Helper method to classify a single return value into a state.
        """
        if pd.isna(return_val):
            return None
        if return_val > self.threshold:
            return 'Bull'
        elif return_val < -self.threshold:
            return 'Bear'
        else:
            return 'Stable'

    def fit(self, prices):
        """
        Fits the Markov Chain to historical price data.
        :param prices: List or Array of historical close prices.
        :return: The computed Transition Matrix.
        """
        # Create DataFrame for vectorized operations
        df = pd.DataFrame({'price': prices})
        
        # Calculate returns and classify states
        df['return'] = df['price'].pct_change()
        df['current_state'] = df['return'].apply(self._classify_state)
        df['next_state'] = df['current_state'].shift(-1)

        # Drop invalid transitions (e.g., first NaN or last row)
        valid_transitions = df.dropna(subset=['current_state', 'next_state'])

        # Compute the Transition Matrix (Count -> Probability)
        self.transition_matrix = pd.crosstab(
            valid_transitions['current_state'],
            valid_transitions['next_state'],
            normalize='index'
        )

        # Reindex to ensure all states exist (fixes "Sparse Matrix" bugs)
        self.transition_matrix = self.transition_matrix.reindex(
            index=self.states, columns=self.states, fill_value=0.0
        )
        
        return self.transition_matrix

    def predict(self, current_return):
        """
        Predicts the probabilities of the next state based on current return.
        """
        current_state = self._classify_state(current_return)
        if self.transition_matrix is not None and current_state in self.transition_matrix.index:
            return self.transition_matrix.loc[current_state]
        return None

# --- Example Usage (Include this in your "README.md") ---
if __name__ == "__main__":
    # Sample Data (Replace with real market data)
    prices = [100.5, 102.1, 101.8, 101.8, 104.2, 103.5, 105.0, 107.2, 106.8, 106.8, 110.1, 109.5]
    
    # Initialize and Fit Model
    model = MarkovStockModel(threshold=0.002)
    tm = model.fit(prices)
    
    print("Computed Transition Matrix:")
    print(tm)
