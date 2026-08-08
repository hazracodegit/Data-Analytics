# SQL JOINs — Complete Detailed Guide

SQL `JOIN` is used to **combine rows from two or more tables** based on a related column or condition.

JOINs are one of the most important SQL concepts for:

* SQL programming
* Database querying
* Data analytics
* Reporting
* Business intelligence
* Data engineering
* Data cleaning
* Data exploration
* Interview preparation

---

# 1. What is a JOIN?

Suppose we have two tables:

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

The relationship is:

```text
customers.customer_id
        ↓
orders.customer_id
```

We can combine the tables:

```sql
SELECT
    customers.customer_name,
    orders.order_id,
    orders.amount
FROM customers
JOIN orders
    ON customers.customer_id = orders.customer_id;
```

Result:

| customer_name | order_id | amount |
| ------------- | -------: | -----: |
| Rahul         |      101 |    500 |
| Rahul         |      102 |    800 |
| Priya         |      103 |    300 |

Customer `3` has no order, so it doesn't appear in an `INNER JOIN`.

Order `104` has `customer_id = 5`, which doesn't exist in `customers`, so it doesn't appear either.

---

# 2. Why Do We Need JOINs?

Real databases usually don't store everything in one table.

Instead, data is divided into related tables.

For example:

```text
customers
    |
    ├── orders
    |
    ├── payments
    |
    └── addresses
```

An e-commerce database might contain:

```text
customers
products
orders
order_items
payments
categories
employees
```

JOINs allow us to combine these tables when we need information from multiple tables.

---

# 3. Basic JOIN Syntax

```sql
SELECT columns
FROM table1
JOIN table2
    ON table1.column = table2.column;
```

Example:

```sql
SELECT
    customers.customer_name,
    orders.order_id
FROM customers
JOIN orders
    ON customers.customer_id = orders.customer_id;
```

---

# 4. Types of SQL JOINs

The major JOIN types are:

```text
1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL OUTER JOIN
5. CROSS JOIN
6. SELF JOIN
```

You may also encounter:

```text
7. NATURAL JOIN
8. Non-Equi JOIN
9. Equi JOIN
```

The most important ones for analytics are:

```text
INNER JOIN
LEFT JOIN
FULL OUTER JOIN
SELF JOIN
CROSS JOIN
```

---

# 5. JOIN Diagram

Conceptually:

```text
INNER JOIN

     A       B
   ┌─────┐ ┌─────┐
   │     │███████│
   │     │███████│
   └─────┘ └─────┘
       Matching rows
```

```text
LEFT JOIN

     A       B
   ┌─────┐ ┌─────┐
   │█████│███████│
   │█████│███████│
   └─────┘ └─────┘
   All A + matching B
```

```text
FULL OUTER JOIN

     A       B
   ┌─────┐ ┌─────┐
   │█████│███████│
   │█████│███████│
   └─────┘ └─────┘
   Everything from both
```

---

# 6. INNER JOIN

`INNER JOIN` returns only rows where a match exists in both tables.

Syntax:

```sql
SELECT columns
FROM table1
INNER JOIN table2
    ON table1.key = table2.key;
```

`JOIN` without specifying a type generally means `INNER JOIN`.

Therefore:

```sql
SELECT *
FROM customers
JOIN orders
    ON customers.customer_id = orders.customer_id;
```

is equivalent to:

```sql
SELECT *
FROM customers
INNER JOIN orders
    ON customers.customer_id = orders.customer_id;
```

---

# 7. INNER JOIN Example

### Customers

| customer_id | name  |
| ----------: | ----- |
|           1 | Rahul |
|           2 | Priya |
|           3 | Amit  |

### Orders

| order_id | customer_id |
| -------: | ----------: |
|      101 |           1 |
|      102 |           1 |
|      103 |           2 |
|      104 |           5 |

Query:

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result:

| customer_id | name  | order_id |
| ----------: | ----- | -------: |
|           1 | Rahul |      101 |
|           1 | Rahul |      102 |
|           2 | Priya |      103 |

---

# 8. What Does INNER JOIN Remove?

It removes:

```text
Customers without orders
+
Orders without valid customers
```

Only matching records remain.

```text
Customer IDs: 1 2 3
Order IDs:    1 1 2 5

Common IDs:
1, 2
```

Therefore:

```text
1 → included
2 → included
3 → excluded
5 → excluded
```

---

# 9. LEFT JOIN

`LEFT JOIN` returns:

> All rows from the left table + matching rows from the right table.

Syntax:

```sql
SELECT columns
FROM table1
LEFT JOIN table2
    ON table1.key = table2.key;
```

---

# 10. LEFT JOIN Example

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result:

| customer_id | name  | order_id |
| ----------: | ----- | -------: |
|           1 | Rahul |      101 |
|           1 | Rahul |      102 |
|           2 | Priya |      103 |
|           3 | Amit  |     NULL |

Customer `3` doesn't have an order.

Because the customer table is the left table, the customer still appears.

The order columns become:

```text
NULL
```

---

# 11. LEFT JOIN Mental Model

```text
LEFT TABLE
     ↓
EVERY ROW IS PRESERVED

RIGHT TABLE
     ↓
ONLY MATCHING ROWS
```

Remember:

> **LEFT JOIN = Keep everything from the left table.**

---

# 12. Finding Customers Without Orders

This is one of the most important JOIN patterns.

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

This finds customers who have **no matching order**.

Result:

| customer_id | name |
| ----------: | ---- |
|           3 | Amit |

---

# 13. LEFT JOIN for Data Analytics

Suppose you want:

> Every customer and their total spending.

A `LEFT JOIN` is usually appropriate because customers with no orders should still appear.

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

Result conceptually:

| customer_id | name  | total_spending |
| ----------: | ----- | -------------: |
|           1 | Rahul |           1300 |
|           2 | Priya |            300 |
|           3 | Amit  |              0 |

---

# 14. RIGHT JOIN

`RIGHT JOIN` returns:

> All rows from the right table + matching rows from the left table.

Syntax:

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
    ON table1.key = table2.key;
```

Example:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
RIGHT JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 15. RIGHT JOIN Example

Suppose:

### Customers

| customer_id | name  |
| ----------: | ----- |
|           1 | Rahul |
|           2 | Priya |
|           3 | Amit  |

### Orders

| order_id | customer_id |
| -------: | ----------: |
|      101 |           1 |
|      102 |           1 |
|      103 |           2 |
|      104 |           5 |

Query:

```sql
SELECT
    c.name,
    o.order_id,
    o.customer_id
FROM customers c
RIGHT JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result:

| name  | order_id | customer_id |
| ----- | -------: | ----------: |
| Rahul |      101 |           1 |
| Rahul |      102 |           1 |
| Priya |      103 |           2 |
| NULL  |      104 |           5 |

Order `104` is preserved because `orders` is the right table.

---

# 16. RIGHT JOIN vs LEFT JOIN

These are logically reversible.

This:

```sql
SELECT *
FROM customers c
RIGHT JOIN orders o
    ON c.customer_id = o.customer_id;
```

can be rewritten as:

```sql
SELECT *
FROM orders o
LEFT JOIN customers c
    ON c.customer_id = o.customer_id;
```

Many SQL developers prefer `LEFT JOIN` because it is easier to read consistently.

---

# 17. FULL OUTER JOIN

`FULL OUTER JOIN` returns:

> All rows from both tables, matching where possible.

It preserves:

```text
Matching rows
+
Unmatched left rows
+
Unmatched right rows
```

Syntax:

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
    ON table1.key = table2.key;
```

---

# 18. FULL OUTER JOIN Example

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id,
    o.customer_id AS order_customer_id
FROM customers c
FULL OUTER JOIN orders o
    ON c.customer_id = o.customer_id;
```

Result conceptually:

| customer_id | name  | order_id | order_customer_id |
| ----------: | ----- | -------: | ----------------: |
|           1 | Rahul |      101 |                 1 |
|           1 | Rahul |      102 |                 1 |
|           2 | Priya |      103 |                 2 |
|           3 | Amit  |     NULL |              NULL |
|        NULL | NULL  |      104 |                 5 |

It preserves:

```text
Customer 3
Order 104
```

even though they don't have matches.

---

# 19. FULL OUTER JOIN Use Cases

Useful for:

* Comparing datasets
* Data reconciliation
* Finding missing records
* Data migration validation
* Comparing old vs new data
* Auditing
* Data quality analysis

Example:

```text
System A
   ↓
FULL OUTER JOIN
   ↑
System B
```

Then identify:

```text
Only in A
Only in B
In both
```

---

# 20. CROSS JOIN

`CROSS JOIN` returns every possible combination of rows.

It produces a **Cartesian product**.

Syntax:

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

---

# 21. CROSS JOIN Example

Table A:

| color |
| ----- |
| Red   |
| Blue  |

Table B:

| size |
| ---- |
| S    |
| M    |
| L    |

Query:

```sql
SELECT
    color,
    size
FROM colors
CROSS JOIN sizes;
```

Result:

| color | size |
| ----- | ---- |
| Red   | S    |
| Red   | M    |
| Red   | L    |
| Blue  | S    |
| Blue  | M    |
| Blue  | L    |

Total:

```text
2 × 3 = 6 rows
```

---

# 22. CROSS JOIN Row Count

If:

```text
Table A = 10 rows
Table B = 20 rows
```

Then:

```text
CROSS JOIN = 10 × 20 = 200 rows
```

Be careful with large tables.

---

# 23. CROSS JOIN Applications

Useful for:

* Product combinations
* Date/calendar generation
* Scenario analysis
* Creating test combinations
* All product-region combinations
* All customer-month combinations

Example:

```sql
SELECT
    p.product_id,
    r.region
FROM products p
CROSS JOIN regions r;
```

This creates every possible product-region combination.

---

# 24. SELF JOIN

A `SELF JOIN` joins a table to itself.

This is useful when rows in the same table are related to other rows in that table.

Example:

```text
employees
```

contains:

| employee_id | employee_name | manager_id |
| ----------: | ------------- | ---------: |
|           1 | CEO           |       NULL |
|           2 | Rahul         |          1 |
|           3 | Priya         |          1 |
|           4 | Amit          |          2 |

We want:

```text
Employee → Manager
```

---

# 25. SELF JOIN Example

```sql
SELECT
    e.employee_name AS employee,
    m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Result:

| employee | manager |
| -------- | ------- |
| CEO      | NULL    |
| Rahul    | CEO     |
| Priya    | CEO     |
| Amit     | Rahul   |

The table appears twice with different aliases:

```text
employees e
employees m
```

---

# 26. Why Do We Need Aliases in SELF JOIN?

Without aliases, SQL cannot clearly distinguish the two instances of the same table.

We use:

```sql
employees e
```

for employees.

And:

```sql
employees m
```

for managers.

Then:

```sql
e.employee_id
m.employee_id
```

refer to different logical instances.

---

# 27. EQUI JOIN

An equi join uses equality:

```sql
=
```

Example:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

The join condition uses:

```sql
=
```

This is an equi join.

Most common relational JOINs are equi joins.

---

# 28. NON-EQUI JOIN

A non-equi join uses operators other than equality.

For example:

```text
>
<
>=
<=
BETWEEN
```

Example:

### Employees

| employee_id | salary |
| ----------: | -----: |
|           1 |  40000 |
|           2 |  70000 |
|           3 | 120000 |

### Salary Grades

| grade | min_salary | max_salary |
| ----- | ---------: | ---------: |
| C     |          0 |      50000 |
| B     |      50001 |     100000 |
| A     |     100001 |     200000 |

Query:

```sql
SELECT
    e.employee_id,
    e.salary,
    g.grade
FROM employees e
JOIN salary_grades g
    ON e.salary BETWEEN g.min_salary AND g.max_salary;
```

This is a non-equi/range join.

---

# 29. NATURAL JOIN

`NATURAL JOIN` automatically joins columns having the same names.

Example:

```sql
SELECT *
FROM customers
NATURAL JOIN orders;
```

If both tables have:

```text
customer_id
```

the database may automatically use it.

However, `NATURAL JOIN` is generally avoided in production SQL because changes to table schemas can unexpectedly change the join behavior.

Prefer explicit joins:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 30. JOIN Using Primary Key and Foreign Key

A very common relationship:

```text
customers
----------------
customer_id PK
name

orders
----------------
order_id PK
customer_id FK
amount
```

Relationship:

```text
customers.customer_id
          ↑
          │
orders.customer_id
```

Then:

```sql
SELECT
    c.name,
    o.order_id,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 31. Primary Key vs Foreign Key in JOIN

### Primary Key

Uniquely identifies a row.

```text
customers.customer_id
```

### Foreign Key

References a key in another table.

```text
orders.customer_id
```

Therefore:

```text
customers.customer_id = orders.customer_id
```

is commonly used as the JOIN condition.

---

# 32. One-to-One Relationship

Example:

```text
users
user_id
name

user_profiles
user_id
address
```

Query:

```sql
SELECT
    u.name,
    p.address
FROM users u
JOIN user_profiles p
    ON u.user_id = p.user_id;
```

One user corresponds to one profile.

---

# 33. One-to-Many Relationship

This is extremely common.

Example:

```text
One customer
      ↓
Many orders
```

Tables:

```text
customers
orders
```

Query:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

A customer can appear multiple times.

Example:

```text
Rahul → Order 101
Rahul → Order 102
Rahul → Order 103
```

---

# 34. Many-to-Many Relationship

Example:

```text
Students
Courses
```

A student can take multiple courses.

A course can have multiple students.

Usually, a bridge/junction table is used:

```text
students
    ↓
student_courses
    ↓
courses
```

---

# 35. Many-to-Many JOIN

Tables:

```text
students
student_id
student_name
```

```text
student_courses
student_id
course_id
```

```text
courses
course_id
course_name
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

This requires two JOINs.

---

# 36. Joining Three Tables

You can join more than two tables.

Example:

```text
customers
orders
payments
```

Query:

```sql
SELECT
    c.name,
    o.order_id,
    p.payment_id,
    p.amount
FROM customers c

JOIN orders o
    ON c.customer_id = o.customer_id

JOIN payments p
    ON o.order_id = p.order_id;
```

---

# 37. Joining Four Tables

Example:

```text
customers
orders
order_items
products
```

Query:

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name,
    oi.quantity
FROM customers c

JOIN orders o
    ON c.customer_id = o.customer_id

JOIN order_items oi
    ON o.order_id = oi.order_id

JOIN products p
    ON oi.product_id = p.product_id;
```

---

# 38. Multi-Table JOIN Mental Model

Think:

```text
customers
    │
    │ customer_id
    ↓
orders
    │
    │ order_id
    ↓
order_items
    │
    │ product_id
    ↓
products
```

Each JOIN follows a relationship.

---

# 39. JOIN with WHERE

You can filter after joining.

```sql
SELECT
    c.name,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.amount > 1000;
```

Meaning:

```text
1. Join customers and orders
2. Keep orders > 1000
```

---

# 40. JOIN with GROUP BY

Example:

> Find total sales for each customer.

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name;
```

---

# 41. JOIN with ORDER BY

```sql
SELECT
    c.name,
    SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name
ORDER BY total_sales DESC;
```

This finds the highest-spending customers first.

---

# 42. JOIN with HAVING

Example:

> Find customers whose total spending exceeds 100,000.

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
    c.name
HAVING SUM(o.amount) > 100000;
```

---

# 43. JOIN + CASE

You can combine JOIN and CASE.

```sql
SELECT
    c.name,
    SUM(o.amount) AS total_spending,

    CASE
        WHEN SUM(o.amount) >= 100000 THEN 'VIP'
        WHEN SUM(o.amount) >= 50000 THEN 'Gold'
        WHEN SUM(o.amount) >= 10000 THEN 'Silver'
        ELSE 'Bronze'
    END AS customer_segment

FROM customers c

JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.customer_id,
    c.name;
```

This is a very common data analytics pattern.

---

# 44. LEFT JOIN + CASE

Example:

```sql
SELECT
    c.customer_id,
    c.name,

    CASE
        WHEN o.order_id IS NULL
            THEN 'No Orders'
        ELSE 'Has Orders'
    END AS order_status

FROM customers c

LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

This identifies customers with and without orders.

---

# 45. JOIN + COUNT

```sql
SELECT
    c.customer_id,
    c.name,
    COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name;
```

Why `COUNT(o.order_id)` instead of `COUNT(*)`?

Because for a customer with no order:

```text
o.order_id = NULL
```

and `COUNT(column)` doesn't count NULL values.

---

# 46. COUNT(*) vs COUNT(column) with LEFT JOIN

This is very important.

Consider:

```sql
SELECT
    c.name,
    COUNT(*) AS count1,
    COUNT(o.order_id) AS count2
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.name;
```

For a customer with no orders:

```text
COUNT(*)          → 1
COUNT(o.order_id) → 0
```

Therefore:

> When counting matching child records after a LEFT JOIN, `COUNT(child_table.id)` is often what you want.

---

# 47. LEFT JOIN and WHERE — Important Difference

Consider:

```sql
SELECT
    c.name,
    o.amount
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.amount > 1000;
```

The `WHERE` condition removes rows where:

```text
o.amount IS NULL
```

So the query can behave like an INNER JOIN for that condition.

---

# 48. LEFT JOIN Condition in ON vs WHERE

Compare:

### Query 1

```sql
SELECT
    c.name,
    o.amount
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
   AND o.amount > 1000;
```

This preserves all customers.

Only orders above 1000 are matched.

### Query 2

```sql
SELECT
    c.name,
    o.amount
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.amount > 1000;
```

This filters after the JOIN and removes customers without matching orders.

This distinction is extremely important.

---

# 49. JOIN Condition vs Filter Condition

### `ON`

Defines how rows are matched.

```sql
ON c.customer_id = o.customer_id
```

### `WHERE`

Filters the resulting rows.

```sql
WHERE o.amount > 1000
```

Think:

```text
ON     → How should tables connect?
WHERE  → Which resulting rows do I want?
```

---

# 50. Multiple Conditions in JOIN

JOIN conditions can contain multiple conditions.

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
   AND c.region = o.region;
```

Both conditions must be true.

---

# 51. JOIN Using Multiple Columns

Sometimes a relationship requires more than one column.

Example:

```text
Table A
country
product_id

Table B
country
product_id
```

Query:

```sql
SELECT *
FROM table_a a
JOIN table_b b
    ON a.country = b.country
   AND a.product_id = b.product_id;
```

This is a **composite join condition**.

---

# 52. Joining on Non-Key Columns

A JOIN doesn't technically have to use primary/foreign keys.

Example:

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_name = d.department_name;
```

However, joining on non-unique or inconsistent columns can create incorrect or duplicate matches.

Prefer stable keys when possible.

---

# 53. Duplicate Rows After JOIN

This is one of the biggest JOIN problems.

Suppose:

```text
customers
1 Rahul

orders
101 1
102 1
103 1
```

After joining:

```text
Rahul 101
Rahul 102
Rahul 103
```

Rahul appears three times.

This is not necessarily an error.

It happens because one customer has many orders.

---

# 54. JOIN Multiplication

Suppose:

```text
Customer 1
    ↓
3 Orders
    ↓
4 Order Items each
```

Joining customers → orders → order_items can produce:

```text
3 × 4 = 12 rows
```

if each order has four items.

Always understand the **cardinality** of the relationships before aggregating.

---

# 55. Cardinality

Cardinality describes how rows relate.

Common types:

```text
1 : 1
1 : Many
Many : 1
Many : Many
```

Examples:

```text
Customer → Orders
1 : Many
```

```text
Order → Customer
Many : 1
```

Understanding cardinality helps predict JOIN results.

---

# 56. Accidental Cartesian Product

Bad:

```sql
SELECT *
FROM customers c, orders o;
```

If there is no relationship condition, this can create a Cartesian product.

Example:

```text
100 customers
1000 orders
```

Potential result:

```text
100 × 1000 = 100,000 rows
```

Prefer explicit JOIN syntax:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 57. Always Use Explicit JOIN Syntax

Old style:

```sql
SELECT *
FROM customers c, orders o
WHERE c.customer_id = o.customer_id;
```

Preferred:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Explicit JOIN syntax is easier to read and maintain.

---

# 58. Table Aliases

Aliases make JOIN queries shorter.

Without aliases:

```sql
SELECT
    customers.customer_name,
    orders.amount
FROM customers
JOIN orders
    ON customers.customer_id = orders.customer_id;
```

With aliases:

```sql
SELECT
    c.customer_name,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Aliases are strongly recommended for multi-table queries.

---

# 59. Always Qualify Ambiguous Columns

Suppose both tables have:

```text
customer_id
```

Avoid:

```sql
SELECT customer_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Better:

```sql
SELECT
    c.customer_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Use:

```text
c.column
o.column
```

to clearly identify the source.

---

# 60. JOIN with Same Column Name

Example:

```sql
SELECT
    c.customer_id,
    o.customer_id,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Both columns can be selected.

You can give them aliases:

```sql
SELECT
    c.customer_id AS customer_id,
    o.customer_id AS order_customer_id,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 61. Joining Tables with Different Column Names

The matching columns don't need to have the same name.

Example:

```text
customers:
customer_id

orders:
buyer_id
```

Query:

```sql
SELECT *
FROM customers c
JOIN orders o
    ON c.customer_id = o.buyer_id;
```

The important thing is the relationship, not the column names.

---

# 62. JOIN with Expressions

You can sometimes join using expressions.

```sql
SELECT *
FROM customers c
JOIN orders o
    ON LOWER(c.email) = LOWER(o.customer_email);
```

However, applying functions to join columns can affect performance and may prevent efficient index usage depending on the database.

---

# 63. INNER JOIN vs LEFT JOIN

| Feature              | INNER JOIN                             | LEFT JOIN                    |
| -------------------- | -------------------------------------- | ---------------------------- |
| Matching rows        | Yes                                    | Yes                          |
| Unmatched left rows  | No                                     | Yes                          |
| Unmatched right rows | No                                     | No                           |
| NULLs generated      | Possible from existing nullable values | Yes for unmatched right side |
| Common use           | Only related records                   | Preserve all left records    |

Example:

```sql
-- Only customers with orders
SELECT *
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

```sql
-- All customers
SELECT *
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 64. LEFT JOIN vs RIGHT JOIN

| LEFT JOIN            | RIGHT JOIN                            |
| -------------------- | ------------------------------------- |
| Preserves left table | Preserves right table                 |
| More commonly used   | Less commonly used                    |
| Easy to read         | Can usually be rewritten as LEFT JOIN |

Example:

```sql
A LEFT JOIN B
```

means:

```text
Keep A
```

Example:

```sql
A RIGHT JOIN B
```

means:

```text
Keep B
```

---

# 65. LEFT JOIN vs FULL OUTER JOIN

### LEFT JOIN

Keeps:

```text
All left
+
Matching right
```

### FULL OUTER JOIN

Keeps:

```text
All left
+
All right
```

Use FULL OUTER JOIN when unmatched rows on **both sides** matter.

---

# 66. INNER JOIN vs FULL OUTER JOIN

```text
INNER JOIN
→ only matches

FULL OUTER JOIN
→ matches + unmatched rows from both sides
```

---

# 67. JOIN Summary

```text
INNER JOIN
    → Matching rows only

LEFT JOIN
    → Everything from left + matches from right

RIGHT JOIN
    → Everything from right + matches from left

FULL OUTER JOIN
    → Everything from both tables

CROSS JOIN
    → Every possible combination

SELF JOIN
    → Table joined with itself
```

---

# 68. Finding Records Only in Left Table

A common analytics technique:

```sql
SELECT
    a.*
FROM table_a a
LEFT JOIN table_b b
    ON a.id = b.id
WHERE b.id IS NULL;
```

Meaning:

```text
Records in A
but not in B
```

---

# 69. Finding Records Only in Right Table

```sql
SELECT
    b.*
FROM table_a a
RIGHT JOIN table_b b
    ON a.id = b.id
WHERE a.id IS NULL;
```

Or more consistently:

```sql
SELECT
    b.*
FROM table_b b
LEFT JOIN table_a a
    ON b.id = a.id
WHERE a.id IS NULL;
```

---

# 70. Finding Records Existing in Both

Use:

```sql
SELECT *
FROM table_a a
INNER JOIN table_b b
    ON a.id = b.id;
```

This returns matching records.

---

# 71. Data Reconciliation with FULL OUTER JOIN

Suppose two systems should contain the same customers.

```sql
SELECT
    a.customer_id AS system_a_id,
    b.customer_id AS system_b_id
FROM system_a a
FULL OUTER JOIN system_b b
    ON a.customer_id = b.customer_id
WHERE a.customer_id IS NULL
   OR b.customer_id IS NULL;
```

This identifies records missing from one system.

---

# 72. JOIN for Data Quality

Example:

> Find orders whose customer does not exist.

```sql
SELECT
    o.order_id,
    o.customer_id
FROM orders o
LEFT JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

This can identify referential integrity/data quality issues.

---

# 73. JOIN for Orphan Records

An **orphan record** is a child record that has no corresponding parent.

Example:

```text
Order
  ↓
Customer missing
```

Query:

```sql
SELECT o.*
FROM orders o
LEFT JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

---

# 74. JOIN for Customer Analysis

### Total orders per customer

```sql
SELECT
    c.customer_id,
    c.name,
    COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name;
```

---

# 75. JOIN for Revenue Analysis

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS revenue
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name
ORDER BY revenue DESC;
```

---

# 76. JOIN for Product Analysis

Tables:

```text
orders
order_items
products
```

Query:

```sql
SELECT
    p.product_id,
    p.product_name,
    SUM(oi.quantity) AS units_sold
FROM products p
JOIN order_items oi
    ON p.product_id = oi.product_id
GROUP BY
    p.product_id,
    p.product_name
ORDER BY units_sold DESC;
```

---

# 77. JOIN for Category Analysis

Suppose:

```text
products
categories
order_items
```

Query:

```sql
SELECT
    c.category_name,
    SUM(oi.quantity * oi.price) AS revenue
FROM categories c

JOIN products p
    ON c.category_id = p.category_id

JOIN order_items oi
    ON p.product_id = oi.product_id

GROUP BY
    c.category_id,
    c.category_name

ORDER BY revenue DESC;
```

This is a typical analytics query.

---

# 78. JOIN for Regional Analysis

```sql
SELECT
    c.region,
    SUM(o.amount) AS total_revenue
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.region
ORDER BY total_revenue DESC;
```

---

# 79. JOIN + Date Filtering

```sql
SELECT
    c.name,
    SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_date >= '2026-01-01'
GROUP BY
    c.customer_id,
    c.name;
```

This can answer:

> How much did each customer spend during the period?

---

# 80. JOIN + CASE + GROUP BY

```sql
SELECT
    c.region,

    CASE
        WHEN o.amount >= 10000 THEN 'High Value'
        WHEN o.amount >= 5000 THEN 'Medium Value'
        ELSE 'Low Value'
    END AS order_category,

    COUNT(*) AS order_count

FROM customers c

JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.region,
    CASE
        WHEN o.amount >= 10000 THEN 'High Value'
        WHEN o.amount >= 5000 THEN 'Medium Value'
        ELSE 'Low Value'
    END;
```

This creates a category after joining.

---

# 81. JOIN with CTE

CTEs can make complex JOINs easier to understand.

```sql
WITH customer_orders AS (
    SELECT
        c.customer_id,
        c.name,
        o.amount
    FROM customers c
    JOIN orders o
        ON c.customer_id = o.customer_id
)

SELECT
    customer_id,
    name,
    SUM(amount) AS total_spending
FROM customer_orders
GROUP BY
    customer_id,
    name;
```

---

# 82. JOIN with Subquery

```sql
SELECT
    c.name,
    x.total_spending
FROM customers c
JOIN (
    SELECT
        customer_id,
        SUM(amount) AS total_spending
    FROM orders
    GROUP BY customer_id
) x
    ON c.customer_id = x.customer_id;
```

---

# 83. JOIN and DISTINCT

Sometimes JOINs produce duplicates.

You might see:

```sql
SELECT DISTINCT
    c.customer_id,
    c.name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

This returns each matching customer once.

But don't automatically use `DISTINCT` to hide duplicate rows.

First understand **why the duplicates exist**.

---

# 84. JOIN and Aggregation Order

Suppose:

```text
Customer
   ↓
Orders
   ↓
Order Items
```

If you directly join all three and then aggregate, you must ensure you are calculating at the correct grain.

For example:

```sql
SELECT
    c.customer_id,
    SUM(oi.quantity * oi.price) AS revenue
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN order_items oi
    ON o.order_id = oi.order_id
GROUP BY c.customer_id;
```

This is appropriate when each order item represents a sales line.

---

# 85. Grain of Data

**Grain** means:

> What does one row represent?

Examples:

```text
customers
→ one row = one customer

orders
→ one row = one order

order_items
→ one row = one order line

payments
→ one row = one payment
```

Before JOINing tables, always ask:

> What does one row represent in each table?

This prevents many analytical errors.

---

# 86. JOIN and Double Counting

Suppose:

```text
orders
1 order = $100

payments
2 payment records = $50 + $50
```

If you join orders to payments and then sum the order amount:

```sql
SELECT
    SUM(o.amount)
FROM orders o
JOIN payments p
    ON o.order_id = p.order_id;
```

The order could appear twice.

You might incorrectly calculate:

```text
$100 + $100 = $200
```

instead of:

```text
$100
```

This is called **double counting due to JOIN multiplication**.

---

# 87. Avoiding Double Counting

One approach is to aggregate before joining.

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

This reduces the payment table to one row per order before the JOIN.

---

# 88. JOIN Performance

JOIN performance depends on:

* Table size
* Join columns
* Indexes
* Data types
* Query structure
* Filtering
* Database engine
* Execution plan
* Cardinality
* Statistics

---

# 89. Indexes and JOINs

If a column is frequently used for JOINs, an appropriate index can improve performance.

Example:

```sql
CREATE INDEX idx_orders_customer_id
ON orders(customer_id);
```

The exact indexing strategy depends on the database and workload.

---

# 90. Filter Before Joining When Appropriate

Suppose you only need 2026 orders.

Instead of joining all historical orders, you may reduce the data first.

For example:

```sql
WITH recent_orders AS (
    SELECT *
    FROM orders
    WHERE order_date >= '2026-01-01'
)

SELECT
    c.name,
    r.order_id,
    r.amount
FROM customers c
JOIN recent_orders r
    ON c.customer_id = r.customer_id;
```

The optimizer may perform equivalent transformations automatically, but writing logically scoped queries can improve clarity.

---

# 91. JOIN Execution — Conceptual Order

SQL's logical processing order is important.

A simplified model:

```text
FROM
 ↓
JOIN
 ↓
ON
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
LIMIT
```

Remember that this is a **logical processing order**, not necessarily the physical order used by the database engine.

---

# 92. Why JOIN Comes Before WHERE Conceptually

Consider:

```sql
SELECT
    c.name,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.amount > 1000;
```

Conceptually:

```text
1. FROM customers
2. JOIN orders
3. Match using ON
4. Filter using WHERE
5. Return selected columns
```

---

# 93. ON vs WHERE — Interview Question

Question:

> What is the difference between `ON` and `WHERE` in a LEFT JOIN?

Answer:

```text
ON
→ Determines which rows from the right table match each left row.

WHERE
→ Filters the result after the JOIN.
```

Moving a condition from `ON` to `WHERE` can change a `LEFT JOIN` into behavior similar to an `INNER JOIN`.

---

# 94. JOIN Conditions with OR

You can use `OR`.

```sql
SELECT *
FROM customers c
JOIN contacts x
    ON c.email = x.email
    OR c.phone = x.phone;
```

However, OR-based JOINs can be difficult to reason about and may produce unexpected multiple matches.

Use carefully.

---

# 95. JOIN with BETWEEN

Range joins are useful for:

```text
Salary bands
Tax brackets
Date ranges
Price ranges
Commission rates
Age groups
```

Example:

```sql
SELECT
    e.employee_id,
    e.salary,
    g.grade
FROM employees e
JOIN salary_grades g
    ON e.salary BETWEEN g.min_salary AND g.max_salary;
```

---

# 96. JOIN with Date Ranges

Suppose:

```text
employee
employee_id
start_date
end_date
```

and:

```text
calendar
date
```

You might match dates falling within employment periods:

```sql
SELECT
    e.employee_id,
    c.date
FROM employees e
JOIN calendar c
    ON c.date BETWEEN e.start_date AND e.end_date;
```

This is a range/non-equi JOIN.

---

# 97. Self JOIN for Hierarchies

Self JOIN is useful for organizational structures.

```sql
SELECT
    e.employee_name AS employee,
    m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

It can also be used for:

* Employee-manager relationships
* Parent-child records
* Categories/subcategories
* Organizational hierarchies
* Referral relationships

---

# 98. Self JOIN for Comparing Employees

Suppose you want pairs of employees in the same department.

```sql
SELECT
    e1.employee_name AS employee1,
    e2.employee_name AS employee2,
    e1.department_id
FROM employees e1
JOIN employees e2
    ON e1.department_id = e2.department_id
   AND e1.employee_id < e2.employee_id;
```

The condition:

```sql
e1.employee_id < e2.employee_id
```

prevents:

```text
Rahul - Priya
Priya - Rahul
```

from both appearing.

---

# 99. Self JOIN for Duplicate Detection

Suppose duplicate emails should not exist.

```sql
SELECT
    a.customer_id AS customer1,
    b.customer_id AS customer2,
    a.email
FROM customers a
JOIN customers b
    ON a.email = b.email
   AND a.customer_id < b.customer_id;
```

This identifies pairs of records sharing the same email.

---

# 100. JOIN vs UNION

These are completely different.

### JOIN

Combines columns horizontally.

```text
Table A          Table B
   ↓                ↓
       JOIN
         ↓
More columns
```

### UNION

Combines rows vertically.

```text
Table A
 ↓
UNION
 ↓
Table B
 ↓
More rows
```

---

# 101. JOIN Example vs UNION Example

JOIN:

```sql
SELECT
    c.name,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

UNION:

```sql
SELECT name
FROM customers_2025

UNION

SELECT name
FROM customers_2026;
```

Remember:

```text
JOIN  → columns
UNION → rows
```

---

# 102. JOIN vs Subquery

A JOIN combines related datasets.

```sql
SELECT
    c.name,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

A subquery can calculate or filter something separately.

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

Both can sometimes solve similar problems, but they express different logic.

---

# 103. JOIN vs EXISTS

Instead of:

```sql
SELECT DISTINCT c.*
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

you can sometimes use:

```sql
SELECT c.*
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

`EXISTS` is useful when you only need to know whether a related row exists rather than retrieving columns from the related table.

---

# 104. Important JOIN Interview Questions

## Q1. What is a JOIN?

A JOIN combines rows from multiple tables based on a related condition.

---

## Q2. What is INNER JOIN?

Returns only matching rows from both tables.

---

## Q3. What is LEFT JOIN?

Returns all rows from the left table and matching rows from the right table.

---

## Q4. What is RIGHT JOIN?

Returns all rows from the right table and matching rows from the left table.

---

## Q5. What is FULL OUTER JOIN?

Returns all rows from both tables, matching where possible.

---

## Q6. What is CROSS JOIN?

Returns every possible combination of rows from both tables.

---

## Q7. What is SELF JOIN?

A table joined with itself.

---

## Q8. Why do JOINs create duplicates?

Usually because the relationship is one-to-many or many-to-many.

---

## Q9. How do you find unmatched records?

Use a `LEFT JOIN` and check for NULL on the right side.

```sql
SELECT a.*
FROM A a
LEFT JOIN B b
    ON a.id = b.id
WHERE b.id IS NULL;
```

---

## Q10. What is the difference between ON and WHERE?

`ON` controls matching; `WHERE` filters the resulting rows.

---

# 105. JOIN Cheat Sheet

```text
┌─────────────────────┬─────────────────────────────────┐
│ JOIN                │ Result                          │
├─────────────────────┼─────────────────────────────────┤
│ INNER JOIN          │ Matching rows only              │
│ LEFT JOIN           │ All left + matching right       │
│ RIGHT JOIN          │ All right + matching left       │
│ FULL OUTER JOIN     │ All rows from both              │
│ CROSS JOIN          │ Every possible combination      │
│ SELF JOIN           │ Table joined with itself        │
│ EQUI JOIN           │ Join using =                    │
│ NON-EQUI JOIN       │ Join using ranges/comparisons   │
│ NATURAL JOIN        │ Automatic same-name matching   │
└─────────────────────┴─────────────────────────────────┘
```

---

# 106. Most Important JOIN Patterns

## Pattern 1 — Matching Records

```sql
SELECT *
FROM A
INNER JOIN B
    ON A.id = B.id;
```

---

## Pattern 2 — Keep Everything from A

```sql
SELECT *
FROM A
LEFT JOIN B
    ON A.id = B.id;
```

---

## Pattern 3 — Find Missing Records

```sql
SELECT A.*
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

---

## Pattern 4 — Aggregate Related Data

```sql
SELECT
    A.id,
    SUM(B.amount)
FROM A
JOIN B
    ON A.id = B.a_id
GROUP BY A.id;
```

---

## Pattern 5 — Count Related Records

```sql
SELECT
    A.id,
    COUNT(B.id)
FROM A
LEFT JOIN B
    ON A.id = B.a_id
GROUP BY A.id;
```

---

## Pattern 6 — Conditional Analytics

```sql
SELECT
    A.category,

    SUM(
        CASE
            WHEN B.status = 'Completed'
                THEN B.amount
            ELSE 0
        END
    ) AS completed_sales

FROM A
JOIN B
    ON A.id = B.a_id

GROUP BY A.category;
```

---

# 107. JOIN Decision Guide

Ask yourself:

### Do I need only matching records?

```text
→ INNER JOIN
```

### Do I need every row from the first table?

```text
→ LEFT JOIN
```

### Do I need every row from the second table?

```text
→ RIGHT JOIN
```

### Do I need everything from both?

```text
→ FULL OUTER JOIN
```

### Do I need every possible combination?

```text
→ CROSS JOIN
```

### Does a table relate to itself?

```text
→ SELF JOIN
```

### Do I need a range match?

```text
→ NON-EQUI / RANGE JOIN
```

---

# 108. Complete Real-World Example

Suppose we have:

### customers

```text
customer_id
name
region
```

### orders

```text
order_id
customer_id
order_date
amount
status
```

We want:

> Find every customer, their order count, completed revenue, and customer segment.

```sql
SELECT
    c.customer_id,
    c.name,
    c.region,

    COUNT(o.order_id) AS order_count,

    SUM(
        CASE
            WHEN o.status = 'Completed'
                THEN o.amount
            ELSE 0
        END
    ) AS completed_revenue,

    CASE
        WHEN SUM(
            CASE
                WHEN o.status = 'Completed'
                    THEN o.amount
                ELSE 0
            END
        ) >= 100000
            THEN 'VIP'

        WHEN SUM(
            CASE
                WHEN o.status = 'Completed'
                    THEN o.amount
                ELSE 0
            END
        ) >= 50000
            THEN 'Gold'

        WHEN SUM(
            CASE
                WHEN o.status = 'Completed'
                    THEN o.amount
                ELSE 0
            END
        ) >= 10000
            THEN 'Silver'

        ELSE 'Bronze'
    END AS customer_segment

FROM customers c

LEFT JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.customer_id,
    c.name,
    c.region;
```

This combines:

```text
LEFT JOIN
+
COUNT
+
CASE
+
SUM
+
GROUP BY
```

This is the kind of SQL pattern frequently used in analytics.

---

# 109. JOIN Learning Roadmap

Learn JOINs in this order:

```text
1. Understand Primary Key / Foreign Key
             ↓
2. INNER JOIN
             ↓
3. LEFT JOIN
             ↓
4. RIGHT JOIN
             ↓
5. FULL OUTER JOIN
             ↓
6. CROSS JOIN
             ↓
7. SELF JOIN
             ↓
8. Multi-table JOIN
             ↓
9. JOIN + WHERE
             ↓
10. JOIN + GROUP BY
             ↓
11. JOIN + HAVING
             ↓
12. JOIN + CASE
             ↓
13. JOIN + Aggregate Functions
             ↓
14. Conditional Aggregation
             ↓
15. JOIN + CTE
             ↓
16. JOIN + Window Functions
             ↓
17. Advanced JOIN problems
```

---

# 110. Final Revision Table

| Concept           | Remember                      |
| ----------------- | ----------------------------- |
| `JOIN`            | Combines tables               |
| `INNER JOIN`      | Matching rows                 |
| `LEFT JOIN`       | Keep all left rows            |
| `RIGHT JOIN`      | Keep all right rows           |
| `FULL OUTER JOIN` | Keep everything               |
| `CROSS JOIN`      | All combinations              |
| `SELF JOIN`       | Table with itself             |
| `ON`              | Matching condition            |
| `WHERE`           | Filters result                |
| `GROUP BY`        | Groups joined rows            |
| `HAVING`          | Filters groups                |
| `CASE`            | Conditional logic             |
| `COUNT()`         | Counts rows/non-NULL values   |
| `SUM()`           | Adds values                   |
| `DISTINCT`        | Removes duplicate result rows |
| PK                | Uniquely identifies a row     |
| FK                | References another table      |
| Cardinality       | Relationship between rows     |
| Grain             | What one row represents       |

---

# 111. Final JOIN Mental Model

Remember this:

```text
                 SQL JOIN
                    │
        ┌───────────┼────────────┐
        ↓           ↓            ↓
    INNER        OUTER         CROSS
      │             │             │
      │       ┌─────┼─────┐       │
      │       ↓     ↓     ↓       │
      │     LEFT  RIGHT FULL      │
      │                           │
      └────────────┬──────────────┘
                   ↓
              SELF JOIN
```

For analytics, the most important mental model is:

```text
Tables
  ↓
JOIN
  ↓
Combine related data
  ↓
Filter
  ↓
GROUP BY
  ↓
Aggregate
  ↓
CASE / calculations
  ↓
HAVING
  ↓
ORDER BY
  ↓
Business insight
```

---

# 112. ⭐ The 10 JOIN Patterns You Should Memorize

### 1. Inner join

```sql
SELECT *
FROM A
JOIN B
    ON A.id = B.id;
```

### 2. Left join

```sql
SELECT *
FROM A
LEFT JOIN B
    ON A.id = B.id;
```

### 3. Find missing records

```sql
SELECT A.*
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

### 4. Aggregate after join

```sql
SELECT
    A.id,
    SUM(B.amount)
FROM A
JOIN B
    ON A.id = B.a_id
GROUP BY A.id;
```

### 5. Count child records

```sql
SELECT
    A.id,
    COUNT(B.id)
FROM A
LEFT JOIN B
    ON A.id = B.a_id
GROUP BY A.id;
```

### 6. Three-table join

```sql
SELECT *
FROM A
JOIN B
    ON A.id = B.a_id
JOIN C
    ON B.id = C.b_id;
```

### 7. Self join

```sql
SELECT
    e.name,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

### 8. Range join

```sql
SELECT *
FROM employees e
JOIN salary_grades g
    ON e.salary BETWEEN g.min_salary AND g.max_salary;
```

### 9. Conditional aggregation

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed' THEN amount
            ELSE 0
        END
    )
FROM orders;
```

### 10. Customer analytics

```sql
SELECT
    c.customer_id,
    COUNT(o.order_id) AS orders,
    SUM(o.amount) AS spending
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id;
```

---

# ⭐ Final Takeaway

The most important thing to understand about SQL JOINs is **not just memorizing the syntax**.

Always ask these four questions:

```text
1. Which tables am I combining?
2. What column/relationship connects them?
3. Which rows must be preserved?
4. What is the grain/cardinality after the JOIN?
```

Then choose:

```text
Only matches          → INNER JOIN
Keep left table       → LEFT JOIN
Keep right table      → RIGHT JOIN
Keep both tables      → FULL OUTER JOIN
Every combination     → CROSS JOIN
Same table relationship → SELF JOIN
Range-based matching  → NON-EQUI JOIN
```

And for data analytics, remember the powerful combination:

```text
JOIN
  +
GROUP BY
  +
Aggregate Functions
  +
CASE
  +
HAVING
```

This combination forms the foundation of a large number of real-world SQL analytics queries.
