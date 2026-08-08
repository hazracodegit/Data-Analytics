# 🐍 NumPy — Complete Notes for Data Analytics

> **NumPy = Numerical Python**

NumPy is one of the most important Python libraries for **numerical computing, data analysis, scientific computing, machine learning, and data science**.

Its most important feature is the **N-dimensional array (`ndarray`)**.

Official documentation: [NumPy Documentation](https://numpy.org/doc/stable/?utm_source=chatgpt.com)

---

# 📚 Table of Contents

1. What is NumPy?
2. Why NumPy?
3. Applications of NumPy
4. NumPy in Data Analytics
5. Installation
6. Importing NumPy
7. NumPy Version
8. Python List vs NumPy Array
9. NumPy Array
10. Dimensions
11. Creating Arrays
12. Array Attributes
13. Data Types
14. Type Conversion
15. Indexing
16. Slicing
17. Negative Indexing
18. 2D Array Indexing
19. Boolean Indexing
20. Fancy Indexing
21. Array Operations
22. Arithmetic Operations
23. Comparison Operations
24. Logical Operations
25. Broadcasting
26. Aggregation Functions
27. Axis
28. Mathematical Functions
29. Rounding Functions
30. Trigonometric Functions
31. Exponential and Logarithmic Functions
32. Array Manipulation
33. Reshape
34. Flatten
35. Ravel
36. Transpose
37. Swap Axes
38. Expand Dimensions
39. Squeeze
40. Concatenation
41. Stack
42. Split
43. Repeat
44. Tile
45. Sorting
46. Searching
47. Unique Values
48. Set Operations
49. Copy vs View
50. Missing Values / NaN
51. Infinity
52. Random Module
53. Random Numbers
54. Random Sampling
55. Statistics
56. Percentiles
57. Covariance
58. Correlation
59. Linear Algebra
60. Matrix Operations
61. Dot Product
62. Matrix Multiplication
63. Inverse
64. Determinant
65. Eigenvalues
66. Solving Equations
67. Polynomial Operations
68. File Handling with NumPy
69. CSV Data
70. Performance
71. Vectorization
72. Broadcasting in Analytics
73. NumPy with Pandas
74. NumPy with Matplotlib
75. NumPy with Scikit-learn
76. Data Analytics Examples
77. Complete Analytics Example
78. Important Functions Cheat Sheet
79. Interview Questions
80. Practice Questions
81. Final Revision Checklist

---

# 🧠 What is NumPy?

NumPy is an open-source Python library designed primarily for **efficient numerical computation**.

It provides:

* Multidimensional arrays
* Fast array operations
* Mathematical functions
* Statistical functions
* Linear algebra
* Random number generation
* Sorting and searching
* Array manipulation
* Fourier transforms
* Numerical utilities

NumPy's central object is:

```python
numpy.ndarray
```

The official documentation describes `ndarray` as a homogeneous N-dimensional array object and NumPy as a core part of the scientific Python ecosystem.

---

# 🎯 Why is NumPy Used?

Python lists are useful, but numerical data processing using lists can become inefficient.

NumPy provides arrays designed specifically for numerical computation.

Example:

```python
numbers = [10, 20, 30, 40]
```

NumPy:

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])
```

NumPy arrays support operations directly on the whole array.

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])

print(numbers * 2)
```

Output:

```text
[20 40 60 80]
```

No explicit Python loop is required.

NumPy arrays are generally more compact and efficient for homogeneous numerical data than Python lists.

---

# 🚀 Main Features of NumPy

## 1. N-dimensional arrays

```python
np.array()
```

supports:

```text
1D
2D
3D
...
ND
```

---

## 2. Vectorized operations

```python
arr * 2
```

instead of:

```python
for x in arr:
    ...
```

---

## 3. Broadcasting

Allows arithmetic between compatible arrays of different shapes.

---

## 4. Mathematical functions

Examples:

```python
np.sqrt()
np.exp()
np.log()
np.sin()
np.cos()
```

---

## 5. Statistical functions

Examples:

```python
np.mean()
np.median()
np.std()
np.var()
np.percentile()
```

---

## 6. Linear algebra

Examples:

```python
np.linalg.inv()
np.linalg.det()
np.linalg.solve()
np.linalg.eig()
```

---

## 7. Random number generation

```python
np.random
```

---

## 8. Array manipulation

Examples:

```python
reshape()
flatten()
transpose()
concatenate()
split()
```

---

# 🌍 Applications of NumPy

NumPy is used in:

### Data Analytics

* Numerical calculations
* Data cleaning support
* Statistical calculations
* Feature preparation
* Aggregation
* Outlier calculations
* Normalization
* Standardization

### Machine Learning

* Feature matrices
* Numerical preprocessing
* Model calculations
* Linear algebra
* Random initialization

### Scientific Computing

* Physics
* Chemistry
* Biology
* Engineering
* Simulations

### Finance

* Portfolio calculations
* Risk analysis
* Returns
* Statistical modeling

### Image Processing

Images can be represented as arrays.

```text
Image
 ↓
Pixel matrix
 ↓
NumPy array
```

### Signal Processing

* Signals
* FFT
* Filtering calculations

### Deep Learning

Libraries such as PyTorch and TensorFlow use array/tensor concepts heavily, although their core tensor implementations are distinct from NumPy.

---

# 📊 NumPy in Data Analytics

This is especially important.

A typical analytics workflow looks like:

```text
Raw Data
   ↓
Pandas
   ↓
NumPy
   ↓
Numerical Processing
   ↓
Statistics
   ↓
Visualization
   ↓
Insights
```

NumPy is particularly useful when you need to perform fast numerical calculations on columns, matrices, arrays, or model inputs.

---

# 📈 Example: Data Analytics

Suppose sales are:

```python
import numpy as np

sales = np.array([10000, 12000, 15000, 9000, 18000])
```

Average:

```python
print(np.mean(sales))
```

Maximum:

```python
print(np.max(sales))
```

Minimum:

```python
print(np.min(sales))
```

Standard deviation:

```python
print(np.std(sales))
```

---

# 📦 Installation

Using pip:

```bash
pip install numpy
```

Using conda:

```bash
conda install numpy
```

The official beginner documentation lists both `pip install numpy` and `conda install numpy`.

---

# 📥 Import NumPy

The standard convention is:

```python
import numpy as np
```

Then:

```python
np.array()
np.mean()
np.max()
```

---

# 🔢 Check NumPy Version

```python
import numpy as np

print(np.__version__)
```

The current stable NumPy documentation is for **2.5**.

---

# 🐍 Python List vs NumPy Array

## Python List

```python
numbers = [1, 2, 3, 4]
```

## NumPy Array

```python
import numpy as np

numbers = np.array([1, 2, 3, 4])
```

### Important Differences

| Python List                           | NumPy Array                         |
| ------------------------------------- | ----------------------------------- |
| General-purpose                       | Numerical computing                 |
| Can contain mixed types               | Normally homogeneous dtype          |
| More flexible                         | More efficient for numerical arrays |
| Basic operations                      | Vectorized operations               |
| Less suitable for matrix calculations | Excellent for matrix calculations   |

NumPy arrays generally contain elements of a common data type (`dtype`).

---

# 🧱 Creating NumPy Arrays

## `np.array()`

```python
import numpy as np

arr = np.array([1, 2, 3, 4])

print(arr)
```

Output:

```text
[1 2 3 4]
```

---

# 📐 2D Array

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr)
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

---

# 📦 3D Array

```python
arr = np.array([
    [
        [1, 2],
        [3, 4]
    ],
    [
        [5, 6],
        [7, 8]
    ]
])

print(arr)
```

---

# 📏 Dimensions

## 0D

Single value:

```python
np.array(10)
```

---

## 1D

```python
np.array([1, 2, 3])
```

---

## 2D

```python
np.array([
    [1, 2],
    [3, 4]
])
```

---

## 3D

```python
np.array([
    [
        [1, 2],
        [3, 4]
    ]
])
```

---

# 🔍 Array Attributes

Important attributes:

```text
ndim
shape
size
dtype
itemsize
nbytes
```

---

# `ndim`

Returns number of dimensions.

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

print(arr.ndim)
```

Output:

```text
2
```

---

# `shape`

Returns dimensions along each axis.

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.shape)
```

Output:

```text
(2, 3)
```

Meaning:

```text
2 rows
3 columns
```

---

# `size`

Returns total number of elements.

```python
print(arr.size)
```

Output:

```text
6
```

---

# `dtype`

Returns data type.

```python
arr = np.array([1, 2, 3])

print(arr.dtype)
```

---

# `itemsize`

Returns bytes used by each element.

```python
print(arr.itemsize)
```

---

# `nbytes`

Total bytes occupied by array elements.

```python
print(arr.nbytes)
```

---

# 🏗️ Array Creation Functions

Important functions:

```text
np.array()
np.zeros()
np.ones()
np.empty()
np.full()
np.arange()
np.linspace()
np.eye()
np.identity()
np.diag()
```

---

# `np.zeros()`

Creates an array filled with zeros.

```python
arr = np.zeros(5)

print(arr)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

2D:

```python
arr = np.zeros((2, 3))

print(arr)
```

---

# `np.ones()`

```python
arr = np.ones(5)

print(arr)
```

---

# `np.full()`

```python
arr = np.full(5, 10)

print(arr)
```

Output:

```text
[10 10 10 10 10]
```

---

# `np.empty()`

Creates an array without initializing its values to a particular value.

```python
arr = np.empty(5)

print(arr)
```

Do not assume the values are zero.

---

# `np.arange()`

Creates evenly spaced values with a specified step.

```python
arr = np.arange(1, 10)

print(arr)
```

Output:

```text
[1 2 3 4 5 6 7 8 9]
```

Step:

```python
arr = np.arange(1, 10, 2)

print(arr)
```

Output:

```text
[1 3 5 7 9]
```

---

# `np.linspace()`

Creates a specified number of evenly spaced values between two endpoints.

```python
arr = np.linspace(0, 10, 5)

print(arr)
```

Output:

```text
[ 0.   2.5  5.   7.5 10. ]
```

### Difference

```text
arange()
→ controls step size

linspace()
→ controls number of values
```

---

# `np.eye()`

Creates an identity-like 2D array.

```python
arr = np.eye(3)

print(arr)
```

Output:

```text
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

---

# `np.identity()`

```python
arr = np.identity(3)

print(arr)
```

---

# `np.diag()`

Create diagonal array:

```python
arr = np.diag([1, 2, 3])

print(arr)
```

Output:

```text
[[1 0 0]
 [0 2 0]
 [0 0 3]]
```

---

# 🔢 Data Types

NumPy supports many numeric and other dtypes.

Common ones:

```text
int8
int16
int32
int64

uint8
uint16
uint32
uint64

float16
float32
float64

complex64
complex128

bool
str/object-related types
datetime64
timedelta64
```

Example:

```python
arr = np.array([1, 2, 3], dtype=np.float64)

print(arr)
print(arr.dtype)
```

---

# 🔄 Type Conversion

Use:

```python
astype()
```

Example:

```python
arr = np.array([1, 2, 3])

new_arr = arr.astype(float)

print(new_arr)
print(new_arr.dtype)
```

---

# 🔢 Integer to Float

```python
arr = np.array([1, 2, 3])

arr = arr.astype(np.float64)

print(arr)
```

---

# 🔤 Float to Integer

```python
arr = np.array([1.9, 2.8, 3.7])

new_arr = arr.astype(int)

print(new_arr)
```

The conversion truncates toward zero for ordinary finite floating values.

---

# 🎯 Specifying dtype

```python
arr = np.array(
    [1, 2, 3],
    dtype=np.float32
)
```

---

# 🔎 Indexing

NumPy indexing starts from `0`.

```python
arr = np.array([10, 20, 30, 40])

print(arr[0])
print(arr[2])
```

Output:

```text
10
30
```

---

# 🔙 Negative Indexing

```python
arr = np.array([10, 20, 30, 40])

print(arr[-1])
print(arr[-2])
```

Output:

```text
40
30
```

---

# ✂️ Slicing

Syntax:

```text
array[start:stop:step]
```

Example:

```python
arr = np.array([10, 20, 30, 40, 50])

print(arr[1:4])
```

Output:

```text
[20 30 40]
```

---

# Slicing with Step

```python
print(arr[::2])
```

Output:

```text
[10 30 50]
```

Reverse:

```python
print(arr[::-1])
```

---

# 📊 2D Indexing

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr[0, 1])
```

Output:

```text
20
```

Format:

```text
arr[row, column]
```

---

# 📌 Access Row

```python
print(arr[0])
```

Output:

```text
[10 20 30]
```

---

# 📌 Access Column

```python
print(arr[:, 1])
```

Output:

```text
[20 50]
```

---

# 🎯 Boolean Indexing

Very important for Data Analytics.

```python
arr = np.array([10, 20, 30, 40, 50])

print(arr[arr > 25])
```

Output:

```text
[30 40 50]
```

This is extremely useful for filtering.

---

# 🔥 Multiple Conditions

Use:

```python
&
|
~
```

Example:

```python
arr = np.array([10, 20, 30, 40, 50])

result = arr[(arr > 20) & (arr < 50)]

print(result)
```

Output:

```text
[30 40]
```

---

# 🎯 Fancy Indexing

Use arrays/lists of indices.

```python
arr = np.array([10, 20, 30, 40, 50])

indices = [0, 2, 4]

print(arr[indices])
```

Output:

```text
[10 30 50]
```

---

# ➕ Arithmetic Operations

NumPy performs element-wise arithmetic.

```python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)
print(a - b)
print(a * b)
print(a / b)
```

Output:

```text
[11 22 33]
[ 9 18 27]
[10 40 90]
[10. 10. 10.]
```

---

# ➗ Other Arithmetic

```python
print(a // b)
print(a % b)
print(a ** b)
```

---

# ➕ Scalar Operations

```python
arr = np.array([10, 20, 30])

print(arr + 5)
print(arr * 2)
print(arr / 10)
```

---

# ⚖️ Comparison Operations

```python
arr = np.array([10, 20, 30])

print(arr > 15)
print(arr == 20)
print(arr != 20)
print(arr <= 20)
```

Output contains Boolean values.

---

# 🧠 Logical Operations

Functions:

```text
np.logical_and()
np.logical_or()
np.logical_not()
np.logical_xor()
```

Example:

```python
arr = np.array([10, 20, 30, 40])

result = np.logical_and(arr > 15, arr < 40)

print(result)
```

---

# 📡 Broadcasting

Broadcasting allows NumPy to perform operations between arrays with compatible shapes.

Example:

```python
arr = np.array([10, 20, 30])

print(arr + 5)
```

Conceptually:

```text
[10, 20, 30]
+
[ 5,  5,  5]
```

Result:

```text
[15, 25, 35]
```

---

# 📊 2D Broadcasting

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr + 10)
```

Output:

```text
[[20 30 40]
 [50 60 70]]
```

---

# 📈 Column Broadcasting

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

column = np.array([
    [10],
    [20]
])

print(arr + column)
```

Output:

```text
[[11 12 13]
 [24 25 26]]
```

Broadcasting is powerful, but very large intermediate arrays can increase memory usage, so it should be used thoughtfully.

---

# 📊 Aggregation Functions

Very important in Data Analytics.

Common functions:

```text
np.sum()
np.mean()
np.median()
np.min()
np.max()
np.std()
np.var()
np.prod()
np.ptp()
```

---

# `np.sum()`

```python
arr = np.array([10, 20, 30, 40])

print(np.sum(arr))
```

Output:

```text
100
```

---

# `np.mean()`

```python
print(np.mean(arr))
```

Output:

```text
25.0
```

---

# `np.median()`

```python
arr = np.array([10, 20, 30, 40, 50])

print(np.median(arr))
```

---

# `np.min()`

```python
print(np.min(arr))
```

---

# `np.max()`

```python
print(np.max(arr))
```

---

# `np.std()`

Standard deviation:

```python
print(np.std(arr))
```

---

# `np.var()`

Variance:

```python
print(np.var(arr))
```

---

# `np.prod()`

Product of elements:

```python
arr = np.array([1, 2, 3, 4])

print(np.prod(arr))
```

Output:

```text
24
```

---

# `np.ptp()`

Peak-to-peak range:

```text
maximum - minimum
```

```python
arr = np.array([10, 20, 50])

print(np.ptp(arr))
```

Output:

```text
40
```

---

# 📐 Axis

One of the most important NumPy concepts.

Consider:

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
```

Shape:

```text
(2, 3)
```

## `axis=0`

Operate down rows, producing one result for each column.

```python
print(np.sum(arr, axis=0))
```

Output:

```text
[50 70 90]
```

Calculation:

```text
10 + 40 = 50
20 + 50 = 70
30 + 60 = 90
```

---

## `axis=1`

Operate across columns, producing one result for each row.

```python
print(np.sum(arr, axis=1))
```

Output:

```text
[ 60 150]
```

Calculation:

```text
10 + 20 + 30 = 60
40 + 50 + 60 = 150
```

---

# 🧮 Mathematical Functions

NumPy provides many mathematical functions.

Common ones:

```text
np.abs()
np.sqrt()
np.square()
np.power()
np.exp()
np.log()
np.log10()
np.log2()
np.sign()
```

---

# `np.abs()`

```python
arr = np.array([-10, -20, 30])

print(np.abs(arr))
```

Output:

```text
[10 20 30]
```

---

# `np.sqrt()`

```python
arr = np.array([4, 9, 16])

print(np.sqrt(arr))
```

Output:

```text
[2. 3. 4.]
```

---

# `np.square()`

```python
arr = np.array([2, 3, 4])

print(np.square(arr))
```

---

# `np.power()`

```python
arr = np.array([2, 3, 4])

print(np.power(arr, 2))
```

---

# `np.exp()`

```python
arr = np.array([1, 2, 3])

print(np.exp(arr))
```

---

# `np.log()`

Natural logarithm:

```python
arr = np.array([1, 10, 100])

print(np.log(arr))
```

---

# `np.log10()`

```python
print(np.log10([1, 10, 100]))
```

Output:

```text
[0. 1. 2.]
```

---

# 🔄 Rounding Functions

Common:

```text
np.round()
np.floor()
np.ceil()
np.trunc()
```

---

# `np.round()`

```python
arr = np.array([1.234, 2.567, 3.891])

print(np.round(arr, 2))
```

---

# `np.floor()`

Rounds down.

```python
arr = np.array([1.2, 2.8, -1.2])

print(np.floor(arr))
```

---

# `np.ceil()`

Rounds upward.

```python
print(np.ceil(arr))
```

---

# 📐 Trigonometric Functions

```text
np.sin()
np.cos()
np.tan()
np.arcsin()
np.arccos()
np.arctan()
```

Example:

```python
angles = np.array([0, np.pi / 2, np.pi])

print(np.sin(angles))
```

---

# 🔢 Degrees and Radians

```python
degrees = np.array([0, 90, 180])

radians = np.deg2rad(degrees)

print(radians)
```

Convert back:

```python
print(np.rad2deg(radians))
```

---

# 📦 Array Shape Manipulation

Important functions:

```text
reshape()
flatten()
ravel()
transpose()
T
swapaxes()
moveaxis()
expand_dims()
squeeze()
```

---

# `reshape()`

Changes shape without changing the number of elements.

```python
arr = np.arange(6)

new_arr = arr.reshape(2, 3)

print(new_arr)
```

Output:

```text
[[0 1 2]
 [3 4 5]]
```

Total elements must remain compatible:

```text
2 × 3 = 6
```

---

# `reshape(-1)`

Let NumPy infer one dimension.

```python
arr = np.arange(12)

new_arr = arr.reshape(3, -1)

print(new_arr)
```

Output:

```text
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

---

# `flatten()`

Converts to 1D and returns a copy.

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

flat = arr.flatten()

print(flat)
```

Output:

```text
[1 2 3 4]
```

---

# `ravel()`

Returns a flattened array, often as a view when possible.

```python
flat = arr.ravel()

print(flat)
```

---

# `flatten()` vs `ravel()`

```text
flatten()
→ always returns a copy

ravel()
→ returns a flattened view when possible
```

The distinction between copies and views is important for both memory usage and accidental modification of source data.

---

# 🔄 Transpose

Transpose changes rows into columns.

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.T)
```

Output:

```text
[[1 4]
 [2 5]
 [3 6]]
```

Also:

```python
print(np.transpose(arr))
```

---

# 🔀 `swapaxes()`

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

print(np.swapaxes(arr, 0, 1))
```

---

# ➕ `expand_dims()`

Adds a dimension.

```python
arr = np.array([1, 2, 3])

new_arr = np.expand_dims(arr, axis=0)

print(new_arr)
print(new_arr.shape)
```

---

# ➖ `squeeze()`

Removes dimensions of size `1`.

```python
arr = np.array([[1, 2, 3]])

print(arr.shape)

result = np.squeeze(arr)

print(result.shape)
```

---

# 🔗 Concatenation

Combines arrays.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.concatenate((a, b))

print(result)
```

Output:

```text
[1 2 3 4 5 6]
```

---

# 🧱 Vertical Stack

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.vstack((a, b)))
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

---

# ↔️ Horizontal Stack

```python
print(np.hstack((a, b)))
```

---

# 📚 Stack

`stack()` adds a new axis.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.stack((a, b))

print(result)
```

---

# ✂️ Splitting Arrays

## `np.split()`

```python
arr = np.array([1, 2, 3, 4, 5, 6])

result = np.split(arr, 3)

print(result)
```

---

# `np.array_split()`

Unlike `split()`, `array_split()` can split into unequal-sized pieces when necessary.

```python
arr = np.array([1, 2, 3, 4, 5])

result = np.array_split(arr, 2)

print(result)
```

---

# 🔁 Repeat

```python
arr = np.array([1, 2, 3])

print(np.repeat(arr, 2))
```

Output:

```text
[1 1 2 2 3 3]
```

---

# 🧩 Tile

Repeats an entire pattern.

```python
arr = np.array([1, 2, 3])

print(np.tile(arr, 2))
```

Output:

```text
[1 2 3 1 2 3]
```

---

# 🔃 Sorting

```python
arr = np.array([40, 10, 30, 20])

print(np.sort(arr))
```

Output:

```text
[10 20 30 40]
```

---

# 🔎 `argsort()`

Returns indices that would sort the array.

```python
arr = np.array([40, 10, 30, 20])

indices = np.argsort(arr)

print(indices)
```

Output:

```text
[1 3 2 0]
```

This is extremely useful when you need the **ranking/order of observations**.

---

# 🔍 Search Functions

Important:

```text
np.where()
np.argmax()
np.argmin()
np.searchsorted()
```

---

# `np.where()`

Find positions satisfying a condition.

```python
arr = np.array([10, 20, 30, 40])

print(np.where(arr > 20))
```

---

# `np.argmax()`

Index of maximum value.

```python
arr = np.array([10, 50, 30])

print(np.argmax(arr))
```

Output:

```text
1
```

---

# `np.argmin()`

```python
print(np.argmin(arr))
```

Output:

```text
0
```

---

# 🔢 `np.unique()`

Returns unique values.

```python
arr = np.array([1, 2, 2, 3, 3, 3])

print(np.unique(arr))
```

Output:

```text
[1 2 3]
```

---

# 📊 Unique Values with Counts

```python
values, counts = np.unique(
    arr,
    return_counts=True
)

print(values)
print(counts)
```

This is useful for categorical frequency calculations when the categories are represented in an appropriate NumPy dtype.

---

# 🧮 Set Operations

NumPy provides:

```text
np.unique()
np.intersect1d()
np.union1d()
np.setdiff1d()
np.setxor1d()
```

---

# Intersection

```python
a = np.array([1, 2, 3, 4])
b = np.array([3, 4, 5, 6])

print(np.intersect1d(a, b))
```

Output:

```text
[3 4]
```

---

# Union

```python
print(np.union1d(a, b))
```

---

# Difference

```python
print(np.setdiff1d(a, b))
```

---

# 🔄 Copy vs View

This is extremely important.

## View

A view shares the underlying data.

```python
arr = np.array([1, 2, 3, 4])

view = arr[1:3]

view[0] = 100

print(arr)
```

The original array may change because the slice is a view.

Basic slicing generally produces views.

---

# Copy

```python
arr = np.array([1, 2, 3, 4])

copy_arr = arr.copy()

copy_arr[0] = 100

print(arr)
print(copy_arr)
```

Original remains unchanged.

---

# 🌧️ NaN

`NaN` means:

```text
Not a Number
```

Example:

```python
arr = np.array([10, 20, np.nan, 40])

print(arr)
```

---

# Check NaN

```python
print(np.isnan(arr))
```

---

# Sum with NaN

Normal:

```python
print(np.sum(arr))
```

may produce `nan`.

Use:

```python
print(np.nansum(arr))
```

---

# NaN Statistical Functions

Useful:

```text
np.nanmean()
np.nanmedian()
np.nanstd()
np.nanvar()
np.nanmin()
np.nanmax()
np.nansum()
```

Example:

```python
arr = np.array([10, 20, np.nan, 40])

print(np.nanmean(arr))
```

---

# ♾️ Infinity

```python
arr = np.array([
    10,
    np.inf,
    -np.inf
])

print(arr)
```

Check:

```python
print(np.isinf(arr))
```

---

# 🔢 Random Module

Modern NumPy code should generally use the newer random generator API:

```python
rng = np.random.default_rng()
```

instead of relying on the older global random-state style.

---

# 🎲 Random Number

```python
rng = np.random.default_rng()

print(rng.random())
```

---

# Random Array

```python
rng = np.random.default_rng()

arr = rng.random(5)

print(arr)
```

---

# Random Integers

```python
rng = np.random.default_rng()

arr = rng.integers(1, 10, size=5)

print(arr)
```

---

# Random Normal Distribution

```python
rng = np.random.default_rng()

arr = rng.normal(
    loc=50,
    scale=10,
    size=5
)

print(arr)
```

---

# Random Choice

```python
rng = np.random.default_rng()

arr = rng.choice(
    [10, 20, 30, 40],
    size=3
)

print(arr)
```

---

# Reproducible Random Numbers

Use a seed:

```python
rng = np.random.default_rng(42)

print(rng.random(5))
```

Running the same generator setup with the same seed gives reproducible results.

---

# 🎯 Random Sampling

Random sampling is useful for:

* Testing
* Simulation
* Sampling
* Machine learning experiments
* Monte Carlo methods

Example:

```python
rng = np.random.default_rng(42)

data = np.arange(100)

sample = rng.choice(
    data,
    size=10,
    replace=False
)

print(sample)
```

---

# 📊 Statistics

Important functions:

```text
np.mean()
np.median()
np.std()
np.var()
np.min()
np.max()
np.percentile()
np.quantile()
np.average()
np.cov()
np.corrcoef()
```

---

# Mean

```python
data = np.array([10, 20, 30, 40, 50])

print(np.mean(data))
```

---

# Median

```python
print(np.median(data))
```

---

# Standard Deviation

```python
print(np.std(data))
```

---

# Variance

```python
print(np.var(data))
```

---

# Weighted Average

```python
values = np.array([10, 20, 30])

weights = np.array([1, 2, 3])

print(np.average(values, weights=weights))
```

---

# 📈 Percentile

Percentiles are extremely useful in Data Analytics.

```python
data = np.array([10, 20, 30, 40, 50])

print(np.percentile(data, 50))
```

The 50th percentile corresponds to the median for this simple example.

---

# Quartiles

```python
q1 = np.percentile(data, 25)
q2 = np.percentile(data, 50)
q3 = np.percentile(data, 75)

print(q1)
print(q2)
print(q3)
```

---

# 📦 IQR

Interquartile Range:

```text
IQR = Q3 - Q1
```

```python
q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)

iqr = q3 - q1

print(iqr)
```

Useful for outlier analysis.

---

# 📊 Covariance

Covariance describes how two variables vary together.

```python
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 6, 8, 10])

print(np.cov(x, y))
```

---

# 🔗 Correlation

```python
print(np.corrcoef(x, y))
```

Correlation is generally between:

```text
-1 and +1
```

Rough interpretation:

```text
+1 → strong positive linear relationship
 0 → no linear correlation
-1 → strong negative linear relationship
```

Correlation does **not** by itself establish causation.

---

# 🧮 Linear Algebra

NumPy provides the `linalg` module.

```python
import numpy as np
```

Common functions:

```text
np.linalg.det()
np.linalg.inv()
np.linalg.solve()
np.linalg.eig()
np.linalg.norm()
np.linalg.matrix_rank()
np.linalg.svd()
```

---

# ✖️ Dot Product

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.dot(a, b))
```

Calculation:

```text
1×4 + 2×5 + 3×6
= 4 + 10 + 18
= 32
```

---

# Matrix Multiplication

Use:

```python
A @ B
```

Example:

```python
A = np.array([
    [1, 2],
    [3, 4]
])

B = np.array([
    [5, 6],
    [7, 8]
])

print(A @ B)
```

---

# `np.matmul()`

```python
print(np.matmul(A, B))
```

---

# `np.dot()` vs `@`

For 2D matrices, both can perform matrix multiplication in common cases.

```python
A @ B
```

is generally the clearest modern notation for matrix multiplication.

---

# 🔢 Matrix Determinant

```python
A = np.array([
    [1, 2],
    [3, 4]
])

print(np.linalg.det(A))
```

---

# 🔄 Matrix Inverse

```python
print(np.linalg.inv(A))
```

Only invertible matrices have an inverse.

---

# 🧮 Solve Linear Equations

Given:

```text
2x + y = 5
x + 3y = 6
```

Represent:

```python
A = np.array([
    [2, 1],
    [1, 3]
])

b = np.array([5, 6])

solution = np.linalg.solve(A, b)

print(solution)
```

---

# 📐 Eigenvalues and Eigenvectors

```python
A = np.array([
    [2, 0],
    [0, 3]
])

values, vectors = np.linalg.eig(A)

print(values)
print(vectors)
```

---

# 📏 Matrix Norm

```python
A = np.array([
    [3, 4]
])

print(np.linalg.norm(A))
```

---

# 🔢 Matrix Rank

```python
A = np.array([
    [1, 2],
    [2, 4]
])

print(np.linalg.matrix_rank(A))
```

---

# 📉 SVD

Singular Value Decomposition:

```python
A = np.array([
    [1, 2],
    [3, 4]
])

U, S, Vt = np.linalg.svd(A)

print(U)
print(S)
print(Vt)
```

SVD is used in areas such as:

* Dimensionality reduction
* Matrix approximation
* Signal processing
* Recommendation systems
* Numerical linear algebra

---

# 📐 Polynomial Operations

NumPy provides polynomial functionality.

For example:

```text
y = x² + 2x + 1
```

Coefficients:

```python
coefficients = [1, 2, 1]
```

Modern NumPy also provides the `numpy.polynomial` package for polynomial operations.

---

# 🔢 Evaluate Polynomial

```python
from numpy.polynomial import Polynomial

p = Polynomial([1, 2, 1])

print(p(2))
```

---

# ➕ Polynomial Addition

```python
p1 = Polynomial([1, 2])
p2 = Polynomial([3, 4])

print(p1 + p2)
```

---

# 📂 NumPy File Handling

NumPy can save and load arrays.

Common functions:

```text
np.save()
np.load()
np.savez()
np.savetxt()
np.loadtxt()
np.genfromtxt()
```

---

# 💾 Save `.npy`

```python
arr = np.array([10, 20, 30])

np.save("data.npy", arr)
```

---

# 📥 Load `.npy`

```python
arr = np.load("data.npy")

print(arr)
```

---

# 💾 Save Text

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

np.savetxt(
    "data.txt",
    arr
)
```

---

# 📥 Load Text

```python
arr = np.loadtxt("data.txt")

print(arr)
```

---

# 📄 CSV

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

np.savetxt(
    "data.csv",
    arr,
    delimiter=","
)
```

Load:

```python
arr = np.loadtxt(
    "data.csv",
    delimiter=","
)

print(arr)
```

For real-world CSV files with headers, missing values, mixed data types, and richer tabular operations, **Pandas is usually the better tool**.

---

# ⚡ Vectorization

Vectorization means performing operations on complete arrays rather than writing explicit Python loops.

Without vectorization:

```python
numbers = [1, 2, 3, 4]

result = []

for x in numbers:
    result.append(x * 2)

print(result)
```

With NumPy:

```python
import numpy as np

numbers = np.array([1, 2, 3, 4])

result = numbers * 2

print(result)
```

---

# 🚀 Why Vectorization Matters

Vectorized NumPy operations can be much faster for numerical workloads because NumPy can execute operations efficiently in compiled code.

Instead of:

```text
Python loop
 ↓
one element
 ↓
Python loop
 ↓
one element
```

NumPy can perform:

```text
Array
 ↓
optimized numerical operation
 ↓
Array
```

---

# 📊 NumPy for Data Cleaning

Suppose:

```python
data = np.array([
    10,
    20,
    np.nan,
    40,
    50
])
```

Find missing values:

```python
print(np.isnan(data))
```

Count missing values:

```python
print(np.sum(np.isnan(data)))
```

---

# 📊 Data Filtering

```python
data = np.array([
    10, 20, 30, 40, 50
])

filtered = data[data >= 30]

print(filtered)
```

Output:

```text
[30 40 50]
```

---

# 🚨 Outlier Detection

Using IQR:

```python
data = np.array([
    10, 12, 11, 13, 12, 100
])

q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)

iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outliers = data[
    (data < lower) |
    (data > upper)
]

print(outliers)
```

---

# 📏 Min-Max Normalization

Formula:

```text
x' = (x - min) / (max - min)
```

NumPy:

```python
data = np.array([10, 20, 30, 40, 50])

normalized = (
    data - np.min(data)
) / (
    np.max(data) - np.min(data)
)

print(normalized)
```

Output:

```text
[0.   0.25 0.5  0.75 1.  ]
```

---

# 📊 Standardization

Formula:

```text
z = (x - mean) / standard_deviation
```

Code:

```python
data = np.array([10, 20, 30, 40, 50])

standardized = (
    data - np.mean(data)
) / np.std(data)

print(standardized)
```

---

# 📈 Data Transformation

Suppose you need to increase all prices by 10%.

```python
prices = np.array([
    100,
    200,
    300,
    400
])

new_prices = prices * 1.10

print(new_prices)
```

---

# 💰 Revenue Calculation

Suppose:

```python
quantity = np.array([10, 20, 15, 30])
price = np.array([100, 200, 150, 80])
```

Revenue:

```python
revenue = quantity * price

print(revenue)
```

Total revenue:

```python
total_revenue = np.sum(revenue)

print(total_revenue)
```

---

# 📊 Sales Analytics

```python
sales = np.array([
    12000,
    15000,
    18000,
    11000,
    22000,
    25000
])

print("Total:", np.sum(sales))
print("Average:", np.mean(sales))
print("Minimum:", np.min(sales))
print("Maximum:", np.max(sales))
print("Std:", np.std(sales))
```

---

# 🏆 Find Best Sales Day

```python
sales = np.array([
    12000,
    15000,
    18000,
    11000,
    22000,
    25000
])

index = np.argmax(sales)

print("Index:", index)
print("Sales:", sales[index])
```

---

# 📅 Monthly Sales

Suppose each row represents a year and each column a month:

```python
sales = np.array([
    [100, 120, 130, 140],
    [110, 130, 150, 160],
    [120, 140, 160, 170]
])
```

Year-wise total:

```python
print(np.sum(sales, axis=1))
```

Month-wise total:

```python
print(np.sum(sales, axis=0))
```

---

# 📊 NumPy + Pandas

NumPy and Pandas are closely connected.

Typical workflow:

```text
CSV / Excel / Database
        ↓
      Pandas
        ↓
   DataFrame
        ↓
     NumPy
        ↓
Numerical calculations
        ↓
     Results
```

Example:

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "sales": [100, 200, 300, 400]
})

sales = df["sales"].to_numpy()

print(np.mean(sales))
```

Pandas is generally preferred for labeled/tabular data, while NumPy is excellent for underlying numerical arrays.

---

# 📊 NumPy + Matplotlib

NumPy can generate numerical data for visualization.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)

y = x ** 2

plt.plot(x, y)

plt.xlabel("X")
plt.ylabel("Y")

plt.show()
```

---

# 🤖 NumPy + Machine Learning

Machine learning data is often represented numerically as:

```text
Rows → Observations
Columns → Features
```

Example:

```python
X = np.array([
    [20, 50000],
    [25, 60000],
    [30, 70000],
    [35, 80000]
])

y = np.array([
    0,
    0,
    1,
    1
])
```

Here:

```text
X → Features
y → Target
```

NumPy is fundamental to the numerical ecosystem used by many scientific and machine-learning Python packages.

---

# 🧠 Universal Functions — ufuncs

A **ufunc** is a function that operates element-by-element on arrays.

Examples:

```python
np.add()
np.subtract()
np.multiply()
np.divide()

np.sqrt()
np.exp()
np.log()

np.sin()
np.cos()
```

Example:

```python
arr = np.array([1, 4, 9])

print(np.sqrt(arr))
```

Output:

```text
[1. 2. 3.]
```

---

# ➕ `np.add()`

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.add(a, b))
```

---

# ➖ `np.subtract()`

```python
print(np.subtract(a, b))
```

---

# ✖️ `np.multiply()`

```python
print(np.multiply(a, b))
```

---

# ➗ `np.divide()`

```python
print(np.divide(a, b))
```

---

# 🧠 Conditional Selection — `np.where()`

Very useful in analytics.

```python
marks = np.array([
    35, 80, 45, 90
])

result = np.where(
    marks >= 40,
    "Pass",
    "Fail"
)

print(result)
```

Output:

```text
['Fail' 'Pass' 'Pass' 'Pass']
```

---

# 🔀 `np.select()`

Useful for multiple conditions.

```python
marks = np.array([30, 55, 75, 90])

conditions = [
    marks < 40,
    marks < 60,
    marks < 80,
    marks >= 80
]

choices = [
    "Fail",
    "Average",
    "Good",
    "Excellent"
]

result = np.select(
    conditions,
    choices,
    default="Unknown"
)

print(result)
```

---

# 🔍 `np.clip()`

Restricts values to a range.

```python
arr = np.array([
    10,
    20,
    30,
    40,
    50
])

result = np.clip(arr, 20, 40)

print(result)
```

Output:

```text
[20 20 30 40 40]
```

Useful for:

* Bounding values
* Data preprocessing
* Outlier handling
* Image processing

---

# 🔢 Counting

```python
arr = np.array([1, 2, 2, 3, 3, 3])

print(np.count_nonzero(arr == 3))
```

Output:

```text
3
```

---

# 🔎 `np.any()`

Checks whether at least one condition is true.

```python
arr = np.array([10, 20, 30])

print(np.any(arr > 25))
```

Output:

```text
True
```

---

# 🔎 `np.all()`

Checks whether all conditions are true.

```python
print(np.all(arr > 5))
```

Output:

```text
True
```

---

# 🔢 Cumulative Functions

Important:

```text
np.cumsum()
np.cumprod()
```

---

# Cumulative Sum

```python
arr = np.array([10, 20, 30, 40])

print(np.cumsum(arr))
```

Output:

```text
[ 10  30  60 100]
```

Useful for:

* Running totals
* Cumulative sales
* Financial analysis

---

# Cumulative Product

```python
arr = np.array([1, 2, 3, 4])

print(np.cumprod(arr))
```

---

# 📊 Difference

```python
arr = np.array([10, 15, 25, 30])

print(np.diff(arr))
```

Output:

```text
[ 5 10  5]
```

Useful for:

* Change between observations
* Time-series preprocessing
* Growth calculations

---

# 🔄 Gradient

```python
arr = np.array([10, 20, 40, 80])

print(np.gradient(arr))
```

Useful for numerical rate-of-change approximations.

---

# 🧮 GCD and LCM

```python
a = np.array([12, 18, 24])
b = np.array([8, 12, 16])

print(np.gcd(a, b))
print(np.lcm(a, b))
```

---

# 🔢 Bitwise Operations

NumPy supports:

```text
np.bitwise_and()
np.bitwise_or()
np.bitwise_xor()
np.bitwise_not()
np.left_shift()
np.right_shift()
```

Example:

```python
a = np.array([5])
b = np.array([3])

print(np.bitwise_and(a, b))
```

These are mainly useful for integer/bit-level operations rather than everyday analytics.

---

# 🔤 String Operations

NumPy also has string-related functionality, although for general text processing Python strings or Pandas string operations are usually more convenient.

The NumPy reference includes string functionality among its routine categories.

---

# 🕒 Date and Time

NumPy provides:

```text
datetime64
timedelta64
```

Example:

```python
dates = np.array([
    "2026-01-01",
    "2026-01-02",
    "2026-01-03"
], dtype="datetime64")

print(dates)
```

---

# ➕ Date Difference

```python
start = np.datetime64("2026-01-01")
end = np.datetime64("2026-01-10")

print(end - start)
```

---

# 🪟 Window Functions

Modern NumPy includes window-function support for numerical operations involving neighborhoods/windows.

For ordinary analytics, Pandas rolling operations are often more convenient for labeled time series.

---

# 🧩 Structured Arrays

NumPy can store structured records with named fields.

```python
data = np.array([
    ("Rahul", 20),
    ("Anita", 22)
], dtype=[
    ("name", "U20"),
    ("age", "i4")
])

print(data["name"])
print(data["age"])
```

Structured arrays are useful for certain lower-level numerical/data tasks, although Pandas is usually preferable for business-style tabular analytics.

---

# 🧮 Masked Arrays

NumPy also provides masked arrays for situations where some values should be excluded from computations.

```python
import numpy as np

data = np.ma.array(
    [10, 20, 30, 40],
    mask=[False, True, False, False]
)

print(data)
```

---

# 📐 Shape Rules

Remember:

```text
1D:
(n,)

2D:
(rows, columns)

3D:
(depth, rows, columns)
```

Example:

```python
arr = np.zeros((2, 3, 4))

print(arr.shape)
```

Output:

```text
(2, 3, 4)
```

Total elements:

```text
2 × 3 × 4 = 24
```

---

# 🧠 Important Array Concepts

You should understand:

```text
ndarray
shape
ndim
size
dtype
axis
indexing
slicing
broadcasting
view
copy
vectorization
```

These are more important for analytics than memorizing hundreds of function names.

---

# ⚡ Performance Tips

## Prefer vectorization

Good:

```python
result = arr * 2
```

Instead of:

```python
result = []

for x in arr:
    result.append(x * 2)
```

---

## Avoid unnecessary copies

```python
copy = arr.copy()
```

creates additional memory.

Understand when you need a true copy versus a view.

---

## Use appropriate dtypes

For large datasets, choosing an appropriate dtype can reduce memory usage.

```python
arr = np.array(
    [1, 2, 3],
    dtype=np.int32
)
```

---

## Be careful with broadcasting

Broadcasting is powerful, but inappropriate large broadcasts can create large intermediate arrays.

---

# 🆚 NumPy vs Pandas

| NumPy                     | Pandas                                |
| ------------------------- | ------------------------------------- |
| Numerical arrays          | Tabular/labeled data                  |
| `ndarray`                 | `DataFrame`, `Series`                 |
| Fast numerical operations | Data manipulation                     |
| Matrix operations         | CSV/Excel/database-oriented workflows |
| Mathematical functions    | Grouping, merging, joining            |
| Linear algebra            | Missing-data handling                 |
| Scientific computing      | Business analytics                    |

In real Data Analytics:

```text
Pandas + NumPy
```

are often used together.

---

# 🧠 When Should You Use NumPy?

Use NumPy when you need:

### Numerical calculations

```python
np.mean(data)
```

### Matrix calculations

```python
A @ B
```

### Fast array operations

```python
data * 2
```

### Statistical calculations

```python
np.std(data)
```

### Random sampling

```python
rng.choice(...)
```

### Numerical preprocessing

```python
(data - mean) / std
```

### Scientific calculations

```python
np.sqrt()
np.exp()
np.log()
```

---

# ❌ When Not to Use NumPy Alone

Don't force NumPy to handle everything.

For:

```text
CSV reading
Excel
SQL-like operations
groupby
merge
join
labeled columns
missing-value workflows
complex tabular data
```

Pandas is usually more appropriate.

For:

```text
Deep learning
```

use frameworks such as:

```text
PyTorch
TensorFlow
```

For:

```text
Advanced scientific algorithms
```

consider:

```text
SciPy
```

---

# 📊 Complete Data Analytics Example

Suppose we have student marks:

```python
import numpy as np

marks = np.array([
    45,
    67,
    89,
    34,
    76,
    92,
    55,
    40,
    88,
    73
])
```

---

## Total

```python
total = np.sum(marks)

print("Total:", total)
```

---

## Average

```python
average = np.mean(marks)

print("Average:", average)
```

---

## Highest

```python
highest = np.max(marks)

print("Highest:", highest)
```

---

## Lowest

```python
lowest = np.min(marks)

print("Lowest:", lowest)
```

---

## Standard Deviation

```python
std = np.std(marks)

print("Standard Deviation:", std)
```

---

## Median

```python
median = np.median(marks)

print("Median:", median)
```

---

## Pass Students

```python
passed = marks[marks >= 40]

print("Passed:", passed)
```

---

## Failed Students

```python
failed = marks[marks < 40]

print("Failed:", failed)
```

---

## Number of Passed Students

```python
pass_count = np.sum(marks >= 40)

print("Passed Students:", pass_count)
```

---

## Number of Failed Students

```python
fail_count = np.sum(marks < 40)

print("Failed Students:", fail_count)
```

---

## Pass Percentage

```python
pass_percentage = (
    np.sum(marks >= 40) / marks.size
) * 100

print("Pass Percentage:", pass_percentage)
```

---

## Top Students

```python
top_students = marks[marks >= 80]

print(top_students)
```

---

## Ranking

```python
ranking = np.argsort(marks)[::-1]

print(ranking)
```

---

# 📈 Complete Sales Analytics Example

```python
import numpy as np

sales = np.array([
    12000,
    15000,
    18000,
    11000,
    22000,
    25000,
    19000,
    21000,
    17000,
    23000
])

print("Total Sales:", np.sum(sales))
print("Average Sales:", np.mean(sales))
print("Minimum Sales:", np.min(sales))
print("Maximum Sales:", np.max(sales))
print("Median Sales:", np.median(sales))
print("Std Dev:", np.std(sales))
```

---

# 🏆 Best Sales Day

```python
best_index = np.argmax(sales)

print("Best Day Index:", best_index)
print("Best Sales:", sales[best_index])
```

---

# 📉 Worst Sales Day

```python
worst_index = np.argmin(sales)

print("Worst Day Index:", worst_index)
print("Worst Sales:", sales[worst_index])
```

---

# 📊 Above-Average Sales

```python
average = np.mean(sales)

above_average = sales[sales > average]

print(above_average)
```

---

# 📈 Cumulative Sales

```python
cumulative_sales = np.cumsum(sales)

print(cumulative_sales)
```

---

# 💰 Add 10% Growth

```python
future_sales = sales * 1.10

print(future_sales)
```

---

# 📊 Normalize Sales

```python
normalized = (
    sales - np.min(sales)
) / (
    np.max(sales) - np.min(sales)
)

print(normalized)
```

---

# 🧠 Important NumPy Functions Cheat Sheet

## Array Creation

```text
np.array()
np.zeros()
np.ones()
np.empty()
np.full()
np.arange()
np.linspace()
np.eye()
np.identity()
np.diag()
```

---

## Inspection

```text
arr.ndim
arr.shape
arr.size
arr.dtype
arr.itemsize
arr.nbytes
```

---

## Indexing

```text
arr[index]
arr[start:stop]
arr[start:stop:step]
arr[row, column]
arr[condition]
```

---

## Shape

```text
np.reshape()
np.ravel()
np.flatten()
np.transpose()
arr.T
np.swapaxes()
np.moveaxis()
np.expand_dims()
np.squeeze()
```

---

## Combining

```text
np.concatenate()
np.stack()
np.vstack()
np.hstack()
np.column_stack()
np.row_stack()
```

---

## Splitting

```text
np.split()
np.array_split()
np.hsplit()
np.vsplit()
```

---

## Arithmetic

```text
np.add()
np.subtract()
np.multiply()
np.divide()
np.floor_divide()
np.mod()
np.power()
```

---

## Mathematical

```text
np.abs()
np.sqrt()
np.square()
np.exp()
np.log()
np.log10()
np.log2()
np.sign()
```

---

## Trigonometry

```text
np.sin()
np.cos()
np.tan()
np.arcsin()
np.arccos()
np.arctan()
np.deg2rad()
np.rad2deg()
```

---

## Statistics

```text
np.mean()
np.median()
np.std()
np.var()
np.min()
np.max()
np.sum()
np.prod()
np.ptp()
np.average()
np.percentile()
np.quantile()
```

---

## NaN

```text
np.isnan()
np.nanmean()
np.nanmedian()
np.nanstd()
np.nanvar()
np.nanmin()
np.nanmax()
np.nansum()
```

---

## Searching

```text
np.where()
np.argmax()
np.argmin()
np.searchsorted()
```

---

## Sorting

```text
np.sort()
np.argsort()
```

---

## Unique / Sets

```text
np.unique()
np.intersect1d()
np.union1d()
np.setdiff1d()
np.setxor1d()
```

---

## Logic

```text
np.logical_and()
np.logical_or()
np.logical_not()
np.logical_xor()
np.any()
np.all()
```

---

## Conditional

```text
np.where()
np.select()
np.choose()
np.clip()
```

---

## Cumulative

```text
np.cumsum()
np.cumprod()
np.diff()
np.gradient()
```

---

## Random

Prefer the modern generator API:

```text
np.random.default_rng()
```

Common generator methods:

```text
rng.random()
rng.integers()
rng.normal()
rng.uniform()
rng.choice()
rng.permutation()
rng.shuffle()
```

---

## Linear Algebra

```text
np.dot()
np.matmul()
np.linalg.det()
np.linalg.inv()
np.linalg.solve()
np.linalg.eig()
np.linalg.norm()
np.linalg.matrix_rank()
np.linalg.svd()
```

---

## File I/O

```text
np.save()
np.load()
np.savez()
np.savetxt()
np.loadtxt()
np.genfromtxt()
```

---

# 🎯 Most Important Functions for Data Analytics

If your goal is **Data Analytics**, prioritize these first:

```text
1. np.array()
2. np.arange()
3. np.linspace()
4. np.zeros()
5. np.ones()

6. arr.shape
7. arr.ndim
8. arr.size
9. arr.dtype

10. Indexing
11. Slicing
12. Boolean indexing
13. Fancy indexing

14. np.reshape()
15. np.flatten()
16. np.ravel()
17. np.concatenate()
18. np.vstack()
19. np.hstack()

20. np.sum()
21. np.mean()
22. np.median()
23. np.std()
24. np.var()
25. np.min()
26. np.max()
27. np.percentile()

28. np.unique()
29. np.where()
30. np.argmax()
31. np.argmin()

32. np.isnan()
33. np.nanmean()
34. np.nansum()

35. np.sort()
36. np.argsort()

37. np.cumsum()
38. np.diff()

39. Broadcasting
40. Vectorization

41. np.corrcoef()
42. np.cov()

43. np.random.default_rng()
44. rng.choice()
45. rng.integers()

46. np.linalg.solve()
47. np.linalg.inv()
48. np.linalg.det()
49. np.dot()
50. @
```

---

# 🧠 NumPy Concepts You MUST Understand

Don't only memorize functions.

You should understand these concepts deeply:

```text
                  NumPy
                    │
        ┌───────────┴───────────┐
        │                       │
      ndarray                 dtype
        │
   ┌────┼────┬─────┐
   │    │    │     │
 shape ndim size  axis
   │
   ├── Indexing
   ├── Slicing
   ├── Boolean Indexing
   ├── Fancy Indexing
   ├── Broadcasting
   ├── Vectorization
   ├── Views
   └── Copies
```

---

# 📝 NumPy Interview Questions

## 1. What is NumPy?

NumPy is a Python library for numerical computing that provides multidimensional arrays and efficient numerical operations.

---

## 2. What is ndarray?

`ndarray` is NumPy's N-dimensional homogeneous array data structure.

---

## 3. Why is NumPy faster than Python lists for numerical operations?

NumPy uses compact homogeneous arrays and performs many operations through optimized compiled numerical code, reducing Python-level looping overhead.

---

## 4. What is vectorization?

Performing operations on whole arrays instead of explicitly looping over individual elements in Python.

---

## 5. What is broadcasting?

Broadcasting is NumPy's mechanism for performing operations on arrays with compatible but different shapes.

---

## 6. What is `shape`?

It describes the size of an array along each dimension.

```python
arr.shape
```

---

## 7. What is `ndim`?

Number of dimensions.

```python
arr.ndim
```

---

## 8. What is `size`?

Total number of elements.

```python
arr.size
```

---

## 9. What is `dtype`?

The data type used by array elements.

```python
arr.dtype
```

---

## 10. Difference between `arange()` and `linspace()`?

```text
arange()
→ step-based

linspace()
→ number-of-values-based
```

---

## 11. Difference between `flatten()` and `ravel()`?

```text
flatten()
→ copy

ravel()
→ view when possible
```

---

## 12. Difference between view and copy?

```text
View
→ shares underlying data

Copy
→ independent data
```

---

## 13. What is axis?

Axis identifies the dimension along which an operation is performed.

---

## 14. What does `axis=0` mean?

For a 2D array, an aggregation over `axis=0` reduces the row dimension and produces one result per column.

---

## 15. What does `axis=1` mean?

For a 2D array, an aggregation over `axis=1` reduces the column dimension and produces one result per row.

---

## 16. How do you find missing values?

```python
np.isnan(arr)
```

---

## 17. How do you calculate average ignoring NaN?

```python
np.nanmean(arr)
```

---

## 18. How do you find maximum index?

```python
np.argmax(arr)
```

---

## 19. How do you filter an array?

```python
arr[arr > 50]
```

---

## 20. How do you sort an array?

```python
np.sort(arr)
```

---

## 21. How do you get sorting indices?

```python
np.argsort(arr)
```

---

## 22. How do you find unique values?

```python
np.unique(arr)
```

---

## 23. How do you calculate correlation?

```python
np.corrcoef(x, y)
```

---

## 24. How do you multiply matrices?

```python
A @ B
```

---

## 25. What is NumPy's role in Data Analytics?

NumPy provides efficient numerical operations used for:

* Data transformation
* Statistical calculations
* Filtering
* Aggregation
* Normalization
* Standardization
* Outlier calculations
* Matrix operations
* Numerical preprocessing
* Sampling

---

# 🧪 Practice Programs

## Beginner

1. Create a NumPy array.
2. Create a 2D array.
3. Find its shape.
4. Find its dimensions.
5. Find its size.
6. Find its dtype.
7. Convert integer array to float.
8. Create zeros.
9. Create ones.
10. Create an identity matrix.

---

## Intermediate

11. Perform array arithmetic.
12. Filter values greater than 50.
13. Find minimum and maximum.
14. Find average.
15. Find median.
16. Find standard deviation.
17. Find variance.
18. Find unique values.
19. Find duplicate counts.
20. Sort an array.
21. Find maximum index.
22. Find minimum index.
23. Reshape an array.
24. Flatten an array.
25. Concatenate arrays.
26. Split an array.
27. Transpose a matrix.
28. Use broadcasting.
29. Find NaN values.
30. Calculate cumulative sum.

---

## Data Analytics Practice

31. Calculate student pass percentage.
32. Calculate average salary.
33. Find highest salary.
34. Find lowest salary.
35. Find employees earning above average.
36. Normalize a dataset.
37. Standardize a dataset.
38. Detect outliers using IQR.
39. Calculate correlation.
40. Calculate covariance.
41. Calculate monthly sales.
42. Find best-selling month.
43. Find worst-selling month.
44. Calculate cumulative revenue.
45. Calculate percentage growth.
46. Randomly sample records.
47. Generate simulated sales data.
48. Calculate quartiles.
49. Calculate percentile values.
50. Perform matrix calculations.

---

# 🏆 Complete Data Analytics Workflow Using NumPy

```text
                  RAW DATA
                     │
                     ↓
             Load / Receive Data
                     │
                     ↓
               NumPy Array
                     │
             ┌───────┴───────┐
             ↓               ↓
         Inspect          Clean
             │               │
     shape / dtype      NaN / filtering
             │               │
             └───────┬───────┘
                     ↓
                Transform
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
      Normalize   Reshape    Filter
          │          │          │
          └──────────┼──────────┘
                     ↓
                 Analyze
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
      Mean         Median        Std
        ↓            ↓            ↓
        └────────────┼────────────┘
                     ↓
                Find Insights
                     │
                     ↓
               Visualization
                     │
                     ↓
                  Report
```

---

# 🧠 NumPy vs Python List — Remember This

Python list:

```python
numbers = [1, 2, 3, 4]

result = []

for x in numbers:
    result.append(x * 2)
```

NumPy:

```python
numbers = np.array([1, 2, 3, 4])

result = numbers * 2
```

This is the fundamental idea:

```text
Python List
     ↓
General-purpose collection

NumPy Array
     ↓
Numerical computation
     ↓
Vectorization
     ↓
Fast mathematical operations
```

---

# 🚀 NumPy Learning Order

For a Data Analytics learner, study NumPy in this order:

```text
1. Installation
       ↓
2. np.array()
       ↓
3. 1D / 2D arrays
       ↓
4. ndim / shape / size / dtype
       ↓
5. Indexing
       ↓
6. Slicing
       ↓
7. Boolean indexing
       ↓
8. Array arithmetic
       ↓
9. Broadcasting
       ↓
10. Aggregation
       ↓
11. axis
       ↓
12. Mathematical functions
       ↓
13. Reshape
       ↓
14. Transpose
       ↓
15. Concatenation
       ↓
16. Split
       ↓
17. Sorting
       ↓
18. Searching
       ↓
19. Unique
       ↓
20. NaN handling
       ↓
21. Statistics
       ↓
22. Random
       ↓
23. Linear algebra
       ↓
24. Vectorization
       ↓
25. NumPy + Pandas
       ↓
26. Real Data Analytics
```

---

# 🔥 FINAL REVISION CHEAT SHEET

```text
NUMPY
│
├── ndarray
│   ├── 1D
│   ├── 2D
│   ├── 3D
│   └── ND
│
├── Attributes
│   ├── shape
│   ├── ndim
│   ├── size
│   ├── dtype
│   ├── itemsize
│   └── nbytes
│
├── Creation
│   ├── array()
│   ├── zeros()
│   ├── ones()
│   ├── empty()
│   ├── full()
│   ├── arange()
│   ├── linspace()
│   ├── eye()
│   └── diag()
│
├── Indexing
│   ├── Index
│   ├── Slice
│   ├── Boolean
│   └── Fancy
│
├── Operations
│   ├── Arithmetic
│   ├── Comparison
│   ├── Logical
│   └── Broadcasting
│
├── Statistics
│   ├── mean()
│   ├── median()
│   ├── std()
│   ├── var()
│   ├── min()
│   ├── max()
│   ├── percentile()
│   └── quantile()
│
├── Manipulation
│   ├── reshape()
│   ├── flatten()
│   ├── ravel()
│   ├── transpose()
│   ├── concatenate()
│   ├── stack()
│   ├── split()
│   └── squeeze()
│
├── Search
│   ├── where()
│   ├── argmax()
│   ├── argmin()
│   └── searchsorted()
│
├── Sorting
│   ├── sort()
│   └── argsort()
│
├── Sets
│   ├── unique()
│   ├── intersect1d()
│   ├── union1d()
│   └── setdiff1d()
│
├── Missing Data
│   ├── isnan()
│   ├── nanmean()
│   ├── nanmedian()
│   └── nansum()
│
├── Random
│   ├── default_rng()
│   ├── random()
│   ├── integers()
│   ├── normal()
│   └── choice()
│
├── Linear Algebra
│   ├── dot()
│   ├── matmul()
│   ├── det()
│   ├── inv()
│   ├── solve()
│   ├── eig()
│   └── svd()
│
├── I/O
│   ├── save()
│   ├── load()
│   ├── savetxt()
│   ├── loadtxt()
│   └── genfromtxt()
│
└── Data Analytics
    ├── Filtering
    ├── Cleaning
    ├── Transformation
    ├── Normalization
    ├── Standardization
    ├── Statistics
    ├── Outlier Detection
    ├── Correlation
    ├── Sampling
    └── Numerical Modeling
```

---

# 🎯 What You Need to Remember for Data Analytics

If you're learning NumPy specifically for **Data Analytics**, don't try to memorize every API function.

Master these **10 core concepts**:

```text
1. ndarray
2. shape / ndim / size / dtype
3. Indexing and slicing
4. Boolean filtering
5. Vectorization
6. Broadcasting
7. axis
8. Aggregation/statistics
9. NaN handling
10. NumPy + Pandas
```

Once these are strong, the remaining NumPy functions become much easier to learn from the documentation/reference. The official NumPy reference organizes the API into array creation/manipulation, math, logic, indexing, linear algebra, random sampling, statistics, sorting/searching, I/O, FFT, and other categories.

---

# 📌 One-Line Memory Notes

```text
np.array()
→ Create array

shape
→ Dimensions of each axis

ndim
→ Number of dimensions

size
→ Total elements

dtype
→ Data type

reshape()
→ Change shape

flatten()
→ Flatten + copy

ravel()
→ Flatten, view when possible

T
→ Transpose

axis=0
→ Reduce rows / operate down columns

axis=1
→ Reduce columns / operate across rows

Boolean indexing
→ Filter data

where()
→ Conditional selection/positions

unique()
→ Unique values

sort()
→ Sorted values

argsort()
→ Sorting indices

argmax()
→ Index of maximum

argmin()
→ Index of minimum

mean()
→ Average

median()
→ Middle value

std()
→ Standard deviation

var()
→ Variance

percentile()
→ Percentile

isnan()
→ Find NaN

nanmean()
→ Mean ignoring NaN

cumsum()
→ Cumulative sum

diff()
→ Differences

corrcoef()
→ Correlation matrix

cov()
→ Covariance matrix

@ 
→ Matrix multiplication

linalg
→ Linear algebra

default_rng()
→ Modern random generator

broadcasting
→ Compatible different shapes

vectorization
→ Array operations without explicit Python loops

view
→ Shares data

copy
→ Independent data
```

# 🏁 Final Takeaway

NumPy is **not just a library for creating arrays**.

Think of it as the numerical foundation underneath a large part of the Python data-science ecosystem:

```text
                    NUMPY
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
    Arrays       Mathematics     Statistics
       │              │              │
       └──────────────┼──────────────┘
                      ↓
               Data Processing
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
       Pandas      SciPy      Scikit-learn
          │           │           │
          └───────────┼───────────┘
                      ↓
                Data Analytics
                      ↓
             Machine Learning
                      ↓
                Data Science
```

For your **Data Analytics path**, the most important progression is:

```text
Python
  ↓
NumPy
  ↓
Pandas
  ↓
Matplotlib
  ↓
Seaborn
  ↓
SQL
  ↓
Statistics
  ↓
EDA
  ↓
Machine Learning
```
