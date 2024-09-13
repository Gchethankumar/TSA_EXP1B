
#### Developed By : G.Chethan kumar
#### Register no. : 212222240022
#### Date: 

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

### Load the data
data = pd.read_csv('india-gdp.csv',nrows=100)

### Convert 'date' to datetime format
data['date'] = pd.to_datetime(data['date'], format='%d-%m-%Y')

### Group by date and calculate the average money spent per day
daily_average = data.groupby('date')['AnnualChange'].mean().reset_index()
### Log transformation
daily_average['Log_Change'] = np.log(daily_average['AnnualChange'])

### Regular differencing
daily_average['Diff_Log_Change'] = daily_average['Log_Change'].diff()

### Seasonal differencing (assuming daily data with weekly seasonality, period=7)
daily_average['Seasonal_Diff_Log_Change'] = daily_average['Log_Change'].diff(7)

### Plotting
plt.figure(figsize=(14, 12))

### Original data
plt.subplot(4, 1, 1)
plt.plot(daily_average['date'], daily_average['AnnualChange'], label='Original')
plt.title('Original Data')
plt.ylabel('Average Annual % Change')
plt.grid()

### Log transformed data
plt.subplot(4, 1, 2)
plt.plot(daily_average['date'], daily_average['Log_Change'], label='Log Transformed', color='orange')
plt.title('Log Transformed Data')
plt.ylabel('Log(Average Annual % Change)')
plt.grid()

### Regular differenced data
plt.subplot(4, 1, 3)
plt.plot(daily_average['date'], daily_average['Diff_Log_Change'], label='Differenced', color='green')
plt.title('Differenced Log Data')
plt.ylabel('Diff(Log(Average Annual % Change))')
plt.grid()
```

### OUTPUT:

#### REGULAR DIFFERENCING:

ORIGINAL DATA: 

![Screenshot 2024-09-13 091459](https://github.com/user-attachments/assets/efc79121-2330-4bc1-9753-a2452fe3bd91)

REGULAR DIFFERENCING:

![Uploading Screenshot 2024-09-13 091508.png…]()

SEASONAL ADJUSTMENT:

![Uploading Screenshot 2024-09-13 091515.png…]()

LOG TRANSFORMATION:

![Uploading Screenshot 2024-09-13 091522.png…]()


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger data.
