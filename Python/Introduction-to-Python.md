Python Programming — Complete Beginner Guide 🐍

A complete beginner-friendly guide to Python programming fundamentals. This README covers Python introduction, features, applications, installation, input/output, variables, data types, type conversion, operators, conditional statements, loops, and jumping statements.

---

📚 Table of Contents

- "1. What is Python?" (#1-what-is-python)
- "2. Features of Python" (#2-features-of-python)
- "3. Applications of Python" (#3-applications-of-python)
- "4. Installing Python" (#4-installing-python)
- "5. First Python Program" (#5-first-python-program)
- "6. Output in Python" (#6-output-in-python)
- "7. Taking Input" (#7-taking-input)
- "8. Comments" (#8-comments)
- "9. Variables" (#9-variables)
- "10. Data Types" (#10-data-types)
- "11. Rules for Variables" (#11-rules-for-variable-names)
- "12. Type Conversion" (#12-type-conversion)
- "13. Operators and Operands" (#13-operators-and-operands)
- "14. Conditional Statements" (#14-conditional-statements)
- "15. Loops" (#15-loops)
- "16. Jumping Statements" (#16-jumping-statements)
- "17. Important Built-in Functions" (#17-important-built-in-functions)
- "18. Common Mistakes" (#18-common-beginner-mistakes)
- "19. Practice Programs" (#19-practice-programs)
- "20. What's Next?" (#20-whats-next)

---

1. What is Python?

Python is a high-level, general-purpose, interpreted programming language.

It was created by Guido van Rossum and first released in 1991.

Python is popular because its syntax is simple, readable, and easy to understand.

Example

print("Hello, World!")

Output:

Hello, World!

Python is used for:

- Web development
- Data Science
- Machine Learning
- Artificial Intelligence
- Automation
- Scripting
- Game development
- Desktop applications
- Cybersecurity
- Scientific computing

---

2. Features of Python

2.1 Easy to Learn

Python has simple and readable syntax.

name = "Alice"
age = 20

print(name)
print(age)

---

2.2 High-Level Language

Python provides high-level abstractions, so programmers do not need to manage low-level computer operations for most tasks.

---

2.3 Interpreted Language

Python code is executed by the Python interpreter.

print("First")
print("Second")
print("Third")

The interpreter executes the program during runtime.

---

2.4 Dynamically Typed

Python does not require us to declare the data type of a variable explicitly.

x = 10

x = "Hello"

The same variable can refer to values of different types at different times.

---

2.5 Object-Oriented

Python supports Object-Oriented Programming concepts such as:

- Classes
- Objects
- Inheritance
- Encapsulation
- Polymorphism

---

2.6 Portable

Python programs can run on different operating systems such as:

- Windows
- Linux
- macOS

---

2.7 Open Source

Python is free to use and its source code is publicly available.

---

2.8 Large Standard Library

Python provides many built-in modules.

Examples:

import math
import random
import datetime

---

2.9 Large Community

Python has a large developer community and many third-party libraries.

Examples:

- NumPy
- Pandas
- Flask
- Django
- TensorFlow
- PyTorch
- OpenCV

---

3. Applications of Python

3.1 Web Development

Popular Python frameworks:

- Django
- Flask
- FastAPI

Example:

from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello Python"

---

3.2 Data Science

Popular libraries:

- NumPy
- Pandas
- Matplotlib

---

3.3 Machine Learning

Popular libraries:

- Scikit-learn
- TensorFlow
- PyTorch

---

3.4 Artificial Intelligence

Python is widely used in:

- Machine Learning
- Deep Learning
- Natural Language Processing
- Computer Vision
- Generative AI

---

3.5 Automation

Python can automate repetitive tasks such as:

- File operations
- Data processing
- Sending emails
- Report generation
- Web automation

---

3.6 Game Development

Libraries such as Pygame can be used for game development.

---

3.7 Desktop Applications

Python can be used to create GUI applications using:

- Tkinter
- PyQt
- Kivy

---

3.8 Cybersecurity

Python can be used for:

- Security automation
- Network programming
- Log analysis
- Security tools

---

4. Installing Python

Step 1: Download Python

Download Python from the official Python website:

https://www.python.org/

---

Step 2: Install Python

On Windows, during installation, make sure to enable:

Add Python to PATH

Then complete the installation.

---

Step 3: Verify Installation

Open Command Prompt or Terminal and run:

python --version

Example output:

Python 3.13.0

On some systems, use:

python3 --version

---

Step 4: Start Python

Run:

python

Then:

print("Hello Python")

---

5. First Python Program

The simplest Python program is:

print("Hello, World!")

Output:

Hello, World!

The "print()" function is used to display information on the screen.

---

6. Output in Python

Python uses the "print()" function to display output.

Basic Output

print("Hello")
print(100)
print(10 + 20)

Output:

Hello
100
30

---

Printing Multiple Values

name = "Alice"
age = 20

print(name, age)

Output:

Alice 20

---

Using "sep"

"sep" specifies the separator between multiple values.

print("Python", "Java", "C++", sep=" | ")

Output:

Python | Java | C++

---

Using "end"

By default, "print()" moves to a new line.

print("Hello")
print("World")

Output:

Hello
World

Using "end":

print("Hello", end=" ")
print("World")

Output:

Hello World

---

7. Taking Input

Python uses the "input()" function to take input from the user.

name = input("Enter your name: ")

print(name)

Example:

Enter your name: Alice
Alice

---

Important: "input()" Returns a String

Consider:

age = input("Enter your age: ")

print(type(age))

Even if the user enters:

20

the type will be:

<class 'str'>

Therefore, convert the input when a number is required.

age = int(input("Enter your age: "))

print(age)

---

Taking Multiple Inputs

a, b = input("Enter two values: ").split()

print(a)
print(b)

For integers:

a, b = map(int, input("Enter two numbers: ").split())

print(a + b)

Input:

10 20

Output:

30

---

8. Comments

Comments are used to explain code.

Python ignores comments during program execution.

Single-Line Comment

Use "#".

# This is a comment

x = 10
print(x)

---

Multiple-Line Documentation

Triple quotes can be used for multi-line strings and documentation.

"""
This is a multi-line string.
It can also be used as a docstring.
"""

For normal comments, using "#" on each line is preferred.

---

9. Variables

A variable is a name that refers to a value.

age = 20
name = "Alice"

Here:

age  → variable
20   → value

---

Assignment Operator

The "=" operator assigns a value to a variable.

x = 10

It means:

Store 10 in x

It does NOT mean mathematical equality.

---

Multiple Assignment

a = b = c = 10

Now all three variables contain "10".

---

Assigning Multiple Values

a, b, c = 10, 20, 30

This is equivalent to:

a = 10
b = 20
c = 30

---

Swapping Variables

Python allows variables to be swapped easily.

a = 10
b = 20

a, b = b, a

print(a)
print(b)

Output:

20
10

---

10. Data Types

A data type defines the type of value stored in a variable.

Python's important built-in data types include:

Data Type| Example
"int"| "10"
"float"| "10.5"
"complex"| "2 + 3j"
"bool"| "True"
"str"| ""Hello""
"list"| "[1, 2, 3]"
"tuple"| "(1, 2, 3)"
"set"| "{1, 2, 3}"
"dict"| "{"name": "Alice"}"
"NoneType"| "None"

---

10.1 Integer

Integers are whole numbers.

x = 100
y = -50

Type:

print(type(x))

Output:

<class 'int'>

---

10.2 Float

Floats represent decimal numbers.

price = 99.99
temperature = 36.5

---

10.3 Complex

Complex numbers contain real and imaginary parts.

z = 2 + 3j

print(z)

---

10.4 Boolean

Boolean values are:

True
False

Example:

is_logged_in = True

print(is_logged_in)

---

10.5 String

A string is a sequence of characters.

name = "Python"

Strings can be written using single or double quotes:

name1 = "Python"
name2 = 'Python'

---

10.6 List

A list stores multiple values.

Lists are mutable, meaning their elements can be changed.

numbers = [10, 20, 30]

numbers[0] = 100

print(numbers)

Output:

[100, 20, 30]

---

10.7 Tuple

A tuple stores multiple values and is immutable.

numbers = (10, 20, 30)

print(numbers)

---

10.8 Set

A set stores unique values.

numbers = {10, 20, 30, 10}

print(numbers)

The duplicate "10" is removed.

---

10.9 Dictionary

A dictionary stores data as key-value pairs.

student = {
    "name": "Alice",
    "age": 20
}

print(student)

Access a value:

print(student["name"])

Output:

Alice

---

10.10 None

"None" represents the absence of a value.

result = None

print(result)

---

11. Rules for Variable Names

Python has specific rules for naming variables.

Rule 1: Must Start With a Letter or Underscore

Valid:

name = "Alice"
_age = 20

Invalid:

2name = "Alice"

---

Rule 2: Cannot Start With a Number

Invalid:

1student = "Alice"

Valid:

student1 = "Alice"

---

Rule 3: Only Letters, Numbers and Underscores

Valid:

student_name = "Alice"
student1 = "Bob"

Invalid:

student-name = "Alice"

---

Rule 4: Cannot Use Python Keywords

Invalid:

if = 10

Python keywords include:

if
else
elif
for
while
break
continue
def
class
return
import
try
except
True
False
None

---

Rule 5: Python is Case-Sensitive

These are different variables:

name = "Alice"
Name = "Bob"
NAME = "Charlie"

---

12. Type Conversion

Type conversion means changing one data type into another.

---

String to Integer

x = "100"

y = int(x)

print(y)
print(type(y))

---

String to Float

x = "10.5"

y = float(x)

print(y)

---

Integer to Float

x = 10

y = float(x)

print(y)

Output:

10.0

---

Float to Integer

x = 10.8

y = int(x)

print(y)

Output:

10

"int()" removes the decimal portion. It does not round the number.

---

Integer to String

x = 100

y = str(x)

print(y)
print(type(y))

---

Boolean Conversion

print(bool(1))
print(bool(0))

Output:

True
False

---

13. Operators and Operands

An operator is a symbol or keyword that performs an operation.

An operand is the value on which the operation is performed.

Example:

10 + 20

Here:

10 and 20 → operands
+         → operator

---

13.1 Arithmetic Operators

Arithmetic operators are used for mathematical operations.

Operator| Meaning| Example
"+"| Addition| "10 + 5"
"-"| Subtraction| "10 - 5"
"*"| Multiplication| "10 * 5"
"/"| Division| "10 / 5"
"//"| Floor Division| "10 // 3"
"%"| Modulus| "10 % 3"
"**"| Exponent| "2 ** 3"

Example:

a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)

Output:

13
7
30
3.3333333333333335
3
1
1000

---

13.2 Comparison Operators

Comparison operators compare two values and return "True" or "False".

Operator| Meaning
"=="| Equal to
"!="| Not equal to
">"| Greater than
"<"| Less than
">="| Greater than or equal to
"<="| Less than or equal to

Example:

a = 10
b = 20

print(a == b)
print(a != b)
print(a < b)
print(a > b)
print(a <= b)
print(a >= b)

---

13.3 Logical Operators

Python has three logical operators:

- "and"
- "or"
- "not"

"and"

Returns "True" only when both conditions are true.

age = 20

print(age >= 18 and age <= 60)

Output:

True

---

"or"

Returns "True" if at least one condition is true.

age = 20

print(age < 18 or age > 60)

Output:

False

---

"not"

Reverses the result.

x = True

print(not x)

Output:

False

---

13.4 Assignment Operators

Assignment operators assign or update values.

Operator| Example| Equivalent
"="| "x = 5"| "x = 5"
"+="| "x += 5"| "x = x + 5"
"-="| "x -= 5"| "x = x - 5"
"*="| "x *= 5"| "x = x * 5"
"/="| "x /= 5"| "x = x / 5"
"//="| "x //= 5"| "x = x // 5"
"%="| "x %= 5"| "x = x % 5"
"**="| "x **= 5"| "x = x ** 5"

Example:

x = 10

x += 5

print(x)

Output:

15

---

13.5 Membership Operators

Membership operators check whether a value exists in a sequence.

Operators:

in
not in

Example:

numbers = [10, 20, 30]

print(20 in numbers)
print(50 not in numbers)

Output:

True
True

---

13.6 Identity Operators

Identity operators check whether two references refer to the same object.

Operators:

is
is not

Example:

x = None

print(x is None)

Output:

True

"==" vs "is"

Use "==" to compare values:

a = 10
b = 10

print(a == b)

Use "is" when checking object identity:

x = None

print(x is None)

---

13.7 Bitwise Operators

Bitwise operators work on binary representations of integers.

Operator| Meaning
"&"| AND
`| `
"^"| XOR
"~"| NOT
"<<"| Left Shift
">>"| Right Shift

Example:

a = 5
b = 3

print(a & b)
print(a | b)
print(a ^ b)

---

13.8 Operator Precedence

When multiple operators are used, Python follows operator precedence.

Example:

result = 10 + 2 * 3

print(result)

Output:

16

Multiplication is performed before addition.

Using parentheses:

result = (10 + 2) * 3

print(result)

Output:

36

A simplified precedence order:

()
**
* / // %
+ -
< > <= >= == !=
not
and
or

---

14. Conditional Statements

Conditional statements are used to make decisions in a program.

Python provides:

- "if"
- "if-else"
- "if-elif-else"
- Nested "if"

---

14.1 "if" Statement

Syntax:

if condition:
    statement

Example:

age = 20

if age >= 18:
    print("Eligible to vote")

Output:

Eligible to vote

Important

Python uses indentation to define a block of code.

---

14.2 "if-else"

Used when there are two possible outcomes.

age = 16

if age >= 18:
    print("Eligible")
else:
    print("Not eligible")

Output:

Not eligible

---

14.3 "if-elif-else"

Used when there are multiple conditions.

marks = 75

if marks >= 90:
    print("A")
elif marks >= 75:
    print("B")
elif marks >= 50:
    print("C")
else:
    print("Fail")

Output:

B

Python checks conditions from top to bottom.

Once a condition becomes "True", the remaining conditions are skipped.

---

14.4 Nested "if"

An "if" statement inside another "if" statement is called a nested "if".

age = 20
citizen = True

if age >= 18:
    if citizen:
        print("Eligible")

---

15. Loops

Loops are used to execute a block of code repeatedly.

Python mainly provides:

1. "for" loop
2. "while" loop

---

15.1 "for" Loop

A "for" loop is used to iterate over a sequence or range.

Example:

for i in range(5):
    print(i)

Output:

0
1
2
3
4

---

Understanding "range()"

The basic syntax is:

range(start, stop, step)

The "stop" value is not included.

---

"range(stop)"

for i in range(5):
    print(i)

Output:

0
1
2
3
4

---

"range(start, stop)"

for i in range(2, 6):
    print(i)

Output:

2
3
4
5

---

"range(start, stop, step)"

for i in range(1, 10, 2):
    print(i)

Output:

1
3
5
7
9

---

Reverse Loop

for i in range(5, 0, -1):
    print(i)

Output:

5
4
3
2
1

---

15.2 Iterating Over a String

name = "Python"

for character in name:
    print(character)

Output:

P
y
t
h
o
n

---

15.3 Iterating Over a List

numbers = [10, 20, 30]

for number in numbers:
    print(number)

Output:

10
20
30

---

15.4 "while" Loop

A "while" loop executes as long as its condition is "True".

Syntax:

while condition:
    statement

Example:

i = 1

while i <= 5:
    print(i)
    i += 1

Output:

1
2
3
4
5

---

Infinite Loop

If the condition never becomes "False", the loop becomes an infinite loop.

Example:

i = 1

while i <= 5:
    print(i)

The value of "i" never changes, so the condition remains "True".

Correct version:

i = 1

while i <= 5:
    print(i)
    i += 1

---

"for" Loop vs "while" Loop

"for"| "while"
Used for iterating over sequences/ranges| Used while a condition is true
Usually used when number of iterations is known| Useful when number of iterations is not known
Works naturally with "range()"| Requires a condition
Example: "for i in range(10)"| Example: "while x < 10"

---

16. Jumping Statements

Jumping statements change the normal flow of execution.

Python provides:

- "break"
- "continue"
- "pass"

---

16.1 "break"

"break" immediately terminates the loop.

Example:

for i in range(1, 10):

    if i == 5:
        break

    print(i)

Output:

1
2
3
4

When "i" becomes "5", the loop stops completely.

---

16.2 "continue"

"continue" skips the current iteration and moves to the next iteration.

Example:

for i in range(1, 6):

    if i == 3:
        continue

    print(i)

Output:

1
2
4
5

The value "3" is skipped.

---

16.3 "pass"

"pass" does nothing.

It is used as a placeholder when a statement is required syntactically but no action is needed yet.

Example:

for i in range(5):
    pass

Another example:

if True:
    pass

---

"break" vs "continue" vs "pass"

Statement| Meaning
"break"| Stop the loop completely
"continue"| Skip the current iteration
"pass"| Do nothing

Easy way to remember:

break     → STOP
continue  → SKIP
pass      → DO NOTHING

---

17. Important Built-in Functions

Python provides many built-in functions.

Some important beginner-level functions are:

Function| Purpose
"print()"| Display output
"input()"| Take input
"type()"| Find data type
"int()"| Convert to integer
"float()"| Convert to float
"str()"| Convert to string
"bool()"| Convert to Boolean
"len()"| Find length
"sum()"| Calculate sum
"max()"| Find maximum
"min()"| Find minimum
"abs()"| Absolute value
"round()"| Round a number
"range()"| Generate a range
"sorted()"| Return sorted values

Example:

numbers = [10, 20, 30, 40]

print(len(numbers))
print(sum(numbers))
print(max(numbers))
print(min(numbers))

Output:

4
100
40
10

---

18. Common Beginner Mistakes

Mistake 1: Using "=" Instead of "=="

Wrong:

if x = 10:
    print("Ten")

Correct:

if x == 10:
    print("Ten")

Remember:

=   → Assignment
==  → Comparison

---

Mistake 2: Forgetting Indentation

Wrong:

if age >= 18:
print("Adult")

Correct:

if age >= 18:
    print("Adult")

---

Mistake 3: Forgetting Input Conversion

Wrong:

a = input()
b = input()

print(a + b)

If the input is:

10
20

Output:

1020

Why?

Because "input()" returns a string.

Correct:

a = int(input())
b = int(input())

print(a + b)

Output:

30

---

Mistake 4: Incorrect "range()" Understanding

range(1, 5)

generates:

1 2 3 4

It does not include "5".

---

Mistake 5: Forgetting to Update a "while" Loop

Wrong:

i = 1

while i <= 5:
    print(i)

Correct:

i = 1

while i <= 5:
    print(i)
    i += 1

---

19. Practice Programs

Try solving these programs yourself.

Beginner Programs

1. Print "Hello Python".
2. Take your name as input and print it.
3. Take two numbers and print their sum.
4. Take two numbers and print their difference.
5. Calculate the area of a circle.
6. Convert Celsius to Fahrenheit.
7. Check whether a number is positive or negative.
8. Check whether a number is even or odd.
9. Find the largest of two numbers.
10. Find the largest of three numbers.
11. Check whether a person is eligible to vote.
12. Check whether a year is a leap year.

---

Loop Programs

13. Print numbers from 1 to 100.
14. Print numbers from 100 to 1.
15. Print all even numbers from 1 to 100.
16. Print all odd numbers from 1 to 100.
17. Print the multiplication table of a number.
18. Find the sum of numbers from 1 to N.
19. Find the factorial of a number.
20. Count the number of digits in a number.
21. Reverse a number.
22. Check whether a number is a palindrome.
23. Check whether a number is prime.
24. Print all prime numbers between two numbers.
25. Find the sum of digits of a number.

---

20. What's Next?

After completing these Python fundamentals, continue learning in this order:

Python Basics
      ↓
Strings
      ↓
Lists
      ↓
Tuples
      ↓
Sets
      ↓
Dictionaries
      ↓
Functions
      ↓
Recursion
      ↓
Lambda Functions
      ↓
List / Set / Dictionary Comprehension
      ↓
Modules and Packages
      ↓
Exception Handling
      ↓
File Handling
      ↓
Object-Oriented Programming
      ↓
Iterators and Generators
      ↓
Decorators
      ↓
Virtual Environments
      ↓
PIP
      ↓
Projects

---

🧠 Quick Revision

Input and Output

print()
input()

Data Types

int
float
complex

