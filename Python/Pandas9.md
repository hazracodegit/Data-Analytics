# 🐼 Pandas — Complete Guide for Python & Data Analytics

> **Pandas is one of the most important Python libraries for Data Analysis, Data Science, Machine Learning, and Data Engineering.**

---

# 📌 Table of Contents

1. [What is Pandas?](#1-what-is-pandas)
2. [Why Use Pandas?](#2-why-use-pandas)
3. [Applications of Pandas](#3-applications-of-pandas)
4. [Installation](#4-installation)
5. [Import Pandas](#5-import-pandas)
6. [Pandas Data Structures](#6-pandas-data-structures)
7. [Series](#7-series)
8. [DataFrame](#8-dataframe)
9. [Creating DataFrames](#9-creating-dataframes)
10. [DataFrame Attributes](#10-dataframe-attributes)
11. [Viewing Data](#11-viewing-data)
12. [Selecting Columns](#12-selecting-columns)
13. [Selecting Rows](#13-selecting-rows)
14. [loc and iloc](#14-loc-and-iloc)
15. [Filtering Data](#15-filtering-data)
16. [Adding Columns](#16-adding-columns)
17. [Updating Columns](#17-updating-columns)
18. [Deleting Rows and Columns](#18-deleting-rows-and-columns)
19. [Missing Values](#19-missing-values)
20. [Handling Duplicates](#20-handling-duplicates)
21. [Sorting](#21-sorting)
22. [Renaming](#22-renaming)
23. [Data Types](#23-data-types)
24. [Type Conversion](#24-type-conversion)
25. [String Operations](#25-string-operations)
26. [Mathematical Operations](#26-mathematical-operations)
27. [Statistical Operations](#27-statistical-operations)
28. [describe()](#28-describe)
29. [GroupBy](#29-groupby)
30. [Aggregation](#30-aggregation)
31. [apply(), map(), applymap()](#31-apply-map-applymap)
32. [Combining Data](#32-combining-data)
33. [concat()](#33-concat)
34. [merge()](#34-merge)
35. [join()](#35-join)
36. [pivot() and pivot_table()](#36-pivot-and-pivot_table)
37. [melt()](#37-melt)
38. [Reading Files](#38-reading-files)
39. [Writing Files](#39-writing-files)
40. [CSV Operations](#40-csv-operations)
41. [Excel Operations](#41-excel-operations)
42. [JSON Operations](#42-json-operations)
43. [Date and Time](#43-date-and-time)
44. [Index Operations](#44-index-operations)
45. [Categorical Data](#45-categorical-data)
46. [Data Cleaning](#46-data-cleaning)
47. [Data Analysis Workflow](#47-data-analysis-workflow)
48. [Pandas in Data Analytics](#48-pandas-in-data-analytics)
49. [Pandas vs NumPy](#49-pandas-vs-numpy)
50. [Important Pandas Methods Cheat Sheet](#50-important-pandas-methods-cheat-sheet)
51. [Common Interview Questions](#51-common-interview-questions)

---

# 1. What is Pandas?

**Pandas** is an open-source Python library used for:

* Data manipulation
* Data cleaning
* Data analysis
* Data preprocessing
* Data transformation
* Data exploration
* Working with structured data

Pandas provides two main data structures:

```text
Series
DataFrame
```

Example:

```python
import pandas as pd

data = {
    "Name": ["John", "Alice", "Bob"],
    "Age": [20, 21, 22],
    "Marks": [85, 90, 78]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name  Age  Marks
0   John   20     85
1  Alice   21     90
2    Bob   22     78
```

---

# 2. Why Use Pandas?

Raw Python data structures can become difficult to manage when datasets become large.

Pandas makes data manipulation much easier.

### Without Pandas

```python
students = [
    ["John", 20, 85],
    ["Alice", 21, 90],
    ["Bob", 22, 78]
]
```

Accessing and manipulating columns manually is inconvenient.

### With Pandas

```python
df["Marks"]
```

Filtering:

```python
df[df["Marks"] > 80]
```

Average:

```python
df["Marks"].mean()
```

Sorting:

```python
df.sort_values("Marks")
```

Grouping:

```python
df.groupby("Age")["Marks"].mean()
```

---

# 3. Applications of Pandas

Pandas is heavily used in:

### 📊 Data Analytics

* Data cleaning
* Data transformation
* Statistical analysis
* Exploratory Data Analysis (EDA)
* Report generation

### 🤖 Machine Learning

Pandas is commonly used to:

* Load datasets
* Clean datasets
* Handle missing values
* Encode categorical data
* Select features
* Prepare data for ML algorithms

### 💰 Finance

* Stock analysis
* Financial reports
* Transaction analysis
* Time-series analysis

### 🛒 Business

* Sales analysis
* Customer analysis
* Product analysis
* Revenue analysis

### 🔬 Research

* Experimental data analysis
* Statistical calculations
* Data preprocessing

---

# 4. Installation

Install Pandas using pip:

```bash
pip install pandas
```

Check installation:

```python
import pandas as pd

print(pd.__version__)
```

---

# 5. Import Pandas

Standard import:

```python
import pandas as pd
```

`pd` is the commonly used alias.

Example:

```python
import pandas as pd

df = pd.DataFrame()
```

---

# 6. Pandas Data Structures

Pandas mainly provides:

```text
Series
DataFrame
```

---


# 📊 Series vs DataFrame

Both **Series** and **DataFrame** are fundamental Pandas data structures.

| Feature                          | Series                 | DataFrame                             |
| -------------------------------- | ---------------------- | ------------------------------------- |
| Dimension                        | 1-Dimensional          | 2-Dimensional                         |
| Structure                        | Single column of data  | Rows and multiple columns             |
| Similar to                       | A single column        | A complete table                      |
| Has Index                        | ✅ Yes                  | ✅ Yes                                 |
| Has Columns                      | ❌ No                   | ✅ Yes                                 |
| Can contain different data types | Usually one main dtype | Different dtype for each column       |
| Created using                    | `pd.Series()`          | `pd.DataFrame()`                      |
| Example                          | `[10, 20, 30]`         | `{"Name": [...], "Age": [...]}`       |
| Access                           | `s[0]` / `s["A"]`      | `df["Name"]`, `df.loc[]`, `df.iloc[]` |
| Shape                            | `(n,)`                 | `(rows, columns)`                     |

---

## Series

A **Series** is a one-dimensional labeled data structure.

```python
import pandas as pd

s = pd.Series(
    [80, 90, 75],
    index=["John", "Alice", "Bob"]
)

print(s)
```

Output:

```text
John     80
Alice    90
Bob      75
dtype: int64
```

Think of a Series as **one column**:

```text
John     → 80
Alice    → 90
Bob      → 75
```

---

## DataFrame

A **DataFrame** is a two-dimensional labeled data structure.

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["John", "Alice", "Bob"],
    "Age": [20, 21, 22],
    "Marks": [80, 90, 75]
})

print(df)
```

Output:

```text
    Name  Age  Marks
0   John   20     80
1  Alice   21     90
2    Bob   22     75
```

Think of a DataFrame as a **complete table**.

---

## Relationship Between Series and DataFrame

A DataFrame is essentially a collection of Series that share the same index.

```text
             DataFrame
    ┌──────────┬──────┬───────┐
    │   Name   │ Age  │ Marks │
    ├──────────┼──────┼───────┤
    │ John     │ 20   │ 80    │
    │ Alice    │ 21   │ 90    │
    │ Bob      │ 22   │ 75    │
    └──────────┴──────┴───────┘
         ↓        ↓       ↓
       Series   Series  Series
```

For example:

```python
names = df["Name"]
ages = df["Age"]
marks = df["Marks"]
```

Each of these is a **Series**.

```python
print(type(names))
```

Output:

```text
<class 'pandas.core.series.Series'>
```

Whereas:

```python
print(type(df))
```

Output:

```text
<class 'pandas.core.frame.DataFrame'>
```

---

## Converting Series to DataFrame

A Series can be converted into a DataFrame:

```python
s = pd.Series([10, 20, 30])

df = s.to_frame(
    name="Marks"
)

print(df)
```

Output:

```text
   Marks
0     10
1     20
2     30
```

---

## Selecting One Column vs Multiple Columns

### One column → Series

```python
df["Name"]
```

Result:

```text
0     John
1    Alice
2      Bob
```

Type:

```python
type(df["Name"])
```

```text
Series
```

### Multiple columns → DataFrame

```python
df[["Name", "Age"]]
```

Result:

```text
    Name  Age
0   John   20
1  Alice   21
2    Bob   22
```

Type:

```python
type(df[["Name", "Age"]])
```

```text
DataFrame
```

### ⭐ Important Interview Point

Remember:

```python
df["Name"]       # Series
df[["Name"]]     # DataFrame
```

The difference is the **double square brackets**.

---

## Quick Memory Trick

```text
Series
   ↓
ONE column
   ↓
1D
```

```text
DataFrame
   ↓
MULTIPLE columns / table
   ↓
2D
```

### Easy analogy

Think of an Excel spreadsheet:

```text
One column          → Series

Entire spreadsheet  → DataFrame
```

### Final Rule

> **Series = one labeled column of data.**
> **DataFrame = a collection of labeled columns forming a table.**
---

# 7. Series

A **Series** is a one-dimensional labeled array.

It can contain:

* Integers
* Floats
* Strings
* Objects
* Dates
* Boolean values

Example:

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

print(s)
```

Output:

```text
0    10
1    20
2    30
3    40
dtype: int64
```

The left side is the **index**.

The right side is the **value**.

---

## Creating Series

### From List

```python
s = pd.Series([10, 20, 30])
```

### With Custom Index

```python
s = pd.Series(
    [10, 20, 30],
    index=["a", "b", "c"]
)

print(s)
```

Output:

```text
a    10
b    20
c    30
```

### From Dictionary

```python
data = {
    "Math": 90,
    "Science": 85,
    "English": 88
}

s = pd.Series(data)
```

---

## Access Series Elements

```python
print(s[0])
```

Label-based:

```python
print(s["Math"])
```

Multiple values:

```python
print(s[["Math", "English"]])
```

---

# 8. DataFrame

A **DataFrame** is a two-dimensional labeled data structure.

Think of it as a table.

```text
Rows    → Records
Columns → Features
```

Example:

```python
data = {
    "Name": ["John", "Alice", "Bob"],
    "Age": [20, 21, 22],
    "Marks": [85, 90, 78]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name  Age  Marks
0   John   20     85
1  Alice   21     90
2    Bob   22     78
```

---

# 9. Creating DataFrames

## From Dictionary

```python
data = {
    "Name": ["John", "Alice"],
    "Age": [20, 21]
}

df = pd.DataFrame(data)
```

---

## From List of Lists

```python
data = [
    ["John", 20],
    ["Alice", 21],
    ["Bob", 22]
]

df = pd.DataFrame(
    data,
    columns=["Name", "Age"]
)
```

---

## From List of Dictionaries

```python
data = [
    {"Name": "John", "Age": 20},
    {"Name": "Alice", "Age": 21}
]

df = pd.DataFrame(data)
```

---

## Empty DataFrame

```python
df = pd.DataFrame()

print(df)
```

---

# 10. DataFrame Attributes

Attributes provide information about the DataFrame.

---

## shape

Returns:

```text
(number of rows, number of columns)
```

```python
print(df.shape)
```

Example:

```text
(100, 5)
```

---

## columns

```python
print(df.columns)
```

---

## index

```python
print(df.index)
```

---

## dtypes

Shows data type of each column.

```python
print(df.dtypes)
```

---

## size

Total number of elements:

```python
print(df.size)
```

---

## ndim

Number of dimensions:

```python
print(df.ndim)
```

DataFrame:

```text
2
```

---

## values

Returns underlying values:

```python
print(df.values)
```

---

# 11. Viewing Data

## head()

Displays first 5 rows.

```python
df.head()
```

First 10 rows:

```python
df.head(10)
```

---

## tail()

Last 5 rows:

```python
df.tail()
```

Last 10:

```python
df.tail(10)
```

---

## sample()

Random rows:

```python
df.sample()
```

Multiple:

```python
df.sample(5)
```

---

## info()

Provides important DataFrame information.

```python
df.info()
```

Shows:

* Column names
* Number of entries
* Data types
* Non-null values
* Memory usage

---

# 12. Selecting Columns

Suppose:

```python
df = pd.DataFrame({
    "Name": ["John", "Alice", "Bob"],
    "Age": [20, 21, 22],
    "Marks": [85, 90, 78]
})
```

---

## Single Column

```python
print(df["Name"])
```

Returns a Series.

---

## Multiple Columns

```python
print(df[["Name", "Marks"]])
```

Returns a DataFrame.

---

# 13. Selecting Rows

## Using Index

```python
df.iloc[0]
```

First row.

---

## Multiple Rows

```python
df.iloc[0:3]
```

---

## Specific Rows

```python
df.iloc[[0, 2]]
```

---

# 14. loc and iloc

These are extremely important.

---

# loc

`loc` is primarily **label-based indexing**.

```python
df.loc[0]
```

Specific row and column:

```python
df.loc[0, "Name"]
```

Multiple:

```python
df.loc[0:2, ["Name", "Marks"]]
```

---

# iloc

`iloc` is **integer-position based indexing**.

```python
df.iloc[0]
```

First row.

```python
df.iloc[0, 1]
```

First row, second column.

```python
df.iloc[0:2, 0:2]
```

---

## Difference

| loc                 | iloc                   |
| ------------------- | ---------------------- |
| Label based         | Position based         |
| Uses labels         | Uses integer positions |
| `df.loc[0, "Name"]` | `df.iloc[0, 0]`        |

---

# 15. Filtering Data

Filtering means selecting rows based on conditions.

Example:

```python
df[df["Marks"] > 80]
```

---

## Equal

```python
df[df["Age"] == 20]
```

## Not Equal

```python
df[df["Age"] != 20]
```

## Greater Than

```python
df[df["Marks"] > 80]
```

## Less Than

```python
df[df["Marks"] < 80]
```

## Greater Than or Equal

```python
df[df["Marks"] >= 80]
```

---

# Multiple Conditions

Use:

```text
&  → AND
|  → OR
~  → NOT
```

### AND

```python
df[
    (df["Age"] > 20) &
    (df["Marks"] > 80)
]
```

### OR

```python
df[
    (df["Marks"] > 90) |
    (df["Age"] < 21)
]
```

### NOT

```python
df[~(df["Age"] > 20)]
```

---

# isin()

Check whether values belong to a list.

```python
df[df["Age"].isin([20, 22])]
```

---

# between()

```python
df[df["Marks"].between(70, 90)]
```

---

# query()

```python
df.query("Marks > 80")
```

Multiple conditions:

```python
df.query("Age > 20 and Marks > 80")
```

---

# 16. Adding Columns

Create a new column:

```python
df["Passed"] = True
```

---

## Column Based on Calculation

```python
df["Total"] = df["Marks"] + 10
```

---

## Conditional Column

```python
df["Result"] = df["Marks"].apply(
    lambda x: "Pass" if x >= 40 else "Fail"
)
```

---

# 17. Updating Columns

Change values:

```python
df["Age"] = df["Age"] + 1
```

Update one value:

```python
df.loc[0, "Age"] = 25
```

---

# 18. Deleting Rows and Columns

## Drop Column

```python
df.drop("Age", axis=1)
```

`axis=1` means columns.

---

## Permanently Remove Column

```python
df.drop("Age", axis=1, inplace=True)
```

---

## Drop Multiple Columns

```python
df.drop(
    ["Age", "Marks"],
    axis=1,
    inplace=True
)
```

---

## Drop Row

```python
df.drop(0)
```

---

## Drop Multiple Rows

```python
df.drop([0, 2])
```

---

# 19. Missing Values

Missing values are commonly represented as:

```text
NaN
None
NaT
```

---

## Detect Missing Values

```python
df.isna()
```

or:

```python
df.isnull()
```

---

## Count Missing Values

```python
df.isna().sum()
```

---

## Total Missing Values

```python
df.isna().sum().sum()
```

---

# fillna()

Replace missing values.

```python
df["Age"] = df["Age"].fillna(0)
```

---

## Fill with Mean

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)
```

---

## Fill with Median

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

## Fill with Mode

```python
df["City"] = df["City"].fillna(
    df["City"].mode()[0]
)
```

---

# dropna()

Remove rows containing missing values.

```python
df.dropna()
```

Remove columns:

```python
df.dropna(axis=1)
```

---

## dropna Parameters

```python
df.dropna(
    axis=0,
    how="any"
)
```

`how="any"`:

Remove if at least one value is missing.

`how="all"`:

Remove only if all values are missing.

---

# 20. Handling Duplicates

Check duplicates:

```python
df.duplicated()
```

Count:

```python
df.duplicated().sum()
```

Remove:

```python
df.drop_duplicates()
```

Remove based on specific columns:

```python
df.drop_duplicates(
    subset=["Name"]
)
```

---

# 21. Sorting

## Sort by Column

```python
df.sort_values("Marks")
```

Descending:

```python
df.sort_values(
    "Marks",
    ascending=False
)
```

---

## Multiple Columns

```python
df.sort_values(
    ["Age", "Marks"]
)
```

Different directions:

```python
df.sort_values(
    ["Age", "Marks"],
    ascending=[True, False]
)
```

---

# sort_index()

Sort according to index.

```python
df.sort_index()
```

Descending:

```python
df.sort_index(
    ascending=False
)
```

---

# 22. Renaming

Rename columns:

```python
df.rename(
    columns={
        "Name": "Student_Name",
        "Marks": "Score"
    }
)
```

Rename index:

```python
df.rename(
    index={0: "A", 1: "B"}
)
```

---

# 23. Data Types

Check data types:

```python
df.dtypes
```

Common Pandas data types:

```text
int64
float64
bool
object
string
datetime64
category
```

Modern Pandas also supports nullable types such as:

```text
Int64
Float64
boolean
string
```

---

# 24. Type Conversion

Use:

```python
astype()
```

Example:

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

## pd.to_numeric()

Useful when data may contain invalid numeric values.

```python
df["Marks"] = pd.to_numeric(
    df["Marks"],
    errors="coerce"
)
```

`errors="coerce"` converts invalid values to `NaN`.

---

# 25. String Operations

Pandas provides string methods through:

```python
.str
```

Example:

```python
df["Name"].str.upper()
```

---

## lower()

```python
df["Name"].str.lower()
```

---

## upper()

```python
df["Name"].str.upper()
```

---

## title()

```python
df["Name"].str.title()
```

---

## capitalize()

```python
df["Name"].str.capitalize()
```

---

## strip()

Remove leading/trailing spaces:

```python
df["Name"].str.strip()
```

---

## replace()

```python
df["Name"].str.replace(
    "John",
    "Johnny"
)
```

---

## contains()

```python
df[
    df["Name"].str.contains("a")
]
```

Case-insensitive:

```python
df[
    df["Name"].str.contains(
        "a",
        case=False,
        na=False
    )
]
```

---

## startswith()

```python
df["Name"].str.startswith("A")
```

---

## endswith()

```python
df["Name"].str.endswith("n")
```

---

## len()

```python
df["Name"].str.len()
```

---

## split()

```python
df["Name"].str.split(" ")
```

Expand:

```python
df["Name"].str.split(
    " ",
    expand=True
)
```

---

# 26. Mathematical Operations

Suppose:

```python
df["Marks"]
```

---

## Sum

```python
df["Marks"].sum()
```

---

## Mean

```python
df["Marks"].mean()
```

---

## Median

```python
df["Marks"].median()
```

---

## Minimum

```python
df["Marks"].min()
```

---

## Maximum

```python
df["Marks"].max()
```

---

## Standard Deviation

```python
df["Marks"].std()
```

---

## Variance

```python
df["Marks"].var()
```

---

## Count

```python
df["Marks"].count()
```

---

# 27. Statistical Operations

Important functions:

```python
df.sum()
df.mean()
df.median()
df.mode()
df.min()
df.max()
df.std()
df.var()
df.count()
df.quantile()
```

---

## Quantile

```python
df["Marks"].quantile(0.25)
```

25th percentile.

```python
df["Marks"].quantile(0.50)
```

Median.

```python
df["Marks"].quantile(0.75)
```

75th percentile.

---

## Unique Values

```python
df["City"].unique()
```

---

## Number of Unique Values

```python
df["City"].nunique()
```

---

## Frequency Count

```python
df["City"].value_counts()
```

---

# 28. describe()

One of the most important methods for data analysis.

```python
df.describe()
```

For numeric columns it provides:

```text
count
mean
std
min
25%
50%
75%
max
```

---

For categorical columns:

```python
df.describe(include="object")
```

All columns:

```python
df.describe(include="all")
```

---

# 29. GroupBy

`groupby()` is extremely important in Data Analytics.

It allows us to divide data into groups and perform calculations.

Example:

```python
df.groupby("Department")["Salary"].mean()
```

Meaning:

```text
Group employees by Department
        ↓
Select Salary
        ↓
Calculate Mean
```

---

## Group by One Column

```python
df.groupby("City")["Salary"].sum()
```

---

## Group by Multiple Columns

```python
df.groupby(
    ["Department", "Gender"]
)["Salary"].mean()
```

---

# 30. Aggregation

Use:

```python
agg()
```

Example:

```python
df.groupby("Department")["Salary"].agg(
    ["mean", "min", "max", "sum"]
)
```

---

## Named Aggregation

```python
df.groupby("Department").agg(
    average_salary=("Salary", "mean"),
    maximum_salary=("Salary", "max"),
    employee_count=("Salary", "count")
)
```

This produces readable column names.

---

# Common Aggregation Functions

```text
sum
mean
median
min
max
count
std
var
first
last
nunique
```

---

# 31. apply(), map(), applymap()

These are important for transformations.

---

# map()

Usually used with a Series.

```python
df["Gender"].map({
    "M": "Male",
    "F": "Female"
})
```

---

# apply()

Can apply a function to a Series or DataFrame.

```python
df["Marks"].apply(
    lambda x: x + 5
)
```

Example:

```python
def grade(mark):
    if mark >= 90:
        return "A"
    elif mark >= 75:
        return "B"
    elif mark >= 50:
        return "C"
    else:
        return "F"

df["Grade"] = df["Marks"].apply(grade)
```

---

# DataFrame apply()

```python
df.apply(
    lambda column: column.max()
)
```

---

# applymap()

Historically used to apply a function element-by-element across a DataFrame.

In newer Pandas versions, prefer:

```python
df.map(function)
```

for element-wise DataFrame transformations.

Example:

```python
df.map(
    lambda x: str(x).upper()
)
```

---

# 32. Combining Data

Pandas provides several methods to combine datasets:

```text
concat()
merge()
join()
```

---

# 33. concat()

Used to concatenate DataFrames.

---

## Vertical Concatenation

```python
result = pd.concat(
    [df1, df2]
)
```

Rows are combined.

---

## Horizontal Concatenation

```python
result = pd.concat(
    [df1, df2],
    axis=1
)
```

Columns are combined.

---

## Ignore Index

```python
result = pd.concat(
    [df1, df2],
    ignore_index=True
)
```

---

# 34. merge()

`merge()` is similar to SQL JOIN.

Example:

### Customers

```python
customers = pd.DataFrame({
    "CustomerID": [1, 2, 3],
    "Name": ["John", "Alice", "Bob"]
})
```

### Orders

```python
orders = pd.DataFrame({
    "CustomerID": [1, 2, 3],
    "Amount": [500, 700, 300]
})
```

Merge:

```python
result = pd.merge(
    customers,
    orders,
    on="CustomerID"
)
```

---

# Types of Merge

## Inner Join

Only matching records.

```python
pd.merge(
    df1,
    df2,
    on="ID",
    how="inner"
)
```

---

## Left Join

All records from left DataFrame.

```python
pd.merge(
    df1,
    df2,
    on="ID",
    how="left"
)
```

---

## Right Join

All records from right DataFrame.

```python
pd.merge(
    df1,
    df2,
    on="ID",
    how="right"
)
```

---

## Outer Join

All records from both.

```python
pd.merge(
    df1,
    df2,
    on="ID",
    how="outer"
)
```

---

## Cross Join

Cartesian product:

```python
pd.merge(
    df1,
    df2,
    how="cross"
)
```

---

# Different Column Names

```python
pd.merge(
    df1,
    df2,
    left_on="CustomerID",
    right_on="ID"
)
```

---

# 35. join()

`join()` is primarily convenient for combining DataFrames based on their indexes.

```python
result = df1.join(df2)
```

---

# 36. pivot() and pivot_table()

Useful for reshaping data.

---

# pivot()

Example:

```python
df.pivot(
    index="Date",
    columns="Product",
    values="Sales"
)
```

`pivot()` requires combinations of index/columns to be unique.

---

# pivot_table()

More flexible because it supports aggregation.

```python
pd.pivot_table(
    df,
    index="Department",
    columns="Gender",
    values="Salary",
    aggfunc="mean"
)
```

Common `aggfunc`:

```python
"mean"
"sum"
"count"
"min"
"max"
```

---

# 37. melt()

`melt()` converts wide data into long format.

Example:

```python
pd.melt(
    df,
    id_vars=["Name"],
    value_vars=["Math", "Science"]
)
```

Useful when preparing data for analysis and visualization.

---

# 38. Reading Files

Pandas can read many data formats.

Common functions:

```text
read_csv()
read_excel()
read_json()
read_sql()
read_html()
read_parquet()
```

---

# 39. Writing Files

Common methods:

```text
to_csv()
to_excel()
to_json()
to_sql()
to_parquet()
```

---

# 40. CSV Operations

CSV means:

```text
Comma-Separated Values
```

---

## Read CSV

```python
df = pd.read_csv("students.csv")
```

---

## Display

```python
print(df)
```

---

## Save CSV

```python
df.to_csv("output.csv")
```

---

## Without Index

Usually useful when exporting a clean dataset:

```python
df.to_csv(
    "output.csv",
    index=False
)
```

---

## Custom Separator

```python
df = pd.read_csv(
    "data.csv",
    sep=";"
)
```

---

## Specific Columns

```python
df = pd.read_csv(
    "data.csv",
    usecols=["Name", "Age"]
)
```

---

## Read Specific Number of Rows

```python
df = pd.read_csv(
    "data.csv",
    nrows=100
)
```

---

# 41. Excel Operations

Excel support commonly uses an additional engine such as `openpyxl`.

Install:

```bash
pip install openpyxl
```

Read:

```python
df = pd.read_excel("students.xlsx")
```

Write:

```python
df.to_excel(
    "output.xlsx",
    index=False
)
```

---

## Specific Sheet

```python
df = pd.read_excel(
    "students.xlsx",
    sheet_name="Sheet1"
)
```

---

## Read Multiple Sheets

```python
data = pd.read_excel(
    "students.xlsx",
    sheet_name=None
)
```

This returns a dictionary of DataFrames.

---

# 42. JSON Operations

JSON example:

```json
[
    {
        "name": "John",
        "age": 20
    },
    {
        "name": "Alice",
        "age": 21
    }
]
```

Read:

```python
df = pd.read_json("students.json")
```

Write:

```python
df.to_json(
    "output.json"
)
```

---

# 43. Date and Time

Pandas provides powerful date/time functionality.

---

## Convert to DateTime

```python
df["Date"] = pd.to_datetime(
    df["Date"]
)
```

---

## Extract Year

```python
df["Date"].dt.year
```

---

## Month

```python
df["Date"].dt.month
```

---

## Day

```python
df["Date"].dt.day
```

---

## Day Name

```python
df["Date"].dt.day_name()
```

---

## Month Name

```python
df["Date"].dt.month_name()
```

---

## Hour

```python
df["Date"].dt.hour
```

---

## Difference Between Dates

```python
df["End"] - df["Start"]
```

---

## Date Range

```python
dates = pd.date_range(
    start="2025-01-01",
    end="2025-01-10"
)
```

---

# 44. Index Operations

The index identifies rows.

---

## Set Index

```python
df.set_index("ID")
```

---

## Reset Index

```python
df.reset_index()
```

---

## Rename Index

```python
df.index.name = "Student_ID"
```

---

## Check Index

```python
df.index
```

---

# Reindex

```python
df.reindex(
    [2, 0, 1]
)
```

Useful for changing row order or aligning data.

---

# 45. Categorical Data

Categorical data contains a limited number of possible values.

Examples:

```text
Male / Female
Red / Blue / Green
Small / Medium / Large
```

Convert:

```python
df["Gender"] = df["Gender"].astype("category")
```

Check:

```python
df["Gender"].dtype
```

Categories:

```python
df["Gender"].cat.categories
```

---

# 46. Data Cleaning

Data cleaning is one of the most important uses of Pandas.

A typical dataset may contain:

```text
Missing values
Duplicate rows
Incorrect data types
Extra spaces
Invalid values
Inconsistent capitalization
Outliers
Incorrect dates
```

---

## Remove Extra Spaces

```python
df["Name"] = df["Name"].str.strip()
```

---

## Standardize Text

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)
```

---

## Convert Numeric Data

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

---

## Convert Dates

```python
df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
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

## Handle Missing Values

```python
df["Salary"] = df["Salary"].fillna(
    df["Salary"].median()
)
```

---

# Replacing Values

```python
df["Gender"] = df["Gender"].replace({
    "M": "Male",
    "F": "Female"
})
```

---

# replace()

Specific value:

```python
df.replace(
    "Unknown",
    None
)
```

Multiple:

```python
df.replace({
    "N/A": None,
    "NA": None,
    "?": None
})
```

---

# 47. Data Analysis Workflow

A common Pandas workflow looks like this:

```text
        Load Data
           ↓
      Understand Data
           ↓
      Inspect Data
           ↓
     Clean Data
           ↓
   Handle Missing Values
           ↓
    Remove Duplicates
           ↓
    Correct Data Types
           ↓
      Transform Data
           ↓
     Analyze Data
           ↓
    Group / Aggregate
           ↓
     Find Insights
           ↓
     Visualize Results
           ↓
       Export Data
```

---

# Example Complete Workflow

```python
import pandas as pd

# 1. Load dataset
df = pd.read_csv("sales.csv")

# 2. Inspect
print(df.head())
print(df.info())
print(df.describe())

# 3. Check missing values
print(df.isna().sum())

# 4. Remove duplicates
df.drop_duplicates(inplace=True)

# 5. Clean text
df["City"] = df["City"].str.strip().str.title()

# 6. Convert data type
df["Sales"] = pd.to_numeric(
    df["Sales"],
    errors="coerce"
)

# 7. Handle missing values
df["Sales"] = df["Sales"].fillna(
    df["Sales"].median()
)

# 8. Filter
high_sales = df[df["Sales"] > 10000]

# 9. Group
summary = df.groupby("City")["Sales"].sum()

# 10. Sort
summary = summary.sort_values(
    ascending=False
)

print(summary)

# 11. Export
df.to_csv(
    "cleaned_sales.csv",
    index=False
)
```

---

# 48. Pandas in Data Analytics

Pandas is extremely important in the Data Analytics process.

A Data Analyst commonly receives raw data such as:

```text
CSV
Excel
Database
JSON
API
Parquet
```

Pandas can load this data and transform it into an analysis-ready DataFrame.

---

## Typical Data Analytics Process

```text
Raw Data
   ↓
Pandas
   ↓
Data Cleaning
   ↓
Data Transformation
   ↓
Exploratory Data Analysis
   ↓
Aggregation
   ↓
Visualization
   ↓
Business Insights
```

---

# Example: Sales Analysis

Suppose we have:

```text
Date
Product
Category
Region
Quantity
Price
```

Create revenue:

```python
df["Revenue"] = (
    df["Quantity"] *
    df["Price"]
)
```

Total revenue:

```python
df["Revenue"].sum()
```

Revenue by region:

```python
df.groupby("Region")["Revenue"].sum()
```

Revenue by product:

```python
df.groupby("Product")["Revenue"].sum()
```

Top products:

```python
df.groupby("Product")["Revenue"].sum().sort_values(
    ascending=False
).head(10)
```

Monthly analysis:

```python
df["Date"] = pd.to_datetime(df["Date"])

df["Month"] = df["Date"].dt.month

df.groupby("Month")["Revenue"].sum()
```

This is a typical Data Analytics workflow.

---

# 49. Pandas vs NumPy

| Feature                        | NumPy                         | Pandas                             |
| ------------------------------ | ----------------------------- | ---------------------------------- |
| Main structure                 | ndarray                       | Series/DataFrame                   |
| Data type                      | Usually homogeneous           | Can have different types by column |
| Labels                         | No built-in row/column labels | Yes                                |
| Missing data                   | Basic support                 | Extensive support                  |
| Tabular data                   | Less convenient               | Excellent                          |
| Data cleaning                  | Limited                       | Excellent                          |
| GroupBy                        | Limited                       | Powerful                           |
| CSV                            | Basic tools                   | Excellent                          |
| Excel                          | No direct focus               | Supported                          |
| Data analysis                  | Numerical                     | Tabular + analytical               |
| Machine Learning preprocessing | Useful                        | Very useful                        |

### Relationship

Pandas is built heavily around NumPy concepts.

```text
NumPy
  ↓
Numerical Computing

Pandas
  ↓
Data Manipulation + Data Analysis
```

Both are important.

---

# 50. Important Pandas Methods Cheat Sheet

## Creating

```python
pd.Series()
pd.DataFrame()
```

---

## Inspecting

```python
df.head()
df.tail()
df.sample()
df.info()
df.describe()
df.shape
df.size
df.ndim
df.dtypes
df.columns
df.index
```

---

## Selecting

```python
df["column"]
df[["col1", "col2"]]

df.loc[]
df.iloc[]
```

---

## Filtering

```python
df[df["Age"] > 20]

df["City"].isin(["Delhi", "Mumbai"])

df["Marks"].between(50, 90)

df.query("Marks > 80")
```

---

## Missing Data

```python
df.isna()
df.isnull()
df.notna()
df.notnull()

df.fillna()
df.dropna()
```

---

## Duplicates

```python
df.duplicated()
df.drop_duplicates()
```

---

## Sorting

```python
df.sort_values()
df.sort_index()
```

---

## Columns

```python
df.rename()
df.drop()
df.insert()
```

---

## Statistics

```python
df.sum()
df.mean()
df.median()
df.mode()
df.min()
df.max()
df.std()
df.var()
df.count()
df.quantile()
```

---

## Unique Values

```python
df.unique()
df.nunique()
df.value_counts()
```

For a Series:

```python
df["City"].unique()
df["City"].nunique()
df["City"].value_counts()
```

---

## Grouping

```python
df.groupby()
df.agg()
```

---

## Combining

```python
pd.concat()
pd.merge()

df.join()
```

---

## Reshaping

```python
df.pivot()
pd.pivot_table()

df.melt()
```

---

## String Operations

```python
.str.lower()
.str.upper()
.str.title()
.str.strip()
.str.replace()
.str.contains()
.str.startswith()
.str.endswith()
.str.len()
.str.split()
```

---

## Date Operations

```python
pd.to_datetime()

.dt.year
.dt.month
.dt.day
.dt.hour
.dt.minute
.dt.second
.dt.day_name()
.dt.month_name()
```

---

## Input / Output

```python
pd.read_csv()
df.to_csv()

pd.read_excel()
df.to_excel()

pd.read_json()
df.to_json()

pd.read_sql()
df.to_sql()

pd.read_parquet()
df.to_parquet()
```

---

# 51. Important Pandas Concepts to Remember

## Series

```text
1-dimensional
```

Example:

```python
pd.Series([10, 20, 30])
```

---

## DataFrame

```text
2-dimensional
```

Example:

```python
pd.DataFrame({
    "Name": ["A", "B"],
    "Age": [20, 21]
})
```

---

## Index

Identifies rows.

```python
df.index
```

---

## Columns

Identify variables/features.

```python
df.columns
```

---

## loc

Label-based selection.

```python
df.loc[0, "Name"]
```

---

## iloc

Position-based selection.

```python
df.iloc[0, 0]
```

---

## axis

Very important.

```text
axis=0 → rows/index direction
axis=1 → columns direction
```

For example:

```python
df.drop("Age", axis=1)
```

means:

```text
Drop the Age column.
```

---

# ⭐ Most Important Pandas Operations for Data Analytics

If you are preparing for a **Data Analyst / Data Science interview**, make sure you are comfortable with these:

```python
pd.read_csv()
pd.DataFrame()

df.head()
df.tail()
df.info()
df.describe()

df.shape
df.columns
df.dtypes

df["column"]
df[["col1", "col2"]]

df.loc[]
df.iloc[]

df[df["column"] > value]

df.isna().sum()
df.fillna()
df.dropna()

df.drop_duplicates()

df.sort_values()

df.groupby()
df.agg()

pd.merge()
pd.concat()

df.pivot_table()
df.melt()

df["column"].value_counts()
df["column"].unique()
df["column"].nunique()

df["column"].mean()
df["column"].sum()
df["column"].min()
df["column"].max()
df["column"].median()
df["column"].std()

df["column"].str.lower()
df["column"].str.upper()
df["column"].str.strip()

pd.to_datetime()

df.to_csv()
df.to_excel()
```

---

# 🧠 Pandas Mental Model

Remember Pandas like this:

```text
                     PANDAS
                        │
          ┌─────────────┴─────────────┐
          │                           │
       SERIES                      DATAFRAME
          │                           │
    1-Dimensional                2-Dimensional
                                      │
              ┌───────────────────────┼───────────────────────┐
              │                       │                       │
          SELECT                    CLEAN                  ANALYZE
              │                       │                       │
        loc / iloc              fillna / dropna          groupby
        filtering               duplicates               agg
        columns                 replace                  statistics
              │                       │                       │
              └───────────────────────┼───────────────────────┘
                                      │
                                  TRANSFORM
                                      │
                           ┌──────────┼──────────┐
                           │          │          │
                         merge      concat     pivot
                           │          │          │
                           └──────────┼──────────┘
                                      │
                                   EXPORT
                                      │
                         CSV / Excel / JSON
```

---

# 🚀 Complete Example

```python
import pandas as pd

# --------------------------------
# 1. CREATE DATA
# --------------------------------

data = {
    "Name": ["John", "Alice", "Bob", "John"],
    "Age": [20, 21, 22, 20],
    "Department": ["IT", "HR", "IT", "IT"],
    "Salary": [50000, 60000, 55000, 50000]
}

df = pd.DataFrame(data)

# --------------------------------
# 2. INSPECT
# --------------------------------

print(df.head())
print(df.info())
print(df.describe())

# --------------------------------
# 3. CHECK DATA
# --------------------------------

print(df.shape)
print(df.columns)
print(df.dtypes)

# --------------------------------
# 4. REMOVE DUPLICATES
# --------------------------------

df.drop_duplicates(inplace=True)

# --------------------------------
# 5. SELECT
# --------------------------------

print(df["Name"])
print(df[["Name", "Salary"]])

# --------------------------------
# 6. FILTER
# --------------------------------

high_salary = df[
    df["Salary"] > 50000
]

print(high_salary)

# --------------------------------
# 7. CREATE NEW COLUMN
# --------------------------------

df["Bonus"] = df["Salary"] * 0.10

# --------------------------------
# 8. STRING OPERATION
# --------------------------------

df["Name"] = df["Name"].str.upper()

# --------------------------------
# 9. STATISTICS
# --------------------------------

print(df["Salary"].mean())
print(df["Salary"].max())
print(df["Salary"].min())

# --------------------------------
# 10. GROUPBY
# --------------------------------

department_salary = (
    df.groupby("Department")["Salary"]
    .mean()
)

print(department_salary)

# --------------------------------
# 11. SORT
# --------------------------------

df = df.sort_values(
    "Salary",
    ascending=False
)

# --------------------------------
# 12. EXPORT
# --------------------------------

df.to_csv(
    "employees.csv",
    index=False
)
```

---

# 🎯 Final Revision Summary

### Pandas is mainly used for:

```text
Data Loading
     ↓
Data Inspection
     ↓
Data Cleaning
     ↓
Data Transformation
     ↓
Data Filtering
     ↓
Data Aggregation
     ↓
Data Analysis
     ↓
Data Export
```

### Two primary structures:

```text
Series    → 1D
DataFrame → 2D
```

### Most important concepts:

```text
DataFrame
Series
Index
loc
iloc
Filtering
Missing Values
Duplicates
Sorting
Grouping
Aggregation
Merging
Concatenation
Pivot Tables
String Operations
DateTime
File I/O
Data Cleaning
Statistical Analysis
```

### The most important methods to memorize:

```python
read_csv()
DataFrame()

head()
tail()
info()
describe()

loc[]
iloc[]

isna()
fillna()
dropna()

drop_duplicates()
sort_values()

groupby()
agg()

merge()
concat()

pivot_table()
melt()

value_counts()
unique()
nunique()

mean()
median()
sum()
min()
max()
std()
var()

to_datetime()

to_csv()
to_excel()
```

---

# 🏆 One-Line Interview Definitions

**Pandas:**

> A Python library used for data manipulation, data cleaning, analysis, and handling structured/tabular data.

**Series:**

> A one-dimensional labeled array in Pandas.

**DataFrame:**

> A two-dimensional labeled tabular data structure consisting of rows and columns.

**loc:**

> Label-based data selection.

**iloc:**

> Integer-position-based data selection.

**groupby():**

> Used to split data into groups and perform operations such as aggregation.

**merge():**

> Used to combine DataFrames based on common columns or indexes, similar to SQL joins.

**concat():**

> Used to concatenate multiple Pandas objects along rows or columns.

**fillna():**

> Used to replace missing values.

**dropna():**

> Used to remove missing values.

**drop_duplicates():**

> Used to remove duplicate rows.

**describe():**

> Generates descriptive statistics for numerical and other applicable columns.

**value_counts():**

> Counts the frequency of unique values in a Series.

**pivot_table():**

> Creates a spreadsheet-style summary table with aggregation.

---

# 📚 Recommended Learning Order

For learning Pandas efficiently, follow this order:

```text
1. Series
      ↓
2. DataFrame
      ↓
3. Creating DataFrames
      ↓
4. head(), tail(), info(), describe()
      ↓
5. Columns and Index
      ↓
6. loc and iloc
      ↓
7. Filtering
      ↓
8. Missing Values
      ↓
9. Duplicates
      ↓
10. Sorting
      ↓
11. String Operations
      ↓
12. DateTime
      ↓
13. Statistics
      ↓
14. GroupBy
      ↓
15. Aggregation
      ↓
16. apply() / map()
      ↓
17. concat()
      ↓
18. merge()
      ↓
19. join()
      ↓
20. pivot_table()
      ↓
21. melt()
      ↓
22. File Handling
      ↓
23. Data Cleaning
      ↓
24. Exploratory Data Analysis
```

> **For Data Analytics, don't just memorize Pandas methods. Practice taking a messy CSV, cleaning it, filtering it, grouping it, calculating KPIs, and extracting business insights. That is where Pandas becomes most useful.**
