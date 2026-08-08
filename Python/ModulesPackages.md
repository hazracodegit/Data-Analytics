# 🐍 Python Modules and Packages — Complete Revision Notes

Modules and packages are used to **organize, reuse, and maintain Python code**.

Instead of writing an entire application in one file, Python allows us to divide code into:

```text
Module
   ↓
A single .py file

Package
   ↓
A directory containing related modules
```

---

# 📚 Table of Contents

1. [What is a Module?](#-what-is-a-module)
2. [Why Use Modules?](#-why-use-modules)
3. [Creating a Module](#-creating-a-module)
4. [Importing a Module](#-importing-a-module)
5. [Accessing Module Members](#-accessing-module-members)
6. [import Statement](#-import-statement)
7. [from import](#-from-import)
8. [Import Multiple Members](#-import-multiple-members)
9. [import as Alias](#-import-as-alias)
10. [from import as](#-from-import-as)
11. [Built-in Modules](#-built-in-modules)
12. [Important Python Standard Library Modules](#-important-python-standard-library-modules)
13. [dir() Function](#-dir-function)
14. [help() Function](#-help-function)
15. [Module Attributes](#-module-attributes)
16. [**name**](#-name)
17. [**main**](#-main)
18. [if **name** == "**main**"](#-if-name--main)
19. [Module Search Path](#-module-search-path)
20. [sys.path](#-syspath)
21. [What is a Package?](#-what-is-a-package)
22. [Creating a Package](#-creating-a-package)
23. [Importing from a Package](#-importing-from-a-package)
24. [Subpackages](#-subpackages)
25. [**init**.py](#-initpy)
26. [Package Initialization](#-package-initialization)
27. [Absolute Imports](#-absolute-imports)
28. [Relative Imports](#-relative-imports)
29. [Importing a Module from Another Module](#-importing-a-module-from-another-module)
30. [Wildcard Import](#-wildcard-import)
31. [Circular Imports](#-circular-imports)
32. [Standard Library vs Third-Party Packages](#-standard-library-vs-third-party-packages)
33. [pip](#-pip)
34. [Installing Packages](#-installing-packages)
35. [requirements.txt](#-requirementstxt)
36. [Virtual Environments](#-virtual-environments)
37. [Package Structure](#-package-structure)
38. [Creating a Reusable Package](#-creating-a-reusable-package)
39. [Namespace Packages](#-namespace-packages)
40. [Common Import Errors](#-common-import-errors)
41. [Best Practices](#-best-practices)
42. [Interview Questions](#-interview-questions)
43. [Practice Programs](#-practice-programs)
44. [Quick Revision](#-quick-revision)

---

# 📦 What is a Module?

A **module** is a Python file containing code such as:

* Variables
* Functions
* Classes
* Statements
* Constants

A module normally has the `.py` extension.

Example:

```text
math_utils.py
```

Contents:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b
```

Now `math_utils.py` is a module.

---

# 🎯 Why Use Modules?

Modules provide:

### 1. Code Reusability

Write code once and use it in multiple programs.

### 2. Organization

Large programs can be divided into smaller files.

### 3. Maintainability

It is easier to update and debug smaller modules.

### 4. Namespace Management

Modules help prevent naming conflicts.

### 5. Collaboration

Different developers can work on different modules.

---

# 🏗️ Creating a Module

Create a file:

```text
calculator.py
```

Add:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


PI = 3.14159
```

Now another Python file can import this module.

---

# 📥 Importing a Module

Suppose we have:

```text
project/
│
├── calculator.py
└── main.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`main.py`:

```python
import calculator

result = calculator.add(10, 20)

print(result)
```

Output:

```text
30
```

---

# 🔑 Accessing Module Members

Use the dot `.` operator.

```python
import calculator

print(calculator.add(10, 20))
```

If the module contains:

```python
PI = 3.14
```

Access it:

```python
import calculator

print(calculator.PI)
```

---

# 📌 import Statement

Basic syntax:

```python
import module_name
```

Example:

```python
import math

print(math.sqrt(25))
```

Output:

```text
5.0
```

---

# 📥 from import

Instead of importing the entire module namespace, specific members can be imported.

```python
from math import sqrt

print(sqrt(25))
```

You can also import multiple members:

```python
from math import sqrt, pi

print(sqrt(25))
print(pi)
```

---

# 🔢 Import Multiple Members

```python
from math import sqrt, pow, factorial

print(sqrt(16))
print(pow(2, 3))
print(factorial(5))
```

---

# 🏷️ import as Alias

An alias gives a module another name.

```python
import math as m

print(m.sqrt(25))
```

Output:

```text
5.0
```

This is useful when:

* Module names are long
* You want a shorter name
* A conventional alias exists

Example:

```python
import datetime as dt

print(dt.datetime.now())
```

---

# 🏷️ from import as

You can also give an imported member an alias.

```python
from math import sqrt as square_root

print(square_root(25))
```

Output:

```text
5.0
```

---

# 📚 Built-in Modules

Python provides a large **standard library** containing modules that can be used without installing third-party packages.

Examples:

```python
import math
import random
import os
import sys
import datetime
import json
import re
```

---

# 🧰 Important Python Standard Library Modules

| Module        | Purpose                           |
| ------------- | --------------------------------- |
| `math`        | Mathematical functions            |
| `random`      | Random numbers and selections     |
| `os`          | Operating-system interfaces       |
| `sys`         | Python runtime/system information |
| `datetime`    | Date and time                     |
| `time`        | Time-related functions            |
| `json`        | JSON processing                   |
| `re`          | Regular expressions               |
| `statistics`  | Statistical calculations          |
| `collections` | Specialized container types       |
| `itertools`   | Iterator tools                    |
| `functools`   | Higher-order functions            |
| `pathlib`     | Object-oriented filesystem paths  |
| `csv`         | CSV file handling                 |
| `sqlite3`     | SQLite database                   |
| `logging`     | Application logging               |
| `random`      | Random operations                 |
| `decimal`     | Decimal arithmetic                |
| `fractions`   | Rational numbers                  |
| `subprocess`  | Running subprocesses              |
| `urllib`      | URL handling                      |

---

# 🧮 math Module

```python
import math

print(math.sqrt(16))
print(math.pi)
print(math.ceil(4.2))
print(math.floor(4.8))
```

Output:

```text
4.0
3.141592653589793
5
4
```

---

# 🎲 random Module

```python
import random

print(random.randint(1, 10))
```

Choose a random item:

```python
import random

colors = ["red", "green", "blue"]

print(random.choice(colors))
```

---

# 📁 os Module

```python
import os

print(os.getcwd())
```

Create a directory:

```python
import os

os.mkdir("demo")
```

Check whether a file exists:

```python
import os

print(os.path.exists("data.txt"))
```

---

# 🖥️ sys Module

```python
import sys

print(sys.version)
```

Command-line arguments:

```python
import sys

print(sys.argv)
```

If executed as:

```text
python main.py hello
```

`sys.argv` contains the command-line arguments.

---

# 📅 datetime Module

```python
from datetime import datetime

now = datetime.now()

print(now)
```

Date:

```python
from datetime import date

today = date.today()

print(today)
```

---

# 🔍 dir() Function

`dir()` returns names available in an object/module.

Example:

```python
import math

print(dir(math))
```

It can help discover available functions, classes, constants, and attributes.

---

# ❓ help() Function

`help()` displays documentation.

```python
import math

help(math)
```

You can also ask about a particular function:

```python
help(math.sqrt)
```

---

# 🔍 Module Attributes

Modules have special attributes.

Example:

```python
import math

print(math.__name__)
```

Output:

```text
math
```

Other useful attributes include:

```python
__name__
__doc__
__file__
__package__
__spec__
```

---

# ⭐ **name**

Every Python module has a special variable:

```python
__name__
```

When a file is imported, `__name__` normally contains the module's import name.

Example:

```python
# calculator.py

print(__name__)
```

If imported:

```python
import calculator
```

Output:

```text
calculator
```

---

# 🚀 **main**

When Python executes a file directly, its:

```python
__name__
```

is:

```text
__main__
```

Example:

```python
print(__name__)
```

If you execute:

```text
python test.py
```

Output:

```text
__main__
```

---

# 🛡️ if **name** == "**main**"

This is one of the most important concepts in Python modules.

Example:

```python
def add(a, b):
    return a + b


if __name__ == "__main__":
    print(add(10, 20))
```

If you run the file directly:

```text
python calculator.py
```

The code inside:

```python
if __name__ == "__main__":
```

runs.

If another file imports it:

```python
import calculator
```

the block does not run.

---

# 🎯 Why Use `if __name__ == "__main__"`?

It allows a Python file to work as both:

```text
Reusable module
       +
Standalone program
```

Example:

```python
def greet(name):
    return f"Hello, {name}"


if __name__ == "__main__":
    name = input("Enter name: ")
    print(greet(name))
```

---

# 🛣️ Module Search Path

When you write:

```python
import mymodule
```

Python searches for the module in locations specified by its import system.

One important source of search locations is:

```python
sys.path
```

---

# 🧭 sys.path

```python
import sys

for path in sys.path:
    print(path)
```

It displays paths Python searches when importing modules.

---

# 📦 What is a Package?

A **package** is a way of organizing related Python modules into a directory structure.

Example:

```text
my_package/
│
├── __init__.py
├── calculator.py
├── geometry.py
└── conversion.py
```

Here:

```text
my_package
```

is the package.

The files:

```text
calculator.py
geometry.py
conversion.py
```

are modules.

---

# 🧠 Module vs Package

| Module                          | Package                                |
| ------------------------------- | -------------------------------------- |
| Usually a single `.py` file     | Usually a directory of related modules |
| Contains functions/classes/etc. | Organizes multiple modules/subpackages |
| Example: `math_utils.py`        | Example: `utilities/`                  |
| Smaller unit                    | Larger organizational unit             |

Think:

```text
Package
   │
   ├── Module
   ├── Module
   └── Module
```

---

# 🏗️ Creating a Package

Suppose we create:

```text
project/
│
├── main.py
│
└── utilities/
    ├── __init__.py
    ├── calculator.py
    └── converter.py
```

---

# 📄 calculator.py

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b
```

---

# 📄 converter.py

```python
def km_to_miles(km):
    return km * 0.621371


def miles_to_km(miles):
    return miles / 0.621371
```

---

# 📥 Importing from a Package

In `main.py`:

```python
from utilities import calculator

print(calculator.add(10, 20))
```

Output:

```text
30
```

---

# 📥 Import Specific Function from Package Module

```python
from utilities.calculator import add

print(add(10, 20))
```

---

# 📥 Import Multiple Functions

```python
from utilities.calculator import add, subtract

print(add(10, 20))
print(subtract(20, 5))
```

---

# 📦 Import Module Using Package Name

```python
import utilities.calculator

print(utilities.calculator.add(10, 20))
```

---

# 🪆 Subpackages

A package can contain other packages.

Example:

```text
project/
│
├── main.py
│
└── application/
    ├── __init__.py
    │
    ├── math/
    │   ├── __init__.py
    │   ├── basic.py
    │   └── advanced.py
    │
    └── user/
        ├── __init__.py
        └── account.py
```

Here:

```text
application
    ↓
    ├── math
    │     ↓
    │   modules
    │
    └── user
          ↓
        modules
```

---

# 📄 Importing from a Subpackage

```python
from application.math.basic import add

print(add(10, 20))
```

---

# 📄 **init**.py

`__init__.py` is a special file associated with Python packages.

Example:

```text
utilities/
│
├── __init__.py
├── calculator.py
└── converter.py
```

It can be empty:

```python
# __init__.py
```

It can also contain package initialization code or expose selected package members.

---

# 🧠 Is **init**.py Always Required?

Modern Python supports **namespace packages**, so a directory can participate in a package without an `__init__.py` in certain situations.

However, for learning, conventional package design, and explicit package initialization, you will frequently see:

```text
__init__.py
```

It is still very common and useful.

---

# ⚙️ Package Initialization

`__init__.py` can expose selected functions.

Example:

```text
utilities/
│
├── __init__.py
└── calculator.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`__init__.py`:

```python
from .calculator import add
```

Now:

```python
from utilities import add

print(add(10, 20))
```

---

# 🔗 Absolute Imports

An absolute import specifies the package/module path from the top-level package context.

Example:

```python
from utilities.calculator import add
```

This is an absolute-style import.

---

# 🔗 Relative Imports

Relative imports use dots to refer to the current package hierarchy.

Example:

```python
from .calculator import add
```

Meaning:

```text
. = current package
```

Another example:

```python
from .submodule import function
```

---

# 🪜 Relative Import Levels

```text
.       → current package
..      → parent package
...     → parent of parent
```

Example:

```python
from ..utils import helper
```

This refers to a module in the parent package hierarchy.

---

# 📥 Importing One Module from Another

Suppose:

```text
project/
│
├── main.py
├── calculator.py
└── geometry.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`geometry.py`:

```python
import calculator

print(calculator.add(10, 20))
```

---

# ⚠️ Wildcard Import

You can write:

```python
from math import *
```

This imports many names from the module into the current namespace.

Example:

```python
from math import *

print(sqrt(25))
print(pi)
```

### Why is it generally discouraged?

It can:

* Pollute the namespace
* Make code harder to understand
* Cause naming conflicts
* Make it unclear where names came from

Prefer:

```python
import math

print(math.sqrt(25))
```

or:

```python
from math import sqrt

print(sqrt(25))
```

---

# 🔄 Circular Imports

A circular import happens when modules depend on each other.

Example:

```text
module_a
   ↓
module_b
   ↓
module_a
```

Example:

```python
# a.py

import b
```

```python
# b.py

import a
```

This can cause import problems and partially initialized modules.

### How to Avoid Circular Imports

* Improve module organization
* Move shared functionality to a third module
* Reduce unnecessary dependencies
* Import locally only when appropriate

Better structure:

```text
a.py ─────┐
          ↓
       common.py
          ↑
          │
b.py ─────┘
```

---

# 📚 Standard Library vs Third-Party Packages

Python libraries can broadly be categorized as:

```text
Python Ecosystem
│
├── Standard Library
│      ↓
│   Comes with Python
│
└── Third-Party Packages
       ↓
    Installed separately
```

---

# 🏛️ Standard Library

Examples:

```python
import math
import os
import json
import datetime
```

No separate package installation is normally required.

---

# 🌐 Third-Party Packages

Third-party packages are created outside the Python standard library.

Examples include:

```text
requests
numpy
pandas
flask
django
pytest
```

These generally need to be installed separately.

---

# 📦 What is pip?

`pip` is the standard package installer commonly used to install Python packages from the Python Package Index (PyPI).

Check pip:

```bash
python -m pip --version
```

---

# 📥 Installing a Package

Example:

```bash
python -m pip install requests
```

Another:

```bash
python -m pip install numpy
```

Using:

```bash
python -m pip
```

is often preferable because it clearly associates pip with the Python interpreter you selected.

---

# ⬆️ Upgrade a Package

```bash
python -m pip install --upgrade requests
```

---

# 🗑️ Uninstall a Package

```bash
python -m pip uninstall requests
```

---

# 📋 Show Installed Packages

```bash
python -m pip list
```

---

# 🔎 Show Package Information

```bash
python -m pip show requests
```

---

# 📦 requirements.txt

`requirements.txt` is commonly used to record project dependencies.

Example:

```text
requests
numpy
pandas
```

Install them:

```bash
python -m pip install -r requirements.txt
```

You can also pin versions:

```text
requests==2.32.4
```

This helps make environments more reproducible.

---

# 🔒 Virtual Environments

A virtual environment creates an isolated Python environment for a project.

Example:

```bash
python -m venv .venv
```

---

# ▶️ Activating Virtual Environment

## Windows CMD

```bash
.venv\Scripts\activate
```

## Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

## macOS/Linux

```bash
source .venv/bin/activate
```

After activation, install packages:

```bash
python -m pip install requests
```

---

# ❌ Deactivating Virtual Environment

```bash
deactivate
```

---

# 🎯 Why Use Virtual Environments?

Suppose:

```text
Project A → requests version A
Project B → requests version B
```

Installing everything globally can create conflicts.

Virtual environments isolate project dependencies:

```text
System Python
│
├── Project A
│   └── .venv
│       └── dependencies
│
└── Project B
    └── .venv
        └── dependencies
```

---

# 🏗️ Professional Project Structure

A simple Python project may look like:

```text
my_project/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── main.py
│
└── app/
    ├── __init__.py
    ├── calculator.py
    ├── database.py
    └── utils.py
```

---

# 🏢 Larger Project Structure

A larger application can be organized as:

```text
my_project/
│
├── README.md
├── pyproject.toml
├── .gitignore
│
├── src/
│   └── my_package/
│       ├── __init__.py
│       ├── main.py
│       │
│       ├── models/
│       │   ├── __init__.py
│       │   └── user.py
│       │
│       ├── services/
│       │   ├── __init__.py
│       │   └── user_service.py
│       │
│       └── utils/
│           ├── __init__.py
│           └── helpers.py
│
└── tests/
    ├── test_user.py
    └── test_utils.py
```

---

# 📦 Creating a Reusable Package

Suppose:

```text
calculator_package/
│
├── pyproject.toml
└── src/
    └── calculator/
        ├── __init__.py
        └── operations.py
```

`operations.py`:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b
```

`__init__.py`:

```python
from .operations import add, subtract
```

Users can then write:

```python
from calculator import add

print(add(10, 20))
```

---

# ⚙️ pyproject.toml

Modern Python packaging commonly uses:

```text
pyproject.toml
```

to define project/build configuration and package metadata.

A simple example:

```toml
[build-system]
requires = ["setuptools>=61"]
build-backend = "setuptools.build_meta"

[project]
name = "my-calculator"
version = "1.0.0"
description = "A simple calculator package"
```

The exact configuration depends on the packaging tool and project structure.

---

# 🌐 Namespace Packages

A namespace package allows a package namespace to be spread across multiple directories/distributions.

Unlike traditional packages, a namespace package can exist without an `__init__.py` at the namespace level.

Conceptually:

```text
company/
    project_a/
    project_b/
```

Both can contribute to the same namespace under appropriate packaging/import configuration.

For most beginner and normal application projects, a regular package with `__init__.py` is simpler.

---

# ❌ Common Import Errors

## ModuleNotFoundError

Occurs when Python cannot find the requested module.

```python
import something_that_does_not_exist
```

Possible result:

```text
ModuleNotFoundError
```

---

# ❌ ImportError

Occurs when an import cannot be completed, for example when a requested name cannot be imported.

```python
from math import something_that_does_not_exist
```

This can produce:

```text
ImportError
```

---

# ❌ AttributeError

The module exists, but the requested attribute doesn't.

```python
import math

print(math.unknown_function())
```

Possible result:

```text
AttributeError
```

---

# 🐛 Debugging Import Problems

Check:

```python
import sys

print(sys.path)
```

Check module location:

```python
import math

print(math.__file__)
```

Check module members:

```python
import math

print(dir(math))
```

---

# ⚠️ Naming Conflicts

Avoid naming your own file after an important standard library or third-party module.

For example, don't create:

```text
random.py
```

and then expect:

```python
import random
```

to always refer to Python's standard-library `random` module.

Your local file may shadow the intended module.

Other problematic names include:

```text
math.py
json.py
os.py
typing.py
email.py
```

---

# 🧠 Module Caching

Once a module is imported, Python generally caches the loaded module in:

```python
sys.modules
```

Example:

```python
import sys

import math

print("math" in sys.modules)
```

Output:

```text
True
```

This helps avoid repeatedly loading the same module during a process.

---

# 🔄 Reloading a Module

Python provides:

```python
import importlib
```

You can reload an already imported module:

```python
import calculator
import importlib

importlib.reload(calculator)
```

This is mainly useful in development and interactive environments.

---

# 📌 Import Once

Consider:

```python
import math
import math
```

The module isn't normally loaded from scratch each time. Python's import system uses its module cache.

---

# 🧩 Module Namespace

A module provides its own namespace.

Example:

```python
# calculator.py

x = 100
```

Another file:

```python
import calculator

x = 500

print(x)
print(calculator.x)
```

Output:

```text
500
100
```

The two `x` names belong to different namespaces.

---

# 🎯 Why Modules Prevent Naming Conflicts

Without modules:

```python
x = 10
x = 20
```

The second assignment replaces the first.

With modules:

```python
module1.x
module2.x
```

Both can exist independently.

---

# 🧠 Import Styles Comparison

### Style 1

```python
import math

math.sqrt(25)
```

**Advantage:** clear where `sqrt` came from.

---

### Style 2

```python
from math import sqrt

sqrt(25)
```

**Advantage:** shorter.

---

### Style 3

```python
import math as m

m.sqrt(25)
```

**Advantage:** convenient alias.

---

### Style 4

```python
from math import *
```

Generally avoid because it can make the namespace unclear.

---

# 📊 Import Comparison

| Syntax                             | Example                      | Recommendation    |
| ---------------------------------- | ---------------------------- | ----------------- |
| `import module`                    | `import math`                | ⭐ Recommended     |
| `from module import name`          | `from math import sqrt`      | ⭐ Good            |
| `import module as alias`           | `import numpy as np`         | ⭐ Good            |
| `from module import name as alias` | `from math import sqrt as s` | Sometimes useful  |
| `from module import *`             | `from math import *`         | ❌ Generally avoid |

---

# 🧪 Complete Example

Project:

```text
calculator_project/
│
├── main.py
│
└── calculator/
    ├── __init__.py
    ├── basic.py
    └── advanced.py
```

---

## basic.py

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def multiply(a, b):
    return a * b


def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")

    return a / b
```

---

## advanced.py

```python
def square(number):
    return number ** 2


def cube(number):
    return number ** 3
```

---

## **init**.py

```python
from .basic import add, subtract, multiply, divide
from .advanced import square, cube
```

---

## main.py

```python
from calculator import (
    add,
    subtract,
    multiply,
    divide,
    square,
    cube
)

print(add(10, 20))
print(subtract(20, 5))
print(multiply(5, 4))
print(divide(20, 5))

print(square(5))
print(cube(3))
```

Output:

```text
30
15
20
4.0
25
27
```

---

# 🧠 Module vs Package vs Library vs Framework

These terms are often confused.

## Module

A reusable Python file.

```text
calculator.py
```

---

## Package

A collection/organization of related modules.

```text
calculator/
├── __init__.py
├── basic.py
└── advanced.py
```

---

## Library

A broader collection of reusable code that provides functionality to applications.

A library may consist of many packages and modules.

Examples:

```text
NumPy
Requests
Pandas
```

---

## Framework

A larger software structure that provides an application architecture and often controls the flow of your application.

Examples:

```text
Django
Flask
```

The distinction between "library" and "framework" can depend on context, but the common idea is:

```text
Module
   ↓
Package
   ↓
Library
   ↓
Application
```

A framework is more about providing the structure and execution model for an application.

---

# 🔥 Real-World Organization

A web application might look like:

```text
my_app/
│
├── main.py
│
├── models/
│   ├── __init__.py
│   ├── user.py
│   └── product.py
│
├── services/
│   ├── __init__.py
│   ├── auth.py
│   └── payment.py
│
├── database/
│   ├── __init__.py
│   └── connection.py
│
└── utils/
    ├── __init__.py
    ├── validation.py
    └── helpers.py
```

This organization makes large applications easier to understand and maintain.

---

# 🛠️ Best Practices

## 1. Give Modules Meaningful Names

Good:

```text
database.py
calculator.py
authentication.py
```

Avoid unclear names:

```text
abc.py
test123.py
stuff.py
```

unless appropriate for a temporary/internal purpose.

---

## 2. Keep Modules Focused

A module should generally have a clear responsibility.

Instead of:

```text
everything.py
```

prefer:

```text
database.py
authentication.py
validation.py
email.py
```

---

## 3. Avoid Circular Imports

Design dependencies carefully.

---

## 4. Avoid Wildcard Imports

Prefer:

```python
import math

math.sqrt(25)
```

instead of:

```python
from math import *
```

---

## 5. Use Meaningful Aliases

Common conventions can improve readability:

```python
import numpy as np
import pandas as pd
```

Don't use confusing aliases unnecessarily.

---

## 6. Use `if __name__ == "__main__"`

For modules that can also be executed directly:

```python
def main():
    print("Program started")


if __name__ == "__main__":
    main()
```

---

## 7. Use Virtual Environments

Keep project dependencies isolated.

```bash
python -m venv .venv
```

---

## 8. Track Dependencies

Use a dependency file such as:

```text
requirements.txt
```

or modern project metadata in:

```text
pyproject.toml
```

---

# 🎯 Interview Questions

## 1. What is a module?

A module is a Python file containing reusable code such as functions, classes, and variables.

---

## 2. What is a package?

A package is a way to organize related Python modules into a directory hierarchy.

---

## 3. How do you import a module?

```python
import math
```

---

## 4. How do you import a specific function?

```python
from math import sqrt
```

---

## 5. What is an alias?

An alternate name for an imported module or member.

```python
import math as m
```

---

## 6. What is `__name__`?

`__name__` is a special module variable that identifies the module's execution/import context.

When a file is run directly:

```python
__name__ == "__main__"
```

---

## 7. Why use `if __name__ == "__main__"`?

To execute certain code only when the file is run directly rather than imported.

---

## 8. What is `__init__.py`?

It is a special file traditionally used to mark and initialize regular Python packages and can expose package-level names.

---

## 9. What is `sys.path`?

It contains paths that Python uses as part of its module import search process.

---

## 10. What is pip?

`pip` is a package installer commonly used to install Python packages.

---

## 11. What is a virtual environment?

An isolated Python environment with its own installed dependencies.

---

## 12. What is `requirements.txt`?

A file commonly used to specify project dependencies.

---

## 13. What is a circular import?

When modules directly or indirectly depend on each other during import.

Example:

```text
A → B → A
```

---

## 14. Difference between `import module` and `from module import name`?

```python
import math

math.sqrt(25)
```

keeps the module namespace explicit.

Whereas:

```python
from math import sqrt

sqrt(25)
```

imports `sqrt` directly into the current namespace.

---

## 15. Why avoid `from module import *`?

It can pollute the namespace and make it unclear where names originated.

---

# 🧪 Practice Programs

## Beginner

1. Create a calculator module.
2. Create a module containing arithmetic functions.
3. Import functions from another file.
4. Use aliases with modules.
5. Use the `math` module.
6. Use the `random` module.
7. Use the `datetime` module.
8. Use `dir()` on a module.
9. Use `help()` on a module.
10. Display `__name__`.

---

## Intermediate

11. Create a utilities package.
12. Create a calculator package.
13. Create separate modules for addition and subtraction.
14. Create a package for unit conversion.
15. Create a package for student management.
16. Create a package for banking operations.
17. Use `__init__.py` to expose functions.
18. Use relative imports.
19. Create and use subpackages.
20. Create a project with `requirements.txt`.

---

## Advanced

21. Create a reusable Python package.
22. Add package metadata using `pyproject.toml`.
23. Create multiple custom modules.
24. Build a package with subpackages.
25. Design a project without circular imports.
26. Create a package with tests.
27. Create a package and install it into a virtual environment.
28. Build a command-line application using modules.
29. Build a multi-module banking application.
30. Build a multi-package student management system.

---

# 🚀 Mini Project — Student Management Package

Project structure:

```text
student_project/
│
├── main.py
│
└── student/
    ├── __init__.py
    ├── student.py
    ├── validation.py
    └── report.py
```

---

## student.py

```python
class Student:

    def __init__(self, name, age, marks):
        self.name = name
        self.age = age
        self.marks = marks

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)
        print("Marks:", self.marks)
```

---

## validation.py

```python
def validate_marks(marks):

    if marks < 0 or marks > 100:
        raise ValueError("Marks must be between 0 and 100")

    return True
```

---

## report.py

```python
def get_grade(marks):

    if marks >= 90:
        return "A"

    elif marks >= 75:
        return "B"

    elif marks >= 60:
        return "C"

    elif marks >= 40:
        return "D"

    return "F"
```

---

## **init**.py

```python
from .student import Student
from .validation import validate_marks
from .report import get_grade
```

---

## main.py

```python
from student import Student
from student import validate_marks
from student import get_grade


try:
    name = input("Enter student name: ")
    age = int(input("Enter age: "))
    marks = float(input("Enter marks: "))

    validate_marks(marks)

    student = Student(name, age, marks)

    student.display()

    print("Grade:", get_grade(marks))

except ValueError as error:
    print("Error:", error)
```

This demonstrates:

```text
Package
   ↓
Modules
   ↓
Classes
   ↓
Functions
   ↓
Imports
   ↓
Exception Handling
```

---

# 🧠 Complete Mental Map

```text
                    PYTHON CODE ORGANIZATION
                              │
             ┌────────────────┴────────────────┐
             │                                 │
          MODULE                            PACKAGE
             │                                 │
        .py file                       Directory structure
             │                                 │
      ┌──────┼──────┐                  ┌───────┼───────┐
      │      │      │                  │       │       │
   Functions Classes Variables      Module  Module  Subpackage
             │                                 │
             └────────────────┬────────────────┘
                              │
                           IMPORT
                              │
              ┌───────────────┼───────────────┐
              │               │               │
           import          from import      alias
              │               │               │
              └───────────────┼───────────────┘
                              │
                       Third-party packages
                              │
                             pip
                              │
                       Virtual environment
                              │
                         requirements.txt
                              │
                        pyproject.toml
```

---

# ⭐ Quick Revision

```text
MODULE
→ A Python file containing reusable code.

PACKAGE
→ A directory structure used to organize related modules.

IMPORT
→ Used to access code from another module/package.

import module
→ Imports a module.

from module import name
→ Imports a specific name.

import module as alias
→ Gives a module an alternate name.

__name__
→ Special module variable.

__main__
→ Value of __name__ when the file is executed directly.

if __name__ == "__main__":
→ Runs code only when the file is executed directly.

__init__.py
→ Common package initialization/interface file.

sys.path
→ Import search path information.

dir()
→ Shows names available in an object/module.

help()
→ Displays documentation.

pip
→ Installs Python packages.

requirements.txt
→ Records project dependencies.

venv
→ Creates an isolated environment.

Absolute import
→ Import using the full package path.

Relative import
→ Import using . and .. within a package.

Circular import
→ Modules depend on each other during import.

Wildcard import
→ from module import *
→ Generally avoid.

Module
→ Single reusable unit.

Package
→ Organized collection of modules.

Library
→ Larger collection of reusable functionality.

Framework
→ Provides an application structure/execution model.
```

---

# 🏁 One-Line Memory Trick

```text
Module  → One .py file
Package → Collection/organization of modules
Import  → Bring code into another module
pip     → Install packages
venv    → Isolate dependencies
__name__ → Identify execution/import context
__main__ → File is running directly
```

### Most important syntax to remember:

```python
# Import module
import math

# Import specific member
from math import sqrt

# Alias
import math as m

# Package import
from utilities.calculator import add

# Relative import
from .calculator import add

# Main check
if __name__ == "__main__":
    main()
```

---

# 🎓 Final Revision Checklist

Before considering **Modules and Packages** complete, make sure you understand:

* [ ] What is a module?
* [ ] Why modules are used
* [ ] How to create a module
* [ ] `import`
* [ ] `from ... import`
* [ ] Import aliases
* [ ] Multiple imports
* [ ] Built-in modules
* [ ] Standard library
* [ ] `dir()`
* [ ] `help()`
* [ ] Module namespace
* [ ] `__name__`
* [ ] `__main__`
* [ ] `if __name__ == "__main__"`
* [ ] Module search path
* [ ] `sys.path`
* [ ] What is a package?
* [ ] Creating packages
* [ ] `__init__.py`
* [ ] Package initialization
* [ ] Importing from packages
* [ ] Subpackages
* [ ] Absolute imports
* [ ] Relative imports
* [ ] Wildcard imports
* [ ] Circular imports
* [ ] Module caching
* [ ] `sys.modules`
* [ ] `importlib.reload()`
* [ ] Standard vs third-party packages
* [ ] `pip`
* [ ] Installing packages
* [ ] `requirements.txt`
* [ ] Virtual environments
* [ ] `pyproject.toml`
* [ ] Basic package structure
* [ ] Reusable packages
* [ ] Namespace packages
* [ ] Import errors
* [ ] Module naming conflicts
* [ ] Module/package best practices

**If you understand all of the above, you have a strong foundation in Python Modules and Packages.**
