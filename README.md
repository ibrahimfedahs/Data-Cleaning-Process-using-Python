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
# loan_data
```
import pandas as pd

df = pd.read_csv("Loan_data.csv")
print(df)

print(df.info())
print(df.describe())
print(df.isnull().sum())

df_clean = df.dropna()

df_clean.to_csv("Clean_Loan_data.csv", index=False)

print("Clean data saved successfully!")

import pandas as pd

df = pd.read_csv("Clean_Loan_data.csv")

columns = ['ApplicantIncome', 'CoapplicantIncome', 'LoanAmount']

for col in columns:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    df = df[(df[col] >= lower) & (df[col] <= upper)]

df.to_csv("IQR_Loan_data.csv", index=False)

print("Outliers removed using IQR!")

import pandas as pd
from scipy import stats

df = pd.read_csv("Clean_Loan_data.csv")

columns = ['ApplicantIncome', 'CoapplicantIncome', 'LoanAmount']

z = stats.zscore(df[columns])

df = df[(abs(z) < 3).all(axis=1)]

df.to_csv("Zscore_Loan_data.csv", index=False)

print("Outliers removed using Z-score!")
```
<img width="812" height="548" alt="image" src="https://github.com/user-attachments/assets/436a9837-47ca-4ae5-8d94-c10ef48c90b7" />
<img width="697" height="414" alt="image" src="https://github.com/user-attachments/assets/abc6c9be-a4a8-4de9-882d-80a72ed46962" />
<img width="470" height="318" alt="image" src="https://github.com/user-attachments/assets/137f3a87-a3ce-4378-a00a-9a9e131fbe12" />

# heights
```
import pandas as pd

df = pd.read_csv("heights.csv")

print(df.head())
print(df.info())
print(df.describe())

df = df.dropna()

df.to_csv("clean_heights.csv", index=False)

print("Clean data saved successfully")

Q1 = df.select_dtypes(include='number').quantile(0.25)
Q3 = df.select_dtypes(include='number').quantile(0.75)

IQR = Q3 - Q1

df = df[~((df.select_dtypes(include='number') < (Q1 - 1.5 * IQR)) |
          (df.select_dtypes(include='number') > (Q3 + 1.5 * IQR))).any(axis=1)]

print(df)

from scipy import stats
import numpy as np

numeric_df = df.select_dtypes(include='number')

z = np.abs(stats.zscore(numeric_df))

df = df[(z < 3).all(axis=1)]

print(df)

df.to_csv("final_clean_heights.csv", index=False)

print("Final data saved successfully")

```
<img width="254" height="217" alt="image" src="https://github.com/user-attachments/assets/990bdb5d-a834-40cf-8e90-3824e43f5b8b" />
<img width="350" height="318" alt="image" src="https://github.com/user-attachments/assets/2ca8464e-3a6e-4a82-9cf4-b1c85422e154" />
<img width="315" height="190" alt="image" src="https://github.com/user-attachments/assets/71251c3b-8dd2-4f0f-999d-aab7779d1161" />
<img width="349" height="200" alt="image" src="https://github.com/user-attachments/assets/b8b80c6c-b99e-44f2-97d0-e7ac7de43f14" />

# summary

The following data-cleaning steps were performed on both datasets:
1. Read the Data: Loaded both CSV files using Pandas.
2. Understand the Data: Used head(), info() and describe() to understand the datasets.
3. Remove Null Values: Removed missing values using dropna().
4. Save Clean Data: Saved the cleaned datasets into new CSV files.
5. Remove Outliers using IQR: Used the Interquartile Range method to identify and remove abnormal values.
6. Remove Outliers using Z-score: Used the Z-score method to identify and remove values that were far from the mean.

# Result
          Data cleaning and outlier removal were performed on both Loan Data and Heights Data.
