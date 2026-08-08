# 📊 Data Preprocessing in Python — Complete README

> Complete revision notes for **Data Preprocessing**, including theory, data cleaning, manipulation, transformation, encoding, scaling, feature engineering, feature selection, data splitting, and practical Python/Pandas/Scikit-learn examples.

---

# 📚 Table of Contents

1. [What is Data Preprocessing?](#1-what-is-data-preprocessing)
2. [Why is Data Preprocessing Important?](#2-why-is-data-preprocessing-important)
3. [Raw Data vs Processed Data](#3-raw-data-vs-processed-data)
4. [Data Preprocessing Workflow](#4-data-preprocessing-workflow)
5. [Data Preprocessing vs Data Cleaning vs Data Manipulation](#5-data-preprocessing-vs-data-cleaning-vs-data-manipulation)
6. [Types of Data Preprocessing](#6-types-of-data-preprocessing)
7. [Data Collection](#7-data-collection)
8. [Understanding the Dataset](#8-understanding-the-dataset)
9. [Handling Missing Values](#9-handling-missing-values)
10. [Handling Duplicate Data](#10-handling-duplicate-data)
11. [Handling Incorrect Data](#11-handling-incorrect-data)
12. [Handling Inconsistent Data](#12-handling-inconsistent-data)
13. [Handling Outliers](#13-handling-outliers)
14. [Data Type Conversion](#14-data-type-conversion)
15. [Data Transformation](#15-data-transformation)
16. [Data Manipulation](#16-data-manipulation)
17. [Categorical Data](#17-categorical-data)
18. [Label Encoding](#18-label-encoding)
19. [One-Hot Encoding](#19-one-hot-encoding)
20. [Ordinal Encoding](#20-ordinal-encoding)
21. [Feature Engineering](#21-feature-engineering)
22. [Feature Selection](#22-feature-selection)
23. [Feature Scaling](#23-feature-scaling)
24. [Normalization](#24-normalization)
25. [Standardization](#25-standardization)
26. [Train-Test Split](#26-train-test-split)
27. [Data Leakage](#27-data-leakage)
28. [Handling Imbalanced Data](#28-handling-imbalanced-data)
29. [Data Reduction](#29-data-reduction)
30. [Data Integration](#30-data-integration)
31. [Validation](#31-validation)
32. [Preprocessing with Pandas](#32-preprocessing-with-pandas)
33. [Preprocessing with Scikit-learn](#33-preprocessing-with-scikit-learn)
34. [ColumnTransformer](#34-columntransformer)
35. [Pipeline](#35-pipeline)
36. [Complete Example](#36-complete-example)
37. [Data Preprocessing in Data Analytics](#37-data-preprocessing-in-data-analytics)
38. [Data Preprocessing in Machine Learning](#38-data-preprocessing-in-machine-learning)
39. [Common Mistakes](#39-common-mistakes)
40. [Interview Questions](#40-interview-questions)
41. [Quick Revision](#41-quick-revision)

---

# 1. What is Data Preprocessing?

**Data preprocessing** is the process of converting raw, incomplete, inconsistent, and potentially unsuitable data into a clean and usable format for **data analysis, visualization, statistics, or machine learning**.

In simple words:

> **Data preprocessing means preparing data before using it.**

### Basic idea

```text
Raw Data
   ↓
Data Preprocessing
   ↓
Clean + Consistent + Suitable Data
   ↓
Analysis / Visualization / Machine Learning
```

---

# 2. Why is Data Preprocessing Important?

Real-world data is rarely perfect.

It may contain:

```text
Missing values
Duplicate records
Incorrect values
Inconsistent formats
Wrong data types
Outliers
Categorical values
Different scales
Unnecessary columns
Irrelevant features
Imbalanced classes
```

For example:

```text
Age
25
30
NaN
"35"
-10
```

This data cannot be blindly used for analysis or machine learning.

Preprocessing helps us turn it into something meaningful.

---

# 3. Raw Data vs Processed Data

## Raw Data

Raw data is data collected directly from sources before proper preparation.

Example:

```text
Name       Age       Salary       City
John       25        50000        Hyderabad
Alice      NaN       60000        hyderabad
Bob        "30"      70000        Delhi
John       25        50000        Hyderabad
```

Problems:

```text
Missing value
Different capitalization
Age stored as string
Duplicate record
```

---

## Processed Data

After preprocessing:

```text
Name       Age       Salary       City
John       25        50000        Hyderabad
Alice      27        60000        Hyderabad
Bob        30        70000        Delhi
```

Now the dataset is much more suitable for analysis.

---

# 4. Data Preprocessing Workflow

A typical workflow is:

```text
                RAW DATA
                    ↓
             Data Collection
                    ↓
          Understand the Dataset
                    ↓
             Data Cleaning
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
 Missing Values             Duplicates
 Invalid Values             Inconsistency
 Outliers                   Wrong Types
        └───────────┬───────────┘
                    ↓
             Data Manipulation
                    ↓
             Data Transformation
                    ↓
             Categorical Encoding
                    ↓
             Feature Engineering
                    ↓
              Feature Selection
                    ↓
               Feature Scaling
                    ↓
             Train/Test Split
                    ↓
             Validation
                    ↓
       Analysis / Machine Learning
```

> Not every project requires every step. The preprocessing workflow depends on the dataset and the goal.

---

# 5. Data Preprocessing vs Data Cleaning vs Data Manipulation

This is an important concept.

## Data Preprocessing

**Data preprocessing is the broader concept.**

```text
Data Preprocessing
│
├── Data Cleaning
├── Data Manipulation
├── Data Transformation
├── Data Encoding
├── Feature Engineering
├── Feature Selection
├── Feature Scaling
├── Data Reduction
└── Data Integration
```

---

## Data Cleaning

Data cleaning focuses on **data quality**.

Question:

> "Is my data correct and consistent?"

Examples:

```text
Handle missing values
Remove duplicates
Fix incorrect values
Fix inconsistent formats
Correct data types
Handle invalid records
Handle outliers
```

---

## Data Manipulation

Data manipulation focuses on **organizing and modifying data**.

Question:

> "How should I change or organize this data?"

Examples:

```text
Filtering
Sorting
Grouping
Aggregation
Merging
Joining
Reshaping
Creating columns
Selecting rows
```

---

## Data Transformation

Transformation changes the representation of data.

Examples:

```text
Scaling
Normalization
Encoding
Log transformation
Changing date formats
Converting units
```

---

## Simple Relationship

```text
                DATA PREPROCESSING
                        │
       ┌────────────────┼────────────────┐
       ↓                ↓                ↓
   CLEANING       MANIPULATION     TRANSFORMATION
       │                │                │
       ↓                ↓                ↓
   Fix data        Organize data    Change format
       │                │                │
       └────────────────┼────────────────┘
                        ↓
                Prepared Data
```

### One-line memory trick

> 🧹 **Cleaning = Fix the data**
> 🔄 **Manipulation = Organize/change the data**
> 🔧 **Transformation = Convert the data**
> 📊 **Preprocessing = Overall preparation process**

---

# 6. Types of Data Preprocessing

Major preprocessing tasks include:

```text
1. Data Cleaning
2. Missing Value Handling
3. Duplicate Removal
4. Outlier Handling
5. Data Type Conversion
6. Data Transformation
7. Data Manipulation
8. Categorical Encoding
9. Feature Engineering
10. Feature Selection
11. Feature Scaling
12. Data Reduction
13. Data Integration
14. Data Splitting
15. Validation
16. Imbalance Handling
```

---

# 7. Data Collection

Before preprocessing, data must be collected.

Data may come from:

```text
CSV files
Excel files
Databases
APIs
Web applications
Sensors
Surveys
Transaction systems
Logs
Cloud storage
```

Example:

```python
import pandas as pd

df = pd.read_csv("customers.csv")
```

---

# 8. Understanding the Dataset

Before changing data, understand it.

## View first rows

```python
df.head()
```

## View last rows

```python
df.tail()
```

## Dataset dimensions

```python
df.shape
```

Output:

```text
(rows, columns)
```

Example:

```text
(1000, 8)
```

means:

```text
1000 rows
8 columns
```

---

## Column names

```python
df.columns
```

---

## Data types

```python
df.dtypes
```

---

## Dataset information

```python
df.info()
```

---

## Statistical summary

```python
df.describe()
```

---

## Missing values

```python
df.isnull().sum()
```

---

## Duplicate count

```python
df.duplicated().sum()
```

---

# 9. Handling Missing Values

Missing values are one of the most common preprocessing problems.

Example:

```text
Name       Age       Salary
John       25        50000
Alice      NaN       60000
Bob        30        NaN
```

---

## 9.1 Detect Missing Values

```python
df.isnull()
```

Count:

```python
df.isnull().sum()
```

Alternative:

```python
df.isna().sum()
```

---

# 9.2 Remove Missing Rows

```python
df.dropna()
```

This removes rows containing missing values.

### Important

Do not automatically remove every missing row.

If many rows contain missing values, you may lose a large amount of useful information.

---

# 9.3 Fill with Mean

For numerical data:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)
```

Mean:

```text
Mean = Sum of values / Number of values
```

---

# 9.4 Fill with Median

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

Median is often preferable when data contains outliers.

---

# 9.5 Fill with Mode

For categorical data:

```python
df["City"] = df["City"].fillna(
    df["City"].mode()[0]
)
```

Mode means the most frequently occurring value.

---

# 9.6 Forward Fill

```python
df["Sales"] = df["Sales"].ffill()
```

The previous available value is used.

Useful in some time-series situations.

---

# 9.7 Backward Fill

```python
df["Sales"] = df["Sales"].bfill()
```

The next available value is used.

---

# 10. Handling Duplicate Data

Check duplicates:

```python
df.duplicated()
```

Count duplicates:

```python
df.duplicated().sum()
```

Remove duplicates:

```python
df = df.drop_duplicates()
```

Duplicates can cause:

```text
Incorrect counts
Incorrect averages
Incorrect totals
Biased analysis
```

---

# 11. Handling Incorrect Data

Incorrect values can occur because of:

```text
Human errors
Data-entry mistakes
System errors
Sensor errors
Import problems
```

Example:

```text
Age
25
30
-10
200
```

An age of `-10` is invalid.

You can identify it:

```python
df[df["Age"] < 0]
```

Then decide whether to:

```text
Correct it
Remove it
Replace it
Mark it as missing
Investigate the source
```

---

# 12. Handling Inconsistent Data

Example:

```text
City
Hyderabad
hyderabad
HYDERABAD
 Hyderabad
```

These may represent the same category.

Standardize:

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.lower()
)
```

Output:

```text
hyderabad
hyderabad
hyderabad
hyderabad
```

You can use title case instead:

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)
```

---

# 13. Handling Outliers

An **outlier** is an observation that is unusually far from the rest of the data.

Example:

```text
Salary
30000
35000
40000
45000
50000
5000000
```

`5000000` may be an outlier.

But:

> **An outlier is not automatically an error.**

It could be a legitimate observation.

---

## 13.1 Detect Using Box Plot

```python
import matplotlib.pyplot as plt

plt.boxplot(df["Salary"])

plt.show()
```

---

## 13.2 IQR Method

IQR means:

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

Python:

```python
Q1 = df["Salary"].quantile(0.25)
Q3 = df["Salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

Find outliers:

```python
outliers = df[
    (df["Salary"] < lower) |
    (df["Salary"] > upper)
]
```

---

# 14. Data Type Conversion

Data may be stored using the wrong data type.

Example:

```text
Age
"25"
"30"
"35"
```

These may be strings instead of numbers.

Convert:

```python
df["Age"] = df["Age"].astype(int)
```

---

## Numeric Conversion

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

`errors="coerce"` converts invalid values into `NaN`.

---

## Date Conversion

```python
df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)
```

Correct data types are important for:

```text
Calculations
Sorting
Filtering
Grouping
Visualization
Machine learning
```

---

# 15. Data Transformation

Data transformation changes data into a more useful representation.

Examples:

```text
Scaling
Normalization
Standardization
Encoding
Log transformation
Unit conversion
Date transformation
```

---

## Example: Unit Conversion

Suppose salary is stored in rupees:

```python
df["Salary_Lakh"] = (
    df["Salary"] / 100000
)
```

---

## Example: Log Transformation

For heavily skewed positive data:

```python
import numpy as np

df["Log_Sales"] = np.log1p(
    df["Sales"]
)
```

`log1p(x)` computes:

```text
log(1 + x)
```

and is convenient when zero values may exist.

---

# 16. Data Manipulation

Data manipulation is a part of broader preprocessing.

Common operations:

```text
Filtering
Sorting
Selecting
Grouping
Aggregation
Merging
Joining
Reshaping
Creating columns
Removing columns
```

---

## Filtering

```python
df[df["Age"] > 25]
```

---

## Selecting Columns

```python
df[
    ["Name", "Age", "Salary"]
]
```

---

## Sorting

```python
df.sort_values(
    "Salary",
    ascending=False
)
```

---

## Creating a Column

```python
df["Annual_Bonus"] = (
    df["Salary"] * 0.10
)
```

---

## Grouping

```python
df.groupby("City")["Salary"].mean()
```

---

## Aggregation

```python
df.groupby("Department").agg({
    "Salary": "mean",
    "Age": "median"
})
```

---

## Merging

```python
merged = pd.merge(
    customers,
    orders,
    on="Customer_ID"
)
```

---

# 17. Categorical Data

Categorical variables represent categories.

Example:

```text
Gender
Male
Female
Male
Female
```

Machine learning algorithms generally require numerical representations of categorical variables.

Therefore, categorical data may need to be encoded.

---

# 18. Label Encoding

Label encoding assigns an integer to each category.

Example:

```text
Male   → 0
Female → 1
```

Using Scikit-learn:

```python
from sklearn.preprocessing import LabelEncoder

encoder = LabelEncoder()

df["Gender"] = encoder.fit_transform(
    df["Gender"]
)
```

### Important

Label encoding can unintentionally imply an order.

For example:

```text
Red   → 0
Blue  → 1
Green → 2
```

The numbers do not necessarily mean:

```text
Green > Blue > Red
```

Therefore, label encoding is not always appropriate for nominal categories.

---

# 19. One-Hot Encoding

One-hot encoding creates separate binary columns.

Original:

```text
City
Delhi
Mumbai
Hyderabad
```

After encoding:

```text
City_Delhi    City_Mumbai    City_Hyderabad
1             0              0
0             1              0
0             0              1
```

Using Pandas:

```python
df = pd.get_dummies(
    df,
    columns=["City"]
)
```

Using Scikit-learn:

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(
    handle_unknown="ignore"
)
```

---

# 20. Ordinal Encoding

Ordinal data has a meaningful order.

Example:

```text
Education

High School
Bachelor
Master
PhD
```

There is an order:

```text
High School < Bachelor < Master < PhD
```

Ordinal encoding can represent that order numerically.

Example:

```text
High School → 0
Bachelor     → 1
Master       → 2
PhD          → 3
```

This is different from nominal categories, where there is no meaningful order.

---

# 21. Feature Engineering

**Feature engineering** means creating new useful features from existing data.

Example:

```text
First Name
Last Name
```

could be combined into:

```text
Full Name
```

---

## Example

```python
df["Total_Sales"] = (
    df["Quantity"] *
    df["Price"]
)
```

---

## Extract Year

```python
df["Year"] = (
    df["Date"].dt.year
)
```

---

## Extract Month

```python
df["Month"] = (
    df["Date"].dt.month
)
```

---

## Extract Day

```python
df["Day"] = (
    df["Date"].dt.day
)
```

---

## Age Group

```python
df["Age_Group"] = pd.cut(
    df["Age"],
    bins=[0, 18, 30, 50, 100],
    labels=[
        "Child",
        "Young Adult",
        "Adult",
        "Senior"
    ]
)
```

---

# 22. Feature Selection

**Feature selection** means selecting the most useful features for analysis or machine learning.

Suppose:

```text
Age
Salary
City
Height
Weight
Customer_ID
Random_Number
```

Some variables may be:

```text
Relevant
Irrelevant
Redundant
```

We may remove unnecessary features.

Example:

```python
X = df[
    [
        "Age",
        "Salary",
        "Height",
        "Weight"
    ]
]
```

Feature selection can help:

```text
Reduce complexity
Reduce noise
Improve training efficiency
Improve interpretability
Potentially improve model performance
```

---

# 23. Feature Scaling

Different features can have very different ranges.

Example:

```text
Age       → 18 to 80
Salary    → 20,000 to 500,000
Experience → 0 to 30
```

Some algorithms are sensitive to feature scale.

Scaling puts features on comparable numerical scales.

---

# 24. Normalization

Normalization commonly scales values to a fixed range, often:

```text
0 to 1
```

A common min-max formula is:

```text
X_scaled = (X - X_min) / (X_max - X_min)
```

Using Scikit-learn:

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

df["Salary"] = scaler.fit_transform(
    df[["Salary"]]
)
```

---

# 25. Standardization

Standardization transforms data so that it is centered around:

```text
Mean = 0
Standard Deviation = 1
```

Formula:

```text
Z = (X - μ) / σ
```

where:

```text
μ = Mean
σ = Standard Deviation
```

Using Scikit-learn:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

---

# 26. Normalization vs Standardization

| Normalization                        | Standardization                          |
| ------------------------------------ | ---------------------------------------- |
| Commonly scales to 0–1               | Centers around mean 0                    |
| Uses min and max                     | Uses mean and standard deviation         |
| Sensitive to extreme values          | Often less directly dependent on min/max |
| Useful when bounded scale is desired | Commonly used for many ML algorithms     |

### Memory trick

```text
Normalization
     ↓
0 to 1

Standardization
     ↓
Mean = 0
Std = 1
```

---

# 27. Train-Test Split

In machine learning, data is commonly divided into:

```text
Training Data
+
Testing Data
```

Training data is used to train the model.

Testing data is used to evaluate the model on unseen examples.

Example:

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = (
    train_test_split(
        X,
        y,
        test_size=0.2,
        random_state=42
    )
)
```

Here:

```text
80% → Training
20% → Testing
```

---

# 28. Data Leakage

**Data leakage** occurs when information from outside the training process improperly influences the model.

This can produce overly optimistic results.

A common mistake is fitting preprocessing on the entire dataset before splitting.

### Wrong approach

```python
scaler.fit_transform(X)

X_train, X_test = train_test_split(X)
```

The scaler has already seen information from the future test set.

### Better approach

```python
X_train, X_test, y_train, y_test = (
    train_test_split(
        X,
        y,
        test_size=0.2,
        random_state=42
    )
)

scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### Important rule

> **Fit preprocessing steps using training data, then use the fitted transformation to transform test/new data.**

---

# 29. Handling Imbalanced Data

An imbalanced dataset occurs when one class is much more common than another.

Example:

```text
Class 0 → 9500
Class 1 → 500
```

This is a highly imbalanced classification dataset.

Possible approaches include:

```text
Oversampling
Undersampling
Class weights
Synthetic sampling methods
Appropriate evaluation metrics
```

---

## Class Weights

Some machine learning algorithms support:

```python
class_weight="balanced"
```

Example:

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(
    class_weight="balanced"
)
```

---

# 30. Data Reduction

Data reduction means reducing the size or complexity of data while trying to preserve useful information.

Methods include:

```text
Feature selection
Sampling
Aggregation
Dimensionality reduction
```

Examples:

```text
10 million rows
      ↓
Sample representative rows
```

or:

```text
100 features
      ↓
Select 20 useful features
```

---

# 31. Data Integration

Data integration combines data from multiple sources.

Example:

```text
Customer Data
       +
Order Data
       +
Product Data
       ↓
Integrated Dataset
```

Using Pandas:

```python
df = pd.merge(
    customers,
    orders,
    on="Customer_ID"
)
```

---

# 32. Validation

After preprocessing, verify that the data is actually correct.

Check:

```python
df.info()
```

Missing values:

```python
df.isnull().sum()
```

Duplicates:

```python
df.duplicated().sum()
```

Statistics:

```python
df.describe()
```

Unique values:

```python
df["City"].unique()
```

Value counts:

```python
df["City"].value_counts()
```

---

# 33. Preprocessing with Pandas

Pandas is extremely useful for data preprocessing.

Typical workflow:

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df.head())
print(df.info())

# Missing values
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)

# Duplicates
df = df.drop_duplicates()

# Standardization
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)

# Data type
df["Age"] = pd.to_numeric(
    df["Age"],
    errors="coerce"
)

# New feature
df["Total"] = (
    df["Quantity"] *
    df["Price"]
)
```

---

# 34. ColumnTransformer

Scikit-learn's `ColumnTransformer` is useful when different columns need different preprocessing.

Example:

```text
Numerical columns
      ↓
Scaling

Categorical columns
      ↓
One-hot encoding
```

Example:

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import (
    StandardScaler,
    OneHotEncoder
)

preprocessor = ColumnTransformer(
    transformers=[
        (
            "num",
            StandardScaler(),
            ["Age", "Salary"]
        ),
        (
            "cat",
            OneHotEncoder(
                handle_unknown="ignore"
            ),
            ["City", "Gender"]
        )
    ]
)
```

---

# 35. Pipeline

A pipeline combines preprocessing and modeling into one workflow.

Example:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    (
        "scaler",
        StandardScaler()
    ),
    (
        "model",
        LogisticRegression()
    )
])
```

Train:

```python
pipeline.fit(
    X_train,
    y_train
)
```

Predict:

```python
predictions = pipeline.predict(
    X_test
)
```

### Why pipelines are useful

They help:

```text
Prevent preprocessing mistakes
Prevent data leakage
Keep workflow organized
Apply the same transformations consistently
Make model deployment easier
```

---

# 36. Complete Example

Consider this dataset:

```text
Name    Age    Salary    City       Experience
John    25     50000     Hyderabad  2
Alice   NaN    60000     hyderabad  4
Bob     30     70000     Delhi      5
John    25     50000     Hyderabad  2
```

---

## Step 1 — Load

```python
import pandas as pd

df = pd.read_csv(
    "employees.csv"
)
```

---

## Step 2 — Inspect

```python
print(df.head())

print(df.info())

print(df.describe())
```

---

## Step 3 — Missing Value

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

---

## Step 4 — Remove Duplicates

```python
df = df.drop_duplicates()
```

---

## Step 5 — Standardize City

```python
df["City"] = (
    df["City"]
    .str.strip()
    .str.title()
)
```

---

## Step 6 — Convert Data Type

```python
df["Age"] = pd.to_numeric(
    df["Age"],
    errors="coerce"
)
```

---

## Step 7 — Create Feature

Create salary in lakhs:

```python
df["Salary_Lakh"] = (
    df["Salary"] / 100000
)
```

---

## Step 8 — Encode Category

```python
df = pd.get_dummies(
    df,
    columns=["City"]
)
```

---

## Step 9 — Validate

```python
print(df.info())

print(df.isnull().sum())

print(df.duplicated().sum())
```

Now the dataset is prepared for further analysis or modeling.

---

# 37. Data Preprocessing in Data Analytics

For **data analytics**, preprocessing usually focuses on making data reliable and analysis-ready.

Typical workflow:

```text
Raw Data
   ↓
Cleaning
   ↓
Missing Values
   ↓
Duplicates
   ↓
Incorrect Data
   ↓
Manipulation
   ↓
Transformation
   ↓
Feature Creation
   ↓
Visualization
   ↓
Analysis
```

Example questions:

```text
What is the average sales?
Which product sells most?
Which city generates the most revenue?
What is the monthly trend?
```

---

# 38. Data Preprocessing in Machine Learning

Machine learning often requires additional preprocessing.

Typical workflow:

```text
Raw Data
   ↓
Cleaning
   ↓
Missing Values
   ↓
Outliers
   ↓
Categorical Encoding
   ↓
Feature Engineering
   ↓
Feature Selection
   ↓
Feature Scaling
   ↓
Train/Test Split
   ↓
Model Training
   ↓
Evaluation
```

The exact steps depend on the algorithm and data.

---

# 39. Common Mistakes

## Mistake 1 — Cleaning Without Understanding the Data

Do not blindly delete missing values or outliers.

First ask:

```text
Why is the value missing?
Is the outlier valid?
What does the column represent?
```

---

## Mistake 2 — Treating Every Outlier as an Error

An outlier can be:

```text
Error
OR
Valid rare observation
```

Investigate before removing it.

---

## Mistake 3 — Encoding Everything with Label Encoding

Nominal categories generally do not have a natural numerical order.

One-hot encoding is often more appropriate.

---

## Mistake 4 — Scaling Before Splitting

Avoid fitting a scaler on the complete dataset.

Instead:

```text
Split
 ↓
Fit on training
 ↓
Transform training
 ↓
Transform test
```

---

## Mistake 5 — Data Leakage

Never allow test-set information to influence preprocessing fitted on training data.

---

## Mistake 6 — Removing Too Much Data

Aggressive cleaning can cause:

```text
Information loss
Smaller dataset
Biased results
```

---

## Mistake 7 — Forgetting Validation

After preprocessing, always check:

```python
df.info()
df.describe()
df.isnull().sum()
df.duplicated().sum()
```

---

# 40. Interview Questions

## Q1. What is data preprocessing?

> Data preprocessing is the process of preparing raw data by cleaning, transforming, organizing, encoding, and scaling it so that it becomes suitable for analysis or machine learning.

---

## Q2. Is data preprocessing the same as data cleaning?

No.

> **Data cleaning is a component of data preprocessing.**

Cleaning focuses mainly on data quality, while preprocessing is broader.

---

## Q3. Is data manipulation the same as preprocessing?

No.

> **Data manipulation is generally considered one component of the broader data preprocessing/data preparation process.**

---

## Q4. Why is preprocessing required?

Because real-world data may contain:

```text
Missing values
Duplicates
Errors
Inconsistencies
Outliers
Categorical variables
Different scales
Irrelevant features
```

---

## Q5. What are common preprocessing steps?

```text
Data cleaning
Missing value handling
Duplicate removal
Outlier handling
Data type conversion
Transformation
Encoding
Feature engineering
Feature selection
Scaling
Data splitting
Validation
```

---

## Q6. What is feature engineering?

Feature engineering is the process of creating useful new features from existing data.

Example:

```python
df["Total_Sales"] = (
    df["Quantity"] *
    df["Price"]
)
```

---

## Q7. What is feature scaling?

Feature scaling transforms numerical features so that differences in their numerical ranges do not disproportionately affect algorithms that are sensitive to feature scale.

---

## Q8. What is normalization?

A common normalization approach scales values to a fixed range such as 0 to 1.

---

## Q9. What is standardization?

Standardization transforms values using the mean and standard deviation, commonly producing features with mean 0 and standard deviation 1.

---

## Q10. What is data leakage?

Data leakage occurs when information that should not be available during model training influences the training or preprocessing process.

---

## Q11. Why do we split data?

To evaluate the model on data that was not used to train it.

---

## Q12. What is one-hot encoding?

One-hot encoding converts categorical values into separate binary indicator columns.

---

## Q13. What is the difference between normalization and standardization?

```text
Normalization
→ commonly maps values to 0–1

Standardization
→ commonly produces mean 0 and standard deviation 1
```

---

# 41. Quick Revision

## Data Preprocessing

```text
Raw Data
   ↓
Prepare Data
   ↓
Analysis / ML
```

---

## Data Cleaning

```text
Missing Values
Duplicates
Invalid Values
Inconsistent Values
Wrong Data Types
Outliers
```

---

## Data Manipulation

```text
Filter
Sort
Group
Aggregate
Merge
Join
Reshape
Create Columns
```

---

## Data Transformation

```text
Scale
Normalize
Standardize
Encode
Convert Units
Transform Distributions
```

---

## Encoding

```text
Categorical Data
       ↓
Encoding
       ↓
Numerical Representation
```

Common types:

```text
Label Encoding
One-Hot Encoding
Ordinal Encoding
```

---

## Feature Engineering

```text
Existing Features
       ↓
Create New Features
       ↓
More Useful Information
```

---

## Feature Selection

```text
Many Features
      ↓
Remove irrelevant/redundant features
      ↓
Useful Features
```

---

## Scaling

```text
Different Ranges
      ↓
Scaling
      ↓
Comparable Ranges
```

---

## Machine Learning Split

```text
Dataset
   ↓
Train / Test Split
   ↓
Training Data → Fit preprocessing + model
Testing Data  → Transform using fitted preprocessing + evaluate
```

---

# 🧠 Final Memory Map

```text
                         DATA PREPROCESSING
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        ↓                         ↓                         ↓
   DATA CLEANING            DATA MANIPULATION        TRANSFORMATION
        │                         │                         │
        ├─ Missing values         ├─ Filtering              ├─ Scaling
        ├─ Duplicates             ├─ Sorting                ├─ Normalization
        ├─ Invalid values         ├─ Grouping               ├─ Standardization
        ├─ Inconsistency          ├─ Aggregation            ├─ Encoding
        ├─ Data types             ├─ Merging                └─ Unit conversion
        └─ Outliers               └─ Reshaping
                                  │
                                  ↓
                         FEATURE ENGINEERING
                                  │
                                  ↓
                          FEATURE SELECTION
                                  │
                                  ↓
                         TRAIN / TEST SPLIT
                                  │
                                  ↓
                              VALIDATION
                                  │
                    ┌─────────────┴─────────────┐
                    ↓                           ↓
              DATA ANALYTICS              MACHINE LEARNING
                    ↓                           ↓
             Visualization                  Model
                    ↓                           ↓
                Insights                   Evaluation
```

---

# ⭐ Most Important Concepts

Remember these five definitions:

### 1. Data Preprocessing

> **The overall process of preparing raw data for analysis or machine learning.**

### 2. Data Cleaning

> **Fixing problems in data quality.**

### 3. Data Manipulation

> **Selecting, organizing, modifying, and reshaping data.**

### 4. Data Transformation

> **Changing data into a more suitable representation.**

### 5. Feature Engineering

> **Creating useful new features from existing data.**

---

# 🔥 One-Line Revision

```text
Preprocessing = Prepare
Cleaning      = Fix
Manipulation  = Organize
Transformation= Convert
Engineering   = Create
Selection     = Choose
Scaling       = Adjust
Encoding      = Represent
Validation    = Verify
```

> **Data preprocessing is the broader umbrella; cleaning, manipulation, transformation, encoding, feature engineering, feature selection, and scaling are common tasks within the broader data-preparation process.**
