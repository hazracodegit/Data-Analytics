# SQL Aggregate Functions

Aggregate functions are SQL functions that **perform calculations on multiple rows and return a single result**.

They are heavily used in:

* Data analysis
* Business intelligence
* Reporting
* Data summarization
* Statistics
* Dashboards
* KPI calculation
* Group-wise analysis

---

# 1. What Are Aggregate Functions?

An aggregate function takes values from multiple rows and produces one summarized value.

Example:

```sql
SELECT SUM(salary)
FROM employees;
```

If the salaries are:

```text
50000
60000
70000
80000
```

`SUM()` produces:

```text
260000
```

Conceptually:

```text
Multiple Rows
     ↓
Aggregate Function
     ↓
Single Result
```

---

# 2. Main Aggregate Functions

The five most important aggregate functions are:

| Function  | Purpose            |
| --------- | ------------------ |
| `COUNT()` | Counts rows/values |
| `SUM()`   | Calculates total   |
| `AVG()`   | Calculates average |
| `MIN()`   | Finds minimum      |
| `MAX()`   | Finds maximum      |

These five functions are essential for SQL and data analytics.

---

# 3. Sample Table

Throughout this README, assume we have the following table:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    age INT
);
```

Example data:

| employee_id | name  | department | salary | age |
| ----------: | ----- | ---------- | -----: | --: |
|           1 | Rahul | IT         |  60000 |  25 |
|           2 | Priya | IT         |  75000 |  28 |
|           3 | Arun  | HR         |  50000 |  30 |
|           4 | Sneha | HR         |  55000 |  27 |
|           5 | Kiran | Finance    |  80000 |  35 |
|           6 | Anil  | Finance    |  70000 |  32 |

---

# 4. COUNT()

`COUNT()` is used to count rows or non-NULL values.

There are three important forms:

```text
COUNT(*)
COUNT(column)
COUNT(DISTINCT column)
```

---

# 5. COUNT(*)

`COUNT(*)` counts the number of rows.

```sql
SELECT COUNT(*)
FROM employees;
```

Output:

```text
6
```

It counts every row, including rows containing NULL values.

---

# 6. COUNT(column)

`COUNT(column)` counts only **non-NULL values** in that column.

```sql
SELECT COUNT(salary)
FROM employees;
```

If every employee has a salary:

```text
6
```

Suppose one salary is NULL:

```text
COUNT(*)      → 6
COUNT(salary) → 5
```

This distinction is very important.

---

# 7. COUNT(DISTINCT column)

Counts unique non-NULL values.

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

Departments:

```text
IT
IT
HR
HR
Finance
Finance
```

Result:

```text
3
```

Because there are three unique departments.

---

# 8. COUNT() for Data Analytics

Count total employees:

```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```

Count employees in IT:

```sql
SELECT COUNT(*) AS it_employees
FROM employees
WHERE department = 'IT';
```

Count unique departments:

```sql
SELECT COUNT(DISTINCT department) AS department_count
FROM employees;
```

---

# 9. SUM()

`SUM()` calculates the total of numeric values.

```sql
SELECT SUM(salary)
FROM employees;
```

Calculation:

```text
60000
+75000
+50000
+55000
+80000
+70000
-------
390000
```

Result:

```text
390000
```

---

# 10. SUM() with WHERE

Calculate total IT salaries:

```sql
SELECT SUM(salary) AS total_it_salary
FROM employees
WHERE department = 'IT';
```

Calculation:

```text
60000 + 75000 = 135000
```

---

# 11. SUM() in Sales Analytics

Suppose we have:

```text
sales
------
product
quantity
price
```

Calculate total sales:

```sql
SELECT SUM(quantity * price) AS total_sales
FROM sales;
```

This is a common real-world analytics calculation.

---

# 12. AVG()

`AVG()` calculates the arithmetic mean.

```sql
SELECT AVG(salary)
FROM employees;
```

Conceptually:

```text
SUM(salary)
------------
COUNT(salary)
```

For the sample data:

```text
390000 / 6
= 65000
```

Result:

```text
65000
```

---

# 13. AVG() with ROUND()

For cleaner output:

```sql
SELECT ROUND(AVG(salary), 2) AS average_salary
FROM employees;
```

`ROUND()` is not an aggregate function here; it is being applied to the aggregate result.

Conceptually:

```text
AVG()
 ↓
ROUND()
```

---

# 14. AVG() and NULL

`AVG()` ignores NULL values.

Suppose salaries are:

```text
60000
75000
NULL
55000
80000
70000
```

`AVG(salary)` does not treat NULL as zero.

It calculates:

```text
60000 + 75000 + 55000 + 80000 + 70000
------------------------------------------------
5
```

Therefore, remember:

```text
NULL is generally ignored by AVG()
```

---

# 15. MIN()

`MIN()` returns the smallest value.

```sql
SELECT MIN(salary) AS minimum_salary
FROM employees;
```

Result:

```text
50000
```

It can be used with:

* Numbers
* Dates
* Some text types, according to database ordering rules

---

# 16. MIN() with Dates

Suppose:

```text
order_date
----------
2026-01-10
2026-02-15
2026-01-05
```

Find the earliest order:

```sql
SELECT MIN(order_date) AS first_order_date
FROM orders;
```

Result:

```text
2026-01-05
```

This is useful for finding:

* First purchase
* First login
* Earliest transaction
* First activity

---

# 17. MAX()

`MAX()` returns the largest value.

```sql
SELECT MAX(salary) AS maximum_salary
FROM employees;
```

Result:

```text
80000
```

---

# 18. MAX() with Dates

```sql
SELECT MAX(order_date) AS latest_order_date
FROM orders;
```

This can identify the most recent transaction.

---

# 19. Using All Aggregate Functions Together

You can use multiple aggregate functions in the same query.

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

Possible output:

| employee_count | total_salary | average_salary | minimum_salary | maximum_salary |
| -------------: | -----------: | -------------: | -------------: | -------------: |
|              6 |       390000 |          65000 |          50000 |          80000 |

This gives a quick statistical summary of the table.

---

# 20. Aggregate Functions with GROUP BY

Aggregate functions become much more powerful when combined with `GROUP BY`.

Without `GROUP BY`:

```sql
SELECT AVG(salary)
FROM employees;
```

You get the average salary of all employees.

With `GROUP BY`:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

Output:

| department | average_salary |
| ---------- | -------------: |
| IT         |          67500 |
| HR         |          52500 |
| Finance    |          75000 |

Now the calculation is performed separately for each department.

---

# 21. How GROUP BY Works

Conceptually:

```text
Employees
    ↓
GROUP BY department
    ↓
┌─────────┐
│   IT    │
├─────────┤
│   HR    │
├─────────┤
│ Finance │
└─────────┘
    ↓
Aggregate each group
    ↓
Results
```

---

# 22. COUNT() with GROUP BY

Count employees in each department:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Output:

| department | employee_count |
| ---------- | -------------: |
| IT         |              2 |
| HR         |              2 |
| Finance    |              2 |

---

# 23. SUM() with GROUP BY

Calculate total salary per department:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

Output:

| department | total_salary |
| ---------- | -----------: |
| IT         |       135000 |
| HR         |       105000 |
| Finance    |       150000 |

---

# 24. AVG() with GROUP BY

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 25. MIN() with GROUP BY

```sql
SELECT
    department,
    MIN(salary) AS minimum_salary
FROM employees
GROUP BY department;
```

---

# 26. MAX() with GROUP BY

```sql
SELECT
    department,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```

---

# 27. Multiple Aggregates with GROUP BY

This is one of the most common analytics queries:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```

This creates a department-level summary.

---

# 28. GROUP BY Multiple Columns

You can group by more than one column.

Suppose we have:

```text
department
gender
salary
```

Query:

```sql
SELECT
    department,
    gender,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department, gender;
```

The data is grouped by the combination:

```text
department + gender
```

---

# 29. GROUP BY and ORDER BY

You can sort aggregated results.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```

This displays departments from highest average salary to lowest.

---

# 30. GROUP BY and LIMIT

You can find the top departments.

For example:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC
LIMIT 3;
```

`LIMIT` syntax varies by database system.

---

# 31. HAVING with Aggregate Functions

`HAVING` filters groups after aggregation.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Only departments whose average salary is greater than 60,000 are returned.

---

# 32. WHERE vs HAVING

This is extremely important.

### WHERE

Filters individual rows **before grouping**.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary > 40000
GROUP BY department;
```

### HAVING

Filters groups **after aggregation**.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Remember:

```text
WHERE
↓
Filters rows

GROUP BY
↓
Creates groups

Aggregate
↓
Calculates group values

HAVING
↓
Filters groups
```

---

# 33. DISTINCT with Aggregate Functions

`DISTINCT` can be used with aggregate functions.

Example:

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

Another example:

```sql
SELECT SUM(DISTINCT salary)
FROM employees;
```

`SUM(DISTINCT salary)` adds each distinct salary value only once.

Be careful: this is not the same as summing every employee's salary.

---

# 34. COUNT(DISTINCT)

Very common in data analytics.

Suppose:

```text
customer_id
-----------
101
101
102
103
103
103
```

Query:

```sql
SELECT COUNT(DISTINCT customer_id)
FROM orders;
```

Result:

```text
3
```

This represents the number of unique customers.

---

# 35. COUNT(DISTINCT) for Analytics

Unique customers:

```sql
SELECT COUNT(DISTINCT customer_id) AS unique_customers
FROM orders;
```

Unique products:

```sql
SELECT COUNT(DISTINCT product_id) AS unique_products
FROM sales;
```

Unique cities:

```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customers;
```

---

# 36. Conditional Aggregation

Conditional aggregation means using conditions inside aggregate calculations.

The most common method is:

```text
CASE + Aggregate Function
```

Example:

```sql
SELECT
    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees;
```

This counts employees earning at least 60,000.

---

# 37. COUNT with CASE

```sql
SELECT
    COUNT(
        CASE
            WHEN salary >= 60000 THEN 1
        END
    ) AS high_salary_employees
FROM employees;
```

Why does this work?

`COUNT(expression)` ignores NULL.

So:

```text
Condition TRUE
    ↓
1
    ↓
COUNT()

Condition FALSE
    ↓
NULL
    ↓
COUNT() ignores it
```

---

# 38. SUM with CASE

Another common pattern:

```sql
SELECT
    SUM(
        CASE
            WHEN department = 'IT' THEN 1
            ELSE 0
        END
    ) AS it_employees
FROM employees;
```

---

# 39. Multiple Conditional Aggregates

You can calculate multiple metrics at once.

```sql
SELECT
    COUNT(*) AS total_employees,

    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees,

    SUM(
        CASE
            WHEN salary < 60000 THEN 1
            ELSE 0
        END
    ) AS low_salary_employees
FROM employees;
```

This is very useful for dashboards.

---

# 40. Conditional Aggregation by Group

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count

FROM employees
GROUP BY department;
```

This answers:

> How many high-salary employees does each department have?

---

# 41. Calculating Percentages with Aggregates

Suppose you want the percentage of employees earning at least 60,000.

```sql
SELECT
    100.0 *
    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    )
    / NULLIF(COUNT(*), 0) AS percentage_high_salary
FROM employees;
```

`NULLIF()` protects the denominator from being zero.

---

# 42. Aggregate Functions and NULL

Most aggregate functions ignore NULL values.

For example:

```text
salary
------
50000
60000
NULL
70000
```

Then:

```sql
SELECT SUM(salary)
FROM employees;
```

calculates:

```text
50000 + 60000 + 70000
```

not:

```text
50000 + 60000 + 0 + 70000
```

For `SUM()`, the result is effectively the same as treating NULL as absent, but conceptually NULL is not converted to zero.

---

# 43. NULL and COUNT()

This distinction is especially important:

```sql
SELECT COUNT(*)
FROM employees;
```

Counts all rows.

```sql
SELECT COUNT(salary)
FROM employees;
```

Counts only non-NULL salary values.

---

# 44. NULL and AVG()

Suppose:

```text
10
20
NULL
30
```

Then:

```sql
SELECT AVG(value)
FROM table_name;
```

calculates:

```text
(10 + 20 + 30) / 3
```

not:

```text
(10 + 20 + 0 + 30) / 4
```

---

# 45. NULL and MIN/MAX

`MIN()` and `MAX()` generally ignore NULL values.

Example:

```text
10
20
NULL
30
```

Then:

```text
MIN() → 10
MAX() → 30
```

---

# 46. What Happens When All Values Are NULL?

For functions such as:

```text
SUM()
AVG()
MIN()
MAX()
```

if there are no non-NULL values, the result is generally `NULL`.

Example:

```sql
SELECT SUM(salary)
FROM employees
WHERE department = 'Unknown';
```

If no matching rows exist, the result may be `NULL`.

You can use `COALESCE()`:

```sql
SELECT COALESCE(SUM(salary), 0) AS total_salary
FROM employees
WHERE department = 'Unknown';
```

Result:

```text
0
```

---

# 47. Aggregate Functions with Expressions

You can aggregate calculated expressions.

Example:

```sql
SELECT
    SUM(quantity * price) AS total_revenue
FROM sales;
```

You don't need to create a separate column for:

```text
quantity × price
```

---

# 48. SUM of Calculated Values

```sql
SELECT
    SUM(revenue - cost) AS total_profit
FROM sales;
```

This calculates total profit.

---

# 49. AVG of Calculated Values

```sql
SELECT
    AVG(revenue - cost) AS average_profit
FROM sales;
```

---

# 50. MIN/MAX of Expressions

```sql
SELECT
    MIN(price * quantity) AS minimum_order_value,
    MAX(price * quantity) AS maximum_order_value
FROM sales;
```

---

# 51. Aggregate Functions with CASE

You can use `CASE` inside any appropriate aggregate.

Example:

```sql
SELECT
    MAX(
        CASE
            WHEN department = 'IT' THEN salary
        END
    ) AS highest_it_salary
FROM employees;
```

---

# 52. Finding the Average by Category

```sql
SELECT
    department,
    ROUND(AVG(salary), 2) AS avg_salary
FROM employees
GROUP BY department;
```

This is one of the most common data-analysis patterns.

---

# 53. Finding the Highest Salary by Department

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

# 54. Finding the Lowest Salary by Department

```sql
SELECT
    department,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

---

# 55. Finding Total Salary by Department

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

---

# 56. Finding Employee Count by Department

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

---

# 57. Complete Department Summary

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    ROUND(AVG(salary), 2) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```

This is an excellent example to remember for data analytics.

---

# 58. Aggregate Functions with Multiple Groups

Suppose the table contains:

```text
department
gender
salary
```

You can calculate average salary by department and gender:

```sql
SELECT
    department,
    gender,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department, gender;
```

Grouping happens by the combination of both columns.

---

# 59. Aggregate Functions and Joins

Aggregate functions are frequently used after joining tables.

Example:

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spending
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name;
```

This calculates customer-level spending.

---

# 60. Aggregate Functions with LEFT JOIN

Suppose some customers have no orders.

A `LEFT JOIN` can preserve those customers:

```sql
SELECT
    c.customer_id,
    c.name,
    COALESCE(SUM(o.amount), 0) AS total_spending
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name;
```

`COALESCE()` converts a NULL total into zero.

This is a very useful analytics pattern.

---

# 61. Aggregate Functions in Subqueries

Example:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

This finds employees earning more than the overall average salary.

Conceptually:

```text
Inner query
    ↓
AVG(salary)
    ↓
Overall average
    ↓
Outer query
    ↓
Employees above average
```

---

# 62. Aggregate Functions with CTEs

A Common Table Expression can make complex analytics easier to read.

```sql
WITH department_stats AS (
    SELECT
        department,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM department_stats
WHERE average_salary > 60000;
```

---

# 63. Aggregate Functions vs Window Functions

This distinction is extremely important.

### Aggregate

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

Result:

```text
department | avg_salary
-----------|-----------
IT         | 67500
HR         | 52500
Finance    | 75000
```

Rows are collapsed into groups.

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

Every employee remains in the result.

Remember:

```text
Aggregate + GROUP BY
        ↓
Reduces rows

Window Function
        ↓
Keeps rows
```

---

# 64. Aggregate Functions vs Scalar Functions

### Scalar function

Works on individual values/rows.

```sql
SELECT UPPER(name)
FROM employees;
```

One transformed result per row.

### Aggregate function

Works across multiple rows.

```sql
SELECT AVG(salary)
FROM employees;
```

One summarized result.

Remember:

```text
Scalar
→ row-level transformation

Aggregate
→ group/table-level summarization
```

---

# 65. Aggregate Functions in Data Analytics

Aggregate functions help answer questions such as:

### Customers

```text
How many customers do we have?
How much does each customer spend?
What is the average order value?
```

### Sales

```text
What is total revenue?
What is average revenue?
What is the highest sale?
What is the lowest sale?
```

### Employees

```text
How many employees are there?
What is the average salary?
Which department has the highest salary?
What is the total salary expense?
```

### Products

```text
How many products were sold?
What is total quantity sold?
What is average price?
What is maximum sales?
```

---

# 66. KPI Calculations

Aggregate functions are commonly used to create KPIs.

Examples:

```text
Total Revenue
Average Order Value
Number of Customers
Number of Orders
Total Units Sold
Maximum Transaction
Minimum Transaction
Average Transaction
```

Example:

```sql
SELECT
    SUM(amount) AS total_revenue,
    COUNT(*) AS total_orders,
    COUNT(DISTINCT customer_id) AS total_customers,
    AVG(amount) AS average_order_value
FROM orders;
```

---

# 67. Important Aggregate Patterns

### Total

```sql
SELECT SUM(amount)
FROM orders;
```

### Average

```sql
SELECT AVG(amount)
FROM orders;
```

### Count

```sql
SELECT COUNT(*)
FROM orders;
```

### Unique count

```sql
SELECT COUNT(DISTINCT customer_id)
FROM orders;
```

### Minimum

```sql
SELECT MIN(amount)
FROM orders;
```

### Maximum

```sql
SELECT MAX(amount)
FROM orders;
```

### Group summary

```sql
SELECT
    category,
    SUM(amount)
FROM orders
GROUP BY category;
```

### Filter groups

```sql
SELECT
    category,
    SUM(amount)
FROM orders
GROUP BY category
HAVING SUM(amount) > 100000;
```

---

# 68. Common Mistakes

## Mistake 1 — Using aggregate in WHERE

Incorrect:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE AVG(salary) > 60000
GROUP BY department;
```

Use `HAVING`:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 69. Mistake 2 — Selecting Non-Grouped Columns

This is generally invalid:

```sql
SELECT
    department,
    name,
    AVG(salary)
FROM employees
GROUP BY department;
```

Why?

Because multiple employees can exist within one department, so SQL cannot determine which `name` should be returned.

Use:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Or aggregate/group the additional information appropriately.

---

# 70. Mistake 3 — Confusing COUNT(*) and COUNT(column)

Remember:

```text
COUNT(*) 
→ rows

COUNT(column)
→ non-NULL column values
```

---

# 71. Mistake 4 — Treating NULL as Zero

`NULL` does not automatically mean zero.

Bad assumption:

```text
NULL = 0
```

They are different concepts.

Use:

```sql
COALESCE(column, 0)
```

when you explicitly want to replace missing values with zero.

---

# 72. Mistake 5 — Forgetting DISTINCT

If the requirement is:

> Count unique customers

Don't use:

```sql
COUNT(customer_id)
```

Use:

```sql
COUNT(DISTINCT customer_id)
```

---

# 73. Execution Concept

For a typical grouped aggregate query:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary > 40000
GROUP BY department
HAVING AVG(salary) > 60000
ORDER BY average_salary DESC;
```

A useful conceptual processing order is:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
Aggregate calculations
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY
```

This helps understand why `WHERE` and `HAVING` are different.

---

# 74. Aggregate Functions Cheat Sheet

```text
COUNT(*)
    → Number of rows

COUNT(column)
    → Number of non-NULL values

COUNT(DISTINCT column)
    → Number of unique non-NULL values

SUM(column)
    → Total

AVG(column)
    → Average

MIN(column)
    → Minimum

MAX(column)
    → Maximum
```

---

# 75. Complete Aggregate Query Template

```sql
SELECT
    group_column,

    COUNT(*) AS total_rows,

    COUNT(DISTINCT unique_column) AS unique_count,

    SUM(numeric_column) AS total_value,

    AVG(numeric_column) AS average_value,

    MIN(numeric_column) AS minimum_value,

    MAX(numeric_column) AS maximum_value

FROM table_name

WHERE condition

GROUP BY group_column

HAVING AVG(numeric_column) > value

ORDER BY average_value DESC;
```

Not every clause is required; add them according to the problem.

---

# 76. Interview/Revision Questions

### Q1. What are aggregate functions?

Functions that summarize multiple rows and return a result for a table or group.

### Q2. Name the five major aggregate functions.

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

### Q3. Difference between COUNT(*) and COUNT(column)?

```text
COUNT(*)      → counts rows
COUNT(column) → counts non-NULL values
```

### Q4. What is COUNT(DISTINCT)?

Counts unique non-NULL values.

### Q5. Can aggregate functions be used with GROUP BY?

Yes.

### Q6. WHERE or HAVING for filtering aggregate results?

`HAVING`.

### Q7. Do aggregate functions generally ignore NULL?

Yes, for the standard aggregate behavior of `SUM`, `AVG`, `MIN`, and `MAX`; `COUNT(*)` counts rows, while `COUNT(column)` ignores NULL.

### Q8. Can aggregate functions be used without GROUP BY?

Yes.

```sql
SELECT AVG(salary)
FROM employees;
```

### Q9. Can aggregate functions be used with JOIN?

Yes, and this is extremely common in analytics.

### Q10. What is conditional aggregation?

Using conditions, usually `CASE`, inside aggregate functions to calculate conditional metrics.

---

# 77. Final Revision Map

```text
                 AGGREGATE FUNCTIONS
                         │
        ┌────────────────┼────────────────┐
        │                │                │
      COUNT             SUM              AVG
        │                │                │
    COUNT(*)       Total value        Average
    COUNT(col)
    COUNT(DISTINCT)
        │
        └────────────────┬────────────────┐
                         │                │
                       MIN              MAX
                         │                │
                    Minimum value    Maximum value


                    WITH GROUP BY
                         │
                         ↓
                  Group-wise analysis
                         │
                         ↓
                      HAVING
                         │
                         ↓
                   Filter groups


                 ADVANCED ANALYTICS
                         │
              ┌──────────┼──────────┐
              │          │          │
             CASE     DISTINCT     JOIN
              │          │          │
              └──────────┼──────────┘
                         ↓
               Conditional Metrics
                         ↓
                    KPI / Reports
```

---

# 78. Most Important Things to Remember

```text
1. COUNT() → counting
2. SUM()   → total
3. AVG()   → average
4. MIN()   → minimum
5. MAX()   → maximum

6. GROUP BY → perform aggregation per group

7. HAVING → filter aggregated groups

8. WHERE → filter rows before aggregation

9. COUNT(*) → counts rows

10. COUNT(column) → counts non-NULL values

11. COUNT(DISTINCT column) → counts unique values

12. Aggregate functions generally ignore NULL values

13. COALESCE() can replace NULL with a chosen value

14. CASE + aggregate = conditional aggregation

15. Aggregate + GROUP BY reduces rows

16. Window functions calculate across rows while preserving them

17. Aggregate functions are fundamental to SQL data analytics.
```

---

# 79. One Query That Combines Everything

A useful revision example:

```sql
SELECT
    department,

    COUNT(*) AS employee_count,

    COUNT(DISTINCT name) AS unique_employee_names,

    SUM(salary) AS total_salary,

    ROUND(AVG(salary), 2) AS average_salary,

    MIN(salary) AS minimum_salary,

    MAX(salary) AS maximum_salary,

    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count

FROM employees

WHERE age >= 25

GROUP BY department

HAVING AVG(salary) >= 50000

ORDER BY average_salary DESC;
```

This one query demonstrates the core concepts:

```text
COUNT()
COUNT(DISTINCT)
SUM()
AVG()
ROUND()
MIN()
MAX()
CASE
WHERE
GROUP BY
HAVING
ORDER BY
```

For **SQL + Data Analytics**, mastering this pattern is extremely important.
