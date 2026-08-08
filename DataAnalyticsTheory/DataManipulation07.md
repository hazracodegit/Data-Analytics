# 📊 Data Manipulation

> Complete beginner-to-advanced notes on Data Manipulation for Data Analytics, covering filtering, sorting, selecting, transforming, aggregating, grouping, merging, joining, reshaping, handling duplicates, dates, strings, missing values, calculated columns, Pandas operations, SQL operations, and real-world analytical workflows.

---

# 📚 Table of Contents

1. [What is Data Manipulation?](#1-what-is-data-manipulation)
2. [Technical Definition](#2-technical-definition)
3. [Why Data Manipulation is Important](#3-why-data-manipulation-is-important)
4. [Data Manipulation vs Data Cleaning](#4-data-manipulation-vs-data-cleaning)
5. [Data Manipulation vs Data Preprocessing](#5-data-manipulation-vs-data-preprocessing)
6. [Data Manipulation vs Data Transformation](#6-data-manipulation-vs-data-transformation)
7. [Data Manipulation Workflow](#7-data-manipulation-workflow)
8. [Understanding a Dataset](#8-understanding-a-dataset)
9. [Selecting Columns](#9-selecting-columns)
10. [Selecting Rows](#10-selecting-rows)
11. [Filtering Data](#11-filtering-data)
12. [Multiple Conditions](#12-multiple-conditions)
13. [Sorting Data](#13-sorting-data)
14. [Limiting Data](#14-limiting-data)
15. [Adding Columns](#15-adding-columns)
16. [Modifying Columns](#16-modifying-columns)
17. [Deleting Columns](#17-deleting-columns)
18. [Renaming Columns](#18-renaming-columns)
19. [Changing Data Types](#19-changing-data-types)
20. [String Manipulation](#20-string-manipulation)
21. [Date and Time Manipulation](#21-date-and-time-manipulation)
22. [Missing Value Manipulation](#22-missing-value-manipulation)
23. [Duplicate Manipulation](#23-duplicate-manipulation)
24. [Conditional Transformation](#24-conditional-transformation)
25. [Mapping Values](#25-mapping-values)
26. [Apply and Lambda](#26-apply-and-lambda)
27. [Aggregation](#27-aggregation)
28. [GroupBy](#28-groupby)
29. [Pivot Tables](#29-pivot-tables)
30. [Crosstab](#30-crosstab)
31. [Merging Data](#31-merging-data)
32. [Joining Data](#32-joining-data)
33. [Concatenating Data](#33-concatenating-data)
34. [Reshaping Data](#34-reshaping-data)
35. [Wide vs Long Data](#35-wide-vs-long-data)
36. [Melt](#36-melt)
37. [Pivot](#37-pivot)
38. [Stack and Unstack](#38-stack-and-unstack)
39. [Ranking](#39-ranking)
40. [Window-Based Manipulation](#40-window-based-manipulation)
41. [Rolling Operations](#41-rolling-operations)
42. [Lag and Lead](#42-lag-and-lead)
43. [Cumulative Operations](#43-cumulative-operations)
44. [Percentage Change](#44-percentage-change)
45. [SQL Data Manipulation](#45-sql-data-manipulation)
46. [SQL Filtering](#46-sql-filtering)
47. [SQL Aggregation](#47-sql-aggregation)
48. [SQL Grouping](#48-sql-grouping)
49. [SQL Joins](#49-sql-joins)
50. [SQL Subqueries](#50-sql-subqueries)
51. [SQL CTEs](#51-sql-ctes)
52. [SQL Window Functions](#52-sql-window-functions)
53. [Data Manipulation for Analytics](#53-data-manipulation-for-analytics)
54. [Sales Analytics](#54-sales-analytics)
55. [Customer Analytics](#55-customer-analytics)
56. [Time-Series Manipulation](#56-time-series-manipulation)
57. [Real-World Example](#57-real-world-example)
58. [Common Mistakes](#58-common-mistakes)
59. [Best Practices](#59-best-practices)
60. [Interview Questions](#60-interview-questions)
61. [Final Revision](#61-final-revision)

---

# 1. What is Data Manipulation?

## Easy Definition

**Data manipulation is the process of selecting, modifying, organizing, combining, filtering, aggregating, and reshaping data to make it useful for analysis.**

Example:

Raw sales data:

```text
Customer | Product | Quantity | Price
---------------------------------------
A        | Laptop  | 2        | 50000
B        | Mouse   | 5        | 1000
C        | Laptop  | 1        | 50000
```

We can manipulate it to calculate:

```text
Revenue = Quantity × Price
```

Result:

```text
Customer | Product | Revenue
----------------------------
A        | Laptop  | 100000
B        | Mouse   | 5000
C        | Laptop  | 50000
```

---

# 2. Technical Definition

> **Data manipulation is the systematic process of selecting, filtering, transforming, combining, aggregating, sorting, and restructuring data to produce a form suitable for analysis, reporting, visualization, or further processing.**

---

# 3. Why Data Manipulation is Important

Raw data is rarely in the exact format required for analysis.

Data manipulation helps us:

```text
Select relevant data
Filter records
Create calculated columns
Aggregate information
Combine datasets
Reshape datasets
Sort records
Group observations
Calculate metrics
Prepare analytical datasets
```

---

# 4. Data Manipulation vs Data Cleaning

These concepts overlap but are not identical.

## Data Cleaning

Focus:

> Fix data-quality problems.

Examples:

```text
Missing values
Duplicates
Invalid values
Incorrect formats
Inconsistent values
```

---

## Data Manipulation

Focus:

> Change and organize data to answer analytical questions.

Examples:

```text
Filtering
Sorting
Grouping
Aggregation
Joining
Creating columns
Reshaping
Calculating metrics
```

### Relationship

```text
Data
 │
 ├── Cleaning
 │
 └── Manipulation
```

Cleaning can be considered part of broader data preparation, while manipulation is specifically about working with the structure and values to produce useful datasets.

---

# 5. Data Manipulation vs Data Preprocessing

## Data Preprocessing

Broad preparation before analysis/modeling.

```text
Cleaning
Integration
Transformation
Encoding
Scaling
Feature engineering
Feature selection
```

## Data Manipulation

Operations used to work with data.

```text
Select
Filter
Sort
Group
Aggregate
Join
Merge
Reshape
Calculate
```

### Relationship

```text
Data Preprocessing
        │
        ├── Cleaning
        ├── Transformation
        ├── Encoding
        ├── Scaling
        │
        └── Data Manipulation
             ├── Filtering
             ├── Grouping
             ├── Joining
             ├── Aggregation
             └── Reshaping
```

The exact boundaries vary by context.

---

# 6. Data Manipulation vs Data Transformation

## Data Manipulation

Changes or reorganizes data to perform an operation or analysis.

Example:

```text
Filter customers
Group sales by month
Join customer and transaction tables
```

## Data Transformation

Changes the representation of data.

Example:

```text
Convert salary to log scale
Encode categories
Standardize numerical features
```

Transformation is therefore often considered one type of manipulation or data-preparation operation, depending on the terminology being used.

---

# 7. Data Manipulation Workflow

Typical analytics workflow:

```text
Raw Data
   ↓
Understand Data
   ↓
Select Required Data
   ↓
Filter Data
   ↓
Clean Data
   ↓
Transform Data
   ↓
Create Calculated Columns
   ↓
Group Data
   ↓
Aggregate Data
   ↓
Join / Merge Data
   ↓
Reshape Data
   ↓
Analyze
   ↓
Visualize
```

---

# 8. Understanding a Dataset

Before manipulating data, inspect it.

```python
import pandas as pd

df = pd.read_csv("sales.csv")
```

View first rows:

```python
df.head()
```

View last rows:

```python
df.tail()
```

Shape:

```python
df.shape
```

Columns:

```python
df.columns
```

Data types:

```python
df.dtypes
```

Information:

```python
df.info()
```

Summary:

```python
df.describe()
```

---

# 9. Selecting Columns

Suppose:

```python
df
```

contains:

```text
customer
product
quantity
price
city
date
```

Select one column:

```python
df["customer"]
```

Select multiple columns:

```python
df[
    ["customer", "product", "price"]
]
```

---

# 10. Selecting Rows

## `iloc`

Select by integer position.

```python
df.iloc[0]
```

First row.

```python
df.iloc[0:5]
```

First five rows.

---

## Specific rows and columns

```python
df.iloc[
    0:5,
    0:3
]
```

---

## `loc`

Select using labels or conditions.

```python
df.loc[0]
```

---

# 11. Filtering Data

Suppose:

```text
price > 50000
```

Python:

```python
df[df["price"] > 50000]
```

---

## Equal To

```python
df[df["city"] == "Hyderabad"]
```

---

## Not Equal

```python
df[df["city"] != "Hyderabad"]
```

---

## Greater Than

```python
df[df["sales"] > 10000]
```

---

## Less Than

```python
df[df["sales"] < 10000]
```

---

# 12. Multiple Conditions

## AND

Use `&`.

```python
df[
    (df["age"] > 25) &
    (df["salary"] > 50000)
]
```

Both conditions must be true.

---

## OR

Use `|`.

```python
df[
    (df["city"] == "Hyderabad") |
    (df["city"] == "Mumbai")
]
```

---

## NOT

Use `~`.

```python
df[
    ~(df["city"] == "Hyderabad")
]
```

---

# 13. Sorting Data

Ascending:

```python
df.sort_values("salary")
```

Descending:

```python
df.sort_values(
    "salary",
    ascending=False
)
```

Multiple columns:

```python
df.sort_values(
    ["city", "salary"],
    ascending=[True, False]
)
```

---

# 14. Limiting Data

First 10 rows:

```python
df.head(10)
```

Top 10 salaries:

```python
df.sort_values(
    "salary",
    ascending=False
).head(10)
```

---

# 15. Adding Columns

Create revenue:

```python
df["revenue"] = (
    df["quantity"] *
    df["price"]
)
```

Create profit:

```python
df["profit"] = (
    df["revenue"] -
    df["cost"]
)
```

---

# 16. Modifying Columns

Example:

```python
df["price"] = df["price"] * 1.10
```

This increases price by 10%.

---

# 17. Deleting Columns

```python
df = df.drop(
    columns=["unnecessary_column"]
)
```

Multiple columns:

```python
df = df.drop(
    columns=[
        "column1",
        "column2"
    ]
)
```

---

# 18. Renaming Columns

```python
df = df.rename(
    columns={
        "cust_id": "customer_id",
        "amt": "amount"
    }
)
```

---

# 19. Changing Data Types

Integer:

```python
df["age"] = df["age"].astype("Int64")
```

Float:

```python
df["price"] = df["price"].astype(float)
```

String:

```python
df["city"] = df["city"].astype(str)
```

Date:

```python
df["date"] = pd.to_datetime(
    df["date"]
)
```

---

# 20. String Manipulation

Pandas provides `.str`.

Convert to lowercase:

```python
df["city"] = (
    df["city"]
    .str.lower()
)
```

Uppercase:

```python
df["city"] = (
    df["city"]
    .str.upper()
)
```

Remove spaces:

```python
df["city"] = (
    df["city"]
    .str.strip()
)
```

Replace:

```python
df["city"] = (
    df["city"]
    .str.replace(
        "Hyd",
        "Hyderabad",
        regex=False
    )
)
```

Check whether text contains something:

```python
df[
    df["product"]
    .str.contains(
        "laptop",
        case=False,
        na=False
    )
]
```

---

# 21. Date and Time Manipulation

Convert:

```python
df["date"] = pd.to_datetime(
    df["date"]
)
```

Extract year:

```python
df["year"] = df["date"].dt.year
```

Month:

```python
df["month"] = df["date"].dt.month
```

Day:

```python
df["day"] = df["date"].dt.day
```

Day of week:

```python
df["day_of_week"] = (
    df["date"].dt.dayofweek
)
```

Quarter:

```python
df["quarter"] = (
    df["date"].dt.quarter
)
```

---

# 22. Missing Value Manipulation

Check:

```python
df.isnull().sum()
```

Filter missing:

```python
df[df["salary"].isnull()]
```

Fill:

```python
df["salary"] = (
    df["salary"]
    .fillna(df["salary"].median())
)
```

Remove:

```python
df = df.dropna(
    subset=["customer_id"]
)
```

Remember:

> Missing-value handling is primarily a data-cleaning/preprocessing activity, but it is often performed during a broader manipulation workflow.

---

# 23. Duplicate Manipulation

Check duplicates:

```python
df.duplicated().sum()
```

View:

```python
df[
    df.duplicated(
        keep=False
    )
]
```

Remove exact duplicates:

```python
df = df.drop_duplicates()
```

Based on a key:

```python
df = df.drop_duplicates(
    subset=["customer_id"]
)
```

---

# 24. Conditional Transformation

Create customer segments:

```python
df["segment"] = df["sales"].apply(
    lambda x:
        "High" if x >= 100000
        else "Medium" if x >= 50000
        else "Low"
)
```

For vectorized conditions, `np.select()` is often preferable for larger datasets:

```python
import numpy as np

conditions = [
    df["sales"] >= 100000,
    df["sales"] >= 50000
]

choices = [
    "High",
    "Medium"
]

df["segment"] = np.select(
    conditions,
    choices,
    default="Low"
)
```

---

# 25. Mapping Values

Suppose:

```text
M → Male
F → Female
```

Use:

```python
df["gender"] = df["gender"].map({
    "M": "Male",
    "F": "Female"
})
```

---

# 26. Apply and Lambda

## Lambda

A small anonymous function.

```python
square = lambda x: x ** 2

print(square(5))
```

Output:

```text
25
```

---

## Apply

```python
df["salary"] = df["salary"].apply(
    lambda x: x * 1.10
)
```

However, for simple column-wise arithmetic, vectorized Pandas operations are usually preferable:

```python
df["salary"] = df["salary"] * 1.10
```

---

# 27. Aggregation

Aggregation summarizes multiple records into a smaller result.

Examples:

```text
SUM
COUNT
AVG
MIN
MAX
MEDIAN
```

Python:

```python
df["sales"].sum()
```

```python
df["sales"].mean()
```

```python
df["sales"].min()
```

```python
df["sales"].max()
```

```python
df["sales"].count()
```

---

# 28. GroupBy

`groupby()` is one of the most important data manipulation operations.

Suppose:

```text
City       Sales
Hyderabad  10000
Hyderabad  20000
Mumbai     15000
Mumbai     25000
```

Group by city:

```python
df.groupby("city")["sales"].sum()
```

Result:

```text
Hyderabad → 30000
Mumbai    → 40000
```

---

# 29. GroupBy with Multiple Aggregations

```python
df.groupby("city")["sales"].agg(
    [
        "sum",
        "mean",
        "min",
        "max",
        "count"
    ]
)
```

---

## Different functions for different columns

```python
df.groupby("city").agg({
    "sales": "sum",
    "quantity": "sum",
    "price": "mean"
})
```

---

# 30. Pivot Tables

Pivot tables summarize data across dimensions.

```python
pd.pivot_table(
    df,
    values="sales",
    index="city",
    columns="product",
    aggfunc="sum",
    fill_value=0
)
```

Conceptually:

```text
             Laptop   Phone
Hyderabad     50000   30000
Mumbai        70000   40000
```

---

# 31. Crosstab

Used for frequency/count relationships between categorical variables.

```python
pd.crosstab(
    df["gender"],
    df["city"]
)
```

Example:

```text
city
gender       Delhi   Mumbai   Hyderabad
Male             10       15        20
Female           12       18        22
```

---

# 32. Merging Data

Suppose we have:

### Customers

```text
customer_id | name
1           | Ravi
2           | Priya
```

### Orders

```text
order_id | customer_id | amount
101      | 1           | 5000
102      | 2           | 7000
```

Merge:

```python
result = pd.merge(
    customers,
    orders,
    on="customer_id"
)
```

---

# 33. Joining Data

## Inner Join

Only matching records.

```python
pd.merge(
    customers,
    orders,
    on="customer_id",
    how="inner"
)
```

---

## Left Join

Keep all customers.

```python
pd.merge(
    customers,
    orders,
    on="customer_id",
    how="left"
)
```

---

## Right Join

Keep all orders.

```python
pd.merge(
    customers,
    orders,
    on="customer_id",
    how="right"
)
```

---

## Outer Join

Keep everything.

```python
pd.merge(
    customers,
    orders,
    on="customer_id",
    how="outer"
)
```

---

# 34. Concatenating Data

Suppose:

```text
January data
February data
March data
```

Stack rows:

```python
all_sales = pd.concat(
    [
        january,
        february,
        march
    ],
    ignore_index=True
)
```

---

## Concatenate Columns

```python
result = pd.concat(
    [df1, df2],
    axis=1
)
```

Use carefully because row alignment matters.

---

# 35. Reshaping Data

Reshaping changes the structure of a dataset.

Main operations:

```text
Melt
Pivot
Stack
Unstack
Transpose
```

---

# 36. Wide vs Long Data

## Wide Format

```text
Customer | Jan | Feb | Mar
A        | 100 | 200 | 300
B        | 150 | 250 | 350
```

## Long Format

```text
Customer | Month | Sales
A        | Jan   | 100
A        | Feb   | 200
A        | Mar   | 300
B        | Jan   | 150
```

Long format is often convenient for analysis and visualization.

---

# 37. Melt

Convert wide → long.

```python
long_df = pd.melt(
    df,
    id_vars=["customer"],
    var_name="month",
    value_name="sales"
)
```

---

# 38. Pivot

Convert long → wide.

```python
wide_df = df.pivot(
    index="customer",
    columns="month",
    values="sales"
)
```

If duplicate combinations exist, use `pivot_table()` with an aggregation function.

---

# 39. Stack and Unstack

`stack()` moves columns into an index level.

```python
df.stack()
```

`unstack()` moves an index level into columns.

```python
df.unstack()
```

These operations are particularly useful with MultiIndex data.

---

# 40. Ranking

Rank customers by sales:

```python
df["sales_rank"] = (
    df["sales"]
    .rank(
        ascending=False,
        method="dense"
    )
)
```

Example:

```text
Customer   Sales   Rank
A          100000   1
B           90000   2
C           80000   3
```

---

# 41. Window-Based Manipulation

Window operations calculate values relative to other rows without collapsing the dataset.

Examples:

```text
Rolling Average
Rank
Running Total
Previous Value
Next Value
Percentage Change
```

---

# 42. Rolling Operations

7-day moving average:

```python
df["rolling_7"] = (
    df["sales"]
    .rolling(7)
    .mean()
)
```

---

## Rolling Sum

```python
df["rolling_sales"] = (
    df["sales"]
    .rolling(7)
    .sum()
)
```

Useful for:

```text
Trend analysis
Smoothing
Time-series analysis
```

---

# 43. Lag and Lead

## Lag

Previous observation:

```python
df["previous_sales"] = (
    df["sales"]
    .shift(1)
)
```

---

## Lead

Next observation:

```python
df["next_sales"] = (
    df["sales"]
    .shift(-1)
)
```

---

# 44. Cumulative Operations

Running total:

```python
df["running_sales"] = (
    df["sales"]
    .cumsum()
)
```

Cumulative maximum:

```python
df["running_max"] = (
    df["sales"]
    .cummax()
)
```

Cumulative minimum:

```python
df["running_min"] = (
    df["sales"]
    .cummin()
)
```

---

# 45. Percentage Change

Calculate period-over-period change:

```python
df["growth"] = (
    df["sales"]
    .pct_change()
)
```

Percentage:

```python
df["growth_percent"] = (
    df["sales"]
    .pct_change() * 100
)
```

Formula:

```text
Percentage Change =
(Current - Previous) / Previous × 100
```

---

# 46. SQL Data Manipulation

SQL is extremely important for data analytics.

Common SQL manipulation operations:

```text
SELECT
WHERE
ORDER BY
LIMIT
CASE
GROUP BY
HAVING
JOIN
UNION
CTE
Subqueries
Window Functions
```

---

# 47. SQL Filtering

```sql
SELECT *
FROM customers
WHERE age > 25;
```

Multiple conditions:

```sql
SELECT *
FROM customers
WHERE age > 25
  AND salary > 50000;
```

---

# 48. SQL Aggregation

```sql
SELECT
    SUM(sales) AS total_sales,
    AVG(sales) AS average_sales,
    MIN(sales) AS minimum_sales,
    MAX(sales) AS maximum_sales,
    COUNT(*) AS transaction_count
FROM sales;
```

---

# 49. SQL Grouping

```sql
SELECT
    city,
    SUM(sales) AS total_sales
FROM sales
GROUP BY city;
```

Multiple groups:

```sql
SELECT
    city,
    product,
    SUM(sales) AS total_sales
FROM sales
GROUP BY
    city,
    product;
```

---

# 50. SQL Joins

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Types:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
CROSS JOIN
SELF JOIN
```

---

# 51. SQL Subqueries

Example:

Find customers whose spending is above average:

```sql
SELECT *
FROM customers
WHERE total_spending >
(
    SELECT AVG(total_spending)
    FROM customers
);
```

---

# 52. SQL CTEs

CTE:

**Common Table Expression**

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)

SELECT *
FROM customer_sales
WHERE total_sales > 100000;
```

CTEs improve readability and can simplify complex analytical queries.

---

# 53. SQL Window Functions

Example:

```sql
SELECT
    customer_id,
    sales,
    RANK() OVER (
        ORDER BY sales DESC
    ) AS sales_rank
FROM sales;
```

---

## Partitioned Window

```sql
SELECT
    city,
    customer_id,
    sales,
    RANK() OVER (
        PARTITION BY city
        ORDER BY sales DESC
    ) AS city_rank
FROM sales;
```

---

# 54. Data Manipulation for Analytics

Data manipulation is essential for analytical questions.

Example:

> Which city generated the highest revenue?

Steps:

```text
Sales Data
   ↓
Group by city
   ↓
SUM(revenue)
   ↓
Sort descending
   ↓
Top city
```

Python:

```python
result = (
    df.groupby("city")["revenue"]
      .sum()
      .sort_values(ascending=False)
)
```

SQL:

```sql
SELECT
    city,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY city
ORDER BY total_revenue DESC;
```

---

# 55. Sales Analytics

Useful manipulations:

```text
Total Sales
Average Order Value
Revenue by Product
Revenue by Region
Monthly Sales
Top Products
Sales Growth
Profit Margin
```

---

## Revenue

```python
df["revenue"] = (
    df["quantity"] *
    df["unit_price"]
)
```

---

## SQL

```sql
SELECT
    quantity * unit_price AS revenue
FROM sales;
```

---

# 56. Customer Analytics

Common metrics:

```text
Total Customers
Active Customers
Orders per Customer
Average Customer Spend
Customer Lifetime Value
Repeat Purchase Rate
Customer Segmentation
```

Example:

```python
customer_summary = (
    df.groupby("customer_id")
      .agg(
          orders=("order_id", "nunique"),
          revenue=("revenue", "sum"),
          average_order=("revenue", "mean")
      )
)
```

---

# 57. Time-Series Manipulation

Important operations:

```text
Date extraction
Sorting by date
Resampling
Aggregation
Rolling average
Lag
Lead
Growth
Cumulative totals
```

---

## Monthly Sales

```python
df["date"] = pd.to_datetime(df["date"])

monthly_sales = (
    df.set_index("date")
      .resample("ME")["sales"]
      .sum()
)
```

---

## SQL

Syntax varies by database.

Conceptually:

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(sales) AS total_sales
FROM orders
GROUP BY
    DATE_TRUNC('month', order_date)
ORDER BY month;
```

---

# 58. Real-World Example

Suppose we have:

```text
orders.csv
customers.csv
products.csv
```

---

## Step 1 — Load Data

```python
orders = pd.read_csv("orders.csv")
customers = pd.read_csv("customers.csv")
products = pd.read_csv("products.csv")
```

---

## Step 2 — Inspect

```python
print(orders.info())
print(customers.info())
print(products.info())
```

---

## Step 3 — Calculate Revenue

```python
orders["revenue"] = (
    orders["quantity"] *
    orders["unit_price"]
)
```

---

## Step 4 — Merge Customers

```python
orders = orders.merge(
    customers,
    on="customer_id",
    how="left"
)
```

---

## Step 5 — Merge Products

```python
orders = orders.merge(
    products,
    on="product_id",
    how="left"
)
```

---

## Step 6 — Create Date Features

```python
orders["order_date"] = (
    pd.to_datetime(
        orders["order_date"]
    )
)

orders["year"] = (
    orders["order_date"].dt.year
)

orders["month"] = (
    orders["order_date"].dt.month
)
```

---

## Step 7 — Calculate Customer Revenue

```python
customer_revenue = (
    orders
    .groupby("customer_id")
    ["revenue"]
    .sum()
    .reset_index()
)
```

---

## Step 8 — Find Top Customers

```python
top_customers = (
    customer_revenue
    .sort_values(
        "revenue",
        ascending=False
    )
    .head(10)
)
```

---

## Step 9 — Monthly Sales

```python
monthly_sales = (
    orders
    .set_index("order_date")
    .resample("ME")["revenue"]
    .sum()
)
```

---

# 59. Common Mistakes

## Mistake 1 — Modifying original data

Keep a raw copy.

```python
raw_df = df.copy()
```

---

## Mistake 2 — Ignoring data types

Dates should generally be represented as dates/timestamps rather than arbitrary strings when date operations are required.

---

## Mistake 3 — Applying Python loops unnecessarily

Prefer vectorized Pandas operations when practical.

Instead of:

```python
for i in range(len(df)):
    df.loc[i, "revenue"] = (
        df.loc[i, "quantity"] *
        df.loc[i, "price"]
    )
```

prefer:

```python
df["revenue"] = (
    df["quantity"] *
    df["price"]
)
```

---

## Mistake 4 — Incorrect joins

Always understand:

```text
Primary key
Foreign key
One-to-one
One-to-many
Many-to-many
```

before merging.

---

## Mistake 5 — Accidental many-to-many duplication

If both datasets contain multiple rows for the same join key, a merge can multiply records.

Always validate expected join cardinality.

---

# 60. Best Practices

### 1. Understand the data first

```text
Schema
Types
Keys
Relationships
Business meaning
```

---

### 2. Keep raw data unchanged

```text
Raw
 ↓
Processed copy
```

---

### 3. Use meaningful column names

Bad:

```text
x1
x2
x3
```

Better:

```text
customer_id
order_date
revenue
```

---

### 4. Validate results

After manipulation check:

```python
df.shape
df.head()
df.info()
df.describe()
```

---

### 5. Check joins

Compare row counts before and after merging.

---

### 6. Use vectorized operations

They are usually cleaner and faster than row-by-row Python loops.

---

### 7. Document important transformations

Record what was changed and why.

---

# 61. Interview Questions

## Q1. What is data manipulation?

Data manipulation is the process of selecting, filtering, transforming, aggregating, combining, and restructuring data for analysis.

---

## Q2. What is the difference between cleaning and manipulation?

Cleaning focuses on fixing data-quality problems.

Manipulation focuses on changing, organizing, combining, and summarizing data for analytical use.

---

## Q3. What is `groupby()`?

`groupby()` divides data into groups based on one or more columns and allows aggregation or other group-level operations.

---

## Q4. What is aggregation?

Aggregation summarizes multiple observations into statistics such as:

```text
SUM
AVG
COUNT
MIN
MAX
```

---

## Q5. What is the difference between merge and concat?

### Merge

Combines datasets based on matching keys.

```python
pd.merge(...)
```

### Concat

Stacks or combines datasets along an axis.

```python
pd.concat(...)
```

---

## Q6. What is reshaping?

Changing the structural arrangement of data.

Examples:

```text
Wide → Long
Long → Wide
```

Using:

```text
melt
pivot
stack
unstack
```

---

## Q7. What is a window operation?

A calculation performed across a related set of rows while generally preserving the original row-level detail.

Examples:

```text
Ranking
Running total
Rolling average
Lag
Lead
```

---

# 62. Final Revision

## 🔥 Core Data Manipulation Operations

```text
DATA MANIPULATION
│
├── SELECT
│   ├── Columns
│   └── Rows
│
├── FILTER
│   ├── Conditions
│   ├── AND
│   ├── OR
│   └── NOT
│
├── SORT
│   ├── Ascending
│   └── Descending
│
├── TRANSFORM
│   ├── Calculated Columns
│   ├── Mapping
│   ├── Apply
│   └── Lambda
│
├── AGGREGATE
│   ├── SUM
│   ├── AVG
│   ├── COUNT
│   ├── MIN
│   └── MAX
│
├── GROUP
│   └── GROUP BY
│
├── COMBINE
│   ├── Merge
│   ├── Join
│   └── Concatenate
│
├── RESHAPE
│   ├── Melt
│   ├── Pivot
│   ├── Stack
│   └── Unstack
│
├── TIME SERIES
│   ├── Lag
│   ├── Lead
│   ├── Rolling
│   ├── Cumulative
│   └── Percentage Change
│
└── ANALYTICS
    ├── Sales
    ├── Customer
    ├── Product
    ├── Financial
    └── Time Series
```

---

# 🧠 Most Important Pandas Commands

```python
df.head()
df.tail()
df.shape
df.info()
df.describe()

df["column"]
df[["col1", "col2"]]

df.loc[]
df.iloc[]

df[df["age"] > 25]

df.sort_values()
df.sort_index()

df.rename()
df.drop()
df.astype()

df.isnull()
df.fillna()
df.dropna()

df.drop_duplicates()

df.groupby()
df.agg()

df.merge()
pd.concat()

pd.pivot_table()
pd.crosstab()

pd.melt()

df.apply()
df.map()

df.shift()
df.rolling()
df.cumsum()
df.pct_change()
df.rank()
```

---

# 🧠 Most Important SQL Commands for Manipulation

```sql
SELECT
FROM
WHERE
ORDER BY
LIMIT
DISTINCT

CASE
GROUP BY
HAVING

JOIN
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN

UNION
UNION ALL

WITH

Subqueries

Window Functions
OVER()
PARTITION BY
ORDER BY
```

---

# ⭐ Final Mental Model

```text
                 DATA MANIPULATION
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
      SELECT          FILTER           SORT
        │               │                │
        └───────────────┼────────────────┘
                        ↓
                   TRANSFORM
                        │
                        ↓
                  CALCULATED DATA
                        │
                        ↓
                     GROUP
                        │
                        ↓
                   AGGREGATE
                        │
                        ↓
                MERGE / JOIN DATA
                        │
                        ↓
                    RESHAPE
                        │
                        ↓
                 ANALYTICAL DATA
                        │
             ┌──────────┼──────────┐
             ↓          ↓          ↓
           SALES     CUSTOMER    TIME SERIES
             │          │          │
             └──────────┼──────────┘
                        ↓
                    INSIGHTS
```

> **Core idea:** Data manipulation is the process of turning available data into the **right structure, subset, calculations, and summaries needed to answer analytical questions**. In data analytics, the most important skills are **filtering, selecting, sorting, creating calculated columns, grouping, aggregation, joining, merging, reshaping, and window-based operations** using tools such as **Pandas and SQL**.
