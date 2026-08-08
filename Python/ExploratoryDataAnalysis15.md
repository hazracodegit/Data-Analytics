# 🔍 Exploratory Data Analysis (EDA) in Python

> **Exploratory Data Analysis (EDA)** is the process of understanding, summarizing, investigating, and visualizing a dataset before performing further analysis or building a machine-learning model.

EDA helps us answer:

```text
What does the data look like?
How large is the dataset?
What type of data do we have?
Are there missing values?
Are there duplicate records?
Are there outliers?
How are variables distributed?
Which variables are related?
Are there patterns or trends?
Is the data suitable for analysis?
```

---

# 📚 Table of Contents

1. [What is EDA?](#1-what-is-eda)
2. [Why is EDA Important?](#2-why-is-eda-important)
3. [Objectives of EDA](#3-objectives-of-eda)
4. [EDA in the Data Analytics Workflow](#4-eda-in-the-data-analytics-workflow)
5. [EDA vs Data Cleaning vs Data Preprocessing vs Data Manipulation](#5-eda-vs-data-cleaning-vs-data-preprocessing-vs-data-manipulation)
6. [Types of EDA](#6-types-of-eda)
7. [Univariate Analysis](#7-univariate-analysis)
8. [Bivariate Analysis](#8-bivariate-analysis)
9. [Multivariate Analysis](#9-multivariate-analysis)
10. [Getting a Dataset](#10-getting-a-dataset)
11. [Loading Data](#11-loading-data)
12. [Understanding Dataset Structure](#12-understanding-dataset-structure)
13. [First and Last Records](#13-first-and-last-records)
14. [Dataset Shape](#14-dataset-shape)
15. [Columns](#15-columns)
16. [Data Types](#16-data-types)
17. [Statistical Summary](#17-statistical-summary)
18. [Missing Values](#18-missing-values)
19. [Duplicate Values](#19-duplicate-values)
20. [Unique Values](#20-unique-values)
21. [Value Counts](#21-value-counts)
22. [Sorting Data](#22-sorting-data)
23. [Filtering Data](#23-filtering-data)
24. [Categorical Analysis](#24-categorical-analysis)
25. [Numerical Analysis](#25-numerical-analysis)
26. [Distribution Analysis](#26-distribution-analysis)
27. [Outlier Detection](#27-outlier-detection)
28. [Correlation Analysis](#28-correlation-analysis)
29. [Visualization in EDA](#29-visualization-in-eda)
30. [Histograms](#30-histograms)
31. [Box Plots](#31-box-plots)
32. [Bar Charts](#32-bar-charts)
33. [Scatter Plots](#33-scatter-plots)
34. [Line Charts](#34-line-charts)
35. [Pie Charts](#35-pie-charts)
36. [Heatmaps](#36-heatmaps)
37. [Pair Plots](#37-pair-plots)
38. [Skewness](#38-skewness)
39. [Kurtosis](#39-kurtosis)
40. [Relationships Between Variables](#40-relationships-between-variables)
41. [GroupBy Analysis](#41-groupby-analysis)
42. [EDA with Pandas](#42-eda-with-pandas)
43. [EDA with NumPy](#43-eda-with-numpy)
44. [EDA with Matplotlib](#44-eda-with-matplotlib)
45. [EDA with Seaborn](#45-eda-with-seaborn)
46. [Complete EDA Workflow](#46-complete-eda-workflow)
47. [Real-World Example](#47-real-world-example)
48. [EDA Checklist](#48-eda-checklist)
49. [Common Mistakes](#49-common-mistakes)
50. [Interview Questions](#50-interview-questions)
51. [Quick Revision](#51-quick-revision)

---

# 1. What is EDA?

EDA stands for:

```text
Exploratory Data Analysis
```

It is the process of **exploring a dataset to understand its structure, characteristics, quality, patterns, relationships, and anomalies**.

EDA is generally performed before advanced statistical analysis or machine learning.

Example dataset:

```text
Name     Age    Salary    Department
Rahul    25     30000     IT
Priya    28     45000     HR
Amit     35     60000     IT
Sneha    30     50000     Sales
```

During EDA, we might ask:

```text
How many employees are there?
What is the average salary?
What is the minimum age?
Which department has the most employees?
Are there missing salaries?
Are there duplicate employees?
Is salary related to age?
Are there unusual salary values?
```

---

# 2. Why is EDA Important?

EDA is important because raw data is rarely immediately ready for analysis.

Real-world data may contain:

```text
Missing values
Duplicate records
Incorrect data types
Outliers
Inconsistent values
Incorrect formatting
Unexpected categories
Skewed distributions
Invalid values
```

EDA helps us discover these problems.

### Example

Suppose:

```text
Age
20
22
25
27
200
30
```

EDA immediately reveals that:

```text
200
```

is suspicious.

It may be:

```text
Data entry error
Wrong unit
Invalid value
```

---

# 3. Objectives of EDA

The major objectives are:

### 1. Understand the data

```text
Rows
Columns
Variables
Data types
Categories
```

### 2. Identify data quality problems

```text
Missing values
Duplicates
Invalid values
Inconsistent values
```

### 3. Understand distributions

```text
Normal
Skewed
Uniform
Bimodal
```

### 4. Detect outliers

```text
Extremely high values
Extremely low values
```

### 5. Find relationships

```text
Age ↔ Salary
Experience ↔ Salary
Sales ↔ Profit
Temperature ↔ Ice Cream Sales
```

### 6. Generate hypotheses

EDA can help us form questions such as:

```text
Does experience increase salary?
Does advertising increase sales?
Does price affect demand?
```

### 7. Prepare for modeling

EDA helps determine whether data needs:

```text
Cleaning
Transformation
Encoding
Scaling
Feature engineering
```

---

# 4. EDA in the Data Analytics Workflow

A typical workflow is:

```text
                RAW DATA
                    ↓
            DATA COLLECTION
                    ↓
            DATA UNDERSTANDING
                    ↓
                   EDA
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
      CLEANING   ANALYSIS   VISUALIZATION
        ↓           ↓           ↓
        └───────────┼───────────┘
                    ↓
            DATA PREPROCESSING
                    ↓
          STATISTICAL ANALYSIS
                    ↓
             MACHINE LEARNING
                    ↓
                INSIGHTS
                    ↓
              DECISIONS
```

Important:

> EDA is not a single operation. It is an iterative process of inspecting, analyzing, visualizing, discovering, and asking questions about data.

---

# 5. EDA vs Data Cleaning vs Data Preprocessing vs Data Manipulation

These concepts are related but **not exactly the same**.

## EDA

Focus:

```text
Understand the data
Find patterns
Find problems
Discover relationships
Generate questions
```

---

## Data Cleaning

Focus:

```text
Fix data quality problems
```

Examples:

```text
Remove duplicates
Handle missing values
Correct invalid values
Fix inconsistent categories
Correct data types
```

---

## Data Manipulation

Focus:

```text
Change, filter, transform, combine, or organize data
```

Examples:

```text
Filtering
Sorting
Grouping
Merging
Joining
Creating columns
Aggregating
Reshaping
```

---

## Data Preprocessing

Focus:

```text
Prepare data for analysis/modeling
```

Examples:

```text
Encoding
Scaling
Normalization
Transformation
Feature selection
Feature engineering
Train-test preparation
```

---

## Relationship

```text
                 EDA
                  ↓
       Understand the dataset
                  ↓
       Discover data problems
                  ↓
            Data Cleaning
                  ↓
        Correct data quality
                  ↓
        Data Manipulation
                  ↓
       Transform/organize data
                  ↓
       Data Preprocessing
                  ↓
      Prepare for ML/analysis
```

However, these steps can overlap and are often repeated iteratively.

---

# 6. Types of EDA

EDA can be classified into:

```text
1. Univariate Analysis
2. Bivariate Analysis
3. Multivariate Analysis
```

---

# 7. Univariate Analysis

"Uni" means one.

Univariate analysis studies **one variable at a time**.

Example:

```text
Age
```

Questions:

```text
What is the average age?
What is the minimum age?
What is the maximum age?
How is age distributed?
Are there outliers?
```

Common methods:

```text
Mean
Median
Mode
Minimum
Maximum
Variance
Standard deviation
Histogram
Box plot
```

---

# 8. Bivariate Analysis

"Bi" means two.

Bivariate analysis studies the relationship between **two variables**.

Examples:

```text
Age vs Salary
Experience vs Salary
Gender vs Salary
Department vs Salary
```

Common methods:

```text
Scatter plot
Correlation
Grouped statistics
Bar chart
Box plot
```

---

# 9. Multivariate Analysis

Multivariate analysis studies **three or more variables simultaneously**.

Example:

```text
Age
Experience
Education
Department
Salary
```

We may investigate:

```text
Age + Experience + Education → Salary
```

Common tools:

```text
Correlation matrix
Heatmap
Pair plot
Multivariate plots
```

---

# 10. Getting a Dataset

Example dataset:

```text
employees.csv
```

Example:

```text
Name,Age,Salary,Department
Rahul,25,30000,IT
Priya,28,45000,HR
Amit,35,60000,IT
Sneha,30,50000,Sales
Arjun,40,75000,IT
```

---

# 11. Loading Data

Use Pandas.

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df)
```

---

# 12. Understanding Dataset Structure

## `head()`

Shows the first five rows.

```python
df.head()
```

Custom number:

```python
df.head(10)
```

---

## `tail()`

Shows the last rows.

```python
df.tail()
```

---

## `sample()`

Shows random rows.

```python
df.sample(5)
```

Useful for quickly seeing whether the data appears representative.

---

# 13. First and Last Records

```python
print(df.head())
print(df.tail())
```

---

# 14. Dataset Shape

Use:

```python
df.shape
```

Example output:

```text
(1000, 8)
```

Meaning:

```text
1000 rows
8 columns
```

---

# 15. Columns

Get column names:

```python
df.columns
```

Convert to a list:

```python
df.columns.tolist()
```

Example:

```python
print(df.columns.tolist())
```

Output:

```text
['Name', 'Age', 'Salary', 'Department']
```

---

# 16. Data Types

Use:

```python
df.dtypes
```

Example:

```text
Name           object
Age             int64
Salary          int64
Department     object
```

---

## `info()`

One of the most important EDA functions:

```python
df.info()
```

It provides:

```text
Number of rows
Column names
Non-null counts
Data types
Memory usage
```

---

# 17. Statistical Summary

Use:

```python
df.describe()
```

For numerical columns, it provides:

```text
count
mean
std
min
25%
50%
75%
max
```

Example:

```python
print(df.describe())
```

---

## Categorical Summary

For object/category columns:

```python
df.describe(include="object")
```

For all columns:

```python
df.describe(include="all")
```

---

# 18. Missing Values

Missing data is extremely important during EDA.

Check missing values:

```python
df.isnull()
```

Usually we want counts:

```python
df.isnull().sum()
```

Example:

```text
Name          0
Age           2
Salary        5
Department    1
```

This means:

```text
Age → 2 missing
Salary → 5 missing
Department → 1 missing
```

---

## Missing Percentage

```python
missing_percentage = (
    df.isnull().sum() / len(df)
) * 100

print(missing_percentage)
```

---

# 19. Duplicate Values

Check duplicate rows:

```python
df.duplicated()
```

Count:

```python
df.duplicated().sum()
```

Remove duplicates:

```python
df = df.drop_duplicates()
```

---

# 20. Unique Values

Check unique values in a column:

```python
df["Department"].unique()
```

Count unique values:

```python
df["Department"].nunique()
```

Example:

```text
IT
HR
Sales
Finance
```

---

# 21. Value Counts

Find frequency of each category:

```python
df["Department"].value_counts()
```

Example:

```text
IT         500
Sales      250
HR         150
Finance    100
```

This is extremely useful for categorical EDA.

---

## Percentage

```python
df["Department"].value_counts(normalize=True) * 100
```

---

# 22. Sorting Data

Sort by salary:

```python
df.sort_values("Salary")
```

Descending:

```python
df.sort_values(
    "Salary",
    ascending=False
)
```

Useful for identifying:

```text
Highest salary
Lowest salary
Top customers
Best-performing products
```

---

# 23. Filtering Data

Example:

```python
df[df["Salary"] > 50000]
```

Multiple conditions:

```python
df[
    (df["Age"] > 30) &
    (df["Salary"] > 50000)
]
```

OR:

```python
df[
    (df["Department"] == "IT") |
    (df["Department"] == "Sales")
]
```

---

# 24. Categorical Analysis

Categorical variables contain categories.

Examples:

```text
Gender
Department
City
Product Category
Payment Method
```

Useful functions:

```python
df["Department"].value_counts()
```

Visualization:

```python
import seaborn as sns

sns.countplot(
    data=df,
    x="Department"
)
```

---

# 25. Numerical Analysis

Numerical variables include:

```text
Age
Salary
Height
Weight
Sales
Profit
```

Basic statistics:

```python
df["Salary"].mean()
df["Salary"].median()
df["Salary"].min()
df["Salary"].max()
df["Salary"].std()
df["Salary"].var()
```

---

# 26. Distribution Analysis

Distribution tells us how values are spread.

Example:

```text
Salary:
20K
25K
30K
35K
40K
...
```

We want to know:

```text
Where are most observations?
Is the distribution symmetric?
Is it skewed?
Are there multiple peaks?
Are there outliers?
```

Common visualization:

```text
Histogram
KDE plot
Box plot
```

---

# 27. Outlier Detection

An outlier is an observation that is unusually far from the rest of the data.

Example:

```text
20
22
25
27
29
30
500
```

`500` may be an outlier.

---

## IQR Method

First:

```text
Q1 = 25th percentile
Q3 = 75th percentile
```

Then:

```text
IQR = Q3 - Q1
```

Lower bound:

```text
Q1 - 1.5 × IQR
```

Upper bound:

```text
Q3 + 1.5 × IQR
```

Values outside these bounds are commonly flagged as potential outliers.

---

## Python

```python
Q1 = df["Salary"].quantile(0.25)
Q3 = df["Salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["Salary"] < lower) |
    (df["Salary"] > upper)
]

print(outliers)
```

---

# 28. Correlation Analysis

Correlation measures the strength and direction of a linear relationship between numerical variables.

Use:

```python
df.corr(numeric_only=True)
```

Example:

```text
          Age   Salary
Age       1.0    0.85
Salary    0.85   1.00
```

This suggests a strong positive linear relationship.

---

## Correlation Range

```text
+1 → Strong perfect positive linear relationship
 0 → No linear relationship
-1 → Strong perfect negative linear relationship
```

Important:

```text
Correlation ≠ Causation
```

---

# 29. Visualization in EDA

Visualization is one of the most important parts of EDA.

It allows patterns to be recognized more easily than from tables alone.

Important libraries:

```text
Matplotlib
Seaborn
```

---

# 30. Histograms

A histogram shows the distribution of numerical data.

```python
import matplotlib.pyplot as plt

plt.hist(df["Salary"])

plt.xlabel("Salary")
plt.ylabel("Frequency")
plt.title("Salary Distribution")

plt.show()
```

Useful for identifying:

```text
Distribution
Spread
Skewness
Possible outliers
```

---

# 31. Box Plots

Box plot is excellent for identifying:

```text
Median
Quartiles
Spread
Potential outliers
```

Example:

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.boxplot(
    data=df,
    y="Salary"
)

plt.show()
```

---

## Box Plot Structure

```text
          Maximum / upper whisker
                  |
              ┌───────┐
              │       │
Q3 ───────────│       │
              │ Median│
Q1 ───────────│       │
              │       │
              └───────┘
                  |
          Minimum / lower whisker

     •  •  •
     Potential outliers
```

---

# 32. Bar Charts

Useful for categorical data.

Example:

```python
sns.countplot(
    data=df,
    x="Department"
)

plt.show()
```

Can answer:

```text
Which department has the most employees?
Which category is most common?
```

---

# 33. Scatter Plots

Used to study the relationship between two numerical variables.

Example:

```python
sns.scatterplot(
    data=df,
    x="Age",
    y="Salary"
)

plt.show()
```

Can reveal:

```text
Positive relationship
Negative relationship
No obvious relationship
Clusters
Outliers
```

---

# 34. Line Charts

Useful when the x-axis represents an ordered variable such as:

```text
Time
Date
Month
Year
```

Example:

```python
plt.plot(
    df["Date"],
    df["Sales"]
)

plt.xlabel("Date")
plt.ylabel("Sales")

plt.show()
```

---

# 35. Pie Charts

Pie charts show proportions of categories.

Example:

```python
counts = df["Department"].value_counts()

plt.pie(
    counts,
    labels=counts.index,
    autopct="%1.1f%%"
)

plt.show()
```

Pie charts can be useful for a small number of categories, but bar charts are often easier to compare precisely.

---

# 36. Heatmaps

Heatmaps use color to represent values.

A common EDA use is visualizing a correlation matrix.

```python
import seaborn as sns
import matplotlib.pyplot as plt

corr = df.corr(numeric_only=True)

sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm"
)

plt.show()
```

---

# 37. Pair Plots

Pair plots visualize relationships between multiple numerical variables.

```python
sns.pairplot(df)

plt.show()
```

They can help identify:

```text
Relationships
Clusters
Distributions
Potential correlations
```

For large datasets, use a carefully selected subset of columns because pair plots can become crowded and slow.

---

# 38. Skewness

Skewness describes the asymmetry of a distribution.

## Symmetric

```text
       /\
      /  \
     /    \
____/      \____
```

---

## Right / Positive Skew

The tail extends toward larger values.

```text
       /\
      /  \
     /    \
____/      \________
```

Usually:

```text
Mean > Median
```

---

## Left / Negative Skew

The tail extends toward smaller values.

```text
          /\
         /  \
________/    \
```

Usually:

```text
Mean < Median
```

---

## Python

```python
df["Salary"].skew()
```

Interpretation depends on context and the magnitude of skewness; there is no universal cutoff that works for every dataset.

---

# 39. Kurtosis

Kurtosis describes aspects of the shape of a distribution, particularly tail behavior and peakedness relative to a reference distribution.

Python:

```python
df["Salary"].kurt()
```

In Pandas, the reported kurtosis uses a convention related to **excess kurtosis**.

Conceptually:

```text
High kurtosis
→ heavier tails / more extreme observations

Low kurtosis
→ lighter tails
```

Be careful not to interpret kurtosis simply as "peak height"; tail behavior is important.

---

# 40. Relationships Between Variables

EDA tries to discover relationships.

Examples:

```text
Age → Salary
Experience → Salary
Advertising → Sales
Price → Demand
Study Hours → Marks
```

---

## Positive Relationship

```text
X increases
↓
Y tends to increase
```

Example:

```text
Experience ↑
Salary ↑
```

---

## Negative Relationship

```text
X increases
↓
Y tends to decrease
```

Example:

```text
Price ↑
Demand ↓
```

---

## No Obvious Relationship

Values don't show a clear linear pattern.

---

# 41. GroupBy Analysis

`groupby()` is extremely important in EDA.

Example:

```python
df.groupby("Department")["Salary"].mean()
```

Output might look like:

```text
Department
Finance    55000
HR         45000
IT         65000
Sales      50000
```

This tells us average salary by department.

---

## Multiple Statistics

```python
df.groupby("Department")["Salary"].agg(
    ["count", "mean", "median", "min", "max"]
)
```

This is extremely useful for analytical summaries.

---

# 42. EDA with Pandas

Pandas is the primary tool for tabular EDA.

Important functions:

```python
df.head()
df.tail()
df.sample()
df.shape
df.columns
df.dtypes
df.info()
df.describe()
df.isnull().sum()
df.duplicated().sum()
df.nunique()
df["column"].unique()
df["column"].value_counts()
df.sort_values()
df.groupby()
df.corr()
```

---

# 43. EDA with NumPy

NumPy is useful for numerical calculations.

```python
import numpy as np

data = np.array([10, 20, 30, 40, 50])

print(np.mean(data))
print(np.median(data))
print(np.std(data))
print(np.var(data))
print(np.min(data))
print(np.max(data))
```

NumPy is particularly useful for:

```text
Numerical arrays
Mathematical operations
Vectorized calculations
Numerical transformations
```

---

# 44. EDA with Matplotlib

Matplotlib provides low-level/general-purpose plotting capabilities.

```python
import matplotlib.pyplot as plt
```

Common plots:

```text
plot()
scatter()
bar()
hist()
boxplot()
pie()
```

Example:

```python
plt.hist(df["Salary"])
plt.show()
```

---

# 45. EDA with Seaborn

Seaborn provides a higher-level statistical visualization interface built on Matplotlib.

```python
import seaborn as sns
```

Common EDA functions:

```python
sns.histplot()
sns.boxplot()
sns.countplot()
sns.scatterplot()
sns.lineplot()
sns.heatmap()
sns.pairplot()
```

---

# 46. Complete EDA Workflow

Here is a practical EDA process.

## Step 1 — Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## Step 2 — Load Data

```python
df = pd.read_csv("data.csv")
```

---

## Step 3 — Inspect Data

```python
print(df.head())
print(df.tail())
```

---

## Step 4 — Check Shape

```python
print(df.shape)
```

---

## Step 5 — Check Columns

```python
print(df.columns)
```

---

## Step 6 — Check Data Types

```python
print(df.dtypes)
```

---

## Step 7 — Check Information

```python
df.info()
```

---

## Step 8 — Statistical Summary

```python
print(df.describe())
```

---

## Step 9 — Missing Values

```python
print(df.isnull().sum())
```

---

## Step 10 — Duplicate Records

```python
print(df.duplicated().sum())
```

---

## Step 11 — Unique Values

```python
for column in df.columns:
    print(column)
    print(df[column].nunique())
```

---

## Step 12 — Categorical Analysis

```python
print(df["Department"].value_counts())
```

---

## Step 13 — Numerical Analysis

```python
print(df["Salary"].mean())
print(df["Salary"].median())
print(df["Salary"].std())
```

---

## Step 14 — Outlier Analysis

```python
sns.boxplot(
    data=df,
    y="Salary"
)

plt.show()
```

---

## Step 15 — Distribution

```python
sns.histplot(
    data=df,
    x="Salary",
    kde=True
)

plt.show()
```

---

## Step 16 — Correlation

```python
corr = df.corr(numeric_only=True)

print(corr)
```

---

## Step 17 — Correlation Heatmap

```python
sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm"
)

plt.show()
```

---

## Step 18 — Relationship Analysis

```python
sns.scatterplot(
    data=df,
    x="Age",
    y="Salary"
)

plt.show()
```

---

## Step 19 — Group Analysis

```python
print(
    df.groupby("Department")["Salary"].mean()
)
```

---

# 47. Real-World Example

Suppose we have an employee dataset:

```text
Employee_ID
Name
Age
Gender
Department
Experience
Salary
Performance
```

---

## Question 1: How many employees?

```python
len(df)
```

or:

```python
df.shape[0]
```

---

## Question 2: What is the average salary?

```python
df["Salary"].mean()
```

---

## Question 3: What is the median salary?

```python
df["Salary"].median()
```

---

## Question 4: Which department has the most employees?

```python
df["Department"].value_counts()
```

---

## Question 5: Which department has the highest average salary?

```python
df.groupby(
    "Department"
)["Salary"].mean().sort_values(
    ascending=False
)
```

---

## Question 6: Are there missing values?

```python
df.isnull().sum()
```

---

## Question 7: Are there duplicate rows?

```python
df.duplicated().sum()
```

---

## Question 8: Is salary related to experience?

```python
df[["Experience", "Salary"]].corr()
```

Visualize:

```python
sns.scatterplot(
    data=df,
    x="Experience",
    y="Salary"
)

plt.show()
```

---

## Question 9: Are there salary outliers?

```python
sns.boxplot(
    data=df,
    y="Salary"
)

plt.show()
```

---

# 48. EDA Checklist

When you receive a new dataset, use this checklist.

## A. Understand

```text
☐ What does the dataset represent?
☐ What is one row?
☐ What does each column mean?
☐ What is the target/business question?
```

---

## B. Structure

```text
☐ Number of rows
☐ Number of columns
☐ Column names
☐ Data types
```

Commands:

```python
df.shape
df.columns
df.dtypes
df.info()
```

---

## C. Data Quality

```text
☐ Missing values
☐ Duplicates
☐ Invalid values
☐ Inconsistent categories
☐ Incorrect data types
```

Commands:

```python
df.isnull().sum()
df.duplicated().sum()
```

---

## D. Statistics

```text
☐ Mean
☐ Median
☐ Mode
☐ Minimum
☐ Maximum
☐ Standard deviation
☐ Quartiles
```

Command:

```python
df.describe()
```

---

## E. Distribution

```text
☐ Histogram
☐ Box plot
☐ Skewness
☐ Outliers
```

---

## F. Relationships

```text
☐ Correlation
☐ Scatter plots
☐ Grouped analysis
☐ Categorical relationships
```

---

## G. Visualization

```text
☐ Histogram
☐ Box plot
☐ Bar chart
☐ Scatter plot
☐ Line chart
☐ Heatmap
☐ Pair plot
```

---

# 49. Common Mistakes

## Mistake 1 — Starting analysis without understanding the data

Always understand:

```text
What is a row?
What is a column?
What does each variable mean?
```

---

## Mistake 2 — Ignoring missing values

Never assume missing values don't matter.

Check:

```python
df.isnull().sum()
```

---

## Mistake 3 — Ignoring duplicates

Check:

```python
df.duplicated().sum()
```

---

## Mistake 4 — Automatically removing outliers

An outlier may be:

```text
Error
OR
A genuine observation
```

Do not remove it blindly.

---

## Mistake 5 — Assuming correlation means causation

```text
Correlation
≠
Causation
```

---

## Mistake 6 — Only looking at statistics

Numbers alone may hide patterns.

Always combine:

```text
Statistics
+
Visualization
```

---

## Mistake 7 — Creating too many visualizations

EDA should answer questions.

Do not create charts simply because you can.

---

# 50. Interview Questions

## Q1. What is EDA?

> Exploratory Data Analysis is the process of examining, summarizing, visualizing, and investigating data to understand its structure, quality, distributions, relationships, and patterns before deeper analysis or modeling.

---

## Q2. Why is EDA important?

> EDA helps identify data-quality issues, distributions, outliers, relationships, patterns, and potential assumptions before statistical analysis or machine learning.

---

## Q3. What are the types of EDA?

```text
Univariate
Bivariate
Multivariate
```

---

## Q4. What is univariate analysis?

> Analysis of one variable at a time.

Example:

```python
df["Age"].describe()
```

---

## Q5. What is bivariate analysis?

> Analysis of the relationship between two variables.

Example:

```text
Age vs Salary
```

---

## Q6. What is multivariate analysis?

> Analysis involving three or more variables.

---

## Q7. How do you check missing values?

```python
df.isnull().sum()
```

---

## Q8. How do you check duplicates?

```python
df.duplicated().sum()
```

---

## Q9. How do you check data types?

```python
df.dtypes
```

or:

```python
df.info()
```

---

## Q10. How do you find unique values?

```python
df["column"].unique()
```

---

## Q11. How do you find the frequency of categories?

```python
df["column"].value_counts()
```

---

## Q12. How do you detect outliers?

Common methods include:

```text
Box plots
IQR method
Z-scores
Domain-specific rules
```

---

## Q13. What is correlation?

> Correlation measures the direction and strength of a linear relationship between two variables.

---

## Q14. What is a heatmap used for?

> A heatmap can visually represent a matrix of values. In EDA it is commonly used to display a correlation matrix.

---

## Q15. What is the purpose of `describe()`?

> It provides summary statistics for columns, especially numerical columns, including count, mean, standard deviation, minimum, quartiles, and maximum.

---

## Q16. Difference between EDA and data cleaning?

> EDA focuses on understanding and discovering patterns or issues in data, while data cleaning focuses on correcting data-quality problems. Cleaning can be part of an iterative EDA process.

---

## Q17. Difference between EDA and data preprocessing?

> EDA is primarily about understanding and exploring the data. Preprocessing prepares data into a form suitable for analysis or machine learning, such as through encoding, scaling, transformation, and feature engineering.

---

# 51. Quick Revision

## EDA

```text
Exploratory Data Analysis
↓
Understand data
↓
Find problems
↓
Find patterns
↓
Find relationships
↓
Generate insights
```

---

## Main EDA Categories

```text
                 EDA
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Univariate  Bivariate  Multivariate
       │          │          │
       ↓          ↓          ↓
    1 variable  2 variables 3+ variables
```

---

## Important Pandas Commands

```python
df.head()
df.tail()
df.sample()
df.shape
df.columns
df.dtypes
df.info()
df.describe()

df.isnull().sum()
df.duplicated().sum()

df["column"].unique()
df["column"].nunique()
df["column"].value_counts()

df.sort_values()
df.groupby()

df.corr(numeric_only=True)
```

---

## Important Visualizations

```text
Histogram
    ↓
Distribution

Box Plot
    ↓
Outliers + Spread

Bar Chart
    ↓
Categories

Scatter Plot
    ↓
Relationship

Line Chart
    ↓
Trend over ordered/time data

Heatmap
    ↓
Matrix / Correlation

Pair Plot
    ↓
Multiple relationships
```

---

# 🧠 EDA Mental Model

Remember EDA using:

```text
                 EDA
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
   UNDERSTAND            INVESTIGATE
        │                   │
   shape/types          relationships
   columns              correlations
   categories           patterns
        │                   │
        └─────────┬─────────┘
                  ↓
              CHECK DATA
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     Missing   Duplicate  Outliers
        │         │         │
        └─────────┼─────────┘
                  ↓
             SUMMARIZE
                  │
        mean / median / std
        quartiles / counts
                  ↓
            VISUALIZE
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     Histogram  Boxplot   Scatter
        │         │         │
        └─────────┼─────────┘
                  ↓
              INSIGHTS
                  ↓
         CLEAN / TRANSFORM
                  ↓
          FURTHER ANALYSIS
                  ↓
           MACHINE LEARNING
```

---

# 🔥 Most Important EDA Commands to Memorize

```python
# Basic inspection
df.head()
df.shape
df.columns
df.info()
df.describe()

# Missing values
df.isnull().sum()

# Duplicates
df.duplicated().sum()

# Categories
df["column"].unique()
df["column"].value_counts()

# Statistics
df["column"].mean()
df["column"].median()
df["column"].std()
df["column"].min()
df["column"].max()

# Group analysis
df.groupby("category")["value"].mean()

# Correlation
df.corr(numeric_only=True)

# Visualization
sns.histplot(data=df, x="column")
sns.boxplot(data=df, y="column")
sns.scatterplot(data=df, x="x", y="y")
sns.heatmap(df.corr(numeric_only=True), annot=True)
```

---

# 🎯 Final Concept

The easiest way to remember EDA is:

```text
                 EDA
                  ↓
             "Know Your Data"
                  ↓
       ┌──────────┼──────────┐
       ↓          ↓          ↓
    Structure   Quality    Patterns
       ↓          ↓          ↓
     shape      missing    trends
     types      duplicate  relationships
     columns    outliers   distributions
       └──────────┼──────────┘
                  ↓
             Statistics
                  +
            Visualization
                  ↓
              Insights
```

> **EDA is not simply `df.describe()` or creating graphs.** It is a systematic process of asking meaningful questions about a dataset, using statistics and visualizations to investigate those questions, identifying data-quality issues and patterns, and using what you learn to decide what should happen next.

## 🔗 Relationship with your previous topics

```text
Python
  ↓
NumPy
  ↓
Pandas
  ↓
Data Cleaning
  ↓
Data Manipulation
  ↓
Data Preprocessing
  ↓
Statistics
  ↓
EDA  ← combines many of these concepts
  ↓
Data Visualization
  ↓
Data Analysis / Machine Learning
```

EDA therefore acts as a **bridge between raw/prepared data and deeper statistical analysis or machine learning**.
