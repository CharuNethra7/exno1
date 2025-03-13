# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
## Data Cleaning
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/f4a1e538-4902-4510-8eb6-094ccbdf9c06)

```
df.isnull().sum()
```

![image](https://github.com/user-attachments/assets/93dc1d78-71f5-4721-b45e-0d7d3dc8ce6d)

```
df.isnull().any()
```

![image](https://github.com/user-attachments/assets/1be40928-4261-4542-af76-2c688ffce27f)

```
df.dropna()
```

![image](https://github.com/user-attachments/assets/014c5113-234d-4be3-b20c-8930153770d6)

```
df.fillna(0)
```

![image](https://github.com/user-attachments/assets/f70535f4-4fb9-4fba-b099-e43e34be2e3f)

```
df.fillna(method = "ffill")
```

![image](https://github.com/user-attachments/assets/d086d3c2-f053-4284-afb5-6216bae63670)

```
df.fillna(method = 'bfill')
```

![image](https://github.com/user-attachments/assets/5831be92-f239-4e21-a16d-a57feb4a649f)

```
df_dropped = df.dropna()
df_dropped
```

![image](https://github.com/user-attachments/assets/302cb9d7-bd9d-4621-ab3d-2b8b2dca9622)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```

![image](https://github.com/user-attachments/assets/cbf517ee-807a-4913-9d25-288afee61922)

## IQR(Inter Quartile Range)
```
ir=pd.read_csv('iris.csv')
ir
```

![image](https://github.com/user-attachments/assets/2266cc1e-637a-4e11-9a00-e8c9bdb380f3)

```
ir.describe()
```

![image](https://github.com/user-attachments/assets/5bc953ff-12f7-4774-8375-8bfef6cbf24d)

```
import seaborn as sns
import matplotlib.pyplot as plt
sns.boxplot(x='sepal_width',data=ir)
plt.show()

```

![image](https://github.com/user-attachments/assets/0d1211ca-f10f-435b-a468-14158e136caa)

```
 c1=ir.sepal_width.quantile(0.25)
 c3=ir.sepal_width.quantile(0.75)
 iq=c3-c1
 print(c3)
```

![image](https://github.com/user-attachments/assets/98889d32-294f-4118-af38-5cdcaf0036c9)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![image](https://github.com/user-attachments/assets/4df70e36-b218-4aeb-9df2-e9aa6e94fff3)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![image](https://github.com/user-attachments/assets/259af6a8-b1e0-4749-9fe6-909746d05be4)

```
sns.boxplot(x='sepal_width',data=delid)
```

![image](https://github.com/user-attachments/assets/f9e30250-7654-4b67-b8c5-0e221fccee44)

## Z - Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/user-attachments/assets/582c48ea-ba0d-4ba7-8ed7-b325a4efa583)

```
df = pd.read_csv("heights.csv")

q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```

![image](https://github.com/user-attachments/assets/bb99613d-aabf-420a-8e7b-2e00f013e923)


```
low = q1- 1.5*iqr
low
```

![image](https://github.com/user-attachments/assets/2abcae26-a4a2-4778-8a8d-382db355f468)

```
high = q3 + 1.5*iqr
high
```

![image](https://github.com/user-attachments/assets/1df8702d-7bf7-4a41-8f93-346bcd0f3443)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```

![image](https://github.com/user-attachments/assets/e31c785c-9490-4ce6-b3c6-e58d8059303e)

```
z = np.abs(stats.zscore(df['height']))
z
```

![image](https://github.com/user-attachments/assets/09e852c7-0a71-4546-a202-c84af5d07375)

```
df1 = df[z<3]
df1
```

![image](https://github.com/user-attachments/assets/3c42fb30-ce85-4b12-9464-fe95ab556afd)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
