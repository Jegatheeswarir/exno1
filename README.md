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
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![Screenshot 2024-09-04 132958](https://github.com/user-attachments/assets/026f4082-6321-417e-805c-78d57b432d0a)
```
df.shape
```
![Screenshot 2024-09-04 133118](https://github.com/user-attachments/assets/cd2b2730-e03a-4d08-9409-f8e62e739d3a)
```
df.describe()
```
![Screenshot 2024-09-04 132958](https://github.com/user-attachments/assets/f82bb6e4-885e-455f-9619-38848c443bd1)
```
df.info()
```
![Screenshot 2024-09-04 133232](https://github.com/user-attachments/assets/63c4b3f3-f335-459e-ba25-18dc6f491bb4)
```
df.head(3)
```
![Screenshot 2024-09-04 133315](https://github.com/user-attachments/assets/6eb0a0f9-e0d5-41a8-82c1-2c67421e56ea)
```
df.tail(3)
```
![Screenshot 2024-09-04 133345](https://github.com/user-attachments/assets/ce0f5c2d-ec5c-4316-a9d5-89b73a800c62)
```
df.isna().sum()
```
![Screenshot 2024-09-04 133421](https://github.com/user-attachments/assets/5ce44890-a05f-46bf-88e4-9e7584365e9b)
```
df.shape
```
![Screenshot 2024-09-04 133511](https://github.com/user-attachments/assets/69239562-b0ce-41d2-ac7c-fa2d301c591d)

```
x=df.dropna(how='any')
df
```
![Screenshot 2024-09-04 133601](https://github.com/user-attachments/assets/ea67973d-b70b-4894-ac3e-608fdaf0f2b1)
```
x2=df.dropna(how='all').shape
df
```
![Screenshot 2024-09-04 133643](https://github.com/user-attachments/assets/6c867b92-8d5f-4078-98f2-f2fe716420da)
```
mn=df.TOTAL.mean()
mn
```
![Screenshot 2024-09-04 133719](https://github.com/user-attachments/assets/6ab18dbf-efe6-4f68-92be-9b7310ec5733)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![Screenshot 2024-09-04 133747](https://github.com/user-attachments/assets/19421869-1438-42f3-9b85-6fcca05a8872)
```
df.isnull().sum()
```
![Screenshot 2024-09-04 133810](https://github.com/user-attachments/assets/18c6d4f7-9dfa-49f0-b560-a572b4774108)
```
df.M1.dropna(inplace=True)
df
```
![Screenshot 2024-09-04 133947](https://github.com/user-attachments/assets/ec6bd755-3a64-44ac-ac6a-2b83a0042a5d)
```
df.M1.fillna(method='ffill',inplace=True)
df
```
![Screenshot 2024-09-04 134140](https://github.com/user-attachments/assets/1c8040dd-5de1-45fa-acdb-db26ee917505)
```
df.isnull().sum()
```
![Screenshot 2024-09-04 134217](https://github.com/user-attachments/assets/c4e57f5f-eef5-41ad-a8a4-594dc2d82715)
```
df.M2.fillna(method='ffill',inplace=True)
df
```
![Screenshot 2024-09-04 134309](https://github.com/user-attachments/assets/71a53cc8-b7ab-47e6-b63d-f37b412ff2bc)
```
df.isnull().sum()
```
![Screenshot 2024-09-04 134415](https://github.com/user-attachments/assets/5b82f386-7595-4dff-978d-7ff2d5bb08ae)
```
df.M3.fillna(method='ffill',inplace=True)
df
```
![Screenshot 2024-09-04 134544](https://github.com/user-attachments/assets/21a71fe2-604f-4a12-b187-90a1c1d83a2a)
```
df.isnull().sum()
```
![Screenshot 2024-09-04 134631](https://github.com/user-attachments/assets/8ffd32b0-12e3-4803-97fa-b8c9f6ae607f)
```
df.duplicated()
```
![Screenshot 2024-09-04 134721](https://github.com/user-attachments/assets/12e34cdf-6149-473b-af48-f0740f0a5282)
```
df.drop_duplicates(inplace=True)
df
```
![Screenshot 2024-09-04 134802](https://github.com/user-attachments/assets/18be9be3-5916-4965-85ef-4d45b108030d)
```
df['DOB']
```
![Screenshot 2024-09-04 134828](https://github.com/user-attachments/assets/5f92813a-f7ac-46d1-9f00-cf7d3008f3bd)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![Screenshot 2024-09-04 134907](https://github.com/user-attachments/assets/0d9d259d-a849-4315-b22a-36e44fc88af2)
```
df.dropna(inplace=True)
df
```
![Screenshot 2024-09-04 134937](https://github.com/user-attachments/assets/e9ac6026-d430-4711-8c89-25d0fa60343f)
```
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![Screenshot 2024-09-04 134959](https://github.com/user-attachments/assets/6b82eb96-d861-4604-a4aa-ef4732fa209c)
## OUTLIER DETECTION AND REMOVAL USING IQR
```
import pandas as pd
import seaborn as sns
import numpy as np

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![Screenshot 2024-09-04 184205](https://github.com/user-attachments/assets/e766a2d9-06a3-4eb1-9165-bb19bc5ab913)
```
sns.boxplot(data=af)
```
![Screenshot 2024-09-04 184242](https://github.com/user-attachments/assets/16b3db8e-24e7-41c8-9a46-078cbf87847d)
```
sns.scatterplot(data=af)
```
![Screenshot 2024-09-04 184309](https://github.com/user-attachments/assets/86bd298f-6489-42e2-a1d9-ef60e031d415)
```
q1=af.quantile(0.25)
q2=af.quantile(0.50)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![Screenshot 2024-09-04 184332](https://github.com/user-attachments/assets/66c2f8d5-cb19-42ad-8925-1e7156f3447a)
```
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![Screenshot 2024-09-04 184356](https://github.com/user-attachments/assets/eb99ae4f-0eff-448e-8bda-e14c8db1271f)
```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
upper_bound
```
![Screenshot 2024-09-04 184441](https://github.com/user-attachments/assets/82159a80-7a90-416a-9f94-10a5c0d07e33)
```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR:",IQR)
print("Lower bound:",lower_bound)
print("Upper bound:",upper_bound)
print("Outliers:",outliers)
```
![Screenshot 2024-09-04 184551](https://github.com/user-attachments/assets/d0d4ae5b-a393-4a76-8602-0b8371c161bf)
```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
![Screenshot 2024-09-04 184632](https://github.com/user-attachments/assets/b38d9a6c-3aa8-4b11-8fa7-9b8e656a35b9)
```
af.dropna()
```
![Screenshot 2024-09-04 184657](https://github.com/user-attachments/assets/1bf7689a-44b4-41f6-a695-4df188988067)
```
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print("mean of the dataset is",mean)
print("std.deviation is",std)
```
![Screenshot 2024-09-04 184730](https://github.com/user-attachments/assets/bafe24b2-21b7-4459-b2c6-fabf190fbd01)
```
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z > threshold:
    outlier.append(i)
print("outlier in dataset is",outlier)
```
![Screenshot 2024-09-04 184841](https://github.com/user-attachments/assets/e55c24bd-2420-4796-b185-733f577035cb)
```
import pandas as pd
import numpy as np
import seaborn as sns
from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df
```
![Screenshot 2024-09-04 184933](https://github.com/user-attachments/assets/4af140c6-9a8f-4b73-9034-f165a9647a62)
```
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![Screenshot 2024-09-04 184959](https://github.com/user-attachments/assets/e6f643bd-d4ff-4929-a965-1fac4ff34dad)



# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
