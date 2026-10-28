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
           
**1) CODING :**
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

**OUTPUT :**

 <img width="912" height="555" alt="image" src="https://github.com/user-attachments/assets/e5a9dd4d-57f2-49e5-8ce5-424e2388f675" />


**2) CODING :** 
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

**OUTPUT :**

<img width="762" height="112" alt="image" src="https://github.com/user-attachments/assets/a84a6791-85db-4b67-9c06-b364f5bbdd58" />


**3) CODING :**
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

**OUTPUT :**

<img width="1026" height="467" alt="image" src="https://github.com/user-attachments/assets/dd854d4e-a02a-41a1-a7d3-fc470ec5fd96" />


**4) CODING :**
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

**OUTPUT :**

<img width="887" height="325" alt="image" src="https://github.com/user-attachments/assets/9fb989d3-6ccd-469b-8225-cb84bbe6f581" />


**5) CODING :**
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

**OUTPUT :**

<img width="992" height="852" alt="image" src="https://github.com/user-attachments/assets/a89f59f8-bbc9-46dd-b384-ec897b3a8815" />


# Summary
```
# Data Cleaning 
In this experiment, I understood that data cleaning is an important step before data
analysis. It helps to handle missing, duplicate, incorrect and unusual data so that the
dataset becomes more useful for analysis.

# Reading the Dataset
The dataset is read using Pandas and stored in a DataFrame. This makes it easier to
view the data and perform different cleaning operations on its columns.

# Handling Missing Values
Missing values are checked using isnull().sum(). For categorical columns, missing
values can be replaced with “Unknown”. For numerical columns, the median is used
to fill missing values.

# Saving the Cleaned Data
After cleaning, the data is saved as a new CSV file using to_csv(). This keeps the
original dataset separate from the cleaned dataset.

# Removing Duplicate Data
I learned that duplicate records can affect the result of analysis. The drop_duplicates()
function is used to remove repeated rows. Duplicate registration numbers are also
checked in the sample data

# Finding Outliers
An outlier is a value that is very different from the other values in the dataset. The
experiment uses two methods to identify outliers: IQR and Z-score.

# IQR Method
For the IQR method, Q1 and Q3 are calculated first. IQR is found using Q3 − Q1.
Values below Q1 − 1.5 × IQR or above Q3 + 1.5 × IQR are identified as possible
outliers.

# Z-Score Method
The Z-score shows how far a value is from the mean. In this experiment, values with an
absolute Z-score greater than 3 are identified as possible outliers.

# Overall Summary
Overall, I understood that data cleaning is necessary before performing data analysis.
Through this experiment, I learned how to handle missing values, remove duplicate
records, check data consistency and identify outliers using IQR and Z-score.
```

# Result
     Thus the given data successfully performed data cleaning and saved the cleaned data to a file.     
