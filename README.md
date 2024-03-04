<h1 align="center">Ex. 1   Data Cleaning and Outlier Detection & Removal</h1>


## AIM
### To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation
### Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm
### STEP 1
#### Read the given Data

### STEP 2
#### Get the information about the data

### STEP 3 
#### Remove the null values from the data

### STEP 4
#### Save the Clean data to the file

### STEP 5
#### Remove outliers using IQR

### STEP 6
#### Use zscore of to remove outliers

## Coding and Outputs

<h3 align="center">Data Cleaning</h3>

```py
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/bef00b14-e844-4890-9e94-d4f51d0a24ef)

```py
df.isnull().sum()

```

![image](https://github.com/ShriramGH/exno1/assets/117991122/97dace32-d9ed-4e74-9cef-be56fae1acaf)


```py
df.isnull().any()
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/3f0e8ca4-8bf2-4acd-9993-c3426a0c893d)

```py
df.dropna()
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/997f994d-2694-422e-9056-e0cd809ea7fc)

```py
df.fillna(0)
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/4bc21c2b-9c61-4a40-8b3f-16f3eb01ccd7)

```py
df.fillna(method = 'ffill')
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/51b76a1d-14e1-4fa8-b57c-67ef525c1dff)

```py

df.fillna(method = 'bfill')
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/63b02ffa-e193-45f3-9328-5bab4ff67ed0)

```py
df_dropped = df.dropna()
df_dropped
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/d4c59216-13f9-4dbf-be29-6be605cbd9ec)

```py
df.fillna({'GENDER':'TRANS','NAME':'KANISHKAR','ADDRESS':'ARANI','M1':100,'M2':100,'M3':100,'M4':100,'TOTAL':400,'AVG':100.000000}
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/8b895027-3b05-48b6-839a-6a1b3d9b0982)

<hr><hr>

<h3 align="center">IQR(Inter Quartile Range)</h3>

```py
import pandas as pd
```

```py
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/28516ce9-5190-4706-93df-0ae41c34bf02)

```py
ir.describe()
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/7c480d80-64d6-4c90-93c3-bbce145badd9)

```py
import seaborn as sns
```

```py

sns.boxplot(x='sepal_width',data=ir)
```


![image](https://github.com/ShriramGH/exno1/assets/117991122/150ac1be-977e-425c-a33b-5b4fcdf4c2b1)

```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/63cfb771-c3d2-4450-82d3-c40d37a633dc)

```py

rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/96d2eb10-9804-49ec-8dbc-a2f5f515be96)

```py
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/8cc2e387-f486-4eb9-8ee8-8ef27d949a64)

```py
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/be71cab2-e501-496c-8304-312d0dbe14d8)

<hr><hr>

<h3 align="center">Z-Score</h3>

```py
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```
```py
dataset=pd.read_csv("heights.csv")
dataset
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/73ab03a3-e3c3-4469-b36a-2c52ee037809)


```py
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```py
iqr = q3-q1
iqr
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/aa386c6f-6d2d-4c3b-b0d8-54f709b6ca54)

```py
low = q1 - 1.5*iqr
low
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/fe9a68b7-abf1-444b-a709-6de2c19b1675)

```py
high = q3 + 1.5*iqr
high
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/4ad382ba-2c0b-4837-acef-0458c7fa2e20)


```py
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/77ff2159-7e82-4ef9-afc0-9473efd940ca)


```py
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/ShriramGH/exno1/assets/117991122/d246b1b0-0c49-4116-848a-fea4925cc93a)

```py
df1 = df[z<3]
df1
```

![image](https://github.com/ShriramGH/exno1/assets/117991122/6078b187-7bef-48d7-9358-58647a4727bc)


<hr>

## Result
<br>

### Hence the data was cleaned , outliers were detected and removed.
