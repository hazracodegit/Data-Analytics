# 🐍 Python List, Tuple, Set & Dictionary — Complete Revision Notes

> A complete revision guide for Python's four major built-in collection data types: **List, Tuple, Set, and Dictionary**.

---

# 📚 Table of Contents

* [1. Python Collections](#1-python-collections)
* [2. List](#2-list)

  * [Creating Lists](#creating-lists)
  * [List Indexing](#list-indexing)
  * [Negative Indexing](#negative-indexing)
  * [List Slicing](#list-slicing)
  * [Changing List Elements](#changing-list-elements)
  * [Adding Elements](#adding-elements)
  * [Removing Elements](#removing-elements)
  * [Searching Lists](#searching-lists)
  * [Sorting Lists](#sorting-lists)
  * [Copying Lists](#copying-lists)
  * [List Concatenation](#list-concatenation)
  * [List Repetition](#list-repetition)
  * [List Unpacking](#list-unpacking)
  * [Nested Lists](#nested-lists)
  * [List Comprehension](#list-comprehension)
  * [List Methods](#list-methods)
* [3. Tuple](#3-tuple)

  * [Creating Tuples](#creating-tuples)
  * [Tuple Indexing](#tuple-indexing)
  * [Tuple Slicing](#tuple-slicing)
  * [Tuple Operations](#tuple-operations)
  * [Tuple Methods](#tuple-methods)
  * [Tuple Packing](#tuple-packing)
  * [Tuple Unpacking](#tuple-unpacking)
  * [Nested Tuples](#nested-tuples)
* [4. Set](#4-set)

  * [Creating Sets](#creating-sets)
  * [Set Properties](#set-properties)
  * [Adding Elements](#adding-elements)
  * [Removing Elements](#removing-elements)
  * [Set Operations](#set-operations)
  * [Set Comparisons](#set-comparisons)
  * [Set Methods](#set-methods)
  * [Set Comprehension](#set-comprehension)
  * [Frozen Set](#frozen-set)
* [5. Dictionary](#5-dictionary)

  * [Creating Dictionaries](#creating-dictionaries)
  * [Accessing Values](#accessing-values)
  * [Adding and Updating](#adding-and-updating)
  * [Removing Elements](#removing-elements-1)
  * [Dictionary Methods](#dictionary-methods)
  * [Dictionary Iteration](#dictionary-iteration)
  * [Dictionary Comprehension](#dictionary-comprehension)
  * [Nested Dictionaries](#nested-dictionaries)
  * [Dictionary Unpacking](#dictionary-unpacking)
* [6. Collections Comparison](#6-collections-comparison)
* [7. Mutable vs Immutable](#7-mutable-vs-immutable)
* [8. Ordered vs Unordered](#8-ordered-vs-unordered)
* [9. Hashable Objects](#9-hashable-objects)
* [10. Common Programs](#10-common-programs)
* [11. Interview & Exam Questions](#11-interview--exam-questions)
* [12. Complete Cheat Sheet](#12-complete-cheat-sheet)
* [13. Final Revision](#13-final-revision)

---

# 1. Python Collections

Python provides several built-in collection types.

The four most important are:

```text
List
Tuple
Set
Dictionary
```

They are used to store multiple values in a single variable.

---

## Quick Comparison

| Feature    | List               | Tuple            | Set                            | Dictionary     |
| ---------- | ------------------ | ---------------- | ------------------------------ | -------------- |
| Syntax     | `[]`               | `()`             | `{}`                           | `{key: value}` |
| Ordered    | Yes                | Yes              | No meaningful positional order | Yes*           |
| Mutable    | Yes                | No               | Yes                            | Yes            |
| Duplicates | Allowed            | Allowed          | Not allowed                    | Keys: No       |
| Indexing   | Yes                | Yes              | No                             | By key         |
| Slicing    | Yes                | Yes              | No                             | No             |
| Hashable   | No                 | Sometimes        | No                             | No             |
| Main Use   | General collection | Fixed collection | Unique values                  | Key-value data |

> `dict` preserves insertion order in modern Python versions (Python 3.7+ as a language guarantee).

---

# 2. List

A **list** is an ordered and mutable collection that can contain duplicate values.

### Syntax

```python
list_name = [item1, item2, item3]
```

### Example

```python
fruits = ["apple", "banana", "mango"]

print(fruits)
```

### Output

```text
['apple', 'banana', 'mango']
```

---

# Creating Lists

## Empty List

```python
numbers = []

print(numbers)
```

### Output

```text
[]
```

---

## List with Different Data Types

A list can contain different data types.

```python
data = [10, "Python", 3.14, True]

print(data)
```

### Output

```text
[10, 'Python', 3.14, True]
```

---

## List Using `list()`

```python
numbers = list((1, 2, 3))

print(numbers)
```

### Output

```text
[1, 2, 3]
```

---

# List Indexing

Lists use zero-based indexing.

```text
Value:   10   20   30   40   50
Index:    0    1    2    3    4
```

### Code

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[0])
print(numbers[2])
print(numbers[4])
```

### Output

```text
10
30
50
```

---

# Negative Indexing

Negative indexing starts from `-1`.

```text
Value:   10    20    30    40    50
Index:   -5    -4    -3    -2    -1
```

### Code

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[-1])
print(numbers[-2])
```

### Output

```text
50
40
```

---

# List Slicing

### Syntax

```python
list[start:stop:step]
```

### Code

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
```

### Output

```text
[20, 30, 40]
```

---

## Reverse a List

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[::-1])
```

### Output

```text
[50, 40, 30, 20, 10]
```

---

# Changing List Elements

Lists are mutable.

Therefore, individual elements can be changed.

### Code

```python
numbers = [10, 20, 30]

numbers[1] = 200

print(numbers)
```

### Output

```text
[10, 200, 30]
```

---

## Changing Multiple Elements

```python
numbers = [10, 20, 30, 40]

numbers[1:3] = [200, 300]

print(numbers)
```

### Output

```text
[10, 200, 300, 40]
```

---

# Adding Elements

Important methods:

```text
append()
insert()
extend()
```

---

## `append()`

Adds one item to the end.

```python
numbers = [10, 20, 30]

numbers.append(40)

print(numbers)
```

### Output

```text
[10, 20, 30, 40]
```

---

## `insert()`

Adds an element at a specific index.

### Syntax

```python
list.insert(index, value)
```

### Code

```python
numbers = [10, 20, 30]

numbers.insert(1, 15)

print(numbers)
```

### Output

```text
[10, 15, 20, 30]
```

---

## `extend()`

Adds multiple elements to the end.

```python
numbers = [1, 2, 3]

numbers.extend([4, 5, 6])

print(numbers)
```

### Output

```text
[1, 2, 3, 4, 5, 6]
```

---

## `append()` vs `extend()`

### `append()`

Adds the entire object as one element.

```python
numbers = [1, 2]

numbers.append([3, 4])

print(numbers)
```

### Output

```text
[1, 2, [3, 4]]
```

### `extend()`

Adds individual elements from an iterable.

```python
numbers = [1, 2]

numbers.extend([3, 4])

print(numbers)
```

### Output

```text
[1, 2, 3, 4]
```

---

# Removing Elements

Important methods:

```text
remove()
pop()
clear()
del
```

---

## `remove()`

Removes the first matching value.

```python
numbers = [10, 20, 30, 20]

numbers.remove(20)

print(numbers)
```

### Output

```text
[10, 30, 20]
```

If the value doesn't exist, `remove()` raises `ValueError`.

---

## `pop()`

Removes and returns an element.

### Without index

Removes the last element.

```python
numbers = [10, 20, 30]

value = numbers.pop()

print(value)
print(numbers)
```

### Output

```text
30
[10, 20]
```

### With index

```python
numbers = [10, 20, 30]

value = numbers.pop(1)

print(value)
print(numbers)
```

### Output

```text
20
[10, 30]
```

---

## `clear()`

Removes all elements.

```python
numbers = [10, 20, 30]

numbers.clear()

print(numbers)
```

### Output

```text
[]
```

---

## `del`

Deletes an element or slice.

```python
numbers = [10, 20, 30, 40]

del numbers[1]

print(numbers)
```

### Output

```text
[10, 30, 40]
```

Delete a range:

```python
numbers = [10, 20, 30, 40, 50]

del numbers[1:4]

print(numbers)
```

### Output

```text
[10, 50]
```

Delete the entire list:

```python
numbers = [1, 2, 3]

del numbers
```

---

# Searching Lists

## `index()`

Returns the index of the first matching value.

```python
fruits = ["apple", "banana", "mango"]

print(fruits.index("banana"))
```

### Output

```text
1
```

---

## `count()`

Counts occurrences.

```python
numbers = [10, 20, 10, 30, 10]

print(numbers.count(10))
```

### Output

```text
3
```

---

## `in`

Checks whether an element exists.

```python
fruits = ["apple", "banana", "mango"]

print("banana" in fruits)
print("orange" in fruits)
```

### Output

```text
True
False
```

---

# Sorting Lists

## `sort()`

Sorts the original list.

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort()

print(numbers)
```

### Output

```text
[10, 20, 30, 40, 50]
```

---

## Descending Order

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort(reverse=True)

print(numbers)
```

### Output

```text
[50, 40, 30, 20, 10]
```

---

## Sorting Strings

```python
names = ["Rahul", "Amit", "John", "David"]

names.sort()

print(names)
```

### Output

```text
['Amit', 'David', 'John', 'Rahul']
```

---

## `sorted()`

Returns a new sorted list without modifying the original iterable.

```python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers)

print(result)
print(numbers)
```

### Output

```text
[10, 20, 30, 40, 50]
[50, 10, 40, 20, 30]
```

---

## Sort by Length

```python
words = ["Python", "C", "Java", "JavaScript"]

words.sort(key=len)

print(words)
```

### Output

```text
['C', 'Java', 'Python', 'JavaScript']
```

---

# Reversing a List

## `reverse()`

Reverses the original list.

```python
numbers = [1, 2, 3, 4, 5]

numbers.reverse()

print(numbers)
```

### Output

```text
[5, 4, 3, 2, 1]
```

---

# Copying Lists

This is an important concept.

## Simple Assignment

```python
a = [1, 2, 3]

b = a

b.append(4)

print(a)
print(b)
```

### Output

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
```

Both variables refer to the same list object.

---

## `copy()`

Creates a shallow copy.

```python
a = [1, 2, 3]

b = a.copy()

b.append(4)

print(a)
print(b)
```

### Output

```text
[1, 2, 3]
[1, 2, 3, 4]
```

---

## Slicing Copy

```python
a = [1, 2, 3]

b = a[:]

b.append(4)

print(a)
print(b)
```

### Output

```text
[1, 2, 3]
[1, 2, 3, 4]
```

---

# List Concatenation

Use `+`.

```python
a = [1, 2, 3]
b = [4, 5, 6]

print(a + b)
```

### Output

```text
[1, 2, 3, 4, 5, 6]
```

---

# List Repetition

Use `*`.

```python
numbers = [1, 2]

print(numbers * 3)
```

### Output

```text
[1, 2, 1, 2, 1, 2]
```

---

# List Unpacking

A list can be unpacked into variables.

```python
numbers = [10, 20, 30]

a, b, c = numbers

print(a)
print(b)
print(c)
```

### Output

```text
10
20
30
```

---

## Extended Unpacking

```python
numbers = [1, 2, 3, 4, 5]

a, *b, c = numbers

print(a)
print(b)
print(c)
```

### Output

```text
1
[2, 3, 4]
5
```

---

# Nested Lists

A list can contain other lists.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix)
```

### Output

```text
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

Access an element:

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[1][2])
```

### Output

```text
6
```

---

# List Comprehension

List comprehension provides a short way to create lists.

### Normal Approach

```python
numbers = []

for i in range(1, 6):
    numbers.append(i)

print(numbers)
```

### Output

```text
[1, 2, 3, 4, 5]
```

### List Comprehension

```python
numbers = [i for i in range(1, 6)]

print(numbers)
```

### Output

```text
[1, 2, 3, 4, 5]
```

---

## List Comprehension with Condition

```python
even = [i for i in range(1, 11) if i % 2 == 0]

print(even)
```

### Output

```text
[2, 4, 6, 8, 10]
```

---

## List Comprehension with Expression

```python
squares = [i ** 2 for i in range(1, 6)]

print(squares)
```

### Output

```text
[1, 4, 9, 16, 25]
```

---

## List Comprehension with `if-else`

```python
result = ["Even" if i % 2 == 0 else "Odd" for i in range(1, 6)]

print(result)
```

### Output

```text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

---

## Nested List Comprehension

```python
matrix = [[j for j in range(3)] for i in range(3)]

print(matrix)
```

### Output

```text
[[0, 1, 2], [0, 1, 2], [0, 1, 2]]
```

---

# List Methods

| Method      | Purpose                     |
| ----------- | --------------------------- |
| `append()`  | Adds one item               |
| `clear()`   | Removes all items           |
| `copy()`    | Creates shallow copy        |
| `count()`   | Counts value                |
| `extend()`  | Adds multiple items         |
| `index()`   | Finds index                 |
| `insert()`  | Inserts at index            |
| `pop()`     | Removes and returns item    |
| `remove()`  | Removes first matching item |
| `reverse()` | Reverses list               |
| `sort()`    | Sorts list                  |

---

# 3. Tuple

A **tuple** is an ordered and immutable collection.

### Syntax

```python
tuple_name = (item1, item2, item3)
```

### Example

```python
numbers = (10, 20, 30)

print(numbers)
```

### Output

```text
(10, 20, 30)
```

---

# Creating Tuples

## Empty Tuple

```python
t = ()

print(t)
```

### Output

```text
()
```

---

## Tuple with Multiple Values

```python
t = (10, 20, 30)

print(t)
```

### Output

```text
(10, 20, 30)
```

---

## Single-Element Tuple

This is an important point.

### Correct

```python
t = (10,)

print(type(t))
```

### Output

```text
<class 'tuple'>
```

### Incorrect

```python
t = (10)

print(type(t))
```

### Output

```text
<class 'int'>
```

The comma creates the tuple.

---

## Tuple Without Parentheses

Parentheses are often optional when the context is unambiguous.

```python
t = 10, 20, 30

print(t)
print(type(t))
```

### Output

```text
(10, 20, 30)
<class 'tuple'>
```

---

# Tuple Indexing

Tuples support indexing.

```python
numbers = (10, 20, 30, 40)

print(numbers[0])
print(numbers[-1])
```

### Output

```text
10
40
```

---

# Tuple Slicing

```python
numbers = (10, 20, 30, 40, 50)

print(numbers[1:4])
```

### Output

```text
(20, 30, 40)
```

Reverse:

```python
numbers = (10, 20, 30, 40)

print(numbers[::-1])
```

### Output

```text
(40, 30, 20, 10)
```

---

# Tuple Immutability

Tuples cannot be modified after creation.

### Incorrect

```python
numbers = (10, 20, 30)

numbers[1] = 200
```

### Result

```text
TypeError
```

---

# Tuple Operations

## Concatenation

```python
a = (1, 2)
b = (3, 4)

print(a + b)
```

### Output

```text
(1, 2, 3, 4)
```

---

## Repetition

```python
t = (1, 2)

print(t * 3)
```

### Output

```text
(1, 2, 1, 2, 1, 2)
```

---

## Membership

```python
t = (10, 20, 30)

print(20 in t)
print(50 in t)
```

### Output

```text
True
False
```

---

# Tuple Methods

Tuples have only two main methods:

```text
count()
index()
```

---

## `count()`

```python
t = (10, 20, 10, 30, 10)

print(t.count(10))
```

### Output

```text
3
```

---

## `index()`

```python
t = (10, 20, 30)

print(t.index(20))
```

### Output

```text
1
```

---

# Tuple Packing

Packing means putting multiple values into one tuple.

```python
person = "Rahul", 20, "Python"

print(person)
```

### Output

```text
('Rahul', 20, 'Python')
```

---

# Tuple Unpacking

```python
person = ("Rahul", 20, "Python")

name, age, language = person

print(name)
print(age)
print(language)
```

### Output

```text
Rahul
20
Python
```

---

## Extended Tuple Unpacking

```python
numbers = (1, 2, 3, 4, 5)

a, *b, c = numbers

print(a)
print(b)
print(c)
```

### Output

```text
1
[2, 3, 4]
5
```

> The starred variable receives a list.

---

# Swapping Variables Using Tuple Unpacking

```python
a = 10
b = 20

a, b = b, a

print(a)
print(b)
```

### Output

```text
20
10
```

---

# Nested Tuples

```python
data = (
    ("Rahul", 20),
    ("Amit", 21)
)

print(data[0][0])
```

### Output

```text
Rahul
```

---

# Converting List to Tuple

```python
numbers = [1, 2, 3]

t = tuple(numbers)

print(t)
```

### Output

```text
(1, 2, 3)
```

---

# Converting Tuple to List

```python
t = (1, 2, 3)

numbers = list(t)

print(numbers)
```

### Output

```text
[1, 2, 3]
```

---

# Why Use Tuples?

Tuples are useful when:

* Data should not be changed
* You want a fixed collection
* A sequence is conceptually a record
* You need an immutable sequence
* A tuple needs to be used as a dictionary key or set element, provided its contents are hashable

---

# 4. Set

A **set** is a mutable collection of unique elements.

### Syntax

```python
s = {1, 2, 3}
```

### Example

```python
numbers = {10, 20, 30}

print(numbers)
```

### Output

```text
{10, 20, 30}
```

> Set display order should not be relied upon.

---

# Creating Sets

## Empty Set

This is important.

### Correct

```python
s = set()

print(type(s))
```

### Output

```text
<class 'set'>
```

### Incorrect

```python
s = {}

print(type(s))
```

### Output

```text
<class 'dict'>
```

`{}` creates an empty dictionary, not an empty set.

---

## Duplicate Values

Sets automatically remove duplicates.

```python
numbers = {1, 2, 2, 3, 3, 3}

print(numbers)
```

### Output

```text
{1, 2, 3}
```

---

# Set Properties

A set is:

```text
Mutable
Unordered
Unique
Iterable
No indexing
No slicing
```

---

# Set Cannot Use Indexing

### Incorrect

```python
s = {10, 20, 30}

print(s[0])
```

### Result

```text
TypeError
```

Use membership testing or iteration instead.

---

# Adding Elements

## `add()`

Adds one element.

```python
s = {1, 2, 3}

s.add(4)

print(s)
```

### Output

```text
{1, 2, 3, 4}
```

---

## `update()`

Adds multiple elements from an iterable.

```python
s = {1, 2}

s.update([3, 4, 5])

print(s)
```

### Output

```text
{1, 2, 3, 4, 5}
```

---

# Removing Elements

## `remove()`

Removes an element.

Raises `KeyError` if the element does not exist.

```python
s = {1, 2, 3}

s.remove(2)

print(s)
```

### Output

```text
{1, 3}
```

---

## `discard()`

Removes an element if it exists.

Does not raise an error if it doesn't exist.

```python
s = {1, 2, 3}

s.discard(5)

print(s)
```

### Output

```text
{1, 2, 3}
```

---

## `pop()`

Removes and returns an arbitrary element.

```python
s = {10, 20, 30}

value = s.pop()

print(value)
print(s)
```

### Output

```text
10
{20, 30}
```

> Do not depend on which element `pop()` removes.

---

## `clear()`

Removes all elements.

```python
s = {1, 2, 3}

s.clear()

print(s)
```

### Output

```text
set()
```

---

# Set Operations

The major set operations are:

```text
Union
Intersection
Difference
Symmetric Difference
```

---

# Union

Union contains elements from both sets.

### Operator

```text
|
```

### Method

```text
union()
```

### Code

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)
```

### Output

```text
{1, 2, 3, 4, 5}
```

Using method:

```python
print(a.union(b))
```

---

# Intersection

Intersection contains elements common to both sets.

### Operator

```text
&
```

### Code

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a & b)
```

### Output

```text
{2, 3}
```

---

# Difference

Difference contains elements present in the first set but not the second.

### Operator

```text
-
```

### Code

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a - b)
print(b - a)
```

### Output

```text
{1}
{4}
```

---

# Symmetric Difference

Contains elements present in either set but not both.

### Operator

```text
^
```

### Code

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a ^ b)
```

### Output

```text
{1, 4}
```

---

# Set Operation Diagram

```text
A = {1, 2, 3}
B = {3, 4, 5}

Union              → {1, 2, 3, 4, 5}
Intersection       → {3}
A - B              → {1, 2}
B - A              → {4, 5}
Symmetric Difference → {1, 2, 4, 5}
```

---

# Set Comparisons

## `issubset()`

Checks whether all elements of one set are contained in another.

```python
a = {1, 2}
b = {1, 2, 3}

print(a.issubset(b))
```

### Output

```text
True
```

Operator:

```python
print(a <= b)
```

---

## `issuperset()`

Checks whether a set contains all elements of another set.

```python
a = {1, 2, 3}
b = {1, 2}

print(a.issuperset(b))
```

### Output

```text
True
```

Operator:

```python
print(a >= b)
```

---

## `isdisjoint()`

Returns `True` if two sets have no common elements.

```python
a = {1, 2}
b = {3, 4}

print(a.isdisjoint(b))
```

### Output

```text
True
```

---

# Set Update Operations

## `update()`

Union update.

```python
a = {1, 2}

a.update({3, 4})

print(a)
```

### Output

```text
{1, 2, 3, 4}
```

---

## `intersection_update()`

Keeps only common elements.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.intersection_update(b)

print(a)
```

### Output

```text
{2, 3}
```

---

## `difference_update()`

Removes elements found in another set.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.difference_update(b)

print(a)
```

### Output

```text
{1}
```

---

## `symmetric_difference_update()`

Updates the set to its symmetric difference.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.symmetric_difference_update(b)

print(a)
```

### Output

```text
{1, 4}
```

---

# Set Methods

| Method                          | Purpose                      |
| ------------------------------- | ---------------------------- |
| `add()`                         | Adds element                 |
| `clear()`                       | Removes all elements         |
| `copy()`                        | Creates shallow copy         |
| `difference()`                  | Difference                   |
| `difference_update()`           | Updates with difference      |
| `discard()`                     | Removes if present           |
| `intersection()`                | Common elements              |
| `intersection_update()`         | Updates with intersection    |
| `isdisjoint()`                  | Checks no common elements    |
| `issubset()`                    | Checks subset                |
| `issuperset()`                  | Checks superset              |
| `pop()`                         | Removes arbitrary element    |
| `remove()`                      | Removes element              |
| `symmetric_difference()`        | Symmetric difference         |
| `symmetric_difference_update()` | Updates symmetric difference |
| `union()`                       | Combines sets                |
| `update()`                      | Adds elements                |

---

# Set Comprehension

Set comprehensions create sets in a concise way.

### Code

```python
squares = {x ** 2 for x in range(1, 6)}

print(squares)
```

### Output

```text
{1, 4, 9, 16, 25}
```

---

## Set Comprehension with Condition

```python
even = {x for x in range(1, 11) if x % 2 == 0}

print(even)
```

### Output

```text
{2, 4, 6, 8, 10}
```

---

# Frozen Set

A `frozenset` is an immutable set.

### Creating

```python
numbers = frozenset([1, 2, 3])

print(numbers)
print(type(numbers))
```

### Output

```text
frozenset({1, 2, 3})
<class 'frozenset'>
```

A frozenset cannot be modified.

It can be used as a dictionary key or as an element of another set if its contents are hashable.

---

# 5. Dictionary

A **dictionary** stores data in **key-value pairs**.

### Syntax

```python
dictionary = {
    key: value
}
```

### Example

```python
student = {
    "name": "Rahul",
    "age": 20,
    "course": "Python"
}

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 20, 'course': 'Python'}
```

---

# Dictionary Properties

A dictionary is:

```text
Mutable
Ordered by insertion
Key-value based
Keys are unique
Keys must be hashable
Values can be duplicates
Values can be of any type
```

---

# Creating Dictionaries

## Empty Dictionary

```python
d = {}

print(d)
```

### Output

```text
{}
```

---

## Using `dict()`

```python
student = dict(name="Rahul", age=20)

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

---

## Dictionary with Different Value Types

```python
data = {
    "name": "Rahul",
    "age": 20,
    "marks": 85.5,
    "passed": True
}

print(data)
```

### Output

```text
{'name': 'Rahul', 'age': 20, 'marks': 85.5, 'passed': True}
```

---

# Dictionary Keys

Keys must be hashable.

Common valid keys:

```text
int
float
str
tuple (if its elements are hashable)
frozenset
```

Example:

```python
data = {
    1: "One",
    "name": "Rahul",
    (10, 20): "Tuple key"
}

print(data)
```

### Output

```text
{1: 'One', 'name': 'Rahul', (10, 20): 'Tuple key'}
```

Lists, sets, and dictionaries cannot be dictionary keys because they are unhashable.

---

# Dictionary Keys Must Be Unique

If the same key appears multiple times, the last value wins.

```python
student = {
    "name": "Rahul",
    "name": "Amit"
}

print(student)
```

### Output

```text
{'name': 'Amit'}
```

---

# Accessing Dictionary Values

## Using Key

```python
student = {
    "name": "Rahul",
    "age": 20
}

print(student["name"])
print(student["age"])
```

### Output

```text
Rahul
20
```

If the key does not exist, `[]` raises `KeyError`.

---

# `get()`

`get()` safely accesses a value.

```python
student = {
    "name": "Rahul",
    "age": 20
}

print(student.get("name"))
print(student.get("city"))
```

### Output

```text
Rahul
None
```

You can provide a default.

```python
print(student.get("city", "Not Available"))
```

### Output

```text
Not Available
```

---

# Adding Dictionary Elements

```python
student = {
    "name": "Rahul"
}

student["age"] = 20

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

---

# Updating Dictionary Values

```python
student = {
    "name": "Rahul",
    "age": 20
}

student["age"] = 21

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 21}
```

---

# `update()`

Updates multiple key-value pairs.

```python
student = {
    "name": "Rahul",
    "age": 20
}

student.update({
    "age": 21,
    "city": "Hyderabad"
})

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 21, 'city': 'Hyderabad'}
```

---

# Removing Dictionary Elements

Important methods:

```text
pop()
popitem()
clear()
del
```

---

## `pop()`

Removes a specific key and returns its value.

```python
student = {
    "name": "Rahul",
    "age": 20,
    "city": "Hyderabad"
}

value = student.pop("age")

print(value)
print(student)
```

### Output

```text
20
{'name': 'Rahul', 'city': 'Hyderabad'}
```

---

## `popitem()`

Removes and returns the last inserted key-value pair.

```python
student = {
    "name": "Rahul",
    "age": 20
}

item = student.popitem()

print(item)
print(student)
```

### Output

```text
('age', 20)
{'name': 'Rahul'}
```

---

## `del`

```python
student = {
    "name": "Rahul",
    "age": 20
}

del student["age"]

print(student)
```

### Output

```text
{'name': 'Rahul'}
```

---

## `clear()`

```python
student = {
    "name": "Rahul",
    "age": 20
}

student.clear()

print(student)
```

### Output

```text
{}
```

---

# Dictionary Methods

## `keys()`

Returns a dynamic view of keys.

```python
student = {
    "name": "Rahul",
    "age": 20
}

print(student.keys())
```

### Output

```text
dict_keys(['name', 'age'])
```

---

## `values()`

Returns a dynamic view of values.

```python
student = {
    "name": "Rahul",
    "age": 20
}

print(student.values())
```

### Output

```text
dict_values(['Rahul', 20])
```

---

## `items()`

Returns key-value pairs.

```python
student = {
    "name": "Rahul",
    "age": 20
}

print(student.items())
```

### Output

```text
dict_items([('name', 'Rahul'), ('age', 20)])
```

---

# `setdefault()`

Returns the value of a key.

If the key does not exist, it inserts the key with a default value.

```python
student = {
    "name": "Rahul"
}

result = student.setdefault("age", 20)

print(result)
print(student)
```

### Output

```text
20
{'name': 'Rahul', 'age': 20}
```

If the key already exists, its value is not replaced.

```python
student = {
    "name": "Rahul",
    "age": 20
}

student.setdefault("age", 30)

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

---

# `fromkeys()`

Creates a dictionary from a sequence of keys with the same initial value.

```python
keys = ["name", "age", "city"]

student = dict.fromkeys(keys, "Unknown")

print(student)
```

### Output

```text
{'name': 'Unknown', 'age': 'Unknown', 'city': 'Unknown'}
```

---

# `copy()`

Creates a shallow copy.

```python
student = {
    "name": "Rahul",
    "age": 20
}

new_student = student.copy()

new_student["age"] = 21

print(student)
print(new_student)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
{'name': 'Rahul', 'age': 21}
```

---

# Dictionary Iteration

## Iterate Through Keys

```python
student = {
    "name": "Rahul",
    "age": 20
}

for key in student:
    print(key)
```

### Output

```text
name
age
```

---

## Iterate Through Values

```python
student = {
    "name": "Rahul",
    "age": 20
}

for value in student.values():
    print(value)
```

### Output

```text
Rahul
20
```

---

## Iterate Through Key-Value Pairs

Use `items()`.

```python
student = {
    "name": "Rahul",
    "age": 20
}

for key, value in student.items():
    print(key, ":", value)
```

### Output

```text
name : Rahul
age : 20
```

---

# Dictionary Comprehension

Dictionary comprehension provides a short way to create dictionaries.

### Code

```python
squares = {x: x ** 2 for x in range(1, 6)}

print(squares)
```

### Output

```text
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

---

## Dictionary Comprehension with Condition

```python
even_squares = {
    x: x ** 2
    for x in range(1, 11)
    if x % 2 == 0
}

print(even_squares)
```

### Output

```text
{2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

---

# Nested Dictionaries

A dictionary can contain another dictionary.

```python
students = {
    "student1": {
        "name": "Rahul",
        "age": 20
    },
    "student2": {
        "name": "Amit",
        "age": 21
    }
}

print(students)
```

### Output

```text
{
    'student1': {'name': 'Rahul', 'age': 20},
    'student2': {'name': 'Amit', 'age': 21}
}
```

Access nested value:

```python
print(students["student1"]["name"])
```

### Output

```text
Rahul
```

---

# Dictionary Unpacking

Dictionaries can be unpacked using `**`.

```python
student = {
    "name": "Rahul",
    "age": 20
}

new_student = {
    **student,
    "city": "Hyderabad"
}

print(new_student)
```

### Output

```text
{'name': 'Rahul', 'age': 20, 'city': 'Hyderabad'}
```

---

# Merging Dictionaries

Python supports dictionary merging with `|`.

```python
a = {
    "name": "Rahul"
}

b = {
    "age": 20
}

result = a | b

print(result)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

The `|=` operator updates a dictionary in place.

```python
a = {
    "name": "Rahul"
}

b = {
    "age": 20
}

a |= b

print(a)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

---

# Dictionary Methods

| Method         | Purpose                      |
| -------------- | ---------------------------- |
| `clear()`      | Removes all items            |
| `copy()`       | Creates shallow copy         |
| `fromkeys()`   | Creates dictionary from keys |
| `get()`        | Gets value safely            |
| `items()`      | Returns key-value view       |
| `keys()`       | Returns keys                 |
| `pop()`        | Removes specified key        |
| `popitem()`    | Removes last inserted pair   |
| `setdefault()` | Gets/inserts default         |
| `update()`     | Updates dictionary           |
| `values()`     | Returns values               |

---

# 6. Collections Comparison

## List vs Tuple

| Feature     | List                    | Tuple             |
| ----------- | ----------------------- | ----------------- |
| Syntax      | `[]`                    | `()`              |
| Ordered     | Yes                     | Yes               |
| Mutable     | Yes                     | No                |
| Duplicates  | Yes                     | Yes               |
| Indexing    | Yes                     | Yes               |
| Slicing     | Yes                     | Yes               |
| Methods     | Many                    | Few               |
| Performance | Generally more overhead | Generally lighter |
| Use         | Data may change         | Fixed data        |

---

## List vs Set

| Feature    | List                    | Set                          |
| ---------- | ----------------------- | ---------------------------- |
| Ordered    | Yes                     | No positional order          |
| Mutable    | Yes                     | Yes                          |
| Duplicates | Yes                     | No                           |
| Indexing   | Yes                     | No                           |
| Slicing    | Yes                     | No                           |
| Membership | Linear search generally | Hash-based average-case fast |
| Main Use   | Sequence                | Unique values                |

---

## List vs Dictionary

| Feature          | List   | Dictionary      |
| ---------------- | ------ | --------------- |
| Stores           | Values | Key-value pairs |
| Access           | Index  | Key             |
| Duplicate values | Yes    | Yes             |
| Duplicate keys   | N/A    | No              |
| Ordered          | Yes    | Yes             |
| Mutable          | Yes    | Yes             |

---

## Tuple vs Set

| Feature    | Tuple          | Set                 |
| ---------- | -------------- | ------------------- |
| Ordered    | Yes            | No positional order |
| Mutable    | No             | Yes                 |
| Duplicates | Yes            | No                  |
| Indexing   | Yes            | No                  |
| Hashable   | Sometimes      | No                  |
| Main Use   | Fixed sequence | Unique elements     |

---

## Set vs Dictionary

Both use `{}` syntax in some situations.

### Set

```python
s = {1, 2, 3}
```

### Dictionary

```python
d = {
    "name": "Rahul"
}
```

The difference is:

```text
Set        → Values
Dictionary → Key : Value
```

---

# 7. Mutable vs Immutable

This is extremely important.

## Mutable

Can be changed after creation.

```text
list
set
dict
```

Example:

```python
numbers = [1, 2, 3]

numbers[0] = 100

print(numbers)
```

### Output

```text
[100, 2, 3]
```

---

## Immutable

Cannot be changed after creation.

```text
tuple
str
int
float
bool
frozenset
```

Example:

```python
numbers = (1, 2, 3)

numbers[0] = 100
```

### Result

```text
TypeError
```

---

# 8. Ordered vs Unordered

## List

Ordered.

```python
a = [3, 1, 2]

print(a)
```

The insertion order is preserved.

---

## Tuple

Ordered.

```python
a = (3, 1, 2)

print(a)
```

---

## Dictionary

Dictionaries preserve insertion order.

```python
d = {}

d["a"] = 1
d["b"] = 2
d["c"] = 3

print(d)
```

### Output

```text
{'a': 1, 'b': 2, 'c': 3}
```

---

## Set

Sets do not provide positional indexing or a guaranteed insertion-order interface.

```python
s = {3, 1, 2}

print(s)
```

The displayed order should not be relied upon.

---

# 9. Hashable Objects

Hashability is important for:

* Set elements
* Dictionary keys

Immutable built-in objects are often hashable, but hashability depends on the object.

### Common hashable objects

```text
int
float
str
bool
tuple of hashable elements
frozenset
```

### Common unhashable objects

```text
list
set
dict
```

---

## Valid Dictionary Key

```python
data = {
    (1, 2): "Tuple key"
}

print(data)
```

### Output

```text
{(1, 2): 'Tuple key'}
```

---

## Invalid Dictionary Key

```python
data = {
    [1, 2]: "List key"
}
```

### Result

```text
TypeError: unhashable type: 'list'
```

---

# 10. Common Programs

# Program 1: Find Largest Number in a List

```python
numbers = [10, 50, 20, 80, 30]

largest = max(numbers)

print("Largest:", largest)
```

### Output

```text
Largest: 80
```

---

# Program 2: Find Smallest Number

```python
numbers = [10, 50, 20, 80, 30]

smallest = min(numbers)

print("Smallest:", smallest)
```

### Output

```text
Smallest: 10
```

---

# Program 3: Sum of List Elements

```python
numbers = [10, 20, 30, 40]

print("Sum:", sum(numbers))
```

### Output

```text
Sum: 100
```

---

# Program 4: Remove Duplicates from a List

```python
numbers = [1, 2, 2, 3, 3, 4, 5, 5]

result = list(set(numbers))

print(result)
```

### Output

```text
[1, 2, 3, 4, 5]
```

> This removes duplicates but does not guarantee preserving the original list order. If order must be preserved, use another approach such as `dict.fromkeys()`.

### Order-Preserving Approach

```python
numbers = [1, 2, 2, 3, 3, 4, 5, 5]

result = list(dict.fromkeys(numbers))

print(result)
```

### Output

```text
[1, 2, 3, 4, 5]
```

---

# Program 5: Find Even Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

even = [x for x in numbers if x % 2 == 0]

print(even)
```

### Output

```text
[2, 4, 6, 8]
```

---

# Program 6: Find Common Elements

```python
a = [1, 2, 3, 4]
b = [3, 4, 5, 6]

common = list(set(a) & set(b))

print(common)
```

### Output

```text
[3, 4]
```

---

# Program 7: Merge Two Lists

```python
a = [1, 2, 3]
b = [4, 5, 6]

result = a + b

print(result)
```

### Output

```text
[1, 2, 3, 4, 5, 6]
```

---

# Program 8: Find Frequency Using Dictionary

```python
numbers = [1, 2, 2, 3, 3, 3]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

print(frequency)
```

### Output

```text
{1: 1, 2: 2, 3: 3}
```

---

# Program 9: Find Maximum Value in Dictionary

```python
marks = {
    "Rahul": 85,
    "Amit": 92,
    "John": 78
}

highest = max(marks.values())

print(highest)
```

### Output

```text
92
```

---

# Program 10: Find Student with Highest Marks

```python
marks = {
    "Rahul": 85,
    "Amit": 92,
    "John": 78
}

student = max(marks, key=marks.get)

print(student)
```

### Output

```text
Amit
```

---

# Program 11: Merge Two Dictionaries

```python
a = {
    "name": "Rahul"
}

b = {
    "age": 20
}

result = a | b

print(result)
```

### Output

```text
{'name': 'Rahul', 'age': 20}
```

---

# Program 12: Find Common Elements Using Set

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

common = a.intersection(b)

print(common)
```

### Output

```text
{3, 4}
```

---

# Program 13: Find Unique Elements

```python
numbers = [1, 2, 2, 3, 4, 4, 5]

unique = set(numbers)

print(unique)
```

### Output

```text
{1, 2, 3, 4, 5}
```

---

# Program 14: Convert List to Tuple

```python
numbers = [1, 2, 3]

result = tuple(numbers)

print(result)
```

### Output

```text
(1, 2, 3)
```

---

# Program 15: Convert Tuple to List

```python
numbers = (1, 2, 3)

result = list(numbers)

print(result)
```

### Output

```text
[1, 2, 3]
```

---

# Program 16: Convert List to Set

```python
numbers = [1, 2, 2, 3, 3]

result = set(numbers)

print(result)
```

### Output

```text
{1, 2, 3}
```

---

# Program 17: Find Duplicate Elements

```python
numbers = [1, 2, 3, 2, 4, 1, 5]

duplicates = {
    x for x in numbers
    if numbers.count(x) > 1
}

print(duplicates)
```

### Output

```text
{1, 2}
```

---

# Program 18: Create Dictionary from Two Lists

```python
keys = ["name", "age", "city"]
values = ["Rahul", 20, "Hyderabad"]

student = dict(zip(keys, values))

print(student)
```

### Output

```text
{'name': 'Rahul', 'age': 20, 'city': 'Hyderabad'}
```

---

# Program 19: Swap Two Values

```python
a = 10
b = 20

a, b = b, a

print(a)
print(b)
```

### Output

```text
20
10
```

---

# Program 20: Matrix Using Nested Lists

```python
matrix = [
    [1, 2],
    [3, 4]
]

for row in matrix:
    for value in row:
        print(value)
```

### Output

```text
1
2
3
4
```

---

# 11. Interview & Exam Questions

## 1. What is a list?

A list is an **ordered, mutable collection** that allows duplicate values.

---

## 2. What is a tuple?

A tuple is an **ordered, immutable collection** that allows duplicate values.

---

## 3. What is a set?

A set is a **mutable collection of unique elements** with no positional indexing.

---

## 4. What is a dictionary?

A dictionary is a **mutable mapping of unique keys to values**.

---

## 5. Which collections allow duplicates?

```text
List   → Yes
Tuple  → Yes
Set    → No
Dict   → Values yes, keys no
```

---

## 6. Which collections are mutable?

```text
List   → Yes
Tuple  → No
Set    → Yes
Dict   → Yes
```

---

## 7. Which collection is best for unique values?

**Set**

---

## 8. Which collection stores key-value pairs?

**Dictionary**

---

## 9. Can a list be a dictionary key?

**No.**

Lists are unhashable.

---

## 10. Can a tuple be a dictionary key?

**Yes, if all of its elements are hashable.**

Example:

```python
data = {
    (1, 2): "value"
}

print(data)
```

### Output

```text
{(1, 2): 'value'}
```

---

## 11. Can a set contain a list?

No.

A list is unhashable.

---

## 12. Can a set contain a tuple?

Yes, if the tuple contains only hashable elements.

```python
s = {(1, 2), (3, 4)}

print(s)
```

### Output

```text
{(1, 2), (3, 4)}
```

---

## 13. Difference between `remove()` and `discard()` in sets?

```text
remove()  → Raises KeyError if element doesn't exist
discard() → Does nothing if element doesn't exist
```

---

## 14. Difference between `append()` and `extend()`?

```text
append() → Adds one object
extend() → Adds elements from an iterable
```

Example:

```python
a = [1, 2]

a.append([3, 4])

print(a)
```

Output:

```text
[1, 2, [3, 4]]
```

Whereas:

```python
a = [1, 2]

a.extend([3, 4])

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

---

## 15. Difference between `sort()` and `sorted()`?

```text
sort()   → Modifies the list itself
sorted() → Returns a new sorted list
```

---

## 16. Difference between `remove()` and `pop()` in lists?

```text
remove(value) → Removes a matching value
pop(index)    → Removes and returns an element by index
```

---

## 17. Difference between `del`, `remove()` and `pop()`?

```text
del      → Deletes using index/slice/name
remove() → Removes by value
pop()    → Removes and returns by index
```

---

## 18. Why does `{}` create a dictionary instead of a set?

Because `{}` is reserved for an empty dictionary.

Use:

```python
set()
```

for an empty set.

---

## 19. What is list comprehension?

A concise syntax for creating lists.

```python
squares = [x ** 2 for x in range(5)]
```

---

## 20. What is dictionary comprehension?

A concise syntax for creating dictionaries.

```python
squares = {x: x ** 2 for x in range(5)}
```

---

## 21. What is set comprehension?

A concise syntax for creating sets.

```python
squares = {x ** 2 for x in range(5)}
```

---

## 22. Does a tuple have `append()`?

No.

Tuples are immutable.

---

## 23. How many main methods does a tuple have?

Two:

```text
count()
index()
```

---

## 24. How do you create a single-element tuple?

Use a comma.

```python
t = (10,)
```

Not:

```python
t = (10)
```

---

## 25. Can dictionary values be duplicated?

Yes.

```python
d = {
    "a": 10,
    "b": 10
}

print(d)
```

### Output

```text
{'a': 10, 'b': 10}
```

---

# 12. Complete Cheat Sheet

# 🟦 LIST

### Create

```python
a = [1, 2, 3]
```

### Access

```python
a[0]
a[-1]
```

### Slice

```python
a[1:3]
a[::-1]
```

### Add

```python
a.append(4)
a.insert(1, 10)
a.extend([5, 6])
```

### Remove

```python
a.remove(2)
a.pop()
a.pop(1)
a.clear()
```

### Search

```python
a.index(2)
a.count(2)
2 in a
```

### Sort

```python
a.sort()
a.sort(reverse=True)
sorted(a)
```

### Reverse

```python
a.reverse()
```

### Copy

```python
b = a.copy()
```

### Comprehension

```python
[x * 2 for x in a]
```

---

# 🟨 TUPLE

### Create

```python
t = (1, 2, 3)
```

### Single Element

```python
t = (1,)
```

### Access

```python
t[0]
t[-1]
```

### Slice

```python
t[1:3]
```

### Count

```python
t.count(2)
```

### Index

```python
t.index(2)
```

### Unpack

```python
a, b, c = t
```

---

# 🟩 SET

### Create

```python
s = {1, 2, 3}
```

### Empty

```python
s = set()
```

### Add

```python
s.add(4)
s.update([5, 6])
```

### Remove

```python
s.remove(2)
s.discard(2)
s.pop()
s.clear()
```

### Union

```python
a | b
a.union(b)
```

### Intersection

```python
a & b
a.intersection(b)
```

### Difference

```python
a - b
a.difference(b)
```

### Symmetric Difference

```python
a ^ b
a.symmetric_difference(b)
```

### Subset

```python
a.issubset(b)
a <= b
```

### Superset

```python
a.issuperset(b)
a >= b
```

### Disjoint

```python
a.isdisjoint(b)
```

### Comprehension

```python
{x * 2 for x in range(5)}
```

---

# 🟥 DICTIONARY

### Create

```python
d = {
    "name": "Rahul",
    "age": 20
}
```

### Access

```python
d["name"]
d.get("name")
```

### Add / Update

```python
d["city"] = "Hyderabad"
d.update({"age": 21})
```

### Remove

```python
d.pop("age")
d.popitem()
del d["city"]
d.clear()
```

### Keys

```python
d.keys()
```

### Values

```python
d.values()
```

### Items

```python
d.items()
```

### Default

```python
d.setdefault("city", "Hyderabad")
```

### Copy

```python
new_d = d.copy()
```

### Comprehension

```python
{x: x ** 2 for x in range(5)}
```

---

# 13. Final Revision

## 🧠 Remember the Four Collections

```text
┌───────────────────────────────────────────────┐
│                 PYTHON COLLECTIONS            │
├───────────────┬───────────┬───────────────────┤
│ LIST          │ TUPLE     │ SET               │
│ []            │ ()        │ {} / set()        │
│ Mutable       │ Immutable │ Mutable           │
│ Ordered       │ Ordered   │ No positional     │
│ Duplicates ✓  │ Duplicates│ Duplicates ✗      │
│ Indexing ✓    │ Indexing ✓│ Indexing ✗        │
└───────────────┴───────────┴───────────────────┘

              DICTIONARY
              {key: value}
              Mutable
              Ordered
              Keys unique
              Access by key
```

---

# ⭐ The Most Important Differences

## List

```text
[] 
Mutable
Ordered
Duplicates allowed
Indexing available
```

Use when:

> You have a collection of values that may change.

---

## Tuple

```text
()
Immutable
Ordered
Duplicates allowed
Indexing available
```

Use when:

> You have a fixed collection of values.

---

## Set

```text
{}
set()
Mutable
Unique elements
No indexing
Set operations
```

Use when:

> You need unique values or mathematical set operations.

---

## Dictionary

```text
{key: value}
Mutable
Ordered
Unique keys
Key-value access
```

Use when:

> You need to associate a key with a value.

---

# 🔥 Most Important Methods to Memorize

```text
LIST
────────────────────────
append()
extend()
insert()
remove()
pop()
clear()
index()
count()
sort()
reverse()
copy()


TUPLE
────────────────────────
count()
index()


SET
────────────────────────
add()
update()
remove()
discard()
pop()
clear()
union()
intersection()
difference()
symmetric_difference()
issubset()
issuperset()
isdisjoint()


DICTIONARY
────────────────────────
get()
keys()
values()
items()
update()
pop()
popitem()
clear()
setdefault()
fromkeys()
copy()
```

---

# 🚀 Conversion Between Collections

## List → Tuple

```python
tuple([1, 2, 3])
```

Result:

```text
(1, 2, 3)
```

## Tuple → List

```python
list((1, 2, 3))
```

Result:

```text
[1, 2, 3]
```

## List → Set

```python
set([1, 2, 2, 3])
```

Result:

```text
{1, 2, 3}
```

## Set → List

```python
list({1, 2, 3})
```

Result:

```text
[1, 2, 3]
```

## Tuple → Set

```python
set((1, 2, 3))
```

Result:

```text
{1, 2, 3}
```

## Set → Tuple

```python
tuple({1, 2, 3})
```

Result:

```text
(1, 2, 3)
```

> When converting from a set, don't rely on the resulting order.

---

# 🎯 Final One-Minute Revision

```text
LIST
→ Ordered
→ Mutable
→ Duplicates allowed
→ Indexing
→ Slicing
→ []

TUPLE
→ Ordered
→ Immutable
→ Duplicates allowed
→ Indexing
→ Slicing
→ ()

SET
→ Unique
→ Mutable
→ No indexing
→ Set operations
→ {1, 2, 3}

DICTIONARY
→ Key : Value
→ Mutable
→ Keys unique
→ Ordered by insertion
→ Access using keys
→ {"name": "Rahul"}
```

### Most Important Operators

```text
LIST / TUPLE
+       → Concatenation
*       → Repetition
in      → Membership
not in  → Non-membership
[]      → Indexing
[:]     → Slicing


SET
|       → Union
&       → Intersection
-       → Difference
^       → Symmetric Difference
<=      → Subset
>=      → Superset


DICTIONARY
[]      → Access / update by key
|       → Merge
|=      → Merge in place
in      → Check keys
```

---

# 📝 Revision Practice Checklist

Before considering these topics complete, make sure you can do all of the following:

### List

* [ ] Create a list
* [ ] Access list elements
* [ ] Use positive and negative indexing
* [ ] Slice a list
* [ ] Modify list elements
* [ ] Add using `append()`
* [ ] Add using `insert()`
* [ ] Add using `extend()`
* [ ] Remove using `remove()`
* [ ] Remove using `pop()`
* [ ] Use `clear()`
* [ ] Use `del`
* [ ] Search using `index()`
* [ ] Count using `count()`
* [ ] Sort using `sort()`
* [ ] Use `sorted()`
* [ ] Reverse a list
* [ ] Copy a list
* [ ] Understand shallow copying
* [ ] Use list unpacking
* [ ] Work with nested lists
* [ ] Write list comprehensions

### Tuple

* [ ] Create a tuple
* [ ] Create a single-element tuple
* [ ] Index a tuple
* [ ] Slice a tuple
* [ ] Understand immutability
* [ ] Concatenate tuples
* [ ] Repeat tuples
* [ ] Use `count()`
* [ ] Use `index()`
* [ ] Pack values into tuples
* [ ] Unpack tuples
* [ ] Swap variables
* [ ] Work with nested tuples
* [ ] Convert list ↔ tuple

### Set

* [ ] Create a set
* [ ] Create an empty set correctly
* [ ] Remove duplicates
* [ ] Add elements
* [ ] Update a set
* [ ] Use `remove()`
* [ ] Use `discard()`
* [ ] Use `pop()`
* [ ] Perform union
* [ ] Perform intersection
* [ ] Perform difference
* [ ] Perform symmetric difference
* [ ] Check subset
* [ ] Check superset
* [ ] Check disjoint sets
* [ ] Use set comprehension
* [ ] Understand `frozenset`

### Dictionary

* [ ] Create a dictionary
* [ ] Create an empty dictionary
* [ ] Access values using keys
* [ ] Use `get()`
* [ ] Add key-value pairs
* [ ] Update values
* [ ] Use `update()`
* [ ] Remove using `pop()`
* [ ] Use `popitem()`
* [ ] Use `del`
* [ ] Use `clear()`
* [ ] Use `keys()`
* [ ] Use `values()`
* [ ] Use `items()`
* [ ] Use `setdefault()`
* [ ] Use `fromkeys()`
* [ ] Copy dictionaries
* [ ] Iterate through dictionaries
* [ ] Work with nested dictionaries
* [ ] Use dictionary comprehension
* [ ] Understand dictionary keys and hashability
* [ ] Merge dictionaries

---

# 🏆 Final Concept Map

```text
                         PYTHON COLLECTIONS
                                │
             ┌──────────────────┼──────────────────┐
             │                  │                  │
           LIST               TUPLE               SET
             │                  │                  │
          Mutable           Immutable           Mutable
          Ordered            Ordered            Unique
          []                  ()                 {}
             │                  │                  │
       ┌─────┼─────┐      ┌─────┼─────┐      ┌────┼─────┐
       │     │     │      │     │     │      │    │     │
    Index Slice Methods  Index Slice Methods  Add  Remove Operations
       │     │     │      │     │     │      │    │     │
       └─────┴─────┘      └─────┴─────┘      └────┴─────┘

                                │
                          DICTIONARY
                                │
                         {key: value}
                                │
                   ┌────────────┼────────────┐
                   │            │            │
                 Keys         Values       Items
                   │            │            │
                Unique       Duplicates    Pairs
                   │
              Hashable Keys
```

---

# 💡 Golden Rule

> **List → Ordered data that can change**
>
> **Tuple → Ordered data that should not change**
>
> **Set → Unique data**
>
> **Dictionary → Key-value data**

Once these four concepts are strong, a large part of Python's **data handling and problem-solving foundation** becomes much easier.
