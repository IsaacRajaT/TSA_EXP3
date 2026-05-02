# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
# Date: 02/05/2026
# Name: Isaac Raja T
# Reg No: 212224040123

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
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Load dataset
data = pd.read_csv('Truck_sales.csv')

# Convert 'Month-Year' column to datetime
data['Month-Year'] = pd.to_datetime(data['Month-Year'], format='%y-%b')

# Sort data (important for time series)
data.sort_values('Month-Year', inplace=True)

# Extract the series
series = data['Number_Trucks_Sold'].values

# Parameters
N = len(series)
lags = range(min(35, N))  # avoid exceeding data length

autocorr_values = []

mean_data = np.mean(series)
variance_data = np.var(series)

# Compute autocorrelation
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((series[:-lag] - mean_data) * (series[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)

# Plot
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title('Autocorrelation of Truck Sales Data')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```

### OUTPUT:
<img width="950" height="616" alt="image" src="https://github.com/user-attachments/assets/7fa262b1-4b2d-4896-b07b-340e78de5c70" />


### RESULT:
 Thus we have successfully implemented the auto correlation function in python.
