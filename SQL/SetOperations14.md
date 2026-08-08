# SQL — JOIN Analysis, Subqueries, Subquery Operators & Set Operations

This README covers four important SQL topics:

1. **JOIN Analysis**
2. **Subqueries**
3. **Subquery Operators**
4. **Set Operations**

These concepts are especially important for:

* SQL programming
* Data analytics
* Data engineering
* Business intelligence
* Reporting
* Database interviews
* Complex SQL queries

---

# Table of Contents

* [1. JOIN Analysis](#1-join-analysis)

  * [Understanding JOIN Results](#understanding-join-results)
  * [JOIN Cardinality](#join-cardinality)
  * [One-to-One JOIN](#one-to-one-join)
  * [One-to-Many JOIN](#one-to-many-join)
  * [Many-to-Many JOIN](#many-to-many-join)
  * [JOIN Multiplication](#join-multiplication)
  * [Duplicate Rows](#duplicate-rows)
  * [Grain of Data](#grain-of-data)
  * [JOIN and Aggregation](#join-and-aggregation)
  * [JOIN and Double Counting](#join-and-double-counting)
  * [JOIN Analysis Patterns](#join-analysis-patterns)

* [2. Subqueries](#2-subqueries)

  * [What is a Subquery](#what-is-a-subquery)
  * [Why Use Subqueries](#why-use-subqueries)
  * [Types of Subqueries](#types-of-subqueries)
  * [Scalar Subquery](#scalar-subquery)
  * [Single-Row Subquery](#single-row-subquery)
  * [Multi-Row Subquery](#multi-row-subquery)
  * [Multi-Column Subquery](#multi-column-subquery)
  * [Correlated Subquery](#correlated-subquery)
  * [Nested Subquery](#nested-subquery)
  * [Subquery in SELECT](#subquery-in-select)
  * [Subquery in FROM](#subquery-in-from)
  * [Subquery in WHERE](#subquery-in-where)
  * [Subquery in HAVING](#subquery-in-having)
  * [EXISTS Subquery](#exists-subquery)

* [3. Subquery Operators](#3-subquery-operators)

  * [IN](#in)
  * [NOT IN](#not-in)
  * [EXISTS](#exists)
  * [NOT EXISTS](#not-exists)
  * [ANY](#any)
  * [SOME](#some)
  * [ALL](#all)
  * [Comparison Operators](#comparison-operators)
  * [Operator Selection Guide](#operator-selection-guide)

* [4. Set Operations](#4-set-operations)

  * [UNION](#union)
  * [UNION ALL](#union-all)
  * [INTERSECT](#intersect)
  * [EXCEPT](#except)
  * [MINUS](#minus)
  * [Set Operation Rules](#set-operation-rules)
  * [JOIN vs Set Operations](#join-vs-set-operations)

* [5. Practical Analytics Examples](#5-practical-analytics-examples)

* [6. Common Mistakes](#6-common-mistakes)

* [7. Interview Questions](#7-interview-questions)

* [8. Quick Revision Cheat Sheet](#8-quick-revision-cheat-sheet)

---

# 1. JOIN Analysis

## What is JOIN Analysis?

JOIN analysis means understanding:

* Which tables are being joined
* How tables are related
* Which columns are used for matching
* How many rows will be produced
* Whether duplicate rows can occur
* What happens to unmatched rows
* Whether aggregation can cause double counting
* What the grain of the result is

Knowing JOIN syntax is not enough.

For data analytics, you must understand **what happens to the data after the JOIN**.

---

# Understanding JOIN Results

Consider two tables.

### Customers

| customer_id | customer_name |
| ----------: | ------------- |
|           1 | Rahul         |
|           2 | Priya         |
|           3 | Amit          |

### Orders

| order_id | customer_id | amount |
| -------: | ----------: | -----: |
|      101 |           1 |    500 |
|      102 |           1 |    800 |
|      103 |           2 |    300 |
|      104 |           5 |    900 |

Relationship:

```text
customers.customer_id
          ↓
orders.customer_id
```

Customer `1` has two orders.

Customer `2` has one order.

Customer `3` has no order.

Order `104` references customer `5`, which doesn't exist.

---

# INNER JOIN Analysis

```sql
SELECT
    c.customer_id,
    c.customer_name,
    o.order_id,
    o.amount
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result:

| customer_id | customer_name | order_id | amount |
| ----------: | ------------- | -------: | -----: |
|           1 | Rahul         |      101 |    500 |
|           1 | Rahul         |      102 |    800 |
|           2 | Priya         |      103 |    300 |

Notice:

```text
Customer 3 → removed
Order 104   → removed
```

because there is no matching record.

---

# LEFT JOIN Analysis

```sql
SELECT
    c.customer_id,
    c.customer_name,
    o.order_id,
    o.amount
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result:

| customer_id | customer_name | order_id | amount |
| ----------: | ------------- | -------: | -----: |
|           1 | Rahul         |      101 |    500 |
|           1 | Rahul         |      102 |    800 |
|           2 | Priya         |      103 |    300 |
|           3 | Amit          |     NULL |   NULL |

The left table is preserved.

Therefore:

```text
LEFT JOIN
    ↓
All rows from left table
+
Matching rows from right table
```

---

# JOIN Cardinality

**Cardinality** describes how rows in one table relate to rows in another table.

Main relationships:

```text
1 : 1
1 : Many
Many : 1
Many : Many
```

Understanding cardinality is critical for JOIN analysis.

---

# One-to-One JOIN

One row in table A corresponds to one row in table B.

Example:

```text
users
   ↓
user_profiles
```

One user has one profile.

```sql
SELECT
    u.user_id,
    u.name,
    p.address
FROM users u
JOIN user_profiles p
    ON u.user_id = p.user_id;
```

Expected behavior:

```text
1 user → 1 profile
```

---

# One-to-Many JOIN

This is extremely common.

Example:

```text
Customer
    ↓
Many Orders
```

```sql
SELECT
    c.customer_id,
    c.customer_name,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

If Rahul has 3 orders:

```text
Rahul → Order 101
Rahul → Order 102
Rahul → Order 103
```

Rahul appears three times.

This is normal.

---

# Many-to-One JOIN

The reverse relationship:

```text
Many Orders
     ↓
One Customer
```

Many orders can belong to one customer.

```text
orders.customer_id
        ↓
customers.customer_id
```

---

# Many-to-Many JOIN

Example:

```text
Students
    ↕
Courses
```

A student can take many courses.

A course can have many students.

A junction table is normally used:

```text
students
    ↓
student_courses
    ↓
courses
```

Query:

```sql
SELECT
    s.student_name,
    c.course_name
FROM students s
JOIN student_courses sc
    ON s.student_id = sc.student_id
JOIN courses c
    ON sc.course_id = c.course_id;
```

---

# JOIN Multiplication

One of the most important concepts in SQL analytics is **row multiplication**.

Suppose:

```text
Customer
    ↓
3 Orders
```

Joining produces three rows.

Now suppose each order has four items:

```text
Customer
   ↓
3 Orders
   ↓
4 Items per Order
```

The final result can contain:

```text
3 × 4 = 12
```

rows for that customer's order items.

This is not necessarily an error.

It is a consequence of the relationship between the tables.

---

# Example of JOIN Multiplication

### Orders

| order_id | customer_id |
| -------: | ----------: |
|        1 |          10 |
|        2 |          10 |

### Payments

| payment_id | order_id | amount |
| ---------: | -------: | -----: |
|          1 |        1 |     50 |
|          2 |        1 |     50 |
|          3 |        2 |    100 |

Query:

```sql
SELECT
    o.order_id,
    o.customer_id,
    p.payment_id,
    p.amount
FROM orders o
JOIN payments p
    ON o.order_id = p.order_id;
```

Result:

| order_id | customer_id | payment_id | amount |
| -------: | ----------: | ---------: | -----: |
|        1 |          10 |          1 |     50 |
|        1 |          10 |          2 |     50 |
|        2 |          10 |          3 |    100 |

Order `1` appears twice because it has two payments.

---

# Duplicate Rows

A JOIN can appear to create duplicates.

For example:

```text
Customer 1
Order 101
Order 102
```

Result:

```text
Customer 1 → Order 101
Customer 1 → Order 102
```

The customer is repeated, but the rows are not necessarily duplicates.

They represent different orders.

---

# Real Duplicate vs JOIN Multiplication

### Real duplicate

Two rows contain exactly the same logical information.

### JOIN multiplication

The same parent appears multiple times because it has multiple child records.

Important:

> Do not use `DISTINCT` blindly to fix JOIN problems.

First determine why multiple rows exist.

---

# Grain of Data

**Grain** means:

> What does one row represent?

Examples:

```text
customers
→ 1 row = 1 customer

orders
→ 1 row = 1 order

order_items
→ 1 row = 1 order item

payments
→ 1 row = 1 payment
```

Before writing a JOIN, always ask:

```text
What does one row represent?
```

---

# Why Grain Matters

Suppose:

```text
orders
1 row = 1 order
```

and:

```text
order_items
1 row = 1 product within an order
```

After joining:

```text
orders
    ↓
order_items
```

the result is no longer:

```text
1 row = 1 order
```

It becomes:

```text
1 row = 1 order item
```

This matters when calculating:

```text
COUNT
SUM
AVG
MIN
MAX
```

---

# JOIN and Aggregation

Consider:

```sql
SELECT
    c.customer_id,
    SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id;
```

This calculates total order value per customer.

---

# JOIN and Double Counting

Suppose:

### Orders

| order_id | amount |
| -------: | -----: |
|        1 |    100 |

### Payments

| payment_id | order_id | amount |
| ---------: | -------: | -----: |
|          1 |        1 |     50 |
|          2 |        1 |     50 |

If we do:

```sql
SELECT
    SUM(o.amount)
FROM orders o
JOIN payments p
    ON o.order_id = p.order_id;
```

The order appears twice.

The result becomes:

```text
100 + 100 = 200
```

instead of:

```text
100
```

This is a classic **double-counting problem**.

---

# Preventing Double Counting

Aggregate the many-side table first.

```sql
WITH payment_summary AS (
    SELECT
        order_id,
        SUM(amount) AS total_payment
    FROM payments
    GROUP BY order_id
)

SELECT
    o.order_id,
    o.amount,
    p.total_payment
FROM orders o
LEFT JOIN payment_summary p
    ON o.order_id = p.order_id;
```

Now there is only one payment-summary row per order.

---

# JOIN Analysis Checklist

Before executing a JOIN, ask:

```text
1. What are the two tables?
2. What is the relationship?
3. What is the JOIN key?
4. Is the key unique?
5. Is it 1:1?
6. Is it 1:Many?
7. Is it Many:Many?
8. Which table must be preserved?
9. What will be the grain after JOIN?
10. Can rows multiply?
11. Can aggregation double-count?
12. Are NULL values involved?
```

---

# Common JOIN Analysis Patterns

## Find customers without orders

```sql
SELECT
    c.*
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

---

## Find orders without customers

```sql
SELECT
    o.*
FROM orders o
LEFT JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

---

## Find customers who have at least one order

```sql
SELECT DISTINCT
    c.*
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Or use `EXISTS`:

```sql
SELECT
    c.*
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# 2. Subqueries

## What is a Subquery?

A **subquery** is a SQL query written inside another SQL query.

It is also called:

* Inner query
* Nested query
* Inner SELECT

The outer query is called:

```text
Outer Query
```

The query inside it is called:

```text
Subquery
```

---

# Basic Subquery Structure

```sql
SELECT columns
FROM table
WHERE column IN (
    SELECT column
    FROM another_table
);
```

The inner query executes logically to produce a result that the outer query uses.

---

# Simple Example

Find customers who have placed orders:

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

Inner query:

```sql
SELECT customer_id
FROM orders;
```

Outer query:

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id IN (...);
```

---

# Why Use Subqueries?

Subqueries are useful for:

* Filtering based on another query
* Comparing values with calculated results
* Finding maximum/minimum values
* Checking existence
* Creating temporary result sets
* Breaking complex problems into smaller parts
* Performing nested analysis
* Correlated analysis

---

# Types of Subqueries

Important categories:

```text
1. Scalar Subquery
2. Single-Row Subquery
3. Multi-Row Subquery
4. Multi-Column Subquery
5. Correlated Subquery
6. Non-Correlated Subquery
7. Nested Subquery
8. Subquery in SELECT
9. Subquery in FROM
10. Subquery in WHERE
11. Subquery in HAVING
```

---

# Scalar Subquery

A scalar subquery returns exactly **one value**.

Example:

```sql
SELECT
    AVG(salary)
FROM employees;
```

Suppose result:

```text
65000
```

We can use it:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The subquery returns one value:

```text
65000
```

Then the outer query finds employees earning more than 65000.

---

# Single-Row Subquery

A single-row subquery returns one row.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

The subquery returns one value:

```text
120000
```

The outer query finds the employee with that salary.

---

# Multi-Row Subquery

A multi-row subquery returns multiple rows.

Example:

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

The inner query may return:

```text
1
2
5
7
9
```

Therefore, `IN` is appropriate.

---

# Multi-Column Subquery

A subquery can return multiple columns.

Example:

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM employees
WHERE (department_id, salary) IN (
    SELECT
        department_id,
        MAX(salary)
    FROM employees
    GROUP BY department_id
);
```

This searches for employees whose:

```text
department_id + salary
```

matches a department's maximum salary.

Support for row-value comparisons varies somewhat by SQL database, so syntax should be checked for your specific database.

---

# Non-Correlated Subquery

A non-correlated subquery does not depend on the outer query.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query can be evaluated independently.

---

# Correlated Subquery

A correlated subquery depends on the current row of the outer query.

Example:

```sql
SELECT
    e.employee_name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

The inner query references:

```text
e.department_id
```

from the outer query.

Therefore, the subquery is correlated.

---

# Correlated Subquery Mental Model

Conceptually:

```text
Outer row
    ↓
Run subquery using outer row's value
    ↓
Compare result
    ↓
Move to next outer row
    ↓
Repeat
```

This makes correlated subqueries powerful, but potentially expensive on large datasets.

---

# Correlated Subquery Example

Find employees who earn more than their department average:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

For every employee, the subquery calculates the average salary for that employee's department.

---

# Subquery in WHERE

The most common usage.

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Subquery in FROM

A subquery in the `FROM` clause creates a derived table.

Example:

```sql
SELECT
    department_id,
    average_salary
FROM (
    SELECT
        department_id,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department_id
) AS dept_summary;
```

The subquery creates:

```text
dept_summary
```

which behaves like a temporary result table for that query.

---

# Subquery in SELECT

A scalar subquery can be used in the SELECT list.

```sql
SELECT
    employee_name,
    salary,
    (
        SELECT AVG(salary)
        FROM employees
    ) AS company_avg_salary
FROM employees;
```

Result conceptually:

| employee_name | salary | company_avg_salary |
| ------------- | -----: | -----------------: |
| Rahul         |  50000 |              65000 |
| Priya         |  70000 |              65000 |
| Amit          |  75000 |              65000 |

---

# Subquery in HAVING

Example:

```sql
SELECT
    department_id,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM employees
);
```

This finds departments whose average salary is above the company-wide average.

---

# Subquery in FROM vs WHERE

### FROM

Used to create a temporary result set:

```sql
SELECT *
FROM (
    SELECT ...
) AS x;
```

### WHERE

Used for filtering:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Nested Subquery

A subquery can contain another subquery.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id = (
        SELECT department_id
        FROM departments
        WHERE department_name = 'IT'
    )
);
```

Conceptually:

```text
Outer Query
    ↓
Subquery
    ↓
Nested Subquery
```

Avoid excessive nesting when a JOIN or CTE makes the logic clearer.

---

# 3. Subquery Operators

Subquery operators determine how the result of a subquery is used.

Important operators:

```text
IN
NOT IN
EXISTS
NOT EXISTS
ANY
SOME
ALL
=
<>
!=
>
<
>=
<=
```

---

# IN

`IN` checks whether a value exists in the result of a subquery.

Example:

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

If the subquery returns:

```text
1
2
4
7
```

the outer query selects customers with IDs:

```text
1, 2, 4, 7
```

---

# IN with Multiple Values

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Hyderabad'
);
```

Meaning:

> Find employees belonging to departments located in Hyderabad.

---

# NOT IN

`NOT IN` finds values that do not appear in the subquery result.

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
);
```

This attempts to find customers without orders.

---

# Important NOT IN + NULL Problem

Suppose the subquery returns:

```text
1
2
NULL
```

Then:

```sql
WHERE customer_id NOT IN (...)
```

can produce unexpected results because SQL uses three-valued logic involving `NULL`.

For anti-matching logic, `NOT EXISTS` is often safer.

---

# EXISTS

`EXISTS` checks whether the subquery returns **at least one row**.

Example:

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Meaning:

> Return customers for whom at least one order exists.

---

# Why SELECT 1 in EXISTS?

You may see:

```sql
SELECT 1
```

inside `EXISTS`.

Example:

```sql
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

The actual selected value doesn't matter.

`EXISTS` only cares whether at least one matching row exists.

Therefore, these are conceptually equivalent:

```sql
SELECT 1
```

and:

```sql
SELECT *
```

inside an `EXISTS` test.

---

# NOT EXISTS

`NOT EXISTS` checks whether no matching row exists.

Example:

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

This finds customers without orders.

---

# EXISTS vs IN

Both can be used to test relationships.

### IN

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

### EXISTS

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Conceptually:

```text
IN
→ Is this value in the returned set?

EXISTS
→ Does at least one matching row exist?
```

The optimizer may transform these logically, so performance depends on the database, indexes, data distribution, and query shape.

---

# EXISTS vs JOIN

Suppose we want customers who have orders.

JOIN:

```sql
SELECT DISTINCT
    c.customer_id,
    c.customer_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

EXISTS:

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

`EXISTS` is often a natural choice when you only need to know whether a related row exists and do not need columns from the related table.

---

# ANY

`ANY` compares a value with values returned by a subquery.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

Meaning:

> Salary is greater than at least one salary returned by the subquery.

---

# ANY Example

Suppose the subquery returns:

```text
30000
50000
70000
```

Condition:

```sql
salary > ANY (...)
```

means:

```text
salary > 30000
OR
salary > 50000
OR
salary > 70000
```

Conceptually, for a nonempty set, this behaves like being greater than the minimum value.

---

# SOME

`SOME` is generally a synonym for `ANY`.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > SOME (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

In supported SQL dialects:

```text
ANY ≈ SOME
```

---

# ALL

`ALL` requires the comparison to be true for every value returned by the subquery.

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

Meaning:

> Salary is greater than every salary in department 10.

For a nonempty set, this corresponds conceptually to being greater than the maximum value.

---

# ANY vs ALL

Suppose subquery returns:

```text
30000
50000
70000
```

### `> ANY`

```sql
salary > ANY (...)
```

Means:

```text
salary > at least one value
```

Effectively:

```text
salary > 30000
```

for a nonempty set.

### `> ALL`

```sql
salary > ALL (...)
```

Means:

```text
salary > every value
```

Effectively:

```text
salary > 70000
```

for a nonempty set.

---

# Comparison Operators with Subqueries

A scalar subquery can be used with:

```text
=
<>
!=
>
<
>=
<=
```

Example:

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

# Greater Than Subquery

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Less Than Subquery

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary < (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Not Equal Subquery

```sql
SELECT
    employee_name,
    department_id
FROM employees
WHERE department_id <> (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

This requires the subquery to return exactly one row.

---

# Operator Selection Guide

| Requirement                      | Operator     |
| -------------------------------- | ------------ |
| Match one returned value         | `=`          |
| Match multiple returned values   | `IN`         |
| Exclude multiple returned values | `NOT IN`     |
| At least one matching row        | `EXISTS`     |
| No matching row                  | `NOT EXISTS` |
| Greater than at least one        | `> ANY`      |
| Greater than every value         | `> ALL`      |
| Less than at least one           | `< ANY`      |
| Less than every value            | `< ALL`      |

---

# 4. Set Operations

## What are Set Operations?

Set operations combine the results of two or more `SELECT` queries.

Important set operations:

```text
UNION
UNION ALL
INTERSECT
EXCEPT
MINUS
```

Unlike JOINs, set operations generally combine result sets **vertically**.

---

# JOIN vs SET Operation

### JOIN

Combines columns horizontally:

```text
Table A       Table B
   ↓             ↓
       JOIN
         ↓
More columns
```

### SET OPERATION

Combines rows vertically:

```text
Query A
   ↓
UNION
   ↓
Query B
   ↓
More rows
```

Remember:

```text
JOIN
→ Horizontal combination

SET OPERATION
→ Vertical combination
```

---

# Set Operation Requirements

The SELECT queries generally need:

1. Same number of columns
2. Corresponding columns with compatible data types
3. Columns in the same logical order

Example:

```sql
SELECT
    customer_id,
    customer_name
FROM customers_2025

UNION

SELECT
    customer_id,
    customer_name
FROM customers_2026;
```

Both queries return:

```text
2 columns
```

---

# UNION

`UNION` combines results and removes duplicate rows.

Syntax:

```sql
SELECT column1, column2
FROM table1

UNION

SELECT column1, column2
FROM table2;
```

---

# UNION Example

Table 2025:

| customer_id | name  |
| ----------: | ----- |
|           1 | Rahul |
|           2 | Priya |

Table 2026:

| customer_id | name  |
| ----------: | ----- |
|           2 | Priya |
|           3 | Amit  |

Query:

```sql
SELECT
    customer_id,
    name
FROM customers_2025

UNION

SELECT
    customer_id,
    name
FROM customers_2026;
```

Result:

| customer_id | name  |
| ----------: | ----- |
|           1 | Rahul |
|           2 | Priya |
|           3 | Amit  |

`Priya` appears once.

---

# UNION Removes Duplicates

Conceptually:

```text
Query A:
1
2
3

Query B:
3
4
5

UNION:
1
2
3
4
5
```

---

# UNION ALL

`UNION ALL` combines results **without removing duplicates**.

```sql
SELECT
    customer_id,
    name
FROM customers_2025

UNION ALL

SELECT
    customer_id,
    name
FROM customers_2026;
```

Result:

| customer_id | name  |
| ----------: | ----- |
|           1 | Rahul |
|           2 | Priya |
|           2 | Priya |
|           3 | Amit  |

---

# UNION vs UNION ALL

| Feature                  | UNION     | UNION ALL   |
| ------------------------ | --------- | ----------- |
| Combines results         | Yes       | Yes         |
| Removes duplicates       | Yes       | No          |
| Usually faster           | No        | Yes         |
| Preserves duplicate rows | No        | Yes         |
| Useful for raw appending | Sometimes | Very common |

---

# Why UNION ALL is Usually Faster

`UNION` must identify duplicate rows.

Conceptually:

```text
Query A
   +
Query B
   ↓
Duplicate elimination
   ↓
Result
```

`UNION ALL` doesn't need duplicate elimination:

```text
Query A
   +
Query B
   ↓
Result
```

Therefore, `UNION ALL` is often more efficient when duplicates are intentionally allowed or impossible.

---

# INTERSECT

`INTERSECT` returns rows common to both result sets.

Example:

```sql
SELECT
    customer_id
FROM customers_2025

INTERSECT

SELECT
    customer_id
FROM customers_2026;
```

If:

```text
2025:
1
2
3

2026:
2
3
4
```

Result:

```text
2
3
```

---

# INTERSECT Meaning

Think:

```text
A ∩ B
```

Only common records.

```text
A = {1, 2, 3}
B = {2, 3, 4}

A ∩ B = {2, 3}
```

---

# INTERSECT Use Cases

Useful for:

* Finding common customers
* Comparing datasets
* Finding overlapping IDs
* Identifying users active in multiple periods
* Data validation
* Data reconciliation

---

# EXCEPT

`EXCEPT` returns rows from the first query that are not present in the second query.

Example:

```sql
SELECT
    customer_id
FROM customers_2025

EXCEPT

SELECT
    customer_id
FROM customers_2026;
```

If:

```text
2025:
1
2
3

2026:
2
3
4
```

Result:

```text
1
```

Meaning:

```text
Present in 2025
but absent in 2026
```

---

# EXCEPT Meaning

Think:

```text
A - B
```

Example:

```text
A = {1, 2, 3}
B = {2, 3, 4}

A - B = {1}
```

---

# MINUS

Some databases use:

```sql
MINUS
```

instead of:

```sql
EXCEPT
```

Example:

```sql
SELECT
    customer_id
FROM customers_2025

MINUS

SELECT
    customer_id
FROM customers_2026;
```

Conceptually:

```text
MINUS ≈ EXCEPT
```

But support depends on the database system.

---

# Set Operations Comparison

Suppose:

```text
A = {1, 2, 3}
B = {2, 3, 4}
```

### UNION

```text
{1, 2, 3, 4}
```

### UNION ALL

```text
{1, 2, 3, 2, 3, 4}
```

### INTERSECT

```text
{2, 3}
```

### EXCEPT

```text
{1}
```

---

# Set Operation Diagram

Conceptually:

```text
A                    B

┌─────────┐       ┌─────────┐
│  1      │       │      4  │
│  2  ┌───┼───────┼───┐  3  │
│  3  │   │       │   │     │
└─────┴───┘       └───┴─────┘
```

```text
UNION
→ Everything

INTERSECT
→ Common part

EXCEPT
→ Left-only part
```

---

# Set Operations and ORDER BY

Usually, `ORDER BY` is applied to the final combined result.

Example:

```sql
SELECT customer_id
FROM customers_2025

UNION

SELECT customer_id
FROM customers_2026

ORDER BY customer_id;
```

Don't normally put separate `ORDER BY` clauses on each component query unless your database specifically supports a more complex construction using subqueries/parentheses.

---

# Set Operations with WHERE

Each query can have its own filtering.

```sql
SELECT
    customer_id,
    name
FROM customers
WHERE region = 'South'

UNION

SELECT
    customer_id,
    name
FROM customers
WHERE region = 'North';
```

---

# Set Operations with Different Tables

The source tables can be completely different as long as the selected result columns are compatible.

Example:

```sql
SELECT
    employee_id AS person_id,
    employee_name AS person_name
FROM employees

UNION

SELECT
    customer_id,
    customer_name
FROM customers;
```

Result:

```text
person_id
person_name
```

---

# Column Names in UNION

The output column names generally come from the **first SELECT**.

Example:

```sql
SELECT
    employee_id AS id,
    employee_name AS name
FROM employees

UNION

SELECT
    customer_id,
    customer_name
FROM customers;
```

Result column names:

```text
id
name
```

The aliases from the second query do not determine the final column names.

---

# Data Types in SET Operations

Corresponding columns should have compatible data types.

Good:

```text
INTEGER + INTEGER
VARCHAR + VARCHAR
DATE + DATE
```

Potentially problematic:

```text
INTEGER + unrelated text
DATE + incompatible data
```

Exact implicit conversion rules depend on the database.

---

# UNION with Aggregation

You can aggregate each query before combining.

```sql
SELECT
    region,
    SUM(amount) AS revenue
FROM orders_2025
GROUP BY region

UNION ALL

SELECT
    region,
    SUM(amount) AS revenue
FROM orders_2026
GROUP BY region;
```

This produces separate yearly regional summaries.

---

# Combining Yearly Data

A common analytics scenario:

```text
sales_2024
sales_2025
sales_2026
```

You can combine them:

```sql
SELECT *
FROM sales_2024

UNION ALL

SELECT *
FROM sales_2025

UNION ALL

SELECT *
FROM sales_2026;
```

This is useful when tables have the same structure.

---

# UNION ALL for Data Warehousing

A common warehouse pattern:

```text
January data
     ↓
February data
     ↓
March data
     ↓
UNION ALL
     ↓
Combined dataset
```

If duplicate rows are legitimate, `UNION ALL` is usually the appropriate choice.

---

# UNION vs JOIN Example

Suppose:

### Customers 2025

```text
1 Rahul
2 Priya
```

### Customers 2026

```text
2 Priya
3 Amit
```

If you want:

> All customers appearing in either year

Use:

```sql
SELECT customer_id, name
FROM customers_2025

UNION

SELECT customer_id, name
FROM customers_2026;
```

If you want:

> Customer details from 2025 matched to 2026

you would use a JOIN:

```sql
SELECT
    a.customer_id,
    a.name AS name_2025,
    b.name AS name_2026
FROM customers_2025 a
JOIN customers_2026 b
    ON a.customer_id = b.customer_id;
```

---

# JOIN vs UNION

| JOIN                         | UNION                               |
| ---------------------------- | ----------------------------------- |
| Combines columns             | Combines rows                       |
| Usually needs a relationship | Does not require a key relationship |
| Uses `ON`                    | Uses compatible SELECT lists        |
| Horizontal combination       | Vertical combination                |
| Can multiply rows            | Usually appends result rows         |
| Used for related tables      | Used for similar result structures  |

---

# JOIN vs INTERSECT

Both can find common records, but they operate differently.

JOIN:

```sql
SELECT
    a.id,
    b.id
FROM A a
JOIN B b
    ON a.id = b.id;
```

INTERSECT:

```sql
SELECT id
FROM A

INTERSECT

SELECT id
FROM B;
```

JOIN can return columns from both tables.

INTERSECT returns the common result rows of the two SELECT statements.

---

# JOIN vs EXCEPT

To find records in A but not B:

Using LEFT JOIN:

```sql
SELECT
    a.*
FROM A a
LEFT JOIN B b
    ON a.id = b.id
WHERE b.id IS NULL;
```

Using EXCEPT:

```sql
SELECT id
FROM A

EXCEPT

SELECT id
FROM B;
```

Both can express an anti-matching requirement, but they differ in output shape and semantics.

---

# Subquery vs JOIN

Example using subquery:

```sql
SELECT
    customer_id,
    customer_name
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

Equivalent style using JOIN:

```sql
SELECT DISTINCT
    c.customer_id,
    c.customer_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

But the two approaches are not always interchangeable in terms of duplicates, NULL behavior, readability, or performance.

---

# Subquery vs CTE

Subquery:

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

CTE:

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

CTEs are often easier to read when the logic becomes complex or when the intermediate result is referenced multiple times.

---

# Subquery vs Window Function

Problem:

> Find employees earning above their department average.

Correlated subquery:

```sql
SELECT
    e.employee_name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

Window function alternative:

```sql
SELECT
    employee_name,
    salary,
    department_id
FROM (
    SELECT
        employee_name,
        salary,
        department_id,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees
) x
WHERE salary > department_avg;
```

For analytics, window functions are often extremely useful for these types of comparisons.

---

# Practical Analytics Examples

# Example 1 — Customers Above Average Spending

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > (
    SELECT AVG(total_spending)
    FROM (
        SELECT
            customer_id,
            SUM(amount) AS total_spending
        FROM orders
        GROUP BY customer_id
    ) x
);
```

This demonstrates nested aggregation.

---

# Example 2 — Highest Paid Employee

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

# Example 3 — Employees Above Company Average

```sql
SELECT
    employee_name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Example 4 — Employees Above Department Average

```sql
SELECT
    e.employee_name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# Example 5 — Customers With Orders

Using `EXISTS`:

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Example 6 — Customers Without Orders

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Example 7 — Customers in Multiple Years

```sql
SELECT customer_id
FROM customers_2025

INTERSECT

SELECT customer_id
FROM customers_2026;
```

This finds customers present in both years.

---

# Example 8 — Customers Lost in 2026

```sql
SELECT customer_id
FROM customers_2025

EXCEPT

SELECT customer_id
FROM customers_2026;
```

Meaning:

```text
Customers in 2025
but not in 2026
```

This can be useful for customer-retention/churn analysis.

---

# Example 9 — Customers Added in 2026

```sql
SELECT customer_id
FROM customers_2026

EXCEPT

SELECT customer_id
FROM customers_2025;
```

Meaning:

```text
Customers in 2026
but not in 2025
```

---

# Example 10 — Combine Monthly Data

```sql
SELECT *
FROM sales_january

UNION ALL

SELECT *
FROM sales_february

UNION ALL

SELECT *
FROM sales_march;
```

---

# Example 11 — Products Never Ordered

Using `NOT EXISTS`:

```sql
SELECT
    p.product_id,
    p.product_name
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.product_id
);
```

---

# Example 12 — Products Ordered at Least Once

```sql
SELECT
    p.product_id,
    p.product_name
FROM products p
WHERE EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.product_id
);
```

---

# Example 13 — Department with Highest Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) = (
    SELECT MAX(avg_salary)
    FROM (
        SELECT
            department_id,
            AVG(salary) AS avg_salary
        FROM employees
        GROUP BY department_id
    ) x
);
```

---

# Common Mistakes

## Mistake 1 — Using `=` with Multiple Rows

Wrong:

```sql
SELECT *
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
);
```

If the subquery returns multiple rows, this can fail.

Use:

```sql
WHERE department_id IN (
    SELECT department_id
    FROM departments
);
```

when multiple values are expected.

---

# Mistake 2 — Ignoring NULL with NOT IN

Potentially dangerous:

```sql
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
);
```

If the subquery contains `NULL`, results can be surprising.

Often safer:

```sql
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Mistake 3 — Double Counting After JOIN

Bad analytical pattern:

```sql
SELECT
    SUM(o.amount)
FROM orders o
JOIN payments p
    ON o.order_id = p.order_id;
```

if one order can have multiple payments.

Always understand the grain before aggregating.

---

# Mistake 4 — Using DISTINCT to Hide JOIN Problems

Instead of immediately doing:

```sql
SELECT DISTINCT ...
```

ask:

```text
Why are multiple rows being generated?
```

The answer is often:

```text
1-to-many
Many-to-many
Incorrect JOIN condition
Missing JOIN condition
```

---

# Mistake 5 — Incorrect JOIN Key

Bad:

```sql
ON c.name = o.customer_name
```

when a stable ID exists.

Prefer:

```sql
ON c.customer_id = o.customer_id
```

Keys are generally more reliable than names.

---

# Mistake 6 — Unnecessary Nested Subqueries

Very complex:

```text
Query
 ↓
Subquery
 ↓
Subquery
 ↓
Subquery
 ↓
Subquery
```

Consider whether a:

```text
JOIN
CTE
Window Function
```

would make the query easier to understand.

---

# Mistake 7 — Confusing UNION and UNION ALL

Remember:

```text
UNION
→ removes duplicates

UNION ALL
→ keeps duplicates
```

---

# Mistake 8 — Incorrect Column Count in UNION

Wrong:

```sql
SELECT
    id,
    name
FROM A

UNION

SELECT
    id
FROM B;
```

The queries don't return the same number of columns.

Correct:

```sql
SELECT
    id,
    name
FROM A

UNION

SELECT
    id,
    name
FROM B;
```

---

# Mistake 9 — Incompatible Data Types

For example:

```sql
SELECT
    employee_id
FROM employees

UNION

SELECT
    order_date
FROM orders;
```

The corresponding columns have incompatible meanings/types.

---

# Mistake 10 — Forgetting the Direction of EXCEPT

These are different:

```sql
A EXCEPT B
```

and:

```sql
B EXCEPT A
```

Remember:

```text
A EXCEPT B
→ Rows in A that aren't in B
```

---

# Performance Considerations

For complex queries, performance can depend on:

* Indexes
* Table size
* Join keys
* Data distribution
* Query optimizer
* Statistics
* Correlated subqueries
* Duplicate elimination
* `UNION` vs `UNION ALL`
* Filtering
* Aggregation

---

# Correlated Subquery Performance

Example:

```sql
SELECT
    e.employee_name
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

Conceptually, the inner query is associated with each outer row.

For very large datasets, an equivalent JOIN/CTE/window-function approach may be easier for the optimizer or easier to maintain.

Always check the execution plan for performance-sensitive queries.

---

# UNION vs UNION ALL Performance

When duplicate removal is unnecessary:

Prefer:

```sql
UNION ALL
```

instead of:

```sql
UNION
```

because `UNION` has to perform duplicate elimination.

---

# EXISTS Performance Concept

`EXISTS` is useful when you only need to answer:

```text
Does a related row exist?
```

You don't need to retrieve all matching rows.

Example:

```sql
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
)
```

This expresses the intent clearly.

---

# Interview Questions

## 1. What is a subquery?

A query inside another SQL query.

---

## 2. What is a correlated subquery?

A subquery that references columns from the outer query.

---

## 3. Difference between IN and EXISTS?

```text
IN
→ compares a value against values returned by a subquery.

EXISTS
→ checks whether at least one matching row exists.
```

---

## 4. Difference between IN and NOT IN?

```text
IN
→ value exists in result

NOT IN
→ value does not exist in result
```

But remember NULL complications with `NOT IN`.

---

## 5. Difference between EXISTS and NOT EXISTS?

```text
EXISTS
→ at least one match

NOT EXISTS
→ no match
```

---

## 6. What is ANY?

Comparison must be true for at least one value returned by the subquery.

---

## 7. What is ALL?

Comparison must be true for every value returned by the subquery.

---

## 8. What is UNION?

Combines two compatible query results and removes duplicates.

---

## 9. What is UNION ALL?

Combines query results without removing duplicates.

---

## 10. What is INTERSECT?

Returns rows common to both query results.

---

## 11. What is EXCEPT?

Returns rows from the first query that aren't present in the second.

---

## 12. What is MINUS?

In databases that support it, it performs the same general set-difference operation as `EXCEPT`.

---

## 13. JOIN vs UNION?

```text
JOIN
→ combines columns based on a relationship.

UNION
→ combines rows from compatible query results.
```

---

## 14. Why can JOIN cause duplicate rows?

Because of one-to-many or many-to-many relationships, or because the JOIN condition is not sufficiently specific.

---

## 15. What is grain?

The meaning represented by one row of a dataset.

---

## 16. How do you find records in A but not B?

Using LEFT JOIN:

```sql
SELECT a.*
FROM A a
LEFT JOIN B b
    ON a.id = b.id
WHERE b.id IS NULL;
```

Or set difference:

```sql
SELECT id
FROM A

EXCEPT

SELECT id
FROM B;
```

---

# Advanced Concept — Semi Join

A **semi join** means:

> Return rows from one table when a matching row exists in another table, without returning columns from the second table.

SQL commonly expresses this with:

```sql
EXISTS
```

Example:

```sql
SELECT
    c.*
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Advanced Concept — Anti Join

An **anti join** means:

> Return rows from one table that have no matching row in another table.

Common implementations:

```sql
LEFT JOIN ... IS NULL
```

or:

```sql
NOT EXISTS
```

Example:

```sql
SELECT
    c.*
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# Semi Join vs Anti Join

```text
SEMI JOIN
    ↓
Matching records

ANTI JOIN
    ↓
Non-matching records
```

Typical SQL:

```text
Semi Join → EXISTS
Anti Join → NOT EXISTS
```

---

# Complete Conceptual Relationship

These topics are connected:

```text
                    SQL DATA ANALYSIS
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
        JOIN           SUBQUERY         SET OPERATIONS
          │                │                │
          ↓                ↓                ↓
    Combine Tables    Nested Query     Combine Results
          │                │                │
    ┌─────┼─────┐     ┌────┼────┐     ┌────┼────────┐
    ↓     ↓     ↓     ↓    ↓    ↓     ↓    ↓        ↓
 INNER  LEFT  FULL   IN EXISTS ANY    UNION INTERSECT EXCEPT
```

---

# Practical Decision Guide

## Need columns from another table?

Use:

```text
JOIN
```

---

## Need to filter based on another query?

Use:

```text
SUBQUERY
```

---

## Need to know if a related record exists?

Use:

```text
EXISTS
```

---

## Need to know if a related record does NOT exist?

Use:

```text
NOT EXISTS
```

---

## Need to combine similar result sets?

Use:

```text
UNION / UNION ALL
```

---

## Need common records?

Use:

```text
INTERSECT
```

---

## Need records in A but not B?

Use:

```text
EXCEPT / MINUS
```

---

# ⭐ Quick Revision Cheat Sheet

## JOIN

```text
INNER JOIN
→ Matching rows

LEFT JOIN
→ All left + matching right

RIGHT JOIN
→ All right + matching left

FULL OUTER JOIN
→ Everything from both

CROSS JOIN
→ Every combination

SELF JOIN
→ Table joined with itself
```

---

## JOIN Analysis

```text
Cardinality
→ 1:1
→ 1:Many
→ Many:1
→ Many:Many

Grain
→ What does one row represent?

Always check:
→ Row multiplication
→ Duplicates
→ NULLs
→ Double counting
→ Aggregation level
```

---

## Subqueries

```text
Scalar
→ One value

Single-row
→ One row

Multi-row
→ Multiple rows

Multi-column
→ Multiple columns

Correlated
→ Depends on outer query

Non-correlated
→ Independent of outer query
```

---

## Subquery Operators

```text
=
→ Exactly one value

IN
→ Value exists in result

NOT IN
→ Value doesn't exist in result

EXISTS
→ At least one row exists

NOT EXISTS
→ No matching row

ANY
→ Condition true for at least one value

SOME
→ Same general meaning as ANY

ALL
→ Condition true for every value
```

---

## Set Operations

```text
UNION
→ Combine + remove duplicates

UNION ALL
→ Combine + keep duplicates

INTERSECT
→ Common rows

EXCEPT
→ First query minus second

MINUS
→ EXCEPT-style operation in supported databases
```

---

# ⭐ Most Important SQL Patterns to Memorize

## 1. Find matching records

```sql
SELECT *
FROM A
JOIN B
    ON A.id = B.id;
```

---

## 2. Find unmatched records

```sql
SELECT A.*
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

---

## 3. Find records using IN

```sql
SELECT *
FROM A
WHERE id IN (
    SELECT id
    FROM B
);
```

---

## 4. Find records using EXISTS

```sql
SELECT *
FROM A
WHERE EXISTS (
    SELECT 1
    FROM B
    WHERE B.id = A.id
);
```

---

## 5. Find records using NOT EXISTS

```sql
SELECT *
FROM A
WHERE NOT EXISTS (
    SELECT 1
    FROM B
    WHERE B.id = A.id
);
```

---

## 6. Compare against average

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

## 7. Combine datasets

```sql
SELECT *
FROM A

UNION ALL

SELECT *
FROM B;
```

---

## 8. Find common records

```sql
SELECT id
FROM A

INTERSECT

SELECT id
FROM B;
```

---

## 9. Find A-only records

```sql
SELECT id
FROM A

EXCEPT

SELECT id
FROM B;
```

---

# Final Mental Model

```text
                         SQL
                          │
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
      JOIN            SUBQUERY         SET OPERATIONS
        │                 │                 │
        ↓                 ↓                 ↓
 Combine tables      Query inside      Combine results
                     another query
        │                 │                 │
        ↓                 ↓                 ↓
 INNER / LEFT       IN / EXISTS       UNION
 RIGHT / FULL       ANY / ALL         UNION ALL
 CROSS / SELF       NOT EXISTS        INTERSECT
                                      EXCEPT
                                      MINUS
```

For **data analytics**, the most important concepts to master are:

```text
1. JOIN cardinality
2. Data grain
3. JOIN multiplication
4. Double-counting prevention
5. INNER vs LEFT JOIN
6. EXISTS / NOT EXISTS
7. IN / NOT IN and NULL behavior
8. Correlated subqueries
9. UNION vs UNION ALL
10. INTERSECT
11. EXCEPT / MINUS
12. JOIN + GROUP BY
13. JOIN + CASE
14. JOIN + aggregation
15. Subquery vs CTE vs JOIN vs window function
```

The biggest practical lesson is:

> **Don't just ask whether a SQL query runs. Ask what each row represents after every JOIN, what rows are being removed or preserved, and whether your aggregation is counting each business entity exactly once.**
