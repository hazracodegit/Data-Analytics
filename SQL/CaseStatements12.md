# SQL CASE Statements — Complete Guide

`CASE` is one of the most important SQL expressions for **conditional logic**.

It allows you to perform logic similar to:

```text
if
else if
else
```

in programming languages.

In SQL, `CASE` is commonly used for:

* Creating categories
* Conditional calculations
* Data transformation
* Data cleaning
* Data classification
* Conditional aggregation
* Creating flags
* Handling NULL values
* Creating derived columns
* Business rules
* Customer segmentation
* Data analytics
* Sorting
* Filtering
* Updating data

---

# 1. What is CASE?

`CASE` evaluates conditions and returns a value based on which condition is satisfied.

Basic structure:

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN condition3 THEN result3
    ELSE result4
END
```

Think of it as:

```text
IF condition1
    return result1

ELSE IF condition2
    return result2

ELSE IF condition3
    return result3

ELSE
    return result4
```

---

# 2. Basic Syntax

```sql
CASE
    WHEN condition THEN result
    ELSE result
END
```

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

Output:

| name  | salary | salary_category |
| ----- | -----: | --------------- |
| John  | 120000 | High            |
| David |  80000 | Low             |
| Sara  | 150000 | High            |

---

# 3. Why Do We Need CASE?

SQL is mainly used to retrieve and analyze data.

But analytics often requires creating new business logic.

For example:

```text
Salary >= 100000 → High
Salary >= 50000  → Medium
Salary < 50000   → Low
```

SQL doesn't have Python-style `if/elif/else` statements for expressions.

Instead, we use:

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

---

# 4. CASE Syntax Types

There are two major forms:

```text
1. Simple CASE
2. Searched CASE
```

---

# 5. Simple CASE

Simple `CASE` compares one expression against multiple values.

Syntax:

```sql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    WHEN value3 THEN result3
    ELSE result
END
```

Example:

```sql
SELECT
    employee_id,
    department_id,
    CASE department_id
        WHEN 1 THEN 'IT'
        WHEN 2 THEN 'HR'
        WHEN 3 THEN 'Finance'
        WHEN 4 THEN 'Sales'
        ELSE 'Other'
    END AS department_name
FROM employees;
```

---

# 6. Simple CASE Example

Suppose:

```text
department_id
-------------
1
2
3
4
```

Query:

```sql
SELECT
    department_id,
    CASE department_id
        WHEN 1 THEN 'IT'
        WHEN 2 THEN 'HR'
        WHEN 3 THEN 'Finance'
        WHEN 4 THEN 'Sales'
        ELSE 'Unknown'
    END AS department
FROM employees;
```

Result:

| department_id | department |
| ------------: | ---------- |
|             1 | IT         |
|             2 | HR         |
|             3 | Finance    |
|             4 | Sales      |

---

# 7. Searched CASE

Searched `CASE` evaluates conditions.

Syntax:

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN condition3 THEN result3
    ELSE result
END
```

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_level
FROM employees;
```

This is the most commonly used form in data analytics.

---

# 8. Simple CASE vs Searched CASE

| Feature                  | Simple CASE    | Searched CASE      |
| ------------------------ | -------------- | ------------------ |
| Compares                 | One expression | Conditions         |
| Uses `WHEN value`        | Yes            | No                 |
| Uses comparisons         | Limited        | Yes                |
| Uses `>`, `<`, `BETWEEN` | Not directly   | Yes                |
| Best for                 | Exact matching | Complex conditions |

Simple:

```sql
CASE department_id
    WHEN 1 THEN 'IT'
    WHEN 2 THEN 'HR'
END
```

Searched:

```sql
CASE
    WHEN salary > 100000 THEN 'High'
    WHEN salary > 50000 THEN 'Medium'
    ELSE 'Low'
END
```

---

# 9. CASE with Comparison Operators

You can use:

```text
=
<>
>
<
>=
<=
```

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High Salary'
        WHEN salary >= 50000 THEN 'Medium Salary'
        WHEN salary < 50000 THEN 'Low Salary'
        ELSE 'Unknown'
    END AS salary_category
FROM employees;
```

---

# 10. CASE with AND

Multiple conditions can be combined using `AND`.

```sql
SELECT
    name,
    age,
    salary,
    CASE
        WHEN age >= 25 AND salary >= 60000
            THEN 'Eligible'
        ELSE 'Not Eligible'
    END AS status
FROM employees;
```

---

# 11. CASE with OR

```sql
SELECT
    name,
    department,
    CASE
        WHEN department = 'IT'
          OR department = 'Finance'
            THEN 'Technical/Financial'
        ELSE 'Other'
    END AS department_group
FROM employees;
```

---

# 12. CASE with NOT

```sql
SELECT
    name,
    status,
    CASE
        WHEN NOT status = 'Inactive'
            THEN 'Active Employee'
        ELSE 'Inactive Employee'
    END AS employee_status
FROM employees;
```

A clearer version is often:

```sql
SELECT
    name,
    status,
    CASE
        WHEN status <> 'Inactive'
            THEN 'Active Employee'
        ELSE 'Inactive Employee'
    END AS employee_status
FROM employees;
```

---

# 13. CASE with BETWEEN

Very common for creating ranges.

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary BETWEEN 50000 AND 80000
            THEN 'Medium'
        WHEN salary > 80000
            THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 14. CASE with IN

```sql
SELECT
    name,
    department,
    CASE
        WHEN department IN ('IT', 'Engineering')
            THEN 'Technical'
        WHEN department IN ('HR', 'Finance')
            THEN 'Corporate'
        ELSE 'Other'
    END AS department_group
FROM employees;
```

---

# 15. CASE with LIKE

```sql
SELECT
    name,
    email,
    CASE
        WHEN email LIKE '%@gmail.com'
            THEN 'Gmail'
        WHEN email LIKE '%@yahoo.com'
            THEN 'Yahoo'
        ELSE 'Other'
    END AS email_provider
FROM customers;
```

---

# 16. CASE with NULL

You can use `IS NULL` and `IS NOT NULL`.

```sql
SELECT
    name,
    phone,
    CASE
        WHEN phone IS NULL THEN 'Missing'
        ELSE 'Available'
    END AS phone_status
FROM customers;
```

---

# 17. CASE for NULL Replacement

Example:

```sql
SELECT
    name,
    CASE
        WHEN phone IS NULL THEN 'Not Provided'
        ELSE phone
    END AS phone_number
FROM customers;
```

However, for simple NULL replacement, `COALESCE()` is often more concise:

```sql
SELECT
    name,
    COALESCE(phone, 'Not Provided') AS phone_number
FROM customers;
```

---

# 18. CASE with Multiple Conditions

Example:

```sql
SELECT
    employee_id,
    age,
    salary,
    experience,

    CASE
        WHEN age < 25 AND experience < 2
            THEN 'Junior'

        WHEN age >= 25
             AND experience BETWEEN 2 AND 5
            THEN 'Mid-Level'

        WHEN experience > 5
            THEN 'Senior'

        ELSE 'Other'
    END AS employee_level

FROM employees;
```

---

# 19. Important: CASE Executes in Order

This is extremely important.

Consider:

```sql
CASE
    WHEN salary >= 50000 THEN 'Medium'
    WHEN salary >= 100000 THEN 'High'
    ELSE 'Low'
END
```

A salary of `120000` will return:

```text
Medium
```

Why?

Because:

```text
120000 >= 50000
```

is already true.

SQL stops at the first matching `WHEN`.

---

# 20. Correct Ordering

More specific or higher threshold conditions should generally come first.

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

Now:

```text
120000 → High
70000  → Medium
30000  → Low
```

---

# 21. CASE and ELSE

`ELSE` defines what happens when no `WHEN` condition matches.

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

If no condition matches:

```text
Low
```

---

# 22. What Happens If ELSE Is Missing?

Example:

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
END
```

If neither condition matches, the result is generally:

```text
NULL
```

Therefore, for complete business logic, explicitly using `ELSE` is often safer.

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

---

# 23. CASE in SELECT

This is the most common usage.

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 24. CASE Creates a Derived Column

`CASE` does not modify the original column.

It creates a calculated/derived result.

```sql
SELECT
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

The original:

```text
salary
```

remains unchanged.

The query creates:

```text
salary_category
```

---

# 25. CASE for Age Groups

```sql
SELECT
    name,
    age,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 30 THEN 'Young Adult'
        WHEN age BETWEEN 31 AND 50 THEN 'Adult'
        WHEN age > 50 THEN 'Senior'
        ELSE 'Unknown'
    END AS age_group
FROM customers;
```

---

# 26. CASE for Customer Segmentation

Example:

```text
Total spending >= 100000 → Premium
Total spending >= 50000  → Gold
Total spending >= 10000  → Silver
Otherwise                → Bronze
```

```sql
SELECT
    customer_id,
    total_spending,
    CASE
        WHEN total_spending >= 100000 THEN 'Premium'
        WHEN total_spending >= 50000 THEN 'Gold'
        WHEN total_spending >= 10000 THEN 'Silver'
        ELSE 'Bronze'
    END AS customer_segment
FROM customer_summary;
```

This is extremely common in data analytics.

---

# 27. CASE for Sales Performance

```sql
SELECT
    salesperson,
    sales,
    CASE
        WHEN sales >= 1000000 THEN 'Excellent'
        WHEN sales >= 500000 THEN 'Good'
        WHEN sales >= 100000 THEN 'Average'
        ELSE 'Poor'
    END AS performance
FROM sales;
```

---

# 28. CASE for Pass/Fail

```sql
SELECT
    student_name,
    marks,
    CASE
        WHEN marks >= 40 THEN 'Pass'
        ELSE 'Fail'
    END AS result
FROM students;
```

---

# 29. CASE for Grades

```sql
SELECT
    student_name,
    marks,
    CASE
        WHEN marks >= 90 THEN 'A'
        WHEN marks >= 80 THEN 'B'
        WHEN marks >= 70 THEN 'C'
        WHEN marks >= 60 THEN 'D'
        WHEN marks >= 40 THEN 'E'
        ELSE 'F'
    END AS grade
FROM students;
```

---

# 30. CASE for Employee Experience

```sql
SELECT
    employee_id,
    experience_years,
    CASE
        WHEN experience_years < 2 THEN 'Fresher/Junior'
        WHEN experience_years < 5 THEN 'Mid-Level'
        WHEN experience_years < 10 THEN 'Experienced'
        ELSE 'Senior'
    END AS experience_level
FROM employees;
```

---

# 31. CASE for Product Stock

```sql
SELECT
    product_id,
    stock_quantity,
    CASE
        WHEN stock_quantity = 0 THEN 'Out of Stock'
        WHEN stock_quantity < 10 THEN 'Low Stock'
        WHEN stock_quantity < 50 THEN 'Normal Stock'
        ELSE 'High Stock'
    END AS inventory_status
FROM products;
```

---

# 32. CASE for Order Status

```sql
SELECT
    order_id,
    status,
    CASE
        WHEN status = 'Delivered' THEN 'Completed'
        WHEN status = 'Cancelled' THEN 'Failed'
        WHEN status IN ('Pending', 'Processing')
            THEN 'In Progress'
        ELSE 'Other'
    END AS order_category
FROM orders;
```

---

# 33. CASE for Profitability

Suppose:

```text
profit > 0 → Profitable
profit = 0 → Break-even
profit < 0 → Loss
```

```sql
SELECT
    product_id,
    profit,
    CASE
        WHEN profit > 0 THEN 'Profitable'
        WHEN profit = 0 THEN 'Break-even'
        ELSE 'Loss'
    END AS profit_status
FROM products;
```

---

# 34. CASE for Percentage

Suppose we calculate profit margin:

```sql
SELECT
    product_id,
    revenue,
    cost,
    CASE
        WHEN revenue = 0 THEN 0
        ELSE ((revenue - cost) * 100.0 / revenue)
    END AS profit_margin
FROM sales;
```

The `CASE` prevents division by zero.

---

# 35. CASE to Prevent Division by Zero

Very important in analytics.

Potentially problematic:

```sql
SELECT
    revenue / quantity AS average_price
FROM sales;
```

If:

```text
quantity = 0
```

you may get a division-by-zero error depending on the database.

Using `CASE`:

```sql
SELECT
    CASE
        WHEN quantity = 0 THEN NULL
        ELSE revenue / quantity
    END AS average_price
FROM sales;
```

---

# 36. CASE for Conditional Calculation

You can return numbers.

```sql
SELECT
    product,
    price,
    CASE
        WHEN price >= 1000 THEN price * 0.90
        ELSE price * 0.95
    END AS discounted_price
FROM products;
```

Meaning:

```text
Price >= 1000
→ 10% discount

Otherwise
→ 5% discount
```

---

# 37. CASE Can Return Different Data Types?

Avoid mixing incompatible result types.

Good:

```sql
CASE
    WHEN salary > 50000 THEN 1
    ELSE 0
END
```

Good:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
END
```

Bad practice:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 100
END
```

Different SQL databases handle type resolution differently, and this may cause conversion errors.

Prefer consistent result types.

---

# 38. CASE for Boolean/Flag Columns

A very common analytics technique.

```sql
SELECT
    customer_id,
    CASE
        WHEN total_spending >= 50000 THEN 1
        ELSE 0
    END AS high_value_customer
FROM customer_summary;
```

Output:

| customer_id | high_value_customer |
| ----------- | ------------------: |
| 101         |                   1 |
| 102         |                   0 |
| 103         |                   1 |

This is called a **flag**.

---

# 39. Creating Multiple Flags

```sql
SELECT
    customer_id,

    CASE
        WHEN total_spending >= 50000 THEN 1
        ELSE 0
    END AS high_value_flag,

    CASE
        WHEN order_count >= 10 THEN 1
        ELSE 0
    END AS loyal_customer_flag,

    CASE
        WHEN last_order_date >= CURRENT_DATE - INTERVAL '30' DAY
            THEN 1
        ELSE 0
    END AS active_customer_flag

FROM customer_summary;
```

The exact date syntax varies by database.

---

# 40. CASE with COUNT()

One of the most important analytics techniques is:

```text
CASE inside aggregate function
```

Example:

```sql
SELECT
    COUNT(
        CASE
            WHEN salary >= 100000 THEN 1
        END
    ) AS high_salary_employees
FROM employees;
```

This counts employees satisfying the condition.

---

# 41. Conditional Aggregation

Conditional aggregation means:

> Aggregate only rows satisfying a condition.

Example:

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed' THEN 1
            ELSE 0
        END
    ) AS completed_orders
FROM orders;
```

---

# 42. Conditional COUNT Using CASE

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed' THEN 1
            ELSE 0
        END
    ) AS completed_orders,

    SUM(
        CASE
            WHEN status = 'Cancelled' THEN 1
            ELSE 0
        END
    ) AS cancelled_orders

FROM orders;
```

This gives multiple metrics in one query.

---

# 43. Conditional SUM

Suppose we want total revenue from completed orders.

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue
FROM orders;
```

---

# 44. Conditional AVG

You can calculate an average for a subset of rows.

```sql
SELECT
    AVG(
        CASE
            WHEN gender = 'Female'
                THEN salary
        END
    ) AS average_female_salary
FROM employees;
```

Because the `ELSE` is omitted, unmatched rows produce NULL, and `AVG()` generally ignores NULL.

---

# 45. Conditional Aggregation by Group

This is extremely important for data analytics.

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN gender = 'Male' THEN 1
            ELSE 0
        END
    ) AS male_count,

    SUM(
        CASE
            WHEN gender = 'Female' THEN 1
            ELSE 0
        END
    ) AS female_count

FROM employees

GROUP BY department;
```

Result conceptually:

| department | male_count | female_count |
| ---------- | ---------: | -----------: |
| IT         |         30 |           20 |
| HR         |         10 |           25 |
| Finance    |         15 |           15 |

---

# 46. Conditional Revenue Analysis

```sql
SELECT
    region,

    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue,

    SUM(
        CASE
            WHEN status = 'Cancelled'
                THEN revenue
            ELSE 0
        END
    ) AS cancelled_revenue

FROM sales

GROUP BY region;
```

This is a common business analytics pattern.

---

# 47. Multiple CASE Expressions

You can use multiple `CASE` expressions in one query.

```sql
SELECT
    employee_id,

    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category,

    CASE
        WHEN experience_years >= 5 THEN 'Experienced'
        ELSE 'Junior'
    END AS experience_category,

    CASE
        WHEN performance_score >= 80 THEN 'Good'
        ELSE 'Needs Improvement'
    END AS performance_category

FROM employees;
```

---

# 48. CASE in GROUP BY

You can group based on a calculated category.

Example:

```sql
SELECT
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category,

    COUNT(*) AS employee_count

FROM employees

GROUP BY
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END;
```

Some databases allow using the alias in `GROUP BY`, while others may require the full expression.

---

# 49. Better Approach Using a CTE

Instead of repeating the `CASE`:

```sql
WITH employee_categories AS (
    SELECT
        employee_id,
        salary,
        CASE
            WHEN salary >= 100000 THEN 'High'
            WHEN salary >= 50000 THEN 'Medium'
            ELSE 'Low'
        END AS salary_category
    FROM employees
)

SELECT
    salary_category,
    COUNT(*) AS employee_count
FROM employee_categories
GROUP BY salary_category;
```

This is often easier to maintain.

---

# 50. CASE in HAVING

You can use conditional aggregation with `HAVING`.

Example:

> Find departments with at least 5 employees earning over 100K.

```sql
SELECT
    department,

    SUM(
        CASE
            WHEN salary > 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count

FROM employees

GROUP BY department

HAVING
    SUM(
        CASE
            WHEN salary > 100000 THEN 1
            ELSE 0
        END
    ) >= 5;
```

---

# 51. CASE in ORDER BY

`CASE` can control sorting.

Example:

```sql
SELECT
    product,
    status
FROM products
ORDER BY
    CASE
        WHEN status = 'Critical' THEN 1
        WHEN status = 'Low' THEN 2
        WHEN status = 'Normal' THEN 3
        ELSE 4
    END;
```

This creates custom sorting.

---

# 52. Custom Priority Sorting

Suppose statuses are:

```text
Critical
High
Medium
Low
```

We want that exact order.

```sql
SELECT
    ticket_id,
    priority
FROM tickets
ORDER BY
    CASE
        WHEN priority = 'Critical' THEN 1
        WHEN priority = 'High' THEN 2
        WHEN priority = 'Medium' THEN 3
        WHEN priority = 'Low' THEN 4
        ELSE 5
    END;
```

This is extremely useful.

---

# 53. CASE in UPDATE

`CASE` can be used to update values conditionally.

Example:

```sql
UPDATE employees
SET salary = CASE
    WHEN performance_rating = 'Excellent'
        THEN salary * 1.20

    WHEN performance_rating = 'Good'
        THEN salary * 1.10

    ELSE salary
END;
```

Meaning:

```text
Excellent → 20% raise
Good      → 10% raise
Other     → no change
```

---

# 54. CASE in UPDATE with WHERE

A safer pattern is to restrict the rows being updated.

```sql
UPDATE employees
SET salary = CASE
    WHEN performance_rating = 'Excellent'
        THEN salary * 1.20
    WHEN performance_rating = 'Good'
        THEN salary * 1.10
    ELSE salary
END
WHERE performance_rating IN ('Excellent', 'Good');
```

---

# 55. CASE in DELETE?

`CASE` itself is not normally used as the direct replacement for `WHERE` in a `DELETE`.

Use conditions:

```sql
DELETE FROM employees
WHERE status = 'Inactive';
```

If conditional logic is required, use `CASE` to derive data in a subquery/CTE or use logical conditions directly in `WHERE`.

---

# 56. CASE with JOIN

You can create categories after joining tables.

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spending,

    CASE
        WHEN SUM(o.amount) >= 100000 THEN 'Premium'
        WHEN SUM(o.amount) >= 50000 THEN 'Gold'
        WHEN SUM(o.amount) >= 10000 THEN 'Silver'
        ELSE 'Bronze'
    END AS customer_segment

FROM customers c

JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.customer_id,
    c.name;
```

Notice that the `CASE` uses an aggregate:

```sql
SUM(o.amount)
```

---

# 57. CASE with JOIN and HAVING

```sql
SELECT
    c.customer_id,
    c.name,

    COUNT(o.order_id) AS order_count,

    CASE
        WHEN COUNT(o.order_id) >= 20 THEN 'VIP'
        WHEN COUNT(o.order_id) >= 10 THEN 'Loyal'
        WHEN COUNT(o.order_id) >= 5 THEN 'Regular'
        ELSE 'New'
    END AS customer_type

FROM customers c

LEFT JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.customer_id,
    c.name

HAVING COUNT(o.order_id) > 0;
```

---

# 58. CASE for Data Cleaning

CASE is extremely useful for cleaning inconsistent categories.

Suppose data contains:

```text
M
Male
male
MALE
F
Female
female
```

We can standardize it:

```sql
SELECT
    customer_id,
    CASE
        WHEN LOWER(gender) IN ('m', 'male')
            THEN 'Male'

        WHEN LOWER(gender) IN ('f', 'female')
            THEN 'Female'

        ELSE 'Unknown'
    END AS standardized_gender

FROM customers;
```

---

# 59. CASE for Standardizing Categories

Suppose:

```text
NY
New York
new york
NYC
```

You can normalize them:

```sql
SELECT
    CASE
        WHEN UPPER(TRIM(city)) IN ('NY', 'NYC', 'NEW YORK')
            THEN 'New York'
        ELSE TRIM(city)
    END AS standardized_city
FROM customers;
```

This combines:

```text
TRIM()
UPPER()
CASE
```

for data cleaning.

---

# 60. CASE for Missing Data Categories

```sql
SELECT
    customer_id,
    CASE
        WHEN email IS NULL OR TRIM(email) = ''
            THEN 'Missing'
        ELSE 'Available'
    END AS email_status
FROM customers;
```

---

# 61. CASE for Data Quality Flags

```sql
SELECT
    customer_id,

    CASE
        WHEN email IS NULL
            THEN 'Missing Email'

        WHEN phone IS NULL
            THEN 'Missing Phone'

        WHEN email IS NULL AND phone IS NULL
            THEN 'Missing Both'

        ELSE 'Complete'
    END AS data_quality_status

FROM customers;
```

### Important ordering issue

The above order has a problem.

If both are NULL, the first condition:

```sql
email IS NULL
```

matches first.

So `"Missing Both"` will never be reached.

Correct:

```sql
SELECT
    customer_id,

    CASE
        WHEN email IS NULL AND phone IS NULL
            THEN 'Missing Both'

        WHEN email IS NULL
            THEN 'Missing Email'

        WHEN phone IS NULL
            THEN 'Missing Phone'

        ELSE 'Complete'
    END AS data_quality_status

FROM customers;
```

This demonstrates why **CASE condition order matters**.

---

# 62. CASE for Outlier Detection

You can create simple rule-based flags.

```sql
SELECT
    customer_id,
    transaction_amount,

    CASE
        WHEN transaction_amount > 100000
            THEN 'Potential Outlier'
        ELSE 'Normal'
    END AS transaction_status

FROM transactions;
```

This is not a statistical outlier method, but it can be useful for rule-based screening.

---

# 63. CASE for Business Rules

Example:

```text
Customer is VIP if:
- Spending >= 100000
OR
- Orders >= 20
```

```sql
SELECT
    customer_id,
    total_spending,
    order_count,

    CASE
        WHEN total_spending >= 100000
          OR order_count >= 20
            THEN 'VIP'
        ELSE 'Regular'
    END AS customer_type

FROM customer_summary;
```

---

# 64. CASE for Customer Churn Flags

Example rule:

```text
No purchase for 90+ days → At Risk
```

Database-specific date syntax varies, but conceptually:

```sql
SELECT
    customer_id,
    last_order_date,

    CASE
        WHEN last_order_date < CURRENT_DATE - INTERVAL '90' DAY
            THEN 'At Risk'
        ELSE 'Active'
    END AS customer_status

FROM customers;
```

---

# 65. CASE for Revenue Buckets

```sql
SELECT
    customer_id,
    revenue,

    CASE
        WHEN revenue >= 1000000 THEN '1M+'
        WHEN revenue >= 500000 THEN '500K-1M'
        WHEN revenue >= 100000 THEN '100K-500K'
        WHEN revenue >= 50000 THEN '50K-100K'
        ELSE 'Below 50K'
    END AS revenue_bucket

FROM sales;
```

---

# 66. CASE for Age Buckets

```sql
SELECT
    customer_id,
    age,

    CASE
        WHEN age < 18 THEN 'Under 18'
        WHEN age BETWEEN 18 AND 24 THEN '18-24'
        WHEN age BETWEEN 25 AND 34 THEN '25-34'
        WHEN age BETWEEN 35 AND 44 THEN '35-44'
        WHEN age BETWEEN 45 AND 54 THEN '45-54'
        ELSE '55+'
    END AS age_group

FROM customers;
```

---

# 67. CASE for Date-Based Classification

Example:

```sql
SELECT
    order_id,
    order_date,

    CASE
        WHEN EXTRACT(MONTH FROM order_date) IN (12, 1, 2)
            THEN 'Winter'

        WHEN EXTRACT(MONTH FROM order_date) IN (3, 4, 5)
            THEN 'Spring'

        WHEN EXTRACT(MONTH FROM order_date) IN (6, 7, 8)
            THEN 'Summer'

        ELSE 'Autumn'
    END AS season

FROM orders;
```

Date functions vary by SQL database.

---

# 68. CASE with Mathematical Expressions

```sql
SELECT
    product_id,
    price,
    quantity,

    CASE
        WHEN quantity > 100
            THEN price * quantity * 0.90

        WHEN quantity > 50
            THEN price * quantity * 0.95

        ELSE price * quantity
    END AS final_revenue

FROM sales;
```

---

# 69. CASE for Discounts

```sql
SELECT
    product_id,
    price,

    CASE
        WHEN price >= 10000 THEN price * 0.80
        WHEN price >= 5000 THEN price * 0.90
        WHEN price >= 1000 THEN price * 0.95
        ELSE price
    END AS discounted_price

FROM products;
```

---

# 70. CASE and NULL vs ELSE 0

Consider:

```sql
SUM(
    CASE
        WHEN status = 'Completed'
            THEN revenue
    END
)
```

Unmatched rows return NULL.

Alternatively:

```sql
SUM(
    CASE
        WHEN status = 'Completed'
            THEN revenue
        ELSE 0
    END
)
```

Unmatched rows return 0.

For `SUM`, both often produce the same total when at least one matching row exists, but the behavior when no rows match can differ depending on the database and expression. Choose deliberately.

---

# 71. CASE + SUM Pattern

Memorize this:

```sql
SUM(
    CASE
        WHEN condition THEN value
        ELSE 0
    END
)
```

Example:

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed'
                THEN amount
            ELSE 0
        END
    ) AS completed_sales
FROM orders;
```

This pattern is extremely important in analytics.

---

# 72. CASE + COUNT Pattern

Another important pattern:

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

Example:

```sql
SELECT
    SUM(
        CASE
            WHEN status = 'Completed' THEN 1
            ELSE 0
        END
    ) AS completed_orders
FROM orders;
```

Think:

```text
CASE → creates 1/0
SUM  → counts the 1s
```

---

# 73. CASE + GROUP BY + Aggregate

Example:

```sql
SELECT
    region,

    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue,

    SUM(
        CASE
            WHEN status = 'Cancelled'
                THEN revenue
            ELSE 0
        END
    ) AS cancelled_revenue

FROM sales

GROUP BY region;
```

This gives multiple conditional metrics per region.

---

# 74. CASE for Pivot-Style Analysis

You can create columns based on categories.

```sql
SELECT
    region,

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
    ) AS clothing_revenue,

    SUM(
        CASE
            WHEN category = 'Furniture'
                THEN revenue
            ELSE 0
        END
    ) AS furniture_revenue

FROM sales

GROUP BY region;
```

This is often called **conditional aggregation** or a **manual pivot**.

---

# 75. CASE with HAVING and Conditional Aggregation

Example:

> Find regions where completed revenue is greater than 1 million.

```sql
SELECT
    region,

    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue

FROM sales

GROUP BY region

HAVING
    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) > 1000000;
```

---

# 76. CASE for Conversion Rate

Suppose we have:

```text
visitors
conversions
```

We can avoid division by zero:

```sql
SELECT
    campaign,

    CASE
        WHEN visitors = 0 THEN 0
        ELSE conversions * 100.0 / visitors
    END AS conversion_rate

FROM campaigns;
```

---

# 77. CASE for Profit Margin

```sql
SELECT
    product_id,
    revenue,
    cost,

    CASE
        WHEN revenue = 0 THEN 0
        ELSE (revenue - cost) * 100.0 / revenue
    END AS profit_margin

FROM products;
```

---

# 78. CASE for Employee Bonus

```sql
SELECT
    employee_id,
    salary,
    performance_score,

    CASE
        WHEN performance_score >= 90
            THEN salary * 0.20

        WHEN performance_score >= 80
            THEN salary * 0.10

        WHEN performance_score >= 70
            THEN salary * 0.05

        ELSE 0
    END AS bonus

FROM employees;
```

---

# 79. CASE vs COALESCE

These are different tools.

### CASE

Used for general conditional logic.

```sql
CASE
    WHEN salary IS NULL THEN 0
    WHEN salary < 50000 THEN 50000
    ELSE salary
END
```

### COALESCE

Used to return the first non-NULL value.

```sql
COALESCE(salary, 0)
```

Use:

```text
CASE → complex conditions
COALESCE → simple NULL replacement
```

---

# 80. CASE vs NULLIF

`NULLIF()` returns NULL when two expressions are equal.

Example:

```sql
NULLIF(quantity, 0)
```

Can help avoid division by zero:

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS average_price
FROM sales;
```

This can be more concise than:

```sql
CASE
    WHEN quantity = 0 THEN NULL
    ELSE revenue / quantity
END
```

Both are useful patterns.

---

# 81. CASE vs IF

Some SQL databases provide functions such as `IF()` or `IIF()`.

However, `CASE` is part of standard SQL and is generally more portable.

Prefer:

```sql
CASE
    WHEN condition THEN result
    ELSE result
END
```

when writing SQL intended to work across different database systems.

---

# 82. CASE vs WHERE

They serve different purposes.

### WHERE

Filters rows.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### CASE

Creates a conditional value.

```sql
SELECT
    name,
    CASE
        WHEN salary > 50000 THEN 'High'
        ELSE 'Low'
    END AS category
FROM employees;
```

---

# 83. CASE vs HAVING

### HAVING

Filters groups:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### CASE

Creates conditional output:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary,

    CASE
        WHEN AVG(salary) > 60000
            THEN 'High'
        ELSE 'Low'
    END AS salary_status

FROM employees
GROUP BY department;
```

---

# 84. CASE and Window Functions

You can use `CASE` with window functions.

Example:

```sql
SELECT
    employee_id,
    department,
    salary,

    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_average,

    CASE
        WHEN salary >
             AVG(salary) OVER (
                 PARTITION BY department
             )
            THEN 'Above Average'
        ELSE 'Below/Equal Average'
    END AS salary_position

FROM employees;
```

This combines:

```text
CASE
+
Window Function
```

for employee-level analytics.

---

# 85. CASE with RANKING

Example:

```sql
SELECT
    employee_id,
    salary,

    CASE
        WHEN salary >= 100000 THEN 'Top Salary'
        ELSE 'Standard Salary'
    END AS salary_type,

    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank

FROM employees;
```

---

# 86. CASE for Cohort Classification

Suppose customers joined in different years.

```sql
SELECT
    customer_id,
    signup_year,

    CASE
        WHEN signup_year = 2026 THEN '2026 Cohort'
        WHEN signup_year = 2025 THEN '2025 Cohort'
        WHEN signup_year = 2024 THEN '2024 Cohort'
        ELSE 'Older Cohort'
    END AS cohort

FROM customers;
```

---

# 87. CASE in Data Analytics Workflow

A typical analytics workflow can look like:

```text
Raw Data
   ↓
Data Cleaning
   ↓
CASE
   ↓
Create categories / flags
   ↓
GROUP BY
   ↓
Aggregation
   ↓
HAVING
   ↓
Analysis
```

For example:

```sql
SELECT
    CASE
        WHEN age < 25 THEN 'Young'
        WHEN age < 40 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group,

    COUNT(*) AS customer_count,

    AVG(spending) AS average_spending

FROM customers

GROUP BY
    CASE
        WHEN age < 25 THEN 'Young'
        WHEN age < 40 THEN 'Adult'
        ELSE 'Senior'
    END

HAVING COUNT(*) >= 100;
```

---

# 88. Common CASE Mistakes

## Mistake 1 — Forgetting END

Wrong:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
```

Correct:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
END
```

---

# 89. Mistake 2 — Incorrect Condition Order

Wrong:

```sql
CASE
    WHEN salary >= 50000 THEN 'Medium'
    WHEN salary >= 100000 THEN 'High'
    ELSE 'Low'
END
```

Correct:

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

---

# 90. Mistake 3 — Forgetting ELSE

Possible result:

```text
NULL
```

Safer:

```sql
CASE
    WHEN condition THEN 'Yes'
    ELSE 'No'
END
```

---

# 91. Mistake 4 — Mixing Data Types

Avoid:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 0
END
```

Use consistent types:

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
END
```

or:

```sql
CASE
    WHEN salary > 50000 THEN 1
    ELSE 0
END
```

---

# 92. Mistake 5 — Confusing `=` and `IS NULL`

Wrong:

```sql
CASE
    WHEN phone = NULL THEN 'Missing'
END
```

Correct:

```sql
CASE
    WHEN phone IS NULL THEN 'Missing'
END
```

Remember:

```text
NULL is not compared using =
```

---

# 93. Mistake 6 — Overlapping Conditions

Example:

```sql
CASE
    WHEN age >= 18 THEN 'Adult'
    WHEN age >= 65 THEN 'Senior'
END
```

A 70-year-old matches:

```text
age >= 18
```

first.

Correct:

```sql
CASE
    WHEN age >= 65 THEN 'Senior'
    WHEN age >= 18 THEN 'Adult'
    ELSE 'Minor'
END
```

---

# 94. Mistake 7 — Forgetting ELSE for Unexpected Data

Suppose known statuses are:

```text
Active
Inactive
Pending
```

Instead of:

```sql
CASE
    WHEN status = 'Active' THEN 'A'
    WHEN status = 'Inactive' THEN 'I'
END
```

consider:

```sql
CASE
    WHEN status = 'Active' THEN 'A'
    WHEN status = 'Inactive' THEN 'I'
    WHEN status = 'Pending' THEN 'P'
    ELSE 'Unknown'
END
```

This makes unexpected values visible.

---

# 95. CASE Performance Considerations

`CASE` itself is usually not a problem.

But complex expressions can increase query complexity.

For example:

```sql
CASE
    WHEN condition1 THEN ...
    WHEN condition2 THEN ...
    WHEN condition3 THEN ...
    ...
    WHEN condition50 THEN ...
END
```

If business logic becomes very large, consider:

* Lookup tables
* Mapping tables
* CTEs
* Views
* Dimension tables
* Separate transformation layers

Instead of maintaining hundreds of hard-coded conditions.

---

# 96. CASE vs Lookup Table

Suppose you repeatedly use:

```sql
CASE
    WHEN department_id = 1 THEN 'IT'
    WHEN department_id = 2 THEN 'HR'
    WHEN department_id = 3 THEN 'Finance'
END
```

A better database design may be:

```text
departments
--------------------
department_id
department_name
```

Then:

```sql
SELECT
    e.employee_id,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Use `CASE` for **logic**, and lookup tables for **stable mappings**.

---

# 97. Real Data Analytics Example

Suppose we have:

```text
customer_id
age
income
orders
spending
```

We can create customer segments:

```sql
SELECT
    customer_id,

    CASE
        WHEN spending >= 100000
             AND orders >= 20
            THEN 'VIP'

        WHEN spending >= 50000
             AND orders >= 10
            THEN 'High Value'

        WHEN spending >= 10000
            THEN 'Regular'

        ELSE 'Low Value'
    END AS customer_segment

FROM customer_summary;
```

This is a real-world analytics transformation.

---

# 98. Advanced Example — Multiple Business Metrics

```sql
SELECT
    region,

    COUNT(*) AS total_orders,

    SUM(revenue) AS total_revenue,

    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue,

    SUM(
        CASE
            WHEN status = 'Cancelled'
                THEN revenue
            ELSE 0
        END
    ) AS cancelled_revenue,

    SUM(
        CASE
            WHEN revenue >= 10000
                THEN 1
            ELSE 0
        END
    ) AS high_value_orders

FROM sales

GROUP BY region;
```

This produces several business metrics at once.

---

# 99. Advanced Example — CASE + HAVING

```sql
SELECT
    region,

    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) AS completed_revenue,

    COUNT(
        CASE
            WHEN status = 'Completed'
                THEN order_id
        END
    ) AS completed_orders

FROM sales

GROUP BY region

HAVING
    SUM(
        CASE
            WHEN status = 'Completed'
                THEN revenue
            ELSE 0
        END
    ) > 1000000;
```

Meaning:

> Return only regions with completed revenue above 1 million.

---

# 100. Advanced Example — Customer Segmentation

```sql
WITH customer_summary AS (
    SELECT
        customer_id,
        COUNT(*) AS order_count,
        SUM(amount) AS total_spending
    FROM orders
    GROUP BY customer_id
)

SELECT
    customer_id,
    order_count,
    total_spending,

    CASE
        WHEN total_spending >= 100000
             AND order_count >= 20
            THEN 'VIP'

        WHEN total_spending >= 50000
             AND order_count >= 10
            THEN 'Gold'

        WHEN total_spending >= 10000
            THEN 'Silver'

        ELSE 'Bronze'
    END AS customer_segment

FROM customer_summary;
```

This is a very good pattern to understand for analytics projects.

---

# 101. CASE Decision Tree

When writing a CASE statement, think like this:

```text
             Start
               │
               ↓
       Is condition 1 true?
          /           \
        YES            NO
         ↓              ↓
     Result 1     Is condition 2 true?
                    /          \
                  YES           NO
                   ↓             ↓
               Result 2     Is condition 3 true?
                               /       \
                             YES        NO
                              ↓          ↓
                          Result 3      ELSE
```

---

# 102. CASE Mental Model

Remember:

```text
CASE
 │
 ├── WHEN → condition
 │
 ├── THEN → result if true
 │
 ├── WHEN → next condition
 │
 ├── THEN → next result
 │
 ├── ELSE → default result
 │
 └── END → finishes CASE
```

---

# 103. CASE Cheat Sheet

### Basic

```sql
CASE
    WHEN condition THEN result
    ELSE result
END
```

### Multiple conditions

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result3
END
```

### Exact matching

```sql
CASE column
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ELSE result
END
```

### Conditional flag

```sql
CASE
    WHEN condition THEN 1
    ELSE 0
END
```

### Conditional count

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

### Conditional sum

```sql
SUM(
    CASE
        WHEN condition THEN amount
        ELSE 0
    END
)
```

### NULL handling

```sql
CASE
    WHEN column IS NULL THEN 'Missing'
    ELSE 'Available'
END
```

### Custom sorting

```sql
ORDER BY
    CASE
        WHEN status = 'High' THEN 1
        WHEN status = 'Medium' THEN 2
        WHEN status = 'Low' THEN 3
        ELSE 4
    END;
```

---

# 104. CASE — Most Important Rules

## Rule 1

`CASE` returns a value.

```sql
CASE
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
END
```

---

## Rule 2

`WHEN` contains a condition.

```sql
WHEN salary > 50000
```

---

## Rule 3

`THEN` contains the returned value.

```sql
THEN 'High'
```

---

## Rule 4

`ELSE` is the default result.

```sql
ELSE 'Low'
```

---

## Rule 5

`END` closes the CASE.

```sql
END
```

---

## Rule 6

Conditions are evaluated in order.

```text
First matching WHEN wins.
```

---

## Rule 7

Use `IS NULL`, not `= NULL`.

```sql
column IS NULL
```

---

## Rule 8

Keep result data types compatible.

---

## Rule 9

`CASE` can be used with:

```text
SELECT
WHERE-related expressions
GROUP BY
HAVING-related expressions
ORDER BY
UPDATE
Aggregations
Window functions
CTEs
JOIN queries
```

---

# 105. CASE vs Programming IF

### Python

```python
if salary >= 100000:
    category = "High"
elif salary >= 50000:
    category = "Medium"
else:
    category = "Low"
```

### SQL

```sql
CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

Conceptually:

```text
Python IF/ELIF/ELSE
          ↓
       SQL CASE
```

---

# 106. Most Important Interview Patterns

### Pattern 1 — Categorization

```sql
CASE
    WHEN value >= 100 THEN 'High'
    WHEN value >= 50 THEN 'Medium'
    ELSE 'Low'
END
```

### Pattern 2 — Binary Flag

```sql
CASE
    WHEN condition THEN 1
    ELSE 0
END
```

### Pattern 3 — Conditional Count

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

### Pattern 4 — Conditional Sum

```sql
SUM(
    CASE
        WHEN condition THEN amount
        ELSE 0
    END
)
```

### Pattern 5 — Conditional Average

```sql
AVG(
    CASE
        WHEN condition THEN value
    END
)
```

### Pattern 6 — NULL Handling

```sql
CASE
    WHEN column IS NULL THEN 'Missing'
    ELSE 'Available'
END
```

### Pattern 7 — Custom Sorting

```sql
ORDER BY
    CASE
        WHEN priority = 'High' THEN 1
        WHEN priority = 'Medium' THEN 2
        ELSE 3
    END
```

---

# 107. Final Revision Example

This combines many concepts:

```sql
SELECT
    c.customer_id,

    COUNT(o.order_id) AS order_count,

    SUM(o.amount) AS total_spending,

    CASE
        WHEN SUM(o.amount) >= 100000
             AND COUNT(o.order_id) >= 20
            THEN 'VIP'

        WHEN SUM(o.amount) >= 50000
             AND COUNT(o.order_id) >= 10
            THEN 'Gold'

        WHEN SUM(o.amount) >= 10000
            THEN 'Silver'

        ELSE 'Bronze'
    END AS customer_segment

FROM customers c

LEFT JOIN orders o
    ON c.customer_id = o.customer_id

GROUP BY
    c.customer_id

HAVING COUNT(o.order_id) > 0

ORDER BY
    total_spending DESC;
```

This query demonstrates:

```text
JOIN
 ↓
GROUP BY
 ↓
COUNT()
 ↓
SUM()
 ↓
CASE
 ↓
HAVING
 ↓
ORDER BY
```

---

# 108. Final Mental Model

```text
                 SQL CASE
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
     Simple CASE         Searched CASE
          │                   │
     Exact values          Conditions
          │                   │
   CASE column          CASE
      WHEN 1             WHEN salary > ...
      WHEN 2             WHEN salary > ...
```

And for analytics:

```text
CASE
 ↓
Create categories / flags
 ↓
GROUP BY
 ↓
Aggregate
 ↓
HAVING
 ↓
Filter groups
 ↓
ORDER BY
 ↓
Analyze
```

## ⭐ One-Line Memory Trick

> **CASE = SQL's conditional logic: evaluate conditions and return the first matching result.**

## ⭐ The Most Important Analytics Pattern

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

This pattern is worth memorizing because it is used constantly for **conditional counting, business metrics, dashboards, reporting, segmentation, and data analysis**.
