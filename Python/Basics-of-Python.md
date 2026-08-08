🐍 Python Programming — Complete Beginner Guide

A complete beginner-friendly guide to Python fundamentals, covering everything from Python introduction to loops and jumping statements.

---

📌 Table of Contents

1. "What is Python?" (#-what-is-python)
2. "Features of Python" (#-features-of-python)
3. "Applications of Python" (#-applications-of-python)
4. "Installing Python" (#-installing-python)
5. "Writing Your First Python Program" (#-writing-your-first-python-program)
6. "Output in Python" (#-output-in-python)
7. "Taking Input" (#-taking-input)
8. "Comments" (#-comments)
9. "Variables" (#-variables)
10. "Data Types" (#-data-types)
11. "Rules for Naming Variables" (#-rules-for-naming-variables)
12. "Type Conversion" (#-type-conversion)
13. "Operators and Operands" (#-operators-and-operands)
14. "Conditional Statements" (#-conditional-statements)
15. "Loops" (#-loops)
16. "Jumping Statements" (#-jumping-statements)
17. "Important Python Concepts to Remember" (#-important-python-concepts-to-remember)
18. "Common Beginner Mistakes" (#-common-beginner-mistakes)
19. "Practice Questions" (#-practice-questions)

---

🐍 What is Python?

Python is a high-level, interpreted, general-purpose programming language.

It was created by Guido van Rossum and first released in 1991.

Python is designed to be easy to read and write because its syntax is close to the English language.

Example

print("Hello, World!")

Output:

Hello, World!

Instead of writing many lines of complex code, Python allows us to perform tasks with simple and readable syntax.

---

⭐ Features of Python

1. Easy to Learn

Python has simple and readable syntax.

a = 10
b = 20

print(a + b)

---

2. High-Level Language

Python handles many low-level operations internally.

The programmer does not need to manually manage memory in most cases.

---

3. Interpreted Language

Python programs are executed by the Python interpreter.

For example:

print("Hello")
print("Python")

The Python interpreter executes the program during runtime.

---

4. Dynamically Typed

We don't have to explicitly declare the data type of a variable.

x = 10
x = "Hello"

The type of "x" can change during execution.

---

5. Object-Oriented

Python supports object-oriented programming concepts such as:

- Classes
- Objects
- Inheritance
- Polymorphism
- Encapsulation

---

6. Portable

Python programs can generally run on different operating systems with little or no modification.

For example:

- Windows
- Linux
- macOS

---

7. Open Source

Python is free to use and its source code is publicly available.

---

8. Large Standard Library

Python provides many built-in modules and libraries.

Examples:

math
random
datetime
os
sys

---

9. Supports Multiple Programming Paradigms

Python supports:

- Procedural programming
- Object-oriented programming
- Functional programming

---

10. Large Community

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

💻 Applications of Python

Python is used in many areas.

1. Web Development

Frameworks:

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

2. Data Science

Popular libraries:

- NumPy
- Pandas
- Matplotlib
- Seaborn

---

3. Machine Learning

Popular libraries:

- Scikit-learn
- TensorFlow
- PyTorch

---

4. Artificial Intelligence

Python is widely used for:

- Machine learning
- Deep learning
- Natural language processing
- Computer vision
- Generative AI

---

5. Automation

Python can automate repetitive tasks.

For example:

- File handling
- Sending emails
- Data processing
- Web automation

---

6. Game Development

Libraries such as "pygame" can be used to create games.

---

7. Desktop Applications

Libraries such as:

- Tkinter
- PyQt
- Kivy

can be used to create GUI applications.

---

8. Cybersecurity

Python is used for:

- Security automation
- Network programming
- Penetration testing tools
- Log analysis

---

⚙️ Installing Python

Step 1: Download Python

Download Python from the official Python website.

During installation on Windows, make sure to select:

Add Python to PATH

Then continue with the installation.

---

Step 2: Verify Installation

Open Command Prompt or Terminal.

Run:

python --version

You may get output similar to:

Python 3.x.x

On some systems:

python3 --version

---

Step 3: Start Python

You can run:

python

Then try:

print("Hello Python")

---

📝 Writing Your First Python Program

print("Hello, World!")

Output:

Hello, World!

Explanation

"print()" is a built-in Python function used to display information on the screen.

---

📤 Output in Python

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

By default, "print()" moves to the next line.

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

📥 Taking Input

Python uses the "input()" function to take input from the user.

name = input("Enter your name: ")

print(name)

If the user enters:

Alice

Output:

Alice

---

⚠️ Important: "input()" Returns a String

Consider:

age = input("Enter your age: ")

print(type(age))

Even if the user enters:

20

the type will be:

<class 'str'>

Therefore, when we need a number, we usually convert the input.

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

💬 Comments

Comments are messages written inside the code for explanation.

Python ignores comments during execution.

Single-Line Comment

Use "#".

# This is a comment

x = 10
print(x)

---

Multi-Line Comments

Python does not have a dedicated multi-line comment syntax.

Triple-quoted strings are commonly used for documentation or multi-line text.

"""
This is a multi-line
string.
"""

For actual comments, "#" is preferred.

---

📦 Variables

A variable is a name used to refer to a value.

age = 20
name = "Alice"

Here:

age  → variable
20   → value

Another example:

x = 10
y = 20

print(x + y)

Output:

30

---

Variable Assignment

x = 10

The "=" operator assigns the value "10" to "x".

It does not mean mathematical equality.

---

Multiple Assignment

a = b = c = 10

All three variables contain "10".

---

Assigning Different Values

a, b, c = 10, 20, 30

This is equivalent to:

a = 10
b = 20
c = 30

---

Swapping Variables

Python allows easy swapping:

a = 10
b = 20

a, b = b, a

print(a)
print(b)

Output:

20
10

---

🔢 Data Types

A data type tells Python what kind of value a variable contains.

Important built-in data types include:

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

1. Integer — "int"

Whole numbers.

x = 100
y = -50

---

2. Float — "float"

Numbers containing decimal values.

price = 99.99
temperature = 36.5

---

3. Complex — "complex"

Complex numbers contain a real and imaginary part.

z = 2 + 3j

Here:

2 → real part
3j → imaginary part

---

4. Boolean — "bool"

Boolean values are:

True
False

Example:

is_logged_in = True

---

5. String — "str"

A string is a sequence of characters.

name = "Python"

Strings can use:

"Hello"
'Hello'

---

6. List — "list"

Lists store multiple values and are mutable.

numbers = [10, 20, 30]

You can modify them:

numbers[0] = 100

print(numbers)

Output:

[100, 20, 30]

---

7. Tuple — "tuple"

Tuples store multiple values and are immutable.

numbers = (10, 20, 30)

---

8. Set — "set"

Sets store unique values.

numbers = {10, 20, 30, 10}

print(numbers)

Duplicate values are removed.

---

9. Dictionary — "dict"

Dictionaries store data in key-value pairs.

student = {
    "name": "Alice",
    "age": 20
}

Access a value:

print(student["name"])

Output:

Alice

---

10. None

"None" represents the absence of a value.

result = None

---

🔍 Checking Data Type

Use the "type()" function.

x = 10

print(type(x))

Output:

<class 'int'>

Another example:

name = "Python"

print(type(name))

Output:

<class 'str'>

---

📏 Rules for Naming Variables

Python has rules for variable names.

Rule 1: Must start with a letter or underscore

Valid:

name = "Alice"
_age = 20

Invalid:

2name = "Alice"

---

Rule 2: Cannot start with a number

Invalid:

1student = "Alice"

Valid:

student1 = "Alice"

---

Rule 3: Only letters, numbers and underscore are allowed

Valid:

student_name = "Alice"
student1 = "Bob"

Invalid:

student-name = "Alice"

---

Rule 4: Keywords cannot be used

You cannot use Python keywords as variable names.

Invalid:

if = 10

---

Rule 5: Python is Case-Sensitive

These are different variables:

name = "Alice"
Name = "Bob"
NAME = "Charlie"

---

🔄 Type Conversion

Type conversion means changing one data type into another.

---

String to Integer

x = "100"

y = int(x)

print(y)
print(type(y))

---

Integer to Float

x = 10

y = float(x)

print(y)

Output:

10.0

---

Integer to String

x = 100

y = str(x)

print(y)

---

Float to Integer

x = 10.8

y = int(x)

print(y)

Output:

10

Important

"int()" removes the decimal part. It does not round the number.

---

String to Float

x = "10.5"

y = float(x)

print(y)

---

Boolean Conversion

print(bool(1))
print(bool(0))

Output:

True
False

---

➕ Operators and Operands

An operator is a symbol that performs an operation.

An operand is the value on which the operator operates.

Example:

10 + 20

Here:

10 and 20 → operands
+         → operator

---

🧮 Arithmetic Operators

Operator| Meaning| Example
"+"| Addition| "10 + 5"
"-"| Subtraction| "10 - 5"
"*"| Multiplication| "10 * 5"
"/"| Division| "10 / 5"
"//"| Floor Division| "10 // 3"
"%"| Modulus| "10 % 3"
"**"| Exponent| "2 ** 3"

Example

a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)

---

⚖️ Comparison Operators

Comparison operators compare values.

Operator| Meaning
"=="| Equal to
"!="| Not equal
">"| Greater than
"<"| Less than
">="| Greater than or equal
"<="| Less than or equal

Example:

a = 10
b = 20

print(a == b)
print(a < b)
print(a > b)

Output:

False
True
False

---

🧠 Logical Operators

Python provides three logical operators.

"and"

Returns "True" when both conditions are true.

age = 20

print(age >= 18 and age <= 60)

---

"or"

Returns "True" when at least one condition is true.

age = 20

print(age < 18 or age > 60)

---

"not"

Reverses the result.

x = True

print(not x)

Output:

False

---

📝 Assignment Operators

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

---

🔍 Membership Operators

Membership operators check whether a value exists inside a sequence.

numbers = [10, 20, 30]

print(20 in numbers)
print(50 not in numbers)

Output:

True
True

Operators:

in
not in

---

🆔 Identity Operators

Identity operators check whether two references point to the same object.

is
is not

Example:

a = None

print(a is None)

Output:

True

Important

Do not generally use "is" when you want to compare values.

Use:

==

for value comparison.

---

🔢 Operator Precedence

When multiple operators are used, Python follows precedence rules.

Example:

result = 10 + 2 * 3

Multiplication happens first.

10 + (2 * 3)
= 16

Parentheses can be used to control the order:

result = (10 + 2) * 3

Output:

36

A simplified order to remember:

()
**
* / // %
+ -
< > <= >= == !=
not
and
or

---

🔀 Conditional Statements

Conditional statements allow a program to make decisions.

Python mainly provides:

- "if"
- "if-else"
- "if-elif-else"
- Nested "if"

---

1. "if" Statement

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

Python uses indentation to define blocks.

---

2. "if-else"

Used when there are two possible outcomes.

age = 16

if age >= 18:
    print("Eligible")
else:
    print("Not eligible")

Output:

Not eligible

---

3. "if-elif-else"

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

Once a condition is "True", the remaining "elif" and "else" blocks are skipped.

---

4. Nested "if"

An "if" statement inside another "if" statement.

age = 20
citizen = True

if age >= 18:
    if citizen:
        print("Eligible")

---

🔁 Loops

Loops are used when we need to execute a block of code repeatedly.

Python has two main loops:

1. "for"
2. "while"

---

🔢 "for" Loop

A "for" loop is commonly used to iterate over a sequence or a range of values.

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

range(start, stop, step)

Example

range(1, 6)

Generates:

1 2 3 4 5

The "stop" value is not included.

---

Start and Stop

for i in range(2, 6):
    print(i)

Output:

2
3
4
5

---

Step

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

🔄 Iterating Over a String

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

🔄 Iterating Over a List

numbers = [10, 20, 30]

for number in numbers:
    print(number)

---

⏳ "while" Loop

A "while" loop executes as long as a condition is true.

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

⚠️ Infinite Loop

If the condition never becomes false, the loop continues indefinitely.

Example:

i = 1

while i <= 5:
    print(i)

Here "i" never changes, so the condition remains true.

Correct version:

i = 1

while i <= 5:
    print(i)
    i += 1

---

🚦 Jumping Statements

Jumping statements change the normal flow of execution.

Python provides:

- "break"
- "continue"
- "pass"

---

🛑 "break"

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

When "i" becomes "5", the loop stops.

---

⏭️ "continue"

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

"3" is skipped.

---

⏸️ "pass"

"pass" does nothing.

It is used as a placeholder when a statement is syntactically required but you don't want to execute anything yet.

Example:

for i in range(5):
    pass

Another example:

if True:
    pass

---

🔄 "break" vs "continue" vs "pass"

Statement| Purpose
"break"| Stops the loop completely
"continue"| Skips current iteration
"pass"| Does nothing

Easy way to remember

break    → STOP
continue → SKIP
pass     → DO NOTHING

---

🧩 Important Python Concepts to Remember

1. Indentation

Python uses indentation instead of "{}" to define blocks.

Correct:

if age >= 18:
    print("Adult")

Incorrect:

if age >= 18:
print("Adult")

---

2. Colon ":"

A colon is generally required after statements that introduce a block.

Examples:

if condition:

for i in range(5):

while condition:

---

3. Case Sensitivity

Python is case-sensitive.

name = "Alice"
Name = "Bob"

These are different variables.

---

4. No Semicolon Required

Python generally does not require semicolons.

x = 10
y = 20

---

5. Everything is an Object

In Python, values such as integers, strings, lists, functions, and classes are objects.

---

🧮 Basic Example Program

Add Two Numbers

a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

sum = a + b

print("Sum =", sum)

Example:

Enter first number: 10
Enter second number: 20

Sum = 30

---

🎯 Check Whether a Number is Even or Odd

number = int(input("Enter a number: "))

if number % 2 == 0:
    print("Even")
else:
    print("Odd")

---

🎯 Find the Largest of Two Numbers

a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

if a > b:
    print("Largest =", a)
else:
    print("Largest =", b)

---

🔢 Print Numbers from 1 to 10

for i in range(1, 11):
    print(i)

---

✖️ Multiplication Table

number = int(input("Enter a number: "))

for i in range(1, 11):
    print(number, "x", i, "=", number * i)

---

🔢 Sum of Numbers from 1 to N

n = int(input("Enter n: "))

total = 0

for i in range(1, n + 1):
    total += i

print("Sum =", total)

---

🔍 Find Whether a Number is Positive, Negative or Zero

number = int(input("Enter a number: "))

if number > 0:
    print("Positive")
elif number < 0:
    print("Negative")
else:
    print("Zero")

---

❌ Common Beginner Mistakes

Mistake 1: Using "=" instead of "=="

Wrong:

if x = 10:

Correct:

if x == 10:

Remember:

=   → assignment
==  → comparison

---

Mistake 2: Forgetting indentation

Wrong:

if x > 10:
print(x)

Correct:

if x > 10:
    print(x)

---

Mistake 3: Forgetting to convert input

Wrong:

a = input()
b = input()

print(a + b)

If input is:

10
20

Output:

1020

Why?

Because "input()" returns strings.

Correct:

a = int(input())
b = int(input())

print(a + b)

Output:

30

---

Mistake 4: Incorrect range understanding

range(1, 5)

does not generate:

1 2 3 4 5

It generates:

1 2 3 4

The ending value is excluded.

---

🧠 Quick Revision

Python

High-level
Interpreted
Dynamically typed
Object-oriented
Portable
Open-source

Output

print()

Input

input()

Type

type()

Type Conversion

int()
float()
str()
bool()

Conditions

if
elif
else

Loops

for
while

Jump Statements

break
continue
pass

Important Operators

Arithmetic
+
-
*
/
//
%
**

Comparison
==
!=
>
<
>=
<=

Logical
and
or
not

Assignment
=
+=
-=
*=
/=
%=

Membership
in
not in

Identity
is
is not

---

📝 Practice Questions

Try solving these without looking at the solution.

Beginner

1. Print ""Hello Python"".
2. Take your name as input and print it.
3. Take two numbers and print their sum.
4. Find the area of a circle.
5. Convert Celsius to Fahrenheit.
6. Check whether a number is positive or negative.
7. Check whether a number is even or odd.
8. Find the largest of two numbers.
9. Find the largest of three numbers.
10. Check whether a person is eligible to vote.

Loops

11. Print numbers from 1 to 100.
12. Print even numbers from 1 to 100.
13. Print odd numbers from 1 to 100.
14. Print the multiplication table of a number.
15. Find the sum of numbers from 1 to N.
16. Find the factorial of a number.
17. Count the number of digits in a number.
18. Reverse a number.
19. Check whether a number is a palindrome.
20. Check whether a number is prime.

---

🚀 Recommended Learning Order

If you are completely new to Python, learn in this order:

1. Python Introduction
       ↓
2. Installation
       ↓
3. print()
       ↓
4. input()
       ↓
5. Comments
       ↓
6. Variables
       ↓
7. Data Types
       ↓
8. Type Conversion
       ↓
9. Operators
       ↓
10. if / elif / else
       ↓
11. for Loop
       ↓
12. while Loop
       ↓
13. break / continue / pass
       ↓
14. Strings
       ↓
15. Lists
       ↓
16. Tuples
       ↓
17. Sets
       ↓
18. Dictionaries
       ↓
19. Functions
       ↓
20. Modules
       ↓
21. E
