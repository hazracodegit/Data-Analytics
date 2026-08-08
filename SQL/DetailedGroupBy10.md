# SQL GROUP BY — Complete Guide

`GROUP BY` is one of the most important SQL concepts for **data analytics, reporting, aggregation, and business intelligence**.

It is used to:

* Divide rows into groups
* Perform calculations for each group
* Generate summaries
* Analyze data category-wise
* Calculate KPIs
* Compare groups
* Work with aggregate functions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`

---

# 1. What is GROUP BY?

`GROUP BY` groups rows that have the same value in one or more columns.

### Basic syntax

```sql
SELECT column_name, aggregate_function(column)
FROM table_name
GROUP BY column_name;
```

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Instead of getting every employee separately, SQL creates one group for each department.

---

# 2. Why Do We Need GROUP BY?

Suppose we have:

| employee | department | salary |
| -------- | ---------- | -----: |
| Rahul    | IT         |  60000 |
| Priya    | IT         |  75000 |
| Arun     | HR         |  50000 |
| Sneha    | HR         |  55000 |
| Kiran    | Finance    |  80000 |
| Anil     | Finance    |  70000 |

If we want:

> How many employees are in each department?

We need `GROUP BY`.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Result:

| department | employee_count |
| ---------- | -------------: |
| IT         |              2 |
| HR         |              2 |
| Finance    |              2 |

---

# 3. GROUP BY Without Aggregate Functions

Technically, `GROUP BY` can be used without an aggregate function in some SQL situations, but its most important purpose is **group-wise aggregation**.

For finding unique combinations, `DISTINCT` is usually clearer.

For example:

```sql
SELECT department
FROM employees
GROUP BY department;
```

This can return:

```text
IT
HR
Finance
```

But for simply finding unique values, prefer:

```sql
SELECT DISTINCT department
FROM employees;
```

---

# 4. GROUP BY with COUNT()

Count employees in each department:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Result:

| department | employee_count |
| ---------- | -------------: |
| Finance    |              2 |
| HR         |              2 |
| IT         |              2 |

The exact output order is not guaranteed unless `ORDER BY` is used.

---

# 5. GROUP BY with SUM()

Calculate total salary for each department:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

Result:

| department | total_salary |
| ---------- | -----------: |
| IT         |       135000 |
| HR         |       105000 |
| Finance    |       150000 |

---

# 6. GROUP BY with AVG()

Calculate average salary per department:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

Result:

| department | average_salary |
| ---------- | -------------: |
| IT         |          67500 |
| HR         |          52500 |
| Finance    |          75000 |

---

# 7. GROUP BY with MIN()

Find the minimum salary in each department:

```sql
SELECT
    department,
    MIN(salary) AS minimum_salary
FROM employees
GROUP BY department;
```

---

# 8. GROUP BY with MAX()

Find the maximum salary in each department:

```sql
SELECT
    department,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```

---

# 9. Multiple Aggregate Functions

You can use several aggregate functions together.

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

This produces a complete department-level summary.

---

# 10. How GROUP BY Works

Suppose the data is:

```text
IT       60000
IT       75000
HR       50000
HR       55000
Finance  80000
Finance  70000
```

SQL conceptually creates:

```text
IT
 ├── 60000
 └── 75000

HR
 ├── 50000
 └── 55000

Finance
 ├── 80000
 └── 70000
```

Then the aggregate function works separately on each group.

For example:

```text
IT
→ AVG(60000, 75000)
→ 67500

HR
→ AVG(50000, 55000)
→ 52500

Finance
→ AVG(80000, 70000)
→ 75000
```

---

# 11. GROUP BY and Data Granularity

`GROUP BY` changes the **granularity** of your result.

Original data:

```text
One row = one employee
```

After:

```sql
GROUP BY department
```

The result becomes:

```text
One row = one department
```

This idea of **granularity** is extremely important in data analytics.

Examples:

```text
GROUP BY customer_id
→ one row per customer

GROUP BY product_id
→ one row per product

GROUP BY department
→ one row per department

GROUP BY city
→ one row per city

GROUP BY date
→ one row per date
```

---

# 12. GROUP BY One Column

Basic example:

```sql
SELECT
    department,
    COUNT(*) AS employees
FROM employees
GROUP BY department;
```

Here there is only one grouping column:

```text
department
```

---

# 13. GROUP BY Multiple Columns

You can group by multiple columns.

Syntax:

```sql
SELECT
    column1,
    column2,
    aggregate_function(column3)
FROM table_name
GROUP BY column1, column2;
```

Example:

```sql
SELECT
    department,
    gender,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department, gender;
```

Now SQL creates groups based on:

```text
department + gender
```

---

# 14. How Multiple GROUP BY Columns Work

Suppose:

| department | gender |
| ---------- | ------ |
| IT         | Male   |
| IT         | Female |
| IT         | Male   |
| HR         | Female |
| HR         | Male   |
| HR         | Female |

Grouping by:

```sql
GROUP BY department, gender
```

creates groups such as:

```text
IT + Male
IT + Female
HR + Male
HR + Female
```

Each combination is treated as a separate group.

---

# 15. GROUP BY Three or More Columns

You can group using multiple columns.

```sql
SELECT
    department,
    gender,
    city,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    department,
    gender,
    city;
```

Groups are based on the complete combination:

```text
department + gender + city
```

Be careful: adding more grouping columns usually creates **more detailed/smaller groups**.

---

# 16. GROUP BY with WHERE

`WHERE` filters rows **before grouping**.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary >= 50000
GROUP BY department;
```

Conceptually:

```text
All employees
      ↓
WHERE salary >= 50000
      ↓
Remaining employees
      ↓
GROUP BY department
      ↓
AVG(salary)
```

---

# 17. WHERE vs GROUP BY

### WHERE

Filters individual rows.

```sql
WHERE salary > 50000
```

### GROUP BY

Creates groups.

```sql
GROUP BY department
```

Together:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE salary > 50000
GROUP BY department;
```

---

# 18. GROUP BY with HAVING

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

This means:

1. Create department groups
2. Calculate average salary
3. Keep only departments where average salary > 60000

---

# 19. WHERE vs HAVING

This is one of the most important SQL concepts.

### WHERE

```sql
WHERE salary > 50000
```

Filters rows.

### HAVING

```sql
HAVING AVG(salary) > 60000
```

Filters groups.

Remember:

```text
WHERE
↓
Rows

GROUP BY
↓
Groups

HAVING
↓
Groups after aggregation
```

---

# 20. GROUP BY + WHERE + HAVING

You can use both.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE age >= 25
GROUP BY department
HAVING AVG(salary) > 60000;
```

Meaning:

```text
1. Keep employees age >= 25
2. Group them by department
3. Calculate average salary
4. Keep departments with average salary > 60000
```

---

# 21. GROUP BY with ORDER BY

You can sort grouped results.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```

Result will be ordered from highest average salary to lowest.

---

# 22. ORDER BY Aggregate Function

You can also write:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY AVG(salary) DESC;
```

Both approaches are commonly supported.

Using the alias is usually cleaner:

```sql
ORDER BY average_salary DESC;
```

---

# 23. GROUP BY with LIMIT

You can find the top groups.

Example:

> Find the top 3 departments by total salary.

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC
LIMIT 3;
```

`LIMIT` syntax differs between database systems.

---

# 24. GROUP BY with DISTINCT

`DISTINCT` and `GROUP BY` can sometimes produce similar results when no aggregate is involved.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

Similar:

```sql
SELECT department
FROM employees
GROUP BY department;
```

But their purposes are different.

### DISTINCT

Used mainly to remove duplicate result rows.

### GROUP BY

Used mainly to create groups for aggregation.

Prefer:

```sql
SELECT DISTINCT department
FROM employees;
```

when you simply need unique departments.

---

# 25. GROUP BY and NULL

`NULL` values are grouped together.

Suppose:

| department |
| ---------- |
| IT         |
| IT         |
| HR         |
| NULL       |
| NULL       |

Then:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

The NULL values form their own group.

Conceptually:

```text
IT       → 2
HR       → 1
NULL     → 2
```

---

# 26. GROUP BY with NULL

If you want to display a meaningful label instead of NULL:

```sql
SELECT
    COALESCE(department, 'Unknown') AS department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY COALESCE(department, 'Unknown');
```

Result may look like:

```text
IT       → 2
HR       → 1
Unknown  → 2
```

---

# 27. GROUP BY and COUNT(*)

One of the most common patterns:

```sql
SELECT
    department,
    COUNT(*) AS count
FROM employees
GROUP BY department;
```

This answers:

> How many rows belong to each department?

---

# 28. GROUP BY and COUNT(column)

Consider:

```sql
SELECT
    department,
    COUNT(manager_id) AS manager_count
FROM employees
GROUP BY department;
```

`COUNT(manager_id)` counts only non-NULL `manager_id` values within each department.

This differs from:

```sql
COUNT(*)
```

which counts all rows.

---

# 29. GROUP BY and COUNT(DISTINCT)

Very common in analytics.

Example:

```sql
SELECT
    department,
    COUNT(DISTINCT city) AS city_count
FROM employees
GROUP BY department;
```

This answers:

> How many unique cities have employees in each department?

---

# 30. GROUP BY with SUM

Example sales table:

```text
product_category | sales
-----------------|------
Electronics      | 1000
Electronics      | 2000
Clothing         | 500
Clothing         | 700
```

Query:

```sql
SELECT
    product_category,
    SUM(sales) AS total_sales
FROM sales
GROUP BY product_category;
```

Result:

```text
Electronics → 3000
Clothing    → 1200
```

---

# 31. GROUP BY in Sales Analytics

A typical analytics query:

```sql
SELECT
    product_category,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY product_category
ORDER BY total_revenue DESC;
```

This identifies the best-performing categories.

---

# 32. GROUP BY by Customer

Find total spending for every customer:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id;
```

Result:

```text
customer_id | total_spending
------------|---------------
101         | 5000
102         | 7200
103         | 3100
```

This changes the granularity from:

```text
one row per order
```

to:

```text
one row per customer
```

---

# 33. GROUP BY by Product

Find the number of units sold per product:

```sql
SELECT
    product_id,
    SUM(quantity) AS total_quantity
FROM sales
GROUP BY product_id;
```

---

# 34. GROUP BY by City

```sql
SELECT
    city,
    COUNT(*) AS customer_count
FROM customers
GROUP BY city;
```

This tells you how many customers belong to each city.

---

# 35. GROUP BY by Date

Suppose an orders table has:

```text
order_date
amount
```

You may want daily revenue.

```sql
SELECT
    order_date,
    SUM(amount) AS daily_revenue
FROM orders
GROUP BY order_date
ORDER BY order_date;
```

Result:

```text
date        | daily_revenue
------------|--------------
2026-01-01  | 25000
2026-01-02  | 31000
2026-01-03  | 28000
```

---

# 36. GROUP BY Month

The exact syntax depends on the database.

For databases supporting `EXTRACT()`:

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(amount) AS total_sales
FROM orders
GROUP BY
    EXTRACT(YEAR FROM order_date),
    EXTRACT(MONTH FROM order_date)
ORDER BY year, month;
```

Grouping by both year and month prevents January from different years being combined.

---

# 37. GROUP BY Year

Example:

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    SUM(amount) AS yearly_sales
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date)
ORDER BY year;
```

This provides yearly sales trends.

---

# 38. GROUP BY with Calculated Columns

You can group by expressions.

Example:

```sql
SELECT
    CASE
        WHEN salary < 50000 THEN 'Low'
        WHEN salary < 70000 THEN 'Medium'
        ELSE 'High'
    END AS salary_category,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    CASE
        WHEN salary < 50000 THEN 'Low'
        WHEN salary < 70000 THEN 'Medium'
        ELSE 'High'
    END;
```

This creates salary categories.

---

# 39. GROUP BY with CASE

This is very useful for analytics.

```sql
SELECT
    CASE
        WHEN age < 25 THEN 'Young'
        WHEN age < 35 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    CASE
        WHEN age < 25 THEN 'Young'
        WHEN age < 35 THEN 'Adult'
        ELSE 'Senior'
    END;
```

---

# 40. Conditional Aggregation with GROUP BY

You can combine `GROUP BY` with conditional aggregation.

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count,

    SUM(
        CASE
            WHEN salary < 60000 THEN 1
            ELSE 0
        END
    ) AS low_salary_count

FROM employees

GROUP BY department;
```

This creates multiple metrics for every department.

---

# 41. GROUP BY with Percentage

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    100.0 * COUNT(*) /
        SUM(COUNT(*)) OVER () AS percentage_of_employees
FROM employees
GROUP BY department;
```

This combines grouping with a window function.

Conceptually:

```text
GROUP BY
    ↓
department counts
    ↓
window calculation
    ↓
percentage of total
```

---

# 42. GROUP BY with JOIN

`GROUP BY` is extremely common after joining tables.

Suppose:

```text
customers
---------
customer_id
name

orders
------
order_id
customer_id
amount
```

Query:

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

This calculates total spending per customer.

---

# 43. GROUP BY with LEFT JOIN

If you want customers who have no orders too:

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

Customers without orders can appear with:

```text
total_spending = 0
```

---

# 44. GROUP BY and Duplicate Rows After JOIN

This is an important analytics issue.

Suppose a join creates multiple rows for the same business entity.

Then:

```sql
SUM()
COUNT()
AVG()
```

can produce unexpected results if the join multiplies rows.

Always understand the relationship between tables before aggregating.

For example:

```text
Customer
   ↓
Multiple Orders
   ↓
Multiple Order Items
```

Joining all three can multiply rows.

---

# 45. GROUP BY with Subquery

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) >
       (
           SELECT AVG(salary)
           FROM employees
       );
```

This finds departments whose average salary is greater than the company-wide average.

---

# 46. GROUP BY with CTE

CTEs make analytical queries easier to understand.

```sql
WITH department_summary AS (
    SELECT
        department,
        COUNT(*) AS employee_count,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM department_summary
WHERE average_salary > 60000;
```

---

# 47. GROUP BY and Window Functions

Do not confuse these concepts.

### GROUP BY

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

Employee rows are collapsed.

### Window Function

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

Every employee remains visible.

### Key difference

```text
GROUP BY
→ Reduces rows

PARTITION BY
→ Does not reduce rows
```

---

# 48. GROUP BY vs PARTITION BY

| GROUP BY                          | PARTITION BY                             |
| --------------------------------- | ---------------------------------------- |
| Used for aggregation              | Used with window functions               |
| Usually reduces rows              | Keeps original rows                      |
| Produces group-level results      | Produces row-level + group-level results |
| Common with `COUNT`, `SUM`, `AVG` | Common with `SUM() OVER`, `AVG() OVER`   |
| Useful for summaries              | Useful for comparisons                   |

---

# 49. GROUP BY vs DISTINCT

| GROUP BY                      | DISTINCT                       |
| ----------------------------- | ------------------------------ |
| Creates groups                | Removes duplicate result rows  |
| Commonly used with aggregates | Usually used for unique values |
| Used for analysis             | Used for deduplication         |
| Supports `HAVING`             | Does not use `HAVING`          |
| Changes result granularity    | Removes duplicate combinations |

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

vs:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department;
```

The second query provides actual group-level analysis.

---

# 50. GROUP BY Execution Order

Consider:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE age >= 25
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

This explains why:

```sql
WHERE AVG(salary) > 60000
```

is generally invalid.

The aggregate has not yet been calculated at the `WHERE` stage.

Instead:

```sql
HAVING AVG(salary) > 60000
```

is used.

---

# 51. SELECT and GROUP BY Rule

A very important SQL rule:

When using `GROUP BY`, a selected column generally must either:

1. Be included in the `GROUP BY`, or
2. Be wrapped in an aggregate function

Example:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Valid.

But:

```sql
SELECT
    department,
    name,
    AVG(salary)
FROM employees
GROUP BY department;
```

is generally invalid because `name` is neither grouped nor aggregated.

---

# 52. Correcting the Previous Query

If you want employee names, you need a different approach depending on your goal.

For example, if you only want department summary:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

If you need the highest-paid employee per department, use a suitable window-function or ranking approach rather than arbitrarily selecting `name`.

---

# 53. GROUP BY Aliases

Whether you can use a `SELECT` alias in `GROUP BY` depends on the SQL database.

For maximum portability, this is clear:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

The grouped column is directly referenced.

For expressions, database behavior can differ, so avoid relying on alias behavior when writing portable SQL.

---

# 54. GROUP BY Ordinal Positions

Some SQL systems allow:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY 1;
```

Here `1` refers to the first selected expression.

Although supported in some databases, it is generally clearer to write:

```sql
GROUP BY department;
```

because it is easier to read and maintain.

---

# 55. GROUP BY and HAVING Without SELECT Alias

For maximum compatibility, use the aggregate expression:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Some databases allow:

```sql
HAVING average_salary > 60000
```

but alias support differs.

---

# 56. GROUP BY with COUNT and HAVING

Find departments having more than 5 employees:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

This is a very common interview and analytics pattern.

---

# 57. GROUP BY with SUM and HAVING

Find categories with total sales above 100,000:

```sql
SELECT
    category,
    SUM(sales) AS total_sales
FROM sales
GROUP BY category
HAVING SUM(sales) > 100000;
```

---

# 58. GROUP BY with AVG and HAVING

Find departments where average salary exceeds 60,000:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 59. GROUP BY with MIN and HAVING

For example:

```sql
SELECT
    department,
    MIN(salary) AS minimum_salary
FROM employees
GROUP BY department
HAVING MIN(salary) >= 40000;
```

---

# 60. GROUP BY with MAX and HAVING

```sql
SELECT
    department,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department
HAVING MAX(salary) > 90000;
```

---

# 61. Nested Aggregation

Sometimes you need to aggregate an already aggregated result.

Example:

> Find the average of department-level average salaries.

A subquery can be used:

```sql
SELECT AVG(department_average)
FROM (
    SELECT
        department,
        AVG(salary) AS department_average
    FROM employees
    GROUP BY department
) AS department_summary;
```

Important:

```text
Employee-level data
       ↓
GROUP BY department
       ↓
Department averages
       ↓
AVG()
       ↓
Average of department averages
```

Note that this is **not necessarily the same** as the overall employee average because departments may have different numbers of employees.

---

# 62. Weighted vs Unweighted Averages

This is very important in data analytics.

Suppose:

```text
Department A
100 employees
Average salary = 50000

Department B
2 employees
Average salary = 100000
```

The average of department averages is:

```text
(50000 + 100000) / 2
= 75000
```

But the overall employee average is:

```text
(100 × 50000 + 2 × 100000) / 102
```

which is very different.

Therefore:

> Be careful when aggregating averages.

---

# 63. GROUP BY for Data Analytics

`GROUP BY` is fundamental to exploratory data analysis.

You can use it to analyze:

### Customers

```sql
SELECT
    city,
    COUNT(*) AS customers
FROM customers
GROUP BY city;
```

### Sales

```sql
SELECT
    category,
    SUM(amount) AS revenue
FROM sales
GROUP BY category;
```

### Employees

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

### Products

```sql
SELECT
    product_id,
    SUM(quantity) AS units_sold
FROM sales
GROUP BY product_id;
```

---

# 64. GROUP BY for EDA

During exploratory data analysis, common questions are:

```text
How many records are in each category?
What is the average value by category?
Which category has the highest sales?
Which region has the most customers?
What is the total revenue by month?
Which product sells the most?
```

Most of these questions can be solved using:

```text
GROUP BY
+
Aggregate Functions
```

---

# 65. Common GROUP BY Analytics Patterns

### Count by category

```sql
SELECT
    category,
    COUNT(*) AS count
FROM table_name
GROUP BY category;
```

### Sum by category

```sql
SELECT
    category,
    SUM(amount) AS total
FROM table_name
GROUP BY category;
```

### Average by category

```sql
SELECT
    category,
    AVG(amount) AS average
FROM table_name
GROUP BY category;
```

### Maximum by category

```sql
SELECT
    category,
    MAX(amount) AS maximum
FROM table_name
GROUP BY category;
```

### Minimum by category

```sql
SELECT
    category,
    MIN(amount) AS minimum
FROM table_name
GROUP BY category;
```

---

# 66. Complete Analytics Example

Suppose we have:

```text
sales
-----
order_id
customer_id
product_id
category
region
quantity
revenue
order_date
```

We want to know:

> Revenue, order count, customer count, and quantity sold by region.

Query:

```sql
SELECT
    region,
    COUNT(*) AS order_count,
    COUNT(DISTINCT customer_id) AS customer_count,
    SUM(quantity) AS units_sold,
    SUM(revenue) AS total_revenue,
    AVG(revenue) AS average_order_value
FROM sales
GROUP BY region
ORDER BY total_revenue DESC;
```

This is a realistic data-analytics query.

---

# 67. GROUP BY for KPI Reporting

A dashboard might require:

```text
Region
Total Revenue
Total Orders
Unique Customers
Average Order Value
Units Sold
```

SQL:

```sql
SELECT
    region,
    SUM(revenue) AS total_revenue,
    COUNT(*) AS total_orders,
    COUNT(DISTINCT customer_id) AS unique_customers,
    AVG(revenue) AS average_order_value,
    SUM(quantity) AS total_units
FROM sales
GROUP BY region;
```

---

# 68. Common Mistakes

## Mistake 1: Forgetting GROUP BY

Incorrect:

```sql
SELECT
    department,
    AVG(salary)
FROM employees;
```

If you want an average for every department:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

---

# 69. Mistake 2: Using WHERE for Aggregate Filtering

Incorrect:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
WHERE AVG(salary) > 60000
GROUP BY department;
```

Correct:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 70. Mistake 3: Selecting an Un-grouped Column

Incorrect:

```sql
SELECT
    department,
    name,
    COUNT(*)
FROM employees
GROUP BY department;
```

`name` is not grouped or aggregated.

---

# 71. Mistake 4: Grouping at the Wrong Granularity

Suppose you need:

```text
monthly sales
```

but group by:

```sql
GROUP BY order_id;
```

That gives order-level results instead of monthly results.

Always ask:

> What should one output row represent?

For example:

```text
One row per customer
→ GROUP BY customer_id

One row per product
→ GROUP BY product_id

One row per region
→ GROUP BY region

One row per month
→ GROUP BY month expression
```

---

# 72. Mistake 5: Grouping by Too Many Columns

Suppose:

```sql
GROUP BY department, name, employee_id;
```

If each employee is unique, the result becomes almost one row per employee.

That defeats the purpose of department-level aggregation.

Remember:

```text
More GROUP BY columns
→ More detailed groups
→ More rows
```

---

# 73. Mistake 6: Ignoring NULL

If a grouping column contains NULL:

```sql
GROUP BY department
```

NULL values form their own group.

Don't assume NULL means:

```text
Unknown
Not applicable
Zero
Empty string
```

They are different concepts.

---

# 74. Mistake 7: Incorrect JOIN Before GROUP BY

If a JOIN duplicates rows, aggregation can produce inflated numbers.

Always verify:

```text
What is the grain of each table?
What is the JOIN relationship?
Will the JOIN multiply rows?
```

before using:

```text
SUM()
COUNT()
AVG()
```

---

# 75. GROUP BY Mental Model

Think of `GROUP BY` as:

```text
Raw Data
   ↓
Choose grouping columns
   ↓
Create groups
   ↓
Apply aggregate functions
   ↓
One result row per group
```

Example:

```text
Employees
   ↓
GROUP BY department
   ↓
IT / HR / Finance
   ↓
COUNT / SUM / AVG
   ↓
Department summary
```

---

# 76. GROUP BY Cheat Sheet

```sql
-- Count rows per group
SELECT category, COUNT(*)
FROM table_name
GROUP BY category;
```

```sql
-- Total per group
SELECT category, SUM(amount)
FROM table_name
GROUP BY category;
```

```sql
-- Average per group
SELECT category, AVG(amount)
FROM table_name
GROUP BY category;
```

```sql
-- Minimum per group
SELECT category, MIN(amount)
FROM table_name
GROUP BY category;
```

```sql
-- Maximum per group
SELECT category, MAX(amount)
FROM table_name
GROUP BY category;
```

```sql
-- Filter rows before grouping
SELECT category, SUM(amount)
FROM table_name
WHERE amount > 100
GROUP BY category;
```

```sql
-- Filter groups after aggregation
SELECT category, SUM(amount)
FROM table_name
GROUP BY category
HAVING SUM(amount) > 10000;
```

```sql
-- Sort grouped results
SELECT category, SUM(amount) AS total
FROM table_name
GROUP BY category
ORDER BY total DESC;
```

```sql
-- Top groups
SELECT category, SUM(amount) AS total
FROM table_name
GROUP BY category
ORDER BY total DESC
LIMIT 5;
```

---

# 77. Most Important Difference

Memorize this:

```text
WHERE
→ Filters ROWS

GROUP BY
→ Creates GROUPS

HAVING
→ Filters GROUPS

ORDER BY
→ Sorts RESULT

LIMIT
→ Limits RESULT ROWS
```

Complete pattern:

```sql
SELECT
    group_column,
    aggregate_function(value_column) AS result
FROM table_name
WHERE row_condition
GROUP BY group_column
HAVING aggregate_function(value_column) > condition
ORDER BY result DESC
LIMIT 10;
```

---

# 78. GROUP BY Revision Questions

### 1. What is GROUP BY?

It groups rows with the same values so aggregate calculations can be performed separately for each group.

### 2. Why is GROUP BY important?

It is essential for summarizing and analyzing data by categories, customers, products, regions, dates, departments, etc.

### 3. Can GROUP BY work with aggregate functions?

Yes. This is its most common use.

### 4. What is the difference between WHERE and HAVING?

```text
WHERE  → filters rows
HAVING → filters groups
```

### 5. Can we group by multiple columns?

Yes.

```sql
GROUP BY department, gender;
```

### 6. What happens to NULL values in GROUP BY?

NULL values are grouped together.

### 7. Can GROUP BY be used with JOIN?

Yes, and it is extremely common in analytics.

### 8. Can GROUP BY be used with CASE?

Yes.

### 9. What does GROUP BY do to granularity?

It changes the result to one row per unique grouping combination.

### 10. GROUP BY vs window function?

```text
GROUP BY
→ collapses rows

Window function
→ keeps rows
```

---

# 79. Final Revision Diagram

```text
                         GROUP BY
                            │
             ┌──────────────┼──────────────┐
             │              │              │
          One Column    Multiple Columns   Expression
             │              │              │
       department      dept + gender     CASE/date
             │              │              │
             └──────────────┼──────────────┘
                            ↓
                         GROUPS
                            │
              ┌─────────────┼─────────────┐
              │             │             │
            COUNT          SUM           AVG
              │             │             │
              └─────────────┼─────────────┘
                            │
                       MIN / MAX
                            │
                            ↓
                     GROUP SUMMARY
                            │
              ┌─────────────┴─────────────┐
              ↓                           ↓
           HAVING                      ORDER BY
        Filter groups                Sort results
              │                           │
              └─────────────┬─────────────┘
                            ↓
                          LIMIT
                            ↓
                       Final Result
```

# 80. Final Things to Memorize

```text
GROUP BY = Group rows for analysis.

GROUP BY + COUNT()
→ Count per group

GROUP BY + SUM()
→ Total per group

GROUP BY + AVG()
→ Average per group

GROUP BY + MIN()
→ Minimum per group

GROUP BY + MAX()
→ Maximum per group

WHERE
→ Filters rows before grouping

HAVING
→ Filters groups after aggregation

ORDER BY
→ Sorts grouped results

GROUP BY multiple columns
→ Groups by combinations

COUNT(DISTINCT)
→ Counts unique values

GROUP BY changes result granularity.

Most important analytics question:
"What should one output row represent?"
```

### One-line memory trick

```text
WHERE → ROWS → GROUP BY → GROUPS → HAVING → SORT → LIMIT
```

This sequence is one of the most useful mental models for solving SQL analytics problems.
