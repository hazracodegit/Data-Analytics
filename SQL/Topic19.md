# SQL — Triggers, Cursors, Error Handling, Security, Query Execution & Optimization

> Complete SQL revision notes covering **Triggers, Cursors, Error Handling, SQL Security, Query Execution, and Query Optimization** with theory, examples, and practical concepts.

---

# Table of Contents

1. [Triggers](#1-triggers)
2. [Why Triggers Are Used](#2-why-triggers-are-used)
3. [Types of Triggers](#3-types-of-triggers)
4. [BEFORE Triggers](#4-before-triggers)
5. [AFTER Triggers](#5-after-triggers)
6. [INSERT Triggers](#6-insert-triggers)
7. [UPDATE Triggers](#7-update-triggers)
8. [DELETE Triggers](#8-delete-triggers)
9. [OLD and NEW Values](#9-old-and-new-values)
10. [Row-Level and Statement-Level Triggers](#10-row-level-and-statement-level-triggers)
11. [Trigger Examples](#11-trigger-examples)
12. [Trigger Use Cases](#12-trigger-use-cases)
13. [Advantages and Disadvantages of Triggers](#13-advantages-and-disadvantages-of-triggers)
14. [Cursors](#14-cursors)
15. [Why Cursors Are Used](#15-why-cursors-are-used)
16. [Cursor Lifecycle](#16-cursor-lifecycle)
17. [Cursor Components](#17-cursor-components)
18. [Cursor Example](#18-cursor-example)
19. [Cursor with Loop](#19-cursor-with-loop)
20. [Cursor Error Handling](#20-cursor-error-handling)
21. [Cursor Advantages and Disadvantages](#21-cursor-advantages-and-disadvantages)
22. [Set-Based Processing vs Cursors](#22-set-based-processing-vs-cursors)
23. [Error Handling](#23-error-handling)
24. [Types of SQL Errors](#24-types-of-sql-errors)
25. [Exception Handling](#25-exception-handling)
26. [Transactions and Error Handling](#26-transactions-and-error-handling)
27. [SQL Security](#27-sql-security)
28. [Authentication vs Authorization](#28-authentication-vs-authorization)
29. [Users, Roles and Privileges](#29-users-roles-and-privileges)
30. [GRANT](#30-grant)
31. [REVOKE](#31-revoke)
32. [Principle of Least Privilege](#32-principle-of-least-privilege)
33. [SQL Injection](#33-sql-injection)
34. [Preventing SQL Injection](#34-preventing-sql-injection)
35. [Views and Security](#35-views-and-security)
36. [Stored Procedures and Security](#36-stored-procedures-and-security)
37. [Encryption and Sensitive Data](#37-encryption-and-sensitive-data)
38. [Query Execution](#38-query-execution)
39. [SQL Query Processing Order](#39-sql-query-processing-order)
40. [Logical Query Processing](#40-logical-query-processing)
41. [Physical Query Execution](#41-physical-query-execution)
42. [Query Execution Plan](#42-query-execution-plan)
43. [EXPLAIN](#43-explain)
44. [EXPLAIN ANALYZE](#44-explain-analyze)
45. [Table Scan](#45-table-scan)
46. [Index Scan](#46-index-scan)
47. [Index Seek](#47-index-seek)
48. [Join Algorithms](#48-join-algorithms)
49. [Query Optimization](#49-query-optimization)
50. [Cost-Based Optimization](#50-cost-based-optimization)
51. [Statistics](#51-statistics)
52. [Index Optimization](#52-index-optimization)
53. [Composite Indexes](#53-composite-indexes)
54. [SARGable Queries](#54-sargable-queries)
55. [WHERE Optimization](#55-where-optimization)
56. [JOIN Optimization](#56-join-optimization)
57. [GROUP BY Optimization](#57-group-by-optimization)
58. [ORDER BY Optimization](#58-order-by-optimization)
59. [LIMIT Optimization](#59-limit-optimization)
60. [Subquery Optimization](#60-subquery-optimization)
61. [CTE Optimization](#61-cte-optimization)
62. [Avoiding SELECT *](#62-avoiding-select-)
63. [Functions and Indexes](#63-functions-and-indexes)
64. [Implicit Type Conversion](#64-implicit-type-conversion)
65. [OR vs UNION](#65-or-vs-union)
66. [Pagination Optimization](#66-pagination-optimization)
67. [Query Optimization Checklist](#67-query-optimization-checklist)
68. [Complete Optimization Example](#68-complete-optimization-example)
69. [Triggers vs Procedures vs Functions vs Cursors](#69-triggers-vs-procedures-vs-functions-vs-cursors)
70. [Interview Questions](#70-interview-questions)
71. [Final Revision](#71-final-revision)

---

# 1. Triggers

## Technical Definition

A **trigger** is a database object that automatically executes a predefined set of SQL statements when a specified event occurs on a table or other supported database object.

## Easy Meaning

A trigger is:

> **Automatic database logic that runs when something happens.**

For example:

```text
INSERT happens
     ↓
Trigger automatically runs
     ↓
Audit record created
```

The application does not need to explicitly call the trigger.

---

# 2. Why Triggers Are Used

Triggers are commonly used for:

```text
✓ Auditing
✓ Maintaining history
✓ Automatic calculations
✓ Data validation
✓ Enforcing business rules
✓ Maintaining derived data
✓ Logging changes
✓ Synchronizing related data
```

Example:

When an employee's salary changes:

```text
EMPLOYEES
    ↓
Salary updated
    ↓
TRIGGER
    ↓
SALARY_HISTORY
    ↓
Old salary + New salary recorded
```

---

# 3. Types of Triggers

Triggers can be classified in several ways.

## By Timing

```text
BEFORE
AFTER
INSTEAD OF
```

Availability depends on the DBMS.

---

## By Event

```text
INSERT
UPDATE
DELETE
```

Some systems also support triggers for other database events, such as DDL or login events.

---

## By Granularity

```text
ROW-LEVEL
STATEMENT-LEVEL
```

---

# 4. BEFORE Triggers

## Technical Definition

A `BEFORE` trigger executes before the triggering operation is completed.

Example:

```text
INSERT
  ↓
BEFORE trigger
  ↓
Actual INSERT
```

---

## Example

Suppose we want to ensure that salary is never negative.

```sql
DELIMITER //

CREATE TRIGGER before_employee_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN

    IF NEW.salary < 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary cannot be negative';
    END IF;

END //

DELIMITER ;
```

Now:

```sql
INSERT INTO employees
(employee_id, employee_name, salary)
VALUES
(101, 'Alice', -5000);
```

The trigger prevents the invalid data.

---

# 5. AFTER Triggers

## Technical Definition

An `AFTER` trigger executes after the triggering operation has occurred.

Example:

```text
INSERT
  ↓
Actual row inserted
  ↓
AFTER trigger
  ↓
Audit record
```

---

## Example

```sql
DELIMITER //

CREATE TRIGGER after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN

    INSERT INTO employee_audit
    (
        employee_id,
        action_type,
        action_time
    )
    VALUES
    (
        NEW.employee_id,
        'INSERT',
        CURRENT_TIMESTAMP
    );

END //

DELIMITER ;
```

Whenever an employee is inserted, an audit record is created automatically.

---

# 6. INSERT Triggers

An INSERT trigger executes when rows are inserted.

Example:

```sql
CREATE TRIGGER employee_insert_audit
AFTER INSERT ON employees
FOR EACH ROW
BEGIN

    INSERT INTO employee_audit(employee_id, action_type)
    VALUES (NEW.employee_id, 'INSERT');

END;
```

---

# 7. UPDATE Triggers

An UPDATE trigger executes when rows are updated.

Example:

```sql
DELIMITER //

CREATE TRIGGER employee_salary_audit
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN

    IF OLD.salary <> NEW.salary THEN

        INSERT INTO salary_history
        (
            employee_id,
            old_salary,
            new_salary,
            changed_at
        )
        VALUES
        (
            OLD.employee_id,
            OLD.salary,
            NEW.salary,
            CURRENT_TIMESTAMP
        );

    END IF;

END //

DELIMITER ;
```

---

# 8. DELETE Triggers

A DELETE trigger executes when rows are deleted.

Example:

```sql
DELIMITER //

CREATE TRIGGER employee_delete_audit
AFTER DELETE ON employees
FOR EACH ROW
BEGIN

    INSERT INTO employee_audit
    (
        employee_id,
        action_type,
        action_time
    )
    VALUES
    (
        OLD.employee_id,
        'DELETE',
        CURRENT_TIMESTAMP
    );

END //

DELIMITER ;
```

For a deleted row, the old values are available through `OLD`.

---

# 9. OLD and NEW Values

This is one of the most important trigger concepts.

## `NEW`

Represents the new row values.

Commonly available for:

```text
INSERT
UPDATE
```

Example:

```sql
NEW.salary
```

---

## `OLD`

Represents the previous row values.

Commonly available for:

```text
UPDATE
DELETE
```

Example:

```sql
OLD.salary
```

---

## Comparison

For an UPDATE:

```text
OLD.salary = 50000
NEW.salary = 60000
```

Therefore:

```text
Salary increased by 10000
```

---

## Quick Table

| Event  | OLD                 | NEW                 |
| ------ | ------------------- | ------------------- |
| INSERT | Usually unavailable | Available           |
| UPDATE | Available           | Available           |
| DELETE | Available           | Usually unavailable |

Exact trigger capabilities vary by database.

---

# 10. Row-Level and Statement-Level Triggers

## Row-Level Trigger

A row-level trigger executes once for each affected row.

Suppose:

```sql
DELETE FROM employees
WHERE department_id = 10;
```

If 100 employees are deleted:

```text
100 rows affected
      ↓
100 trigger executions
```

In MySQL, triggers are row-level using:

```sql
FOR EACH ROW
```

---

# 10.1 Statement-Level Trigger

A statement-level trigger executes once for the SQL statement, regardless of how many rows it affects.

Example concept:

```sql
DELETE FROM employees
WHERE department_id = 10;
```

If 100 rows are deleted:

```text
100 rows
   ↓
1 trigger execution
```

Database support varies. PostgreSQL and Oracle support statement-level triggers, while MySQL triggers are row-level.

---

# 11. Trigger Example — Audit System

Suppose:

```text
employees
```

contains:

```text
employee_id
employee_name
salary
```

Create audit table:

```sql
CREATE TABLE salary_history (
    history_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT,
    old_salary DECIMAL(10,2),
    new_salary DECIMAL(10,2),
    changed_at TIMESTAMP
);
```

Create trigger:

```sql
DELIMITER //

CREATE TRIGGER salary_change_audit
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN

    IF OLD.salary <> NEW.salary THEN

        INSERT INTO salary_history
        (
            employee_id,
            old_salary,
            new_salary,
            changed_at
        )
        VALUES
        (
            OLD.employee_id,
            OLD.salary,
            NEW.salary,
            CURRENT_TIMESTAMP
        );

    END IF;

END //

DELIMITER ;
```

Update salary:

```sql
UPDATE employees
SET salary = 65000
WHERE employee_id = 101;
```

The history table automatically receives:

```text
employee_id | old_salary | new_salary
------------|------------|-----------
101         | 60000      | 65000
```

---

# 12. Trigger Use Cases

## 1. Auditing

Track:

```text
Who changed data?
What changed?
When did it change?
```

---

## 2. History Tables

Store previous versions.

```text
employees
    ↓
UPDATE
    ↓
salary_history
```

---

## 3. Automatic Timestamp

For example:

```text
created_at
updated_at
```

---

## 4. Validation

Prevent invalid data.

---

## 5. Derived Data

Automatically update related information.

---

# 13. Advantages and Disadvantages of Triggers

## Advantages

```text
✓ Automatic
✓ Centralized database logic
✓ Useful for auditing
✓ Enforces certain rules consistently
✓ Application doesn't need to remember every audit operation
```

## Disadvantages

```text
✗ Hidden side effects
✗ Can make debugging difficult
✗ Can slow INSERT/UPDATE/DELETE
✗ Complex trigger chains are difficult to understand
✗ Database-specific syntax
```

Important:

> Use triggers carefully. Automatic behavior should remain understandable to developers and database administrators.

---

# 14. Cursors

## Technical Definition

A **cursor** is a database mechanism that allows a result set to be processed one row at a time.

## Easy Meaning

Normally SQL works with many rows at once.

A cursor says:

> "Take the result and process each row individually."

---

# 15. Why Cursors Are Used

Cursors are useful when a task genuinely requires procedural, row-by-row processing.

Example:

```text
100 employees
     ↓
Cursor
     ↓
Employee 1 → process
Employee 2 → process
Employee 3 → process
...
Employee 100 → process
```

---

# 16. Why Cursors Are Often Avoided

SQL is designed around **set-based processing**.

Instead of:

```text
Process row 1
Process row 2
Process row 3
...
```

SQL can often do:

```text
Process all matching rows
```

This is usually simpler and more efficient.

---

# 17. Cursor Lifecycle

A typical cursor lifecycle is:

```text
DECLARE
   ↓
OPEN
   ↓
FETCH
   ↓
PROCESS
   ↓
FETCH
   ↓
PROCESS
   ↓
...
   ↓
CLOSE
```

Some DBMSs also require explicit cursor deallocation.

---

# 18. Cursor Components

## 1. DECLARE

Define the cursor.

```sql
DECLARE employee_cursor CURSOR FOR
SELECT employee_id, salary
FROM employees;
```

---

## 2. OPEN

Open the cursor.

```sql
OPEN employee_cursor;
```

---

## 3. FETCH

Retrieve the next row.

```sql
FETCH employee_cursor
INTO employee_id, employee_salary;
```

Exact syntax varies by DBMS.

---

## 4. CLOSE

Close the cursor.

```sql
CLOSE employee_cursor;
```

---

# 19. Cursor Example — MySQL

```sql
DELIMITER //

CREATE PROCEDURE ProcessEmployees()
BEGIN

    DECLARE done INT DEFAULT FALSE;

    DECLARE emp_id INT;
    DECLARE emp_salary DECIMAL(10,2);

    DECLARE employee_cursor CURSOR FOR
        SELECT employee_id, salary
        FROM employees;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET done = TRUE;

    OPEN employee_cursor;

    employee_loop: LOOP

        FETCH employee_cursor
        INTO emp_id, emp_salary;

        IF done THEN
            LEAVE employee_loop;
        END IF;

        -- Process one employee here

        SELECT emp_id, emp_salary;

    END LOOP;

    CLOSE employee_cursor;

END //

DELIMITER ;
```

---

# 20. Understanding the Cursor Example

First:

```sql
DECLARE employee_cursor CURSOR FOR
SELECT employee_id, salary
FROM employees;
```

This defines the result set.

Then:

```sql
OPEN employee_cursor;
```

opens it.

Then:

```sql
FETCH employee_cursor
INTO emp_id, emp_salary;
```

gets one row.

Then:

```sql
IF done THEN
    LEAVE employee_loop;
END IF;
```

checks whether there are no more rows.

Finally:

```sql
CLOSE employee_cursor;
```

releases the cursor.

---

# 21. Cursor with Calculation

Suppose we want to calculate a bonus individually.

```sql
DELIMITER //

CREATE PROCEDURE CalculateBonuses()
BEGIN

    DECLARE done INT DEFAULT FALSE;

    DECLARE emp_id INT;
    DECLARE emp_salary DECIMAL(10,2);
    DECLARE bonus DECIMAL(10,2);

    DECLARE employee_cursor CURSOR FOR
        SELECT employee_id, salary
        FROM employees;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET done = TRUE;

    OPEN employee_cursor;

    employee_loop: LOOP

        FETCH employee_cursor
        INTO emp_id, emp_salary;

        IF done THEN
            LEAVE employee_loop;
        END IF;

        SET bonus = emp_salary * 0.10;

        INSERT INTO employee_bonus
        (
            employee_id,
            bonus
        )
        VALUES
        (
            emp_id,
            bonus
        );

    END LOOP;

    CLOSE employee_cursor;

END //

DELIMITER ;
```

---

# 22. Cursor Error Handling

A cursor can encounter a "no more rows" condition.

In MySQL:

```sql
DECLARE CONTINUE HANDLER FOR NOT FOUND
SET done = TRUE;
```

Then:

```sql
FETCH cursor
INTO variables;

IF done THEN
    LEAVE loop;
END IF;
```

This prevents the loop from continuing after the cursor is exhausted.

---

# 23. Cursor Advantages and Disadvantages

## Advantages

```text
✓ Row-by-row processing
✓ Useful for procedural tasks
✓ Can implement complex per-row logic
✓ Useful when set-based SQL cannot conveniently express the operation
```

## Disadvantages

```text
✗ Usually slower than set-based SQL
✗ More procedural code
✗ More memory/processing overhead
✗ Can hold database resources
✗ Can increase transaction duration
✗ More difficult to maintain
```

---

# 24. Set-Based Processing vs Cursors

Suppose we want to give every employee a 10% salary increase.

### Cursor approach

```text
Employee 1 → update
Employee 2 → update
Employee 3 → update
...
```

### Set-based approach

```sql
UPDATE employees
SET salary = salary * 1.10;
```

The set-based query is usually preferable.

---

# 25. When Should You Use a Cursor?

Use a cursor when:

```text
✓ Row-by-row logic is genuinely required
✓ Each row requires procedural interaction
✓ The operation cannot reasonably be expressed as set-based SQL
✓ You understand the performance implications
```

Avoid cursors when a normal:

```text
SELECT
UPDATE
INSERT
DELETE
JOIN
CTE
WINDOW FUNCTION
```

can solve the problem efficiently.

---

# 26. Error Handling

## Technical Definition

**Error handling** is the process of detecting, managing, and responding to errors or exceptional conditions during SQL execution.

## Easy Meaning

When something goes wrong:

```text
Error occurs
    ↓
Detect it
    ↓
Handle it
    ↓
Take appropriate action
```

For example:

```text
Invalid data
Duplicate key
Foreign key violation
Transaction failure
Permission denied
Connection failure
```

---

# 27. Why Error Handling Is Important

Without error handling:

```text
Operation fails
     ↓
Partial changes may remain
     ↓
Data inconsistency
```

With proper error handling:

```text
Operation fails
     ↓
Detect error
     ↓
ROLLBACK
     ↓
Database remains consistent
```

---

# 28. Types of SQL Errors

Different database systems classify errors differently, but conceptually we can identify:

## 1. Syntax Errors

Invalid SQL syntax.

```sql
SELEC *
FROM employees;
```

`SELECT` is misspelled.

---

# 28.1 Constraint Errors

Example:

```sql
INSERT INTO employees(employee_id)
VALUES (101);
```

If `employee_id = 101` already exists and is a primary key:

```text
Duplicate key error
```

---

# 28.2 Foreign Key Errors

Example:

```sql
INSERT INTO orders(order_id, customer_id)
VALUES (500, 99999);
```

If customer `99999` does not exist:

```text
Foreign key violation
```

---

# 28.3 Data Type Errors

Example:

```sql
INSERT INTO employees(age)
VALUES ('hello');
```

Depending on the DBMS and configuration, this may cause a conversion/type error.

---

# 28.4 Permission Errors

A user may attempt:

```sql
DELETE FROM employees;
```

without the required privilege.

---

# 28.5 Transaction Errors

An operation may fail after earlier operations have already occurred.

This is where:

```text
ROLLBACK
```

becomes important.

---

# 29. Exception Handling

Database procedural languages provide mechanisms to handle errors.

The exact syntax depends on the DBMS.

For MySQL:

```sql
DECLARE EXIT HANDLER FOR SQLEXCEPTION
BEGIN
    ROLLBACK;
END;
```

Conceptually:

```text
TRY operation
     ↓
Success → Continue
     ↓
Failure
     ↓
Handler
     ↓
ROLLBACK / LOG / RETURN ERROR
```

---

# 30. MySQL Error Handling Example

```sql
DELIMITER //

CREATE PROCEDURE CreateOrder()
BEGIN

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
    END;

    START TRANSACTION;

    INSERT INTO orders
    (
        order_id,
        customer_id
    )
    VALUES
    (
        1001,
        101
    );

    INSERT INTO order_items
    (
        order_id,
        product_id,
        quantity
    )
    VALUES
    (
        1001,
        501,
        2
    );

    COMMIT;

END //

DELIMITER ;
```

If an error occurs:

```text
ROLLBACK
```

is executed.

---

# 31. Error Handling with Transaction

Consider a bank transfer.

We need:

```text
Account A
    ↓
Subtract money

Account B
    ↓
Add money
```

Both operations must succeed.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

---

# 32. ACID and Error Handling

Transactions follow the ACID principles.

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

Error handling is especially related to:

```text
Atomicity
```

because a transaction should behave as an all-or-nothing unit.

---

# 33. SQL Security

## Technical Definition

**SQL security** refers to the mechanisms used to protect databases, data, database objects, and database operations from unauthorized access, modification, disclosure, or destruction.

## Easy Meaning

SQL security answers:

```text
Who can access the database?
What can they access?
What can they do?
How is sensitive data protected?
```

---

# 34. Main Areas of SQL Security

```text
Authentication
Authorization
Privileges
Roles
Access control
Encryption
SQL injection prevention
Auditing
Secure connections
Data masking
Backup security
```

---

# 35. Authentication vs Authorization

These two are frequently confused.

## Authentication

> **Who are you?**

Example:

```text
Username
Password
Certificate
Identity provider
```

---

## Authorization

> **What are you allowed to do?**

Example:

```text
SELECT
INSERT
UPDATE
DELETE
```

---

## Easy Memory

```text
AUTHENTICATION
= Who are you?

AUTHORIZATION
= What can you do?
```

---

# 36. Users

A database can have multiple users.

Example:

```text
admin
analyst
reporting_user
application_user
readonly_user
```

Each user can have different permissions.

---

# 37. Roles

## Technical Definition

A **role** is a named collection of privileges that can be assigned to users.

## Easy Meaning

Instead of giving permissions individually:

```text
User A → SELECT
User A → INSERT
User A → UPDATE
```

create:

```text
sales_role
```

with those permissions.

Then assign:

```text
sales_role → User A
```

---

# 38. GRANT

`GRANT` gives privileges.

Example:

```sql
GRANT SELECT
ON employees
TO analyst;
```

The analyst can now read the table, subject to the DBMS's permission model.

---

# 39. Multiple Privileges

```sql
GRANT
    SELECT,
    INSERT,
    UPDATE
ON employees
TO hr_user;
```

---

# 40. Database-Level Privileges

Syntax varies by DBMS.

Conceptually:

```sql
GRANT SELECT
ON database_name.table_name
TO user_name;
```

---

# 41. REVOKE

`REVOKE` removes privileges.

```sql
REVOKE INSERT
ON employees
FROM analyst;
```

Now the user no longer has that granted privilege, subject to inherited permissions.

---

# 42. Principle of Least Privilege

One of the most important security principles.

## Definition

Give users only the minimum permissions required to perform their job.

Example:

A reporting user only needs:

```text
SELECT
```

They usually do not need:

```text
DROP
DELETE
ALTER
CREATE USER
```

---

# 43. Why Least Privilege Matters

Suppose an application account has:

```text
SELECT
INSERT
UPDATE
DELETE
DROP
CREATE USER
```

If the application is compromised, the attacker may inherit those privileges.

Better:

```text
Application
    ↓
Minimum required privileges
```

---

# 44. SQL Injection

## Technical Definition

SQL injection is a security vulnerability where untrusted input is incorporated into SQL in a way that allows the input to alter the intended SQL statement.

## Easy Meaning

The user provides input that becomes part of the SQL code instead of being treated only as data.

---

# 45. Unsafe SQL

Suppose an application constructs:

```text
"SELECT * FROM users WHERE username = '" + username + "'"
```

If input is malicious, the resulting SQL may not mean what the developer intended.

---

# 46. Parameterized Query

The correct approach is to use parameterized/prepared statements.

Example concept:

```sql
SELECT *
FROM users
WHERE username = ?;
```

The application supplies the username as a parameter separately from the SQL code.

---

# 47. Why Parameterized Queries Are Safer

Without parameters:

```text
Input + SQL
     ↓
One SQL string
```

With parameters:

```text
SQL structure
     +
Data parameter
     ↓
Database
```

The input is treated as data rather than SQL syntax.

---

# 48. Other SQL Security Practices

```text
✓ Use parameterized queries
✓ Apply least privilege
✓ Use strong authentication
✓ Encrypt connections
✓ Protect credentials
✓ Don't expose database directly to the internet unnecessarily
✓ Keep database software patched
✓ Audit sensitive operations
✓ Protect backups
✓ Avoid storing plaintext passwords
```

---

# 49. Password Storage

Never store user passwords as plaintext.

Bad:

```text
password
---------
MyPassword123
```

Instead, applications should use a strong password hashing algorithm designed for password storage, such as:

```text
Argon2
bcrypt
scrypt
```

with appropriate parameters and salts.

---

# 50. Encryption

Encryption can protect data:

```text
At Rest
```

and:

```text
In Transit
```

## Encryption at Rest

Protects stored database files/backups.

## Encryption in Transit

Protects data traveling between:

```text
Application
      ↓
Network
      ↓
Database
```

TLS is commonly used for secure database connections.

---

# 51. Views and Security

Views can expose only selected data.

Suppose:

```text
employees
-------------------------
employee_id
name
salary
phone
address
```

A reporting user may not need salary or phone.

Create:

```sql
CREATE VIEW employee_public AS
SELECT
    employee_id,
    name
FROM employees;
```

Then give access to the view rather than the base table where appropriate.

```text
employees
    ↓
VIEW
    ↓
Only approved columns
```

---

# 52. Row-Level Security

Some database systems support **Row-Level Security (RLS)**.

## Definition

Row-level security restricts which rows a user can access.

Example:

```text
Manager A
    ↓
Only Department A rows

Manager B
    ↓
Only Department B rows
```

This is different from simply hiding columns.

---

# 53. SQL Auditing

Auditing records security-sensitive events.

Examples:

```text
Login
Data changes
Permission changes
DDL operations
Administrative actions
```

Audit information can help with:

```text
Security investigations
Compliance
Troubleshooting
Accountability
```

---

# 54. Query Execution

Now we move from security to how the database actually executes SQL.

## Important Concept

When you write:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

the database does not simply execute the text from top to bottom.

The database:

```text
SQL Query
   ↓
Parse
   ↓
Validate
   ↓
Rewrite/Transform
   ↓
Optimize
   ↓
Execution Plan
   ↓
Execute
   ↓
Return Result
```

---

# 55. Query Processing Stages

A simplified model:

```text
1. Parsing
      ↓
2. Semantic validation
      ↓
3. Query rewriting
      ↓
4. Optimization
      ↓
5. Execution plan
      ↓
6. Execution
      ↓
7. Result
```

Exact architecture differs between database systems.

---

# 56. Parsing

The database checks whether the SQL syntax is valid.

Example:

```sql
SELEC *
FROM employees;
```

This has invalid syntax.

The parser detects the problem.

---

# 57. Semantic Analysis

The database checks whether referenced objects make sense.

Example:

```sql
SELECT employee_name
FROM employees;
```

The database checks:

```text
Does employees exist?
Does employee_name exist?
Does the user have permission?
```

---

# 58. Query Rewriting

The optimizer may transform a query into an equivalent form that is easier or cheaper to execute.

For example, some database systems may simplify predicates or transform subqueries into joins/semi-joins where beneficial.

The important idea:

```text
Same result
     ↓
Different internal representation
```

---

# 59. Query Optimization

The database considers possible execution strategies.

For example:

```text
Option A
Full table scan

Option B
Use index

Option C
Different join order

Option D
Different join algorithm
```

The optimizer estimates costs and chooses a plan.

---

# 60. Execution Plan

## Technical Definition

An **execution plan** is the database's selected strategy for retrieving and processing the requested data.

## Easy Meaning

It is the database's **step-by-step plan for answering your query**.

Example:

```text
Index Scan
    ↓
Filter
    ↓
Join
    ↓
Sort
    ↓
Result
```

---

# 61. EXPLAIN

`EXPLAIN` is used to inspect the query plan in many database systems.

Example:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE department_id = 10;
```

The output may show information such as:

```text
Access method
Index used
Estimated rows
Join strategy
Estimated cost
```

Exact output differs by database.

---

# 62. EXPLAIN ANALYZE

Some database systems support:

```sql
EXPLAIN ANALYZE
```

It generally executes the query and provides actual runtime information alongside plan information.

Example:

```sql
EXPLAIN ANALYZE
SELECT *
FROM employees
WHERE department_id = 10;
```

This can help compare:

```text
Estimated rows
vs
Actual rows
```

which is extremely useful for diagnosing poor optimizer estimates.

> Be careful: unlike plain `EXPLAIN` in many systems, `EXPLAIN ANALYZE` can execute the statement. For `INSERT`, `UPDATE`, or `DELETE`, use the DBMS-specific precautions/options for analyzing without unintended data changes.

---

# 63. Table Scan

## Definition

A table scan reads rows from the table to find matching records.

Example:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

If there is no useful index:

```text
Table
 ↓
Read many/all rows
 ↓
Check salary
 ↓
Return matches
```

For a small table, this may be perfectly acceptable.

---

# 64. Index Scan

An index scan reads entries from an index, potentially accessing a substantial portion of the index.

Conceptually:

```text
Index
 ↓
Read index entries
 ↓
Locate rows
 ↓
Return/process rows
```

Exact terminology varies by DBMS.

---

# 65. Index Seek

An index seek generally means using an index to navigate directly toward the required key range rather than scanning the whole index.

Example:

```sql
SELECT *
FROM employees
WHERE employee_id = 101;
```

With an index on:

```text
employee_id
```

the database can efficiently locate the row.

SQL Server commonly uses the term **Index Seek**. Other systems use different terminology.

---

# 66. Scan vs Seek

```text
SCAN
→ Read many entries/pages to find matches.

SEEK
→ Navigate directly to a relevant key/range.
```

But:

> A scan is not automatically bad, and a seek is not automatically good.

For example, if a query needs 90% of a table, a sequential/table scan may be cheaper than repeatedly using an index.

---

# 67. Join Algorithms

When joining tables, the optimizer can choose different algorithms.

Common algorithms include:

```text
Nested Loop Join
Hash Join
Merge Join
```

Availability and implementation details depend on the database.

---

# 68. Nested Loop Join

## Concept

For each row from one input, search the other input for matching rows.

```text
Outer table
   ↓
Row 1 → Search inner
Row 2 → Search inner
Row 3 → Search inner
```

Works well when:

```text
✓ One side is small
✓ Inner side has a useful index
```

---

# 69. Hash Join

## Concept

The database builds a hash structure from one input and probes it with rows from the other input.

```text
Table A
  ↓
Build hash table
  ↓
Table B
  ↓
Probe hash table
```

Often effective for larger equality joins.

---

# 70. Merge Join

## Concept

A merge join works efficiently when inputs are ordered on the join keys.

```text
Sorted A
   +
Sorted B
   ↓
Merge matching values
```

Useful when appropriate ordering already exists or can be obtained efficiently.

---

# 71. Query Optimization

## Technical Definition

**Query optimization** is the process of finding an efficient execution strategy for a SQL query while preserving its required result.

## Easy Meaning

Query optimization means:

> **Making SQL queries execute efficiently without changing the result.**

---

# 72. Why Query Optimization Matters

A query might work correctly but still be slow.

Example:

```text
Query A
1 second

Query B
30 seconds
```

If the application executes the query:

```text
1,000,000 times
```

the performance difference becomes huge.

---

# 73. Cost-Based Optimization

Modern relational databases commonly use **cost-based optimization**.

The optimizer considers alternatives such as:

```text
Table scan
Index access
Join order
Join algorithm
Sorting
Aggregation
Parallel execution
```

It estimates the cost of each plan and chooses what it believes is efficient.

---

# 74. Query Cost

Cost can involve resources such as:

```text
CPU
Disk I/O
Memory
Network I/O
Temporary storage
Parallel execution resources
```

The exact cost model is database-specific.

---

# 75. Statistics

## Technical Definition

Database statistics describe characteristics of the data that help the optimizer estimate cardinalities and costs.

Examples:

```text
Number of rows
Value distribution
Distinct values
Data distribution
Histograms
```

---

# 76. Why Statistics Matter

Suppose:

```text
employees = 10 million rows
```

and:

```text
department_id = 10
```

matches only:

```text
100 rows
```

An index could be very useful.

But if:

```text
department_id = 10
```

matches:

```text
9 million rows
```

a large scan might be more efficient.

The optimizer needs good statistics to estimate this.

---

# 77. Stale Statistics

If statistics are outdated:

```text
Actual data
     ≠
Optimizer assumptions
```

Then the optimizer may choose a poor plan.

Database systems provide different mechanisms for collecting/updating statistics.

---

# 78. Index Optimization

Indexes are one of the most important performance tools.

Example:

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

Query:

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

The index may allow efficient access.

---

# 79. When Indexes Help

Indexes are often useful for columns frequently used in:

```text
WHERE
JOIN
ORDER BY
GROUP BY
UNIQUE constraints
```

But the exact benefit depends on selectivity, data distribution, query shape, and DBMS.

---

# 80. Indexes Have a Cost

Indexes are not free.

They require:

```text
Storage
+
Maintenance
+
Write overhead
```

When inserting:

```text
INSERT
 ↓
Table modification
 ↓
Indexes also updated
```

When updating indexed columns:

```text
UPDATE
 ↓
Table update
 ↓
Index maintenance
```

Therefore:

> Don't create indexes on every column.

---

# 81. Composite Index

A composite index contains multiple columns.

```sql
CREATE INDEX idx_employee_dept_salary
ON employees(department_id, salary);
```

This index is ordered according to:

```text
department_id
      ↓
salary
```

---

# 82. Leftmost Prefix Principle

For a composite index:

```text
(department_id, salary)
```

queries using:

```text
department_id
```

can generally benefit from the leading portion of the index.

Example:

```sql
WHERE department_id = 10
```

is a natural use case.

A query filtering only on:

```sql
WHERE salary > 50000
```

may not be able to use that composite index efficiently for the salary condition alone.

Exact optimizer behavior varies by DBMS.

---

# 83. Index Column Order

Suppose:

```text
(department_id, salary)
```

versus:

```text
(salary, department_id)
```

The order matters.

For queries like:

```sql
WHERE department_id = 10
AND salary > 50000;
```

a composite index beginning with `department_id` can be a strong candidate.

But the best order depends on:

```text
Query patterns
Selectivity
Equality vs range predicates
Sort requirements
Join patterns
```

Don't choose index order using a single universal rule.

---

# 84. SARGable Queries

## Technical Definition

A **SARGable** predicate is one that allows the database to efficiently use an index through an appropriate search argument.

## Easy Meaning

Write conditions in a way that lets the database use the indexed column effectively.

---

# 85. Non-SARGable Example

Suppose:

```sql
WHERE YEAR(order_date) = 2026
```

The function is applied to the column.

Depending on the DBMS and index structure, this can prevent efficient use of a normal index on `order_date`.

---

# 86. More Index-Friendly Form

Instead, use a range:

```sql
WHERE order_date >= '2026-01-01'
  AND order_date < '2027-01-01'
```

This expresses the condition directly on the indexed column.

---

# 87. Another Non-SARGable Pattern

Potentially problematic:

```sql
WHERE LOWER(email) = 'alice@example.com'
```

If a normal index exists on:

```text
email
```

the function may prevent normal index usage.

Possible solutions include:

```text
Appropriate collation
Functional/expression index
Computed/generated column
Normalized stored value
```

depending on the database.

---

# 88. WHERE Optimization

Good:

```sql
SELECT employee_id, employee_name
FROM employees
WHERE department_id = 10;
```

Potentially less efficient:

```sql
SELECT *
FROM employees;
```

The first query:

```text
Returns fewer columns
Returns filtered rows
```

The second:

```text
May read and transfer much more data
```

---

# 89. Filter Early

Suppose:

```text
10 million orders
```

but only:

```text
1,000 orders
```

are required.

Filtering early can reduce the amount of data processed by later operations.

Conceptually:

```text
10,000,000 rows
       ↓
WHERE
       ↓
1,000 rows
       ↓
JOIN / GROUP / SORT
```

Modern optimizers often push filters down automatically when safe.

---

# 90. JOIN Optimization

Example:

```sql
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

Important considerations:

```text
✓ Index join columns where appropriate
✓ Filter unnecessary rows
✓ Return only required columns
✓ Check join cardinality
✓ Examine execution plan
```

---

# 91. Index Foreign Keys Where Appropriate

Suppose:

```text
orders.customer_id
```

references:

```text
customers.customer_id
```

An index on:

```text
orders.customer_id
```

can be useful for joins and other queries.

Example:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

Whether it is beneficial depends on workload and DBMS.

---

# 92. Avoid Unnecessary JOINs

Bad:

```sql
SELECT
    o.order_id
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

If no column or condition from `customers` is actually needed, the join may be unnecessary.

Better:

```sql
SELECT
    order_id
FROM orders;
```

---

# 93. GROUP BY Optimization

Suppose:

```sql
SELECT
    department_id,
    COUNT(*)
FROM employees
GROUP BY department_id;
```

The database must group rows.

Potential performance considerations include:

```text
Input row count
Available indexes
Memory
Sort/hash strategy
Data distribution
```

Use:

```text
EXPLAIN
```

to see what the optimizer chooses.

---

# 94. ORDER BY Optimization

Sorting can be expensive.

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

The database may need to sort many rows.

If an appropriate index can provide the requested ordering, the database may be able to avoid an explicit sort.

But whether that is possible depends on:

```text
Index definition
Filtering
Ordering direction
Query structure
DBMS
```

---

# 95. LIMIT Optimization

Suppose:

```sql
SELECT *
FROM products
ORDER BY price DESC
LIMIT 10;
```

Only 10 rows are required.

An appropriate index can sometimes allow the database to find the top rows efficiently.

For example, an index involving:

```text
price
```

may help.

---

# 96. OFFSET Pagination Problem

Consider:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 100000;
```

The database may need to process/skip a large number of rows before returning the requested page.

This can become slow for deep pages.

---

# 97. Keyset / Seek Pagination

Instead of:

```sql
LIMIT 20 OFFSET 100000
```

use a continuation key.

Example:

```sql
SELECT *
FROM products
WHERE product_id > 100000
ORDER BY product_id
LIMIT 20;
```

This is commonly called:

```text
Keyset pagination
Seek pagination
```

It can scale much better for deep pagination when the ordering key is appropriate and indexed.

---

# 98. Subquery Optimization

Consider:

```sql
SELECT *
FROM employees
WHERE department_id IN
(
    SELECT department_id
    FROM departments
    WHERE location = 'Delhi'
);
```

Depending on the database, the optimizer may transform this into a semi-join or another equivalent plan.

You should not automatically assume:

```text
JOIN is always faster than subquery
```

Instead:

```text
Check EXPLAIN / execution plan.
```

---

# 99. EXISTS

For existence checks:

```sql
SELECT c.customer_id
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

`EXISTS` expresses:

> Does at least one matching row exist?

This can be efficient, especially when supported by a suitable index.

---

# 100. CTE Optimization

CTEs improve readability:

```sql
WITH high_value_orders AS (
    SELECT *
    FROM orders
    WHERE total_amount > 10000
)
SELECT *
FROM high_value_orders;
```

But:

> A CTE is not automatically faster than an equivalent subquery.

Materialization behavior varies by database and version.

Some systems can inline CTEs; others may materialize them in certain situations.

Always check the execution plan when performance matters.

---

# 101. Avoid SELECT *

Instead of:

```sql
SELECT *
FROM employees;
```

prefer:

```sql
SELECT
    employee_id,
    employee_name,
    department_id
FROM employees;
```

Benefits can include:

```text
✓ Less data transferred
✓ Less memory
✓ Less I/O
✓ More stable application interfaces
✓ Potentially better use of covering indexes
```

---

# 102. Functions on Indexed Columns

Potentially problematic:

```sql
WHERE YEAR(order_date) = 2026
```

Prefer:

```sql
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
```

This is especially useful when `order_date` has a normal B-tree index.

---

# 103. Implicit Type Conversion

Suppose:

```text
employee_id
```

is an integer.

Avoid comparing it to incompatible string data:

```sql
WHERE employee_id = '101';
```

Depending on the DBMS, implicit conversion may occur.

Prefer matching types:

```sql
WHERE employee_id = 101;
```

Implicit conversion can sometimes:

```text
Increase CPU work
Prevent efficient index usage
Cause unexpected behavior
```

---

# 104. OR vs UNION

Sometimes:

```sql
WHERE department_id = 10
   OR department_id = 20
```

can be rewritten as:

```sql
SELECT *
FROM employees
WHERE department_id = 10

UNION ALL

SELECT *
FROM employees
WHERE department_id = 20;
```

But:

> Do not assume `UNION ALL` is always faster.

The optimizer may already optimize the original query effectively.

Also:

```text
UNION
```

removes duplicates.

```text
UNION ALL
```

does not remove duplicates and is usually cheaper when duplicate elimination isn't required.

---

# 105. UNION vs UNION ALL

## UNION

```sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
```

Duplicates are removed.

---

## UNION ALL

```sql
SELECT city FROM customers
UNION ALL
SELECT city FROM suppliers;
```

Duplicates are retained.

Therefore:

```text
UNION
→ Combine + remove duplicates

UNION ALL
→ Combine without duplicate removal
```

When duplicate removal isn't required, `UNION ALL` is usually preferable.

---

# 106. DISTINCT and Performance

Example:

```sql
SELECT DISTINCT department_id
FROM employees;
```

The database must eliminate duplicates.

This may require:

```text
Sorting
or
Hashing
```

depending on the execution plan.

Don't use `DISTINCT` just to hide duplicate rows caused by an incorrect join.

First understand why duplicates exist.

---

# 107. Avoid Accidental Cartesian Products

Bad:

```sql
SELECT *
FROM employees e
JOIN departments d;
```

If no join condition is supplied and the DBMS permits it as a cross join, every employee can be combined with every department.

If:

```text
Employees = 10,000
Departments = 100
```

potential combinations:

```text
10,000 × 100 = 1,000,000
```

Use the correct join condition.

---

# 108. Query Execution Example

Query:

```sql
SELECT
    c.customer_name,
    COUNT(o.order_id) AS order_count
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_date >= '2026-01-01'
GROUP BY c.customer_id, c.customer_name
ORDER BY order_count DESC;
```

A simplified conceptual processing flow is:

```text
FROM
 ↓
JOIN
 ↓
WHERE
 ↓
GROUP BY
 ↓
SELECT
 ↓
ORDER BY
```

But this is the **logical processing order**, not necessarily the physical order used internally by the database.

---

# 109. SQL Logical Processing Order

A commonly taught logical order is:

```text
1. FROM
2. JOIN
3. ON
4. WHERE
5. GROUP BY
6. HAVING
7. SELECT
8. DISTINCT
9. ORDER BY
10. LIMIT / OFFSET
```

This helps explain why aliases sometimes cannot be referenced in certain clauses.

---

# 110. Example of Logical Order

Query:

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
WHERE salary > 50000
GROUP BY department_id
HAVING COUNT(*) > 5
ORDER BY employee_count DESC;
```

Conceptually:

```text
FROM employees
      ↓
WHERE salary > 50000
      ↓
GROUP BY department_id
      ↓
HAVING COUNT(*) > 5
      ↓
SELECT department_id, COUNT(*)
      ↓
ORDER BY employee_count
```

---

# 111. WHERE vs HAVING

## WHERE

Filters rows before grouping.

```sql
WHERE salary > 50000
```

## HAVING

Filters groups after aggregation.

```sql
HAVING COUNT(*) > 5
```

Memory:

```text
WHERE
→ Rows

HAVING
→ Groups
```

---

# 112. Physical Execution

The database does not necessarily execute exactly in the logical order.

For example, it may:

```text
Use index
 ↓
Filter rows
 ↓
Join
 ↓
Aggregate
 ↓
Sort
```

The optimizer chooses the physical strategy.

---

# 113. Query Optimization Example

Suppose:

```sql
SELECT *
FROM orders
WHERE customer_id = 101;
```

Without index:

```text
Table Scan
 ↓
Check every row
 ↓
Return customer 101 rows
```

With:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

the database may choose an index-based access path.

Conceptually:

```text
Index
 ↓
Find customer_id = 101
 ↓
Fetch matching rows
```

---

# 114. Covering Index

## Technical Definition

A **covering index** contains all columns required by a particular query, allowing the database to answer the query from the index without needing to fetch the base table rows.

Example query:

```sql
SELECT customer_id, order_date
FROM orders
WHERE customer_id = 101;
```

Potential index:

```sql
CREATE INDEX idx_orders_customer_date
ON orders(customer_id, order_date);
```

The index contains both:

```text
customer_id
order_date
```

so it may be able to cover the query.

Exact behavior depends on the DBMS.

---

# 115. Index Selectivity

## Definition

Selectivity describes how effectively a condition narrows down rows.

High selectivity:

```text
1,000,000 rows
      ↓
10 matching rows
```

Low selectivity:

```text
1,000,000 rows
      ↓
900,000 matching rows
```

Indexes tend to be more useful for selective predicates, though there are important exceptions.

---

# 116. Cardinality

## Technical Definition

Cardinality refers to the number of rows or distinct values, depending on context.

Examples:

```text
Table cardinality
→ Number of rows

Column cardinality
→ Number of distinct values
```

Example:

```text
Gender:
Male
Female
```

Low distinct-value cardinality.

```text
Email:
alice@example.com
bob@example.com
...
```

Potentially high distinct-value cardinality.

---

# 117. Query Optimization and Data Distribution

Suppose:

```text
status
------
ACTIVE
INACTIVE
```

If:

```text
95% = ACTIVE
5% = INACTIVE
```

an index may be more useful for:

```sql
WHERE status = 'INACTIVE'
```

than:

```sql
WHERE status = 'ACTIVE'
```

The optimizer uses statistics to reason about such distributions.

---

# 118. Avoid Functions When Range Predicates Work

Bad:

```sql
SELECT *
FROM orders
WHERE MONTH(order_date) = 8;
```

This asks for August but applies a function to every date.

Better:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-08-01'
  AND order_date < '2026-09-01';
```

This can make normal index access more straightforward.

---

# 119. Avoid Leading Wildcards When Possible

Query:

```sql
WHERE name LIKE '%john%'
```

A normal B-tree index generally cannot efficiently seek to the beginning because the pattern starts with `%`.

Potentially more index-friendly:

```sql
WHERE name LIKE 'john%'
```

because the beginning of the value is known.

For true substring search, specialized indexes/search systems may be more appropriate.

---

# 120. Temporary Tables and Performance

Temporary tables can sometimes help when:

```text
✓ Intermediate result is reused
✓ Complex processing is broken into stages
✓ Materializing a result is beneficial
```

Example:

```sql
CREATE TEMPORARY TABLE high_value_orders AS
SELECT *
FROM orders
WHERE total_amount > 10000;
```

Then:

```sql
SELECT *
FROM high_value_orders;
```

But temporary tables also have:

```text
Creation cost
Storage cost
Potential indexing cost
```

Use them when they solve a real problem.

---

# 121. Query Optimization with Materialized Results

Some systems support **materialized views**.

Unlike a normal view:

```text
VIEW
→ Stores query definition
→ Usually computes when queried
```

A materialized view:

```text
→ Stores the query result
→ Can be refreshed
```

Useful for:

```text
Reporting
Analytics
Expensive aggregations
```

---

# 122. Query Optimization Checklist

Before optimizing a query:

```text
1. Is the query logically correct?
2. How many rows does it process?
3. Which tables are involved?
4. Which columns are filtered?
5. Which columns are joined?
6. Which indexes exist?
7. What does EXPLAIN show?
8. Are estimated and actual rows different?
9. Is there unnecessary sorting?
10. Is there unnecessary grouping?
11. Is SELECT * being used?
12. Are functions applied to indexed columns?
13. Are implicit conversions occurring?
14. Is there an unnecessary JOIN?
15. Is pagination inefficient?
16. Are statistics current?
```

---

# 123. Bad Query Example

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026
AND customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE country = 'India'
)
ORDER BY order_date DESC;
```

Potential issues:

```text
SELECT *
YEAR(order_date)
Subquery
Possible sorting
Potential missing indexes
```

---

# 124. Better Query

A possible rewrite:

```sql
SELECT
    o.order_id,
    o.customer_id,
    o.order_date,
    o.total_amount
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.country = 'India'
  AND o.order_date >= '2026-01-01'
  AND o.order_date < '2027-01-01'
ORDER BY o.order_date DESC;
```

Potential supporting indexes could include:

```sql
CREATE INDEX idx_customers_country_customer
ON customers(country, customer_id);
```

and possibly:

```sql
CREATE INDEX idx_orders_customer_date
ON orders(customer_id, order_date);
```

But the correct indexes must be validated against the actual workload and execution plan.

---

# 125. Query Optimization Workflow

Use this process:

```text
Slow Query
    ↓
Measure
    ↓
EXPLAIN / EXPLAIN ANALYZE
    ↓
Identify bottleneck
    ↓
Check row estimates
    ↓
Check indexes
    ↓
Check joins
    ↓
Check filters
    ↓
Rewrite if needed
    ↓
Test again
    ↓
Compare performance
```

---

# 126. Never Optimize Blindly

Bad approach:

```text
Query is slow
    ↓
Create 20 indexes
```

This can make things worse.

Better:

```text
Query is slow
    ↓
Measure
    ↓
Find bottleneck
    ↓
Apply targeted change
    ↓
Measure again
```

---

# 127. Query Optimization Metrics

Useful metrics include:

```text
Execution time
CPU time
Rows examined
Rows returned
Logical reads
Physical reads
Memory usage
Temporary space
Sort operations
Number of loops
Actual vs estimated rows
```

The exact metrics depend on the database.

---

# 128. Estimated vs Actual Rows

Suppose optimizer estimates:

```text
Estimated rows = 10
```

but execution finds:

```text
Actual rows = 1,000,000
```

This is a major estimation error.

Possible causes:

```text
Stale statistics
Data skew
Correlated columns
Complex predicates
Optimizer limitations
```

This can lead to a poor execution plan.

---

# 129. Join Order

Suppose:

```text
A = 10 million rows
B = 1,000 rows
C = 10 rows
```

The order in which joins are processed can greatly affect intermediate result sizes.

A good optimizer tries to choose an efficient order.

You should generally let the optimizer choose unless you have a specific reason to influence the plan.

---

# 130. Predicate Pushdown

## Technical Definition

Predicate pushdown means applying filters as close as possible to the data source to reduce the number of rows processed by later operators.

Example:

```text
10 million rows
       ↓
Filter
       ↓
100,000 rows
       ↓
Join
```

instead of:

```text
10 million rows
       ↓
Join
       ↓
Filter
```

when the latter would create much more unnecessary work.

Modern optimizers often perform this automatically when semantically safe.

---

# 131. Projection Pushdown

Projection means selecting only required columns.

Instead of carrying:

```text
20 columns
```

through every operation, the optimizer may only carry:

```text
4 required columns
```

This can reduce:

```text
Memory
I/O
Data movement
```

---

# 132. Query Optimization and Joins

Consider:

```sql
SELECT
    o.order_id,
    c.customer_name
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.country = 'India';
```

Potential considerations:

```text
customers.country → filtering
customers.customer_id → join
orders.customer_id → join
```

Potential indexes:

```sql
CREATE INDEX idx_customers_country_customer
ON customers(country, customer_id);
```

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

Again:

> The execution plan determines whether these indexes actually help.

---

# 133. Trigger vs Cursor

| Trigger                                | Cursor                                  |
| -------------------------------------- | --------------------------------------- |
| Automatically executes due to an event | Explicitly used to iterate through rows |
| Event-driven                           | Row-by-row processing                   |
| Commonly tied to INSERT/UPDATE/DELETE  | Used inside procedural code             |
| Good for auditing                      | Good for procedural row processing      |
| Can create hidden side effects         | Can create performance overhead         |

---

# 134. Trigger vs Stored Procedure

| Trigger                                | Stored Procedure            |
| -------------------------------------- | --------------------------- |
| Automatically executes                 | Explicitly called           |
| Event-driven                           | Procedure-driven            |
| Usually tied to table events           | Can perform many operations |
| No normal explicit call by application | Application can call it     |
| Useful for auditing                    | Useful for workflows        |

---

# 135. Function vs Trigger

| Function                                                    | Trigger                           |
| ----------------------------------------------------------- | --------------------------------- |
| Explicitly invoked or used in expressions depending on DBMS | Automatically invoked             |
| Returns a result                                            | Performs automatic actions        |
| Useful for reusable calculations                            | Useful for event-driven behavior  |
| Usually predictable from query                              | Can introduce hidden side effects |

---

# 136. Cursor vs Set-Based SQL

```text
CURSOR
→ Row 1
→ Row 2
→ Row 3
→ Row 4

SET-BASED SQL
→ Process the set together
```

General rule:

> Prefer set-based SQL unless row-by-row processing is genuinely necessary.

---

# 137. Security + Query Optimization

Security and performance can sometimes interact.

For example:

```text
Row-Level Security
Views
Encryption
Auditing
```

may add processing overhead depending on implementation.

But:

> Never remove an important security control simply because it adds some overhead without measuring the actual bottleneck and evaluating safer alternatives.

---

# 138. Security Checklist

```text
✓ Strong authentication
✓ Least privilege
✓ Roles
✓ Parameterized queries
✓ Secure credentials
✓ Encryption in transit
✓ Encryption at rest where appropriate
✓ Auditing
✓ Secure backups
✓ Regular patching
✓ Avoid unnecessary public database exposure
✓ Restrict administrative accounts
✓ Protect sensitive data
```

---

# 139. Trigger Checklist

Before creating a trigger, ask:

```text
1. Why is the trigger needed?
2. Can a constraint solve the problem?
3. Can application logic solve it more clearly?
4. Will it affect every row?
5. Could it create recursion?
6. Could it create unexpected side effects?
7. Will it slow writes?
8. Does it need auditing?
9. Is the logic documented?
```

---

# 140. Cursor Checklist

Before using a cursor:

```text
1. Can UPDATE solve it?
2. Can INSERT ... SELECT solve it?
3. Can JOIN solve it?
4. Can CASE solve it?
5. Can a CTE solve it?
6. Can a window function solve it?
7. Is row-by-row processing genuinely required?
```

If the answer is no to the final question:

```text
Avoid the cursor.
```

---

# 141. Error Handling Checklist

```text
✓ Detect errors
✓ Use transactions where appropriate
✓ ROLLBACK on failure
✓ COMMIT only after success
✓ Log important failures
✓ Don't expose sensitive internal errors to users
✓ Return meaningful application-level errors
✓ Test failure scenarios
```

---

# 142. Query Optimization Checklist

```text
✓ Check EXPLAIN
✓ Use EXPLAIN ANALYZE when appropriate
✓ Check indexes
✓ Check row estimates
✓ Avoid unnecessary columns
✓ Avoid unnecessary joins
✓ Filter efficiently
✓ Use appropriate data types
✓ Avoid unnecessary functions on indexed columns
✓ Avoid implicit conversions
✓ Check pagination
✓ Check sorting
✓ Check grouping
✓ Maintain statistics
✓ Measure before and after changes
```

---

# 143. Complete Concept Map

```text
SQL ADVANCED
│
├── TRIGGERS
│   │
│   ├── BEFORE
│   ├── AFTER
│   ├── INSERT
│   ├── UPDATE
│   ├── DELETE
│   ├── OLD
│   ├── NEW
│   ├── ROW LEVEL
│   └── STATEMENT LEVEL
│
├── CURSORS
│   │
│   ├── DECLARE
│   ├── OPEN
│   ├── FETCH
│   ├── PROCESS
│   └── CLOSE
│
├── ERROR HANDLING
│   │
│   ├── Syntax Errors
│   ├── Constraint Errors
│   ├── Data Errors
│   ├── Permission Errors
│   ├── Exception Handling
│   ├── Transactions
│   ├── COMMIT
│   └── ROLLBACK
│
├── SQL SECURITY
│   │
│   ├── Authentication
│   ├── Authorization
│   ├── Users
│   ├── Roles
│   ├── GRANT
│   ├── REVOKE
│   ├── Least Privilege
│   ├── SQL Injection
│   ├── Encryption
│   ├── Views
│   ├── RLS
│   └── Auditing
│
└── QUERY PERFORMANCE
    │
    ├── Query Parsing
    ├── Query Rewriting
    ├── Optimization
    ├── Execution Plan
    ├── EXPLAIN
    ├── EXPLAIN ANALYZE
    ├── Table Scan
    ├── Index Access
    ├── Nested Loop
    ├── Hash Join
    ├── Merge Join
    ├── Statistics
    ├── Cardinality
    ├── Selectivity
    ├── SARGability
    ├── Index Design
    ├── Composite Index
    ├── Covering Index
    ├── Join Optimization
    ├── Sorting
    ├── Grouping
    ├── Pagination
    └── Query Rewriting
```

---

# 144. Interview Questions

## Triggers

### Q1. What is a trigger?

A trigger is a database object that automatically executes when a specified database event occurs.

### Q2. What are common trigger events?

```text
INSERT
UPDATE
DELETE
```

### Q3. What is the difference between BEFORE and AFTER?

```text
BEFORE
→ Runs before the triggering operation completes.

AFTER
→ Runs after the triggering operation.
```

### Q4. What are OLD and NEW?

```text
OLD
→ Previous row value.

NEW
→ New row value.
```

### Q5. What are triggers commonly used for?

```text
Auditing
History
Validation
Automatic actions
Business rules
```

---

# 145. Cursor Interview Questions

### Q1. What is a cursor?

A mechanism for processing a result set row by row.

### Q2. What are cursor steps?

```text
DECLARE
OPEN
FETCH
PROCESS
CLOSE
```

### Q3. Why are cursors generally slower?

Because they perform row-by-row processing rather than exploiting SQL's set-based processing model.

### Q4. What should you use instead of a cursor when possible?

```text
UPDATE
INSERT ... SELECT
JOIN
CTE
CASE
Window functions
Set-based SQL
```

---

# 146. Error Handling Interview Questions

### Q1. Why is error handling important?

To prevent failures from leaving the database in an inconsistent state and to provide controlled failure behavior.

### Q2. What is ROLLBACK?

It reverses changes made within the current transaction, subject to transaction semantics.

### Q3. What is COMMIT?

It makes a transaction's changes durable according to the database's transaction rules.

### Q4. What is exception handling?

A mechanism for detecting and responding to runtime/database errors in procedural SQL.

---

# 147. Security Interview Questions

### Q1. Authentication vs authorization?

```text
Authentication
→ Who are you?

Authorization
→ What can you do?
```

### Q2. What is least privilege?

Give users only the permissions necessary for their tasks.

### Q3. What is SQL injection?

A vulnerability where untrusted input changes the intended SQL statement.

### Q4. How do you prevent SQL injection?

Primarily:

```text
Parameterized queries
Prepared statements
Safe database APIs
Input validation as defense-in-depth
Least privilege
```

---

# 148. Query Execution Interview Questions

### Q1. What is an execution plan?

The strategy chosen by the database to execute a query.

### Q2. What does EXPLAIN do?

It shows the query plan or optimizer information, depending on the database.

### Q3. What is EXPLAIN ANALYZE?

It generally executes the query while providing actual runtime execution information, depending on the DBMS.

### Q4. What is a table scan?

Reading a large portion or all of a table to find qualifying rows.

### Q5. What is an index seek?

Navigating an index directly toward a specific key or range.

---

# 149. Query Optimization Interview Questions

### Q1. What is query optimization?

Finding an efficient execution strategy while preserving the query result.

### Q2. Why are indexes useful?

They can reduce the amount of data the database must examine for suitable queries.

### Q3. Can too many indexes be bad?

Yes.

They:

```text
Consume storage
Slow INSERT
Slow UPDATE
Slow DELETE
Increase maintenance
```

### Q4. What is a composite index?

An index containing multiple columns.

Example:

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

### Q5. What is a covering index?

An index containing all columns needed by a query, potentially allowing the query to be answered from the index alone.

---

# 150. Final Revision — Triggers

```text
TRIGGER
→ Automatically runs because of an event.

BEFORE
→ Before operation.

AFTER
→ After operation.

INSERT
→ New row.

UPDATE
→ OLD + NEW.

DELETE
→ Old row.

OLD
→ Previous value.

NEW
→ New value.
```

---

# 151. Final Revision — Cursors

```text
CURSOR
→ Process rows one by one.

DECLARE
→ Define cursor.

OPEN
→ Start cursor.

FETCH
→ Get next row.

PROCESS
→ Perform operation.

CLOSE
→ Close cursor.
```

---

# 152. Final Revision — Error Handling

```text
ERROR
 ↓
DETECT
 ↓
HANDLE
 ↓
ROLLBACK if necessary
 ↓
LOG / RETURN ERROR
```

Remember:

```text
COMMIT
→ Save transaction changes.

ROLLBACK
→ Undo transaction changes.
```

---

# 153. Final Revision — Security

```text
AUTHENTICATION
→ Who are you?

AUTHORIZATION
→ What can you do?

GRANT
→ Give permission.

REVOKE
→ Remove permission.

ROLE
→ Group of permissions.

LEAST PRIVILEGE
→ Minimum required access.

SQL INJECTION
→ Untrusted input changes SQL.

PARAMETERIZED QUERY
→ Keep SQL structure separate from data.
```

---

# 154. Final Revision — Query Execution

```text
SQL
 ↓
PARSE
 ↓
VALIDATE
 ↓
REWRITE
 ↓
OPTIMIZE
 ↓
EXECUTION PLAN
 ↓
EXECUTE
 ↓
RESULT
```

---

# 155. Final Revision — Query Optimization

```text
SLOW QUERY
   ↓
EXPLAIN
   ↓
CHECK PLAN
   ↓
CHECK ROW ESTIMATES
   ↓
CHECK INDEXES
   ↓
CHECK JOINS
   ↓
CHECK FILTERS
   ↓
CHECK SORT/GROUP
   ↓
REWRITE IF NEEDED
   ↓
TEST
   ↓
MEASURE AGAIN
```

---

# 156. Most Important Performance Rules

```text
1. Measure before optimizing.

2. Use EXPLAIN.

3. Don't create indexes blindly.

4. Index important filtering/join columns when appropriate.

5. Use composite indexes based on real query patterns.

6. Avoid unnecessary SELECT *.

7. Avoid unnecessary JOINs.

8. Avoid functions on indexed columns when they prevent efficient access.

9. Avoid implicit type conversions.

10. Prefer set-based SQL over cursors.

11. Keep statistics healthy.

12. Check actual vs estimated rows.

13. Optimize pagination for large datasets.

14. Don't assume JOIN is always faster than a subquery.

15. Don't assume an index is always better than a scan.

16. Measure the query after every significant optimization.
```

---

# 157. Ultimate Mental Model

```text
TRIGGER
"What should happen AUTOMATICALLY
when data changes?"

CURSOR
"How do I PROCESS ROWS ONE BY ONE?"

ERROR HANDLING
"What should happen WHEN SOMETHING FAILS?"

SQL SECURITY
"WHO can access WHAT and DO WHAT?"

QUERY EXECUTION
"HOW does the database execute my SQL?"

QUERY OPTIMIZATION
"HOW can the database execute it MORE EFFICIENTLY?"
```

---

# 158. One-Page Revision

```text
┌──────────────────────────────────────────────┐
│                 SQL ADVANCED                 │
├──────────────────────────────────────────────┤
│                                              │
│ TRIGGERS                                     │
│ → Automatic event-based execution            │
│ → BEFORE / AFTER                             │
│ → INSERT / UPDATE / DELETE                   │
│ → OLD / NEW                                  │
│                                              │
│ CURSORS                                      │
│ → Row-by-row processing                      │
│ → DECLARE → OPEN → FETCH → CLOSE             │
│ → Prefer set-based SQL when possible         │
│                                              │
│ ERROR HANDLING                               │
│ → Detect → Handle → Rollback/Log             │
│ → Transactions + Exceptions                  │
│                                              │
│ SECURITY                                     │
│ → Authentication                             │
│ → Authorization                              │
│ → Users / Roles                              │
│ → GRANT / REVOKE                             │
│ → Least Privilege                            │
│ → SQL Injection Prevention                   │
│ → Encryption / Auditing                     │
│                                              │
│ QUERY EXECUTION                              │
│ → Parse → Validate → Rewrite                 │
│ → Optimize → Plan → Execute                 │
│                                              │
│ QUERY OPTIMIZATION                           │
│ → EXPLAIN                                    │
│ → Indexes                                    │
│ → Statistics                                 │
│ → Cardinality                                │
│ → Selectivity                                │
│ → SARGability                                │
│ → Join Optimization                          │
│ → Sorting / Grouping                         │
│ → Pagination                                 │
│ → Measure Before/After                       │
│                                              │
└──────────────────────────────────────────────┘
```

---

# 159. Final Memory Formulas

```text
TRIGGER
= Automatic Action

CURSOR
= Row-by-Row Processing

PROCEDURE
= Reusable Database Workflow

FUNCTION
= Reusable Calculation / Result

TRANSACTION
= Group of Operations

ERROR HANDLING
= Controlled Failure

SECURITY
= Authentication + Authorization + Protection

EXECUTION PLAN
= Database's Strategy

INDEX
= Faster Access Path for Suitable Queries

OPTIMIZATION
= Same Result + Better Execution Strategy
```

> **Important:** SQL syntax and behavior for triggers, cursors, procedural error handling, execution plans, indexes, and security vary across **MySQL, PostgreSQL, SQL Server, and Oracle**. For revision, learn the concepts first; when writing production SQL, always use the syntax and optimizer behavior of your specific DBMS.
