# Ex.No: 1B  CONVERSION OF NON STATIONARY TO STATIONARY DATA

### Developed by : M.Pranathi
### Register no : 212222240064
### Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller

data=pd.read_csv('supermarketsales.csv')

data['Date'] = pd.to_datetime(data['Date'])
data = data.sort_values('Date')
data = data.drop_duplicates(subset='Date')
data.set_index('Date', inplace=True)
data = data.reset_index()

REGULAR DIFFERENCING:

data['Diff_Total'] = data['Total'].diff()
data = data.dropna(subset=['Diff_Total'])
data.set_index('Date', inplace=True)
plt.figure(figsize=(10,6))
plt.plot(data['Diff_Total'], label='Differenced')
plt.title('Regular Differencing')
plt.legend()
plt.show()
adf_test = adfuller(data['Diff_Total'])
print('ADF Statistic:', adf_test[0])
print('p-value:', adf_test[1])

SEASONAL ADJUSTMENT:

seasonal_period = 1
data['Seasonal_Diff_Total'] = data['Total'].diff(seasonal_period).dropna()
plt.figure(figsize=(10,6))
plt.plot(data['Seasonal_Diff_Total'], label='Seasonal Differenced')
plt.title('Seasonal Differencing')
plt.legend()
plt.show()
adf_test = adfuller(data['Seasonal_Diff_Total'].dropna())
print('ADF Statistic:', adf_test[0])
print('p-value:', adf_test[1])

LOG TRANSFORMATION:

data['Log_Total'] = np.log(data['Total'])
plt.figure(figsize=(10,6))
plt.plot(data['Log_Total'], label='Log Transformed')
plt.title('Log Transformation')
plt.legend()
plt.show()
adf_test = adfuller(data['Log_Total'].dropna())
print('ADF Statistic:', adf_test[0])
print('p-value:', adf_test[1])
```
### OUTPUT:

REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/1ea2fa7b-6193-4d95-bd8c-c3a869b7c368)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/32dd76ed-b0fc-4397-9b5f-fe5e082bb669)

LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/7725aca7-6fad-4785-b632-66c9949beadf)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
