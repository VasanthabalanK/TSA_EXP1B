# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 01-09-2025

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
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("/content/jee_mains_2013_to_2025_top_30_ranks.csv")
data
data['Year'] = pd.to_datetime(data['Year'], format='%Y')
yearly_data = data.groupby('Year')['Rank'].mean()

rank_diff = yearly_data.diff()

result = seasonal_decompose(yearly_data, model='additive', period=2)
rank_sea_diff = result.resid

rank_log = np.log(yearly_data)
rank_log_diff = rank_log.diff()

result_log = seasonal_decompose(rank_log_diff.dropna(), model='additive', period=2)
rank_log_seasonal_diff = result_log.resid

plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(yearly_data, label='Original (Mean Rank per Year)')
plt.legend(loc='best')
plt.title('Original JEE Mean Rank Data')
plt.xlabel('Year')
plt.ylabel('Rank')
plt.subplot(6, 1, 2)
plt.plot(rank_diff, label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Rank')
plt.subplot(6, 1, 3)
plt.plot(rank_sea_diff, label='Seasonal Adjustment (Residual)')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Residual')
plt.subplot(6, 1, 4)
plt.plot(rank_log, label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Rank)')
plt.subplot(6, 1, 5)
plt.plot(rank_log_diff, label='Log Transformation + Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Log Difference')
plt.subplot(6, 1, 6)
plt.plot(rank_log_seasonal_diff, label='Log Transformation + Differencing + Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing + Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Residual')

plt.tight_layout()
plt.show()
plt.figure(figsize=(12, 6))
plt.plot(yearly_data, label='Original (Mean Rank)')
plt.plot(rank_diff, label='Differenced')
plt.plot(rank_log_diff, label='Log Differenced')
plt.legend(loc='best')
plt.title("JEE Rank Transformations (Yearly Aggregated)")
plt.show()
```

### OUTPUT:


REGULAR DIFFERENCING:

<img width="578" height="138" alt="12" src="https://github.com/user-attachments/assets/138da680-3fb7-4d93-95c7-3083efb536d3" />

SEASONAL ADJUSTMENT:
<img width="554" height="138" alt="13" src="https://github.com/user-attachments/assets/50fa001e-99cc-40cd-9df2-35ea2333f4b1" />


LOG TRANSFORMATION:
<img width="575" height="138" alt="14" src="https://github.com/user-attachments/assets/56b9ce52-a0fd-4976-85f6-9c45603099a6" />

JEE RANK TRANSFORMATION:

<img width="977" height="528" alt="17" src="https://github.com/user-attachments/assets/5352392e-7f13-44dc-9967-aa5c9c25fe90" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
