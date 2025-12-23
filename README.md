import pandas as pd
import numpy as np

data = {
    'Date': pd.date_range(start='2023-01-01', periods=12, freq='D'),
    'Close_Price': [100.5, 102.1, 101.8, 101.8, 104.2, 103.5, 105.0, 107.2, 106.8, 106.8, 110.1, 109.5]
}
df = pd.DataFrame(data)

df['Return'] = df['Close_Price'].pct_change()

def classify_state(ret):
    if pd.isna(ret):
        return None
    if ret > 0.002:
        return 'Bull'
    elif ret < -0.002:
        return 'Bear'
    else:
        return 'Stable'

df['Current_State'] = df['Return'].apply(classify_state)
df['Next_State'] = df['Current_State'].shift(-1)

states = df.dropna(subset=['Current_State', 'Next_State'])
transition_matrix = pd.crosstab(
    states['Current_State'],
    states['Next_State'],
    normalize='index'
)

print(transition_matrix)