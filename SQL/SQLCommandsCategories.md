# SQL Command Categories

SQL commands are commonly divided into **5 major categories**:

```text
SQL Commands
│
├── DDL → Data Definition Language
├── DML → Data Manipulation Language
├── DQL → Data Query Language
├── DCL → Data Control Language
└── TCL → Transaction Control Language
```

---

# 1. DDL — Data Definition Language

**DDL** is used to define and modify the **structure/schema** of database objects such as:

* Databases
* Tables
* Views
* Indexes
* Schemas

### Main DDL Commands

```text
CREATE
ALTER
DROP
TRUNCATE
RENAME
```

---

## 1.1 CREATE

Used to create database objects.

### Create Database

```sql
CREATE DATABASE company;
```

### Create Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

## 1.2 ALTER

Used to modify an existing database object.

### Add Column

```sql
ALTER TABLE employees
ADD email VARCHAR(255);
```

### Modify/Change Column

Syntax varies by DBMS.

For example, in MySQL:

```sql
ALTER TABLE employees
MODIFY salary DECIMAL(12,2);
```

### Rename Column

MySQL/PostgreSQL-style syntax:

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

### Drop Column

```sql
ALTER TABLE employees
DROP COLUMN email;
```

---

## 1.3 DROP

Deletes a database object and its definition.

```sql
DROP TABLE employees;
```

The table itself is removed.

Be careful:

```text
DROP TABLE
    ↓
Table structure removed
    ↓
Data removed
```

---

## 1.4 TRUNCATE

Removes all rows from a table while keeping the table structure.

```sql
TRUNCATE TABLE employees;
```

After:

```text
Table exists
Columns exist
Constraints/indexes behavior depends on DBMS
Rows removed
```

### DELETE vs TRUNCATE

```text
DELETE
→ Removes rows
→ Can use WHERE
→ DML command
→ Transaction behavior depends on DBMS

TRUNCATE
→ Removes all rows
→ Cannot use WHERE
→ DDL in many DBMS classifications
→ Faster for clearing an entire table in many systems
```

---

## 1.5 RENAME

Changes the name of a database object.

Example:

```sql
ALTER TABLE employees
RENAME TO staff;
```

Exact syntax varies by DBMS.

---

# 2. DML — Data Manipulation Language

**DML** is used to manipulate the data stored inside tables.

Main commands:

```text
INSERT
UPDATE
DELETE
```

---

# 2.1 INSERT

Adds new rows.

```sql
INSERT INTO employees
(employee_id, name, salary)
VALUES
(1, 'Rahul', 50000);
```

Insert multiple rows:

```sql
INSERT INTO employees
(employee_id, name, salary)
VALUES
(2, 'Priya', 60000),
(3, 'Arun', 55000),
(4, 'Anita', 70000);
```

---

# 2.2 UPDATE

Modifies existing rows.

```sql
UPDATE employees
SET salary = 65000
WHERE employee_id = 2;
```

Multiple columns:

```sql
UPDATE employees
SET
    name = 'Priya Sharma',
    salary = 70000
WHERE employee_id = 2;
```

### Important

Never casually run:

```sql
UPDATE employees
SET salary = 70000;
```

Without a `WHERE` clause, it can update **every row**.

---

# 2.3 DELETE

Deletes rows from a table.

```sql
DELETE FROM employees
WHERE employee_id = 4;
```

Delete all rows:

```sql
DELETE FROM employees;
```

The table structure remains.

---

# 3. DQL — Data Query Language

**DQL** is commonly used to describe commands that retrieve/query data.

The primary command is:

```text
SELECT
```

---

# 3.1 SELECT

Retrieves data from one or more tables.

```sql
SELECT *
FROM employees;
```

Select specific columns:

```sql
SELECT name, salary
FROM employees;
```

---

# 3.2 SELECT with WHERE

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

# 3.3 SELECT with ORDER BY

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# 3.4 SELECT with GROUP BY

```sql
SELECT department_id, COUNT(*)
FROM employees
GROUP BY department_id;
```

---

# 3.5 SELECT with HAVING

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

---

# 3.6 SELECT with JOIN

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 4. DCL — Data Control Language

**DCL** manages permissions and access to database objects.

Main commands:

```text
GRANT
REVOKE
```

---

# 4.1 GRANT

Gives privileges to a user or role.

Example:

```sql
GRANT SELECT
ON employees
TO analyst;
```

Multiple privileges:

```sql
GRANT SELECT, INSERT, UPDATE
ON employees
TO analyst;
```

---

# 4.2 REVOKE

Removes previously granted privileges.

```sql
REVOKE INSERT
ON employees
FROM analyst;
```

---

# 5. TCL — Transaction Control Language

**TCL** manages transactions.

Main commands:

```text
COMMIT
ROLLBACK
SAVEPOINT
```

Some DBMSs also provide transaction-related commands such as `START TRANSACTION`.

---

# 5.1 COMMIT

Permanently commits changes made in the current transaction, subject to the DBMS transaction model.

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department_id = 10;

COMMIT;
```

---

# 5.2 ROLLBACK

Undoes uncommitted transaction changes.

```sql
UPDATE employees
SET salary = salary + 5000
WHERE department_id = 10;

ROLLBACK;
```

The update is rolled back if it has not already been committed.

---

# 5.3 SAVEPOINT

Creates a point inside a transaction to which you can roll back.

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 5000
WHERE department_id = 10;

SAVEPOINT salary_update;

UPDATE employees
SET salary = salary + 10000
WHERE department_id = 20;

ROLLBACK TO SAVEPOINT salary_update;

COMMIT;
```

Conceptually:

```text
START TRANSACTION
       ↓
UPDATE department 10
       ↓
SAVEPOINT
       ↓
UPDATE department 20
       ↓
ROLLBACK TO SAVEPOINT
       ↓
Only changes after SAVEPOINT are undone
       ↓
COMMIT
```

Exact syntax and behavior can vary by DBMS.

---

# 6. Complete SQL Command Classification

| Category | Full Form                    | Main Commands                         | Purpose                 |
| -------- | ---------------------------- | ------------------------------------- | ----------------------- |
| DDL      | Data Definition Language     | CREATE, ALTER, DROP, TRUNCATE, RENAME | Define/modify structure |
| DML      | Data Manipulation Language   | INSERT, UPDATE, DELETE                | Modify data             |
| DQL      | Data Query Language          | SELECT                                | Retrieve data           |
| DCL      | Data Control Language        | GRANT, REVOKE                         | Manage permissions      |
| TCL      | Transaction Control Language | COMMIT, ROLLBACK, SAVEPOINT           | Manage transactions     |

---

# 7. DDL vs DML vs DQL vs DCL vs TCL

```text
DDL
│
└── Structure
    CREATE
    ALTER
    DROP
    TRUNCATE
    RENAME

DML
│
└── Data Modification
    INSERT
    UPDATE
    DELETE

DQL
│
└── Data Retrieval
    SELECT

DCL
│
└── Permissions
    GRANT
    REVOKE

TCL
│
└── Transactions
    COMMIT
    ROLLBACK
    SAVEPOINT
```

---

# 8. Example: Complete Workflow

Suppose we need to create and work with an employee table.

### Step 1 — DDL

Create the table:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

### Step 2 — DML

Insert data:

```sql
INSERT INTO employees
(employee_id, name, salary)
VALUES
(1, 'Rahul', 50000),
(2, 'Priya', 60000);
```

---

### Step 3 — DQL

Read the data:

```sql
SELECT *
FROM employees;
```

---

### Step 4 — DML

Update data:

```sql
UPDATE employees
SET salary = 65000
WHERE employee_id = 2;
```

---

### Step 5 — DQL

Check the result:

```sql
SELECT *
FROM employees
WHERE employee_id = 2;
```

---

### Step 6 — TCL

Commit the changes:

```sql
COMMIT;
```

---

### Step 7 — DCL

Give an analyst permission to read the table:

```sql
GRANT SELECT
ON employees
TO analyst;
```

---

# 9. Important Difference: DELETE vs TRUNCATE vs DROP

This is one of the most important SQL interview topics.

| Feature                  | DELETE         | TRUNCATE       | DROP             |
| ------------------------ | -------------- | -------------- | ---------------- |
| Removes rows             | Yes            | Yes, all       | Yes, with object |
| Removes table structure  | No             | No             | Yes              |
| `WHERE` allowed          | Yes            | No             | No               |
| Can remove selected rows | Yes            | No             | No               |
| Table remains            | Yes            | Yes            | No               |
| Category commonly used   | DML            | DDL            | DDL              |
| Transaction behavior     | DBMS-dependent | DBMS-dependent | DBMS-dependent   |

Example:

```sql
DELETE FROM employees
WHERE employee_id = 10;
```

Only matching rows are removed.

```sql
TRUNCATE TABLE employees;
```

All rows are removed, but the table remains.

```sql
DROP TABLE employees;
```

The table itself is removed.

---

# 10. Important Difference: DROP vs DELETE

### DELETE

```sql
DELETE FROM employees;
```

Means:

```text
Remove rows
Keep table
```

### DROP

```sql
DROP TABLE employees;
```

Means:

```text
Remove table
Remove structure
Remove data
```

---

# 11. Important Difference: TRUNCATE vs DELETE

### DELETE

```sql
DELETE FROM employees
WHERE salary < 30000;
```

Can selectively delete rows.

### TRUNCATE

```sql
TRUNCATE TABLE employees;
```

Removes all rows and does not support a `WHERE` clause.

---

# 12. Important Difference: DDL vs DML

### DDL

Works mainly with **database structure**.

```sql
CREATE TABLE employees (...);

ALTER TABLE employees ADD email VARCHAR(255);

DROP TABLE employees;
```

### DML

Works mainly with **table data**.

```sql
INSERT INTO employees VALUES (...);

UPDATE employees SET salary = 50000;

DELETE FROM employees WHERE employee_id = 1;
```

---

# 13. Important Difference: DML vs DQL

### DML

Changes data:

```sql
INSERT
UPDATE
DELETE
```

### DQL

Retrieves data:

```sql
SELECT
```

Note:

> Some SQL references group `SELECT` under DML or use "DML" broadly. For learning and interview preparation, treating `SELECT` as **DQL** is a common classification.

---

# 14. SQL Commands — Quick Revision

### DDL

```sql
CREATE
ALTER
DROP
TRUNCATE
RENAME
```

### DML

```sql
INSERT
UPDATE
DELETE
```

### DQL

```sql
SELECT
```

### DCL

```sql
GRANT
REVOKE
```

### TCL

```sql
COMMIT
ROLLBACK
SAVEPOINT
```

---

# 15. Easy Memory Trick

```text
DDL → Define
DML → Modify
DQL → Query
DCL → Control
TCL → Transaction
```

Or:

```text
DDL → Structure
DML → Data
DQL → Read
DCL → Permission
TCL → Transaction
```

---

# 16. Interview Revision Table

| Command   | Category | Main Use                 |
| --------- | -------- | ------------------------ |
| CREATE    | DDL      | Create object            |
| ALTER     | DDL      | Modify structure         |
| DROP      | DDL      | Delete object            |
| TRUNCATE  | DDL      | Remove all rows          |
| RENAME    | DDL      | Rename object            |
| INSERT    | DML      | Add rows                 |
| UPDATE    | DML      | Modify rows              |
| DELETE    | DML      | Delete rows              |
| SELECT    | DQL      | Retrieve rows            |
| GRANT     | DCL      | Give permissions         |
| REVOKE    | DCL      | Remove permissions       |
| COMMIT    | TCL      | Save transaction         |
| ROLLBACK  | TCL      | Undo uncommitted changes |
| SAVEPOINT | TCL      | Create rollback point    |

---

# 17. Final Revision Map

```text
                         SQL COMMANDS
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
       DDL                   DML                   DQL
   Structure             Modify Data           Retrieve Data
        │                     │                     │
  CREATE                  INSERT                 SELECT
  ALTER                   UPDATE
  DROP                    DELETE
  TRUNCATE
  RENAME

        ┌─────────────────────┴─────────────────────┐
        │                                           │
       DCL                                         TCL
   Permissions                                  Transactions
        │                                           │
     GRANT                                      COMMIT
     REVOKE                                    ROLLBACK
                                               SAVEPOINT
```

## One-Line Revision

```text
DDL = Structure
DML = Modify
DQL = Retrieve
DCL = Permissions
TCL = Transactions
```

