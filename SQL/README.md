# SQL — Complete Learning & Revision Index

## 01. SQL Fundamentals

* What is SQL?
* Why SQL?
* SQL Standards
* SQL vs MySQL
* SQL vs PostgreSQL
* SQL vs NoSQL
* DBMS
* RDBMS
* Database
* Schema
* Tables
* Rows
* Columns
* Records
* Attributes
* Relationships
* Relational Model
* SQL Syntax
* SQL Comments
* SQL Statements
* SQL Clauses
* SQL Keywords
* SQL Identifiers

---

# 02. Database Fundamentals

* Database Concepts
* DBMS Architecture
* RDBMS Architecture
* Relational Database
* Database Schema
* Database Instance
* Tables
* Views
* Relationships
* Referential Integrity
* Data Integrity
* Entity
* Attribute
* Cardinality
* Degree
* Database Metadata
* ER Model
* ER Diagram
* Entity
* Attribute
* Relationship
* Primary Key
* Foreign Key

---

# 03. SQL Data Types

### Numeric

* INT
* BIGINT
* SMALLINT
* TINYINT
* DECIMAL
* NUMERIC
* FLOAT
* REAL
* DOUBLE

### Character

* CHAR
* VARCHAR
* TEXT
* NCHAR
* NVARCHAR

### Date & Time

* DATE
* TIME
* DATETIME
* TIMESTAMP
* INTERVAL

### Other

* BOOLEAN
* BINARY
* VARBINARY
* JSON
* ARRAY
* UUID

> Data types vary between MySQL, PostgreSQL, SQL Server, Oracle, etc.

---

# 04. SQL Keys

* Super Key
* Candidate Key
* Primary Key
* Alternate Key
* Foreign Key
* Composite Key
* Natural Key
* Surrogate Key
* Unique Key

### Key Relationships

* Primary Key vs Foreign Key
* Primary Key vs Unique Key
* Natural Key vs Surrogate Key
* Single-column Key
* Composite Key

---

# 05. SQL Constraints

* PRIMARY KEY
* FOREIGN KEY
* NOT NULL
* UNIQUE
* CHECK
* DEFAULT
* Referential Integrity
* Constraint Naming
* Adding Constraints
* Removing Constraints
* Modifying Constraints

---

# 06. SQL Command Categories

### DDL — Data Definition Language

* CREATE
* ALTER
* DROP
* TRUNCATE
* RENAME

### DML — Data Manipulation Language

* INSERT
* UPDATE
* DELETE
* MERGE

### DQL — Data Query Language

* SELECT

### DCL — Data Control Language

* GRANT
* REVOKE

### TCL — Transaction Control Language

* COMMIT
* ROLLBACK
* SAVEPOINT

---

# 07. Database & Table Creation

* CREATE DATABASE
* CREATE SCHEMA
* CREATE TABLE
* CREATE TABLE AS SELECT
* CREATE TABLE LIKE
* Temporary Tables
* Table Comments
* Table Properties

---

# 08. ALTER TABLE

* Add Column
* Drop Column
* Rename Column
* Modify Column
* Change Data Type
* Add Constraint
* Drop Constraint
* Rename Table

---

# 09. INSERT

* INSERT Single Row
* INSERT Multiple Rows
* INSERT Specific Columns
* INSERT from SELECT
* INSERT with Defaults
* INSERT with NULL
* INSERT IGNORE / Conflict Handling
* UPSERT
* MERGE

---

# 10. SELECT

* SELECT *
* Selecting Specific Columns
* Column Expressions
* Calculated Columns
* Column Aliases
* Table Aliases
* DISTINCT
* SELECT with Expressions
* SELECT with Functions

---

# 11. Filtering Data

* WHERE
* Comparison Operators
* Logical Operators
* AND
* OR
* NOT
* IN
* NOT IN
* BETWEEN
* NOT BETWEEN
* LIKE
* NOT LIKE
* IS NULL
* IS NOT NULL
* EXISTS
* NOT EXISTS

---

# 12. SQL Operators

### Arithmetic

* *
* *
* *
* /
* %

### Comparison

* =
* !=
* <>
* >
* <
* > =
* <=

### Logical

* AND
* OR
* NOT

### Other

* IN
* BETWEEN
* LIKE
* IS NULL
* EXISTS
* ANY
* ALL

### Operator Precedence

* Parentheses
* NOT
* AND
* OR

---

# 13. Sorting & Limiting

* ORDER BY
* ASC
* DESC
* Multiple Column Sorting
* Sorting by Expressions
* Sorting by Alias
* LIMIT
* OFFSET
* TOP
* FETCH
* Pagination

---

# 14. SQL Functions

## String Functions

* UPPER
* LOWER
* LENGTH
* TRIM
* LTRIM
* RTRIM
* CONCAT
* SUBSTRING
* LEFT
* RIGHT
* REPLACE
* POSITION
* CHARINDEX
* SPLIT Functions

## Numeric Functions

* ROUND
* CEIL
* FLOOR
* ABS
* POWER
* SQRT
* MOD
* SIGN
* RANDOM

## Date Functions

* CURRENT_DATE
* CURRENT_TIME
* CURRENT_TIMESTAMP
* DATE_PART
* EXTRACT
* DATE_ADD
* DATE_SUB
* DATE_DIFF
* DATE_TRUNC
* YEAR
* MONTH
* DAY

## NULL Functions

* COALESCE
* NULLIF
* IFNULL
* ISNULL

---

# 15. Aggregate Functions

* COUNT
* COUNT(*)
* COUNT(column)
* COUNT(DISTINCT)
* SUM
* AVG
* MIN
* MAX
* STDDEV
* VARIANCE
* GROUP_CONCAT / STRING_AGG

---

# 16. GROUP BY

* Basic GROUP BY
* Multiple Columns
* GROUP BY with Aggregate Functions
* GROUP BY Expressions
* GROUP BY with CASE
* GROUP BY with JOIN
* GROUP BY with NULL
* GROUP BY ROLLUP
* GROUP BY CUBE
* GROUPING SETS

---

# 17. HAVING

* HAVING Basics
* HAVING with COUNT
* HAVING with SUM
* HAVING with AVG
* HAVING with Multiple Conditions
* WHERE vs HAVING

---

# 18. CASE Statements

* Simple CASE
* Searched CASE
* CASE with SELECT
* CASE with WHERE
* CASE with GROUP BY
* CASE with ORDER BY
* CASE with Aggregate Functions
* Nested CASE
* Conditional Aggregation

---

# 19. SQL Joins

### Basic Joins

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* CROSS JOIN

### Advanced Joins

* SELF JOIN
* Multiple JOINs
* Joining 3+ Tables
* Joining on Multiple Columns
* Non-Equi JOIN
* JOIN with Conditions
* JOIN with Aggregation

### Join Concepts

* Primary Key / Foreign Key JOIN
* One-to-One JOIN
* One-to-Many JOIN
* Many-to-Many JOIN
* JOIN Duplicates
* JOIN Cardinality
* JOIN Filtering

---

# 20. JOIN Analysis

* INNER JOIN vs LEFT JOIN
* LEFT JOIN vs RIGHT JOIN
* JOIN vs UNION
* JOIN vs Subquery
* JOIN vs EXISTS
* JOIN Duplicates
* Cartesian Product
* Missing Matches
* Anti JOIN
* Semi JOIN

---

# 21. Subqueries

* What is a Subquery?
* Scalar Subquery
* Single-Row Subquery
* Multi-Row Subquery
* Multi-Column Subquery
* Nested Subquery
* Correlated Subquery
* Subquery in SELECT
* Subquery in WHERE
* Subquery in FROM
* Subquery in HAVING
* Subquery with JOIN

---

# 22. Subquery Operators

* IN
* NOT IN
* EXISTS
* NOT EXISTS
* ANY
* SOME
* ALL

---

# 23. Set Operations

* UNION
* UNION ALL
* INTERSECT
* EXCEPT
* MINUS
* Set Compatibility
* Duplicate Handling

---

# 24. Common Table Expressions — CTE

* What is CTE?
* Basic CTE
* Multiple CTEs
* CTE with JOIN
* CTE with Aggregation
* CTE with CASE
* CTE with Window Functions
* CTE vs Subquery
* CTE vs Temporary Table
* Recursive CTE
* Hierarchical Queries

---

# 25. Window Functions

### Basic Concepts

* Window Functions
* OVER()
* PARTITION BY
* ORDER BY
* Window Frame

### Ranking

* ROW_NUMBER
* RANK
* DENSE_RANK
* NTILE

### Navigation

* LAG
* LEAD
* FIRST_VALUE
* LAST_VALUE
* NTH_VALUE

### Aggregate Window Functions

* SUM OVER
* AVG OVER
* COUNT OVER
* MIN OVER
* MAX OVER

### Advanced

* Running Total
* Cumulative Average
* Moving Average
* Rolling Sum
* Percentage of Total
* Difference from Previous Row
* First/Last Value
* Top N per Group

---

# 26. Advanced Window Functions

* PARTITION BY
* Window Frames
* ROWS
* RANGE
* GROUPS
* UNBOUNDED PRECEDING
* CURRENT ROW
* UNBOUNDED FOLLOWING
* Running Totals
* Rolling Calculations
* Moving Windows
* Sequential Analysis

---

# 27. NULL Handling

* What is NULL?
* NULL vs 0
* NULL vs Empty String
* NULL Comparisons
* Three-Valued Logic
* IS NULL
* IS NOT NULL
* COALESCE
* NULLIF
* NULL in Aggregation
* NULL in JOINs
* NULL in Sorting
* NULL in GROUP BY

---

# 28. Views

* CREATE VIEW
* DROP VIEW
* ALTER VIEW
* Simple Views
* Complex Views
* Updatable Views
* Materialized Views
* View Security
* View vs Table
* View vs CTE
* View vs Temporary Table

---

# 29. Temporary Tables

* Temporary Tables
* Local Temporary Tables
* Global Temporary Tables
* CREATE TEMP TABLE
* Temporary Table Lifecycle
* Temporary Table vs CTE
* Temporary Table vs View

---

# 30. Indexes

* What is Index?
* Why Indexes?
* CREATE INDEX
* DROP INDEX
* Unique Index
* Composite Index
* Single-Column Index
* Covering Index
* Clustered Index
* Non-Clustered Index
* B-Tree Index
* Hash Index
* Full-Text Index
* Index Selectivity
* Index Cardinality
* Index Scanning
* Index Seeking
* Advantages of Indexes
* Disadvantages of Indexes

---

# 31. Transactions

* Transaction Concept
* BEGIN
* START TRANSACTION
* COMMIT
* ROLLBACK
* SAVEPOINT
* ROLLBACK TO SAVEPOINT
* Transaction Boundaries
* Auto Commit

---

# 32. ACID Properties

* Atomicity
* Consistency
* Isolation
* Durability

---

# 33. Transaction Isolation

* Read Uncommitted
* Read Committed
* Repeatable Read
* Serializable
* Snapshot Isolation

### Concurrency Problems

* Dirty Read
* Non-Repeatable Read
* Phantom Read
* Lost Update

---

# 34. Database Relationships

* One-to-One
* One-to-Many
* Many-to-Many
* Self-Referencing Relationships
* Junction Tables
* Foreign Key Relationships
* Referential Integrity
* Cascading

---

# 35. Referential Actions

* ON DELETE CASCADE
* ON DELETE SET NULL
* ON DELETE RESTRICT
* ON UPDATE CASCADE
* ON UPDATE RESTRICT

---

# 36. Normalization

* Data Redundancy
* Data Anomalies
* Insert Anomaly
* Update Anomaly
* Delete Anomaly
* 1NF
* 2NF
* 3NF
* BCNF
* 4NF
* 5NF

---

# 37. Denormalization

* What is Denormalization?
* Why Denormalize?
* Advantages
* Disadvantages
* OLTP vs OLAP
* Normalized Database
* Analytical Database

---

# 38. Stored Procedures

* Stored Procedure Concept
* CREATE PROCEDURE
* Parameters
* IN Parameters
* OUT Parameters
* INOUT Parameters
* Variables
* Conditional Logic
* Loops
* Error Handling
* Calling Procedures
* Procedure vs Function

---

# 39. SQL Functions / User Defined Functions

* Scalar Functions
* Table-Valued Functions
* User-Defined Functions
* Function Parameters
* Return Values
* Function vs Procedure

---

# 40. Triggers

* Trigger Concept
* BEFORE Trigger
* AFTER Trigger
* INSERT Trigger
* UPDATE Trigger
* DELETE Trigger
* Row-Level Trigger
* Statement-Level Trigger
* Audit Triggers
* Trigger Advantages
* Trigger Disadvantages

---

# 41. Cursors

* Cursor Concept
* Implicit Cursor
* Explicit Cursor
* Cursor Declaration
* Cursor Opening
* Cursor Fetching
* Cursor Closing
* Cursor Use Cases
* Cursor vs Set-Based SQL

---

# 42. Error Handling

* SQL Errors
* Exception Handling
* TRY/CATCH
* SIGNAL
* RAISE
* Error Codes
* Transaction Rollback on Error

> Syntax depends heavily on the database system.

---

# 43. SQL Security

* Database Users
* Roles
* Permissions
* GRANT
* REVOKE
* Authentication
* Authorization
* Role-Based Access
* Least Privilege
* SQL Injection
* Parameterized Queries
* Prepared Statements
* Data Encryption
* Sensitive Data

---

# 44. Query Execution

* SQL Query Lifecycle
* Parsing
* Validation
* Optimization
* Execution
* Query Execution Plan
* Logical Query Processing Order
* Physical Execution
* Query Optimizer

### Logical Order

* FROM
* JOIN
* WHERE
* GROUP BY
* HAVING
* SELECT
* DISTINCT
* ORDER BY
* LIMIT / OFFSET

---

# 45. Query Optimization

* Query Performance
* EXPLAIN
* EXPLAIN ANALYZE
* Execution Plans
* Index Optimization
* JOIN Optimization
* Filter Pushdown
* Avoid SELECT *
* Avoid Unnecessary JOINs
* Subquery Optimization
* CTE Considerations
* Aggregation Optimization
* Partitioning

---

# 46. Database Design

* Requirement Analysis
* ER Modeling
* Entity Identification
* Attribute Identification
* Relationship Design
* Primary Key Selection
* Foreign Key Design
* Normalization
* Schema Design
* OLTP Schema
* OLAP Schema

---

# 47. Data Warehousing & SQL

* Data Warehouse
* OLTP
* OLAP
* ETL
* ELT
* Fact Tables
* Dimension Tables
* Star Schema
* Snowflake Schema
* Slowly Changing Dimensions
* Surrogate Keys
* Date Dimension
* Aggregation Tables

---

# 48. SQL for Data Cleaning

* Finding NULL Values
* Handling NULL Values
* Finding Duplicates
* Removing Duplicates
* Standardizing Text
* TRIM
* UPPER / LOWER
* Data Type Conversion
* Date Conversion
* Invalid Values
* Outlier Detection
* Missing Data Analysis
* CASE-Based Cleaning
* Conditional Replacement
* Data Validation

---

# 49. SQL Data Manipulation for Analytics

* Filtering
* Sorting
* Aggregation
* Grouping
* Joining
* Reshaping
* Conditional Aggregation
* Calculated Columns
* Derived Metrics
* Categorization
* Bucketing
* Ranking
* Deduplication

---

# 50. SQL Data Analysis

### Descriptive Analysis

* COUNT
* SUM
* AVG
* MIN
* MAX
* MEDIAN
* Percentiles
* Standard Deviation
* Variance

### Comparative Analysis

* Current vs Previous
* Actual vs Target
* Category Comparison
* Year-over-Year
* Month-over-Month
* Week-over-Week

### Trend Analysis

* Time-Series Analysis
* Running Totals
* Moving Average
* Growth Rate
* Cumulative Growth

---

# 51. SQL for Business Analytics

* KPI Calculation
* Revenue
* Profit
* Cost
* Average Order Value
* Customer Count
* Order Count
* Conversion Rate
* Retention Rate
* Churn Rate
* Customer Lifetime Value
* Average Revenue per User
* Market Share

---

# 52. SQL for Sales Analytics

* Total Sales
* Daily Sales
* Monthly Sales
* Yearly Sales
* Sales by Product
* Sales by Category
* Sales by Region
* Top Products
* Bottom Products
* Sales Growth
* Revenue Growth
* Average Order Value
* Customer Purchase Frequency

---

# 53. SQL for Customer Analytics

* Customer Segmentation
* New Customers
* Returning Customers
* Active Customers
* Inactive Customers
* Customer Retention
* Customer Churn
* Customer Lifetime Value
* Purchase Frequency
* Recency
* Frequency
* Monetary Analysis
* RFM Analysis

---

# 54. SQL Time-Series Analysis

* Date Filtering
* Date Extraction
* Daily Analysis
* Weekly Analysis
* Monthly Analysis
* Quarterly Analysis
* Yearly Analysis
* Month-over-Month
* Year-over-Year
* Rolling Average
* Running Total
* Cumulative Growth
* Seasonality
* Period Comparison

---

# 55. SQL Cohort Analysis

* Cohort Definition
* First Purchase Date
* Signup Cohorts
* Monthly Cohorts
* Retention Matrix
* Cohort Retention
* Cohort Revenue
* Customer Lifetime Analysis

---

# 56. SQL Funnel Analysis

* Funnel Stages
* Users per Stage
* Conversion Rate
* Drop-Off Rate
* Stage-to-Stage Conversion
* Funnel Completion
* Conditional Aggregation

---

# 57. SQL Ranking Problems

* Highest Salary
* Second Highest Salary
* Nth Highest Salary
* Top N Employees
* Top N Products
* Top N Customers
* Top N per Department
* Rank Within Category
* Rank Within Region
* Ranking with Ties

---

# 58. SQL Interview Problems

* Duplicate Records
* Remove Duplicates
* Second Highest Salary
* Nth Highest Salary
* Employees Above Average
* Employees Below Average
* Top N per Group
* Missing Numbers
* Consecutive Records
* Gaps and Islands
* Running Total
* Moving Average
* Duplicate Customers
* First Purchase
* Latest Purchase
* Customers with No Orders
* Products Never Sold
* Department with Highest Average
* Month with Highest Revenue
* Year-over-Year Growth

---

# 59. Advanced SQL Analytics Patterns

* Top N per Group
* Gaps and Islands
* Running Totals
* Moving Averages
* Sessionization
* Deduplication
* First/Last Record
* Latest Record per Entity
* Change Detection
* Retention
* Cohort Analysis
* Funnel Analysis
* Pareto Analysis
* Percentile Analysis
* Median Calculation
* Rolling Metrics

---

# 60. SQL + Python Integration

* Connecting Python to SQL
* SQLAlchemy
* Database Drivers
* Reading SQL into Pandas
* Writing Pandas DataFrames to SQL
* Parameterized Queries
* Executing SQL from Python
* Transactions from Python
* ETL with Python + SQL

---

# 61. SQL + Pandas

* SQL SELECT vs Pandas Selection
* WHERE vs Boolean Filtering
* GROUP BY SQL vs Pandas
* JOIN SQL vs merge()
* ORDER BY vs sort_values()
* SQL Aggregation vs Pandas Aggregation
* SQL Window Functions vs Pandas Operations
* Reading SQL Data into DataFrames
* Writing DataFrames to SQL

---

# 62. SQL Projects for Data Analytics

### Beginner

* Employee Database Analysis
* Student Database Analysis
* Library Database
* Inventory Database

### Intermediate

* Sales Analysis
* Customer Analysis
* E-Commerce Analysis
* Movie Database Analysis
* Hospital Data Analysis

### Advanced

* Customer Retention
* Cohort Analysis
* RFM Analysis
* Sales Funnel
* Revenue Analytics
* Product Analytics
* Marketing Analytics
* Business KPI Dashboard Backend

---

# 63. SQL Practice Levels

## Level 1 — Beginner

* SELECT
* WHERE
* ORDER BY
* DISTINCT
* LIMIT
* Basic Functions

## Level 2 — Intermediate

* GROUP BY
* HAVING
* Aggregation
* CASE
* JOINs
* Subqueries

## Level 3 — Advanced

* CTEs
* Window Functions
* Recursive Queries
* Complex JOINs
* Advanced Aggregations

## Level 4 — Data Analytics

* KPI Queries
* Time-Series
* Cohort
* Retention
* Funnel
* RFM
* Business Analysis

## Level 5 — SQL Development

* Procedures
* Functions
* Triggers
* Transactions
* Indexes
* Optimization
* Security
* Database Design

---

# 64. SQL Cheat Sheets

* SQL Syntax Cheat Sheet
* SELECT Cheat Sheet
* JOIN Cheat Sheet
* Aggregate Functions Cheat Sheet
* String Functions Cheat Sheet
* Date Functions Cheat Sheet
* Window Functions Cheat Sheet
* CTE Cheat Sheet
* Subquery Cheat Sheet
* SQL Interview Cheat Sheet
* Data Analytics SQL Cheat Sheet

---

# 65. SQL Database-Specific Topics

## MySQL

* MySQL Syntax
* MySQL Functions
* MySQL Procedures
* MySQL Triggers
* MySQL Indexes

## PostgreSQL

* PostgreSQL Syntax
* PostgreSQL Functions
* PostgreSQL Arrays
* PostgreSQL JSON
* PostgreSQL Window Functions
* PostgreSQL Extensions

## SQL Server

* T-SQL
* SQL Server Functions
* Stored Procedures
* CTEs
* Window Functions

## Oracle

* PL/SQL
* Oracle Functions
* Procedures
* Packages
* Triggers

---

# 66. Final SQL Master Checklist

### Core SQL

* [ ] SELECT
* [ ] INSERT
* [ ] UPDATE
* [ ] DELETE
* [ ] CREATE
* [ ] ALTER
* [ ] DROP
* [ ] TRUNCATE

### Querying

* [ ] WHERE
* [ ] DISTINCT
* [ ] ORDER BY
* [ ] GROUP BY
* [ ] HAVING
* [ ] LIMIT / OFFSET

### Functions

* [ ] String Functions
* [ ] Numeric Functions
* [ ] Date Functions
* [ ] Aggregate Functions
* [ ] NULL Functions
* [ ] CASE

### Relationships

* [ ] Primary Key
* [ ] Foreign Key
* [ ] Constraints
* [ ] Relationships
* [ ] JOINs

### Advanced Querying

* [ ] Subqueries
* [ ] EXISTS
* [ ] ANY
* [ ] ALL
* [ ] UNION
* [ ] UNION ALL
* [ ] CTE
* [ ] Recursive CTE

### Analytics

* [ ] Window Functions
* [ ] ROW_NUMBER
* [ ] RANK
* [ ] DENSE_RANK
* [ ] LAG
* [ ] LEAD
* [ ] Running Total
* [ ] Moving Average
* [ ] Top N per Group
* [ ] Time-Series
* [ ] Cohort
* [ ] Retention
* [ ] Funnel
* [ ] RFM

### Database Development

* [ ] Views
* [ ] Temporary Tables
* [ ] Indexes
* [ ] Transactions
* [ ] ACID
* [ ] Isolation Levels
* [ ] Procedures
* [ ] Functions
* [ ] Triggers
* [ ] Cursors
* [ ] Error Handling

### Database Design

* [ ] ER Diagrams
* [ ] Normalization
* [ ] Denormalization
* [ ] OLTP
* [ ] OLAP
* [ ] Data Warehousing
* [ ] Star Schema
* [ ] Snowflake Schema

### Performance & Security

* [ ] EXPLAIN
* [ ] Query Optimization
* [ ] Index Optimization
* [ ] Execution Plans
* [ ] SQL Injection
* [ ] Parameterized Queries
* [ ] Users
* [ ] Roles
* [ ] Permissions

### Career / Interview

* [ ] SQL Coding Problems
* [ ] SQL Interview Questions
* [ ] Data Analytics Problems
* [ ] Business Case Studies
* [ ] SQL + Python
* [ ] SQL + Pandas
* [ ] SQL Projects
