# 🧹 Data Cleaning with Python & Pandas — Complete README

> **Data Cleaning** is the process of detecting, correcting, removing, or transforming incorrect, incomplete, inconsistent, and duplicate data so that it becomes suitable for analysis and machine learning.

---

# 📚 Table of Contents

1. [What is Data Cleaning?](#1-what-is-data-cleaning)
2. [Why Data Cleaning is Important](#2-why-data-cleaning-is-important)
3. [Data Cleaning Workflow](#3-data-cleaning-workflow)
4. [Understanding the Dataset](#4-understanding-the-dataset)
5. [Common Data Quality Problems](#5-common-data-quality-problems)
6. [Missing Values](#6-missing-values)
7. [Detecting Missing Values](#7-detecting-missing-values)
8. [Removing Missing Values](#8-removing-missing-values)
9. [Filling Missing Values](#9-filling-missing-values)
10. [Forward Fill and Backward Fill](#10-forward-fill-and-backward-fill)
11. [Duplicate Data](#11-duplicate-data)
12. [Detecting Duplicates](#12-detecting-duplicates)
13. [Removing Duplicates](#13-removing-duplicates)
14. [Incorrect Data Types](#14-incorrect-data-types)
15. [Type Conversion](#15-type-conversion)
16. [Invalid Numeric Data](#16-invalid-numeric-data)
17. [String Cleaning](#17-string-cleaning)
18. [Removing Extra Spaces](#18-removing-extra-spaces)
19. [Standardizing Text](#19-standardizing-text)
20. [Replacing Values](#20-replacing-values)
21. [Handling Invalid Values](#21-handling-invalid-values)
22. [Date and Time Cleaning](#22-date-and-time-cleaning)
23. [Categorical Data Cleaning](#23-categorical-data-cleaning)
24. [Outliers](#24-outliers)
25. [Detecting Outliers Using IQR](#25-detecting-outliers-using-iqr)
26. [Handling Outliers](#26-handling-outliers)
27. [Data Validation](#27-data-validation)
28. [Inconsistent Data](#28-inconsistent-data)
29. [Renaming Columns](#29-renaming-columns)
30. [Removing Unnecessary Columns](#30-removing-unnecessary-columns)
31. [Handling Wrong Records](#31-handling-wrong-records)
32. [Cleaning Multiple Columns](#32-cleaning-multiple-columns)
33. [Cleaning CSV Data](#33-cleaning-csv-data)
34. [Complete Data Cleaning Example](#34-complete-data-cleaning-example)
35. [Data Cleaning Checklist](#35-data-cleaning-checklist)
36. [Important Pandas Methods](#36-important-pandas-methods)
37. [Data Cleaning Interview Questions](#37-data-cleaning-interview-questions)
38. [Final Revision](#38-final-revision)

---

# 1. What is Data Cleaning?

Data cleaning is the process of preparing raw data for analysis.

Raw data may contain:

```text
Missing values
Duplicate records
Incorrect data types
Invalid values
Inconsistent formatting
Extra spaces
Spelling mistakes
Incorrect dates
Outliers
Unnecessary columns
Incorrect records
```

Example of raw data:

```text
Name        Age     City       Salary
John        25      Hyderabad  50000
 john       25      hyderabad  50000
Alice       NaN     Delhi      60000
Bob         -5      Mumbai     70000
David       30      Delhi      "abc"
```

This dataset has several problems.

After cleaning:

```text
Name        Age     City        Salary
John        25      Hyderabad   50000
Alice       27      Delhi       60000
Bob         30      Mumbai      70000
David       30      Delhi       65000
```

The exact treatment depends on the meaning and source of the data.

---

# 2. Why Data Cleaning is Important

Bad data produces bad analysis.

```text
Bad Data
   ↓
Incorrect Analysis
   ↓
Incorrect Insights
   ↓
Bad Business Decisions
```

Clean data produces:

```text
Clean Data
   ↓
Reliable Analysis
   ↓
Correct Insights
   ↓
Better Decisions
```

Data cleaning is especially important in:

* Data Analytics
* Data Science
* Machine Learning
* Business Intelligence
* Financial Analysis
* Healthcare Analytics
* Customer Analytics
* Sales Analysis

---

# 3. Data Cleaning Workflow

A typical data cleaning process:

```text
             Raw Dataset
                  ↓
           Load the Dataset
                  ↓
         Understand the Data
                  ↓
        Identify Data Problems
                  ↓
       ┌──────────┼──────────┐
       ↓          ↓          ↓
    Missing    Duplicate   Invalid
     Data       Data        Data
       ↓          ↓          ↓
       └──────────┼──────────┘
                  ↓
          Correct Data Types
                  ↓
          Clean Text Values
                  ↓
          Clean Date Values
                  ↓
          Handle Outliers
                  ↓
         Validate the Dataset
                  ↓
             Clean Dataset
```

---

# 4. Understanding the Dataset

Before cleaning, first understand the dataset.

Import Pandas:

```python
import pandas as pd
```

Read the dataset:

```python
df = pd.read_csv("data.csv")
```

---

## View First Rows

```python
df.head()
```

---

## View Last Rows

```python
df.tail()
```

---

## Number of Rows and Columns

```python
df.shape
```

Example:

```text
(1000, 8)
```

Means:

```text
1000 rows
8 columns
```

---

## Column Names

```python
df.columns
```

---

## Data Types

```python
df.dtypes
```

---

## Complete Information

```python
df.info()
```

`info()` is one of the most important methods during data cleaning.

It tells you:

* Number of rows
* Column names
* Non-null values
* Data types
* Memory usage

---

## Statistical Summary

```python
df.describe()
```

---

## Summary of Categorical Columns

```python
df.describe(include="object")
```

---

## All Columns

```python
df.describe(include="all")
```

---

# 5. Common Data Quality Problems

The most common problems are:

| Problem             | Example                     |
| ------------------- | --------------------------- |
| Missing values      | `NaN`                       |
| Duplicate rows      | Same customer appears twice |
| Wrong data type     | Age stored as string        |
| Invalid values      | Age = `-20`                 |
| Inconsistent text   | `Delhi`, `delhi`, `DELHI`   |
| Extra spaces        | `" John "`                  |
| Spelling errors     | `"Hydrabad"`                |
| Invalid dates       | `"2025-99-50"`              |
| Outliers            | Salary = 10 crore           |
| Wrong records       | Age = 500                   |
| Unnecessary columns | Empty ID column             |
| Mixed formats       | `01/02/2025`, `2025-02-01`  |

---

# 6. Missing Values

Missing data means a value is unavailable.

Common representations:

```text
NaN
None
NaT
NULL
NA
N/A
?
empty string
```

Example:

```python
data = {
    "Name": ["John", "Alice", "Bob"],
    "Age": [20, None, 22],
    "Salary": [50000, 60000, None]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name   Age   Salary
0   John  20.0  50000.0
1  Alice   NaN  60000.0
2    Bob  22.0      NaN
```

---

# 7. Detecting Missing Values

## isna()

```python
df.isna()
```

Returns `True` where data is missing.

---

## isnull()

```python
df.isnull()
```

`isnull()` and `isna()` are equivalent.

---

## Count Missing Values Per Column

```python
df.isna().sum()
```

Example:

```text
Name      0
Age       1
Salary    1
```

---

## Total Missing Values

```python
df.isna().sum().sum()
```

---

## Percentage of Missing Values

```python
missing_percentage = (
    df.isna().mean() * 100
)

print(missing_percentage)
```

---

## Check Whether Any Missing Value Exists

```python
df.isna().any()
```

---

## Check Whether Entire DataFrame Has Missing Values

```python
df.isna().any().any()
```

---

# 8. Removing Missing Values

Sometimes removing missing records is appropriate.

## Drop Rows Containing Any Missing Value

```python
df.dropna()
```

---

## Permanently Remove

```python
df.dropna(inplace=True)
```

---

## Drop Rows Only If All Values Are Missing

```python
df.dropna(how="all")
```

---

## Drop Columns Containing Missing Values

```python
df.dropna(axis=1)
```

---

## Drop Rows Based on Specific Columns

```python
df.dropna(
    subset=["Name", "Age"]
)
```

This removes rows where `Name` or `Age` is missing.

---

# 9. Filling Missing Values

Instead of deleting data, we can replace missing values.

Use:

```python
fillna()
```

---

## Fill With Constant

```python
df["Age"] = df["Age"].fillna(0)
```

---

## Fill With Mean

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)
```

---

## Fill With Median

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

## Fill With Mode

Useful for categorical data.

```python
df["City"] = df["City"].fillna(
    df["City"].mode()[0]
)
```

---

# Mean vs Median vs Mode

### Mean

```text
Average of values
```

Use when data does not have severe outliers.

```python
df["Salary"].mean()
```

### Median

```text
Middle value
```

Often better when data contains outliers.

```python
df["Salary"].median()
```

### Mode

```text
Most frequently occurring value
```

Commonly used for categorical data.

```python
df["City"].mode()[0]
```

---

# 10. Forward Fill and Backward Fill

Useful especially for time-series data.

---

## Forward Fill

Copies the previous valid value forward.

```python
df["Temperature"] = (
    df["Temperature"].ffill()
)
```

Example:

```text
10
NaN
NaN
20
```

After forward fill:

```text
10
10
10
20
```

---

## Backward Fill

Copies the next valid value backward.

```python
df["Temperature"] = (
    df["Temperature"].bfill()
)
```

Example:

```text
10
NaN
NaN
20
```

After backward fill:

```text
10
20
20
20
```

---

# Important Note

Do not blindly fill every missing value.

You should ask:

```text
Why is the value missing?
What does the column represent?
How much data is missing?
Will filling it introduce bias?
```

For example, replacing a missing salary with `0` may completely distort salary analysis.

---

# 11. Duplicate Data

Duplicate data means the same record occurs more than once.

Example:

```text
Name     Age
John     25
Alice    30
John     25
```

The third row is a duplicate.

---

# 12. Detecting Duplicates

Use:

```python
df.duplicated()
```

Output:

```text
False
False
True
```

---

## Count Duplicates

```python
df.duplicated().sum()
```

---

## Display Duplicate Rows

```python
df[df.duplicated()]
```

---

## Check Duplicates Based on Specific Columns

```python
df.duplicated(
    subset=["Name"]
)
```

---

# 13. Removing Duplicates

Remove duplicate rows:

```python
df.drop_duplicates()
```

Permanent:

```python
df.drop_duplicates(
    inplace=True
)
```

---

## Duplicate Based on Specific Columns

```python
df.drop_duplicates(
    subset=["Name"]
)
```

---

## Keep First Record

```python
df.drop_duplicates(
    keep="first"
)
```

---

## Keep Last Record

```python
df.drop_duplicates(
    keep="last"
)
```

---

## Remove All Duplicate Occurrences

```python
df.drop_duplicates(
    keep=False
)
```

---

# 14. Incorrect Data Types

A column may contain the wrong data type.

Example:

```text
Age
20
21
22
"23"
"24"
```

Check:

```python
df.dtypes
```

---

# 15. Type Conversion

## astype()

```python
df["Age"] = df["Age"].astype(int)
```

Convert to float:

```python
df["Age"] = df["Age"].astype(float)
```

Convert to string:

```python
df["Age"] = df["Age"].astype(str)
```

---

# pd.to_numeric()

This is safer when the column contains invalid values.

```python
df["Age"] = pd.to_numeric(
    df["Age"],
    errors="coerce"
)
```

Invalid values become `NaN`.

---

## Example

Suppose:

```text
Age
20
25
unknown
30
```

Run:

```python
df["Age"] = pd.to_numeric(
    df["Age"],
    errors="coerce"
)
```

Result:

```text
20
25
NaN
30
```

Then handle the missing value:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

# 16. String Cleaning

Text data frequently contains inconsistencies.

Example:

```text
" John"
"John "
" JOHN "
"john"
```

These may represent the same person.

---

# 17. Removing Extra Spaces

Use:

```python
df["Name"] = df["Name"].str.strip()
```

---

## Left Spaces

```python
df["Name"] = df["Name"].str.lstrip()
```

---

## Right Spaces

```python
df["Name"] = df["Name"].str.rstrip()
```

---

# 18. Standardizing Text

Convert to lowercase:

```python
df["City"] = df["City"].str.lower()
```

Convert to uppercase:

```python
df["City"] = df["City"].str.upper()
```

Convert to title case:

```python
df["City"] = df["City"].str.title()
```

---

## Recommended Cleaning Pattern

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.lower()
)
```

This converts:

```text
" Delhi "
"DELHI"
"delhi "
```

into:

```text
"delhi"
```

---

# 19. Replacing Values

Use:

```python
replace()
```

Example:

```python
df["Gender"] = df["Gender"].replace({
    "M": "Male",
    "F": "Female"
})
```

---

## Multiple Incorrect Values

```python
df["City"] = df["City"].replace({
    "Hyd": "Hyderabad",
    "Hydrabad": "Hyderabad",
    "Bengaluru": "Bangalore"
})
```

---

# 20. Handling Invalid Values

Sometimes values are present but logically incorrect.

Example:

```text
Age
20
25
-5
300
30
```

`-5` and `300` are probably invalid ages.

---

## Find Invalid Values

```python
df[
    (df["Age"] < 0) |
    (df["Age"] > 120)
]
```

---

## Replace Invalid Values With NaN

```python
import numpy as np

df.loc[
    (df["Age"] < 0) |
    (df["Age"] > 120),
    "Age"
] = np.nan
```

Then fill:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

# 21. Date and Time Cleaning

Dates can appear in different formats:

```text
01/02/2025
2025-02-01
Feb 1, 2025
01-Feb-2025
```

For analysis, convert them to a proper datetime type.

---

## Convert to Datetime

```python
df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)
```

Invalid dates become `NaT`.

`NaT` means:

```text
Not a Time
```

---

## Extract Year

```python
df["Year"] = df["Date"].dt.year
```

---

## Extract Month

```python
df["Month"] = df["Date"].dt.month
```

---

## Extract Day

```python
df["Day"] = df["Date"].dt.day
```

---

## Day Name

```python
df["Day_Name"] = (
    df["Date"].dt.day_name()
)
```

---

## Month Name

```python
df["Month_Name"] = (
    df["Date"].dt.month_name()
)
```

---

# 22. Categorical Data Cleaning

Categorical data contains a limited number of categories.

Example:

```text
Gender
Male
Female
M
F
male
female
```

Standardize:

```python
df["Gender"] = (
    df["Gender"]
    .str.strip()
    .str.lower()
)
```

Then replace:

```python
df["Gender"] = df["Gender"].replace({
    "m": "male",
    "f": "female"
})
```

---

## Convert to Category

```python
df["Gender"] = (
    df["Gender"].astype("category")
)
```

This can reduce memory usage when a column has relatively few repeated categories.

---

# 23. Outliers

An **outlier** is a value that is unusually far from the rest of the data.

Example:

```text
Salary:

30000
35000
40000
45000
50000
5000000
```

`5,000,000` may be an outlier.

But remember:

> **An outlier is not automatically an error.**

A very high salary could be a genuine executive salary.

Always investigate before removing it.

---

# 24. Detecting Outliers Using IQR

IQR means:

```text
Interquartile Range
```

Formula:

```text
IQR = Q3 - Q1
```

Where:

```text
Q1 = 25th percentile
Q3 = 75th percentile
```

Outlier boundaries:

```text
Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR
```

---

## Calculate IQR

```python
Q1 = df["Salary"].quantile(0.25)

Q3 = df["Salary"].quantile(0.75)

IQR = Q3 - Q1
```

Calculate boundaries:

```python
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

Find outliers:

```python
outliers = df[
    (df["Salary"] < lower) |
    (df["Salary"] > upper)
]
```

---

# 25. Handling Outliers

There is no single correct method.

Possible approaches:

```text
Keep
Remove
Cap
Transform
Investigate
```

---

## Remove Outliers

```python
df = df[
    (df["Salary"] >= lower) &
    (df["Salary"] <= upper)
]
```

---

## Cap Outliers

Using `clip()`:

```python
df["Salary"] = df["Salary"].clip(
    lower=lower,
    upper=upper
)
```

This replaces values outside the limits with the boundary values.

---

## Log Transformation

For heavily skewed positive data:

```python
import numpy as np

df["Salary_Log"] = np.log1p(
    df["Salary"]
)
```

This changes the scale rather than simply deleting observations.

---

# 26. Data Validation

After cleaning, validate your dataset.

Check:

```python
df.info()
```

Check missing values:

```python
df.isna().sum()
```

Check duplicates:

```python
df.duplicated().sum()
```

Check data types:

```python
df.dtypes
```

Check numeric statistics:

```python
df.describe()
```

Check unique values:

```python
df["Gender"].value_counts()
```

---

# 27. Inconsistent Data

Inconsistent data means the same information is represented differently.

Example:

```text
Hyderabad
hyderabad
HYDERABAD
Hyd
Hydrabad
```

Clean it:

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.lower()
)
```

Then fix known variations:

```python
df["City"] = df["City"].replace({
    "hyd": "hyderabad",
    "hydrabad": "hyderabad"
})
```

---

# 28. Renaming Columns

Raw datasets may have bad column names:

```text
Customer Name
customer name
Customer_Name
customer-name
```

Standardize them.

---

## Rename Specific Columns

```python
df.rename(
    columns={
        "Customer Name": "customer_name"
    },
    inplace=True
)
```

---

## Convert All Columns to Lowercase

```python
df.columns = (
    df.columns
    .str.lower()
)
```

---

## Replace Spaces With Underscores

```python
df.columns = (
    df.columns
    .str.lower()
    .str.strip()
    .str.replace(" ", "_")
)
```

Example:

```text
Customer Name
Customer Age
Total Salary
```

becomes:

```text
customer_name
customer_age
total_salary
```

---

# 29. Removing Unnecessary Columns

Sometimes datasets contain columns that are not required.

Example:

```text
Name
Age
Salary
Unnamed: 0
```

Remove:

```python
df.drop(
    columns=["Unnamed: 0"],
    inplace=True
)
```

---

## Detect Unnamed Columns

```python
unnamed = [
    col for col in df.columns
    if col.startswith("Unnamed")
]
```

Remove them:

```python
df.drop(
    columns=unnamed,
    inplace=True
)
```

---

# 30. Handling Wrong Records

Suppose:

```text
Age
20
25
30
500
35
```

You can identify:

```python
invalid_age = df[
    (df["Age"] < 0) |
    (df["Age"] > 120)
]
```

Instead of blindly deleting:

```text
1. Investigate
2. Determine whether it is an error
3. Correct it if possible
4. Otherwise remove or mark it missing
```

---

# 31. Cleaning Multiple Columns

Suppose:

```text
Name
City
Country
```

all contain extra spaces.

You can clean multiple string columns:

```python
string_columns = [
    "Name",
    "City",
    "Country"
]

for col in string_columns:
    df[col] = (
        df[col]
        .str.strip()
        .str.title()
    )
```

---

# Cleaning All Object/String Columns

```python
string_columns = (
    df.select_dtypes(
        include="object"
    ).columns
)

for col in string_columns:
    df[col] = (
        df[col]
        .str.strip()
    )
```

---

# 32. Cleaning CSV Data

A common real-world situation:

```text
You receive a CSV file
        ↓
Load it
        ↓
Inspect it
        ↓
Clean it
        ↓
Analyze it
        ↓
Save cleaned CSV
```

---

## Load CSV

```python
import pandas as pd

df = pd.read_csv(
    "raw_data.csv"
)
```

---

## Inspect

```python
print(df.head())
print(df.shape)
print(df.info())
print(df.describe())
```

---

## Missing Values

```python
print(
    df.isna().sum()
)
```

---

## Duplicates

```python
print(
    df.duplicated().sum()
)
```

---

## Clean Text

```python
df["Name"] = (
    df["Name"]
    .str.strip()
    .str.title()
)
```

---

## Convert Numeric Column

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

---

## Fill Missing Salary

```python
df["Salary"] = (
    df["Salary"]
    .fillna(df["Salary"].median())
)
```

---

## Remove Duplicates

```python
df.drop_duplicates(
    inplace=True
)
```

---

## Save Cleaned Data

```python
df.to_csv(
    "cleaned_data.csv",
    index=False
)
```

---

# 33. Complete Data Cleaning Example

Let's create a deliberately messy dataset.

```python
import pandas as pd
import numpy as np

data = {
    "Name": [
        " John ",
        "ALICE",
        "bob",
        " John ",
        None
    ],

    "Age": [
        25,
        None,
        30,
        25,
        -5
    ],

    "City": [
        "hyderabad",
        " Hyderabad ",
        "HYDERABAD",
        "hyderabad",
        "Delhi"
    ],

    "Salary": [
        "50000",
        "60000",
        "abc",
        "50000",
        "70000"
    ]
}

df = pd.DataFrame(data)

print(df)
```

---

## Step 1 — Inspect

```python
print(df.head())
print(df.info())
print(df.describe(include="all"))
```

---

## Step 2 — Check Missing Values

```python
print(
    df.isna().sum()
)
```

---

## Step 3 — Clean Names

```python
df["Name"] = (
    df["Name"]
    .str.strip()
    .str.title()
)
```

---

## Step 4 — Clean Cities

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.lower()
)
```

---

## Step 5 — Standardize City Names

```python
df["City"] = df["City"].replace({
    "hyd": "hyderabad"
})
```

The example already uses variants that normalize to the same lowercase spelling.

---

## Step 6 — Convert Salary

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

`"abc"` becomes `NaN`.

---

## Step 7 — Detect Invalid Age

```python
df.loc[
    (df["Age"] < 0) |
    (df["Age"] > 120),
    "Age"
] = np.nan
```

---

## Step 8 — Fill Age

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

## Step 9 — Fill Salary

```python
df["Salary"] = df["Salary"].fillna(
    df["Salary"].median()
)
```

---

## Step 10 — Remove Duplicates

```python
df.drop_duplicates(
    inplace=True
)
```

---

## Step 11 — Validate

```python
print(df.info())

print(
    df.isna().sum()
)

print(
    df.duplicated().sum()
)
```

---

## Step 12 — Save

```python
df.to_csv(
    "cleaned_data.csv",
    index=False
)
```

---

# 34. Complete Professional Data Cleaning Pipeline

Here is a reusable template.

```python
import pandas as pd
import numpy as np

# ==========================================
# 1. LOAD DATA
# ==========================================

df = pd.read_csv("raw_data.csv")


# ==========================================
# 2. INITIAL INSPECTION
# ==========================================

print("Shape:")
print(df.shape)

print("\nColumns:")
print(df.columns)

print("\nData Types:")
print(df.dtypes)

print("\nInformation:")
df.info()

print("\nFirst 5 Rows:")
print(df.head())


# ==========================================
# 3. STANDARDIZE COLUMN NAMES
# ==========================================

df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(" ", "_")
)


# ==========================================
# 4. REMOVE COMPLETELY EMPTY COLUMNS
# ==========================================

df.dropna(
    axis=1,
    how="all",
    inplace=True
)


# ==========================================
# 5. CHECK DUPLICATES
# ==========================================

print(
    "Duplicates:",
    df.duplicated().sum()
)


# ==========================================
# 6. REMOVE DUPLICATES
# ==========================================

df.drop_duplicates(
    inplace=True
)


# ==========================================
# 7. CLEAN STRING COLUMNS
# ==========================================

string_columns = (
    df.select_dtypes(
        include="object"
    ).columns
)

for col in string_columns:
    df[col] = (
        df[col]
        .str.strip()
    )


# ==========================================
# 8. CONVERT NUMERIC COLUMNS
# ==========================================

# Example:
# df["age"] = pd.to_numeric(
#     df["age"],
#     errors="coerce"
# )


# ==========================================
# 9. CONVERT DATE COLUMNS
# ==========================================

# Example:
# df["date"] = pd.to_datetime(
#     df["date"],
#     errors="coerce"
# )


# ==========================================
# 10. CHECK MISSING VALUES
# ==========================================

print("\nMissing Values:")
print(df.isna().sum())


# ==========================================
# 11. HANDLE MISSING VALUES
# ==========================================

# Example:
# df["age"] = df["age"].fillna(
#     df["age"].median()
# )


# ==========================================
# 12. FINAL VALIDATION
# ==========================================

print("\nFinal Shape:")
print(df.shape)

print("\nFinal Data Types:")
print(df.dtypes)

print("\nRemaining Missing Values:")
print(df.isna().sum())

print("\nRemaining Duplicates:")
print(df.duplicated().sum())


# ==========================================
# 13. SAVE CLEAN DATA
# ==========================================

df.to_csv(
    "cleaned_data.csv",
    index=False
)
```

---

# 35. Data Cleaning Checklist

Before considering your dataset clean, check:

## Structure

```text
☐ Correct number of rows
☐ Correct columns
☐ No unnecessary columns
☐ Column names standardized
```

## Missing Data

```text
☐ Missing values identified
☐ Missing values analyzed
☐ Appropriate strategy selected
☐ Missing values handled
```

## Duplicates

```text
☐ Duplicate rows identified
☐ Duplicate rows removed when appropriate
```

## Data Types

```text
☐ Numeric columns are numeric
☐ Date columns are datetime
☐ Categorical columns are appropriate
☐ Boolean columns are boolean
```

## Text

```text
☐ Extra spaces removed
☐ Capitalization standardized
☐ Spelling variations corrected
☐ Invalid categories handled
```

## Dates

```text
☐ Dates converted to datetime
☐ Invalid dates handled
☐ Date formats standardized
```

## Numeric Data

```text
☐ Invalid values identified
☐ Negative values checked
☐ Outliers investigated
☐ Units are consistent
```

## Validation

```text
☐ Dataset inspected after cleaning
☐ Missing values checked again
☐ Duplicates checked again
☐ Data types checked again
☐ Statistics checked again
```

---

# 36. Important Pandas Methods for Data Cleaning

## Inspection

```python
df.head()
df.tail()
df.sample()
df.info()
df.describe()
df.shape
df.columns
df.dtypes
```

---

## Missing Values

```python
df.isna()
df.isnull()
df.notna()
df.notnull()

df.isna().sum()

df.fillna()
df.dropna()
```

---

## Duplicates

```python
df.duplicated()
df.duplicated().sum()
df.drop_duplicates()
```

---

## Data Types

```python
df.astype()
pd.to_numeric()
pd.to_datetime()
```

---

## Text Cleaning

```python
.str.strip()
.str.lstrip()
.str.rstrip()

.str.lower()
.str.upper()
.str.title()

.str.replace()
.str.contains()
.str.startswith()
.str.endswith()
.str.split()
.str.len()
```

---

## Value Replacement

```python
df.replace()
```

---

## Sorting

```python
df.sort_values()
df.sort_index()
```

---

## Filtering

```python
df[df["Age"] > 18]

df.loc[]

df.iloc[]

df.query()
```

---

## Statistics

```python
df.mean()
df.median()
df.mode()
df.min()
df.max()
df.std()
df.quantile()
```

---

## Combining

```python
pd.concat()
pd.merge()
df.join()
```

---

# 37. Data Cleaning Interview Questions

## Q1. What is Data Cleaning?

Data cleaning is the process of detecting and correcting missing, incorrect, duplicate, inconsistent, or invalid data.

---

## Q2. How do you find missing values in Pandas?

```python
df.isna().sum()
```

---

## Q3. How do you remove missing values?

```python
df.dropna()
```

---

## Q4. How do you fill missing values?

```python
df.fillna(value)
```

Example:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

## Q5. How do you find duplicates?

```python
df.duplicated().sum()
```

---

## Q6. How do you remove duplicates?

```python
df.drop_duplicates()
```

---

## Q7. How do you convert a column to numeric?

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

---

## Q8. How do you convert a column to datetime?

```python
df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)
```

---

## Q9. How do you remove whitespace?

```python
df["Name"] = df["Name"].str.strip()
```

---

## Q10. How do you standardize text?

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.lower()
)
```

---

## Q11. What is an outlier?

An outlier is an observation that is unusually far from the typical values in a dataset.

---

## Q12. How do you detect outliers using IQR?

```python
Q1 = df["Salary"].quantile(0.25)
Q3 = df["Salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["Salary"] < lower) |
    (df["Salary"] > upper)
]
```

---

## Q13. Should every outlier be removed?

**No.**

An outlier can be:

```text
Data entry error
Measurement error
Fraud
Rare event
Genuine observation
```

Therefore, investigate it before removing it.

---

## Q14. Mean vs Median for Missing Values?

### Mean

Good when the distribution is relatively balanced and not strongly affected by outliers.

### Median

Often better when the data is skewed or contains extreme values.

### Mode

Useful for categorical values.

---

## Q15. What is `errors="coerce"`?

It converts invalid values into missing values.

Example:

```python
pd.to_numeric(
    ["100", "200", "abc"],
    errors="coerce"
)
```

Conceptually:

```text
100
200
NaN
```

---

# 38. Final Revision

## Remember Data Cleaning as:

```text
                DATA CLEANING
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   MISSING       DUPLICATES     INVALID
    VALUES          DATA          DATA
       │             │             │
    fillna()     duplicated()   replace()
    dropna()     drop_duplicates()
       │
       └─────────────┬─────────────┘
                     ↓
                DATA TYPES
                     │
             ┌───────┴────────┐
             ↓                ↓
       to_numeric()      to_datetime()
             │                │
             └───────┬────────┘
                     ↓
               TEXT CLEANING
                     │
       strip / lower / upper / replace
                     ↓
                OUTLIERS
                     │
                  IQR
                     ↓
               VALIDATION
                     │
                     ↓
              CLEAN DATASET
```

---

# ⭐ Most Important Commands

If you are revising Data Cleaning for **Data Analytics interviews**, remember these first:

```python
# Inspect
df.head()
df.info()
df.describe()
df.shape
df.dtypes

# Missing values
df.isna().sum()
df.fillna()
df.dropna()

# Duplicates
df.duplicated().sum()
df.drop_duplicates()

# Type conversion
pd.to_numeric()
pd.to_datetime()
df.astype()

# String cleaning
.str.strip()
.str.lower()
.str.upper()
.str.title()
.str.replace()

# Value replacement
df.replace()

# Filtering
df.loc[]
df.iloc[]
df.query()

# Statistics
df.mean()
df.median()
df.quantile()

# Outliers
Q1 = df["column"].quantile(0.25)
Q3 = df["column"].quantile(0.75)
IQR = Q3 - Q1

# Export
df.to_csv()
df.to_excel()
```

---

# 🧠 Golden Rule of Data Cleaning

> **Never clean data blindly. First understand what the data means, identify why a value is problematic, choose an appropriate treatment, and validate the result afterward.**

The goal is **not to make the dataset look perfect**.

The goal is to make the dataset **accurate, consistent, reliable, and appropriate for the intended analysis**.

---

# 🚀 Data Cleaning → EDA → Visualization

In a typical Data Analytics project:

```text
Raw Dataset
     ↓
Data Cleaning
     ↓
Exploratory Data Analysis (EDA)
     ↓
Statistical Analysis
     ↓
Visualization
     ↓
Business Insights
     ↓
Report / Dashboard
```

And in a Machine Learning project:

```text
Raw Dataset
     ↓
Data Cleaning
     ↓
Feature Engineering
     ↓
Feature Selection
     ↓
Train/Test Split
     ↓
Model Training
     ↓
Model Evaluation
```

**Data cleaning is therefore one of the most important skills to master before moving into EDA, visualization, and machine learning.**
