# 🧹 SQL for Data Cleaning

SQL is widely used for **cleaning, validating, standardizing, transforming, and preparing data** before analysis.

Data cleaning is especially important in data analytics because real-world data commonly contains:

```text
NULL values
Duplicate records
Incorrect data types
Inconsistent text
Invalid values
Incorrect dates
Extra spaces
Missing values
Outliers
Inconsistent categories
Formatting problems
```

---

# 📚 Table of Contents

1. [What is Data Cleaning?](#1-what-is-data-cleaning)
2. [Why Data Cleaning is Important](#2-why-data-cleaning-is-important)
3. [Data Cleaning Workflow](#3-data-cleaning-workflow)
4. [Inspecting Data](#4-inspecting-data)
5. [Finding NULL Values](#5-finding-null-values)
6. [Handling NULL Values](#6-handling-null-values)
7. [COALESCE](#7-coalesce)
8. [NULLIF](#8-nullif)
9. [Replacing NULL Values](#9-replacing-null-values)
10. [Finding Duplicate Records](#10-finding-duplicate-records)
11. [Removing Duplicates](#11-removing-duplicates)
12. [Removing Extra Spaces](#12-removing-extra-spaces)
13. [Cleaning Text](#13-cleaning-text)
14. [Standardizing Case](#14-standardizing-case)
15. [Replacing Characters](#15-replacing-characters)
16. [Handling Empty Strings](#16-handling-empty-strings)
17. [Standardizing Categories](#17-standardizing-categories)
18. [Data Type Conversion](#18-data-type-conversion)
19. [Cleaning Numbers](#19-cleaning-numbers)
20. [Cleaning Dates](#20-cleaning-dates)
21. [Finding Invalid Values](#21-finding-invalid-values)
22. [CASE for Data Cleaning](#22-case-for-data-cleaning)
23. [Removing Invalid Records](#23-removing-invalid-records)
24. [Handling Outliers](#24-handling-outliers)
25. [Data Validation](#25-data-validation)
26. [Referential Integrity](#26-referential-integrity)
27. [Cleaning with CTEs](#27-cleaning-with-ctes)
28. [Cleaning with Temporary Tables](#28-cleaning-with-temporary-tables)
29. [Creating a Clean Table](#29-creating-a-clean-table)
30. [Complete Data Cleaning Example](#30-complete-data-cleaning-example)
31. [Data Cleaning Checklist](#31-data-cleaning-checklist)
32. [SQL Data Cleaning Cheat Sheet](#32-sql-data-cleaning-cheat-sheet)

---

# 1. What is Data Cleaning?

## Easy Definition

**Data cleaning** is the process of identifying and fixing incorrect, incomplete, inconsistent, duplicated, or unusable data.

### Technical Definition

Data cleaning is the process of detecting, correcting, removing, standardizing, and validating data-quality issues before data is used for analysis or decision-making.

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

Clean data:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Validated Data
   ↓
Analysis
   ↓
Reliable Insights
```

---

# 3. Data Cleaning Workflow

A typical SQL data-cleaning workflow:

```text
Raw Data
   ↓
Inspect
   ↓
Identify Problems
   ↓
Handle NULLs
   ↓
Remove Duplicates
   ↓
Clean Text
   ↓
Standardize Categories
   ↓
Convert Data Types
   ↓
Clean Dates
   ↓
Validate Values
   ↓
Handle Outliers
   ↓
Final Quality Check
   ↓
Clean Dataset
```

---

# 4. Inspecting Data

Before changing anything, inspect the dataset.

## View all rows

```sql
SELECT *
FROM customers;
```

## View selected columns

```sql
SELECT
    customer_id,
    name,
    email,
    city
FROM customers;
```

## Count records

```sql
SELECT COUNT(*) AS total_records
FROM customers;
```

## Check unique values

```sql
SELECT DISTINCT city
FROM customers;
```

## Count unique values

```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customers;
```

---

# 5. Finding NULL Values

`NULL` means that a value is missing or unknown.

It is not the same as:

```text
0
''
'NULL'
'Unknown'
```

---

## Find NULL values

```sql
SELECT *
FROM customers
WHERE email IS NULL;
```

---

## Find non-NULL values

```sql
SELECT *
FROM customers
WHERE email IS NOT NULL;
```

---

## Count NULL values

```sql
SELECT
    COUNT(*) AS total_rows,
    COUNT(email) AS non_null_emails
FROM customers;
```

Because `COUNT(column)` does not count NULL values.

Therefore:

```text
NULL emails =
COUNT(*) - COUNT(email)
```

---

# 6. Handling NULL Values

There are several ways to handle missing data.

### Method 1: Keep NULL

Sometimes NULL is meaningful.

Example:

```text
middle_name = NULL
```

This may simply mean the customer has no middle name recorded.

---

### Method 2: Replace NULL

```sql
SELECT
    COALESCE(phone, 'Not Available') AS phone
FROM customers;
```

---

### Method 3: Remove rows

```sql
DELETE FROM customers
WHERE email IS NULL;
```

⚠️ Do this only when missing values make the record unusable and you have confirmed deletion is appropriate.

---

### Method 4: Impute

For numerical data, a missing value may sometimes be replaced with:

```text
Mean
Median
Mode
Business-defined value
```

Example:

```sql
SELECT
    COALESCE(salary, 0) AS salary
FROM employees;
```

But replacing missing values with `0` should only be done when `0` has a valid business meaning.

---

# 7. COALESCE

`COALESCE()` returns the first non-NULL value.

```sql
SELECT
    COALESCE(phone, email, 'No Contact') AS contact
FROM customers;
```

Logic:

```text
phone available?
    ↓ YES → phone
    ↓ NO
email available?
    ↓ YES → email
    ↓ NO
'No Contact'
```

---

## Multiple fallback values

```sql
SELECT
    COALESCE(
        phone,
        alternate_phone,
        email,
        'Not Available'
    ) AS contact
FROM customers;
```

---

# 8. NULLIF

`NULLIF()` returns NULL when two values are equal.

```sql
SELECT
    NULLIF(phone, '') AS phone
FROM customers;
```

This converts an empty string into NULL.

Another example:

```sql
SELECT
    NULLIF(sales, 0) AS sales
FROM orders;
```

Useful for avoiding division-by-zero situations:

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS revenue_per_unit
FROM sales;
```

---

# 9. Replacing NULL Values

## Text

```sql
SELECT
    COALESCE(city, 'Unknown') AS city
FROM customers;
```

## Number

```sql
SELECT
    COALESCE(discount, 0) AS discount
FROM orders;
```

## Date

```sql
SELECT
    COALESCE(order_date, CURRENT_DATE) AS order_date
FROM orders;
```

Be careful with replacing missing dates with the current date because it changes the meaning of the data.

---

# 10. Finding Duplicate Records

Duplicates are one of the most common data-quality problems.

Example:

```text
customer_id | name
------------|------
101         | Rahul
102         | Priya
101         | Rahul
```

Here `customer_id = 101` appears twice.

---

## Find duplicate IDs

```sql
SELECT
    customer_id,
    COUNT(*) AS count_records
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

---

## Find duplicate emails

```sql
SELECT
    email,
    COUNT(*) AS count_records
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

---

## Find complete duplicate rows

```sql
SELECT
    name,
    email,
    city,
    COUNT(*) AS duplicate_count
FROM customers
GROUP BY
    name,
    email,
    city
HAVING COUNT(*) > 1;
```

---

# 11. Removing Duplicates

A common approach is to use `ROW_NUMBER()`.

```sql
WITH duplicates AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY customer_id
        ) AS rn
    FROM customers
)
SELECT *
FROM duplicates
WHERE rn = 1;
```

This keeps one row for each `customer_id`.

---

## More realistic example

Suppose we want to keep the most recently updated record.

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY updated_at DESC
        ) AS rn
    FROM customers
)
SELECT *
FROM ranked
WHERE rn = 1;
```

Here:

```text
rn = 1 → latest record
rn > 1 → duplicate/older records
```

---

# 12. Removing Extra Spaces

Real-world text often contains unwanted spaces.

Example:

```text
'  Rahul  '
```

Use `TRIM()`.

```sql
SELECT
    TRIM(name) AS cleaned_name
FROM customers;
```

Result:

```text
Rahul
```

---

## Update the table

```sql
UPDATE customers
SET name = TRIM(name);
```

---

# 13. Cleaning Text

Useful text functions include:

```text
TRIM()
UPPER()
LOWER()
LENGTH()
SUBSTRING()
REPLACE()
CONCAT()
LEFT()
RIGHT()
```

Availability and syntax can vary by SQL database.

---

# 14. Standardizing Case

Suppose:

```text
Hyderabad
HYDERABAD
hyderabad
HyDeRaBaD
```

These represent the same city but have inconsistent formatting.

Use:

```sql
SELECT
    UPPER(city) AS city
FROM customers;
```

Result:

```text
HYDERABAD
HYDERABAD
HYDERABAD
HYDERABAD
```

Or:

```sql
SELECT
    LOWER(city) AS city
FROM customers;
```

---

# 15. Replacing Characters

Suppose phone numbers contain:

```text
+91-9876543210
+91 9876543210
9876543210
```

You can remove unwanted characters.

```sql
SELECT
    REPLACE(phone, '-', '') AS cleaned_phone
FROM customers;
```

Multiple replacements:

```sql
SELECT
    REPLACE(
        REPLACE(phone, '-', ''),
        ' ',
        ''
    ) AS cleaned_phone
FROM customers;
```

---

# 16. Handling Empty Strings

An empty string:

```text
''
```

is not necessarily the same as `NULL`.

Find empty values:

```sql
SELECT *
FROM customers
WHERE email = '';
```

Find both:

```sql
SELECT *
FROM customers
WHERE email IS NULL
   OR email = '';
```

Convert empty string to NULL:

```sql
SELECT
    NULLIF(TRIM(email), '') AS email
FROM customers;
```

This is useful because:

```text
'     '
```

becomes:

```text
''
```

after `TRIM()`, then `NULLIF()` converts it to NULL.

---

# 17. Standardizing Categories

Suppose the database contains:

```text
Male
male
M
MALE
m
```

These should be standardized.

```sql
SELECT
    CASE
        WHEN LOWER(TRIM(gender)) IN ('male', 'm')
            THEN 'Male'

        WHEN LOWER(TRIM(gender)) IN ('female', 'f')
            THEN 'Female'

        ELSE 'Unknown'
    END AS gender
FROM customers;
```

---

# 18. Data Type Conversion

Incorrect data types can cause problems.

Example:

```text
'100'
'200'
'300'
```

stored as text instead of numbers.

Convert:

```sql
SELECT
    CAST(price AS DECIMAL(10,2)) AS price
FROM products;
```

Some SQL databases also support:

```sql
SELECT
    CAST(price AS INTEGER)
FROM products;
```

or:

```sql
SELECT
    CAST(order_date AS DATE)
FROM orders;
```

Syntax differs between database systems.

---

# 19. Cleaning Numbers

Common numerical problems:

```text
Negative values where impossible
Numbers stored as text
Extreme values
Zero values
Missing values
Incorrect decimal precision
```

---

## Find negative prices

```sql
SELECT *
FROM products
WHERE price < 0;
```

---

## Find invalid quantities

```sql
SELECT *
FROM order_items
WHERE quantity <= 0;
```

---

## Find suspicious ages

```sql
SELECT *
FROM customers
WHERE age < 0
   OR age > 120;
```

The exact business limits should be defined based on the dataset.

---

# 20. Cleaning Dates

Date problems include:

```text
NULL dates
Invalid dates
Future dates
Wrong date format
Different date formats
```

---

## Find NULL dates

```sql
SELECT *
FROM orders
WHERE order_date IS NULL;
```

---

## Find future dates

```sql
SELECT *
FROM orders
WHERE order_date > CURRENT_DATE;
```

---

## Extract year

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year
FROM orders;
```

---

## Extract month

```sql
SELECT
    EXTRACT(MONTH FROM order_date) AS month
FROM orders;
```

---

# 21. Finding Invalid Values

Suppose valid order statuses are:

```text
Pending
Shipped
Delivered
Cancelled
```

Find invalid values:

```sql
SELECT DISTINCT status
FROM orders
WHERE status NOT IN (
    'Pending',
    'Shipped',
    'Delivered',
    'Cancelled'
);
```

---

# 22. CASE for Data Cleaning

`CASE` is extremely useful for transforming dirty data.

Example:

```sql
SELECT
    customer_id,
    CASE
        WHEN age < 0 THEN NULL
        WHEN age > 120 THEN NULL
        ELSE age
    END AS cleaned_age
FROM customers;
```

---

## Standardizing categories

```sql
SELECT
    CASE
        WHEN LOWER(TRIM(city)) IN ('hyd', 'hyderabad')
            THEN 'Hyderabad'

        WHEN LOWER(TRIM(city)) IN ('blr', 'bangalore', 'bengaluru')
            THEN 'Bangalore'

        ELSE 'Other'
    END AS standardized_city
FROM customers;
```

---

# 23. Removing Invalid Records

Suppose orders with negative quantities are invalid.

Find them first:

```sql
SELECT *
FROM order_items
WHERE quantity < 0;
```

If business rules confirm they are invalid and should be deleted:

```sql
DELETE FROM order_items
WHERE quantity < 0;
```

### Important

Do not immediately delete suspicious data.

Prefer:

```text
Identify
   ↓
Validate
   ↓
Understand business rule
   ↓
Fix / quarantine / delete
```

---

# 24. Handling Outliers

An outlier is a value that is unusually different from the rest of the data.

Example:

```text
100
120
110
105
115
1000000
```

`1000000` may be an outlier.

But an outlier is not automatically an error.

It could be:

```text
A genuine large transaction
A special customer
A data-entry error
Fraud
A measurement error
```

---

## Basic statistical detection

Using average and standard deviation:

```sql
SELECT
    AVG(sales_amount) AS avg_sales,
    STDDEV(sales_amount) AS std_sales
FROM sales;
```

A common statistical rule is:

```text
value < mean - 3 × standard deviation
OR
value > mean + 3 × standard deviation
```

However, the appropriate method depends on the dataset and business context.

---

## IQR Method

Another common method uses:

```text
Q1 = 25th percentile
Q3 = 75th percentile

IQR = Q3 - Q1
```

Outlier boundaries:

```text
Lower = Q1 - 1.5 × IQR
Upper = Q3 + 1.5 × IQR
```

Exact percentile functions vary by database.

---

# 25. Data Validation

Data validation means checking whether cleaned data follows expected rules.

Examples:

```text
customer_id must be unique
email should not be NULL
age should be within a valid range
price should not be negative
order_date should not be in the future
foreign keys should have matching records
```

---

## Validation query

```sql
SELECT *
FROM customers
WHERE customer_id IS NULL
   OR age < 0
   OR age > 120;
```

---

## Email validation

A basic pattern check can identify suspicious values.

For example, in databases supporting regular expressions:

```sql
SELECT *
FROM customers
WHERE email NOT REGEXP '^[^@]+@[^@]+\.[^@]+$';
```

The exact regex operator differs by database.

This should be treated as a basic quality check, not a guarantee that an email address actually exists.

---

# 26. Referential Integrity

Suppose:

```text
customers
---------
customer_id

orders
------
customer_id
```

Every `orders.customer_id` should normally correspond to a customer.

Find orphan records:

```sql
SELECT o.*
FROM orders o
LEFT JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

These are called **orphan records**.

---

# 27. Cleaning with CTEs

CTEs are useful when cleaning data through multiple steps.

Example:

```sql
WITH cleaned AS (
    SELECT
        customer_id,
        TRIM(UPPER(name)) AS name,
        LOWER(TRIM(email)) AS email,
        COALESCE(city, 'Unknown') AS city
    FROM customers
)
SELECT *
FROM cleaned;
```

---

## Multiple cleaning steps

```sql
WITH step1 AS (
    SELECT
        *,
        TRIM(name) AS cleaned_name
    FROM customers
),

step2 AS (
    SELECT
        *,
        LOWER(TRIM(email)) AS cleaned_email
    FROM step1
),

step3 AS (
    SELECT
        *,
        COALESCE(city, 'Unknown') AS cleaned_city
    FROM step2
)

SELECT *
FROM step3;
```

This makes complex cleaning logic easier to understand and debug.

---

# 28. Cleaning with Temporary Tables

A temporary table can be useful when performing multiple cleaning operations.

```sql
CREATE TEMPORARY TABLE clean_customers AS
SELECT
    customer_id,
    TRIM(name) AS name,
    LOWER(TRIM(email)) AS email,
    COALESCE(city, 'Unknown') AS city
FROM customers;
```

Then:

```sql
SELECT *
FROM clean_customers;
```

Temporary table behavior varies by database system.

---

# 29. Creating a Clean Table

Instead of modifying the original raw data immediately, create a cleaned table.

```sql
CREATE TABLE clean_customers AS
SELECT
    customer_id,
    TRIM(name) AS name,
    LOWER(TRIM(email)) AS email,
    COALESCE(city, 'Unknown') AS city
FROM customers;
```

This approach can be safer during exploration.

---

# 30. Complete Data Cleaning Example

Suppose we have:

```text
customers
------------------------------------------------
customer_id | name       | email       | city
------------------------------------------------
1           | ' Rahul '  | R@EMAIL.COM | hyd
2           | 'PRIYA'     | NULL        | Hyderabad
3           | ' rahul '  | r@email.com | HYD
3           | ' rahul '  | r@email.com | HYD
4           | 'John'      |             | blr
```

Problems:

```text
1. Extra spaces
2. Inconsistent case
3. NULL email
4. Empty email
5. Inconsistent city names
6. Duplicate customer_id
```

---

## Step 1: Clean text

```sql
SELECT
    customer_id,
    TRIM(name) AS name,
    LOWER(TRIM(email)) AS email,
    TRIM(city) AS city
FROM customers;
```

---

## Step 2: Convert empty email to NULL

```sql
SELECT
    customer_id,
    TRIM(name) AS name,
    NULLIF(LOWER(TRIM(email)), '') AS email,
    TRIM(city) AS city
FROM customers;
```

---

## Step 3: Standardize cities

```sql
SELECT
    customer_id,
    TRIM(name) AS name,
    NULLIF(LOWER(TRIM(email)), '') AS email,

    CASE
        WHEN LOWER(TRIM(city)) IN ('hyd', 'hyderabad')
            THEN 'Hyderabad'

        WHEN LOWER(TRIM(city)) IN ('blr', 'bangalore', 'bengaluru')
            THEN 'Bangalore'

        ELSE 'Unknown'
    END AS city

FROM customers;
```

---

## Step 4: Remove duplicates

Use `ROW_NUMBER()`:

```sql
WITH cleaned AS (
    SELECT
        customer_id,
        TRIM(name) AS name,
        NULLIF(LOWER(TRIM(email)), '') AS email,

        CASE
            WHEN LOWER(TRIM(city)) IN ('hyd', 'hyderabad')
                THEN 'Hyderabad'

            WHEN LOWER(TRIM(city)) IN ('blr', 'bangalore', 'bengaluru')
                THEN 'Bangalore'

            ELSE 'Unknown'
        END AS city,

        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY customer_id
        ) AS rn

    FROM customers
)

SELECT
    customer_id,
    name,
    email,
    city
FROM cleaned
WHERE rn = 1;
```

---

# 31. Data Cleaning Checklist

Before using a dataset for analysis, check:

## Missing Values

```text
[ ] Find NULL values
[ ] Find empty strings
[ ] Decide how to handle missing data
```

## Duplicates

```text
[ ] Find duplicate IDs
[ ] Find duplicate records
[ ] Decide which record to retain
```

## Text

```text
[ ] Remove spaces
[ ] Standardize uppercase/lowercase
[ ] Standardize categories
[ ] Remove unwanted characters
```

## Numbers

```text
[ ] Check data types
[ ] Find negative values
[ ] Find impossible values
[ ] Check outliers
```

## Dates

```text
[ ] Check NULL dates
[ ] Check invalid dates
[ ] Check future dates
[ ] Standardize date representation
```

## Relationships

```text
[ ] Check foreign keys
[ ] Find orphan records
[ ] Check duplicate primary keys
```

## Final Validation

```text
[ ] Check row count
[ ] Check NULL count
[ ] Check duplicate count
[ ] Check distinct categories
[ ] Check numerical ranges
[ ] Compare before/after totals
```

---

# 32. SQL Data Cleaning Cheat Sheet

| Problem               | SQL Technique       |
| --------------------- | ------------------- |
| Missing value         | `IS NULL`           |
| Non-missing           | `IS NOT NULL`       |
| Replace NULL          | `COALESCE()`        |
| Convert value to NULL | `NULLIF()`          |
| Remove spaces         | `TRIM()`            |
| Uppercase             | `UPPER()`           |
| Lowercase             | `LOWER()`           |
| Replace characters    | `REPLACE()`         |
| Conditional cleaning  | `CASE`              |
| Find duplicates       | `GROUP BY + HAVING` |
| Remove duplicate rows | `ROW_NUMBER()`      |
| Convert type          | `CAST()`            |
| Unique values         | `DISTINCT`          |
| Find invalid values   | `WHERE`             |
| Validate categories   | `IN / NOT IN`       |
| Find orphan records   | `LEFT JOIN`         |
| Statistical analysis  | `AVG()`, `STDDEV()` |
| Multi-step cleaning   | `CTE`               |
| Temporary cleaning    | `TEMP TABLE`        |

---

# 🔥 Important SQL Data Cleaning Patterns

## Pattern 1 — NULL Handling

```sql
SELECT
    COALESCE(column_name, 'Unknown')
FROM table_name;
```

---

## Pattern 2 — Empty String Handling

```sql
SELECT
    NULLIF(TRIM(column_name), '')
FROM table_name;
```

---

## Pattern 3 — Text Standardization

```sql
SELECT
    UPPER(TRIM(column_name))
FROM table_name;
```

---

## Pattern 4 — Duplicate Detection

```sql
SELECT
    column_name,
    COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

---

## Pattern 5 — Duplicate Removal

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY id
            ORDER BY updated_at DESC
        ) AS rn
    FROM table_name
)
SELECT *
FROM ranked
WHERE rn = 1;
```

---

## Pattern 6 — Category Standardization

```sql
SELECT
    CASE
        WHEN LOWER(TRIM(category)) IN ('electronics', 'electronic')
            THEN 'Electronics'

        WHEN LOWER(TRIM(category)) IN ('clothes', 'clothing')
            THEN 'Clothing'

        ELSE 'Other'
    END AS clean_category
FROM products;
```

---

## Pattern 7 — Data Validation

```sql
SELECT *
FROM customers
WHERE age < 0
   OR age > 120
   OR email IS NULL;
```

---

## Pattern 8 — Clean + Deduplicate

```sql
WITH cleaned AS (
    SELECT
        customer_id,
        TRIM(name) AS name,
        NULLIF(LOWER(TRIM(email)), '') AS email,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY updated_at DESC
        ) AS rn
    FROM customers
)

SELECT
    customer_id,
    name,
    email
FROM cleaned
WHERE rn = 1;
```

---

# 🧠 Data Cleaning vs Data Manipulation vs Data Preprocessing

These concepts are related but **not exactly the same**.

```text
                 DATA PREPROCESSING
                       |
          -----------------------------
          |             |             |
       Cleaning     Transformation   Reduction
          |             |             |
       NULLs         Scaling        Sampling
       Duplicates    Encoding       Feature
       Errors        Formatting     Selection
          |
          ↓
   DATA MANIPULATION
          |
   --------------------
   |        |         |
 SELECT   FILTER    JOIN
   |        |         |
 GROUP BY SORT     AGGREGATE
```

### Data Cleaning

Focuses on fixing data-quality problems.

```text
NULLs
Duplicates
Invalid values
Inconsistent formatting
Incorrect categories
```

### Data Manipulation

Focuses on changing, combining, filtering, sorting, and aggregating data to obtain useful information.

```text
SELECT
WHERE
JOIN
GROUP BY
ORDER BY
CASE
WINDOW FUNCTIONS
```

### Data Preprocessing

The broader preparation stage before analysis or machine learning.

It can include:

```text
Data Cleaning
Data Transformation
Data Integration
Feature Engineering
Encoding
Scaling
Feature Selection
Data Reduction
```

Therefore:

> **Data cleaning is a part of data preprocessing, while data manipulation is a related set of operations used to transform and analyze data.**

---

# 🎯 SQL Data Cleaning Mental Model

Remember this sequence:

```text
                RAW DATA
                    ↓
                INSPECT
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
      MISSING             DUPLICATES
          ↓                   ↓
     NULL HANDLING       DEDUPLICATION
          ↓                   ↓
          └─────────┬─────────┘
                    ↓
               TEXT CLEANING
                    ↓
             STANDARDIZATION
                    ↓
              TYPE CONVERSION
                    ↓
              DATE CLEANING
                    ↓
             INVALID VALUES
                    ↓
                OUTLIERS
                    ↓
               VALIDATION
                    ↓
              CLEAN DATASET
                    ↓
             DATA ANALYSIS
```

# ⭐ Most Important Functions to Memorize

```text
IS NULL
IS NOT NULL
COALESCE()
NULLIF()
TRIM()
UPPER()
LOWER()
REPLACE()
CAST()
CASE
DISTINCT
COUNT()
ROW_NUMBER()
GROUP BY
HAVING
LEFT JOIN
CTE
```

These form the **core SQL toolkit for data cleaning and data preparation**.
