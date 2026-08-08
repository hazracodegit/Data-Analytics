# 📊 Data Manipulation with Python & Pandas — Complete Notes

> **Data Manipulation** is the process of transforming, organizing, filtering, combining, and modifying data so that it can be analyzed effectively.

This is one of the most important skills in **Data Analytics**, because real-world data rarely comes in the exact structure required for analysis.

---


# 🔗 Data Cleaning vs Data Manipulation

## 1. Relationship Between Data Cleaning and Data Manipulation

**Data Cleaning** and **Data Manipulation** are two different stages of preparing data for analysis, but they are closely related.

A typical data analytics workflow is:

```text
Raw Data
   ↓
Data Collection
   ↓
Data Cleaning
   ↓
Clean Data
   ↓
Data Manipulation / Transformation
   ↓
Analysis-Ready Data
   ↓
Data Analysis
   ↓
Visualization
   ↓
Business Insights
```

However, in real-world projects, these steps are **not always strictly sequential**.

You may clean and manipulate data repeatedly:

```text
Raw Data
   ↓
Clean
   ↓
Manipulate
   ↓
Discover an issue
   ↓
Clean again
   ↓
Manipulate again
   ↓
Final Dataset
```

So, data cleaning and manipulation are often part of an **iterative data preparation process**.

---

# 2. What is Data Cleaning?

**Data Cleaning** is the process of identifying and correcting or handling inaccurate, incomplete, inconsistent, duplicate, or invalid data.

The main goal is:

> **Make the data correct, consistent, reliable, and usable.**

### Examples

```text
Missing values
      ↓
Handle them

Duplicate records
      ↓
Remove them

"India", "india", "INDIA"
      ↓
Standardize them

Age = -25
      ↓
Identify invalid value

"25 years"
      ↓
Convert to numeric if appropriate
```

Common data-cleaning operations include:

```python
df.drop_duplicates()

df.dropna()

df.fillna()

df["Age"] = pd.to_numeric(
    df["Age"],
    errors="coerce"
)

df["Name"] = df["Name"].str.strip()
```

---

# 3. What is Data Manipulation?

**Data Manipulation** is the process of selecting, transforming, organizing, combining, reshaping, and modifying data to make it suitable for analysis.

The main goal is:

> **Convert usable data into a form that answers analytical questions.**

Examples:

```text
Filter customers
       ↓
Group sales by region
       ↓
Calculate total revenue
       ↓
Create profit column
       ↓
Merge customer and sales data
       ↓
Create monthly summary
       ↓
Reshape data for reporting
```

Common manipulation operations:

```python
df[df["Sales"] > 50000]

df["Profit"] = df["Revenue"] - df["Cost"]

df.groupby("Region")["Sales"].sum()

pd.merge(customers, sales, on="Customer_ID")

pd.concat([df1, df2])

df.sort_values("Sales")
```

---

# 4. Main Difference

The simplest way to remember the difference is:

```text
DATA CLEANING
      ↓
"Is my data correct?"

DATA MANIPULATION
      ↓
"How should I transform and organize my data?"
```

Another useful way:

```text
Cleaning  → Fix the data
Manipulation → Change/use the data
```

---

# 5. Detailed Difference Table

| Feature            | Data Cleaning                              | Data Manipulation                        |
| ------------------ | ------------------------------------------ | ---------------------------------------- |
| Main purpose       | Improve data quality                       | Transform data for analysis              |
| Main question      | Is the data correct?                       | How should I organize/use the data?      |
| Focus              | Accuracy and consistency                   | Transformation and organization          |
| Missing values     | Handles missing values                     | May use resulting data in calculations   |
| Duplicates         | Identifies/removes duplicates              | Usually works with already-prepared data |
| Invalid values     | Detects/corrects them                      | Uses valid values                        |
| Data types         | Fixes incorrect types                      | Uses types for calculations              |
| Formatting         | Standardizes data                          | Transforms data into required format     |
| Filtering          | Can be used to remove invalid records      | Used to answer analytical questions      |
| Grouping           | Usually not the primary goal               | Major operation                          |
| Aggregation        | Not usually the primary goal               | Major operation                          |
| Merging            | May be required to identify quality issues | Major operation                          |
| Reshaping          | Sometimes                                  | Very common                              |
| Calculated columns | Rarely the main purpose                    | Very common                              |
| Output             | Trustworthy data                           | Analysis-ready structure                 |
| Example            | Remove duplicate customers                 | Calculate sales by customer              |

---

# 6. Data Cleaning Examples

## Example 1 — Missing Values

Suppose:

```text
Name     Age
John     25
Alice    NaN
Bob      30
```

Cleaning:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

The goal is to **handle the missing value**.

This is data cleaning.

---

# 7. Data Manipulation Example

After cleaning:

```python
df["Age_Group"] = pd.cut(
    df["Age"],
    bins=[0, 18, 30, 50, 100],
    labels=[
        "Child",
        "Young Adult",
        "Adult",
        "Senior"
    ]
)
```

Now we are transforming the data into categories for analysis.

This is data manipulation.

---

# 8. Another Example

Suppose the original data is:

```text
Customer    City       Sales
John        Hyderabad  50000
Alice       hyderabad  70000
Bob         Delhi      30000
John        Hyderabad  50000
```

There are several problems.

### Cleaning

Standardize city names:

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)
```

Remove duplicate records:

```python
df = df.drop_duplicates()
```

Now the data is cleaner.

---

### Manipulation

Calculate total sales by city:

```python
city_sales = (
    df.groupby("City")["Sales"]
    .sum()
)
```

This is data manipulation.

---

# 9. Cleaning and Manipulation Often Overlap

Some operations can belong to **either category depending on why they are being performed**.

For example:

```python
df = df[df["Age"] >= 18]
```

### If your purpose is:

> Remove invalid records because age below 18 is not valid for this dataset.

Then it is:

```text
Data Cleaning
```

### If your purpose is:

> Analyze only customers who are adults.

Then it is:

```text
Data Manipulation
```

Therefore, the **purpose of the operation matters**.

---

# 10. Example: Filtering

Filtering is a good example of the overlap.

### Cleaning

```python
df = df[
    df["Age"] >= 0
]
```

Purpose:

```text
Remove invalid ages
```

→ **Cleaning**

### Manipulation

```python
adult_customers = df[
    df["Age"] >= 18
]
```

Purpose:

```text
Analyze adult customers
```

→ **Manipulation**

The code can look almost identical, but the intention is different.

---

# 11. Example: Removing Duplicates

### Cleaning

```python
df = df.drop_duplicates()
```

Purpose:

```text
Remove duplicate records
```

→ Data Cleaning

### Manipulation

If you intentionally remove duplicate observations for a particular analysis, it may be considered part of data preparation/manipulation.

Therefore:

> **The same Pandas method can be used for different purposes.**

---

# 12. Data Cleaning Operations

Common cleaning operations include:

```text
1. Handle missing values
2. Remove duplicates
3. Correct data types
4. Fix inconsistent formatting
5. Standardize categories
6. Handle invalid values
7. Handle outliers
8. Remove unwanted spaces
9. Correct spelling inconsistencies
10. Validate ranges
11. Validate business rules
12. Handle inconsistent units
13. Detect impossible dates
14. Standardize date formats
15. Handle inconsistent capitalization
```

Common Pandas methods:

```python
dropna()
fillna()
drop_duplicates()
astype()
pd.to_numeric()
pd.to_datetime()
replace()
str.strip()
str.lower()
str.upper()
str.replace()
```

---

# 13. Data Manipulation Operations

Common manipulation operations include:

```text
1. Select columns
2. Select rows
3. Filter records
4. Sort data
5. Create columns
6. Modify columns
7. Delete columns
8. Group data
9. Aggregate data
10. Merge datasets
11. Join datasets
12. Concatenate datasets
13. Reshape data
14. Pivot data
15. Melt data
16. Rank data
17. Bin numerical data
18. Calculate statistics
19. Create analytical features
20. Prepare reporting tables
```

Common Pandas methods:

```python
loc
iloc
query()
sort_values()
groupby()
agg()
transform()
merge()
join()
concat()
pivot()
pivot_table()
melt()
assign()
apply()
map()
rank()
cut()
qcut()
```

---

# 14. How They Work Together

Consider a sales dataset.

### Step 1 — Raw Data

```text
Customer    Date          Product    Quantity    Price
John        01/01/25      Laptop     2           50000
Alice       2025-01-02    Phone      3           20000
John        01/01/25      Laptop     2           50000
Bob         Invalid       Phone      NaN         20000
```

---

### Step 2 — Data Cleaning

Identify:

```text
Duplicate record
Inconsistent date format
Missing quantity
Invalid date
```

Clean it:

```python
df = df.drop_duplicates()

df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)

df["Quantity"] = df["Quantity"].fillna(0)
```

Now we have more reliable data.

---

### Step 3 — Data Manipulation

Create total sales:

```python
df["Total_Sales"] = (
    df["Quantity"] *
    df["Price"]
)
```

Group by product:

```python
product_sales = (
    df.groupby("Product")["Total_Sales"]
    .sum()
)
```

Sort:

```python
product_sales = (
    product_sales
    .sort_values(
        ascending=False
    )
)
```

Now the data is ready for analysis.

---

# 15. Relationship in Data Analytics

The relationship can be remembered as:

```text
                RAW DATA
                   │
                   ↓
          ┌─────────────────┐
          │  DATA CLEANING  │
          └─────────────────┘
                   │
                   ↓
         Reliable / Quality Data
                   │
                   ↓
        ┌─────────────────────┐
        │ DATA MANIPULATION   │
        └─────────────────────┘
                   │
                   ↓
          Analysis-Ready Data
                   │
                   ↓
             DATA ANALYSIS
                   │
                   ↓
          DATA VISUALIZATION
                   │
                   ↓
          BUSINESS INSIGHTS
```

---

# 16. Real-World Example

Imagine an e-commerce company has:

```text
10 million transactions
```

The raw data might contain:

```text
Missing customer IDs
Duplicate orders
Incorrect product names
Invalid prices
Different date formats
Missing quantities
Inconsistent country names
```

### Data Cleaning

The analyst fixes:

```text
Missing values
Duplicates
Invalid values
Incorrect types
Formatting
Inconsistencies
```

Result:

```text
Reliable Transaction Dataset
```

### Data Manipulation

The analyst then:

```text
Calculates revenue
Groups by product
Groups by country
Calculates monthly sales
Merges customer information
Creates customer segments
Creates summary tables
```

Result:

```text
Analysis-Ready Dataset
```

### Analysis

Finally:

```text
Which product sells the most?
Which country generates the most revenue?
Which month has the highest sales?
Which customer segment is most profitable?
```

---

# 17. Cleaning vs Manipulation vs Analysis

These three concepts should not be confused.

```text
DATA CLEANING
"What is wrong with my data?"
          ↓
Fix data quality


DATA MANIPULATION
"How can I transform my data?"
          ↓
Prepare data for analysis


DATA ANALYSIS
"What does my data tell me?"
          ↓
Find patterns and insights
```

---

# 18. Simple Example of All Three

Suppose:

```text
City        Sales
delhi       10000
Delhi       20000
DELHI       15000
Mumbai      30000
Mumbai      25000
```

## Cleaning

Standardize city names:

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)
```

Now:

```text
Delhi
Delhi
Delhi
Mumbai
Mumbai
```

This is cleaning because we corrected inconsistent representation.

---

## Manipulation

Group sales by city:

```python
city_sales = (
    df.groupby("City")["Sales"]
    .sum()
)
```

Result:

```text
Delhi     45000
Mumbai    55000
```

This is manipulation.

---

## Analysis

We conclude:

```text
Mumbai generated more sales than Delhi.
```

This is analysis.

---

# 19. Important Concept: Data Preparation

**Data Preparation** is the broader process of getting data ready for analysis.

It can include:

```text
Data Collection
       ↓
Data Integration
       ↓
Data Cleaning
       ↓
Data Transformation
       ↓
Data Manipulation
       ↓
Feature Engineering
       ↓
Data Validation
       ↓
Analysis-Ready Dataset
```

Therefore:

> **Data Cleaning is part of data preparation, and data manipulation/transformation is also part of the broader data-preparation process.**

---

# 20. Data Cleaning and Manipulation in ETL

In an ETL pipeline:

```text
ETL
│
├── Extract
│      ↓
│   Get raw data
│
├── Transform
│      ↓
│   Clean + Manipulate + Transform
│
└── Load
       ↓
    Store prepared data
```

The **Transform** stage may include both:

```text
Data Cleaning
+
Data Manipulation
+
Data Transformation
```

---

# 21. Important Distinction: Transformation

You may also hear the term **Data Transformation**.

Data transformation means converting data from one structure or representation into another.

Examples:

```python
df["Date"] = pd.to_datetime(df["Date"])
```

```python
df["Salary"] = df["Salary"] * 1.10
```

```python
df["Gender"] = df["Gender"].map({
    "Male": 1,
    "Female": 0
})
```

Transformation is therefore closely related to manipulation.

A useful mental model is:

```text
Data Preparation
│
├── Cleaning
│
├── Transformation
│
├── Manipulation
│
├── Integration
│
└── Validation
```

The exact boundaries can vary between organizations and textbooks.

---

# 22. Quick Comparison

```text
┌─────────────────────────────────────────────────────────┐
│                  DATA CLEANING                           │
├─────────────────────────────────────────────────────────┤
│ Goal: Improve data quality                              │
│                                                         │
│ Examples:                                               │
│ • Handle missing values                                 │
│ • Remove duplicates                                     │
│ • Fix invalid values                                    │
│ • Correct data types                                    │
│ • Standardize formats                                   │
│ • Handle inconsistent values                            │
└─────────────────────────────────────────────────────────┘

                         ↓

┌─────────────────────────────────────────────────────────┐
│                DATA MANIPULATION                        │
├─────────────────────────────────────────────────────────┤
│ Goal: Transform and organize data for analysis          │
│                                                         │
│ Examples:                                               │
│ • Filter rows                                           │
│ • Select columns                                        │
│ • Create columns                                        │
│ • Sort data                                             │
│ • Group data                                            │
│ • Aggregate data                                        │
│ • Merge datasets                                        │
│ • Reshape data                                          │
└─────────────────────────────────────────────────────────┘

                         ↓

┌─────────────────────────────────────────────────────────┐
│                     ANALYSIS                            │
├─────────────────────────────────────────────────────────┤
│ Goal: Extract useful information and insights            │
│                                                         │
│ Examples:                                               │
│ • Find trends                                           │
│ • Compare groups                                        │
│ • Identify patterns                                     │
│ • Calculate KPIs                                        │
│ • Answer business questions                             │
└─────────────────────────────────────────────────────────┘
```

---

# 23. Interview-Level Answer

If an interviewer asks:

### "What is the difference between data cleaning and data manipulation?"

A strong answer is:

> **Data cleaning focuses on improving the quality and reliability of data by handling missing values, duplicates, invalid values, inconsistent formats, and incorrect data types. Data manipulation focuses on transforming and organizing that data for analysis through operations such as filtering, sorting, grouping, aggregation, merging, joining, and reshaping. Cleaning makes the data trustworthy, while manipulation makes the data suitable for answering analytical questions. In practice, both are parts of the broader data-preparation process and are often performed iteratively.**

---

# 24. Final Revision Trick

Remember:

```text
                 DATA PREPARATION
                        │
             ┌──────────┴──────────┐
             ↓                     ↓
       DATA CLEANING        DATA MANIPULATION
             │                     │
             ↓                     ↓
       Fix the data          Transform the data
             │                     │
             ↓                     ↓
       Make it reliable      Make it useful
             │                     │
             └──────────┬──────────┘
                        ↓
                 ANALYSIS-READY DATA
                        ↓
                    ANALYSIS
                        ↓
                   INSIGHTS
```

### One-Line Difference

> 🧹 **Data Cleaning = Make the data correct.**

> 🔄 **Data Manipulation = Make the data useful.**

> 📊 **Data Analysis = Make the data meaningful.**
---

# 📚 Table of Contents

1. [What is Data Manipulation?](#1-what-is-data-manipulation)
2. [Data Manipulation vs Data Cleaning](#2-data-manipulation-vs-data-cleaning)
3. [Why Data Manipulation is Important](#3-why-data-manipulation-is-important)
4. [Pandas for Data Manipulation](#4-pandas-for-data-manipulation)
5. [Creating a DataFrame](#5-creating-a-dataframe)
6. [Inspecting Data](#6-inspecting-data)
7. [Selecting Columns](#7-selecting-columns)
8. [Selecting Rows](#8-selecting-rows)
9. [loc and iloc](#9-loc-and-iloc)
10. [Filtering Data](#10-filtering-data)
11. [Multiple Conditions](#11-multiple-conditions)
12. [query()](#12-query)
13. [Adding Columns](#13-adding-columns)
14. [Modifying Columns](#14-modifying-columns)
15. [Deleting Columns](#15-deleting-columns)
16. [Renaming Columns](#16-renaming-columns)
17. [Changing Index](#17-changing-index)
18. [Sorting Data](#18-sorting-data)
19. [Resetting Index](#19-resetting-index)
20. [Replacing Values](#20-replacing-values)
21. [map()](#21-map)
22. [apply()](#22-apply)
23. [applymap() / map() for DataFrames](#23-map-for-dataframes)
24. [assign()](#24-assign)
25. [Unique Values](#25-unique-values)
26. [Value Counts](#26-value-counts)
27. [Grouping Data](#27-grouping-data)
28. [Aggregation](#28-aggregation)
29. [groupby() with Multiple Aggregations](#29-groupby-with-multiple-aggregations)
30. [agg()](#30-agg)
31. [transform()](#31-transform)
32. [Pivot Tables](#32-pivot-tables)
33. [Crosstab](#33-crosstab)
34. [Combining Data](#34-combining-data)
35. [Concatenation](#35-concatenation)
36. [Merging DataFrames](#36-merging-dataframes)
37. [Join Types](#37-join-types)
38. [Joining DataFrames](#38-joining-dataframes)
39. [Handling Duplicate Columns After Merge](#39-handling-duplicate-columns-after-merge)
40. [Reshaping Data](#40-reshaping-data)
41. [Wide vs Long Data](#41-wide-vs-long-data)
42. [melt()](#42-melt)
43. [pivot()](#43-pivot)
44. [pivot_table()](#44-pivottable)
45. [Stack and Unstack](#45-stack-and-unstack)
46. [Exploding Lists](#46-exploding-lists)
47. [String Manipulation](#47-string-manipulation)
48. [Date Manipulation](#48-date-manipulation)
49. [Numeric Manipulation](#49-numeric-manipulation)
50. [Conditional Column Creation](#50-conditional-column-creation)
51. [Cut and Binning](#51-cut-and-binning)
52. [Ranking](#52-ranking)
53. [Sampling](#53-sampling)
54. [Dropping Rows](#54-dropping-rows)
55. [Handling Columns Dynamically](#55-handling-columns-dynamically)
56. [Chaining Operations](#56-chaining-operations)
57. [Vectorization](#57-vectorization)
58. [Copy vs View](#58-copy-vs-view)
59. [Data Manipulation Workflow](#59-data-manipulation-workflow)
60. [Complete Practical Example](#60-complete-practical-example)
61. [Important Methods Cheat Sheet](#61-important-methods-cheat-sheet)
62. [Interview Questions](#62-interview-questions)
63. [Final Revision](#63-final-revision)

---

# 1. What is Data Manipulation?

Data manipulation means **changing the structure, values, or organization of data** to make it useful for analysis.

For example, suppose we have:

```text
Name     Age     Salary     Department
John     25      50000      IT
Alice    30      60000      HR
Bob      28      55000      IT
```

We might want to:

```text
Filter employees from IT
Sort employees by salary
Calculate average salary
Create a salary category
Rename columns
Add calculated columns
Group employees by department
Combine employee data with another dataset
Reshape the data
```

All of these are **data manipulation operations**.

---

# 2. Data Manipulation vs Data Cleaning

These concepts are related but different.

## Data Cleaning

Focuses on making data **correct and reliable**.

Examples:

```text
Remove duplicates
Handle missing values
Correct invalid values
Fix data types
Remove unwanted spaces
Correct inconsistent categories
```

## Data Manipulation

Focuses on **transforming and organizing data for analysis**.

Examples:

```text
Filter rows
Select columns
Sort data
Group data
Aggregate data
Merge datasets
Create calculated columns
Reshape data
```

### Simple Difference

```text
Data Cleaning
      ↓
Make data correct
      ↓
Data Manipulation
      ↓
Make data useful for analysis
```

In real projects, the two processes often overlap.

---

# 3. Why Data Manipulation is Important

Raw data is often not analysis-ready.

Example:

```text
Sales Data
     ↓
Filter relevant records
     ↓
Create calculated columns
     ↓
Group by product
     ↓
Calculate total sales
     ↓
Merge customer information
     ↓
Create analytical dataset
```

Data manipulation helps analysts:

* Extract useful information
* Transform raw data
* Create new features
* Compare groups
* Calculate statistics
* Combine datasets
* Prepare data for visualization
* Prepare data for machine learning

---

# 4. Pandas for Data Manipulation

The most commonly used Python library for tabular data manipulation is **Pandas**.

Import:

```python
import pandas as pd
```

Often NumPy is also useful:

```python
import numpy as np
```

---

# 5. Creating a DataFrame

Let's create a dataset that we will use throughout this README.

```python
import pandas as pd

data = {
    "Name": ["John", "Alice", "Bob", "David", "Emma"],
    "Age": [25, 30, 28, 35, 22],
    "Department": ["IT", "HR", "IT", "Finance", "HR"],
    "Salary": [50000, 60000, 55000, 75000, 45000],
    "Experience": [2, 5, 3, 10, 1]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name  Age Department  Salary  Experience
0   John   25         IT   50000           2
1  Alice   30         HR   60000           5
2    Bob   28         IT   55000           3
3  David   35    Finance   75000          10
4   Emma   22         HR   45000           1
```

---

# 6. Inspecting Data

Before manipulating data, understand its structure.

## First Rows

```python
df.head()
```

---

## Last Rows

```python
df.tail()
```

---

## Random Rows

```python
df.sample(3)
```

---

## Shape

```python
df.shape
```

Output:

```text
(5, 5)
```

Meaning:

```text
5 rows
5 columns
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

## Information

```python
df.info()
```

---

## Statistical Summary

```python
df.describe()
```

---

# 7. Selecting Columns

## Select One Column

```python
df["Name"]
```

The result is a **Series**.

```python
type(df["Name"])
```

---

## Select Multiple Columns

```python
df[
    ["Name", "Salary"]
]
```

The result is a **DataFrame**.

---

## Important Difference

```python
df["Name"]       # Series

df[["Name"]]     # DataFrame
```

---

# 8. Selecting Rows

Rows can be selected using indexing.

```python
df.iloc[0]
```

This selects the first row.

---

## Multiple Rows

```python
df.iloc[0:3]
```

Selects rows:

```text
0
1
2
```

---

## Specific Rows

```python
df.iloc[[0, 2, 4]]
```

---

# 9. loc and iloc

These are extremely important in Pandas.

---

## iloc

`iloc` means **integer-location based selection**.

It uses numerical positions.

```python
df.iloc[0]
```

First row.

```python
df.iloc[0:3]
```

First three rows.

---

## Select Specific Row and Column

```python
df.iloc[0, 1]
```

Means:

```text
row position = 0
column position = 1
```

---

## Select Multiple Rows and Columns

```python
df.iloc[
    0:3,
    0:3
]
```

---

# loc

`loc` uses **labels**.

```python
df.loc[0]
```

Select row with index label `0`.

---

## Select Columns

```python
df.loc[
    :,
    ["Name", "Salary"]
]
```

---

## Conditional Selection

```python
df.loc[
    df["Age"] > 25
]
```

---

## Modify Using loc

```python
df.loc[
    df["Department"] == "IT",
    "Salary"
] = 60000
```

This changes salary for IT employees.

---

# loc vs iloc

| Feature               | loc          | iloc              |
| --------------------- | ------------ | ----------------- |
| Based on              | Labels       | Integer positions |
| Uses                  | Names/labels | Numbers           |
| Conditional filtering | Yes          | Not directly      |
| Example               | `df.loc[2]`  | `df.iloc[2]`      |
| Column names          | Yes          | No                |

### Easy Memory Trick

```text
loc  → location by label

iloc → integer location
```

---

# 10. Filtering Data

Filtering means selecting only rows that satisfy a condition.

## Age Greater Than 25

```python
df[
    df["Age"] > 25
]
```

---

## Salary Greater Than 50000

```python
df[
    df["Salary"] > 50000
]
```

---

## Department Equals IT

```python
df[
    df["Department"] == "IT"
]
```

---

## Age Less Than 30

```python
df[
    df["Age"] < 30
]
```

---

# 11. Multiple Conditions

Use:

```text
&   → AND
|   → OR
~   → NOT
```

Important:

> Put each condition inside parentheses.

---

## AND

Employees who are older than 25 **and** earn more than 50000:

```python
df[
    (df["Age"] > 25) &
    (df["Salary"] > 50000)
]
```

---

## OR

Employees from IT or HR:

```python
df[
    (df["Department"] == "IT") |
    (df["Department"] == "HR")
]
```

---

## NOT

Employees who are not in IT:

```python
df[
    ~(df["Department"] == "IT")
]
```

---

# 12. query()

`query()` provides a convenient way to filter rows using expressions.

```python
df.query(
    "Age > 25"
)
```

---

## Multiple Conditions

```python
df.query(
    "Age > 25 and Salary > 50000"
)
```

---

## Department

```python
df.query(
    'Department == "IT"'
)
```

---

## Range

```python
df.query(
    "25 <= Age <= 35"
)
```

---

# 13. Adding Columns

A common manipulation is creating new columns.

## Simple Calculation

Create annual salary from monthly salary:

```python
df["Annual_Salary"] = (
    df["Salary"] * 12
)
```

---

## Salary Per Experience

```python
df["Salary_Per_Year"] = (
    df["Salary"] / df["Experience"]
)
```

---

## Boolean Column

```python
df["High_Salary"] = (
    df["Salary"] > 60000
)
```

Result:

```text
True
False
...
```

---

# 14. Modifying Columns

Suppose we want to increase salaries by 10%.

```python
df["Salary"] = (
    df["Salary"] * 1.10
)
```

---

## Modify Text

```python
df["Department"] = (
    df["Department"].str.upper()
)
```

---

## Modify Multiple Columns

```python
df[
    ["Salary", "Experience"]
] = df[
    ["Salary", "Experience"]
].astype(float)
```

---

# 15. Deleting Columns

Use `drop()`.

```python
df.drop(
    columns=["Experience"],
    inplace=True
)
```

---

## Delete Multiple Columns

```python
df.drop(
    columns=[
        "Experience",
        "High_Salary"
    ],
    inplace=True
)
```

---

# 16. Renaming Columns

Rename one column:

```python
df.rename(
    columns={
        "Salary": "Monthly_Salary"
    },
    inplace=True
)
```

---

## Rename Multiple Columns

```python
df.rename(
    columns={
        "Name": "Employee_Name",
        "Age": "Employee_Age"
    },
    inplace=True
)
```

---

# 17. Changing Index

Set a column as index:

```python
df.set_index(
    "Name",
    inplace=True
)
```

Now:

```text
             Age  Department  Salary
Name
John          25       IT      50000
Alice         30       HR      60000
...
```

---

## Access by Index Label

```python
df.loc["John"]
```

---

# 18. Sorting Data

## Sort Ascending

```python
df.sort_values(
    "Salary"
)
```

---

## Sort Descending

```python
df.sort_values(
    "Salary",
    ascending=False
)
```

---

## Sort by Multiple Columns

```python
df.sort_values(
    ["Department", "Salary"]
)
```

---

## Different Order for Each Column

```python
df.sort_values(
    ["Department", "Salary"],
    ascending=[True, False]
)
```

---

# 19. Resetting Index

After filtering or sorting, you may want a clean numerical index.

```python
df.reset_index(
    drop=True,
    inplace=True
)
```

---

# 20. Replacing Values

Use `replace()`.

```python
df["Department"] = (
    df["Department"].replace(
        {
            "IT": "Technology"
        }
    )
)
```

---

## Multiple Values

```python
df["Department"] = (
    df["Department"].replace(
        {
            "IT": "Technology",
            "HR": "Human Resources"
        }
    )
)
```

---

# 21. map()

`map()` applies a mapping to values in a Series.

Example:

```python
df["Department_Code"] = (
    df["Department"].map({
        "IT": 101,
        "HR": 102,
        "Finance": 103
    })
)
```

---

## Example

```python
gender_map = {
    "Male": 1,
    "Female": 2
}

df["Gender_Code"] = (
    df["Gender"].map(gender_map)
)
```

---

# 22. apply()

`apply()` allows you to apply a function to values.

Example:

```python
df["Salary_Double"] = (
    df["Salary"].apply(
        lambda x: x * 2
    )
)
```

---

## Custom Function

```python
def salary_category(salary):
    if salary >= 70000:
        return "High"
    elif salary >= 50000:
        return "Medium"
    else:
        return "Low"
```

Apply:

```python
df["Salary_Category"] = (
    df["Salary"].apply(
        salary_category
    )
)
```

---

# 23. map() for DataFrames

For element-wise transformation across a DataFrame, modern Pandas uses:

```python
df.map()
```

For example:

```python
small_df = df[
    ["Age", "Salary"]
]

result = small_df.map(
    lambda x: x * 2
)
```

> Older Pandas code often uses `applymap()`. In newer Pandas versions, `DataFrame.map()` is the preferred name for element-wise DataFrame mapping.

---

# 24. assign()

`assign()` can create new columns without modifying the original DataFrame directly.

```python
new_df = df.assign(
    Annual_Salary=df["Salary"] * 12
)
```

---

## Multiple Columns

```python
new_df = df.assign(
    Annual_Salary=df["Salary"] * 12,
    Bonus=df["Salary"] * 0.10
)
```

---

# 25. Unique Values

Find unique values:

```python
df["Department"].unique()
```

---

## Number of Unique Values

```python
df["Department"].nunique()
```

---

## Check Whether a Value Exists

```python
"IT" in df["Department"].values
```

---

# 26. value_counts()

Counts the occurrence of each value.

```python
df["Department"].value_counts()
```

Example:

```text
IT         2
HR         2
Finance    1
```

---

## Percentage

```python
df["Department"].value_counts(
    normalize=True
)
```

---

## Include Missing Values

```python
df["Department"].value_counts(
    dropna=False
)
```

---

# 27. Grouping Data

`groupby()` is one of the most important concepts in data analytics.

Suppose:

```text
Department    Salary
IT            50000
IT            55000
HR            60000
HR            45000
Finance       75000
```

We may want:

```text
Department    Average Salary
IT            52500
HR            52500
Finance       75000
```

Use:

```python
df.groupby(
    "Department"
)["Salary"].mean()
```

---

# 28. Aggregation

Common aggregation functions:

```text
sum()
mean()
median()
min()
max()
count()
std()
var()
```

---

## Total Salary by Department

```python
df.groupby(
    "Department"
)["Salary"].sum()
```

---

## Average Salary

```python
df.groupby(
    "Department"
)["Salary"].mean()
```

---

## Maximum Salary

```python
df.groupby(
    "Department"
)["Salary"].max()
```

---

## Number of Employees

```python
df.groupby(
    "Department"
)["Name"].count()
```

---

# 29. groupby() with Multiple Aggregations

```python
df.groupby(
    "Department"
)["Salary"].agg([
    "sum",
    "mean",
    "min",
    "max"
])
```

---

# 30. agg()

`agg()` allows multiple aggregation operations.

```python
df.groupby(
    "Department"
).agg({
    "Salary": ["sum", "mean", "max"],
    "Age": ["mean", "min", "max"]
})
```

---

## Named Aggregations

This produces cleaner column names:

```python
summary = df.groupby(
    "Department"
).agg(
    Average_Salary=("Salary", "mean"),
    Maximum_Salary=("Salary", "max"),
    Employee_Count=("Name", "count")
)
```

---

# 31. transform()

`transform()` performs group-level calculations while keeping the **original row structure**.

Example:

```python
df["Department_Avg_Salary"] = (
    df.groupby("Department")["Salary"]
    .transform("mean")
)
```

Suppose:

```text
Department    Salary
IT            50000
IT            55000
HR            60000
HR            45000
```

Result:

```text
Department    Salary    Department_Avg
IT            50000     52500
IT            55000     52500
HR            60000     52500
HR            45000     52500
```

### Important Difference

```text
groupby().agg()
    ↓
Reduces rows

groupby().transform()
    ↓
Keeps original number of rows
```

---

# 32. Pivot Tables

Pivot tables summarize data across multiple dimensions.

```python
pivot = pd.pivot_table(
    df,
    values="Salary",
    index="Department",
    aggfunc="mean"
)

print(pivot)
```

---

## Multiple Aggregations

```python
pivot = pd.pivot_table(
    df,
    values="Salary",
    index="Department",
    aggfunc=["mean", "sum", "max"]
)
```

---

## Group by Department and Age

```python
pivot = pd.pivot_table(
    df,
    values="Salary",
    index="Department",
    columns="Age",
    aggfunc="mean"
)
```

---

# 33. Crosstab

`pd.crosstab()` creates frequency tables.

Example:

```python
pd.crosstab(
    df["Department"],
    df["Age"]
)
```

It is particularly useful for analyzing relationships between categorical variables.

---

## Normalize

```python
pd.crosstab(
    df["Department"],
    df["Age"],
    normalize=True
)
```

---

# 34. Combining Data

Data manipulation often requires combining multiple datasets.

For example:

```text
Customer Data
      +
Sales Data
      ↓
Combined Dataset
```

Pandas provides:

```text
concat()
merge()
join()
```

---

# 35. Concatenation

`concat()` combines DataFrames along rows or columns.

Suppose:

```python
df1 = pd.DataFrame({
    "Name": ["John", "Alice"],
    "Salary": [50000, 60000]
})

df2 = pd.DataFrame({
    "Name": ["Bob", "David"],
    "Salary": [55000, 70000]
})
```

Combine rows:

```python
result = pd.concat(
    [df1, df2],
    ignore_index=True
)
```

Result:

```text
    Name  Salary
0   John   50000
1  Alice   60000
2    Bob   55000
3  David   70000
```

---

## Concatenate Columns

```python
result = pd.concat(
    [df1, df2],
    axis=1
)
```

`axis=0`:

```text
Rows
```

`axis=1`:

```text
Columns
```

---

# 36. Merging DataFrames

`merge()` is similar to a SQL JOIN.

Customer Data:

```python
customers = pd.DataFrame({
    "Customer_ID": [1, 2, 3],
    "Name": ["John", "Alice", "Bob"]
})
```

Sales Data:

```python
sales = pd.DataFrame({
    "Customer_ID": [1, 2, 3],
    "Amount": [500, 700, 300]
})
```

Merge:

```python
result = pd.merge(
    customers,
    sales,
    on="Customer_ID"
)
```

Result:

```text
Customer_ID    Name    Amount
1              John    500
2              Alice   700
3              Bob     300
```

---

# 37. Join Types

The major SQL-style joins are:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
OUTER JOIN
```

---

## Inner Join

Returns only matching records.

```python
pd.merge(
    customers,
    sales,
    on="Customer_ID",
    how="inner"
)
```

---

## Left Join

Keeps every row from the left DataFrame.

```python
pd.merge(
    customers,
    sales,
    on="Customer_ID",
    how="left"
)
```

---

## Right Join

Keeps every row from the right DataFrame.

```python
pd.merge(
    customers,
    sales,
    on="Customer_ID",
    how="right"
)
```

---

## Outer Join

Keeps all rows from both DataFrames.

```python
pd.merge(
    customers,
    sales,
    on="Customer_ID",
    how="outer"
)
```

---

# Join Diagram

```text
LEFT JOIN

A ────────────────┐
                  ├── Result contains all A
B ────────────────┘
       + matching B


INNER JOIN

A ∩ B

Only matching records


OUTER JOIN

A ∪ B

All records from both
```

---

# 38. Joining DataFrames

`join()` is commonly used when joining based on indexes.

```python
df1.join(
    df2,
    lsuffix="_left",
    rsuffix="_right"
)
```

---

# 39. Handling Duplicate Columns After Merge

Suppose both DataFrames contain:

```text
Name
Salary
```

After merging, Pandas may create:

```text
Name_x
Name_y
```

You can control suffixes:

```python
pd.merge(
    df1,
    df2,
    on="ID",
    suffixes=("_customer", "_sales")
)
```

---

# 40. Reshaping Data

Reshaping means changing the structure of a DataFrame without necessarily changing the underlying information.

Two common formats:

```text
Wide format
Long format
```

---

# 41. Wide vs Long Data

## Wide Format

```text
Name    Jan    Feb    Mar
John    100    120    150
Alice   200    180    220
```

One row contains multiple measurement columns.

---

## Long Format

```text
Name    Month    Sales
John    Jan      100
John    Feb      120
John    Mar      150
Alice   Jan      200
...
```

Long format is often easier for analysis and visualization.

---

# 42. melt()

`melt()` converts wide data into long format.

```python
df_long = pd.melt(
    df,
    id_vars=["Name"],
    var_name="Month",
    value_name="Sales"
)
```

Concept:

```text
Wide
 ↓
melt()
 ↓
Long
```

---

# 43. pivot()

`pivot()` converts long data into wide format.

```python
df_wide = df_long.pivot(
    index="Name",
    columns="Month",
    values="Sales"
)
```

Important:

`pivot()` requires the combination of index and columns to identify a unique value. If duplicates exist, use `pivot_table()`.

---

# 44. pivot_table()

`pivot_table()` is similar to `pivot()`, but it can aggregate duplicate combinations.

```python
pd.pivot_table(
    df,
    values="Sales",
    index="Name",
    columns="Month",
    aggfunc="sum"
)
```

---

# 45. Stack and Unstack

These operations are useful when working with hierarchical indexes.

## stack()

Moves columns into the index.

```python
df.stack()
```

---

## unstack()

Moves an index level into columns.

```python
df.unstack()
```

Think:

```text
stack()
    ↓
Columns → Index

unstack()
    ↓
Index → Columns
```

---

# 46. Exploding Lists

Sometimes a column contains lists.

Example:

```python
df = pd.DataFrame({
    "Name": ["John", "Alice"],
    "Skills": [
        ["Python", "SQL"],
        ["Excel", "Power BI"]
    ]
})
```

Use:

```python
df.explode(
    "Skills"
)
```

Result:

```text
Name     Skills
John     Python
John     SQL
Alice    Excel
Alice    Power BI
```

This is useful for converting list-like values into separate rows.

---

# 47. String Manipulation

Pandas provides `.str` methods.

---

## Lowercase

```python
df["Name"].str.lower()
```

---

## Uppercase

```python
df["Name"].str.upper()
```

---

## Title Case

```python
df["Name"].str.title()
```

---

## Remove Spaces

```python
df["Name"].str.strip()
```

---

## Replace Text

```python
df["Name"].str.replace(
    "John",
    "Jonathan",
    regex=False
)
```

---

## Contains

```python
df[
    df["Name"].str.contains(
        "John",
        case=False,
        na=False
    )
]
```

---

## Starts With

```python
df[
    df["Name"].str.startswith(
        "A",
        na=False
    )
]
```

---

## Ends With

```python
df[
    df["Name"].str.endswith(
        "n",
        na=False
    )
]
```

---

## Split

```python
df["Name"].str.split()
```

---

# 48. Date Manipulation

Convert to datetime first:

```python
df["Date"] = pd.to_datetime(
    df["Date"]
)
```

---

## Year

```python
df["Year"] = df["Date"].dt.year
```

---

## Month

```python
df["Month"] = df["Date"].dt.month
```

---

## Day

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

## Quarter

```python
df["Quarter"] = (
    df["Date"].dt.quarter
)
```

---

## Filter by Date

```python
df[
    df["Date"] >= "2025-01-01"
]
```

---

# 49. Numeric Manipulation

Pandas provides many numerical operations.

## Addition

```python
df["Total"] = (
    df["Price"] + df["Tax"]
)
```

---

## Subtraction

```python
df["Profit"] = (
    df["Revenue"] - df["Cost"]
)
```

---

## Multiplication

```python
df["Total"] = (
    df["Price"] * df["Quantity"]
)
```

---

## Division

```python
df["Average"] = (
    df["Total"] / df["Quantity"]
)
```

---

## Round

```python
df["Salary"] = (
    df["Salary"].round(2)
)
```

---

## Absolute Value

```python
df["Difference"] = (
    df["Difference"].abs()
)
```

---

## Minimum and Maximum

```python
df["Salary"].min()
df["Salary"].max()
```

---

# 50. Conditional Column Creation

A very common analytics task is creating categories.

Example:

```text
Salary >= 70000 → High
Salary >= 50000 → Medium
Otherwise       → Low
```

Using `apply()`:

```python
def salary_category(salary):
    if salary >= 70000:
        return "High"
    elif salary >= 50000:
        return "Medium"
    else:
        return "Low"

df["Salary_Category"] = (
    df["Salary"].apply(
        salary_category
    )
)
```

---

# Using np.select()

For multiple conditions:

```python
conditions = [
    df["Salary"] >= 70000,
    df["Salary"] >= 50000
]

choices = [
    "High",
    "Medium"
]

df["Salary_Category"] = np.select(
    conditions,
    choices,
    default="Low"
)
```

---

# Using np.where()

For a simple condition:

```python
df["Status"] = np.where(
    df["Salary"] >= 60000,
    "High",
    "Low"
)
```

---

# 51. cut() and Binning

Binning means converting continuous numeric data into categories.

Suppose ages are:

```text
18
22
27
35
42
60
```

Create groups:

```text
18–25
26–35
36–50
51+
```

Use:

```python
bins = [
    0,
    25,
    35,
    50,
    100
]

labels = [
    "18-25",
    "26-35",
    "36-50",
    "51+"
]

df["Age_Group"] = pd.cut(
    df["Age"],
    bins=bins,
    labels=labels
)
```

---

# qcut()

`qcut()` creates groups based on quantiles.

```python
df["Salary_Group"] = pd.qcut(
    df["Salary"],
    q=4,
    labels=[
        "Low",
        "Medium-Low",
        "Medium-High",
        "High"
    ]
)
```

Difference:

```text
cut()
    ↓
Fixed numerical boundaries

qcut()
    ↓
Quantile-based groups
```

---

# 52. Ranking

Rank values using:

```python
df["Salary_Rank"] = (
    df["Salary"]
    .rank(ascending=False)
)
```

Highest salary gets rank 1.

---

## Dense Ranking

```python
df["Rank"] = (
    df["Salary"]
    .rank(
        method="dense",
        ascending=False
    )
)
```

---

# 53. Sampling

Take a random sample:

```python
df.sample(
    n=3,
    random_state=42
)
```

Take a percentage:

```python
df.sample(
    frac=0.20,
    random_state=42
)
```

This is useful for:

* Testing
* Data exploration
* Sampling
* Large datasets

---

# 54. Dropping Rows

## Drop Specific Index

```python
df.drop(
    index=[0, 2]
)
```

---

## Drop Rows Based on Condition

```python
df = df[
    df["Age"] >= 18
]
```

---

## Drop Rows With Missing Values

```python
df.dropna()
```

---

# 55. Handling Columns Dynamically

Select numeric columns:

```python
numeric_columns = (
    df.select_dtypes(
        include="number"
    ).columns
)
```

Select categorical columns:

```python
categorical_columns = (
    df.select_dtypes(
        include="object"
    ).columns
)
```

---

## Apply Operation to All Numeric Columns

```python
df[numeric_columns] = (
    df[numeric_columns].fillna(
        df[numeric_columns].median()
    )
)
```

---

# 56. Chaining Operations

Pandas allows operations to be chained.

Instead of:

```python
df = df[
    df["Age"] > 25
]

df = df.sort_values(
    "Salary",
    ascending=False
)

df = df[
    ["Name", "Age", "Salary"]
]
```

You can write:

```python
result = (
    df
    .query("Age > 25")
    .sort_values(
        "Salary",
        ascending=False
    )
    [["Name", "Age", "Salary"]]
)
```

This can make transformation pipelines easier to read.

---

# 57. Vectorization

Vectorization means applying operations to an entire Series or DataFrame without explicitly looping through every row in Python.

Instead of:

```python
df["New_Salary"] = [
    salary * 1.10
    for salary in df["Salary"]
]
```

Prefer:

```python
df["New_Salary"] = (
    df["Salary"] * 1.10
)
```

Pandas and NumPy can perform these operations efficiently.

### Important Principle

Prefer:

```text
Vectorized operations
```

over unnecessary:

```text
Python loops
```

for large datasets.

---

# 58. Copy vs View

This is an important Pandas concept.

Suppose:

```python
subset = df[
    df["Age"] > 25
]
```

If you intend to manipulate `subset` independently, explicitly make a copy:

```python
subset = df[
    df["Age"] > 25
].copy()
```

Then:

```python
subset["Salary"] = (
    subset["Salary"] * 1.10
)
```

Using `.copy()` makes your intention clear and helps avoid confusing chained-assignment behavior.

---

# 59. Data Manipulation Workflow

A typical workflow:

```text
                 Raw Data
                    ↓
              Load Data
                    ↓
            Inspect Data
                    ↓
          Select Relevant Data
                    ↓
         Filter Required Rows
                    ↓
        Create/Modify Columns
                    ↓
         Transform Values
                    ↓
           Group & Aggregate
                    ↓
       Merge / Join Datasets
                    ↓
          Reshape if Required
                    ↓
             Validate
                    ↓
          Analysis / Visualization
```

---

# 60. Complete Practical Example

Let's create a small sales dataset.

```python
import pandas as pd
import numpy as np

sales = pd.DataFrame({
    "Order_ID": [101, 102, 103, 104, 105, 106],
    "Product": [
        "Laptop",
        "Phone",
        "Laptop",
        "Tablet",
        "Phone",
        "Laptop"
    ],
    "Category": [
        "Electronics",
        "Electronics",
        "Electronics",
        "Electronics",
        "Electronics",
        "Electronics"
    ],
    "Quantity": [2, 5, 1, 3, 4, 2],
    "Price": [
        50000,
        20000,
        50000,
        30000,
        20000,
        50000
    ],
    "Region": [
        "South",
        "North",
        "South",
        "East",
        "North",
        "South"
    ]
})

print(sales)
```

---

## Step 1 — Create Total Sales

```python
sales["Total_Sales"] = (
    sales["Quantity"] *
    sales["Price"]
)
```

---

## Step 2 — Filter High-Value Orders

```python
high_value = sales[
    sales["Total_Sales"] > 100000
]
```

---

## Step 3 — Sort by Sales

```python
sales = sales.sort_values(
    "Total_Sales",
    ascending=False
)
```

---

## Step 4 — Group by Product

```python
product_sales = (
    sales
    .groupby("Product")["Total_Sales"]
    .sum()
)

print(product_sales)
```

---

## Step 5 — Group by Region

```python
region_sales = (
    sales
    .groupby("Region")["Total_Sales"]
    .sum()
)
```

---

## Step 6 — Calculate Average Order Value

```python
average_order = (
    sales["Total_Sales"].mean()
)

print(average_order)
```

---

## Step 7 — Create Sales Category

```python
sales["Sales_Category"] = np.where(
    sales["Total_Sales"] >= 100000,
    "High",
    "Low"
)
```

---

## Step 8 — Create Product Summary

```python
summary = (
    sales
    .groupby("Product")
    .agg(
        Total_Revenue=(
            "Total_Sales",
            "sum"
        ),
        Average_Order=(
            "Total_Sales",
            "mean"
        ),
        Total_Quantity=(
            "Quantity",
            "sum"
        )
    )
)

print(summary)
```

---

## Step 9 — Sort Summary

```python
summary = summary.sort_values(
    "Total_Revenue",
    ascending=False
)
```

---

# 61. Important Methods Cheat Sheet

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

## Selection

```python
df["column"]

df[["col1", "col2"]]

df.loc[]

df.iloc[]
```

---

## Filtering

```python
df[df["Age"] > 25]

df[
    (df["Age"] > 25) &
    (df["Salary"] > 50000)
]

df.query("Age > 25")
```

---

## Columns

```python
df["New"] = ...

df.drop(
    columns=["column"]
)

df.rename(
    columns={}
)
```

---

## Sorting

```python
df.sort_values()

df.sort_index()
```

---

## Values

```python
df.replace()

df["column"].unique()

df["column"].nunique()

df["column"].value_counts()
```

---

## Transformation

```python
df["column"].map()

df["column"].apply()

df.assign()
```

---

## Grouping

```python
df.groupby()

df.groupby().sum()

df.groupby().mean()

df.groupby().agg()

df.groupby().transform()
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
pd.melt()

df.pivot()

pd.pivot_table()

df.stack()

df.unstack()

df.explode()
```

---

## Numeric

```python
df.mean()
df.median()
df.sum()
df.min()
df.max()
df.std()
df.var()
df.quantile()
df.rank()
```

---

## Dates

```python
pd.to_datetime()

df["date"].dt.year

df["date"].dt.month

df["date"].dt.day

df["date"].dt.quarter

df["date"].dt.day_name()
```

---

## Strings

```python
.str.lower()
.str.upper()
.str.title()
.str.strip()
.str.replace()
.str.contains()
.str.startswith()
.str.endswith()
.str.split()
```

---

# 62. Data Manipulation Interview Questions

## Q1. What is Data Manipulation?

Data manipulation is the process of transforming, organizing, filtering, combining, and modifying data to make it suitable for analysis.

---

## Q2. What is the difference between `loc` and `iloc`?

`loc` uses labels.

```python
df.loc[2, "Salary"]
```

`iloc` uses integer positions.

```python
df.iloc[2, 3]
```

---

## Q3. How do you filter rows in Pandas?

```python
df[
    df["Age"] > 25
]
```

---

## Q4. How do you filter using multiple conditions?

```python
df[
    (df["Age"] > 25) &
    (df["Salary"] > 50000)
]
```

---

## Q5. What is `groupby()`?

`groupby()` divides data into groups based on one or more columns and allows calculations to be performed for each group.

Example:

```python
df.groupby(
    "Department"
)["Salary"].mean()
```

---

## Q6. What is aggregation?

Aggregation summarizes multiple records into statistics such as:

```text
sum
mean
count
min
max
median
std
```

---

## Q7. Difference between `agg()` and `transform()`?

### `agg()`

Usually reduces the number of rows.

```python
df.groupby(
    "Department"
)["Salary"].agg("mean")
```

### `transform()`

Returns results aligned with the original rows.

```python
df["Avg"] = (
    df.groupby("Department")["Salary"]
    .transform("mean")
)
```

---

## Q8. Difference between `merge()` and `concat()`?

### `concat()`

Combines DataFrames along rows or columns.

```python
pd.concat([df1, df2])
```

### `merge()`

Combines DataFrames based on matching keys.

```python
pd.merge(
    df1,
    df2,
    on="ID"
)
```

Think:

```text
concat → stack data

merge → match data
```

---

## Q9. What is an inner join?

It returns only records where the join key exists in both DataFrames.

---

## Q10. What is a left join?

It keeps every record from the left DataFrame and matching records from the right DataFrame.

---

## Q11. What is `melt()`?

`melt()` converts data from wide format to long format.

```python
pd.melt(df)
```

---

## Q12. What is `pivot()`?

`pivot()` converts long-format data into wide format.

```python
df.pivot(
    index="Name",
    columns="Month",
    values="Sales"
)
```

---

## Q13. What is `pivot_table()`?

`pivot_table()` creates a summary table and can aggregate duplicate combinations.

---

## Q14. What is `apply()`?

`apply()` applies a function along a Series or DataFrame axis.

Example:

```python
df["Salary"].apply(
    lambda x: x * 1.10
)
```

---

## Q15. What is `map()`?

`map()` maps or transforms values in a Series.

Example:

```python
df["Gender"].map({
    "Male": 1,
    "Female": 2
})
```

---

## Q16. What is vectorization?

Vectorization means performing operations on entire arrays/Series rather than manually processing each row with Python loops.

Example:

```python
df["Total"] = (
    df["Price"] *
    df["Quantity"]
)
```

---

## Q17. What is the difference between Series and DataFrame?

```text
Series
  ↓
1D
  ↓
Single labeled column

DataFrame
  ↓
2D
  ↓
Multiple labeled columns
```

---

## Q18. How do you create a new column based on a condition?

Using `np.where()`:

```python
df["Status"] = np.where(
    df["Salary"] >= 50000,
    "High",
    "Low"
)
```

---

# 63. Final Revision

## 🧠 Remember Data Manipulation as 8 Major Tasks

```text
1. SELECT
       ↓
   Choose rows/columns

2. FILTER
       ↓
   Keep required records

3. TRANSFORM
       ↓
   Change values

4. CREATE
       ↓
   Add calculated columns

5. AGGREGATE
       ↓
   Summarize data

6. COMBINE
       ↓
   Merge / Join / Concatenate

7. RESHAPE
       ↓
   Wide ↔ Long

8. SORT
       ↓
   Organize records
```

---

# ⭐ Most Important Pandas Concepts

If you're preparing for **Data Analyst interviews**, prioritize these:

```text
★★★★★  loc / iloc
★★★★★  Filtering
★★★★★  groupby()
★★★★★  agg()
★★★★★  merge()
★★★★★  concat()
★★★★★  Sorting
★★★★★  Creating calculated columns
★★★★★  apply() / map()
★★★★★  pivot_table()
★★★★★  melt()
★★★★☆  transform()
★★★★☆  query()
★★★★☆  value_counts()
★★★★☆  String manipulation
★★★★☆  Date manipulation
★★★★☆  Vectorization
```

---

# 🔥 One-Page Mental Model

```text
                 PANDAS DATA MANIPULATION
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
   SELECT                FILTER             MODIFY
       │                   │                   │
 loc / iloc          conditions          new columns
 columns             query()             replace()
                                           map()
                                           apply()
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ↓
                       GROUP
                           │
                       groupby()
                           ↓
                      AGGREGATE
                           │
                     sum / mean /
                    count / min /
                    max / agg()
                           ↓
                       COMBINE
                           │
                  ┌────────┼────────┐
                  ↓        ↓        ↓
                merge    concat    join
                  │        │        │
                  └────────┼────────┘
                           ↓
                       RESHAPE
                           │
                  ┌────────┴────────┐
                  ↓                 ↓
                melt             pivot
                  │                 │
                  └────────┬────────┘
                           ↓
                        ANALYZE
```

---

# 🎯 Data Analytics Example

A real analyst might receive:

```text
Raw Sales Data
      ↓
Clean missing/invalid data
      ↓
Filter completed orders
      ↓
Create Total_Sales column
      ↓
Group by Product
      ↓
Calculate Revenue
      ↓
Merge Customer Data
      ↓
Create monthly summary
      ↓
Pivot into report format
      ↓
Visualize in Power BI / Tableau
      ↓
Generate Business Insights
```

This is why **Data Manipulation is a core Data Analytics skill**.

---

# 🏆 Final Golden Rules

### Rule 1

> Always inspect your data before manipulating it.

### Rule 2

> Use `loc` for label-based selection and `iloc` for position-based selection.

### Rule 3

> Use `groupby()` when you need analysis by category/group.

### Rule 4

> Use `merge()` when datasets need to be matched using keys.

### Rule 5

> Use `concat()` when you need to stack DataFrames.

### Rule 6

> Use `melt()` and `pivot()` to reshape data.

### Rule 7

> Prefer vectorized Pandas/NumPy operations over unnecessary Python loops.

### Rule 8

> After manipulation, always validate the result.

---

# 🚀 Data Cleaning + Data Manipulation

These two concepts work together:

```text
                 RAW DATA
                    ↓
             DATA CLEANING
                    ↓
       ┌────────────┼────────────┐
       ↓            ↓            ↓
   Missing       Duplicate     Invalid
    Values         Data         Values
       └────────────┼────────────┘
                    ↓
             CLEAN DATA
                    ↓
          DATA MANIPULATION
                    ↓
       ┌────────────┼────────────┐
       ↓            ↓            ↓
    Filter       Transform     Group
       ↓            ↓            ↓
    Select        Create       Aggregate
       └────────────┼────────────┘
                    ↓
             Merge / Join
                    ↓
               Reshape
                    ↓
              ANALYSIS
                    ↓
           VISUALIZATION
                    ↓
          BUSINESS INSIGHTS
```

> **Data Cleaning makes data trustworthy. Data Manipulation makes data useful. Data Analysis turns that prepared data into insights.**
