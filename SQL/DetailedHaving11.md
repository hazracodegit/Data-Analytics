# SQL HAVING — Complete Guide

`HAVING` is used to **filter groups after aggregation**.

It is most commonly used with:

* `GROUP BY`
* Aggregate functions
* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

---

# 1. What is HAVING?

`HAVING` filters the **result of grouped data**.

### Basic syntax

```sql
SELECT
    group_column,
    aggregate_function(column) AS result
FROM table_name
GROUP BY group_column
HAVING aggregate_function(column) condition;
```

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

Meaning:

> Group employees by department and return only departments having more than 5 employees.

---

# 2. Why Do We Need HAVING?

Consider this query:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Suppose the result is:

| department | employee_count |
| ---------- | -------------: |
| IT         |             10 |
| HR         |              4 |
| Finance    |              8 |
| Sales      |             15 |

Now suppose we want only departments having more than 5 employees.

We need:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

Result:

| department | employee_count |
| ---------- | -------------: |
| IT         |             10 |
| Finance    |              8 |
| Sales      |             15 |

---

# 3. Main Purpose of HAVING

The main purpose is:

```text
GROUP BY
    ↓
Create groups
    ↓
Aggregate each group
    ↓
HAVING
    ↓
Filter groups
```

So:

```text
WHERE  → filters rows
HAVING → filters groups
```

---

# 4. WHERE vs HAVING

This is one of the **most important SQL concepts**.

## WHERE

Filters individual rows **before grouping**.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE salary > 50000
GROUP BY department;
```

Here:

```text
salary > 50000
```

is applied to individual employees.

---

## HAVING

Filters groups **after grouping**.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

Here:

```text
COUNT(*) > 5
```

is applied to departments/groups.

---

# 5. Easy Way to Remember

```text
WHERE
↓
Which rows should participate?

GROUP BY
↓
How should those rows be grouped?

HAVING
↓
Which groups should remain?
```

Example:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE age >= 25
GROUP BY department
HAVING AVG(salary) > 60000;
```

Meaning:

```text
1. Select employees age >= 25
2. Group them by department
3. Calculate average salary
4. Keep departments whose average salary > 60000
```

---

# 6. Basic HAVING Syntax

```sql
SELECT
    column_name,
    aggregate_function(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

Example:

```sql
SELECT
    category,
    SUM(sales) AS total_sales
FROM sales
GROUP BY category
HAVING SUM(sales) > 100000;
```

---

# 7. HAVING with COUNT()

One of the most common uses.

### Example

Find departments with more than 10 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

---

# 8. HAVING with COUNT() — Less Than

Find departments with fewer than 5 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) < 5;
```

---

# 9. HAVING with COUNT() — Equal To

Find departments having exactly 5 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) = 5;
```

---

# 10. HAVING with COUNT(DISTINCT)

Very important for data analytics.

Suppose:

```text
customer_id
region
```

We want regions having more than 100 unique customers.

```sql
SELECT
    region,
    COUNT(DISTINCT customer_id) AS customer_count
FROM sales
GROUP BY region
HAVING COUNT(DISTINCT customer_id) > 100;
```

This counts **unique customers**, not rows.

---

# 11. HAVING with SUM()

Find products whose total sales exceed 1,000,000.

```sql
SELECT
    product_id,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY product_id
HAVING SUM(revenue) > 1000000;
```

---

# 12. HAVING with SUM() — Minimum

```sql
SELECT
    category,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY category
HAVING SUM(revenue) >= 50000;
```

Only categories generating at least 50,000 revenue are returned.

---

# 13. HAVING with AVG()

Find departments where average salary is greater than 70,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```

---

# 14. HAVING with AVG() — Range

Find departments whose average salary is between 50,000 and 80,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) BETWEEN 50000 AND 80000;
```

---

# 15. HAVING with MIN()

Find departments where the minimum salary is greater than 30,000.

```sql
SELECT
    department,
    MIN(salary) AS minimum_salary
FROM employees
GROUP BY department
HAVING MIN(salary) > 30000;
```

---

# 16. HAVING with MAX()

Find departments where the highest salary exceeds 150,000.

```sql
SELECT
    department,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department
HAVING MAX(salary) > 150000;
```

---

# 17. HAVING with Multiple Conditions

You can use:

* `AND`
* `OR`
* `NOT`

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 5
   AND AVG(salary) > 60000;
```

Meaning:

```text
employee count > 5
AND
average salary > 60000
```

Both conditions must be true.

---

# 18. HAVING with OR

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 10
    OR AVG(salary) > 80000;
```

A department is returned if **either condition** is true.

---

# 19. HAVING with NOT

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING NOT COUNT(*) < 5;
```

Equivalent logic can often be written more simply as:

```sql
HAVING COUNT(*) >= 5;
```

---

# 20. HAVING with BETWEEN

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) BETWEEN 60000 AND 90000;
```

---

# 21. HAVING with IN

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING department IN ('IT', 'HR', 'Finance');
```

However, if you're simply filtering the underlying rows by department, `WHERE` is generally more appropriate:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE department IN ('IT', 'HR', 'Finance')
GROUP BY department;
```

Use `HAVING` when the filtering condition is genuinely on the **grouped result**.

---

# 22. HAVING with LIKE

Some databases allow conditions on grouped columns in `HAVING`.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING department LIKE 'S%';
```

But if the condition is a row-level filter, prefer:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE department LIKE 'S%'
GROUP BY department;
```

---

# 23. HAVING with Multiple Aggregate Functions

A very common analytics query:

```sql
SELECT
    category,
    COUNT(*) AS order_count,
    SUM(revenue) AS total_revenue,
    AVG(revenue) AS average_order_value
FROM sales
GROUP BY category
HAVING COUNT(*) >= 100
   AND SUM(revenue) > 500000
   AND AVG(revenue) > 5000;
```

This means:

```text
At least 100 orders
AND
Revenue > 500,000
AND
Average order value > 5,000
```

---

# 24. HAVING with WHERE

You can use both.

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
WHERE salary >= 40000
GROUP BY department
HAVING COUNT(*) >= 5;
```

The difference:

```text
WHERE
→ filters employees

GROUP BY
→ creates departments

HAVING
→ filters departments
```

---

# 25. Example of WHERE + HAVING

Suppose we have:

| department | salary |
| ---------- | -----: |
| IT         |  30000 |
| IT         |  60000 |
| IT         |  80000 |
| HR         |  40000 |
| HR         |  70000 |

Query:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE salary >= 50000
GROUP BY department
HAVING COUNT(*) >= 2;
```

First:

```text
WHERE salary >= 50000
```

Remaining:

```text
IT → 60000
IT → 80000
HR → 70000
```

Then:

```text
GROUP BY department
```

Results:

```text
IT → 2
HR → 1
```

Then:

```text
HAVING COUNT(*) >= 2
```

Final:

```text
IT → 2
```

---

# 26. Logical Execution Order

Consider:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE age >= 25
GROUP BY department
HAVING AVG(salary) > 60000
ORDER BY avg_salary DESC;
```

A useful conceptual processing order is:

```text
1. FROM
      ↓
2. WHERE
      ↓
3. GROUP BY
      ↓
4. Aggregate calculations
      ↓
5. HAVING
      ↓
6. SELECT
      ↓
7. ORDER BY
```

Remember:

```text
WHERE → before grouping
HAVING → after grouping
```

---

# 27. Why Can't We Normally Use Aggregate Functions in WHERE?

This is incorrect:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
WHERE AVG(salary) > 60000
GROUP BY department;
```

Why?

Because `WHERE` operates before the grouped aggregate result exists.

Use:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 28. HAVING and GROUP BY

`HAVING` is most commonly associated with `GROUP BY`.

Standard pattern:

```sql
SELECT
    group_column,
    aggregate_function(value)
FROM table_name
GROUP BY group_column
HAVING aggregate_function(value) condition;
```

Example:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 10000;
```

Meaning:

> Find customers whose total spending exceeds 10,000.

---

# 29. HAVING Without GROUP BY

Some SQL databases allow `HAVING` without an explicit `GROUP BY`, treating the entire result as one group.

Example:

```sql
SELECT
    COUNT(*) AS employee_count
FROM employees
HAVING COUNT(*) > 100;
```

This asks:

> Does the entire employees table contain more than 100 rows?

If yes, a row is returned.

If not, no row is returned.

For portability and clarity, use this pattern when appropriate, but remember that exact behavior can vary by database system.

---

# 30. HAVING with a Single Group

Without `GROUP BY`, the aggregate considers the entire table as one group.

```sql
SELECT
    SUM(revenue) AS total_revenue
FROM sales
HAVING SUM(revenue) > 1000000;
```

Conceptually:

```text
Entire sales table
        ↓
One group
        ↓
SUM(revenue)
        ↓
HAVING
        ↓
Keep/discard the result
```

---

# 31. HAVING with JOIN

`HAVING` is heavily used after joins.

Suppose:

```text
customers
---------
customer_id
name

orders
------
order_id
customer_id
amount
```

Find customers whose total spending is greater than 10,000:

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spending
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name
HAVING SUM(o.amount) > 10000;
```

---

# 32. HAVING with LEFT JOIN

Find customers with no orders:

```sql
SELECT
    c.customer_id,
    c.name,
    COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name
HAVING COUNT(o.order_id) = 0;
```

This is a very useful real-world pattern.

---

# 33. HAVING with COUNT(*) vs COUNT(column)

This difference is important.

Consider:

```sql
SELECT
    c.customer_id,
    COUNT(*) AS row_count,
    COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id;
```

For a customer with no matching order:

```text
COUNT(*)          → 1
COUNT(o.order_id) → 0
```

Why?

`COUNT(*)` counts the resulting row created by the `LEFT JOIN`.

`COUNT(o.order_id)` counts only non-NULL order IDs.

Therefore, for finding customers with no orders, this is usually correct:

```sql
HAVING COUNT(o.order_id) = 0;
```

---

# 34. HAVING with DISTINCT

Example:

> Find customers who placed at least 5 different orders.

```sql
SELECT
    customer_id,
    COUNT(DISTINCT order_id) AS order_count
FROM sales
GROUP BY customer_id
HAVING COUNT(DISTINCT order_id) >= 5;
```

Another example:

> Find regions having at least 100 unique customers.

```sql
SELECT
    region,
    COUNT(DISTINCT customer_id) AS customer_count
FROM sales
GROUP BY region
HAVING COUNT(DISTINCT customer_id) >= 100;
```

---

# 35. HAVING with Dates

Find customers who placed orders on at least 3 different dates.

```sql
SELECT
    customer_id,
    COUNT(DISTINCT order_date) AS active_days
FROM orders
GROUP BY customer_id
HAVING COUNT(DISTINCT order_date) >= 3;
```

This is useful for customer engagement analysis.

---

# 36. HAVING for Repeat Customers

Find customers who made more than one order:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

This identifies repeat customers.

---

# 37. HAVING for High-Value Customers

Find customers whose total purchases exceed 50,000:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 50000;
```

---

# 38. HAVING for Product Performance

Find products sold more than 1,000 units:

```sql
SELECT
    product_id,
    SUM(quantity) AS units_sold
FROM sales
GROUP BY product_id
HAVING SUM(quantity) > 1000;
```

---

# 39. HAVING for Category Performance

Find categories generating more than 1 million revenue:

```sql
SELECT
    category,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY category
HAVING SUM(revenue) > 1000000;
```

---

# 40. HAVING for Average Order Value

Find regions where average order value is above 5,000:

```sql
SELECT
    region,
    AVG(order_amount) AS average_order_value
FROM orders
GROUP BY region
HAVING AVG(order_amount) > 5000;
```

---

# 41. HAVING with CASE

You can combine `HAVING` with conditional aggregation.

Example:

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN salary >= 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees

FROM employees

GROUP BY department

HAVING
    SUM(
        CASE
            WHEN salary >= 100000 THEN 1
            ELSE 0
        END
    ) >= 3;
```

Meaning:

> Return departments having at least 3 employees earning 100,000 or more.

---

# 42. HAVING with Multiple Conditional Aggregates

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN salary >= 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count,

    SUM(
        CASE
            WHEN salary < 50000 THEN 1
            ELSE 0
        END
    ) AS low_salary_count

FROM employees

GROUP BY department

HAVING
    SUM(
        CASE
            WHEN salary >= 100000 THEN 1
            ELSE 0
        END
    ) > 2;
```

This is a powerful analytics technique.

---

# 43. HAVING with Subquery

You can compare a group-level aggregate against a value calculated by a subquery.

Example:

> Find departments whose average salary is above the company-wide average.

```sql
SELECT
    department,
    AVG(salary) AS department_avg
FROM employees
GROUP BY department
HAVING AVG(salary) >
(
    SELECT AVG(salary)
    FROM employees
);
```

Conceptually:

```text
Company average salary
        ↓
Subquery
        ↓
Compare with each department average
        ↓
HAVING
        ↓
Keep higher-than-average departments
```

---

# 44. HAVING with CTE

CTEs can make complex queries easier to read.

```sql
WITH department_summary AS (
    SELECT
        department,
        COUNT(*) AS employee_count,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM department_summary
WHERE employee_count > 10
  AND average_salary > 60000;
```

Here, the filtering happens after the CTE has already produced grouped results.

---

# 45. HAVING vs Subquery

These can sometimes solve similar problems.

Using `HAVING`:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Using a subquery/CTE:

```sql
WITH department_summary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM department_summary
WHERE avg_salary > 60000;
```

Both express the idea:

```text
Create department-level results
        ↓
Filter those results
```

---

# 46. HAVING and ORDER BY

You can combine them.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5
ORDER BY employee_count DESC;
```

Processing conceptually:

```text
Rows
 ↓
Groups
 ↓
HAVING
 ↓
Remaining groups
 ↓
ORDER BY
```

---

# 47. HAVING and LIMIT

Find the top 5 departments with more than 10 employees:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 10
ORDER BY employee_count DESC
LIMIT 5;
```

Meaning:

```text
GROUP BY
↓
HAVING > 10
↓
ORDER BY highest count
↓
LIMIT 5
```

---

# 48. Complete SQL Pattern

A very common analytics query structure is:

```sql
SELECT
    group_column,
    COUNT(*) AS row_count,
    SUM(value) AS total_value,
    AVG(value) AS average_value
FROM table_name
WHERE row_condition
GROUP BY group_column
HAVING COUNT(*) > minimum_count
   AND SUM(value) > minimum_total
ORDER BY total_value DESC
LIMIT 10;
```

This pattern is worth memorizing.

---

# 49. Real-World Business Example

Suppose a company wants:

> Find regions with at least 1,000 orders and revenue greater than 10 million.

```sql
SELECT
    region,
    COUNT(*) AS order_count,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY region
HAVING COUNT(*) >= 1000
   AND SUM(revenue) > 10000000
ORDER BY total_revenue DESC;
```

This is a classic business analytics query.

---

# 50. Customer Segmentation Example

Find customers who:

* Have placed at least 5 orders
* Spent more than 50,000

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 5
   AND SUM(amount) > 50000;
```

These customers could be classified as high-value or loyal customers.

---

# 51. Product Analytics Example

Find products that:

* Sold at least 500 units
* Generated more than 100,000 revenue

```sql
SELECT
    product_id,
    SUM(quantity) AS units_sold,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY product_id
HAVING SUM(quantity) >= 500
   AND SUM(revenue) > 100000;
```

---

# 52. Employee Analytics Example

Find departments that:

* Have at least 10 employees
* Average salary is above 60,000

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING COUNT(*) >= 10
   AND AVG(salary) > 60000;
```

---

# 53. Data Analytics Importance of HAVING

`HAVING` is important because analytics often asks questions about **groups**, not individual records.

Examples:

```text
Customers with more than 5 orders
Products selling more than 1,000 units
Regions generating more than $1M
Departments with average salary above $60K
Categories with at least 100 customers
Stores with average sales above target
```

These are all naturally solved using:

```text
GROUP BY + HAVING
```

---

# 54. HAVING in EDA

During exploratory data analysis, you may ask:

```text
Which categories have the most records?
Which customers have multiple purchases?
Which products have high revenue?
Which regions have enough observations?
Which departments have unusually high averages?
```

Typical pattern:

```sql
SELECT
    category,
    COUNT(*) AS record_count
FROM data
GROUP BY category
HAVING COUNT(*) > 100;
```

---

# 55. HAVING and Data Quality

`HAVING` can also help identify suspicious or incomplete groups.

For example:

```sql
SELECT
    customer_id,
    COUNT(*) AS record_count
FROM customer_transactions
GROUP BY customer_id
HAVING COUNT(*) > 1000;
```

This could identify customers with unusually large numbers of transactions for further investigation.

Another example:

```sql
SELECT
    product_id,
    COUNT(*) AS transaction_count
FROM sales
GROUP BY product_id
HAVING COUNT(*) = 0;
```

This particular query would normally return no groups because groups with zero rows don't exist; to find missing products, a `LEFT JOIN` is usually needed.

---

# 56. Important Concept: HAVING Does Not Create Groups

`HAVING` does not group the data.

`GROUP BY` creates groups.

```text
GROUP BY
→ creates groups

HAVING
→ filters those groups
```

Example:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

Here:

```text
GROUP BY department
```

creates groups.

```text
HAVING COUNT(*) > 5
```

removes groups that don't meet the condition.

---

# 57. Important Concept: HAVING Usually Works With Aggregation

The most common pattern is:

```sql
HAVING COUNT(*) > ...
HAVING SUM(...) > ...
HAVING AVG(...) > ...
HAVING MIN(...) > ...
HAVING MAX(...) > ...
```

When you see:

```text
HAVING + aggregate
```

think:

> Filter the summarized groups.

---

# 58. Common Mistake: Using HAVING Instead of WHERE

This may work in some situations:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department
HAVING department = 'IT';
```

But if the intention is to filter rows before grouping, this is usually better:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
WHERE department = 'IT'
GROUP BY department;
```

Why?

Because the filtering is a row-level condition and belongs logically in `WHERE`.

---

# 59. Common Mistake: Using WHERE for Aggregate Conditions

Wrong:

```sql
SELECT
    customer_id,
    SUM(amount)
FROM orders
WHERE SUM(amount) > 10000
GROUP BY customer_id;
```

Correct:

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 10000;
```

---

# 60. Common Mistake: Confusing COUNT(*) and COUNT(column)

Consider:

```sql
HAVING COUNT(*) > 5
```

This counts rows.

But:

```sql
HAVING COUNT(email) > 5
```

counts only rows where `email` is not NULL.

And:

```sql
HAVING COUNT(DISTINCT email) > 5
```

counts unique non-NULL email values.

These three are different.

---

# 61. Common Mistake: Ignoring NULL in Aggregates

Most aggregate functions ignore NULL values.

For example:

```sql
AVG(salary)
```

does not include NULL salaries in the average.

Similarly:

```sql
SUM(salary)
```

ignores NULL salary values.

`COUNT(*)`, however, counts rows regardless of NULL values.

---

# 62. HAVING and NULL

Suppose:

```text
salary
------
50000
60000
NULL
```

Then:

```sql
SELECT
    AVG(salary)
FROM employees;
```

The NULL salary is not included in the average.

Likewise:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

The comparison is based on the aggregate result.

---

# 63. HAVING with Date Grouping

Example:

> Find months where revenue exceeded 1 million.

Database-specific date functions differ, but conceptually:

```sql
SELECT
    year,
    month,
    SUM(revenue) AS monthly_revenue
FROM monthly_sales
GROUP BY
    year,
    month
HAVING SUM(revenue) > 1000000
ORDER BY
    year,
    month;
```

---

# 64. HAVING with Multiple GROUP BY Columns

Example:

```sql
SELECT
    region,
    category,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY
    region,
    category
HAVING SUM(revenue) > 100000;
```

This filters each:

```text
region + category
```

combination.

For example:

```text
North + Electronics
North + Clothing
South + Electronics
South + Clothing
```

Each combination is treated as a separate group.

---

# 65. HAVING and Granularity

Always identify the granularity.

Example:

```sql
GROUP BY customer_id
```

means:

```text
one row = one customer
```

Then:

```sql
HAVING SUM(amount) > 50000
```

means:

```text
keep customers whose total amount > 50000
```

Another:

```sql
GROUP BY region, category
```

means:

```text
one row = one region-category combination
```

Then:

```sql
HAVING SUM(revenue) > 100000
```

means:

```text
keep region-category combinations with revenue > 100000
```

---

# 66. HAVING and Window Functions

`HAVING` and window functions solve different problems.

Example with `GROUP BY`:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

This returns only departments meeting the condition.

A window function keeps employee-level rows:

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Remember:

```text
GROUP BY + HAVING
→ summarize + filter groups

Window function
→ calculate across related rows without collapsing them
```

---

# 67. HAVING vs WHERE — Complete Comparison

| Feature                       | WHERE                  | HAVING                           |
| ----------------------------- | ---------------------- | -------------------------------- |
| Filters                       | Rows                   | Groups                           |
| Applied before grouping       | Yes                    | No                               |
| Applied after grouping        | No                     | Yes                              |
| Commonly used with aggregates | No                     | Yes                              |
| Commonly used with GROUP BY   | Sometimes              | Very often                       |
| Can filter normal columns     | Yes                    | Yes, depending on query/database |
| Can filter aggregate results  | Generally no           | Yes                              |
| Example                       | `WHERE salary > 50000` | `HAVING AVG(salary) > 60000`     |

---

# 68. WHERE + GROUP BY + HAVING

Memorize this pattern:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
WHERE salary >= 40000
GROUP BY department
HAVING COUNT(*) >= 5
   AND AVG(salary) > 60000
ORDER BY average_salary DESC;
```

Interpretation:

```text
WHERE
→ Remove employees earning below 40K

GROUP BY
→ Group remaining employees by department

COUNT / AVG
→ Calculate department metrics

HAVING
→ Keep departments satisfying both conditions

ORDER BY
→ Sort by average salary
```

---

# 69. Interview Question: WHERE or HAVING?

### Question

Find departments having more than 10 employees.

Answer:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

Why?

Because:

```text
COUNT(*) > 10
```

is a condition on the **group**, not on an individual employee.

---

# 70. Interview Question: WHERE or HAVING?

### Question

Find employees whose salary is greater than 50,000 and then count them by department.

Answer:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE salary > 50000
GROUP BY department;
```

Why not `HAVING`?

Because:

```text
salary > 50000
```

is a row-level condition.

---

# 71. Interview Question: Customers with More Than 3 Orders

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 3;
```

---

# 72. Interview Question: Customers Spending More Than 100K

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 100000;
```

---

# 73. Interview Question: Categories with Average Price Above 500

```sql
SELECT
    category,
    AVG(price) AS average_price
FROM products
GROUP BY category
HAVING AVG(price) > 500;
```

---

# 74. Interview Question: Regions with More Than 1,000 Unique Customers

```sql
SELECT
    region,
    COUNT(DISTINCT customer_id) AS customer_count
FROM sales
GROUP BY region
HAVING COUNT(DISTINCT customer_id) > 1000;
```

---

# 75. Interview Question: Departments with High Average Salary

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 75000;
```

---

# 76. Interview Question: Products with High Sales and Revenue

```sql
SELECT
    product_id,
    SUM(quantity) AS units_sold,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY product_id
HAVING SUM(quantity) > 1000
   AND SUM(revenue) > 500000;
```

---

# 77. Performance Consideration

When possible, filter rows using `WHERE` before grouping.

For example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING COUNT(*) > 10;
```

This is logically efficient because inactive employees don't need to participate in the grouping.

Think:

```text
Filter unnecessary rows early
        ↓
Group fewer rows
        ↓
Aggregate
        ↓
Filter groups
```

Database optimizers may rewrite queries internally, but writing the correct predicate in the appropriate clause is important for both clarity and potential performance.

---

# 78. HAVING Best Practices

### 1. Use WHERE for row filtering

```sql
WHERE salary > 50000
```

### 2. Use HAVING for group filtering

```sql
HAVING AVG(salary) > 60000
```

### 3. Always think about granularity

Ask:

> What does one output row represent?

### 4. Use meaningful aliases

```sql
SUM(revenue) AS total_revenue
```

### 5. Be careful with COUNT

Understand:

```text
COUNT(*)
COUNT(column)
COUNT(DISTINCT column)
```

### 6. Check joins before aggregation

A one-to-many join can multiply rows.

### 7. Use ORDER BY when ranking results

```sql
ORDER BY total_revenue DESC
```

---

# 79. Master Pattern

The most important pattern to remember:

```sql
SELECT
    group_column,
    aggregate_function(value_column) AS metric
FROM table_name
WHERE row_condition
GROUP BY group_column
HAVING aggregate_function(value_column) group_condition
ORDER BY metric DESC;
```

Example:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count,
    SUM(amount) AS total_spending
FROM orders
WHERE order_status = 'Completed'
GROUP BY customer_id
HAVING COUNT(*) >= 5
   AND SUM(amount) > 50000
ORDER BY total_spending DESC;
```

Interpretation:

```text
FROM
↓
Get orders

WHERE
↓
Only completed orders

GROUP BY
↓
One group per customer

COUNT + SUM
↓
Calculate customer metrics

HAVING
↓
Keep customers with ≥5 orders
and >50K spending

ORDER BY
↓
Highest spending first
```

---

# 80. Final HAVING Cheat Sheet

```text
HAVING
│
├── Filters GROUPS
│
├── Usually used after GROUP BY
│
├── Commonly works with aggregate functions
│
├── COUNT()
│   └── HAVING COUNT(*) > 5
│
├── SUM()
│   └── HAVING SUM(revenue) > 100000
│
├── AVG()
│   └── HAVING AVG(salary) > 60000
│
├── MIN()
│   └── HAVING MIN(price) > 100
│
├── MAX()
│   └── HAVING MAX(price) > 1000
│
└── COUNT(DISTINCT)
    └── HAVING COUNT(DISTINCT customer_id) > 100
```

---

# 81. Most Important Difference to Memorize

```text
                 SQL FILTERING
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
        WHERE                   HAVING
          │                       │
      Filters ROWS           Filters GROUPS
          │                       │
      Before GROUP BY         After GROUP BY
          │                       │
    salary > 50000          AVG(salary) > 60000
    status = 'Active'       COUNT(*) > 10
    age >= 25               SUM(revenue) > 1M
```

### One-line memory trick

```text
WHERE = Which ROWS?
GROUP BY = Which GROUPS?
HAVING = Which GROUPS should remain?
```

---

# 82. Final Revision Examples

### Rows → Groups → Filter

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING COUNT(*) >= 10;
```

### Revenue analysis

```sql
SELECT
    category,
    SUM(revenue) AS total_revenue
FROM sales
GROUP BY category
HAVING SUM(revenue) > 1000000;
```

### Customer analysis

```sql
SELECT
    customer_id,
    COUNT(*) AS orders,
    SUM(amount) AS spending
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 5
   AND SUM(amount) > 50000;
```

### Unique customer analysis

```sql
SELECT
    region,
    COUNT(DISTINCT customer_id) AS customers
FROM sales
GROUP BY region
HAVING COUNT(DISTINCT customer_id) > 1000;
```

### JOIN + GROUP BY + HAVING

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spending
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.name
HAVING SUM(o.amount) > 50000
ORDER BY total_spending DESC;
```

---

# 83. Final Mental Model

```text
FROM
 ↓
Get the data
 ↓
WHERE
 ↓
Filter individual rows
 ↓
GROUP BY
 ↓
Create groups
 ↓
Aggregate Functions
 ↓
COUNT / SUM / AVG / MIN / MAX
 ↓
HAVING
 ↓
Filter groups
 ↓
ORDER BY
 ↓
Sort results
 ↓
LIMIT
 ↓
Restrict final result
```

## ⭐ Remember

> **WHERE filters rows. HAVING filters groups.**

If you understand that one sentence, you understand the fundamental purpose of `HAVING`.
