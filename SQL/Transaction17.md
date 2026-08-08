# SQL Transactions, Isolation, Database Relationships & Referential Actions

> **Revision format:** Every concept is explained with a **technical definition**, **easy meaning**, and **example**.

---

# 1. Transactions

## 1.1 What is a Transaction?

### Technical Definition

A **transaction** is a logical unit of database operations that is executed as a single unit of work.

### Easy Meaning

A transaction is a **group of SQL operations that should be treated as one complete task**.

Either:

* All operations succeed → `COMMIT`
* Something goes wrong → `ROLLBACK`

### Example

Suppose ₹1,000 is transferred from Account A to Account B.

Two operations are required:

```sql
UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;
```

```sql
UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;
```

Both should happen together.

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

If something fails:

```sql
ROLLBACK;
```

### Easy Memory

```text
Transaction = Complete one task safely
```

---

# 2. Why Do We Need Transactions?

### Technical Definition

Transactions maintain database correctness when multiple operations must be executed together.

### Easy Meaning

Imagine transferring money.

If:

```text
A loses ₹1000
```

but:

```text
B doesn't receive ₹1000
```

the database becomes wrong.

A transaction prevents this type of partial update.

### Real-World Examples

Transactions are used in:

* Banking
* Online shopping
* Ticket booking
* Payments
* Inventory
* Payroll
* Order processing

---

# 3. ACID Properties

Transactions follow four important properties called **ACID**.

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

---

# 4. Atomicity

### Technical Definition

**Atomicity** guarantees that a transaction is treated as an indivisible unit: either all of its operations are successfully applied, or its changes are rolled back.

### Easy Meaning

**All or nothing.**

Example:

```text
Transfer ₹1000

A → -₹1000
B → +₹1000
```

Both must happen.

If B cannot receive the money:

```text
A's ₹1000 deduction → cancelled
```

### Memory

```text
Atomicity = All or Nothing
```

---

# 5. Consistency

### Technical Definition

**Consistency** ensures that a successful transaction preserves the database's defined integrity constraints and rules, moving the database from one valid state to another valid state.

### Easy Meaning

After a transaction finishes, the database should still follow its rules.

For example:

```text
salary > 0
```

If the database has this rule, a transaction should not leave a salary as an invalid value.

### Memory

```text
Consistency = Database rules remain valid
```

---

# 6. Isolation

### Technical Definition

**Isolation** controls the visibility and interaction of concurrent transactions so that their intermediate operations do not produce unacceptable interference.

### Easy Meaning

When two people use the database at the same time, one person's unfinished work should not incorrectly affect the other person.

Example:

```text
Transaction A → updating account
Transaction B → reading account
```

Isolation controls what B is allowed to see from A.

### Memory

```text
Isolation = Keep concurrent transactions properly separated
```

---

# 7. Durability

### Technical Definition

**Durability** guarantees that once a transaction is successfully committed, its changes are preserved despite subsequent failures, according to the database system's durability mechanisms.

### Easy Meaning

Once you successfully save/commit the data, it should not disappear just because the server crashes afterward.

```sql
COMMIT;
```

### Memory

```text
Durability = Committed data stays saved
```

---

# 8. ACID Quick Revision

| Property    | Technical Idea                         | Easy Meaning                             |
| ----------- | -------------------------------------- | ---------------------------------------- |
| Atomicity   | Transaction is indivisible             | All or nothing                           |
| Consistency | Integrity rules preserved              | Database remains valid                   |
| Isolation   | Concurrent transactions are controlled | Transactions don't interfere incorrectly |
| Durability  | Committed changes are preserved        | Saved means saved                        |

---

# 9. COMMIT

### Technical Definition

`COMMIT` permanently commits the changes made by the current transaction.

### Easy Meaning

**Save the transaction.**

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

COMMIT;
```

After successful commit, the transaction is completed.

### Memory

```text
COMMIT = Save changes
```

---

# 10. ROLLBACK

### Technical Definition

`ROLLBACK` undoes changes made during the current transaction that have not been committed.

### Easy Meaning

**Cancel the transaction's uncommitted changes.**

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

ROLLBACK;
```

The update is undone.

### Memory

```text
ROLLBACK = Undo changes
```

---

# 11. SAVEPOINT

### Technical Definition

A **SAVEPOINT** establishes a named point within a transaction to which the transaction can later roll back.

### Easy Meaning

It is like creating a **checkpoint** inside a transaction.

```sql
BEGIN;

INSERT INTO orders
VALUES (101, 1);

SAVEPOINT order_checkpoint;

INSERT INTO orders
VALUES (102, 2);

ROLLBACK TO SAVEPOINT order_checkpoint;

COMMIT;
```

The operation after the savepoint can be undone without necessarily cancelling the entire transaction.

### Memory

```text
SAVEPOINT = Checkpoint
```

---

# 12. Transaction Commands

Common transaction-control commands include:

```text
BEGIN / START TRANSACTION
COMMIT
ROLLBACK
SAVEPOINT
ROLLBACK TO SAVEPOINT
```

Exact syntax and behavior can vary between database systems.

---

# 13. Transaction States

A transaction can conceptually have these states:

```text
Active
  ↓
Partially Committed
  ↓
Committed
```

Or:

```text
Active
  ↓
Failed
  ↓
Aborted
```

---

## Active

### Technical Definition

The transaction is currently executing.

### Easy Meaning

The transaction is still running.

---

## Committed

### Technical Definition

The transaction has completed successfully and its changes have been committed.

### Easy Meaning

The transaction succeeded.

---

## Failed

### Technical Definition

The transaction cannot continue because of an error or failure.

### Easy Meaning

Something went wrong.

---

## Aborted

### Technical Definition

The transaction has been rolled back and its uncommitted changes have been undone.

### Easy Meaning

The transaction was cancelled.

---

# 14. Transaction Isolation

## What is Concurrency?

### Technical Definition

**Concurrency** is the execution or overlapping progress of multiple transactions during the same period.

### Easy Meaning

Multiple users are using the database at the same time.

Example:

```text
User A → Updating employee salary

User B → Reading employee salary

User C → Inserting a new employee
```

All may happen concurrently.

---

# 15. Why Is Isolation Needed?

Without proper isolation, concurrent transactions can create problems.

Important problems include:

```text
1. Dirty Read
2. Non-Repeatable Read
3. Phantom Read
4. Lost Update
```

---

# 16. Dirty Read

### Technical Definition

A **dirty read** occurs when a transaction reads data written by another transaction before that other transaction commits.

### Easy Meaning

You read **someone else's temporary/unconfirmed change**.

Example:

Transaction A:

```sql
BEGIN;

UPDATE accounts
SET balance = 5000
WHERE account_id = 1;
```

A has not committed.

Transaction B:

```sql
SELECT balance
FROM accounts
WHERE account_id = 1;
```

If B sees `5000` and A later does:

```sql
ROLLBACK;
```

B read data that was never committed.

### Memory

```text
Dirty Read = Read uncommitted data
```

---

# 17. Non-Repeatable Read

### Technical Definition

A **non-repeatable read** occurs when a transaction reads the same row more than once and gets different values because another transaction committed a change between the reads.

### Easy Meaning

You read the same row twice, but the value changed between the two reads.

First:

```text
salary = 50,000
```

Another transaction updates it:

```text
salary = 60,000
```

Second read:

```text
salary = 60,000
```

### Memory

```text
Non-Repeatable Read = Same row → Different value
```

---

# 18. Phantom Read

### Technical Definition

A **phantom read** occurs when repeating a query over a range returns a different set of rows because another transaction inserted, deleted, or changed rows that satisfy the query condition.

### Easy Meaning

You run the same query twice, but **new matching rows appear or disappear**.

First query:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Result:

```text
5 rows
```

Another transaction inserts an employee with salary `70000`.

Second query:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Result:

```text
6 rows
```

The new row is a **phantom**.

### Memory

```text
Phantom Read = Same query → Different set of rows
```

---

# 19. Lost Update

### Technical Definition

A **lost update** occurs when one transaction's update is overwritten by another concurrent transaction's update based on stale data.

### Easy Meaning

Two people update the same data, and **one person's change gets overwritten**.

Example:

```text
Original balance = 1000
```

A reads:

```text
1000
```

B reads:

```text
1000
```

A calculates:

```text
1000 + 500 = 1500
```

B calculates:

```text
1000 - 200 = 800
```

If A writes `1500` and B later writes `800`:

```text
A's update is lost.
```

### Memory

```text
Lost Update = One update overwrites another
```

---

# 20. Isolation Levels

The standard SQL isolation levels are:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Think of them as different levels of protection from concurrency problems.

---

# 21. READ UNCOMMITTED

### Technical Definition

Allows a transaction to read data that may have been modified by another transaction but not yet committed.

### Easy Meaning

**Very weak isolation.**

You may see uncommitted data.

Possible problems include:

```text
Dirty Read
Non-Repeatable Read
Phantom Read
```

### Memory

```text
READ UNCOMMITTED
        ↓
Weakest standard isolation
```

---

# 22. READ COMMITTED

### Technical Definition

A transaction generally sees only data committed before each statement/read according to the DBMS's implementation.

### Easy Meaning

You don't normally see another transaction's uncommitted changes.

Prevents:

```text
Dirty Reads
```

But can allow:

```text
Non-Repeatable Reads
Phantom Reads
```

### Memory

```text
READ COMMITTED
→ Read only committed data
```

---

# 23. REPEATABLE READ

### Technical Definition

An isolation level that provides a stronger guarantee that rows read by a transaction remain consistent for repeated reads, subject to the DBMS's implementation.

### Easy Meaning

If you read a row once, repeated reads of that row should remain consistent within the transaction.

Generally prevents:

```text
Dirty Reads
Non-Repeatable Reads
```

Phantom behavior is DBMS-dependent.

### Memory

```text
REPEATABLE READ
→ Same row can be read consistently
```

---

# 24. SERIALIZABLE

### Technical Definition

The strongest standard SQL isolation level, designed to make concurrent execution produce results equivalent to some serial execution order.

### Easy Meaning

It behaves as if transactions are handled **one after another in a safe order**.

It gives the strongest standard isolation but may reduce concurrency.

### Memory

```text
SERIALIZABLE
→ Strongest standard isolation
```

---

# 25. Isolation Level Comparison

| Isolation Level  | Dirty Read | Non-Repeatable Read | Phantom Read   |
| ---------------- | ---------- | ------------------- | -------------- |
| READ UNCOMMITTED | Possible   | Possible            | Possible       |
| READ COMMITTED   | Prevented  | Possible            | Possible       |
| REPEATABLE READ  | Prevented  | Prevented           | DBMS-dependent |
| SERIALIZABLE     | Prevented  | Prevented           | Prevented      |

> Actual behavior can vary by DBMS because databases use different locking and MVCC implementations.

---

# 26. MVCC

### Technical Definition

**MVCC (Multi-Version Concurrency Control)** is a concurrency-control technique that maintains multiple versions of data so transactions can read an appropriate version without necessarily blocking writers.

### Easy Meaning

Instead of everyone fighting over one copy of a row, the database can keep **different versions** of the row.

Conceptually:

```text
Employee salary

Version 1 → ₹50,000
Version 2 → ₹55,000
Version 3 → ₹60,000
```

A transaction reads the version appropriate to its snapshot/isolation rules.

### Benefits

* Better read concurrency
* Less reader/writer blocking
* Consistent snapshots

Implementation differs between database systems.

---

# 27. Database Relationships

## What is a Relationship?

### Technical Definition

A **database relationship** defines how rows in one table are logically associated with rows in another table.

### Easy Meaning

It tells us **how tables are connected**.

Example:

```text
Customers
    ↓
Orders
```

One customer can have multiple orders.

---

# 28. Primary Key

### Technical Definition

A **primary key** is a column or set of columns that uniquely identifies each row in a table.

### Easy Meaning

It is the table's **unique ID** for each record.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);
```

Example:

```text
customer_id | customer_name
------------|--------------
1           | Alice
2           | Bob
3           | John
```

Each `customer_id` identifies one customer.

### Memory

```text
Primary Key = Unique identity of a row
```

---

# 29. Foreign Key

### Technical Definition

A **foreign key** is a column or set of columns in one table that references a candidate/primary key in another table.

### Easy Meaning

It is the **link between two tables**.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

Here:

```text
customers.customer_id
        ↑
        |
orders.customer_id
```

### Memory

```text
Foreign Key = Connection between tables
```

---

# 30. Parent Table

### Technical Definition

A **parent table** is the referenced table in a foreign-key relationship.

### Easy Meaning

It contains the record that another table depends on.

```text
customers
   ↓
orders
```

`customers` is the parent.

---

# 31. Child Table

### Technical Definition

A **child table** is the table containing the foreign key that references the parent table.

### Easy Meaning

It contains the link to the parent.

```text
customers
    ↑
    |
orders
```

`orders` is the child.

---

# 32. One-to-One Relationship

### Technical Definition

A **one-to-one (1:1)** relationship means each row in one table is associated with at most one row in another table, and vice versa.

### Easy Meaning

**One person → One passport**

```text
Person
  |
  | 1 : 1
  |
Passport
```

Example:

```sql
CREATE TABLE persons (
    person_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

```sql
CREATE TABLE passports (
    passport_id INT PRIMARY KEY,
    person_id INT UNIQUE,

    FOREIGN KEY (person_id)
        REFERENCES persons(person_id)
);
```

`UNIQUE` helps enforce at most one passport row per person.

---

# 33. One-to-Many Relationship

### Technical Definition

A **one-to-many (1:N)** relationship means one row in a parent table can be associated with multiple rows in a child table.

### Easy Meaning

**One customer can have many orders.**

```text
Customer
   |
   +---- Order
   |
   +---- Order
   |
   +---- Order
```

Example:

```text
Customer 1
    ↓
Order 101
Order 102
Order 103
```

This is the most common relationship in relational databases.

---

# 34. Many-to-Many Relationship

### Technical Definition

A **many-to-many (M:N)** relationship means multiple rows in one table can be associated with multiple rows in another table.

### Easy Meaning

**Many students can take many courses.**

```text
Student ↔ Course
```

One student:

```text
Student A
   ↓
Math
Python
SQL
```

One course:

```text
Python
   ↓
Student A
Student B
Student C
```

---

# 35. Junction Table

### Technical Definition

A **junction table**, also called an associative table, is an intermediate table used to implement a many-to-many relationship.

### Easy Meaning

Because SQL tables don't directly store many-to-many relationships, we create a **middle table**.

```text
students
    ↓
student_courses
    ↑
courses
```

Example:

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(student_id),

    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);
```

---

# 36. Self-Referencing Relationship

### Technical Definition

A **self-referencing relationship** occurs when a table's foreign key references a key in the same table.

### Easy Meaning

A table is connected to **itself**.

Example:

```text
Employee
   ↓
Manager
```

Both are employees.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    manager_id INT,

    FOREIGN KEY (manager_id)
        REFERENCES employees(employee_id)
);
```

Example:

```text
CEO
├── Alice
│   └── John
└── Bob
```

---

# 37. Optional Relationship

### Technical Definition

An optional relationship is one where a record is not required to have a related record.

### Easy Meaning

The relationship is **not compulsory**.

Example:

```text
CEO → no manager
```

Therefore:

```text
manager_id = NULL
```

---

# 38. Mandatory Relationship

### Technical Definition

A mandatory relationship requires a related record to exist.

### Easy Meaning

The relationship is **required**.

Example:

Every order must belong to a customer.

```sql
customer_id INT NOT NULL
```

Now an order cannot have:

```text
customer_id = NULL
```

---

# 39. Relationship Summary

| Relationship   | Easy Meaning   | Example            |
| -------------- | -------------- | ------------------ |
| 1:1            | One ↔ One      | Person ↔ Passport  |
| 1:N            | One ↔ Many     | Customer ↔ Orders  |
| M:N            | Many ↔ Many    | Students ↔ Courses |
| Self-reference | Table ↔ Itself | Employee ↔ Manager |

---

# 40. Referential Integrity

### Technical Definition

**Referential integrity** is a database integrity rule that ensures foreign-key values correctly reference existing rows in the related parent table, subject to the configured constraints/actions.

### Easy Meaning

It makes sure that **table connections don't point to something that doesn't exist**.

Suppose:

```text
customers

customer_id
-----------
1
2
3
```

Then this is valid:

```text
orders

order_id | customer_id
---------|------------
101      | 1
```

But this is invalid if customer `999` doesn't exist:

```text
order_id | customer_id
---------|------------
102      | 999
```

---

# 41. Orphan Record

### Technical Definition

An **orphan record** is a child record whose referenced parent record does not exist.

### Easy Meaning

A child record is pointing to a parent that is **missing**.

Example:

```text
Order 101
customer_id = 999
```

But:

```text
Customer 999 doesn't exist
```

This is an orphan relationship.

Foreign keys help prevent this.

---

# 42. Referential Actions

### Technical Definition

**Referential actions** specify what the database should do to related child rows when a referenced parent row is updated or deleted.

### Easy Meaning

They answer:

> "What should happen to the child when the parent changes?"

Common actions:

```text
CASCADE
SET NULL
SET DEFAULT
RESTRICT
NO ACTION
```

---

# 43. ON DELETE CASCADE

### Technical Definition

`ON DELETE CASCADE` automatically deletes matching child rows when the referenced parent row is deleted.

### Easy Meaning

**Delete parent → automatically delete children.**

Example:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
        ON DELETE CASCADE
);
```

If:

```text
Customer 1
   ↓
Order 101
Order 102
```

and customer 1 is deleted:

```text
Customer 1 → Deleted
Order 101  → Deleted
Order 102  → Deleted
```

### Memory

```text
CASCADE = Parent deletion travels to children
```

---

# 44. ON DELETE SET NULL

### Technical Definition

`ON DELETE SET NULL` sets the foreign-key values of matching child rows to `NULL` when the referenced parent is deleted.

### Easy Meaning

**Delete parent → keep children → remove their parent connection.**

Example:

```text
Manager
employee_id = 1
     ↓
Alice
manager_id = 1
```

Delete manager 1:

```text
Alice
manager_id = NULL
```

Example:

```sql
FOREIGN KEY (manager_id)
REFERENCES employees(employee_id)
ON DELETE SET NULL
```

The foreign-key column must permit `NULL`.

### Memory

```text
SET NULL = Keep child, remove connection
```

---

# 45. ON DELETE SET DEFAULT

### Technical Definition

`ON DELETE SET DEFAULT` sets the child foreign-key value to its column default when the referenced parent is deleted, where supported and valid.

### Easy Meaning

**Delete parent → replace the parent ID with a default value.**

Example:

```text
Department 0 = Unknown
```

If department 10 is deleted:

```text
employee.department_id
10 → 0
```

Support and exact behavior vary by DBMS.

### Memory

```text
SET DEFAULT = Replace with default
```

---

# 46. ON DELETE RESTRICT

### Technical Definition

`RESTRICT` prevents deletion of a referenced parent row when matching child rows exist.

### Easy Meaning

**If children exist, don't allow parent deletion.**

Example:

```text
Customer 1
   ↓
Order 101
```

Try:

```sql
DELETE FROM customers
WHERE customer_id = 1;
```

Database blocks the deletion.

### Memory

```text
RESTRICT = Stop deletion
```

---

# 47. ON DELETE NO ACTION

### Technical Definition

`NO ACTION` does not automatically modify related child rows and prevents the operation from leaving a referential-integrity violation, according to the DBMS's constraint-checking rules.

### Easy Meaning

**Don't automatically change the children; make sure the relationship remains valid.**

In many databases it behaves similarly to `RESTRICT`, but timing can differ when deferred constraint checking is supported.

---

# 48. ON UPDATE CASCADE

### Technical Definition

`ON UPDATE CASCADE` automatically updates matching foreign-key values when the referenced key value changes.

### Easy Meaning

**Parent ID changes → child ID changes automatically.**

Example:

```text
Parent ID:
10 → 20
```

Child:

```text
customer_id:
10 → 20
```

Example:

```sql
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id)
ON UPDATE CASCADE
```

Primary keys are usually stable, so changing them is uncommon.

---

# 49. Referential Action Comparison

| Action            | Easy Meaning                                              |
| ----------------- | --------------------------------------------------------- |
| CASCADE           | Parent deleted → children deleted                         |
| SET NULL          | Parent deleted → child FK becomes NULL                    |
| SET DEFAULT       | Parent deleted → child FK becomes default                 |
| RESTRICT          | Parent cannot be deleted if children exist                |
| NO ACTION         | Don't automatically change children; enforce relationship |
| ON UPDATE CASCADE | Parent key changes → child FK changes                     |

---

# 50. Complete Example

Consider an online shopping system.

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
    |
    | N:1
    ↓
PRODUCTS
```

---

## Customers

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL
);
```

---

## Products

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);
```

---

## Orders

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE NOT NULL,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
        ON DELETE RESTRICT
);
```

---

## Order Items

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,

    PRIMARY KEY (order_id, product_id),

    FOREIGN KEY (order_id)
        REFERENCES orders(order_id)
        ON DELETE CASCADE,

    FOREIGN KEY (product_id)
        REFERENCES products(product_id)
        ON DELETE RESTRICT
);
```

---

# 51. Why Different Referential Actions?

Consider:

```text
Customer
   ↓
Order
```

We might use:

```text
ON DELETE RESTRICT
```

because deleting a customer with historical orders may be undesirable.

But:

```text
Order
   ↓
Order Items
```

We might use:

```text
ON DELETE CASCADE
```

because an order item usually has no meaning without its order.

Therefore:

```text
Customer → Order
       RESTRICT

Order → Order Items
       CASCADE
```

---

# 52. Transactions + Relationships

Transactions and relationships often work together.

Suppose a customer places an order.

We may need to:

```text
1. Create order
2. Create order items
3. Reduce product stock
4. Record payment
```

These operations should often be treated as one business transaction.

```sql
BEGIN;

INSERT INTO orders (...);

INSERT INTO order_items (...);

UPDATE products
SET stock = stock - 1
WHERE product_id = 101;

INSERT INTO payments (...);

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

### Easy Meaning

Either the complete order process succeeds, or we undo the incomplete work.

---

# 53. Transaction vs Relationship

This is very important.

## Transaction

### Technical

A transaction is a logical unit of database work.

### Easy

**A group of operations treated as one task.**

```text
Transaction
    ↓
INSERT
UPDATE
INSERT
    ↓
COMMIT
```

---

## Relationship

### Technical

A relationship describes the association between records in tables.

### Easy

**How tables are connected.**

```text
Customer
    ↓
Order
```

### Memory

```text
Transaction = Group of work

Relationship = Connection between data
```

---

# 54. Foreign Key vs Referential Action

## Foreign Key

### Technical

Defines/enforces a relationship between a child table and a referenced parent key.

```sql
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id)
```

### Easy

**Creates the connection.**

---

## Referential Action

### Technical

Defines how related rows are handled when the referenced key is updated or deleted.

```sql
ON DELETE CASCADE
```

### Easy

**Defines what happens to the connection when the parent changes.**

---

# 55. Primary Key vs Foreign Key

| Primary Key              | Foreign Key                             |
| ------------------------ | --------------------------------------- |
| Identifies a row         | Connects to another table               |
| Usually unique           | May contain repeated values             |
| Belongs to its own table | References another table's key          |
| Cannot normally be NULL  | Can be NULL if relationship is optional |
| Example: `customer_id`   | Example: `customer_id` in `orders`      |

Example:

```text
customers
----------------
customer_id PK
     ↑
     |
orders
----------------
customer_id FK
```

---

# 56. CASCADE vs RESTRICT

This is a very common interview question.

## CASCADE

```text
Delete parent
      ↓
Delete children
```

Use when child data should not exist without the parent.

---

## RESTRICT

```text
Delete parent
      ↓
Children exist?
      ↓
YES
      ↓
BLOCK
```

Use when child/history data should prevent deletion of the parent.

---

# 57. NULL and Foreign Keys

A foreign key can generally contain `NULL` unless it is declared `NOT NULL`.

Example:

```sql
manager_id INT
```

allows:

```text
manager_id = NULL
```

Meaning:

```text
No manager assigned
```

But:

```sql
manager_id INT NOT NULL
```

means:

```text
Every employee must have a manager
```

subject to the table's business rules.

---

# 58. Soft Delete

### Technical Definition

A **soft delete** marks a record as inactive/deleted instead of physically removing it.

### Easy Meaning

Instead of actually deleting:

```sql
DELETE FROM products
WHERE product_id = 101;
```

we can do:

```sql
UPDATE products
SET is_active = FALSE
WHERE product_id = 101;
```

The record remains in the database.

### Why?

Useful when we need:

* History
* Auditing
* Analytics
* Recovery
* Historical references

---

# 59. Complete Concept Map

```text
DATABASE
│
├── TRANSACTION
│   │
│   ├── COMMIT
│   ├── ROLLBACK
│   ├── SAVEPOINT
│   │
│   └── ACID
│       ├── Atomicity
│       ├── Consistency
│       ├── Isolation
│       └── Durability
│
├── CONCURRENCY
│   │
│   ├── Dirty Read
│   ├── Non-Repeatable Read
│   ├── Phantom Read
│   └── Lost Update
│
├── ISOLATION LEVELS
│   │
│   ├── Read Uncommitted
│   ├── Read Committed
│   ├── Repeatable Read
│   └── Serializable
│
├── RELATIONSHIPS
│   │
│   ├── 1:1
│   ├── 1:N
│   ├── M:N
│   └── Self-Referencing
│
└── REFERENTIAL INTEGRITY
    │
    ├── Primary Key
    ├── Foreign Key
    │
    └── Referential Actions
        ├── CASCADE
        ├── SET NULL
        ├── SET DEFAULT
        ├── RESTRICT
        └── NO ACTION
```

---

# 60. One-Line Revision

```text
Transaction
→ Group of database operations treated as one unit.

Atomicity
→ All or nothing.

Consistency
→ Database rules remain valid.

Isolation
→ Controls interaction between concurrent transactions.

Durability
→ Committed changes remain preserved.

COMMIT
→ Save transaction changes.

ROLLBACK
→ Undo uncommitted changes.

SAVEPOINT
→ Create a rollback checkpoint.

Dirty Read
→ Read uncommitted data.

Non-Repeatable Read
→ Same row gives different values.

Phantom Read
→ Same query gives a different set of rows.

Lost Update
→ One update overwrites another.

Primary Key
→ Uniquely identifies a row.

Foreign Key
→ Connects one table to another.

1:1
→ One record ↔ one record.

1:N
→ One record ↔ many records.

M:N
→ Many records ↔ many records.

Referential Integrity
→ Keeps table relationships valid.

CASCADE
→ Automatically affect related rows.

SET NULL
→ Set child FK to NULL.

SET DEFAULT
→ Set child FK to default.

RESTRICT
→ Block parent operation if dependent rows exist.

NO ACTION
→ Enforce referential integrity without automatically modifying children.
```

---

# ⭐ Most Important Mental Model

```text
                 DATABASE
                    |
        +-----------+-----------+
        |                       |
   TRANSACTIONS             RELATIONSHIPS
        |                       |
      ACID                Primary Key
        |                       |
   +----+----+                  |
   |         |                  ↓
Isolation  Durability       Foreign Key
   |                            |
   ↓                            ↓
Concurrency              Referential Integrity
Problems                       |
   |                      Referential Actions
   |                            |
   +----+----+              +---+---+
        |                    |   |   |
      Dirty              CASCADE NULL
      Read               RESTRICT
      Phantom
      Non-repeatable
      Lost Update
```

### Final Memory Trick

```text
TRANSACTION
= "What work should happen together?"

ACID
= "How safely should that work happen?"

ISOLATION
= "How should simultaneous work interact?"

RELATIONSHIP
= "How are tables connected?"

FOREIGN KEY
= "What connects the tables?"

REFERENTIAL ACTION
= "What happens to connected rows when the parent changes?"
```
