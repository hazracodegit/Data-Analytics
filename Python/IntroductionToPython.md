# 🐍 Python Programming – Introduction & Fundamentals

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Beginner Friendly](https://img.shields.io/badge/Level-Beginner-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

A beginner-friendly introduction to **Python programming**, covering Python's history, features, applications, installation, syntax, variables, data types, operators, conditional statements, loops, and jumping statements.

---

## 📚 Table of Contents

* [Introduction](#-introduction)
* [Features of Python](#-features-of-python)
* [Applications of Python](#-applications-of-python)
* [Installation](#-installation)
* [Python Version](#-python-version)
* [History of Python](#-history-of-python)
* [First Python Program](#-first-python-program)
* [Taking Input](#-taking-input)
* [Displaying Output](#-displaying-output)
* [Variables](#-variables)
* [Keywords](#-keywords)
* [Data Types](#-data-types)
* [Type Conversion](#-type-conversion)
* [Operators and Operands](#-operators-and-operands)
* [Conditional Statements](#-conditional-statements)
* [Looping Statements](#-looping-statements)
* [Jumping Statements](#-jumping-statements)
* [Conclusion](#-conclusion)

---

# 🐍 Introduction

**Python** is a high-level, interpreted, general-purpose programming language known for its simple syntax and readability.

Python allows developers to write programs using fewer lines of code compared with many other programming languages.

### Example

```python
print("Hello, World!")
```

Output:

```text
Hello, World!
```

Python is widely used by beginners as well as professional developers.

---

# ✨ Features of Python

Some important features of Python are:

* 🟢 **Easy to learn** – Python has simple and readable syntax.
* 🟢 **Easy to understand** – Programs look close to natural language.
* 🟢 **Interpreted** – Python code is executed by the Python interpreter.
* 🟢 **High-level language** – Developers do not need to manage low-level memory operations directly.
* 🟢 **Object-oriented** – Supports classes and objects.
* 🟢 **Dynamically typed** – Variable types are determined at runtime.
* 🟢 **Portable** – Python programs can run on different operating systems.
* 🟢 **Open source** – Python is freely available.
* 🟢 **Large standard library** – Provides many built-in modules.
* 🟢 **Extensible** – Python can work with code written in languages such as C and C++.
* 🟢 **Large community** – There are many libraries, tutorials, and learning resources available.

---

# 💻 Applications of Python

Python is used in many areas of software development and technology.

### 1. 🌐 Web Development

Frameworks such as:

* Django
* Flask
* FastAPI

are commonly used for building web applications and APIs.

### 2. 🤖 Artificial Intelligence

Python is widely used for:

* Machine Learning
* Deep Learning
* Natural Language Processing
* Computer Vision

Popular libraries include:

* NumPy
* Pandas
* Scikit-learn
* TensorFlow
* PyTorch

### 3. 📊 Data Science

Python is commonly used for:

* Data analysis
* Data visualization
* Statistical analysis
* Data processing

### 4. ⚙️ Automation

Python can automate repetitive tasks such as:

* File handling
* Data processing
* Report generation
* Web tasks
* System administration

### 5. 🎮 Game Development

Python can be used to create simple games using libraries such as `pygame`.

### 6. 🖥️ Desktop Applications

Python supports GUI application development using libraries such as:

* Tkinter
* PyQt
* Kivy

### 7. 🔐 Cybersecurity

Python is used for security automation, network programming, security testing, and analysis.

---

# 📥 Installation

## Windows

1. Download Python from the official Python website.
2. Run the installer.
3. Enable **Add Python to PATH** during installation.
4. Click **Install Now**.
5. Open Command Prompt and verify the installation.

```bash
python --version
```

or:

```bash
py --version
```

## Linux

Many Linux distributions include Python.

Check the installed version:

```bash
python3 --version
```

If Python is not installed, use your distribution's package manager.

For Ubuntu/Debian:

```bash
sudo apt update
sudo apt install python3
```

## macOS

Check whether Python 3 is available:

```bash
python3 --version
```

Python can also be installed using the official installer or a package manager such as Homebrew.

---

# 🔢 Python Version

Python has two major historical branches:

* **Python 2**
* **Python 3**

Python 2 reached its official end of life in **2020**.

For new projects, use **Python 3**.

Check your installed version:

```bash
python --version
```

Example:

```text
Python 3.x.x
```

The exact current Python 3 release should be checked from the official Python release information before specifying it in a project README.

---

# 📜 History of Python

Python was created by **Guido van Rossum**.

### Important milestones

| Year  | Event                                   |
| ----- | --------------------------------------- |
| 1989  | Python development began                |
| 1991  | Python was first publicly released      |
| 2000  | Python 2.0 was released                 |
| 2008  | Python 3.0 was released                 |
| 2020  | Python 2 officially reached end of life |
| Today | Python 3 continues to evolve            |

The name **Python** was inspired by the British comedy group **Monty Python**, rather than the snake.

---

# 👋 First Python Program

The traditional first Python program is:

```python
print("Hello, World!")
```

Output:

```text
Hello, World!
```

The `print()` function is used to display information on the screen.

---

# ⌨️ Taking Input

Python uses the `input()` function to take input from the user.

### Example

```python
name = input("Enter your name: ")

print("Hello", name)
```

Example output:

```text
Enter your name: Rahul
Hello Rahul
```

By default, `input()` returns the entered value as a **string**.

### Taking an Integer

```python
age = int(input("Enter your age: "))

print(age)
```

### Taking a Floating-Point Number

```python
price = float(input("Enter the price: "))

print(price)
```

### Taking Multiple Values

```python
a, b = input("Enter two numbers: ").split()

print(a)
print(b)
```

To convert them to integers:

```python
a, b = map(int, input("Enter two numbers: ").split())

print(a + b)
```

---

# 🖥️ Displaying Output

The `print()` function is used to display output.

### Basic Example

```python
print("Welcome to Python")
```

### Printing Multiple Values

```python
name = "Alice"
age = 20

print(name, age)
```

Output:

```text
Alice 20
```

### Using f-strings

f-strings provide a convenient way to insert variables into strings.

```python
name = "Alice"
age = 20

print(f"My name is {name} and I am {age} years old.")
```

Output:

```text
My name is Alice and I am 20 years old.
```

---

# 📦 Variables

A **variable** is a name used to store a value.

Python does not require you to explicitly declare the variable type.

### Example

```python
name = "John"
age = 25
salary = 45000.50
```

Here:

* `name` contains a string.
* `age` contains an integer.
* `salary` contains a floating-point number.

### Variable Naming Rules

A variable name:

* Can contain letters, numbers, and underscores.
* Cannot start with a number.
* Cannot contain spaces.
* Cannot be a Python keyword.
* Is case-sensitive.

### Valid Names

```python
name = "John"
student_age = 20
total_marks = 450
```

### Invalid Names

```python
# 1name = "John"       # Invalid
# student age = 20    # Invalid
# class = "Python"    # Invalid keyword
```

Python is case-sensitive:

```python
name = "John"
Name = "Alice"
```

`name` and `Name` are different variables.

---

# 🔑 Keywords

**Keywords** are reserved words that have special meaning in Python.

Examples include:

```text
False
None
True
and
as
assert
async
await
break
case
class
continue
def
del
elif
else
except
finally
for
from
global
if
import
in
is
lambda
match
nonlocal
not
or
pass
raise
return
try
while
with
yield
```

You can use Python's `keyword` module to see the keywords available in your installed version:

```python
import keyword

print(keyword.kwlist)
```

---

# 🧮 Data Types

A **data type** defines the kind of value stored by an object.

Python has several built-in data types.

## 1. Integer (`int`)

Used for whole numbers.

```python
age = 20
marks = 95

print(type(age))
```

Output:

```text
<class 'int'>
```

---

## 2. Float (`float`)

Used for decimal numbers.

```python
price = 99.50

print(type(price))
```

---

## 3. Complex (`complex`)

Used for complex numbers.

```python
number = 3 + 4j

print(number)
```

---

## 4. String (`str`)

Used for text.

```python
name = "Python"

print(name)
```

---

## 5. Boolean (`bool`)

Contains either `True` or `False`.

```python
is_student = True

print(is_student)
```

---

## 6. List (`list`)

A list is an ordered and mutable collection.

```python
numbers = [10, 20, 30, 40]

print(numbers)
```

You can modify a list:

```python
numbers[0] = 100

print(numbers)
```

---

## 7. Tuple (`tuple`)

A tuple is an ordered and immutable collection.

```python
numbers = (10, 20, 30)

print(numbers)
```

---

## 8. Set (`set`)

A set is an unordered collection of unique elements.

```python
numbers = {10, 20, 30, 20}

print(numbers)
```

Duplicate values are removed.

---

## 9. Dictionary (`dict`)

A dictionary stores data as **key-value pairs**.

```python
student = {
    "name": "John",
    "age": 20,
    "marks": 85
}

print(student)
```

Access a value:

```python
print(student["name"])
```

---

## 10. None (`NoneType`)

`None` represents the absence of a value.

```python
result = None

print(result)
```

---

# 🔄 Type Conversion

**Type conversion** means converting a value from one data type to another.

## String to Integer

```python
x = "100"

number = int(x)

print(number)
print(type(number))
```

## Integer to Float

```python
x = 10

y = float(x)

print(y)
```

## Integer to String

```python
x = 100

y = str(x)

print(y)
print(type(y))
```

## Float to Integer

```python
x = 10.75

y = int(x)

print(y)
```

Output:

```text
10
```

The fractional part is discarded.

## String to Float

```python
price = "99.50"

price = float(price)

print(price)
```

### Common Conversion Functions

| Function  | Conversion                 |
| --------- | -------------------------- |
| `int()`   | Converts to integer        |
| `float()` | Converts to floating-point |
| `str()`   | Converts to string         |
| `bool()`  | Converts to Boolean        |
| `list()`  | Converts to list           |
| `tuple()` | Converts to tuple          |
| `set()`   | Converts to set            |

---

# ➕ Operators and Operands

An **operator** is a symbol or keyword used to perform an operation.

An **operand** is the value on which the operator operates.

Example:

```python
a + b
```

Here:

* `+` → Operator
* `a` and `b` → Operands

---

## 1. Arithmetic Operators

| Operator | Meaning        | Example   |
| -------- | -------------- | --------- |
| `+`      | Addition       | `10 + 5`  |
| `-`      | Subtraction    | `10 - 5`  |
| `*`      | Multiplication | `10 * 5`  |
| `/`      | Division       | `10 / 5`  |
| `//`     | Floor division | `10 // 3` |
| `%`      | Modulus        | `10 % 3`  |
| `**`     | Exponentiation | `2 ** 3`  |

Example:

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

---

## 2. Comparison Operators

Comparison operators return `True` or `False`.

| Operator | Meaning                  |
| -------- | ------------------------ |
| `==`     | Equal to                 |
| `!=`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

Example:

```python
a = 10
b = 20

print(a == b)
print(a < b)
print(a != b)
```

---

## 3. Logical Operators

| Operator | Meaning                                |
| -------- | -------------------------------------- |
| `and`    | True if both conditions are true       |
| `or`     | True if at least one condition is true |
| `not`    | Reverses a Boolean result              |

Example:

```python
age = 20
has_id = True

print(age >= 18 and has_id)
```

---

## 4. Assignment Operators

| Operator | Example   |
| -------- | --------- |
| `=`      | `x = 10`  |
| `+=`     | `x += 5`  |
| `-=`     | `x -= 5`  |
| `*=`     | `x *= 5`  |
| `/=`     | `x /= 5`  |
| `//=`    | `x //= 5` |
| `%=`     | `x %= 5`  |
| `**=`    | `x **= 2` |

Example:

```python
x = 10

x += 5

print(x)
```

Output:

```text
15
```

---

## 5. Membership Operators

Membership operators check whether a value exists in a sequence or collection.

```python
numbers = [10, 20, 30]

print(20 in numbers)
print(50 not in numbers)
```

Operators:

```text
in
not in
```

---

## 6. Identity Operators

Identity operators compare whether two references refer to the same object.

```python
a = [1, 2, 3]
b = a

print(a is b)
print(a is not b)
```

Operators:

```text
is
is not
```

---

# 🔀 Conditional Statements

Conditional statements are used to make decisions in a program.

Python provides:

* `if`
* `elif`
* `else`
* `match` / `case` for structural pattern matching

---

## 1. if Statement

```python
age = 20

if age >= 18:
    print("You are an adult.")
```

---

## 2. if-else Statement

```python
age = 16

if age >= 18:
    print("Eligible to vote")
else:
    print("Not eligible to vote")
```

---

## 3. if-elif-else Statement

```python
marks = 85

if marks >= 90:
    print("Grade A+")
elif marks >= 80:
    print("Grade A")
elif marks >= 70:
    print("Grade B")
else:
    print("Grade C")
```

---

## 4. Nested if

An `if` statement can be placed inside another `if` statement.

```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("Entry allowed")
```

---

## 5. Conditional Expression

Python supports a short form of `if-else`.

```python
age = 20

result = "Adult" if age >= 18 else "Minor"

print(result)
```

---

# 🔁 Looping Statements

Loops are used to execute a block of code repeatedly.

Python mainly provides:

* `for` loop
* `while` loop

---

# 1. for Loop

A `for` loop is used to iterate over a sequence or iterable.

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

### Iterating Through a List

```python
fruits = ["Apple", "Banana", "Mango"]

for fruit in fruits:
    print(fruit)
```

---

## range()

The `range()` function is commonly used with `for` loops.

```python
for i in range(1, 6):
    print(i)
```

Output:

```text
1
2
3
4
5
```

Syntax:

```python
range(start, stop, step)
```

Example:

```python
for i in range(2, 11, 2):
    print(i)
```

Output:

```text
2
4
6
8
10
```

---

# 2. while Loop

A `while` loop executes as long as its condition is true.

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

Output:

```text
1
2
3
4
5
```

### Infinite Loop

Be careful when using `while` loops.

```python
while True:
    print("Running...")
```

This loop continues indefinitely unless it is interrupted or contains logic to exit.

---

# 🛑 Jumping Statements

Jumping statements change the normal flow of program execution.

The main jumping/control-flow statements are:

* `break`
* `continue`
* `pass`
* `return`

---

## 1. break

The `break` statement immediately terminates the nearest loop.

```python
for i in range(1, 10):
    if i == 5:
        break

    print(i)
```

Output:

```text
1
2
3
4
```

---

## 2. continue

The `continue` statement skips the remaining code in the current iteration and moves to the next iteration.

```python
for i in range(1, 6):
    if i == 3:
        continue

    print(i)
```

Output:

```text
1
2
4
5
```

---

## 3. pass

The `pass` statement does nothing.

It is useful as a placeholder when a statement is syntactically required but you do not want to execute any code yet.

```python
for i in range(5):
    pass
```

Example:

```python
def my_function():
    pass
```

---

## 4. return

The `return` statement is used inside a function to send a value back to the caller and end that function's execution.

```python
def add(a, b):
    return a + b

result = add(10, 20)

print(result)
```

Output:

```text
30
```

---

# 📝 Complete Beginner Example

The following program combines several Python concepts:

```python
name = input("Enter your name: ")
marks = float(input("Enter your marks: "))

if marks >= 90:
    grade = "A+"
elif marks >= 80:
    grade = "A"
elif marks >= 70:
    grade = "B"
elif marks >= 60:
    grade = "C"
else:
    grade = "D"

print(f"\nStudent Name: {name}")
print(f"Marks: {marks}")
print(f"Grade: {grade}")
```

Example:

```text
Enter your name: Rahul
Enter your marks: 85

Student Name: Rahul
Marks: 85.0
Grade: A
```

---

# 📌 Quick Reference

| Topic           | Example                  |
| --------------- | ------------------------ |
| Output          | `print("Hello")`         |
| Input           | `input("Enter value: ")` |
| Variable        | `name = "John"`          |
| Integer         | `age = 20`               |
| Float           | `price = 10.5`           |
| String          | `name = "Python"`        |
| Boolean         | `is_valid = True`        |
| List            | `[1, 2, 3]`              |
| Tuple           | `(1, 2, 3)`              |
| Set             | `{1, 2, 3}`              |
| Dictionary      | `{"name": "John"}`       |
| Type conversion | `int("10")`              |
| Condition       | `if age >= 18:`          |
| for loop        | `for i in range(5):`     |
| while loop      | `while x < 5:`           |
| Break           | `break`                  |
| Continue        | `continue`               |
| Placeholder     | `pass`                   |
| Return          | `return value`           |

---

# 🚀 How to Run a Python Program

Create a file named:

```text
hello.py
```

Add:

```python
print("Hello, Python!")
```

Run it from the terminal:

```bash
python hello.py
```

On some systems, use:

```bash
python3 hello.py
```

---

# 🎯 Learning Roadmap

After learning these fundamentals, you can continue with:

1. Functions
2. Modules and Packages
3. File Handling
4. Exception Handling
5. Object-Oriented Programming
6. List Comprehensions
7. Iterators and Generators
8. Decorators
9. Virtual Environments
10. Database Connectivity
11. Web Development
12. Data Science
13. Machine Learning
14. APIs and Automation

---

# 📚 Conclusion

Python is a powerful and beginner-friendly programming language. Its simple syntax, extensive ecosystem, and broad range of applications make it an excellent language for learning programming and developing real-world software.

Start with the fundamentals:

```text
Variables
   ↓
Data Types
   ↓
Input & Output
   ↓
Operators
   ↓
Conditions
   ↓
Loops
   ↓
Functions
   ↓
Object-Oriented Programming
   ↓
Real-World Projects
```

Happy Coding! 🐍💻

---

## ⭐ Support

If this README helped you learn Python, consider giving the repository a ⭐ on GitHub.

**Keep Learning • Keep Building • Keep Coding 🚀**
