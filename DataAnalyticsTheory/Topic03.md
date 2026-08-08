# 📊 Data Analytics Life Cycle & Types of Data Analytics

> Complete beginner-to-advanced notes for Data Analytics revision.

---

# 📚 Table of Contents

## Part 1 — Data Analytics Life Cycle

1. [What is the Data Analytics Life Cycle?](#1-what-is-the-data-analytics-life-cycle)
2. [Why is the Life Cycle Important?](#2-why-is-the-life-cycle-important)
3. [Overview of the Life Cycle](#3-overview-of-the-life-cycle)
4. [Phase 1 — Business Understanding](#4-phase-1--business-understanding)
5. [Phase 2 — Data Discovery](#5-phase-2--data-discovery)
6. [Phase 3 — Data Collection](#6-phase-3--data-collection)
7. [Phase 4 — Data Preparation](#7-phase-4--data-preparation)
8. [Phase 5 — Data Cleaning](#8-phase-5--data-cleaning)
9. [Phase 6 — Exploratory Data Analysis](#9-phase-6--exploratory-data-analysis)
10. [Phase 7 — Data Analysis and Modeling](#10-phase-7--data-analysis-and-modeling)
11. [Phase 8 — Data Visualization](#11-phase-8--data-visualization)
12. [Phase 9 — Interpretation](#12-phase-9--interpretation)
13. [Phase 10 — Communication](#13-phase-10--communication)
14. [Phase 11 — Decision Making](#14-phase-11--decision-making)
15. [Phase 12 — Deployment and Monitoring](#15-phase-12--deployment-and-monitoring)
16. [Iterative Nature of Analytics](#16-iterative-nature-of-analytics)

## Part 2 — Types of Data Analytics

17. [What are the Types of Data Analytics?](#17-what-are-the-types-of-data-analytics)
18. [Descriptive Analytics](#18-descriptive-analytics)
19. [Diagnostic Analytics](#19-diagnostic-analytics)
20. [Predictive Analytics](#20-predictive-analytics)
21. [Prescriptive Analytics](#21-prescriptive-analytics)
22. [Cognitive Analytics](#22-cognitive-analytics)
23. [Real-Time Analytics](#23-real-time-analytics)
24. [Exploratory Analytics](#24-exploratory-analytics)
25. [Confirmatory Analytics](#25-confirmatory-analytics)
26. [Quantitative Analytics](#26-quantitative-analytics)
27. [Qualitative Analytics](#27-qualitative-analytics)
28. [Types Comparison](#28-types-comparison)
29. [How the Four Main Types Connect](#29-how-the-four-main-types-connect)
30. [Real-World Business Example](#30-real-world-business-example)
31. [Analytics vs Data Science vs Machine Learning](#31-analytics-vs-data-science-vs-machine-learning)
32. [Common Tools](#32-common-tools)
33. [Important Interview Questions](#33-important-interview-questions)
34. [Final Revision Summary](#34-final-revision-summary)

---

# PART 1 — DATA ANALYTICS LIFE CYCLE

# 1. What is the Data Analytics Life Cycle?

## Easy Definition

The **Data Analytics Life Cycle** is a systematic sequence of steps used to:

```text
Identify a problem
      ↓
Collect data
      ↓
Prepare data
      ↓
Analyze data
      ↓
Find insights
      ↓
Communicate findings
      ↓
Make decisions
      ↓
Monitor results
```

---

## Technical Definition

> The Data Analytics Life Cycle is an iterative framework that describes the stages through which an analytical problem progresses, from business problem definition and data acquisition through preparation, exploration, modeling, interpretation, communication, deployment, and monitoring.

The exact names and number of stages vary across organizations and methodologies, but the underlying activities are broadly similar.

---

# 2. Why is the Life Cycle Important?

A data analyst should not immediately open Python or SQL and start calculating.

The correct process is:

```text
Business Problem
       ↓
Analytical Question
       ↓
Data
       ↓
Analysis
       ↓
Insight
       ↓
Action
       ↓
Business Result
```

Without a structured process, analysts may:

* solve the wrong problem
* use irrelevant data
* introduce data-quality errors
* produce misleading conclusions
* create unnecessary reports
* fail to connect analysis with business decisions

---

# 3. Overview of the Life Cycle

A practical analytics life cycle can be represented as:

```text
                 ┌─────────────────────┐
                 │ 1. Business         │
                 │    Understanding    │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 2. Data Discovery   │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 3. Data Collection  │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 4. Data Preparation │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 5. Data Cleaning    │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 6. EDA              │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 7. Analysis /       │
                 │    Modeling         │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 8. Visualization    │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 9. Interpretation   │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 10. Communication   │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 11. Decision        │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ 12. Deployment &    │
                 │     Monitoring      │
                 └──────────┬──────────┘
                            │
                            └──────→ Iterate
```

Not every project requires every stage to the same depth.

---

# 4. Phase 1 — Business Understanding

This is usually the **most important starting point**.

## Easy Definition

Understand:

> **What problem are we trying to solve?**

---

## Example

A company says:

> "Our sales are decreasing."

That is a business problem, not yet a precise analytical question.

The analyst should ask:

* When did sales begin decreasing?
* Which products are affected?
* Which regions are affected?
* Are customers buying less?
* Are prices changing?
* Is competition increasing?
* Has marketing performance changed?

---

## Convert Business Problem into Analytical Questions

Business problem:

```text
Sales are declining.
```

Analytical questions:

```text
Which products experienced the largest decline?

Which regions experienced the largest decline?

When did the decline begin?

What customer segments changed their purchasing behavior?

Which factors are associated with the decline?
```

---

## Define KPIs

Examples:

```text
Revenue
Profit
Orders
Average Order Value
Conversion Rate
Customer Retention
Customer Acquisition Cost
Churn Rate
```

---

## Output

The output of this phase should include:

```text
Business objective
Analytical questions
KPIs
Scope
Constraints
Success criteria
Stakeholders
```

---

# 5. Phase 2 — Data Discovery

Now determine:

> **What data do we need?**

---

## Questions

```text
What data exists?

Where is it stored?

Who owns it?

How much data is available?

What variables are available?

How frequently is it updated?

Is the data accessible?

Are there privacy restrictions?
```

---

## Example

For sales analysis, possible sources:

```text
Sales Database
CRM
Product Database
Marketing Platform
Customer Support System
Website Analytics
```

---

## Output

```text
Data inventory
Data source list
Data dictionary
Available variables
Data accessibility information
```

---

# 6. Phase 3 — Data Collection

Now acquire the required data.

Sources may include:

```text
SQL databases
CSV files
Excel
APIs
Cloud storage
Data warehouses
Surveys
Application logs
Sensors
Third-party datasets
```

---

## Example

Suppose the analyst needs:

```text
Customer ID
Order Date
Product
Quantity
Price
Region
Customer Segment
```

The data may be extracted using SQL.

```sql
SELECT
    customer_id,
    order_date,
    product,
    quantity,
    price,
    region,
    customer_segment
FROM orders;
```

---

## Output

```text
Raw dataset
```

---

# 7. Phase 4 — Data Preparation

Data preparation converts raw data into a form suitable for analysis.

It can involve:

```text
Data integration
Data transformation
Data formatting
Data type conversion
Data structuring
Feature creation
Data filtering
```

---

## Example

Raw:

```text
"01/08/2026"
"02/08/2026"
"03/08/2026"
```

Convert to proper date values.

Similarly:

```text
"₹50,000"
```

may need to become:

```text
50000
```

before numerical analysis.

---

# 8. Phase 5 — Data Cleaning

Data cleaning identifies and corrects or appropriately handles problems in the dataset.

Common issues:

```text
Missing values
Duplicate records
Invalid values
Incorrect data types
Inconsistent categories
Outliers
Formatting errors
Incorrect dates
Data-entry errors
```

---

## Example

Suppose:

| Customer |  Age |
| -------- | ---: |
| A        |   25 |
| B        | NULL |
| C        |  -10 |
| D        |   25 |

Problems:

```text
NULL → Missing
-10 → Potentially invalid
Duplicate 25 → Not necessarily an error
```

Important:

> Not every unusual value is an error.

Cleaning decisions should be based on domain knowledge and context.

---

# 9. Phase 6 — Exploratory Data Analysis

EDA means:

> **Exploring the data to understand what is happening.**

Typical activities:

```text
Summary statistics
Distribution analysis
Missing-value analysis
Outlier analysis
Correlation analysis
Group comparisons
Trend analysis
Visualization
```

---

## Example Questions

```text
What is the average revenue?

Which product sells the most?

Which region generates the most revenue?

Are there seasonal trends?

Which variables are correlated?

Are there unusual observations?
```

---

## Common Python Tools

```python
df.head()
df.info()
df.describe()
df.isnull().sum()
df.nunique()
df.corr(numeric_only=True)
```

---

# 10. Phase 7 — Data Analysis and Modeling

Now perform analysis based on the business question.

Depending on the project, this can include:

```text
Descriptive statistics
Statistical testing
Correlation analysis
Regression
Forecasting
Segmentation
Classification
Clustering
Time-series analysis
Experiment analysis
```

---

## Example

Question:

> Does advertising expenditure relate to sales?

Possible analysis:

```text
Advertising Spend
        ↓
Correlation
        ↓
Regression
        ↓
Estimate relationship
```

---

## Important

**Analysis does not automatically mean machine learning.**

Many analytics projects use:

```text
SQL
Excel
Statistics
Pivot tables
Aggregations
Dashboards
```

without machine learning.

---

# 11. Phase 8 — Data Visualization

Visualization converts analytical results into graphical representations.

Common charts:

```text
Bar Chart
Line Chart
Pie Chart
Histogram
Scatter Plot
Box Plot
Heatmap
Area Chart
Map
```

---

## Match Visualization to Question

### Compare categories

```text
Bar Chart
```

### Show trends

```text
Line Chart
```

### Show distribution

```text
Histogram
Box Plot
```

### Show relationship

```text
Scatter Plot
```

### Show geographic patterns

```text
Map
```

---

# 12. Phase 9 — Interpretation

Analysis gives results.

Interpretation explains:

> **What do those results actually mean?**

Example:

Analysis:

```text
Region A revenue decreased by 15%.
```

Interpretation:

```text
The decline is concentrated primarily in two products,
while other products remained relatively stable.
```

---

## Important Distinction

```text
Result ≠ Insight
```

Result:

> Revenue decreased 15%.

Insight:

> Revenue decreased primarily because Product X lost demand in Region A.

An insight should connect evidence to a meaningful explanation or implication, while avoiding unsupported causal claims.

---

# 13. Phase 10 — Communication

The analyst must communicate findings to stakeholders.

Possible formats:

```text
Dashboard
Report
Presentation
Email
Executive Summary
Data Story
```

---

## Good Analytical Communication

A strong presentation generally answers:

```text
What happened?
Why does it matter?
What evidence supports it?
What should we do?
What are the limitations?
```

---

# 14. Phase 11 — Decision Making

Analytics exists to support better decisions.

Example:

Analysis:

```text
Product A
↓
High sales
↓
High margin
↓
Strong growth
```

Possible business decision:

```text
Increase inventory
Increase marketing
Expand distribution
```

---

## Important

An analyst provides **evidence and recommendations**.

The final business decision may depend on:

```text
Budget
Risk
Strategy
Operations
Legal requirements
Management priorities
```

---

# 15. Phase 12 — Deployment and Monitoring

For recurring or operational analytics, the solution may need to be deployed and monitored.

Examples:

```text
Automated Dashboard
Scheduled SQL Pipeline
Data Pipeline
Forecasting System
Fraud Detection System
Recommendation System
```

---

## Monitoring

Track:

```text
Data quality
Data freshness
Dashboard failures
Metric changes
Model performance
Business KPIs
```

---

# 16. Iterative Nature of Analytics

The analytics life cycle is **not always linear**.

You may discover:

```text
Missing Data
    ↓
Return to Data Collection
```

or:

```text
Unexpected Pattern
    ↓
Return to EDA
```

or:

```text
Business Question Changes
    ↓
Return to Business Understanding
```

Therefore:

```text
Analytics Life Cycle
        ↻
   Iterative Process
```

---

# PART 2 — TYPES OF DATA ANALYTICS

# 17. What are the Types of Data Analytics?

The four fundamental types are:

```text
1. Descriptive
2. Diagnostic
3. Predictive
4. Prescriptive
```

A useful progression is:

```text
What happened?
      ↓
Why did it happen?
      ↓
What might happen?
      ↓
What should we do?
```

---

# 18. Descriptive Analytics

## Easy Definition

Descriptive analytics explains:

> **What happened?**

---

## Technical Definition

> Descriptive analytics summarizes historical or current data to describe observed patterns, trends, distributions, and key performance indicators.

---

## Examples

```text
Total sales = ₹10 crore
Orders = 50,000
Average order value = ₹2,000
Customer churn = 8%
```

---

## Common Techniques

```text
Count
Sum
Average
Median
Minimum
Maximum
Percentage
Rate
Frequency
Grouping
Aggregation
```

---

## SQL Example

```sql
SELECT
    SUM(sales) AS total_sales,
    AVG(sales) AS average_sales,
    COUNT(*) AS total_orders
FROM orders;
```

---

## Tools

```text
SQL
Excel
Python
Pandas
Power BI
Tableau
Matplotlib
```

---

# 19. Diagnostic Analytics

## Easy Definition

Diagnostic analytics asks:

> **Why did it happen?**

---

## Technical Definition

> Diagnostic analytics investigates relationships, patterns, anomalies, and contributing factors in order to explain observed outcomes.

---

## Example

Descriptive:

```text
Sales decreased by 20%.
```

Diagnostic:

```text
Sales decreased primarily because:
- Product A demand fell
- Region B experienced fewer orders
- Customer churn increased
```

---

## Techniques

```text
Drill-down
Root-cause analysis
Correlation analysis
Segmentation
Comparison
Variance analysis
Trend analysis
Cohort analysis
Funnel analysis
```

---

## Example

Overall sales:

```text
₹10 crore → ₹8 crore
```

Break down:

```text
Region A → -5%
Region B → -30%
Region C → +2%
```

Now investigate Region B.

Then:

```text
Region B
   ↓
Product A
   ↓
Customer Segment X
```

This is diagnostic analysis.

---

# 20. Predictive Analytics

## Easy Definition

Predictive analytics asks:

> **What is likely to happen?**

---

## Technical Definition

> Predictive analytics uses historical data, statistical methods, and often machine-learning models to estimate future or unknown outcomes.

---

## Examples

```text
Next month's sales
Customer churn probability
Loan default probability
Demand forecast
Fraud probability
```

---

## Techniques

```text
Regression
Time-Series Forecasting
Classification
Machine Learning
Statistical Modeling
```

---

## Example

Historical data:

```text
2023 → ₹5 crore
2024 → ₹6 crore
2025 → ₹7.2 crore
```

A forecasting model may estimate:

```text
2026 → ₹8.5 crore
```

This is a prediction, not a guaranteed outcome.

---

# 21. Prescriptive Analytics

## Easy Definition

Prescriptive analytics asks:

> **What should we do?**

---

## Technical Definition

> Prescriptive analytics recommends actions or decisions by evaluating possible alternatives, constraints, objectives, and predicted outcomes.

---

## Example

Predictive:

```text
Demand next month = 100,000 units
```

Prescriptive:

```text
Increase inventory to 110,000 units
```

because the business wants to balance:

```text
Expected demand
+
Safety stock
+
Storage cost
+
Stockout risk
```

---

## Techniques

```text
Optimization
Simulation
Decision analysis
Scenario analysis
Operations research
Constraint optimization
```

---

# 22. Cognitive Analytics

Cognitive analytics is a broader advanced concept involving systems that can process complex information and support reasoning-like tasks.

It may combine:

```text
Machine Learning
Natural Language Processing
Computer Vision
Knowledge Representation
AI
```

---

## Example

A customer-support system analyzes:

```text
Customer message
+
Customer history
+
Product information
```

and suggests:

```text
Likely issue
Recommended response
Priority
```

---

# 23. Real-Time Analytics

## Definition

> Real-time analytics analyzes data with very low latency so that insights can support decisions close to the time events occur.

Examples:

```text
Fraud Detection
Stock Market Monitoring
Website Monitoring
IoT Monitoring
Payment Monitoring
Cybersecurity
```

---

## Example

```text
Transaction occurs
       ↓
Data arrives
       ↓
Rules/model analyze it
       ↓
Risk score calculated
       ↓
Possible transaction block/review
```

---

# 24. Exploratory Analytics

## Definition

> Exploratory analytics is used to investigate data, discover patterns, generate hypotheses, and identify relationships before or alongside formal analysis.

Typical activities:

```text
EDA
Visual exploration
Grouping
Correlation
Outlier investigation
Trend discovery
Segmentation
```

---

## Example

You don't know why customers are leaving.

You explore:

```text
Age
Location
Subscription
Usage
Support Tickets
Payment History
```

and discover:

> Churn appears particularly high among customers with low product usage.

This may lead to a formal hypothesis.

---

# 25. Confirmatory Analytics

## Definition

> Confirmatory analysis evaluates predefined hypotheses or questions using appropriate statistical methods and assumptions.

Example hypothesis:

```text
H₀:
The new website does not change conversion rate.

H₁:
The new website changes conversion rate.
```

Then use an appropriate statistical test or experimental framework.

---

## Difference

```text
Exploratory → Discover
Confirmatory → Test
```

---

# 26. Quantitative Analytics

Quantitative analytics uses numerical data and mathematical/statistical methods.

Examples:

```text
Revenue Analysis
Sales Analysis
Statistical Testing
Forecasting
Regression
Correlation
```

---

# 27. Qualitative Analytics

Qualitative analytics analyzes non-numeric information such as:

```text
Customer Reviews
Interviews
Open-ended Survey Responses
Feedback
Documents
```

Common techniques include:

```text
Thematic Analysis
Content Analysis
Sentiment Analysis
Coding
Topic Analysis
```

---

# 28. Types Comparison

| Type         | Main Question                                 | Typical Output           |
| ------------ | --------------------------------------------- | ------------------------ |
| Descriptive  | What happened?                                | Summary                  |
| Diagnostic   | Why did it happen?                            | Explanation              |
| Predictive   | What might happen?                            | Forecast/probability     |
| Prescriptive | What should we do?                            | Recommendation           |
| Exploratory  | What patterns exist?                          | Hypotheses/insights      |
| Confirmatory | Is this hypothesis supported?                 | Statistical conclusion   |
| Real-time    | What is happening now?                        | Immediate insight/action |
| Cognitive    | How can intelligent systems assist reasoning? | AI-supported insight     |

---

# 29. How the Four Main Types Connect

Consider an e-commerce company.

## Step 1 — Descriptive

```text
Sales decreased 15%.
```

Question:

> What happened?

---

## Step 2 — Diagnostic

```text
Sales decreased mainly in Region B
because Product X purchases declined.
```

Question:

> Why did it happen?

---

## Step 3 — Predictive

```text
If the current trend continues,
next month's sales may decline another 8%.
```

Question:

> What might happen?

---

## Step 4 — Prescriptive

```text
Increase Product X promotion in Region B
and adjust inventory based on expected demand.
```

Question:

> What should we do?

---

# 30. Real-World Business Example

Suppose a food-delivery company has declining orders.

---

## Descriptive Analytics

```text
Orders decreased by 12%.
```

---

## Diagnostic Analytics

Analysis reveals:

```text
Customer retention decreased.
Delivery times increased.
The largest decline occurred in urban customers.
```

---

## Predictive Analytics

A model estimates:

```text
Customers with delivery times > 45 minutes
have a higher predicted probability of churn.
```

---

## Prescriptive Analytics

The company evaluates:

```text
More delivery partners
vs
Higher delivery fees
vs
Smaller delivery zones
```

and selects an action based on expected business impact and constraints.

---

# 31. Analytics vs Data Science vs Machine Learning

These concepts overlap but are not identical.

## Data Analytics

Focus:

```text
Understanding data
Finding insights
Supporting decisions
```

Typical tools:

```text
SQL
Excel
Python
Statistics
Power BI
Tableau
```

---

## Data Science

Broader field involving:

```text
Statistics
Programming
Machine Learning
Data Engineering concepts
Experimentation
Analytics
Modeling
```

---

## Machine Learning

Focuses on algorithms that learn patterns from data to make predictions or decisions.

Examples:

```text
Classification
Regression
Clustering
Recommendation
Forecasting
```

---

## Simple Relationship

```text
              DATA SCIENCE
             /            \
            /              \
     DATA ANALYTICS      MACHINE LEARNING
```

There is substantial overlap, but the terms are not interchangeable.

---

# 32. Common Tools

## SQL

Used for:

```text
Data extraction
Filtering
Joining
Aggregation
Transformation
Analysis
```

---

## Excel

Used for:

```text
Data cleaning
Pivot Tables
Formulas
Charts
Quick analysis
```

---

## Python

Common libraries:

```text
Pandas
NumPy
Matplotlib
Seaborn
SciPy
Statsmodels
Scikit-learn
```

---

## BI Tools

```text
Power BI
Tableau
Looker
```

Used for:

```text
Dashboards
Reporting
Interactive visualization
Business monitoring
```

---

# 33. Important Interview Questions

## Q1. What is the Data Analytics Life Cycle?

**Answer:**

> It is an iterative process for solving analytical problems, generally involving business understanding, data discovery and collection, preparation and cleaning, exploration, analysis/modeling, visualization, interpretation, communication, decision-making, and where applicable deployment and monitoring.

---

## Q2. What are the four main types of analytics?

```text
Descriptive
Diagnostic
Predictive
Prescriptive
```

---

## Q3. What does descriptive analytics answer?

```text
What happened?
```

---

## Q4. What does diagnostic analytics answer?

```text
Why did it happen?
```

---

## Q5. What does predictive analytics answer?

```text
What might happen?
```

---

## Q6. What does prescriptive analytics answer?

```text
What should we do?
```

---

## Q7. Is analytics a linear process?

No.

It is generally **iterative**.

You may move backward when:

```text
Data is insufficient
Data quality is poor
New questions arise
Unexpected patterns appear
Business requirements change
```

---

## Q8. Is EDA part of the analytics life cycle?

Yes.

EDA is typically used to understand:

```text
Data distributions
Relationships
Patterns
Outliers
Missing values
Potential hypotheses
```

---

## Q9. Does predictive analytics always mean machine learning?

No.

Predictive analytics can use:

```text
Statistical models
Time-series methods
Regression
Machine learning
```

Machine learning is one possible approach.

---

# 34. Final Revision Summary

## Data Analytics Life Cycle

```text
1. Business Understanding
        ↓
2. Data Discovery
        ↓
3. Data Collection
        ↓
4. Data Preparation
        ↓
5. Data Cleaning
        ↓
6. Exploratory Data Analysis
        ↓
7. Analysis / Modeling
        ↓
8. Visualization
        ↓
9. Interpretation
        ↓
10. Communication
        ↓
11. Decision Making
        ↓
12. Deployment & Monitoring
        ↓
     ITERATE
```

---

# ⭐ Four Main Types of Analytics

Remember:

```text
DESCRIPTIVE
"What happened?"
        ↓
DIAGNOSTIC
"Why did it happen?"
        ↓
PREDICTIVE
"What might happen?"
        ↓
PRESCRIPTIVE
"What should we do?"
```

---

# 🧠 One Complete Example

```text
BUSINESS PROBLEM
Sales are declining.
        ↓
DESCRIPTIVE
Sales declined 15%.
        ↓
DIAGNOSTIC
Product X and Region B caused most of the decline.
        ↓
PREDICTIVE
Sales may decline another 8% next month.
        ↓
PRESCRIPTIVE
Increase targeted promotion and optimize inventory.
        ↓
DECISION
Management chooses an action.
        ↓
MONITORING
Track sales and customer response.
        ↓
NEW DATA
        ↓
ANALYSIS CYCLE CONTINUES
```

---

# 🎯 Final Mental Model

When solving a real analytics problem, think:

```text
                    BUSINESS
                       │
                       ▼
                What do we need?
                       │
                       ▼
                     DATA
                       │
                       ▼
               Is the data usable?
                    /       \
                  NO         YES
                  │           │
                  ▼           ▼
               CLEAN        EDA
                              │
                              ▼
                           ANALYSIS
                              │
                 ┌────────────┼────────────┐
                 ▼            ▼            ▼
            DESCRIPTIVE   DIAGNOSTIC   PREDICTIVE
                 │            │            │
                 └────────────┼────────────┘
                              ▼
                        PRESCRIPTIVE
                              │
                              ▼
                       COMMUNICATION
                              │
                              ▼
                          DECISION
                              │
                              ▼
                         MONITORING
                              │
                              └────→ ITERATE
```

> **The ultimate purpose of data analytics is not simply to calculate numbers. It is to transform data into reliable evidence and insights that support better decisions.**
