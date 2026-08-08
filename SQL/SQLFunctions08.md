# SQL Functions — Complete Guide

SQL functions are **predefined operations** that perform a specific task on data and return a result.

They are used for:

* Data transformation
* Calculations
* Text manipulation
* Date manipulation
* Statistical analysis
* Aggregation
* NULL handling
* Data cleaning
* Data preprocessing
* Reporting
* Data analytics

---

# 1. What is a SQL Function?

A function accepts one or more inputs, called **arguments**, performs an operation, and returns a value.

Basic structure:

```sql
FUNCTION_NAME(argument);
```

Example:

```sql
SELECT UPPER('python');
```

Output:

```text
PYTHON
```

Another example:

```sql
SELECT LENGTH('Python');
```

Output:

```text
6
```

---

# 2. Types of SQL Functions

SQL functions can broadly be divided into:

```text
SQL FUNCTIONS
│
├── Scalar / Single-Row Functions
│   ├── String Functions
│   ├── Numeric Functions
│   ├── Date & Time Functions
│   ├── Conversion Functions
│   ├── NULL Functions
│   └── Conditional Functions
│
├── Aggregate / Group Functions
│   ├── COUNT()
│   ├── SUM()
│   ├── AVG()
│   ├── MIN()
│   └── MAX()
│
└── Window Functions
    ├── ROW_NUMBER()
    ├── RANK()
    ├── DENSE_RANK()
    ├── LAG()
    ├── LEAD()
    └── Running / moving calculations
```

Exact function names and syntax can differ between MySQL, PostgreSQL, SQL Server, Oracle, SQLite, etc.

---

# 3. Scalar Functions

A scalar function generally operates on a value from each row and returns one result per row.

Example:

```sql
SELECT
    name,
    UPPER(name) AS uppercase_name
FROM employees;
```

If there are 5 employees, the query produces a transformed value for each employee.

Conceptually:

```text
Row 1 → Function → Result 1
Row 2 → Function → Result 2
Row 3 → Function → Result 3
...
```

Common scalar functions:

```text
String functions
Numeric functions
Date functions
Conversion functions
NULL functions
Conditional functions
```

---

# 4. Aggregate Functions

Aggregate functions process multiple rows and return a single result for a group.

Common aggregate functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Example:

```sql
SELECT AVG(salary)
FROM employees;
```

Conceptually:

```text
50000
60000
70000
80000
   ↓
  AVG()
   ↓
65000
```

---

# 5. COUNT()

`COUNT()` counts rows or non-NULL values depending on how it is used.

---

## COUNT(*)

Counts rows.

```sql
SELECT COUNT(*)
FROM employees;
```

Example output:

```text
100
```

Meaning:

```text
There are 100 rows.
```

---

# 6. COUNT(column)

Counts non-NULL values in a particular column.

```sql
SELECT COUNT(email)
FROM employees;
```

If 100 employees exist but 10 have NULL email values:

```text
COUNT(*)     → 100
COUNT(email) → 90
```

This difference is extremely important.

---

# 7. COUNT(DISTINCT)

Counts unique non-NULL values.

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

Example:

```text
IT
HR
Finance
IT
HR
```

Result:

```text
3
```

---

# 8. SUM()

Returns the total of numeric values.

```sql
SELECT SUM(salary)
FROM employees;
```

Example:

```text
50000
60000
70000
```

Result:

```text
180000
```

---

# 9. AVG()

Returns the average.

```sql
SELECT AVG(salary)
FROM employees;
```

Conceptually:

```text
(50000 + 60000 + 70000) / 3
= 60000
```

NULL values are generally ignored by aggregate functions such as `AVG()`.

---

# 10. MIN()

Returns the minimum value.

```sql
SELECT MIN(salary)
FROM employees;
```

Example:

```text
30000
```

---

# 11. MAX()

Returns the maximum value.

```sql
SELECT MAX(salary)
FROM employees;
```

Example:

```text
100000
```

---

# 12. Aggregate Function Summary

| Function  | Purpose |
| --------- | ------- |
| `COUNT()` | Count   |
| `SUM()`   | Total   |
| `AVG()`   | Average |
| `MIN()`   | Minimum |
| `MAX()`   | Maximum |

These are extremely important for data analytics.

---

# 13. Aggregate Functions with GROUP BY

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

Output:

```text
department | average_salary
-----------|---------------
IT         | 75000
HR         | 55000
Finance    | 68000
```

---

# 14. Multiple Aggregate Functions

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

This is very useful for descriptive analytics.

---

# 15. Aggregate Functions with HAVING

`HAVING` filters groups after aggregation.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 16. String Functions

String functions work with text.

Common functions include:

```text
UPPER()
LOWER()
LENGTH()
TRIM()
LTRIM()
RTRIM()
CONCAT()
SUBSTRING()
REPLACE()
LEFT()
RIGHT()
POSITION()
```

Exact availability varies by DBMS.

---

# 17. UPPER()

Converts text to uppercase.

```sql
SELECT UPPER(name)
FROM employees;
```

Example:

```text
rahul
```

becomes:

```text
RAHUL
```

Useful for:

* Standardization
* Case normalization
* Data cleaning

---

# 18. LOWER()

Converts text to lowercase.

```sql
SELECT LOWER(name)
FROM employees;
```

Example:

```text
RAHUL
```

becomes:

```text
rahul
```

---

# 19. LENGTH()

Returns the number of characters.

```sql
SELECT LENGTH('Python');
```

Result:

```text
6
```

Example:

```sql
SELECT
    name,
    LENGTH(name) AS name_length
FROM employees;
```

---

# 20. TRIM()

Removes leading and trailing whitespace.

```sql
SELECT TRIM('   Python   ');
```

Result:

```text
Python
```

Very important for data cleaning.

Example:

```sql
SELECT TRIM(name)
FROM customers;
```

---

# 21. LTRIM()

Removes whitespace from the left side.

```sql
SELECT LTRIM('   Python');
```

---

# 22. RTRIM()

Removes whitespace from the right side.

```sql
SELECT RTRIM('Python   ');
```

---

# 23. CONCAT()

Combines strings.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

Example:

```text
Rahul + " " + Kumar
```

becomes:

```text
Rahul Kumar
```

Some databases use different concatenation syntax, such as `||`.

---

# 24. String Concatenation

Example:

```sql
SELECT
    first_name || ' ' || last_name AS full_name
FROM employees;
```

This syntax is common in PostgreSQL and Oracle.

SQL Server commonly uses:

```sql
SELECT
    first_name + ' ' + last_name AS full_name
FROM employees;
```

Always check your DBMS.

---

# 25. SUBSTRING()

Extracts part of a string.

A common form is:

```sql
SUBSTRING(string, start_position, length)
```

Example:

```sql
SELECT SUBSTRING('Python', 1, 3);
```

Result:

```text
Pyt
```

Syntax differs among database systems.

---

# 26. LEFT()

Returns characters from the left.

```sql
SELECT LEFT('Python', 3);
```

Result:

```text
Pyt
```

Availability varies by DBMS.

---

# 27. RIGHT()

Returns characters from the right.

```sql
SELECT RIGHT('Python', 3);
```

Result:

```text
hon
```

---

# 28. REPLACE()

Replaces text.

```sql
SELECT REPLACE('I like Java', 'Java', 'Python');
```

Result:

```text
I like Python
```

Useful for data cleaning.

Example:

```sql
SELECT REPLACE(phone, '-', '')
FROM customers;
```

This can remove hyphens from phone-number strings.

---

# 29. Finding Text Position

Many databases provide a function such as:

```sql
POSITION('a' IN 'Data');
```

Result:

```text
2
```

Other databases use functions such as:

```sql
CHARINDEX()
INSTR()
STRPOS()
```

The exact function is DBMS-specific.

---

# 30. Numeric Functions

Numeric functions perform mathematical operations.

Common examples:

```text
ABS()
ROUND()
CEILING()/CEIL()
FLOOR()
POWER()
SQRT()
MOD()
SIGN()
```

Some function names vary by DBMS.

---

# 31. ABS()

Returns the absolute value.

```sql
SELECT ABS(-25);
```

Result:

```text
25
```

Useful for calculating absolute differences.

```sql
SELECT ABS(actual - predicted) AS absolute_error
FROM predictions;
```

---

# 32. ROUND()

Rounds a number.

```sql
SELECT ROUND(123.4567, 2);
```

Result:

```text
123.46
```

Useful for:

* Financial reports
* Percentages
* Averages
* Dashboard values

Example:

```sql
SELECT
    ROUND(AVG(salary), 2) AS average_salary
FROM employees;
```

---

# 33. CEILING()

Rounds a number upward to the nearest integer.

```sql
SELECT CEILING(10.2);
```

Result:

```text
11
```

Some databases use:

```sql
CEIL()
```

instead.

---

# 34. FLOOR()

Rounds downward.

```sql
SELECT FLOOR(10.9);
```

Result:

```text
10
```

---

# 35. POWER()

Raises a number to a power.

```sql
SELECT POWER(2, 3);
```

Result:

```text
8
```

---

# 36. SQRT()

Returns the square root.

```sql
SELECT SQRT(25);
```

Result:

```text
5
```

---

# 37. MOD()

Returns the remainder after division.

```sql
SELECT MOD(10, 3);
```

Result:

```text
1
```

Some systems use the `%` operator instead.

Example:

```sql
SELECT *
FROM employees
WHERE employee_id % 2 = 0;
```

This can identify even IDs in systems supporting `%`.

---

# 38. Date and Time Functions

Date/time functions are extremely important in data analytics.

Common concepts:

```text
CURRENT_DATE
CURRENT_TIME
CURRENT_TIMESTAMP
EXTRACT()
DATE_PART()
DATEADD()
DATEDIFF()
DATE_TRUNC()
```

Exact syntax is DBMS-specific.

---

# 39. CURRENT_DATE

Returns the current date.

```sql
SELECT CURRENT_DATE;
```

Example:

```text
2026-08-08
```

The actual result depends on the database/session date.

---

# 40. CURRENT_TIMESTAMP

Returns the current date and time.

```sql
SELECT CURRENT_TIMESTAMP;
```

---

# 41. Extracting Date Components

You may want:

```text
Year
Month
Day
Hour
Minute
Second
```

A standard-style approach is:

```sql
SELECT EXTRACT(YEAR FROM order_date)
FROM orders;
```

Month:

```sql
SELECT EXTRACT(MONTH FROM order_date)
FROM orders;
```

Day:

```sql
SELECT EXTRACT(DAY FROM order_date)
FROM orders;
```

---

# 42. Extracting Year for Analytics

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    SUM(amount) AS total_sales
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date);
```

This gives yearly sales.

---

# 43. Extracting Month

```sql
SELECT
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(amount) AS total_sales
FROM orders
GROUP BY EXTRACT(MONTH FROM order_date)
ORDER BY month;
```

---

# 44. Date Difference

Different DBMSs provide different functions for calculating the difference between dates.

For example, SQL Server:

```sql
SELECT DATEDIFF(day, start_date, end_date)
FROM projects;
```

Some other databases use different approaches.

Concept:

```text
end date - start date
        ↓
number of days
```

---

# 45. Date Addition

Different DBMSs use different functions.

For example, SQL Server:

```sql
SELECT DATEADD(day, 7, order_date)
FROM orders;
```

Meaning:

```text
order_date + 7 days
```

PostgreSQL can use interval arithmetic:

```sql
SELECT order_date + INTERVAL '7 days'
FROM orders;
```

---

# 46. Date Truncation

`DATE_TRUNC()` is commonly used in PostgreSQL and some other systems.

Example:

```sql
SELECT DATE_TRUNC('month', order_date)
FROM orders;
```

This can convert dates to the beginning of their month for grouping.

Example:

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount) AS total_sales
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;
```

This is extremely useful for time-series analysis.

---

# 47. NULL Functions

NULL represents missing/unknown data.

Important functions:

```text
COALESCE()
NULLIF()
IFNULL()
ISNULL()
```

Not all are portable across DBMSs.

---

# 48. COALESCE()

`COALESCE()` returns the first non-NULL value.

```sql
SELECT COALESCE(phone, 'Not Available')
FROM customers;
```

If:

```text
phone = NULL
```

result:

```text
Not Available
```

If:

```text
phone = '9876543210'
```

result:

```text
9876543210
```

---

# 49. COALESCE() with Multiple Values

```sql
SELECT
    COALESCE(
        mobile,
        home_phone,
        office_phone,
        'No phone'
    ) AS contact_number
FROM customers;
```

SQL checks from left to right.

```text
mobile
  ↓
if NULL
  ↓
home_phone
  ↓
if NULL
  ↓
office_phone
  ↓
if NULL
  ↓
'No phone'
```

---

# 50. IFNULL()

Common in MySQL and some other systems.

```sql
SELECT IFNULL(phone, 'Not Available')
FROM customers;
```

It generally accepts two arguments:

```text
IFNULL(value, replacement)
```

---

# 51. ISNULL()

SQL Server provides:

```sql
SELECT ISNULL(phone, 'Not Available')
FROM customers;
```

Important:

```text
ISNULL()
```

has DBMS-specific behavior and should not be confused with:

```sql
IS NULL
```

which is a SQL predicate.

---

# 52. NULLIF()

Returns NULL if two expressions are equal.

```sql
SELECT NULLIF(10, 10);
```

Result:

```text
NULL
```

If they are different:

```sql
SELECT NULLIF(10, 20);
```

Result:

```text
10
```

---

# 53. Preventing Division by Zero

`NULLIF()` is useful in analytics.

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS revenue_per_unit
FROM sales;
```

If quantity is zero:

```text
NULLIF(quantity, 0)
        ↓
NULL
        ↓
revenue / NULL
        ↓
NULL
```

This can prevent a division-by-zero error in systems where that error would otherwise occur.

---

# 54. Conditional Functions

Conditional logic can be implemented using:

```text
CASE
COALESCE()
NULLIF()
```

The most important is:

```text
CASE
```

---

# 55. CASE Expression

`CASE` works like conditional logic.

Basic structure:

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 56. CASE with Multiple Conditions

```sql
SELECT
    product,
    sales,
    CASE
        WHEN sales >= 100000 THEN 'Excellent'
        WHEN sales >= 50000 THEN 'Good'
        WHEN sales >= 10000 THEN 'Average'
        ELSE 'Poor'
    END AS performance
FROM products;
```

This is heavily used in analytics.

---

# 57. Simple CASE

You can compare one expression against several values.

```sql
SELECT
    name,
    CASE department
        WHEN 'IT' THEN 'Technology'
        WHEN 'HR' THEN 'Human Resources'
        WHEN 'Finance' THEN 'Financial Team'
        ELSE 'Other'
    END AS department_group
FROM employees;
```

---

# 58. Searched CASE vs Simple CASE

### Searched CASE

Uses conditions:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
END
```

### Simple CASE

Compares one expression:

```sql
CASE department
    WHEN 'IT' THEN 'Technology'
    WHEN 'HR' THEN 'Human Resources'
END
```

---

# 59. Conversion Functions

Conversion functions change one data type into another.

Common concepts/functions:

```text
CAST()
CONVERT()
```

Exact support varies by DBMS.

---

# 60. CAST()

Converts a value to another data type.

Example:

```sql
SELECT CAST('123' AS INTEGER);
```

Result:

```text
123
```

Another example:

```sql
SELECT CAST(123.456 AS INTEGER);
```

The exact resulting value can depend on the DBMS's casting rules.

---

# 61. CAST in Analytics

Suppose a column contains numeric data stored as text:

```text
'100'
'200'
'300'
```

You may need:

```sql
SELECT
    CAST(amount AS DECIMAL(10,2))
FROM sales;
```

This is common in data cleaning and preprocessing.

---

# 62. CONVERT()

SQL Server commonly uses:

```sql
SELECT CONVERT(INT, '123');
```

It can also be used for date/time formatting/conversion.

Example:

```sql
SELECT CONVERT(DATE, order_timestamp)
FROM orders;
```

Exact behavior and style codes are SQL Server-specific.

---

# 63. Mathematical Analytics Example

Calculate profit:

```sql
SELECT
    product,
    revenue,
    cost,
    revenue - cost AS profit
FROM sales;
```

Round profit:

```sql
SELECT
    product,
    ROUND(revenue - cost, 2) AS profit
FROM sales;
```

---

# 64. Percentage Calculation

Example:

```sql
SELECT
    product,
    sales,
    total_sales,
    ROUND(
        sales * 100.0 / NULLIF(total_sales, 0),
        2
    ) AS sales_percentage
FROM sales_summary;
```

Important:

```text
100.0
```

is often used to encourage decimal arithmetic rather than unintended integer division, depending on the DBMS and data types.

---

# 65. Aggregate + CASE

Functions can be combined with conditional logic.

Example:

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(
        CASE
            WHEN salary >= 50000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees;
```

This is a powerful analytics pattern.

---

# 66. Conditional Aggregation

Example:

```sql
SELECT
    department,
    SUM(
        CASE
            WHEN salary >= 50000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count
FROM employees
GROUP BY department;
```

This allows you to calculate multiple business metrics in one query.

---

# 67. COUNT with CASE

```sql
SELECT
    COUNT(
        CASE
            WHEN salary >= 50000 THEN 1
        END
    ) AS high_salary_count
FROM employees;
```

Because `COUNT(expression)` ignores NULL, only rows satisfying the condition are counted.

---

# 68. SUM with CASE

A commonly used pattern:

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed' THEN 1
            ELSE 0
        END
    ) AS completed_orders
FROM orders;
```

---

# 69. Multiple Metrics

```sql
SELECT
    COUNT(*) AS total_orders,

    SUM(
        CASE
            WHEN status = 'Completed' THEN 1
            ELSE 0
        END
    ) AS completed_orders,

    SUM(
        CASE
            WHEN status = 'Cancelled' THEN 1
            ELSE 0
        END
    ) AS cancelled_orders
FROM orders;
```

This is very useful for dashboards.

---

# 70. Window Functions

Window functions perform calculations across related rows **without collapsing those rows into one row per group**.

This is one of the most important SQL topics for data analytics.

Common window functions:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
FIRST_VALUE()
LAST_VALUE()
SUM() OVER()
AVG() OVER()
COUNT() OVER()
```

---

# 71. Window Function Syntax

General structure:

```sql
FUNCTION() OVER (
    PARTITION BY column
    ORDER BY column
)
```

Example:

```sql
SELECT
    name,
    department,
    salary,
    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 72. Window Functions vs GROUP BY

### GROUP BY

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Returns one row per department.

### Window function

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Keeps every employee row while adding the department average.

This difference is extremely important.

---

# 73. ROW_NUMBER()

Assigns a unique sequential number.

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

Example:

```text
name   salary   row_num
-----  -------  -------
A      90000    1
B      80000    2
C      80000    3
D      70000    4
```

Even tied salaries receive different row numbers.

---

# 74. RANK()

Assigns the same rank to ties.

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Example:

```text
salary   rank
-------  ----
90000    1
80000    2
80000    2
70000    4
```

Notice the gap after the tie.

---

# 75. DENSE_RANK()

Also assigns the same rank to ties, but does not leave gaps.

```sql
SELECT
    name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Example:

```text
salary   rank
-------  ----
90000    1
80000    2
80000    2
70000    3
```

---

# 76. ROW_NUMBER vs RANK vs DENSE_RANK

| Function       | Ties              | Gaps |
| -------------- | ----------------- | ---- |
| `ROW_NUMBER()` | Different numbers | No   |
| `RANK()`       | Same rank         | Yes  |
| `DENSE_RANK()` | Same rank         | No   |

Remember:

```text
ROW_NUMBER → unique position
RANK       → competition ranking
DENSE_RANK → ranking without gaps
```

---

# 77. PARTITION BY

`PARTITION BY` divides rows into groups for a window function.

Example:

```sql
SELECT
    name,
    department,
    salary,
    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS department_rank
FROM employees;
```

This ranks employees separately inside each department.

---

# 78. LAG()

Returns a value from a previous row.

Example:

```sql
SELECT
    order_date,
    sales,
    LAG(sales) OVER (
        ORDER BY order_date
    ) AS previous_sales
FROM daily_sales;
```

Useful for:

* Month-over-month analysis
* Day-over-day analysis
* Previous transaction comparison
* Growth calculations

---

# 79. LEAD()

Returns a value from a following row.

```sql
SELECT
    order_date,
    sales,
    LEAD(sales) OVER (
        ORDER BY order_date
    ) AS next_sales
FROM daily_sales;
```

---

# 80. Growth Calculation with LAG()

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales
FROM monthly_sales;
```

Then:

```sql
SELECT
    month,
    sales,
    previous_month_sales,
    ROUND(
        (sales - previous_month_sales)
        * 100.0
        / NULLIF(previous_month_sales, 0),
        2
    ) AS growth_percentage
FROM monthly_sales_with_previous;
```

A subquery/CTE is commonly used because a window-function alias generally cannot be reused directly in the same `SELECT` list.

---

# 81. Running Total

`SUM()` can also be used as a window function.

```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
    ) AS running_total
FROM daily_sales;
```

Example:

```text
date   sales   running_total
-----  -----   -------------
Jan 1  100     100
Jan 2  200     300
Jan 3  150     450
Jan 4  250     700
```

---

# 82. Running Average

```sql
SELECT
    order_date,
    sales,
    AVG(sales) OVER (
        ORDER BY order_date
    ) AS running_average
FROM daily_sales;
```

---

# 83. Windowed COUNT()

```sql
SELECT
    name,
    department,
    COUNT(*) OVER (
        PARTITION BY department
    ) AS department_employee_count
FROM employees;
```

Every employee row shows the number of employees in their department.

---

# 84. Windowed SUM()

```sql
SELECT
    department,
    name,
    salary,
    SUM(salary) OVER (
        PARTITION BY department
    ) AS department_total_salary
FROM employees;
```

---

# 85. Windowed AVG()

```sql
SELECT
    department,
    name,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_average_salary
FROM employees;
```

---

# 86. FIRST_VALUE()

Returns the first value in a window according to its ordering.

Example:

```sql
SELECT
    name,
    department,
    salary,
    FIRST_VALUE(name) OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS highest_paid_employee
FROM employees;
```

This can identify the first/highest-paid employee according to the specified window ordering.

---

# 87. LAST_VALUE()

Returns the last value according to the window frame.

Example:

```sql
SELECT
    name,
    department,
    salary,
    LAST_VALUE(name) OVER (
        PARTITION BY department
        ORDER BY salary
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS last_employee
FROM employees;
```

`LAST_VALUE()` is more subtle than `FIRST_VALUE()` because the window frame matters.

---

# 88. Window Frame

A window can have a frame specifying which rows are considered.

Common concepts:

```text
UNBOUNDED PRECEDING
CURRENT ROW
UNBOUNDED FOLLOWING
```

Example:

```sql
SUM(sales) OVER (
    ORDER BY order_date
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND CURRENT ROW
)
```

This calculates a running total.

---

# 89. Moving Average

Example:

```sql
SELECT
    order_date,
    sales,
    AVG(sales) OVER (
        ORDER BY order_date
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS three_day_average
FROM daily_sales;
```

This calculates a 3-row moving average.

---

# 90. SQL Functions in Data Analytics

Functions are fundamental to the analytics workflow.

```text
Raw Data
   ↓
Cleaning
   ↓
Transformation
   ↓
Aggregation
   ↓
Analysis
   ↓
Reporting
```

Functions support every stage.

---

# 91. Functions for Data Cleaning

Common examples:

```sql
SELECT
    TRIM(name),
    LOWER(email),
    REPLACE(phone, '-', ''),
    COALESCE(city, 'Unknown')
FROM customers;
```

Here:

```text
TRIM()       → removes unnecessary spaces
LOWER()      → standardizes case
REPLACE()    → cleans text
COALESCE()   → handles missing values
```

---

# 92. Functions for Data Transformation

Example:

```sql
SELECT
    salary,
    salary * 12 AS annual_salary,
    ROUND(salary * 12, 2) AS rounded_annual_salary
FROM employees;
```

---

# 93. Functions for Feature Creation

Analytics and machine-learning workflows often create derived columns.

Example:

```sql
SELECT
    age,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age < 30 THEN 'Young Adult'
        WHEN age < 60 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM customers;
```

This creates a new categorical feature.

---

# 94. Functions for Time-Series Analysis

Example:

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount) AS monthly_sales
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;
```

This converts transaction-level data into monthly sales data.

---

# 95. Functions for Customer Analytics

Example:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count,
    SUM(amount) AS total_spending,
    AVG(amount) AS average_order_value,
    MAX(order_date) AS latest_order
FROM orders
GROUP BY customer_id;
```

This produces customer-level metrics.

---

# 96. Functions for Sales Analytics

```sql
SELECT
    product_id,
    COUNT(*) AS number_of_orders,
    SUM(quantity) AS units_sold,
    SUM(quantity * price) AS revenue,
    AVG(price) AS average_price,
    MIN(price) AS minimum_price,
    MAX(price) AS maximum_price
FROM sales
GROUP BY product_id;
```

---

# 97. Combining Multiple Functions

Real SQL queries commonly combine functions.

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    ROUND(AVG(salary), 2) AS avg_salary,
    MAX(salary) AS highest_salary,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC;
```

Here we use:

```text
COUNT()
AVG()
ROUND()
MAX()
MIN()
HAVING
ORDER BY
```

---

# 98. Function Nesting

Functions can be placed inside other functions.

Example:

```sql
SELECT
    ROUND(AVG(salary), 2)
FROM employees;
```

Execution conceptually:

```text
salary values
     ↓
   AVG()
     ↓
average
     ↓
 ROUND()
     ↓
rounded average
```

Another example:

```sql
SELECT
    COALESCE(ROUND(AVG(salary), 2), 0)
FROM employees;
```

Conceptually:

```text
AVG()
 ↓
ROUND()
 ↓
COALESCE()
```

---

# 99. Function Categories — Quick Reference

## Aggregate

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

## String

```text
UPPER()
LOWER()
LENGTH()
TRIM()
LTRIM()
RTRIM()
CONCAT()
SUBSTRING()
REPLACE()
LEFT()
RIGHT()
```

## Numeric

```text
ABS()
ROUND()
CEILING()
FLOOR()
POWER()
SQRT()
MOD()
```

## Date/Time

```text
CURRENT_DATE
CURRENT_TIME
CURRENT_TIMESTAMP
EXTRACT()
DATE_TRUNC()
DATEDIFF()
DATEADD()
```

## NULL

```text
COALESCE()
NULLIF()
IFNULL()
ISNULL()
```

## Conversion

```text
CAST()
CONVERT()
```

## Conditional

```text
CASE
```

## Window

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
FIRST_VALUE()
LAST_VALUE()
SUM() OVER()
AVG() OVER()
COUNT() OVER()
```

---

# 100. Scalar vs Aggregate vs Window Functions

| Type      | Operates on                        | Result               |
| --------- | ---------------------------------- | -------------------- |
| Scalar    | Individual row/value               | One result per row   |
| Aggregate | Multiple rows                      | One result per group |
| Window    | Related rows while preserving rows | One result per row   |

Example:

```sql
-- Scalar
SELECT UPPER(name)
FROM employees;
```

```sql
-- Aggregate
SELECT AVG(salary)
FROM employees;
```

```sql
-- Window
SELECT
    name,
    AVG(salary) OVER (PARTITION BY department)
FROM employees;
```

---

# 101. Important Difference: Aggregate vs Window

### Aggregate

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Output:

```text
IT       70000
HR       55000
Finance  65000
```

One row per department.

### Window

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Output conceptually:

```text
Name    Department   Salary   Department Avg
------  -----------  -------  --------------
A       IT           70000    75000
B       IT           80000    75000
C       HR           50000    55000
D       HR           60000    55000
```

The individual rows remain.

---

# 102. Important Difference: COUNT(*) vs COUNT(column)

```text
COUNT(*)
    ↓
Counts rows

COUNT(column)
    ↓
Counts non-NULL values

COUNT(DISTINCT column)
    ↓
Counts unique non-NULL values
```

This is one of the most important SQL interview concepts.

---

# 103. Important Difference: WHERE vs HAVING with Functions

`WHERE` filters rows before aggregation.

```sql
SELECT
    department,
    AVG(salary)
FROM employees
WHERE salary > 30000
GROUP BY department;
```

`HAVING` filters groups after aggregation.

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Remember:

```text
WHERE  → filter rows
HAVING → filter groups
```

---

# 104. Important Function Execution Concept

Consider:

```sql
SELECT
    department,
    ROUND(AVG(salary), 2) AS avg_salary
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC;
```

Conceptually:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
Aggregate function AVG()
 ↓
HAVING
 ↓
SELECT / ROUND()
 ↓
ORDER BY
```

Actual optimizer behavior can differ, but this is a useful conceptual model for learning SQL.

---

# 105. Most Important Functions for Data Analytics

If your goal is **SQL + Data Analytics**, prioritize these:

### Level 1 — Must Know

```text
COUNT()
SUM()
AVG()
MIN()
MAX()

UPPER()
LOWER()
TRIM()
LENGTH()
REPLACE()

ROUND()
ABS()

COALESCE()
NULLIF()

CAST()

CASE
```

### Level 2 — Very Important

```text
EXTRACT()
DATE_TRUNC()
DATEDIFF()
DATEADD()

COUNT(DISTINCT)

CONCAT()
SUBSTRING()

ROW_NUMBER()
RANK()
DENSE_RANK()
```

### Level 3 — Advanced Analytics

```text
LAG()
LEAD()
FIRST_VALUE()
LAST_VALUE()

SUM() OVER()
AVG() OVER()
COUNT() OVER()

Window frames
Running totals
Moving averages
Top-N per group
Period-over-period analysis
```

---

# 106. Practical Analytics Example

Suppose you have:

```text
orders
------
order_id
customer_id
order_date
amount
status
```

You can calculate:

```sql
SELECT
    customer_id,
    COUNT(*) AS total_orders,
    SUM(amount) AS total_spending,
    ROUND(AVG(amount), 2) AS average_order_value,
    MIN(order_date) AS first_order,
    MAX(order_date) AS latest_order
FROM orders
WHERE status = 'Completed'
GROUP BY customer_id;
```

This single query uses:

```text
COUNT()
SUM()
AVG()
ROUND()
MIN()
MAX()
WHERE
GROUP BY
```

This is exactly the type of SQL used in real data analytics.

---

# 107. Complete SQL Functions Mental Map

```text
                         SQL FUNCTIONS
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
       SCALAR             AGGREGATE            WINDOW
          │                   │                   │
    ┌─────┼─────┐       ┌─────┼─────┐       ┌────┼─────┐
    │     │     │       │     │     │       │    │     │
 Strings Numeric Dates COUNT SUM AVG       Rank Lag   Lead
    │     │     │       MIN  MAX           │
    │     │     │                       Running Total
    │     │     │                       Moving Avg
    │     │     │
    │     │     └── Date/Time
    │     │
    │     └──────── Numeric
    │
    └────────────── String

          Other Important Categories
                    │
          ┌─────────┼─────────┐
          │         │         │
       NULL      CASE      Conversion
          │         │         │
     COALESCE()   CASE()     CAST()
     NULLIF()                CONVERT()
```

---

# 108. Final Revision Cheat Sheet

```text
COUNT(*)             → Count rows
COUNT(column)        → Count non-NULL values
COUNT(DISTINCT col)  → Count unique values

SUM()                → Total
AVG()                → Average
MIN()                → Minimum
MAX()                → Maximum

UPPER()              → Uppercase
LOWER()              → Lowercase
LENGTH()             → String length
TRIM()               → Remove surrounding spaces
CONCAT()             → Join strings
SUBSTRING()          → Extract part of string
REPLACE()            → Replace text

ABS()                → Absolute value
ROUND()              → Round number
CEILING()            → Round upward
FLOOR()              → Round downward
POWER()              → Power
SQRT()               → Square root
MOD()                → Remainder

CURRENT_DATE         → Current date
CURRENT_TIMESTAMP    → Current date/time
EXTRACT()            → Extract date component
DATE_TRUNC()         → Truncate date to period
DATEDIFF()           → Date difference
DATEADD()            → Add date interval

COALESCE()           → First non-NULL value
NULLIF()             → NULL when values are equal
IFNULL()             → Replace NULL (DBMS-specific)
ISNULL()             → Replace/check NULL (DBMS-specific)

CAST()               → Convert data type
CONVERT()            → Convert data type (DBMS-specific)

CASE                 → Conditional logic

ROW_NUMBER()         → Unique row numbering
RANK()               → Ranking with gaps
DENSE_RANK()         → Ranking without gaps
LAG()                → Previous row
LEAD()               → Next row

SUM() OVER()         → Windowed/running sum
AVG() OVER()         → Windowed average
COUNT() OVER()       → Windowed count
```

---

# 109. Essential SQL Function Patterns to Memorize

### Average rounded to 2 decimals

```sql
SELECT ROUND(AVG(salary), 2)
FROM employees;
```

### Count unique customers

```sql
SELECT COUNT(DISTINCT customer_id)
FROM orders;
```

### Replace NULL

```sql
SELECT COALESCE(phone, 'Unknown')
FROM customers;
```

### Categorize values

```sql
SELECT
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

### Clean text

```sql
SELECT
    LOWER(TRIM(email)) AS cleaned_email
FROM customers;
```

### Convert data type

```sql
SELECT CAST(amount AS DECIMAL(10,2))
FROM sales;
```

### Rank within groups

```sql
SELECT
    name,
    department,
    salary,
    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS department_rank
FROM employees;
```

### Previous value

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales
FROM monthly_sales;
```

### Running total

```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
    ) AS running_sales
FROM daily_sales;
```

---

# 110. Final Takeaway

For **SQL coding**, understand:

```text
Function syntax
Arguments
Return values
Scalar functions
Aggregate functions
CASE
NULL handling
Type conversion
Date manipulation
Window functions
```

For **Data Analytics**, especially master:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()

COUNT(DISTINCT)

CASE

COALESCE()
NULLIF()

ROUND()

DATE functions

GROUP BY + aggregate functions

Conditional aggregation

ROW_NUMBER()
RANK()
DENSE_RANK()

LAG()
LEAD()

SUM() OVER()
AVG() OVER()

Running totals
Moving averages
Period-over-period comparison
Top-N per group
```

The most important idea is:

```text
SQL Functions
     ↓
Transform Data
     ↓
Clean Data
     ↓
Calculate Metrics
     ↓
Aggregate Data
     ↓
Compare Rows
     ↓
Analyze Trends
     ↓
Generate Business Insights
```
