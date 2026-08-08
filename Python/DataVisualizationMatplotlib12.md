# 📊 Data Visualization and Matplotlib — Complete Notes

> A complete revision guide for **Data Visualization using Python and Matplotlib**, from basics to commonly used advanced concepts.

---

# 📚 Table of Contents

1. [What is Data Visualization?](#1-what-is-data-visualization)
2. [Why Data Visualization is Important](#2-why-data-visualization-is-important)
3. [Applications of Data Visualization](#3-applications-of-data-visualization)
4. [Data Visualization in Data Analytics](#4-data-visualization-in-data-analytics)
5. [Types of Data](#5-types-of-data)
6. [Common Types of Charts](#6-common-types-of-charts)
7. [What is Matplotlib?](#7-what-is-matplotlib)
8. [Why Use Matplotlib?](#8-why-use-matplotlib)
9. [Applications of Matplotlib](#9-applications-of-matplotlib)
10. [Installation](#10-installation)
11. [Importing Matplotlib](#11-importing-matplotlib)
12. [Pyplot](#12-pyplot)
13. [Basic Plot](#13-basic-plot)
14. [Figure and Axes](#14-figure-and-axes)
15. [Line Chart](#15-line-chart)
16. [Bar Chart](#16-bar-chart)
17. [Horizontal Bar Chart](#17-horizontal-bar-chart)
18. [Pie Chart](#18-pie-chart)
19. [Scatter Plot](#19-scatter-plot)
20. [Histogram](#20-histogram)
21. [Box Plot](#21-box-plot)
22. [Area Chart](#22-area-chart)
23. [Stem Plot](#23-stem-plot)
24. [Stack Plot](#24-stack-plot)
25. [Step Plot](#25-step-plot)
26. [Error Bars](#26-error-bars)
27. [Labels](#27-labels)
28. [Title](#28-title)
29. [Legend](#29-legend)
30. [Colors](#30-colors)
31. [Line Styles](#31-line-styles)
32. [Markers](#32-markers)
33. [Line Width](#33-line-width)
34. [Grid](#34-grid)
35. [Axis Limits](#35-axis-limits)
36. [Ticks](#36-ticks)
37. [Text and Annotations](#37-text-and-annotations)
38. [Figure Size](#38-figure-size)
39. [Transparency](#39-transparency)
40. [Subplots](#40-subplots)
41. [Multiple Plots](#41-multiple-plots)
42. [Saving Figures](#42-saving-figures)
43. [Display and Show](#43-display-and-show)
44. [Working with NumPy](#44-working-with-numpy)
45. [Working with Pandas](#45-working-with-pandas)
46. [Matplotlib Object-Oriented Approach](#46-matplotlib-object-oriented-approach)
47. [Common Plot Parameters](#47-common-plot-parameters)
48. [Choosing the Right Chart](#48-choosing-the-right-chart)
49. [Good Visualization Practices](#49-good-visualization-practices)
50. [Common Mistakes](#50-common-mistakes)
51. [Matplotlib vs Other Visualization Libraries](#51-matplotlib-vs-other-visualization-libraries)
52. [Data Visualization Workflow](#52-data-visualization-workflow)
53. [Real-World Example](#53-real-world-example)
54. [Interview Questions](#54-interview-questions)
55. [Quick Revision](#55-quick-revision)

---

# 1. What is Data Visualization?

**Data Visualization** is the graphical representation of data using charts, graphs, plots, diagrams, and other visual elements.

Instead of looking at thousands of rows of data, visualization allows us to understand:

* Patterns
* Trends
* Relationships
* Comparisons
* Distributions
* Outliers
* Changes over time
* Proportions

### Example

Suppose we have:

```text
Month       Sales
January     10000
February    15000
March       12000
April       20000
May         25000
```

Looking at numbers tells us the values.

A line chart immediately shows the **trend of sales over time**.

---

# 2. Why Data Visualization is Important

Data visualization is important because humans understand visual information faster than large tables of numbers.

### Main benefits

```text
Raw Data
   ↓
Visualization
   ↓
Patterns become visible
   ↓
Better Understanding
   ↓
Better Decisions
```

### It helps us identify:

* Increasing trends
* Decreasing trends
* Seasonal patterns
* Correlations
* Outliers
* Distribution
* Differences between groups
* Relationships between variables

---

# 3. Applications of Data Visualization

Data visualization is used in:

### Business

* Sales analysis
* Revenue tracking
* Profit analysis
* Customer analysis
* KPI dashboards

### Finance

* Stock price analysis
* Risk analysis
* Portfolio analysis
* Market trends

### Marketing

* Campaign performance
* Customer segmentation
* Conversion rates
* Website traffic

### Healthcare

* Patient statistics
* Disease trends
* Medical research

### Education

* Student performance
* Attendance analysis
* Exam results

### Data Science

* Exploratory Data Analysis (EDA)
* Feature analysis
* Model evaluation
* Error analysis

### Machine Learning

* Feature relationships
* Classification results
* Prediction errors
* Model performance

---

# 4. Data Visualization in Data Analytics

A typical data analytics workflow is:

```text
Data Collection
      ↓
Data Cleaning
      ↓
Data Manipulation
      ↓
Exploratory Data Analysis
      ↓
Data Visualization
      ↓
Pattern Identification
      ↓
Insights
      ↓
Decision Making
```

Visualization is especially important during **Exploratory Data Analysis (EDA)**.

---

# 5. Types of Data

Understanding the type of data helps us select the correct chart.

## 5.1 Numerical Data

Numerical data contains numbers.

Examples:

```text
Age
Salary
Height
Weight
Sales
Profit
Temperature
```

Numerical data can be:

### Discrete

Countable values.

```text
Number of students = 50
Number of products = 100
```

### Continuous

Can have decimal values.

```text
Height = 175.5 cm
Temperature = 36.7°C
Weight = 72.5 kg
```

---

# 5.2 Categorical Data

Categorical data represents groups or categories.

Examples:

```text
Gender
City
Department
Product Category
Country
Payment Method
```

Example:

```text
Male
Female
Male
Female
```

---

# 5.3 Time-Series Data

Data collected over time.

Examples:

```text
Date        Sales
Jan         10000
Feb         12000
Mar         15000
Apr         14000
```

Common visualization:

```text
Line Chart
```

---

# 6. Common Types of Charts

| Chart          | Main Purpose              |
| -------------- | ------------------------- |
| Line Chart     | Trends over time          |
| Bar Chart      | Compare categories        |
| Horizontal Bar | Compare categories        |
| Pie Chart      | Part-to-whole             |
| Scatter Plot   | Relationship/correlation  |
| Histogram      | Distribution              |
| Box Plot       | Distribution and outliers |
| Area Chart     | Trend + magnitude         |
| Stack Plot     | Composition over time     |
| Stem Plot      | Discrete numerical data   |

---

# 7. What is Matplotlib?

**Matplotlib** is a popular Python library used for creating static, animated, and interactive visualizations.

It is one of the fundamental visualization libraries in Python.

The main plotting module commonly used is:

```python
matplotlib.pyplot
```

Usually imported as:

```python
import matplotlib.pyplot as plt
```

---

# 8. Why Use Matplotlib?

Matplotlib provides:

* Line plots
* Bar charts
* Pie charts
* Histograms
* Scatter plots
* Box plots
* Area plots
* Subplots
* Custom colors
* Labels
* Titles
* Legends
* Annotations
* Axis customization
* Figure customization
* Image export

It also provides the foundation for several other Python visualization tools.

---

# 9. Applications of Matplotlib

Matplotlib is commonly used for:

```text
Exploratory Data Analysis
        ↓
Statistical Visualization
        ↓
Scientific Visualization
        ↓
Business Analysis
        ↓
Machine Learning Analysis
        ↓
Research
        ↓
Reporting
```

---

# 10. Installation

Install using pip:

```bash
pip install matplotlib
```

If using Jupyter Notebook:

```bash
pip install matplotlib
```

Verify installation:

```python
import matplotlib

print(matplotlib.__version__)
```

---

# 11. Importing Matplotlib

The standard import is:

```python
import matplotlib.pyplot as plt
```

`plt` is simply an alias commonly used for `matplotlib.pyplot`.

Example:

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [10, 20, 30])
plt.show()
```

---

# 12. Pyplot

`pyplot` provides functions for creating and customizing plots.

Common functions include:

```python
plt.plot()
plt.bar()
plt.barh()
plt.scatter()
plt.pie()
plt.hist()
plt.boxplot()
plt.fill_between()
plt.stem()
plt.stackplot()
plt.step()
plt.xlabel()
plt.ylabel()
plt.title()
plt.legend()
plt.grid()
plt.xlim()
plt.ylim()
plt.xticks()
plt.yticks()
plt.show()
plt.savefig()
```

---

# 13. Basic Plot

The simplest plot:

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 25, 30]

plt.plot(x, y)

plt.show()
```

Output:

```text
A line chart connecting the points.
```

---

# 14. Figure and Axes

Two important Matplotlib concepts are:

```text
Figure
   ↓
Complete canvas/window
   ↓
Axes
   ↓
Actual plotting area
```

### Figure

The entire visualization container.

### Axes

The area containing:

* X-axis
* Y-axis
* Plot
* Labels
* Title
* Data

Example:

```python
fig, ax = plt.subplots()

ax.plot([1, 2, 3], [10, 20, 30])

plt.show()
```

This is the **object-oriented approach**.

---

# 15. Line Chart

A line chart is mainly used to show:

* Trends
* Changes over time
* Continuous data
* Ordered data

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [10000, 15000, 12000, 20000, 25000]

plt.plot(months, sales)

plt.show()
```

---

## 15.1 Line Chart with Labels

```python
plt.plot(
    months,
    sales,
    color="blue",
    marker="o",
    linestyle="-",
    linewidth=2
)

plt.xlabel("Month")
plt.ylabel("Sales")
plt.title("Monthly Sales")

plt.show()
```

---

# 16. Bar Chart

Bar charts are used to compare categories.

```python
import matplotlib.pyplot as plt

products = ["Laptop", "Phone", "Tablet", "Watch"]
sales = [500, 800, 300, 400]

plt.bar(products, sales)

plt.xlabel("Product")
plt.ylabel("Sales")
plt.title("Product Sales")

plt.show()
```

---

## 16.1 Changing Bar Color

```python
plt.bar(
    products,
    sales,
    color="skyblue"
)

plt.show()
```

---

## 16.2 Different Colors

```python
colors = [
    "red",
    "blue",
    "green",
    "orange"
]

plt.bar(
    products,
    sales,
    color=colors
)

plt.show()
```

---

# 17. Horizontal Bar Chart

Use:

```python
plt.barh()
```

Example:

```python
products = ["Laptop", "Phone", "Tablet", "Watch"]
sales = [500, 800, 300, 400]

plt.barh(products, sales)

plt.xlabel("Sales")
plt.ylabel("Product")
plt.title("Product Sales")

plt.show()
```

### When useful?

Horizontal bars are useful when category names are long.

---

# 18. Pie Chart

Pie charts show **parts of a whole**.

```python
import matplotlib.pyplot as plt

labels = [
    "Laptop",
    "Phone",
    "Tablet",
    "Watch"
]

sales = [500, 800, 300, 400]

plt.pie(
    sales,
    labels=labels
)

plt.title("Sales Distribution")

plt.show()
```

---

## 18.1 Percentages

Use:

```python
autopct="%1.1f%%"
```

Example:

```python
plt.pie(
    sales,
    labels=labels,
    autopct="%1.1f%%"
)

plt.show()
```

---

## 18.2 Explode

`explode` separates a slice from the pie.

```python
explode = [0, 0.1, 0, 0]

plt.pie(
    sales,
    labels=labels,
    explode=explode,
    autopct="%1.1f%%"
)

plt.show()
```

---

## 18.3 Start Angle

```python
plt.pie(
    sales,
    labels=labels,
    startangle=90
)

plt.show()
```

---

# 19. Scatter Plot

Scatter plots show the relationship between two numerical variables.

Example:

```python
import matplotlib.pyplot as plt

height = [150, 160, 165, 170, 175, 180]
weight = [50, 55, 60, 65, 70, 80]

plt.scatter(height, weight)

plt.xlabel("Height")
plt.ylabel("Weight")
plt.title("Height vs Weight")

plt.show()
```

Scatter plots are useful for identifying:

* Positive relationships
* Negative relationships
* No relationship
* Clusters
* Outliers

---

# 20. Histogram

A histogram shows the **distribution of numerical data**.

Example:

```python
import matplotlib.pyplot as plt

ages = [
    18, 20, 21, 22, 22,
    25, 25, 26, 28, 30,
    31, 32, 35, 40, 42
]

plt.hist(ages)

plt.xlabel("Age")
plt.ylabel("Frequency")
plt.title("Age Distribution")

plt.show()
```

---

## 20.1 Bins

Bins divide numerical data into intervals.

```python
plt.hist(
    ages,
    bins=5
)

plt.show()
```

More bins:

```python
plt.hist(
    ages,
    bins=10
)

plt.show()
```

---

# 21. Box Plot

A box plot is useful for understanding:

* Median
* Quartiles
* Spread
* Outliers

```python
import matplotlib.pyplot as plt

salary = [
    20000,
    25000,
    30000,
    35000,
    40000,
    45000,
    50000,
    100000
]

plt.boxplot(salary)

plt.ylabel("Salary")
plt.title("Salary Distribution")

plt.show()
```

---

## Box Plot Components

```text
        Maximum
           |
      ────────
        Upper
       Whisker
           |
      ┌────────┐
      │        │
      │ Median │
      │        │
      └────────┘
           |
      Lower Whisker
           |
        Minimum

    • = Possible Outlier
```

Important terms:

```text
Minimum
Q1
Median
Q3
Maximum
IQR
Outliers
```

Where:

```text
IQR = Q3 - Q1
```

---

# 22. Area Chart

An area chart shows trends while emphasizing magnitude.

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
sales = [100, 150, 130, 200]

plt.fill_between(
    months,
    sales
)

plt.xlabel("Month")
plt.ylabel("Sales")
plt.title("Sales Area Chart")

plt.show()
```

---

# 23. Stem Plot

A stem plot represents discrete numerical data.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 30, 25]

plt.stem(x, y)

plt.show()
```

---

# 24. Stack Plot

A stack plot shows how multiple quantities contribute to a total over time.

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]

product_a = [10, 20, 30, 40]
product_b = [20, 30, 25, 35]
product_c = [15, 25, 20, 30]

plt.stackplot(
    months,
    product_a,
    product_b,
    product_c,
    labels=[
        "Product A",
        "Product B",
        "Product C"
    ]
)

plt.legend()

plt.show()
```

---

# 25. Step Plot

A step plot displays values as steps rather than continuous diagonal lines.

```python
x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 30, 25]

plt.step(x, y)

plt.show()
```

Useful for:

* Discrete changes
* State changes
* Stepwise processes

---

# 26. Error Bars

Error bars represent uncertainty or variability.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 15, 20, 25]
error = [1, 2, 1.5, 2]

plt.errorbar(
    x,
    y,
    yerr=error,
    fmt="o"
)

plt.show()
```

---

# 27. Labels

Labels explain what the axes represent.

### X-axis

```python
plt.xlabel("Month")
```

### Y-axis

```python
plt.ylabel("Sales")
```

Example:

```python
plt.plot(months, sales)

plt.xlabel("Month")
plt.ylabel("Sales")

plt.show()
```

---

# 28. Title

Use:

```python
plt.title()
```

Example:

```python
plt.title("Monthly Sales Analysis")
```

Complete example:

```python
plt.plot(months, sales)

plt.xlabel("Month")
plt.ylabel("Sales")
plt.title("Monthly Sales Analysis")

plt.show()
```

---

# 29. Legend

A legend identifies different data series.

```python
months = ["Jan", "Feb", "Mar", "Apr"]

sales = [100, 150, 130, 200]
profit = [20, 40, 30, 60]

plt.plot(
    months,
    sales,
    label="Sales"
)

plt.plot(
    months,
    profit,
    label="Profit"
)

plt.legend()

plt.show()
```

---

# 30. Colors

Matplotlib supports many ways to specify colors.

Examples:

```python
color="red"
color="blue"
color="green"
color="black"
color="orange"
color="purple"
color="pink"
```

Hexadecimal colors:

```python
color="#3498db"
```

RGB-style colors can also be specified using normalized values:

```python
color=(0.2, 0.5, 0.8)
```

---

# 31. Line Styles

Common line styles:

```text
-      Solid
--     Dashed
:      Dotted
-.     Dash-dot
```

Example:

```python
plt.plot(
    x,
    y,
    linestyle="--"
)

plt.show()
```

---

# 32. Markers

Markers indicate individual data points.

Common markers:

```text
o    Circle
s    Square
^    Triangle
*    Star
+    Plus
x    X
D    Diamond
```

Example:

```python
plt.plot(
    x,
    y,
    marker="o"
)

plt.show()
```

---

# 33. Line Width

Use:

```python
linewidth
```

Example:

```python
plt.plot(
    x,
    y,
    linewidth=3
)

plt.show()
```

---

# 34. Grid

Grid lines can make a chart easier to read.

```python
plt.grid()
```

Example:

```python
plt.plot(x, y)

plt.grid()

plt.show()
```

Customize:

```python
plt.grid(
    linestyle="--",
    alpha=0.5
)
```

---

# 35. Axis Limits

## X-axis

```python
plt.xlim(0, 10)
```

## Y-axis

```python
plt.ylim(0, 100)
```

Example:

```python
plt.plot(x, y)

plt.xlim(0, 6)
plt.ylim(0, 40)

plt.show()
```

---

# 36. Ticks

Ticks are the values shown along the axes.

## X ticks

```python
plt.xticks(
    [1, 2, 3, 4, 5]
)
```

## Y ticks

```python
plt.yticks(
    [0, 10, 20, 30, 40]
)
```

You can also rotate labels:

```python
plt.xticks(
    rotation=45
)
```

---

# 37. Text and Annotations

## Add Text

```python
plt.text(
    3,
    20,
    "Important Point"
)
```

---

## Annotate a Point

```python
plt.annotate(
    "Highest Sales",
    xy=(5, 30),
    xytext=(3, 25),
    arrowprops={
        "arrowstyle": "->"
    }
)
```

Annotations are useful for highlighting important observations.

---

# 38. Figure Size

Use:

```python
plt.figure(figsize=(10, 6))
```

Example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.plot(x, y)

plt.show()
```

`figsize` is generally specified as:

```text
(width, height)
```

in inches.

---

# 39. Transparency

Transparency is controlled using `alpha`.

Example:

```python
plt.plot(
    x,
    y,
    alpha=0.5
)
```

Where:

```text
alpha = 1.0 → completely opaque
alpha = 0.5 → semi-transparent
alpha = 0.0 → completely transparent
```

---

# 40. Subplots

Subplots allow multiple plots to be displayed in one figure.

```python
import matplotlib.pyplot as plt

plt.subplot(2, 1, 1)

plt.plot(
    [1, 2, 3],
    [10, 20, 30]
)

plt.title("Line Chart")


plt.subplot(2, 1, 2)

plt.bar(
    ["A", "B", "C"],
    [20, 30, 15]
)

plt.title("Bar Chart")

plt.tight_layout()

plt.show()
```

The syntax is:

```python
plt.subplot(
    rows,
    columns,
    position
)
```

---

# 41. Multiple Plots Using `subplots()`

The preferred object-oriented approach:

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(
    2,
    2,
    figsize=(10, 8)
)

axes[0, 0].plot(
    [1, 2, 3],
    [10, 20, 30]
)

axes[0, 1].bar(
    ["A", "B", "C"],
    [20, 30, 15]
)

axes[1, 0].scatter(
    [1, 2, 3],
    [30, 20, 40]
)

axes[1, 1].hist(
    [10, 20, 20, 30, 30, 30]
)

plt.tight_layout()

plt.show()
```

Layout:

```text
┌──────────────┬──────────────┐
│ Line         │ Bar          │
├──────────────┼──────────────┤
│ Scatter      │ Histogram    │
└──────────────┴──────────────┘
```

---

# 42. Saving Figures

Use:

```python
plt.savefig()
```

Example:

```python
plt.plot(x, y)

plt.savefig(
    "sales_chart.png"
)

plt.show()
```

You can save as:

```text
PNG
JPG/JPEG
PDF
SVG
```

Example:

```python
plt.savefig(
    "sales_chart.pdf"
)
```

---

## High Resolution

Use `dpi`:

```python
plt.savefig(
    "chart.png",
    dpi=300
)
```

Higher DPI generally produces a higher-resolution raster image.

---

# 43. Display and Show

Use:

```python
plt.show()
```

to display the figure.

Typical workflow:

```python
plt.plot(x, y)

plt.title("My Chart")

plt.show()
```

---

# 44. Working with NumPy

Matplotlib works very well with NumPy.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(
    0,
    10,
    100
)

y = x ** 2

plt.plot(x, y)

plt.xlabel("X")
plt.ylabel("Y")
plt.title("X Squared")

plt.show()
```

---

# 45. Working with Pandas

Matplotlib can visualize Pandas DataFrames.

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "Month": [
        "Jan",
        "Feb",
        "Mar",
        "Apr"
    ],
    "Sales": [
        100,
        150,
        130,
        200
    ]
})

plt.plot(
    df["Month"],
    df["Sales"]
)

plt.xlabel("Month")
plt.ylabel("Sales")
plt.title("Monthly Sales")

plt.show()
```

---

# 46. Matplotlib Object-Oriented Approach

There are two common approaches.

## Pyplot Style

```python
plt.plot(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Chart")
plt.show()
```

## Object-Oriented Style

```python
fig, ax = plt.subplots()

ax.plot(x, y)

ax.set_xlabel("X")
ax.set_ylabel("Y")
ax.set_title("Chart")

plt.show()
```

### Difference

Pyplot is convenient for simple plots.

Object-oriented Matplotlib is generally preferable for:

* Multiple plots
* Subplots
* Complex figures
* Reusable visualization code
* Larger projects

---

# 47. Common Plot Parameters

Many Matplotlib plotting functions accept common parameters.

| Parameter         | Purpose             |
| ----------------- | ------------------- |
| `color`           | Color               |
| `marker`          | Data point marker   |
| `linestyle`       | Line style          |
| `linewidth`       | Line thickness      |
| `alpha`           | Transparency        |
| `label`           | Legend label        |
| `markersize`      | Marker size         |
| `markerfacecolor` | Marker fill         |
| `markeredgecolor` | Marker border       |
| `markeredgewidth` | Marker border width |

Example:

```python
plt.plot(
    x,
    y,
    color="blue",
    marker="o",
    linestyle="--",
    linewidth=2,
    markersize=8,
    alpha=0.7,
    label="Sales"
)

plt.legend()

plt.show()
```

---

# 48. Choosing the Right Chart

Choosing the correct visualization is extremely important.

## Compare Categories

Use:

```text
Bar Chart
```

Example:

```text
Sales by Product
```

---

## Show Trend Over Time

Use:

```text
Line Chart
```

Example:

```text
Monthly Revenue
```

---

## Show Relationship

Use:

```text
Scatter Plot
```

Example:

```text
Advertising Spend vs Sales
```

---

## Show Distribution

Use:

```text
Histogram
```

Example:

```text
Age Distribution
```

---

## Show Outliers and Spread

Use:

```text
Box Plot
```

Example:

```text
Salary Distribution
```

---

## Show Part of Whole

Use:

```text
Pie Chart
```

when there are only a few meaningful categories making up one total.

Example:

```text
Market Share
```

---

# 49. Good Visualization Practices

A good visualization should be:

### 1. Clear

The viewer should understand the chart quickly.

### 2. Relevant

Use the chart that matches the analytical question.

### 3. Simple

Avoid unnecessary decoration.

### 4. Properly Labeled

Always consider:

```text
Title
X-axis
Y-axis
Legend
Units
```

### 5. Accurate

Do not visually distort the data.

### 6. Readable

Avoid:

* Tiny labels
* Excessive colors
* Overlapping text
* Unnecessary 3D effects

---

# 50. Common Mistakes

## Mistake 1 — Wrong Chart

Using a pie chart for a time series.

Better:

```text
Time Series → Line Chart
```

---

## Mistake 2 — Missing Labels

Bad:

```python
plt.plot(x, y)
```

Better:

```python
plt.plot(x, y)

plt.xlabel("Month")
plt.ylabel("Revenue")
plt.title("Monthly Revenue")

plt.show()
```

---

## Mistake 3 — Too Many Colors

Using many colors without meaning makes charts difficult to understand.

Use color intentionally.

---

## Mistake 4 — Too Much Information

Putting dozens of unrelated variables into one chart can make it confusing.

---

## Mistake 5 — Misleading Axis

Axis scaling can make small differences appear much larger or smaller than they really are.

Always inspect axis limits carefully.

---

# 51. Matplotlib vs Other Visualization Libraries

| Library    | Main Strength                         |
| ---------- | ------------------------------------- |
| Matplotlib | Flexible foundational plotting        |
| Seaborn    | Statistical visualization             |
| Plotly     | Interactive visualization             |
| Bokeh      | Interactive web visualizations        |
| Altair     | Declarative statistical visualization |

### Matplotlib

Best when you need:

```text
Detailed control
Customization
Static charts
Scientific plots
Publication-quality figures
```

### Seaborn

Built on Matplotlib and particularly useful for statistical visualizations.

### Plotly

Excellent for interactive charts and dashboards.

---

# 52. Data Visualization Workflow

A practical workflow:

```text
1. Understand the question
        ↓
2. Collect data
        ↓
3. Clean data
        ↓
4. Manipulate data
        ↓
5. Understand variable types
        ↓
6. Select suitable chart
        ↓
7. Create visualization
        ↓
8. Add labels/title/legend
        ↓
9. Interpret visualization
        ↓
10. Extract insights
```

---

# 53. Real-World Example

Suppose an e-commerce company has:

```text
Month       Sales       Profit
Jan         100000      20000
Feb         120000      25000
Mar         150000      35000
Apr         140000      30000
May         180000      45000
```

We can visualize sales and profit.

```python
import matplotlib.pyplot as plt

months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May"
]

sales = [
    100000,
    120000,
    150000,
    140000,
    180000
]

profit = [
    20000,
    25000,
    35000,
    30000,
    45000
]

plt.figure(figsize=(10, 6))

plt.plot(
    months,
    sales,
    marker="o",
    label="Sales"
)

plt.plot(
    months,
    profit,
    marker="o",
    label="Profit"
)

plt.xlabel("Month")
plt.ylabel("Amount")
plt.title("Monthly Sales and Profit")

plt.legend()
plt.grid(alpha=0.3)

plt.show()
```

### What can we observe?

The visualization can help us identify:

```text
Sales trend
Profit trend
Highest sales month
Highest profit month
Month-to-month changes
Relationship between sales and profit
```

---

# 54. Interview Questions

## Q1. What is data visualization?

Data visualization is the graphical representation of data using charts, graphs, plots, and other visual elements to identify patterns, trends, relationships, distributions, and insights.

---

## Q2. What is Matplotlib?

Matplotlib is a Python visualization library used to create static, animated, and interactive visualizations.

---

## Q3. How do you install Matplotlib?

```bash
pip install matplotlib
```

---

## Q4. How do you import Matplotlib?

```python
import matplotlib.pyplot as plt
```

---

## Q5. What is `pyplot`?

`pyplot` is a Matplotlib module that provides a collection of functions for creating and customizing plots.

---

## Q6. What is `plt.show()`?

It displays the current Matplotlib figure.

---

## Q7. What is `plt.plot()`?

It is commonly used to create line plots.

---

## Q8. What is the difference between a bar chart and histogram?

### Bar Chart

Used to compare **categorical data**.

```text
Product A → 100
Product B → 200
Product C → 150
```

### Histogram

Used to show the **distribution of numerical data**.

```text
Age
10–20
20–30
30–40
40–50
```

---

## Q9. What is a scatter plot?

A scatter plot displays individual observations using points to show the relationship between two numerical variables.

---

## Q10. What is a box plot?

A box plot summarizes the distribution of numerical data using quartiles, median, whiskers, and potential outliers.

---

## Q11. What is a subplot?

A subplot allows multiple plots to be placed within one figure.

---

## Q12. What is the difference between Figure and Axes?

```text
Figure → Entire visualization canvas

Axes → Individual plotting area
```

A Figure can contain multiple Axes.

---

## Q13. How do you save a Matplotlib chart?

```python
plt.savefig("chart.png")
```

---

## Q14. How do you add a title?

```python
plt.title("Sales Analysis")
```

---

## Q15. How do you add axis labels?

```python
plt.xlabel("Month")
plt.ylabel("Sales")
```

---

## Q16. How do you add a legend?

```python
plt.legend()
```

---

## Q17. How do you display grid lines?

```python
plt.grid()
```

---

# 55. Quick Revision

## Matplotlib Import

```python
import matplotlib.pyplot as plt
```

## Line

```python
plt.plot(x, y)
```

## Bar

```python
plt.bar(x, y)
```

## Horizontal Bar

```python
plt.barh(x, y)
```

## Scatter

```python
plt.scatter(x, y)
```

## Pie

```python
plt.pie(values, labels=labels)
```

## Histogram

```python
plt.hist(data)
```

## Box Plot

```python
plt.boxplot(data)
```

## Area

```python
plt.fill_between(x, y)
```

## Stem

```python
plt.stem(x, y)
```

## Stack Plot

```python
plt.stackplot(x, y1, y2, y3)
```

## Step Plot

```python
plt.step(x, y)
```

## Title

```python
plt.title("Title")
```

## X Label

```python
plt.xlabel("X")
```

## Y Label

```python
plt.ylabel("Y")
```

## Legend

```python
plt.legend()
```

## Grid

```python
plt.grid()
```

## X Limits

```python
plt.xlim(min, max)
```

## Y Limits

```python
plt.ylim(min, max)
```

## Figure Size

```python
plt.figure(figsize=(10, 6))
```

## Save

```python
plt.savefig("chart.png")
```

## Display

```python
plt.show()
```

## Subplots

```python
fig, axes = plt.subplots(2, 2)
```

---

# 🧠 Final Memory Map

```text
                 DATA VISUALIZATION
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
     Compare          Trends          Relationships
        │                │                │
      Bar              Line           Scatter
        │
        └───────────────┐
                        ↓
                 Distribution
                  ┌─────┴─────┐
                  ↓           ↓
              Histogram     Box Plot
                  
                 Composition
                      ↓
                    Pie

                         │
                         ↓
                    MATPLOTLIB
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
       Pyplot         Figure          Axes
          │
          ↓
    Create Plot
          │
          ├── plot()
          ├── bar()
          ├── barh()
          ├── scatter()
          ├── pie()
          ├── hist()
          ├── boxplot()
          ├── stackplot()
          ├── stem()
          └── step()
          
          ↓
     Customize
          │
          ├── title()
          ├── xlabel()
          ├── ylabel()
          ├── legend()
          ├── grid()
          ├── xlim()
          ├── ylim()
          ├── xticks()
          └── yticks()
          
          ↓
      Save / Display
          │
          ├── savefig()
          └── show()
```

---

# ⭐ Most Important Things to Remember

```text
Data Visualization
        ↓
Convert data into visual form

Matplotlib
        ↓
Python library for visualization

plt.plot()
        ↓
Line chart

plt.bar()
        ↓
Bar chart

plt.scatter()
        ↓
Relationship between numerical variables

plt.hist()
        ↓
Distribution

plt.boxplot()
        ↓
Distribution + outliers

plt.pie()
        ↓
Part-to-whole

plt.subplots()
        ↓
Multiple plots

plt.xlabel()
plt.ylabel()
        ↓
Axis labels

plt.title()
        ↓
Chart title

plt.legend()
        ↓
Identify data series

plt.grid()
        ↓
Grid lines

plt.savefig()
        ↓
Save chart

plt.show()
        ↓
Display chart
```

## 🔑 One-Line Revision

> **Data Visualization converts data into visual insights, and Matplotlib is a flexible Python library used to create and customize those visualizations.**
