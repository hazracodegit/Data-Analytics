# 📊 Python `statistics` Library — Complete Revision Notes

> A complete revision guide to Python's built-in `statistics` module, including measures of central tendency, dispersion, averages, covariance, correlation, quantiles, probability-related functions, and practical data-analysis examples.

---

# 📚 Table of Contents

1. [What is the Statistics Library?](#1-what-is-the-statistics-library)
2. [Why Use the Statistics Library?](#2-why-use-the-statistics-library)
3. [Importing Statistics](#3-importing-statistics)
4. [Types of Statistics](#4-types-of-statistics)
5. [Measures of Central Tendency](#5-measures-of-central-tendency)
6. [Mean](#6-mean)
7. [Median](#7-median)
8. [Median Low](#8-median-low)
9. [Median High](#9-median-high)
10. [Median Grouped](#10-median-grouped)
11. [Mode](#11-mode)
12. [Multimode](#12-multimode)
13. [Measures of Dispersion](#13-measures-of-dispersion)
14. [Variance](#14-variance)
15. [Population Variance](#15-population-variance)
16. [Standard Deviation](#16-standard-deviation)
17. [Population Standard Deviation](#17-population-standard-deviation)
18. [Quantiles](#18-quantiles)
19. [Covariance](#19-covariance)
20. [Correlation](#20-correlation)
21. [Linear Regression](#21-linear-regression)
22. [Harmonic Mean](#22-harmonic-mean)
23. [Geometric Mean](#23-geometric-mean)
24. [Weighted Mean](#24-weighted-mean)
25. [Frequency Data](#25-frequency-data)
26. [Data Types Supported](#26-data-types-supported)
27. [Statistics vs NumPy](#27-statistics-vs-numpy)
28. [Statistics vs Pandas](#28-statistics-vs-pandas)
29. [Statistics in Data Analytics](#29-statistics-in-data-analytics)
30. [Complete Example](#30-complete-example)
31. [Important Formulas](#31-important-formulas)
32. [Common Mistakes](#32-common-mistakes)
33. [Interview Questions](#33-interview-questions)
34. [Quick Revision](#34-quick-revision)

---

# 1. What is the Statistics Library?

Python provides a built-in module called:

```python
statistics
```

It provides functions for calculating common statistical measures.

It is part of Python's **standard library**, so you do not normally need to install an external package to use it.

It is useful for:

```text
Mean
Median
Mode
Variance
Standard deviation
Quantiles
Correlation
Covariance
Regression
Geometric mean
Harmonic mean
Weighted mean
```

Basic import:

```python
import statistics
```

---

# 2. Why Use the Statistics Library?

The `statistics` module is useful when you need statistical calculations without requiring a large external numerical library.

For example:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.mean(data))
```

Output:

```text
30
```

### Advantages

```text
Simple
Built into Python
Easy syntax
Useful for basic statistics
Good for small datasets
Useful for learning statistics
Useful for quick calculations
```

---

# 3. Importing Statistics

## Method 1 — Import module

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.mean(data))
```

---

## Method 2 — Import specific functions

```python
from statistics import mean, median, mode

data = [10, 20, 30, 40, 50]

print(mean(data))
print(median(data))
print(mode(data))
```

---

## Method 3 — Import everything

```python
from statistics import *
```

This is generally not recommended because it can make it unclear where names came from.

Prefer:

```python
import statistics
```

or specific imports.

---

# 4. Types of Statistics

Statistics is broadly divided into:

```text
Statistics
│
├── Descriptive Statistics
│
└── Inferential Statistics
```

## Descriptive Statistics

Descriptive statistics summarize the data you already have.

Examples:

```text
Mean
Median
Mode
Range
Variance
Standard deviation
Quantiles
```

Example:

```text
Marks:
50, 60, 70, 80, 90
```

We can calculate:

```text
Mean = 70
Median = 70
```

---

## Inferential Statistics

Inferential statistics use sample data to make conclusions about a larger population.

Examples:

```text
Hypothesis testing
Confidence intervals
Statistical inference
```

The basic Python `statistics` module mainly focuses on **descriptive statistics**, although it also provides tools such as correlation and simple linear regression.

---

# 5. Measures of Central Tendency

Central tendency tells us about the **center** or typical value of data.

Main measures:

```text
Mean
Median
Mode
```

---

# 6. Mean

Mean is commonly called the **average**.

Formula:

```text
Mean = Sum of all values / Number of values
```

Example:

```text
10, 20, 30, 40, 50
```

```text
Mean = (10 + 20 + 30 + 40 + 50) / 5
     = 150 / 5
     = 30
```

Python:

```python
import statistics

data = [10, 20, 30, 40, 50]

result = statistics.mean(data)

print(result)
```

Output:

```text
30
```

---

## When to use Mean?

Mean is useful when:

```text
Data is numerical
There are no extreme outliers
You want the arithmetic average
```

### Problem with mean

Mean can be strongly affected by outliers.

Example:

```text
10, 20, 30, 40, 1000
```

The `1000` significantly increases the mean.

---

# 7. Median

The median is the **middle value after sorting the data**.

Example:

```text
10, 20, 30, 40, 50
```

Median:

```text
30
```

Python:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.median(data))
```

Output:

```text
30
```

---

## Even number of values

Example:

```text
10, 20, 30, 40
```

Middle values:

```text
20 and 30
```

Median:

```text
(20 + 30) / 2 = 25
```

Python:

```python
data = [10, 20, 30, 40]

print(statistics.median(data))
```

Output:

```text
25.0
```

---

## Mean vs Median

```text
Mean
 ↓
Affected by outliers

Median
 ↓
More resistant to outliers
```

Example:

```text
10, 20, 30, 40, 1000
```

The median is still:

```text
30
```

while the mean becomes much larger.

---

# 8. Median Low

Function:

```python
statistics.median_low()
```

It returns the lower of the two middle values when there is an even number of observations.

Example:

```python
import statistics

data = [10, 20, 30, 40]

print(statistics.median_low(data))
```

Output:

```text
20
```

Normal median:

```text
25
```

Median low:

```text
20
```

---

# 9. Median High

Function:

```python
statistics.median_high()
```

It returns the higher of the two middle values.

Example:

```python
import statistics

data = [10, 20, 30, 40]

print(statistics.median_high(data))
```

Output:

```text
30
```

Therefore:

```text
median_low  → 20
median      → 25
median_high → 30
```

---

# 10. Median Grouped

Function:

```python
statistics.median_grouped()
```

It estimates the median of grouped/continuous data.

Example:

```python
import statistics

data = [10, 10, 20, 20, 20, 30, 30]

print(statistics.median_grouped(data))
```

It is mainly useful when working with data represented in grouped intervals.

---

# 11. Mode

Mode is the value that occurs **most frequently**.

Example:

```text
10, 20, 20, 30, 40
```

Mode:

```text
20
```

Python:

```python
import statistics

data = [10, 20, 20, 30, 40]

print(statistics.mode(data))
```

Output:

```text
20
```

---

## When is mode useful?

Mode is particularly useful for:

```text
Categorical data
Most common category
Most frequently occurring value
```

Example:

```text
Red
Blue
Red
Green
Red
Blue
```

Mode:

```text
Red
```

---

# 12. Multimode

Sometimes multiple values have the same highest frequency.

Example:

```text
10, 10, 20, 20, 30
```

Both:

```text
10
20
```

occur twice.

Use:

```python
import statistics

data = [10, 10, 20, 20, 30]

print(statistics.multimode(data))
```

Output:

```text
[10, 20]
```

---

# 13. Measures of Dispersion

Central tendency tells us about the center.

Dispersion tells us about **how spread out the data is**.

Important measures:

```text
Range
Variance
Standard deviation
```

---

# 14. Variance

Variance measures how far data values tend to spread from the mean.

Conceptually:

```text
Large variance
→ Values are more spread out

Small variance
→ Values are closer together
```

The `statistics` module provides:

```python
statistics.variance()
```

for **sample variance**.

Example:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.variance(data))
```

---

## Sample Variance

Sample variance uses:

```text
n - 1
```

in the denominator.

Formula:

```text
s² = Σ(x - x̄)² / (n - 1)
```

where:

```text
x  = individual value
x̄  = sample mean
n  = number of observations
```

---

# 15. Population Variance

Function:

```python
statistics.pvariance()
```

Population variance uses:

```text
n
```

rather than:

```text
n - 1
```

Example:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.pvariance(data))
```

---

## Sample vs Population Variance

| Function      | Meaning             | Denominator |
| ------------- | ------------------- | ----------- |
| `variance()`  | Sample variance     | `n - 1`     |
| `pvariance()` | Population variance | `n`         |

### Remember

```text
variance()
    ↓
sample

pvariance()
    ↓
population
```

---

# 16. Standard Deviation

Standard deviation measures the spread of data around its mean.

It is the square root of variance.

```text
Standard Deviation = √Variance
```

Python:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.stdev(data))
```

`stdev()` calculates **sample standard deviation**.

---

# 17. Population Standard Deviation

Use:

```python
statistics.pstdev()
```

Example:

```python
import statistics

data = [10, 20, 30, 40, 50]

print(statistics.pstdev(data))
```

---

## Sample vs Population Standard Deviation

| Function   | Meaning                       |
| ---------- | ----------------------------- |
| `stdev()`  | Sample standard deviation     |
| `pstdev()` | Population standard deviation |

---

## Variance vs Standard Deviation

```text
Variance
 ↓
Squared units

Standard deviation
 ↓
Same units as original data
```

For example, if salary is measured in rupees:

```text
Variance
→ rupees²

Standard deviation
→ rupees
```

This makes standard deviation easier to interpret.

---

# 18. Quantiles

Quantiles divide ordered data into intervals containing approximately equal numbers of observations.

Python:

```python
statistics.quantiles()
```

Example:

```python
import statistics

data = [10, 20, 30, 40, 50, 60, 70, 80]

result = statistics.quantiles(data, n=4)

print(result)
```

When:

```text
n = 4
```

the data is divided into four parts.

These are related to:

```text
Q1
Q2
Q3
```

where:

```text
Q1 → 25th percentile
Q2 → 50th percentile
Q3 → 75th percentile
```

---

## Quartiles

```text
Q1 → 25%
Q2 → 50%
Q3 → 75%
```

The interquartile range is:

```text
IQR = Q3 - Q1
```

IQR is widely used for detecting outliers.

---

# 19. Covariance

Covariance measures how two variables vary together.

Python:

```python
statistics.covariance(x, y)
```

Example:

```python
import statistics

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

print(statistics.covariance(x, y))
```

Positive covariance generally means:

```text
As X increases
→ Y tends to increase
```

Negative covariance generally means:

```text
As X increases
→ Y tends to decrease
```

Near-zero covariance indicates little linear co-movement, though it does not prove independence.

---

# 20. Correlation

Correlation measures the **strength and direction of a linear relationship** between two variables.

Python:

```python
statistics.correlation(x, y)
```

Example:

```python
import statistics

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

result = statistics.correlation(x, y)

print(result)
```

A correlation coefficient is generally between:

```text
-1 and +1
```

Interpretation:

```text
+1 → Perfect positive linear correlation
 0 → No linear correlation
-1 → Perfect negative linear correlation
```

### Important

> Correlation does **not** prove causation.

If two variables are correlated, it does not automatically mean one causes the other.

---

# 21. Linear Regression

The statistics module provides:

```python
statistics.linear_regression()
```

It calculates a simple linear regression model.

The basic form is:

```text
y = intercept + slope × x
```

Example:

```python
import statistics

x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 8, 10]

result = statistics.linear_regression(x, y)

print(result.slope)
print(result.intercept)
```

The result provides information about:

```text
Slope
Intercept
```

The slope tells us the estimated change in `y` for a one-unit increase in `x`.

---

# 22. Harmonic Mean

Function:

```python
statistics.harmonic_mean()
```

Harmonic mean is useful for certain types of **rates and ratios**.

Formula:

```text
HM = n / Σ(1/x)
```

Example:

```python
import statistics

data = [10, 20, 30]

print(statistics.harmonic_mean(data))
```

---

## When is Harmonic Mean Useful?

Common examples include:

```text
Rates
Ratios
Speed over equal distances
Some financial ratios
```

It should not be used automatically for every average.

---

# 23. Geometric Mean

Function:

```python
statistics.geometric_mean()
```

Geometric mean is useful for multiplicative data and growth rates.

Formula:

```text
GM = ⁿ√(x₁ × x₂ × ... × xₙ)
```

Example:

```python
import statistics

data = [2, 8]

print(statistics.geometric_mean(data))
```

Output:

```text
4.0
```

because:

```text
√(2 × 8)
= √16
= 4
```

---

## When is Geometric Mean Useful?

Examples:

```text
Growth rates
Investment returns
Ratios
Multiplicative processes
```

---

# 24. Weighted Mean

A weighted mean gives different importance to different values.

Python:

```python
statistics.fmean(data, weights=weights)
```

Example:

```python
import statistics

marks = [80, 70, 90]
weights = [0.3, 0.2, 0.5]

result = statistics.fmean(
    marks,
    weights=weights
)

print(result)
```

The weights represent the relative importance of each value.

---

## Example: Student Grades

Suppose:

```text
Assignment = 80 → 20%
Midterm    = 70 → 30%
Final      = 90 → 50%
```

Then:

```text
Weighted score =
80×0.20 +
70×0.30 +
90×0.50
```

This is more appropriate than a simple mean when the components have different importance.

---

# 25. Frequency Data

Sometimes data is represented as:

```text
Value + Frequency
```

Example:

```text
Score    Frequency
10       2
20       3
30       5
```

The statistics module provides functions such as:

```python
statistics.mean()
statistics.median()
statistics.mode()
```

For frequency-based data, you may need to expand the data or use appropriate weighted calculations depending on the statistic.

Example:

```python
data = [10, 10, 20, 20, 20, 30, 30, 30, 30, 30]
```

Then:

```python
import statistics

print(statistics.mean(data))
print(statistics.median(data))
print(statistics.mode(data))
```

---

# 26. Data Types Supported

The `statistics` module works with common numeric data such as:

```text
int
float
Decimal
Fraction
```

Example:

```python
from fractions import Fraction
import statistics

data = [
    Fraction(1, 2),
    Fraction(1, 4),
    Fraction(3, 4)
]

print(statistics.mean(data))
```

---

# 27. Statistics vs NumPy

Both can perform statistical calculations, but their purposes differ.

| Statistics                            | NumPy                          |
| ------------------------------------- | ------------------------------ |
| Python standard library               | External numerical library     |
| Simple statistics                     | Numerical computing            |
| Works naturally with Python sequences | Optimized arrays               |
| Easy for basic calculations           | Powerful vectorized operations |
| Good for small/simple tasks           | Excellent for numerical data   |
| No installation normally required     | Requires installation          |

### Example

Statistics:

```python
import statistics

statistics.mean([10, 20, 30])
```

NumPy:

```python
import numpy as np

np.mean([10, 20, 30])
```

For large numerical datasets, NumPy is generally more appropriate.

---

# 28. Statistics vs Pandas

Pandas is primarily a **data manipulation and analysis library**.

Example:

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df["Salary"].mean())
print(df["Salary"].median())
print(df["Salary"].std())
```

Pandas is better when working with:

```text
DataFrames
Series
CSV
Excel
Missing values
Grouping
Filtering
Data cleaning
Data manipulation
```

---

# 29. Statistics in Data Analytics

Statistics is extremely important in data analytics.

A typical analytics workflow is:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Preprocessing
   ↓
Statistical Analysis
   ↓
Visualization
   ↓
Insights
   ↓
Decision Making
```

Statistics helps answer questions such as:

```text
What is the average?
What is the middle value?
What is the most common value?
How spread out is the data?
Are there outliers?
How are variables related?
Is there a trend?
Can we predict one variable from another?
```

---

# 30. Complete Example

Let's analyze employee salaries.

```python
import statistics

salaries = [
    30000,
    35000,
    40000,
    45000,
    50000,
    55000,
    60000
]
```

---

## Mean

```python
mean = statistics.mean(salaries)

print("Mean:", mean)
```

---

## Median

```python
median = statistics.median(salaries)

print("Median:", median)
```

---

## Mode

```python
mode = statistics.mode(salaries)

print("Mode:", mode)
```

---

## Variance

```python
variance = statistics.variance(salaries)

print("Variance:", variance)
```

---

## Standard Deviation

```python
std = statistics.stdev(salaries)

print("Standard Deviation:", std)
```

---

## Quantiles

```python
quartiles = statistics.quantiles(
    salaries,
    n=4
)

print("Quartiles:", quartiles)
```

---

# 31. Important Formulas

## Mean

```text
x̄ = Σx / n
```

---

## Population Variance

```text
σ² = Σ(x - μ)² / N
```

---

## Sample Variance

```text
s² = Σ(x - x̄)² / (n - 1)
```

---

## Population Standard Deviation

```text
σ = √σ²
```

---

## Sample Standard Deviation

```text
s = √s²
```

---

## Range

```text
Range = Maximum - Minimum
```

Note: the `statistics` module does not provide a dedicated `range()` statistical function; Python's built-in `max()` and `min()` are sufficient.

Example:

```python
data = [10, 20, 30, 40, 50]

result = max(data) - min(data)

print(result)
```

---

## IQR

```text
IQR = Q3 - Q1
```

---

## Z-Score

A common standard score is:

```text
z = (x - μ) / σ
```

It indicates how many standard deviations a value lies from the mean.

---

# 32. Common Mistakes

## Mistake 1 — Confusing Mean and Median

```text
Mean
→ arithmetic average

Median
→ middle value
```

---

## Mistake 2 — Using Mean with Extreme Outliers

Example:

```text
10, 20, 30, 40, 10000
```

Mean is strongly influenced by `10000`.

Median is often more robust.

---

## Mistake 3 — Confusing Variance and Standard Deviation

```text
Variance
→ squared spread

Standard deviation
→ square root of variance
```

---

## Mistake 4 — Confusing Sample and Population

```text
variance()
→ sample variance

pvariance()
→ population variance

stdev()
→ sample standard deviation

pstdev()
→ population standard deviation
```

---

## Mistake 5 — Assuming Correlation Means Causation

```text
Correlation
≠
Causation
```

---

## Mistake 6 — Using the Wrong Type of Mean

```text
Arithmetic mean
→ normal numerical average

Geometric mean
→ growth/multiplicative data

Harmonic mean
→ rates/ratios
```

---

# 33. Interview Questions

## Q1. What is Python's statistics module?

> `statistics` is a Python standard-library module that provides functions for common statistical calculations such as mean, median, mode, variance, standard deviation, quantiles, correlation, covariance, and simple linear regression.

---

## Q2. How do you calculate mean?

```python
import statistics

statistics.mean(data)
```

---

## Q3. Difference between mean and median?

> Mean is the arithmetic average, while median is the middle value after ordering the data.

---

## Q4. Which is more resistant to outliers?

> Median is generally more resistant to outliers than mean.

---

## Q5. Difference between variance and standard deviation?

> Standard deviation is the square root of variance and is expressed in the same units as the original data.

---

## Q6. Difference between `variance()` and `pvariance()`?

```text
variance()
→ sample variance

pvariance()
→ population variance
```

---

## Q7. Difference between `stdev()` and `pstdev()`?

```text
stdev()
→ sample standard deviation

pstdev()
→ population standard deviation
```

---

## Q8. What does correlation measure?

> Correlation measures the direction and strength of a linear relationship between two variables.

---

## Q9. Does correlation imply causation?

> No. Correlation alone does not establish causation.

---

## Q10. What is mode?

> Mode is the most frequently occurring value in a dataset.

---

## Q11. What is `multimode()`?

> It returns all values that have the highest frequency.

---

## Q12. What is quantile?

> A quantile is a value that divides ordered data into specified proportions.

---

# 34. Quick Revision

## Central Tendency

```text
Mean
Median
Mode
```

---

## Dispersion

```text
Range
Variance
Standard Deviation
```

---

## Position

```text
Quantiles
Quartiles
Percentiles
```

---

## Relationship

```text
Covariance
Correlation
```

---

## Prediction

```text
Linear Regression
```

---

## Different Types of Mean

```text
Arithmetic Mean
Geometric Mean
Harmonic Mean
Weighted Mean
```

---

# 🧠 Function Cheat Sheet

| Function              | Purpose                        |
| --------------------- | ------------------------------ |
| `mean()`              | Arithmetic mean                |
| `fmean()`             | Floating-point arithmetic mean |
| `median()`            | Median                         |
| `median_low()`        | Lower middle value             |
| `median_high()`       | Higher middle value            |
| `median_grouped()`    | Grouped-data median estimate   |
| `mode()`              | Most common value              |
| `multimode()`         | All modes                      |
| `quantiles()`         | Quantiles                      |
| `variance()`          | Sample variance                |
| `pvariance()`         | Population variance            |
| `stdev()`             | Sample standard deviation      |
| `pstdev()`            | Population standard deviation  |
| `geometric_mean()`    | Geometric mean                 |
| `harmonic_mean()`     | Harmonic mean                  |
| `covariance()`        | Sample covariance              |
| `correlation()`       | Correlation                    |
| `linear_regression()` | Simple linear regression       |

---

# 🔥 Most Important for Data Analytics

If you are learning Python for **Data Analytics**, prioritize these:

```text
1. mean()
2. median()
3. mode()
4. multimode()
5. variance()
6. stdev()
7. quantiles()
8. covariance()
9. correlation()
10. linear_regression()
```

Then learn the same concepts using:

```text
Pandas
   ↓
NumPy
   ↓
Matplotlib / Seaborn
   ↓
Scikit-learn
```

---

# 🎯 Final Memory Map

```text
                    PYTHON STATISTICS
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
    CENTER               SPREAD            RELATIONSHIP
       │                   │                   │
       ├─ Mean             ├─ Variance         ├─ Covariance
       ├─ Median           ├─ Std Dev          └─ Correlation
       └─ Mode             └─ Quantiles
                           │
                           ↓
                     OTHER MEASURES
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
          Geometric     Harmonic      Weighted
             Mean         Mean          Mean
                           │
                           ↓
                    PREDICTION
                           │
                           ↓
                  Linear Regression
```

---

# 🚀 One-Minute Revision

```text
statistics.mean()
→ Average

statistics.median()
→ Middle

statistics.mode()
→ Most frequent

statistics.multimode()
→ All most-frequent values

statistics.variance()
→ Sample variance

statistics.pvariance()
→ Population variance

statistics.stdev()
→ Sample standard deviation

statistics.pstdev()
→ Population standard deviation

statistics.quantiles()
→ Quantiles

statistics.covariance()
→ How two variables vary together

statistics.correlation()
→ Strength/direction of linear relationship

statistics.linear_regression()
→ Simple linear relationship for prediction

statistics.geometric_mean()
→ Multiplicative growth

statistics.harmonic_mean()
→ Rates/ratios
```

> **Core idea:** The `statistics` module gives you the basic statistical building blocks needed to understand and summarize data. In a data-analytics workflow, these concepts become especially powerful when combined with **Pandas for data manipulation, NumPy for numerical computation, and Matplotlib/Seaborn for visualization**.
