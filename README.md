# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 02/05/2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:

```py

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv("user_behavior_timeseries.csv")
data.columns = data.columns.str.strip()


data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data = data.groupby('Date').mean(numeric_only=True)

col = "App Usage Time"
series = data[col].values

series = series + np.random.randint(-20,20,len(series))

# ACF Calculation
N = len(series)
lags = range(20)

mean_val = np.mean(series)
var_val = np.var(series)

acf_values = []

for lag in lags:
    if lag == 0:
        acf_values.append(1)
    else:
        cov = np.sum((series[:-lag] - mean_val) * (series[lag:] - mean_val)) / N
        acf_values.append(cov / var_val)

# Plot
plt.figure(figsize=(10,5))
plt.stem(lags, acf_values)

plt.title("ACF - Output")
plt.xlabel("Lag")
plt.ylabel("Correlation")
plt.grid(True)

plt.show()

```
### OUTPUT:

![ACF](image.png)

### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
