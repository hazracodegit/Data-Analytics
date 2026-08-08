# SQL Database & Table Operations

This chapter covers the basic SQL operations required to start working with databases and tables:

```text
1. Create Database
2. Select Database
3. Create Table
4. View Table Structure
5. ALTER TABLE
6. INSERT Data
7. UPDATE Data
8. Filtering Data
9. Operators used for Filtering
10. NULL Handling
11. Practical Examples
12. Revision Summary
```

---

# 1. Creating a Database

A database is a container that stores related database objects such as:

```text
Tables
Views
Indexes
Stored Procedures
Functions
Triggers
```

The exact objects supported depend on the DBMS.

## Syntax

```sql
CREATE DATABASE database_name;
```

## Example

```sql
CREATE DATABASE company;
```

---

# 2. Viewing Databases

The command depends on the database system.

### MySQL

```sql
SHOW DATABASES;
```

PostgreSQL, SQL Server, and Oracle use different commands/tools for listing databases.

---

# 3. Selecting a Database

In MySQL:

```sql
USE company;
```

This tells MySQL that subsequent unqualified table operations should use the `company` database.

> PostgreSQL and other DBMSs use different mechanisms for connecting/selecting a database.

---

# 4. Creating a Table

A table stores data in:

```text
Rows + Columns
```

Example:

```text
employees

employee_id | name   | age | salary
------------+--------+-----+--------
1           | Rahul  | 25  | 50000
2           | Priya  | 28  | 60000
3           | Arun   | 30  | 70000
```

---

# 5. CREATE TABLE Syntax

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

---

# 6. Creating an Employee Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    salary DECIMAL(10,2),
    department VARCHAR(50)
);
```

The table contains:

```text
employee_id → INT + PRIMARY KEY
name        → VARCHAR + NOT NULL
age         → INT
salary      → DECIMAL
department  → VARCHAR
```

---

# 7. Creating a Table with More Constraints

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary >= 0),
    department VARCHAR(50),
    status VARCHAR(20) DEFAULT 'Active'
);
```

Here:

```text
PRIMARY KEY → Unique row identification
NOT NULL    → Value is required
UNIQUE      → Duplicate values are restricted
CHECK       → Values must satisfy a condition
DEFAULT     → Supplies a value when omitted
```

---

# 8. Viewing Table Structure

### MySQL

```sql
DESCRIBE employees;
```

or:

```sql
DESC employees;
```

This shows information such as:

```text
Column
Data Type
NULL/NOT NULL
Key
Default
Extra
```

---

# 9. Viewing Table Data

```sql
SELECT *
FROM employees;
```

`*` means all selected columns.

---

# 10. ALTER TABLE

`ALTER TABLE` is used to modify the structure of an existing table.

Common operations:

```text
ADD COLUMN
DROP COLUMN
RENAME COLUMN
ALTER/MODIFY COLUMN
ADD CONSTRAINT
DROP CONSTRAINT
```

Exact syntax varies between database systems.

---

# 11. ADD COLUMN

Add a new column:

```sql
ALTER TABLE employees
ADD email VARCHAR(255);
```

Now the table has an additional column:

```text
employee_id
name
age
salary
department
email
```

---

# 12. ADD Multiple Columns

Some DBMSs support adding multiple columns in one statement.

Example:

```sql
ALTER TABLE employees
ADD phone VARCHAR(20),
ADD city VARCHAR(50);
```

Syntax may differ between DBMSs.

---

# 13. RENAME COLUMN

Rename a column:

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

Before:

```text
name
```

After:

```text
employee_name
```

---

# 14. MODIFY / ALTER COLUMN

The syntax varies significantly by DBMS.

### MySQL

```sql
ALTER TABLE employees
MODIFY salary DECIMAL(12,2);
```

### PostgreSQL

```sql
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(12,2);
```

The concept is the same:

```text
Change the definition of an existing column
```

---

# 15. DROP COLUMN

Remove a column:

```sql
ALTER TABLE employees
DROP COLUMN phone;
```

The column and its stored values are removed.

Be careful when dropping columns because existing applications/queries may depend on them.

---

# 16. Adding a Constraint

Example:

```sql
ALTER TABLE employees
ADD CONSTRAINT chk_salary
CHECK (salary >= 0);
```

This adds a validation rule to the table.

---

# 17. Adding a Foreign Key

Suppose we have:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

We can add a foreign key to `employees`:

```sql
ALTER TABLE employees
ADD CONSTRAINT fk_department
FOREIGN KEY (department_id)
REFERENCES departments(department_id);
```

---

# 18. INSERT Statement

`INSERT` is used to add rows to a table.

Basic syntax:

```sql
INSERT INTO table_name
(column1, column2, column3)
VALUES
(value1, value2, value3);
```

---

# 19. Insert One Row

```sql
INSERT INTO employees
(employee_id, name, age, salary, department)
VALUES
(1, 'Rahul', 25, 50000, 'IT');
```

---

# 20. Insert Multiple Rows

```sql
INSERT INTO employees
(employee_id, name, age, salary, department)
VALUES
(2, 'Priya', 28, 60000, 'HR'),
(3, 'Arun', 30, 70000, 'IT'),
(4, 'Anita', 26, 55000, 'Finance'),
(5, 'Kiran', 32, 80000, 'IT');
```

---

# 21. Insert Data into Selected Columns

You do not always need to provide every column.

```sql
INSERT INTO employees
(employee_id, name, age)
VALUES
(6, 'Vijay', 27);
```

Columns not supplied may receive:

```text
NULL
```

or their defined `DEFAULT` value, depending on the column definition.

---

# 22. INSERT with DEFAULT

Suppose:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100),
    status VARCHAR(20) DEFAULT 'Active'
);
```

Then:

```sql
INSERT INTO users
(user_id, name)
VALUES
(1, 'Rahul');
```

The database can use:

```text
status = 'Active'
```

---

# 23. INSERT Using SELECT

You can insert the result of a query into another table.

```sql
INSERT INTO high_salary_employees
(employee_id, name, salary)
SELECT employee_id, name, salary
FROM employees
WHERE salary > 60000;
```

This is useful for:

```text
Data migration
Data transformation
Creating summary/staging tables
```

---

# 24. UPDATE Statement

`UPDATE` modifies existing rows.

Syntax:

```sql
UPDATE table_name
SET column1 = value1
WHERE condition;
```

---

# 25. Update One Row

```sql
UPDATE employees
SET salary = 55000
WHERE employee_id = 1;
```

Only employee `1` is targeted.

---

# 26. Update Multiple Columns

```sql
UPDATE employees
SET
    salary = 65000,
    department = 'Finance'
WHERE employee_id = 2;
```

---

# 27. Update Multiple Rows

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

Every employee in the IT department receives the increase.

---

# 28. UPDATE Without WHERE

This is extremely important.

```sql
UPDATE employees
SET salary = 50000;
```

This can update **every row** in the table.

Before executing an important update, first test the condition:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Then perform:

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

---

# 29. Filtering Data

Filtering means selecting only rows that satisfy a condition.

The primary SQL clause used for filtering is:

```sql
WHERE
```

Basic syntax:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

---

# 30. Simple Filtering

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

Returns employees whose salary is greater than `60000`.

---

# 31. Equality Operator

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

`=` checks equality.

---

# 32. Not Equal

Common SQL forms:

```sql
SELECT *
FROM employees
WHERE department <> 'IT';
```

Some DBMSs also support:

```sql
SELECT *
FROM employees
WHERE department != 'IT';
```

`<>` is the standard SQL not-equal operator.

---

# 33. Comparison Operators

SQL commonly provides:

```text
=       Equal
<>      Not equal
!=      Not equal in many DBMSs
>       Greater than
<       Less than
>=      Greater than or equal
<=      Less than or equal
```

Example:

```sql
SELECT *
FROM employees
WHERE age >= 25;
```

---

# 34. AND Operator

`AND` requires all conditions to be true.

```sql
SELECT *
FROM employees
WHERE age >= 25
AND salary > 50000;
```

Meaning:

```text
age >= 25
       AND
salary > 50000
```

Both conditions must be satisfied.

---

# 35. OR Operator

`OR` requires at least one condition to be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

---

# 36. NOT Operator

`NOT` reverses a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

Equivalent in many cases to:

```sql
SELECT *
FROM employees
WHERE department <> 'IT';
```

---

# 37. Combining AND and OR

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

Parentheses make the intended logic explicit.

---

# 38. BETWEEN

`BETWEEN` checks whether a value falls within an inclusive range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 70000;
```

Conceptually:

```text
50000 <= salary <= 70000
```

The endpoints are included.

---

# 39. NOT BETWEEN

```sql
SELECT *
FROM employees
WHERE salary NOT BETWEEN 50000 AND 70000;
```

---

# 40. IN Operator

`IN` checks whether a value matches one of several values.

Instead of:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Finance';
```

Use:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

This is cleaner and easier to maintain.

---

# 41. NOT IN

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

### Important NULL Note

`NOT IN` can produce unexpected results when the compared expression or list involves `NULL`. For robust SQL, understand SQL's three-valued logic before using `NOT IN` with nullable data.

---

# 42. LIKE Operator

`LIKE` is used for pattern matching.

Two important wildcards:

```text
% → Zero or more characters
_ → Exactly one character
```

---

# 43. LIKE — Starts With

Find names beginning with `A`:

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Matches examples such as:

```text
Arun
Anita
Amit
```

---

# 44. LIKE — Ends With

```sql
SELECT *
FROM employees
WHERE name LIKE '%a';
```

Matches names ending in `a`, subject to the database's collation/case-sensitivity rules.

---

# 45. LIKE — Contains

```sql
SELECT *
FROM employees
WHERE name LIKE '%it%';
```

Finds names containing `it`.

---

# 46. LIKE — Single Character

`_` represents one character.

```sql
SELECT *
FROM employees
WHERE name LIKE 'A_i%';
```

Pattern:

```text
A
↓
one character
↓
i
↓
anything
```

---

# 47. IS NULL

`NULL` does not mean:

```text
0
''
FALSE
```

It represents a missing, unknown, or not-applicable value depending on context.

You should use:

```sql
IS NULL
```

to test for NULL.

Example:

```sql
SELECT *
FROM employees
WHERE department IS NULL;
```

---

# 48. IS NOT NULL

```sql
SELECT *
FROM employees
WHERE department IS NOT NULL;
```

Returns rows where `department` is not NULL.

---

# 49. Do NOT Use `= NULL`

Incorrect:

```sql
SELECT *
FROM employees
WHERE department = NULL;
```

Correct:

```sql
SELECT *
FROM employees
WHERE department IS NULL;
```

---

# 50. Filtering Dates

Example:

```sql
SELECT *
FROM employees
WHERE joining_date >= '2025-01-01';
```

Date syntax and literal handling can vary between DBMSs.

---

# 51. Filtering by Date Range

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

This avoids accidentally excluding times on the last day.

---

# 52. Filtering Numeric Data

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Other examples:

```sql
SELECT *
FROM employees
WHERE age <= 30;
```

```sql
SELECT *
FROM employees
WHERE salary >= 50000
AND salary <= 80000;
```

Or:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

---

# 53. Filtering Text Data

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Multiple values:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

Pattern:

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

---

# 54. DISTINCT

`DISTINCT` removes duplicate result values.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

If the table contains:

```text
IT
IT
HR
Finance
Finance
```

Result:

```text
IT
HR
Finance
```

---

# 55. ORDER BY

Filtering answers:

```text
Which rows do I want?
```

`ORDER BY` answers:

```text
In what order should I display them?
```

Example:

```sql
SELECT *
FROM employees
ORDER BY salary;
```

Descending:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Ascending:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

`ASC` is commonly the default.

---

# 56. LIMIT

Some DBMSs support `LIMIT` to restrict the number of returned rows.

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

This returns the top 5 rows according to the specified ordering.

> SQL Server commonly uses `TOP` or `OFFSET ... FETCH`, while standard/DBMS-specific alternatives vary.

---

# 57. Filtering + Sorting

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000
ORDER BY salary DESC;
```

Process conceptually:

```text
employees
    ↓
WHERE salary > 50000
    ↓
remaining rows
    ↓
ORDER BY salary DESC
    ↓
final result
```

---

# 58. Filtering + Selecting Specific Columns

```sql
SELECT
    name,
    department,
    salary
FROM employees
WHERE salary >= 60000;
```

This is usually preferable to `SELECT *` when you only need specific columns.

---

# 59. UPDATE with Filtering

Filtering is not only for `SELECT`.

It is extremely important for `UPDATE`.

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'IT';
```

Only IT employees are affected.

---

# 60. DELETE with Filtering

Filtering also applies to `DELETE`.

```sql
DELETE FROM employees
WHERE employee_id = 10;
```

Only the matching row is targeted.

---

# 61. Safe UPDATE Workflow

Before:

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

First check:

```sql
SELECT employee_id, name, salary
FROM employees
WHERE department = 'IT';
```

Then execute:

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department = 'IT';
```

This is a good practical habit.

---

# 62. Safe DELETE Workflow

Before:

```sql
DELETE FROM employees
WHERE department = 'IT';
```

First check:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Then delete:

```sql
DELETE FROM employees
WHERE department = 'IT';
```

---

# 63. Complete Practical Example

## Step 1 — Create Database

```sql
CREATE DATABASE company;
```

---

## Step 2 — Select Database

MySQL:

```sql
USE company;
```

---

## Step 3 — Create Department Table

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);
```

---

## Step 4 — Create Employee Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    salary DECIMAL(10,2),
    department_id INT,
    status VARCHAR(20) DEFAULT 'Active',

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

## Step 5 — Insert Departments

```sql
INSERT INTO departments
(department_id, department_name)
VALUES
(1, 'IT'),
(2, 'HR'),
(3, 'Finance');
```

---

## Step 6 — Insert Employees

```sql
INSERT INTO employees
(employee_id, name, age, salary, department_id)
VALUES
(101, 'Rahul', 25, 50000, 1),
(102, 'Priya', 28, 65000, 2),
(103, 'Arun', 30, 75000, 1),
(104, 'Anita', 26, 55000, 3),
(105, 'Kiran', 32, 90000, 1);
```

---

# 64. Retrieve All Employees

```sql
SELECT *
FROM employees;
```

---

# 65. Retrieve Selected Columns

```sql
SELECT
    name,
    age,
    salary
FROM employees;
```

---

# 66. Employees with Salary Greater Than 60000

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

---

# 67. Employees Between 50000 and 80000

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

---

# 68. Employees from IT or HR

```sql
SELECT *
FROM employees
WHERE department_id IN (1, 2);
```

---

# 69. Employees Whose Names Start with A

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

# 70. Employees Older Than 25 with Salary Above 60000

```sql
SELECT *
FROM employees
WHERE age > 25
AND salary > 60000;
```

---

# 71. Employees Who Are Not in IT

```sql
SELECT *
FROM employees
WHERE department_id <> 1;
```

---

# 72. Sort Employees by Salary

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# 73. Find Highest Paid Employees

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

With a DBMS supporting `LIMIT`:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

---

# 74. Update an Employee Salary

```sql
UPDATE employees
SET salary = 70000
WHERE employee_id = 101;
```

---

# 75. Give IT Employees a Raise

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 1;
```

---

# 76. Add a New Column

```sql
ALTER TABLE employees
ADD email VARCHAR(255);
```

---

# 77. Update the New Column

```sql
UPDATE employees
SET email = 'rahul@example.com'
WHERE employee_id = 101;
```

---

# 78. Filtering Operators — Quick Reference

| Operator      | Meaning          | Example                       |
| ------------- | ---------------- | ----------------------------- |
| `=`           | Equal            | `salary = 50000`              |
| `<>`          | Not equal        | `salary <> 50000`             |
| `!=`          | Not equal        | `salary != 50000`             |
| `>`           | Greater than     | `salary > 50000`              |
| `<`           | Less than        | `salary < 50000`              |
| `>=`          | Greater/equal    | `salary >= 50000`             |
| `<=`          | Less/equal       | `salary <= 50000`             |
| `AND`         | Both conditions  | `age > 20 AND salary > 50000` |
| `OR`          | Either condition | `dept = 'IT' OR dept = 'HR'`  |
| `NOT`         | Negation         | `NOT dept = 'IT'`             |
| `BETWEEN`     | Range            | `salary BETWEEN 50K AND 80K`  |
| `IN`          | Match list       | `dept IN ('IT','HR')`         |
| `LIKE`        | Pattern matching | `name LIKE 'A%'`              |
| `IS NULL`     | Check NULL       | `email IS NULL`               |
| `IS NOT NULL` | Not NULL         | `email IS NOT NULL`           |

---

# 79. LIKE Wildcards

```text
%  → Zero or more characters
_  → Exactly one character
```

Examples:

```sql
-- Starts with A
WHERE name LIKE 'A%'

-- Ends with a
WHERE name LIKE '%a'

-- Contains "an"
WHERE name LIKE '%an%'

-- A followed by exactly one character and then n
WHERE name LIKE 'A_n%'
```

Case sensitivity depends on the database and collation/settings.

---

# 80. SQL Command Flow

A typical workflow is:

```text
CREATE DATABASE
      ↓
SELECT / CONNECT TO DATABASE
      ↓
CREATE TABLE
      ↓
ALTER TABLE
      ↓
INSERT DATA
      ↓
SELECT DATA
      ↓
WHERE → FILTER
      ↓
UPDATE DATA
      ↓
SELECT AGAIN TO VERIFY
```

---

# 81. Important SQL Concepts to Remember

```text
CREATE DATABASE
→ Creates the database

CREATE TABLE
→ Creates table structure

ALTER TABLE
→ Changes existing structure

INSERT
→ Adds new rows

SELECT
→ Retrieves rows

WHERE
→ Filters rows

UPDATE
→ Modifies existing rows

DELETE
→ Removes rows

ORDER BY
→ Sorts result

DISTINCT
→ Removes duplicate result values

LIKE
→ Pattern matching

IN
→ Matches against a list

BETWEEN
→ Range filtering

IS NULL
→ Checks missing/NULL values
```

---

# 82. Final Revision Cheat Sheet

```sql
-- DATABASE
CREATE DATABASE company;

-- SELECT DATABASE (MySQL)
USE company;

-- TABLE
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);

-- ALTER
ALTER TABLE employees
ADD email VARCHAR(255);

-- INSERT
INSERT INTO employees
(employee_id, name, salary)
VALUES
(1, 'Rahul', 50000);

-- SELECT
SELECT *
FROM employees;

-- FILTER
SELECT *
FROM employees
WHERE salary > 40000;

-- UPDATE
UPDATE employees
SET salary = 55000
WHERE employee_id = 1;

-- SORT
SELECT *
FROM employees
ORDER BY salary DESC;

-- DISTINCT
SELECT DISTINCT name
FROM employees;

-- IN
SELECT *
FROM employees
WHERE name IN ('Rahul', 'Priya');

-- BETWEEN
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;

-- LIKE
SELECT *
FROM employees
WHERE name LIKE 'R%';

-- NULL
SELECT *
FROM employees
WHERE email IS NULL;
```

---

# 83. One-Page Mental Model

```text
DATABASE
   │
   └── TABLE
        │
        ├── CREATE
        │
        ├── ALTER
        │
        ├── INSERT
        │      ↓
        │    ADD ROWS
        │
        ├── SELECT
        │      ↓
        │    READ DATA
        │      ↓
        │    WHERE
        │      ↓
        │    FILTER
        │      ↓
        │    ORDER BY
        │      ↓
        │    SORT
        │
        └── UPDATE
               ↓
             MODIFY
             ROWS
```

## Golden Rule for Practice

Before running an `UPDATE` or `DELETE` with a condition, run the corresponding `SELECT` first:

```sql
SELECT *
FROM employees
WHERE <your_condition>;
```

Then, if the returned rows are exactly what you intend to modify:

```sql
UPDATE employees
SET ...
WHERE <your_condition>;
```

This habit prevents many accidental data changes.
