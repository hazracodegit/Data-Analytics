# 🐍 Python Strings — Complete Revision Notes

> A complete revision guide for **Strings in Python**, covering everything from basic concepts to advanced string methods, formatting, slicing, searching, validation, Unicode, and practical programs.

---

# 📚 Table of Contents

* [1. What is a String?](#1-what-is-a-string)
* [2. Creating Strings](#2-creating-strings)
* [3. Single, Double and Triple Quotes](#3-single-double-and-triple-quotes)
* [4. Multiline Strings](#4-multiline-strings)
* [5. Empty String](#5-empty-string)
* [6. String Immutability](#6-string-immutability)
* [7. String Indexing](#7-string-indexing)
* [8. Positive Indexing](#8-positive-indexing)
* [9. Negative Indexing](#9-negative-indexing)
* [10. String Slicing](#10-string-slicing)
* [11. Slice Syntax](#11-slice-syntax)
* [12. String Concatenation](#12-string-concatenation)
* [13. String Repetition](#13-string-repetition)
* [14. Membership Operators](#14-membership-operators)
* [15. Comparing Strings](#15-comparing-strings)
* [16. Iterating Through Strings](#16-iterating-through-strings)
* [17. String Length](#17-string-length)
* [18. Escape Sequences](#18-escape-sequences)
* [19. Raw Strings](#19-raw-strings)
* [20. String Conversion](#20-string-conversion)
* [21. `str()` Function](#21-str-function)
* [22. Important String Methods](#22-important-string-methods)
* [23. Case Conversion Methods](#23-case-conversion-methods)
* [24. Searching Methods](#24-searching-methods)
* [25. Counting Occurrences](#25-counting-occurrences)
* [26. Checking Starting and Ending](#26-checking-starting-and-ending)
* [27. Removing Whitespace](#27-removing-whitespace)
* [28. Replacing Strings](#28-replacing-strings)
* [29. Splitting Strings](#29-splitting-strings)
* [30. Joining Strings](#30-joining-strings)
* [31. Partitioning Strings](#31-partitioning-strings)
* [32. String Validation Methods](#32-string-validation-methods)
* [33. Alignment Methods](#33-alignment-methods)
* [34. `zfill()`](#34-zfill)
* [35. Translation and `maketrans()`](#35-translation-and-maketrans)
* [36. Encoding Strings](#36-encoding-strings)
* [37. Unicode](#37-unicode)
* [38. String Formatting](#38-string-formatting)
* [39. f-Strings](#39-f-strings)
* [40. `format()` Method](#40-format-method)
* [41. Format Specifiers](#41-format-specifiers)
* [42. Old `%` Formatting](#42-old--formatting)
* [43. String Methods Quick Reference](#43-string-methods-quick-reference)
* [44. Common String Programs](#44-common-string-programs)
* [45. Important Interview/Exam Points](#45-important-interviewexam-points)
* [46. Quick Revision Sheet](#46-quick-revision-sheet)

---

# 1. What is a String?

A **string** is a sequence of characters enclosed inside quotes.

In Python, strings are objects of the `str` class.

### Example

```python
name = "Python"
```

### Output

```text
Python
```

You can check its type using `type()`.

### Code

```python
name = "Python"

print(type(name))
```

### Output

```text
<class 'str'>
```

---

# 2. Creating Strings

Strings can be created using:

* Single quotes `' '`
* Double quotes `" "`
* Triple single quotes `''' '''`
* Triple double quotes `""" """`

### Example

```python
a = 'Python'
b = "Python"
c = '''Python'''
d = """Python"""

print(a)
print(b)
print(c)
print(d)
```

### Output

```text
Python
Python
Python
Python
```

---

# 3. Single, Double and Triple Quotes

## Single Quotes

```python
name = 'Python'
```

## Double Quotes

```python
name = "Python"
```

Both create strings.

---

## When to Use Double Quotes

Double quotes are useful when the string contains a single quote.

### Code

```python
message = "Python's syntax is simple"

print(message)
```

### Output

```text
Python's syntax is simple
```

---

## When to Use Single Quotes

Single quotes are useful when the string contains double quotes.

### Code

```python
message = 'He said "Hello"'

print(message)
```

### Output

```text
He said "Hello"
```

---

## Triple Quotes

Triple quotes are commonly used for multiline strings and docstrings.

### Code

```python
message = """This is
a multiline
string."""

print(message)
```

### Output

```text
This is
a multiline
string.
```

---

# 4. Multiline Strings

A multiline string can be created using triple quotes.

### Code

```python
text = """Python
is
easy
to learn."""

print(text)
```

### Output

```text
Python
is
easy
to learn.
```

---

# 5. Empty String

A string containing no characters is called an empty string.

### Code

```python
text = ""

print(text)
print(len(text))
```

### Output

```text
0
```

The length of an empty string is `0`.

---

# 6. String Immutability

Python strings are **immutable**.

This means that once a string is created, its individual characters cannot be changed.

### Incorrect

```python
name = "Python"

name[0] = "J"
```

### Error

```text
TypeError: 'str' object does not support item assignment
```

Instead, create a new string.

### Correct

```python
name = "Python"

name = "J" + name[1:]

print(name)
```

### Output

```text
Jython
```

### Important

```text
String → Immutable
List   → Mutable
```

---

# 7. String Indexing

**Indexing** is used to access individual characters from a string.

Python uses **zero-based indexing**.

### Example

```python
text = "Python"

print(text[0])
print(text[1])
print(text[2])
```

### Output

```text
P
y
t
```

---

# 8. Positive Indexing

Positive indexing starts from `0` from the left.

For:

```text
Python
```

The indexes are:

```text
 P   y   t   h   o   n
 0   1   2   3   4   5
```

### Code

```python
text = "Python"

print(text[0])
print(text[3])
print(text[5])
```

### Output

```text
P
h
n
```

---

# 9. Negative Indexing

Negative indexing starts from `-1` from the right.

```text
 P    y    t    h    o    n
-6   -5   -4   -3   -2   -1
```

### Code

```python
text = "Python"

print(text[-1])
print(text[-2])
print(text[-6])
```

### Output

```text
n
o
P
```

---

# 10. String Slicing

Slicing is used to extract a portion of a string.

### Example

```python
text = "Python Programming"

print(text[0:6])
```

### Output

```text
Python
```

---

# 11. Slice Syntax

The general syntax is:

```python
string[start:stop:step]
```

### Important Rule

The `stop` index is **not included**.

---

## Basic Slicing

```python
text = "Python"

print(text[0:3])
```

### Output

```text
Pyt
```

---

## Start Omitted

```python
text = "Python"

print(text[:3])
```

### Output

```text
Pyt
```

---

## Stop Omitted

```python
text = "Python"

print(text[3:])
```

### Output

```text
hon
```

---

## Both Omitted

```python
text = "Python"

print(text[:])
```

### Output

```text
Python
```

---

## Using Step

```python
text = "Python"

print(text[0:6:2])
```

### Output

```text
Pto
```

---

## Negative Step

Negative step moves from right to left.

### Code

```python
text = "Python"

print(text[::-1])
```

### Output

```text
nohtyP
```

This is a common way to reverse a string.

---

# 12. String Concatenation

**Concatenation** means joining strings together.

The `+` operator is used.

### Code

```python
first = "Hello"
second = "World"

result = first + " " + second

print(result)
```

### Output

```text
Hello World
```

### Important

You cannot directly concatenate a string and an integer.

### Incorrect

```python
age = 20

print("Age: " + age)
```

This produces a `TypeError`.

### Correct

```python
age = 20

print("Age: " + str(age))
```

### Output

```text
Age: 20
```

---

# 13. String Repetition

The `*` operator can repeat a string.

### Code

```python
text = "Python "

print(text * 3)
```

### Output

```text
Python Python Python
```

Another example:

```python
print("*" * 10)
```

### Output

```text
**********
```

---

# 14. Membership Operators

The operators:

```text
in
not in
```

are used to check whether a substring or character exists in a string.

### Code

```python
text = "Python Programming"

print("Python" in text)
print("Java" in text)
print("Java" not in text)
```

### Output

```text
True
False
True
```

---

# 15. Comparing Strings

Strings can be compared using comparison operators.

```text
==
!=
<
>
<=
>=
```

### Code

```python
a = "apple"
b = "banana"

print(a == b)
print(a != b)
print(a < b)
```

### Output

```text
False
True
True
```

String comparison is based on Unicode code-point values.

---

# 16. Iterating Through Strings

A string can be traversed character by character using a `for` loop.

### Code

```python
text = "Python"

for char in text:
    print(char)
```

### Output

```text
P
y
t
h
o
n
```

---

# 17. String Length

The `len()` function returns the number of characters.

### Code

```python
text = "Python"

print(len(text))
```

### Output

```text
6
```

Spaces are also counted.

### Code

```python
text = "Hello World"

print(len(text))
```

### Output

```text
11
```

---

# 18. Escape Sequences

Escape sequences begin with a backslash `\`.

| Escape Sequence | Meaning                           |
| --------------- | --------------------------------- |
| `\n`            | New line                          |
| `\t`            | Tab                               |
| `\\`            | Backslash                         |
| `\'`            | Single quote                      |
| `\"`            | Double quote                      |
| `\r`            | Carriage return                   |
| `\b`            | Backspace                         |
| `\f`            | Form feed                         |
| `\v`            | Vertical tab                      |
| `\a`            | Alert/bell                        |
| `\0`            | Null character                    |
| `\xhh`          | Character using hexadecimal value |
| `\ooo`          | Character using octal value       |
| `\N{name}`      | Unicode character by name         |
| `\uXXXX`        | Unicode character                 |
| `\UXXXXXXXX`    | Unicode character                 |

---

## `\n` — New Line

```python
print("Hello\nWorld")
```

### Output

```text
Hello
World
```

---

## `\t` — Tab

```python
print("Hello\tWorld")
```

### Output

```text
Hello   World
```

---

## `\\` — Backslash

```python
print("C:\\Users\\Python")
```

### Output

```text
C:\Users\Python
```

---

## `\"` — Double Quote

```python
print("He said \"Hello\"")
```

### Output

```text
He said "Hello"
```

---

## `\'` — Single Quote

```python
print('Python\'s syntax')
```

### Output

```text
Python's syntax
```

---

# 19. Raw Strings

A raw string treats backslashes mostly as literal characters instead of interpreting ordinary escape sequences.

Prefix the string with `r` or `R`.

### Code

```python
path = r"C:\Users\Python\Documents"

print(path)
```

### Output

```text
C:\Users\Python\Documents
```

Raw strings are commonly useful for:

* Windows paths
* Regular expressions
* Text containing many backslashes

> A raw string still has some syntax limitations. For example, a raw string cannot end with a single backslash.

---

# 20. String Conversion

Other values can be converted to strings.

### Code

```python
age = 20
price = 99.50
is_valid = True

print(str(age))
print(str(price))
print(str(is_valid))
```

### Output

```text
20
99.5
True
```

---

# 21. `str()` Function

The `str()` function converts an object into its string representation.

### Syntax

```python
str(object)
```

### Example

```python
number = 100

text = str(number)

print(text)
print(type(text))
```

### Output

```text
100
<class 'str'>
```

---

# 22. Important String Methods

Python provides many built-in methods for strings.

### Major categories

```text
Case Conversion
Searching
Checking
Splitting
Joining
Replacing
Removing Whitespace
Validation
Formatting
Alignment
Translation
Encoding
```

---

# 23. Case Conversion Methods

Important methods:

```text
capitalize()
casefold()
lower()
upper()
title()
swapcase()
```

---

## `capitalize()`

Converts the first character to uppercase and the remaining characters to lowercase.

### Code

```python
text = "python PROGRAMMING"

print(text.capitalize())
```

### Output

```text
Python programming
```

---

## `lower()`

Converts characters to lowercase.

### Code

```python
text = "PYTHON"

print(text.lower())
```

### Output

```text
python
```

---

## `upper()`

Converts characters to uppercase.

### Code

```python
text = "python"

print(text.upper())
```

### Output

```text
PYTHON
```

---

## `title()`

Converts the first character of each word to uppercase.

### Code

```python
text = "python programming language"

print(text.title())
```

### Output

```text
Python Programming Language
```

---

## `swapcase()`

Converts uppercase characters to lowercase and lowercase characters to uppercase.

### Code

```python
text = "Python PROGRAMMING"

print(text.swapcase())
```

### Output

```text
pYTHON programming
```

---

## `casefold()`

Converts a string to a form suitable for caseless comparison.

It is generally more aggressive than `lower()` for Unicode text.

### Code

```python
a = "HELLO"
b = "hello"

print(a.casefold() == b.casefold())
```

### Output

```text
True
```

### `lower()` vs `casefold()`

```text
lower()   → General lowercase conversion
casefold() → Stronger Unicode-aware case normalization for comparison
```

---

# 24. Searching Methods

Important searching methods:

```text
find()
rfind()
index()
rindex()
```

---

## `find()`

Returns the lowest index where a substring is found.

Returns `-1` if not found.

### Code

```python
text = "Python Programming"

print(text.find("Python"))
print(text.find("Java"))
```

### Output

```text
0
-1
```

### Syntax

```python
string.find(substring, start, end)
```

---

## `rfind()`

Returns the highest index where a substring is found.

### Code

```python
text = "Python Python"

print(text.rfind("Python"))
```

### Output

```text
7
```

---

## `index()`

Works like `find()`, but raises `ValueError` if the substring is not found.

### Code

```python
text = "Python Programming"

print(text.index("Python"))
```

### Output

```text
0
```

If not found:

```python
text = "Python"

print(text.index("Java"))
```

### Result

```text
ValueError
```

---

## `rindex()`

Returns the highest index where a substring is found.

Raises `ValueError` if it is not found.

### Code

```python
text = "Python Python"

print(text.rindex("Python"))
```

### Output

```text
7
```

---

# 25. Counting Occurrences

## `count()`

Returns the number of non-overlapping occurrences of a substring.

### Code

```python
text = "banana"

print(text.count("a"))
print(text.count("an"))
```

### Output

```text
3
2
```

### Syntax

```python
string.count(substring, start, end)
```

---

# 26. Checking Starting and Ending

Two important methods:

```text
startswith()
endswith()
```

---

## `startswith()`

Checks whether a string starts with a particular substring.

### Code

```python
text = "Python Programming"

print(text.startswith("Python"))
print(text.startswith("Java"))
```

### Output

```text
True
False
```

---

## `endswith()`

Checks whether a string ends with a particular substring.

### Code

```python
filename = "program.py"

print(filename.endswith(".py"))
print(filename.endswith(".txt"))
```

### Output

```text
True
False
```

Both methods can accept tuples of possible prefixes/suffixes.

### Code

```python
filename = "photo.jpg"

print(filename.endswith((".jpg", ".png", ".gif")))
```

### Output

```text
True
```

---

# 27. Removing Whitespace

Important methods:

```text
strip()
lstrip()
rstrip()
```

---

## `strip()`

Removes leading and trailing whitespace.

### Code

```python
text = "   Python   "

print(text.strip())
```

### Output

```text
Python
```

---

## `lstrip()`

Removes leading whitespace.

### Code

```python
text = "   Python"

print(text.lstrip())
```

### Output

```text
Python
```

---

## `rstrip()`

Removes trailing whitespace.

### Code

```python
text = "Python   "

print(text.rstrip())
```

### Output

```text
Python
```

---

## Removing Specific Characters

`strip()`, `lstrip()`, and `rstrip()` can receive a set of characters to remove.

### Code

```python
text = "###Python###"

print(text.strip("#"))
```

### Output

```text
Python
```

> These methods remove characters from the ends, not arbitrary occurrences in the middle.

---

# 28. Replacing Strings

## `replace()`

Replaces occurrences of one substring with another.

### Syntax

```python
string.replace(old, new, count)
```

### Code

```python
text = "I like Java"

result = text.replace("Java", "Python")

print(result)
```

### Output

```text
I like Python
```

---

## Using `count`

### Code

```python
text = "apple apple apple"

print(text.replace("apple", "mango", 2))
```

### Output

```text
mango mango apple
```

---

# 29. Splitting Strings

## `split()`

Splits a string into a list.

### Code

```python
text = "Python is easy"

words = text.split()

print(words)
```

### Output

```text
['Python', 'is', 'easy']
```

### Using a Separator

```python
text = "apple,banana,mango"

fruits = text.split(",")

print(fruits)
```

### Output

```text
['apple', 'banana', 'mango']
```

### Syntax

```python
string.split(separator, maxsplit)
```

---

## `rsplit()`

Splits from the right side.

### Code

```python
text = "one-two-three-four"

print(text.rsplit("-", 2))
```

### Output

```text
['one-two', 'three', 'four']
```

---

## `splitlines()`

Splits a string at line boundaries.

### Code

```python
text = "Python\nJava\nC++"

print(text.splitlines())
```

### Output

```text
['Python', 'Java', 'C++']
```

---

# 30. Joining Strings

## `join()`

Joins elements of an iterable using a separator.

### Code

```python
words = ["Python", "is", "easy"]

result = " ".join(words)

print(result)
```

### Output

```text
Python is easy
```

---

## Joining with Comma

```python
fruits = ["Apple", "Banana", "Mango"]

result = ", ".join(fruits)

print(result)
```

### Output

```text
Apple, Banana, Mango
```

### Important

The elements being joined must be strings.

Incorrect:

```python
numbers = [1, 2, 3]

print(",".join(numbers))
```

Correct:

```python
numbers = [1, 2, 3]

print(",".join(map(str, numbers)))
```

### Output

```text
1,2,3
```

---

# 31. Partitioning Strings

## `partition()`

Splits a string into exactly three parts:

```text
before separator
separator
after separator
```

### Code

```python
text = "Python is easy"

print(text.partition("is"))
```

### Output

```text
('Python ', 'is', ' easy')
```

If the separator is not found:

```python
text = "Python is easy"

print(text.partition("Java"))
```

### Output

```text
('Python is easy', '', '')
```

---

## `rpartition()`

Searches for the separator from the right.

### Code

```python
text = "one-two-three"

print(text.rpartition("-"))
```

### Output

```text
('one-two', '-', 'three')
```

---

# 32. String Validation Methods

Python provides many `is...()` methods.

Important ones:

```text
isalnum()
isalpha()
isascii()
isdecimal()
isdigit()
isidentifier()
islower()
isnumeric()
isprintable()
isspace()
istitle()
isupper()
```

---

# `isalnum()`

Returns `True` if all characters are alphanumeric and the string is not empty.

Alphanumeric means:

```text
A-Z
a-z
0-9
```

### Code

```python
print("Python123".isalnum())
print("Python 123".isalnum())
```

### Output

```text
True
False
```

---

# `isalpha()`

Returns `True` if all characters are alphabetic and the string is not empty.

### Code

```python
print("Python".isalpha())
print("Python123".isalpha())
```

### Output

```text
True
False
```

---

# `isascii()`

Returns `True` if all characters are ASCII characters or the string is empty.

### Code

```python
print("Python".isascii())
print("Python©".isascii())
```

### Output

```text
True
False
```

---

# `isdecimal()`

Checks whether all characters are decimal characters.

### Code

```python
print("123".isdecimal())
print("123.45".isdecimal())
```

### Output

```text
True
False
```

---

# `isdigit()`

Checks whether all characters are digits.

### Code

```python
print("123".isdigit())
print("123.45".isdigit())
```

### Output

```text
True
False
```

---

# `isnumeric()`

Checks whether all characters are numeric.

### Code

```python
print("123".isnumeric())
```

### Output

```text
True
```

---

## `isdecimal()` vs `isdigit()` vs `isnumeric()`

This is an important exam/interview topic.

```text
isdecimal() → Most restrictive
isdigit()   → Broader
isnumeric() → Broadest
```

For ordinary ASCII digits:

```python
print("123".isdecimal())
print("123".isdigit())
print("123".isnumeric())
```

### Output

```text
True
True
True
```

They differ for some Unicode numeric characters.

---

# `isidentifier()`

Checks whether a string is a valid Python identifier.

### Code

```python
print("student".isidentifier())
print("student_name".isidentifier())
print("123student".isidentifier())
print("student-name".isidentifier())
```

### Output

```text
True
True
False
False
```

> `isidentifier()` does not mean the name is necessarily usable as a variable. A Python keyword such as `"class"` is an identifier syntactically but cannot be used as an ordinary variable name.

---

# `islower()`

Checks whether all cased characters are lowercase.

### Code

```python
print("python".islower())
print("Python".islower())
```

### Output

```text
True
False
```

---

# `isupper()`

Checks whether all cased characters are uppercase.

### Code

```python
print("PYTHON".isupper())
print("Python".isupper())
```

### Output

```text
True
False
```

---

# `istitle()`

Checks whether the string follows title-case rules.

### Code

```python
print("Python Programming".istitle())
print("python programming".istitle())
```

### Output

```text
True
False
```

---

# `isspace()`

Checks whether all characters are whitespace and the string is not empty.

### Code

```python
print("   ".isspace())
print("Python".isspace())
```

### Output

```text
True
False
```

---

# `isprintable()`

Checks whether all characters are printable or the string is empty.

### Code

```python
print("Python".isprintable())
print("Hello\nWorld".isprintable())
```

### Output

```text
True
False
```

---

# 33. Alignment Methods

Important methods:

```text
center()
ljust()
rjust()
```

---

## `center()`

Centers a string inside a field of a specified width.

### Code

```python
text = "Python"

print(text.center(20, "-"))
```

### Output

```text
-------Python-------
```

---

## `ljust()`

Left-aligns a string.

### Code

```python
text = "Python"

print(text.ljust(10, "-"))
```

### Output

```text
Python----
```

---

## `rjust()`

Right-aligns a string.

### Code

```python
text = "Python"

print(text.rjust(10, "-"))
```

### Output

```text
----Python
```

---

# 34. `zfill()`

Pads a numeric string on the left with zeros.

### Code

```python
number = "42"

print(number.zfill(5))
```

### Output

```text
00042
```

It also handles a leading sign.

### Code

```python
print("-42".zfill(5))
print("+42".zfill(5))
```

### Output

```text
-0042
+0042
```

---

# 35. Translation and `maketrans()`

Python provides:

```text
maketrans()
translate()
```

for character translation.

---

## `maketrans()`

Creates a translation table.

### Code

```python
table = str.maketrans("abc", "123")

print("abc cab".translate(table))
```

### Output

```text
123 312
```

---

## `translate()`

Applies a translation table to a string.

### Example

```python
table = str.maketrans({
    "a": "1",
    "e": "2",
    "i": "3",
    "o": "4",
    "u": "5"
})

text = "education"

print(text.translate(table))
```

### Output

```text
2d5c1t34n
```

---

## Removing Characters with `translate()`

You can map characters to `None`.

### Code

```python
table = str.maketrans("", "", "aeiou")

text = "education"

print(text.translate(table))
```

### Output

```text
dctn
```

---

# 36. Encoding Strings

Strings can be converted into bytes using `encode()`.

### Code

```python
text = "Python"

data = text.encode()

print(data)
print(type(data))
```

### Output

```text
b'Python'
<class 'bytes'>
```

---

## UTF-8 Encoding

UTF-8 is commonly used.

### Code

```python
text = "Python"

data = text.encode("utf-8")

print(data)
```

### Output

```text
b'Python'
```

---

## Decoding Bytes

Bytes can be converted back into a string using `decode()`.

### Code

```python
data = b"Python"

text = data.decode("utf-8")

print(text)
```

### Output

```text
Python
```

### Remember

```text
String
   ↓ encode()
Bytes
   ↓ decode()
String
```

---

# 37. Unicode

Python 3 strings are Unicode text.

Unicode allows Python to represent characters from many writing systems and symbols.

### Code

```python
text = "Hello नमस्ते 世界 🌍"

print(text)
```

### Output

```text
Hello नमस्ते 世界 🌍
```

---

## `ord()`

Returns the Unicode code point of a character.

### Code

```python
print(ord("A"))
print(ord("a"))
```

### Output

```text
65
97
```

---

## `chr()`

Converts a Unicode code point into a character.

### Code

```python
print(chr(65))
print(chr(97))
```

### Output

```text
A
a
```

### Relationship

```text
ord("A") → 65
chr(65)  → "A"
```

---

# 38. String Formatting

String formatting means inserting values into strings.

Python provides several approaches:

```text
1. Concatenation
2. % formatting
3. str.format()
4. f-strings
```

---

# 39. f-Strings

f-strings are the modern and highly convenient way to format strings.

Prefix a string with `f` or `F`.

### Code

```python
name = "Rahul"
age = 20

print(f"My name is {name} and I am {age} years old.")
```

### Output

```text
My name is Rahul and I am 20 years old.
```

---

## Expressions in f-Strings

Expressions can be placed inside `{}`.

### Code

```python
a = 10
b = 20

print(f"Sum = {a + b}")
```

### Output

```text
Sum = 30
```

---

## Calling Functions

```python
name = "python"

print(f"{name.upper()}")
```

### Output

```text
PYTHON
```

---

## Formatting Decimal Values

### Code

```python
price = 99.5678

print(f"{price:.2f}")
```

### Output

```text
99.57
```

---

# 40. `format()` Method

The `format()` method inserts values into `{}` placeholders.

### Code

```python
name = "Rahul"
age = 20

print("My name is {} and I am {} years old.".format(name, age))
```

### Output

```text
My name is Rahul and I am 20 years old.
```

---

## Positional Arguments

### Code

```python
print("{} + {} = {}".format(10, 20, 30))
```

### Output

```text
10 + 20 = 30
```

---

## Index Numbers

### Code

```python
print("{1} {0}".format("Python", "Programming"))
```

### Output

```text
Programming Python
```

---

## Keyword Arguments

### Code

```python
print(
    "Name: {name}, Age: {age}".format(
        name="Rahul",
        age=20
    )
)
```

### Output

```text
Name: Rahul, Age: 20
```

---

# 41. Format Specifiers

Format specifications are used to control how values are displayed.

---

## Decimal Places

```python
price = 99.5678

print(f"{price:.2f}")
```

### Output

```text
99.57
```

---

## Percentage

```python
value = 0.75

print(f"{value:.2%}")
```

### Output

```text
75.00%
```

---

## Comma Separator

```python
number = 1000000

print(f"{number:,}")
```

### Output

```text
1,000,000
```

---

## Width

```python
name = "Python"

print(f"{name:10}")
```

### Output

```text
Python
```

The field has a minimum width of 10.

---

## Alignment

### Left

```python
print(f"{'Python':<10}")
```

### Output

```text
Python
```

### Center

```python
print(f"{'Python':^10}")
```

### Output

```text
  Python
```

### Right

```python
print(f"{'Python':>10}")
```

### Output

```text
    Python
```

---

## Padding with Zeros

```python
number = 42

print(f"{number:05}")
```

### Output

```text
00042
```

---

# 42. Old `%` Formatting

Python also supports the older `%` formatting style.

### `%s` — String

```python
name = "Rahul"

print("Hello %s" % name)
```

### Output

```text
Hello Rahul
```

---

## `%d` — Integer

```python
age = 20

print("Age = %d" % age)
```

### Output

```text
Age = 20
```

---

## `%f` — Float

```python
price = 99.50

print("Price = %f" % price)
```

### Output

```text
Price = 99.500000
```

---

## Multiple Values

```python
name = "Rahul"
age = 20

print("Name: %s, Age: %d" % (name, age))
```

### Output

```text
Name: Rahul, Age: 20
```

> For new Python code, prefer **f-strings** or `str.format()` over old `%` formatting.

---

# 43. String Methods Quick Reference

| Method           | Purpose                                                 |
| ---------------- | ------------------------------------------------------- |
| `capitalize()`   | Capitalizes first character                             |
| `casefold()`     | Aggressive lowercase conversion for caseless comparison |
| `center()`       | Centers string                                          |
| `count()`        | Counts occurrences                                      |
| `encode()`       | Converts string to bytes                                |
| `endswith()`     | Checks ending                                           |
| `expandtabs()`   | Replaces tabs with spaces                               |
| `find()`         | Finds substring, returns `-1` if absent                 |
| `format()`       | Formats string                                          |
| `format_map()`   | Formats using a mapping                                 |
| `index()`        | Finds substring, raises error if absent                 |
| `isalnum()`      | Checks alphanumeric                                     |
| `isalpha()`      | Checks alphabetic                                       |
| `isascii()`      | Checks ASCII                                            |
| `isdecimal()`    | Checks decimal characters                               |
| `isdigit()`      | Checks digit characters                                 |
| `isidentifier()` | Checks valid identifier syntax                          |
| `islower()`      | Checks lowercase                                        |
| `isnumeric()`    | Checks numeric characters                               |
| `isprintable()`  | Checks printable characters                             |
| `isspace()`      | Checks whitespace                                       |
| `istitle()`      | Checks title case                                       |
| `isupper()`      | Checks uppercase                                        |
| `join()`         | Joins iterable elements                                 |
| `ljust()`        | Left-aligns                                             |
| `lower()`        | Converts to lowercase                                   |
| `lstrip()`       | Removes left-side characters                            |
| `maketrans()`    | Creates translation table                               |
| `partition()`    | Splits at first separator                               |
| `removeprefix()` | Removes prefix if present                               |
| `removesuffix()` | Removes suffix if present                               |
| `replace()`      | Replaces substring                                      |
| `rfind()`        | Finds substring from right                              |
| `rindex()`       | Finds substring from right                              |
| `rjust()`        | Right-aligns                                            |
| `rpartition()`   | Splits at last separator                                |
| `rsplit()`       | Splits from right                                       |
| `rstrip()`       | Removes right-side characters                           |
| `split()`        | Splits into list                                        |
| `splitlines()`   | Splits at line boundaries                               |
| `startswith()`   | Checks beginning                                        |
| `strip()`        | Removes leading/trailing characters                     |
| `swapcase()`     | Swaps upper/lower case                                  |
| `title()`        | Converts to title case                                  |
| `translate()`    | Applies translation table                               |
| `upper()`        | Converts to uppercase                                   |
| `zfill()`        | Pads with zeros                                         |

---

# 44. Additional String Methods

## `expandtabs()`

Replaces tab characters with spaces according to a tab size.

### Code

```python
text = "Python\tProgramming"

print(text.expandtabs(4))
```

### Output

```text
Python  Programming
```

---

## `removeprefix()`

Removes a specified prefix if present.

### Code

```python
text = "Python Programming"

print(text.removeprefix("Python "))
```

### Output

```text
Programming
```

If the prefix is absent, the original string is returned.

---

## `removesuffix()`

Removes a specified suffix if present.

### Code

```python
filename = "program.py"

print(filename.removesuffix(".py"))
```

### Output

```text
program
```

---

## `format_map()`

Formats a string using a mapping object.

### Code

```python
data = {
    "name": "Rahul",
    "age": 20
}

text = "Name: {name}, Age: {age}"

print(text.format_map(data))
```

### Output

```text
Name: Rahul, Age: 20
```

---

# 45. Common String Programs

These are especially useful for revision and interviews.

---

# Program 1: Reverse a String

### Code

```python
text = input("Enter a string: ")

reverse = text[::-1]

print("Reverse:", reverse)
```

### Example Input

```text
Enter a string: Python
```

### Output

```text
Reverse: nohtyP
```

---

# Program 2: Check Palindrome

A palindrome reads the same forward and backward.

Examples:

```text
madam
level
radar
```

### Code

```python
text = input("Enter a string: ")

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not a palindrome")
```

### Example Input

```text
Enter a string: madam
```

### Output

```text
Palindrome
```

---

# Program 3: Count Characters

### Code

```python
text = input("Enter a string: ")

print("Length:", len(text))
```

### Example Input

```text
Enter a string: Python
```

### Output

```text
Length: 6
```

---

# Program 4: Count Vowels

### Code

```python
text = input("Enter a string: ")

count = 0

for char in text.lower():
    if char in "aeiou":
        count += 1

print("Vowels:", count)
```

### Example Input

```text
Enter a string: Python Programming
```

### Output

```text
Vowels: 4
```

---

# Program 5: Count Consonants

### Code

```python
text = input("Enter a string: ")

count = 0

for char in text.lower():
    if char.isalpha() and char not in "aeiou":
        count += 1

print("Consonants:", count)
```

### Example Input

```text
Enter a string: Python
```

### Output

```text
Consonants: 5
```

---

# Program 6: Count Words

### Code

```python
text = input("Enter a sentence: ")

words = text.split()

print("Number of words:", len(words))
```

### Example Input

```text
Enter a sentence: Python is easy to learn
```

### Output

```text
Number of words: 5
```

---

# Program 7: Count a Specific Character

### Code

```python
text = input("Enter a string: ")
char = input("Enter character: ")

print("Count:", text.count(char))
```

### Example Input

```text
Enter a string: banana
Enter character: a
```

### Output

```text
Count: 3
```

---

# Program 8: Remove Spaces

### Code

```python
text = input("Enter a string: ")

result = text.replace(" ", "")

print(result)
```

### Example Input

```text
Enter a string: Python is easy
```

### Output

```text
Pythoniseasy
```

---

# Program 9: Find Duplicate Characters

### Code

```python
text = input("Enter a string: ")

duplicates = []

for char in text:
    if text.count(char) > 1 and char not in duplicates:
        duplicates.append(char)

print("Duplicate characters:", duplicates)
```

### Example Input

```text
Enter a string: programming
```

### Output

```text
Duplicate characters: ['r', 'g', 'm']
```

---

# Program 10: Remove Duplicate Characters

### Code

```python
text = input("Enter a string: ")

result = ""

for char in text:
    if char not in result:
        result += char

print(result)
```

### Example Input

```text
Enter a string: programming
```

### Output

```text
progamin
```

---

# Program 11: Check Anagram

Two strings are anagrams if they contain the same characters with the same frequencies, ignoring order.

### Code

```python
a = input("Enter first string: ")
b = input("Enter second string: ")

if sorted(a.replace(" ", "").lower()) == sorted(b.replace(" ", "").lower()):
    print("Anagram")
else:
    print("Not anagram")
```

### Example Input

```text
Enter first string: listen
Enter second string: silent
```

### Output

```text
Anagram
```

---

# Program 12: Character Frequency

### Code

```python
text = input("Enter a string: ")

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

print(frequency)
```

### Example Input

```text
Enter a string: hello
```

### Output

```text
{'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

---

# Program 13: First Non-Repeating Character

### Code

```python
text = input("Enter a string: ")

for char in text:
    if text.count(char) == 1:
        print("First non-repeating character:", char)
        break
else:
    print("No non-repeating character")
```

### Example Input

```text
Enter a string: swiss
```

### Output

```text
First non-repeating character: w
```

---

# Program 14: Check String Contains Only Digits

### Code

```python
text = input("Enter a value: ")

if text.isdigit():
    print("Contains only digits")
else:
    print("Contains non-digit characters")
```

### Example Input

```text
Enter a value: 12345
```

### Output

```text
Contains only digits
```

---

# Program 15: Convert First Letter of Every Word

### Code

```python
text = input("Enter a sentence: ")

print(text.title())
```

### Example Input

```text
Enter a sentence: python programming language
```

### Output

```text
Python Programming Language
```

---

# Program 16: Longest Word

### Code

```python
text = input("Enter a sentence: ")

words = text.split()

longest = max(words, key=len)

print("Longest word:", longest)
```

### Example Input

```text
Enter a sentence: Python programming is interesting
```

### Output

```text
Longest word: interesting
```

---

# Program 17: Reverse Each Word

### Code

```python
text = input("Enter a sentence: ")

words = text.split()

result = " ".join(word[::-1] for word in words)

print(result)
```

### Example Input

```text
Enter a sentence: Python is easy
```

### Output

```text
nohtyP si ysae
```

---

# Program 18: Check Prefix and Suffix

### Code

```python
filename = input("Enter filename: ")

if filename.startswith("data"):
    print("Starts with data")

if filename.endswith(".csv"):
    print("CSV file")
```

### Example Input

```text
Enter filename: data.csv
```

### Output

```text
Starts with data
CSV file
```

---

# 46. Important Interview/Exam Points

## 1. Are Python strings mutable?

**No.**

Strings are immutable.

---

## 2. What is the string data type?

```python
str
```

---

## 3. What is indexing?

Accessing individual characters using their position.

```python
text[0]
```

---

## 4. What is slicing?

Extracting a portion of a string.

```python
text[start:stop:step]
```

---

## 5. Does slicing include the stop index?

**No.**

```python
text[0:3]
```

accesses indexes:

```text
0, 1, 2
```

---

## 6. What is the first index?

```text
0
```

---

## 7. What is the last negative index?

```text
-1
```

---

## 8. How do you reverse a string?

```python
text[::-1]
```

---

## 9. Difference between `find()` and `index()`

```text
find()  → Returns -1 when not found
index() → Raises ValueError when not found
```

---

## 10. Difference between `split()` and `join()`

```text
split() → String → List
join()  → Iterable of strings → String
```

Example:

```python
text = "a,b,c"

items = text.split(",")

result = "-".join(items)

print(result)
```

### Output

```text
a-b-c
```

---

## 11. Difference between `strip()` and `replace()`

```text
strip()   → Removes characters from the ends
replace() → Replaces matching substrings anywhere
```

---

## 12. Difference between `is` and `==`

```text
== → Compares values
is → Checks object identity
```

For strings, use `==` when you want to compare their contents.

### Code

```python
a = "Python"
b = "Python"

print(a == b)
```

### Output

```text
True
```

---

## 13. Difference between `lower()` and `casefold()`

```text
lower()   → Converts to lowercase
casefold() → Stronger Unicode-aware case normalization
```

Use `casefold()` when doing case-insensitive comparisons where Unicode behavior matters.

---

## 14. Difference between `isalpha()` and `isalnum()`

```text
isalpha() → Letters only
isalnum() → Letters + numbers
```

Example:

```python
print("Python".isalpha())
print("Python123".isalnum())
```

### Output

```text
True
True
```

---

## 15. Difference between `isdigit()`, `isdecimal()`, and `isnumeric()`

```text
isdecimal() → Decimal characters
isdigit()   → Digit characters
isnumeric() → Numeric characters
```

For simple ASCII digits, all three return `True`.

---

# 47. String Operations Summary

| Operation         | Syntax          | Purpose              |
| ----------------- | --------------- | -------------------- |
| Concatenation     | `a + b`         | Joins strings        |
| Repetition        | `a * 3`         | Repeats string       |
| Indexing          | `a[0]`          | Gets character       |
| Negative indexing | `a[-1]`         | Gets from end        |
| Slicing           | `a[1:4]`        | Gets substring       |
| Reverse           | `a[::-1]`       | Reverses string      |
| Membership        | `"a" in text`   | Checks existence     |
| Length            | `len(text)`     | Number of characters |
| Comparison        | `a == b`        | Compares values      |
| Iteration         | `for x in text` | Traverses characters |

---

# 48. String Method Categories

For quick memorization:

### 🔤 Case

```text
capitalize()
casefold()
lower()
upper()
title()
swapcase()
```

### 🔍 Search

```text
find()
rfind()
index()
rindex()
count()
```

### 🔎 Check

```text
startswith()
endswith()
```

### 🧹 Remove

```text
strip()
lstrip()
rstrip()
removeprefix()
removesuffix()
```

### 🔄 Replace

```text
replace()
translate()
```

### ✂️ Split

```text
split()
rsplit()
splitlines()
partition()
rpartition()
```

### 🔗 Join

```text
join()
```

### ✅ Validation

```text
isalnum()
isalpha()
isascii()
isdecimal()
isdigit()
isidentifier()
islower()
isnumeric()
isprintable()
isspace()
istitle()
isupper()
```

### 📐 Alignment

```text
center()
ljust()
rjust()
zfill()
```

### 🔤 Translation / Encoding

```text
maketrans()
translate()
encode()
```

### 📝 Formatting

```text
format()
format_map()
```

---

# 49. String Cheat Sheet

```text
                 PYTHON STRING
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     Creation       Access          Operations
        │              │              │
   'text'           Indexing       +
   "text"           Slicing        *
   '''text'''       [0]            in
   """text"""       [-1]           not in
                                    ==
        │
        └──────────────────────────────┐
                                       │
                                  Methods
                                       │
          ┌────────────┬───────────────┼──────────────┐
          │            │               │              │
        Case         Search          Split          Check
          │            │               │              │
     upper()       find()          split()       isalpha()
     lower()       rfind()         rsplit()      isdigit()
     title()       index()         splitlines()  isalnum()
     capitalize()  rindex()        partition()   isspace()
     swapcase()    count()         rpartition()  isupper()
     casefold()                                  islower()
```

---

# 50. Most Important Syntax to Remember

## Create

```python
text = "Python"
```

## Access

```python
text[0]
```

## Last Character

```python
text[-1]
```

## Slice

```python
text[start:stop:step]
```

## Reverse

```python
text[::-1]
```

## Length

```python
len(text)
```

## Uppercase

```python
text.upper()
```

## Lowercase

```python
text.lower()
```

## Remove Spaces

```python
text.strip()
```

## Replace

```python
text.replace("old", "new")
```

## Search

```python
text.find("Python")
```

## Count

```python
text.count("a")
```

## Split

```python
text.split()
```

## Join

```python
" ".join(words)
```

## Check

```python
text.isalpha()
text.isdigit()
text.isalnum()
```

## Format

```python
f"Hello {name}"
```

---

# 51. Important Things to Remember

### ⭐ Remember these rules

```text
1. Strings are immutable.

2. Indexing starts from 0.

3. Negative indexing starts from -1.

4. Slicing does not include the stop index.

5. Strings support + for concatenation.

6. Strings support * for repetition.

7. Strings support in and not in.

8. len() returns the number of characters.

9. input() returns a string by default.

10. find() returns -1 when not found.

11. index() raises ValueError when not found.

12. split() returns a list.

13. join() creates a string from an iterable of strings.

14. strip() removes characters from the ends.

15. replace() returns a new string.

16. String methods do not modify the original string.

17. f-strings are a modern way to format strings.

18. Python 3 strings are Unicode text.

19. encode() converts str → bytes.

20. decode() converts bytes → str.
```

---

# 🎯 Final Revision Table

| Concept           | Remember              |
| ----------------- | --------------------- |
| Data Type         | `str`                 |
| Mutable?          | ❌ No                  |
| Index Start       | `0`                   |
| Negative Start    | `-1`                  |
| Slice             | `[start:stop:step]`   |
| Reverse           | `[::-1]`              |
| Length            | `len()`               |
| Concatenation     | `+`                   |
| Repetition        | `*`                   |
| Membership        | `in`, `not in`        |
| Search            | `find()`, `index()`   |
| Count             | `count()`             |
| Replace           | `replace()`           |
| Split             | `split()`             |
| Join              | `join()`              |
| Remove Ends       | `strip()`             |
| Uppercase         | `upper()`             |
| Lowercase         | `lower()`             |
| Title Case        | `title()`             |
| Validation        | `is...()` methods     |
| Formatting        | f-string / `format()` |
| Character Code    | `ord()`               |
| Code to Character | `chr()`               |
| String → Bytes    | `encode()`            |
| Bytes → String    | `decode()`            |

---

# 🧠 One-Minute Revision

If you have only one minute before an exam, remember:

```python
# Create
s = "Python"

# Index
s[0]
s[-1]

# Slice
s[1:4]
s[::-1]

# Length
len(s)

# Concatenate
"Hello" + "World"

# Repeat
"Hi " * 3

# Membership
"Py" in s

# Case
s.upper()
s.lower()
s.title()

# Search
s.find("th")
s.index("th")

# Count
s.count("t")

# Replace
s.replace("Python", "Java")

# Split
s.split()

# Join
"-".join(["A", "B", "C"])

# Remove whitespace
s.strip()

# Validation
s.isalpha()
s.isdigit()
s.isalnum()

# Formatting
f"Name: {s}"

# Reverse
s[::-1]

# Unicode
ord("A")
chr(65)

# Encoding
s.encode()

# String type
type(s)
```

---

# 🚀 Final Takeaway

Python strings are one of the most important concepts to master because strings are used everywhere:

```text
User Input
   ↓
Text Processing
   ↓
Searching
   ↓
Validation
   ↓
Data Cleaning
   ↓
File Handling
   ↓
Web Development
   ↓
APIs
   ↓
Data Science
   ↓
Automation
```

If you understand:

```text
Creation
   ↓
Indexing
   ↓
Slicing
   ↓
Immutability
   ↓
Operators
   ↓
Methods
   ↓
Formatting
   ↓
Validation
   ↓
String Programs
```

you have a strong foundation in **Python Strings**.

---

# ⭐ Practice Checklist

Before moving to the next Python topic, make sure you can solve these without looking at the notes:

* [ ] Create strings using different quote styles
* [ ] Access characters using positive indexing
* [ ] Access characters using negative indexing
* [ ] Perform slicing
* [ ] Reverse a string
* [ ] Concatenate strings
* [ ] Repeat strings
* [ ] Check substring membership
* [ ] Compare strings
* [ ] Iterate through a string
* [ ] Find string length
* [ ] Use escape sequences
* [ ] Use raw strings
* [ ] Convert values using `str()`
* [ ] Use case-conversion methods
* [ ] Search using `find()` and `index()`
* [ ] Count characters
* [ ] Use `startswith()` and `endswith()`
* [ ] Remove whitespace
* [ ] Replace text
* [ ] Split a string
* [ ] Join strings
* [ ] Use `partition()`
* [ ] Validate strings with `is...()` methods
* [ ] Align strings
* [ ] Use `zfill()`
* [ ] Use `translate()` and `maketrans()`
* [ ] Encode and decode strings
* [ ] Understand Unicode
* [ ] Use `ord()` and `chr()`
* [ ] Format strings using f-strings
* [ ] Use `format()`
* [ ] Solve palindrome problems
* [ ] Count vowels and consonants
* [ ] Find duplicate characters
* [ ] Check anagrams
* [ ] Count character frequency
* [ ] Find the longest word

---

## 🐍 Keep Practicing

> **Don't just read the string methods — write small programs using each one.**

**Python Strings → Practice → Problems → Confidence 💪**
