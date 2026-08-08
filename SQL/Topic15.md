# SQL — CTEs, Window Functions, Advanced Window Functions & NULL Handling

This README covers four major SQL topics:

1. **Common Table Expressions (CTEs)**
2. **Window Functions**
3. **Advanced Window Functions**
4. **NULL Handling**

These concepts are extremely important for:

* Data Analytics
* Data Science
* Business Intelligence
* Reporting
* SQL Interviews
* Data Engineering
* Advanced SQL Querying

---

# Table of Contents

* [1. Common Table Expressions — CTE](#1-common-table-expressions--cte)

  * [What is a CTE](#what-is-a-cte)
  * [Why Use CTEs](#why-use-ctes)
  * [Basic Syntax](#basic-syntax)
  * [Simple CTE](#simple-cte)
  * [Multiple CTEs](#multiple-ctes)
  * [CTE Referencing Another CTE](#cte-referencing-another-cte)
  * [CTE with JOIN](#cte-with-join)
  * [CTE with GROUP BY](#cte-with-group-by)
  * [CTE with Window Functions](#cte-with-window-functions)
  * [Recursive CTE](#recursive-cte)
  * [CTE vs Subquery](#cte-vs-subquery)
  * [CTE vs Temporary Table](#cte-vs-temporary-table)
  * [CTE Best Practices](#cte-best-practices)

* [2. Window Functions](#2-window-functions)

  * [What is a Window Function](#what-is-a-window-function)
  * [Aggregate vs Window Function](#aggregate-vs-window-function)
  * [Basic Syntax](#basic-syntax-1)
  * [OVER](#over)
  * [PARTITION BY](#partition-by)
  * [ORDER BY](#order-by)
  * [Window Without PARTITION BY](#window-without-partition-by)
  * [Aggregate Window Functions](#aggregate-window-functions)
  * [Ranking Functions](#ranking-functions)
  * [ROW_NUMBER](#row_number)
  * [RANK](#rank)
  * [DENSE_RANK](#dense_rank)
  * [NTILE](#ntile)

* [3. Advanced Window Functions](#3-advanced-window-functions)

  * [Running Total](#running-total)
  * [Running Average](#running-average)
  * [Moving Average](#moving-average)
  * [LAG](#lag)
  * [LEAD](#lead)
  * [FIRST_VALUE](#first_value)
  * [LAST_VALUE](#last_value)
  * [NTH_VALUE](#nth_value)
  * [Percentage of Total](#percentage-of-total)
  * [Difference from Previous Row](#difference-from-previous-row)
  * [Growth Rate](#growth-rate)
  * [Cumulative Maximum](#cumulative-maximum)
  * [Window Frames](#window-frames)
  * [ROWS vs RANGE](#rows-vs-range)
  * [Top N Per Group](#top-n-per-group)
  * [Deduplication](#deduplication)

* [4. NULL Handling](#4-null-handling)

  * [What is NULL](#what-is-null)
  * [NULL vs Zero](#null-vs-zero)
  * [NULL vs Empty String](#null-vs-empty-string)
  * [Three-Valued Logic](#three-valued-logic)
  * [IS NULL](#is-null)
  * [IS NOT NULL](#is-not-null)
  * [COALESCE](#coalesce)
  * [NULLIF](#nullif)
  * [CASE with NULL](#case-with-null)
  * [NULL in Calculations](#null-in-calculations)
  * [NULL in Aggregations](#null-in-aggregations)
  * [NULL in GROUP BY](#null-in-group-by)
  * [NULL in ORDER BY](#null-in-order-by)
  * [NULL in JOINs](#null-in-joins)
  * [NULL with IN](#null-with-in)
  * [NULL with NOT IN](#null-with-not-in)
  * [NULL with EXISTS](#null-with-exists)
  * [NULL in Window Functions](#null-in-window-functions)
  * [NULL-safe Comparisons](#null-safe-comparisons)

* [5. CTE + Window Function Patterns](#5-cte--window-function-patterns)

* [6. Data Analytics Examples](#6-data-analytics-examples)

* [7. Common Mistakes](#7-common-mistakes)

* [8. Interview Questions](#8-interview-questions)

* [9. Quick Revision Cheat Sheet](#9-quick-revision-cheat-sheet)

---

# 1. Common Table Expressions — CTE

## What is a CTE?

CTE stands for:

```text
Common Table Expression
```

A CTE is a temporary named result set defined using the `WITH` clause.

It exists for the duration of a single SQL statement.

Basic idea:

```text
WITH
   ↓
Create temporary named query
   ↓
Use it in the main query
```

---

# Why Use CTEs?

CTEs are useful for:

* Making complex queries easier to read
* Breaking a large query into logical steps
* Reusing an intermediate result within a statement
* Combining multiple transformations
* Working with window functions
* Recursive queries
* Replacing deeply nested subqueries
* Improving query organization

---

# Basic Syntax

```sql
WITH cte_name AS (
    SELECT
        column1,
        column2
    FROM table_name
)
SELECT *
FROM cte_name;
```

---

# Simple CTE

Suppose we want employees with salary above 60,000.

```sql
WITH high_salary AS (
    SELECT
        employee_id,
        employee_name,
        salary
    FROM employees
    WHERE salary > 60000
)

SELECT *
FROM high_salary;
```

The CTE is:

```text
high_salary
```

The main query reads from it like a table.

---

# CTE Structure

```text
WITH
    ↓
cte_name
    ↓
AS
    ↓
(
    SELECT ...
)
    ↓
Main Query
```

Example:

```sql
WITH employee_data AS (
    SELECT *
    FROM employees
)
SELECT *
FROM employee_data;
```

---

# CTE Does Not Permanently Create a Table

Important:

```sql
WITH employee_data AS (...)
SELECT *
FROM employee_data;
```

does **not** permanently create:

```text
employee_data
```

as a database table.

The CTE exists for that SQL statement.

---

# Multiple CTEs

You can define multiple CTEs.

```sql
WITH employees_data AS (
    SELECT *
    FROM employees
),

departments_data AS (
    SELECT *
    FROM departments
)

SELECT
    e.employee_name,
    d.department_name
FROM employees_data e
JOIN departments_data d
    ON e.department_id = d.department_id;
```

---

# CTE Referencing Another CTE

A later CTE can use an earlier CTE.

```sql
WITH employee_data AS (
    SELECT
        employee_id,
        department_id,
        salary
    FROM employees
),

department_salary AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employee_data
    GROUP BY department_id
)

SELECT *
FROM department_salary;
```

Flow:

```text
employees
    ↓
employee_data
    ↓
department_salary
    ↓
final query
```

---

# CTE with WHERE

```sql
WITH active_customers AS (
    SELECT
        customer_id,
        customer_name
    FROM customers
    WHERE status = 'Active'
)

SELECT *
FROM active_customers;
```

---

# CTE with GROUP BY

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)

SELECT *
FROM customer_sales;
```

---

# CTE with HAVING

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
    HAVING SUM(amount) > 10000
)

SELECT *
FROM customer_sales;
```

---

# CTE with JOIN

```sql
WITH order_data AS (
    SELECT
        o.order_id,
        o.customer_id,
        c.customer_name,
        o.amount
    FROM orders o
    JOIN customers c
        ON o.customer_id = c.customer_id
)

SELECT *
FROM order_data;
```

---

# CTE with CASE

```sql
WITH employee_categories AS (
    SELECT
        employee_id,
        employee_name,
        salary,
        CASE
            WHEN salary >= 100000 THEN 'High'
            WHEN salary >= 50000 THEN 'Medium'
            ELSE 'Low'
        END AS salary_category
    FROM employees
)

SELECT *
FROM employee_categories;
```

---

# CTE with Window Functions

CTEs and window functions are frequently used together.

Example:

```sql
WITH ranked_employees AS (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)

SELECT *
FROM ranked_employees
WHERE salary_rank <= 3;
```

This finds the top 3 salary ranks per department.

---

# Why Use a CTE with a Window Function?

Window functions are commonly calculated in a query layer and then filtered in an outer query.

For example:

```sql
WITH ranked_data AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS rn
    FROM orders
)

SELECT *
FROM ranked_data
WHERE rn = 1;
```

This finds the latest order for each customer.

---

# Recursive CTE

A recursive CTE refers to itself.

It is useful for hierarchical data such as:

```text
Employee
   ↓
Manager
   ↓
Director
```

or:

```text
Category
   ↓
Subcategory
   ↓
Product
```

Generic structure:

```sql
WITH RECURSIVE hierarchy AS (

    -- Anchor query
    SELECT
        employee_id,
        employee_name,
        manager_id,
        1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive query
    SELECT
        e.employee_id,
        e.employee_name,
        e.manager_id,
        h.level + 1
    FROM employees e
    JOIN hierarchy h
        ON e.manager_id = h.employee_id
)

SELECT *
FROM hierarchy;
```

Syntax differs slightly across database systems.

---

# Recursive CTE Components

A recursive CTE generally contains:

```text
1. Anchor member
2. UNION ALL
3. Recursive member
```

Conceptually:

```text
Anchor
  ↓
Level 1
  ↓
Recursive query
  ↓
Level 2
  ↓
Recursive query
  ↓
Level 3
  ↓
...
```

---

# CTE vs Subquery

### Subquery

```sql
SELECT *
FROM (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) x;
```

### CTE

```sql
WITH department_salary AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)

SELECT *
FROM department_salary;
```

CTE is often easier to read when the query has multiple logical steps.

---

# CTE vs Subquery

| CTE                         | Subquery                            |
| --------------------------- | ----------------------------------- |
| Named                       | Usually unnamed                     |
| Defined with `WITH`         | Defined inline                      |
| Easier for multi-step logic | Convenient for small logic          |
| Can define multiple CTEs    | Can nest subqueries                 |
| Can be recursive            | Normal subqueries are not recursive |
| Improves readability        | Can become deeply nested            |

---

# CTE vs Temporary Table

A CTE:

```text
Exists for one SQL statement
```

A temporary table:

```text
Can exist for a session/transaction depending on database
```

CTE:

```sql
WITH x AS (...)
SELECT ...
```

Temporary table:

```sql
CREATE TEMPORARY TABLE x AS
SELECT ...;
```

Use temporary tables when you need to persist intermediate data across multiple statements or when database-specific performance/workflow considerations make that appropriate.

---

# CTE Best Practices

Use CTEs to:

```text
✓ Break complex queries into steps
✓ Give meaningful names
✓ Separate transformations
✓ Improve readability
✓ Simplify debugging
✓ Combine with window functions
```

Avoid:

```text
✗ Creating unnecessary CTEs
✗ Making every tiny SELECT a CTE
✗ Assuming CTE automatically improves performance
```

Important:

> A CTE is primarily a query-organization tool. It does not automatically materialize data or guarantee better performance.

---

# 2. Window Functions

# What is a Window Function?

A window function performs a calculation across a set of related rows **without collapsing those rows into one row**.

This is the most important difference between:

```text
GROUP BY
```

and:

```text
Window Function
```

---

# GROUP BY vs Window Function

Suppose:

| employee | department | salary |
| -------- | ---------- | -----: |
| Rahul    | IT         |  50000 |
| Priya    | IT         |  70000 |
| Amit     | HR         |  60000 |
| Neha     | HR         |  80000 |

Using `GROUP BY`:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Result:

| department | avg_salary |
| ---------- | ---------: |
| IT         |      60000 |
| HR         |      70000 |

Rows are collapsed.

---

Using a window function:

```sql
SELECT
    employee,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Result:

| employee | department | salary | department_avg |
| -------- | ---------- | -----: | -------------: |
| Rahul    | IT         |  50000 |          60000 |
| Priya    | IT         |  70000 |          60000 |
| Amit     | HR         |  60000 |          70000 |
| Neha     | HR         |  80000 |          70000 |

The original rows remain.

---

# Key Difference

```text
GROUP BY
→ Multiple rows become one row per group.

WINDOW FUNCTION
→ Rows remain individual rows while calculations are performed across related rows.
```

---

# Basic Syntax

```sql
function_name(...)
OVER (
    PARTITION BY ...
    ORDER BY ...
    ROWS/RANGE ...
)
```

Example:

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

---

# OVER

`OVER` defines the window over which the function operates.

Example:

```sql
SUM(amount) OVER ()
```

means:

> Calculate the sum over the entire result set.

---

# PARTITION BY

`PARTITION BY` divides rows into independent groups for the window calculation.

Example:

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

Conceptually:

```text
All employees
     ↓
Partition by department
     ↓
IT group
HR group
Sales group
Finance group
```

Each department gets its own calculation.

---

# ORDER BY in Window Functions

`ORDER BY` determines the logical ordering within the window.

Example:

```sql
SUM(amount) OVER (
    ORDER BY order_date
)
```

This can create a running total.

---

# PARTITION BY + ORDER BY

```sql
SUM(amount) OVER (
    PARTITION BY customer_id
    ORDER BY order_date
)
```

Meaning:

> Calculate a cumulative sum separately for each customer, ordered by date.

---

# Window Function Categories

Important categories:

```text
1. Aggregate window functions
2. Ranking functions
3. Value/navigation functions
```

---

# Aggregate Window Functions

Common ones:

```text
SUM()
AVG()
COUNT()
MIN()
MAX()
```

Example:

```sql
SELECT
    employee_name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg
FROM employees;
```

---

# SUM as Window Function

```sql
SELECT
    employee_name,
    salary,
    SUM(salary) OVER () AS total_salary
FROM employees;
```

Every row gets the total salary.

---

# COUNT as Window Function

```sql
SELECT
    employee_name,
    department_id,
    COUNT(*) OVER (
        PARTITION BY department_id
    ) AS employees_in_department
FROM employees;
```

---

# MIN as Window Function

```sql
SELECT
    employee_name,
    salary,
    MIN(salary) OVER (
        PARTITION BY department_id
    ) AS minimum_department_salary
FROM employees;
```

---

# MAX as Window Function

```sql
SELECT
    employee_name,
    salary,
    MAX(salary) OVER (
        PARTITION BY department_id
    ) AS maximum_department_salary
FROM employees;
```

---

# Ranking Functions

Important ranking functions:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
NTILE()
```

---

# ROW_NUMBER()

Assigns a unique sequential number to each row.

```sql
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

Example:

| employee | salary | row_num |
| -------- | -----: | ------: |
| Neha     |  90000 |       1 |
| Priya    |  80000 |       2 |
| Amit     |  70000 |       3 |
| Rahul    |  60000 |       4 |

---

# ROW_NUMBER with PARTITION

```sql
SELECT
    employee_name,
    department_id,
    salary,
    ROW_NUMBER() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

This restarts numbering for each department.

---

# RANK()

`RANK()` assigns the same rank to tied values.

Example:

```sql
SELECT
    employee_name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Suppose salaries are:

```text
100000
90000
90000
80000
```

Ranks:

```text
100000 → 1
90000  → 2
90000  → 2
80000  → 4
```

Notice the gap.

---

# DENSE_RANK()

`DENSE_RANK()` also gives equal values the same rank, but does not create gaps.

```text
100000 → 1
90000  → 2
90000  → 2
80000  → 3
```

---

# RANK vs DENSE_RANK

| Salary | RANK | DENSE_RANK |
| -----: | ---: | ---------: |
| 100000 |    1 |          1 |
|  90000 |    2 |          2 |
|  90000 |    2 |          2 |
|  80000 |    4 |          3 |

Remember:

```text
RANK
→ gaps after ties

DENSE_RANK
→ no gaps
```

---

# ROW_NUMBER vs RANK vs DENSE_RANK

| Function       | Ties           | Gaps |
| -------------- | -------------- | ---- |
| `ROW_NUMBER()` | Unique numbers | No   |
| `RANK()`       | Same rank      | Yes  |
| `DENSE_RANK()` | Same rank      | No   |

---

# NTILE()

Divides rows into approximately equal groups.

```sql
SELECT
    employee_name,
    salary,
    NTILE(4) OVER (
        ORDER BY salary DESC
    ) AS quartile
FROM employees;
```

For 100 rows:

```text
Quartile 1 → approximately 25 rows
Quartile 2 → approximately 25 rows
Quartile 3 → approximately 25 rows
Quartile 4 → approximately 25 rows
```

Useful for:

* Customer segmentation
* Salary bands
* Performance groups
* Percentile-style analysis

---

# 3. Advanced Window Functions

# Running Total

A running total accumulates values over time.

Example:

| date  | sales |
| ----- | ----: |
| Jan 1 |   100 |
| Jan 2 |   200 |
| Jan 3 |   150 |

Query:

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

Result:

| date  | amount | running_total |
| ----- | -----: | ------------: |
| Jan 1 |    100 |           100 |
| Jan 2 |    200 |           300 |
| Jan 3 |    150 |           450 |

---

# Running Total Per Customer

```sql
SELECT
    customer_id,
    order_date,
    amount,
    SUM(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS customer_running_total
FROM orders;
```

Each customer's cumulative total is calculated separately.

---

# Running Average

```sql
SELECT
    order_date,
    amount,
    AVG(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_average
FROM orders;
```

---

# Moving Average

A moving average uses a limited window around the current row.

Example: 3-row moving average.

```sql
SELECT
    order_date,
    amount,
    AVG(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN 2 PRECEDING
        AND CURRENT ROW
    ) AS moving_average
FROM orders;
```

For:

```text
100
200
300
400
```

Moving averages:

```text
100
150
200
300
```

---

# Window Frame

A window frame specifies which rows are included relative to the current row.

Example:

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

means:

```text
Current row
+
Previous row
+
Two rows before
```

---

# Common Window Frames

```text
UNBOUNDED PRECEDING
→ Start of partition

CURRENT ROW
→ Current row

n PRECEDING
→ n rows before

n FOLLOWING
→ n rows after

UNBOUNDED FOLLOWING
→ End of partition
```

---

# Running Total with Explicit Frame

```sql
SUM(amount) OVER (
    ORDER BY order_date
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND CURRENT ROW
)
```

This means:

```text
Beginning
   ↓
All previous rows
   +
Current row
```

---

# LAG()

`LAG()` retrieves a value from a previous row.

Example:

```sql
SELECT
    order_date,
    amount,
    LAG(amount) OVER (
        ORDER BY order_date
    ) AS previous_amount
FROM orders;
```

Result:

| date  | amount | previous_amount |
| ----- | -----: | --------------: |
| Jan 1 |    100 |            NULL |
| Jan 2 |    200 |             100 |
| Jan 3 |    150 |             200 |

---

# LAG with Offset

```sql
LAG(amount, 2) OVER (
    ORDER BY order_date
)
```

means:

> Get the value from two rows earlier.

---

# LAG with Default Value

Some SQL dialects support a third argument:

```sql
LAG(amount, 1, 0) OVER (
    ORDER BY order_date
)
```

If there is no previous row, return `0` instead of `NULL`.

Syntax support can vary by database.

---

# LEAD()

`LEAD()` retrieves a value from a future row.

```sql
SELECT
    order_date,
    amount,
    LEAD(amount) OVER (
        ORDER BY order_date
    ) AS next_amount
FROM orders;
```

Result:

| date  | amount | next_amount |
| ----- | -----: | ----------: |
| Jan 1 |    100 |         200 |
| Jan 2 |    200 |         150 |
| Jan 3 |    150 |        NULL |

---

# LAG vs LEAD

```text
LAG
→ Look backward

LEAD
→ Look forward
```

Memory trick:

```text
LAG  ← Previous
LEAD → Next
```

---

# Difference from Previous Row

```sql
SELECT
    order_date,
    amount,
    amount -
        LAG(amount) OVER (
            ORDER BY order_date
        ) AS difference
FROM orders;
```

Example:

```text
100
200
150
```

Difference:

```text
NULL
100
-50
```

---

# Growth Rate

Growth percentage can be calculated using `LAG()`.

```sql
SELECT
    order_date,
    amount,
    (
        amount - LAG(amount) OVER (
            ORDER BY order_date
        )
    )
    /
    NULLIF(
        LAG(amount) OVER (
            ORDER BY order_date
        ),
        0
    ) * 100 AS growth_percentage
FROM orders;
```

`NULLIF()` prevents division by zero.

---

# FIRST_VALUE()

Returns the first value in the window.

```sql
SELECT
    employee_name,
    department_id,
    salary,
    FIRST_VALUE(salary) OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS highest_salary
FROM employees;
```

This gives the highest salary in each department.

---

# FIRST_VALUE Example

Suppose IT salaries:

```text
90000
80000
70000
```

With:

```sql
FIRST_VALUE(salary) OVER (
    PARTITION BY department_id
    ORDER BY salary DESC
)
```

each IT employee gets:

```text
90000
```

---

# LAST_VALUE()

Returns the last value according to the window frame.

Important:

`LAST_VALUE()` is commonly misunderstood because the default frame may end at the current row in some SQL systems.

Safer explicit example:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department_id
    ORDER BY salary
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

This explicitly makes the frame cover the whole partition.

---

# NTH_VALUE()

Returns the value at a specified position within the window.

Example:

```sql
NTH_VALUE(salary, 2) OVER (
    PARTITION BY department_id
    ORDER BY salary DESC
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

This can return the second-highest salary in each department.

Support and exact behavior vary by SQL database.

---

# Percentage of Total

A common analytics problem:

> What percentage of total sales does each product represent?

```sql
SELECT
    product_id,
    SUM(amount) AS product_sales,
    SUM(SUM(amount)) OVER () AS total_sales
FROM sales
GROUP BY product_id;
```

To calculate percentage:

```sql
SELECT
    product_id,
    SUM(amount) AS product_sales,
    SUM(SUM(amount)) OVER () AS total_sales,
    SUM(amount) * 100.0
        / SUM(SUM(amount)) OVER () AS percentage_of_total
FROM sales
GROUP BY product_id;
```

---

# Percentage Within Department

```sql
SELECT
    department_id,
    employee_id,
    salary,
    salary * 100.0 /
        SUM(salary) OVER (
            PARTITION BY department_id
        ) AS salary_percentage
FROM employees;
```

This calculates each employee's salary as a percentage of their department's total salary.

---

# Cumulative Maximum

```sql
SELECT
    order_date,
    amount,
    MAX(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS cumulative_max
FROM orders;
```

Useful for:

* Record highs
* Peak sales
* Highest historical value
* Performance tracking

---

# Cumulative Minimum

```sql
SELECT
    order_date,
    amount,
    MIN(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS cumulative_min
FROM orders;
```

---

# Top N Per Group

One of the most important SQL analytics patterns.

Problem:

> Find top 3 employees by salary in each department.

```sql
WITH ranked_employees AS (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)

SELECT *
FROM ranked_employees
WHERE rn <= 3;
```

---

# Top N Per Group Using RANK

If ties should share a rank:

```sql
WITH ranked_employees AS (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
)

SELECT *
FROM ranked_employees
WHERE rnk <= 3;
```

This can return more than three employees in a department because of ties.

---

# Deduplication Using ROW_NUMBER

Suppose a customer table contains multiple records.

```sql
WITH ranked_customers AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY updated_at DESC
        ) AS rn
    FROM customers
)

SELECT *
FROM ranked_customers
WHERE rn = 1;
```

This keeps the most recently updated row per customer.

---

# Finding Duplicate Records

```sql
WITH duplicate_check AS (
    SELECT
        *,
        COUNT(*) OVER (
            PARTITION BY email
        ) AS email_count
    FROM customers
)

SELECT *
FROM duplicate_check
WHERE email_count > 1;
```

---

# Compare Current Row to Previous Row

```sql
SELECT
    order_date,
    amount,
    LAG(amount) OVER (
        ORDER BY order_date
    ) AS previous_amount,
    amount -
        LAG(amount) OVER (
            ORDER BY order_date
        ) AS difference
FROM orders;
```

---

# Compare Current Row to Next Row

```sql
SELECT
    order_date,
    amount,
    LEAD(amount) OVER (
        ORDER BY order_date
    ) AS next_amount
FROM orders;
```

---

# Find First Purchase Per Customer

```sql
WITH purchases AS (
    SELECT
        customer_id,
        order_id,
        order_date,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date
        ) AS rn
    FROM orders
)

SELECT *
FROM purchases
WHERE rn = 1;
```

---

# Find Latest Purchase Per Customer

```sql
WITH purchases AS (
    SELECT
        customer_id,
        order_id,
        order_date,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS rn
    FROM orders
)

SELECT *
FROM purchases
WHERE rn = 1;
```

---

# Window Frame: ROWS

`ROWS` defines a physical row-based frame.

Example:

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

Means:

```text
Current row
Previous row
Two rows before
```

---

# ROWS vs RANGE

This is an important advanced concept.

### ROWS

Works based on physical row positions.

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

### RANGE

Works based on the ordering values and can include peer rows with the same ordering value, depending on the database and expression.

This distinction matters when there are duplicate values in the `ORDER BY` column.

For deterministic row-by-row calculations, `ROWS` is often clearer.

---

# Example: Duplicate Dates

Suppose:

| date  | amount |
| ----- | -----: |
| Jan 1 |    100 |
| Jan 1 |    200 |
| Jan 2 |    300 |

With:

```sql
SUM(amount) OVER (
    ORDER BY date
)
```

the exact behavior around duplicate ordering values depends on the default frame and database.

For predictable row-based accumulation, consider:

```sql
SUM(amount) OVER (
    ORDER BY date, order_id
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND CURRENT ROW
)
```

Use a deterministic tie-breaker when row order matters.

---

# Window Functions Cannot Usually Be Used Directly in WHERE

This is generally invalid:

```sql
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS rn
FROM employees
WHERE rn <= 5;
```

Why?

Because the window result is calculated after the filtering phase where `WHERE` is evaluated.

Use a CTE:

```sql
WITH ranked AS (
    SELECT
        employee_name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)

SELECT *
FROM ranked
WHERE rn <= 5;
```

---

# Window Functions and QUALIFY

Some databases support:

```sql
QUALIFY
```

Example:

```sql
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS rn
FROM employees
QUALIFY rn <= 5;
```

`QUALIFY` filters after window functions are evaluated.

However, `QUALIFY` is not supported by every SQL database.

The CTE/subquery approach is more portable.

---

# 4. NULL Handling

# What is NULL?

`NULL` represents:

```text
Missing
Unknown
Not available
Not applicable
```

It does **not** mean:

```text
0
```

and it does not necessarily mean:

```text
''
```

---

# NULL vs Zero

These are different:

```text
NULL
→ Unknown / missing

0
→ Known numeric value of zero
```

Example:

```text
salary = NULL
```

means:

> Salary is unknown/missing.

Whereas:

```text
salary = 0
```

means:

> Salary is known to be zero.

---

# NULL vs Empty String

These are conceptually different:

```text
NULL
→ Missing/unknown

''
→ Empty string
```

Whether an empty string is treated specially can vary by database system, so don't assume every database behaves identically.

---

# NULL is Not Equal to Anything

This is incorrect:

```sql
WHERE manager_id = NULL
```

Use:

```sql
WHERE manager_id IS NULL
```

---

# IS NULL

Find rows where a column is NULL:

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

# IS NOT NULL

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

---

# Three-Valued Logic

SQL uses three logical states:

```text
TRUE
FALSE
UNKNOWN
```

When NULL is involved, comparisons can result in `UNKNOWN`.

Example:

```sql
salary > 50000
```

If:

```text
salary = NULL
```

the result is:

```text
UNKNOWN
```

not `FALSE`.

---

# Example

Suppose:

| employee | salary |
| -------- | -----: |
| Rahul    |  70000 |
| Priya    |   NULL |
| Amit     |  40000 |

Query:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Result:

```text
Rahul
```

Why not Priya?

Because:

```text
NULL > 50000
```

produces `UNKNOWN`.

`WHERE` keeps only rows where the condition evaluates to `TRUE`.

---

# NULL and Equality

This does not work as expected:

```sql
WHERE salary = NULL
```

Because:

```text
NULL = NULL
```

is not `TRUE`.

Use:

```sql
WHERE salary IS NULL
```

---

# NULL and NOT Equal

This can also surprise people:

```sql
WHERE salary <> 50000
```

Rows with:

```text
salary = NULL
```

do not satisfy the condition because the comparison is `UNKNOWN`.

If you want to explicitly include NULLs:

```sql
WHERE salary <> 50000
   OR salary IS NULL;
```

---

# COALESCE

`COALESCE()` returns the first non-NULL expression.

Syntax:

```sql
COALESCE(value1, value2, value3, ...)
```

Example:

```sql
SELECT
    employee_name,
    COALESCE(phone, 'Not Available') AS phone
FROM employees;
```

If:

```text
phone = NULL
```

result:

```text
Not Available
```

---

# COALESCE with Multiple Values

```sql
SELECT
    COALESCE(
        mobile_phone,
        home_phone,
        work_phone,
        'No Phone'
    ) AS contact_number
FROM customers;
```

Logic:

```text
mobile_phone
    ↓
if NULL → home_phone
    ↓
if NULL → work_phone
    ↓
if NULL → 'No Phone'
```

---

# COALESCE in Calculations

Suppose:

```text
salary = 50000
bonus = NULL
```

This:

```sql
SELECT salary + bonus
FROM employees;
```

may return:

```text
NULL
```

because arithmetic involving NULL generally produces NULL.

Use:

```sql
SELECT
    salary + COALESCE(bonus, 0)
FROM employees;
```

Result:

```text
50000
```

---

# COALESCE in Aggregations

Example:

```sql
SELECT
    customer_id,
    SUM(COALESCE(amount, 0)) AS total_amount
FROM orders
GROUP BY customer_id;
```

Be aware that `SUM()` already ignores NULL input values in standard aggregate behavior, so `COALESCE` is not always necessary there. It becomes especially useful when you need to convert NULL values to a specific value before another calculation.

---

# NULLIF

`NULLIF()` returns `NULL` if two expressions are equal.

Syntax:

```sql
NULLIF(expression1, expression2)
```

Example:

```sql
SELECT
    NULLIF(10, 10);
```

Result:

```text
NULL
```

---

# NULLIF for Division by Zero

Very important in analytics.

Instead of:

```sql
SELECT
    sales / orders
FROM metrics;
```

which may fail when:

```text
orders = 0
```

use:

```sql
SELECT
    sales / NULLIF(orders, 0)
FROM metrics;
```

If:

```text
orders = 0
```

then:

```text
NULLIF(orders, 0)
```

becomes:

```text
NULL
```

and division by zero is avoided.

---

# COALESCE + NULLIF

You can combine them:

```sql
SELECT
    COALESCE(
        sales / NULLIF(orders, 0),
        0
    ) AS conversion_rate
FROM metrics;
```

Logic:

```text
orders = 0
       ↓
NULLIF → NULL
       ↓
division → NULL
       ↓
COALESCE → 0
```

---

# CASE with NULL

You can handle NULL using `CASE`.

Correct:

```sql
CASE
    WHEN salary IS NULL THEN 'Missing'
    ELSE 'Available'
END
```

Incorrect:

```sql
CASE
    WHEN salary = NULL THEN 'Missing'
    ELSE 'Available'
END
```

---

# CASE + COALESCE

```sql
SELECT
    employee_name,
    CASE
        WHEN COALESCE(salary, 0) = 0
            THEN 'No Salary'
        ELSE 'Salary Available'
    END AS salary_status
FROM employees;
```

Be careful: treating NULL as zero changes the business meaning, so only do this when that interpretation is appropriate.

---

# NULL in Aggregate Functions

Most standard aggregate functions ignore NULL values.

Example:

| salary |
| -----: |
|  50000 |
|  60000 |
|   NULL |

Query:

```sql
SELECT AVG(salary)
FROM employees;
```

The NULL salary is ignored by the aggregate.

Conceptually:

```text
(50000 + 60000) / 2
```

not:

```text
(50000 + 60000 + NULL) / 3
```

---

# COUNT and NULL

This is very important.

### COUNT(*)

Counts rows.

```sql
SELECT COUNT(*)
FROM employees;
```

NULL values do not matter.

---

### COUNT(column)

Counts non-NULL values.

```sql
SELECT COUNT(phone)
FROM employees;
```

If phone is NULL, that row is not counted.

---

# COUNT Example

Suppose:

| employee | phone |
| -------- | ----- |
| Rahul    | 9999  |
| Priya    | NULL  |
| Amit     | 8888  |

```sql
COUNT(*)
```

returns:

```text
3
```

while:

```sql
COUNT(phone)
```

returns:

```text
2
```

---

# COUNT DISTINCT and NULL

```sql
COUNT(DISTINCT phone)
```

generally counts distinct non-NULL values.

The exact treatment of NULL should be confirmed for the specific database when edge cases matter.

---

# SUM and NULL

```sql
SUM(amount)
```

normally ignores NULL amounts.

However, if there are no non-NULL rows to aggregate, the result can be NULL rather than zero.

Therefore, when you need a guaranteed zero result:

```sql
COALESCE(SUM(amount), 0)
```

---

# AVG and NULL

`AVG()` normally ignores NULL values.

Example:

```text
100
200
NULL
```

Average:

```text
150
```

not:

```text
100
```

or:

```text
100
200
0
```

---

# MIN and MAX with NULL

Aggregate `MIN()` and `MAX()` generally ignore NULL values.

Example:

```text
100
200
NULL
```

```text
MIN → 100
MAX → 200
```

If all values are NULL, the result is NULL.

---

# NULL in GROUP BY

NULL values form a group together.

Example:

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

If some employees have:

```text
department_id = NULL
```

they are grouped together under the NULL group.

---

# Replacing NULL Group Labels

```sql
SELECT
    COALESCE(
        department_id,
        'Unknown'
    ) AS department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    COALESCE(
        department_id,
        'Unknown'
    );
```

Use a type-compatible replacement.

---

# NULL in ORDER BY

Sorting behavior for NULL depends on the database and whether `NULLS FIRST` / `NULLS LAST` is supported.

Some databases place NULLs first by default for ascending order, while others place them last.

You can often explicitly control this where supported:

```sql
ORDER BY salary ASC NULLS LAST;
```

or:

```sql
ORDER BY salary DESC NULLS LAST;
```

For maximum portability, you can also use an expression:

```sql
ORDER BY
    CASE WHEN salary IS NULL THEN 1 ELSE 0 END,
    salary;
```

---

# NULL in JOINs

Suppose:

### Customers

| customer_id |
| ----------: |
|           1 |
|           2 |
|        NULL |

### Orders

| customer_id |
| ----------: |
|           1 |
|           2 |
|        NULL |

This:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

does not normally match:

```text
NULL = NULL
```

because NULL comparisons produce UNKNOWN.

Therefore, the NULL customer IDs do not match under ordinary equality.

---

# NULL-Safe JOIN

Some databases provide a NULL-safe equality operator or syntax.

For example, PostgreSQL supports:

```sql
IS NOT DISTINCT FROM
```

Example:

```sql
ON c.customer_id IS NOT DISTINCT FROM o.customer_id
```

This treats two NULLs as equal for comparison.

Other databases have different syntax, such as MySQL's `<=>`.

Always use the syntax supported by your database.

---

# NULL in IN

Suppose:

```text
IN list:
1
2
NULL
```

A condition like:

```sql
customer_id IN (1, 2, NULL)
```

can produce `UNKNOWN` for values that do not match 1 or 2.

Do not treat NULL as an ordinary comparable value.

---

# NULL in NOT IN

This is one of the most important SQL NULL traps.

Suppose:

```sql
SELECT customer_id
FROM orders;
```

returns:

```text
1
2
NULL
```

Then:

```sql
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
)
```

can result in no rows matching as expected because comparisons against NULL become UNKNOWN.

---

# Safer Alternative: NOT EXISTS

Instead of:

```sql
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
)
```

prefer:

```sql
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
)
```

when the goal is anti-matching.

---

# NULL in EXISTS

`EXISTS` is based on whether the subquery returns rows.

It does not care whether the selected value itself is NULL.

Example:

```sql
WHERE EXISTS (
    SELECT NULL
    FROM orders o
    WHERE o.customer_id = c.customer_id
)
```

If a matching row exists, `EXISTS` is TRUE even though the selected expression is NULL.

---

# NULL in Window Functions

Window aggregate functions generally follow the same NULL behavior as their aggregate counterparts.

Example:

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

normally ignores NULL salaries.

---

# LAG and NULL

Suppose:

| date  | sales |
| ----- | ----: |
| Jan 1 |   100 |
| Jan 2 |  NULL |
| Jan 3 |   300 |

```sql
LAG(sales) OVER (
    ORDER BY date
)
```

may return:

```text
Jan 1 → NULL
Jan 2 → 100
Jan 3 → NULL
```

The NULL from Jan 2 is a legitimate value returned from the previous row.

---

# Handling LAG NULL

You can use:

```sql
COALESCE(
    LAG(sales) OVER (
        ORDER BY date
    ),
    0
)
```

But be careful:

```text
No previous row
```

and:

```text
Previous row exists but sales is NULL
```

are different business situations.

Replacing both with zero may hide that distinction.

---

# NULL and Running Totals

Example:

```sql
SUM(amount) OVER (
    ORDER BY order_date
)
```

Aggregate window functions generally ignore NULL values.

If:

```text
100
NULL
200
```

the cumulative values are conceptually:

```text
100
100
300
```

---

# NULL and Ranking

Ranking functions generally rank rows based on the `ORDER BY` expression.

Because NULL ordering varies by database/defaults, explicitly control NULL placement when it matters.

Example:

```sql
ORDER BY
    CASE WHEN salary IS NULL THEN 1 ELSE 0 END,
    salary DESC
```

---

# 5. CTE + Window Function Patterns

This combination is extremely important for analytics.

---

# Pattern 1 — Top N Per Group

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)

SELECT *
FROM ranked
WHERE rn <= 3;
```

---

# Pattern 2 — Latest Record Per Entity

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY updated_at DESC
        ) AS rn
    FROM customer_history
)

SELECT *
FROM ranked
WHERE rn = 1;
```

---

# Pattern 3 — Compare to Group Average

```sql
WITH employee_stats AS (
    SELECT
        employee_name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees
)

SELECT *
FROM employee_stats
WHERE salary > department_avg;
```

---

# Pattern 4 — Running Total

```sql
WITH sales_data AS (
    SELECT
        order_date,
        amount
    FROM orders
)

SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total
FROM sales_data;
```

---

# Pattern 5 — Month-over-Month Growth

```sql
WITH monthly_sales AS (
    SELECT
        month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY month
),

sales_with_previous AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM monthly_sales
)

SELECT
    month,
    sales,
    previous_sales,
    (sales - previous_sales) * 100.0
        / NULLIF(previous_sales, 0) AS growth_percentage
FROM sales_with_previous;
```

This is a very common data analytics pattern.

---

# Pattern 6 — Deduplicate Data

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

---

# Pattern 7 — Find Duplicate Records

```sql
WITH duplicate_data AS (
    SELECT
        *,
        COUNT(*) OVER (
            PARTITION BY email
        ) AS duplicate_count
    FROM customers
)

SELECT *
FROM duplicate_data
WHERE duplicate_count > 1;
```

---

# 6. Data Analytics Examples

# Example 1 — Customer Running Spend

```sql
SELECT
    customer_id,
    order_date,
    amount,
    SUM(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_spend
FROM orders;
```

---

# Example 2 — Customer Rank by Spending

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)

SELECT
    customer_id,
    total_sales,
    RANK() OVER (
        ORDER BY total_sales DESC
    ) AS customer_rank
FROM customer_sales;
```

---

# Example 3 — Department Salary Rank

```sql
SELECT
    employee_name,
    department_id,
    salary,
    DENSE_RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# Example 4 — Above Department Average

```sql
WITH employee_stats AS (
    SELECT
        employee_name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees
)

SELECT *
FROM employee_stats
WHERE salary > department_avg;
```

---

# Example 5 — Previous Month Sales

```sql
WITH monthly_sales AS (
    SELECT
        month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY month
)

SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales
FROM monthly_sales;
```

---

# Example 6 — Month-over-Month Change

```sql
WITH monthly_sales AS (
    SELECT
        month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY month
)

SELECT
    month,
    sales,
    sales -
        LAG(sales) OVER (
            ORDER BY month
        ) AS sales_change
FROM monthly_sales;
```

---

# Example 7 — Top 3 Products Per Category

```sql
WITH product_sales AS (
    SELECT
        category_id,
        product_id,
        SUM(amount) AS total_sales
    FROM sales
    GROUP BY
        category_id,
        product_id
),

ranked_products AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY category_id
            ORDER BY total_sales DESC
        ) AS rn
    FROM product_sales
)

SELECT *
FROM ranked_products
WHERE rn <= 3;
```

---

# Example 8 — Customer Percentage of Total Revenue

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)

SELECT
    customer_id,
    total_sales,
    total_sales * 100.0 /
        SUM(total_sales) OVER () AS revenue_percentage
FROM customer_sales;
```

---

# Example 9 — Employee Salary as Department Percentage

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary,
    salary * 100.0 /
        SUM(salary) OVER (
            PARTITION BY department_id
        ) AS department_salary_percentage
FROM employees;
```

---

# Example 10 — Detect Sales Drops

```sql
WITH sales_data AS (
    SELECT
        month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY month
),

comparison AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM sales_data
)

SELECT
    month,
    sales,
    previous_sales,
    sales - previous_sales AS change
FROM comparison
WHERE sales < previous_sales;
```

---

# 7. Common Mistakes

# Mistake 1 — Using GROUP BY When You Need Individual Rows

Wrong approach:

```sql
SELECT
    department_id,
    AVG(salary)
FROM employees
GROUP BY department_id;
```

This removes employee-level detail.

Use:

```sql
SELECT
    employee_name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg
FROM employees;
```

when you need both employee detail and department-level statistics.

---

# Mistake 2 — Filtering Window Functions Directly in WHERE

Don't generally do:

```sql
WHERE ROW_NUMBER() OVER (...) <= 3
```

Use a CTE/subquery or `QUALIFY` where supported.

---

# Mistake 3 — Confusing RANK and ROW_NUMBER

`ROW_NUMBER()`:

```text
1
2
3
4
```

even with ties.

`RANK()`:

```text
1
2
2
4
```

---

# Mistake 4 — Forgetting PARTITION BY

Without:

```sql
PARTITION BY customer_id
```

a running total may be calculated across all customers.

Wrong for per-customer analysis:

```sql
SUM(amount) OVER (
    ORDER BY order_date
)
```

Correct:

```sql
SUM(amount) OVER (
    PARTITION BY customer_id
    ORDER BY order_date
)
```

---

# Mistake 5 — Not Defining Window Frame

For advanced cumulative/moving calculations, explicitly define the frame when behavior matters:

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND CURRENT ROW
```

---

# Mistake 6 — Misunderstanding LAST_VALUE

This can surprise you:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department_id
    ORDER BY salary
)
```

The default frame may end at the current row.

Use an explicit full frame when you need the last value in the entire partition:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department_id
    ORDER BY salary
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

---

# Mistake 7 — Treating NULL as Zero

Don't automatically do:

```sql
COALESCE(salary, 0)
```

unless NULL really should mean zero for the business problem.

Missing salary and zero salary have different meanings.

---

# Mistake 8 — Using `= NULL`

Wrong:

```sql
WHERE salary = NULL;
```

Correct:

```sql
WHERE salary IS NULL;
```

---

# Mistake 9 — Using NOT IN with Nullable Data

Potentially dangerous:

```sql
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
);
```

If the subquery can contain NULL, consider:

```sql
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Mistake 10 — Assuming CTE Improves Performance

A CTE primarily improves query structure/readability.

It does not automatically mean:

```text
CTE = Faster
```

The optimizer and database engine determine execution behavior.

---

# Mistake 11 — Forgetting Deterministic Ordering

This:

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC
)
```

may assign arbitrary row numbers among tied salaries.

If you need deterministic results:

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC, employee_id
)
```

---

# 8. Interview Questions

## What is a CTE?

A named temporary result set defined using the `WITH` clause for use within a SQL statement.

---

## Why use a CTE?

To:

* Improve readability
* Break complex logic into steps
* Simplify nested queries
* Support recursive queries
* Combine transformations

---

## CTE vs Subquery?

CTEs are named and often easier to organize for multi-step logic. Subqueries are inline query expressions.

---

## What is a window function?

A function that performs calculations across related rows while retaining the individual rows in the result.

---

## GROUP BY vs Window Function?

```text
GROUP BY
→ Collapses rows.

Window Function
→ Keeps rows.
```

---

## What is PARTITION BY?

It divides rows into independent groups for a window calculation.

---

## What is ORDER BY inside OVER?

It determines the logical order of rows for the window calculation.

---

## ROW_NUMBER vs RANK?

```text
ROW_NUMBER
→ Always unique sequential numbers.

RANK
→ Ties receive the same rank and gaps appear.
```

---

## RANK vs DENSE_RANK?

```text
RANK
→ Gaps after ties.

DENSE_RANK
→ No gaps.
```

---

## What is LAG?

Returns a value from a previous row.

---

## What is LEAD?

Returns a value from a following row.

---

## What is a running total?

A cumulative sum from the beginning of the window up to the current row.

---

## What is a moving average?

An average calculated over a sliding set of rows around the current row.

---

## What is a window frame?

The specific subset of rows included in a window calculation.

---

## What is NULL?

A marker representing missing, unknown, or unavailable data.

---

## Is NULL equal to zero?

No.

```text
NULL ≠ 0
```

---

## Is NULL equal to NULL?

Ordinary SQL equality does not treat NULL = NULL as TRUE.

Use:

```sql
IS NULL
```

when checking for NULL.

---

## What is COALESCE?

Returns the first non-NULL expression.

```sql
COALESCE(phone, 'Unknown')
```

---

## What is NULLIF?

Returns NULL when two expressions are equal.

```sql
NULLIF(denominator, 0)
```

is commonly used to prevent division by zero.

---

## Why is NOT IN dangerous with NULL?

If the subquery contains NULL, SQL's three-valued logic can make the predicate evaluate to UNKNOWN, causing unexpected filtering.

---

# 9. Quick Revision Cheat Sheet

# CTE

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT *
FROM cte_name;
```

Remember:

```text
CTE
→ Named temporary query result
→ Exists for one statement
→ Improves readability
→ Can be recursive
```

---

# Window Function Syntax

```sql
function(...)
OVER (
    PARTITION BY ...
    ORDER BY ...
    ROWS/RANGE ...
)
```

Remember:

```text
PARTITION BY
→ Groups the window

ORDER BY
→ Orders rows

ROWS/RANGE
→ Defines frame
```

---

# Aggregate Window Functions

```text
SUM()
AVG()
COUNT()
MIN()
MAX()
```

---

# Ranking Functions

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
NTILE()
```

---

# Value / Navigation Functions

```text
LAG()
LEAD()
FIRST_VALUE()
LAST_VALUE()
NTH_VALUE()
```

---

# Common Window Patterns

## Running total

```sql
SUM(amount) OVER (
    ORDER BY date
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND CURRENT ROW
)
```

## Moving average

```sql
AVG(amount) OVER (
    ORDER BY date
    ROWS BETWEEN 2 PRECEDING
    AND CURRENT ROW
)
```

## Previous value

```sql
LAG(amount) OVER (
    ORDER BY date
)
```

## Next value

```sql
LEAD(amount) OVER (
    ORDER BY date
)
```

## Rank within group

```sql
RANK() OVER (
    PARTITION BY department_id
    ORDER BY salary DESC
)
```

## Top N per group

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY category
            ORDER BY sales DESC
        ) AS rn
    FROM sales
)

SELECT *
FROM ranked
WHERE rn <= 3;
```

---

# NULL Functions

```text
IS NULL
→ Check NULL

IS NOT NULL
→ Check non-NULL

COALESCE()
→ First non-NULL value

NULLIF()
→ NULL when two values are equal
```

---

# NULL Rules to Memorize

```text
NULL ≠ 0

NULL ≠ ''

NULL = NULL
→ Not TRUE under ordinary SQL equality

column = NULL
→ Wrong

column IS NULL
→ Correct

column <> value
→ NULL rows are not TRUE

COUNT(*)
→ Counts rows

COUNT(column)
→ Counts non-NULL values

SUM()
→ Ignores NULL inputs

AVG()
→ Ignores NULL inputs

MIN()
→ Ignores NULL inputs

MAX()
→ Ignores NULL inputs

NOT IN + NULL
→ Potentially dangerous

NOT EXISTS
→ Often safer for anti-matching
```

---

# ⭐ Most Important Analytics Patterns

If you are preparing for **Data Analyst / Data Science / SQL interviews**, master these patterns:

```text
1. CTE
2. Multiple CTEs
3. Recursive CTE
4. GROUP BY vs Window Functions
5. PARTITION BY
6. ORDER BY inside OVER
7. ROW_NUMBER
8. RANK
9. DENSE_RANK
10. NTILE
11. Running Total
12. Running Average
13. Moving Average
14. LAG
15. LEAD
16. FIRST_VALUE
17. LAST_VALUE
18. Percentage of Total
19. Top N per Group
20. Deduplication
21. Previous/Next Row Comparison
22. Month-over-Month Growth
23. Cumulative Maximum
24. NULL handling
25. COALESCE
26. NULLIF
27. NULL with JOIN
28. NULL with IN/NOT IN
29. NULL with Aggregates
30. NULL with Window Functions
```

---

# Final Mental Model

```text
                         ADVANCED SQL
                              │
             ┌────────────────┼────────────────┐
             ↓                ↓                ↓
            CTE         WINDOW FUNCTIONS     NULL
             │                │                │
             ↓                ↓                ↓
       Break query       Analyze rows       Handle missing
        into steps        without           data
                           collapsing
             │                │                │
       ┌─────┴─────┐     ┌────┴─────┐    ┌────┴─────┐
       ↓           ↓     ↓          ↓    ↓          ↓
   Multiple     Recursive Rank    LAG  IS NULL  COALESCE
    CTEs          CTE            LEAD  IS NOT    NULLIF
                                      NULL
```

## The Most Important Concept

For data analytics, think of these tools as solving different problems:

```text
CTE
→ "How can I break my query into understandable steps?"

Window Function
→ "How can I calculate something across related rows
   without losing the individual rows?"

PARTITION BY
→ "Which rows should be treated as one group?"

ORDER BY
→ "In what sequence should the calculation happen?"

Window Frame
→ "Exactly which rows should participate?"

LAG / LEAD
→ "How does this row compare with another row?"

ROW_NUMBER / RANK / DENSE_RANK
→ "How does this row rank within its group?"

NULL Handling
→ "What should happen when the data is missing or unknown?"
```

Mastering these concepts gives you the foundation for many advanced **SQL data-analytics problems**, especially ranking, retention, cohort analysis, time-series analysis, deduplication, running metrics, and business reporting.
