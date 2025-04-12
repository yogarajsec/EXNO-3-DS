## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.

2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.

3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.

4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
  ```
import pandas as pd
import numpy as np
from scipy import stats
df
```
![Screenshot 2025-03-29 113058](https://github.com/user-attachments/assets/9eff59dc-afea-4d67-ac9d-4b26793906d1)
```
from sklearn.preprocessing import LabelEncoder , OrdinalEncoder
climate=['Cold','Warm','Hot','Very Hot']
ele=OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```
![Screenshot 2025-03-29 113109](https://github.com/user-attachments/assets/1ad4b32d-210d-4e9b-974d-c25d0cbfd009)
```
df['bo2']=ele.fit_transform(df[['Ord_1']])
df
```
![Screenshot 2025-03-29 113114](https://github.com/user-attachments/assets/d7440c0e-79eb-43a7-92c1-18503859148a)
```
le=LabelEncoder()
df2=df.copy()
df2['Ord_2']=le.fit_transform(df2['Ord_2'])
df2
```
![Screenshot 2025-03-29 113120](https://github.com/user-attachments/assets/b1a9e323-2e67-4b3e-9f85-2697b078d393)
```
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder()
df3=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2=pd.concat([enc,df3],axis=1)
df2
```
![Screenshot 2025-03-29 113128](https://github.com/user-attachments/assets/2454c7a7-ed8e-43ea-b56f-e05cf5786063)
```
pd.get_dummies(df,columns=['City'])
```
![Screenshot 2025-03-29 113138](https://github.com/user-attachments/assets/dcef2883-860f-424e-8b05-a6164afbbcba)
```
from category_encoders import BinaryEncoder
df= pd.read_csv("/content/data (1).csv")
df
```
![Screenshot 2025-03-29 113144](https://github.com/user-attachments/assets/cc26571c-9ec1-4a0e-9be3-4cd47dfbc74d)
```
be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
df
```
![Screenshot 2025-03-29 113149](https://github.com/user-attachments/assets/50e47aad-422f-4d1b-be47-e1904cad5c1a)
```
from category_encoders import TargetEncoder
te=TargetEncoder()
CC=df.copy()
new=te.fit_transform(CC["City"],y=CC["Target"])
CC=pd.concat([CC,new],axis=1)
CC
```
![Screenshot 2025-03-29 113157](https://github.com/user-attachments/assets/e077298e-0003-4ebb-ae50-e7124b19c4ee)
```
new = te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![Screenshot 2025-03-29 113203](https://github.com/user-attachments/assets/9513e67d-daec-4728-b66e-152694c0b5ee)
```
df=pd.read_csv("/content/Data_to_Transform.csv")
df
```
![Screenshot 2025-03-29 113208](https://github.com/user-attachments/assets/961a4c4c-9ea2-402e-a18f-248803fb7495)
```
df.skew()
```
![Screenshot 2025-03-29 113213](https://github.com/user-attachments/assets/cbec7676-9e58-479e-9dde-c57779eba5e8)
```
np.log(df["Highly Positive Skew"])
```
![Screenshot 2025-03-29 113220](https://github.com/user-attachments/assets/2f07f3e9-959e-47ef-abb6-0b3522dd359a)
```
np.reciprocal(df["Moderate Positive Skew"])
```
![Screenshot 2025-03-29 113226](https://github.com/user-attachments/assets/00f6de98-fc04-442b-bcde-1e7cd697268f)
```
np.sqrt(df["Highly Positive Skew"])
```
![Screenshot 2025-03-29 113231](https://github.com/user-attachments/assets/a77df248-a368-4e33-9849-6546e4927c32)
```
np.square(df["Highly Positive Skew"])
```
![Screenshot 2025-03-29 113238](https://github.com/user-attachments/assets/e8843731-7c1e-4291-896a-490ea57f61ac)
```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
df
```
![Screenshot 2025-03-29 113246](https://github.com/user-attachments/assets/1f27ab96-c959-4947-8dfe-04c530d561e3)

```
df["Moderate Negative Skew_yeojohnson"],parameters =stats.yeojohnson(df["Moderate Negative Skew"])
df
```
![Screenshot 2025-03-29 113255](https://github.com/user-attachments/assets/07e6caa2-0c09-4b77-9998-1d445838a943)
```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df
```
![Screenshot 2025-03-29 113319](https://github.com/user-attachments/assets/ec4cb17c-a6c0-4694-b218-030416ad08ad)
```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df['Moderate Negative Skew'],line='45')
plt.show()
```
![Screenshot 2025-03-29 113330](https://github.com/user-attachments/assets/ce7cae79-c585-4aa8-9cac-f15d24c0c9e6)
```
sm.qqplot(df["Moderate Negative Skew_1"],line='45')
plt.show()
```
![Screenshot 2025-03-29 113335](https://github.com/user-attachments/assets/1818cfda-d751-449c-bb6b-7725ebfd0e55)
```
df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df['Highly Negative Skew'],line='45')
plt.show()
```
![Screenshot 2025-03-29 113340](https://github.com/user-attachments/assets/b54fd06e-eff8-400c-aa46-6cf0ea1faf24)
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```
![download](https://github.com/user-attachments/assets/2a46a1b0-5aeb-41f3-8640-0c430dcd96d3)

```
sm.qqplot(df["Highly Negative Skew_1"],line='45')
plt.show()
```
![download](https://github.com/user-attachments/assets/95739910-1961-435d-a1ae-899af71e0bcb)

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line='45')
plt.show()
```
![Screenshot 2025-03-29 113355](https://github.com/user-attachments/assets/a048f447-bd83-41ea-8a8d-4538ddb985d6)

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line='45')
plt.show()
```
![Screenshot 2025-03-29 113402](https://github.com/user-attachments/assets/8b34842f-4790-4fcd-83c9-c8d989b855da)

```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```
![Screenshot 2025-03-29 113411](https://github.com/user-attachments/assets/de8dfd77-4347-45b7-9f05-1b34caa946c0)

```
pd.concat([cc,new],axis=1)
```
![Screenshot 2025-03-29 113422](https://github.com/user-attachments/assets/a295335a-68ee-43ce-8e03-656f54772e9a)

# RESULT:
  Thus, performing Feature Encoding and Transformation process for the given data set is completed.       

       
