# Ex.No: 1(B) CONVERSION OF NON STATIONARY TO STATIONARY DATA
### Date: 12/08/2025
### Name: SHYAM S
### Reg.No: 212223240156

## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
## PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("/content/index_1.csv")
data.head()
data.tail()

data['date'] = pd.to_datetime(data['date'])
data.set_index('date', inplace=True)
data_monthly = data['money'].resample('M').sum()
data_monthly_diff = data_monthly - data_monthly.shift(1)

# Seasonal decomposition
result = seasonal_decompose(data_monthly, model='additive', period=6)
data_monthly_sea_diff = result.resid

# Log transformation

data_monthly_log = np.log(data_monthly)
data_monthly_log_diff = data_monthly_log - data_monthly_log.shift(1)

# Seasonal decomposition on log diff

result = seasonal_decompose(data_monthly_log_diff.dropna(), model='additive', period=6)
data_monthly_log_sea_diff = result.resid

# Plotting with colors
plt.figure(figsize=(12,12))

plt.subplot(6,1,1)
plt.plot(data_monthly, label='Original', color='blue', linewidth=2)
plt.legend()
plt.title('Original Money Spent')

plt.subplot(6,1,2)
plt.plot(data_monthly_diff, label='Regular Difference', color='orange', linewidth=2)
plt.legend()
plt.title('Regular Differencing')

plt.subplot(6,1,3)
plt.plot(data_monthly_sea_diff, label='Seasonal Adjustment', color='green', linewidth=2)
plt.legend()
plt.title('Seasonal Adjustment')

plt.subplot(6,1,4)
plt.plot(data_monthly_log, label='Log Transformation', color='red', linewidth=2)
plt.legend()
plt.title('Log Transformation')

plt.subplot(6,1,5)
plt.plot(data_monthly_log_diff, label='Log + Regular Differencing', color='purple', linewidth=2)
plt.legend()
plt.title('Log + Regular Differencing')

plt.subplot(6,1,6)
plt.plot(data_monthly_log_sea_diff, label='Log + Regular + Seasonal Diff', color='brown', linewidth=2)
plt.legend()
plt.title('Log + Regular + Seasonal Differencing')

plt.tight_layout()
plt.show()

# Overall

plt.figure(figsize=(10,8))

plt.plot(data_monthly, label='Original', color='blue', linewidth=2)
plt.plot(data_monthly_diff, label='Regular Differencing', color='orange', linewidth=2)
plt.plot(data_monthly_sea_diff, label='Seasonal Adjustment', color='green', linewidth=2)
plt.plot(data_monthly_log, label='Log Transformation', color='red', linewidth=2)
plt.plot(data_monthly_log_diff, label='Log + Regular Differencing', color='purple', linewidth=2)
plt.plot(data_monthly_log_sea_diff, label='Log + Regular + Seasonal Differencing', color='brown', linewidth=2)

plt.title('OVERALL VIEW: All Transformations')
plt.xlabel('Month')
plt.ylabel('Money / Transformed Money')
plt.legend(loc='best', fontsize=9)
plt.grid(True)
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()

```

## OUTPUT:

ORIGINAL:

<img width="1373" height="227" alt="image" src="https://github.com/user-attachments/assets/12c9dfda-95df-47eb-938d-3216f029d6ff" />


REGULAR DIFFERENCING:

<img width="1372" height="227" alt="image" src="https://github.com/user-attachments/assets/926d660c-c49f-4905-aab8-a446fdd3c509" />


SEASONAL ADJUSTMENT:

<img width="1371" height="227" alt="image" src="https://github.com/user-attachments/assets/f9260219-1c48-4f65-ac96-e1ac45cb5011" />


LOG TRANSFORMATION:

<img width="1328" height="662" alt="image" src="https://github.com/user-attachments/assets/a103a02a-a921-488f-ac12-5104492430b7" />


OVERALL:

<img width="922" height="732" alt="image" src="https://github.com/user-attachments/assets/f762819f-4ffc-45c0-a4f1-656ce0e5cd07" />


### RESULT:
Thus we have created a Python program to convert non-stationary coffee transaction data into stationary data using regular differencing, log transformation, and seasonal decomposition.
