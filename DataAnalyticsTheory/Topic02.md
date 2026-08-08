# 📊 Types of Data, Measurement Scales & Data Sources

> Complete beginner-to-advanced revision notes for Data Analytics.

---

# 📚 Table of Contents

1. [What is Data?](#1-what-is-data)
2. [Why Data Classification Matters](#2-why-data-classification-matters)
3. [Types of Data - Overview](#3-types-of-data---overview)
4. [Qualitative Data](#4-qualitative-data)
5. [Quantitative Data](#5-quantitative-data)
6. [Qualitative vs Quantitative Data](#6-qualitative-vs-quantitative-data)
7. [Categorical Data](#7-categorical-data)
8. [Numerical Data](#8-numerical-data)
9. [Discrete Data](#9-discrete-data)
10. [Continuous Data](#10-continuous-data)
11. [Categorical vs Numerical Data](#11-categorical-vs-numerical-data)
12. [Structured Data](#12-structured-data)
13. [Semi-Structured Data](#13-semi-structured-data)
14. [Unstructured Data](#14-unstructured-data)
15. [Structured vs Semi-Structured vs Unstructured](#15-structured-vs-semi-structured-vs-unstructured)
16. [Primary and Secondary Data](#16-primary-and-secondary-data)
17. [Cross-Sectional Data](#17-cross-sectional-data)
18. [Time-Series Data](#18-time-series-data)
19. [Panel / Longitudinal Data](#19-panel--longitudinal-data)
20. [Measurement Scales](#20-measurement-scales)
21. [Nominal Scale](#21-nominal-scale)
22. [Ordinal Scale](#22-ordinal-scale)
23. [Interval Scale](#23-interval-scale)
24. [Ratio Scale](#24-ratio-scale)
25. [Measurement Scales Comparison](#25-measurement-scales-comparison)
26. [Qualitative Data and Measurement Scales](#26-qualitative-data-and-measurement-scales)
27. [Quantitative Data and Measurement Scales](#27-quantitative-data-and-measurement-scales)
28. [Data Sources](#28-data-sources)
29. [Primary Data Sources](#29-primary-data-sources)
30. [Secondary Data Sources](#30-secondary-data-sources)
31. [Internal Data Sources](#31-internal-data-sources)
32. [External Data Sources](#32-external-data-sources)
33. [Human-Generated Data](#33-human-generated-data)
34. [Machine-Generated Data](#34-machine-generated-data)
35. [Transactional Data](#35-transactional-data)
36. [Operational Data](#36-operational-data)
37. [Web and Digital Data](#37-web-and-digital-data)
38. [Public and Government Data](#38-public-and-government-data)
39. [Survey Data](#39-survey-data)
40. [Experimental Data](#40-experimental-data)
41. [Database Data](#41-database-data)
42. [API Data](#42-api-data)
43. [File-Based Data](#43-file-based-data)
44. [Cloud Data Sources](#44-cloud-data-sources)
45. [Big Data Sources](#45-big-data-sources)
46. [Data Source Selection](#46-data-source-selection)
47. [Data Quality Dimensions](#47-data-quality-dimensions)
48. [Data Source vs Data Type](#48-data-source-vs-data-type)
49. [Complete Classification](#49-complete-classification)
50. [Real-World Example](#50-real-world-example)
51. [Quick Revision](#51-quick-revision)

---

# 1. What is Data?

## Easy Definition

**Data is a collection of facts, observations, measurements, values, or records.**

Example:

```text
25
Hyderabad
₹50,000
Male
Electronics
2026-08-08
```

These are individual pieces of data.

A complete customer record could be:

| Customer | Age | City      |  Income | Product |
| -------- | --: | --------- | ------: | ------- |
| Ravi     |  25 | Hyderabad | ₹50,000 | Laptop  |

---

## Technical Definition

> Data is a representation of facts, observations, measurements, or entities that can be collected, stored, processed, analyzed, and interpreted.

---

# 2. Why Data Classification Matters

Before analyzing data, we need to understand what type of data we have.

Different data types require different:

* statistical methods
* visualizations
* storage methods
* preprocessing techniques
* machine-learning algorithms
* mathematical operations

For example:

```text
Gender → Categorical
Age → Numerical
Customer Rating → Ordinal
Temperature in Celsius → Interval
Income → Ratio
```

You should **not treat all variables the same way**.

---

# 3. Types of Data - Overview

Data can be classified in several different ways.

The important classifications are:

```text
DATA
│
├── By Nature
│   ├── Qualitative
│   └── Quantitative
│
├── By Value Structure
│   ├── Categorical
│   └── Numerical
│       ├── Discrete
│       └── Continuous
│
├── By Organization
│   ├── Structured
│   ├── Semi-Structured
│   └── Unstructured
│
├── By Collection
│   ├── Primary
│   └── Secondary
│
├── By Time Dimension
│   ├── Cross-Sectional
│   ├── Time-Series
│   └── Panel / Longitudinal
│
└── By Source
    ├── Internal
    └── External
```

These classifications are **not mutually exclusive**.

For example:

> Monthly sales from a company's database

can simultaneously be:

```text
Quantitative
Numerical
Continuous or discrete depending on the variable
Structured
Internal
Transactional
Time-series
```

---

# 4. Qualitative Data

## Easy Definition

Qualitative data describes **qualities, characteristics, categories, or attributes**.

It generally answers:

> **What kind?**

Examples:

```text
Color = Red
Gender = Female
City = Hyderabad
Product Category = Electronics
Customer Type = Premium
Feedback = Excellent
```

---

## Technical Definition

> Qualitative data is non-numeric or categorical information representing attributes, characteristics, labels, or categories of observations.

---

## Examples

| Variable         | Values             |
| ---------------- | ------------------ |
| Color            | Red, Blue, Green   |
| Department       | HR, Sales, IT      |
| City             | Hyderabad, Chennai |
| Product Type     | Laptop, Phone      |
| Customer Segment | Premium, Standard  |

---

## Important

Qualitative data can sometimes be represented using numbers.

Example:

```text
1 = Male
2 = Female
3 = Other
```

The numbers are **codes**, not quantities.

You cannot meaningfully calculate:

```text
1 + 2 = 3
```

because the codes represent categories.

---

# 5. Quantitative Data

## Easy Definition

Quantitative data represents **numbers or measurable quantities**.

It answers:

> **How much?**

Examples:

```text
Age = 25
Salary = ₹50,000
Height = 175.5 cm
Sales = ₹10,00,000
Orders = 500
```

---

## Technical Definition

> Quantitative data is numerical data representing measurable quantities on which arithmetic or statistical operations can meaningfully be performed, subject to the measurement scale.

---

## Examples

| Variable |   Value |
| -------- | ------: |
| Age      |      25 |
| Salary   |   50000 |
| Height   |   175.5 |
| Orders   |     500 |
| Revenue  | 1000000 |

---

# 6. Qualitative vs Quantitative Data

| Qualitative          | Quantitative          |
| -------------------- | --------------------- |
| Describes categories | Represents quantities |
| Usually non-numeric  | Numeric               |
| Answers "what kind?" | Answers "how much?"   |
| Color                | Age                   |
| City                 | Income                |
| Product category     | Revenue               |
| Gender               | Number of orders      |

---

# 7. Categorical Data

## Definition

> Categorical data represents observations belonging to distinct groups or categories.

Examples:

```text
Department
Gender
Country
Product Category
Customer Segment
Payment Method
```

---

## Example

| Customer | Payment Method |
| -------- | -------------- |
| A        | Cash           |
| B        | Card           |
| C        | UPI            |
| D        | Card           |

Payment method is categorical.

---

## Two Important Types

```text
Categorical
├── Nominal
└── Ordinal
```

---

# 8. Numerical Data

Numerical data represents numbers that quantify observations.

Examples:

```text
Age
Salary
Weight
Revenue
Quantity
Temperature
Distance
```

Numerical data is commonly divided into:

```text
Numerical
├── Discrete
└── Continuous
```

---

# 9. Discrete Data

## Definition

> Discrete data consists of countable values, usually whole numbers.

Examples:

```text
Number of customers = 100
Number of orders = 50
Number of employees = 250
Number of complaints = 7
```

You generally cannot have:

```text
2.5 customers
3.7 employees
```

---

## Key Characteristic

Discrete data is usually generated through **counting**.

```text
Number of orders
Number of students
Number of products
Number of calls
```

---

# 10. Continuous Data

## Definition

> Continuous data can take any value within a range and is typically obtained through measurement.

Examples:

```text
Height = 175.43 cm
Weight = 68.72 kg
Temperature = 36.7°C
Distance = 10.543 km
Time = 5.238 seconds
```

---

## Key Characteristic

Continuous data is usually generated through **measurement**.

```text
COUNTING → DISCRETE
MEASURING → CONTINUOUS
```

---

# 11. Categorical vs Numerical Data

| Categorical       | Numerical             |
| ----------------- | --------------------- |
| Represents groups | Represents quantities |
| Usually labels    | Measurements/counts   |
| Gender            | Age                   |
| City              | Salary                |
| Product type      | Revenue               |
| Payment method    | Quantity              |
| Department        | Height                |

---

# 12. Structured Data

## Easy Definition

Structured data is data organized in a predefined format, usually rows and columns.

Example:

| ID | Name  | Age | Salary |
| -: | ----- | --: | -----: |
|  1 | Ravi  |  25 |  50000 |
|  2 | Priya |  30 |  60000 |

---

## Technical Definition

> Structured data conforms to a predefined schema and can be stored and queried efficiently using tabular or relational structures.

---

## Examples

```text
SQL Tables
Excel Sheets
CSV Files
Relational Databases
```

---

## Advantages

```text
Easy to query
Easy to analyze
Easy to validate
Easy to aggregate
Compatible with SQL
```

---

# 13. Semi-Structured Data

Semi-structured data does not follow a strict tabular schema but contains organizational elements such as keys, tags, or metadata.

Examples:

```text
JSON
XML
HTML
Email
```

Example JSON:

```json
{
  "name": "Ravi",
  "age": 25,
  "city": "Hyderabad"
}
```

The structure exists, but it is not necessarily a fixed relational table.

---

# 14. Unstructured Data

## Definition

> Unstructured data does not follow a predefined tabular or rigid data model.

Examples:

```text
Images
Videos
Audio
PDF Documents
Text Documents
Social Media Posts
Emails
```

---

## Example

A customer review:

```text
"The product is excellent, but delivery was very late."
```

This is primarily unstructured text.

---

# 15. Structured vs Semi-Structured vs Unstructured

| Feature      | Structured    | Semi-Structured                   | Unstructured                    |
| ------------ | ------------- | --------------------------------- | ------------------------------- |
| Schema       | Fixed         | Flexible                          | No predefined tabular schema    |
| Rows/Columns | Yes           | Not necessarily                   | No                              |
| SQL querying | Easy          | Possible with appropriate systems | Requires specialized processing |
| Example      | SQL table     | JSON                              | Image                           |
| Storage      | Relational DB | Document stores/files             | Object/file storage             |

---

# 16. Primary and Secondary Data

Another important classification is based on **how the data was obtained**.

```text
DATA
├── Primary Data
└── Secondary Data
```

---

# 17. Primary Data

## Definition

> Primary data is data collected directly by the researcher or organization for a specific purpose.

Examples:

```text
Surveys
Interviews
Experiments
Observations
Questionnaires
User testing
```

---

## Example

A company wants to know:

> "Why are customers unhappy?"

It conducts a survey with 5,000 customers.

The collected responses are **primary data**.

---

## Advantages

```text
Specific to objective
Current
Controlled collection
Relevant
```

---

## Disadvantages

```text
Expensive
Time-consuming
Requires planning
Potential response bias
```

---

# 18. Secondary Data

## Definition

> Secondary data is data originally collected by another person or organization or previously collected for a different purpose and subsequently reused.

Examples:

```text
Government datasets
Published research
Company reports
Public databases
Historical records
Industry reports
Existing organizational data
```

---

## Advantages

```text
Less expensive
Faster to obtain
Large datasets may already exist
Useful for background research
```

---

## Disadvantages

```text
May not match the exact objective
Potential quality issues
May be outdated
Unknown collection methodology
Potential licensing restrictions
```

---

# 19. Cross-Sectional Data

## Definition

> Cross-sectional data contains observations from multiple entities at approximately one point or period in time.

Example:

A survey of 1,000 customers in August 2026:

| Customer | Age | Income | Satisfaction |
| -------- | --: | -----: | -----------: |
| A        |  25 |  40000 |            4 |
| B        |  30 |  60000 |            5 |
| C        |  28 |  50000 |            3 |

This compares different entities at the same time.

---

## Use

Useful for:

```text
Customer surveys
Population studies
Market research
Comparing regions
Comparing companies
```

---

# 20. Time-Series Data

## Definition

> Time-series data consists of observations recorded sequentially over time, usually at regular or identifiable time intervals.

Example:

| Month | Revenue |
| ----- | ------: |
| Jan   |  100000 |
| Feb   |  120000 |
| Mar   |  150000 |
| Apr   |  140000 |

---

## Used For

```text
Trend Analysis
Forecasting
Seasonality
Demand Analysis
Financial Analysis
```

---

# 21. Panel / Longitudinal Data

## Definition

> Panel or longitudinal data tracks multiple entities repeatedly over time.

Example:

| Customer | Month | Spending |
| -------- | ----- | -------: |
| A        | Jan   |      500 |
| A        | Feb   |      700 |
| A        | Mar   |      600 |
| B        | Jan   |      300 |
| B        | Feb   |      400 |
| B        | Mar   |      450 |

It combines:

```text
Cross-sectional dimension
+
Time dimension
```

---

# 22. Measurement Scales

Measurement scales describe **what the values of a variable mean and what mathematical comparisons are valid**.

The four classical measurement scales are:

```text
1. Nominal
2. Ordinal
3. Interval
4. Ratio
```

Remember:

```text
N → O → I → R
```

or:

> **Nominal → Ordinal → Interval → Ratio**

As we move from Nominal to Ratio, the mathematical information available generally increases.

---

# 23. Nominal Scale

## Easy Definition

Nominal data is used to **name or label categories**.

There is no inherent order.

Examples:

```text
Gender
Blood Group
Country
Color
Department
Payment Method
Product Category
```

---

## Example

```text
Payment Method:

Cash
Card
UPI
Net Banking
```

There is no natural ranking:

```text
UPI > Card
```

doesn't make sense.

---

## Properties

```text
✓ Categories
✓ Labels
✗ No ranking
✗ No meaningful differences
✗ No meaningful ratios
```

---

## Valid Operations

You can calculate:

```text
Frequency
Count
Mode
Proportion
Percentage
```

Example:

```text
UPI = 500 customers
Card = 300 customers
Cash = 200 customers
```

---

# 24. Ordinal Scale

## Easy Definition

Ordinal data has categories with a **meaningful order or ranking**.

Examples:

```text
Poor
Average
Good
Excellent
```

There is an order:

```text
Poor < Average < Good < Excellent
```

But the exact distance between categories is not necessarily known or equal.

---

## Examples

### Customer Satisfaction

```text
1 = Very Dissatisfied
2 = Dissatisfied
3 = Neutral
4 = Satisfied
5 = Very Satisfied
```

### Education Level

```text
High School
Bachelor's
Master's
Doctorate
```

---

## Properties

```text
✓ Categories
✓ Ranking
✗ Equal intervals not guaranteed
✗ Ratio interpretation generally invalid
```

---

## Valid Operations

Commonly:

```text
Frequency
Mode
Median
Percentiles/ranks
Order comparisons
```

Arithmetic operations require caution because category spacing may not be equal.

---

# 25. Interval Scale

## Definition

> Interval data has ordered values with meaningful and equal intervals, but zero does not represent an absolute absence of the measured quantity.

Classic examples:

```text
Temperature in Celsius
Temperature in Fahrenheit
Calendar years
```

---

## Example

Consider Celsius:

```text
10°C
20°C
30°C
```

The difference between:

```text
10°C and 20°C = 10°C
20°C and 30°C = 10°C
```

The intervals are equal.

But:

```text
0°C
```

does not mean "no temperature."

Therefore:

```text
20°C is NOT twice as hot as 10°C
```

---

## Properties

```text
✓ Categories/order
✓ Meaningful differences
✓ Equal intervals
✗ No absolute zero
✗ Ratios are not generally meaningful
```

---

## Common Operations

```text
Mean
Median
Standard Deviation
Addition/subtraction of differences
Correlation
Regression
```

---

# 26. Ratio Scale

## Definition

> Ratio data has ordered values, equal intervals, and a meaningful absolute zero, allowing meaningful ratio comparisons.

Examples:

```text
Age
Height
Weight
Distance
Income
Revenue
Sales Quantity
Duration
```

---

## Example

```text
Income A = ₹20,000
Income B = ₹40,000
```

We can meaningfully say:

> B's income is twice A's income.

Because income has a meaningful zero and ratios are meaningful.

---

## Properties

```text
✓ Categories/order
✓ Equal intervals
✓ Absolute zero
✓ Meaningful differences
✓ Meaningful ratios
```

---

## Mathematical Operations

Most standard arithmetic operations are meaningful:

```text
+
-
×
÷
```

and many statistical procedures can be applied depending on assumptions.

---

# 27. Measurement Scales Comparison

| Property              | Nominal |         Ordinal | Interval | Ratio |
| --------------------- | ------: | --------------: | -------: | ----: |
| Categories            |       ✓ |               ✓ |        ✓ |     ✓ |
| Order                 |       ✗ |               ✓ |        ✓ |     ✓ |
| Equal intervals       |       ✗ |  Not guaranteed |        ✓ |     ✓ |
| Absolute zero         |       ✗ |               ✗ |        ✗ |     ✓ |
| Meaningful difference |       ✗ | Not necessarily |        ✓ |     ✓ |
| Meaningful ratio      |       ✗ |               ✗ |        ✗ |     ✓ |

---

# 28. Qualitative Data and Measurement Scales

Qualitative/categorical variables are commonly associated with:

```text
Nominal
Ordinal
```

Examples:

### Nominal

```text
Color
Country
Gender
Department
```

### Ordinal

```text
Satisfaction
Education Level
Risk Level
Service Rating
```

---

# 29. Quantitative Data and Measurement Scales

Quantitative variables commonly use:

```text
Interval
Ratio
```

Examples:

### Interval

```text
Temperature in Celsius
Calendar Year
```

### Ratio

```text
Age
Height
Weight
Revenue
Income
Distance
```

---

# 30. Data Sources

A **data source** is the origin from which data is obtained.

Examples:

```text
Database
Survey
API
Website
Sensor
Transaction System
Government Portal
Mobile Application
Social Media
```

---

# 31. Primary Data Sources

Common primary sources include:

## Surveys

Collect responses directly from participants.

Example:

```text
Customer Satisfaction Survey
```

---

## Interviews

Data is collected through direct conversations.

Useful for:

```text
Opinions
Experiences
Motivations
Qualitative research
```

---

## Experiments

Data is generated under controlled conditions.

Example:

```text
A/B Testing
```

---

## Observations

Researchers directly observe behavior.

Example:

```text
Customers' movement inside a store
```

---

# 32. Secondary Data Sources

Examples:

```text
Government publications
Research papers
Industry reports
Public datasets
Historical databases
Existing company records
Published statistics
```

---

# 33. Internal Data Sources

Internal data originates **within an organization**.

Examples:

```text
Sales Database
CRM
ERP
Finance System
HR System
Inventory System
Website Analytics
Customer Support
```

---

## Example

An e-commerce company may have:

```text
Customers
Orders
Payments
Products
Returns
Inventory
```

All of these are internal sources.

---

# 34. External Data Sources

External data originates **outside the organization**.

Examples:

```text
Government Data
Market Data
Economic Indicators
Weather Data
Public APIs
Industry Reports
Social Media
Third-Party Providers
```

---

# 35. Human-Generated Data

Data created directly by people.

Examples:

```text
Survey Responses
Reviews
Social Media Posts
Emails
Documents
Forms
Interviews
```

---

# 36. Machine-Generated Data

Data automatically generated by machines, software, or devices.

Examples:

```text
Sensor Data
Server Logs
GPS Data
Application Logs
IoT Data
Machine Telemetry
Clickstream Events
```

---

# 37. Transactional Data

Transactional data records business transactions or events.

Examples:

```text
Orders
Payments
Refunds
Purchases
Bank Transactions
Bookings
```

Example:

| Transaction ID | Customer | Amount |
| -------------- | -------- | -----: |
| T001           | C001     |    500 |
| T002           | C002     |   1200 |
| T003           | C001     |    800 |

---

# 38. Operational Data

Operational data is generated during routine business operations.

Examples:

```text
Inventory
Employee Records
Orders
Shipments
Production
Customer Support
```

Operational data is often used by systems that run the business.

---

# 39. Web and Digital Data

Digital platforms generate large quantities of data.

Examples:

```text
Website Visits
Page Views
Clicks
Sessions
Search Queries
Ad Impressions
Conversions
App Events
```

---

## Clickstream Data

Clickstream data records users' interactions with websites or applications.

Example:

```text
Homepage
   ↓
Product Page
   ↓
Add to Cart
   ↓
Checkout
   ↓
Payment
```

This is especially useful for:

```text
Funnel Analysis
Conversion Analysis
User Behavior Analysis
```

---

# 40. Public and Government Data

Government organizations publish datasets such as:

```text
Population
Census
Economic Indicators
Employment
Education
Healthcare
Transportation
Weather
```

These can be used for:

```text
Research
Policy Analysis
Market Analysis
Social Studies
```

Always check the dataset's methodology, update date, definitions, and licensing before using it.

---

# 41. Survey Data

Survey data is collected through structured questions.

Example:

```text
How satisfied are you?

1 → Very Dissatisfied
2 → Dissatisfied
3 → Neutral
4 → Satisfied
5 → Very Satisfied
```

This is typically **ordinal**.

---

# 42. Experimental Data

Experimental data is generated through controlled experiments.

A common business example is:

## A/B Testing

```text
Users
  |
  ├── Group A → Old Website
  |
  └── Group B → New Website
```

Compare:

```text
Conversion Rate
Revenue
Engagement
Retention
```

The goal is often to estimate whether an intervention caused a difference, subject to experimental design and statistical assumptions.

---

# 43. Database Data

Organizations commonly store structured data in databases.

Examples:

```text
Customer Database
Sales Database
Inventory Database
Employee Database
```

Relational databases organize data using tables.

Example:

```text
CUSTOMERS
--------------------------------
customer_id
name
city
email
```

```text
ORDERS
--------------------------------
order_id
customer_id
order_date
amount
```

SQL can be used to retrieve and analyze this data.

---

# 44. API Data

## Definition

> An API (Application Programming Interface) provides a defined way for software systems to communicate and exchange data or functionality.

Example:

```text
Your Application
      ↓
      API
      ↓
External Service
      ↓
JSON Response
```

Example response:

```json
{
  "city": "Hyderabad",
  "temperature": 31,
  "humidity": 65
}
```

APIs are commonly used to obtain:

```text
Weather
Financial Data
Maps
Social Data
Product Data
Public Data
```

---

# 45. File-Based Data

Common file formats include:

```text
CSV
Excel
JSON
XML
Parquet
TXT
```

---

## CSV

Example:

```csv
id,name,age
1,Ravi,25
2,Priya,30
```

CSV is commonly used for tabular data exchange.

---

## Excel

Useful for:

```text
Manual analysis
Business reporting
Small/medium datasets
```

---

## JSON

Common for:

```text
APIs
Web applications
Semi-structured data
```

---

# 46. Cloud Data Sources

Modern organizations often store data in cloud-based systems.

Examples of categories:

```text
Cloud Databases
Cloud Data Warehouses
Cloud Object Storage
Cloud Data Lakes
Cloud Analytics Platforms
```

These support large-scale storage and analytical processing.

---

# 47. Big Data Sources

Large-scale data may originate from:

```text
Social Media
IoT Devices
Web Logs
Mobile Applications
Streaming Systems
Sensors
E-Commerce
Financial Transactions
```

Characteristics may include:

```text
High Volume
High Velocity
High Variety
```

---

# 48. Data Source Selection

When selecting a data source, consider:

## 1. Relevance

Does the data answer the business question?

---

## 2. Accuracy

Is the data correct?

---

## 3. Completeness

Are important values missing?

---

## 4. Timeliness

Is the data sufficiently current?

---

## 5. Consistency

Does the data use consistent definitions and formats?

---

## 6. Reliability

Can the source be trusted?

---

## 7. Accessibility

Can authorized users obtain the data?

---

## 8. Cost

Is obtaining and maintaining the data economically reasonable?

---

## 9. Privacy

Does the data contain sensitive or personal information?

---

## 10. Security

Can the data be accessed and stored securely?

---

## 11. Licensing

Are you permitted to use and redistribute the data?

---

# 49. Data Quality Dimensions

Data quality is critical because analytical results depend heavily on the underlying data.

Important dimensions include:

```text
Accuracy
Completeness
Consistency
Timeliness
Validity
Uniqueness
```

---

## Accuracy

Does the value represent reality?

```text
Actual Age = 25
Database Age = 52
```

The database value is inaccurate.

---

## Completeness

Are required values present?

```text
Customer Name = Ravi
Age = NULL
City = NULL
```

The record may be incomplete.

---

## Consistency

Are values consistent across systems?

Example:

```text
System A → Hyderabad
System B → HYD
System C → Hyd
```

These may refer to the same city but use inconsistent representations.

---

## Timeliness

Is the data sufficiently current?

For real-time fraud detection, yesterday's data may be too old.

---

## Validity

Does the data follow required rules?

Example:

```text
Age = -50
```

This is invalid under ordinary age definitions.

---

## Uniqueness

Are duplicate records present?

```text
Customer ID = 101
Customer ID = 101
```

If they represent the same customer record unintentionally, duplication is a quality problem.

---

# 50. Data Source vs Data Type

These are different concepts.

## Data Type

Describes **what the data represents or how it is structured**.

Examples:

```text
Categorical
Numerical
Discrete
Continuous
Structured
Unstructured
```

---

## Data Source

Describes **where the data came from**.

Examples:

```text
Database
Survey
API
Sensor
Government Dataset
Website
CRM
```

---

## Example

Suppose we collect customer ages from a CRM database.

```text
Source:
CRM Database

Nature:
Quantitative

Value Type:
Numerical

Measurement:
Ratio

Organization:
Structured

Origin:
Internal

Collection:
Existing/secondary for a new analysis
```

This demonstrates that **one dataset can have multiple classifications simultaneously**.

---

# 51. Complete Classification

Consider this variable:

> Customer satisfaction rating from 1 to 5 collected through a survey.

Classification:

```text
Variable
   ↓
Categorical
   ↓
Ordinal
   ↓
Primary Data
   ↓
Survey Data
```

Another example:

> Customer revenue stored in an organization's SQL database.

```text
Revenue
   ↓
Quantitative
   ↓
Numerical
   ↓
Ratio
   ↓
Structured
   ↓
Internal
   ↓
Transactional
   ↓
Database
```

Another example:

> Customer review text.

```text
Review
   ↓
Qualitative
   ↓
Unstructured
   ↓
Human-generated
   ↓
Potentially internal or external
```

---

# 52. Real-World Example

Imagine an e-commerce company.

It collects:

### Customer Information

```text
Customer ID
Name
Age
Gender
City
```

### Order Information

```text
Order ID
Order Date
Product
Quantity
Price
```

### Customer Feedback

```text
Rating
Review Text
```

### Website Behavior

```text
Page Views
Clicks
Sessions
Add-to-Cart
Purchases
```

Let's classify them.

---

## Customer Age

```text
Quantitative
Numerical
Ratio
Structured
Internal
```

---

## Gender

```text
Qualitative
Categorical
Nominal
Structured
Internal
```

---

## Customer Satisfaction

```text
Qualitative/Categorical
Ordinal
Structured
Primary if collected through a new survey
```

---

## Revenue

```text
Quantitative
Numerical
Ratio
Structured
Transactional
Internal
```

---

## Customer Review

```text
Qualitative
Unstructured
Human-generated
```

---

## Website Clicks

```text
Quantitative
Discrete
Machine-generated
Digital/Web data
Internal
```

---

## Monthly Revenue

```text
Quantitative
Numerical
Ratio
Structured
Time-series
Transactional
```

---

# 🧠 Master Classification Diagram

```text
                              DATA
                                │
        ┌───────────────────────┼────────────────────────┐
        │                       │                        │
        ▼                       ▼                        ▼
     NATURE                 STRUCTURE                ORIGIN
        │                       │                        │
   ┌────┴────┐           ┌──────┼──────┐          ┌─────┴─────┐
   │         │           │      │      │          │           │
Qualitative Quantitative Structured Semi-  Unstructured Primary Secondary
                              Structured
                  │
             ┌────┴────┐
             │         │
          Discrete  Continuous


                    MEASUREMENT SCALE
                           │
             ┌─────────────┼─────────────┐
             │             │             │
          Nominal       Ordinal       Interval
                                         │
                                      Ratio
```

---

# 🎯 Measurement Scale Memory Trick

Remember:

```text
N → O → I → R
```

### N — Nominal

> **Name**

```text
Red
Blue
Green
```

No order.

---

### O — Ordinal

> **Order**

```text
Poor
Average
Good
Excellent
```

Order exists.

---

### I — Interval

> **Intervals are equal**

```text
10°C
20°C
30°C
```

Differences are meaningful.

---

### R — Ratio

> **Real zero**

```text
0 kg
0 ₹
0 km
```

Ratios are meaningful.

---

# 🔥 Most Important Differences

## Discrete vs Continuous

```text
Discrete → Count
Continuous → Measure
```

Example:

```text
Customers → Discrete
Height → Continuous
```

---

## Qualitative vs Quantitative

```text
Qualitative → Categories/qualities
Quantitative → Numerical quantities
```

---

## Nominal vs Ordinal

```text
Nominal → No order
Ordinal → Order exists
```

---

## Ordinal vs Interval

```text
Ordinal → Order, but equal spacing is not guaranteed
Interval → Order + equal intervals
```

---

## Interval vs Ratio

```text
Interval → No absolute zero
Ratio → Absolute zero exists
```

---

## Primary vs Secondary

```text
Primary → Collected directly for the current purpose
Secondary → Previously collected data reused for another/current purpose
```

---

## Structured vs Unstructured

```text
Structured → Predefined schema
Unstructured → No predefined tabular structure
```

---

## Internal vs External

```text
Internal → Comes from inside organization
External → Comes from outside organization
```

---

# 📌 Complete Quick Revision Table

| Concept           | Meaning                           | Example             |
| ----------------- | --------------------------------- | ------------------- |
| Qualitative       | Descriptive/category data         | Color               |
| Quantitative      | Numerical quantity                | Age                 |
| Categorical       | Group/category                    | Department          |
| Discrete          | Countable                         | Number of orders    |
| Continuous        | Measurable                        | Height              |
| Structured        | Fixed schema                      | SQL table           |
| Semi-Structured   | Flexible structure                | JSON                |
| Unstructured      | No predefined tabular structure   | Image               |
| Primary           | Directly collected                | Survey              |
| Secondary         | Existing/reused data              | Government report   |
| Cross-sectional   | Many entities at one time         | Customer survey     |
| Time-series       | Values over time                  | Monthly sales       |
| Panel             | Entities tracked over time        | Customer-month data |
| Nominal           | Labels, no order                  | Blood group         |
| Ordinal           | Ordered categories                | Satisfaction        |
| Interval          | Equal intervals, no absolute zero | Celsius             |
| Ratio             | Equal intervals + absolute zero   | Revenue             |
| Internal          | From organization                 | CRM                 |
| External          | Outside organization              | Government data     |
| Human-generated   | Created by people                 | Reviews             |
| Machine-generated | Automatically generated           | Sensor data         |
| Transactional     | Records transactions              | Orders              |
| Operational       | Business operations               | Inventory           |
| Digital           | Online/app activity               | Clickstream         |

---

# 🧠 Final Mental Model

When you receive a dataset, ask these questions:

```text
QUESTION 1
What does the data represent?
        ↓
Qualitative / Quantitative
        ↓

QUESTION 2
If numerical, is it counted or measured?
        ↓
Discrete / Continuous
        ↓

QUESTION 3
How is it organized?
        ↓
Structured / Semi-Structured / Unstructured
        ↓

QUESTION 4
How was it obtained?
        ↓
Primary / Secondary
        ↓

QUESTION 5
Where did it come from?
        ↓
Internal / External
        ↓

QUESTION 6
How does it vary over time?
        ↓
Cross-sectional / Time-series / Panel
        ↓

QUESTION 7
What measurement scale does the variable use?
        ↓
Nominal / Ordinal / Interval / Ratio
```

---

# 🚀 Final Revision Summary

The most important framework to remember is:

```text
DATA
│
├── BY NATURE
│   ├── Qualitative
│   └── Quantitative
│       ├── Discrete
│       └── Continuous
│
├── BY STRUCTURE
│   ├── Structured
│   ├── Semi-Structured
│   └── Unstructured
│
├── BY COLLECTION
│   ├── Primary
│   └── Secondary
│
├── BY TIME
│   ├── Cross-Sectional
│   ├── Time-Series
│   └── Panel
│
├── BY SOURCE
│   ├── Internal
│   └── External
│
└── BY MEASUREMENT SCALE
    ├── Nominal
    ├── Ordinal
    ├── Interval
    └── Ratio
```

### The one-line memory rules:

```text
Qualitative  → What kind?
Quantitative → How much?

Categorical → Which group?
Numerical   → How much/how many?

Discrete    → Count
Continuous  → Measure

Nominal     → Name
Ordinal     → Order
Interval    → Equal intervals
Ratio       → Real zero

Primary     → Collect yourself
Secondary   → Already collected

Internal    → Inside organization
External    → Outside organization

Structured  → Fixed schema
Semi        → Flexible structure
Unstructured→ No predefined tabular structure

Cross-sectional → Many entities, one period
Time-series     → One/more measures across time
Panel           → Same entities tracked across time
```
