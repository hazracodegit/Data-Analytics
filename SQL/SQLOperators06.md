# SQL Operators — Complete Guide

SQL operators are symbols or keywords used to perform operations on data and to create conditions in SQL queries.

They are mainly used for:

```text
Arithmetic calculations
Comparisons
Filtering
Logical conditions
Pattern matching
Range checking
NULL checking
Combining query results
```

---

# 1. Types of SQL Operators

```text
SQL OPERATORS
│
├── 1. Arithmetic Operators
│
├── 2. Comparison Operators
│
├── 3. Logical Operators
│
├── 4. Bitwise Operators
│
├── 5. Special Operators
│   ├── IN
│   ├── NOT IN
│   ├── BETWEEN
│   ├── NOT BETWEEN
│   ├── LIKE
│   ├── NOT LIKE
│   ├── IS NULL
│   ├── IS NOT NULL
│   ├── EXISTS
│   └── NOT EXISTS
│
├── 6. String/Concatenation Operators
│
└── 7. Set Operators
    ├── UNION
    ├── UNION ALL
    ├── INTERSECT
    └── EXCEPT
```

> Operator names and syntax can vary slightly between MySQL, PostgreSQL, SQL Server, Oracle, and other DBMSs.

---

# 2. Arithmetic Operators

Arithmetic operators perform mathematical calculations.

| Operator | Meaning            |
| -------- | ------------------ |
| `+`      | Addition           |
| `-`      | Subtraction        |
| `*`      | Multiplication     |
| `/`      | Division           |
| `%`      | Modulo / remainder |

---

# 3. Addition `+`

Adds two numeric values.

```sql
SELECT 10 + 20 AS result;
```

Result:

```text
30
```

With table data:

```sql
SELECT
    salary,
    salary + 5000 AS increased_salary
FROM employees;
```

---

# 4. Subtraction `-`

```sql
SELECT 100 - 30 AS result;
```

Result:

```text
70
```

Example:

```sql
SELECT
    salary,
    salary - 5000 AS reduced_salary
FROM employees;
```

---

# 5. Multiplication `*`

```sql
SELECT 10 * 5 AS result;
```

Result:

```text
50
```

Example:

```sql
SELECT
    salary,
    salary * 12 AS annual_salary
FROM employees;
```

This assumes `salary` represents a monthly salary.

---

# 6. Division `/`

```sql
SELECT 100 / 5 AS result;
```

Result:

```text
20
```

Example:

```sql
SELECT
    salary,
    salary / 12 AS monthly_amount
FROM employees;
```

The exact behavior of integer division can vary by DBMS and data type.

---

# 7. Modulo `%`

Returns the remainder after division in DBMSs that support `%`.

```sql
SELECT 10 % 3 AS remainder;
```

Result:

```text
1
```

Example:

```sql
SELECT *
FROM employees
WHERE employee_id % 2 = 0;
```

This can find even-numbered employee IDs.

> Some DBMSs use a different modulo function/operator, so check your DBMS syntax.

---

# 8. Arithmetic Expressions

Multiple operators can be combined.

```sql
SELECT
    salary,
    salary * 12 + 5000 AS calculated_value
FROM employees;
```

Use parentheses to make the intended calculation clear:

```sql
SELECT
    salary,
    (salary * 12) + 5000 AS calculated_value
FROM employees;
```

---

# 9. Operator Precedence

SQL generally follows arithmetic precedence similar to mathematics:

```text
1. Parentheses
2. Multiplication / Division / Modulo
3. Addition / Subtraction
4. Comparisons
5. Logical operations
```

Example:

```sql
SELECT 10 + 5 * 2 AS result;
```

Result:

```text
20
```

Because multiplication is evaluated before addition.

Using parentheses:

```sql
SELECT (10 + 5) * 2 AS result;
```

Result:

```text
30
```

---

# 10. Comparison Operators

Comparison operators compare two values.

| Operator | Meaning                 |
| -------- | ----------------------- |
| `=`      | Equal                   |
| `<>`     | Not equal               |
| `!=`     | Not equal in many DBMSs |
| `>`      | Greater than            |
| `<`      | Less than               |
| `>=`     | Greater than or equal   |
| `<=`     | Less than or equal      |

They are commonly used with `WHERE`, `HAVING`, `JOIN`, and `CASE`.

---

# 11. Equal `=`

Checks whether two values are equal.

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Numeric example:

```sql
SELECT *
FROM employees
WHERE salary = 50000;
```

---

# 12. Not Equal `<>`

The standard SQL not-equal operator is:

```sql
<>
```

Example:

```sql
SELECT *
FROM employees
WHERE department <> 'IT';
```

This returns employees whose department is not IT.

---

# 13. Not Equal `!=`

Many DBMSs support:

```sql
!=
```

Example:

```sql
SELECT *
FROM employees
WHERE salary != 50000;
```

For portable SQL, `<>` is generally preferred.

---

# 14. Greater Than `>`

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

Meaning:

```text
salary must be greater than 60000
```

---

# 15. Less Than `<`

```sql
SELECT *
FROM employees
WHERE salary < 60000;
```

---

# 16. Greater Than or Equal `>=`

```sql
SELECT *
FROM employees
WHERE salary >= 60000;
```

This includes `60000`.

---

# 17. Less Than or Equal `<=`

```sql
SELECT *
FROM employees
WHERE salary <= 60000;
```

This also includes `60000`.

---

# 18. Comparison Example

Suppose:

```text
salary
------
40000
50000
60000
70000
80000
```

Query:

```sql
SELECT *
FROM employees
WHERE salary >= 60000;
```

Returns:

```text
60000
70000
80000
```

---

# 19. Logical Operators

Logical operators combine or reverse conditions.

Main operators:

```text
AND
OR
NOT
```

They are extremely important for filtering data.

---

# 20. AND Operator

`AND` returns true only when all conditions are true.

```sql
SELECT *
FROM employees
WHERE age > 25
AND salary > 50000;
```

The employee must satisfy:

```text
age > 25
AND
salary > 50000
```

Both must be true.

---

# 21. AND Truth Table

| Condition A | Condition B | A AND B |
| ----------- | ----------- | ------- |
| TRUE        | TRUE        | TRUE    |
| TRUE        | FALSE       | FALSE   |
| FALSE       | TRUE        | FALSE   |
| FALSE       | FALSE       | FALSE   |

---

# 22. OR Operator

`OR` returns true when at least one condition is true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

An employee can belong to either IT or HR.

---

# 23. OR Truth Table

| A     | B     | A OR B |
| ----- | ----- | ------ |
| TRUE  | TRUE  | TRUE   |
| TRUE  | FALSE | TRUE   |
| FALSE | TRUE  | TRUE   |
| FALSE | FALSE | FALSE  |

---

# 24. NOT Operator

`NOT` reverses a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

This means:

```text
department is not IT
```

Another example:

```sql
SELECT *
FROM employees
WHERE NOT salary > 50000;
```

Conceptually, this selects rows where the comparison is not true; NULL introduces SQL's three-valued logic.

---

# 25. Combining AND and OR

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 60000
OR age > 30;
```

For clarity, use parentheses:

```sql
SELECT *
FROM employees
WHERE
    (department = 'IT' AND salary > 60000)
    OR age > 30;
```

This clearly defines the intended logic.

---

# 26. Parentheses in Logical Conditions

Consider:

```sql
WHERE A OR B AND C
```

SQL generally evaluates `AND` before `OR`.

So it is interpreted approximately as:

```text
A OR (B AND C)
```

If you want:

```text
(A OR B) AND C
```

write it explicitly:

```sql
WHERE (A OR B) AND C
```

**Best practice:** use parentheses whenever a condition contains both `AND` and `OR`.

---

# 27. Special SQL Operators

Special operators simplify common filtering tasks.

```text
IN
NOT IN
BETWEEN
NOT BETWEEN
LIKE
NOT LIKE
IS NULL
IS NOT NULL
EXISTS
NOT EXISTS
```

---

# 28. IN Operator

`IN` checks whether a value matches any value in a list.

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

This is cleaner.

---

# 29. IN with Numbers

```sql
SELECT *
FROM employees
WHERE age IN (20, 25, 30, 35);
```

---

# 30. NOT IN

Returns rows whose value does not match any value in the list.

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

### Important NULL Issue

`NOT IN` can produce unexpected results if the list/subquery contains `NULL`, because comparisons involving NULL are not TRUE or FALSE but UNKNOWN.

For example, this can be problematic:

```sql
SELECT *
FROM employees
WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
);
```

if the subquery can return NULL.

In such cases, `NOT EXISTS` is often safer.

---

# 31. BETWEEN Operator

Checks whether a value is within an inclusive range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

Conceptually:

```text
50000 <= salary <= 80000
```

The lower and upper values are included.

---

# 32. NOT BETWEEN

```sql
SELECT *
FROM employees
WHERE salary NOT BETWEEN 50000 AND 80000;
```

Returns values outside the inclusive range.

---

# 33. BETWEEN with Dates

```sql
SELECT *
FROM employees
WHERE joining_date
BETWEEN '2025-01-01' AND '2025-12-31';
```

For timestamp columns, be careful with inclusive end dates. A half-open range is often safer:

```sql
SELECT *
FROM employees
WHERE joining_timestamp >= '2025-01-01'
  AND joining_timestamp < '2026-01-01';
```

---

# 34. LIKE Operator

`LIKE` performs pattern matching.

It mainly uses:

```text
% → Zero or more characters
_ → Exactly one character
```

---

# 35. LIKE — Starts With

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Matches:

```text
Arun
Anita
Amit
```

---

# 36. LIKE — Ends With

```sql
SELECT *
FROM employees
WHERE name LIKE '%a';
```

Matches names ending with `a`, subject to the database's collation/case-sensitivity behavior.

---

# 37. LIKE — Contains

```sql
SELECT *
FROM employees
WHERE name LIKE '%an%';
```

Matches names containing `an`.

---

# 38. LIKE — One Character

`_` represents exactly one character.

```sql
SELECT *
FROM employees
WHERE name LIKE 'A_i%';
```

The pattern means:

```text
A
↓
exactly one character
↓
i
↓
zero or more characters
```

---

# 39. NOT LIKE

Returns rows that do not match the pattern.

```sql
SELECT *
FROM employees
WHERE name NOT LIKE 'A%';
```

---

# 40. IS NULL Operator

`NULL` represents a missing/unknown/not-applicable value.

To test for NULL:

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

---

# 41. IS NOT NULL

```sql
SELECT *
FROM employees
WHERE email IS NOT NULL;
```

---

# 42. Why `= NULL` Does Not Work

Incorrect:

```sql
SELECT *
FROM employees
WHERE email = NULL;
```

Correct:

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

SQL uses three-valued logic:

```text
TRUE
FALSE
UNKNOWN
```

Comparisons with NULL generally produce `UNKNOWN`.

---

# 43. EXISTS Operator

`EXISTS` checks whether a subquery returns at least one row.

Example:

```sql
SELECT *
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

Meaning:

```text
For each department:
    Does at least one employee exist?
```

If yes, the department is returned.

---

# 44. NOT EXISTS

Checks whether the subquery returns no rows.

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

# 45. EXISTS vs IN

Both can be used for related filtering tasks.

Using `IN`:

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

Using `EXISTS`:

```sql
SELECT *
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
      AND d.department_name = 'IT'
);
```

Which is better depends on the query, data, indexes, and DBMS optimizer. Don't assume one is always faster.

---

# 46. String Concatenation Operators

String concatenation syntax differs between DBMSs.

### Standard-style / PostgreSQL

```sql
SELECT first_name || ' ' || last_name AS full_name
FROM employees;
```

### MySQL

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

### SQL Server

```sql
SELECT first_name + ' ' + last_name AS full_name
FROM employees;
```

Be careful with NULL behavior because it can vary by DBMS/settings.

---

# 47. Bitwise Operators

Some DBMSs support bitwise operations.

Common operators include:

```text
&   Bitwise AND
|   Bitwise OR
^   Bitwise XOR
~   Bitwise NOT
<<  Left shift
>>  Right shift
```

Exact support and syntax vary by DBMS.

---

# 48. Bitwise AND

Example:

```sql
SELECT 5 & 3 AS result;
```

Binary representation:

```text
5 = 101
3 = 011
---------
    001
```

Result:

```text
1
```

Bitwise operations are generally more relevant to specialized technical applications than ordinary data analytics.

---

# 49. Bitwise OR

```sql
SELECT 5 | 3 AS result;
```

Binary:

```text
101
011
---
111
```

Result:

```text
7
```

---

# 50. Bitwise XOR

In DBMSs that support `^` for XOR:

```sql
SELECT 5 ^ 3 AS result;
```

Binary:

```text
101
011
---
110
```

Result:

```text
6
```

Check your DBMS because operator meanings can differ.

---

# 51. Set Operators

Set operators combine the results of separate `SELECT` statements.

Main set operators:

```text
UNION
UNION ALL
INTERSECT
EXCEPT
```

These are sometimes called set operations rather than ordinary row-level operators.

---

# 52. UNION

Combines results and removes duplicate rows.

```sql
SELECT name
FROM employees_it

UNION

SELECT name
FROM employees_hr;
```

---

# 53. UNION ALL

Combines results without removing duplicates.

```sql
SELECT name
FROM employees_it

UNION ALL

SELECT name
FROM employees_hr;
```

`UNION ALL` is often preferable when duplicates are meaningful or when you know the inputs cannot overlap, because it avoids duplicate elimination.

---

# 54. INTERSECT

Returns rows appearing in both result sets.

```sql
SELECT employee_id
FROM project_a

INTERSECT

SELECT employee_id
FROM project_b;
```

This means:

```text
Employees in Project A
        AND
Employees in Project B
```

Support varies by DBMS/version.

---

# 55. EXCEPT

Returns rows from the first result that are absent from the second.

```sql
SELECT employee_id
FROM project_a

EXCEPT

SELECT employee_id
FROM project_b;
```

Meaning:

```text
Project A
minus
Project B
```

Some DBMSs use `MINUS` instead.

---

# 56. Operator Categories — Quick Table

| Category       | Operators                                   |                         |
| -------------- | ------------------------------------------- | ----------------------- |
| Arithmetic     | `+`, `-`, `*`, `/`, `%`                     |                         |
| Comparison     | `=`, `<>`, `!=`, `>`, `<`, `>=`, `<=`       |                         |
| Logical        | `AND`, `OR`, `NOT`                          |                         |
| Membership     | `IN`, `NOT IN`                              |                         |
| Range          | `BETWEEN`, `NOT BETWEEN`                    |                         |
| Pattern        | `LIKE`, `NOT LIKE`                          |                         |
| NULL           | `IS NULL`, `IS NOT NULL`                    |                         |
| Existence      | `EXISTS`, `NOT EXISTS`                      |                         |
| Bitwise        | `&`, `                                      | `, `^`, `~`, `<<`, `>>` |
| Set operations | `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT` |                         |

---

# 57. Operators with WHERE

The `WHERE` clause is where you will use operators most frequently.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Multiple operators:

```sql
SELECT *
FROM employees
WHERE salary >= 50000
AND department IN ('IT', 'HR')
AND name LIKE 'A%';
```

---

# 58. Operators with HAVING

Operators are also used with aggregated values.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 59. Operators with CASE

Comparison operators are commonly used inside `CASE`.

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

# 60. Operators in JOIN Conditions

Comparison operators are commonly used in joins.

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

The `=` operator creates the matching condition.

---

# 61. Multiple Operators in a Real Query

```sql
SELECT
    name,
    salary,
    department
FROM employees
WHERE
    salary BETWEEN 50000 AND 100000
    AND department IN ('IT', 'Finance')
    AND name LIKE 'A%'
    AND email IS NOT NULL
ORDER BY salary DESC;
```

This uses:

```text
BETWEEN
AND
IN
LIKE
IS NOT NULL
ORDER BY
```

---

# 62. SQL Three-Valued Logic

This is an important theoretical concept.

SQL conditions can produce:

```text
TRUE
FALSE
UNKNOWN
```

`UNKNOWN` commonly occurs because of `NULL`.

Example:

```sql
SELECT *
FROM employees
WHERE salary > NULL;
```

The comparison does not become TRUE.

It evaluates to UNKNOWN.

Therefore, the row does not pass the `WHERE` filter.

---

# 63. TRUE / FALSE / UNKNOWN with AND

Important examples:

```text
TRUE AND TRUE      → TRUE
TRUE AND FALSE     → FALSE
TRUE AND UNKNOWN   → UNKNOWN
FALSE AND UNKNOWN  → FALSE
UNKNOWN AND UNKNOWN → UNKNOWN
```

---

# 64. TRUE / FALSE / UNKNOWN with OR

```text
TRUE OR UNKNOWN     → TRUE
FALSE OR UNKNOWN    → UNKNOWN
FALSE OR FALSE      → FALSE
UNKNOWN OR UNKNOWN  → UNKNOWN
```

This explains why NULL can produce surprising filtering results.

---

# 65. NULL and NOT

Suppose:

```sql
salary = NULL
```

is UNKNOWN.

Then:

```sql
NOT (salary = NULL)
```

is still UNKNOWN, not TRUE.

Therefore:

```sql
WHERE NOT salary = NULL
```

does not correctly find non-NULL salaries.

Use:

```sql
WHERE salary IS NOT NULL
```

---

# 66. Operator Precedence

A simplified logical precedence order is:

```text
1. Parentheses
2. Arithmetic operations
3. Comparison operators
4. NOT
5. AND
6. OR
```

Example:

```sql
WHERE NOT age < 30
AND salary > 50000
OR department = 'IT'
```

For readability, write:

```sql
WHERE
    (NOT (age < 30) AND salary > 50000)
    OR department = 'IT';
```

When in doubt, use parentheses.

---

# 67. Arithmetic vs Comparison vs Logical

Consider:

```sql
SELECT *
FROM employees
WHERE salary * 12 > 600000
AND age >= 25;
```

There are three types of operations:

```text
salary * 12
    ↓
Arithmetic

> 600000
    ↓
Comparison

AND
    ↓
Logical
```

---

# 68. Operators in Data Analytics

Operators are essential in analytics.

### Filtering

```sql
WHERE sales > 10000
```

### Customer segmentation

```sql
WHERE age BETWEEN 18 AND 30
```

### Category filtering

```sql
WHERE region IN ('North', 'South')
```

### Pattern analysis

```sql
WHERE customer_name LIKE 'A%'
```

### Missing data

```sql
WHERE email IS NULL
```

### Conditional metrics

```sql
SUM(
    CASE
        WHEN sales > 10000 THEN sales
        ELSE 0
    END
)
```

### Date filtering

```sql
WHERE order_date >= '2026-01-01'
```

---

# 69. Practical Data Analytics Example

Suppose we have:

```text
sales
----------------------------------------
order_id
customer
region
quantity
price
sales_amount
```

Find orders where:

```text
sales_amount > 10000
AND
region is North or South
AND
quantity is between 5 and 20
```

Query:

```sql
SELECT *
FROM sales
WHERE sales_amount > 10000
AND region IN ('North', 'South')
AND quantity BETWEEN 5 AND 20;
```

Operators used:

```text
>        Comparison
AND      Logical
IN       Membership
BETWEEN  Range
```

---

# 70. Practical Analytics Example — Customer Classification

```sql
SELECT
    customer,
    sales_amount,
    CASE
        WHEN sales_amount >= 100000 THEN 'Premium'
        WHEN sales_amount >= 50000 THEN 'Regular'
        ELSE 'Basic'
    END AS customer_category
FROM sales;
```

Operators:

```text
>=
CASE
WHEN
```

---

# 71. Practical Analytics Example — Profit

Suppose:

```text
revenue
cost
```

Calculate profit:

```sql
SELECT
    revenue,
    cost,
    revenue - cost AS profit
FROM sales;
```

Calculate profit margin:

```sql
SELECT
    revenue,
    cost,
    (revenue - cost) / NULLIF(revenue, 0) * 100
        AS profit_margin
FROM sales;
```

Operators used:

```text
-
/
*
```

along with:

```text
NULLIF()
```

to avoid division by zero.

---

# 72. Operator Selection Guide

When you want to:

```text
Compare two values
→ =, <>, >, <, >=, <=

Combine conditions
→ AND, OR

Reverse condition
→ NOT

Check several possible values
→ IN

Check a range
→ BETWEEN

Search a text pattern
→ LIKE

Check missing value
→ IS NULL

Check non-missing value
→ IS NOT NULL

Check whether related rows exist
→ EXISTS

Perform calculations
→ +, -, *, /, %

Combine result sets
→ UNION, UNION ALL, INTERSECT, EXCEPT

Perform bit-level operations
→ Bitwise operators
```

---

# 73. Most Important Operators for SQL Interviews

Prioritize these:

```text
1. =
2. <>
3. >
4. <
5. >=
6. <=
7. AND
8. OR
9. NOT
10. IN
11. NOT IN
12. BETWEEN
13. NOT BETWEEN
14. LIKE
15. NOT LIKE
16. IS NULL
17. IS NOT NULL
18. EXISTS
19. NOT EXISTS
20. +
21. -
22. *
23. /
24. %
25. UNION
26. UNION ALL
27. INTERSECT
28. EXCEPT
```

---

# 74. Most Important Operators for Data Analytics

For data analytics, focus especially on:

```text
WHERE
    ↓
=, >, <, >=, <=
    ↓
AND / OR / NOT
    ↓
IN / BETWEEN / LIKE
    ↓
IS NULL / IS NOT NULL
    ↓
CASE
    ↓
Arithmetic operators
    ↓
GROUP BY + HAVING
    ↓
JOIN conditions
    ↓
EXISTS / NOT EXISTS
    ↓
Window functions
```

---

# 75. Complete SQL Operators Cheat Sheet

```sql
-- =========================
-- ARITHMETIC
-- =========================

SELECT 10 + 5;
SELECT 10 - 5;
SELECT 10 * 5;
SELECT 10 / 5;
SELECT 10 % 3;


-- =========================
-- COMPARISON
-- =========================

SELECT *
FROM employees
WHERE salary = 50000;

SELECT *
FROM employees
WHERE salary <> 50000;

SELECT *
FROM employees
WHERE salary > 50000;

SELECT *
FROM employees
WHERE salary < 50000;

SELECT *
FROM employees
WHERE salary >= 50000;

SELECT *
FROM employees
WHERE salary <= 50000;


-- =========================
-- LOGICAL
-- =========================

SELECT *
FROM employees
WHERE age > 25
AND salary > 50000;

SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';

SELECT *
FROM employees
WHERE NOT department = 'IT';


-- =========================
-- IN
-- =========================

SELECT *
FROM employees
WHERE department IN ('IT', 'HR');


-- =========================
-- NOT IN
-- =========================

SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');


-- =========================
-- BETWEEN
-- =========================

SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 80000;


-- =========================
-- NOT BETWEEN
-- =========================

SELECT *
FROM employees
WHERE salary NOT BETWEEN 50000 AND 80000;


-- =========================
-- LIKE
-- =========================

SELECT *
FROM employees
WHERE name LIKE 'A%';

SELECT *
FROM employees
WHERE name LIKE '%a';

SELECT *
FROM employees
WHERE name LIKE '%an%';

SELECT *
FROM employees
WHERE name LIKE 'A_i%';


-- =========================
-- NOT LIKE
-- =========================

SELECT *
FROM employees
WHERE name NOT LIKE 'A%';


-- =========================
-- NULL
-- =========================

SELECT *
FROM employees
WHERE email IS NULL;

SELECT *
FROM employees
WHERE email IS NOT NULL;


-- =========================
-- EXISTS
-- =========================

SELECT *
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);


-- =========================
-- NOT EXISTS
-- =========================

SELECT *
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);


-- =========================
-- SET OPERATIONS
-- =========================

SELECT name FROM employees_it
UNION
SELECT name FROM employees_hr;


SELECT name FROM employees_it
UNION ALL
SELECT name FROM employees_hr;


SELECT employee_id FROM project_a
INTERSECT
SELECT employee_id FROM project_b;


SELECT employee_id FROM project_a
EXCEPT
SELECT employee_id FROM project_b;
```

---

# 76. Final Revision Map

```text
                         SQL OPERATORS
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
    ARITHMETIC           COMPARISON             LOGICAL
        │                     │                     │
   + - * / %           = <> != > <            AND OR NOT
                        >= <=
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                       SPECIAL OPERATORS
                              │
          ┌───────────┬───────┼────────┬──────────┐
          │           │       │        │          │
         IN       BETWEEN    LIKE     NULL     EXISTS
       NOT IN    NOT BETWEEN NOT LIKE          NOT EXISTS
          │           │       │        │          │
          └───────────┴───────┴────────┴──────────┘
                              │
                        SET OPERATIONS
                              │
             UNION / UNION ALL / INTERSECT / EXCEPT
```

## One-Line Revision

```text
Arithmetic → Calculate
Comparison → Compare
Logical → Combine conditions
IN → Match a list
BETWEEN → Match a range
LIKE → Match a pattern
IS NULL → Find missing values
EXISTS → Check whether rows exist
Set operators → Combine query results
```

## Golden Rule

For most SQL data-analysis queries, think in this order:

```text
What data?
    ↓
FROM / JOIN

Which rows?
    ↓
WHERE

How should they be grouped?
    ↓
GROUP BY

Which groups?
    ↓
HAVING

What should I calculate/display?
    ↓
SELECT

How should results be arranged?
    ↓
ORDER BY
```

This operator knowledge is the foundation for writing **SQL queries for data analytics, reporting, dashboards, and SQL interviews**.
