# 📊 Data Preprocessing in Data Analytics

> Complete beginner-to-advanced notes on Data Preprocessing, covering data cleaning, integration, transformation, reduction, encoding, scaling, feature engineering, outliers, missing values, preprocessing for analytics and machine learning, and practical Python examples.

---

# 📚 Table of Contents

1. [What is Data Preprocessing?](#1-what-is-data-preprocessing)
2. [Technical Definition](#2-technical-definition)
3. [Why Data Preprocessing is Required](#3-why-data-preprocessing-is-required)
4. [Raw Data vs Processed Data](#4-raw-data-vs-processed-data)
5. [Data Cleaning vs Data Preprocessing](#5-data-cleaning-vs-data-preprocessing)
6. [Data Preprocessing vs Data Transformation](#6-data-preprocessing-vs-data-transformation)
7. [Data Preprocessing Pipeline](#7-data-preprocessing-pipeline)
8. [Step 1: Understanding the Dataset](#8-step-1-understanding-the-dataset)
9. [Data Profiling](#9-data-profiling)
10. [Data Quality Checks](#10-data-quality-checks)
11. [Step 2: Handling Missing Data](#11-step-2-handling-missing-data)
12. [Types of Missing Data](#12-types-of-missing-data)
13. [Deleting Missing Values](#13-deleting-missing-values)
14. [Mean Imputation](#14-mean-imputation)
15. [Median Imputation](#15-median-imputation)
16. [Mode Imputation](#16-mode-imputation)
17. [Forward Fill and Backward Fill](#17-forward-fill-and-backward-fill)
18. [Interpolation](#18-interpolation)
19. [Advanced Missing Value Imputation](#19-advanced-missing-value-imputation)
20. [Step 3: Handling Duplicate Data](#20-step-3-handling-duplicate-data)
21. [Step 4: Handling Incorrect Data](#21-step-4-handling-incorrect-data)
22. [Step 5: Handling Inconsistent Data](#22-step-5-handling-inconsistent-data)
23. [Step 6: Handling Invalid Data](#23-step-6-handling-invalid-data)
24. [Step 7: Data Type Conversion](#24-step-7-data-type-conversion)
25. [Step 8: Handling Outliers](#25-step-8-handling-outliers)
26. [What are Outliers?](#26-what-are-outliers)
27. [IQR Method](#27-iqr-method)
28. [Z-Score Method](#28-z-score-method)
29. [Outlier Treatment](#29-outlier-treatment)
30. [Step 9: Data Integration](#30-step-9-data-integration)
31. [Data Integration Problems](#31-data-integration-problems)
32. [Step 10: Data Transformation](#32-step-10-data-transformation)
33. [Scaling](#33-scaling)
34. [Normalization](#34-normalization)
35. [Standardization](#35-standardization)
36. [Robust Scaling](#36-robust-scaling)
37. [Log Transformation](#37-log-transformation)
38. [Power Transformation](#38-power-transformation)
39. [Quantile Transformation](#39-quantile-transformation)
40. [Step 11: Encoding Categorical Data](#40-step-11-encoding-categorical-data)
41. [Label Encoding](#41-label-encoding)
42. [Ordinal Encoding](#42-ordinal-encoding)
43. [One-Hot Encoding](#43-one-hot-encoding)
44. [Binary Encoding](#44-binary-encoding)
45. [Target Encoding](#45-target-encoding)
46. [Frequency Encoding](#46-frequency-encoding)
47. [Step 12: Feature Engineering](#47-step-12-feature-engineering)
48. [Step 13: Feature Selection](#48-step-13-feature-selection)
49. [Step 14: Feature Extraction](#49-step-14-feature-extraction)
50. [Step 15: Data Reduction](#50-step-15-data-reduction)
51. [Sampling](#51-sampling)
52. [Dimensionality Reduction](#52-dimensionality-reduction)
53. [PCA](#53-pca)
54. [Step 16: Handling Skewness](#54-step-16-handling-skewness)
55. [Step 17: Date and Time Preprocessing](#55-step-17-date-and-time-preprocessing)
56. [Step 18: Text Preprocessing](#56-step-18-text-preprocessing)
57. [Step 19: Train-Test Split](#57-step-19-train-test-split)
58. [Validation Data](#58-validation-data)
59. [Data Leakage](#59-data-leakage)
60. [Preprocessing for Machine Learning](#60-preprocessing-for-machine-learning)
61. [Preprocessing for Data Analytics](#61-preprocessing-for-data-analytics)
62. [Preprocessing for Time Series](#62-preprocessing-for-time-series)
63. [Preprocessing Using Python](#63-preprocessing-using-python)
64. [Preprocessing Using SQL](#64-preprocessing-using-sql)
65. [Scikit-Learn Pipeline](#65-scikit-learn-pipeline)
66. [ColumnTransformer](#66-columntransformer)
67. [Common Preprocessing Mistakes](#67-common-preprocessing-mistakes)
68. [Best Practices](#68-best-practices)
69. [Complete Preprocessing Workflow](#69-complete-preprocessing-workflow)
70. [Real-World Example](#70-real-world-example)
71. [Interview Questions](#71-interview-questions)
72. [Final Revision](#72-final-revision)

---

# 1. What is Data Preprocessing?

## Easy Definition

**Data preprocessing is the process of converting raw data into a clean, consistent, structured, and suitable form for analysis or machine learning.**

Raw data is rarely ready to use directly.

It may contain:

```text
Missing values
Duplicates
Incorrect values
Different formats
Outliers
Categorical values
Different scales
Unnecessary columns
Text
Dates
Noise
Inconsistent representations
```

Preprocessing prepares this data for the next stage.

---

# 2. Technical Definition

> **Data preprocessing is a systematic process of cleaning, integrating, transforming, encoding, reducing, and preparing raw data so that it satisfies the requirements of statistical analysis, visualization, machine learning, or other analytical tasks.**

---

# 3. Why Data Preprocessing is Required

Real-world data is usually messy.

Example:

| Name  |  Age | Salary | Gender | City      |
| ----- | ---: | -----: | ------ | --------- |
| Ravi  |   25 |  30000 | Male   | Hyderabad |
| Priya | NULL |  45000 | Female | Hyderabad |
| Arun  |   -5 |  50000 | M      | hyderabad |
| Ravi  |   25 |  30000 | Male   | Hyderabad |

Problems:

```text
Age = NULL
Age = -5
Male / M
Hyderabad / hyderabad
Duplicate Ravi
```

Before analysis, these issues may need to be addressed.

---

# 4. Raw Data vs Processed Data

## Raw Data

Data directly collected from sources.

```text
CSV
Excel
Database
API
Sensors
Websites
Applications
Logs
Surveys
```

It may be:

```text
Messy
Incomplete
Inconsistent
Unstructured
Duplicated
```

---

## Processed Data

Data after appropriate preprocessing.

```text
Clean
Structured
Consistent
Validated
Transformed
Analysis-ready
```

---

# 5. Data Cleaning vs Data Preprocessing

These concepts are related but **not identical**.

## Data Cleaning

Focuses primarily on fixing data-quality problems.

Examples:

```text
Missing values
Duplicates
Invalid values
Incorrect formats
Inconsistent values
```

## Data Preprocessing

Is broader.

It can include:

```text
Data Cleaning
Data Integration
Data Transformation
Encoding
Scaling
Feature Engineering
Feature Selection
Dimensionality Reduction
Data Splitting
```

Therefore:

> **Data cleaning is a component of data preprocessing.**

---

# 6. Data Preprocessing vs Data Transformation

### Data Transformation

Changing the representation or scale of data.

Examples:

```text
Standardization
Normalization
Log transformation
Encoding
Aggregation
```

### Data Preprocessing

The complete preparation process.

```text
Preprocessing
│
├── Cleaning
├── Integration
├── Transformation
├── Encoding
├── Feature Engineering
├── Feature Selection
├── Reduction
└── Splitting
```

Therefore:

> **Transformation is one part of preprocessing.**

---

# 7. Data Preprocessing Pipeline

A typical workflow:

```text
Raw Data
   ↓
Data Understanding
   ↓
Data Profiling
   ↓
Data Cleaning
   ↓
Data Integration
   ↓
Data Transformation
   ↓
Encoding
   ↓
Outlier Treatment
   ↓
Feature Engineering
   ↓
Feature Selection
   ↓
Feature Scaling
   ↓
Train/Test Split
   ↓
Model / Analysis
```

The exact order can vary depending on the problem.

---

# 8. Step 1: Understanding the Dataset

Before modifying data, understand it.

Questions:

```text
What does each row represent?
What does each column represent?
What is the data source?
What is the target variable?
What are the data types?
Which columns are categorical?
Which columns are numerical?
Are there missing values?
Are there duplicates?
Are there outliers?
```

---

## Python

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df.head())
print(df.shape)
print(df.columns)
print(df.dtypes)
```

---

# 9. Data Profiling

Data profiling means examining the dataset before preprocessing.

Important checks:

```python
df.info()
```

```python
df.describe()
```

```python
df.isnull().sum()
```

```python
df.nunique()
```

```python
df.duplicated().sum()
```

---

# 10. Data Quality Checks

Check:

### Completeness

```text
Are required values present?
```

### Accuracy

```text
Are values correct?
```

### Consistency

```text
Do representations agree?
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

---

# 11. Handling Missing Data

Missing data is one of the most common preprocessing problems.

Example:

```text
Age = NULL
Salary = NULL
City = NULL
```

---

# 12. Types of Missing Data

Statistical analysis commonly distinguishes:

## MCAR

**Missing Completely At Random**

Missingness is unrelated to observed and unobserved values.

---

## MAR

**Missing At Random**

Missingness may depend on other observed variables.

---

## MNAR

**Missing Not At Random**

Missingness depends on the missing value itself or unobserved factors.

---

# 13. Deleting Missing Values

## Drop Rows

```python
df.dropna()
```

Useful when:

```text
Very few rows are missing
Missing rows are not important
Dataset is large
```

---

## Drop Columns

```python
df.drop(columns=["unnecessary_column"])
```

Useful when a column has excessive missingness and is not useful.

But deletion should be based on the analytical context.

---

# 14. Mean Imputation

Replace missing numerical values with the mean.

Formula:

```text
Mean = Sum of values / Number of values
```

Python:

```python
df["age"] = df["age"].fillna(df["age"].mean())
```

Best suited when the distribution is reasonably symmetric and the mean is an appropriate summary.

---

# 15. Median Imputation

Replace missing values with the median.

```python
df["salary"] = df["salary"].fillna(df["salary"].median())
```

Median is often preferred when data contains outliers or is skewed.

---

# 16. Mode Imputation

Used mainly for categorical variables.

```python
df["city"] = df["city"].fillna(df["city"].mode()[0])
```

Example:

```text
Hyderabad
Hyderabad
Mumbai
NULL
Hyderabad
```

Mode:

```text
Hyderabad
```

---

# 17. Forward Fill and Backward Fill

Common in time-series data.

## Forward Fill

Uses the previous known value.

```python
df["price"] = df["price"].ffill()
```

Example:

```text
10
10
NULL
10
```

---

## Backward Fill

Uses the next known value.

```python
df["price"] = df["price"].bfill()
```

These methods should be used only when their assumptions make sense.

---

# 18. Interpolation

Interpolation estimates missing values based on surrounding observations.

Example:

```text
10
20
NULL
40
50
```

Possible interpolated value:

```text
30
```

Python:

```python
df["sales"] = df["sales"].interpolate()
```

Especially useful for ordered/time-series data when appropriate.

---

# 19. Advanced Missing Value Imputation

More advanced techniques include:

```text
KNN Imputation
Regression Imputation
Multiple Imputation
Iterative Imputation
Model-based Imputation
```

---

## KNN Imputation

Finds similar observations and uses their values to estimate missing values.

---

## Iterative Imputation

Predicts missing values using other features and iteratively refines the estimates.

---

## Important

More sophisticated imputation is not automatically better.

The method should match:

```text
Data type
Missingness mechanism
Distribution
Business meaning
Analytical goal
```

---

# 20. Handling Duplicate Data

Check:

```python
df.duplicated().sum()
```

Remove exact duplicates:

```python
df = df.drop_duplicates()
```

---

## Subset-Based Duplicate Detection

```python
df.duplicated(subset=["customer_id"]).sum()
```

Remove based on a business key:

```python
df = df.drop_duplicates(
    subset=["customer_id"],
    keep="first"
)
```

Do not blindly remove duplicates without understanding what defines a unique record.

---

# 21. Handling Incorrect Data

Example:

```text
Age = -10
```

If age cannot be negative, investigate the source.

Possible actions:

```text
Correct
Replace
Remove
Set to missing
Flag for review
```

The correct choice depends on available evidence.

---

# 22. Handling Inconsistent Data

Example:

```text
Male
M
male
MALE
```

Standardize:

```python
df["gender"] = df["gender"].str.strip().str.lower()
```

Result:

```text
male
```

---

# 23. Handling Invalid Data

Example:

```text
Age = 500
```

Validation rule:

```text
0 <= age <= 120
```

Python:

```python
df.loc[
    (df["age"] < 0) | (df["age"] > 120),
    "age"
] = None
```

But in real projects, the valid range should come from domain/business rules rather than an arbitrary assumption.

---

# 24. Data Type Conversion

Correct data types are important.

Example:

```python
df["age"] = df["age"].astype("Int64")
```

---

## Date Conversion

```python
df["date"] = pd.to_datetime(df["date"])
```

---

## Numeric Conversion

```python
df["salary"] = pd.to_numeric(
    df["salary"],
    errors="coerce"
)
```

Invalid values become missing with `errors="coerce"`.

---

# 25. Handling Outliers

An outlier is an observation that is unusually far from the typical pattern of the data.

Example:

```text
20
22
21
23
24
500
```

500 may be an outlier.

But:

> **An outlier is not automatically an error.**

It could represent:

```text
Real high-value customer
Fraud
Measurement error
Data-entry error
Rare event
```

---

# 26. What are Outliers?

Outliers can be identified using:

```text
IQR
Z-score
Modified Z-score
Percentiles
Visualizations
Domain rules
```

---

# 27. IQR Method

IQR:

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
Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["salary"] < lower) |
    (df["salary"] > upper)
]
```

---

# 28. Z-Score Method

Formula:

```text
z = (x - μ) / σ
```

Where:

```text
x = observation
μ = mean
σ = standard deviation
```

A large absolute z-score indicates an observation far from the mean.

A common heuristic is:

```text
|z| > 3
```

but this is not a universal rule.

---

# 29. Outlier Treatment

Possible methods:

```text
Keep
Remove
Cap/Winsorize
Transform
Replace
Investigate
```

---

## Capping

Example:

```python
df["salary"] = df["salary"].clip(
    lower=lower,
    upper=upper
)
```

Never remove an outlier merely because it is inconvenient for the analysis.

---

# 30. Data Integration

Data integration combines data from multiple sources.

Example:

```text
CRM
 +
Sales Database
 +
Marketing Platform
 +
Website
 ↓
Integrated Dataset
```

---

# 31. Data Integration Problems

Common issues:

```text
Different column names
Different data types
Different formats
Different units
Different identifiers
Duplicate entities
Different definitions
```

---

## Example

System A:

```text
customer_id
```

System B:

```text
cust_id
```

They may represent the same concept but need mapping.

---

# 32. Data Transformation

Transformation changes data into a more useful representation.

Examples:

```text
Scaling
Normalization
Standardization
Encoding
Aggregation
Log transformation
Date extraction
Unit conversion
```

---

# 33. Scaling

Scaling changes numerical variables to comparable ranges.

Example:

```text
Age:      18–80
Salary:   20,000–500,000
```

Salary has much larger numerical magnitude.

Some algorithms can be sensitive to this difference.

---

# 34. Normalization

Normalization commonly means **Min-Max scaling**.

Formula:

```text
x' = (x - min(x)) / (max(x) - min(x))
```

Typically produces values between:

```text
0 and 1
```

---

## Python

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

df["salary_scaled"] = scaler.fit_transform(
    df[["salary"]]
)
```

---

# 35. Standardization

Formula:

```text
z = (x - μ) / σ
```

After standardization, the transformed variable generally has:

```text
Mean ≈ 0
Standard deviation ≈ 1
```

---

## Python

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

df["salary_scaled"] = scaler.fit_transform(
    df[["salary"]]
)
```

---

# 36. Robust Scaling

Robust scaling uses:

```text
Median
IQR
```

It is less sensitive to extreme values.

Conceptually:

```text
x' = (x - median) / IQR
```

Python:

```python
from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()
```

---

# 37. Log Transformation

Useful for heavily right-skewed positive data.

Example:

```text
Income
Sales
Transaction Amount
```

Transformation:

```python
import numpy as np

df["log_sales"] = np.log1p(df["sales"])
```

`log1p(x)` computes:

```text
log(1 + x)
```

and is convenient when zero values are present.

---

# 38. Power Transformation

Power transformations can make distributions more symmetric.

Common methods include:

```text
Box-Cox
Yeo-Johnson
```

Scikit-learn:

```python
from sklearn.preprocessing import PowerTransformer

pt = PowerTransformer()
```

Box-Cox has restrictions on the input values, while Yeo-Johnson can handle zero and negative values.

---

# 39. Quantile Transformation

Transforms data based on its rank/quantiles.

```python
from sklearn.preprocessing import QuantileTransformer

qt = QuantileTransformer(
    output_distribution="normal"
)
```

Useful in some cases when distributions are highly non-normal, but it changes the original distribution substantially.

---

# 40. Encoding Categorical Data

Machine learning algorithms generally require numerical representations of categorical variables.

Example:

```text
City

Hyderabad
Mumbai
Delhi
```

Need to be represented appropriately.

---

# 41. Label Encoding

Maps categories to integer labels.

Example:

```text
Red    → 0
Blue   → 1
Green  → 2
```

This can be appropriate for target labels or genuinely ordinal categories in the right context.

---

## Warning

Using arbitrary integers for nominal categories can create a false ordering.

For example:

```text
Mumbai = 0
Delhi = 1
Hyderabad = 2
```

does not mean Hyderabad > Delhi > Mumbai.

---

# 42. Ordinal Encoding

Used when categories have a natural order.

Example:

```text
Low
Medium
High
```

Can be encoded:

```text
Low    → 1
Medium → 2
High   → 3
```

---

# 43. One-Hot Encoding

Creates one binary column per category.

Original:

```text
City
```

Values:

```text
Hyderabad
Mumbai
Delhi
```

Becomes:

| Hyderabad | Mumbai | Delhi |
| --------: | -----: | ----: |
|         1 |      0 |     0 |
|         0 |      1 |     0 |
|         0 |      0 |     1 |

Python:

```python
pd.get_dummies(
    df,
    columns=["city"],
    dtype=int
)
```

---

# 44. Binary Encoding

Represents categories using binary digits.

Useful when a categorical feature has many distinct categories.

It can reduce the number of columns compared with one-hot encoding.

---

# 45. Target Encoding

Replaces a category with a statistic based on the target.

Example:

```text
City → Average purchase
```

Potentially:

```text
Hyderabad → 5000
Mumbai    → 7000
Delhi     → 4500
```

### Critical Warning

Target encoding can cause **target leakage** if calculated using the full dataset before splitting.

It should be performed using training data appropriately, often with smoothing/cross-fitting techniques.

---

# 46. Frequency Encoding

Replace a category with its frequency or proportion.

Example:

```text
Hyderabad → 500
Mumbai    → 300
Delhi     → 200
```

Useful for high-cardinality categorical variables in some modeling contexts.

---

# 47. Feature Engineering

Feature engineering creates useful variables from existing data.

Example:

```text
Date of Birth
```

can become:

```text
Age
```

---

## Example

```python
df["age"] = (
    pd.Timestamp.today().year
    - df["birth_date"].dt.year
)
```

A production implementation should account carefully for whether the birthday has occurred yet.

---

## Other Examples

```text
Total Price = Quantity × Unit Price

Profit = Revenue - Cost

Conversion Rate = Conversions / Visitors

Age Group = Age → category
```

---

# 48. Feature Selection

Feature selection means choosing useful existing features and removing unnecessary ones.

Example:

```text
100 columns
      ↓
Feature Selection
      ↓
25 useful columns
```

Benefits:

```text
Less noise
Faster training
Lower complexity
Better interpretability
Potentially better generalization
```

---

## Methods

```text
Correlation-based methods
Filter methods
Wrapper methods
Embedded methods
Mutual information
Model-based importance
```

---

# 49. Feature Extraction

Feature extraction creates new features from existing features.

Difference:

```text
Feature Selection
→ Choose existing features

Feature Extraction
→ Create new representations
```

Examples:

```text
PCA
TF-IDF
Embeddings
```

---

# 50. Data Reduction

Data reduction reduces the amount or dimensionality of data while attempting to preserve useful information.

Methods:

```text
Sampling
Aggregation
Feature Selection
Dimensionality Reduction
Compression
```

---

# 51. Sampling

Sampling selects a subset of observations.

Types:

```text
Simple Random Sampling
Stratified Sampling
Systematic Sampling
Cluster Sampling
```

---

## Stratified Sampling

Preserves important subgroup proportions.

Example:

```text
Population:
70% Class A
30% Class B
```

A stratified sample attempts to maintain similar proportions.

---

# 52. Dimensionality Reduction

Reduces the number of features.

Example:

```text
100 features
     ↓
20 features
```

Methods:

```text
PCA
LDA
Autoencoders
```

The appropriate method depends on the task.

---

# 53. PCA

**Principal Component Analysis**

PCA transforms correlated variables into a smaller number of new variables called **principal components**.

The components are ordered by the amount of variance they explain.

Example:

```text
50 features
     ↓
PCA
     ↓
10 components
```

---

## Basic Python

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)

X_reduced = pca.fit_transform(X)
```

---

## Important

PCA is sensitive to feature scale, so numerical features are commonly standardized before PCA.

---

# 54. Handling Skewness

Skewness describes asymmetry in a distribution.

### Right Skew

Long tail toward larger values.

Common examples:

```text
Income
Sales
House prices
Transaction values
```

---

## Possible Transformations

```text
Log
Square root
Power transformation
Yeo-Johnson
```

But transformation should be driven by the analytical/modeling need, not applied automatically.

---

# 55. Date and Time Preprocessing

Raw date:

```text
2026-08-08 14:35:22
```

Can be decomposed into:

```text
Year
Month
Day
Hour
Minute
Day of Week
Week of Year
Quarter
```

---

## Python

```python
df["date"] = pd.to_datetime(df["date"])

df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day
df["day_of_week"] = df["date"].dt.dayofweek
```

---

## Time Differences

```python
df["days_since_signup"] = (
    df["today"] - df["signup_date"]
).dt.days
```

---

# 56. Text Preprocessing

For text analytics, common steps include:

```text
Lowercasing
Removing unwanted characters
Tokenization
Stop-word handling
Stemming
Lemmatization
Vectorization
```

Example:

```text
"I LOVE Python!!!"
```

May become:

```text
"i love python"
```

---

## Text Representation

Machine learning requires numerical representations.

Common techniques:

```text
Bag of Words
TF-IDF
Word embeddings
Sentence embeddings
```

---

# 57. Train-Test Split

For supervised machine learning, data is commonly divided into:

```text
Training Data
Validation Data
Test Data
```

Example:

```text
70% Training
15% Validation
15% Test
```

Other ratios are also possible.

---

## Python

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

---

# 58. Validation Data

Validation data is used for:

```text
Model selection
Hyperparameter tuning
Threshold selection
Feature decisions
```

Test data should remain untouched until final evaluation.

---

# 59. Data Leakage

One of the most important preprocessing concepts.

## Definition

> Data leakage occurs when information unavailable at prediction time improperly influences model training or evaluation.

Example:

You calculate a feature using the target or future information.

```text
Future information
       ↓
Training data
       ↓
Artificially high performance
```

---

## Preprocessing Leakage

Suppose you calculate the mean and standard deviation using the entire dataset before splitting.

```python
scaler.fit(X)
```

before train/test split.

Information from the test set influences the transformation.

Better:

```python
scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

---

# 60. Preprocessing for Machine Learning

Typical ML pipeline:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Train/Test Split
   ↓
Fit preprocessing on Training Data
   ↓
Transform Training Data
   ↓
Transform Validation/Test Data
   ↓
Model Training
   ↓
Evaluation
```

---

## Important Rule

> **Fit preprocessing transformations on training data only.**

Then use the fitted transformation to transform validation/test/new data.

---

# 61. Preprocessing for Data Analytics

For descriptive and business analytics, preprocessing may involve:

```text
Cleaning
Aggregation
Joining
Filtering
Date handling
Standardization
Derived metrics
Categorization
Outlier investigation
```

Example:

```text
Raw Transactions
       ↓
Remove invalid transactions
       ↓
Standardize dates
       ↓
Join customer information
       ↓
Calculate revenue
       ↓
Aggregate by month
       ↓
Business Dashboard
```

---

# 62. Preprocessing for Time Series

Time-series preprocessing may include:

```text
Sort by timestamp
Handle missing timestamps
Handle missing values
Resample
Aggregate
Create lag features
Create rolling features
Handle seasonality
Handle time zones
Detect anomalies
```

---

## Lag

```python
df["sales_lag_1"] = df["sales"].shift(1)
```

---

## Rolling Average

```python
df["rolling_7"] = (
    df["sales"]
    .rolling(7)
    .mean()
)
```

Be careful not to use future observations when constructing prediction features.

---

# 63. Preprocessing Using Python

Example dataset:

```python
import pandas as pd
import numpy as np

df = pd.read_csv("customers.csv")
```

---

## Inspect

```python
print(df.head())
print(df.shape)
print(df.info())
print(df.describe(include="all"))
```

---

## Missing Values

```python
print(df.isnull().sum())
```

---

## Duplicate Check

```python
print(df.duplicated().sum())
```

---

## Remove Exact Duplicates

```python
df = df.drop_duplicates()
```

---

## Standardize Text

```python
df["city"] = (
    df["city"]
    .str.strip()
    .str.lower()
)
```

---

## Convert Date

```python
df["order_date"] = pd.to_datetime(
    df["order_date"],
    errors="coerce"
)
```

---

## Convert Numeric

```python
df["sales"] = pd.to_numeric(
    df["sales"],
    errors="coerce"
)
```

---

# 64. Preprocessing Using SQL

## Find NULL values

```sql
SELECT COUNT(*) AS missing_age
FROM customers
WHERE age IS NULL;
```

---

## Find duplicates

```sql
SELECT
    customer_id,
    COUNT(*) AS cnt
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

---

## Handle invalid values

```sql
SELECT *
FROM customers
WHERE age < 0
   OR age > 120;
```

---

## Standardize categories

```sql
SELECT
    LOWER(TRIM(city)) AS city_clean
FROM customers;
```

---

## Create derived feature

```sql
SELECT
    quantity,
    unit_price,
    quantity * unit_price AS revenue
FROM sales;
```

---

# 65. Scikit-Learn Pipeline

For machine learning, pipelines help organize preprocessing and modeling.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("model", LogisticRegression())
])

pipeline.fit(X_train, y_train)

predictions = pipeline.predict(X_test)
```

---

# 66. ColumnTransformer

Different columns often need different preprocessing.

Example:

```text
Numerical columns
→ Imputation + Scaling

Categorical columns
→ Imputation + One-Hot Encoding
```

---

## Example

```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import (
    StandardScaler,
    OneHotEncoder
)

numeric_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("scaler", StandardScaler())
])

categorical_pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("encoder", OneHotEncoder(handle_unknown="ignore"))
])

preprocessor = ColumnTransformer([
    ("num", numeric_pipeline, numeric_columns),
    ("cat", categorical_pipeline, categorical_columns)
])
```

This is a common production-oriented pattern.

---

# 67. Common Preprocessing Mistakes

## Mistake 1: Removing all NULL rows

This can unnecessarily discard large amounts of data.

---

## Mistake 2: Filling all NULL values with zero

Zero may have a completely different meaning from missing.

---

## Mistake 3: Removing every outlier

Outliers may be legitimate observations.

---

## Mistake 4: Scaling before train/test split

Can cause leakage.

---

## Mistake 5: Encoding nominal categories with arbitrary numbers

Can create false ordering.

---

## Mistake 6: Using test data to choose preprocessing

This contaminates evaluation.

---

## Mistake 7: Ignoring business context

A statistically unusual value may be perfectly valid from a business perspective.

---

## Mistake 8: Changing raw data directly

Always preserve the original raw dataset.

---

# 68. Best Practices

## 1. Preserve raw data

```text
Raw Data
   ↓
Copy
   ↓
Preprocessing
```

Never destroy the original unnecessarily.

---

## 2. Profile before modifying

Understand the data first.

---

## 3. Document transformations

Record:

```text
What changed?
Why?
How?
When?
```

---

## 4. Use reproducible code

Avoid undocumented manual editing.

---

## 5. Validate after preprocessing

Check:

```text
Row count
Column count
Nulls
Duplicates
Ranges
Distributions
Relationships
```

---

## 6. Prevent leakage

Fit data-dependent transformations only on training data in predictive modeling.

---

## 7. Preserve business meaning

Do not blindly optimize statistical properties while destroying useful information.

---

# 69. Complete Preprocessing Workflow

A practical workflow:

```text
                 RAW DATA
                     ↓
             UNDERSTAND DATA
                     ↓
               PROFILE DATA
                     ↓
             CHECK DATA QUALITY
                     ↓
            ┌────────┴────────┐
            ↓                 ↓
       MISSING VALUES     DUPLICATES
            ↓                 ↓
       HANDLE THEM        HANDLE THEM
            └────────┬────────┘
                     ↓
             INVALID VALUES
                     ↓
              INCONSISTENCIES
                     ↓
              DATA TYPES
                     ↓
              OUTLIER REVIEW
                     ↓
             DATA INTEGRATION
                     ↓
             TRANSFORMATION
                     ↓
                ENCODING
                     ↓
           FEATURE ENGINEERING
                     ↓
             FEATURE SELECTION
                     ↓
            SCALING / TRANSFORM
                     ↓
             TRAIN / TEST SPLIT
                     ↓
             MODEL / ANALYSIS
```

For predictive modeling, some steps should occur **after the split** and be fitted only on training data.

---

# 70. Real-World Example

Suppose an e-commerce dataset contains:

| Customer |  Age | Income | City      | Gender | Purchase |
| -------- | ---: | -----: | --------- | ------ | -------: |
| A        |   25 |  30000 | Hyderabad | Male   |      500 |
| B        | NULL |  40000 | Mumbai    | Female |      700 |
| C        |  -10 |  50000 | hyderabad | M      |      900 |
| A        |   25 |  30000 | Hyderabad | Male   |      500 |
| D        |  200 |   NULL | Delhi     | Female |     1000 |

---

## Step 1 — Missing Values

```text
Age → missing
Income → missing
```

Investigate and handle according to the use case.

---

## Step 2 — Duplicates

Customer A appears twice.

Determine whether these are:

```text
Duplicate customer records
```

or

```text
Two legitimate transactions
```

before deleting anything.

---

## Step 3 — Invalid Values

```text
Age = -10
Age = 200
```

Investigate against domain rules.

---

## Step 4 — Standardization

```text
hyderabad → hyderabad
Hyderabad → hyderabad

M → male
Male → male
```

---

## Step 5 — Encoding

Gender:

```text
Male
Female
```

can be one-hot encoded if appropriate.

---

## Step 6 — Scaling

Income may have a much larger magnitude than age.

Depending on the model, scaling may be appropriate.

---

## Step 7 — Feature Engineering

Create:

```text
Income Group
Age Group
Purchase Frequency
Average Purchase
Customer Lifetime Value
```

where justified by the analytical objective.

---

# 71. Data Preprocessing for Different Tasks

| Task                  | Common Preprocessing                                      |
| --------------------- | --------------------------------------------------------- |
| Descriptive Analytics | Cleaning, aggregation, formatting                         |
| Business Analytics    | Cleaning, joins, calculations, aggregation                |
| Visualization         | Cleaning, transformation, aggregation                     |
| Machine Learning      | Cleaning, encoding, scaling, feature engineering          |
| Classification        | Encoding, imputation, scaling depending on algorithm      |
| Regression            | Cleaning, transformations, scaling depending on algorithm |
| Clustering            | Scaling, outlier handling, dimensionality reduction       |
| Time Series           | Dates, ordering, missing timestamps, lag features         |
| NLP                   | Tokenization, normalization, vectorization                |
| Deep Learning         | Scaling, encoding, tensor preparation                     |

---

# 72. Which Algorithms Need Scaling?

Scaling is particularly important for algorithms based on distances, magnitudes, or optimization behavior.

Common examples:

```text
KNN
K-Means
SVM
PCA
Many neural networks
Regularized linear/logistic models
```

Often less important for:

```text
Decision Trees
Random Forests
Many gradient-boosted tree implementations
```

because tree splits are based on feature thresholds rather than Euclidean distance or comparable feature magnitudes.

---

# 73. Preprocessing and Statistics

Preprocessing is closely connected to statistics.

Important concepts:

```text
Mean
Median
Mode
Variance
Standard Deviation
Percentiles
IQR
Correlation
Skewness
Distribution
Sampling
Probability
```

These help understand and transform data appropriately.

---

# 74. Preprocessing and Data Analytics

For data analytics, preprocessing helps produce trustworthy:

```text
Reports
Dashboards
KPIs
Visualizations
Aggregations
Statistical summaries
Business insights
```

Example:

```text
Raw Sales Data
      ↓
Remove invalid transactions
      ↓
Handle missing values
      ↓
Standardize categories
      ↓
Convert dates
      ↓
Calculate revenue
      ↓
Aggregate monthly
      ↓
Analyze sales trends
```

---

# 75. Preprocessing and Machine Learning

Machine learning adds additional concerns:

```text
Train/Test Split
Feature Engineering
Encoding
Scaling
Data Leakage
Cross-Validation
Pipeline Construction
Feature Selection
Dimensionality Reduction
```

---

# 76. Important Difference: Cleaning vs Preprocessing vs EDA

These three are frequently confused.

## Data Cleaning

```text
Fix data-quality problems.
```

Examples:

```text
Missing values
Duplicates
Invalid values
Formatting
```

---

## Data Preprocessing

```text
Prepare data for analysis/modeling.
```

Includes cleaning plus:

```text
Transformation
Encoding
Scaling
Feature engineering
Feature selection
```

---

## EDA

**Exploratory Data Analysis**

```text
Understand patterns, relationships,
distributions, trends, and anomalies.
```

EDA often informs preprocessing decisions.

---

# 77. Relationship Between Data Quality, Cleaning, Preprocessing and EDA

Think of it like this:

```text
                 DATA
                   ↓
              DATA QUALITY
                   ↓
             DATA PROFILING
                   ↓
                  EDA
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
 DATA CLEANING        PREPROCESSING
        ↓                     ↓
        └──────────┬──────────┘
                   ↓
            ANALYSIS / ML
```

In practice, EDA and preprocessing are often iterative rather than strictly sequential.

---

# 78. Most Important Formulas

## Mean

```text
Mean = Σx / n
```

---

## Standard Deviation

Conceptually:

```text
σ = √(Σ(x - μ)² / N)
```

The sample standard deviation uses `n - 1` in the denominator.

---

## Z-Score

```text
z = (x - μ) / σ
```

---

## IQR

```text
IQR = Q3 - Q1
```

---

## IQR Lower Bound

```text
Q1 - 1.5 × IQR
```

---

## IQR Upper Bound

```text
Q3 + 1.5 × IQR
```

---

## Min-Max Scaling

```text
x' = (x - min) / (max - min)
```

---

# 79. Important Interview Questions

## Q1. What is data preprocessing?

Data preprocessing is the process of preparing raw data for analysis or machine learning through activities such as cleaning, integration, transformation, encoding, feature engineering, and reduction.

---

## Q2. Why is preprocessing important?

Because real-world data is often:

```text
Incomplete
Inconsistent
Noisy
Unstructured
Duplicated
Incorrect
```

Preprocessing improves its suitability for analysis and modeling.

---

## Q3. Is data cleaning the same as preprocessing?

**No.**

Cleaning is one component of preprocessing.

---

## Q4. What are the main preprocessing steps?

```text
Data understanding
Profiling
Cleaning
Integration
Transformation
Encoding
Outlier handling
Feature engineering
Feature selection
Scaling
Dimensionality reduction
Data splitting
```

Not every project requires every step.

---

## Q5. What is normalization?

Often refers to Min-Max scaling:

```text
(x - min) / (max - min)
```

which maps values to a specified range, commonly 0 to 1.

---

## Q6. What is standardization?

Transformation using:

```text
(x - mean) / standard deviation
```

producing approximately mean 0 and standard deviation 1 under the usual standardization setup.

---

## Q7. Normalization vs standardization?

| Normalization         | Standardization             |
| --------------------- | --------------------------- |
| Often Min-Max scaling | Z-score transformation      |
| Usually fixed range   | Mean around 0               |
| Often 0 to 1          | Standard deviation around 1 |
| Sensitive to min/max  | Sensitive to mean/std       |

---

## Q8. What is data leakage?

When information that should not be available during model training influences training or evaluation.

---

## Q9. Why should scaling be fitted only on training data?

To prevent information from the validation/test data from influencing the transformation.

---

## Q10. Should every dataset be normalized?

**No.**

The appropriate transformation depends on:

```text
Algorithm
Distribution
Business meaning
Analytical goal
Feature properties
```

---

# 80. Final Revision

## 🔥 Remember This Pipeline

```text
RAW DATA
   ↓
UNDERSTAND
   ↓
PROFILE
   ↓
CLEAN
   ├── Missing Values
   ├── Duplicates
   ├── Invalid Values
   ├── Incorrect Values
   └── Inconsistencies
   ↓
INTEGRATE
   ↓
TRANSFORM
   ├── Scaling
   ├── Normalization
   ├── Standardization
   └── Log/Power Transform
   ↓
ENCODE
   ├── One-Hot
   ├── Ordinal
   └── Other Encodings
   ↓
OUTLIERS
   ↓
FEATURE ENGINEERING
   ↓
FEATURE SELECTION
   ↓
DIMENSIONALITY REDUCTION
   ↓
SPLIT DATA
   ↓
ANALYSIS / MACHINE LEARNING
```

---

# 🧠 One-Line Definitions for Revision

| Topic                        | One-Line Definition                                        |
| ---------------------------- | ---------------------------------------------------------- |
| **Data Preprocessing**       | Preparing raw data for analysis or modeling                |
| **Data Cleaning**            | Fixing or handling data-quality problems                   |
| **Data Integration**         | Combining data from multiple sources                       |
| **Data Transformation**      | Changing data representation into a useful form            |
| **Imputation**               | Estimating/replacing missing values                        |
| **Encoding**                 | Converting categorical data into a usable representation   |
| **Scaling**                  | Adjusting numerical feature magnitudes                     |
| **Normalization**            | Commonly Min-Max scaling                                   |
| **Standardization**          | Transforming using mean and standard deviation             |
| **Outlier**                  | An unusually extreme observation                           |
| **Feature Engineering**      | Creating useful features from available data               |
| **Feature Selection**        | Selecting useful existing features                         |
| **Feature Extraction**       | Creating new representations/features                      |
| **Dimensionality Reduction** | Reducing the number of dimensions/features                 |
| **Data Leakage**             | Improper use of information unavailable at prediction time |
| **Data Profiling**           | Examining data structure and quality                       |
| **Pipeline**                 | A reproducible sequence of preprocessing/modeling steps    |

---

# ⭐ Final Mental Model

```text
                DATA PREPROCESSING
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
     CLEANING      TRANSFORMATION   INTEGRATION
        │              │              │
        ↓              ↓              ↓
   Missing Values   Scaling         Multiple
   Duplicates       Encoding        Sources
   Invalid Data     Log Transform
   Inconsistency    Feature Eng.
        │              │
        └──────────────┼──────────────┘
                       ↓
                FEATURE PREPARATION
                       ↓
              TRAIN / TEST SEPARATION
                       ↓
                 ANALYSIS / MODEL
                       ↓
                    INSIGHTS
```

> **Core idea:** Data preprocessing is the bridge between **raw data and usable analytical data**. It includes much more than simply cleaning missing values. A strong preprocessing process considers **data quality, missing values, duplicates, invalid values, outliers, data types, integration, transformations, encoding, scaling, feature engineering, feature selection, dimensionality reduction, and leakage prevention**. The correct preprocessing strategy always depends on the **data, business problem, and analytical/modeling objective**.
