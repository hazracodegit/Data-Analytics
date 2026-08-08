# SQL — Views, Temporary Tables & Indexes

> A complete revision guide for **SQL Views, Temporary Tables, and Indexes**, including concepts, syntax, examples, differences, use cases, advantages, disadvantages, and data-analytics applications.

---

# 📚 Table of Contents

1. [Views](#1-views)

   * What is a View?
   * Why Views?
   * Syntax
   * Creating Views
   * Querying Views
   * Updating Views
   * Replacing Views
   * Dropping Views
   * View with JOIN
   * View with Aggregation
   * View with WHERE
   * Simple vs Complex Views
   * Advantages
   * Disadvantages
   * Views in Data Analytics

2. [Temporary Tables](#2-temporary-tables)

   * What is a Temporary Table?
   * Why Temporary Tables?
   * Syntax
   * Creating Temporary Tables
   * Inserting Data
   * Creating from SELECT
   * Updating Temporary Tables
   * Joining Temporary Tables
   * Dropping Temporary Tables
   * Temporary Table Lifetime
   * Advantages
   * Disadvantages
   * Temporary Tables in Data Analytics

3. [Indexes](#3-indexes)

   * What is an Index?
   * Why Indexes?
   * How Indexes Work
   * Syntax
   * Creating Indexes
   * Unique Index
   * Composite Index
   * Dropping Indexes
   * Clustered vs Non-Clustered Index
   * Index Selection
   * Index and WHERE
   * Index and JOIN
   * Index and ORDER BY
   * Index and GROUP BY
   * Advantages
   * Disadvantages
   * When Not to Use Indexes

4. [Views vs Temporary Tables vs Indexes](#views-vs-temporary-tables-vs-indexes)

5. [Important Interview Questions](#important-interview-questions)

6. [Quick Revision](#quick-revision)

---

# 1. Views

## 1.1 What is a View?

A **View** is a virtual table created from the result of a SQL query.

It does not normally store the actual result data itself. Instead, it stores the **SQL query definition**.

When we query the view, the database uses the underlying query to retrieve the data.

### Basic idea

```text
Base Tables
     ↓
   SELECT
     ↓
   VIEW
     ↓
User/Application
```

For example:

```sql
CREATE VIEW employee_view AS
SELECT employee_id, name, salary
FROM employees;
```

Now:

```sql
SELECT *
FROM employee_view;
```

The view behaves like a table when querying it.

---

# 1.2 Why Do We Use Views?

Views are mainly used for:

* Simplifying complex SQL queries
* Hiding unnecessary columns
* Improving security
* Reusing queries
* Creating a consistent data layer
* Presenting business-friendly data
* Simplifying reporting
* Abstracting database complexity

---

# 1.3 View Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

---

# 1.4 Creating a Simple View

Suppose we have:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);
```

Create a view:

```sql
CREATE VIEW employee_details AS
SELECT employee_id, name, department
FROM employees;
```

Query:

```sql
SELECT *
FROM employee_details;
```

Output conceptually:

```text
employee_id | name   | department
------------|--------|-----------
1           | Alice  | IT
2           | Bob    | HR
3           | John   | Sales
```

---

# 1.5 View with WHERE

```sql
CREATE VIEW high_salary_employees AS
SELECT employee_id, name, salary
FROM employees
WHERE salary > 50000;
```

Query:

```sql
SELECT *
FROM high_salary_employees;
```

The view only exposes employees whose salary is greater than 50,000.

---

# 1.6 View with JOIN

Views can contain joins.

```sql
CREATE VIEW employee_department AS
SELECT
    e.employee_id,
    e.name,
    e.salary,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Now:

```sql
SELECT *
FROM employee_department;
```

This avoids rewriting the JOIN every time.

---

# 1.7 View with Aggregation

Views can also contain aggregate calculations.

```sql
CREATE VIEW department_salary AS
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

Query:

```sql
SELECT *
FROM department_salary;
```

---

# 1.8 View with ORDER BY

Depending on the SQL database, `ORDER BY` inside a view may have restrictions or may not guarantee the final result order.

Therefore, prefer:

```sql
CREATE VIEW employee_view AS
SELECT employee_id, name, salary
FROM employees;
```

Then:

```sql
SELECT *
FROM employee_view
ORDER BY salary DESC;
```

The final query should control the ordering.

---

# 1.9 Updating a View

Some views can be updated.

For example:

```sql
CREATE VIEW employee_basic AS
SELECT employee_id, name, salary
FROM employees;
```

An update may be possible:

```sql
UPDATE employee_basic
SET salary = 60000
WHERE employee_id = 1;
```

The underlying `employees` table is updated.

However, whether a view is updatable depends on the database and the complexity of the view.

---

# 1.10 Views That Are Usually Difficult to Update

Views containing things such as:

* `GROUP BY`
* Aggregate functions
* `DISTINCT`
* Complex joins
* Set operations
* Certain subqueries
* Calculated/derived structures

may not be directly updatable.

Example:

```sql
CREATE VIEW department_summary AS
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

Trying to update this view generally does not make sense because one row represents an aggregation of many underlying rows.

---

# 1.11 Replacing a View

Some databases support:

```sql
CREATE OR REPLACE VIEW employee_view AS
SELECT
    employee_id,
    name,
    department,
    salary
FROM employees;
```

This modifies the view definition.

Database syntax differs, so always check the specific DBMS.

---

# 1.12 Dropping a View

```sql
DROP VIEW employee_view;
```

This removes the view.

It does **not normally delete the underlying table data**.

Example:

```sql
DROP VIEW high_salary_employees;
```

The original `employees` table remains.

---

# 1.13 View Security

Views can be used to expose only selected columns.

Suppose the table contains:

```text
employee_id
name
email
salary
password_hash
```

We don't want normal users to access sensitive columns.

Create:

```sql
CREATE VIEW employee_public AS
SELECT
    employee_id,
    name,
    email
FROM employees;
```

Users can access:

```sql
SELECT *
FROM employee_public;
```

without directly exposing sensitive columns.

> Views can help with security, but proper permissions and access controls are still required.

---

# 1.14 Simple View vs Complex View

## Simple View

Usually based on one table.

```sql
CREATE VIEW employee_view AS
SELECT employee_id, name, salary
FROM employees;
```

## Complex View

May contain:

* Multiple tables
* JOIN
* GROUP BY
* Aggregation
* Calculations
* Subqueries

Example:

```sql
CREATE VIEW sales_summary AS
SELECT
    c.customer_name,
    SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_name;
```

---

# 1.15 Advantages of Views

### 1. Simplifies Queries

Instead of repeatedly writing:

```sql
SELECT ...
FROM ...
JOIN ...
WHERE ...
GROUP BY ...
```

we can create a view once.

---

### 2. Reusability

The same business logic can be reused.

```sql
SELECT *
FROM sales_summary;
```

---

### 3. Security

Only required columns can be exposed.

---

### 4. Abstraction

Users don't need to know the underlying database structure.

---

### 5. Consistency

Business logic can be centralized.

For example, if "active customer" means:

```sql
status = 'ACTIVE'
AND deleted_at IS NULL
```

we can put this logic into a view.

---

# 1.16 Disadvantages of Views

* Complex views can be difficult to understand.
* Performance depends on the underlying query.
* Some views cannot be updated.
* Nested views can become complicated.
* Changing underlying tables may break views.
* Views do not automatically mean better performance.

---

# 1.17 Views in Data Analytics

Views are extremely useful in analytics.

Suppose raw tables contain:

```text
customers
orders
products
payments
```

An analyst repeatedly needs customer revenue.

Instead of repeatedly writing:

```sql
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.amount) AS revenue
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.customer_name;
```

Create:

```sql
CREATE VIEW customer_revenue AS
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.amount) AS revenue
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.customer_name;
```

Then:

```sql
SELECT *
FROM customer_revenue
ORDER BY revenue DESC;
```

This is useful for:

* Dashboards
* BI reports
* Repeated analysis
* Business metrics
* Reporting layers
* Data marts

---

# 2. Temporary Tables

# 2.1 What is a Temporary Table?

A **Temporary Table** is a table created for temporary use.

It is generally used to store intermediate results during a database session, transaction, procedure, or analytical workflow, depending on the DBMS.

Unlike a normal permanent table, its lifetime is temporary.

---

# 2.2 Why Use Temporary Tables?

Temporary tables are useful when:

* Breaking a complex query into steps
* Storing intermediate results
* Performing multi-step analysis
* Preparing data before final querying
* Reducing repeated calculations
* Debugging SQL
* Performing ETL transformations
* Working with large intermediate datasets

---

# 2.3 Basic Syntax

Syntax differs between database systems.

A common pattern is:

```sql
CREATE TEMPORARY TABLE temp_table (
    id INT,
    name VARCHAR(100)
);
```

Some systems use:

```sql
CREATE TEMP TABLE temp_table (
    id INT,
    name VARCHAR(100)
);
```

Always check your specific DBMS.

---

# 2.4 Creating a Temporary Table

```sql
CREATE TEMPORARY TABLE temp_employees (
    employee_id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

# 2.5 Inserting Data

```sql
INSERT INTO temp_employees
VALUES
(1, 'Alice', 50000),
(2, 'Bob', 60000),
(3, 'John', 70000);
```

Query:

```sql
SELECT *
FROM temp_employees;
```

---

# 2.6 Creating Temporary Table from SELECT

This is extremely useful in data analytics.

```sql
CREATE TEMPORARY TABLE high_salary_employees AS
SELECT
    employee_id,
    name,
    salary
FROM employees
WHERE salary > 50000;
```

Now:

```sql
SELECT *
FROM high_salary_employees;
```

---

# 2.7 Temporary Table for Intermediate Analysis

Suppose we first calculate customer sales.

```sql
CREATE TEMPORARY TABLE customer_sales AS
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM orders
GROUP BY customer_id;
```

Then analyze:

```sql
SELECT *
FROM customer_sales
WHERE total_sales > 100000;
```

Then join it:

```sql
SELECT
    c.customer_name,
    cs.total_sales
FROM customers c
JOIN customer_sales cs
    ON c.customer_id = cs.customer_id;
```

This makes complex workflows easier to manage.

---

# 2.8 Updating a Temporary Table

Temporary tables can generally be manipulated like regular tables.

```sql
UPDATE temp_employees
SET salary = salary * 1.10
WHERE salary < 60000;
```

---

# 2.9 Deleting Data

```sql
DELETE FROM temp_employees
WHERE salary < 50000;
```

---

# 2.10 Joining Temporary Tables

```sql
CREATE TEMPORARY TABLE temp_sales AS
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM orders
GROUP BY customer_id;
```

Then:

```sql
SELECT
    c.customer_name,
    t.total_sales
FROM customers c
JOIN temp_sales t
    ON c.customer_id = t.customer_id;
```

---

# 2.11 Dropping Temporary Tables

```sql
DROP TABLE temp_sales;
```

Some databases automatically remove temporary tables when their applicable session ends.

---

# 2.12 Lifetime of Temporary Tables

The exact behavior depends on the DBMS.

Common behavior:

```text
Create temporary table
        ↓
Use it
        ↓
Session ends
        ↓
Temporary table removed
```

However, databases differ in:

* Session lifetime
* Transaction lifetime
* Visibility
* Storage
* Automatic cleanup
* Logging
* Scope

---

# 2.13 Temporary Tables vs Permanent Tables

| Feature                          | Temporary Table        | Permanent Table |
| -------------------------------- | ---------------------- | --------------- |
| Lifetime                         | Temporary              | Persistent      |
| Storage                          | Temporary/intermediate | Permanent       |
| Automatically removed            | Often                  | No              |
| Used for intermediate results    | Yes                    | Possible        |
| Shared as normal database object | Usually limited        | Yes             |
| Good for ETL steps               | Yes                    | Yes             |
| Long-term storage                | No                     | Yes             |

---

# 2.14 Advantages of Temporary Tables

### 1. Break Complex Queries

Instead of one huge query:

```text
Step 1 → Step 2 → Step 3 → Final Result
```

---

### 2. Intermediate Storage

Useful for storing calculated results.

---

### 3. Easier Debugging

You can inspect intermediate results:

```sql
SELECT *
FROM temp_sales;
```

---

### 4. Reuse Intermediate Data

If a calculation is needed multiple times, storing the result can simplify later queries.

---

### 5. Useful in ETL

Temporary tables can be used while:

```text
Extract
   ↓
Transform
   ↓
Validate
   ↓
Load
```

---

# 2.15 Disadvantages

* Database-specific behavior
* Additional storage/resource usage
* Poorly designed temporary tables can increase workload
* Temporary objects can make scripts more complicated
* Lifetime/scope behavior differs between databases

---

# 2.16 Temporary Tables in Data Analytics

A typical analytics workflow might look like:

```sql
CREATE TEMPORARY TABLE filtered_orders AS
SELECT *
FROM orders
WHERE order_date >= '2026-01-01';
```

Then:

```sql
CREATE TEMPORARY TABLE customer_revenue AS
SELECT
    customer_id,
    SUM(amount) AS revenue
FROM filtered_orders
GROUP BY customer_id;
```

Then:

```sql
SELECT
    c.customer_name,
    cr.revenue
FROM customers c
JOIN customer_revenue cr
    ON c.customer_id = cr.customer_id
ORDER BY cr.revenue DESC;
```

This creates a multi-step analytical pipeline.

---

# 3. Indexes

# 3.1 What is an Index?

An **Index** is a database structure used to make data retrieval faster.

It is similar to the index of a book.

### Without an index

If you search for:

```text
Customer ID = 1050
```

the database may need to inspect many rows.

This is called a **table scan** or **sequential scan**, depending on the database and execution plan.

### With an index

The database can potentially locate the relevant rows much faster.

Conceptually:

```text
Index
  ↓
Find key
  ↓
Locate row
  ↓
Return data
```

---

# 3.2 Simple Real-World Example

Imagine a book with 2,000 pages.

Without an index:

```text
Page 1
Page 2
Page 3
...
Page 2000
```

You may need to search many pages.

With an index:

```text
Python → Page 500
SQL    → Page 850
NumPy  → Page 1200
```

You can jump closer to the required information.

Database indexes provide a similar concept for data access.

---

# 3.3 Why Are Indexes Used?

Indexes are mainly used to improve:

```text
SELECT performance
JOIN performance
WHERE filtering
ORDER BY
GROUP BY
UNIQUE lookups
```

However, indexes are not automatically beneficial for every query.

---

# 3.4 Basic Index Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

---

# 3.5 Query Using Indexed Column

```sql
SELECT *
FROM employees
WHERE name = 'Alice';
```

The database optimizer may choose the index.

Important:

> Creating an index does not guarantee that the database will use it.

The optimizer decides based on statistics, cost, selectivity, table size, query structure, and other factors.

---

# 3.6 Index on Multiple Columns

A **composite index** contains multiple columns.

```sql
CREATE INDEX idx_employee_dept_salary
ON employees(department, salary);
```

This is called a:

```text
Composite Index
```

---

# 3.7 Column Order Matters

Consider:

```sql
CREATE INDEX idx_example
ON employees(department, salary);
```

The order is:

```text
department → salary
```

This can be particularly useful for queries filtering or ordering based on the leading column(s), depending on the database optimizer.

For example:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

And potentially:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

But an index beginning with `department` is not equivalent to an index beginning with `salary`.

---

# 3.8 Composite Index Example

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

Useful query:

```sql
SELECT *
FROM orders
WHERE customer_id = 101
AND order_date >= '2026-01-01';
```

The exact usefulness depends on the database and data distribution.

---

# 3.9 Unique Index

A unique index prevents duplicate indexed values.

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employees(email);
```

Now two employees generally cannot have the same email.

Example:

```text
alice@example.com
bob@example.com
```

Allowed.

But:

```text
alice@example.com
alice@example.com
```

would violate the uniqueness rule.

> A `UNIQUE` constraint is the logical integrity feature; a unique index is an index structure enforcing uniqueness in many database systems. The exact implementation is DBMS-specific.

---

# 3.10 Primary Key and Indexes

When you create:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

the database typically creates or uses an index-like structure to enforce efficient uniqueness for the primary key.

The exact physical implementation depends on the database.

Therefore, you generally don't need to create another ordinary index on the exact same primary-key column just for basic primary-key lookups.

---

# 3.11 Index for WHERE

Indexes are often useful for filtering.

```sql
CREATE INDEX idx_salary
ON employees(salary);
```

Query:

```sql
SELECT *
FROM employees
WHERE salary > 80000;
```

The optimizer may use the index depending on the data distribution and query cost.

---

# 3.12 Index for JOIN

Suppose:

```sql
SELECT *
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Indexes on join columns can improve performance, particularly for large tables and suitable query plans.

Example:

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

---

# 3.13 Index for ORDER BY

Suppose:

```sql
SELECT *
FROM employees
ORDER BY salary;
```

An index on salary may sometimes help:

```sql
CREATE INDEX idx_salary
ON employees(salary);
```

Whether it helps depends on the database optimizer, requested ordering, selectivity, query shape, and other factors.

---

# 3.14 Index for GROUP BY

Query:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department;
```

An index on:

```sql
department
```

may help some execution plans.

```sql
CREATE INDEX idx_department
ON employees(department);
```

But again, the optimizer decides whether using the index is actually cheaper.

---

# 3.15 Index for LIKE

Consider:

```sql
SELECT *
FROM employees
WHERE name LIKE 'Ali%';
```

An index on `name` may be useful depending on the DBMS and collation.

But:

```sql
WHERE name LIKE '%Ali%'
```

is much harder for many conventional B-tree indexes to optimize because the search begins with a wildcard.

---

# 3.16 Index and Functions

Consider:

```sql
SELECT *
FROM employees
WHERE UPPER(name) = 'ALICE';
```

A normal index on:

```sql
name
```

may not be usable efficiently because the query transforms the column.

Some databases support **functional/expression indexes**, for example conceptually:

```sql
CREATE INDEX idx_upper_name
ON employees(UPPER(name));
```

Syntax and availability vary by DBMS.

---

# 3.17 Clustered Index

A **clustered index** determines how table data is physically organized according to the index key in database systems that support this concept.

A common conceptual representation:

```text
Index
 ↓
Data organized according to index
```

Important:

> "Clustered" does not mean the same thing in every database system.

For example, SQL Server has a specific clustered-index concept, while other databases use different storage architectures.

---

# 3.18 Non-Clustered Index

A non-clustered index is a separate index structure that points toward the underlying table data.

Conceptually:

```text
Index
 ↓
Row locator
 ↓
Table data
```

This can allow multiple secondary indexes on different columns.

---

# 3.19 Clustered vs Non-Clustered

| Feature           | Clustered                                         | Non-Clustered            |
| ----------------- | ------------------------------------------------- | ------------------------ |
| Data organization | Related to index key                              | Separate index structure |
| Number per table  | Often limited to one in systems with this concept | Usually many             |
| Lookup            | Can be efficient                                  | Can be efficient         |
| Physical storage  | Depends on DBMS                                   | Depends on DBMS          |
| Terminology       | DBMS-specific                                     | More general concept     |

> Do not assume every database implements clustered/non-clustered indexes identically.

---

# 3.20 B-Tree Index

One of the most common index structures is the **B-tree/B+ tree family**.

Conceptually:

```text
             Root
           /      \
        Node      Node
       /   \      /   \
    Leaf   Leaf Leaf  Leaf
```

It keeps keys organized so the database can efficiently navigate toward matching values.

Common uses include:

```sql
=
>
<
>=
<=
BETWEEN
ORDER BY
```

depending on the database and query.

---

# 3.21 Hash Index

Hash-based indexes use a hash structure.

Conceptually:

```text
Key
 ↓
Hash function
 ↓
Bucket
 ↓
Value
```

They can be particularly useful for equality lookups in systems that support them.

Example:

```sql
WHERE employee_id = 100
```

But hash indexing is generally not suitable for range queries such as:

```sql
WHERE salary > 50000
```

Exact capabilities depend on the DBMS.

---

# 3.22 Full-Text Index

For searching natural language text, specialized full-text indexes can be used.

Example concept:

```sql
SELECT *
FROM articles
WHERE ...
```

Full-text search is different from simply using:

```sql
LIKE '%keyword%'
```

Databases provide different full-text search features and syntax.

---

# 3.23 Spatial Index

Spatial databases can use specialized indexes for:

* Geographic coordinates
* Locations
* Maps
* Polygons
* Geographic objects

Applications include:

```text
Maps
GPS
Delivery systems
Location-based services
Geospatial analytics
```

---

# 3.24 Partial / Filtered Index

Some database systems support indexes that contain only rows satisfying a condition.

Conceptually:

```sql
CREATE INDEX idx_active_users
ON users(email)
WHERE status = 'ACTIVE';
```

This is DBMS-specific.

It can be useful when only a subset of rows is frequently queried.

---

# 3.25 Covering Index

A **covering index** contains all columns needed for a query, allowing the database to potentially answer the query directly from the index without fetching additional table data.

Example:

```sql
CREATE INDEX idx_employee_dept_name
ON employees(department, name);
```

Query:

```sql
SELECT name
FROM employees
WHERE department = 'IT';
```

The index may contain everything needed for the query.

Whether the optimizer uses it depends on the database and execution plan.

---

# 3.26 Index Selectivity

**Selectivity** describes how effectively a column distinguishes rows.

### High-selectivity column

Example:

```text
email
employee_id
passport_number
```

Many unique values.

### Low-selectivity column

Example:

```text
gender
status
boolean flags
```

Few distinct values.

High-selectivity columns are often good candidates for indexes, although this is not an absolute rule.

---

# 3.27 Example

Suppose:

```text
1,000,000 employees
```

Column:

```text
employee_id
```

contains:

```text
1, 2, 3, 4, ...
```

Very high selectivity.

But:

```text
status
```

contains only:

```text
ACTIVE
INACTIVE
```

Low selectivity.

An index on `employee_id` is often more obviously useful for point lookups than an index on `status`, though the latter can still be useful in certain queries and data distributions.

---

# 3.28 Indexes and Write Operations

Indexes improve many reads, but they also have a cost.

Consider:

```sql
INSERT
UPDATE
DELETE
```

When table data changes, relevant indexes may also need to be updated.

Therefore:

```text
More indexes
      ↓
Faster some SELECTs
      +
More maintenance
      ↓
Potentially slower INSERT/UPDATE/DELETE
```

---

# 3.29 Index Storage

Indexes consume storage.

Suppose:

```text
Table = 10 GB
Indexes = 5 GB
```

Total database storage becomes approximately:

```text
15 GB
```

The exact storage depends on the database, data types, index structure, compression, and other factors.

---

# 3.30 Dropping an Index

Syntax varies by database.

A common form is:

```sql
DROP INDEX index_name;
```

Some DBMSs require specifying the table:

```sql
DROP INDEX index_name ON table_name;
```

Always check your database's syntax.

---

# 3.31 Finding Indexes

Most database systems provide metadata tables/views for inspecting indexes.

For example, database-specific catalog commands can show:

```text
Index name
Table
Columns
Index type
Uniqueness
Size
```

The exact command differs between PostgreSQL, MySQL, SQL Server, Oracle, SQLite, etc.

---

# 3.32 EXPLAIN and Indexes

One of the most important tools for understanding indexes is:

```sql
EXPLAIN
```

Example:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_id = 100;
```

Some databases also support:

```sql
EXPLAIN ANALYZE
```

This helps inspect how the database plans or executes a query.

---

# 3.33 Query Plan

A query plan may show operations such as:

```text
Table Scan
Index Scan
Index Seek
Hash Join
Nested Loop
Sort
Aggregate
```

Exact terminology varies by database.

The plan helps answer:

> Is my index actually helping?

---

# 3.34 Indexing Best Practices

### 1. Index Frequently Filtered Columns

Example:

```sql
WHERE customer_id = 100
```

---

### 2. Index Important Join Columns

Example:

```sql
ON orders.customer_id = customers.customer_id
```

---

### 3. Consider Composite Indexes

When queries frequently use:

```sql
WHERE customer_id = ?
AND order_date >= ?
```

consider:

```sql
(customer_id, order_date)
```

if supported by workload analysis.

---

### 4. Don't Index Everything

Every index has a cost.

---

### 5. Analyze Query Plans

Use:

```sql
EXPLAIN
```

or the database's equivalent.

---

### 6. Consider Data Distribution

An index useful for one dataset may be less useful for another.

---

### 7. Monitor Unused Indexes

Unused indexes consume resources and may slow writes.

---

# 3.35 When Should You NOT Create an Index?

Avoid unnecessary indexes when:

### 1. Table is Tiny

For a small table, scanning the entire table may already be extremely fast.

### 2. Column Has Very Low Selectivity

Example:

```text
is_active = TRUE/FALSE
```

An index may not always help.

### 3. Table Has Heavy Writes

If the table receives enormous numbers of:

```text
INSERT
UPDATE
DELETE
```

too many indexes can increase write overhead.

### 4. Index Is Never Used

An unused index provides little read benefit while consuming storage and maintenance resources.

---

# 3.36 Indexes in Data Analytics

Indexes can be useful in analytics when working with large relational datasets.

Example:

```sql
SELECT
    customer_id,
    SUM(amount)
FROM orders
WHERE order_date >= '2026-01-01'
GROUP BY customer_id;
```

Potentially useful index:

```sql
CREATE INDEX idx_orders_date_customer
ON orders(order_date, customer_id);
```

But the best index depends on:

* Data size
* Query frequency
* Data distribution
* Selectivity
* Database engine
* Existing indexes
* Execution plan
* Read/write workload

Never assume an index is useful simply because a column appears in a query.

---

# 4. Views vs Temporary Tables vs Indexes

These three concepts solve completely different problems.

| Feature                    | View                       | Temporary Table                | Index                    |
| -------------------------- | -------------------------- | ------------------------------ | ------------------------ |
| Main purpose               | Reusable query abstraction | Temporary intermediate storage | Faster data access       |
| Stores query definition    | Yes                        | No                             | No                       |
| Stores data                | Usually no                 | Yes                            | Index structure          |
| Temporary                  | Usually no                 | Yes                            | No                       |
| Improves readability       | Yes                        | Yes                            | Not primarily            |
| Improves performance       | Not necessarily            | Sometimes                      | Often for suitable reads |
| Used for intermediate data | Not primarily              | Yes                            | No                       |
| Used for security          | Yes                        | Not primarily                  | No                       |
| Can contain query logic    | Yes                        | Data comes from queries        | No                       |
| Useful in analytics        | Very useful                | Very useful                    | Very useful              |

---

# 5. View vs Temporary Table

## View

A view is like a **saved query**.

```text
Query definition
      ↓
     View
      ↓
Query whenever needed
```

Example:

```sql
CREATE VIEW high_value_customers AS
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 100000;
```

---

## Temporary Table

A temporary table is like a **temporary working table**.

```text
Query
 ↓
Temporary data
 ↓
Manipulate
 ↓
Analyze
 ↓
Remove
```

Example:

```sql
CREATE TEMPORARY TABLE high_value_customers AS
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id;
```

---

# 6. View vs Temporary Table — Key Difference

### View

```text
Saved SQL logic
```

### Temporary Table

```text
Temporary stored result/data
```

A view is primarily an abstraction layer.

A temporary table is primarily a workspace for intermediate data.

---

# 7. Index vs View

These are completely different.

### View

Helps with:

```text
Abstraction
Reusability
Security
Simplification
```

### Index

Helps with:

```text
Data retrieval performance
```

Example:

```sql
CREATE VIEW employee_view AS
SELECT employee_id, name
FROM employees;
```

versus:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

The first creates a logical interface.

The second creates an access structure.

---

# 8. Index vs Temporary Table

### Index

```text
Permanent optimization structure
```

### Temporary Table

```text
Temporary data storage
```

Example:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

versus:

```sql
CREATE TEMPORARY TABLE temp_orders AS
SELECT *
FROM orders
WHERE amount > 1000;
```

---

# 9. Practical Analytics Example

Suppose we have:

```text
customers
orders
products
```

We want to build a customer sales report.

---

## Step 1 — Create a View

```sql
CREATE VIEW customer_orders AS
SELECT
    c.customer_id,
    c.customer_name,
    o.order_id,
    o.order_date,
    o.amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Now analysts can query:

```sql
SELECT *
FROM customer_orders;
```

---

## Step 2 — Create Temporary Analysis Table

```sql
CREATE TEMPORARY TABLE customer_sales AS
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM customer_orders
GROUP BY customer_id;
```

---

## Step 3 — Analyze

```sql
SELECT
    c.customer_name,
    cs.total_sales
FROM customers c
JOIN customer_sales cs
    ON c.customer_id = cs.customer_id
ORDER BY cs.total_sales DESC;
```

---

## Step 4 — Use an Index

If customer joins are frequent:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

Now we have:

```text
VIEW
 ↓
Simplify reusable logic

TEMP TABLE
 ↓
Store intermediate analytical results

INDEX
 ↓
Improve suitable data access
```

---

# 10. Important Interview Questions

## Q1. What is a View?

A view is a virtual table based on a SQL query.

---

## Q2. Does a View store data?

Normally, a standard view stores the query definition rather than storing a separate copy of the result data.

Some databases also support **materialized views**, which are different because they physically store query results.

---

## Q3. What is a Temporary Table?

A temporary table is a table intended for temporary/intermediate use, with its lifetime and scope determined by the database system.

---

## Q4. Why use Temporary Tables?

They are useful for:

* Intermediate results
* Complex transformations
* Multi-step analysis
* ETL
* Debugging
* Breaking large queries into manageable steps

---

## Q5. What is an Index?

An index is a database data structure that can improve data retrieval performance.

---

## Q6. Does an index always make queries faster?

**No.**

The optimizer decides whether an index is beneficial.

For small tables, low-selectivity conditions, or queries where scanning is cheaper, the database may ignore the index.

---

## Q7. Can indexes slow down INSERT?

Yes.

Because indexes may need to be maintained when rows are inserted.

---

## Q8. Can indexes slow down UPDATE?

Yes, especially when indexed columns are modified.

---

## Q9. Can indexes slow down DELETE?

Yes.

The database may need to remove corresponding entries from indexes.

---

## Q10. What is a Composite Index?

An index created on multiple columns.

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

---

## Q11. Does column order matter in a composite index?

**Yes.**

```sql
(customer_id, order_date)
```

is not equivalent to:

```sql
(order_date, customer_id)
```

The optimal order depends on the workload and query patterns.

---

## Q12. What is a Unique Index?

An index that enforces uniqueness of indexed values, subject to database rules around `NULL` and other details.

```sql
CREATE UNIQUE INDEX idx_email
ON employees(email);
```

---

## Q13. What is a Clustered Index?

A database-specific index concept where the table's data organization is associated with the index key.

The exact implementation differs between DBMSs.

---

## Q14. What is a Non-Clustered Index?

A separate index structure that provides another access path to table data.

---

## Q15. What is EXPLAIN?

`EXPLAIN` is used to inspect how the database plans to execute a query.

Example:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_id = 100;
```

---

# 11. Quick Revision

## VIEW

```text
Saved SQL query
     ↓
Virtual table
     ↓
Reusable
```

### Syntax

```sql
CREATE VIEW view_name AS
SELECT ...
FROM ...;
```

### Delete

```sql
DROP VIEW view_name;
```

### Main Uses

```text
Abstraction
Security
Reusability
Reporting
Simplification
```

---

# TEMPORARY TABLE

```text
Temporary working table
       ↓
Intermediate data
       ↓
Analysis
       ↓
Cleanup
```

### Syntax

```sql
CREATE TEMPORARY TABLE temp_name AS
SELECT ...;
```

### Main Uses

```text
Intermediate results
ETL
Complex analysis
Data transformation
Debugging
```

---

# INDEX

```text
Index
 ↓
Faster data access
```

### Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

### Composite Index

```sql
CREATE INDEX idx_name
ON table_name(column1, column2);
```

### Unique Index

```sql
CREATE UNIQUE INDEX idx_name
ON table_name(column_name);
```

### Main Uses

```text
WHERE
JOIN
ORDER BY
GROUP BY
Lookup
```

---

# 12. One-Line Memory Trick

```text
VIEW          → "Save the QUERY"
TEMP TABLE    → "Save the DATA temporarily"
INDEX         → "Find the DATA faster"
```

---

# 13. Complete Concept Map

```text
                    SQL DATABASE OBJECTS
                           |
          +----------------+----------------+
          |                |                |
        VIEW          TEMPORARY TABLE      INDEX
          |                |                |
     Saved query       Temporary data    Access structure
          |                |                |
     Reusability       Intermediate       Faster reads
     Abstraction       Analysis           Lookup
     Security          ETL                JOIN
     Reporting         Transformation     Filtering
          |                |                |
          +----------------+----------------+
                           |
                     DATA ANALYTICS
                           |
          +----------------+----------------+
          |                |                |
       Reporting       Transformation    Performance
          |                |                |
        Views        Temp Tables         Indexes
```

---

# 14. Final Revision Table

| Concept             | Remember This                                                  |
| ------------------- | -------------------------------------------------------------- |
| View                | Saved SQL query / virtual table                                |
| Temporary Table     | Temporary working data                                         |
| Index               | Faster access path to data                                     |
| Simple View         | Usually based on one table                                     |
| Complex View        | Can involve joins, aggregation, etc.                           |
| Composite Index     | Index on multiple columns                                      |
| Unique Index        | Enforces uniqueness                                            |
| Clustered Index     | DBMS-specific data/index organization concept                  |
| Non-Clustered Index | Separate access structure                                      |
| B-tree              | Common index structure                                         |
| Hash Index          | Useful for equality-style lookups where supported              |
| Full-text Index     | Text searching                                                 |
| Spatial Index       | Geographic/spatial data                                        |
| Covering Index      | Index contains data needed by a query                          |
| Selectivity         | How well values distinguish rows                               |
| EXPLAIN             | Inspect query execution plan                                   |
| Too Many Indexes    | More storage + write/maintenance overhead                      |
| View ≠ Index        | View abstracts; index optimizes access                         |
| Temp Table ≠ View   | Temp table stores temporary data; view stores query definition |

---

# ⭐ Most Important Points to Remember

```text
1. VIEW
   → Virtual/logical representation based on a query
   → Excellent for abstraction, reuse, security, reporting

2. TEMPORARY TABLE
   → Temporary physical working data
   → Excellent for intermediate analysis and multi-step processing

3. INDEX
   → Data access structure
   → Can make suitable SELECT queries much faster
   → Has storage and write-maintenance costs

4. COMPOSITE INDEX
   → Multiple columns
   → Column order matters

5. EXPLAIN
   → Used to understand query execution plans

6. INDEX ≠ GUARANTEED SPEED
   → The optimizer decides whether to use it

7. VIEW ≠ MATERIALIZED VIEW
   → Standard view generally stores query definition
   → Materialized view stores computed results and requires refresh/maintenance

8. TEMP TABLE ≠ PERMANENT TABLE
   → Temporary tables are intended for temporary/intermediate work

9. MORE INDEXES ≠ ALWAYS BETTER
   → More indexes can improve reads but increase storage and write overhead
```

---

# 🚀 Data Analytics Perspective

For a **Data Analyst**, remember the three concepts like this:

```text
                    DATA ANALYST
                         |
          +--------------+--------------+
          |              |              |
        VIEW        TEMP TABLE        INDEX
          |              |              |
     Reporting       Analysis       Performance
     Dashboards      ETL steps      Faster queries
     Reusable SQL    Intermediate   Large datasets
     Business logic  calculations   Filtering
```

### Typical workflow

```text
Raw Database Tables
        ↓
      VIEW
        ↓
Standardized analytical dataset
        ↓
TEMPORARY TABLE
        ↓
Intermediate calculations
        ↓
INDEX
        ↓
Efficient data retrieval
        ↓
Final SQL Analysis
        ↓
Dashboard / Report / Python / Power BI
```

This makes **Views, Temporary Tables, and Indexes** three important concepts to understand when moving from basic SQL into **real-world SQL development and data analytics**.
