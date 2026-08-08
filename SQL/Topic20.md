# 🗄️ Database Design, Data Warehousing & SQL

A complete revision guide for **database design, relational databases, data warehouses, dimensional modeling, ETL/ELT, OLTP, OLAP, star/snowflake schemas, fact and dimension tables, and SQL usage in analytical systems**.

---

# 📚 Table of Contents

1. [Database Design](#1-database-design)
2. [Database Design Process](#2-database-design-process)
3. [Requirements Analysis](#3-requirements-analysis)
4. [Entities and Attributes](#4-entities-and-attributes)
5. [Relationships](#5-relationships)
6. [ER Model](#6-er-model)
7. [Cardinality](#7-cardinality)
8. [Primary and Foreign Keys](#8-primary-and-foreign-keys)
9. [Database Schema](#9-database-schema)
10. [Normalization](#10-normalization)
11. [Denormalization](#11-denormalization)
12. [OLTP](#12-oltp)
13. [OLAP](#13-olap)
14. [OLTP vs OLAP](#14-oltp-vs-olap)
15. [Data Warehousing](#15-data-warehousing)
16. [Why Data Warehouses Are Needed](#16-why-data-warehouses-are-needed)
17. [Data Warehouse Architecture](#17-data-warehouse-architecture)
18. [Data Warehouse Components](#18-data-warehouse-components)
19. [ETL](#19-etl)
20. [ELT](#20-elt)
21. [ETL vs ELT](#21-etl-vs-elt)
22. [Data Warehouse Schemas](#22-data-warehouse-schemas)
23. [Star Schema](#23-star-schema)
24. [Snowflake Schema](#24-snowflake-schema)
25. [Star vs Snowflake](#25-star-vs-snowflake)
26. [Fact Tables](#26-fact-tables)
27. [Dimension Tables](#27-dimension-tables)
28. [Fact vs Dimension](#28-fact-vs-dimension)
29. [Measures](#29-measures)
30. [Granularity](#30-granularity)
31. [Surrogate Keys](#31-surrogate-keys)
32. [Slowly Changing Dimensions](#32-slowly-changing-dimensions)
33. [Data Marts](#33-data-marts)
34. [ODS](#34-ods)
35. [Data Lake](#35-data-lake)
36. [Data Warehouse vs Data Lake](#36-data-warehouse-vs-data-lake)
37. [Modern Data Architecture](#37-modern-data-architecture)
38. [SQL in Data Warehousing](#38-sql-in-data-warehousing)
39. [Analytical SQL Example](#39-analytical-sql-example)
40. [OLAP Operations](#40-olap-operations)
41. [SQL Aggregations](#41-sql-aggregations)
42. [SQL Window Functions in Warehousing](#42-sql-window-functions-in-warehousing)
43. [CTEs in Analytical Queries](#43-ctes-in-analytical-queries)
44. [Date and Time Analysis](#44-date-and-time-analysis)
45. [Business Intelligence](#45-business-intelligence)
46. [Data Warehouse Best Practices](#46-data-warehouse-best-practices)
47. [Database Design Best Practices](#47-database-design-best-practices)
48. [Complete Data Warehouse Example](#48-complete-data-warehouse-example)
49. [Important Interview Questions](#49-important-interview-questions)
50. [Quick Revision](#50-quick-revision)

---

# 1. Database Design

## Easy Definition

**Database design** is the process of planning how data should be stored, organized, related, and accessed inside a database.

Think of it as creating a **blueprint for a database** before actually building it.

### Technical Definition

Database design is the process of defining:

* Entities
* Attributes
* Relationships
* Constraints
* Keys
* Tables
* Data types
* Normalization structure
* Indexes
* Security requirements

to create an efficient and reliable database system.

---

# 2. Database Design Process

A typical database design process is:

```text
Requirements
     ↓
Identify Entities
     ↓
Identify Attributes
     ↓
Identify Relationships
     ↓
Create ER Diagram
     ↓
Define Keys
     ↓
Normalize
     ↓
Create Logical Schema
     ↓
Create Physical Database
     ↓
Indexes & Optimization
     ↓
Testing
```

---

# 3. Requirements Analysis

Before creating tables, understand what the application needs.

### Example

Suppose we are designing a database for an online shopping application.

Requirements:

* Customers can register.
* Customers can place orders.
* Orders contain products.
* Products belong to categories.
* Customers can make payments.
* Orders have statuses.

From these requirements, we can identify entities.

```text
Customer
Product
Category
Order
OrderItem
Payment
```

---

# 4. Entities and Attributes

## Entity

An **entity** is a real-world object or concept about which we store information.

Examples:

```text
Student
Employee
Customer
Product
Order
Department
```

## Attribute

An **attribute** describes an entity.

Example:

```text
Customer
---------
customer_id
name
email
phone
address
```

Here:

* `Customer` → Entity
* `customer_id` → Attribute
* `name` → Attribute
* `email` → Attribute

---

# 5. Relationships

A relationship describes how entities are connected.

Example:

```text
Customer → places → Order
```

Another example:

```text
Department → employs → Employee
```

```text
Customer → purchases → Product
```

---

# 6. ER Model

**ER = Entity Relationship**

An ER model represents:

* Entities
* Attributes
* Relationships

Example:

```text
CUSTOMER
---------
customer_id
name
email
   |
   | places
   ↓
ORDER
---------
order_id
order_date
amount
```

### Purpose

ER modeling helps us understand the database before implementing it.

---

# 7. Cardinality

Cardinality describes how many records of one entity can be associated with another entity.

## One-to-One

```text
Person 1 ───── 1 Passport
```

One person has one passport.

---

## One-to-Many

```text
Department 1 ───── N Employees
```

One department can have many employees.

---

## Many-to-Many

```text
Student N ───── N Course
```

A student can take many courses.

A course can have many students.

Usually, many-to-many relationships require a junction table.

```text
Student
   |
   ↓
Student_Course
   ↑
   |
Course
```

---

# 8. Primary and Foreign Keys

## Primary Key

A primary key uniquely identifies each record.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150)
);
```

Example:

```text
customer_id
-----------
1
2
3
4
```

A primary key must be:

* Unique
* Non-null

---

## Foreign Key

A foreign key connects one table to another.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

Relationship:

```text
customers
    |
    | customer_id
    ↓
orders
```

---

# 9. Database Schema

A **schema** describes the structure of a database.

It defines:

* Tables
* Columns
* Data types
* Relationships
* Constraints
* Views
* Indexes
* Other database objects

Example:

```text
Sales Database

Customers
Orders
Order_Items
Products
Payments
```

---

# 10. Normalization

Normalization is the process of organizing data to:

* Reduce redundancy
* Prevent inconsistencies
* Improve data integrity
* Eliminate update anomalies

Example of poor design:

```text
Order_ID | Customer | Product1 | Product2 | Product3
```

Better design:

```text
Orders
Order_Items
Products
Customers
```

---

# 11. Denormalization

Denormalization intentionally introduces redundancy to improve query performance.

Example:

Instead of joining:

```text
Orders
Customers
Products
```

we may store some frequently accessed information directly in an analytical table.

### Normalization

```text
Less redundancy
More joins
Better transactional integrity
```

### Denormalization

```text
More redundancy
Fewer joins
Often faster analytical queries
```

---

# 12. OLTP

**OLTP = Online Transaction Processing**

OLTP systems are designed for everyday transactions.

Examples:

* Banking
* E-commerce
* Railway booking
* ATM
* Payroll
* Order processing

Example:

```sql
INSERT INTO orders
VALUES (101, 10, CURRENT_DATE);
```

This represents a transaction.

---

# 13. OLAP

**OLAP = Online Analytical Processing**

OLAP systems are designed for analysis.

Examples:

```text
Sales analysis
Customer analysis
Revenue analysis
Profit analysis
Regional analysis
Yearly trends
```

Example:

```sql
SELECT
    region,
    SUM(sales_amount) AS total_sales
FROM sales
GROUP BY region;
```

---

# 14. OLTP vs OLAP

| Feature     | OLTP                 | OLAP                           |
| ----------- | -------------------- | ------------------------------ |
| Purpose     | Transactions         | Analysis                       |
| Data        | Current              | Historical                     |
| Queries     | Short                | Complex                        |
| Operations  | INSERT/UPDATE/DELETE | Mostly SELECT                  |
| Users       | Applications         | Analysts/BI users              |
| Database    | Highly normalized    | Often dimensional/denormalized |
| Data volume | Moderate             | Very large                     |
| Example     | Banking system       | Sales dashboard                |

---

# 15. Data Warehousing

## Easy Definition

A **data warehouse** is a centralized system used to store large amounts of historical data for analysis and reporting.

Think:

```text
Operational Databases
       ↓
Data Warehouse
       ↓
Reports / Dashboards / Analytics
```

### Technical Definition

A data warehouse is a subject-oriented, integrated, time-variant, and non-volatile collection of data designed to support analytical and decision-making workloads.

---

# 16. Why Data Warehouses Are Needed

Operational databases are designed mainly for transactions.

Suppose a company has:

```text
E-commerce Database
CRM Database
Payment Database
Website Database
Marketing Database
```

Management wants:

> "Show total sales by product, region, customer segment, and year for the last five years."

Running this directly against operational systems may be expensive.

Instead:

```text
Multiple Sources
       ↓
ETL / ELT
       ↓
Data Warehouse
       ↓
Analytics
```

---

# 17. Data Warehouse Architecture

Basic architecture:

```text
          DATA SOURCES
               |
     -----------------------
     |          |          |
   MySQL      CRM        CSV
     |          |          |
     -----------------------
               |
               ↓
          ETL / ELT
               |
               ↓
        STAGING AREA
               |
               ↓
       DATA WAREHOUSE
               |
       ----------------
       |              |
   Data Marts      Semantic Layer
       |              |
       ----------------
               |
               ↓
       BI / Analytics
```

---

# 18. Data Warehouse Components

Important components:

```text
1. Source Systems
2. Data Ingestion
3. Staging Area
4. ETL / ELT
5. Data Warehouse
6. Data Marts
7. Semantic Layer
8. BI Tools
```

---

# 19. ETL

**ETL = Extract, Transform, Load**

```text
Extract
   ↓
Transform
   ↓
Load
```

## Extract

Get data from sources.

```text
MySQL
CSV
Excel
API
CRM
ERP
```

## Transform

Clean and modify data.

Examples:

```text
Remove duplicates
Handle NULLs
Convert data types
Standardize dates
Calculate metrics
Validate values
```

## Load

Load transformed data into the warehouse.

---

# 20. ELT

**ELT = Extract, Load, Transform**

```text
Extract
   ↓
Load
   ↓
Transform
```

The raw data is first loaded into the target platform and transformation happens there.

Modern cloud data platforms commonly support this approach.

---

# 21. ETL vs ELT

| ETL                             | ELT                                         |
| ------------------------------- | ------------------------------------------- |
| Transform before loading        | Transform after loading                     |
| Traditional architecture        | Common modern architecture                  |
| Processing outside warehouse    | Processing often inside warehouse           |
| Useful for controlled pipelines | Useful for large-scale analytical platforms |

---

# 22. Data Warehouse Schemas

The most important dimensional schemas are:

```text
1. Star Schema
2. Snowflake Schema
```

---

# 23. Star Schema

A star schema contains:

* One central fact table
* Multiple dimension tables

Example:

```text
              Dim_Date
                 |
                 |
Dim_Product — Fact_Sales — Dim_Customer
                 |
                 |
             Dim_Store
```

It looks like a star.

---

# 24. Snowflake Schema

Snowflake schema normalizes dimensions.

Example:

```text
                 Dim_Date
                    |
                    |
Dim_Product — Fact_Sales — Dim_Customer
     |
     ↓
Dim_Category
     |
     ↓
Dim_Department
```

---

# 25. Star vs Snowflake

| Star                                | Snowflake                |
| ----------------------------------- | ------------------------ |
| Dimensions usually denormalized     | Dimensions normalized    |
| Simple                              | More complex             |
| Fewer joins                         | More joins               |
| Often easier for BI                 | Can reduce redundancy    |
| Faster/simple queries in many cases | More complex query paths |

---

# 26. Fact Tables

A **fact table** stores measurable business events.

Examples:

```text
Sales
Orders
Payments
Transactions
Shipments
```

Example:

```text
fact_sales
----------------
sales_id
date_key
product_key
customer_key
store_key
quantity
sales_amount
profit
```

Facts generally contain:

* Foreign keys
* Numeric measurements

---

# 27. Dimension Tables

Dimension tables provide descriptive information.

Examples:

```text
dim_customer
dim_product
dim_date
dim_store
dim_employee
```

Example:

```text
dim_product
----------------
product_key
product_id
product_name
category
brand
price
```

---

# 28. Fact vs Dimension

| Fact                  | Dimension                       |
| --------------------- | ------------------------------- |
| Measures events       | Describes entities              |
| Numeric data common   | Descriptive data common         |
| Usually large         | Usually smaller                 |
| Contains foreign keys | Contains descriptive attributes |
| Sales amount          | Product name                    |
| Quantity              | Customer city                   |

---

# 29. Measures

Measures are numerical values used for analysis.

Examples:

```text
sales_amount
quantity
profit
discount
cost
```

Example:

```sql
SELECT SUM(sales_amount)
FROM fact_sales;
```

---

# 30. Granularity

**Granularity** means the level of detail represented by one row.

This is one of the most important concepts in data warehouse design.

Suppose:

```text
One row = One product sold in one order
```

Then the grain is:

> One product line per order.

Another table might have:

```text
One row = One complete order
```

These are different grains.

### Always define the grain before designing a fact table.

---

# 31. Surrogate Keys

A surrogate key is an artificial key generated for warehouse records.

Example:

```text
product_key
-----------
1001
1002
1003
```

Instead of using the source system's business identifier directly:

```text
product_id = PROD-001
```

Warehouse systems commonly use surrogate keys for dimensions.

Example:

```text
dim_product

product_key | product_id | product_name
------------|------------|-------------
1           | P100       | Laptop
2           | P101       | Mouse
```

---

# 32. Slowly Changing Dimensions

**SCD = Slowly Changing Dimension**

SCD deals with changes in dimension attributes over time.

Example:

A customer moves from:

```text
Hyderabad
```

to:

```text
Bangalore
```

How should the warehouse handle this change?

---

## SCD Type 0

Do not change the value.

```text
Original value remains forever
```

---

## SCD Type 1

Overwrite the old value.

```text
Before:
Hyderabad

After:
Bangalore
```

History is lost.

---

## SCD Type 2

Maintain complete history.

Example:

```text
customer_key | city       | start_date | end_date   | current
-------------|------------|------------|------------|--------
1            | Hyderabad  | 2024-01-01 | 2025-06-30 | 0
2            | Bangalore  | 2025-07-01 | NULL       | 1
```

This is extremely important in data warehousing.

---

# 33. Data Marts

A **data mart** is a smaller analytical data store focused on a specific business area.

Examples:

```text
Sales Data Mart
Finance Data Mart
Marketing Data Mart
HR Data Mart
```

Example:

```text
Enterprise Data Warehouse
          |
    ----------------
    |       |      |
  Sales   HR    Finance
   Mart   Mart    Mart
```

---

# 34. ODS

**ODS = Operational Data Store**

An ODS is commonly used as an intermediate store containing relatively current integrated operational data.

```text
Source Systems
      ↓
     ODS
      ↓
Data Warehouse
```

### ODS vs Data Warehouse

| ODS                              | Data Warehouse                  |
| -------------------------------- | ------------------------------- |
| More current data                | Historical data                 |
| Operational/integration purposes | Analytical purposes             |
| Frequently refreshed             | Often batch/incremental refresh |
| Shorter-term operational view    | Long-term analytical view       |

---

# 35. Data Lake

A **data lake** stores large amounts of data, often in raw or semi-processed form.

It can contain:

```text
Structured data
Semi-structured data
Unstructured data
```

Examples:

```text
CSV
JSON
Images
Logs
Videos
Database exports
IoT data
```

---

# 36. Data Warehouse vs Data Lake

| Data Warehouse           | Data Lake                            |
| ------------------------ | ------------------------------------ |
| Structured/curated data  | Raw + structured + semi-structured   |
| Schema-on-write commonly | Schema-on-read commonly              |
| BI and reporting         | Data science, ML, analytics, storage |
| Highly organized         | Flexible                             |
| Curated                  | Often raw                            |

---

# 37. Modern Data Architecture

A modern analytical architecture can look like:

```text
                 DATA SOURCES
                      |
        -----------------------------
        |             |             |
     Databases       APIs          Files
        |             |             |
        -----------------------------
                      |
                 INGESTION
                      |
                      ↓
                  DATA LAKE
                      |
                      ↓
              DATA WAREHOUSE
                      |
             ----------------
             |              |
        Data Marts      Semantic Layer
             |              |
             ----------------
                      |
                      ↓
              BI / Analytics
```

---

# 38. SQL in Data Warehousing

SQL is one of the most important languages for working with data warehouses.

SQL is used for:

```text
Data extraction
Data transformation
Data cleaning
Data aggregation
Data analysis
Reporting
Data validation
Data quality checks
Table creation
Views
CTEs
Window functions
Performance optimization
```

---

# 39. Analytical SQL Example

Suppose we have:

```text
fact_sales
-----------
date_key
product_key
customer_key
store_key
quantity
sales_amount
profit
```

And:

```text
dim_product
-----------
product_key
product_name
category
```

We can calculate sales by category:

```sql
SELECT
    p.category,
    SUM(s.sales_amount) AS total_sales
FROM fact_sales s
JOIN dim_product p
    ON s.product_key = p.product_key
GROUP BY p.category
ORDER BY total_sales DESC;
```

Result:

```text
category       total_sales
-------------- -----------
Electronics    500000
Clothing       350000
Furniture      250000
```

---

# 40. OLAP Operations

Important OLAP operations include:

```text
1. Roll-up
2. Drill-down
3. Slice
4. Dice
5. Pivot
```

---

## Roll-Up

Move from detailed data to summarized data.

```text
Day
 ↓
Month
 ↓
Quarter
 ↓
Year
```

Example:

```text
Daily Sales
     ↓
Monthly Sales
     ↓
Yearly Sales
```

SQL:

```sql
SELECT
    EXTRACT(YEAR FROM sale_date) AS year,
    SUM(sales_amount) AS sales
FROM sales
GROUP BY EXTRACT(YEAR FROM sale_date);
```

---

## Drill-Down

Move from summary to detailed data.

```text
Year
 ↓
Quarter
 ↓
Month
 ↓
Day
```

---

## Slice

Select one dimension value.

Example:

```text
Sales for 2026 only
```

```sql
SELECT *
FROM fact_sales
WHERE year = 2026;
```

---

## Dice

Select multiple dimensions.

```text
Year = 2026
AND
Region IN ('South', 'West')
AND
Category = 'Electronics'
```

---

## Pivot

Change the orientation of analytical data.

Example:

```text
Rows    → Products
Columns → Years
Values  → Sales
```

---

# 41. SQL Aggregations

Common aggregation functions:

```sql
SUM()
AVG()
COUNT()
MIN()
MAX()
```

Example:

```sql
SELECT
    category,
    SUM(sales_amount) AS total_sales,
    AVG(sales_amount) AS avg_sales,
    COUNT(*) AS transactions,
    MIN(sales_amount) AS minimum_sale,
    MAX(sales_amount) AS maximum_sale
FROM sales
GROUP BY category;
```

---

# 42. SQL Window Functions in Warehousing

Window functions are extremely important in analytical SQL.

Example:

```sql
SELECT
    product_id,
    sales_amount,
    SUM(sales_amount) OVER (
        PARTITION BY product_id
    ) AS product_total
FROM sales;
```

Unlike `GROUP BY`, window functions can preserve individual rows.

---

## Ranking

```sql
SELECT
    product_id,
    sales_amount,
    RANK() OVER (
        ORDER BY sales_amount DESC
    ) AS sales_rank
FROM sales;
```

---

## Partitioned Ranking

```sql
SELECT
    region,
    product_id,
    sales_amount,
    RANK() OVER (
        PARTITION BY region
        ORDER BY sales_amount DESC
    ) AS region_rank
FROM sales;
```

---

# 43. CTEs in Analytical Queries

**CTE = Common Table Expression**

CTEs make complex queries easier to understand.

```sql
WITH category_sales AS (
    SELECT
        category,
        SUM(sales_amount) AS total_sales
    FROM sales
    GROUP BY category
)
SELECT *
FROM category_sales
WHERE total_sales > 100000;
```

Multiple CTEs can be used:

```sql
WITH sales_data AS (
    SELECT *
    FROM sales
),
category_sales AS (
    SELECT
        category,
        SUM(sales_amount) AS total_sales
    FROM sales_data
    GROUP BY category
)
SELECT *
FROM category_sales
ORDER BY total_sales DESC;
```

---

# 44. Date and Time Analysis

Time analysis is one of the most important warehouse operations.

Common levels:

```text
Year
Quarter
Month
Week
Day
Hour
```

Example:

```sql
SELECT
    EXTRACT(YEAR FROM sale_date) AS year,
    EXTRACT(MONTH FROM sale_date) AS month,
    SUM(sales_amount) AS total_sales
FROM sales
GROUP BY
    EXTRACT(YEAR FROM sale_date),
    EXTRACT(MONTH FROM sale_date)
ORDER BY year, month;
```

---

## Year-over-Year Analysis

Suppose:

```text
2025 sales = 100000
2026 sales = 120000
```

Growth:

```text
20%
```

Example using `LAG()`:

```sql
WITH yearly_sales AS (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        SUM(sales_amount) AS sales
    FROM sales
    GROUP BY EXTRACT(YEAR FROM sale_date)
)
SELECT
    year,
    sales,
    LAG(sales) OVER (ORDER BY year) AS previous_year_sales,
    sales - LAG(sales) OVER (ORDER BY year) AS sales_change
FROM yearly_sales;
```

---

# 45. Business Intelligence

**BI = Business Intelligence**

BI converts data into useful information for decision-making.

Typical flow:

```text
Data Sources
     ↓
ETL / ELT
     ↓
Data Warehouse
     ↓
Data Modeling
     ↓
BI Tool
     ↓
Dashboard
     ↓
Business Decision
```

Examples of business questions:

```text
What are our total sales?
Which product generates the most revenue?
Which region performs best?
Who are our top customers?
What is the monthly sales trend?
Which products are declining?
```

---

# 46. Data Warehouse Best Practices

## 1. Define the grain

Always define:

> What does one row represent?

before designing a fact table.

---

## 2. Use appropriate keys

Use:

```text
Primary keys
Foreign keys
Surrogate keys
```

where appropriate.

---

## 3. Maintain data quality

Check:

```text
NULL values
Duplicates
Invalid dates
Invalid categories
Negative values
Missing records
Referential integrity
```

---

## 4. Separate facts and dimensions

Example:

```text
Fact → numerical business events

Dimension → descriptive context
```

---

## 5. Design for analytical queries

Think about queries users will run.

Example:

```sql
GROUP BY
JOIN
WHERE
WINDOW FUNCTIONS
ORDER BY
```

---

## 6. Optimize large tables

Consider:

```text
Partitioning
Clustering
Indexes where supported/useful
Materialized views
Query pruning
Appropriate data types
```

Exact optimization features depend on the database/warehouse platform.

---

# 47. Database Design Best Practices

### 1. Understand requirements

Do not create tables before understanding the business.

### 2. Choose appropriate data types

Bad:

```sql
age VARCHAR(10)
```

Better:

```sql
age INT
```

### 3. Use constraints

```sql
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
CHECK
DEFAULT
```

### 4. Avoid unnecessary duplication

Use normalization in transactional systems when appropriate.

### 5. Use indexes carefully

Indexes can improve reads but can add storage and write overhead.

### 6. Maintain referential integrity

Ensure foreign keys point to valid records where enforced.

---

# 48. Complete Data Warehouse Example

Let's design a simple **Sales Data Warehouse**.

---

## Step 1: Business Requirement

Management wants to analyze:

```text
Sales by product
Sales by customer
Sales by region
Sales by month
Sales by year
Profit by category
Top products
Top customers
```

---

## Step 2: Identify Dimensions

```text
Customer
Product
Date
Store
```

---

## Step 3: Identify Fact

```text
Sales
```

---

## Step 4: Create Dimension Tables

### Customer

```sql
CREATE TABLE dim_customer (
    customer_key INT PRIMARY KEY,
    customer_id INT,
    customer_name VARCHAR(100),
    city VARCHAR(100),
    state VARCHAR(100),
    region VARCHAR(50)
);
```

### Product

```sql
CREATE TABLE dim_product (
    product_key INT PRIMARY KEY,
    product_id INT,
    product_name VARCHAR(150),
    category VARCHAR(100),
    brand VARCHAR(100)
);
```

### Date

```sql
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,
    full_date DATE,
    day INT,
    month INT,
    month_name VARCHAR(20),
    quarter INT,
    year INT
);
```

---

## Step 5: Fact Table

```sql
CREATE TABLE fact_sales (
    sales_key INT PRIMARY KEY,
    date_key INT,
    customer_key INT,
    product_key INT,
    quantity INT,
    sales_amount DECIMAL(15,2),
    cost_amount DECIMAL(15,2),
    profit DECIMAL(15,2),

    FOREIGN KEY (date_key)
        REFERENCES dim_date(date_key),

    FOREIGN KEY (customer_key)
        REFERENCES dim_customer(customer_key),

    FOREIGN KEY (product_key)
        REFERENCES dim_product(product_key)
);
```

---

# 49. Analytical Queries

## Total Sales

```sql
SELECT
    SUM(sales_amount) AS total_sales
FROM fact_sales;
```

---

## Total Profit

```sql
SELECT
    SUM(profit) AS total_profit
FROM fact_sales;
```

---

## Sales by Product

```sql
SELECT
    p.product_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_product p
    ON f.product_key = p.product_key
GROUP BY p.product_name
ORDER BY total_sales DESC;
```

---

## Sales by Category

```sql
SELECT
    p.category,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_product p
    ON f.product_key = p.product_key
GROUP BY p.category
ORDER BY total_sales DESC;
```

---

## Sales by Region

```sql
SELECT
    c.region,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_customer c
    ON f.customer_key = c.customer_key
GROUP BY c.region
ORDER BY total_sales DESC;
```

---

## Monthly Sales

```sql
SELECT
    d.year,
    d.month,
    d.month_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_date d
    ON f.date_key = d.date_key
GROUP BY
    d.year,
    d.month,
    d.month_name
ORDER BY
    d.year,
    d.month;
```

---

## Top 10 Products

```sql
SELECT
    p.product_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_product p
    ON f.product_key = p.product_key
GROUP BY p.product_name
ORDER BY total_sales DESC
LIMIT 10;
```

---

## Top Customers

```sql
SELECT
    c.customer_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_customer c
    ON f.customer_key = c.customer_key
GROUP BY c.customer_name
ORDER BY total_sales DESC
LIMIT 10;
```

---

## Category Profit

```sql
SELECT
    p.category,
    SUM(f.profit) AS total_profit
FROM fact_sales f
JOIN dim_product p
    ON f.product_key = p.product_key
GROUP BY p.category
ORDER BY total_profit DESC;
```

---

# 50. Important Interview Questions

## Database Design

### What is database design?

Database design is the process of defining the structure, relationships, keys, constraints, and organization of data.

### What is an entity?

A real-world object or concept represented in a database.

### What is an attribute?

A property describing an entity.

### What is cardinality?

The number of records that can participate in a relationship.

### What is normalization?

Organizing data to reduce redundancy and improve integrity.

### What is denormalization?

Intentionally introducing redundancy to improve performance or simplify access.

---

# Data Warehouse Questions

### What is a data warehouse?

A centralized analytical data store containing integrated and historical data.

### Why do we need a data warehouse?

To combine data from different sources and support analytical queries, reporting, and decision-making.

### What is a fact table?

A table containing measurable business events.

### What is a dimension table?

A table containing descriptive context for facts.

### What is granularity?

The level of detail represented by each row in a fact table.

### What is a star schema?

A central fact table connected directly to dimension tables.

### What is a snowflake schema?

A dimensional model where dimensions are further normalized.

### What is a data mart?

A subject-specific analytical data store.

### What is SCD?

Slowly Changing Dimension, a technique for managing changes to dimension attributes over time.

---

# ⭐ Most Important Concepts to Remember

```text
DATABASE DESIGN
      ↓
Requirements
      ↓
Entities
      ↓
Attributes
      ↓
Relationships
      ↓
Keys
      ↓
ER Model
      ↓
Normalization
      ↓
Schema
```

---

```text
OLTP
 ↓
Transactions
 ↓
Operational Database
```

```text
OLAP
 ↓
Analysis
 ↓
Data Warehouse
 ↓
BI / Reporting
```

---

```text
DATA WAREHOUSE
       |
       ↓
   FACT TABLE
       |
   ----------------
   |      |       |
   ↓      ↓       ↓
PRODUCT CUSTOMER DATE
DIM      DIM      DIM
```

---

```text
ETL

Extract
   ↓
Transform
   ↓
Load
```

```text
ELT

Extract
   ↓
Load
   ↓
Transform
```

---

# 🔥 Complete Learning Flow

For SQL + Data Analytics, understand these concepts in this order:

```text
SQL Fundamentals
       ↓
Database Fundamentals
       ↓
Tables & Relationships
       ↓
Keys & Constraints
       ↓
CRUD Operations
       ↓
Filtering
       ↓
Operators
       ↓
Functions
       ↓
GROUP BY
       ↓
HAVING
       ↓
CASE
       ↓
JOINS
       ↓
Subqueries
       ↓
CTEs
       ↓
Window Functions
       ↓
Views
       ↓
Indexes
       ↓
Transactions
       ↓
Normalization
       ↓
Database Design
       ↓
OLTP
       ↓
OLAP
       ↓
Data Warehousing
       ↓
Fact & Dimension Tables
       ↓
Star / Snowflake Schema
       ↓
ETL / ELT
       ↓
SCD
       ↓
Analytical SQL
       ↓
BI / Reporting
```

---

# 🧠 One-Minute Revision

| Concept         | Remember                                    |
| --------------- | ------------------------------------------- |
| Database        | Organized collection of data                |
| Database Design | Blueprint for storing data                  |
| Entity          | Real-world object                           |
| Attribute       | Property of entity                          |
| Relationship    | Connection between entities                 |
| Primary Key     | Uniquely identifies a row                   |
| Foreign Key     | Connects tables                             |
| Normalization   | Reduce redundancy                           |
| Denormalization | Add redundancy for access/performance       |
| OLTP            | Transaction processing                      |
| OLAP            | Analytical processing                       |
| Data Warehouse  | Central analytical data store               |
| ETL             | Extract → Transform → Load                  |
| ELT             | Extract → Load → Transform                  |
| Fact            | Business event/measure                      |
| Dimension       | Descriptive context                         |
| Grain           | Detail represented by one fact row          |
| Star Schema     | Fact + denormalized dimensions              |
| Snowflake       | Fact + normalized dimensions                |
| Data Mart       | Department/subject-focused analytical store |
| SCD             | Handling dimension changes                  |
| Data Lake       | Large repository of raw/flexible data       |
| BI              | Turning data into business insights         |

---

# 🎯 Final Mental Model

The entire concept can be understood as:

```text
                 BUSINESS
                    |
                    ↓
              DATA SOURCES
                    |
          ---------------------
          |         |         |
       Database    API       Files
          |         |         |
          ---------------------
                    |
                    ↓
               ETL / ELT
                    |
                    ↓
              DATA WAREHOUSE
                    |
          ---------------------
          |                   |
     FACT TABLES        DIMENSION TABLES
          |                   |
          -----------JOIN------
                    |
                    ↓
              ANALYTICAL SQL
                    |
        -----------------------
        |          |          |
      Sales      Profit     Trends
        |          |          |
        -----------------------
                    |
                    ↓
              BI DASHBOARD
                    |
                    ↓
           BUSINESS DECISIONS
```

## The core idea

> **Database design determines how data is stored.**

> **OLTP databases handle day-to-day transactions.**

> **Data warehouses store integrated historical data for analysis.**

> **Fact tables store measurable events.**

> **Dimension tables provide context.**

> **ETL/ELT moves and transforms data.**

> **SQL extracts, transforms, aggregates, and analyzes the warehouse data.**

> **BI tools turn the analytical results into dashboards and business insights.**
