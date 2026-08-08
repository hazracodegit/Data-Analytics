# Database Fundamentals

> Complete database fundamentals revision notes for **SQL, Data Analytics, Backend Development, Data Engineering, and Database Management**.

---

# 1. What is Data?

**Data** is a collection of facts, observations, or values.

Examples:

```text
Name      = Rahul
Age       = 22
Salary    = 50000
City      = Hyderabad
```

Data can be:

* Numbers
* Text
* Dates
* Images
* Audio
* Video
* Boolean values
* Sensor readings
* Transactions
* Customer information

---

# 2. What is a Database?

A **database** is an organized collection of data that allows data to be stored, managed, retrieved, updated, and analyzed efficiently.

Example:

```text
Company Database
│
├── Employees
├── Departments
├── Customers
├── Products
├── Orders
└── Payments
```

Instead of storing thousands or millions of records in separate files, a database provides a structured way to manage them.

---

# 3. Why Do We Need Databases?

Without a database, organizations may store data in:

```text
Excel files
CSV files
Text files
JSON files
Documents
```

This becomes difficult when data grows.

A database helps with:

* Large-scale data storage
* Fast data retrieval
* Data organization
* Data security
* Data consistency
* Concurrent access
* Data relationships
* Data integrity
* Backup and recovery
* Transaction management
* Data analysis

---

# 4. Database Example

Consider an online shopping application.

It needs to store:

```text
Customers
Products
Orders
Payments
Addresses
Reviews
```

A database can organize this information:

```text
Database
│
├── customers
├── products
├── orders
├── order_items
├── payments
├── addresses
└── reviews
```

These tables can be connected using relationships.

---

# 5. Database Management System

## DBMS

**DBMS = Database Management System**

A DBMS is software used to create, manage, access, and control databases.

Examples:

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server
* SQLite
* MariaDB

A DBMS acts as an interface between applications/users and stored data.

```text
User / Application
        ↓
      DBMS
        ↓
    Database
```

---

# 6. Main Responsibilities of a DBMS

A DBMS manages:

```text
Data Storage
Data Retrieval
Data Modification
Data Security
Data Integrity
Transactions
Concurrency
Backup
Recovery
Access Control
```

---

# 7. DBMS Components

A typical database system contains:

```text
Database System
│
├── Database
├── DBMS Software
├── Users
├── Applications
├── Query Processor
├── Storage Manager
├── Transaction Manager
└── Security / Authorization
```

---

# 8. Database Users

Different people interact with databases differently.

## Database Administrator

**DBA = Database Administrator**

Responsible for:

* Database configuration
* Security
* User permissions
* Backup
* Recovery
* Monitoring
* Performance
* Maintenance

---

## Database Developer

Works on:

* SQL
* Stored procedures
* Functions
* Triggers
* Database design
* Application-database integration

---

## Data Analyst

Uses databases to:

* Extract data
* Clean data
* Transform data
* Aggregate data
* Calculate metrics
* Generate reports
* Perform analysis

---

## Data Engineer

Works with:

* Data pipelines
* ETL/ELT
* Data warehouses
* Data lakes
* Large-scale data processing
* Database infrastructure

---

## Application Developer

Uses databases to store and retrieve application data.

Example:

```text
Python Application
       ↓
Database Driver
       ↓
Database
```

---

# 9. Database Architecture

A basic application architecture:

```text
User
 ↓
Application
 ↓
Database
```

Example:

```text
Browser
   ↓
Frontend
   ↓
Backend API
   ↓
Database
```

For example:

```text
React
  ↓
Python / Java / Node.js
  ↓
PostgreSQL / MySQL
```

---

# 10. Database Server

A database server is a system that hosts and manages a database service.

Example:

```text
Application
     ↓
Database Server
     ↓
Database
     ↓
Tables
```

The database server receives requests and returns results.

---

# 11. Database Client

A database client is a tool or application used to connect to a database.

Examples include:

* Command-line clients
* Database IDEs
* Application programs
* BI tools
* Administration tools

Conceptually:

```text
Database Client
      ↓
Database Server
```

---

# 12. Database Models

A **database model** describes how data is organized and related.

Major models include:

```text
Database Models
│
├── Hierarchical
├── Network
├── Relational
├── Object-Oriented
├── Document
├── Key-Value
├── Graph
└── Column-Family
```

---

# 13. Hierarchical Database Model

Data is organized like a tree.

```text
Company
│
├── IT
│   ├── Employee 1
│   └── Employee 2
│
└── HR
    ├── Employee 3
    └── Employee 4
```

Relationship:

```text
Parent
  │
  ├── Child
  ├── Child
  └── Child
```

It works well for hierarchical data but is less flexible for complex relationships.

---

# 14. Network Database Model

The network model allows records to have multiple relationships.

Conceptually:

```text
A ───── B
│ ╲     │
│  ╲    │
C ───── D
```

It can represent many-to-many relationships.

---

# 15. Relational Database Model

The **relational model** stores data in tables.

Example:

```text
employees

+----+--------+------------+
| id | name   | department |
+----+--------+------------+
| 1  | Rahul  | IT         |
| 2  | Priya  | HR         |
| 3  | Arun   | IT         |
+----+--------+------------+
```

Tables can be related using keys.

Examples of relational databases:

* PostgreSQL
* MySQL
* Oracle Database
* SQL Server
* SQLite

---

# 16. Non-Relational Databases

Non-relational databases are commonly called **NoSQL databases**.

They may use different data models such as:

* Document
* Key-value
* Graph
* Wide-column

Examples:

```text
MongoDB     → Document
Redis       → Key-Value
Neo4j       → Graph
Cassandra   → Wide-Column
```

---

# 17. Relational vs Non-Relational Databases

| Relational                                  | Non-Relational                                    |
| ------------------------------------------- | ------------------------------------------------- |
| Tables                                      | Various data models                               |
| Rows and columns                            | Documents/key-value/graph/etc.                    |
| Strong relationships                        | Relationships handled differently                 |
| Structured schema commonly used             | Often more flexible schema                        |
| SQL commonly used                           | Query language depends on database                |
| Excellent for structured transactional data | Useful for various distributed/flexible workloads |

Neither is universally better.

The choice depends on the application.

---

# 18. What is a Table?

A table stores related data in rows and columns.

Example:

```text
employees

+----+--------+--------+
| id | name   | salary |
+----+--------+--------+
| 1  | Rahul  | 50000  |
| 2  | Priya  | 60000  |
| 3  | Arun   | 70000  |
+----+--------+--------+
```

---

# 19. Row

A row represents one record.

```text
1 | Rahul | 50000
```

This represents one employee.

A row can also be called a:

```text
Record
Tuple
```

---

# 20. Column

A column represents an attribute.

Example:

```text
id
name
salary
```

Each column generally has:

* Name
* Data type
* Constraints

---

# 21. Table, Row, Column

Remember:

```text
Table
│
├── Column → Attribute
│
├── Column → Attribute
│
└── Row → Record
```

Example:

```text
+----+--------+--------+
| id | name   | salary |
+----+--------+--------+
| 1  | Rahul  | 50000  | ← Row
| 2  | Priya  | 60000  | ← Row
+----+--------+--------+
  ↑       ↑       ↑
Columns
```

---

# 22. Entity

An **entity** is something about which information is stored.

Examples:

```text
Student
Employee
Customer
Product
Order
Department
```

Example:

```text
Entity: Customer

Attributes:
- customer_id
- name
- email
- phone
- city
```

---

# 23. Attribute

An attribute is a property of an entity.

For an employee:

```text
Employee
│
├── employee_id
├── name
├── email
├── salary
├── department
└── joining_date
```

These are attributes.

In a relational database, attributes generally correspond to columns.

---

# 24. Record

A record is one complete collection of attribute values.

Example:

```text
101 | Rahul | IT | 60000
```

This is one employee record.

---

# 25. Schema

A **schema** describes the structure of a database or a namespace of database objects, depending on the DBMS.

It can include:

* Tables
* Columns
* Data types
* Constraints
* Views
* Functions
* Relationships
* Other objects

Example:

```text
Company Schema
│
├── employees
├── departments
├── customers
└── orders
```

---

# 26. Database Schema vs Database Instance

### Schema

The structure/design of the database.

Example:

```text
employees(
    employee_id,
    name,
    salary
)
```

### Instance

The actual data stored at a particular moment.

```text
1 | Rahul | 50000
2 | Priya | 60000
```

Think:

```text
Schema     → Structure
Instance   → Current Data
```

---

# 27. Data Types

A database uses data types to determine what kind of value a column can store.

Common categories:

```text
Numeric
Character/String
Date/Time
Boolean
Binary
JSON / Semi-structured
```

Examples:

```text
INT
DECIMAL
VARCHAR
DATE
TIMESTAMP
BOOLEAN
```

Exact data types vary between DBMSs.

---

# 28. Constraints

Constraints are rules applied to data.

Common constraints:

```text
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
CHECK
DEFAULT
```

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(200) UNIQUE,
    salary DECIMAL(10,2) CHECK (salary >= 0)
);
```

---

# 29. Primary Key

A **primary key** uniquely identifies a row.

Example:

```text
employee_id
```

Properties:

* Unique
* Cannot be NULL
* Identifies one row
* One primary key constraint per table
* Can contain multiple columns as a composite key

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

# 30. Candidate Key

A **candidate key** is a column or combination of columns that can uniquely identify a row.

Example:

```text
employees

employee_id
email
```

If both are unique, both can potentially be candidate keys.

One is selected as the primary key.

```text
Candidate Keys
      │
      ├── employee_id
      └── email
             ↓
       Primary Key
```

---

# 31. Alternate Key

A candidate key that is not selected as the primary key is often called an **alternate key**.

Example:

```text
Candidate Keys:
- employee_id
- email

Primary Key:
- employee_id

Alternate Key:
- email
```

---

# 32. Composite Key

A composite key uses multiple columns to uniquely identify a row.

Example:

```text
student_id
course_id
```

Together:

```text
(student_id, course_id)
```

can identify a unique enrollment.

Example:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

---

# 33. Foreign Key

A foreign key references a key in another table.

Example:

```text
departments

department_id
     ↑
     │
     │
employees

department_id
```

SQL:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

# 34. Referential Integrity

**Referential integrity** ensures that relationships between related tables remain valid.

Suppose:

```text
departments

10 → IT
20 → HR
```

Then an employee's:

```text
department_id = 10
```

is valid.

But:

```text
department_id = 99
```

would be invalid if department 99 does not exist and the foreign-key rules don't permit it.

---

# 35. UNIQUE Constraint

Ensures values are unique according to the database's constraint semantics.

Example:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(200) UNIQUE
);
```

Two users should not have the same email under this constraint.

---

# 36. NOT NULL Constraint

Requires a value to be present.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

`name` cannot be NULL.

---

# 37. CHECK Constraint

Ensures that a condition is satisfied.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    salary DECIMAL(10,2)
        CHECK (salary >= 0)
);
```

Negative salary values are rejected.

Exact enforcement details can vary by DBMS and version.

---

# 38. DEFAULT Constraint

Provides a default value when a value is not supplied.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'Active'
);
```

If status isn't supplied, the database can use:

```text
Active
```

---

# 39. NULL

`NULL` represents a missing, unknown, or not-applicable value.

It is not:

```text
0
```

It is not:

```text
''
```

It is not:

```text
FALSE
```

Example:

```text
employee_id | phone
------------+-------
1           | NULL
```

---

# 40. Keys — Complete Overview

```text
Keys
│
├── Super Key
├── Candidate Key
├── Primary Key
├── Alternate Key
├── Foreign Key
└── Composite Key
```

---

# 41. Super Key

A **super key** is any set of one or more attributes that uniquely identifies a row.

Example:

```text
employee_id
```

may uniquely identify an employee.

So:

```text
(employee_id)
```

is a super key.

If `employee_id` is unique, then:

```text
(employee_id, name)
```

is also technically a super key, but it contains unnecessary information.

A candidate key is a **minimal** super key.

---

# 42. Relationships

Tables can have relationships.

Major types:

```text
One-to-One
One-to-Many
Many-to-Many
```

---

# 43. One-to-One

One record in Table A corresponds to one record in Table B.

Example:

```text
Person
  1
  │
  │
  1
Passport
```

---

# 44. One-to-Many

One record can have multiple related records.

Example:

```text
Department
    1
    │
    │
    N
Employees
```

One department can have many employees.

---

# 45. Many-to-Many

Many records on both sides can be related.

Example:

```text
Students ←→ Courses
```

A student can enroll in many courses.

A course can contain many students.

Usually implemented using a junction table:

```text
students
    │
    ↓
student_courses
    ↑
    │
courses
```

---

# 46. Junction Table

A junction table resolves many-to-many relationships.

Example:

```text
student_courses

student_id | course_id
-----------+----------
1          | 101
1          | 102
2          | 101
3          | 103
```

This creates relationships between:

```text
students
```

and:

```text
courses
```

---

# 47. Cardinality

Cardinality describes how many records can participate in a relationship.

Examples:

```text
1 : 1
1 : N
N : 1
M : N
```

Examples:

```text
Customer : Order
1 : N
```

```text
Student : Course
M : N
```

---

# 48. ER Model

**ER = Entity Relationship**

An ER model represents:

* Entities
* Attributes
* Relationships

Example:

```text
+-------------+
|  CUSTOMER   |
+-------------+
| customer_id |
| name        |
| email       |
+-------------+
       |
       | places
       |
       | 1:N
       ↓
+-------------+
|   ORDER     |
+-------------+
| order_id    |
| order_date  |
| customer_id |
+-------------+
```

---

# 49. ER Diagram

An **ER diagram (ERD)** visually represents database structure.

It shows:

```text
Entities
Attributes
Relationships
Keys
Cardinality
```

Example:

```text
CUSTOMER
    │
    │ 1
    │
    │
    N
    ↓
ORDER
```

---

# 50. Database Design

Database design means planning how data should be organized.

A basic design process:

```text
Requirements
      ↓
Identify Entities
      ↓
Identify Attributes
      ↓
Identify Relationships
      ↓
Choose Keys
      ↓
Normalize
      ↓
Create Tables
      ↓
Add Constraints
      ↓
Create Indexes
      ↓
Test
```

---

# 51. Data Redundancy

**Data redundancy** means unnecessarily storing the same information multiple times.

Bad design:

```text
order_id | customer_name | customer_city
---------+---------------+--------------
1        | Rahul         | Hyderabad
2        | Rahul         | Hyderabad
3        | Rahul         | Hyderabad
```

Customer information is repeated.

This can cause:

* More storage
* Inconsistency
* Update problems
* Maintenance problems

---

# 52. Data Integrity

Data integrity means maintaining accurate, consistent, and valid data.

Major types include:

```text
Entity Integrity
Referential Integrity
Domain Integrity
User-Defined Integrity
```

---

# 53. Entity Integrity

Entity integrity ensures that every row can be uniquely identified.

Usually achieved using:

```text
PRIMARY KEY
```

Example:

```text
employee_id
```

must uniquely identify each employee.

---

# 54. Referential Integrity

Maintains valid relationships between tables.

Usually enforced using:

```text
FOREIGN KEY
```

Example:

```text
employees.department_id
        ↓
departments.department_id
```

---

# 55. Domain Integrity

Ensures that values belong to an appropriate domain.

Examples:

```text
Age >= 0
Salary >= 0
Status ∈ {Active, Inactive}
```

Can be enforced using:

* Data types
* CHECK constraints
* NOT NULL
* DEFAULT
* Other constraints

---

# 56. Database Normalization

**Normalization** is the process of organizing relational data to reduce unnecessary redundancy and improve data integrity.

Main normal forms:

```text
1NF
2NF
3NF
BCNF
4NF
5NF
```

For most beginner and analytics work, understanding **1NF, 2NF, and 3NF** is essential.

---

# 57. First Normal Form — 1NF

A table should have atomic values rather than repeating groups or multi-valued fields in a single cell.

Bad:

```text
student_id | courses
-----------+------------------
1          | SQL, Python, Java
```

Better:

```text
student_id | course
-----------+---------
1          | SQL
1          | Python
1          | Java
```

---

# 58. Second Normal Form — 2NF

A table should:

1. Be in 1NF
2. Have no partial dependency on part of a composite key

This matters primarily when a table has a composite key.

Example conceptual problem:

```text
(student_id, course_id)
```

If:

```text
student_id → student_name
```

then `student_name` depends only on part of the composite key.

That creates a partial dependency.

---

# 59. Third Normal Form — 3NF

A table should:

1. Be in 2NF
2. Have no inappropriate transitive dependency of non-key attributes on other non-key attributes

Example:

```text
employee_id
department_id
department_name
```

If:

```text
employee_id → department_id
department_id → department_name
```

then `department_name` depends indirectly on `employee_id`.

A normalized design can separate:

```text
employees
departments
```

---

# 60. Normalization Example

Bad design:

```text
employees

employee_id | employee_name | department | manager
------------+---------------+------------+--------
1           | Rahul         | IT         | Ravi
2           | Priya         | IT         | Ravi
3           | Arun          | HR         | Sita
```

Better:

```text
employees

employee_id | employee_name | department_id
------------+---------------+--------------
1           | Rahul         | 10
2           | Priya         | 10
3           | Arun          | 20
```

```text
departments

department_id | department_name | manager
--------------+-----------------+--------
10            | IT              | Ravi
20            | HR              | Sita
```

---

# 61. Normalization vs Denormalization

### Normalization

Focuses on:

```text
Less redundancy
Better consistency
Better integrity
```

### Denormalization

Intentionally introduces some redundancy to improve:

```text
Read performance
Reporting performance
Query simplicity
```

This is common in analytics and data warehousing.

---

# 62. Transaction

A **transaction** is a logical unit of database work.

Example:

A bank transfer:

```text
Account A
   ↓
Subtract ₹1000
   ↓
Account B
   ↓
Add ₹1000
```

Both operations should be treated as one logical operation.

```text
Transaction
├── Debit
└── Credit
```

If something goes wrong, the transaction can be rolled back depending on the system and transaction state.

---

# 63. ACID Properties

Transactions are commonly discussed using **ACID**.

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

---

# 64. Atomicity

A transaction is treated as a whole.

Either:

```text
All operations succeed
```

or:

```text
The transaction is rolled back
```

Conceptually:

```text
Transaction
│
├── Operation 1 ✓
├── Operation 2 ✓
└── Operation 3 ✗
       ↓
Rollback
```

---

# 65. Consistency

A transaction should move the database from one valid state to another valid state while respecting defined rules and constraints.

Example:

```text
Before transaction → Valid
After transaction  → Valid
```

---

# 66. Isolation

Concurrent transactions should not improperly interfere with one another.

Example:

```text
Transaction A
Transaction B
     ↓
Database
```

The DBMS uses isolation mechanisms to control what each transaction can see.

---

# 67. Durability

Once a transaction is successfully committed, its changes should persist despite failures covered by the database's durability guarantees.

```text
COMMIT
  ↓
Persistent Data
```

---

# 68. ACID Summary

| Property    | Meaning                                     |
| ----------- | ------------------------------------------- |
| Atomicity   | All-or-nothing                              |
| Consistency | Preserves database rules                    |
| Isolation   | Controls concurrent transaction interaction |
| Durability  | Committed changes persist                   |

---

# 69. Concurrency

**Concurrency** means multiple users or transactions access the database around the same time.

Example:

```text
User A ──┐
         │
User B ──┼──→ Database
         │
User C ──┘
```

The DBMS must coordinate these operations safely.

---

# 70. Concurrency Problems

Common problems include:

### Dirty Read

A transaction reads data written by another transaction that has not yet committed.

### Non-Repeatable Read

A transaction reads the same row twice and gets different committed values.

### Phantom Read

A repeated query returns a different set of rows because another transaction inserted or removed matching rows.

### Lost Update

One update unintentionally overwrites another update.

---

# 71. Isolation Levels

Common SQL transaction isolation levels:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Some systems also support:

```text
SNAPSHOT
```

or MVCC-based implementations.

The exact behavior depends on the DBMS.

---

# 72. Read Uncommitted

Allows the weakest isolation.

Potentially permits dirty reads.

```text
Isolation
↓
Low
```

---

# 73. Read Committed

A transaction generally sees only committed data.

It prevents dirty reads.

It may still allow non-repeatable reads and, depending on the DBMS, phantom behavior.

---

# 74. Repeatable Read

Provides stronger guarantees for repeated reads.

The exact behavior varies by database system.

---

# 75. Serializable

Provides the strongest standard isolation level.

Conceptually, concurrent transactions behave as though they were executed serially.

Trade-off:

```text
Higher consistency
       ↓
Potentially lower concurrency
```

---

# 76. Transaction Commands

Common transaction commands:

```text
BEGIN
COMMIT
ROLLBACK
SAVEPOINT
```

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If an error occurs:

```sql
ROLLBACK;
```

Exact transaction syntax varies between DBMSs.

---

# 77. SAVEPOINT

A savepoint allows partial rollback within a transaction.

Conceptually:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

SAVEPOINT transfer_step;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

ROLLBACK TO transfer_step;

COMMIT;
```

Support and syntax can vary.

---

# 78. Index

An **index** is a database structure used to speed up data retrieval.

Without an appropriate index:

```text
Database
   ↓
Search many rows
   ↓
Find matching data
```

With an index:

```text
Query
  ↓
Index
  ↓
Locate relevant rows
  ↓
Data
```

---

# 79. Example of an Index

Suppose:

```text
employees
```

contains millions of records.

Queries frequently search:

```sql
SELECT *
FROM employees
WHERE email = 'rahul@example.com';
```

An index on `email` can make this lookup much more efficient in suitable circumstances.

Example:

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

---

# 80. Advantages of Indexes

Indexes can:

* Speed up searches
* Improve joins
* Help sorting
* Improve filtering
* Support uniqueness

But indexes also have costs:

* Additional storage
* Slower inserts
* Slower updates to indexed columns
* Slower deletes
* Maintenance overhead

Therefore:

> Do not create indexes blindly.

---

# 81. Clustered vs Non-Clustered Index

The terminology depends on the database system.

A simplified conceptual distinction:

### Clustered

The table's data is organized around the clustered index structure.

### Non-Clustered

The index is a separate structure that points to the underlying rows/data.

Not every DBMS implements these concepts in exactly the same way.

---

# 82. View

A **view** is a virtual table defined by a query.

Example:

```sql
CREATE VIEW employee_summary AS
SELECT
    employee_id,
    name,
    salary
FROM employees;
```

Then:

```sql
SELECT *
FROM employee_summary;
```

Views can provide:

* Simplified queries
* Security abstraction
* Reusable logic
* Reporting layers

---

# 83. Materialized View

A **materialized view** stores the result of a query physically rather than calculating it every time.

Conceptually:

```text
Query
  ↓
Materialized Result
  ↓
Stored Data
```

Useful for:

* Reporting
* Analytics
* Expensive aggregations
* Frequently accessed summaries

It must be refreshed according to the database system's mechanisms.

---

# 84. Stored Procedure

A stored procedure is a reusable program stored in the database.

It can contain:

* SQL statements
* Parameters
* Variables
* Conditions
* Loops
* Error handling

Example concept:

```text
Application
    ↓
Stored Procedure
    ↓
Database Operations
```

Syntax varies significantly between DBMSs.

---

# 85. Function

A database function performs an operation and returns a value or result.

Example concept:

```text
Input
 ↓
Function
 ↓
Output
```

Functions can be:

* Built-in
* User-defined

Examples of built-in functions:

```text
COUNT()
SUM()
AVG()
UPPER()
LOWER()
ROUND()
```

---

# 86. Trigger

A trigger is database logic automatically executed when a specified event occurs.

Example:

```text
INSERT
   ↓
Trigger
   ↓
Audit Log
```

Possible events:

```text
INSERT
UPDATE
DELETE
```

Triggers are useful for certain auditing and integrity tasks, but should be used carefully because they introduce hidden side effects.

---

# 87. Sequence

A sequence generates numeric values, often used for identifiers.

Conceptually:

```text
1
2
3
4
5
...
```

PostgreSQL and Oracle commonly provide sequence objects.

Other systems may use:

```text
AUTO_INCREMENT
IDENTITY
```

or equivalent mechanisms.

---

# 88. Identity / Auto Increment

Used to automatically generate numeric identifiers.

Example concept:

```text
employee_id

1
2
3
4
5
```

Syntax varies by database.

Example in MySQL:

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

# 89. Referential Actions

Foreign keys can define what happens when referenced rows are updated or deleted.

Common actions:

```text
CASCADE
SET NULL
SET DEFAULT
RESTRICT
NO ACTION
```

Example:

```sql
FOREIGN KEY (department_id)
REFERENCES departments(department_id)
ON DELETE CASCADE
```

The exact behavior and support vary by DBMS.

---

# 90. Database Security

Database security protects data from unauthorized access.

Important concepts:

```text
Authentication
Authorization
Roles
Privileges
Encryption
Auditing
Access Control
```

---

# 91. Authentication

Authentication answers:

> Who are you?

Examples:

```text
Username + Password
Certificate
SSO
Authentication Token
```

---

# 92. Authorization

Authorization answers:

> What are you allowed to do?

Example:

```text
Analyst
   ↓
SELECT permission

Admin
   ↓
SELECT
INSERT
UPDATE
DELETE
CREATE
...
```

---

# 93. Roles

A role is a collection of permissions.

Example:

```text
Role: Analyst
│
├── SELECT
└── EXECUTE
```

Another:

```text
Role: Admin
│
├── SELECT
├── INSERT
├── UPDATE
├── DELETE
└── CREATE
```

---

# 94. Principle of Least Privilege

Users should receive only the permissions they need.

Example:

A reporting analyst may need:

```text
SELECT
```

but not:

```text
DROP TABLE
```

This reduces security risks.

---

# 95. Backup

A backup is a copy of database data used for recovery.

Types can include:

```text
Full Backup
Incremental Backup
Differential Backup
Logical Backup
Physical Backup
```

Exact backup mechanisms vary by DBMS.

---

# 96. Recovery

Recovery means restoring database availability and/or data after a failure.

Possible failures:

* Hardware failure
* Software failure
* Human error
* Corruption
* Accidental deletion
* Infrastructure failure

A good database system should have:

```text
Backup
+
Recovery Strategy
+
Testing
```

---

# 97. Replication

Replication copies data from one database/server to another.

Conceptually:

```text
Primary
   │
   ├────────→ Replica 1
   │
   └────────→ Replica 2
```

Uses include:

* High availability
* Read scaling
* Disaster recovery
* Geographic distribution

Replication behavior depends heavily on the database system.

---

# 98. Primary and Replica

A common architecture:

```text
              ┌──→ Read Replica 1
              │
Application → Primary
              │
              └──→ Read Replica 2
```

Writes generally go to the primary.

Reads may be distributed to replicas, depending on the architecture.

---

# 99. Partitioning

Partitioning divides a large table or index into smaller logical pieces.

Example:

```text
orders

2024 data → Partition 1
2025 data → Partition 2
2026 data → Partition 3
```

Types include:

```text
Range Partitioning
List Partitioning
Hash Partitioning
```

Partitioning can improve manageability and sometimes query performance.

---

# 100. Sharding

**Sharding** distributes data across multiple database servers.

Example:

```text
Database
│
├── Server 1 → Customers 1–1M
├── Server 2 → Customers 1M–2M
└── Server 3 → Customers 2M–3M
```

Sharding is different from partitioning because it generally involves distribution across separate nodes/servers.

---

# 101. Partitioning vs Sharding

| Partitioning                         | Sharding                                             |
| ------------------------------------ | ---------------------------------------------------- |
| Splits data into partitions          | Distributes data across nodes                        |
| Can occur within one database system | Typically across multiple servers                    |
| Helps manage large tables            | Helps horizontal scalability                         |
| DBMS usually manages partitions      | Application/database cluster may manage distribution |

---

# 102. Vertical Scaling

Increase resources on the same server.

```text
Server
│
├── More CPU
├── More RAM
└── Faster Storage
```

This is called:

**Scale Up**

---

# 103. Horizontal Scaling

Add more machines.

```text
Server 1
Server 2
Server 3
Server 4
```

This is called:

**Scale Out**

Commonly associated with:

* Replication
* Sharding
* Distributed databases

---

# 104. OLTP

**OLTP = Online Transaction Processing**

Designed for day-to-day transactions.

Examples:

```text
Banking
Shopping
Ticket Booking
Payment Processing
Order Management
```

Characteristics:

* Many small transactions
* Frequent INSERT/UPDATE/DELETE
* Strong consistency requirements
* Low-latency operations
* Highly concurrent workloads

---

# 105. OLAP

**OLAP = Online Analytical Processing**

Designed for analysis and reporting.

Examples:

```text
Sales Analysis
Customer Analysis
Business Intelligence
Financial Reporting
Trend Analysis
```

Characteristics:

* Large analytical queries
* Aggregations
* Historical data
* Complex joins
* Reporting
* Trend analysis

---

# 106. OLTP vs OLAP

| OLTP                      | OLAP                             |
| ------------------------- | -------------------------------- |
| Transactions              | Analytics                        |
| Operational systems       | Analytical systems               |
| Many small queries        | Fewer complex queries            |
| Frequent writes           | Often read-heavy                 |
| Current data              | Historical/aggregated data       |
| Normalized designs common | Denormalized/star schemas common |

---

# 107. Data Warehouse

A **data warehouse** is a system designed primarily for analytical workloads.

Typical flow:

```text
Operational Databases
        ↓
       ETL/ELT
        ↓
Data Warehouse
        ↓
BI / Analytics
```

Examples of data warehouse platforms include:

* Snowflake
* Google BigQuery
* Amazon Redshift
* Microsoft Fabric / Synapse technologies

---

# 108. Data Lake

A **data lake** stores large volumes of raw or semi-structured/structured data.

Example:

```text
Data Lake
│
├── CSV
├── JSON
├── Logs
├── Images
├── Parquet
└── Other Data
```

---

# 109. Data Warehouse vs Data Lake

| Data Warehouse                                 | Data Lake                                         |
| ---------------------------------------------- | ------------------------------------------------- |
| Structured analytical data                     | Raw and diverse data                              |
| Schema commonly defined before/around analysis | Often supports schema-on-read approaches          |
| BI and reporting                               | Big data, ML, exploration                         |
| Highly curated                                 | Can contain raw data                              |
| SQL heavily used                               | SQL may be used along with other processing tools |

Modern architectures often combine features of both.

---

# 110. Data Mart

A **data mart** is a smaller analytical data store focused on a specific business area.

Examples:

```text
Enterprise Warehouse
       │
       ├── Sales Data Mart
       ├── Finance Data Mart
       ├── Marketing Data Mart
       └── HR Data Mart
```

---

# 111. ETL

**ETL = Extract, Transform, Load**

```text
Source
  ↓
Extract
  ↓
Transform
  ↓
Load
  ↓
Data Warehouse
```

Example:

```text
MySQL
  ↓
Extract
  ↓
Clean + Transform
  ↓
Warehouse
```

---

# 112. ELT

**ELT = Extract, Load, Transform**

```text
Source
  ↓
Extract
  ↓
Load
  ↓
Data Warehouse
  ↓
Transform
```

Modern cloud data platforms often support ELT workflows effectively.

---

# 113. Database Normalization vs Data Warehousing

Operational databases often prioritize:

```text
Consistency
Integrity
Reduced redundancy
Transactions
```

Analytical databases often prioritize:

```text
Query performance
Aggregation
Reporting
Historical analysis
```

Therefore their designs can be very different.

---

# 114. Star Schema

Common in data warehousing.

Structure:

```text
             Dimension
                 |
                 |
Dimension ── Fact ── Dimension
                 |
                 |
             Dimension
```

Example:

```text
             dim_customer
                  |
                  |
dim_product ─ fact_sales ─ dim_date
                  |
                  |
             dim_store
```

---

# 115. Fact Table

A fact table contains measurable business events.

Example:

```text
fact_sales

date_id
product_id
customer_id
store_id
quantity
sales_amount
profit
```

Measures include:

```text
quantity
revenue
profit
cost
```

---

# 116. Dimension Table

A dimension table describes business entities.

Examples:

```text
dim_customer
dim_product
dim_date
dim_store
```

Example:

```text
dim_product

product_id
product_name
category
brand
```

---

# 117. Fact vs Dimension

| Fact            | Dimension               |
| --------------- | ----------------------- |
| Measures/events | Descriptive information |
| Revenue         | Product                 |
| Quantity        | Customer                |
| Profit          | Store                   |
| Sales event     | Date                    |

---

# 118. Database Performance

Database performance depends on factors such as:

```text
Query Design
Indexes
Data Volume
Schema Design
Hardware
Memory
Storage
Concurrency
Execution Plan
Statistics
Partitioning
Caching
```

---

# 119. Query Optimization

Query optimization means improving query execution efficiency.

Example:

Instead of:

```sql
SELECT *
FROM employees;
```

if you only need two columns:

```sql
SELECT employee_id, salary
FROM employees;
```

Other techniques include:

* Appropriate indexes
* Efficient joins
* Filtering early where appropriate
* Avoiding unnecessary calculations
* Proper schema design
* Query plan analysis

---

# 120. Execution Plan

An execution plan describes how the database intends to execute a query.

It can show operations such as:

```text
Table Scan
Index Scan
Index Seek
Join
Sort
Aggregate
Filter
```

Example conceptual plan:

```text
Query
 ↓
Index Scan
 ↓
Filter
 ↓
Join
 ↓
Aggregate
 ↓
Result
```

Tools such as `EXPLAIN` or database-specific equivalents can be used to inspect plans.

---

# 121. Table Scan

A table scan reads many or all rows in a table.

```text
Table
 ↓
Read rows
 ↓
Check conditions
 ↓
Result
```

For very large tables, this can be expensive when a more selective access path exists.

However, a full scan can sometimes be the optimal strategy.

---

# 122. Index Scan / Seek

An index can allow the database to locate relevant records without reading every row.

Conceptually:

```text
Query
 ↓
Index
 ↓
Relevant rows
```

The exact terminology differs by database system.

---

# 123. Database Deadlock

A deadlock occurs when transactions wait for each other indefinitely.

Example:

```text
Transaction A
locks Resource 1
     ↓
waits for Resource 2

Transaction B
locks Resource 2
     ↓
waits for Resource 1
```

Result:

```text
A waits for B
B waits for A
```

Database systems usually detect and resolve deadlocks by aborting one transaction.

---

# 124. Database Locking

Locks control concurrent access to data.

Conceptually:

```text
Shared Lock
Exclusive Lock
```

### Shared Lock

Allows compatible reads depending on the DBMS and isolation model.

### Exclusive Lock

Used when modifying data and prevents conflicting operations.

Modern databases may also use MVCC and other concurrency mechanisms.

---

# 125. MVCC

**MVCC = Multi-Version Concurrency Control**

Instead of forcing readers and writers to always block each other, the database can maintain multiple row versions.

Conceptually:

```text
Old Version
     ↓
New Version
```

Readers can often see an appropriate consistent version while another transaction writes.

MVCC is used by systems such as PostgreSQL and is also used in various forms by other database systems.

---

# 126. Database Metadata

Metadata is **data about data**.

Examples:

```text
Table names
Column names
Data types
Indexes
Constraints
Permissions
Statistics
```

Example:

```text
employees
│
├── employee_id → INTEGER
├── name        → VARCHAR
└── salary      → DECIMAL
```

This is metadata describing the table.

---

# 127. Data Dictionary

A data dictionary contains metadata about database objects.

It can describe:

* Tables
* Columns
* Data types
* Constraints
* Indexes
* Users
* Permissions

Many DBMSs provide system catalogs or information-schema views for this purpose.

---

# 128. Database Catalog

A database catalog stores metadata about the database.

Conceptually:

```text
Database
│
├── User Tables
├── System Catalog
├── Metadata
├── Constraints
└── Object Definitions
```

---

# 129. Database Connection

An application needs a connection to communicate with a database.

Conceptually:

```text
Application
    ↓
Database Driver
    ↓
Connection
    ↓
Database Server
```

A connection commonly involves:

```text
Host
Port
Database Name
Username
Password / Authentication
```

---

# 130. Connection Pooling

Opening a new database connection for every request can be expensive.

Connection pooling keeps a set of reusable connections.

```text
Application
    ↓
Connection Pool
│
├── Connection 1
├── Connection 2
├── Connection 3
└── Connection 4
    ↓
Database
```

Benefits:

* Lower connection overhead
* Better performance
* Better resource management
* Improved application scalability

---

# 131. Database Driver

A database driver allows an application to communicate with a specific database system.

Example:

```text
Python
  ↓
Database Driver
  ↓
PostgreSQL
```

For Python, examples include drivers/libraries such as:

```text
psycopg
mysql-connector-python
pyodbc
sqlite3
```

---

# 132. Database API

An application can communicate with a database through APIs provided by drivers or frameworks.

Example:

```python
connection = database.connect(...)
cursor = connection.cursor()

cursor.execute(
    "SELECT * FROM employees"
)
```

The exact API depends on the programming language and database driver.

---

# 133. Database Transaction Flow

A typical transaction:

```text
BEGIN
  ↓
Read Data
  ↓
Modify Data
  ↓
Validate
  ↓
COMMIT
```

If something goes wrong:

```text
BEGIN
  ↓
Operations
  ↓
Error
  ↓
ROLLBACK
```

---

# 134. Database Lifecycle

A database project can follow:

```text
Requirements
      ↓
Design
      ↓
ER Modeling
      ↓
Normalization
      ↓
Implementation
      ↓
Testing
      ↓
Deployment
      ↓
Monitoring
      ↓
Backup
      ↓
Maintenance
```

---

# 135. Database Design Principles

Good database design should aim for:

```text
Accuracy
Consistency
Integrity
Security
Performance
Scalability
Maintainability
Availability
Recoverability
```

---

# 136. Common Database Problems

Poor database design can cause:

### Data Redundancy

Same data stored repeatedly.

### Data Inconsistency

Different copies contain different values.

### Update Anomaly

Changing one fact requires multiple updates.

### Insert Anomaly

Cannot insert data without unrelated information.

### Delete Anomaly

Deleting one record accidentally removes important information.

Normalization helps address these problems in relational designs.

---

# 137. Database Anomalies

## Update Anomaly

Suppose a department manager is stored in every employee row.

If the manager changes:

```text
100 employee records
```

may need to be updated.

This creates risk of inconsistent data.

---

## Insert Anomaly

You cannot add a department until you have an employee for that department.

A poor schema can create this problem.

---

## Delete Anomaly

Deleting the only employee of a department may accidentally remove the only stored information about that department.

Separating entities can prevent this.

---

# 138. Database Availability

Availability means the database is accessible when needed.

High availability can involve:

```text
Replication
Failover
Backups
Redundancy
Monitoring
Disaster Recovery
```

---

# 139. High Availability

A highly available architecture may look like:

```text
Application
     ↓
Load Balancer
     ↓
┌───────────────┐
│               │
Primary       Replica
│               │
└───────────────┘
```

Actual architectures vary significantly.

---

# 140. Disaster Recovery

Disaster recovery is the process of restoring database services and data after a major failure.

Important concepts:

### RPO

**Recovery Point Objective**

How much data loss is acceptable in time terms.

Example:

```text
RPO = 15 minutes
```

means the organization aims to recover to a point no more than roughly 15 minutes before the failure, depending on implementation.

### RTO

**Recovery Time Objective**

How quickly the system should be restored.

Example:

```text
RTO = 1 hour
```

---

# 141. RPO vs RTO

| RPO                  | RTO                      |
| -------------------- | ------------------------ |
| Acceptable data loss | Acceptable recovery time |
| Measured in time     | Measured in time         |
| Focuses on data      | Focuses on availability  |

Remember:

```text
RPO → How much data can we lose?
RTO → How quickly must we recover?
```

---

# 142. Database Scalability

Scalability is the ability of a database system to handle increasing workloads.

Scaling can involve:

```text
Vertical Scaling
Horizontal Scaling
Read Replicas
Partitioning
Sharding
Caching
Query Optimization
Indexes
```

---

# 143. Database Monitoring

Important metrics include:

```text
CPU Usage
Memory Usage
Disk Usage
Query Latency
Transactions Per Second
Connections
Lock Waits
Deadlocks
Cache Hit Rate
Replication Lag
Storage Growth
```

Monitoring helps identify bottlenecks.

---

# 144. Database Documentation

A good database project should document:

```text
Tables
Columns
Data Types
Relationships
Keys
Constraints
Business Rules
Indexes
Data Sources
Data Definitions
```

This makes the database easier to maintain.

---

# 145. Database Naming Conventions

Good names:

```text
customer_id
order_id
product_id
order_date
total_amount
```

Poor names:

```text
x
abc
temp1
data
```

Use consistent naming across the database.

---

# 146. Surrogate Key

A surrogate key is an artificial/system-generated identifier.

Example:

```text
customer_id = 101
```

The value itself has no business meaning.

Common examples:

```text
AUTO_INCREMENT
IDENTITY
SEQUENCE
UUID
```

---

# 147. Natural Key

A natural key is a real-world attribute that naturally identifies an entity.

Examples:

```text
Email
National ID
ISBN
Product Code
```

Natural keys can be useful, but they may change or have business-specific constraints.

---

# 148. Surrogate Key vs Natural Key

| Surrogate Key             | Natural Key                  |
| ------------------------- | ---------------------------- |
| Artificial identifier     | Real-world identifier        |
| Usually stable            | May change                   |
| Often numeric/UUID        | Has business meaning         |
| Common in database design | Useful when naturally unique |

---

# 149. UUID

**UUID = Universally Unique Identifier**

Example:

```text
550e8400-e29b-41d4-a716-446655440000
```

UUIDs can be used as identifiers.

Advantages:

* Very low collision probability
* Can be generated across distributed systems
* Doesn't require a central sequential counter

Disadvantages can include:

* Larger storage
* Less human-readable
* Potential index/storage considerations

---

# 150. Database Consistency

Consistency means database state follows defined rules.

Examples:

```text
Primary keys are unique
Foreign keys reference valid rows
Salary cannot be negative
Required fields cannot be NULL
```

Constraints help enforce consistency.

---

# 151. Database Integrity vs Consistency

### Integrity

Focuses on correctness and validity of data.

### Consistency

Focuses on the database remaining in a valid state according to its rules, especially across transactions.

They are closely related but not identical concepts.

---

# 152. Database Security Layers

Security can exist at multiple levels:

```text
Application Security
       ↓
Network Security
       ↓
Database Authentication
       ↓
Authorization
       ↓
Row/Column Access
       ↓
Encryption
       ↓
Auditing
```

---

# 153. Encryption

Database environments may use:

### Encryption in Transit

Protects data while moving between application and database.

```text
Application
   ↓ encrypted connection
Database
```

### Encryption at Rest

Protects stored data on disk.

Security architecture depends on the system and environment.

---

# 154. Auditing

Auditing tracks important database activities.

Examples:

```text
Who accessed data?
Who modified data?
When was it modified?
What was changed?
```

Useful for:

* Security
* Compliance
* Troubleshooting
* Investigations

---

# 155. Database vs File System

| Database                     | File System                              |
| ---------------------------- | ---------------------------------------- |
| Structured data management   | File-based storage                       |
| Querying capabilities        | Basic file operations                    |
| Transactions                 | Usually not database transactions        |
| Constraints                  | Limited                                  |
| Concurrent access management | Different mechanisms                     |
| Relationships                | Native relational relationships in RDBMS |
| Security and permissions     | File-level permissions                   |

A database is more than simply a collection of files.

---

# 156. Spreadsheet vs Database

| Spreadsheet                  | Database                                       |
| ---------------------------- | ---------------------------------------------- |
| Good for small datasets      | Designed for larger managed datasets           |
| Easy for manual work         | Better for applications                        |
| Limited concurrency          | Supports concurrent access mechanisms          |
| Basic relationships          | Strong relationship support                    |
| Manual data integrity        | Constraints and rules                          |
| Basic querying               | Powerful querying                              |
| Suitable for ad-hoc analysis | Suitable for operational systems and analytics |

Spreadsheets are still extremely useful; they simply serve different purposes.

---

# 157. Database Fundamentals for Data Analytics

As a data analyst, you should understand:

```text
Database
 ↓
Schema
 ↓
Tables
 ↓
Rows
 ↓
Columns
 ↓
Primary Keys
 ↓
Foreign Keys
 ↓
Relationships
 ↓
SQL
 ↓
Joins
 ↓
Aggregations
 ↓
Business Metrics
```

You should be able to understand a database schema before writing analytical queries.

---

# 158. Example Analytics Database

Suppose an e-commerce company has:

```text
customers
products
orders
order_items
payments
```

Relationships:

```text
customers
    │
    │ 1:N
    ↓
orders
    │
    │ 1:N
    ↓
order_items
    │
    │ N:1
    ↓
products
```

A data analyst can use these relationships to calculate:

```text
Total Revenue
Average Order Value
Customer Lifetime Value
Product Sales
Monthly Revenue
Customer Retention
Top Products
Repeat Customers
```

---

# 159. OLTP Database Example

An e-commerce operational database:

```text
customers
orders
order_items
products
payments
addresses
```

It handles:

```text
Create order
Update inventory
Process payment
Update customer
Create shipment
```

This is an OLTP workload.

---

# 160. Analytics Database Example

A data warehouse might contain:

```text
fact_sales
dim_customer
dim_product
dim_date
dim_store
```

This is designed for analytical queries.

Example:

```text
Monthly Revenue by Product Category
```

---

# 161. Operational Database vs Analytical Database

```text
Operational Database
        ↓
      ETL/ELT
        ↓
Data Warehouse
        ↓
Analytics
        ↓
Dashboard
```

Example:

```text
Application
   ↓
PostgreSQL
   ↓
ETL
   ↓
Data Warehouse
   ↓
Power BI / Tableau
```

---

# 162. Database Fundamentals Mental Model

Remember this hierarchy:

```text
DATABASE
│
├── Schema
│
├── Tables
│   │
│   ├── Columns
│   │
│   └── Rows
│
├── Keys
│   ├── Primary Key
│   └── Foreign Key
│
├── Constraints
│
├── Indexes
│
├── Views
│
├── Functions
│
├── Procedures
│
└── Triggers
```

---

# 163. Complete Database Concept Map

```text
DATABASE FUNDAMENTALS
│
├── Data
│
├── Database
│
├── DBMS
│
├── RDBMS
│
├── Database Models
│   ├── Relational
│   ├── Hierarchical
│   ├── Network
│   ├── Document
│   ├── Key-Value
│   └── Graph
│
├── Database Structure
│   ├── Database
│   ├── Schema
│   ├── Table
│   ├── Row
│   ├── Column
│   ├── Entity
│   └── Attribute
│
├── Keys
│   ├── Super Key
│   ├── Candidate Key
│   ├── Primary Key
│   ├── Alternate Key
│   ├── Foreign Key
│   └── Composite Key
│
├── Relationships
│   ├── 1:1
│   ├── 1:N
│   └── M:N
│
├── Constraints
│   ├── PRIMARY KEY
│   ├── FOREIGN KEY
│   ├── UNIQUE
│   ├── NOT NULL
│   ├── CHECK
│   └── DEFAULT
│
├── Database Design
│   ├── ER Model
│   ├── ER Diagram
│   ├── Normalization
│   ├── 1NF
│   ├── 2NF
│   ├── 3NF
│   └── Denormalization
│
├── Transactions
│   ├── ACID
│   ├── COMMIT
│   ├── ROLLBACK
│   ├── SAVEPOINT
│   └── Isolation
│
├── Performance
│   ├── Indexes
│   ├── Query Optimization
│   ├── Execution Plans
│   ├── Partitioning
│   └── Caching
│
├── Security
│   ├── Authentication
│   ├── Authorization
│   ├── Roles
│   ├── Privileges
│   ├── Encryption
│   └── Auditing
│
├── Availability
│   ├── Backup
│   ├── Recovery
│   ├── Replication
│   ├── Failover
│   └── Disaster Recovery
│
└── Analytics
    ├── OLTP
    ├── OLAP
    ├── Data Warehouse
    ├── Data Mart
    ├── Fact Tables
    ├── Dimension Tables
    └── Star Schema
```

---

# 164. Database Fundamentals Revision Checklist

## Basic Concepts

* [ ] Data
* [ ] Database
* [ ] DBMS
* [ ] RDBMS
* [ ] Database Server
* [ ] Database Client
* [ ] Database Schema
* [ ] Database Instance
* [ ] Metadata

## Database Models

* [ ] Hierarchical
* [ ] Network
* [ ] Relational
* [ ] Document
* [ ] Key-Value
* [ ] Graph
* [ ] Wide-Column

## Relational Concepts

* [ ] Table
* [ ] Row
* [ ] Column
* [ ] Record
* [ ] Entity
* [ ] Attribute
* [ ] Relationship
* [ ] Cardinality
* [ ] ER Model
* [ ] ER Diagram

## Keys

* [ ] Super Key
* [ ] Candidate Key
* [ ] Primary Key
* [ ] Alternate Key
* [ ] Foreign Key
* [ ] Composite Key
* [ ] Natural Key
* [ ] Surrogate Key

## Constraints

* [ ] PRIMARY KEY
* [ ] FOREIGN KEY
* [ ] UNIQUE
* [ ] NOT NULL
* [ ] CHECK
* [ ] DEFAULT

## Database Design

* [ ] Data Redundancy
* [ ] Data Integrity
* [ ] Entity Integrity
* [ ] Referential Integrity
* [ ] Domain Integrity
* [ ] Normalization
* [ ] 1NF
* [ ] 2NF
* [ ] 3NF
* [ ] BCNF
* [ ] Denormalization
* [ ] Update Anomaly
* [ ] Insert Anomaly
* [ ] Delete Anomaly

## Transactions

* [ ] Transaction
* [ ] ACID
* [ ] Atomicity
* [ ] Consistency
* [ ] Isolation
* [ ] Durability
* [ ] COMMIT
* [ ] ROLLBACK
* [ ] SAVEPOINT
* [ ] Isolation Levels
* [ ] Locks
* [ ] Deadlocks
* [ ] MVCC

## Performance

* [ ] Index
* [ ] Clustered Index
* [ ] Non-Clustered Index
* [ ] Query Optimization
* [ ] Execution Plan
* [ ] Partitioning
* [ ] Sharding
* [ ] Caching

## Security

* [ ] Authentication
* [ ] Authorization
* [ ] Roles
* [ ] Privileges
* [ ] Least Privilege
* [ ] Encryption
* [ ] Auditing

## Reliability

* [ ] Backup
* [ ] Recovery
* [ ] Replication
* [ ] Failover
* [ ] High Availability
* [ ] Disaster Recovery
* [ ] RPO
* [ ] RTO

## Analytics

* [ ] OLTP
* [ ] OLAP
* [ ] Data Warehouse
* [ ] Data Mart
* [ ] Data Lake
* [ ] ETL
* [ ] ELT
* [ ] Fact Table
* [ ] Dimension Table
* [ ] Star Schema
* [ ] Snowflake Schema

---

# 165. Recommended Learning Order

For a complete **SQL + Data Analytics** path, study database concepts in this order:

```text
1. Data & Database
       ↓
2. DBMS & RDBMS
       ↓
3. Tables, Rows & Columns
       ↓
4. Schema & Database Models
       ↓
5. Entities & Attributes
       ↓
6. Keys
       ↓
7. Relationships
       ↓
8. ER Diagrams
       ↓
9. Constraints
       ↓
10. Data Integrity
       ↓
11. Normalization
       ↓
12. Transactions
       ↓
13. ACID
       ↓
14. Concurrency
       ↓
15. Indexes
       ↓
16. Query Optimization
       ↓
17. Security
       ↓
18. Backup & Recovery
       ↓
19. Replication
       ↓
20. Partitioning & Sharding
       ↓
21. OLTP vs OLAP
       ↓
22. Data Warehousing
       ↓
23. Fact & Dimension Tables
       ↓
24. Star Schema
       ↓
25. SQL
       ↓
26. Advanced SQL
       ↓
27. Data Analytics
```

---

# 166. Most Important Concepts for Interviews

If you are preparing for interviews, make sure you can clearly explain:

```text
1. DBMS vs RDBMS
2. Database vs Schema
3. Table vs Database
4. Row vs Column
5. Primary Key
6. Foreign Key
7. Candidate Key
8. Composite Key
9. Natural vs Surrogate Key
10. Primary Key vs Unique Key
11. Relationships
12. 1:1, 1:N, M:N
13. Normalization
14. 1NF, 2NF, 3NF
15. Normalization vs Denormalization
16. Data Integrity
17. Referential Integrity
18. Transactions
19. ACID
20. Isolation Levels
21. Deadlocks
22. Indexes
23. Clustered vs Non-Clustered Index
24. Views
25. Stored Procedures
26. Functions
27. Triggers
28. OLTP vs OLAP
29. Database vs Data Warehouse
30. Fact vs Dimension
31. Star Schema
32. Partitioning vs Sharding
33. Backup vs Replication
34. RPO vs RTO
35. Vertical vs Horizontal Scaling
```

---

# 167. Final Database Mental Model

The most important thing to remember is:

```text
                    DATABASE
                       │
            ┌──────────┴──────────┐
            ↓                     ↓
        STRUCTURE                DATA
            │                     │
       Tables/Schema         Rows/Values
            │
      ┌─────┴─────┐
      ↓           ↓
    Keys      Constraints
      │           │
      └─────┬─────┘
            ↓
       Relationships
            ↓
       Database Design
            ↓
       Normalization
            ↓
        Transactions
            ↓
      Performance
            ↓
        Security
            ↓
     Backup & Recovery
            ↓
     Analytics / SQL
```

> **Core idea:** A database is not simply a place where data is stored. It is a system for **organizing, relating, protecting, validating, retrieving, updating, and reliably managing data**.

