# 📥 Data Collection in Data Analytics

> Complete beginner-to-advanced notes for understanding how data is collected, from defining the objective to obtaining analysis-ready data.

---

# 📚 Table of Contents

1. [What is Data Collection?](#1-what-is-data-collection)
2. [Technical Definition](#2-technical-definition)
3. [Why Data Collection is Important](#3-why-data-collection-is-important)
4. [Data Collection in the Analytics Life Cycle](#4-data-collection-in-the-analytics-life-cycle)
5. [Data Collection Process](#5-data-collection-process)
6. [Step 1 - Define the Objective](#6-step-1---define-the-objective)
7. [Step 2 - Define the Population](#7-step-2---define-the-population)
8. [Step 3 - Identify Variables](#8-step-3---identify-variables)
9. [Step 4 - Identify Data Sources](#9-step-4---identify-data-sources)
10. [Step 5 - Select Collection Method](#10-step-5---select-collection-method)
11. [Step 6 - Design the Collection Instrument](#11-step-6---design-the-collection-instrument)
12. [Step 7 - Sampling](#12-sampling)
13. [Step 8 - Collect the Data](#13-collect-the-data)
14. [Step 9 - Validate the Data](#14-validate-the-data)
15. [Step 10 - Store and Document the Data](#15-store-and-document-the-data)
16. [Primary Data Collection](#16-primary-data-collection)
17. [Secondary Data Collection](#17-secondary-data-collection)
18. [Internal and External Data](#18-internal-and-external-data)
19. [Quantitative Data Collection](#19-quantitative-data-collection)
20. [Qualitative Data Collection](#20-qualitative-data-collection)
21. [Surveys](#21-surveys)
22. [Interviews](#22-interviews)
23. [Observation](#23-observation)
24. [Experiments](#24-experiments)
25. [Focus Groups](#25-focus-groups)
26. [Forms and Questionnaires](#26-forms-and-questionnaires)
27. [Transactional Data](#27-transactional-data)
28. [Database Data Collection](#28-database-data-collection)
29. [API Data Collection](#29-api-data-collection)
30. [Web Data Collection](#30-web-data-collection)
31. [Sensor and IoT Data](#31-sensor-and-iot-data)
32. [Log Data](#32-log-data)
33. [Sampling](#33-sampling)
34. [Population vs Sample](#34-population-vs-sample)
35. [Probability Sampling](#35-probability-sampling)
36. [Simple Random Sampling](#36-simple-random-sampling)
37. [Systematic Sampling](#37-systematic-sampling)
38. [Stratified Sampling](#38-stratified-sampling)
39. [Cluster Sampling](#39-cluster-sampling)
40. [Multistage Sampling](#40-multistage-sampling)
41. [Non-Probability Sampling](#41-non-probability-sampling)
42. [Convenience Sampling](#42-convenience-sampling)
43. [Purposive Sampling](#43-purposive-sampling)
44. [Quota Sampling](#44-quota-sampling)
45. [Snowball Sampling](#45-snowball-sampling)
46. [Census](#46-census)
47. [Sample Size](#47-sample-size)
48. [Questionnaire Design](#48-questionnaire-design)
49. [Types of Questions](#49-types-of-questions)
50. [Good vs Bad Questions](#50-good-vs-bad-questions)
51. [Data Collection Bias](#51-data-collection-bias)
52. [Sampling Bias](#52-sampling-bias)
53. [Nonresponse Bias](#53-nonresponse-bias)
54. [Measurement Bias](#54-measurement-bias)
55. [Selection Bias](#55-selection-bias)
56. [Recall Bias](#56-recall-bias)
57. [Observer Bias](#57-observer-bias)
58. [Response Bias](#58-response-bias)
59. [Data Collection Errors](#59-data-collection-errors)
60. [Data Quality](#60-data-quality)
61. [Data Validation](#61-data-validation)
62. [Data Documentation](#62-data-documentation)
63. [Data Collection Ethics](#63-data-collection-ethics)
64. [Privacy and Personal Data](#64-privacy-and-personal-data)
65. [Consent](#65-consent)
66. [Data Security](#66-data-security)
67. [Data Collection Tools](#67-data-collection-tools)
68. [Real-World Example](#68-real-world-example)
69. [Data Collection vs Data Preparation](#69-data-collection-vs-data-preparation)
70. [Data Collection vs Data Cleaning](#70-data-collection-vs-data-cleaning)
71. [Advantages and Disadvantages](#71-advantages-and-disadvantages)
72. [Best Practices](#72-best-practices)
73. [Complete Data Collection Workflow](#73-complete-data-collection-workflow)
74. [Interview Questions](#74-interview-questions)
75. [Final Revision](#75-final-revision)

---

# 1. What is Data Collection?

## Easy Definition

**Data collection is the process of gathering information from relevant sources for a specific purpose.**

Example:

A company wants to understand customer satisfaction.

It may collect:

```text
Customer ID
Age
Location
Product
Rating
Feedback
Purchase frequency
```

---

# 2. Technical Definition

> **Data collection is the systematic process of obtaining observations, measurements, responses, records, or other information from defined sources using specified methods for analysis, research, decision-making, or operational purposes.**

The quality of the final analysis depends heavily on the quality and relevance of the collected data.

---

# 3. Why Data Collection is Important

Analytics starts with data.

```text
Good Data
    ↓
Good Analysis
    ↓
Reliable Insights
    ↓
Better Decisions
```

Poor collection can lead to:

```text
Poor Data
    ↓
Biased Analysis
    ↓
Incorrect Insights
    ↓
Poor Decisions
```

---

## Example

Suppose a company asks only its most loyal customers:

> "Are you satisfied with our service?"

It may receive overwhelmingly positive responses.

The result may not represent all customers.

The problem occurred during **data collection**, before analysis even started.

---

# 4. Data Collection in the Analytics Life Cycle

Data collection is one stage in the larger analytics process.

```text
Business Understanding
        ↓
Data Discovery
        ↓
DATA COLLECTION
        ↓
Data Preparation
        ↓
Data Cleaning
        ↓
EDA
        ↓
Analysis
        ↓
Visualization
        ↓
Interpretation
        ↓
Decision
```

---

# 5. Data Collection Process

A typical process is:

```text
1. Define objective
        ↓
2. Define population
        ↓
3. Identify variables
        ↓
4. Identify sources
        ↓
5. Select collection method
        ↓
6. Design instrument/system
        ↓
7. Select sample
        ↓
8. Collect data
        ↓
9. Validate data
        ↓
10. Store and document
```

---

# 6. Step 1 - Define the Objective

Before collecting data, determine:

> **Why are we collecting this data?**

---

## Example

Bad objective:

```text
Collect customer data.
```

Better objective:

```text
Identify factors associated with customer churn
among monthly subscription customers.
```

Now the required data becomes clearer.

Possible variables:

```text
Customer ID
Subscription type
Tenure
Monthly usage
Support tickets
Payment history
Churn status
```

---

# 7. Step 2 - Define the Population

## Population

> The population is the complete group of entities that the study or analysis is intended to describe or make inferences about.

Example:

```text
All customers of the company
```

---

## Sample

A sample is a subset of the population.

Example:

```text
Population = 1,000,000 customers
Sample = 10,000 customers
```

---

## Why Define Population?

Because your conclusions depend on **who the data represents**.

Example:

If your objective is:

> Analyze all customers in India.

But your sample contains only:

```text
Customers from Hyderabad
```

your results may not generalize to all customers in India.

---

# 8. Step 3 - Identify Variables

Determine what information is required.

Example:

Business question:

> What factors influence customer churn?

Possible variables:

```text
Customer_ID
Age
Gender
Location
Subscription
Tenure
Monthly_Usage
Support_Tickets
Monthly_Fee
Payment_Method
Churn
```

---

## Variable Types

Variables may be:

```text
Categorical
Numerical
Discrete
Continuous
Ordinal
Nominal
Date/Time
Text
Boolean
```

---

# 9. Step 4 - Identify Data Sources

Possible sources:

```text
Internal databases
CRM
ERP
Sales systems
Surveys
APIs
Government datasets
Public datasets
Websites
Applications
Sensors
Logs
Third-party providers
```

---

## Internal Sources

```text
Sales Database
Customer Database
HR System
Finance System
CRM
ERP
```

---

## External Sources

```text
Government Data
Market Research
Public APIs
Industry Reports
Third-Party Data Providers
```

---

# 10. Step 5 - Select Collection Method

The method depends on:

```text
Objective
Data type
Population
Cost
Time
Accuracy requirements
Availability
Privacy
```

---

## Example

If you need customer opinions:

```text
Survey
Interview
Focus Group
```

If you need sales transactions:

```text
Database
ERP
Transaction System
```

If you need machine temperature:

```text
Sensor
IoT Device
```

---

# 11. Step 6 - Design the Collection Instrument

A **data collection instrument** is the tool or mechanism used to collect information.

Examples:

```text
Questionnaire
Survey form
Interview guide
Observation checklist
Sensor
Application form
Database schema
API request
```

---

# 12. Step 7 - Sampling

If collecting data from the entire population is impractical, select a sample.

Example:

```text
Population
1,000,000 customers
        ↓
Sampling
        ↓
10,000 customers
```

The sample should be appropriate for the objective and study design.

---

# 13. Step 8 - Collect the Data

Now actually obtain the data.

Examples:

```text
Survey responses
SQL extraction
API responses
Transaction records
Sensor readings
Interviews
Experiments
Application logs
```

---

# 14. Step 9 - Validate the Data

Check whether the collected data meets expected rules.

Examples:

```text
Age >= 0
Age <= reasonable upper bound
Email format valid
Date valid
Required ID present
No impossible values
Expected categories present
```

---

## Example

Suppose:

```text
Age = -20
```

Validation should flag this value.

---

# 15. Step 10 - Store and Document the Data

Collected data should be stored appropriately.

Possible formats:

```text
CSV
Excel
JSON
SQL Database
Data Warehouse
Data Lake
Cloud Storage
```

Also document:

```text
Source
Collection date
Variables
Definitions
Units
Sampling method
Missing-value codes
Data owner
Access restrictions
```

---

# 16. Primary Data Collection

Primary data is collected directly for the current research or business purpose.

Methods:

```text
Surveys
Interviews
Experiments
Observation
Focus Groups
Field Studies
```

---

## Example

A company wants to know:

> Why do customers abandon checkout?

It conducts a survey of current and recent customers.

The resulting responses are primary data.

---

# 17. Secondary Data Collection

Secondary data is data that already exists and is reused for the current analysis.

Sources:

```text
Company databases
Government datasets
Research papers
Industry reports
Public datasets
Historical records
Existing surveys
```

---

## Important

"Secondary" is relative to the current use.

Data collected by a company for operations can become secondary data when an analyst later reuses it for a different research question.

---

# 18. Internal and External Data

## Internal Data

Generated within the organization.

```text
Orders
Customers
Payments
Employees
Inventory
Website events
```

---

## External Data

Obtained from outside.

```text
Government statistics
Economic indicators
Market data
Weather data
Third-party demographic data
```

---

# 19. Quantitative Data Collection

Quantitative collection produces numerical observations.

Examples:

```text
Age
Income
Revenue
Quantity
Height
Weight
Number of orders
Rating
```

Methods:

```text
Surveys
Experiments
Transactions
Sensors
Databases
Logs
```

---

# 20. Qualitative Data Collection

Qualitative collection gathers descriptive information.

Examples:

```text
Interview responses
Customer reviews
Open-ended feedback
Observational notes
Focus-group discussions
```

---

## Example

Question:

> Why did you cancel your subscription?

Answer:

> "The service became too expensive and I wasn't using it enough."

This provides qualitative information.

---

# 21. Surveys

A survey collects information from respondents using a structured set of questions.

Example:

```text
How satisfied are you?

1 - Very dissatisfied
2 - Dissatisfied
3 - Neutral
4 - Satisfied
5 - Very satisfied
```

---

## Advantages

```text
Large populations
Relatively inexpensive
Standardized responses
Easy to quantify
Easy to automate
```

---

## Disadvantages

```text
Nonresponse
Response bias
Poorly designed questions
Limited depth
Sampling problems
```

---

# 22. Interviews

An interview involves directly asking participants questions.

Types:

```text
Structured
Semi-structured
Unstructured
```

---

## Structured Interview

Same questions for everyone.

Useful when:

```text
Standardization is important
```

---

## Semi-Structured Interview

Uses predefined questions but allows follow-up questions.

Useful for:

```text
Research
Customer understanding
User research
```

---

## Unstructured Interview

More conversational and flexible.

Useful for:

```text
Exploration
Deep qualitative research
```

---

# 23. Observation

Observation collects data by watching behavior, events, or processes.

Example:

A retail company observes:

```text
Customer enters store
      ↓
Visits electronics section
      ↓
Checks laptop
      ↓
Talks to salesperson
      ↓
Leaves without purchase
```

This can reveal behavior that respondents may not accurately report.

---

# 24. Experiments

An experiment changes one or more conditions and measures the resulting outcome.

Example:

```text
Group A → Old webpage
Group B → New webpage
```

Measure:

```text
Conversion Rate
```

This is commonly called **A/B testing** when comparing two variants.

---

## Important Concepts

```text
Treatment
Control
Randomization
Outcome
Confounding
Bias
```

---

# 25. Focus Groups

A focus group is a moderated discussion with a selected group of participants.

Used for:

```text
Product research
Market research
User research
Brand research
Understanding opinions
```

It is primarily qualitative.

---

# 26. Forms and Questionnaires

Forms are structured tools for collecting standardized information.

Common platforms include:

```text
Online forms
Mobile forms
Internal business forms
Survey platforms
```

A questionnaire may contain:

```text
Multiple choice
Checkboxes
Ratings
Ranking
Open-ended questions
Numeric input
Date fields
```

---

# 27. Transactional Data

Transactional systems automatically generate data.

Examples:

```text
Purchase
Payment
Refund
Booking
Order
Withdrawal
Deposit
```

Example:

| Transaction | Customer | Amount | Date       |
| ----------- | -------- | -----: | ---------- |
| T001        | C101     |    500 | 2026-08-01 |
| T002        | C102     |    900 | 2026-08-02 |

---

# 28. Database Data Collection

Analysts frequently collect existing data from databases.

Example:

```sql
SELECT
    customer_id,
    order_date,
    amount
FROM orders
WHERE order_date >= '2026-01-01';
```

This is common in data analytics because business systems continuously generate structured records.

---

# 29. API Data Collection

An API can provide data programmatically.

Typical process:

```text
Application
    ↓
API Request
    ↓
Authentication
    ↓
Server
    ↓
Response
    ↓
JSON/XML
    ↓
Store
    ↓
Analyze
```

Example JSON:

```json
{
  "product_id": 101,
  "price": 59999,
  "category": "Laptop"
}
```

---

# 30. Web Data Collection

Web-based data may come from:

```text
Web APIs
Web pages
Public datasets
Web analytics
Clickstream systems
```

---

## Important

Web data collection must respect:

```text
Terms of service
Copyright
Privacy requirements
Access controls
Robots directives where applicable
Applicable laws and regulations
```

---

# 31. Sensor and IoT Data

Sensors automatically collect measurements.

Examples:

```text
Temperature
Humidity
Pressure
Motion
Location
Speed
Heart rate
Machine vibration
```

Example:

```text
Timestamp        Temperature
10:00            28.2°C
10:05            28.7°C
10:10            29.1°C
```

This often produces **time-series data**.

---

# 32. Log Data

Software systems generate logs describing events.

Examples:

```text
Login
Logout
Error
Page request
Database query
API call
Application event
```

Example:

```text
2026-08-08 10:30:15
USER_LOGIN
user_id=1024
```

Logs are useful for:

```text
System monitoring
Security analysis
Performance analysis
User behavior analysis
Troubleshooting
```

---

# 33. Sampling

## Definition

> Sampling is the process of selecting a subset of a population for data collection or analysis.

Example:

```text
Population = 1,000,000 customers
Sample = 20,000 customers
```

---

# 34. Population vs Sample

| Population                          | Sample                     |
| ----------------------------------- | -------------------------- |
| Entire target group                 | Subset                     |
| Usually larger                      | Usually smaller            |
| Often expensive to study completely | Usually cheaper            |
| Parameter describes population      | Statistic describes sample |

---

## Example

```text
Population:
All customers

Sample:
5,000 selected customers
```

---

# 35. Probability Sampling

In probability sampling, members of the target population have a known, non-zero probability of selection under the sampling design.

Common methods:

```text
Simple Random
Systematic
Stratified
Cluster
Multistage
```

---

# 36. Simple Random Sampling

Every eligible population member has an equal selection probability under the design.

Example:

```text
100,000 customers
        ↓
Randomly select
        ↓
5,000 customers
```

---

## Advantage

Simple and conceptually straightforward.

## Limitation

Requires a suitable sampling frame and may not ensure adequate representation of small subgroups.

---

# 37. Systematic Sampling

Select units at a regular interval after a random starting point.

Example:

```text
Population = 100,000
Sample = 10,000
```

Sampling interval:

```text
k = 100000 / 10000
k = 10
```

Choose a random starting point, then select:

```text
7
17
27
37
47
...
```

---

# 38. Stratified Sampling

Divide the population into meaningful subgroups called **strata**, then sample within each stratum.

Example:

```text
Customers
│
├── Premium
├── Standard
└── Basic
```

Then select customers from each group.

---

## Why Use It?

To ensure important subgroups are represented in the sample.

---

# 39. Cluster Sampling

Divide the population into natural groups called clusters and select clusters, often followed by sampling or surveying units within selected clusters.

Example:

```text
All Schools
│
├── School A
├── School B
├── School C
├── School D
└── School E
```

Select:

```text
School B
School D
```

and collect data from students within selected schools according to the design.

---

## Common Use

When the population is geographically dispersed and sampling individual units directly is costly.

---

# 40. Multistage Sampling

Sampling occurs through multiple stages.

Example:

```text
Country
   ↓
States
   ↓
Cities
   ↓
Schools
   ↓
Students
```

This is common in large population surveys.

---

# 41. Non-Probability Sampling

In non-probability sampling, selection probabilities are not known in the same way as in probability sampling.

Methods include:

```text
Convenience
Purposive
Quota
Snowball
```

These can be useful for exploratory or qualitative research but generally provide weaker grounds for statistical generalization to a target population.

---

# 42. Convenience Sampling

Select participants who are easiest to access.

Example:

```text
Survey the first 500 people
who visit a website.
```

---

## Advantage

```text
Fast
Cheap
Easy
```

## Disadvantage

```text
High risk of selection bias
May not represent population
```

---

# 43. Purposive Sampling

Participants are deliberately selected because they meet specific criteria or have relevant expertise/experience.

Example:

```text
Select experienced data analysts
for interviews about analytics workflows.
```

Useful for:

```text
Expert research
Qualitative research
Specialized populations
```

---

# 44. Quota Sampling

Select participants until predefined category quotas are filled.

Example:

```text
Age 18-25 → 100
Age 26-40 → 100
Age 41-60 → 100
```

Unlike stratified probability sampling, selection within the categories may be non-random.

---

# 45. Snowball Sampling

Existing participants help identify or recruit additional eligible participants.

Example:

```text
Participant A
      ↓
Participant B
      ↓
Participant C
      ↓
Participant D
```

Useful when the target population is difficult to identify or reach.

---

# 46. Census

A census attempts to collect data from **every member of the target population**.

Example:

```text
Population = 10,000 employees

Census = Collect data from all 10,000
```

---

## Advantages

```text
No sampling selection within the target population
Complete population coverage if successfully conducted
```

## Disadvantages

```text
Expensive
Time-consuming
Operationally difficult
Still subject to nonresponse and measurement errors
```

---

# 47. Sample Size

Sample size is the number of observations or units included in the sample.

There is **no universal correct sample size**.

It depends on:

```text
Population
Sampling design
Expected variability
Desired precision
Confidence level
Statistical power
Effect size
Response rate
Cost
```

---

## Important

A larger sample does not automatically remove:

```text
Selection bias
Measurement bias
Nonresponse bias
Poor question design
```

A biased large sample can still produce biased results.

---

# 48. Questionnaire Design

A good questionnaire should be:

```text
Clear
Specific
Neutral
Relevant
Short enough
Logically ordered
Easy to answer
```

---

# 49. Types of Questions

## Multiple Choice

```text
Which payment method do you use?

A. Cash
B. Card
C. UPI
D. Other
```

---

## Multiple Response

```text
Which services do you use?

☐ Banking
☐ Insurance
☐ Investments
☐ Loans
```

---

## Rating Scale

```text
Rate our service:

1 2 3 4 5
```

---

## Ranking

```text
Rank these factors:

Price
Quality
Delivery
Support
```

---

## Open-Ended

```text
What could we improve?
```

---

# 50. Good vs Bad Questions

## Good

```text
How satisfied are you with delivery time?
```

Specific and focused.

---

## Bad

```text
How satisfied are you with our amazing products and excellent delivery service?
```

Problems:

```text
Leading language
Multiple concepts
Biased wording
```

---

## Double-Barreled Question

Avoid:

```text
How satisfied are you with our price and service?
```

Price and service are different dimensions.

Better:

```text
How satisfied are you with our pricing?

How satisfied are you with our service?
```

---

# 51. Data Collection Bias

Bias is systematic error that can cause the collected data or resulting estimates to differ from the target population or true quantity of interest.

Common types:

```text
Sampling Bias
Selection Bias
Nonresponse Bias
Measurement Bias
Recall Bias
Observer Bias
Response Bias
```

---

# 52. Sampling Bias

Occurs when the sampling process systematically overrepresents or underrepresents parts of the target population.

Example:

A company surveys only premium customers to estimate satisfaction among all customers.

---

# 53. Nonresponse Bias

Occurs when people selected for a study do not respond and nonresponders differ systematically from responders.

Example:

```text
Selected = 10,000
Responded = 2,000
```

If unhappy customers are much less likely to respond, the results may overestimate satisfaction.

---

# 54. Measurement Bias

Occurs when the measurement process systematically produces inaccurate values.

Example:

A faulty sensor consistently records temperature 2°C too high.

---

# 55. Selection Bias

Occurs when inclusion in the observed data is systematically related to the outcome or factors of interest.

Example:

Analyzing customer feedback only from customers who voluntarily leave reviews may not represent all customers.

---

# 56. Recall Bias

Occurs when respondents inaccurately remember past events.

Example:

> "How much did you spend on food over the last 12 months?"

People may not remember accurately.

---

# 57. Observer Bias

Occurs when the observer's expectations influence how observations are recorded or interpreted.

Example:

A researcher expecting a treatment to work may unconsciously rate outcomes more favorably.

Blinding can sometimes reduce this risk.

---

# 58. Response Bias

Occurs when respondents provide answers that systematically differ from their actual behavior or beliefs.

Possible reasons:

```text
Social desirability
Fear
Question wording
Acquiescence
Sensitive topics
```

---

# 59. Data Collection Errors

Common errors include:

```text
Incorrect entries
Missing responses
Duplicate records
Wrong units
Wrong timestamps
Invalid categories
Measurement errors
Coding errors
Sampling errors
Transmission errors
```

---

## Example

Actual:

```text
Age = 25
```

Collected:

```text
Age = 52
```

Possible data-entry error.

---

# 60. Data Quality

Good collected data should be:

```text
Accurate
Complete
Consistent
Valid
Timely
Relevant
Unique
Reliable
```

---

# 61. Data Validation

Validation checks whether collected data conforms to expected rules.

---

## Range Validation

```text
Age >= 0
```

---

## Type Validation

```text
Age → Numeric
Date → Date
```

---

## Format Validation

```text
Email → Valid expected format
```

---

## Domain Validation

```text
Gender → Allowed categories
```

---

## Referential Validation

Check whether related identifiers exist.

Example:

```text
Order.customer_id
```

should correspond to an existing customer when the database design requires that relationship.

---

# 62. Data Documentation

Data collection should be documented.

Important metadata:

```text
Dataset name
Source
Owner
Collection date
Collection method
Population
Sample
Variables
Definitions
Units
Missing-value conventions
Transformations
Access restrictions
Quality notes
```

---

# 63. Data Collection Ethics

Data collection should respect:

```text
Privacy
Consent
Purpose limitation
Data minimization
Security
Fairness
Applicable laws and regulations
```

---

# 64. Privacy and Personal Data

Personal data may include information that identifies or can reasonably be linked to an individual, depending on applicable law.

Examples:

```text
Name
Email
Phone number
Address
Identification numbers
Location information
Online identifiers
```

Some categories may receive additional legal protections depending on jurisdiction.

---

# 65. Consent

When consent is the legal or ethical basis for collection, people should generally understand:

```text
What data is collected
Why it is collected
How it will be used
Who may receive it
How long it may be retained
What choices or rights apply
```

Consent requirements vary by context and jurisdiction.

---

# 66. Data Security

Collected data should be protected using appropriate controls.

Examples:

```text
Access control
Authentication
Encryption
Secure storage
Backups
Audit logs
Data masking
Least privilege
```

---

# 67. Data Collection Tools

## Surveys

```text
Online survey platforms
Mobile forms
Internal forms
```

---

## Databases

```text
MySQL
PostgreSQL
SQL Server
Oracle
Cloud databases
```

---

## Programming

Python can automate data collection and ingestion.

Common libraries include:

```text
requests
pandas
json
```

---

## APIs

Used for programmatic data retrieval.

---

## Cloud Platforms

Common components include:

```text
Object Storage
Data Warehouses
Data Lakes
Streaming Systems
```

---

# 68. Real-World Example

Suppose an e-commerce company wants to understand:

> **Why are customers abandoning their carts?**

---

## Step 1 — Objective

```text
Identify factors associated with cart abandonment.
```

---

## Step 2 — Population

```text
All users who added products to carts.
```

---

## Step 3 — Variables

```text
User ID
Device
Product
Price
Cart Value
Number of Items
Discount
Shipping Cost
Delivery Time
Payment Method
Checkout Completion
```

---

## Step 4 — Sources

```text
Website Event Logs
Orders Database
Product Database
Customer Database
Survey
```

---

## Step 5 — Collection

Use:

```text
SQL
Event Tracking
Survey
```

---

## Step 6 — Validation

Check:

```text
Missing user IDs
Duplicate events
Invalid prices
Incorrect timestamps
Impossible quantities
```

---

## Step 7 — Storage

Store in:

```text
Data Warehouse
```

---

## Step 8 — Analysis

Then perform:

```text
EDA
Funnel Analysis
Segmentation
Statistical Analysis
```

---

# 69. Data Collection vs Data Preparation

| Data Collection                    | Data Preparation                      |
| ---------------------------------- | ------------------------------------- |
| Obtains data                       | Makes data suitable for analysis      |
| Happens earlier                    | Usually follows collection            |
| Focuses on sources and acquisition | Focuses on transformation/integration |
| Survey/API/database extraction     | Formatting, combining, reshaping      |
| Produces raw/initial data          | Produces analysis-ready structure     |

---

# 70. Data Collection vs Data Cleaning

| Data Collection            | Data Cleaning                              |
| -------------------------- | ------------------------------------------ |
| Gather data                | Correct/handle data problems               |
| Focuses on acquisition     | Focuses on quality                         |
| Survey, API, database      | Missing values, duplicates, invalid values |
| Before or during ingestion | Usually after data is obtained             |
| Creates the dataset        | Improves dataset quality                   |

---

# 71. Advantages and Disadvantages

## Primary Data

### Advantages

```text
Specific to objective
Control over collection
Current
Can define variables
```

### Disadvantages

```text
Expensive
Time-consuming
Requires design
Potential response/sampling bias
```

---

## Secondary Data

### Advantages

```text
Fast
Usually cheaper
Large datasets may already exist
Useful for historical analysis
```

### Disadvantages

```text
May be outdated
May not match the objective
Unknown quality
Different definitions
Potential licensing restrictions
```

---

# 72. Best Practices

## 1. Start with the business question

Do not collect data simply because it is available.

---

## 2. Collect only relevant data

Avoid unnecessary data collection.

---

## 3. Define variables clearly

Example:

```text
Revenue = Total recognized sales value
```

rather than simply:

```text
Revenue
```

---

## 4. Standardize formats

Use consistent:

```text
Dates
Units
Categories
Identifiers
Currency
Time zones
```

---

## 5. Validate during collection

Do not wait until the end to discover obvious errors.

---

## 6. Document everything

Record:

```text
Source
Method
Definitions
Time period
Sampling
Transformations
Limitations
```

---

## 7. Protect sensitive data

Use appropriate:

```text
Access controls
Encryption
Retention rules
Privacy safeguards
```

---

## 8. Monitor collection processes

For automated pipelines, monitor:

```text
Data freshness
Volume
Schema changes
Missing records
Duplicate records
Pipeline failures
```

---

# 73. Complete Data Collection Workflow

```text
                    BUSINESS QUESTION
                           ↓
                    DEFINE OBJECTIVE
                           ↓
                    DEFINE POPULATION
                           ↓
                    IDENTIFY VARIABLES
                           ↓
                    IDENTIFY SOURCES
                           ↓
                 CHOOSE COLLECTION METHOD
                           ↓
                 ┌─────────┴─────────┐
                 ↓                   ↓
             PRIMARY             SECONDARY
                 ↓                   ↓
       Survey / Interview       Database / API
       Experiment / Sensor      Public Dataset
                 │                   │
                 └─────────┬─────────┘
                           ↓
                        SAMPLE
                           ↓
                     COLLECT DATA
                           ↓
                       VALIDATE
                           ↓
                        STORE
                           ↓
                      DOCUMENT
                           ↓
                   DATA PREPARATION
                           ↓
                    DATA CLEANING
                           ↓
                         EDA
```

---

# 74. Interview Questions

## Q1. What is data collection?

> Data collection is the systematic process of gathering relevant observations, measurements, responses, or records from defined sources for a specific analytical or research purpose.

---

## Q2. What are the main types of data collection?

Common methods include:

```text
Surveys
Interviews
Observation
Experiments
Focus Groups
Database extraction
API collection
Web data collection
Sensor collection
Log collection
```

---

## Q3. What is primary data?

Data collected directly for the current research or analytical purpose.

---

## Q4. What is secondary data?

Previously existing data reused for the current analysis or purpose.

---

## Q5. What is sampling?

Selecting a subset of a population for study or data collection.

---

## Q6. What is the difference between population and sample?

```text
Population → Entire target group
Sample     → Selected subset
```

---

## Q7. What is probability sampling?

A sampling design in which population units have known, non-zero selection probabilities.

---

## Q8. What is sampling bias?

Systematic distortion caused when the sample or selection process does not adequately represent the target population.

---

## Q9. Does a larger sample always solve bias?

**No.**

A large but systematically biased sample can still produce biased results.

---

## Q10. What makes data high quality?

Important dimensions include:

```text
Accuracy
Completeness
Consistency
Validity
Timeliness
Relevance
Uniqueness
Reliability
```

---

# 75. Final Revision

## 🔥 Data Collection =

```text
WHY?
↓
Business Objective

WHO?
↓
Population

WHAT?
↓
Variables

WHERE?
↓
Data Sources

HOW?
↓
Collection Method

WHO WILL BE INCLUDED?
↓
Sampling

COLLECT
↓
Acquire Data

CHECK
↓
Validate

STORE
↓
Database / Files / Warehouse

DOCUMENT
↓
Metadata + Methodology

THEN
↓
Preparation → Cleaning → EDA → Analysis
```

---

# 🧠 Most Important Concepts to Remember

### Data Collection

> Gathering relevant data from appropriate sources for a defined purpose.

### Primary Data

> Collected directly for the current purpose.

### Secondary Data

> Existing data reused for the current purpose.

### Population

> Entire target group.

### Sample

> Subset of the population.

### Probability Sampling

> Selection probabilities are known under the sampling design.

### Non-Probability Sampling

> Selection probabilities are not known in the same way.

### Sampling Bias

> Systematic distortion caused by the selection process.

### Data Validation

> Checking whether collected data satisfies predefined rules.

### Data Quality

> The degree to which data is accurate, complete, consistent, valid, timely, relevant, and fit for its intended use.

---

# ⭐ Final Mental Model

```text
                 DATA COLLECTION
                        │
         ┌──────────────┼──────────────┐
         ↓              ↓              ↓
      PURPOSE         SOURCE         METHOD
         │              │              │
         ↓              ↓              ↓
   Business Q      Internal/       Survey
   Objective       External         Interview
                                   Experiment
                                   Database
                                   API
                                   Sensor
                        │
                        ↓
                    POPULATION
                        │
                        ↓
                     SAMPLE
                        │
                        ↓
                    COLLECTION
                        │
                        ↓
                    VALIDATION
                        │
                        ↓
                      STORAGE
                        │
                        ↓
                   DOCUMENTATION
                        │
                        ↓
                DATA PREPARATION
                        │
                        ↓
                   DATA CLEANING
                        │
                        ↓
                       EDA
                        │
                        ↓
                     ANALYSIS
```

> **Key idea:** Data collection is not simply "getting data." It is the carefully designed process of obtaining the **right data, from the right population, using the right method, with sufficient quality and appropriate ethical and privacy safeguards**, so that the resulting analysis can answer the intended question reliably.
