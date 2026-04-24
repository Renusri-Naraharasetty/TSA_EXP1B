# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 22.04.26

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

data = pd.read_csv("final_website_stats.csv")

data['timestamp'] = pd.to_datetime(data['timestamp'], format="%d-%m-%Y")

data = data.groupby('timestamp')['page_views'].mean().reset_index()

data.set_index('timestamp', inplace=True)

data['views_diff'] = data['page_views'] - data['page_views'].shift(1)

result = seasonal_decompose(data['page_views'], model='additive', period=7)
data['views_sea_diff'] = result.resid

data['views_log'] = np.log(data['page_views'])

data['views_log_diff'] = data['views_log'] - data['views_log'].shift(1)

result = seasonal_decompose(data['views_log_diff'].dropna(), model='additive', period=7)
data['views_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['page_views'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('Page Views')

plt.subplot(6, 1, 2)
plt.plot(data['views_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Views')

plt.subplot(6, 1, 3)
plt.plot(data['views_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted Views')

plt.subplot(6, 1, 4)
plt.plot(data['views_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Page Views)')

plt.subplot(6, 1, 5)
plt.plot(data['views_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Page Views))')

plt.subplot(6, 1, 6)
plt.plot(data['views_log_seasonal_diff'], label='Log + Regular Diff + Seasonal Diff')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Page Views)))')

plt.tight_layout()
plt.show()
```


### OUTPUT:
<img width="1657" height="265" alt="image" src="https://github.com/user-attachments/assets/7c2d04d4-1ebe-4321-9179-1827b247eebf" />
<img width="1651" height="565" alt="image" src="https://github.com/user-attachments/assets/1ba80436-a9c3-4189-9de8-cccb6b33b605" />


REGULAR DIFFERENCING:
<img width="1649" height="289" alt="image" src="https://github.com/user-attachments/assets/4f5b96c4-8921-46e5-80ac-124be265f8e8" />


SEASONAL ADJUSTMENT:
<img width="1649" height="288" alt="image" src="https://github.com/user-attachments/assets/5f07c27a-857c-40ca-b884-9086af82dd8c" />


LOG TRANSFORMATION:
<img width="1651" height="272" alt="image" src="https://github.com/user-attachments/assets/d51e2949-8370-4675-8b8d-9ae0d8191d3a" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
