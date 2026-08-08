# SQL Fundamentals

> Complete SQL fundamentals notes for **coding, database development, data analytics, and interview preparation**.

---

# 1. What is SQL?

**SQL (Structured Query Language)** is a standard language used to communicate with and manage data stored in **relational databases**.

SQL can be used to:

* Create databases and tables
* Store data
* Retrieve data
* Modify data
* Delete data
* Filter data
* Sort data
* Aggregate data
* Join data from multiple tables
* Analyze data
* Control database access
* Manage transactions
* Create database objects

### Simple Example

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

This query means:

> Get the `name` and `salary` of employees whose salary is greater than 50,000.

---

# 2. Why is SQL Important?

SQL is one of the most important technologies for working with structured data.

It is heavily used in:

* Data Analytics
* Data Science
* Business Intelligence
* Backend Development
* Software Development
* Data Engineering
* Database Administration
* Machine Learning Data Preparation
* Reporting
* Business Intelligence
* ETL/ELT pipelines

### For Data Analysts

SQL is particularly important because analysts frequently need to:

```text
Database
   ↓
SQL Query
   ↓
Filtered Data
   ↓
Aggregated Data
   ↓
Analysis
   ↓
Dashboard / Report / Business Decision
```

---

# 3. What Does SQL Actually Do?

SQL allows you to communicate with a database.

For example, suppose a database contains:

```text
employees
--------------------------------
id | name  | department | salary
--------------------------------
1  | John  | IT         | 60000
2  | Alice | HR         | 45000
3  | Mark  | IT         | 70000
```

You can ask the database:

### Retrieve all employees

```sql
SELECT *
FROM employees;
```

### Retrieve only IT employees

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### Find average salary

```sql
SELECT AVG(salary)
FROM employees;
```

SQL allows you to convert a business question into a database query.

---

# 4. SQL is a Declarative Language

SQL is primarily a **declarative language**.

This means you generally tell the database:

> **What result you want**

rather than:

> **Exactly how the database should produce it**

Example:

```sql
SELECT name
FROM employees
WHERE salary > 50000;
```

You specify:

* Which columns you need
* Which table to use
* Which condition should be satisfied

The database's query optimizer decides how to execute the query.

---

# 5. SQL vs Programming Languages

Traditional programming:

```text
Tell the computer:
1. Open the file
2. Read each row
3. Check salary
4. If salary > 50000
5. Store the name
6. Print the result
```

SQL:

```sql
SELECT name
FROM employees
WHERE salary > 50000;
```

The database handles the execution details.

However, SQL can also contain programming features in database-specific systems, such as:

* Variables
* Loops
* Conditions
* Procedures
* Functions
* Error handling

These are usually provided through extensions such as:

* PL/SQL
* T-SQL
* PL/pgSQL

---

# 6. SQL and Relational Databases

SQL is most strongly associated with **relational databases**.

A relational database stores data in tables.

Example:

```text
customers

+----+----------+----------+
| id | name     | city     |
+----+----------+----------+
| 1  | John     | Delhi    |
| 2  | Alice    | Mumbai   |
| 3  | Mark     | Chennai  |
+----+----------+----------+
```

Another table:

```text
orders

+----+-------------+--------+
| id | customer_id | amount |
+----+-------------+--------+
| 1  | 1           | 5000   |
| 2  | 2           | 3000   |
| 3  | 1           | 2000   |
+----+-------------+--------+
```

The tables can be related using:

```text
customers.id
      ↓
orders.customer_id
```

---

# 7. What is a Database?

A **database** is an organized collection of data that can be stored, managed, retrieved, and manipulated.

Example:

```text
Company Database
│
├── employees
├── departments
├── customers
├── products
└── orders
```

A database can contain:

* Tables
* Views
* Indexes
* Procedures
* Functions
* Triggers
* Constraints
* Other database objects

---

# 8. What is DBMS?

**DBMS = Database Management System**

A DBMS is software that allows users and applications to create, store, retrieve, update, and manage data.

Examples:

* MySQL
* PostgreSQL
* Microsoft SQL Server
* Oracle Database
* SQLite
* MariaDB

A DBMS provides features such as:

* Data storage
* Data retrieval
* Security
* Transactions
* Concurrency
* Backup and recovery
* Access control

---

# 9. What is RDBMS?

**RDBMS = Relational Database Management System**

An RDBMS stores data in related tables.

Example:

```text
customers
     │
     │ customer_id
     ↓
orders
     │
     │ product_id
     ↓
products
```

Important characteristics include:

* Tables
* Rows
* Columns
* Relationships
* Keys
* Constraints
* Referential integrity
* SQL support

---

# 10. DBMS vs RDBMS

| DBMS                               | RDBMS                                   |
| ---------------------------------- | --------------------------------------- |
| General database management system | Relational database management system   |
| May not use relationships          | Uses relationships between tables       |
| Can have different storage models  | Uses relational tables                  |
| May have weaker integrity rules    | Strong support for relational integrity |
| Broader concept                    | Specific type of DBMS                   |

---

# 11. What is a Table?

A **table** is a structured collection of related data arranged into rows and columns.

Example:

```text
employees

+----+--------+-------------+--------+
| id | name   | department  | salary |
+----+--------+-------------+--------+
| 1  | John   | IT          | 60000  |
| 2  | Alice  | HR          | 45000  |
| 3  | Mark   | Finance     | 55000  |
+----+--------+-------------+--------+
```

Here:

* `employees` → table
* `id`, `name`, `department`, `salary` → columns
* Each horizontal record → row

---

# 12. What is a Row?

A **row** represents one record in a table.

Example:

```text
1 | John | IT | 60000
```

This represents one employee.

A row is also commonly called:

* Record
* Tuple

---

# 13. What is a Column?

A **column** represents a particular attribute or property of the data.

Example:

```text
id
name
department
salary
```

Each column normally has:

* Name
* Data type
* Optional constraints

Example:

```sql
salary DECIMAL(10,2)
```

---

# 14. Row vs Column

| Row                            | Column                           |
| ------------------------------ | -------------------------------- |
| Represents a record            | Represents an attribute          |
| Horizontal                     | Vertical                         |
| Contains values for one entity | Contains values for one property |
| Also called tuple              | Also called attribute            |

Example:

```text
+----+--------+--------+
| id | name   | salary |
+----+--------+--------+
| 1  | John   | 60000  | ← Row
| 2  | Alice  | 50000  | ← Row
+----+--------+--------+
  ↑      ↑       ↑
Columns
```

---

# 15. What is a Schema?

A **schema** describes the structure of database objects.

It can define:

* Tables
* Columns
* Data types
* Constraints
* Views
* Functions
* Other objects

Depending on the database system, "schema" can also represent a namespace/container for objects.

Example:

```text
company_schema
│
├── employees
├── departments
├── customers
└── orders
```

---

# 16. Database vs Schema

A simple conceptual distinction:

```text
Database
   │
   ├── Schema
   │      ├── Table
   │      ├── View
   │      └── Function
   │
   └── Other database objects
```

The exact relationship between databases and schemas differs by DBMS.

For example, PostgreSQL makes extensive use of schemas, while MySQL uses the terms **database** and **schema** more interchangeably.

---

# 17. What is a Record?

A record is one complete row of information.

Example:

```text
101 | Rahul | IT | 75000
```

This represents one employee record.

---

# 18. What is an Attribute?

An attribute describes a property of an entity.

For an employee:

```text
Employee
│
├── employee_id
├── name
├── email
├── department
├── salary
└── joining_date
```

Each of these is an attribute.

In a relational table, attributes generally correspond to columns.

---

# 19. What is an Entity?

An **entity** is something about which data is stored.

Examples:

* Employee
* Customer
* Product
* Order
* Student
* Course

Example:

```text
Entity: Employee

Attributes:
- employee_id
- name
- department
- salary
```

---

# 20. Entity vs Attribute vs Record

Consider:

```text
employees

+----+--------+--------+
| id | name   | salary |
+----+--------+--------+
| 1  | John   | 60000  |
+----+--------+--------+
```

* `Employee` → Entity
* `id`, `name`, `salary` → Attributes
* `1, John, 60000` → Values
* Entire row → Record

---

# 21. What is a Relationship?

A relationship defines how entities are associated.

Example:

```text
Customer ───── places ───── Order
```

One customer can place many orders.

```text
Customer
    │
    │ 1
    │
    │
    │ N
    ↓
Order
```

This is a **one-to-many relationship**.

---

# 22. Types of Relationships

## One-to-One

One record is related to one record.

```text
Person ─── Passport
  1          1
```

---

## One-to-Many

One record is related to multiple records.

```text
Customer
   1
   │
   │
   N
 Orders
```

---

## Many-to-Many

Multiple records are related to multiple records.

Example:

```text
Students ←→ Courses
```

A student can take multiple courses.

A course can contain multiple students.

This is usually implemented using a junction/bridge table:

```text
students
    │
    │
student_courses
    │
    │
courses
```

---

# 23. SQL Identifiers

Identifiers are names used for database objects.

Examples:

```text
employees
employee_id
salary
customer_orders
```

Identifiers can name:

* Databases
* Schemas
* Tables
* Columns
* Views
* Functions
* Procedures

Good naming:

```text
employee_id
customer_name
order_date
```

Avoid confusing names such as:

```text
x
abc
data1
```

unless there is a specific reason.

---

# 24. SQL Keywords

Keywords are reserved words that have special meaning in SQL.

Examples:

```text
SELECT
FROM
WHERE
INSERT
UPDATE
DELETE
CREATE
ALTER
DROP
JOIN
GROUP BY
ORDER BY
```

Example:

```sql
SELECT name
FROM employees;
```

Here:

* `SELECT` → keyword
* `FROM` → keyword
* `name` → identifier
* `employees` → identifier

---

# 25. SQL Statements

A SQL statement is an instruction sent to the database.

Example:

```sql
SELECT *
FROM employees;
```

Another:

```sql
INSERT INTO employees
VALUES (1, 'John', 60000);
```

A statement usually ends with:

```text
;
```

Example:

```sql
SELECT * FROM employees;
```

---

# 26. SQL Clauses

A clause is a component of a SQL statement.

Example:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY AVG(salary) DESC;
```

Major clauses:

```text
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
```

---

# 27. SQL Comments

Comments are ignored by the database engine and are used to document code.

## Single-Line Comment

```sql
-- This is a comment

SELECT *
FROM employees;
```

## Multi-Line Comment

```sql
/*
   This is a
   multi-line comment
*/

SELECT *
FROM employees;
```

Comment syntax can vary slightly between database systems.

---

# 28. SQL is Case-Insensitive for Keywords

In most SQL systems, keywords are not case-sensitive.

These are generally equivalent:

```sql
SELECT * FROM employees;
```

```sql
select * from employees;
```

```sql
SeLeCt * FrOm employees;
```

However, **identifier case sensitivity depends on the DBMS and identifier rules**.

Best practice:

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

Use consistent formatting.

---

# 29. SQL Naming Conventions

A common convention is:

```text
snake_case
```

Examples:

```text
employee_id
customer_name
order_date
product_price
```

Avoid unnecessarily complicated names:

```text
x1
a
abc123
```

Use descriptive names:

```text
customer_id
total_revenue
order_date
```

---

# 30. SQL Data Values

A table can contain different types of values.

Example:

```text
+----+---------+-------+------------+
| id | name    | age   | salary     |
+----+---------+-------+------------+
| 1  | Rahul   | 25    | 50000.00   |
+----+---------+-------+------------+
```

Values can include:

* Numbers
* Strings
* Dates
* Times
* Boolean values
* NULL

---

# 31. Strings in SQL

String values are generally enclosed in single quotes.

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Correct:

```sql
'John'
```

Incorrect in standard SQL style:

```sql
"John"
```

Double quotes are commonly used for identifiers in systems that support standard identifier quoting.

---

# 32. Numbers in SQL

Numbers normally do not require quotes.

Correct:

```sql
WHERE salary > 50000
```

Not recommended:

```sql
WHERE salary > '50000'
```

The second may be implicitly converted by some systems, but relying on implicit conversion can cause errors or poor performance.

---

# 33. Dates in SQL

Date syntax varies between DBMSs, but standard-style literals are commonly written as:

```sql
DATE '2026-08-08'
```

Many systems also accept:

```sql
'2026-08-08'
```

Example:

```sql
SELECT *
FROM employees
WHERE joining_date >= '2026-01-01';
```

Always understand the date/time syntax of your specific database.

---

# 34. What is NULL?

`NULL` means:

> Missing, unknown, or not applicable value.

It does **not** mean:

```text
0
```

It does **not** mean:

```text
''
```

It does **not** mean:

```text
FALSE
```

Example:

```text
+----+--------+-------+
| id | name   | phone |
+----+--------+-------+
| 1  | Rahul  | NULL  |
+----+--------+-------+
```

The phone number is unknown or unavailable.

---

# 35. NULL Comparison

This is incorrect:

```sql
WHERE phone = NULL;
```

Use:

```sql
WHERE phone IS NULL;
```

To find non-null values:

```sql
WHERE phone IS NOT NULL;
```

This is extremely important in SQL.

---

# 36. Three-Valued Logic

SQL uses three logical states:

```text
TRUE
FALSE
UNKNOWN
```

Comparisons involving `NULL` often produce `UNKNOWN`.

Example:

```sql
NULL = NULL
```

does not evaluate to TRUE.

Instead, it is UNKNOWN.

This is why SQL uses:

```sql
IS NULL
```

rather than:

```sql
= NULL
```

---

# 37. SQL Command Categories

SQL commands are commonly grouped into categories.

```text
SQL
│
├── DDL
├── DML
├── DQL
├── DCL
└── TCL
```

---

# 38. DDL

**DDL = Data Definition Language**

Used to define or modify database structures.

Common commands:

```text
CREATE
ALTER
DROP
TRUNCATE
RENAME
```

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

# 39. DML

**DML = Data Manipulation Language**

Used to manipulate data stored in tables.

Common commands:

```text
INSERT
UPDATE
DELETE
MERGE
```

Example:

```sql
INSERT INTO employees
(employee_id, name, salary)
VALUES
(1, 'Rahul', 50000);
```

---

# 40. DQL

**DQL = Data Query Language**

Used to retrieve data.

Main command:

```text
SELECT
```

Example:

```sql
SELECT *
FROM employees;
```

Some SQL classifications consider `SELECT` part of DML rather than a separate DQL category. Both classifications are encountered.

---

# 41. DCL

**DCL = Data Control Language**

Used to control access and permissions.

Commands include:

```text
GRANT
REVOKE
```

Example:

```sql
GRANT SELECT
ON employees
TO analyst;
```

Exact syntax varies by DBMS.

---

# 42. TCL

**TCL = Transaction Control Language**

Used to manage transactions.

Commands include:

```text
COMMIT
ROLLBACK
SAVEPOINT
```

Example:

```sql
BEGIN;

UPDATE employees
SET salary = salary + 5000
WHERE employee_id = 1;

COMMIT;
```

Transaction syntax varies by DBMS.

---

# 43. Main SQL Command Categories — Summary

| Category | Meaning                      | Examples               |
| -------- | ---------------------------- | ---------------------- |
| DDL      | Data Definition Language     | CREATE, ALTER, DROP    |
| DML      | Data Manipulation Language   | INSERT, UPDATE, DELETE |
| DQL      | Data Query Language          | SELECT                 |
| DCL      | Data Control Language        | GRANT, REVOKE          |
| TCL      | Transaction Control Language | COMMIT, ROLLBACK       |

---

# 44. CREATE DATABASE

Creates a database.

Example:

```sql
CREATE DATABASE company;
```

Depending on the DBMS, selecting/connecting to the database is handled differently.

---

# 45. CREATE TABLE

Creates a table.

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);
```

Structure:

```text
CREATE TABLE table_name (
    column_name data_type,
    column_name data_type
);
```

---

# 46. Basic Table Structure

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    joining_date DATE
);
```

Conceptually:

```text
employees
│
├── employee_id → INT
├── name        → VARCHAR
├── department  → VARCHAR
├── salary      → DECIMAL
└── joining_date → DATE
```

---

# 47. Primary Key

A primary key uniquely identifies each row.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

A primary key:

* Must uniquely identify rows
* Cannot contain NULL
* Should be stable
* Can be one column
* Can be composite

---

# 48. Foreign Key

A foreign key creates a relationship between tables.

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Relationship:

```text
departments
department_id
      ↑
      │
      │ Foreign Key
      │
employees
department_id
```

---

# 49. Basic SQL CRUD

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

---

## Create

```sql
INSERT INTO employees
(employee_id, name, salary)
VALUES
(1, 'Rahul', 50000);
```

---

## Read

```sql
SELECT *
FROM employees;
```

---

## Update

```sql
UPDATE employees
SET salary = 55000
WHERE employee_id = 1;
```

---

## Delete

```sql
DELETE FROM employees
WHERE employee_id = 1;
```

---

# 50. SELECT Statement

The `SELECT` statement retrieves data.

Basic syntax:

```sql
SELECT column1, column2
FROM table_name;
```

Example:

```sql
SELECT name, salary
FROM employees;
```

---

# 51. SELECT *

`*` means all columns.

```sql
SELECT *
FROM employees;
```

This returns every column.

For production analytics queries, prefer selecting only required columns:

```sql
SELECT employee_id, name, salary
FROM employees;
```

This makes the query clearer and can reduce unnecessary data transfer.

---

# 52. DISTINCT

`DISTINCT` removes duplicate result values.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

Result:

```text
IT
HR
Finance
```

Without `DISTINCT`, repeated departments may appear.

---

# 53. Column Aliases

Aliases give temporary names to columns in query results.

```sql
SELECT
    name AS employee_name,
    salary AS monthly_salary
FROM employees;
```

Result:

```text
employee_name | monthly_salary
--------------+---------------
Rahul         | 50000
```

The alias does not normally rename the underlying table column.

---

# 54. Table Aliases

Table aliases make queries shorter and easier to read.

```sql
SELECT e.name, e.salary
FROM employees AS e;
```

You can then reference:

```text
e.name
e.salary
```

This becomes especially useful with joins.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
JOIN departments AS d
    ON e.department_id = d.department_id;
```

---

# 55. WHERE Clause

`WHERE` filters rows.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Only rows satisfying the condition are returned.

---

# 56. Comparison Operators

Common operators:

```text
=
<>
!=
>
<
>=
<=
```

Examples:

```sql
SELECT *
FROM employees
WHERE salary = 50000;
```

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

```sql
SELECT *
FROM employees
WHERE department <> 'HR';
```

---

# 57. Logical Operators

## AND

Both conditions must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

---

## OR

At least one condition must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

---

## NOT

Negates a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

---

# 58. BETWEEN

Used to check whether a value falls within a range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;
```

`BETWEEN` is generally inclusive of both boundaries.

Conceptually:

```text
40000 ≤ salary ≤ 70000
```

---

# 59. IN

Checks whether a value belongs to a list.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

Instead of:

```sql
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Finance'
```

---

# 60. LIKE

Used for pattern matching.

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

Meaning:

```text
Starts with R
```

Common wildcard:

```text
% → zero or more characters
_ → exactly one character
```

Examples:

```sql
-- Starts with A
WHERE name LIKE 'A%';

-- Ends with a
WHERE name LIKE '%a';

-- Contains 'an'
WHERE name LIKE '%an%';

-- Exactly four characters
WHERE name LIKE '____';
```

Pattern behavior can depend on collation and DBMS.

---

# 61. ORDER BY

Sorts query results.

Ascending:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Descending:

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

---

# 62. LIMIT / TOP / FETCH

Different database systems use different syntax to limit rows.

### MySQL / PostgreSQL

```sql
SELECT *
FROM employees
LIMIT 10;
```

### SQL Server

```sql
SELECT TOP 10 *
FROM employees;
```

### Standard-style FETCH

```sql
SELECT *
FROM employees
FETCH FIRST 10 ROWS ONLY;
```

Pagination often uses:

```sql
LIMIT 10 OFFSET 20;
```

But syntax differs between database systems.

---

# 63. INSERT

Insert one row:

```sql
INSERT INTO employees
(employee_id, name, department, salary)
VALUES
(1, 'Rahul', 'IT', 60000);
```

Multiple rows:

```sql
INSERT INTO employees
(employee_id, name, department, salary)
VALUES
(1, 'Rahul', 'IT', 60000),
(2, 'Priya', 'HR', 50000),
(3, 'Arun', 'Finance', 55000);
```

---

# 64. UPDATE

Used to modify existing data.

```sql
UPDATE employees
SET salary = 65000
WHERE employee_id = 1;
```

Multiple columns:

```sql
UPDATE employees
SET
    salary = 65000,
    department = 'Finance'
WHERE employee_id = 1;
```

### Important

Never forget the `WHERE` condition unless you intentionally want to update every row.

This:

```sql
UPDATE employees
SET salary = 65000;
```

updates all rows.

---

# 65. DELETE

Deletes rows.

```sql
DELETE FROM employees
WHERE employee_id = 1;
```

Without `WHERE`:

```sql
DELETE FROM employees;
```

all rows are deleted.

The table structure remains.

---

# 66. DELETE vs TRUNCATE vs DROP

| Command  |       Removes Rows | Removes Table | Structure Remains |
| -------- | -----------------: | ------------: | ----------------: |
| DELETE   |                Yes |            No |               Yes |
| TRUNCATE | Yes, generally all |            No |               Yes |
| DROP     |                Yes |           Yes |                No |

Important:

```sql
DELETE FROM employees;
```

removes rows.

```sql
TRUNCATE TABLE employees;
```

removes all rows using a table-level operation whose transactional behavior varies by DBMS.

```sql
DROP TABLE employees;
```

removes the table itself.

---

# 67. ALTER TABLE

Used to modify table structure.

Add column:

```sql
ALTER TABLE employees
ADD email VARCHAR(200);
```

Rename column syntax varies by DBMS.

Example in PostgreSQL:

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

Drop column:

```sql
ALTER TABLE employees
DROP COLUMN email;
```

---

# 68. DROP

Removes a database object.

Example:

```sql
DROP TABLE employees;
```

The table and its structure are removed.

Other examples:

```sql
DROP VIEW employee_view;
```

```sql
DROP INDEX idx_employee_name;
```

Exact syntax depends on DBMS.

---

# 69. TRUNCATE

Removes all rows from a table while keeping the table structure.

```sql
TRUNCATE TABLE employees;
```

Important:

* Usually much faster than deleting rows one at a time
* Cannot normally use a `WHERE` clause
* Transaction and rollback behavior varies by DBMS
* Trigger behavior can differ by DBMS

---

# 70. SQL Query Example

Suppose:

```text
employees

employee_id | name  | department | salary
------------+-------+------------+--------
1           | Rahul | IT         | 60000
2           | Priya | HR         | 45000
3           | Arun  | IT         | 70000
4           | Neha  | Finance    | 55000
```

Query:

```sql
SELECT name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Result:

```text
name  | salary
------+-------
Arun  | 70000
Rahul | 60000
```

---

# 71. SQL Expressions

An expression produces a value.

Example:

```sql
SELECT salary * 12 AS annual_salary
FROM employees;
```

Expression:

```text
salary * 12
```

Result:

```text
annual_salary
-------------
720000
540000
840000
...
```

Expressions can contain:

* Column values
* Constants
* Operators
* Functions
* CASE expressions

---

# 72. Arithmetic Operations

Example:

```sql
SELECT
    salary,
    salary * 12 AS annual_salary
FROM employees;
```

Common arithmetic operators:

```text
+
-
*
/
%
```

Exact behavior of division and modulo can vary by DBMS and data type.

---

# 73. SQL Functions

A function performs an operation and returns a value.

Examples:

```sql
SELECT UPPER(name)
FROM employees;
```

```sql
SELECT ROUND(salary, 0)
FROM employees;
```

```sql
SELECT COUNT(*)
FROM employees;
```

Major categories:

```text
SQL Functions
│
├── String Functions
├── Numeric Functions
├── Date/Time Functions
├── Aggregate Functions
├── NULL Functions
└── Conditional Functions
```

---

# 74. Aggregate Functions

Aggregate functions operate across multiple rows.

Common functions:

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

---

# 75. COUNT

Count rows:

```sql
SELECT COUNT(*)
FROM employees;
```

Count non-null values:

```sql
SELECT COUNT(email)
FROM employees;
```

Count unique values:

```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```

Important distinction:

```text
COUNT(*)              → counts rows
COUNT(column)         → counts non-NULL values
COUNT(DISTINCT col)   → counts distinct non-NULL values
```

---

# 76. GROUP BY

`GROUP BY` creates groups of rows for aggregation.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

Result:

```text
department | average_salary
-----------+---------------
IT         | 65000
HR         | 45000
Finance    | 55000
```

---

# 77. HAVING

`HAVING` filters groups after aggregation.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

# 78. WHERE vs HAVING

### WHERE

Filters rows **before grouping**.

```sql
SELECT department, AVG(salary)
FROM employees
WHERE salary > 40000
GROUP BY department;
```

### HAVING

Filters groups **after aggregation**.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

Think:

```text
WHERE  → rows
HAVING → groups
```

---

# 79. CASE Expression

`CASE` provides conditional logic.

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 70000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

Result:

```text
name  | salary | salary_category
------+--------+----------------
Rahul | 60000  | Medium
Arun  | 70000  | High
Priya | 45000  | Low
```

`CASE` is extremely important for data analytics.

---

# 80. Basic SQL JOIN Concept

A JOIN combines related data from multiple tables.

Example:

```text
employees

employee_id | name | department_id
------------+------+--------------
1           | Rahul| 10
2           | Priya| 20
```

```text
departments

department_id | department_name
--------------+----------------
10            | IT
20            | HR
```

Query:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Result:

```text
name  | department_name
------+----------------
Rahul | IT
Priya | HR
```

JOINs are one of the most important SQL concepts for both coding and analytics.

---

# 81. SQL Query Structure

A basic query:

```sql
SELECT column1, column2
FROM table_name
WHERE condition
GROUP BY column1, column2
HAVING aggregate_condition
ORDER BY column1
LIMIT 10;
```

Not every clause is required.

---

# 82. Logical Query Processing Order

Although we write:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

the database logically processes a query approximately in this order:

```text
1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. DISTINCT
8. ORDER BY
9. LIMIT / OFFSET
```

Example:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC;
```

Conceptual processing:

```text
FROM
 ↓
JOIN
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
LIMIT
```

This order is essential for understanding advanced SQL.

---

# 83. Physical Execution vs Logical Processing

The logical query processing order describes **how SQL semantics are understood**.

The database does not necessarily execute the query physically in exactly that order.

The query optimizer may:

* Reorder operations
* Use indexes
* Filter early
* Choose different join algorithms
* Change execution strategies

Therefore:

```text
Logical Query Order
        ↓
Query Optimizer
        ↓
Physical Execution Plan
        ↓
Result
```

---

# 84. SQL Dialects

SQL has standards, but database systems implement their own dialects.

Major systems include:

```text
MySQL
PostgreSQL
SQL Server
Oracle
SQLite
MariaDB
```

They share core SQL concepts but differ in:

* Functions
* Data types
* Date syntax
* String functions
* Pagination
* Stored procedures
* JSON support
* Administrative commands
* Advanced features

---

# 85. SQL vs MySQL

This is a very important distinction.

### SQL

A language used to interact with relational databases.

### MySQL

A database management system that implements SQL.

Think:

```text
SQL
 ↓
Language
```

```text
MySQL
 ↓
Database Management System
```

Similarly:

```text
SQL
├── MySQL
├── PostgreSQL
├── SQL Server
├── Oracle
└── SQLite
```

Each provides its own SQL dialect.

---

# 86. SQL vs NoSQL

### SQL Databases

Usually relational.

Data is commonly organized into:

```text
Tables
Rows
Columns
Relationships
```

Examples:

```text
MySQL
PostgreSQL
SQL Server
Oracle
```

### NoSQL

A broad category of non-relational database systems.

Examples include:

```text
MongoDB
Redis
Cassandra
DynamoDB
```

SQL databases are often preferred when:

* Relationships are important
* Structured data is dominant
* Complex queries are needed
* Strong transactional consistency is required

NoSQL systems may be preferred for particular use cases involving:

* Flexible schemas
* High-scale distributed workloads
* Specialized data models

The choice depends on the application.

---

# 87. SQL in Data Analytics

SQL is a core tool for data analysts.

A typical analytics workflow:

```text
Raw Database
     ↓
SQL
     ↓
Data Extraction
     ↓
Data Cleaning
     ↓
Data Transformation
     ↓
Aggregation
     ↓
Analysis
     ↓
Dashboard / Report
```

Example business question:

> Which product category generated the highest revenue?

SQL can answer it:

```sql
SELECT
    category,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY category
ORDER BY revenue DESC;
```

---

# 88. SQL for Data Cleaning

SQL can help identify:

### Missing values

```sql
SELECT *
FROM customers
WHERE email IS NULL;
```

### Duplicate values

```sql
SELECT
    email,
    COUNT(*) AS count
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

### Standardization

```sql
SELECT LOWER(TRIM(name))
FROM customers;
```

### Invalid values

```sql
SELECT *
FROM employees
WHERE salary < 0;
```

---

# 89. SQL for Data Manipulation

SQL can transform data using:

* CASE
* Functions
* JOINs
* Aggregations
* CTEs
* Subqueries
* Window functions

Example:

```sql
SELECT
    product,
    quantity,
    price,
    quantity * price AS revenue
FROM sales;
```

---

# 90. SQL for Business Questions

A data analyst might receive:

> How much revenue did we generate last month?

The analyst translates the question into SQL.

Example:

```sql
SELECT
    SUM(amount) AS total_revenue
FROM orders
WHERE order_date >= '2026-07-01'
  AND order_date < '2026-08-01';
```

Another question:

> Which customers have never placed an order?

This requires understanding table relationships and joins.

SQL is therefore not just about syntax.

It is about **translating business questions into data queries**.

---

# 91. SQL Best Practices

## Use meaningful names

Good:

```sql
customer_id
order_date
total_revenue
```

Avoid:

```sql
x
abc
data1
```

---

## Avoid unnecessary SELECT *

Instead of:

```sql
SELECT *
FROM employees;
```

Prefer:

```sql
SELECT
    employee_id,
    name,
    salary
FROM employees;
```

---

## Use aliases

```sql
SELECT
    e.name,
    d.department_name
FROM employees AS e
JOIN departments AS d
    ON e.department_id = d.department_id;
```

---

## Format SQL

Bad:

```sql
select name,salary from employees where salary>50000 order by salary desc;
```

Better:

```sql
SELECT
    name,
    salary
FROM employees
WHERE salary > 50000
ORDER BY salary DESC;
```

---

## Be careful with UPDATE

Always check:

```sql
UPDATE employees
SET salary = 70000
WHERE employee_id = 10;
```

before executing.

---

## Be careful with DELETE

Use:

```sql
DELETE FROM employees
WHERE employee_id = 10;
```

rather than accidentally deleting every row.

---

# 92. Common Beginner Mistakes

### Mistake 1 — Using `=` with NULL

Wrong:

```sql
WHERE email = NULL;
```

Correct:

```sql
WHERE email IS NULL;
```

---

### Mistake 2 — Forgetting WHERE in UPDATE

Dangerous:

```sql
UPDATE employees
SET salary = 50000;
```

This updates every row.

---

### Mistake 3 — Forgetting WHERE in DELETE

Dangerous:

```sql
DELETE FROM employees;
```

This deletes every row.

---

### Mistake 4 — Using WHERE for aggregate filtering

Incorrect:

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
WHERE AVG(salary) > 50000;
```

Correct:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

### Mistake 5 — Confusing SQL and MySQL

Remember:

```text
SQL    → Language
MySQL  → Database System
```

---

# 93. Fundamental SQL Mental Model

When solving a SQL problem, think in this sequence:

```text
1. What data do I need?
        ↓
2. Which table contains it?
        ↓
3. Do I need other tables?
        ↓
4. How are the tables related?
        ↓
5. Which rows should I filter?
        ↓
6. Do I need calculated columns?
        ↓
7. Do I need grouping?
        ↓
8. Do I need aggregate functions?
        ↓
9. Do I need to filter groups?
        ↓
10. How should the result be sorted?
        ↓
11. Do I need to limit the result?
```

This thinking process becomes extremely important in analytics.

---

# 94. Fundamental SQL Query Template

```sql
SELECT
    column1,
    column2,
    aggregate_function(column3) AS calculated_value
FROM table1
JOIN table2
    ON table1.key = table2.key
WHERE condition
GROUP BY
    column1,
    column2
HAVING aggregate_condition
ORDER BY calculated_value DESC
LIMIT 10;
```

You will gradually learn when each part is necessary.

---

# 95. SQL Fundamentals — Key Concepts to Remember

```text
SQL
│
├── Database
│
├── Schema
│
├── Table
│   ├── Rows
│   └── Columns
│
├── Data Types
│
├── Keys
│   ├── Primary Key
│   └── Foreign Key
│
├── Constraints
│
├── CRUD
│   ├── INSERT
│   ├── SELECT
│   ├── UPDATE
│   └── DELETE
│
├── Filtering
│   ├── WHERE
│   ├── IN
│   ├── BETWEEN
│   └── LIKE
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
├── GROUP BY
│
├── HAVING
│
├── CASE
│
└── JOIN
```

---

# 96. SQL Fundamentals Revision Checklist

## Database Concepts

* [ ] SQL
* [ ] Database
* [ ] DBMS
* [ ] RDBMS
* [ ] Schema
* [ ] Table
* [ ] Row
* [ ] Column
* [ ] Record
* [ ] Attribute
* [ ] Entity
* [ ] Relationship

## SQL Syntax

* [ ] SQL Statement
* [ ] SQL Clause
* [ ] SQL Keyword
* [ ] Identifier
* [ ] Comment
* [ ] String
* [ ] Numeric Value
* [ ] Date
* [ ] NULL

## SQL Commands

* [ ] CREATE
* [ ] ALTER
* [ ] DROP
* [ ] TRUNCATE
* [ ] INSERT
* [ ] SELECT
* [ ] UPDATE
* [ ] DELETE
* [ ] GRANT
* [ ] REVOKE
* [ ] COMMIT
* [ ] ROLLBACK

## Querying

* [ ] SELECT
* [ ] DISTINCT
* [ ] WHERE
* [ ] AND
* [ ] OR
* [ ] NOT
* [ ] IN
* [ ] BETWEEN
* [ ] LIKE
* [ ] ORDER BY
* [ ] LIMIT / FETCH / TOP

## Aggregation

* [ ] COUNT
* [ ] SUM
* [ ] AVG
* [ ] MIN
* [ ] MAX
* [ ] GROUP BY
* [ ] HAVING

## Core Advanced Foundation

* [ ] CASE
* [ ] JOIN
* [ ] Primary Key
* [ ] Foreign Key
* [ ] Relationships
* [ ] NULL Handling
* [ ] Logical Query Processing Order
* [ ] SQL Dialects

## Analytics Foundation

* [ ] Filtering
* [ ] Data Cleaning
* [ ] Data Transformation
* [ ] Aggregation
* [ ] Business Metrics
* [ ] Revenue Analysis
* [ ] Customer Analysis
* [ ] Time-Based Analysis

---

# 97. What to Learn Next

After completing SQL Fundamentals, continue in this order:

```text
SQL Fundamentals
       ↓
Data Types & Constraints
       ↓
SELECT & Filtering
       ↓
Functions
       ↓
GROUP BY & Aggregation
       ↓
CASE & NULL Handling
       ↓
JOINS
       ↓
Subqueries
       ↓
CTEs
       ↓
Window Functions
       ↓
Advanced SQL
       ↓
SQL Data Cleaning
       ↓
SQL Data Manipulation
       ↓
SQL Data Analysis
       ↓
Time-Series Analysis
       ↓
Cohort & Retention Analysis
       ↓
Advanced Analytics
       ↓
SQL Interview Problems
       ↓
Real-World SQL Projects
```

---

# 98. Final Takeaway

SQL fundamentals are not just about memorizing commands.

You should understand the relationship between:

```text
Database
   ↓
Tables
   ↓
Rows + Columns
   ↓
Keys + Relationships
   ↓
SQL Queries
   ↓
Filtering
   ↓
Transformation
   ↓
Aggregation
   ↓
Analysis
```

For **SQL coding**, focus strongly on:

```text
DDL
DML
SELECT
JOINs
Subqueries
CTEs
Functions
Transactions
Indexes
Procedures
Triggers
Optimization
```

For **Data Analytics**, focus especially on:

```text
SELECT
WHERE
GROUP BY
HAVING
CASE
JOINs
Aggregations
Date Functions
Window Functions
CTEs
Data Cleaning
Data Transformation
Time-Series Analysis
Cohort Analysis
Retention
Funnel Analysis
Business Metrics
```

Once these fundamentals are strong, advanced SQL becomes much easier to understand.
