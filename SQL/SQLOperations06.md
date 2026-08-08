# SQL Operations — Complete Guide

SQL operations are the actions performed on data stored in relational databases.

A useful way to understand SQL operations is:

```text
SQL OPERATIONS
│
├── Database Operations
├── Table Operations
├── CRUD Operations
│   ├── INSERT
│   ├── SELECT
│   ├── UPDATE
│   └── DELETE
│
├── Filtering Operations
│   ├── WHERE
│   ├── AND
│   ├── OR
│   ├── NOT
│   ├── IN
│   ├── BETWEEN
│   ├── LIKE
│   └── IS NULL
│
├── Sorting
│   └── ORDER BY
│
├── Aggregation
│   ├── COUNT
│   ├── SUM
│   ├── AVG
│   ├── MIN
│   └── MAX
│
├── Grouping
│   ├── GROUP BY
│   └── HAVING
│
├── Joins
│   ├── INNER JOIN
│   ├── LEFT JOIN
│   ├── RIGHT JOIN
│   ├── FULL JOIN
│   ├── CROSS JOIN
│   └── SELF JOIN
│
├── Set Operations
│   ├── UNION
│   ├── UNION ALL
│   ├── INTERSECT
│   └── EXCEPT
│
├── Subqueries
├── Window Operations
├── String Operations
├── Numeric Operations
├── Date/Time Operations
└── Transaction Operations
```

---

# 1. Database Operations

## Create Database

```sql
CREATE DATABASE company;
```

## Select Database

MySQL:

```sql
USE company;
```

## Delete Database

```sql
DROP DATABASE company;
```

> `DROP DATABASE` permanently removes the database and its objects. Use with caution.

---

# 2. Table Operations

## Create Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    salary DECIMAL(10,2),
    department VARCHAR(50)
);
```

## Add Column

```sql
ALTER TABLE employees
ADD email VARCHAR(255);
```

## Rename Column

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

## Drop Column

```sql
ALTER TABLE employees
DROP COLUMN email;
```

## Drop Table

```sql
DROP TABLE employees;
```

## Remove All Rows

```sql
TRUNCATE TABLE employees;
```

---

# 3. CRUD Operations

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

SQL mapping:

```text
CREATE → INSERT
READ   → SELECT
UPDATE → UPDATE
DELETE → DELETE
```

---

# 4. CREATE / INSERT Operation

`INSERT` adds new rows to a table.

## Insert One Row

```sql
INSERT INTO employees
(employee_id, name, age, salary, department)
VALUES
(1, 'Rahul', 25, 50000, 'IT');
```

## Insert Multiple Rows

```sql
INSERT INTO employees
(employee_id, name, age, salary, department)
VALUES
(2, 'Priya', 28, 60000, 'HR'),
(3, 'Arun', 30, 70000, 'IT'),
(4, 'Anita', 26, 55000, 'Finance');
```

---

# 5. READ / SELECT Operation

`SELECT` retrieves data.

## Select Everything

```sql
SELECT *
FROM employees;
```

## Select Specific Columns

```sql
SELECT name, salary
FROM employees;
```

## Rename Output Columns with Alias

```sql
SELECT
    name AS employee_name,
    salary AS monthly_salary
FROM employees;
```

---

# 6. DISTINCT Operation

`DISTINCT` removes duplicate combinations from the result.

```sql
SELECT DISTINCT department
FROM employees;
```

Multiple columns:

```sql
SELECT DISTINCT department, age
FROM employees;
```

Here, uniqueness is considered across the combination of `department` and `age`.

---

# 7. Filtering with WHERE

`WHERE` filters rows before they are returned.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

# 8. Comparison Operations

SQL comparison operators:

```text
=       Equal
<>      Not equal
!=      Not equal in many DBMSs
>       Greater than
<       Less than
>=      Greater than or equal
<=      Less than or equal
```

Examples:

```sql
SELECT *
FROM employees
WHERE age = 25;
```

```sql
SELECT *
FROM employees
WHERE salary >= 60000;
```

```sql
SELECT *
FROM employees
WHERE age <> 30;
```

---

# 9. AND Operation

All conditions must be true.

```sql
SELECT *
FROM employees
WHERE age > 25
AND salary > 50000;
```

Logic:

```text
Condition 1 = TRUE
Condition 2 = TRUE
              ↓
            Result
```

---

# 10. OR Operation

At least one condition must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

---

# 11. NOT Operation

Reverses a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

---

# 12. Combining Conditions

Use parentheses when combining `AND` and `OR` to make the intended logic explicit.

```sql
SELECT *
FROM employees
WHERE
    (department = 'IT' AND salary > 60000)
    OR age > 30;
```

Conceptually:

```text
             OR
           /   \
         AND   age > 30
        /   \
    IT      salary > 60000
```

---

# 13. BETWEEN Operation

Checks whether a value is within an inclusive range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 70000;
```

Equivalent conceptually to:

```sql
SELECT *
FROM employees
WHERE salary >= 50000
AND salary <= 70000;
```

---

# 14. IN Operation

Checks whether a value belongs to a list.

Without `IN`:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Finance';
```

Using `IN`:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

---

# 15. NOT IN

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

Be careful when `NULL` values are involved because SQL uses three-valued logic.

---

# 16. LIKE Operation

`LIKE` performs pattern matching.

Wildcards:

```text
% → Zero or more characters
_ → Exactly one character
```

---

## Starts With

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

## Ends With

```sql
SELECT *
FROM employees
WHERE name LIKE '%a';
```

---

## Contains

```sql
SELECT *
FROM employees
WHERE name LIKE '%an%';
```

---

## Single Character

```sql
SELECT *
FROM employees
WHERE name LIKE 'A_i%';
```

Case sensitivity depends on the database and collation/settings.

---

# 17. NULL Operations

`NULL` represents a missing, unknown, or not-applicable value depending on context.

It is not the same as:

```text
0
''
FALSE
```

## Check NULL

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

## Check NOT NULL

```sql
SELECT *
FROM employees
WHERE email IS NOT NULL;
```

Do not use:

```sql
WHERE email = NULL;
```

Use:

```sql
WHERE email IS NULL;
```

---

# 18. UPDATE Operation

`UPDATE` modifies existing rows.

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;
```

---

## Update Multiple Columns

```sql
UPDATE employees
SET
    salary = 65000,
    department = 'Finance'
WHERE employee_id = 1;
```

---

## Update Multiple Rows

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

---

# 19. UPDATE Without WHERE

This:

```sql
UPDATE employees
SET salary = 60000;
```

can update **every row**.

Always verify the target rows first:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Then update:

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

---

# 20. DELETE Operation

Deletes rows.

```sql
DELETE FROM employees
WHERE employee_id = 4;
```

Delete multiple rows:

```sql
DELETE FROM employees
WHERE department = 'Finance';
```

Delete all rows:

```sql
DELETE FROM employees;
```

The table structure remains.

---

# 21. DELETE vs TRUNCATE vs DROP

| Operation | Data             | Structure     | WHERE |
| --------- | ---------------- | ------------- | ----- |
| DELETE    | Removes rows     | Keeps table   | Yes   |
| TRUNCATE  | Removes all rows | Keeps table   | No    |
| DROP      | Removes object   | Removes table | No    |

---

# 22. Sorting Operation — ORDER BY

Sort ascending:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Sort descending:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Multiple columns:

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

This means:

```text
First → department ascending
Then  → salary descending within each department
```

---

# 23. LIMIT / TOP

To retrieve a limited number of rows, syntax depends on the DBMS.

### MySQL/PostgreSQL-style

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

This can be useful for:

```text
Top 5 salaries
Top 10 customers
First N records
```

---

# 24. Aggregate Operations

Aggregate functions perform calculations across multiple rows.

Main functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

# 25. COUNT()

Counts rows or non-NULL values depending on the expression.

## Count All Rows

```sql
SELECT COUNT(*)
FROM employees;
```

## Count Non-NULL Values

```sql
SELECT COUNT(email)
FROM employees;
```

`COUNT(email)` ignores NULL values.

---

# 26. SUM()

Calculates the total.

```sql
SELECT SUM(salary)
FROM employees;
```

---

# 27. AVG()

Calculates the average.

```sql
SELECT AVG(salary)
FROM employees;
```

`AVG()` generally ignores NULL values.

---

# 28. MIN()

Finds the minimum value.

```sql
SELECT MIN(salary)
FROM employees;
```

---

# 29. MAX()

Finds the maximum value.

```sql
SELECT MAX(salary)
FROM employees;
```

---

# 30. Multiple Aggregate Operations

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

---

# 31. GROUP BY Operation

`GROUP BY` creates groups of rows based on one or more columns.

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Conceptually:

```text
Employees
    ↓
Group by department
    ↓
IT       → 10 employees
HR       → 5 employees
Finance  → 7 employees
```

---

# 32. GROUP BY with SUM

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

---

# 33. GROUP BY with AVG

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 34. GROUP BY Multiple Columns

```sql
SELECT
    department,
    age,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department, age;
```

Groups are created based on the combination of both columns.

---

# 35. HAVING Operation

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

---

# 36. WHERE vs HAVING

This is extremely important.

### WHERE

Filters individual rows **before grouping**.

```sql
SELECT department, AVG(salary)
FROM employees
WHERE salary > 40000
GROUP BY department;
```

### HAVING

Filters groups **after grouping**.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Mental model:

```text
WHERE
  ↓
Filter rows
  ↓
GROUP BY
  ↓
Create groups
  ↓
Aggregate
  ↓
HAVING
  ↓
Filter groups
```

---

# 37. JOIN Operations

Joins combine related data from multiple tables.

Suppose we have:

```text
employees
--------------------------------
employee_id | name | department_id

departments
--------------------------------
department_id | department_name
```

Relationship:

```text
employees.department_id
          ↓
departments.department_id
```

---

# 38. INNER JOIN

Returns matching rows from both tables.

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

Conceptually:

```text
Employees          Departments
    │                    │
    └──── matching ──────┘
             ↓
        Matching rows
```

---

# 39. LEFT JOIN

Returns:

```text
All rows from left table
+
Matching rows from right table
```

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

Employees without a matching department still appear, with NULL values for department columns.

---

# 40. RIGHT JOIN

Returns:

```text
All rows from right table
+
Matching rows from left table
```

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
RIGHT JOIN departments d
    ON e.department_id = d.department_id;
```

Support varies by database system.

---

# 41. FULL OUTER JOIN

Returns:

```text
Matching rows
+
Unmatched rows from left
+
Unmatched rows from right
```

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
FULL OUTER JOIN departments d
    ON e.department_id = d.department_id;
```

Not supported directly by every DBMS.

---

# 42. CROSS JOIN

Produces the Cartesian product.

If:

```text
Table A = 3 rows
Table B = 4 rows
```

Then:

```text
3 × 4 = 12 combinations
```

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
CROSS JOIN departments d;
```

Use carefully because the result can become very large.

---

# 43. SELF JOIN

A table can be joined with itself.

Example: employees and their managers.

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Here:

```text
e → employee
m → manager
```

Both aliases refer to the same table.

---

# 44. Set Operations

Set operations combine the results of multiple `SELECT` statements.

Main operations:

```text
UNION
UNION ALL
INTERSECT
EXCEPT
```

The participating queries must have compatible column counts and compatible data types.

---

# 45. UNION

Combines results and removes duplicates.

```sql
SELECT name
FROM employees
WHERE department = 'IT'

UNION

SELECT name
FROM employees
WHERE department = 'HR';
```

---

# 46. UNION ALL

Combines results while keeping duplicates.

```sql
SELECT name
FROM employees
WHERE department = 'IT'

UNION ALL

SELECT name
FROM employees
WHERE department = 'HR';
```

Generally, `UNION ALL` avoids the duplicate-elimination step and can therefore be more efficient when duplicates are intentionally allowed.

---

# 47. INTERSECT

Returns rows present in both query results.

```sql
SELECT employee_id
FROM project_a

INTERSECT

SELECT employee_id
FROM project_b;
```

Support varies by DBMS/version.

---

# 48. EXCEPT

Returns rows from the first query that are not in the second.

```sql
SELECT employee_id
FROM project_a

EXCEPT

SELECT employee_id
FROM project_b;
```

Some DBMSs use `MINUS` instead of `EXCEPT`.

---

# 49. Subquery Operations

A subquery is a query inside another query.

Example:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

Meaning:

```text
Find average salary
       ↓
Compare each employee's salary
       ↓
Return employees above average
```

---

# 50. Subquery with IN

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('IT', 'HR')
);
```

---

# 51. EXISTS Operation

`EXISTS` checks whether a subquery returns at least one row.

```sql
SELECT *
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

This finds departments having at least one employee.

---

# 52. NOT EXISTS

```sql
SELECT *
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

This finds departments with no matching employees.

---

# 53. CASE Operation

`CASE` performs conditional logic inside SQL.

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

Conceptually:

```text
salary >= 80000 → High
salary >= 50000 → Medium
otherwise       → Low
```

---

# 54. CASE with Aggregation

```sql
SELECT
    COUNT(CASE WHEN salary >= 60000 THEN 1 END) AS high_salary_count
FROM employees;
```

This is useful in analytics for conditional counts.

Another common pattern:

```sql
SELECT
    SUM(CASE WHEN department = 'IT' THEN 1 ELSE 0 END) AS it_count,
    SUM(CASE WHEN department = 'HR' THEN 1 ELSE 0 END) AS hr_count
FROM employees;
```

---

# 55. String Operations

SQL provides functions for manipulating text.

Common functions include:

```text
UPPER()
LOWER()
LENGTH()
TRIM()
SUBSTRING()
CONCAT()
REPLACE()
```

Exact names and syntax vary somewhat by DBMS.

---

# 56. UPPER()

```sql
SELECT UPPER(name)
FROM employees;
```

Converts text to uppercase.

---

# 57. LOWER()

```sql
SELECT LOWER(name)
FROM employees;
```

Converts text to lowercase.

---

# 58. TRIM()

Removes leading/trailing whitespace.

```sql
SELECT TRIM(name)
FROM employees;
```

---

# 59. CONCAT()

Combines strings.

```sql
SELECT CONCAT(name, ' - ', department)
FROM employees;
```

Some DBMSs use different concatenation syntax or functions.

---

# 60. LENGTH()

```sql
SELECT
    name,
    LENGTH(name) AS name_length
FROM employees;
```

The exact function can differ by DBMS; for example, SQL Server commonly uses `LEN()`.

---

# 61. REPLACE()

```sql
SELECT
    REPLACE(department, 'IT', 'Technology')
FROM employees;
```

---

# 62. Numeric Operations

SQL supports mathematical expressions.

```sql
SELECT
    salary,
    salary + 5000 AS increased_salary
FROM employees;
```

Other operations:

```text
+
-
*
/
%
```

Modulo syntax varies by DBMS.

---

# 63. Mathematical Functions

Common functions include:

```text
ABS()
ROUND()
CEILING()/CEIL()
FLOOR()
POWER()
SQRT()
```

Examples:

```sql
SELECT ROUND(AVG(salary), 2)
FROM employees;
```

```sql
SELECT ABS(-100);
```

---

# 64. Date and Time Operations

Common date/time functions include DBMS-specific variants such as:

```text
CURRENT_DATE
CURRENT_TIMESTAMP
EXTRACT
DATE_PART
DATEADD
DATEDIFF
```

For example, standard-style current date:

```sql
SELECT CURRENT_DATE;
```

Current timestamp:

```sql
SELECT CURRENT_TIMESTAMP;
```

Exact date arithmetic syntax varies significantly between MySQL, PostgreSQL, SQL Server, Oracle, etc.

---

# 65. Window Operations

Window functions perform calculations across related rows while **keeping individual rows** in the result.

Important functions:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER()
AVG() OVER()
```

---

# 66. ROW_NUMBER()

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

Produces a sequential number.

---

# 67. RANK()

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

If two employees have the same salary, they receive the same rank, and gaps can occur afterward.

Example:

```text
Salary   Rank
90000     1
80000     2
80000     2
70000     4
```

---

# 68. DENSE_RANK()

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
Salary   Dense Rank
90000       1
80000       2
80000       2
70000       3
```

---

# 69. LAG()

Gets a value from a previous row.

```sql
SELECT
    name,
    salary,
    LAG(salary) OVER (
        ORDER BY employee_id
    ) AS previous_salary
FROM employees;
```

Useful for:

```text
Month-over-month comparison
Previous transaction
Previous salary
Previous day's sales
```

---

# 70. LEAD()

Gets a value from a following row.

```sql
SELECT
    name,
    salary,
    LEAD(salary) OVER (
        ORDER BY employee_id
    ) AS next_salary
FROM employees;
```

---

# 71. Running Total

```sql
SELECT
    employee_id,
    salary,
    SUM(salary) OVER (
        ORDER BY employee_id
    ) AS running_total
FROM employees;
```

This is particularly important in data analytics.

---

# 72. PARTITION BY

`PARTITION BY` divides rows into groups for a window function without collapsing them.

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

Meaning:

```text
IT
 ├── Rank employees by salary
 │
HR
 ├── Rank employees by salary
 │
Finance
 └── Rank employees by salary
```

---

# 73. COALESCE

`COALESCE()` returns the first non-NULL value.

```sql
SELECT
    name,
    COALESCE(email, 'No Email') AS email
FROM employees;
```

If:

```text
email = NULL
```

result:

```text
No Email
```

If email exists, the actual email is returned.

---

# 74. NULLIF

`NULLIF(a, b)` returns:

```text
NULL if a = b
a    otherwise
```

Example:

```sql
SELECT NULLIF(salary, 0)
FROM employees;
```

A common analytical use is preventing division by zero:

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS average_price
FROM sales;
```

---

# 75. Division and NULLIF

Instead of:

```sql
SELECT revenue / quantity
FROM sales;
```

which can cause division-by-zero problems if `quantity = 0`, use:

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS average_price
FROM sales;
```

---

# 76. Conditional Aggregation

Very important for data analytics.

```sql
SELECT
    SUM(CASE WHEN department = 'IT' THEN salary ELSE 0 END) AS it_salary,
    SUM(CASE WHEN department = 'HR' THEN salary ELSE 0 END) AS hr_salary
FROM employees;
```

This allows multiple conditional metrics in one query.

---

# 77. SQL Query Execution Order

One of the most important concepts for understanding complex SQL.

A simplified logical processing order is:

```text
FROM
  ↓
JOIN / ON
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
DISTINCT
  ↓
ORDER BY
  ↓
LIMIT / FETCH / TOP
```

For example:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE age >= 25
GROUP BY department
HAVING AVG(salary) > 60000
ORDER BY avg_salary DESC;
```

Conceptually:

```text
FROM employees
      ↓
Filter age >= 25
      ↓
Group by department
      ↓
Calculate AVG(salary)
      ↓
Keep groups with AVG > 60000
      ↓
Select output
      ↓
Sort descending
```

---

# 78. WHERE vs ON in JOINs

This distinction is very important.

Consider:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'IT';
```

The `WHERE` condition can eliminate rows where the department is NULL, making the result behave more like an inner join for that condition.

Compare with putting the condition in `ON`:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
   AND d.department_name = 'IT';
```

Here, all employees remain, while only IT departments match.

This distinction is crucial when working with outer joins.

---

# 79. Operations Used in Data Analytics

SQL operations are heavily used in data analytics.

| Analytical Task            | SQL Operation  |
| -------------------------- | -------------- |
| Filter data                | `WHERE`        |
| Sort data                  | `ORDER BY`     |
| Remove duplicates          | `DISTINCT`     |
| Count records              | `COUNT()`      |
| Calculate total            | `SUM()`        |
| Calculate average          | `AVG()`        |
| Find minimum               | `MIN()`        |
| Find maximum               | `MAX()`        |
| Group data                 | `GROUP BY`     |
| Filter groups              | `HAVING`       |
| Combine tables             | `JOIN`         |
| Combine datasets           | `UNION`        |
| Conditional logic          | `CASE`         |
| Handle missing values      | `COALESCE()`   |
| Ranking                    | `RANK()`       |
| Sequential numbering       | `ROW_NUMBER()` |
| Previous value             | `LAG()`        |
| Next value                 | `LEAD()`       |
| Running total              | `SUM() OVER()` |
| Compare groups             | `PARTITION BY` |
| Subset using another query | Subquery       |
| Check existence            | `EXISTS`       |

---

# 80. Complete Analytical Example

Suppose we need:

> Find the top 3 highest-paid employees in each department.

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
        ) AS rank_num
    FROM employees
) ranked
WHERE rank_num <= 3;
```

Conceptually:

```text
Employees
    ↓
PARTITION BY department
    ↓
Sort salary DESC within each department
    ↓
Assign row numbers
    ↓
Keep row_num <= 3
    ↓
Top 3 employees per department
```

This is a very common data-analytics SQL pattern.

---

# 81. Another Analytical Example

Find departments whose:

* employee count is greater than 5
* average salary is greater than 60,000

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 5
   AND AVG(salary) > 60000;
```

---

# 82. SQL Operations by Purpose

## Data Creation

```text
CREATE
INSERT
```

## Data Retrieval

```text
SELECT
```

## Data Modification

```text
UPDATE
DELETE
```

## Filtering

```text
WHERE
AND
OR
NOT
IN
BETWEEN
LIKE
IS NULL
```

## Sorting

```text
ORDER BY
```

## Aggregation

```text
COUNT
SUM
AVG
MIN
MAX
```

## Grouping

```text
GROUP BY
HAVING
```

## Combining Tables

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
CROSS JOIN
SELF JOIN
```

## Combining Query Results

```text
UNION
UNION ALL
INTERSECT
EXCEPT
```

## Advanced Analysis

```text
CASE
Subqueries
EXISTS
Window Functions
PARTITION BY
LAG
LEAD
RANK
ROW_NUMBER
```

## Missing-Value Handling

```text
IS NULL
IS NOT NULL
COALESCE
NULLIF
```

---

# 83. CRUD vs SQL Operations

CRUD is only a **small part** of SQL.

```text
CRUD
│
├── CREATE → INSERT
├── READ   → SELECT
├── UPDATE → UPDATE
└── DELETE → DELETE
```

But SQL provides many additional operations:

```text
Filtering
Sorting
Aggregation
Grouping
Joins
Set Operations
Subqueries
Window Functions
String Processing
Date Processing
Conditional Logic
NULL Handling
Transactions
```

So:

```text
CRUD ⊂ SQL Operations
```

CRUD is a subset of the operations you can perform with SQL.

---

# 84. Complete SQL Operations Cheat Sheet

```sql
-- CREATE
CREATE TABLE employees (...);

-- INSERT
INSERT INTO employees (...)
VALUES (...);

-- SELECT
SELECT *
FROM employees;

-- FILTER
SELECT *
FROM employees
WHERE salary > 50000;

-- AND
WHERE age > 25
AND salary > 50000;

-- OR
WHERE department = 'IT'
OR department = 'HR';

-- IN
WHERE department IN ('IT', 'HR');

-- BETWEEN
WHERE salary BETWEEN 50000 AND 80000;

-- LIKE
WHERE name LIKE 'A%';

-- NULL
WHERE email IS NULL;

-- DISTINCT
SELECT DISTINCT department
FROM employees;

-- SORT
SELECT *
FROM employees
ORDER BY salary DESC;

-- UPDATE
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';

-- DELETE
DELETE FROM employees
WHERE employee_id = 10;

-- COUNT
SELECT COUNT(*)
FROM employees;

-- SUM
SELECT SUM(salary)
FROM employees;

-- AVG
SELECT AVG(salary)
FROM employees;

-- MIN
SELECT MIN(salary)
FROM employees;

-- MAX
SELECT MAX(salary)
FROM employees;

-- GROUP
SELECT department, COUNT(*)
FROM employees
GROUP BY department;

-- HAVING
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;

-- JOIN
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;

-- UNION
SELECT name FROM employees_it
UNION
SELECT name FROM employees_hr;

-- CASE
SELECT
    name,
    CASE
        WHEN salary >= 70000 THEN 'High'
        ELSE 'Normal'
    END AS category
FROM employees;

-- SUBQUERY
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

-- WINDOW FUNCTION
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 85. Final Mental Map

```text
                         SQL OPERATIONS
                              │
       ┌──────────────────────┼──────────────────────┐
       │                      │                      │
     CRUD                  FILTERING             ANALYSIS
       │                      │                      │
 INSERT / SELECT          WHERE                  GROUP BY
 UPDATE / DELETE          AND / OR               HAVING
                          IN / BETWEEN            AGGREGATES
                          LIKE / NULL             CASE
                                                  WINDOWS
       │                      │
       └──────────────┬───────┘
                      │
                    COMBINE
                      │
                ┌─────┴─────┐
                │           │
              JOINS       SETS
                │           │
          INNER/LEFT     UNION
          RIGHT/FULL     UNION ALL
          CROSS/SELF     INTERSECT
                         EXCEPT
```

## Most Important Operations for Data Analytics

If your goal is **SQL + Data Analytics**, prioritize these:

```text
1. SELECT
2. WHERE
3. AND / OR / NOT
4. IN / BETWEEN / LIKE
5. IS NULL / IS NOT NULL
6. ORDER BY
7. DISTINCT
8. GROUP BY
9. COUNT / SUM / AVG / MIN / MAX
10. HAVING
11. INNER JOIN
12. LEFT JOIN
13. UNION / UNION ALL
14. CASE
15. Subqueries
16. EXISTS
17. COALESCE
18. Window Functions
19. ROW_NUMBER
20. RANK / DENSE_RANK
21. LAG / LEAD
22. PARTITION BY
23. Running totals
24. Conditional aggregation
```

These operations form the foundation for most **SQL coding, interview questions, reporting, and data-analysis tasks**.
