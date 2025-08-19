# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19-08-2025

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
data=pd.read_csv('/content/blood_donor_dataset.csv')
data.head()
data=pd.read_csv('/content/blood_donor_dataset.csv')

data['created_at']=pd.to_datetime(data['created_at'])
data.set_index('created_at',inplace=True)

data_aggregated = data.groupby(data.index)['pints_donated'].mean().to_frame()

data_aggregated['pints_donated_diff']=data_aggregated['pints_donated']-data_aggregated['pints_donated'].shift(1)

data_aggregated['pints_donated_log'] = np.log(data_aggregated['pints_donated'].replace(0, 1e-9))
data_aggregated['pints_donated_log_diff']=data_aggregated['pints_donated_log']-data_aggregated['pints_donated_log'].shift(1)

result = seasonal_decompose(data_aggregated['pints_donated_log_diff'].dropna(), model='additive', period=12)
data_aggregated['pints_donated_log_seasonal_diff']=result.resid

plt.figure(figsize=(20, 24))
plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['pints_donated'], label='Original') 
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('created_at')
plt.ylabel('pints_donated')
plt.subplot(2, 1, 1)
plt.plot(data_aggregated['pints_donated_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('created_at')
plt.ylabel('pints_donated')
plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['pints_donated_log_seasonal_diff'], label='Log Transformation, Regular and Seasonal Differencing') 
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('created_at')
plt.ylabel('SDiff(RDiff(Log(pints_donated)))')
plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['pints_donated_log'], label='Log Transformation') 
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('created_at')
plt.ylabel('Log(pints_donated)')
plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['pints_donated_log_diff'], label='Log Transformation and Regular Differencing') 
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('created_at')
plt.ylabel('RDiff(Log(pints_donated))')
plt.subplot(1,1,1) 
plt.plot(data_aggregated['pints_donated_log_seasonal_diff'], label='Log Transformation and Regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('created_at')
plt.ylabel('SDiff(RDiff(Log(pints_donated)))') 
plt.tight_layout()
plt.show() 
```

### OUTPUT:
<img width="1793" height="483" alt="image" src="https://github.com/user-attachments/assets/5e57e7c9-0281-4a43-81ba-cf9da50f2336" />
<img width="1197" height="421" alt="image" src="https://github.com/user-attachments/assets/fb53ac69-51e3-44b1-91fc-cd9e7fe26eb8" />
<img width="730" height="472" alt="image" src="https://github.com/user-attachments/assets/9b94848c-70cc-44e4-a211-a528b3c83180" />
REGULAR DIFFERENCING:
<img width="817" height="482" alt="image" src="https://github.com/user-attachments/assets/343903c0-7a52-4fdf-a477-805bf370b524" />

SEASONAL ADJUSTMENT:
<img width="1213" height="717" alt="image" src="https://github.com/user-attachments/assets/e97ddf95-23ab-4bdf-950c-cf16823d28e2" />

LOG TRANSFORMATION:
<img width="762" height="485" alt="image" src="https://github.com/user-attachments/assets/72e3c75b-fa2f-4dc4-ad66-8e355df2eb76" />
<img width="1117" height="705" alt="image" src="https://github.com/user-attachments/assets/4f2ac0ce-7795-48be-b627-d13d14349e6c" />
<img width="1298" height="755" alt="image" src="https://github.com/user-attachments/assets/2f7f0a5d-f619-4072-9eaf-c830ea7a4919" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
