# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
Import the packages
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.ar_model import AutoReg
from sklearn.metrics import mean_squared_error
```
Read the Airline Passengers dataset from a CSV file
```
data = pd.read_csv("/content/airline.csv")
```
Display the shape and the first 50 rows of the dataset
```
print("Shape of the dataset:", data.shape)
print("First 50 rows of the dataset:")
print(data.head(50))
```
Plot the first 50 values of the 'International' column
```
plt.plot(data['International '].head(50))
plt.title('First 50 values of the "International" column')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.show()
```
Perform rolling average transformation with a window size of 5
```
rolling_mean_5 = data['International '].rolling(window=5).mean()
```
Display the first 10 values of the rolling mean
```
print("First 10 values of the rolling mean with window size 5:")
print(rolling_mean_5.head(10))
```
Perform rolling average transformation with a window size of 10
```
rolling_mean_10 = data['International '].rolling(window=10).mean()
```
Plot the original data and fitted value (rolling mean with window size 10)
```
plt.plot(data['International '], label='Original Data')
plt.plot(rolling_mean_10, label='Rolling Mean (window=10)')
plt.title('Original Data and Fitted Value (Rolling Mean)')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.legend()
plt.show()
```
Fit an AutoRegressive (AR) model with 13 lags
```
lag_order = 13
model = AutoReg(data['International '], lags=lag_order)
model_fit = model.fit()
```
Plot Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF)
```
plot_acf(data['International '])
plt.title('Autocorrelation Function (ACF)')
plt.show()

plot_pacf(data['International '])
plt.title('Partial Autocorrelation Function (PACF)')
plt.show()
```
Make predictions using the AR model
```
predictions = model_fit.predict(start=lag_order, end=len(data)-1)
```
Compare the predictions with the original data
```
mse = mean_squared_error(data['International '][lag_order:], predictions)
print('Mean Squared Error (MSE):', mse)
```
Plot the original data and predictions
```
plt.plot(data['International '][lag_order:], label='Original Data')
plt.plot(predictions, label='Predictions')
plt.title('AR Model Predictions vs Original Data')
plt.xlabel('Index')
plt.ylabel('International Passengers')
plt.legend()
plt.show()
```


### OUTPUT:
Plot the original data and fitted value

![image](https://github.com/user-attachments/assets/1a2fb5e4-aa2e-4d4f-9328-81e99afb42da)

Plot Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF)

![image](https://github.com/user-attachments/assets/539f665b-f0fa-4ad0-91ba-baf6af189783)

![image](https://github.com/user-attachments/assets/35d88261-b246-4045-b6d4-b2e868944c44)

Plot the original data and predictions

![image](https://github.com/user-attachments/assets/093eb50c-b272-4970-85a2-31ddb3b6132b)



### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
