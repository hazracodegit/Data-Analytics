# SQL Sorting and Limiting — Complete Guide

Sorting and limiting are used to control **the order and number of rows returned by a SQL query**.

They are especially important in:

* Data analysis
* Top-N analysis
* Ranking
* Reports
* Dashboards
* Pagination
* Finding highest/lowest values
* Finding recent records
* Finding the first/last records

---

# 1. Sorting and Limiting

Two major concepts:

```text
SORTING
    ↓
ORDER BY

LIMITING
    ↓
LIMIT
OFFSET
TOP
FETCH FIRST / FETCH NEXT
```

Syntax depends on the database system.

---

# 2. ORDER BY

`ORDER BY` is used to sort query results.

Basic syntax:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column_name;
```

By default, SQL sorts in:

```text
ASC → Ascending order
```

---

# 3. Ascending Order — ASC

Ascending means:

```text
Numbers:
Small → Large

Text:
A → Z

Dates:
Old → New
```

Example:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Example result:

```text
salary
------
30000
40000
50000
60000
80000
```

`ASC` is optional because it is the default in most SQL systems.

Therefore:

```sql
ORDER BY salary;
```

is generally equivalent to:

```sql
ORDER BY salary ASC;
```

---

# 4. Descending Order — DESC

Descending means:

```text
Numbers:
Large → Small

Text:
Z → A

Dates:
New → Old
```

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Result:

```text
salary
------
80000
60000
50000
40000
30000
```

---

# 5. ASC vs DESC

| Order  | Meaning    | Example    |
| ------ | ---------- | ---------- |
| `ASC`  | Ascending  | 1, 2, 3, 4 |
| `DESC` | Descending | 4, 3, 2, 1 |

---

# 6. Sorting Text

```sql
SELECT *
FROM employees
ORDER BY name ASC;
```

Example:

```text
Amit
Anita
John
Rahul
Zoya
```

Descending:

```sql
SELECT *
FROM employees
ORDER BY name DESC;
```

Result:

```text
Zoya
Rahul
John
Anita
Amit
```

Exact text ordering can depend on the database's collation and locale settings.

---

# 7. Sorting Dates

Oldest first:

```sql
SELECT *
FROM employees
ORDER BY joining_date ASC;
```

Newest first:

```sql
SELECT *
FROM employees
ORDER BY joining_date DESC;
```

For analytics, this is commonly used to find recent records:

```sql
SELECT *
FROM orders
ORDER BY order_date DESC;
```

---

# 8. Sorting by Multiple Columns

You can sort using multiple columns.

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

Meaning:

```text
1. Sort by department A → Z
2. Within each department,
   sort salary from high → low
```

---

# 9. How Multiple-Column Sorting Works

Suppose:

```text
department | salary
-----------|-------
IT         | 50000
IT         | 80000
HR         | 60000
HR         | 40000
Finance    | 70000
Finance    | 50000
```

Query:

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

Result:

```text
Finance    | 70000
Finance    | 50000
HR         | 60000
HR         | 40000
IT         | 80000
IT         | 50000
```

The second sorting column only breaks ties within the first sorting column.

---

# 10. Different Directions for Different Columns

You can specify `ASC` or `DESC` independently.

```sql
SELECT *
FROM employees
ORDER BY
    department ASC,
    salary DESC,
    name ASC;
```

Meaning:

```text
department → A to Z
salary     → High to Low
name       → A to Z
```

---

# 11. Sorting by Calculated Values

You can sort using an expression.

```sql
SELECT
    product,
    price,
    quantity,
    price * quantity AS revenue
FROM sales
ORDER BY revenue DESC;
```

This finds the products with the highest calculated revenue first.

---

# 12. Sorting by Expression Directly

You can also write:

```sql
SELECT
    product,
    price,
    quantity
FROM sales
ORDER BY price * quantity DESC;
```

---

# 13. Sorting by Column Alias

If you create an alias in `SELECT`, you can often use it in `ORDER BY`.

```sql
SELECT
    name,
    salary,
    salary * 12 AS annual_salary
FROM employees
ORDER BY annual_salary DESC;
```

This is cleaner than repeating the expression.

---

# 14. Sorting by Column Position

Some SQL systems allow:

```sql
SELECT
    name,
    salary,
    department
FROM employees
ORDER BY 2 DESC;
```

Here:

```text
1 → name
2 → salary
3 → department
```

Therefore, the query sorts by salary descending.

### Recommended

Prefer:

```sql
ORDER BY salary DESC;
```

rather than:

```sql
ORDER BY 2 DESC;
```

because column-position sorting is less readable and can break when the `SELECT` list changes.

---

# 15. ORDER BY with WHERE

`WHERE` filters rows first, and `ORDER BY` sorts the resulting rows.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Conceptually:

```text
employees
    ↓
WHERE department = 'IT'
    ↓
filtered rows
    ↓
ORDER BY salary DESC
    ↓
sorted result
```

---

# 16. ORDER BY with DISTINCT

```sql
SELECT DISTINCT department
FROM employees
ORDER BY department ASC;
```

This returns unique departments in alphabetical order.

---

# 17. ORDER BY with GROUP BY

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```

This sorts departments according to their average salary.

---

# 18. ORDER BY with Aggregate Functions

You can sort by aggregate results.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
ORDER BY employee_count DESC;
```

This gives departments with the most employees first.

---

# 19. ORDER BY with HAVING

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY average_salary DESC;
```

Conceptually:

```text
FROM
 ↓
GROUP BY
 ↓
HAVING
 ↓
ORDER BY
```

---

# 20. LIMIT

`LIMIT` restricts the number of rows returned.

Common syntax:

```sql
SELECT *
FROM employees
LIMIT 5;
```

This returns at most 5 rows.

`LIMIT` is commonly supported by MySQL, PostgreSQL, SQLite, and some other systems.

---

# 21. LIMIT with ORDER BY

This is one of the most important combinations.

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

Meaning:

```text
1. Sort employees by salary
2. Highest salary first
3. Return first 5 rows
```

Therefore, this finds the **top 5 salaries**.

---

# 22. Why ORDER BY Should Come Before LIMIT

Correct:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

Incorrect syntax:

```sql
SELECT *
FROM employees
LIMIT 5
ORDER BY salary DESC;
```

The general query structure is:

```text
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT/OFFSET
```

---

# 23. LIMIT with ASC

Find the 5 lowest salaries:

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 5;
```

---

# 24. Top 10 Customers by Sales

```sql
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM orders
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 10;
```

This is a very common **data analytics query**.

---

# 25. LIMIT with OFFSET

`OFFSET` skips a specified number of rows before returning results.

Syntax:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;
```

Meaning:

```text
Skip first 20 rows
↓
Return next 10 rows
```

---

# 26. LIMIT + OFFSET

Example:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 0;
```

First page.

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 10;
```

Second page.

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;
```

Third page.

---

# 27. Pagination

Pagination means dividing a large result into pages.

Suppose:

```text
Page size = 10
```

Then:

```text
Page 1 → OFFSET 0
Page 2 → OFFSET 10
Page 3 → OFFSET 20
Page 4 → OFFSET 30
```

Formula:

```text
OFFSET = (page_number - 1) × page_size
```

Example:

```text
Page 5
Page size = 20

OFFSET = (5 - 1) × 20
       = 80
```

Query:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 80;
```

---

# 28. Important Pagination Rule

Always use a deterministic `ORDER BY` when paginating.

Avoid:

```sql
SELECT *
FROM employees
LIMIT 10 OFFSET 20;
```

Prefer:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;
```

Without a defined order, SQL does not generally promise which rows will appear first.

---

# 29. LIMIT with WHERE

```sql
SELECT *
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 5;
```

Meaning:

```text
Find IT employees
        ↓
Sort by salary
        ↓
Return top 5
```

---

# 30. LIMIT with GROUP BY

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
ORDER BY employee_count DESC
LIMIT 3;
```

This finds the **3 departments with the highest number of employees**.

---

# 31. LIMIT with DISTINCT

```sql
SELECT DISTINCT city
FROM customers
ORDER BY city
LIMIT 10;
```

Returns the first 10 unique cities in sorted order.

---

# 32. LIMIT with Aggregate Functions

```sql
SELECT
    product,
    SUM(quantity) AS total_quantity
FROM sales
GROUP BY product
ORDER BY total_quantity DESC
LIMIT 10;
```

Finds the top 10 products by quantity sold.

---

# 33. Top-N Analysis

Top-N queries are extremely important in data analytics.

### Top 5 salaries

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

### Top 10 products

```sql
SELECT
    product,
    SUM(sales) AS total_sales
FROM orders
GROUP BY product
ORDER BY total_sales DESC
LIMIT 10;
```

### Top 3 cities

```sql
SELECT
    city,
    COUNT(*) AS customer_count
FROM customers
GROUP BY city
ORDER BY customer_count DESC
LIMIT 3;
```

---

# 34. Bottom-N Analysis

Reverse the sorting direction.

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 5;
```

This finds the 5 lowest salaries.

---

# 35. Highest Single Value

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

This returns one employee row with the highest salary, but if multiple employees tie, only one row is returned.

---

# 36. Lowest Single Value

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 1;
```

Again, ties may mean other equally low rows are excluded.

For all tied rows, use an appropriate ranking/window-function approach.

---

# 37. LIMIT vs MAX()

These are different.

### MAX()

```sql
SELECT MAX(salary)
FROM employees;
```

Returns:

```text
Highest salary value
```

### LIMIT

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

Returns:

```text
The first employee row after sorting
```

So:

```text
MAX() → returns a value
ORDER BY + LIMIT → returns row(s)
```

---

# 38. LIMIT vs TOP

Different databases use different syntax.

### MySQL / PostgreSQL / SQLite

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

### SQL Server

```sql
SELECT TOP 5 *
FROM employees
ORDER BY salary DESC;
```

### Standard SQL / PostgreSQL-style FETCH

```sql
SELECT *
FROM employees
ORDER BY salary DESC
FETCH FIRST 5 ROWS ONLY;
```

Always check the syntax supported by your DBMS.

---

# 39. TOP

`TOP` is commonly used in SQL Server.

```sql
SELECT TOP 5 *
FROM employees
ORDER BY salary DESC;
```

Top 10:

```sql
SELECT TOP 10 *
FROM employees
ORDER BY salary DESC;
```

---

# 40. TOP with Percentage

SQL Server supports:

```sql
SELECT TOP 10 PERCENT *
FROM employees
ORDER BY salary DESC;
```

This returns approximately the top 10% according to SQL Server's `TOP` semantics.

---

# 41. FETCH FIRST

Standard SQL provides row limiting with `FETCH`.

```sql
SELECT *
FROM employees
ORDER BY salary DESC
FETCH FIRST 5 ROWS ONLY;
```

Another form:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
FETCH NEXT 5 ROWS ONLY;
```

Exact support varies by DBMS.

---

# 42. OFFSET with FETCH

Standard-style syntax:

```sql
SELECT *
FROM employees
ORDER BY employee_id
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```

Meaning:

```text
Skip 20
↓
Return next 10
```

---

# 43. SQL Server OFFSET/FETCH

Example:

```sql
SELECT *
FROM employees
ORDER BY employee_id
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```

`ORDER BY` is required for this form.

---

# 44. MySQL/PostgreSQL LIMIT/OFFSET

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;
```

Some systems also allow:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 20, 10;
```

The latter is a MySQL-specific style where:

```text
20 → offset
10 → number of rows
```

For readability and portability, prefer:

```sql
LIMIT 10 OFFSET 20
```

when supported.

---

# 45. NULL Values and Sorting

Sorting NULL values can differ between DBMSs.

Example:

```sql
SELECT *
FROM employees
ORDER BY bonus ASC;
```

If `bonus` contains NULL values, their position depends on the database.

Some databases support explicit control:

```sql
ORDER BY bonus ASC NULLS FIRST;
```

or:

```sql
ORDER BY bonus ASC NULLS LAST;
```

Check your DBMS documentation for support and default behavior.

---

# 46. Sorting NULLs with CASE

If your DBMS does not support `NULLS FIRST/LAST`, you can sometimes control the ordering using `CASE`.

Example:

```sql
SELECT *
FROM employees
ORDER BY
    CASE WHEN bonus IS NULL THEN 1 ELSE 0 END,
    bonus ASC;
```

This places non-NULL bonuses first.

---

# 47. Sorting with CASE

You can create custom sorting rules.

Example:

```sql
SELECT *
FROM employees
ORDER BY
    CASE
        WHEN department = 'IT' THEN 1
        WHEN department = 'Finance' THEN 2
        WHEN department = 'HR' THEN 3
        ELSE 4
    END;
```

Result priority:

```text
IT
Finance
HR
Others
```

This is called **custom sorting**.

---

# 48. Custom Business Sorting

Suppose an e-commerce system has:

```text
Pending
Processing
Shipped
Delivered
Cancelled
```

You may want:

```text
Pending
Processing
Shipped
Delivered
Cancelled
```

Query:

```sql
SELECT *
FROM orders
ORDER BY
    CASE status
        WHEN 'Pending' THEN 1
        WHEN 'Processing' THEN 2
        WHEN 'Shipped' THEN 3
        WHEN 'Delivered' THEN 4
        WHEN 'Cancelled' THEN 5
        ELSE 6
    END;
```

---

# 49. Sorting by Multiple Conditions

```sql
SELECT *
FROM employees
ORDER BY
    department ASC,
    salary DESC,
    joining_date ASC;
```

Priority:

```text
1. Department
2. Salary within department
3. Joining date when salary is tied
```

---

# 50. Stable and Deterministic Sorting

Suppose:

```text
employee | salary
---------|-------
A        | 50000
B        | 50000
C        | 50000
```

Query:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 2;
```

There are three employees tied for the same salary, but only two rows are requested.

Which two rows appear is not something you should rely on unless you provide a tie-breaker.

Better:

```sql
SELECT *
FROM employees
ORDER BY salary DESC, employee_id ASC
LIMIT 2;
```

Now the ordering is deterministic if `employee_id` is unique.

---

# 51. Top-N with Ties

Sometimes you want **all employees who share the top salary**, rather than an arbitrary number of rows.

Using a subquery:

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

If three employees have the highest salary, all three are returned.

---

# 52. Top-N per Group

This is an important analytics problem.

Suppose you want:

```text
Top 3 employees by salary
for EACH department
```

`LIMIT 3` alone cannot do this because it limits the entire result.

Use a window function:

```sql
SELECT *
FROM (
    SELECT
        name,
        department,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rn
    FROM employees
) x
WHERE rn <= 3;
```

Concept:

```text
PARTITION BY department
        ↓
Create ranking separately for each department
        ↓
ORDER BY salary DESC
        ↓
Take rank <= 3
```

---

# 53. RANK vs ROW_NUMBER for Top-N

If ties matter:

```sql
RANK()
```

can be useful.

Example:

```sql
SELECT *
FROM (
    SELECT
        name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk <= 3;
```

Difference:

```text
ROW_NUMBER()
→ Every row gets a unique number

RANK()
→ Tied rows receive the same rank
```

---

# 54. Sorting in Data Analytics

Sorting is used for:

### Highest sales

```sql
ORDER BY total_sales DESC
```

### Lowest sales

```sql
ORDER BY total_sales ASC
```

### Most recent transaction

```sql
ORDER BY transaction_date DESC
```

### Oldest transaction

```sql
ORDER BY transaction_date ASC
```

### Highest-performing products

```sql
ORDER BY revenue DESC
```

### Lowest-performing products

```sql
ORDER BY revenue ASC
```

---

# 55. Limiting in Data Analytics

Limiting is useful for:

```text
Top 5 products
Top 10 customers
Bottom 10 products
Latest 20 transactions
First 100 records
Dashboard previews
Pagination
Sampling a small result set
```

---

# 56. Latest Records

Suppose you want the latest 10 orders:

```sql
SELECT *
FROM orders
ORDER BY order_date DESC
LIMIT 10;
```

Important:

```text
DESC
↓
Newest first
↓
LIMIT 10
↓
Latest 10
```

---

# 57. Oldest Records

```sql
SELECT *
FROM orders
ORDER BY order_date ASC
LIMIT 10;
```

---

# 58. Highest Revenue Products

```sql
SELECT
    product_id,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product_id
ORDER BY revenue DESC
LIMIT 10;
```

Query flow:

```text
FROM sales
     ↓
Calculate quantity × price
     ↓
GROUP BY product
     ↓
SUM revenue
     ↓
ORDER BY revenue DESC
     ↓
LIMIT 10
```

---

# 59. Top Customers

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
ORDER BY total_spending DESC
LIMIT 10;
```

This is a classic analytics query.

---

# 60. Bottom Customers

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
ORDER BY total_spending ASC
LIMIT 10;
```

---

# 61. Sorting and Limiting Query Execution

A simplified conceptual processing order is:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY
 ↓
LIMIT / OFFSET
```

Example:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC
LIMIT 5;
```

Conceptually:

```text
1. Get employees
2. Keep active employees
3. Group by department
4. Calculate average salary
5. Remove groups with average <= 50000
6. Sort by average salary
7. Return top 5
```

---

# 62. ORDER BY vs WHERE

They have different purposes.

### WHERE

Filters rows.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Meaning:

```text
Which rows should I keep?
```

### ORDER BY

Sorts rows.

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Meaning:

```text
In what order should I display them?
```

---

# 63. ORDER BY vs GROUP BY

### GROUP BY

Groups rows for aggregation.

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

### ORDER BY

Sorts the resulting rows.

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;
```

So:

```text
GROUP BY → Creates groups
ORDER BY → Sorts results
```

---

# 64. ORDER BY vs LIMIT

They also solve different problems.

```sql
ORDER BY salary DESC
```

means:

```text
Sort from highest to lowest
```

while:

```sql
LIMIT 5
```

means:

```text
Return at most 5 rows
```

Together:

```sql
ORDER BY salary DESC
LIMIT 5;
```

means:

```text
Sort highest → lowest
        ↓
Take first 5
```

---

# 65. Common Mistake — LIMIT Without ORDER BY

Avoid:

```sql
SELECT *
FROM employees
LIMIT 5;
```

if you mean:

```text
Give me the first 5 employees
```

There is no reliable business meaning to "first" unless you specify an ordering.

Instead:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 5;
```

---

# 66. Common Mistake — Wrong Sort Direction

Want highest salary:

```sql
ORDER BY salary DESC
```

Not:

```sql
ORDER BY salary ASC
```

Remember:

```text
ASC  → Low → High
DESC → High → Low
```

---

# 67. Common Mistake — LIMIT Before ORDER BY

Incorrect:

```sql
SELECT *
FROM employees
LIMIT 5
ORDER BY salary DESC;
```

Correct:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

# 68. Common Mistake — Top N Without Aggregation

Suppose the requirement is:

> Find the top 5 customers by total spending.

This is not necessarily:

```sql
SELECT *
FROM customers
ORDER BY amount DESC
LIMIT 5;
```

If customers have multiple orders, you first need aggregation:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
ORDER BY total_spending DESC
LIMIT 5;
```

---

# 69. Common Mistake — Top N Per Group

This:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

means:

```text
Top 3 employees overall
```

It does NOT mean:

```text
Top 3 employees from every department
```

For top-N per group, use window functions such as:

```sql
ROW_NUMBER()
RANK()
DENSE_RANK()
```

with `PARTITION BY`.

---

# 70. OFFSET Performance

For very large datasets:

```sql
LIMIT 20 OFFSET 1000000;
```

can become inefficient because the database may need to process/skip many rows.

For large-scale pagination, **keyset/cursor pagination** can often be more efficient.

---

# 71. Keyset Pagination

Instead of:

```sql
SELECT *
FROM orders
ORDER BY order_id
LIMIT 20 OFFSET 1000000;
```

Use a known last-seen key:

```sql
SELECT *
FROM orders
WHERE order_id > 1000000
ORDER BY order_id
LIMIT 20;
```

Concept:

```text
Last seen ID = 1000000
        ↓
Get rows after 1000000
        ↓
Sort
        ↓
Return next 20
```

This is often called:

```text
Keyset pagination
Cursor pagination
Seek pagination
```

It works best when the ordering column(s) are indexed and the ordering condition is designed correctly.

---

# 72. Keyset Pagination with Multiple Columns

If sorting by:

```sql
ORDER BY order_date DESC, order_id DESC
```

you need to preserve the complete ordering key.

A common pattern is:

```sql
SELECT *
FROM orders
WHERE
    order_date < '2026-01-15'
    OR (
        order_date = '2026-01-15'
        AND order_id < 5000
    )
ORDER BY order_date DESC, order_id DESC
LIMIT 20;
```

This allows pagination through a stable composite ordering.

---

# 73. Sorting Performance

For large tables, sorting can be expensive.

Indexes can sometimes help the database avoid a separate sort, depending on the query and index design.

Example:

```sql
CREATE INDEX idx_employee_salary
ON employees(salary);
```

Then:

```sql
SELECT *
FROM employees
ORDER BY salary;
```

may benefit from the index, depending on the DBMS and query plan.

Always verify with your database's execution plan tools.

---

# 74. LIMIT and Indexes

This query is common:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 10;
```

An appropriate index can sometimes allow the database to find the required rows efficiently instead of sorting the entire table.

For example:

```sql
CREATE INDEX idx_salary
ON employees(salary);
```

Exact optimization depends on the database engine.

---

# 75. Sorting with JOIN

```sql
SELECT
    e.name,
    d.department_name,
    e.salary
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
ORDER BY e.salary DESC
LIMIT 10;
```

This finds the 10 highest-paid employees along with their department names.

---

# 76. Sorting by Joined Columns

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
ORDER BY d.department_name ASC;
```

You can sort using columns from joined tables.

---

# 77. Sorting by Aggregated Data

```sql
SELECT
    department,
    SUM(salary) AS payroll
FROM employees
GROUP BY department
ORDER BY payroll DESC;
```

This ranks departments by total payroll.

---

# 78. Sorting by Multiple Aggregates

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY
    employee_count DESC,
    avg_salary DESC;
```

Priority:

```text
1. Employee count
2. Average salary when count is tied
```

---

# 79. Real Data Analytics Example

### Question:

> Find the top 5 cities with the highest customer count.

```sql
SELECT
    city,
    COUNT(*) AS customer_count
FROM customers
GROUP BY city
ORDER BY customer_count DESC
LIMIT 5;
```

Breakdown:

```text
GROUP BY city
        ↓
Count customers
        ↓
ORDER BY count DESC
        ↓
LIMIT 5
```

---

# 80. Real Data Analytics Example

### Question:

> Find the 10 products generating the highest revenue.

```sql
SELECT
    product_id,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product_id
ORDER BY revenue DESC
LIMIT 10;
```

---

# 81. Real Data Analytics Example

### Question:

> Show the latest 20 transactions.

```sql
SELECT *
FROM transactions
ORDER BY transaction_date DESC, transaction_id DESC
LIMIT 20;
```

The second ordering column helps break ties when multiple transactions have the same timestamp/date.

---

# 82. Real Data Analytics Example

### Question:

> Find the 5 departments with the lowest average salary.

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary ASC
LIMIT 5;
```

---

# 83. Real Data Analytics Example

### Question:

> Show page 3 with 25 records per page.

Using `LIMIT/OFFSET`:

```sql
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 25 OFFSET 50;
```

Formula:

```text
(page - 1) × page_size

(3 - 1) × 25
= 50
```

---

# 84. Complete Syntax Reference

## ORDER BY

```sql
SELECT columns
FROM table
ORDER BY column ASC;
```

```sql
SELECT columns
FROM table
ORDER BY column DESC;
```

---

## Multiple columns

```sql
SELECT columns
FROM table
ORDER BY
    column1 ASC,
    column2 DESC;
```

---

## LIMIT

```sql
SELECT columns
FROM table
LIMIT number;
```

---

## LIMIT + OFFSET

```sql
SELECT columns
FROM table
LIMIT number OFFSET number;
```

---

## TOP

```sql
SELECT TOP 10 columns
FROM table
ORDER BY column DESC;
```

---

## FETCH

```sql
SELECT columns
FROM table
ORDER BY column DESC
FETCH FIRST 10 ROWS ONLY;
```

---

## OFFSET + FETCH

```sql
SELECT columns
FROM table
ORDER BY column
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```

---

# 85. DBMS Syntax Comparison

| Feature    | MySQL     | PostgreSQL | SQL Server | Oracle                                                   |
| ---------- | --------- | ---------- | ---------- | -------------------------------------------------------- |
| `ORDER BY` | ✅         | ✅          | ✅          | ✅                                                        |
| `LIMIT`    | ✅         | ✅          | ❌          | Modern versions support row limiting, but syntax differs |
| `OFFSET`   | ✅         | ✅          | ✅          | ✅                                                        |
| `TOP`      | ❌         | ❌          | ✅          | ❌                                                        |
| `FETCH`    | Supported | Supported  | Supported  | Supported                                                |
| `ROWNUM`   | ❌         | ❌          | ❌          | Oracle-specific                                          |

The exact syntax and version support should always be checked for the DBMS you're using.

---

# 86. Revision Cheat Sheet

```text
ORDER BY
    ↓
Sort rows

ASC
    ↓
Ascending
Small → Large
A → Z
Old → New

DESC
    ↓
Descending
Large → Small
Z → A
New → Old

LIMIT
    ↓
Restrict number of rows

OFFSET
    ↓
Skip rows

TOP
    ↓
SQL Server row limiting

FETCH
    ↓
Standard-style row limiting
```

---

# 87. Most Important Patterns

### Highest 5

```sql
SELECT *
FROM table_name
ORDER BY value DESC
LIMIT 5;
```

### Lowest 5

```sql
SELECT *
FROM table_name
ORDER BY value ASC
LIMIT 5;
```

### Latest 10

```sql
SELECT *
FROM table_name
ORDER BY date_column DESC
LIMIT 10;
```

### First 10

```sql
SELECT *
FROM table_name
ORDER BY id
LIMIT 10;
```

### Page 2

```sql
SELECT *
FROM table_name
ORDER BY id
LIMIT 10 OFFSET 10;
```

### Top 10 after aggregation

```sql
SELECT
    category,
    SUM(amount) AS total
FROM sales
GROUP BY category
ORDER BY total DESC
LIMIT 10;
```

### Top-N per group

```sql
ROW_NUMBER() OVER (
    PARTITION BY group_column
    ORDER BY value DESC
)
```

---

# 88. Final Revision Map

```text
                    SORTING & LIMITING
                            │
             ┌──────────────┴──────────────┐
             │                             │
          SORTING                       LIMITING
             │                             │
         ORDER BY                    LIMIT / TOP / FETCH
             │                             │
       ┌─────┴─────┐                  ┌────┴────┐
       │           │                  │         │
      ASC         DESC             LIMIT     OFFSET
       │           │                  │         │
   Low → High   High → Low       Return N   Skip N
       │           │                  │         │
       └───────────┴──────────────────┴─────────┘
                            │
                     ANALYTICS USE CASES
                            │
          ┌─────────────────┼──────────────────┐
          │                 │                  │
       Top-N             Bottom-N          Latest-N
          │                 │                  │
      Rankings         Low performers      Recent data
          │                 │                  │
          └─────────────────┼──────────────────┘
                            │
                      ADVANCED ANALYTICS
                            │
                   ┌────────┴────────┐
                   │                 │
              Top-N Overall      Top-N per Group
                   │                 │
             ORDER BY + LIMIT   Window Functions
```

## ⭐ Key Things to Remember

```text
1. ORDER BY → sorting
2. ASC → ascending
3. DESC → descending
4. LIMIT → restrict number of rows
5. OFFSET → skip rows
6. TOP → SQL Server row limiting
7. FETCH → standard-style row limiting
8. ORDER BY + LIMIT → Top-N / Bottom-N
9. ORDER BY DESC → highest/newest first
10. ORDER BY ASC → lowest/oldest first
11. Always use ORDER BY when "first/latest/top" has a specific meaning
12. Use a tie-breaker for deterministic results
13. LIMIT gives top N overall, not top N per group
14. Top-N per group usually requires window functions
15. Large OFFSET pagination can be inefficient; keyset pagination can be better
```
