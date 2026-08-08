# 📊 Data Quality in Data Analytics

> Complete beginner-to-advanced notes on Data Quality, including dimensions, metrics, problems, measurement, profiling, validation, monitoring, root-cause analysis, and practical examples.

---

# 📚 Table of Contents

1. [What is Data Quality?](#1-what-is-data-quality)
2. [Technical Definition](#2-technical-definition)
3. [Why Data Quality Matters](#3-why-data-quality-matters)
4. [Data Quality in the Analytics Lifecycle](#4-data-quality-in-the-analytics-lifecycle)
5. [Data Quality vs Data Cleaning](#5-data-quality-vs-data-cleaning)
6. [Data Quality vs Data Validation](#6-data-quality-vs-data-validation)
7. [Data Quality Dimensions](#7-data-quality-dimensions)
8. [Accuracy](#8-accuracy)
9. [Completeness](#9-completeness)
10. [Consistency](#10-consistency)
11. [Validity](#11-validity)
12. [Uniqueness](#12-uniqueness)
13. [Timeliness](#13-timeliness)
14. [Relevance](#14-relevance)
15. [Integrity](#15-integrity)
16. [Reliability](#16-reliability)
17. [Precision](#17-precision)
18. [Granularity](#18-granularity)
19. [Accessibility](#19-accessibility)
20. [Interpretability](#20-interpretability)
21. [Data Quality Dimensions Compared](#21-data-quality-dimensions-compared)
22. [Common Data Quality Problems](#22-common-data-quality-problems)
23. [Missing Data](#23-missing-data)
24. [Duplicate Data](#24-duplicate-data)
25. [Incorrect Data](#25-incorrect-data)
26. [Invalid Data](#26-invalid-data)
27. [Inconsistent Data](#27-inconsistent-data)
28. [Outdated Data](#28-outdated-data)
29. [Inaccurate Data](#29-inaccurate-data)
30. [Data Type Problems](#30-data-type-problems)
31. [Formatting Problems](#31-formatting-problems)
32. [Referential Integrity Problems](#32-referential-integrity-problems)
33. [Data Quality Metrics](#33-data-quality-metrics)
34. [Completeness Rate](#34-completeness-rate)
35. [Validity Rate](#35-validity-rate)
36. [Accuracy Rate](#36-accuracy-rate)
37. [Duplicate Rate](#37-duplicate-rate)
38. [Consistency Rate](#38-consistency-rate)
39. [Timeliness Metrics](#39-timeliness-metrics)
40. [Data Quality Rules](#40-data-quality-rules)
41. [Data Validation Rules](#41-data-validation-rules)
42. [Data Profiling](#42-data-profiling)
43. [Data Quality Assessment](#43-data-quality-assessment)
44. [Data Quality Score](#44-data-quality-score)
45. [Data Quality Framework](#45-data-quality-framework)
46. [Data Quality Monitoring](#46-data-quality-monitoring)
47. [Data Quality Checks in SQL](#47-data-quality-checks-in-sql)
48. [Data Quality Checks in Python](#48-data-quality-checks-in-python)
49. [Data Quality in ETL](#49-data-quality-in-etl)
50. [Data Quality in Data Warehouses](#50-data-quality-in-data-warehouses)
51. [Data Quality in Data Lakes](#51-data-quality-in-data-lakes)
52. [Data Quality in APIs](#52-data-quality-in-apis)
53. [Data Quality in Machine Learning](#53-data-quality-in-machine-learning)
54. [Data Quality and Bias](#54-data-quality-and-bias)
55. [Data Quality and Business Analytics](#55-data-quality-and-business-analytics)
56. [Data Quality Incident](#56-data-quality-incident)
57. [Root Cause Analysis](#57-root-cause-analysis)
58. [Data Quality Improvement Process](#58-data-quality-improvement-process)
59. [Data Quality Best Practices](#59-data-quality-best-practices)
60. [Real-World Example](#60-real-world-example)
61. [Interview Questions](#61-interview-questions)
62. [Final Revision](#62-final-revision)

---

# 1. What is Data Quality?

## Easy Definition

**Data quality means how suitable and trustworthy data is for its intended use.**

In simple terms:

> **Good-quality data is data that can be trusted for the purpose for which it is being used.**

---

## Example

Suppose a customer table contains:

| Customer_ID | Name  | Age | Email                                     |
| ----------- | ----- | --: | ----------------------------------------- |
| 101         | Ravi  |  25 | [ravi@gmail.com](mailto:ravi@gmail.com)   |
| 102         | Priya |  30 | [priya@gmail.com](mailto:priya@gmail.com) |
| 103         | Arun  |  -5 | [arun@gmail.com](mailto:arun@gmail.com)   |
| 104         | NULL  |  29 | NULL                                      |
| 104         | Arun  |  29 | [arun@gmail.com](mailto:arun@gmail.com)   |

Problems:

```text
Age = -5
Name = NULL
Email = NULL
Customer_ID = duplicate
```

Therefore, the dataset has data-quality problems.

---

# 2. Technical Definition

> **Data quality is the degree to which data possesses characteristics that make it accurate, complete, consistent, valid, unique, timely, relevant, reliable, and fit for its intended purpose.**

The exact dimensions used can vary by organization and use case.

---

# 3. Why Data Quality Matters

Data is the foundation of analytics.

```text
Data
 ↓
Analysis
 ↓
Insight
 ↓
Decision
```

If the data is poor:

```text
Poor Data
   ↓
Poor Analysis
   ↓
Wrong Insight
   ↓
Wrong Decision
```

This is often summarized as:

> **Garbage In → Garbage Out (GIGO)**

---

## Business Impact

Poor data quality can cause:

```text
Wrong revenue reports
Incorrect customer counts
Incorrect inventory levels
Wrong forecasting
Bad marketing decisions
Incorrect financial analysis
Poor customer segmentation
Incorrect ML predictions
Compliance problems
```

---

# 4. Data Quality in the Analytics Lifecycle

Data quality is not only a cleaning activity.

It should be considered throughout the lifecycle.

```text
Data Generation
      ↓
Data Collection
      ↓
Data Ingestion
      ↓
Data Storage
      ↓
Data Transformation
      ↓
Data Analysis
      ↓
Data Reporting
```

Quality problems can enter at any stage.

---

# 5. Data Quality vs Data Cleaning

These concepts are related but different.

| Data Quality                                    | Data Cleaning                                                             |
| ----------------------------------------------- | ------------------------------------------------------------------------- |
| Describes how good/suitable the data is         | Process of correcting or handling data problems                           |
| A condition/assessment                          | An activity/process                                                       |
| Includes accuracy, completeness, validity, etc. | Includes removing duplicates, handling missing values, correcting formats |
| Can be measured                                 | Can improve quality                                                       |
| Broader concept                                 | One component of data-quality management                                  |

### Example

```text
Data Quality Problem:
10% of customer emails are missing.

Data Cleaning:
Fill, remove, flag, or otherwise handle missing emails
according to the business rules.
```

---

# 6. Data Quality vs Data Validation

### Data Validation

Checks whether data satisfies predefined rules.

Example:

```text
Age must be >= 0
```

### Data Quality

Broader concept that includes:

```text
Accuracy
Completeness
Consistency
Validity
Uniqueness
Timeliness
Relevance
Reliability
```

Validation is therefore one mechanism for controlling or measuring data quality.

---

# 7. Data Quality Dimensions

The most important dimensions are:

```text
1. Accuracy
2. Completeness
3. Consistency
4. Validity
5. Uniqueness
6. Timeliness
7. Relevance
8. Integrity
9. Reliability
10. Precision
11. Granularity
12. Accessibility
13. Interpretability
```

Not every organization uses exactly the same list.

---

# 8. Accuracy

## Definition

> Accuracy measures whether data correctly represents the real-world entity, event, or value it is intended to represent.

---

## Example

Actual customer age:

```text
25
```

Database:

```text
25
```

Accurate.

But:

```text
Database = 52
Actual = 25
```

Inaccurate.

---

## Example

Actual product price:

```text
₹999
```

Database:

```text
₹999
```

Accurate.

Database:

```text
₹99
```

Inaccurate.

---

# 9. Completeness

## Definition

> Completeness measures whether required data is present.

Example:

| Customer | Email                             |
| -------- | --------------------------------- |
| A        | [a@gmail.com](mailto:a@gmail.com) |
| B        | NULL                              |
| C        | [c@gmail.com](mailto:c@gmail.com) |

One email is missing.

Completeness:

```text
2 / 3 × 100
= 66.67%
```

---

## Important

Missing data is not automatically an error.

For some variables, missingness may be legitimate.

Example:

```text
Middle_Name = NULL
```

may be perfectly acceptable.

Therefore:

> **Completeness must be evaluated against business requirements.**

---

# 10. Consistency

## Definition

> Consistency means that the same data does not contradict itself across records, systems, fields, or time.

---

## Example

System A:

```text
Customer_ID = 101
City = Hyderabad
```

System B:

```text
Customer_ID = 101
City = Mumbai
```

Potential inconsistency.

---

## Format Consistency

Bad:

```text
Male
M
male
MALE
```

Better standardized representation:

```text
Male
```

---

# 11. Validity

## Definition

> Validity means data conforms to its defined format, type, domain, range, or business rule.

---

## Example

Age:

```text
25 → Valid
35 → Valid
-10 → Invalid
```

---

## Date

```text
2026-08-08 → Valid
2026-99-99 → Invalid
```

---

## Category

Allowed:

```text
Male
Female
Other
```

Value:

```text
Unknown123
```

Potentially invalid depending on the defined domain.

---

# 12. Uniqueness

## Definition

> Uniqueness means that records or identifiers that should be unique are not unnecessarily duplicated.

Example:

```text
Customer_ID
101
102
103
101
```

Customer 101 appears twice.

---

## Important

Duplicate rows are not always errors.

For example:

A transaction table may legitimately contain multiple transactions for the same customer.

So uniqueness must be defined at the correct **key level**.

---

# 13. Timeliness

## Definition

> Timeliness measures whether data is available and current enough for its intended use.

Example:

A real-time fraud detection system needs very recent data.

A historical annual report may not require real-time data.

---

## Example

Required:

```text
Data freshness < 5 minutes
```

Actual:

```text
Last update = 4 hours ago
```

Quality problem for that use case.

---

# 14. Relevance

## Definition

> Relevance measures whether the data is appropriate and useful for the intended analytical or business purpose.

Example:

If analyzing customer churn, useful variables might include:

```text
Tenure
Usage
Subscription
Support interactions
Payment history
```

A completely unrelated field may add little value.

---

# 15. Integrity

## Definition

> Data integrity means data remains correct, consistent, and properly related throughout its lifecycle.

Important forms include:

```text
Entity Integrity
Referential Integrity
Domain Integrity
```

---

## Entity Integrity

Primary keys should uniquely identify records and generally cannot be NULL.

---

## Referential Integrity

Foreign keys should correctly reference existing parent records when the relationship requires it.

Example:

```text
Customer
   ↓
Customer_ID = 101

Order
   ↓
Customer_ID = 101
```

---

# 16. Reliability

## Definition

> Reliability refers to the degree to which data can be depended upon as a stable and trustworthy source for its intended purpose.

Example:

If a sensor produces:

```text
28.1
28.2
28.0
28.3
```

consistently under stable conditions, it may be more reliable than one producing erratic values.

---

# 17. Precision

## Definition

> Precision refers to the level of detail or exactness represented by a measurement.

Example:

```text
10
```

versus:

```text
10.2345
```

More decimal places do **not automatically mean more accuracy**.

This distinction is important:

```text
Accuracy  = closeness to the true value
Precision = level of detail/repeatability depending on context
```

---

# 18. Granularity

## Definition

> Granularity describes the level of detail represented by each record.

Example:

### Daily sales

```text
2026-08-01 → ₹50,000
```

### Transaction-level sales

```text
T001 → ₹500
T002 → ₹1,200
T003 → ₹300
```

Transaction-level data has finer granularity.

---

## Important

The appropriate granularity depends on the analytical question.

---

# 19. Accessibility

## Definition

> Accessibility refers to whether authorized users can obtain and use the data when needed.

Example:

A dataset may be high quality but inaccessible because:

```text
No authorized access
Broken pipeline
Missing credentials
Unavailable system
```

---

# 20. Interpretability

## Definition

> Interpretability means users can understand what the data represents and how it should be interpreted.

Example:

Bad:

```text
amount = 100
```

Questions:

```text
100 what?
USD?
INR?
Revenue?
Cost?
Quantity?
```

Better metadata:

```text
amount = 100
currency = INR
measure = net_sales
```

---

# 21. Data Quality Dimensions Compared

| Dimension        | Main Question                                     |
| ---------------- | ------------------------------------------------- |
| Accuracy         | Is it correct?                                    |
| Completeness     | Is required data present?                         |
| Consistency      | Does it agree across contexts?                    |
| Validity         | Does it follow the rules?                         |
| Uniqueness       | Are unintended duplicates absent?                 |
| Timeliness       | Is it current enough?                             |
| Relevance        | Is it useful for the purpose?                     |
| Integrity        | Are relationships and values preserved correctly? |
| Reliability      | Can we depend on it?                              |
| Precision        | Is the level of detail appropriate?               |
| Granularity      | Is the record-level detail appropriate?           |
| Accessibility    | Can authorized users access it?                   |
| Interpretability | Can users understand it?                          |

---

# 22. Common Data Quality Problems

Common problems include:

```text
Missing values
Duplicates
Incorrect values
Invalid values
Inconsistent formats
Outdated records
Wrong data types
Wrong units
Incorrect relationships
Incorrect timestamps
Truncated values
Encoding problems
Schema mismatches
```

---

# 23. Missing Data

Missing data occurs when an expected value is absent.

Example:

| Customer |  Age | Email                             |
| -------- | ---: | --------------------------------- |
| A        |   25 | [a@gmail.com](mailto:a@gmail.com) |
| B        | NULL | [b@gmail.com](mailto:b@gmail.com) |
| C        |   30 | NULL                              |

---

## Common Causes

```text
User did not provide value
Data not captured
System failure
Integration failure
Optional field
Privacy restriction
Measurement failure
```

---

## Missing Data Types

Statistical analysis often distinguishes:

### MCAR

**Missing Completely At Random**

Missingness is unrelated to observed or unobserved values.

### MAR

**Missing At Random**

Missingness may depend on observed variables after accounting for relevant factors.

### MNAR

**Missing Not At Random**

Missingness depends on the unobserved value itself or other unobserved factors.

These assumptions matter when choosing statistical methods for handling missing data.

---

# 24. Duplicate Data

Example:

```text
101 Ravi 25
101 Ravi 25
```

Potential duplicate.

But duplicates must be assessed using the correct business key.

Example:

```text
Customer_ID
```

may need to be unique.

But:

```text
Customer_ID + Order_ID
```

may define uniqueness in another table.

---

# 25. Incorrect Data

Incorrect data does not represent the real value.

Example:

Actual:

```text
Customer age = 25
```

Stored:

```text
Customer age = 52
```

Possible causes:

```text
Data entry error
Integration problem
Manual error
Transformation error
```

---

# 26. Invalid Data

Invalid data violates defined rules.

Example:

```text
Age = -10
```

If the rule is:

```text
Age >= 0
```

then it is invalid.

---

# 27. Inconsistent Data

Examples:

```text
Hyderabad
hyderabad
HYDERABAD
Hyd.
```

Another example:

```text
2026-08-08
08/08/2026
08-Aug-2026
```

Standardization can improve consistency.

---

# 28. Outdated Data

Example:

A customer changed their address six months ago, but the system still contains the old address.

The data may have been accurate when originally collected but is no longer current.

This shows:

> **Accuracy and timeliness are different dimensions.**

---

# 29. Inaccurate Data

Examples:

```text
Wrong customer name
Wrong price
Wrong address
Wrong age
Wrong product category
Wrong transaction amount
```

---

# 30. Data Type Problems

Example:

Age stored as:

```text
"25"
```

instead of:

```text
25
```

It may be represented as text rather than numeric data.

This can cause:

```text
Sorting problems
Arithmetic problems
Filtering problems
Database errors
```

---

# 31. Formatting Problems

Example:

```text
+91 9876543210
9876543210
+919876543210
```

All may represent the same phone number but have different formats.

Standardization may be required depending on the use case.

---

# 32. Referential Integrity Problems

Example:

Customer table:

```text
101
102
103
```

Order table:

```text
Customer_ID
101
102
999
```

Customer 999 does not exist.

This creates a referential integrity problem if every order must reference an existing customer.

---

# 33. Data Quality Metrics

Data quality should be measurable.

Common metrics:

```text
Completeness Rate
Validity Rate
Accuracy Rate
Duplicate Rate
Consistency Rate
Freshness
Error Rate
Null Rate
```

---

# 34. Completeness Rate

Formula:

```text
Completeness Rate =
Non-missing required values
---------------------------
Total required values
× 100
```

Example:

```text
Total records = 1,000
Records with email = 950

Completeness =
950 / 1000 × 100

= 95%
```

---

# 35. Validity Rate

Formula:

```text
Validity Rate =
Valid values
------------
Total values
× 100
```

Example:

```text
Valid ages = 980
Total ages = 1,000

Validity = 98%
```

---

# 36. Accuracy Rate

If ground truth or a trusted reference is available:

```text
Accuracy Rate =
Correct values
-------------
Checked values
× 100
```

Example:

```text
Correct = 970
Checked = 1000

Accuracy = 97%
```

---

# 37. Duplicate Rate

Example:

```text
Total records = 10,000
Unwanted duplicate records = 300
```

Duplicate rate:

```text
300 / 10000 × 100
= 3%
```

The exact definition should specify whether duplicates are counted as duplicate rows, duplicate entities, or duplicate keys.

---

# 38. Consistency Rate

Example:

```text
Records following standardized rules = 9,500
Total records = 10,000
```

```text
Consistency Rate =
9500 / 10000 × 100

= 95%
```

The actual rule must be clearly defined.

---

# 39. Timeliness Metrics

Timeliness can be measured using:

```text
Data age
Latency
Freshness
Update frequency
SLA compliance
```

Example:

Requirement:

```text
Data must be less than 15 minutes old.
```

Actual:

```text
Data age = 8 minutes
```

Pass.

---

# 40. Data Quality Rules

A **data quality rule** defines what acceptable data looks like.

Examples:

```text
customer_id IS NOT NULL
```

```text
age BETWEEN 0 AND 120
```

```text
order_amount >= 0
```

```text
order_date <= current_date
```

```text
email follows expected format
```

---

# 41. Data Validation Rules

Common rule categories:

## Required Field

```text
customer_id cannot be NULL
```

## Range

```text
age BETWEEN 0 AND 120
```

## Format

```text
email must follow expected format
```

## Domain

```text
status IN ('Active', 'Inactive')
```

## Uniqueness

```text
customer_id must be unique
```

## Referential

```text
customer_id must exist in customer table
```

## Cross-Field

Example:

```text
ship_date >= order_date
```

---

# 42. Data Profiling

## Definition

> Data profiling is the process of examining a dataset to understand its structure, content, patterns, distributions, and quality characteristics.

---

## Profiling Checks

```text
Number of rows
Number of columns
Data types
Null count
Unique count
Duplicate count
Minimum
Maximum
Mean
Median
Frequency
Distinct categories
Outliers
```

---

## Example

```text
Column: age

Type: integer
Rows: 100,000
Nulls: 1,200
Unique: 72
Min: 18
Max: 95
```

This gives an initial understanding of quality.

---

# 43. Data Quality Assessment

A quality assessment asks:

```text
Is the data accurate?
Is it complete?
Is it valid?
Is it consistent?
Is it unique?
Is it timely?
Is it relevant?
```

---

## Example

| Dimension    | Score |
| ------------ | ----: |
| Accuracy     |   97% |
| Completeness |   95% |
| Validity     |   99% |
| Uniqueness   |   98% |
| Timeliness   |   92% |

This provides a quality overview.

---

# 44. Data Quality Score

An organization may create a composite score.

Example:

```text
Quality Score =
0.30 × Accuracy
+ 0.25 × Completeness
+ 0.20 × Validity
+ 0.15 × Consistency
+ 0.10 × Timeliness
```

Weights should reflect business importance.

---

## Important

There is no universal formula for a single "data quality score."

Different organizations define scores differently.

---

# 45. Data Quality Framework

A practical framework:

```text
1. Define quality requirements
        ↓
2. Define rules
        ↓
3. Profile data
        ↓
4. Measure quality
        ↓
5. Identify issues
        ↓
6. Find root causes
        ↓
7. Correct/prevent issues
        ↓
8. Monitor continuously
```

---

# 46. Data Quality Monitoring

Data quality should not be checked only once.

Continuous monitoring can detect:

```text
Sudden null increase
Duplicate increase
Schema changes
Missing records
Invalid values
Delayed pipelines
Unexpected distributions
```

---

## Example

Normal:

```text
Null rate = 2%
```

Today:

```text
Null rate = 35%
```

This should trigger an investigation.

---

# 47. Data Quality Checks in SQL

## Find NULL values

```sql
SELECT COUNT(*) AS missing_email
FROM customers
WHERE email IS NULL;
```

---

## Find duplicates

```sql
SELECT
    customer_id,
    COUNT(*) AS count
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

---

## Find invalid ages

```sql
SELECT *
FROM customers
WHERE age < 0
   OR age > 120;
```

---

## Check allowed categories

```sql
SELECT *
FROM customers
WHERE status NOT IN ('Active', 'Inactive');
```

---

## Check referential integrity

```sql
SELECT o.*
FROM orders o
LEFT JOIN customers c
    ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

---

## Check future dates

```sql
SELECT *
FROM orders
WHERE order_date > CURRENT_DATE;
```

---

# 48. Data Quality Checks in Python

Using pandas:

```python
import pandas as pd

df = pd.read_csv("customers.csv")
```

---

## Check missing values

```python
df.isnull().sum()
```

---

## Check duplicates

```python
df.duplicated().sum()
```

---

## Check data types

```python
df.dtypes
```

---

## Check unique values

```python
df["status"].unique()
```

---

## Check invalid ages

```python
df[(df["age"] < 0) | (df["age"] > 120)]
```

---

## Check descriptive statistics

```python
df.describe()
```

---

# 49. Data Quality in ETL

ETL:

```text
Extract
   ↓
Transform
   ↓
Load
```

Quality checks can occur at each stage.

---

## Extract

Check:

```text
Source availability
Record count
Schema
Missing fields
```

---

## Transform

Check:

```text
Data types
Conversions
Business rules
Duplicates
Join results
```

---

## Load

Check:

```text
Row counts
Constraints
Referential integrity
Nulls
Duplicates
```

---

# 50. Data Quality in Data Warehouses

A data warehouse should maintain trustworthy analytical data.

Important checks:

```text
Schema consistency
Dimension integrity
Fact/dimension relationships
Duplicate keys
Missing keys
Metric definitions
Historical consistency
```

---

## Example

Fact table:

```text
sales
```

Dimension:

```text
customer
```

Every sales record should reference a valid customer according to the warehouse design.

---

# 51. Data Quality in Data Lakes

Data lakes may contain:

```text
Raw data
Semi-structured data
Structured data
Logs
Files
JSON
Images
Events
```

Quality challenges include:

```text
Schema drift
Duplicate files
Inconsistent formats
Missing metadata
Corrupted files
Mixed versions
```

---

# 52. Data Quality in APIs

API data may have:

```text
Missing fields
Unexpected fields
Invalid values
Rate-limit issues
Duplicate responses
Schema changes
Incorrect timestamps
Partial responses
```

Therefore API ingestion should include validation.

---

# 53. Data Quality in Machine Learning

ML models depend heavily on data quality.

Problems can include:

```text
Missing features
Incorrect labels
Data leakage
Outliers
Duplicate observations
Class imbalance
Sampling bias
Distribution shift
Inconsistent preprocessing
```

---

## Example

If customer churn labels are incorrect:

```text
Bad Labels
    ↓
Bad Training Data
    ↓
Bad Model
    ↓
Bad Predictions
```

---

# 54. Data Quality and Bias

Data quality problems can introduce or amplify bias.

Example:

Suppose an analytics system has complete records for urban customers but many missing records for rural customers.

The resulting analysis may disproportionately represent urban behavior.

Therefore:

> **Data quality is not only about technical correctness; it can also affect fairness and representativeness.**

---

# 55. Data Quality and Business Analytics

Business analytics depends on trustworthy metrics.

Example:

Company revenue dashboard shows:

```text
Revenue = ₹50 crore
```

But 8% of transactions were duplicated.

The reported revenue may be inflated.

---

## Business Metrics Affected

```text
Revenue
Profit
Conversion Rate
Customer Count
Churn Rate
Average Order Value
Customer Lifetime Value
Inventory
Sales Forecast
```

---

# 56. Data Quality Incident

A **data quality incident** is a significant event in which data fails defined quality expectations and potentially affects users, systems, decisions, or reports.

Example:

```text
08:00 → ETL pipeline runs
08:15 → Dashboard refreshes
08:30 → Null rate detected
08:45 → Business report affected
09:00 → Pipeline investigated
10:00 → Root cause identified
11:00 → Data corrected
```

---

# 57. Root Cause Analysis

Fixing the bad records is not always enough.

You should ask:

> **Why did the bad data occur?**

---

## Example

Problem:

```text
Customer emails suddenly became NULL.
```

Possible root cause:

```text
Source system changed field name
        ↓
ETL mapping failed
        ↓
Email column became NULL
        ↓
Warehouse loaded bad data
        ↓
Dashboard affected
```

---

## Root-Cause Categories

```text
Source system
Human error
Application bug
ETL failure
Schema change
Integration issue
Business process
Configuration error
```

---

# 58. Data Quality Improvement Process

```text
                 IDENTIFY
                    ↓
                  PROFILE
                    ↓
                  MEASURE
                    ↓
                PRIORITIZE
                    ↓
              ROOT-CAUSE ANALYSIS
                    ↓
                CORRECT DATA
                    ↓
              FIX SOURCE/PROCESS
                    ↓
                 VALIDATE
                    ↓
                 MONITOR
```

---

# 59. Data Quality Best Practices

## 1. Define quality requirements

Know what "good data" means for the use case.

---

## 2. Define data owners

Someone should be responsible for important datasets.

---

## 3. Create quality rules

Example:

```text
customer_id cannot be NULL
```

---

## 4. Validate as early as possible

Catch problems near the source.

---

## 5. Automate quality checks

Avoid relying entirely on manual inspection.

---

## 6. Monitor continuously

Track quality over time.

---

## 7. Track trends

Example:

```text
Null rate

Jan → 2%
Feb → 3%
Mar → 4%
Apr → 18%
```

The sudden increase is a warning signal.

---

## 8. Fix root causes

Do not repeatedly clean the same problem downstream if the source process can be fixed.

---

## 9. Document assumptions

Record:

```text
Definitions
Rules
Sources
Limitations
Transformations
```

---

## 10. Prioritize business impact

Not every quality issue has equal importance.

Example:

```text
Missing middle name → Low impact
Wrong transaction amount → High impact
```

---

# 60. Real-World Example

Consider an e-commerce customer dataset:

| ID  | Name  |  Age | Email                                     | Status | Revenue |
| --- | ----- | ---: | ----------------------------------------- | ------ | ------: |
| 101 | Ravi  |   25 | [ravi@gmail.com](mailto:ravi@gmail.com)   | Active |    5000 |
| 102 | Priya | NULL | [priya@gmail.com](mailto:priya@gmail.com) | Active |    3000 |
| 103 | Arun  |   -5 | [arun@gmail.com](mailto:arun@gmail.com)   | Active |    2000 |
| 101 | Ravi  |   25 | [ravi@gmail.com](mailto:ravi@gmail.com)   | Active |    5000 |
| 104 | Kiran |   32 | NULL                                      | active |    4000 |

---

## Problems

### Completeness

```text
Age missing for ID 102
Email missing for ID 104
```

### Validity

```text
Age = -5
```

### Uniqueness

```text
ID 101 appears twice
```

### Consistency

```text
Active
active
```

### Accuracy

Cannot be established merely by inspecting the table; it requires comparison with a trusted source or ground truth.

---

## Possible Cleaning

```text
Handle missing age
Handle missing email
Investigate negative age
Remove or resolve unintended duplicate
Standardize status
```

---

# 61. Data Quality vs Data Quantity

A large dataset is not automatically a high-quality dataset.

```text
1,000,000 bad records
```

may be less useful than:

```text
100,000 trustworthy records
```

---

## Important Principle

> **Quality is more important than simply having more data.**

However, the required balance between quality, coverage, quantity, and cost depends on the analytical objective.

---

# 62. Data Quality vs Data Accuracy

These are not identical.

### Accuracy

Is the value correct?

### Data Quality

Is the data suitable overall?

Example:

```text
Age = 25
```

may be accurate.

But if:

```text
Email = NULL
Address = outdated
Customer ID = duplicate
```

the dataset can still have poor overall quality.

---

# 63. Data Quality vs Data Completeness

Completeness is only **one dimension** of quality.

Example:

```text
100% complete
```

does not mean:

```text
100% accurate
```

A dataset can have every field populated but contain incorrect values.

---

# 64. Data Quality vs Data Consistency

Consistency asks:

> Do related representations agree?

Example:

```text
System A → Customer Status = Active
System B → Customer Status = Inactive
```

The data may be complete in both systems but inconsistent.

---

# 65. Data Quality vs Data Validity

A value can be valid but inaccurate.

Example:

```text
Allowed age range = 0–120

Database = 52
Actual age = 25
```

52 is:

```text
Valid → Yes
Accurate → No
```

This is an important interview concept.

---

# 66. Data Quality vs Data Timeliness

A value can be accurate but outdated.

Example:

```text
Customer address:
Old address = correct historically
Current address = different
```

The old address may be accurate historically but not timely for current operations.

---

# 67. Quality Gates

A **quality gate** is a checkpoint that prevents or flags data from moving forward when defined quality conditions are not met.

Example:

```text
Incoming Data
      ↓
Quality Gate
      ↓
Completeness >= 95%?
      ↓
   YES / NO
      ↓
Warehouse
```

---

# 68. Quality Thresholds

Organizations can define acceptable limits.

Example:

```text
Null rate < 5%
Duplicate rate < 1%
Validity rate > 99%
Freshness < 30 minutes
```

If a threshold is violated:

```text
Alert
↓
Investigate
↓
Correct
```

---

# 69. Data Quality Dashboard

A quality dashboard may show:

```text
Dataset: Customers

Completeness     97%
Validity         99%
Uniqueness       98%
Consistency      95%
Freshness        100%
```

It may also show trends:

```text
Quality Score
      ↑
100% |             ●
 95% |       ●  ●
 90% |    ●
 85% | ●
      └────────────────
        Jan Feb Mar Apr
```

---

# 70. Advanced Concept — Data Observability

**Data observability** is the ability to understand the health and behavior of data systems through monitoring and diagnostics.

It can include:

```text
Freshness
Volume
Schema
Distribution
Lineage
Quality
```

---

## Example

A pipeline normally produces:

```text
10 million records/day
```

Today:

```text
2 million records
```

Volume monitoring can detect the anomaly.

---

# 71. Advanced Concept — Schema Drift

Schema drift occurs when the structure of incoming data changes unexpectedly.

Example:

Yesterday:

```text
customer_id
name
email
```

Today:

```text
customer_id
full_name
email_address
```

The pipeline may fail or silently produce incorrect results if it expects the old schema.

---

# 72. Advanced Concept — Data Drift

Data drift refers to changes in the distribution or characteristics of data over time.

Example:

Historical:

```text
Average order value = ₹1,000
```

Current:

```text
Average order value = ₹1,700
```

This could be legitimate business change or a data problem.

Investigation is required.

---

# 73. Advanced Concept — Data Lineage

Data lineage tracks where data came from and how it changed.

Example:

```text
CRM
 ↓
ETL
 ↓
Staging
 ↓
Warehouse
 ↓
Data Mart
 ↓
Dashboard
```

If a dashboard metric is wrong, lineage helps identify the upstream source and transformations involved.

---

# 74. Advanced Concept — Data Contracts

A data contract is an explicit agreement between data producers and consumers about expectations for shared data.

It can define:

```text
Schema
Data types
Required fields
Allowed values
Ownership
Freshness expectations
Quality requirements
Change procedures
```

Example:

```text
customer_id → integer → required
email       → string  → optional
created_at  → timestamp → required
```

---

# 75. Advanced Concept — Master Data

Master data represents important core business entities.

Examples:

```text
Customer
Product
Supplier
Employee
Location
```

Poor master data can cause:

```text
Duplicate customers
Duplicate products
Incorrect reporting
Incorrect joins
```

---

# 76. Advanced Concept — Reference Data

Reference data provides standardized values used across systems.

Example:

```text
Country Codes
Currency Codes
Product Categories
Status Codes
```

Instead of:

```text
India
IND
IN
Bharat
```

a system may define a standard representation.

---

# 77. Data Quality Architecture

A mature organization may use:

```text
              DATA SOURCES
                   ↓
             DATA INGESTION
                   ↓
            QUALITY CHECKS
                   ↓
             RAW/STAGING
                   ↓
          TRANSFORMATION
                   ↓
          QUALITY VALIDATION
                   ↓
             DATA WAREHOUSE
                   ↓
             DATA MARTS
                   ↓
              ANALYTICS
                   ↓
             DASHBOARDS
```

Quality monitoring operates across multiple stages.

---

# 78. Complete Data Quality Checklist

Before using a dataset, ask:

### Accuracy

```text
Are the values correct?
```

### Completeness

```text
Are required values present?
```

### Consistency

```text
Do values agree across systems?
```

### Validity

```text
Do values follow defined rules?
```

### Uniqueness

```text
Are unintended duplicates present?
```

### Timeliness

```text
Is the data current enough?
```

### Relevance

```text
Does it answer the intended question?
```

### Integrity

```text
Are relationships preserved?
```

### Reliability

```text
Can the source be trusted?
```

### Interpretability

```text
Do we understand the meaning of the fields?
```

---

# 79. Interview Questions

## Beginner

### Q1. What is data quality?

Data quality is the degree to which data is accurate, complete, consistent, valid, timely, unique, relevant, reliable, and fit for its intended purpose.

---

### Q2. What are the main dimensions of data quality?

```text
Accuracy
Completeness
Consistency
Validity
Uniqueness
Timeliness
Relevance
Integrity
Reliability
```

---

### Q3. What is the difference between accuracy and validity?

```text
Accuracy → Is the value correct?

Validity → Does the value follow the defined rules?
```

Example:

```text
Actual age = 25
Stored age = 52
Allowed range = 0–120
```

52 is valid but inaccurate.

---

### Q4. What is completeness?

The degree to which required data values are present.

---

### Q5. What is data consistency?

The degree to which data agrees across records, systems, fields, or time.

---

### Q6. What is data uniqueness?

The degree to which entities or records that should be unique are not unnecessarily duplicated.

---

### Q7. What is data profiling?

Examining a dataset to understand its structure, distributions, patterns, and quality characteristics.

---

### Q8. How do you improve data quality?

```text
Profile
↓
Define rules
↓
Measure
↓
Identify issues
↓
Find root causes
↓
Clean/correct
↓
Improve source processes
↓
Validate
↓
Monitor
```

---

# 80. Advanced Interview Questions

## Q1. Can data be complete but inaccurate?

**Yes.**

Every field can be populated while values are incorrect.

---

## Q2. Can data be valid but inaccurate?

**Yes.**

Example:

```text
Allowed age = 0–120
Stored age = 52
Actual age = 25
```

52 is valid but inaccurate.

---

## Q3. Can data be accurate but not timely?

**Yes.**

A customer's old address may have been accurate but is no longer current.

---

## Q4. Does removing duplicates always improve data quality?

**No.**

You must determine whether the records are truly unintended duplicates.

Multiple transactions from the same customer are legitimate.

---

## Q5. Does filling all NULL values improve data quality?

**No.**

Blindly filling missing values can introduce incorrect information.

The treatment depends on:

```text
Why data is missing
Variable meaning
Business rules
Statistical assumptions
Analytical purpose
```

---

## Q6. Why is data quality important in machine learning?

Because incorrect, incomplete, biased, or inconsistent training data can produce unreliable models and predictions.

---

# 81. Final Revision

## 🔥 Data Quality = Fitness for Intended Use

Remember:

```text
                DATA QUALITY
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   ACCURACY     COMPLETENESS   CONSISTENCY
       ↓             ↓             ↓
    Correct?      Present?       Agree?
       │             │             │
       └─────────────┼─────────────┘
                     ↓
                  VALIDITY
                     ↓
                Follows Rules?
                     ↓
                 UNIQUENESS
                     ↓
               No Unwanted Duplicates?
                     ↓
                 TIMELINESS
                     ↓
                  Current?
                     ↓
                  RELEVANCE
                     ↓
                 Useful?
```

---

# 🧠 Most Important Concepts

| Concept            | Meaning                                             |
| ------------------ | --------------------------------------------------- |
| **Accuracy**       | Data represents the correct real-world value        |
| **Completeness**   | Required data is present                            |
| **Consistency**    | Data does not contradict itself                     |
| **Validity**       | Data follows defined rules                          |
| **Uniqueness**     | Unintended duplicates are absent                    |
| **Timeliness**     | Data is current enough                              |
| **Relevance**      | Data is useful for the intended purpose             |
| **Integrity**      | Data and relationships remain correct               |
| **Reliability**    | Data can be depended upon                           |
| **Granularity**    | Level of detail in the data                         |
| **Data Profiling** | Examining data to understand quality                |
| **Validation**     | Checking data against rules                         |
| **Data Cleaning**  | Correcting/handling data problems                   |
| **Monitoring**     | Continuously tracking data quality                  |
| **Data Lineage**   | Tracking data from source to destination            |
| **Data Contract**  | Agreement about expected data structure and quality |

---

# ⭐ Final Mental Model

```text
                 DATA QUALITY
                      │
                      ↓
               IS THE DATA...
                      │
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
     ACCURATE      COMPLETE      CONSISTENT
        │             │             │
        ↓             ↓             ↓
      VALID        UNIQUE        TIMELY
        │             │             │
        └─────────────┼─────────────┘
                      ↓
                   RELEVANT
                      ↓
                  TRUSTWORTHY
                      ↓
               FIT FOR PURPOSE
                      ↓
                BUSINESS VALUE
```

> **The most important idea:** Data quality is not simply about having clean data. It is about whether the data is **fit for the specific purpose for which it will be used**. A dataset can be complete but inaccurate, valid but inaccurate, accurate but outdated, or clean but irrelevant. Good data-quality management therefore combines **measurement, validation, cleaning, documentation, governance, root-cause correction, and continuous monitoring**.
