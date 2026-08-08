# 🐍 Python File Handling — Complete Revision Notes

File handling in Python is used to **create, open, read, write, update, and delete files**.

Python provides built-in functions and methods to work with files without requiring external libraries.

---

# 📚 Table of Contents

1. [What is File Handling?](#-what-is-file-handling)
2. [Why File Handling?](#-why-file-handling)
3. [Types of Files](#-types-of-files)
4. [File Handling Workflow](#-file-handling-workflow)
5. [Opening a File](#-opening-a-file)
6. [File Modes](#-file-modes)
7. [Closing a File](#-closing-a-file)
8. [Reading Files](#-reading-files)
9. [Writing to Files](#-writing-to-files)
10. [Appending to Files](#-appending-to-files)
11. [Reading and Writing Together](#-reading-and-writing-together)
12. [File Object](#-file-object)
13. [File Methods](#-important-file-methods)
14. [File Pointer](#-file-pointer)
15. [seek() and tell()](#-seek-and-tell)
16. [with Statement](#-with-statement)
17. [Working with Text Files](#-working-with-text-files)
18. [Encoding](#-encoding)
19. [Reading Line by Line](#-reading-line-by-line)
20. [Writing Multiple Lines](#-writing-multiple-lines)
21. [CSV Files](#-csv-files)
22. [JSON Files](#-json-files)
23. [Binary Files](#-binary-files)
24. [File and Directory Operations](#-file-and-directory-operations)
25. [Renaming Files](#-renaming-files)
26. [Deleting Files](#-deleting-files)
27. [Checking File Existence](#-checking-file-existence)
28. [Exception Handling](#-exception-handling-with-files)
29. [Common Errors](#-common-file-handling-errors)
30. [Important Differences](#-important-differences)
31. [Best Practices](#-best-practices)
32. [Quick Revision](#-quick-revision)
33. [Practice Programs](#-practice-programs)

---

# 📌 What is File Handling?

**File handling** means performing operations on files using a programming language.

Using Python, we can:

* Create files
* Open files
* Read files
* Write files
* Append data
* Update files
* Rename files
* Delete files
* Work with text files
* Work with binary files
* Work with CSV files
* Work with JSON files

Example:

```python
file = open("data.txt", "r")

content = file.read()

print(content)

file.close()
```

---

# 🎯 Why File Handling?

Normally, variables store data temporarily in memory.

```python
name = "John"
age = 25
```

When the program terminates, this data is lost.

Files allow us to **store data permanently**.

```text
Program
   ↓
Data
   ↓
File
   ↓
Stored permanently
```

Example:

```python
name = input("Enter your name: ")

with open("user.txt", "w") as file:
    file.write(name)
```

The name is stored inside `user.txt`.

---

# 📂 Types of Files

There are two major types of files:

```text
Files
│
├── Text Files
│
└── Binary Files
```

## 1. Text Files

Text files contain human-readable characters.

Examples:

```text
.txt
.csv
.json
.html
.py
.xml
```

Example:

```text
name=John
age=25
```

---

## 2. Binary Files

Binary files store data in binary format.

Examples:

```text
.jpg
.png
.mp3
.mp4
.pdf
.exe
```

Binary files are not normally readable directly as text.

---

# 🔄 File Handling Workflow

The basic file-handling process is:

```text
Open
  ↓
Read / Write / Append
  ↓
Close
```

Example:

```python
file = open("data.txt", "r")

data = file.read()

print(data)

file.close()
```

Using `with` is generally preferred:

```python
with open("data.txt", "r") as file:
    data = file.read()

print(data)
```

---

# 📂 Opening a File

Python uses the built-in `open()` function.

### Syntax

```python
open(filename, mode)
```

Example:

```python
file = open("data.txt", "r")
```

Here:

```text
data.txt → File name
r        → File mode
file     → File object
```

---

## 🔹 Full Syntax

```python
open(file, mode="r", buffering=-1, encoding=None, errors=None, newline=None, closefd=True)
```

For most beginner programs, you mainly need:

```python
open("filename", "mode")
```

or:

```python
open("filename", "mode", encoding="utf-8")
```

---

# 🔑 File Modes

File modes determine what operation Python performs on a file.

| Mode | Meaning       |
| ---- | ------------- |
| `r`  | Read          |
| `w`  | Write         |
| `a`  | Append        |
| `x`  | Create        |
| `r+` | Read + Write  |
| `w+` | Write + Read  |
| `a+` | Append + Read |
| `b`  | Binary mode   |
| `t`  | Text mode     |

---

# 📖 `r` — Read Mode

Used to read an existing file.

```python
file = open("data.txt", "r")

print(file.read())

file.close()
```

If the file does not exist:

```text
FileNotFoundError
```

---

# ✍️ `w` — Write Mode

Used to write data to a file.

```python
file = open("data.txt", "w")

file.write("Hello Python")

file.close()
```

### ⚠️ Important

If the file already exists, `w` mode **overwrites the existing contents**.

Suppose the file contains:

```text
Hello
Python
```

Then:

```python
file = open("data.txt", "w")
file.write("Welcome")
file.close()
```

The file becomes:

```text
Welcome
```

The old content is removed.

---

# ➕ `a` — Append Mode

Used to add data at the end of an existing file.

```python
file = open("data.txt", "a")

file.write("Python")

file.close()
```

Existing content is preserved.

Example:

Before:

```text
Hello
```

After:

```text
Hello
Python
```

---

# 🆕 `x` — Create Mode

Used to create a new file.

```python
file = open("newfile.txt", "x")

file.write("Hello")

file.close()
```

If the file already exists:

```text
FileExistsError
```

---

# 🔄 `r+` — Read + Write

Allows both reading and writing.

```python
file = open("data.txt", "r+")

print(file.read())

file.write("Hello")

file.close()
```

The file must already exist.

---

# 🔄 `w+` — Write + Read

Allows writing and reading.

```python
file = open("data.txt", "w+")

file.write("Hello Python")

file.seek(0)

print(file.read())

file.close()
```

⚠️ Existing content is deleted when opening in `w+`.

---

# 🔄 `a+` — Append + Read

Allows appending and reading.

```python
file = open("data.txt", "a+")

file.write("New Line")

file.seek(0)

print(file.read())

file.close()
```

Existing content is preserved.

---

# 🧱 Binary Mode

Add `b` to the mode.

Examples:

```python
open("image.jpg", "rb")
```

```python
open("image.jpg", "wb")
```

Common binary modes:

| Mode  | Meaning              |
| ----- | -------------------- |
| `rb`  | Read binary          |
| `wb`  | Write binary         |
| `ab`  | Append binary        |
| `rb+` | Read + Write binary  |
| `wb+` | Write + Read binary  |
| `ab+` | Append + Read binary |

---

# 📝 Text Mode

Text mode is the default.

```python
file = open("data.txt", "rt")
```

Usually we simply write:

```python
file = open("data.txt", "r")
```

Because `t` is the default.

---

# ❌ Closing a File

After working with a file, it should be closed.

```python
file = open("data.txt", "r")

data = file.read()

print(data)

file.close()
```

Check whether the file is closed:

```python
print(file.closed)
```

Output:

```text
True
```

---

# 📖 Reading Files

Python provides several ways to read files.

Main methods:

```text
read()
readline()
readlines()
```

---

# 1️⃣ `read()`

Reads the entire file.

Suppose `data.txt` contains:

```text
Hello
Welcome to Python
File Handling
```

Code:

```python
with open("data.txt", "r") as file:
    data = file.read()

print(data)
```

Output:

```text
Hello
Welcome to Python
File Handling
```

---

## Reading Specific Number of Characters

```python
with open("data.txt", "r") as file:
    data = file.read(5)

print(data)
```

If the file begins with:

```text
Hello Python
```

Output:

```text
Hello
```

---

# 2️⃣ `readline()`

Reads one line at a time.

```python
with open("data.txt", "r") as file:
    line = file.readline()

print(line)
```

To read multiple lines:

```python
with open("data.txt", "r") as file:
    print(file.readline())
    print(file.readline())
    print(file.readline())
```

---

# 3️⃣ `readlines()`

Reads all lines and returns them as a list.

```python
with open("data.txt", "r") as file:
    lines = file.readlines()

print(lines)
```

Example output:

```python
['Hello\n', 'Python\n', 'File Handling\n']
```

---

# 🔁 Reading Using a Loop

A file can be directly iterated using a `for` loop.

```python
with open("data.txt", "r") as file:
    for line in file:
        print(line)
```

To remove extra newline characters:

```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

This is memory-efficient for large files.

---

# ✍️ Writing to Files

The `write()` method writes a string to a file.

```python
with open("data.txt", "w") as file:
    file.write("Hello Python")
```

---

# 📝 Writing Multiple Lines

```python
with open("data.txt", "w") as file:
    file.write("Python\n")
    file.write("Java\n")
    file.write("C++\n")
```

File content:

```text
Python
Java
C++
```

---

# 📋 `writelines()`

`writelines()` writes multiple strings.

```python
lines = [
    "Python\n",
    "Java\n",
    "C++\n"
]

with open("data.txt", "w") as file:
    file.writelines(lines)
```

### Important

`writelines()` does **not automatically add `\n`**.

This:

```python
lines = ["Python", "Java", "C++"]

with open("data.txt", "w") as file:
    file.writelines(lines)
```

produces:

```text
PythonJavaC++
```

So use:

```python
lines = ["Python\n", "Java\n", "C++\n"]
```

---

# ➕ Appending Data

Use `a` mode.

```python
with open("data.txt", "a") as file:
    file.write("\nNew Content")
```

Example:

Before:

```text
Python
Java
```

After:

```text
Python
Java
New Content
```

---

# 🔄 Reading and Writing Together

## Using `r+`

```python
with open("data.txt", "r+") as file:
    data = file.read()
    print(data)

    file.write("\nNew Data")
```

---

## Using `w+`

```python
with open("data.txt", "w+") as file:
    file.write("Hello Python")

    file.seek(0)

    print(file.read())
```

---

## Using `a+`

```python
with open("data.txt", "a+") as file:
    file.write("\nNew Data")

    file.seek(0)

    print(file.read())
```

---

# 🧩 File Object

When we use:

```python
file = open("data.txt", "r")
```

`file` is a **file object**.

We can use its methods:

```python
file.read()
file.readline()
file.readlines()
file.write()
file.writelines()
file.seek()
file.tell()
file.close()
```

---

# 🛠️ Important File Methods

| Method         | Purpose                      |
| -------------- | ---------------------------- |
| `read()`       | Read entire file             |
| `read(n)`      | Read `n` characters/bytes    |
| `readline()`   | Read one line                |
| `readlines()`  | Read all lines as list       |
| `write()`      | Write a string               |
| `writelines()` | Write multiple strings       |
| `seek()`       | Move file pointer            |
| `tell()`       | Return file pointer position |
| `flush()`      | Flush buffered data          |
| `close()`      | Close file                   |

---

# 📍 File Pointer

A file pointer represents the current position in a file.

Suppose:

```text
Python
```

Initially:

```text
|Python
^
pointer
```

After reading 2 characters:

```text
Py|thon
  ^
pointer
```

The pointer moves as data is read or written.

---

# 📍 `tell()`

`tell()` returns the current file pointer position.

```python
with open("data.txt", "r") as file:
    print(file.tell())

    file.read(5)

    print(file.tell())
```

Example output:

```text
0
5
```

---

# 🔀 `seek()`

`seek()` moves the file pointer to a specified position.

```python
with open("data.txt", "r") as file:
    file.read(5)

    file.seek(0)

    print(file.read())
```

`seek(0)` moves the pointer back to the beginning.

---

## Example

```python
with open("data.txt", "r") as file:
    print(file.read(5))

    file.seek(0)

    print(file.read(5))
```

Output:

```text
Hello
Hello
```

---

# ⭐ `with` Statement

The recommended way to work with files is using `with`.

Instead of:

```python
file = open("data.txt", "r")

data = file.read()

file.close()
```

Use:

```python
with open("data.txt", "r") as file:
    data = file.read()

print(data)
```

The `with` statement automatically closes the file.

---

# ✅ Advantages of `with`

* Automatically closes the file
* Cleaner code
* Safer
* Handles exceptions properly
* Prevents forgetting `close()`

Example:

```python
with open("data.txt", "r") as file:
    print(file.read())
```

After leaving the block:

```python
file.closed
```

will be:

```text
True
```

---

# 🌐 Encoding

Encoding defines how characters are converted into bytes.

A common encoding is:

```text
UTF-8
```

Recommended:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()

print(data)
```

When writing:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("Hello Python")
```

Using an explicit encoding helps make programs more predictable across systems.

---

# 📜 Reading Line by Line

Suppose:

```text
Python
Java
C++
JavaScript
```

Code:

```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

Output:

```text
Python
Java
C++
JavaScript
```

---

# 🧹 `strip()`

When reading lines, they often contain `\n`.

Example:

```python
line = "Python\n"
```

Using:

```python
print(line)
```

may result in extra spacing.

Use:

```python
print(line.strip())
```

`strip()` removes leading and trailing whitespace.

---

# 🔢 Counting Lines

```python
count = 0

with open("data.txt", "r") as file:
    for line in file:
        count += 1

print("Number of lines:", count)
```

---

# 🔤 Counting Characters

```python
with open("data.txt", "r") as file:
    data = file.read()

print("Characters:", len(data))
```

---

# 🔠 Counting Words

```python
with open("data.txt", "r") as file:
    data = file.read()

words = data.split()

print("Words:", len(words))
```

---

# 🔎 Searching in a File

```python
search = input("Enter word to search: ")

with open("data.txt", "r") as file:
    data = file.read()

if search in data:
    print("Word found")
else:
    print("Word not found")
```

---

# 📋 Copying One File to Another

```python
with open("source.txt", "r") as source:
    data = source.read()

with open("destination.txt", "w") as destination:
    destination.write(data)
```

---

# 📂 CSV Files

CSV stands for:

**Comma-Separated Values**

Example:

```text
Name,Age,City
John,25,Delhi
Alice,22,Mumbai
Bob,30,Chennai
```

Python provides the built-in `csv` module.

```python
import csv
```

---

# 📖 Reading CSV

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

Output:

```text
['Name', 'Age', 'City']
['John', '25', 'Delhi']
['Alice', '22', 'Mumbai']
['Bob', '30', 'Chennai']
```

---

# ✍️ Writing CSV

```python
import csv

data = [
    ["Name", "Age", "City"],
    ["John", 25, "Delhi"],
    ["Alice", 22, "Mumbai"]
]

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerows(data)
```

---

# 📌 CSV Using Dictionary

Python also provides `DictReader` and `DictWriter`.

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["Name"], row["Age"])
```

---

# 🗃️ JSON Files

JSON stands for:

**JavaScript Object Notation**

It is commonly used for storing and exchanging structured data.

Example:

```json
{
    "name": "John",
    "age": 25,
    "city": "Delhi"
}
```

Python provides the `json` module.

```python
import json
```

---

# 📖 Reading JSON

```python
import json

with open("data.json", "r", encoding="utf-8") as file:
    data = json.load(file)

print(data)
```

Output:

```python
{'name': 'John', 'age': 25, 'city': 'Delhi'}
```

Access values:

```python
print(data["name"])
print(data["age"])
```

---

# ✍️ Writing JSON

```python
import json

data = {
    "name": "John",
    "age": 25,
    "city": "Delhi"
}

with open("data.json", "w", encoding="utf-8") as file:
    json.dump(data, file, indent=4)
```

The `indent=4` makes the JSON easier to read.

---

# 🔄 `json.load()` vs `json.loads()`

### `json.load()`

Reads JSON from a file.

```python
with open("data.json", "r") as file:
    data = json.load(file)
```

### `json.loads()`

Reads JSON from a string.

```python
import json

text = '{"name": "John", "age": 25}'

data = json.loads(text)

print(data)
```

---

# 🔄 `json.dump()` vs `json.dumps()`

### `json.dump()`

Writes JSON to a file.

```python
json.dump(data, file)
```

### `json.dumps()`

Converts Python data to a JSON string.

```python
text = json.dumps(data)

print(text)
```

---

# 🧱 Binary Files

Binary files contain data in binary format.

Use:

```python
"rb"
```

for reading binary data.

Use:

```python
"wb"
```

for writing binary data.

---

# 📸 Reading Binary File

```python
with open("image.jpg", "rb") as file:
    data = file.read()

print(data)
```

The result is a bytes object.

---

# 📸 Writing Binary File

```python
with open("copy.jpg", "wb") as file:
    file.write(data)
```

---

# 📋 Copying Binary Files

```python
with open("original.jpg", "rb") as source:
    data = source.read()

with open("copy.jpg", "wb") as destination:
    destination.write(data)
```

This approach can be used for many binary files.

---

# 📁 File and Directory Operations

Python provides the `os` module for working with files and directories.

```python
import os
```

---

# 🔍 Checking File Existence

```python
import os

if os.path.exists("data.txt"):
    print("File exists")
else:
    print("File does not exist")
```

---

# 📄 Checking Whether It Is a File

```python
import os

if os.path.isfile("data.txt"):
    print("It is a file")
```

---

# 📁 Checking Whether It Is a Directory

```python
import os

if os.path.isdir("myfolder"):
    print("It is a directory")
```

---

# 📂 Creating a Directory

```python
import os

os.mkdir("myfolder")
```

This creates:

```text
myfolder/
```

---

# 📂 Creating Nested Directories

Use `makedirs()`:

```python
import os

os.makedirs("parent/child/grandchild")
```

---

# 🗑️ Removing a Directory

```python
import os

os.rmdir("myfolder")
```

`rmdir()` can remove an empty directory.

---

# 📋 Listing Directory Contents

```python
import os

print(os.listdir())
```

To list a specific directory:

```python
print(os.listdir("myfolder"))
```

---

# ✏️ Renaming Files

Use `os.rename()`.

```python
import os

os.rename("old.txt", "new.txt")
```

---

# 🗑️ Deleting Files

Use `os.remove()`.

```python
import os

os.remove("data.txt")
```

### Safer version:

```python
import os

if os.path.exists("data.txt"):
    os.remove("data.txt")
else:
    print("File not found")
```

---

# 🛠️ Using `pathlib`

Modern Python programs often use `pathlib` for filesystem paths.

```python
from pathlib import Path
```

Create a path:

```python
path = Path("data.txt")
```

Check existence:

```python
if path.exists():
    print("File exists")
```

Check whether it is a file:

```python
if path.is_file():
    print("It is a file")
```

---

# 📖 Reading Using `pathlib`

```python
from pathlib import Path

path = Path("data.txt")

data = path.read_text(encoding="utf-8")

print(data)
```

---

# ✍️ Writing Using `pathlib`

```python
from pathlib import Path

path = Path("data.txt")

path.write_text("Hello Python", encoding="utf-8")
```

---

# 📂 Creating a Directory Using `pathlib`

```python
from pathlib import Path

path = Path("myfolder")

path.mkdir()
```

For parent directories:

```python
path = Path("parent/child")

path.mkdir(parents=True, exist_ok=True)
```

---

# 🚨 Exception Handling with Files

File operations can generate errors.

Example:

```python
try:
    with open("data.txt", "r") as file:
        data = file.read()

    print(data)

except FileNotFoundError:
    print("File does not exist")
```

---

# 🛡️ Handling Multiple Exceptions

```python
try:
    with open("data.txt", "r") as file:
        data = file.read()

except FileNotFoundError:
    print("File not found")

except PermissionError:
    print("Permission denied")

except OSError:
    print("Some file system error occurred")
```

---

# 🔒 `finally`

The `finally` block always executes.

```python
try:
    file = open("data.txt", "r")
    print(file.read())

except FileNotFoundError:
    print("File not found")

finally:
    print("Operation completed")
```

With `with`, explicit cleanup is normally unnecessary.

---

# ❌ Common File Handling Errors

## 1. FileNotFoundError

Occurs when trying to access a file that doesn't exist.

```python
with open("missing.txt", "r") as file:
    print(file.read())
```

---

## 2. FileExistsError

Usually occurs with `x` mode when the file already exists.

```python
file = open("data.txt", "x")
```

---

## 3. PermissionError

Occurs when the program doesn't have the required permission.

```python
with open("protected.txt", "w") as file:
    file.write("Hello")
```

---

## 4. IsADirectoryError

Occurs when a directory is used where a file is expected.

---

## 5. NotADirectoryError

Occurs when a path component expected to be a directory isn't one.

---

## 6. UnicodeDecodeError

Can occur when reading bytes using the wrong text encoding.

Using the appropriate encoding can help:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

---

# ⚖️ Important Mode Differences

| Mode | Read | Write | Creates File | Deletes Existing Content |
| ---- | ---: | ----: | -----------: | -----------------------: |
| `r`  |    ✅ |     ❌ |            ❌ |                        ❌ |
| `w`  |    ❌ |     ✅ |            ✅ |                        ✅ |
| `a`  |    ❌ |     ✅ |            ✅ |                        ❌ |
| `x`  |    ❌ |     ✅ |            ✅ |                        ❌ |
| `r+` |    ✅ |     ✅ |            ❌ |                        ❌ |
| `w+` |    ✅ |     ✅ |            ✅ |                        ✅ |
| `a+` |    ✅ |     ✅ |            ✅ |                        ❌ |

### Easy way to remember

```text
r → read
w → write / overwrite
a → append
x → create
+ → add read/write capability
b → binary
t → text
```

---

# 🔥 `w` vs `a`

This is one of the most important differences.

### `w`

```python
with open("data.txt", "w") as file:
    file.write("Hello")
```

Existing content is replaced.

### `a`

```python
with open("data.txt", "a") as file:
    file.write("Hello")
```

Existing content is preserved and new content is added at the end.

---

# 🔥 `read()` vs `readline()` vs `readlines()`

| Method        | Result                     |
| ------------- | -------------------------- |
| `read()`      | Entire content as string   |
| `read(n)`     | First `n` characters/bytes |
| `readline()`  | One line as string         |
| `readlines()` | All lines as a list        |

Example:

```python
with open("data.txt", "r") as file:
    print(file.read())
```

```python
with open("data.txt", "r") as file:
    print(file.readline())
```

```python
with open("data.txt", "r") as file:
    print(file.readlines())
```

---

# 🧠 File Handling with User Input

A common real-world pattern:

```python
name = input("Enter your name: ")

with open("users.txt", "a", encoding="utf-8") as file:
    file.write(name + "\n")

print("Name saved successfully!")
```

---

# 🧮 Storing Student Information

```python
name = input("Enter name: ")
age = input("Enter age: ")
marks = input("Enter marks: ")

with open("students.txt", "a", encoding="utf-8") as file:
    file.write(f"{name}, {age}, {marks}\n")

print("Student information saved.")
```

File:

```text
John, 20, 85
Alice, 21, 92
Bob, 19, 78
```

---

# 🔎 Find a Specific Student

```python
search_name = input("Enter student name: ")

found = False

with open("students.txt", "r", encoding="utf-8") as file:
    for line in file:
        if line.startswith(search_name + ","):
            print("Student found:")
            print(line.strip())
            found = True
            break

if not found:
    print("Student not found.")
```

---

# 🔢 Count a Particular Word

```python
word = input("Enter word: ")

with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()

count = data.lower().split().count(word.lower())

print("Count:", count)
```

---

# 🔠 Convert File Content to Uppercase

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()

data = data.upper()

with open("uppercase.txt", "w", encoding="utf-8") as file:
    file.write(data)
```

---

# 🔄 Copy Text File

```python
with open("source.txt", "r", encoding="utf-8") as source:
    content = source.read()

with open("destination.txt", "w", encoding="utf-8") as destination:
    destination.write(content)
```

---

# 📊 Count Lines, Words and Characters

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()

lines = data.splitlines()
words = data.split()
characters = len(data)

print("Lines:", len(lines))
print("Words:", len(words))
print("Characters:", characters)
```

---

# 🔐 File Handling Best Practices

### 1. Prefer `with`

Instead of:

```python
file = open("data.txt")
# ...
file.close()
```

Prefer:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    # work with file
    pass
```

---

### 2. Specify Encoding for Text Files

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

---

### 3. Don't Use `w` When You Want to Preserve Data

Wrong:

```python
with open("data.txt", "w") as file:
    file.write("New data")
```

If existing data must be preserved, use:

```python
with open("data.txt", "a") as file:
    file.write("New data")
```

---

### 4. Handle Expected Errors

```python
try:
    with open("data.txt", "r") as file:
        print(file.read())

except FileNotFoundError:
    print("File not found.")
```

---

### 5. Use `pathlib` for Path Manipulation

```python
from pathlib import Path

path = Path("data") / "students.txt"

print(path)
```

This is more convenient and portable than manually constructing paths.

---

# 🧠 Important Concepts for Revision

## File

A file is a location used to store data permanently.

## File Object

The object returned by `open()`.

```python
file = open("data.txt", "r")
```

## File Mode

Specifies what operation will be performed.

```python
"r"
"w"
"a"
"x"
```

## File Pointer

Indicates the current position within the file.

## `seek()`

Moves the file pointer.

```python
file.seek(0)
```

## `tell()`

Returns the current pointer position.

```python
file.tell()
```

## `with`

Automatically manages the file and closes it.

```python
with open("data.txt") as file:
    pass
```

---

# 📝 Quick Revision Cheat Sheet

```text
OPEN FILE
---------
open("data.txt", "r")


READ
----
file.read()
file.readline()
file.readlines()


WRITE
-----
file.write("Hello")


WRITE MULTIPLE
--------------
file.writelines(lines)


APPEND
------
open("data.txt", "a")


CREATE
------
open("data.txt", "x")


CLOSE
-----
file.close()


POINTER
-------
file.tell()
file.seek(0)


RECOMMENDED
-----------
with open("data.txt", "r") as file:
    data = file.read()


CHECK FILE
----------
os.path.exists()
os.path.isfile()
os.path.isdir()


RENAME
------
os.rename()


DELETE
------
os.remove()


DIRECTORY
---------
os.mkdir()
os.makedirs()
os.rmdir()
os.listdir()


PATHLIB
-------
Path.exists()
Path.is_file()
Path.read_text()
Path.write_text()
Path.mkdir()
```

---

# 📌 File Modes — One-Line Revision

```text
r   → Read existing file
w   → Write / overwrite
a   → Add data at end
x   → Create new file
r+  → Read + write
w+  → Write + read, overwrite
a+  → Append + read
b   → Binary
t   → Text
```

---

# 🎯 Important Interview Questions

### 1. What is file handling?

File handling is the process of creating, opening, reading, writing, updating, and deleting files using a programming language.

---

### 2. Which function is used to open a file?

```python
open()
```

---

### 3. What is the default file mode?

```python
r
```

Read mode.

---

### 4. What happens when a file is opened in `w` mode?

Existing content is truncated, and the file is opened for writing. If the file doesn't exist, Python creates it.

---

### 5. What is the difference between `w` and `a`?

```text
w → overwrites existing content
a → adds content to the end
```

---

### 6. What happens if `r` mode is used on a nonexistent file?

Python raises:

```python
FileNotFoundError
```

---

### 7. What is `read()`?

Reads file content, optionally up to a specified number of characters/bytes.

---

### 8. What is `readline()`?

Reads one line from the file.

---

### 9. What is `readlines()`?

Reads all lines and returns them as a list.

---

### 10. What is `seek()`?

Moves the file pointer to a specified position.

---

### 11. What is `tell()`?

Returns the current file pointer position.

---

### 12. Why use `with open()`?

It automatically closes the file after the block finishes, including when an exception occurs.

---

### 13. What is the difference between text and binary files?

Text files represent data as characters using an encoding, while binary files contain raw bytes.

---

### 14. How do you delete a file?

Using `os.remove()`:

```python
import os

os.remove("data.txt")
```

---

### 15. How do you rename a file?

```python
import os

os.rename("old.txt", "new.txt")
```

---

# 🧪 Practice Programs

Try writing these programs yourself.

### Beginner

1. Create a text file.
2. Write your name into a file.
3. Read a file and display its contents.
4. Append a new line to a file.
5. Count the number of lines.
6. Count the number of words.
7. Count the number of characters.
8. Copy one text file to another.
9. Search for a word in a file.
10. Display every line of a file.

### Intermediate

11. Store student details in a file.
12. Read student details from a file.
13. Find a particular student.
14. Count how many times a word appears.
15. Convert all text to uppercase.
16. Convert all text to lowercase.
17. Separate even and odd numbers from a file.
18. Find the longest line in a file.
19. Find the shortest line in a file.
20. Remove blank lines from a file.

### Advanced

21. Create a CSV student database.
22. Read and process CSV records.
23. Create a JSON-based student database.
24. Update a JSON record.
25. Delete a JSON record.
26. Copy a binary file.
27. Build a simple file manager.
28. Create a command-line notes application.
29. Create a login system using files.
30. Create a student management system using CSV/JSON.

---

# 🚀 Mini Project — Simple Notes Application

```python
def add_note():
    note = input("Enter your note: ")

    with open("notes.txt", "a", encoding="utf-8") as file:
        file.write(note + "\n")

    print("Note saved!")


def view_notes():
    try:
        with open("notes.txt", "r", encoding="utf-8") as file:
            notes = file.read()

        print("\n--- NOTES ---")
        print(notes)

    except FileNotFoundError:
        print("No notes found.")


while True:
    print("\n1. Add Note")
    print("2. View Notes")
    print("3. Exit")

    choice = input("Enter choice: ")

    if choice == "1":
        add_note()

    elif choice == "2":
        view_notes()

    elif choice == "3":
        print("Goodbye!")
        break

    else:
        print("Invalid choice.")
```

---

# 🧠 Final Mental Map

```text
                    FILE HANDLING
                         │
          ┌──────────────┼──────────────┐
          │              │              │
        TEXT           BINARY         STRUCTURED
          │              │              │
       .txt           .jpg/.pdf      CSV / JSON
          │
     ┌────┼────┐
     │    │    │
    read write append
     │    │    │
     ↓    ↓    ↓
   read  write  add
     │
     ├── read()
     ├── readline()
     └── readlines()

File Management
     │
     ├── create
     ├── rename
     ├── delete
     ├── copy
     └── directory operations

File Pointer
     │
     ├── tell()
     └── seek()

Best Practice
     │
     └── with open(...)
```

---

# ⭐ Most Important Things to Remember

```text
1. open() is used to open a file.

2. "r" means read.

3. "w" means write and overwrite.

4. "a" means append.

5. "x" means create.

6. "+" adds read/write capability.

7. "b" means binary.

8. "t" means text.

9. read() reads the file.

10. readline() reads one line.

11. readlines() returns all lines as a list.

12. write() writes a string.

13. writelines() writes multiple strings.

14. tell() returns the pointer position.

15. seek() changes the pointer position.

16. with open() automatically manages closing.

17. UTF-8 is a common text encoding.

18. os provides filesystem operations.

19. pathlib provides an object-oriented way
   to work with paths.

20. csv is used for CSV files.

21. json is used for JSON data.

22. rb/wb are used for binary files.

23. FileNotFoundError occurs when a required
   file does not exist.

24. Always be careful with "w" because it
   replaces existing file contents.
```

---

# 🏁 One Complete Example

This example combines several important concepts:

```python
from pathlib import Path

file_path = Path("students.txt")

# Write data
with file_path.open("w", encoding="utf-8") as file:
    file.write("John,85\n")
    file.write("Alice,92\n")
    file.write("Bob,78\n")


# Read data
with file_path.open("r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())


# Append data
with file_path.open("a", encoding="utf-8") as file:
    file.write("David,88\n")


# Check file
if file_path.exists():
    print("File exists")


# Display final content
print("\nFinal File Content:")

print(file_path.read_text(encoding="utf-8"))
```

Output:

```text
John,85
Alice,92
Bob,78

File exists

Final File Content:
John,85
Alice,92
Bob,78
David,88
```

---

# 📌 File Handling in One Sentence

> **Open → Read/Write/Append → Process → Close**

And the recommended Python pattern is:

```python
with open("filename.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

This is the core pattern you should remember for Python file handling.
