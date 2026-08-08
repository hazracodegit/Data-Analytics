# SQL Data Types, Keys & Constraints

> Complete revision notes for SQL **Data Types, Keys, and Constraints** with definitions, examples, differences, and practical SQL code.

---

# 1. SQL Data Types

A **data type** defines what kind of value a column can store.

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2),
    joining_date DATE,
    is_active BOOLEAN
);
```

Here:

```text
employee_id  → INT
name         → VARCHAR
salary       → DECIMAL
joining_date → DATE
is_active    → BOOLEAN
```

Data types vary slightly between database systems such as MySQL, PostgreSQL, SQL Server, and Oracle.

---

# 2. Main Categories of SQL Data Types

```text
SQL Data Types
│
├── Numeric
│   ├── Integer
│   └── Decimal / Floating Point
│
├── Character / String
│   ├── CHAR
│   ├── VARCHAR
│   └── TEXT
│
├── Date & Time
│   ├── DATE
│   ├── TIME
│   ├── DATETIME
│   └── TIMESTAMP
│
├── Boolean
│
├── Binary
│
└── Semi-Structured / Special
    ├── JSON
    ├── UUID
    └── ARRAY / other DB-specific types
```

---

# 3. Numeric Data Types

Numeric data types store numbers.

Two major groups:

```text
Integer
Decimal / Floating Point
```

---

# 4. INTEGER

`INT` stores whole numbers.

Example:

```sql
CREATE TABLE students (
    student_id INT,
    age INT,
    marks INT
);
```

Values:

```text
1
20
95
100
```

No decimal component.

---

# 5. SMALLINT

Stores smaller-range integers than `INT`.

```sql
CREATE TABLE products (
    product_id INT,
    quantity SMALLINT
);
```

Useful when you know a column does not require the range of a normal integer.

---

# 6. BIGINT

Stores very large integer values.

```sql
CREATE TABLE transactions (
    transaction_id BIGINT
);
```

Useful for:

* Large IDs
* Large counters
* Large transaction systems

---

# 7. Integer Type Comparison

| Type          | General Purpose     |
| ------------- | ------------------- |
| SMALLINT      | Smaller integers    |
| INT / INTEGER | Normal integers     |
| BIGINT        | Very large integers |

Exact ranges depend on the DBMS and implementation.

---

# 8. DECIMAL / NUMERIC

`DECIMAL` and `NUMERIC` are exact numeric types in systems that support them.

They are commonly preferred for values where exact decimal arithmetic matters.

Examples:

```text
Money
Prices
Financial calculations
```

Example:

```sql
CREATE TABLE products (
    product_id INT,
    price DECIMAL(10,2)
);
```

Possible value:

```text
99999.99
```

---

# 9. DECIMAL Precision and Scale

Consider:

```sql
DECIMAL(10,2)
```

Here:

```text
10 → Precision
2  → Scale
```

Precision = total number of digits.

Scale = number of digits after the decimal point.

Example:

```text
12345678.90
```

Total digits:

```text
10
```

Digits after decimal:

```text
2
```

Therefore:

```text
DECIMAL(10,2)
```

can represent values with up to 10 total digits and 2 decimal places, subject to DBMS-specific rules.

---

# 10. FLOAT

`FLOAT` stores approximate floating-point numbers.

Example:

```sql
CREATE TABLE measurements (
    temperature FLOAT
);
```

Useful for:

* Scientific calculations
* Measurements
* Approximate numerical calculations

Because floating-point values are approximate, they are generally not the first choice for exact monetary calculations.

---

# 11. REAL / DOUBLE

Some database systems support:

```text
REAL
DOUBLE
DOUBLE PRECISION
```

These are approximate numeric types.

Example:

```sql
CREATE TABLE analytics (
    value DOUBLE
);
```

Exact names and behavior vary by DBMS.

---

# 12. Exact vs Approximate Numbers

### Exact

```text
DECIMAL
NUMERIC
```

Suitable for:

```text
Money
Financial values
Exact decimal calculations
```

### Approximate

```text
FLOAT
REAL
DOUBLE
```

Suitable for:

```text
Scientific values
Measurements
Large-scale numerical calculations
```

---

# 13. Character / String Data Types

String types store text.

Common types:

```text
CHAR
VARCHAR
TEXT
```

---

# 14. CHAR

`CHAR(n)` stores fixed-length character data.

Example:

```sql
country_code CHAR(2)
```

Possible values:

```text
IN
US
UK
```

It is useful when values have a known fixed length.

---

# 15. VARCHAR

`VARCHAR(n)` stores variable-length character data.

Example:

```sql
CREATE TABLE employees (
    name VARCHAR(100)
);
```

Possible values:

```text
Rahul
Priya Sharma
Arun Kumar
```

The maximum length is specified by `n` in systems that use this syntax.

---

# 16. TEXT

`TEXT` is used for larger amounts of text in databases that support it.

Example:

```sql
CREATE TABLE articles (
    article_id INT,
    content TEXT
);
```

Useful for:

* Articles
* Descriptions
* Comments
* Large text content

The exact limits and indexing behavior depend on the DBMS.

---

# 17. CHAR vs VARCHAR

| CHAR                                          | VARCHAR                        |
| --------------------------------------------- | ------------------------------ |
| Fixed-length                                  | Variable-length                |
| Useful for fixed-size values                  | Useful for varying text        |
| Can be less suitable for highly variable text | Common for names, emails, etc. |

Example:

```text
Country Code → CHAR(2)
Name         → VARCHAR(100)
Email        → VARCHAR(255)
```

---

# 18. VARCHAR vs TEXT

| VARCHAR                           | TEXT                                 |
| --------------------------------- | ------------------------------------ |
| Commonly used for bounded strings | Commonly used for larger text        |
| Length can be specified           | Size/limits depend on DBMS           |
| Often used for names/emails       | Often used for descriptions/articles |

The practical differences depend on the database system.

---

# 19. DATE

Stores a calendar date.

Example:

```sql
CREATE TABLE employees (
    joining_date DATE
);
```

Example value:

```text
2026-08-08
```

Contains:

```text
Year
Month
Day
```

---

# 20. TIME

Stores time of day.

Example:

```sql
CREATE TABLE schedules (
    start_time TIME
);
```

Example:

```text
09:30:00
```

---

# 21. DATETIME

Stores date and time in database systems that support this type.

Example:

```text
2026-08-08 10:30:00
```

Support and semantics vary between DBMSs.

---

# 22. TIMESTAMP

Stores a date/time value with database-specific semantics.

Example:

```sql
created_at TIMESTAMP
```

It is commonly used for:

```text
Created time
Updated time
Event time
Transaction time
```

---

# 23. DATE vs TIME vs DATETIME vs TIMESTAMP

| Type      | Stores                                  |
| --------- | --------------------------------------- |
| DATE      | Date                                    |
| TIME      | Time                                    |
| DATETIME  | Date + Time                             |
| TIMESTAMP | Date + Time with DBMS-specific behavior |

Important:

> `TIMESTAMP` behavior differs between database systems, especially regarding time zones and automatic/default behavior.

---

# 24. BOOLEAN

Used for true/false values.

Example:

```sql
CREATE TABLE users (
    user_id INT,
    is_active BOOLEAN
);
```

Values conceptually:

```text
TRUE
FALSE
```

The exact physical implementation varies by database.

---

# 25. BINARY Data Types

Binary types store raw bytes.

Examples:

```text
BINARY
VARBINARY
BLOB
```

Depending on the DBMS, they may be used for:

* Binary files
* Hashes
* Encoded data
* Images
* Other byte sequences

Example:

```sql
CREATE TABLE files (
    file_id INT,
    file_data BLOB
);
```

For large files, many applications instead store files in object storage and keep only metadata/URLs in the database.

---

# 26. JSON

Some modern databases provide a JSON data type.

Example:

```sql
CREATE TABLE users (
    user_id INT,
    profile JSON
);
```

Possible JSON value:

```json
{
    "city": "Hyderabad",
    "age": 22,
    "skills": ["Python", "SQL"]
}
```

Useful when semi-structured data must be stored.

---

# 27. UUID

Some databases support UUID as a native type.

Example:

```text
550e8400-e29b-41d4-a716-446655440000
```

Useful as identifiers, especially in distributed systems.

---

# 28. Choosing Data Types

Choose a data type based on:

```text
What type of value?
How large can it become?
Does it require exact precision?
How will it be queried?
How much storage is appropriate?
```

Example:

```text
Age          → INT
Salary       → DECIMAL
Name         → VARCHAR
Description  → TEXT
Birth Date   → DATE
Created At   → TIMESTAMP
Active?      → BOOLEAN
```

---

# 29. Example Table with Multiple Data Types

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    age INT,
    salary DECIMAL(10,2),
    joining_date DATE,
    joining_time TIME,
    is_active BOOLEAN,
    profile JSON
);
```

---

# 30. SQL Keys

A **key** is a column or combination of columns used to identify rows or establish relationships between tables.

Important keys:

```text
Super Key
Candidate Key
Primary Key
Alternate Key
Foreign Key
Composite Key
Natural Key
Surrogate Key
```

---

# 31. Why Are Keys Important?

Keys help with:

```text
Unique Identification
Relationships
Data Integrity
Avoiding Duplicate Records
Joining Tables
Referential Integrity
Database Design
```

---

# 32. Super Key

A **super key** is any set of one or more columns that can uniquely identify a row.

Example:

```text
employees

employee_id
email
```

Suppose both are unique.

Then:

```text
employee_id
```

is a super key.

Also:

```text
employee_id + name
```

is technically a super key because it still uniquely identifies the row.

But it contains unnecessary attributes.

---

# 33. Candidate Key

A **candidate key** is a minimal super key.

Suppose:

```text
employee_id → unique
email       → unique
```

Then:

```text
employee_id
email
```

can both be candidate keys.

One can be selected as the primary key.

---

# 34. Primary Key

A **primary key** uniquely identifies each row in a table.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Here:

```text
employee_id
```

is the primary key.

---

# 35. Properties of Primary Key

A primary key:

```text
Must uniquely identify rows
Cannot contain NULL values
Can be one column or multiple columns
There is one PRIMARY KEY constraint per table
```

Example:

```text
employee_id
-----------
1
2
3
4
```

Cannot have:

```text
1
2
2
```

because the values must be unique.

---

# 36. Primary Key Example

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

Valid:

```sql
INSERT INTO students
VALUES (1, 'Rahul', 22);
```

Invalid duplicate:

```sql
INSERT INTO students
VALUES (1, 'Priya', 21);
```

The second row violates the primary key constraint.

---

# 37. Alternate Key

If multiple candidate keys exist, the candidate key not selected as the primary key is an **alternate key**.

Example:

```text
Candidate Keys:

employee_id
email
```

Choose:

```text
employee_id → Primary Key
```

Then:

```text
email → Alternate Key
```

A `UNIQUE` constraint is commonly used to enforce uniqueness of an alternate candidate key.

---

# 38. Foreign Key

A **foreign key** is a column or group of columns that references a key in another table.

Example:

```text
departments
-------------
department_id
```

```text
employees
-------------
employee_id
department_id
```

Relationship:

```text
employees.department_id
          ↓
departments.department_id
```

---

# 39. Foreign Key Example

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

---

# 40. Why Foreign Keys Are Important

Foreign keys help enforce:

```text
Referential Integrity
Relationships
Valid References
```

For example, if department `10` does not exist, an employee generally cannot reference department `10` when the foreign-key constraint is enforced and no special action permits it.

---

# 41. Composite Key

A **composite key** contains two or more columns.

Example:

```text
student_id
course_id
```

Together they identify an enrollment.

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id)
);
```

---

# 42. Why Composite Keys?

Suppose:

```text
student_id | course_id
-----------+----------
1          | 101
1          | 102
2          | 101
```

A student can take multiple courses.

A course can have multiple students.

Therefore:

```text
(student_id, course_id)
```

uniquely identifies each enrollment.

---

# 43. Natural Key

A natural key comes from real-world/business data.

Examples:

```text
ISBN
Email
National ID
Product Code
```

Example:

```sql
email VARCHAR(255) UNIQUE
```

If email is guaranteed by the business to be unique and suitable as an identifier, it can be a candidate/natural key.

---

# 44. Surrogate Key

A surrogate key is an artificial identifier generated for database purposes.

Example:

```text
employee_id = 101
```

It has no business meaning.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

The ID exists mainly to identify the record.

---

# 45. Natural Key vs Surrogate Key

| Natural Key              | Surrogate Key                   |
| ------------------------ | ------------------------------- |
| Comes from business data | Artificial identifier           |
| Has business meaning     | Usually no business meaning     |
| May change               | Often designed to remain stable |
| Example: ISBN            | Example: generated ID           |
| Can be wider/complex     | Often simple                    |

---

# 46. Key Hierarchy

```text
Keys
│
├── Super Key
│
├── Candidate Key
│   ├── Primary Key
│   └── Alternate Key
│
├── Foreign Key
│
├── Composite Key
│
├── Natural Key
│
└── Surrogate Key
```

Important relationship:

```text
Super Key
    ↓
Candidate Key
    ↓
Primary Key
```

A candidate key is a **minimal** super key.

---

# 47. SQL Constraints

A **constraint** is a rule applied to table data.

Constraints help maintain:

```text
Accuracy
Validity
Uniqueness
Consistency
Integrity
```

---

# 48. Main SQL Constraints

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# 49. PRIMARY KEY Constraint

Ensures that the primary key uniquely identifies each row.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

It combines the key's identification role with required non-null uniqueness.

---

# 50. NOT NULL Constraint

Ensures that a column cannot contain `NULL`.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

This is invalid:

```sql
INSERT INTO employees
(employee_id, name)
VALUES
(1, NULL);
```

---

# 51. UNIQUE Constraint

Ensures that duplicate values are not allowed according to the database's uniqueness semantics.

Example:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

This prevents duplicate email values under the constraint.

---

# 52. UNIQUE vs PRIMARY KEY

| PRIMARY KEY                          | UNIQUE                                                             |
| ------------------------------------ | ------------------------------------------------------------------ |
| Identifies the row                   | Enforces uniqueness                                                |
| One primary key constraint per table | Multiple UNIQUE constraints can be defined                         |
| Cannot contain NULL                  | NULL handling varies by DBMS                                       |
| Commonly referenced by foreign keys  | Can also be referenced in systems when it is a suitable unique key |
| Main row identifier                  | Additional uniqueness rule                                         |

Important:

> The exact treatment of `NULL` in a `UNIQUE` constraint varies between DBMSs.

---

# 53. CHECK Constraint

Ensures that values satisfy a condition.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    salary DECIMAL(10,2)
        CHECK (salary >= 0)
);
```

Invalid:

```text
salary = -5000
```

---

# 54. CHECK with Age

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    age INT CHECK (age >= 0 AND age <= 120)
);
```

This prevents values outside the defined range.

---

# 55. CHECK with Status

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    status VARCHAR(20)
        CHECK (status IN ('Active', 'Inactive'))
);
```

Only the defined values are allowed, subject to DBMS behavior.

---

# 56. DEFAULT Constraint

Provides a default value when a value is omitted.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'Active'
);
```

Insert:

```sql
INSERT INTO employees (employee_id)
VALUES (1);
```

The database can store:

```text
employee_id → 1
status      → Active
```

---

# 57. FOREIGN KEY Constraint

Ensures that a foreign-key value references a valid key in another table, subject to the foreign-key rules.

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

---

# 58. ON DELETE

A foreign key can define what happens when the referenced row is deleted.

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
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON DELETE CASCADE
);
```

`CASCADE` means related child rows can be deleted when the referenced parent row is deleted, according to the DBMS's foreign-key semantics.

---

# 59. ON UPDATE

A foreign key can also define behavior when referenced key values are updated.

Example:

```sql
FOREIGN KEY (department_id)
REFERENCES departments(department_id)
ON UPDATE CASCADE
```

Exact support varies by DBMS.

---

# 60. Constraint Naming

Constraints can be explicitly named.

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    salary DECIMAL(10,2),

    CONSTRAINT pk_employees
        PRIMARY KEY (employee_id),

    CONSTRAINT chk_salary
        CHECK (salary >= 0)
);
```

Naming constraints makes database administration and debugging easier.

---

# 61. Complete Table Example

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,

    name VARCHAR(100) NOT NULL,

    email VARCHAR(255) UNIQUE,

    age INT CHECK (age >= 18),

    salary DECIMAL(10,2)
        CHECK (salary >= 0),

    status VARCHAR(20)
        DEFAULT 'Active',

    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This table uses:

```text
PRIMARY KEY
NOT NULL
UNIQUE
CHECK
DEFAULT
FOREIGN KEY
```

---

# 62. Column-Level Constraint

A constraint can be defined directly beside a column.

Example:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

---

# 63. Table-Level Constraint

A constraint can also be defined separately at table level.

Example:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,

    CONSTRAINT pk_enrollment
        PRIMARY KEY (student_id, course_id)
);
```

Table-level constraints are particularly useful for composite keys and relationships involving multiple columns.

---

# 64. Multiple Constraints on One Column

A column can have multiple constraints.

Example:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,

    email VARCHAR(255)
        NOT NULL
        UNIQUE
);
```

Here `email` must:

```text
NOT NULL
+
UNIQUE
```

---

# 65. Constraints Example

Consider:

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    sku VARCHAR(50) UNIQUE,
    price DECIMAL(10,2) CHECK (price >= 0),
    status VARCHAR(20) DEFAULT 'Available'
);
```

Meaning:

```text
product_id
→ PRIMARY KEY

product_name
→ NOT NULL

sku
→ UNIQUE

price
→ CHECK

status
→ DEFAULT
```

---

# 66. Key vs Constraint

These concepts are related but not identical.

### Key

Used to identify rows or establish relationships.

Examples:

```text
Primary Key
Candidate Key
Foreign Key
```

### Constraint

A rule enforced by the database.

Examples:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

Primary and foreign keys are both **keys** and are also implemented through **constraints** in SQL.

---

# 67. Key vs Index

Do not confuse keys with indexes.

### Key

Represents identification or relationship semantics.

### Index

A data structure primarily used to improve data access performance.

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

An index is not automatically the same thing as a key.

---

# 68. Primary Key vs Foreign Key

| Primary Key                          | Foreign Key                       |
| ------------------------------------ | --------------------------------- |
| Identifies a row                     | References a key in another table |
| Must be unique                       | Values can repeat                 |
| Cannot be NULL                       | May be NULL if allowed            |
| Defines entity identity              | Defines relationship              |
| One primary key constraint per table | Multiple foreign keys can exist   |

Example:

```text
departments
department_id ← Primary Key
       ↑
       │
employees
department_id ← Foreign Key
```

---

# 69. Primary Key vs Unique Key

| Primary Key                     | UNIQUE                               |
| ------------------------------- | ------------------------------------ |
| Main row identifier             | Additional uniqueness rule           |
| One primary key constraint      | Multiple UNIQUE constraints possible |
| NULL not allowed                | NULL behavior depends on DBMS        |
| Commonly used as referenced key | Can be a candidate key when suitable |

---

# 70. Foreign Key vs Primary Key

Consider:

```text
departments
```

```text
department_id
```

is:

```text
PRIMARY KEY
```

In:

```text
employees
```

```text
department_id
```

is:

```text
FOREIGN KEY
```

Relationship:

```text
departments
     1
     │
     │
     N
     ↓
employees
```

One department can have many employees.

---

# 71. Constraints and Data Integrity

Constraints help enforce different forms of integrity.

```text
PRIMARY KEY
     ↓
Entity Integrity

FOREIGN KEY
     ↓
Referential Integrity

NOT NULL / CHECK / Data Types
     ↓
Domain/Data Validity

UNIQUE
     ↓
Uniqueness
```

---

# 72. Constraint Summary

| Constraint  | Purpose                   |
| ----------- | ------------------------- |
| PRIMARY KEY | Uniquely identifies rows  |
| FOREIGN KEY | Maintains relationships   |
| UNIQUE      | Prevents duplicate values |
| NOT NULL    | Prevents NULL values      |
| CHECK       | Validates a condition     |
| DEFAULT     | Supplies a default value  |

---

# 73. Complete Example

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,

    department_name VARCHAR(100)
        NOT NULL
        UNIQUE
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,

    name VARCHAR(100)
        NOT NULL,

    email VARCHAR(255)
        NOT NULL
        UNIQUE,

    age INT
        CHECK (age >= 18),

    salary DECIMAL(10,2)
        CHECK (salary >= 0),

    status VARCHAR(20)
        DEFAULT 'Active',

    department_id INT,

    CONSTRAINT fk_employee_department
        FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

# 74. How the Tables Are Related

```text
┌──────────────────────┐
│     departments      │
├──────────────────────┤
│ PK department_id     │
│ department_name      │
└──────────┬───────────┘
           │
           │ 1
           │
           │ N
           ↓
┌──────────────────────┐
│      employees       │
├──────────────────────┤
│ PK employee_id       │
│ name                 │
│ email                │
│ age                  │
│ salary               │
│ status               │
│ FK department_id     │
└──────────────────────┘
```

---

# 75. Quick Revision

## Data Types

```text
INT
BIGINT
DECIMAL
NUMERIC
FLOAT
CHAR
VARCHAR
TEXT
DATE
TIME
DATETIME
TIMESTAMP
BOOLEAN
BINARY
VARBINARY
BLOB
JSON
UUID
```

---

## Keys

```text
Super Key
Candidate Key
Primary Key
Alternate Key
Foreign Key
Composite Key
Natural Key
Surrogate Key
```

---

## Constraints

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# 76. Interview Questions

### Q1. What is a primary key?

A primary key uniquely identifies each row in a table and cannot contain NULL values.

### Q2. Can a table have multiple primary keys?

No. A table has one primary key constraint, although that primary key can consist of multiple columns.

### Q3. Can a table have multiple foreign keys?

Yes.

### Q4. Can a foreign key contain duplicate values?

Yes.

### Q5. Can a foreign key contain NULL?

Yes, if the column permits NULL and the relationship/database rules allow it.

### Q6. What is a composite key?

A key consisting of multiple columns.

### Q7. What is a candidate key?

A minimal super key that can uniquely identify a row.

### Q8. What is an alternate key?

A candidate key that was not selected as the primary key.

### Q9. What is a foreign key?

A column or set of columns that references a key in another table.

### Q10. What is a UNIQUE constraint?

A constraint that prevents duplicate values according to the database's uniqueness rules.

### Q11. What is the difference between `NULL` and `0`?

```text
NULL → Missing/unknown/not applicable
0    → Actual numeric value zero
```

### Q12. What is the difference between `CHAR` and `VARCHAR`?

```text
CHAR    → Fixed-length character data
VARCHAR → Variable-length character data
```

### Q13. What is the difference between `DECIMAL` and `FLOAT`?

```text
DECIMAL → Exact decimal arithmetic
FLOAT   → Approximate floating-point representation
```

### Q14. What is referential integrity?

It ensures that foreign-key relationships reference valid rows according to the defined constraints.

---

# 77. Final Memory Map

```text
                  SQL
                   │
        ┌──────────┴──────────┐
        ↓                     ↓
   DATA TYPES                KEYS
        │                     │
 ┌──────┼──────┐       ┌──────┼────────┐
 ↓      ↓      ↓       ↓      ↓        ↓
Numeric Text  Date   Primary Foreign Composite
        │                     │
        └──────────┬──────────┘
                   ↓
              CONSTRAINTS
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
    NOT NULL     UNIQUE       CHECK
       │           │           │
       └───────────┼───────────┘
                   ↓
              DATA INTEGRITY
                   │
                   ↓
             RELIABLE DATABASE
```

> **Remember:**
> **Data Types** define *what values can be stored*.
> **Keys** define *how rows are identified and related*.
> **Constraints** define *what rules the data must follow*.

