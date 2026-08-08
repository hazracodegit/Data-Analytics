# SQL — Normalization, Denormalization, Stored Procedures & Functions

> Complete revision notes with **technical definitions + easy explanations + examples + SQL code**.

---

# Table of Contents

1. [Normalization](#1-normalization)
2. [Why Normalization is Needed](#2-why-normalization-is-needed)
3. [Data Anomalies](#3-data-anomalies)
4. [Functional Dependency](#4-functional-dependency)
5. [Keys and Normalization](#5-keys-and-normalization)
6. [First Normal Form — 1NF](#6-first-normal-form--1nf)
7. [Second Normal Form — 2NF](#7-second-normal-form--2nf)
8. [Third Normal Form — 3NF](#8-third-normal-form--3nf)
9. [BCNF](#9-bcnf)
10. [Fourth Normal Form — 4NF](#10-fourth-normal-form--4nf)
11. [Fifth Normal Form — 5NF](#11-fifth-normal-form--5nf)
12. [DKNF](#12-domain-key-normal-form--dknf)
13. [Normal Forms Comparison](#13-normal-forms-comparison)
14. [Normalization Example](#14-complete-normalization-example)
15. [Advantages of Normalization](#15-advantages-of-normalization)
16. [Disadvantages of Normalization](#16-disadvantages-of-normalization)
17. [Denormalization](#17-denormalization)
18. [Normalization vs Denormalization](#18-normalization-vs-denormalization)
19. [Stored Procedures](#19-stored-procedures)
20. [Procedure Syntax](#20-procedure-syntax)
21. [Procedure Parameters](#21-procedure-parameters)
22. [IN, OUT and INOUT Parameters](#22-in-out-and-inout-parameters)
23. [Procedure with Conditions](#23-procedure-with-conditions)
24. [Procedure with Transactions](#24-procedure-with-transactions)
25. [Stored Procedure Advantages](#25-stored-procedure-advantages)
26. [Stored Procedure Disadvantages](#26-stored-procedure-disadvantages)
27. [SQL Functions](#27-sql-functions)
28. [Built-in Functions vs User-Defined Functions](#28-built-in-functions-vs-user-defined-functions)
29. [Scalar Functions](#29-scalar-functions)
30. [Table-Valued Functions](#30-table-valued-functions)
31. [User-Defined Functions](#31-user-defined-functions)
32. [Function Parameters](#32-function-parameters)
33. [Function Examples](#33-function-examples)
34. [Procedure vs Function](#34-procedure-vs-function)
35. [Normalization + Procedures + Functions](#35-normalization--procedures--functions)
36. [Interview Revision](#36-interview-revision)
37. [One-Line Revision](#37-one-line-revision)

---

# 1. Normalization

## Technical Definition

**Normalization** is the systematic process of organizing data in a relational database to reduce redundancy, eliminate undesirable dependencies, and improve data integrity.

## Easy Meaning

Normalization means:

> **Breaking a large table into smaller related tables so that data is stored efficiently without unnecessary repetition.**

---

# 2. Why Normalization is Needed

Suppose we have:

```text
Student_ID | Student_Name | Course | Instructor
-----------|--------------|--------|-----------
1          | Alice        | Python | John
2          | Bob          | Python | John
3          | Charlie      | Python | John
4          | David        | SQL    | Mike
```

Notice:

```text
Python → John
```

is repeated multiple times.

If 10,000 students take Python, `John` may be repeated 10,000 times.

Normalization can separate this information.

```text
STUDENTS
---------
student_id
student_name

COURSES
-------
course_id
course_name
instructor_id

INSTRUCTORS
-----------
instructor_id
instructor_name
```

Then tables are connected using keys.

---

# 3. Data Anomalies

Poorly designed tables can create three major problems.

```text
INSERT ANOMALY
UPDATE ANOMALY
DELETE ANOMALY
```

---

# 3.1 Insert Anomaly

## Technical Definition

An **insert anomaly** occurs when a table structure prevents us from inserting a fact without also inserting unrelated data.

## Easy Meaning

You cannot add one piece of information without adding unnecessary information.

Example:

```text
Student_ID | Student_Name | Course | Instructor
-----------|--------------|--------|-----------
1          | Alice        | Python | John
```

Suppose John starts teaching a new course, but no student has enrolled yet.

You may not be able to store the course properly because the table expects student information.

---

# 3.2 Update Anomaly

## Technical Definition

An **update anomaly** occurs when the same fact is stored in multiple rows and updating that fact requires changing multiple records.

Example:

```text
Student_ID | Student | Course | Instructor
-----------|---------|--------|-----------
1          | Alice   | Python | John
2          | Bob     | Python | John
3          | Charlie | Python | John
```

If John changes his name to Jonathan:

```text
John → Jonathan
```

you must update multiple rows.

If one row is forgotten:

```text
Alice   → Jonathan
Bob     → Jonathan
Charlie → John
```

the database becomes inconsistent.

---

# 3.3 Delete Anomaly

## Technical Definition

A **delete anomaly** occurs when deleting a record unintentionally removes other important information.

Example:

```text
Student_ID | Student | Course
-----------|---------|-------
1          | Alice   | Python
2          | Bob     | SQL
```

If Bob is the only student enrolled in SQL and we delete Bob:

```sql
DELETE FROM students
WHERE student_id = 2;
```

we may also lose the only stored information about the SQL course.

---

# 4. Functional Dependency

Functional dependency is one of the most important concepts behind normalization.

## Technical Definition

A functional dependency exists when the value of one attribute uniquely determines the value of another attribute.

Written as:

```text
A → B
```

Read as:

> A determines B.

---

## Example

```text
student_id → student_name
```

If we know:

```text
student_id = 101
```

we can determine:

```text
student_name = Alice
```

Therefore:

```text
student_id → student_name
```

---

# 4.1 Determinant

The attribute on the left side of a functional dependency is called the **determinant**.

```text
student_id → student_name
     ↑
 determinant
```

---

# 4.2 Dependent Attribute

The attribute on the right side is called the **dependent attribute**.

```text
student_id → student_name
                ↑
             dependent
```

---

# 4.3 Full Functional Dependency

An attribute is fully functionally dependent on a composite key when it depends on the entire key and not just part of it.

Example:

```text
(student_id, course_id) → grade
```

`grade` depends on both:

```text
student_id
+
course_id
```

---

# 4.4 Partial Dependency

A **partial dependency** occurs when a non-key attribute depends on only part of a composite key.

Example:

```text
(student_id, course_id) → grade
student_id → student_name
```

Here:

```text
student_name
```

depends only on:

```text
student_id
```

not the complete composite key.

This is a problem addressed by **2NF**.

---

# 4.5 Transitive Dependency

A **transitive dependency** occurs when a non-key attribute depends on another non-key attribute rather than directly on the key.

Example:

```text
employee_id → department_id
department_id → department_name
```

Therefore:

```text
employee_id → department_name
```

indirectly.

This is called a transitive dependency.

3NF addresses this type of dependency.

---

# 5. Keys and Normalization

Understanding keys is important before learning normal forms.

## Super Key

A set of one or more attributes that uniquely identifies a row.

Example:

```text
student_id
```

---

## Candidate Key

A minimal super key.

Example:

```text
student_id
email
```

if both uniquely identify a student.

---

## Primary Key

The candidate key selected to uniquely identify rows.

```sql
PRIMARY KEY (student_id)
```

---

## Composite Key

A key containing multiple columns.

```sql
PRIMARY KEY (student_id, course_id)
```

---

## Foreign Key

A column that references a key in another table.

```sql
FOREIGN KEY (department_id)
REFERENCES departments(department_id)
```

---

# 6. First Normal Form — 1NF

## Technical Definition

A relation is in **First Normal Form (1NF)** when each attribute contains atomic values and there are no repeating groups or multi-valued attributes within a single cell.

## Easy Meaning

**One cell = One value.**

---

## ❌ Not 1NF

```text
student_id | student_name | phone_numbers
-----------|--------------|--------------
1          | Alice        | 9876, 8765
```

One cell contains multiple phone numbers.

---

## ✅ 1NF

```text
student_id | student_name | phone
-----------|--------------|-------
1          | Alice        | 9876
1          | Alice        | 8765
```

Or preferably, use a separate table:

```text
STUDENTS
---------
student_id
student_name

STUDENT_PHONES
--------------
student_id
phone
```

---

# 6.1 Rules of 1NF

A table should have:

```text
✓ Atomic values
✓ No repeating groups
✓ One value per cell
✓ Rows identifiable
```

---

# 7. Second Normal Form — 2NF

## Technical Definition

A relation is in **Second Normal Form (2NF)** when it is in 1NF and every non-key attribute is fully functionally dependent on the entire candidate key.

## Easy Meaning

2NF means:

> **Already in 1NF + no partial dependency.**

Important:

**Partial dependency matters when the key is composite.**

---

# 7.1 Example

Suppose:

```text
ENROLLMENT
--------------------------------
student_id
course_id
student_name
course_name
grade
```

Primary key:

```text
(student_id, course_id)
```

Dependencies:

```text
student_id → student_name

course_id → course_name

(student_id, course_id) → grade
```

Problem:

```text
student_name
```

depends only on:

```text
student_id
```

and:

```text
course_name
```

depends only on:

```text
course_id
```

These are partial dependencies.

---

# 7.2 Convert to 2NF

Create:

```text
STUDENTS
---------
student_id
student_name
```

```text
COURSES
-------
course_id
course_name
```

```text
ENROLLMENT
----------
student_id
course_id
grade
```

Now:

```text
student_id + course_id → grade
```

The non-key attribute depends on the complete composite key.

---

# 7.3 Important 2NF Point

If a table has a **single-column primary key**, it is automatically free from partial dependency.

Therefore:

```text
Single-column key
      ↓
Partial dependency impossible
      ↓
If table is 1NF
      ↓
It satisfies 2NF
```

---

# 8. Third Normal Form — 3NF

## Technical Definition

A relation is in **Third Normal Form (3NF)** when it is in 2NF and has no transitive dependency of non-key attributes on a candidate key.

A common formal formulation is:

> For every functional dependency `X → A`, either `X` is a superkey or `A` is a prime attribute.

## Easy Meaning

3NF means:

> **2NF + remove transitive dependencies.**

---

# 8.1 Example

Suppose:

```text
EMPLOYEES
--------------------------------
employee_id
employee_name
department_id
department_name
```

Dependencies:

```text
employee_id → employee_name
employee_id → department_id
department_id → department_name
```

Therefore:

```text
employee_id → department_name
```

through:

```text
department_id
```

This is a transitive dependency.

---

# 8.2 Convert to 3NF

Create:

```text
EMPLOYEES
---------
employee_id
employee_name
department_id
```

And:

```text
DEPARTMENTS
-----------
department_id
department_name
```

Relationship:

```text
EMPLOYEES
    |
    | department_id
    ↓
DEPARTMENTS
```

---

# 8.3 Easy Rule

```text
1NF
 ↓
Remove repeating/multi-valued data

2NF
 ↓
Remove partial dependency

3NF
 ↓
Remove transitive dependency
```

---

# 9. BCNF

## Boyce-Codd Normal Form

### Technical Definition

A relation is in **BCNF** if, for every non-trivial functional dependency:

```text
X → Y
```

`X` is a superkey.

### Easy Meaning

BCNF is a **stronger version of 3NF**.

Every determinant must be a candidate key/superkey.

---

# 9.1 3NF vs BCNF

```text
BCNF
 ↑
Stronger
 ↑
3NF
```

Every BCNF relation satisfies 3NF, but a 3NF relation may not satisfy BCNF.

---

# 9.2 Example Concept

Consider:

```text
STUDENT_COURSE
----------------
student
course
instructor
```

Suppose:

```text
(student, course) → instructor
instructor → course
```

If:

```text
instructor
```

is not a superkey, then:

```text
instructor → course
```

violates BCNF.

The table may need decomposition.

---

# 10. Fourth Normal Form — 4NF

## Technical Definition

A relation is in **Fourth Normal Form (4NF)** if it is in BCNF and contains no non-trivial multivalued dependencies except those whose determinant is a superkey.

## Easy Meaning

4NF deals mainly with **independent multi-valued facts**.

---

# 10.1 Example

Suppose:

```text
STUDENT
--------------------------------
student | skill | hobby
```

Alice has:

```text
Skills:
Python
SQL
Java
```

and hobbies:

```text
Reading
Music
Travel
```

If skills and hobbies are independent, we may get combinations:

```text
Alice | Python | Reading
Alice | Python | Music
Alice | Python | Travel
Alice | SQL    | Reading
Alice | SQL    | Music
Alice | SQL    | Travel
...
```

This creates unnecessary combinations.

---

# 10.2 Convert to 4NF

Separate the independent multi-valued facts:

```text
STUDENT_SKILLS
--------------
student
skill
```

```text
STUDENT_HOBBIES
---------------
student
hobby
```

Now the independent facts are separated.

---

# 11. Multivalued Dependency

### Technical Definition

A multivalued dependency exists when one attribute determines a set of values for another attribute independently of other attributes.

Notation:

```text
A →→ B
```

Read as:

```text
A multidetermines B
```

4NF primarily addresses problematic multivalued dependencies.

---

# 12. Fifth Normal Form — 5NF

## Project-Join Normal Form

### Technical Definition

A relation is in **Fifth Normal Form (5NF)**, or **Project-Join Normal Form (PJ/NF)**, when every non-trivial join dependency is implied by candidate keys.

## Easy Meaning

5NF handles situations where a table can be decomposed into smaller tables and later reconstructed using joins without introducing incorrect combinations.

It is mainly concerned with complex **join dependencies**.

---

# 12.1 Example Concept

Imagine a business involving:

```text
SUPPLIER
PRODUCT
PROJECT
```

and the rule is that a supplier supplies a product to a project.

A complex relationship may sometimes be represented through multiple smaller relationships:

```text
SUPPLIER_PRODUCT
SUPPLIER_PROJECT
PRODUCT_PROJECT
```

5NF asks whether such decomposition and reconstruction is logically valid without generating false combinations.

---

# 12.2 Practical Importance

In everyday application development:

```text
1NF
2NF
3NF
```

are extremely common.

```text
BCNF
4NF
5NF
```

are important for database design knowledge but are less frequently required in ordinary application schemas.

---

# 13. Domain-Key Normal Form — DKNF

### Technical Definition

**Domain-Key Normal Form (DKNF)** is a theoretical normal form where every constraint on the relation is a logical consequence of domain constraints and key constraints.

### Easy Meaning

All business rules should ideally be enforceable through:

```text
Domain constraints
+
Key constraints
```

without requiring additional complex relational constraints.

### Practical Note

DKNF is mainly a theoretical database-design concept and is rarely implemented directly in typical application development.

---

# 14. Normal Forms Comparison

| Normal Form | Main Goal                                   |
| ----------- | ------------------------------------------- |
| 1NF         | Atomic values, no repeating groups          |
| 2NF         | Remove partial dependencies                 |
| 3NF         | Remove transitive dependencies              |
| BCNF        | Every determinant is a superkey             |
| 4NF         | Remove problematic multivalued dependencies |
| 5NF         | Remove problematic join dependencies        |
| DKNF        | Constraints derive from domains and keys    |

---

# 15. Complete Normalization Example

Suppose we start with:

```text
ORDER_ID
CUSTOMER_NAME
CUSTOMER_PHONE
PRODUCT_NAME
PRODUCT_PRICE
QUANTITY
```

Example:

```text
Order_ID | Customer | Phone | Product | Price | Quantity
---------|----------|-------|---------|-------|---------
101      | Alice    | 9876  | Laptop  | 60000 | 1
101      | Alice    | 9876  | Mouse   | 1000  | 2
102      | Bob      | 8765  | Laptop  | 60000 | 1
```

---

# 15.1 Problems

Customer information repeats:

```text
Alice | 9876
Alice | 9876
```

Product information repeats:

```text
Laptop | 60000
Laptop | 60000
```

This can create update anomalies.

---

# 15.2 Normalized Design

### CUSTOMERS

```text
customer_id
customer_name
phone
```

### PRODUCTS

```text
product_id
product_name
price
```

### ORDERS

```text
order_id
customer_id
order_date
```

### ORDER_ITEMS

```text
order_id
product_id
quantity
```

Relationships:

```text
CUSTOMERS
    |
    | 1:N
    ↓
ORDERS
    |
    | 1:N
    ↓
ORDER_ITEMS
    ↑
    | N:1
    |
PRODUCTS
```

---

# 15.3 SQL Design

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    phone VARCHAR(20)
);
```

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);
```

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE NOT NULL,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,

    PRIMARY KEY (order_id, product_id),

    FOREIGN KEY (order_id)
        REFERENCES orders(order_id),

    FOREIGN KEY (product_id)
        REFERENCES products(product_id)
);
```

---

# 16. Advantages of Normalization

Normalization provides:

### 1. Less Data Redundancy

The same information is not unnecessarily repeated.

### 2. Better Data Consistency

A fact is generally maintained in one appropriate location.

### 3. Easier Updates

Changing one fact doesn't require updating many duplicate rows.

### 4. Prevents Anomalies

Helps prevent:

```text
Insert anomaly
Update anomaly
Delete anomaly
```

### 5. Better Data Integrity

Relationships and constraints can be clearly defined.

### 6. Smaller Tables

Information is separated into logically related entities.

---

# 17. Disadvantages of Normalization

Highly normalized databases can also have disadvantages.

### 1. More Tables

You may end up with many related tables.

### 2. More JOINs

Retrieving information may require multiple joins.

```sql
SELECT ...
FROM orders
JOIN customers ...
JOIN order_items ...
JOIN products ...;
```

### 3. Query Complexity

Queries can become more complex.

### 4. Potential Performance Cost

Complex joins can sometimes increase query cost, especially for analytical workloads.

This depends heavily on:

* Indexes
* Data size
* Query design
* Database engine
* Hardware
* Workload

---

# 18. Denormalization

## Technical Definition

**Denormalization** is the intentional introduction of controlled redundancy into a database schema to improve read performance, simplify queries, or support specific workloads.

## Easy Meaning

Denormalization means:

> **Intentionally storing some repeated data to make reading data faster or easier.**

---

# 18.1 Normalized

```text
ORDERS
------
order_id
customer_id

CUSTOMERS
---------
customer_id
customer_name
```

To get customer name:

```sql
SELECT
    o.order_id,
    c.customer_name
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

---

# 18.2 Denormalized

We could store:

```text
ORDERS
--------------------------------
order_id
customer_id
customer_name
```

Now the query is simpler:

```sql
SELECT
    order_id,
    customer_name
FROM orders;
```

But:

```text
customer_name
```

is duplicated.

If the customer changes their name, multiple records may need updating.

---

# 18.3 Why Denormalize?

Common reasons:

```text
✓ Faster reads
✓ Fewer JOINs
✓ Simpler reporting queries
✓ Analytics workloads
✓ Data warehouses
✓ Dashboards
✓ Precomputed summaries
```

---

# 18.4 Examples of Denormalization

## Duplicate Attribute

```text
orders
-------
customer_id
customer_name
```

---

## Precomputed Total

Instead of calculating every time:

```sql
SELECT SUM(quantity * price)
FROM order_items;
```

we may store:

```text
order_total
```

---

## Summary Table

Instead of repeatedly calculating:

```text
Daily sales
Monthly sales
Product sales
```

we may maintain summary tables.

```text
DAILY_SALES
-----------
sale_date
total_sales
order_count
```

---

# 18.5 Denormalization Trade-Off

Denormalization gives:

```text
Faster reads
     ↓
But
     ↓
More redundancy
     ↓
More update complexity
```

---

# 19. Normalization vs Denormalization

| Normalization                  | Denormalization                                  |
| ------------------------------ | ------------------------------------------------ |
| Reduces redundancy             | Introduces controlled redundancy                 |
| Improves consistency           | Can complicate consistency                       |
| More tables                    | Fewer/combined tables                            |
| More joins                     | Fewer joins                                      |
| Good for transactional systems | Often useful for read-heavy/analytical workloads |
| Easier updates                 | Can require multiple updates                     |
| Data integrity focus           | Read performance focus                           |

---

# 20. OLTP vs OLAP

This distinction is important.

## OLTP

**Online Transaction Processing**

Examples:

```text
Banking
E-commerce orders
Payments
Booking systems
```

Usually benefits from:

```text
Normalized design
```

because many inserts/updates occur and data consistency is important.

---

## OLAP

**Online Analytical Processing**

Examples:

```text
Business intelligence
Reporting
Dashboards
Data warehouses
Analytics
```

Often uses:

```text
Denormalized structures
Star schemas
Summary tables
```

because large analytical queries need efficient reads.

---

# 21. Stored Procedures

## Technical Definition

A **stored procedure** is a named, reusable set of SQL statements and procedural logic stored and executed by the database server.

## Easy Meaning

A stored procedure is like a **saved program inside the database**.

Instead of repeatedly writing:

```sql
INSERT ...
UPDATE ...
SELECT ...
```

you can save the logic as a procedure and call it.

---

# 22. Why Use Stored Procedures?

Suppose an application repeatedly needs to create an order.

Instead of sending many SQL statements:

```text
INSERT order
INSERT order item
UPDATE stock
INSERT payment
```

we can create:

```text
create_order()
```

and call it.

---

# 23. Stored Procedure Syntax

Syntax differs between database systems.

For example, in MySQL:

```sql
DELIMITER //

CREATE PROCEDURE GetCustomers()
BEGIN

    SELECT *
    FROM customers;

END //

DELIMITER ;
```

Call it:

```sql
CALL GetCustomers();
```

---

# 24. SQL Server Procedure Example

SQL Server uses different syntax:

```sql
CREATE PROCEDURE GetCustomers
AS
BEGIN

    SELECT *
    FROM customers;

END;
```

Execute:

```sql
EXEC GetCustomers;
```

> Always check the syntax for your specific database system: MySQL, PostgreSQL, SQL Server, Oracle, etc.

---

# 25. Procedure with Parameters

A procedure can accept input values.

MySQL example:

```sql
DELIMITER //

CREATE PROCEDURE GetCustomerOrders(
    IN p_customer_id INT
)
BEGIN

    SELECT *
    FROM orders
    WHERE customer_id = p_customer_id;

END //

DELIMITER ;
```

Call:

```sql
CALL GetCustomerOrders(101);
```

---

# 26. IN Parameter

### Technical Definition

An `IN` parameter supplies input to a procedure.

### Easy Meaning

You **send a value into the procedure**.

```sql
IN p_customer_id INT
```

Example:

```sql
CALL GetCustomerOrders(101);
```

---

# 27. OUT Parameter

### Technical Definition

An `OUT` parameter allows a procedure to return a value through a parameter.

### Easy Meaning

The procedure **puts a value into the output parameter**.

Example in MySQL:

```sql
DELIMITER //

CREATE PROCEDURE CountCustomers(
    OUT customer_count INT
)
BEGIN

    SELECT COUNT(*)
    INTO customer_count
    FROM customers;

END //

DELIMITER ;
```

Usage:

```sql
CALL CountCustomers(@total);
```

Then:

```sql
SELECT @total;
```

---

# 28. INOUT Parameter

### Technical Definition

An `INOUT` parameter can receive an initial value and return a modified value.

### Easy Meaning

It can work as:

```text
Input → Procedure → Modified Output
```

Example concept:

```sql
INOUT p_value INT
```

---

# 29. Procedure with IF

Example:

```sql
DELIMITER //

CREATE PROCEDURE CheckCustomer(
    IN p_customer_id INT
)
BEGIN

    DECLARE customer_count INT;

    SELECT COUNT(*)
    INTO customer_count
    FROM customers
    WHERE customer_id = p_customer_id;

    IF customer_count > 0 THEN
        SELECT 'Customer exists' AS message;
    ELSE
        SELECT 'Customer not found' AS message;
    END IF;

END //

DELIMITER ;
```

---

# 30. Procedure with Transaction

A stored procedure can contain transaction logic where supported.

Example concept:

```sql
DELIMITER //

CREATE PROCEDURE TransferMoney(
    IN p_from INT,
    IN p_to INT,
    IN p_amount DECIMAL(10,2)
)
BEGIN

    START TRANSACTION;

    UPDATE accounts
    SET balance = balance - p_amount
    WHERE account_id = p_from;

    UPDATE accounts
    SET balance = balance + p_amount
    WHERE account_id = p_to;

    COMMIT;

END //

DELIMITER ;
```

In production, proper error handling should also be included.

---

# 31. Error Handling in Procedures

Procedures can often include exception/error handlers.

MySQL example:

```sql
DECLARE EXIT HANDLER FOR SQLEXCEPTION
BEGIN
    ROLLBACK;
END;
```

Conceptually:

```text
START TRANSACTION
       ↓
Perform operations
       ↓
Success?
  /         \
YES         NO
 |           |
COMMIT     ROLLBACK
```

Exact error-handling syntax varies by DBMS.

---

# 32. Stored Procedure Advantages

### 1. Reusability

Write once and execute multiple times.

### 2. Centralized Logic

Business/database logic can be stored in one place.

### 3. Reduced Network Traffic

The application can call one procedure instead of sending many individual statements.

### 4. Security

Permissions can sometimes be granted on procedures without giving direct access to underlying tables.

### 5. Consistency

The same procedure can apply the same logic every time.

### 6. Transaction Control

Procedures can coordinate multiple operations.

---

# 33. Stored Procedure Disadvantages

### 1. Database Dependency

Procedure syntax differs between database systems.

### 2. Maintenance

Large procedures can become difficult to maintain.

### 3. Testing

Testing database procedural logic may require database-specific tooling.

### 4. Deployment Complexity

Application code and database code need coordinated deployments.

### 5. Business Logic Location

Putting too much application logic inside the database can make architecture harder to manage.

---

# 34. SQL Functions

## Technical Definition

A **SQL function** is a reusable database routine that accepts zero or more inputs and returns a value or, depending on the DBMS and function type, a set/table of rows.

## Easy Meaning

A function is like a reusable calculation or operation.

Example:

```text
Input
 ↓
Function
 ↓
Output
```

---

# 35. Built-in SQL Functions

Databases provide many built-in functions.

Examples:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()

UPPER()
LOWER()
LENGTH()

COALESCE()
NULLIF()

CURRENT_DATE
```

Exact function names vary between databases.

---

# 36. Function Categories

Common categories include:

```text
1. String Functions
2. Numeric Functions
3. Date/Time Functions
4. Aggregate Functions
5. Conversion Functions
6. NULL-handling Functions
7. User-Defined Functions
```

---

# 37. String Function Example

```sql
SELECT UPPER('python');
```

Result:

```text
PYTHON
```

---

# 38. Numeric Function Example

```sql
SELECT ROUND(123.456, 2);
```

Result:

```text
123.46
```

---

# 39. Date Function Example

```sql
SELECT CURRENT_DATE;
```

Returns the current date according to the database system.

---

# 40. Aggregate Function Example

```sql
SELECT COUNT(*)
FROM employees;
```

Aggregate functions operate over multiple rows.

Common examples:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

# 41. User-Defined Functions — UDF

## Technical Definition

A **User-Defined Function (UDF)** is a function created by a database developer to encapsulate reusable custom logic.

## Easy Meaning

If the database doesn't provide the function you need, **you create your own**.

Example:

```text
Built-in:
UPPER()

Your own:
calculate_bonus()
```

---

# 42. Scalar UDF

## Technical Definition

A scalar user-defined function returns a single value for each invocation.

## Easy Meaning

Input:

```text
Salary
```

Output:

```text
Bonus
```

---

# 43. Scalar Function Example — MySQL

```sql
DELIMITER //

CREATE FUNCTION calculate_bonus(
    salary DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN

    RETURN salary * 0.10;

END //

DELIMITER ;
```

Use it:

```sql
SELECT calculate_bonus(50000);
```

Result:

```text
5000
```

---

# 44. Function with Table Data

Example:

```sql
DELIMITER //

CREATE FUNCTION get_bonus(
    salary DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN

    RETURN salary * 0.10;

END //

DELIMITER ;
```

Use:

```sql
SELECT
    employee_name,
    salary,
    get_bonus(salary) AS bonus
FROM employees;
```

Result conceptually:

```text
employee | salary | bonus
---------|--------|------
Alice    | 50000  | 5000
Bob      | 60000  | 6000
John     | 70000  | 7000
```

---

# 45. Function Returning a Table

Some database systems support **table-valued functions**.

## Technical Definition

A table-valued function returns a relation/table-like result that can be queried like a table.

## Easy Meaning

Instead of returning:

```text
one number
```

the function returns:

```text
multiple rows and columns
```

Support and syntax vary significantly by database system.

---

# 46. Table-Valued Function Concept

For example:

```text
get_orders(customer_id)
        ↓
+----------------------+
| order_id | total     |
+----------------------+
| 101      | 5000      |
| 102      | 2500      |
+----------------------+
```

This can then be used in queries in systems that support table-valued functions.

---

# 47. Function Parameters

Functions can accept parameters.

Example:

```sql
calculate_tax(price)
```

Here:

```text
price
 ↓
Function
 ↓
tax
```

Example:

```sql
SELECT calculate_tax(1000);
```

---

# 48. Deterministic Function

## Technical Definition

A deterministic function returns the same result when given the same input and relevant database state.

Example:

```text
calculate_bonus(50000)
```

always returns:

```text
5000
```

assuming the function has no changing external state.

---

# 49. Non-Deterministic Function

## Technical Definition

A non-deterministic function can return different results even with the same input or based on changing database/system state.

Examples can include functions involving:

```text
Current date/time
Random values
Changing external/database state
```

For example:

```sql
SELECT CURRENT_TIMESTAMP;
```

The result changes over time.

---

# 50. Function vs Stored Procedure

This is a **very important interview topic**.

| Function                                        | Stored Procedure                                        |
| ----------------------------------------------- | ------------------------------------------------------- |
| Designed to return a value/result               | Can perform a sequence of operations                    |
| Can often be used inside SQL expressions        | Usually invoked as a separate statement                 |
| Useful for reusable calculations                | Useful for workflows/business operations                |
| Often used in `SELECT` expressions              | Often used with `CALL`/`EXEC` depending on DBMS         |
| Can be scalar or table-valued depending on DBMS | Can return values through output parameters/result sets |
| Restrictions vary by DBMS                       | Can often contain transaction/control logic             |
| Usually focuses on computation                  | Often focuses on operations/workflows                   |

---

# 51. Example: Function vs Procedure

## Function

Question:

> "Calculate the bonus for this salary."

```sql
SELECT calculate_bonus(50000);
```

Output:

```text
5000
```

Think:

```text
FUNCTION
Input → Calculation → Return value
```

---

## Procedure

Question:

> "Create an order."

It may need to:

```text
INSERT order
INSERT order items
UPDATE inventory
INSERT payment
COMMIT
```

Think:

```text
PROCEDURE
Input → Multiple operations → Result/actions
```

---

# 52. Function vs Procedure — Easy Memory

```text
FUNCTION
= Calculate / Return

PROCEDURE
= Perform / Process
```

A function is generally more expression-oriented, while a procedure is generally more operation/workflow-oriented.

---

# 53. Stored Procedure vs UDF

| Stored Procedure                                   | UDF                                                    |
| -------------------------------------------------- | ------------------------------------------------------ |
| Performs database operations                       | Returns a value/result                                 |
| Can contain procedural logic                       | Encapsulates reusable computation/query logic          |
| Often called independently                         | Often usable inside SQL expressions, depending on DBMS |
| Can have IN/OUT/INOUT parameters depending on DBMS | Typically accepts inputs and returns a defined result  |
| Can coordinate workflows                           | Usually focused on computation/data retrieval          |
| Often suitable for CRUD/business workflows         | Suitable for reusable calculations                     |

---

# 54. Normalization + Functions

Normalization determines **how data is stored**.

Functions determine **how reusable calculations/logic are performed**.

Example:

```text
NORMALIZED DATABASE

customers
orders
products
order_items
```

Then a function:

```sql
calculate_order_total(order_id)
```

can calculate:

```text
SUM(quantity × price)
```

Conceptually:

```text
Normalized Tables
       ↓
     Query
       ↓
    Function
       ↓
 Calculated Result
```

---

# 55. Normalization + Stored Procedures

A normalized database can use stored procedures for controlled workflows.

Example:

```text
Customer
   ↓
Order
   ↓
Order Items
```

Procedure:

```text
create_order()
```

could:

```text
1. Validate customer
2. Create order
3. Insert order items
4. Update stock
5. Commit transaction
```

---

# 56. When Should You Normalize?

Prefer normalization when:

```text
✓ Data is frequently inserted/updated
✓ Data consistency is critical
✓ Application is transaction-heavy
✓ Many entities have clear relationships
✓ You want to avoid duplicate data
✓ OLTP workload
```

Examples:

```text
Banking
Order processing
Inventory
Employee management
Payment systems
```

---

# 57. When Should You Denormalize?

Consider denormalization when:

```text
✓ Reads greatly outnumber writes
✓ Queries require expensive repeated joins
✓ Reporting performance is important
✓ Dashboard performance matters
✓ Data warehouse/analytics workload
✓ Controlled redundancy is acceptable
```

Examples:

```text
Data warehouses
BI dashboards
Reporting systems
Analytical databases
```

---

# 58. Normalization Decision Flow

```text
Start
  ↓
Identify entities
  ↓
Identify attributes
  ↓
Identify keys
  ↓
Identify functional dependencies
  ↓
1NF
  ↓
Remove partial dependencies
  ↓
2NF
  ↓
Remove transitive dependencies
  ↓
3NF
  ↓
Check stronger requirements
  ↓
BCNF / 4NF / 5NF
```

---

# 59. Practical Database Design

In real-world application development, you usually don't blindly normalize everything to the highest possible normal form.

A common approach is:

```text
Design normalized schema
        ↓
Usually target 3NF
        ↓
Measure actual performance
        ↓
Identify bottlenecks
        ↓
Denormalize selectively if justified
```

Important principle:

> **Don't denormalize just because joins exist. Denormalize when there is a demonstrated performance or architectural reason.**

---

# 60. Important Terms

## Redundancy

Repeated storage of the same fact.

```text
Alice | Python | John
Bob   | Python | John
```

`John` is repeated.

---

## Dependency

A relationship where one attribute determines another.

```text
student_id → student_name
```

---

## Partial Dependency

Dependency on part of a composite key.

```text
student_id → student_name
```

when key is:

```text
(student_id, course_id)
```

---

## Transitive Dependency

Indirect dependency.

```text
A → B
B → C
Therefore A → C
```

---

## Multivalued Dependency

One attribute independently determines multiple values of another attribute.

```text
A →→ B
```

---

## Join Dependency

A relation can be reconstructed from multiple projections/relations through joins.

Important in:

```text
5NF
```

---

# 61. Normal Forms Memory Trick

```text
1NF
↓
Atomic values

2NF
↓
No partial dependency

3NF
↓
No transitive dependency

BCNF
↓
Every determinant is a superkey

4NF
↓
No problematic multivalued dependency

5NF
↓
No problematic join dependency
```

---

# 62. Anomaly Memory Trick

```text
INSERT
→ Can't add data properly

UPDATE
→ Same fact must be changed multiple times

DELETE
→ Deleting one fact accidentally deletes another
```

---

# 63. Procedure Memory Trick

```text
PROCEDURE
    ↓
Saved database program
    ↓
Can accept parameters
    ↓
Can perform multiple operations
    ↓
Can contain control flow
    ↓
Can coordinate transactions
```

---

# 64. Function Memory Trick

```text
FUNCTION
    ↓
Reusable logic
    ↓
Accept input
    ↓
Perform calculation/query logic
    ↓
Return result
```

---

# 65. Most Important Interview Questions

### Q1. What is normalization?

Normalization is the process of organizing relational data to reduce redundancy, eliminate undesirable dependencies, and improve data integrity.

---

### Q2. Why is normalization used?

To:

```text
Reduce redundancy
Prevent anomalies
Improve consistency
Improve integrity
Create logical table structures
```

---

### Q3. What is 1NF?

```text
Atomic values
+
No repeating groups
```

---

### Q4. What is 2NF?

```text
1NF
+
No partial dependency
```

---

### Q5. What is 3NF?

```text
2NF
+
No transitive dependency
```

---

### Q6. What is BCNF?

Every determinant in every non-trivial functional dependency must be a superkey.

---

### Q7. What is 4NF?

4NF addresses problematic non-trivial multivalued dependencies.

---

### Q8. What is 5NF?

5NF addresses problematic join dependencies and ensures decompositions are justified by candidate keys and join dependencies.

---

### Q9. What is denormalization?

Intentionally introducing controlled redundancy to improve read performance or simplify queries for a particular workload.

---

### Q10. Normalization vs denormalization?

```text
Normalization
→ Reduce redundancy
→ More tables
→ More joins

Denormalization
→ Controlled redundancy
→ Potentially fewer joins
→ Potentially faster reads
```

---

### Q11. What is a stored procedure?

A named, reusable database routine containing SQL statements and procedural logic that is stored and executed by the database.

---

### Q12. What is a UDF?

A User-Defined Function is a custom function created by the developer to encapsulate reusable logic and return a defined result.

---

### Q13. Procedure vs Function?

```text
Procedure
→ Performs operations/workflows

Function
→ Returns a value/result
```

---

# 66. Final Concept Map

```text
DATABASE DESIGN
│
├── NORMALIZATION
│   │
│   ├── 1NF
│   │   └── Atomic values
│   │
│   ├── 2NF
│   │   └── No partial dependency
│   │
│   ├── 3NF
│   │   └── No transitive dependency
│   │
│   ├── BCNF
│   │   └── Determinants are superkeys
│   │
│   ├── 4NF
│   │   └── No problematic MVDs
│   │
│   └── 5NF
│       └── No problematic join dependencies
│
├── DENORMALIZATION
│   │
│   ├── Controlled redundancy
│   ├── Fewer joins
│   ├── Faster reads
│   └── Useful for analytics/reporting
│
└── DATABASE PROGRAMMING
    │
    ├── STORED PROCEDURES
    │   ├── IN
    │   ├── OUT
    │   ├── INOUT
    │   ├── Conditions
    │   ├── Loops
    │   ├── Error Handling
    │   └── Transactions
    │
    └── FUNCTIONS
        ├── Built-in Functions
        ├── Scalar Functions
        ├── Table-Valued Functions
        ├── User-Defined Functions
        ├── Deterministic
        └── Non-Deterministic
```

---

# 67. One-Line Revision

```text
Normalization
→ Organize data to reduce redundancy and improve integrity.

1NF
→ One cell, one atomic value.

2NF
→ 1NF + no partial dependency.

3NF
→ 2NF + no transitive dependency.

BCNF
→ Every determinant must be a superkey.

4NF
→ Remove problematic multivalued dependencies.

5NF
→ Remove problematic join dependencies.

Denormalization
→ Intentionally add controlled redundancy for performance/simplicity.

Insert Anomaly
→ Cannot insert one fact without unrelated data.

Update Anomaly
→ Same fact must be updated in multiple places.

Delete Anomaly
→ Deleting one fact accidentally removes another fact.

Functional Dependency
→ A determines B.

Partial Dependency
→ Attribute depends on part of a composite key.

Transitive Dependency
→ A determines B through another attribute.

Stored Procedure
→ Saved database program for performing operations.

IN
→ Input parameter.

OUT
→ Output parameter.

INOUT
→ Input + output parameter.

SQL Function
→ Reusable logic that returns a result.

UDF
→ Custom function created by the developer.

Scalar Function
→ Returns one value.

Table-Valued Function
→ Returns rows/table-like result.

Deterministic Function
→ Same input → same result under the same relevant state.

Non-Deterministic Function
→ Result can change for the same input.
```

---

# ⭐ Final Mental Model

```text
NORMALIZATION
"What is the best way to STORE the data?"

DENORMALIZATION
"Should I intentionally duplicate some data
to make READS faster?"

STORED PROCEDURE
"What sequence of database OPERATIONS
should be executed together?"

FUNCTION
"What reusable CALCULATION/LOGIC
should return a result?"
```

---

# Quick Revision Formula

```text
NORMALIZATION

1NF → Atomic
2NF → No Partial Dependency
3NF → No Transitive Dependency
BCNF → Determinant = Superkey
4NF → No problematic MVD
5NF → No problematic JD
```

```text
DENORMALIZATION

More Redundancy
      ↓
Fewer Joins
      ↓
Potentially Faster Reads
      ↓
But More Update Complexity
```

```text
PROCEDURE

Input
  ↓
Multiple SQL Operations
  ↓
Business/Database Workflow
  ↓
Output / Changes
```

```text
FUNCTION

Input
  ↓
Calculation / Logic
  ↓
Return Value
```
