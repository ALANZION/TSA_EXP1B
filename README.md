# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 31-10-2026


### AIM:
To develop a Python program to convert non-stationary time series data into stationary data using Regular Differencing, Seasonal Adjustment, and Log Transformation on the International Airline Passenger dataset.

# Dataset Name : AirPassengers

### ALGORITHM:
1. Import the required libraries such as Pandas, NumPy, Matplotlib, and Statsmodels.
2. Read the AirPassengers dataset using Pandas.
3. Convert the Month column into datetime format and set it as the index.
4. Perform Regular Differencing to remove the trend from the data.
5. Perform Seasonal Adjustment to remove seasonal variations.
6. Apply Log Transformation to stabilize the variance.
7. Perform Log Transformation with Regular Differencing.
8. Perform Log Transformation with Regular and Seasonal Differencing.
9. Plot the original data and all transformed data for comparison.
10. Display the graphs and observe the changes.

### PROGRAM:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("/content/cardekho.csv")
print(data.head())

data['mileage(km/ltr/kg)'] = pd.to_numeric(data['mileage(km/ltr/kg)'], errors='coerce')
data = data.dropna(subset=['mileage(km/ltr/kg)'])
print(data.head())

data['mileage(km/ltr/kg)_diff'] = data['mileage(km/ltr/kg)'].diff()
print(data[['mileage(km/ltr/kg)', 'mileage(km/ltr/kg)_diff']].head(10))

period = 365
data['mileage(km/ltr/kg)_diff'] = data['mileage(km/ltr/kg)'].diff(period)
print(data[['mileage(km/ltr/kg)', 'mileage(km/ltr/kg)_diff']].head(370))

data['mileage(km/ltr/kg)_regular_seasonal_diff'] = (
    data['mileage(km/ltr/kg)'].diff().diff(period)
)
print(data[['mileage(km/ltr/kg)_regular_seasonal_diff']].head(370))

plt.subplot(5, 1, 1)
plt.plot(data['mileage(km/ltr/kg)'], label='Original', color='blue')
plt.title('Mileage Data')
plt.xlabel('Year')
plt.ylabel('Index')

plt.grid(True)
plt.legend()

plt.subplot(5, 1, 3)
plt.plot(data['mileage(km/ltr/kg)_diff'], label='Seasonal Differencing (365 days)', color='green')
plt.title('After Seasonal Differencing')
plt.ylabel('Seasonal Diff')

plt.grid(True)
plt.legend()

plt.subplot(5, 1, 4)
plt.plot(data['mileage(km/ltr/kg)_regular_seasonal_diff'], label='Regular & Seasonal Differencing', color='purple')
plt.title('After Regular and Seasonal Differencing')
plt.ylabel('Differenced Mileage')

plt.grid(True)
plt.legend()

plt.subplot(5, 1, 5)
plt.plot(data['mileage(km/ltr/kg)'], label='Original Mileage', alpha=0.5, color='blue')
plt.plot(data['mileage(km/ltr/kg)_log'], label='Log Transformation', color='red')
plt.title('Log Transformation vs Original Mileage')
plt.ylabel('Values')

plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
```
## OUTPUT:
# ORIGINAL DATA:
<img width="588" height="102" alt="image" src="https://github.com/user-attachments/assets/36595b53-e716-47df-9368-dfeb55183457" />
# SEASONAL ADJUSTMENT:
<img width="556" height="82" alt="image" src="https://github.com/user-attachments/assets/90e262d8-aa75-45bd-bac8-8989cd9cae50" />
# After Regular and Seasonal Differencing:
<img width="563" height="125" alt="image" src="https://github.com/user-attachments/assets/2da2602c-db37-4e0c-9310-0a4b80e72aef" />
# Log Transformation vs Original Mileage:
<img width="557" height="80" alt="image" src="https://github.com/user-attachments/assets/2895287f-5dec-4359-ba83-ca8982e083ba" />

## RESULT:
Thus, the Python program for converting non-stationary time series data into stationary data using Regular Differencing, Seasonal Adjustment, and Log Transformation on the International Airline Passenger dataset was successfully developed and executed.data.
