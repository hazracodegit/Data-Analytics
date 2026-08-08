# 📊 SQL for Data Analytics — Beginner to Advanced

A complete practical guide to using SQL for **data manipulation, preprocessing, data analysis, business analytics, sales analytics, customer analytics, time-series analysis, cohort analysis, and funnel analysis**.

---

# 📚 Table of Contents

1. [SQL for Data Analytics](#1-sql-for-data-analytics)
2. [Analytics Database Structure](#2-analytics-database-structure)
3. [Data Manipulation](#3-data-manipulation)
4. [Filtering Data](#4-filtering-data)
5. [Sorting Data](#5-sorting-data)
6. [Limiting Data](#6-limiting-data)
7. [Calculated Columns](#7-calculated-columns)
8. [CASE Statements](#8-case-statements)
9. [NULL Handling](#9-null-handling)
10. [String Manipulation](#10-string-manipulation)
11. [Date Manipulation](#11-date-manipulation)
12. [Data Aggregation](#12-data-aggregation)
13. [GROUP BY](#13-group-by)
14. [HAVING](#14-having)
15. [Joins for Analytics](#15-joins-for-analytics)
16. [Subqueries for Analytics](#16-subqueries-for-analytics)
17. [CTEs for Analytics](#17-ctes-for-analytics)
18. [SQL for Data Preprocessing](#18-sql-for-data-preprocessing)
19. [Data Cleaning](#19-data-cleaning)
20. [Data Transformation](#20-data-transformation)
21. [Data Validation](#21-data-validation)
22. [SQL Data Analysis](#22-sql-data-analysis)
23. [Descriptive Analytics](#23-descriptive-analytics)
24. [Comparative Analysis](#24-comparative-analysis)
25. [Percentage Analysis](#25-percentage-analysis)
26. [Ranking Analysis](#26-ranking-analysis)
27. [Business Analytics](#27-business-analytics)
28. [KPI Analysis](#28-kpi-analysis)
29. [Sales Analytics](#29-sales-analytics)
30. [Product Analytics](#30-product-analytics)
31. [Customer Analytics](#31-customer-analytics)
32. [Customer Segmentation](#32-customer-segmentation)
33. [RFM Analysis](#33-rfm-analysis)
34. [Customer Retention](#34-customer-retention)
35. [Time-Series Analysis](#35-time-series-analysis)
36. [Daily/Weekly/Monthly Analysis](#36-dailyweeklymonthly-analysis)
37. [Moving Averages](#37-moving-averages)
38. [Growth Analysis](#38-growth-analysis)
39. [Year-over-Year Analysis](#39-year-over-year-analysis)
40. [Month-over-Month Analysis](#40-month-over-month-analysis)
41. [Running Totals](#41-running-totals)
42. [Cohort Analysis](#42-cohort-analysis)
43. [Cohort Retention](#43-cohort-retention)
44. [Funnel Analysis](#44-funnel-analysis)
45. [Conversion Rates](#45-conversion-rates)
46. [Advanced Analytics](#46-advanced-analytics)
47. [Window Functions](#47-window-functions)
48. [Advanced Window Analysis](#48-advanced-window-analysis)
49. [Conditional Aggregation](#49-conditional-aggregation)
50. [Percentiles](#50-percentiles)
51. [Statistical SQL](#51-statistical-sql)
52. [Advanced Business Metrics](#52-advanced-business-metrics)
53. [Building Analytics Queries](#53-building-analytics-queries)
54. [Complete Analytics Example](#54-complete-analytics-example)
55. [SQL Analytics Best Practices](#55-sql-analytics-best-practices)
56. [Analytics Cheat Sheet](#56-analytics-cheat-sheet)

---

# 1. SQL for Data Analytics

## What is SQL Analytics?

SQL analytics means using SQL to:

* retrieve data
* clean data
* transform data
* combine datasets
* aggregate data
* calculate metrics
* identify trends
* compare groups
* analyze customers
* analyze sales
* analyze products
* analyze business performance

The overall process:

```text
Raw Data
   ↓
Data Extraction
   ↓
Data Cleaning
   ↓
Data Preprocessing
   ↓
Data Manipulation
   ↓
Data Analysis
   ↓
Business Metrics
   ↓
Insights
   ↓
Decision Making
```

---

# 2. Analytics Database Structure

A typical e-commerce analytics database may contain:

```text
customers
---------
customer_id
name
email
city
signup_date


orders
------
order_id
customer_id
order_date
status
total_amount


order_items
-----------
order_id
product_id
quantity
unit_price


products
--------
product_id
product_name
category
price


events
------
user_id
event_name
event_time
```

Relationships:

```text
customers
    |
    | customer_id
    ↓
orders
    |
    | order_id
    ↓
order_items
    |
    | product_id
    ↓
products
```

---

# 3. Data Manipulation

Data manipulation means changing or transforming data into a form useful for analysis.

Common operations:

```text
SELECT
WHERE
CASE
JOIN
GROUP BY
ORDER BY
DISTINCT
Aggregation
Date manipulation
String manipulation
Window functions
```

---

## SELECT

```sql
SELECT *
FROM customers;
```

Select specific columns:

```sql
SELECT
    customer_id,
    name,
    city
FROM customers;
```

---

# 4. Filtering Data

Use `WHERE`.

```sql
SELECT *
FROM orders
WHERE total_amount > 1000;
```

Multiple conditions:

```sql
SELECT *
FROM orders
WHERE total_amount > 1000
  AND status = 'Completed';
```

Using `OR`:

```sql
SELECT *
FROM customers
WHERE city = 'Hyderabad'
   OR city = 'Bangalore';
```

Using `IN`:

```sql
SELECT *
FROM customers
WHERE city IN ('Hyderabad', 'Bangalore', 'Chennai');
```

Using `BETWEEN`:

```sql
SELECT *
FROM orders
WHERE total_amount BETWEEN 1000 AND 5000;
```

Using pattern matching:

```sql
SELECT *
FROM customers
WHERE name LIKE 'A%';
```

---

# 5. Sorting Data

```sql
SELECT *
FROM orders
ORDER BY total_amount DESC;
```

Multiple columns:

```sql
SELECT *
FROM customers
ORDER BY city ASC, name ASC;
```

---

# 6. Limiting Data

```sql
SELECT *
FROM orders
ORDER BY total_amount DESC
LIMIT 10;
```

This returns the top 10 orders.

---

# 7. Calculated Columns

You can create calculations directly inside SQL.

```sql
SELECT
    product_id,
    quantity,
    unit_price,
    quantity * unit_price AS revenue
FROM order_items;
```

---

## Profit

```sql
SELECT
    selling_price,
    cost_price,
    selling_price - cost_price AS profit
FROM products;
```

---

## Profit Margin

```sql
SELECT
    product_id,
    (selling_price - cost_price)
        / NULLIF(selling_price, 0) * 100 AS profit_margin
FROM products;
```

---

# 8. CASE Statements

`CASE` allows conditional logic.

```sql
SELECT
    order_id,
    total_amount,
    CASE
        WHEN total_amount >= 10000 THEN 'High'
        WHEN total_amount >= 5000 THEN 'Medium'
        ELSE 'Low'
    END AS order_category
FROM orders;
```

---

## Business segmentation

```sql
SELECT
    customer_id,
    total_spend,
    CASE
        WHEN total_spend >= 100000 THEN 'Premium'
        WHEN total_spend >= 50000 THEN 'High Value'
        WHEN total_spend >= 10000 THEN 'Medium Value'
        ELSE 'Low Value'
    END AS customer_segment
FROM customer_summary;
```

---

# 9. NULL Handling

Find missing values:

```sql
SELECT *
FROM customers
WHERE email IS NULL;
```

Replace NULL:

```sql
SELECT
    customer_id,
    COALESCE(city, 'Unknown') AS city
FROM customers;
```

Avoid division by zero:

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS revenue_per_unit
FROM sales;
```

---

# 10. String Manipulation

Common functions:

```text
TRIM()
UPPER()
LOWER()
REPLACE()
SUBSTRING()
LEFT()
RIGHT()
LENGTH()
CONCAT()
```

Example:

```sql
SELECT
    customer_id,
    UPPER(TRIM(name)) AS cleaned_name
FROM customers;
```

---

## Extract email domain

```sql
SELECT
    email,
    SUBSTRING(email FROM POSITION('@' IN email) + 1) AS domain
FROM customers;
```

Exact syntax varies by database.

---

# 11. Date Manipulation

Dates are extremely important in analytics.

Common operations:

```text
Extract year
Extract month
Extract day
Date difference
Date addition
Date truncation
Date filtering
```

---

## Extract year

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year
FROM orders;
```

---

## Extract month

```sql
SELECT
    EXTRACT(MONTH FROM order_date) AS month
FROM orders;
```

---

## Date difference

Database syntax varies.

Example:

```sql
SELECT
    order_date,
    CURRENT_DATE - order_date AS days_since_order
FROM orders;
```

---

# 12. Data Aggregation

Aggregate functions summarize data.

Important functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

## Total sales

```sql
SELECT
    SUM(total_amount) AS total_sales
FROM orders;
```

## Average order value

```sql
SELECT
    AVG(total_amount) AS average_order_value
FROM orders;
```

## Number of orders

```sql
SELECT
    COUNT(*) AS total_orders
FROM orders;
```

---

# 13. GROUP BY

`GROUP BY` creates summaries for groups.

## Sales by city

```sql
SELECT
    city,
    SUM(total_amount) AS total_sales
FROM orders
GROUP BY city;
```

---

## Sales by category

```sql
SELECT
    category,
    SUM(revenue) AS revenue
FROM sales
GROUP BY category;
```

---

# 14. HAVING

`HAVING` filters aggregated groups.

```sql
SELECT
    customer_id,
    SUM(total_amount) AS total_spend
FROM orders
GROUP BY customer_id
HAVING SUM(total_amount) > 50000;
```

Difference:

```text
WHERE
→ filters rows before grouping

HAVING
→ filters groups after aggregation
```

---

# 15. Joins for Analytics

Joins are essential for analytics.

## INNER JOIN

Returns matching records.

```sql
SELECT
    o.order_id,
    c.customer_id,
    c.name,
    o.total_amount
FROM orders o
INNER JOIN customers c
    ON o.customer_id = c.customer_id;
```

---

## LEFT JOIN

Keeps all records from the left table.

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

This is extremely useful for finding customers who have never purchased.

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

---

# 16. Subqueries for Analytics

A subquery is a query inside another query.

Example:

```sql
SELECT *
FROM orders
WHERE total_amount >
(
    SELECT AVG(total_amount)
    FROM orders
);
```

This finds orders above the average order value.

---

# 17. CTEs for Analytics

CTEs make complex analytical queries easier to understand.

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(total_amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)

SELECT *
FROM customer_sales
WHERE total_sales > 50000;
```

Multiple CTEs:

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(total_amount) AS revenue
    FROM orders
    GROUP BY customer_id
),

customer_orders AS (
    SELECT
        customer_id,
        COUNT(*) AS orders
    FROM orders
    GROUP BY customer_id
)

SELECT
    s.customer_id,
    s.revenue,
    o.orders
FROM customer_sales s
JOIN customer_orders o
    ON s.customer_id = o.customer_id;
```

---

# 18. SQL for Data Preprocessing

Data preprocessing means preparing data before analysis or modeling.

It may include:

```text
Cleaning
Transformation
Integration
Encoding
Feature creation
Filtering
Aggregation
Normalization
Standardization
```

---

# 19. Data Cleaning

## Remove whitespace

```sql
SELECT
    TRIM(name) AS name
FROM customers;
```

## Standardize case

```sql
SELECT
    LOWER(email) AS email
FROM customers;
```

## Handle missing values

```sql
SELECT
    COALESCE(city, 'Unknown') AS city
FROM customers;
```

## Remove duplicate records

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY updated_at DESC
        ) AS rn
    FROM customers
)

SELECT *
FROM ranked
WHERE rn = 1;
```

---

# 20. Data Transformation

Transformation means converting data into a more useful representation.

Example:

```sql
SELECT
    quantity * unit_price AS revenue,
    quantity * (unit_price - cost_price) AS profit
FROM order_items;
```

---

## Categorization

```sql
SELECT
    customer_id,
    CASE
        WHEN age < 25 THEN 'Young'
        WHEN age < 40 THEN 'Adult'
        WHEN age < 60 THEN 'Middle Age'
        ELSE 'Senior'
    END AS age_group
FROM customers;
```

---

# 21. Data Validation

Check invalid values.

```sql
SELECT *
FROM customers
WHERE age < 0
   OR age > 120;
```

Check negative sales:

```sql
SELECT *
FROM sales
WHERE revenue < 0;
```

Check invalid categories:

```sql
SELECT DISTINCT status
FROM orders
WHERE status NOT IN (
    'Pending',
    'Completed',
    'Cancelled'
);
```

---

# 22. SQL Data Analysis

SQL data analysis means using SQL to answer questions such as:

```text
What happened?
How much happened?
Where did it happen?
When did it happen?
Who contributed?
Which product performed best?
Which customers are valuable?
Why might performance have changed?
```

---

# 23. Descriptive Analytics

Descriptive analytics answers:

> What happened?

Examples:

```sql
SELECT
    COUNT(*) AS total_orders,
    SUM(total_amount) AS total_revenue,
    AVG(total_amount) AS avg_order_value,
    MIN(total_amount) AS minimum_order,
    MAX(total_amount) AS maximum_order
FROM orders;
```

---

# 24. Comparative Analysis

Compare two groups.

```sql
SELECT
    status,
    COUNT(*) AS orders,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY status;
```

---

## Compare cities

```sql
SELECT
    city,
    COUNT(*) AS customers,
    AVG(total_spend) AS avg_spend
FROM customers
GROUP BY city
ORDER BY avg_spend DESC;
```

---

# 25. Percentage Analysis

Suppose we want each category's percentage of total sales.

```sql
SELECT
    category,
    SUM(revenue) AS category_revenue,
    SUM(revenue) * 100.0
        / SUM(SUM(revenue)) OVER () AS revenue_percentage
FROM sales
GROUP BY category;
```

Concept:

```text
Category Revenue
----------------------- × 100
Total Revenue
```

---

# 26. Ranking Analysis

Use `RANK()`.

```sql
SELECT
    product_id,
    revenue,
    RANK() OVER (
        ORDER BY revenue DESC
    ) AS revenue_rank
FROM product_sales;
```

---

## Top products

```sql
WITH ranked AS (
    SELECT
        product_id,
        revenue,
        RANK() OVER (
            ORDER BY revenue DESC
        ) AS rank
    FROM product_sales
)

SELECT *
FROM ranked
WHERE rank <= 10;
```

---

# 27. Business Analytics

Business analytics uses data to understand business performance and support decisions.

Typical questions:

```text
How much revenue did we generate?
Which region performs best?
Which product generates the most profit?
Who are our most valuable customers?
Are sales growing?
What is our retention rate?
What is our conversion rate?
```

---

# 28. KPI Analysis

Common business KPIs:

```text
Revenue
Profit
Profit Margin
Orders
Customers
Average Order Value
Conversion Rate
Retention Rate
Churn Rate
Customer Lifetime Value
```

---

## Revenue

```sql
SELECT
    SUM(total_amount) AS revenue
FROM orders;
```

---

## AOV

Average Order Value:

```text
AOV = Total Revenue / Number of Orders
```

```sql
SELECT
    SUM(total_amount) / NULLIF(COUNT(*), 0) AS AOV
FROM orders;
```

---

# 29. Sales Analytics

Sales analytics focuses on:

```text
Revenue
Orders
Products
Customers
Regions
Salespeople
Channels
Profit
Growth
```

---

## Total sales

```sql
SELECT
    SUM(total_amount) AS total_sales
FROM orders;
```

---

## Sales by month

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;
```

`DATE_TRUNC()` syntax varies by database.

---

## Sales by product

```sql
SELECT
    p.product_name,
    SUM(oi.quantity * oi.unit_price) AS revenue
FROM order_items oi
JOIN products p
    ON oi.product_id = p.product_id
GROUP BY p.product_name
ORDER BY revenue DESC;
```

---

# 30. Product Analytics

Questions:

```text
Which products sell the most?
Which products generate the most revenue?
Which products have the highest margin?
Which products are declining?
```

---

## Top products by quantity

```sql
SELECT
    product_id,
    SUM(quantity) AS units_sold
FROM order_items
GROUP BY product_id
ORDER BY units_sold DESC;
```

---

## Top products by revenue

```sql
SELECT
    product_id,
    SUM(quantity * unit_price) AS revenue
FROM order_items
GROUP BY product_id
ORDER BY revenue DESC;
```

---

# 31. Customer Analytics

Customer analytics studies customer behavior.

Important metrics:

```text
Total Customers
Active Customers
New Customers
Repeat Customers
Customer Spend
Orders per Customer
Average Customer Value
Retention
Churn
CLV
```

---

## Total customers

```sql
SELECT
    COUNT(DISTINCT customer_id) AS total_customers
FROM customers;
```

---

## Active customers

```sql
SELECT
    COUNT(DISTINCT customer_id) AS active_customers
FROM orders
WHERE order_date >= CURRENT_DATE - INTERVAL '30 days';
```

---

# 32. Customer Segmentation

Segmentation divides customers into meaningful groups.

Example:

```sql
SELECT
    customer_id,
    total_spend,
    CASE
        WHEN total_spend >= 100000 THEN 'Premium'
        WHEN total_spend >= 50000 THEN 'High Value'
        WHEN total_spend >= 10000 THEN 'Medium Value'
        ELSE 'Low Value'
    END AS segment
FROM customer_summary;
```

---

# 33. RFM Analysis

RFM stands for:

```text
R = Recency
F = Frequency
M = Monetary
```

### Recency

How recently did the customer purchase?

### Frequency

How often did the customer purchase?

### Monetary

How much did the customer spend?

---

## Calculate RFM

```sql
SELECT
    customer_id,

    MAX(order_date) AS last_purchase,

    COUNT(DISTINCT order_id) AS frequency,

    SUM(total_amount) AS monetary

FROM orders
GROUP BY customer_id;
```

---

## Recency

```sql
SELECT
    customer_id,
    CURRENT_DATE - MAX(order_date) AS recency
FROM orders
GROUP BY customer_id;
```

Exact date-difference syntax varies by database.

---

# 34. Customer Retention

Retention measures how many customers continue using a product/service after an initial period.

Basic idea:

```text
Customers retained
------------------ × 100
Customers at beginning
```

Example:

```sql
SELECT
    COUNT(DISTINCT customer_id) AS retained_customers
FROM orders
WHERE order_date >= DATE '2026-01-01'
  AND order_date < DATE '2026-02-01';
```

Retention analysis becomes more meaningful when customers are grouped by signup or first-purchase cohort.

---

# 35. Time-Series Analysis

Time-series analysis studies data over time.

Examples:

```text
Daily sales
Weekly sales
Monthly revenue
Yearly growth
Daily active users
Monthly customers
Moving averages
Trends
Seasonality
```

---

# 36. Daily/Weekly/Monthly Analysis

## Daily revenue

```sql
SELECT
    DATE(order_date) AS day,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY DATE(order_date)
ORDER BY day;
```

---

## Monthly revenue

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;
```

---

## Yearly revenue

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY EXTRACT(YEAR FROM order_date)
ORDER BY year;
```

---

# 37. Moving Averages

Moving averages smooth short-term fluctuations.

Example: 7-day moving average.

```sql
WITH daily_sales AS (
    SELECT
        DATE(order_date) AS day,
        SUM(total_amount) AS revenue
    FROM orders
    GROUP BY DATE(order_date)
)

SELECT
    day,
    revenue,

    AVG(revenue) OVER (
        ORDER BY day
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS moving_avg_7_day

FROM daily_sales
ORDER BY day;
```

---

# 38. Growth Analysis

Growth measures how a metric changes over time.

```text
Growth %
=
(Current - Previous)
-------------------- × 100
Previous
```

---

# 39. Year-over-Year Analysis

YoY compares the same period across years.

```sql
WITH yearly_sales AS (
    SELECT
        EXTRACT(YEAR FROM order_date) AS year,
        SUM(total_amount) AS revenue
    FROM orders
    GROUP BY EXTRACT(YEAR FROM order_date)
)

SELECT
    year,
    revenue,

    LAG(revenue) OVER (
        ORDER BY year
    ) AS previous_year_revenue,

    (
        revenue -
        LAG(revenue) OVER (ORDER BY year)
    )
    / NULLIF(
        LAG(revenue) OVER (ORDER BY year),
        0
    ) * 100 AS yoy_growth

FROM yearly_sales
ORDER BY year;
```

---

# 40. Month-over-Month Analysis

MoM compares one month with the previous month.

```sql
WITH monthly_sales AS (
    SELECT
        DATE_TRUNC('month', order_date) AS month,
        SUM(total_amount) AS revenue
    FROM orders
    GROUP BY DATE_TRUNC('month', order_date)
)

SELECT
    month,
    revenue,

    LAG(revenue) OVER (
        ORDER BY month
    ) AS previous_month,

    (
        revenue -
        LAG(revenue) OVER (ORDER BY month)
    )
    / NULLIF(
        LAG(revenue) OVER (ORDER BY month),
        0
    ) * 100 AS mom_growth

FROM monthly_sales;
```

---

# 41. Running Totals

A running total accumulates values over time.

```sql
SELECT
    order_date,
    total_amount,

    SUM(total_amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS cumulative_sales

FROM orders;
```

---

# 42. Cohort Analysis

Cohort analysis groups users based on a common starting event.

Common cohort definitions:

```text
Signup month
First purchase month
First app usage month
Subscription start month
```

Example:

```text
January customers → January cohort
February customers → February cohort
March customers → March cohort
```

---

# 43. Cohort Retention

Suppose:

```text
Customer signup
       ↓
First purchase
       ↓
Month 1
       ↓
Month 2
       ↓
Month 3
```

We can determine when each customer first purchased.

```sql
WITH first_purchase AS (
    SELECT
        customer_id,
        DATE_TRUNC(
            'month',
            MIN(order_date)
        ) AS cohort_month
    FROM orders
    GROUP BY customer_id
)

SELECT *
FROM first_purchase;
```

---

## Customer activity month

```sql
WITH first_purchase AS (
    SELECT
        customer_id,
        DATE_TRUNC(
            'month',
            MIN(order_date)
        ) AS cohort_month
    FROM orders
    GROUP BY customer_id
),

activity AS (
    SELECT DISTINCT
        customer_id,
        DATE_TRUNC(
            'month',
            order_date
        ) AS activity_month
    FROM orders
)

SELECT
    f.cohort_month,
    a.activity_month,
    COUNT(DISTINCT a.customer_id) AS active_customers
FROM first_purchase f
JOIN activity a
    ON f.customer_id = a.customer_id
GROUP BY
    f.cohort_month,
    a.activity_month
ORDER BY
    f.cohort_month,
    a.activity_month;
```

---

## Cohort month number

Conceptually:

```text
Month 0 → acquisition month
Month 1 → one month after acquisition
Month 2 → two months after acquisition
...
```

Depending on your SQL database, use the appropriate month-difference function.

---

## Retention rate

```text
Retention Rate
=
Customers active in period
-------------------------- × 100
Customers in original cohort
```

Example:

```sql
SELECT
    cohort_month,
    activity_month,
    active_customers,
    active_customers * 100.0
        / FIRST_VALUE(active_customers) OVER (
            PARTITION BY cohort_month
            ORDER BY activity_month
        ) AS retention_rate
FROM cohort_activity;
```

---

# 44. Funnel Analysis

Funnel analysis tracks users through sequential stages.

Example:

```text
Website Visit
      ↓
Product View
      ↓
Add to Cart
      ↓
Checkout
      ↓
Purchase
```

---

# 45. Conversion Rates

Suppose:

```text
1000 visitors
 ↓
500 product views
 ↓
200 add to carts
 ↓
100 purchases
```

Conversion:

```text
Visit → Product View
500 / 1000 × 100 = 50%

Product View → Cart
200 / 500 × 100 = 40%

Cart → Purchase
100 / 200 × 100 = 50%

Overall
100 / 1000 × 100 = 10%
```

---

## Funnel using conditional aggregation

```sql
SELECT
    COUNT(DISTINCT CASE
        WHEN event_name = 'visit'
        THEN user_id
    END) AS visitors,

    COUNT(DISTINCT CASE
        WHEN event_name = 'product_view'
        THEN user_id
    END) AS product_viewers,

    COUNT(DISTINCT CASE
        WHEN event_name = 'add_to_cart'
        THEN user_id
    END) AS cart_users,

    COUNT(DISTINCT CASE
        WHEN event_name = 'purchase'
        THEN user_id
    END) AS purchasers

FROM events;
```

---

## Calculate funnel conversion

```sql
WITH funnel AS (
    SELECT
        COUNT(DISTINCT CASE
            WHEN event_name = 'visit'
            THEN user_id
        END) AS visitors,

        COUNT(DISTINCT CASE
            WHEN event_name = 'product_view'
            THEN user_id
        END) AS viewers,

        COUNT(DISTINCT CASE
            WHEN event_name = 'add_to_cart'
            THEN user_id
        END) AS carts,

        COUNT(DISTINCT CASE
            WHEN event_name = 'purchase'
            THEN user_id
        END) AS purchases

    FROM events
)

SELECT
    visitors,
    viewers,
    carts,
    purchases,

    viewers * 100.0
        / NULLIF(visitors, 0) AS visit_to_view,

    carts * 100.0
        / NULLIF(viewers, 0) AS view_to_cart,

    purchases * 100.0
        / NULLIF(carts, 0) AS cart_to_purchase,

    purchases * 100.0
        / NULLIF(visitors, 0) AS overall_conversion

FROM funnel;
```

---

# 46. Advanced Analytics

Once you understand:

```text
SELECT
WHERE
GROUP BY
JOIN
CASE
Aggregation
CTE
Window Functions
```

you can build advanced analytical queries.

Advanced SQL analytics includes:

```text
Window functions
Ranking
Running totals
Moving averages
Percentiles
Cohort analysis
Funnel analysis
Retention
RFM
Growth analysis
Segmentation
Statistical analysis
```

---

# 47. Window Functions

Window functions perform calculations across related rows without collapsing them.

General structure:

```sql
FUNCTION() OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

---

## ROW_NUMBER

```sql
SELECT
    customer_id,
    order_id,
    order_date,

    ROW_NUMBER() OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS order_number

FROM orders;
```

Result:

```text
customer  order  order_number
1         101    1
1         102    2
1         103    3
2         104    1
2         105    2
```

---

# 48. Advanced Window Analysis

## RANK

```sql
SELECT
    product_id,
    revenue,
    RANK() OVER (
        ORDER BY revenue DESC
    ) AS rank
FROM product_sales;
```

## DENSE_RANK

```sql
SELECT
    product_id,
    revenue,
    DENSE_RANK() OVER (
        ORDER BY revenue DESC
    ) AS rank
FROM product_sales;
```

Difference:

```text
RANK:
1
2
2
4

DENSE_RANK:
1
2
2
3
```

---

## LAG

Access previous row.

```sql
SELECT
    month,
    revenue,
    LAG(revenue) OVER (
        ORDER BY month
    ) AS previous_revenue
FROM monthly_sales;
```

---

## LEAD

Access next row.

```sql
SELECT
    month,
    revenue,
    LEAD(revenue) OVER (
        ORDER BY month
    ) AS next_revenue
FROM monthly_sales;
```

---

## FIRST_VALUE

```sql
SELECT
    customer_id,
    order_date,
    FIRST_VALUE(order_date) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS first_order
FROM orders;
```

---

## LAST_VALUE

Window-frame details matter for `LAST_VALUE()`. A suitable explicit frame is often required.

```sql
SELECT
    customer_id,
    order_date,
    LAST_VALUE(order_date) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS last_order
FROM orders;
```

---

# 49. Conditional Aggregation

Conditional aggregation is one of the most important SQL analytics techniques.

```sql
SELECT
    COUNT(*) AS total_orders,

    COUNT(
        CASE
            WHEN status = 'Completed'
            THEN 1
        END
    ) AS completed_orders,

    COUNT(
        CASE
            WHEN status = 'Cancelled'
            THEN 1
        END
    ) AS cancelled_orders

FROM orders;
```

---

## Revenue by condition

```sql
SELECT
    SUM(
        CASE
            WHEN category = 'Electronics'
            THEN revenue
            ELSE 0
        END
    ) AS electronics_revenue,

    SUM(
        CASE
            WHEN category = 'Clothing'
            THEN revenue
            ELSE 0
        END
    ) AS clothing_revenue

FROM sales;
```

---

# 50. Percentiles

Percentiles help understand distributions.

Important concepts:

```text
P25 = 25th percentile
P50 = Median
P75 = 75th percentile
P90 = 90th percentile
P95 = 95th percentile
P99 = 99th percentile
```

Example:

```sql
SELECT
    PERCENTILE_CONT(0.50)
    WITHIN GROUP (
        ORDER BY total_amount
    ) AS median_order_value
FROM orders;
```

Function support varies between SQL databases.

---

# 51. Statistical SQL

SQL can perform basic statistical analysis.

## Mean

```sql
SELECT
    AVG(total_amount) AS mean_order_value
FROM orders;
```

## Minimum

```sql
SELECT
    MIN(total_amount)
FROM orders;
```

## Maximum

```sql
SELECT
    MAX(total_amount)
FROM orders;
```

## Standard deviation

```sql
SELECT
    STDDEV(total_amount) AS standard_deviation
FROM orders;
```

The exact function may be `STDDEV`, `STDDEV_SAMP`, or another database-specific equivalent.

---

# 52. Advanced Business Metrics

## Average Order Value

```text
AOV = Revenue / Orders
```

```sql
SELECT
    SUM(total_amount)
        / NULLIF(COUNT(DISTINCT order_id), 0)
        AS AOV
FROM orders;
```

---

## Customer Average Spend

```sql
SELECT
    SUM(total_amount)
        / NULLIF(COUNT(DISTINCT customer_id), 0)
        AS avg_customer_spend
FROM orders;
```

---

## Purchase Frequency

```sql
SELECT
    customer_id,
    COUNT(DISTINCT order_id) AS purchase_frequency
FROM orders
GROUP BY customer_id;
```

---

## Customer Lifetime Revenue

```sql
SELECT
    customer_id,
    SUM(total_amount) AS lifetime_revenue
FROM orders
GROUP BY customer_id;
```

---

## Repeat Customer Rate

Concept:

```text
Repeat Customers
----------------- × 100
Total Customers
```

SQL:

```sql
WITH customer_orders AS (
    SELECT
        customer_id,
        COUNT(DISTINCT order_id) AS order_count
    FROM orders
    GROUP BY customer_id
)

SELECT
    COUNT(
        CASE
            WHEN order_count > 1
            THEN 1
        END
    ) * 100.0
    / COUNT(*) AS repeat_customer_rate
FROM customer_orders;
```

---

# 53. Building Analytics Queries

A strong analytics query usually follows this thought process:

```text
1. Define the business question
        ↓
2. Identify required tables
        ↓
3. Identify relationships
        ↓
4. Determine required filters
        ↓
5. Clean / preprocess
        ↓
6. Join tables
        ↓
7. Calculate metrics
        ↓
8. Aggregate
        ↓
9. Compare / rank
        ↓
10. Validate result
```

---

# 54. Complete Analytics Example

## Business Question

> Which customers generated the highest revenue in each city during the current year?

---

## Step 1 — Join customers and orders

```sql
SELECT
    c.customer_id,
    c.name,
    c.city,
    o.total_amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

## Step 2 — Filter current year

```sql
SELECT
    c.customer_id,
    c.name,
    c.city,
    o.total_amount
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE EXTRACT(YEAR FROM o.order_date)
      = EXTRACT(YEAR FROM CURRENT_DATE);
```

---

## Step 3 — Aggregate customer revenue

```sql
WITH customer_sales AS (
    SELECT
        c.customer_id,
        c.name,
        c.city,
        SUM(o.total_amount) AS revenue
    FROM customers c
    JOIN orders o
        ON c.customer_id = o.customer_id
    WHERE EXTRACT(YEAR FROM o.order_date)
          = EXTRACT(YEAR FROM CURRENT_DATE)
    GROUP BY
        c.customer_id,
        c.name,
        c.city
)

SELECT *
FROM customer_sales;
```

---

## Step 4 — Rank customers within each city

```sql
WITH customer_sales AS (
    SELECT
        c.customer_id,
        c.name,
        c.city,
        SUM(o.total_amount) AS revenue
    FROM customers c
    JOIN orders o
        ON c.customer_id = o.customer_id
    WHERE EXTRACT(YEAR FROM o.order_date)
          = EXTRACT(YEAR FROM CURRENT_DATE)
    GROUP BY
        c.customer_id,
        c.name,
        c.city
),

ranked AS (
    SELECT
        *,
        RANK() OVER (
            PARTITION BY city
            ORDER BY revenue DESC
        ) AS city_rank
    FROM customer_sales
)

SELECT *
FROM ranked
WHERE city_rank <= 5
ORDER BY city, city_rank;
```

This combines:

```text
JOIN
WHERE
GROUP BY
SUM
CTE
WINDOW FUNCTION
PARTITION BY
RANK
```

---

# 🔥 Analytics Query Patterns You Must Know

## 1. Top N

```sql
SELECT
    product_id,
    SUM(revenue) AS revenue
FROM sales
GROUP BY product_id
ORDER BY revenue DESC
LIMIT 10;
```

---

## 2. Above Average

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

---

## 3. Percentage of Total

```sql
SELECT
    category,
    SUM(revenue) AS revenue,

    SUM(revenue) * 100.0
        / SUM(SUM(revenue)) OVER () AS percentage

FROM sales
GROUP BY category;
```

---

## 4. Ranking

```sql
SELECT
    product_id,
    revenue,
    RANK() OVER (
        ORDER BY revenue DESC
    ) AS rank
FROM product_sales;
```

---

## 5. Ranking Within Groups

```sql
SELECT
    city,
    customer_id,
    revenue,

    RANK() OVER (
        PARTITION BY city
        ORDER BY revenue DESC
    ) AS city_rank

FROM customer_sales;
```

---

## 6. Previous Period

```sql
SELECT
    month,
    revenue,

    LAG(revenue) OVER (
        ORDER BY month
    ) AS previous_month

FROM monthly_sales;
```

---

## 7. Growth Rate

```sql
SELECT
    month,
    revenue,

    (
        revenue -
        LAG(revenue) OVER (ORDER BY month)
    )
    / NULLIF(
        LAG(revenue) OVER (ORDER BY month),
        0
    ) * 100 AS growth_rate

FROM monthly_sales;
```

---

## 8. Running Total

```sql
SELECT
    month,
    revenue,

    SUM(revenue) OVER (
        ORDER BY month
    ) AS cumulative_revenue

FROM monthly_sales;
```

---

## 9. Moving Average

```sql
SELECT
    day,
    revenue,

    AVG(revenue) OVER (
        ORDER BY day
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS seven_day_average

FROM daily_sales;
```

---

## 10. Customer First Purchase

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_purchase
FROM orders
GROUP BY customer_id;
```

---

## 11. Customer Last Purchase

```sql
SELECT
    customer_id,
    MAX(order_date) AS last_purchase
FROM orders
GROUP BY customer_id;
```

---

## 12. Customers With No Orders

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

---

## 13. Repeat Customers

```sql
SELECT
    customer_id
FROM orders
GROUP BY customer_id
HAVING COUNT(DISTINCT order_id) > 1;
```

---

## 14. Revenue by Month

```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(total_amount) AS revenue
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;
```

---

## 15. Revenue by Customer

```sql
SELECT
    customer_id,
    SUM(total_amount) AS lifetime_revenue
FROM orders
GROUP BY customer_id
ORDER BY lifetime_revenue DESC;
```

---

# 🧠 Difference Between Major Analytics Concepts

| Concept              | Main Purpose                            |
| -------------------- | --------------------------------------- |
| Data Cleaning        | Fix incorrect/missing/duplicate data    |
| Data Preprocessing   | Prepare data for analysis/modeling      |
| Data Manipulation    | Transform and organize data             |
| Data Analysis        | Discover patterns and answer questions  |
| Business Analytics   | Use analysis to solve business problems |
| Sales Analytics      | Analyze sales and revenue               |
| Customer Analytics   | Analyze customer behavior               |
| Time-Series Analysis | Analyze changes over time               |
| Cohort Analysis      | Analyze groups sharing a starting event |
| Funnel Analysis      | Analyze sequential conversion stages    |

---

# 🎯 What to Learn in Order

## Beginner

```text
SELECT
WHERE
DISTINCT
ORDER BY
LIMIT
Aliases
Arithmetic
CASE
NULL
COALESCE
String functions
Date functions
```

---

## Intermediate

```text
GROUP BY
HAVING
Aggregate functions
INNER JOIN
LEFT JOIN
Subqueries
CTEs
Conditional aggregation
Date aggregation
Business KPIs
```

---

## Advanced

```text
Window functions
ROW_NUMBER
RANK
DENSE_RANK
LAG
LEAD
FIRST_VALUE
LAST_VALUE
Running totals
Moving averages
Percentages
Growth analysis
RFM
Retention
Cohort analysis
Funnel analysis
Percentiles
Statistical analysis
```

---

# 🏆 SQL Analytics Skill Map

```text
                         SQL ANALYTICS
                              |
        ┌─────────────────────┼─────────────────────┐
        ↓                     ↓                     ↓
   DATA PREPARATION       DATA MANIPULATION     DATA ANALYSIS
        |                     |                     |
   Cleaning               SELECT                 Aggregation
   NULL handling          WHERE                  KPIs
   Duplicates             JOIN                   Comparison
   Validation             CASE                   Ranking
   Transformation         GROUP BY               Percentages
        |                 CTE                    Trends
        |                     |                     |
        └─────────────────────┼─────────────────────┘
                              ↓
                       BUSINESS ANALYTICS
                              |
          ┌───────────────────┼───────────────────┐
          ↓                   ↓                   ↓
    SALES ANALYTICS    CUSTOMER ANALYTICS   PRODUCT ANALYTICS
          |                   |                   |
       Revenue              RFM                 Revenue
       Orders               Retention            Units
       AOV                  Churn                Margin
       Growth               CLV                  Ranking
          |                   |                   |
          └───────────────────┼───────────────────┘
                              ↓
                      ADVANCED ANALYTICS
                              |
          ┌───────────────────┼───────────────────┐
          ↓                   ↓                   ↓
    TIME SERIES          COHORT ANALYSIS     FUNNEL ANALYSIS
          |                   |                   |
       Trends             Cohorts             Stages
       MoM                Retention            Conversion
       YoY                Cohort age           Drop-off
       Moving avg         LTV                  Rates
       Running total
```

---

# 📝 Final SQL Analytics Checklist

Before considering yourself comfortable with SQL analytics, you should be able to answer:

### Data Manipulation

```text
[ ] Can I filter data?
[ ] Can I sort data?
[ ] Can I create calculated columns?
[ ] Can I use CASE?
[ ] Can I manipulate text?
[ ] Can I manipulate dates?
```

### Data Preprocessing

```text
[ ] Can I handle NULLs?
[ ] Can I remove duplicates?
[ ] Can I standardize categories?
[ ] Can I convert data types?
[ ] Can I validate data?
[ ] Can I create clean analytical datasets?
```

### Data Analysis

```text
[ ] Can I aggregate data?
[ ] Can I use GROUP BY?
[ ] Can I use HAVING?
[ ] Can I calculate percentages?
[ ] Can I compare groups?
[ ] Can I rank records?
```

### Business Analytics

```text
[ ] Can I calculate revenue?
[ ] Can I calculate AOV?
[ ] Can I calculate profit?
[ ] Can I calculate growth?
[ ] Can I identify top products?
[ ] Can I identify top customers?
```

### Customer Analytics

```text
[ ] Can I calculate customer spend?
[ ] Can I calculate purchase frequency?
[ ] Can I identify repeat customers?
[ ] Can I perform RFM analysis?
[ ] Can I calculate retention?
[ ] Can I perform customer segmentation?
```

### Time Series

```text
[ ] Can I calculate daily sales?
[ ] Can I calculate monthly sales?
[ ] Can I calculate MoM growth?
[ ] Can I calculate YoY growth?
[ ] Can I calculate running totals?
[ ] Can I calculate moving averages?
```

### Advanced Analytics

```text
[ ] Can I use ROW_NUMBER?
[ ] Can I use RANK?
[ ] Can I use DENSE_RANK?
[ ] Can I use LAG?
[ ] Can I use LEAD?
[ ] Can I use CTEs?
[ ] Can I perform cohort analysis?
[ ] Can I perform funnel analysis?
[ ] Can I calculate retention?
[ ] Can I calculate conversion rates?
[ ] Can I calculate percentiles?
```

---

# 🚀 Final Mental Model

Remember SQL analytics as:

```text
                    SQL
                     |
              ┌──────┴──────┐
              ↓             ↓
          PREPARE        MANIPULATE
              |             |
          Clean          Filter
          Validate       Join
          Transform      Aggregate
              |             |
              └──────┬──────┘
                     ↓
                  ANALYZE
                     |
        ┌────────────┼────────────┐
        ↓            ↓            ↓
      Trends       KPIs       Comparisons
        |            |            |
        └────────────┼────────────┘
                     ↓
              BUSINESS ANALYTICS
                     |
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
     SALES        CUSTOMER       PRODUCT
       |             |             |
       └─────────────┼─────────────┘
                     ↓
              ADVANCED ANALYTICS
                     |
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
  TIME SERIES      COHORT        FUNNEL
       |             |             |
       ↓             ↓             ↓
    Trends       Retention     Conversion
    Growth       Cohorts       Drop-off
    Moving Avg   LTV           Rates
```

> **The most important progression to master is:**
>
> `SELECT → WHERE → GROUP BY → JOIN → CASE → CTE → Window Functions → Business Metrics → Time Series → Cohort → Funnel → Advanced Analytics`

This progression takes you from **basic SQL querying to real-world data analyst SQL**.
