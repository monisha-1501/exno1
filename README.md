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
           
1)
```
 import pandas as pd

df = pd.read_csv("Data_set.csv")

print("Missing values before cleaning:")
print(df.isnull().sum())

categorical_cols = ["show_name", "aired_on", "original_network"]

for col in categorical_cols:
    df[col] = df[col].fillna("Unknown")

numeric_cols = ["rating", "current_overall_rank", "watchers"]

for col in numeric_cols:
    df[col] = df[col].fillna(df[col].median())

df["current_overall_rank"] = df["current_overall_rank"].round().astype("Int64")

print("\nMissing values after cleaning:")
print(df.isnull().sum())

df.to_csv("Data_set_cleaned.csv", index=False)

print("\nCleaned dataset saved successfully!")
 ```

 <img width="912" height="555" alt="image" src="https://github.com/user-attachments/assets/e5a9dd4d-57f2-49e5-8ce5-424e2388f675" />

2)
 ```
import pandas as pd

df = pd.read_csv("heights.csv")

Q1 = df["height"].quantile(0.25)
Q3 = df["height"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[(df["height"] < lower) | (df["height"] > upper)]

print("Unusual height measurements:")
print(outliers)
```

<img width="762" height="112" alt="image" src="https://github.com/user-attachments/assets/a84a6791-85db-4b67-9c06-b364f5bbdd58" />

3)
```
import pandas as pd

df = pd.read_csv("iris.csv")

cols = df.select_dtypes(include="number").columns

for col in cols:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1

    outliers = df[(df[col] < Q1 - 1.5 * IQR) |
                  (df[col] > Q3 + 1.5 * IQR)]

    print("IQR outliers in", col)
    print(outliers[col])

for col in cols:
    z = (df[col] - df[col].mean()) / df[col].std()

    print("Z-score outliers in", col)
    print(df.loc[z.abs() > 3, col])
```

<img width="1026" height="467" alt="image" src="https://github.com/user-attachments/assets/dd854d4e-a02a-41a1-a7d3-fc470ec5fd96" />

4)
```
import pandas as pd

df = pd.read_csv("Loan_data.csv")

num_cols = df.select_dtypes(include="number").columns

for col in num_cols:
    df[col] = df[col].fillna(df[col].median())

cat_cols = df.select_dtypes(include="object").columns

for col in cat_cols:
    if df[col].isnull().any():
        df[col] = df[col].fillna(df[col].mode()[0])

df = df.drop_duplicates()

print(df.isnull().sum())

df.to_csv("Loan_data_cleaned.csv", index=False)

print("Data cleaning completed!")
```

<img width="887" height="325" alt="image" src="https://github.com/user-attachments/assets/9fb989d3-6ccd-469b-8225-cb84bbe6f581" />

5)
```
import pandas as pd

df = pd.read_csv("SAMPLEIDS.csv")

df = df.drop_duplicates()

print("Missing values:")
print(df.isnull().sum())

print("Duplicate registration numbers:")
print(df[df.duplicated("REGNO", keep=False)])

marks = ["M1", "M2", "M3", "M4"]

print("Inconsistent total marks:")
print(df[df["TOTAL"] != df[marks].sum(axis=1, min_count=4)])

df.to_csv("SAMPLEIDS_cleaned.csv", index=False)

print("Cleaning completed!")
```
<img width="992" height="852" alt="image" src="https://github.com/user-attachments/assets/a89f59f8-bbc9-46dd-b384-ec897b3a8815" />




# Result
     Thus the given data successfully performed data cleaning and saved the cleaned data to a file.     
