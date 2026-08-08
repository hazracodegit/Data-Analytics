# 🐍 Python Exception Handling — Complete Revision Notes

Exception handling in Python is used to **handle runtime errors gracefully** without abruptly terminating the program.

It allows us to detect errors, handle them appropriately, and continue program execution when possible.

---

# 📚 Table of Contents

1. [What is an Exception?](#-what-is-an-exception)
2. [What is Exception Handling?](#-what-is-exception-handling)
3. [Why Exception Handling?](#-why-exception-handling)
4. [Syntax Errors vs Exceptions](#-syntax-errors-vs-exceptions)
5. [Common Built-in Exceptions](#-common-built-in-exceptions)
6. [try Block](#-try-block)
7. [except Block](#-except-block)
8. [Handling Specific Exceptions](#-handling-specific-exceptions)
9. [Handling Multiple Exceptions](#-handling-multiple-exceptions)
10. [Multiple except Blocks](#-multiple-except-blocks)
11. [Exception Object](#-exception-object)
12. [else Block](#-else-block)
13. [finally Block](#-finally-block)
14. [Complete try-except-else-finally](#-complete-try-except-else-finally)
15. [Nested try-except](#-nested-try-except)
16. [Exception Hierarchy](#-exception-hierarchy)
17. [BaseException and Exception](#-baseexception-and-exception)
18. [Raising Exceptions](#-raising-exceptions)
19. [raise Statement](#-raise-statement)
20. [Custom Exceptions](#-custom-exceptions)
21. [Custom Exception Classes](#-custom-exception-classes)
22. [Exception Chaining](#-exception-chaining)
23. [from None](#-from-none)
24. [Re-raising Exceptions](#-re-raising-exceptions)
25. [Assertions](#-assertions)
26. [Exception Handling with Files](#-exception-handling-with-files)
27. [Exception Handling with Input](#-exception-handling-with-input)
28. [Exception Handling with Functions](#-exception-handling-with-functions)
29. [Exception Handling with Classes](#-exception-handling-with-classes)
30. [Best Practices](#-best-practices)
31. [Common Mistakes](#-common-mistakes)
32. [Interview Questions](#-interview-questions)
33. [Practice Programs](#-practice-programs)
34. [Quick Revision](#-quick-revision)

---

# 🔥 What is an Exception?

An **exception** is an error that occurs during the execution of a program.

Example:

```python
print(10 / 0)
```

Output:

```text
ZeroDivisionError: division by zero
```

The program cannot normally continue from that point unless the exception is handled.

---

# 🛡️ What is Exception Handling?

**Exception handling** is the process of detecting and handling runtime errors so that the program can respond gracefully.

Example:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")
```

Output:

```text
Cannot divide by zero
```

Instead of displaying a traceback and terminating at the error, our program handles it.

---

# 🎯 Why Exception Handling?

Exception handling is useful because it:

* Prevents unexpected program termination
* Makes programs more reliable
* Handles invalid user input
* Handles missing files
* Handles invalid calculations
* Handles network/database failures
* Allows meaningful error messages
* Separates normal logic from error-handling logic

Example:

```python
try:
    age = int(input("Enter your age: "))
    print("Age:", age)

except ValueError:
    print("Please enter a valid number.")
```

---

# ⚠️ Syntax Errors vs Exceptions

These are different concepts.

## Syntax Error

A syntax error occurs when Python cannot understand the structure of the code.

```python
if True
    print("Hello")
```

Python reports a syntax error before normal execution.

---

## Exception

An exception occurs during execution.

```python
number = 10

print(number / 0)
```

This produces:

```text
ZeroDivisionError
```

### Difference

```text
Syntax Error
     ↓
Invalid Python syntax
     ↓
Program cannot start normally


Exception
     ↓
Problem during execution
     ↓
Can often be handled
```

---

# 🚨 Common Built-in Exceptions

Python provides many built-in exception classes.

| Exception             | Meaning                                         |
| --------------------- | ----------------------------------------------- |
| `Exception`           | General base class for most ordinary exceptions |
| `ValueError`          | Correct type but invalid value                  |
| `TypeError`           | Invalid operation/type                          |
| `ZeroDivisionError`   | Division by zero                                |
| `NameError`           | Name/variable not defined                       |
| `IndexError`          | Index outside sequence range                    |
| `KeyError`            | Dictionary key not found                        |
| `AttributeError`      | Attribute/method doesn't exist                  |
| `FileNotFoundError`   | File doesn't exist                              |
| `FileExistsError`     | File already exists                             |
| `PermissionError`     | Insufficient permission                         |
| `ImportError`         | Import-related failure                          |
| `ModuleNotFoundError` | Module cannot be found                          |
| `RuntimeError`        | Generic runtime problem                         |
| `OverflowError`       | Numeric result too large                        |
| `OSError`             | Operating-system-related error                  |
| `RecursionError`      | Recursion exceeds limit                         |
| `AssertionError`      | Assertion condition is false                    |
| `StopIteration`       | Iterator has no more items                      |
| `KeyboardInterrupt`   | User interrupts program                         |

---

# 🧪 try Block

The `try` block contains code that might raise an exception.

### Syntax

```python
try:
    # risky code
```

Usually it is followed by `except`, `else`, and/or `finally`.

Example:

```python
try:
    number = int(input("Enter number: "))
    print(number)
except ValueError:
    print("Invalid number")
```

---

# 🛡️ except Block

The `except` block handles an exception.

### Syntax

```python
try:
    # code
except:
    # error handling
```

Example:

```python
try:
    print(10 / 0)

except:
    print("An error occurred")
```

Output:

```text
An error occurred
```

### ⚠️ Avoid bare `except` when possible

Prefer catching the specific exception:

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("Cannot divide by zero")
```

---

# 🎯 Handling Specific Exceptions

Always catch the exception you expect whenever practical.

```python
try:
    number = int(input("Enter a number: "))

except ValueError:
    print("Invalid input")
```

Another example:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")
```

---

# 🔢 Handling Multiple Exceptions

Multiple exception types can be handled in one `except`.

```python
try:
    number = int(input("Enter number: "))
    result = 10 / number

except (ValueError, ZeroDivisionError):
    print("Invalid input or division by zero")
```

This is useful when the same response is appropriate for several exceptions.

---

# 🔀 Multiple except Blocks

Different exceptions can have different handling logic.

```python
try:
    number = int(input("Enter number: "))
    result = 100 / number

except ValueError:
    print("Please enter a valid integer.")

except ZeroDivisionError:
    print("Number cannot be zero.")
```

Example inputs:

```text
abc
```

Output:

```text
Please enter a valid integer.
```

For:

```text
0
```

Output:

```text
Number cannot be zero.
```

---

# ⚠️ Order of except Blocks

More specific exceptions should generally come before broader exceptions.

Correct:

```python
try:
    number = int(input("Enter number: "))

except ValueError:
    print("Invalid value")

except Exception:
    print("Some other error")
```

Incorrect:

```python
try:
    number = int(input("Enter number: "))

except Exception:
    print("Some error")

except ValueError:
    print("Invalid value")
```

The second `except` is effectively unreachable for `ValueError` because `Exception` catches it first.

---

# 📦 Exception Object

You can store the exception in a variable using `as`.

```python
try:
    result = 10 / 0

except ZeroDivisionError as error:
    print("Error:", error)
```

Output:

```text
Error: division by zero
```

---

## Another Example

```python
try:
    number = int("hello")

except ValueError as error:
    print("Exception:", error)
```

Output:

```text
Exception: invalid literal for int() with base 10: 'hello'
```

The `error` variable contains the exception object.

---

# 📝 else Block

The `else` block executes **only when no exception occurs in the `try` block**.

### Syntax

```python
try:
    # risky code

except SomeException:
    # error handling

else:
    # executes if no exception
```

Example:

```python
try:
    number = int(input("Enter number: "))

except ValueError:
    print("Invalid number")

else:
    print("You entered:", number)
```

If input is:

```text
25
```

Output:

```text
You entered: 25
```

---

# 🎯 Why Use else?

It is useful for separating:

```text
Risky operations
        ↓
      try

Error handling
        ↓
     except

Successful operations
        ↓
      else
```

Example:

```python
try:
    file = open("data.txt", "r")

except FileNotFoundError:
    print("File not found")

else:
    print("File opened successfully")
    file.close()
```

---

# 🧹 finally Block

The `finally` block **always executes**, whether an exception occurs or not.

### Syntax

```python
try:
    # code

except:
    # error

finally:
    # always executes
```

Example:

```python
try:
    number = 10 / 2
    print(number)

except ZeroDivisionError:
    print("Cannot divide by zero")

finally:
    print("This always executes")
```

Output:

```text
5.0
This always executes
```

---

# ❗ finally When Exception Occurs

```python
try:
    number = 10 / 0

except ZeroDivisionError:
    print("Division by zero")

finally:
    print("Finally executed")
```

Output:

```text
Division by zero
Finally executed
```

---

# 🔥 Complete try-except-else-finally

Python allows all four parts together.

```python
try:
    number = int(input("Enter number: "))

except ValueError:
    print("Invalid input")

else:
    print("Valid number:", number)

finally:
    print("Program finished")
```

Flow:

```text
              try
               │
       ┌───────┴───────┐
       │               │
   Exception        No Exception
       │               │
    except           else
       │               │
       └───────┬───────┘
               │
            finally
               │
             End
```

---

# 📌 Important Rule

`else` runs only if the `try` block completes without an exception.

`finally` runs whether an exception occurs or not.

---

# 🪆 Nested try-except

A `try` block can exist inside another `try` block.

```python
try:
    print("Outer try")

    try:
        print(10 / 0)

    except ZeroDivisionError:
        print("Inner exception handled")

except:
    print("Outer exception handled")
```

Output:

```text
Outer try
Inner exception handled
```

---

# 🏗️ Exception Hierarchy

Python exceptions are organized into a class hierarchy.

Simplified:

```text
BaseException
│
├── KeyboardInterrupt
├── SystemExit
└── Exception
    │
    ├── ArithmeticError
    │   ├── ZeroDivisionError
    │   └── OverflowError
    │
    ├── LookupError
    │   ├── IndexError
    │   └── KeyError
    │
    ├── OSError
    │   ├── FileNotFoundError
    │   ├── PermissionError
    │   └── FileExistsError
    │
    ├── TypeError
    ├── ValueError
    ├── NameError
    ├── AttributeError
    ├── ImportError
    └── RuntimeError
```

---

# 🧬 BaseException and Exception

`BaseException` is the top-level base class for Python's built-in exceptions.

Most ordinary application exceptions derive from:

```python
Exception
```

Example:

```python
try:
    number = int("abc")

except Exception as error:
    print("Error:", error)
```

### Important

Usually catch:

```python
except Exception:
```

rather than:

```python
except BaseException:
```

`BaseException` also includes control-flow exceptions such as `KeyboardInterrupt` and `SystemExit`, which applications generally should not accidentally suppress.

---

# 🔨 Raising Exceptions

Python allows us to manually generate an exception using:

```python
raise
```

Example:

```python
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")
```

Output:

```text
ValueError: Age cannot be negative
```

---

# 🚨 `raise` Statement

### Syntax

```python
raise ExceptionType("message")
```

Example:

```python
raise ValueError("Invalid value")
```

Another:

```python
raise TypeError("Expected an integer")
```

---

# 🎯 Why Use `raise`?

`raise` is useful when we want to enforce rules.

Example:

```python
age = int(input("Enter age: "))

if age < 18:
    raise ValueError("You must be at least 18")

print("Access granted")
```

---

# 🔐 Validation Using raise

```python
username = input("Enter username: ")

if len(username) < 5:
    raise ValueError("Username must contain at least 5 characters")

print("Valid username")
```

---

# 🧑‍💻 Custom Exceptions

Python allows us to create our own exception types.

A custom exception is normally created by inheriting from `Exception`.

### Example

```python
class InvalidAgeError(Exception):
    pass
```

Use it:

```python
age = -1

if age < 0:
    raise InvalidAgeError("Age cannot be negative")
```

---

# 🏗️ Custom Exception Class

Custom exceptions can contain additional behavior.

```python
class InsufficientBalanceError(Exception):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount

        super().__init__(
            f"Insufficient balance: {balance}, required: {amount}"
        )
```

Use it:

```python
balance = 500
withdraw = 1000

if withdraw > balance:
    raise InsufficientBalanceError(balance, withdraw)
```

---

# 🏦 Bank Example

```python
class InsufficientBalanceError(Exception):
    pass


balance = 500

try:
    amount = float(input("Enter withdrawal amount: "))

    if amount > balance:
        raise InsufficientBalanceError(
            "Insufficient balance"
        )

    balance -= amount

    print("Withdrawal successful")
    print("Remaining balance:", balance)

except ValueError:
    print("Enter a valid amount")

except InsufficientBalanceError as error:
    print(error)
```

---

# 🔗 Exception Chaining

Sometimes one exception occurs while handling another exception.

Python supports explicit exception chaining using:

```python
raise NewException(...) from original_exception
```

Example:

```python
try:
    number = int("abc")

except ValueError as error:
    raise RuntimeError("Could not process the number") from error
```

This preserves the relationship between the original and new exception.

---

# 🚫 Suppressing the Original Context with `from None`

You can suppress the displayed exception context using:

```python
raise RuntimeError("Something went wrong") from None
```

Example:

```python
try:
    int("abc")

except ValueError:
    raise RuntimeError("Invalid number") from None
```

---

# 🔄 Re-raising an Exception

Sometimes we catch an exception, perform some action, and then raise it again.

Use:

```python
raise
```

Example:

```python
try:
    number = 10 / 0

except ZeroDivisionError:
    print("Logging the error...")
    raise
```

The original exception is re-raised.

---

# 📌 Difference Between `raise` and `raise error`

Inside an `except` block:

```python
raise
```

is the usual way to re-raise the currently handled exception while preserving its traceback.

Example:

```python
try:
    10 / 0

except ZeroDivisionError:
    print("Error occurred")
    raise
```

---

# ✅ Assertions

Python provides the `assert` statement for checking assumptions.

### Syntax

```python
assert condition
```

Example:

```python
age = 20

assert age >= 18

print("Adult")
```

If the condition is false:

```python
age = 15

assert age >= 18
```

Python raises:

```text
AssertionError
```

---

# 📝 Assertion with Message

```python
age = 15

assert age >= 18, "Age must be at least 18"
```

Output:

```text
AssertionError: Age must be at least 18
```

### Important

Assertions are mainly for **developer checks and internal assumptions**, not for validating untrusted user input in production. Python can disable assertions with optimization options.

---

# 📂 Exception Handling with Files

File handling commonly produces exceptions.

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()

    print(data)

except FileNotFoundError:
    print("File does not exist.")

except PermissionError:
    print("Permission denied.")
```

---

# 🔢 Exception Handling with Input

`input()` always returns a string.

Converting it to another type can raise `ValueError`.

```python
try:
    age = int(input("Enter your age: "))

except ValueError:
    print("Please enter a valid integer.")

else:
    print("Your age is:", age)
```

---

# ➗ Safe Calculator

```python
try:
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    operator = input("Enter operator (+, -, *, /): ")

    if operator == "+":
        result = a + b

    elif operator == "-":
        result = a - b

    elif operator == "*":
        result = a * b

    elif operator == "/":
        result = a / b

    else:
        raise ValueError("Invalid operator")

except ValueError as error:
    print("Error:", error)

except ZeroDivisionError:
    print("Cannot divide by zero")

else:
    print("Result:", result)
```

---

# 🧮 Exception Handling with Functions

Exceptions can be raised inside functions and handled by the caller.

```python
def divide(a, b):
    return a / b


try:
    result = divide(10, 0)
    print(result)

except ZeroDivisionError:
    print("Cannot divide by zero")
```

---

# 🔨 Raising from a Function

```python
def calculate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")

    return age


try:
    age = calculate_age(-10)

except ValueError as error:
    print(error)
```

---

# 🏛️ Exception Handling with Classes

Exceptions can be used inside classes and methods.

```python
class BankAccount:

    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("Insufficient balance")

        self.balance -= amount
        return self.balance


account = BankAccount(1000)

try:
    remaining = account.withdraw(1500)
    print("Remaining:", remaining)

except ValueError as error:
    print(error)
```

---

# 🔄 Returning vs Raising

These are different.

### Return an error value

```python
def divide(a, b):
    if b == 0:
        return None

    return a / b
```

### Raise an exception

```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")

    return a / b
```

Exceptions are often appropriate when an operation cannot fulfill its normal contract.

---

# 🧹 Resource Cleanup

`finally` is commonly used when cleanup must happen.

```python
file = None

try:
    file = open("data.txt", "r", encoding="utf-8")
    print(file.read())

except FileNotFoundError:
    print("File not found")

finally:
    if file is not None:
        file.close()
```

However, for files, the preferred approach is usually:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    print(file.read())
```

---

# 🧠 Exception Handling Flow

Consider:

```python
try:
    print("A")
    print(10 / 0)
    print("B")

except ZeroDivisionError:
    print("C")

else:
    print("D")

finally:
    print("E")
```

Output:

```text
A
C
E
```

Why?

```text
A → executes
10 / 0 → exception
B → skipped
except → executes
else → skipped
finally → executes
```

---

# 🔥 Another Flow Example

```python
try:
    print("A")
    print(10 / 2)
    print("B")

except ZeroDivisionError:
    print("C")

else:
    print("D")

finally:
    print("E")
```

Output:

```text
A
5.0
B
D
E
```

---

# 🧩 Exception Handling Inside a Loop

```python
numbers = [10, 0, 5, 0, 2]

for number in numbers:
    try:
        print(100 / number)

    except ZeroDivisionError:
        print("Cannot divide by zero")
```

Output:

```text
10.0
Cannot divide by zero
20.0
Cannot divide by zero
50.0
```

The loop continues after handled exceptions.

---

# 🔁 Exception Handling in a Loop with User Input

```python
while True:
    try:
        number = int(input("Enter a number: "))
        print("You entered:", number)
        break

    except ValueError:
        print("Invalid input. Try again.")
```

This keeps asking until a valid integer is entered.

---

# 🎯 Practical Example — Login Validation

```python
class InvalidLoginError(Exception):
    pass


correct_username = "admin"
correct_password = "1234"

try:
    username = input("Username: ")
    password = input("Password: ")

    if username != correct_username:
        raise InvalidLoginError("Invalid username")

    if password != correct_password:
        raise InvalidLoginError("Invalid password")

except InvalidLoginError as error:
    print("Login failed:", error)

else:
    print("Login successful")
```

---

# 📊 Practical Example — Marks Validation

```python
class InvalidMarksError(Exception):
    pass


try:
    marks = float(input("Enter marks: "))

    if marks < 0 or marks > 100:
        raise InvalidMarksError(
            "Marks must be between 0 and 100"
        )

except ValueError:
    print("Enter a valid number")

except InvalidMarksError as error:
    print(error)

else:
    print("Valid marks:", marks)
```

---

# 🧠 Best Practices

## 1. Catch Specific Exceptions

Prefer:

```python
try:
    number = int(input("Enter number: "))

except ValueError:
    print("Invalid number")
```

Instead of:

```python
try:
    number = int(input("Enter number: "))

except:
    print("Something went wrong")
```

---

# 2. Keep try Blocks Small

Avoid:

```python
try:
    # hundreds of lines
    ...
except Exception:
    ...
```

Prefer:

```python
try:
    number = int(input("Enter number: "))

except ValueError:
    print("Invalid number")
```

Small `try` blocks make it clearer which operation failed.

---

# 3. Don't Silently Ignore Errors

Avoid:

```python
try:
    risky_operation()

except Exception:
    pass
```

This can hide bugs.

Instead:

```python
try:
    risky_operation()

except Exception as error:
    print("Operation failed:", error)
```

---

# 4. Don't Use Exceptions for Normal Control Flow

Exceptions should generally represent exceptional situations, not ordinary decisions.

Instead of:

```python
try:
    value = my_dict["name"]

except KeyError:
    value = None
```

Sometimes this is clearer:

```python
value = my_dict.get("name")
```

The best choice depends on the situation.

---

# 5. Use Custom Exceptions When Useful

For domain-specific errors:

```python
class InvalidAgeError(Exception):
    pass
```

This makes code easier to understand.

---

# 6. Use `finally` for Cleanup

```python
try:
    resource = acquire_resource()

finally:
    release_resource(resource)
```

For files, prefer `with`.

---

# 7. Don't Catch `BaseException` Normally

Avoid:

```python
except BaseException:
    pass
```

Usually use:

```python
except Exception:
    ...
```

when a broad catch is genuinely appropriate.

---

# ❌ Common Mistakes

## Mistake 1 — Wrong Exception Name

```python
try:
    10 / 0

except ZeroDivision:
    print("Error")
```

Correct:

```python
try:
    10 / 0

except ZeroDivisionError:
    print("Error")
```

---

# Mistake 2 — Catching the Wrong Exception

```python
try:
    int("hello")

except TypeError:
    print("Error")
```

The actual exception is:

```text
ValueError
```

Correct:

```python
try:
    int("hello")

except ValueError:
    print("Error")
```

---

# Mistake 3 — Wrong Order

Avoid:

```python
try:
    risky_operation()

except Exception:
    print("General")

except ValueError:
    print("Value")
```

Put the more specific exception first.

```python
try:
    risky_operation()

except ValueError:
    print("Value")

except Exception:
    print("General")
```

---

# Mistake 4 — Forgetting `as`

If you need the error message:

```python
try:
    10 / 0

except ZeroDivisionError as error:
    print(error)
```

---

# Mistake 5 — Using `finally` as an Error Handler

`finally` is for cleanup that should happen regardless of success/failure.

```python
try:
    risky_operation()

except ValueError:
    print("Handle error")

finally:
    print("Cleanup")
```

---

# ⚖️ `else` vs `finally`

| `else`                           | `finally`                    |
| -------------------------------- | ---------------------------- |
| Runs only if no exception occurs | Runs regardless of exception |
| Used for successful operations   | Used for cleanup             |
| Optional                         | Optional                     |
| Comes after `except`             | Comes after `except`/`else`  |

Example:

```python
try:
    number = int(input("Number: "))

except ValueError:
    print("Invalid")

else:
    print("Success")

finally:
    print("Finished")
```

---

# ⚖️ `raise` vs `assert`

| `raise`                                 | `assert`                              |
| --------------------------------------- | ------------------------------------- |
| Explicitly raises an exception          | Checks an assumption                  |
| Used for application validation/control | Mainly used for development/debugging |
| Can raise any exception                 | Raises `AssertionError` when false    |
| Not disabled by Python optimization     | Assertions can be disabled            |

Example:

```python
raise ValueError("Invalid age")
```

```python
assert age >= 0
```

---

# ⚖️ Error vs Exception

In Python, people often use "error" and "exception" informally.

For example:

```python
10 / 0
```

raises a `ZeroDivisionError`, which is an exception class.

The important idea is:

```text
Problem during execution
        ↓
Exception raised
        ↓
Can potentially be handled
```

---

# 🎯 Interview Questions

## 1. What is an exception?

An exception is an event raised during program execution that indicates an abnormal condition.

---

## 2. What is exception handling?

It is the mechanism used to detect and handle exceptions using constructs such as:

```python
try
except
else
finally
```

---

## 3. What is the purpose of `try`?

It contains code that may raise an exception.

---

## 4. What is the purpose of `except`?

It handles an exception raised by the associated `try` block.

---

## 5. What is the purpose of `else`?

It executes when the `try` block completes without an exception.

---

## 6. What is the purpose of `finally`?

It executes regardless of whether an exception occurs.

---

## 7. What is `raise`?

`raise` manually raises an exception.

```python
raise ValueError("Invalid value")
```

---

## 8. What is a custom exception?

An exception class created by the programmer.

```python
class MyError(Exception):
    pass
```

---

## 9. What does `as` do?

It assigns the caught exception object to a variable.

```python
except ValueError as error:
    print(error)
```

---

## 10. What is exception chaining?

It links a new exception to an original exception.

```python
raise RuntimeError("Failed") from error
```

---

## 11. What is re-raising?

Raising the currently handled exception again:

```python
except Exception:
    raise
```

---

## 12. What is the difference between `raise` and `raise Exception()`?

```python
raise
```

re-raises the currently handled exception inside an `except` block.

```python
raise ValueError("message")
```

creates and raises a new exception.

---

## 13. Can we have multiple `except` blocks?

Yes.

```python
try:
    ...
except ValueError:
    ...
except TypeError:
    ...
```

---

## 14. Can we have `try` without `except`?

Yes, if it has `finally`.

```python
try:
    print("Hello")

finally:
    print("Done")
```

---

## 15. Can we have `try` without `except` and `finally`?

No.

A `try` statement must have at least one `except` or `finally`.

---

## 16. Can `else` exist without `except`?

Yes, with `finally`:

```python
try:
    print("Hello")

else:
    print("Success")

finally:
    print("Done")
```

However, in practice, `else` without `except` is uncommon.

---

# 🧪 Practice Programs

## Beginner

1. Handle division by zero.
2. Handle invalid integer input.
3. Handle invalid float input.
4. Handle a missing file.
5. Handle an invalid list index.
6. Handle a missing dictionary key.
7. Handle an invalid type operation.
8. Use `try-except-else`.
9. Use `try-except-finally`.
10. Catch multiple exception types.

---

## Intermediate

11. Create a safe calculator.
12. Create a number input validator.
13. Create an age validation program.
14. Create a marks validation program.
15. Create a login system with custom exceptions.
16. Create a bank withdrawal system.
17. Create a file reader with exception handling.
18. Create a menu-driven program with error handling.
19. Create a student management system with exceptions.
20. Create a shopping cart with custom exceptions.

---

## Advanced

21. Create multiple custom exception classes.
22. Implement exception chaining.
23. Implement exception logging.
24. Create a banking application with custom exceptions.
25. Create an authentication system.
26. Create an inventory management system.
27. Create a file-based database with error handling.
28. Build a command-line application with robust validation.
29. Create your own exception hierarchy.
30. Build a complete application using custom exceptions.

---

# 🚀 Mini Project — Bank Account

```python
class InsufficientBalanceError(Exception):
    pass


class InvalidAmountError(Exception):
    pass


class BankAccount:

    def __init__(self, balance=0):
        self.balance = balance

    def deposit(self, amount):

        if amount <= 0:
            raise InvalidAmountError(
                "Deposit amount must be positive"
            )

        self.balance += amount

    def withdraw(self, amount):

        if amount <= 0:
            raise InvalidAmountError(
                "Withdrawal amount must be positive"
            )

        if amount > self.balance:
            raise InsufficientBalanceError(
                "Insufficient balance"
            )

        self.balance -= amount


account = BankAccount(1000)

try:

    amount = float(input("Enter withdrawal amount: "))

    account.withdraw(amount)

except ValueError:
    print("Please enter a valid number.")

except InvalidAmountError as error:
    print("Invalid amount:", error)

except InsufficientBalanceError as error:
    print("Transaction failed:", error)

else:
    print("Withdrawal successful.")
    print("Remaining balance:", account.balance)

finally:
    print("Transaction completed.")
```

---

# 🧠 Exception Handling Mental Map

```text
                    EXCEPTION HANDLING
                           │
              ┌────────────┴────────────┐
              │                         │
           Built-in                 Custom
          Exceptions              Exceptions
              │                         │
      ┌───────┼───────┐                 │
      │       │       │                 │
 ValueError TypeError ZeroDivision   class MyError
      │       │       │                 │
      └───────┴───────┴─────────────────┘
                           │
                           ↓
                         try
                           │
                           ↓
                        except
                           │
              ┌────────────┴────────────┐
              │                         │
           Exception                 No Exception
              │                         │
              ↓                         ↓
           except                     else
              │                         │
              └────────────┬────────────┘
                           ↓
                        finally
                           │
                           ↓
                          End
```

---

# 📌 Complete Syntax Cheat Sheet

## Basic

```python
try:
    risky_code()

except SomeException:
    handle_error()
```

---

## Specific Exception

```python
try:
    risky_code()

except ValueError:
    print("Invalid value")
```

---

## Exception Object

```python
try:
    risky_code()

except ValueError as error:
    print(error)
```

---

## Multiple Exceptions

```python
try:
    risky_code()

except (ValueError, TypeError):
    print("Invalid operation")
```

---

## Multiple except Blocks

```python
try:
    risky_code()

except ValueError:
    print("Value error")

except TypeError:
    print("Type error")

except Exception:
    print("Other error")
```

---

## try-except-else

```python
try:
    risky_code()

except ValueError:
    print("Error")

else:
    print("Success")
```

---

## try-except-finally

```python
try:
    risky_code()

except ValueError:
    print("Error")

finally:
    print("Cleanup")
```

---

## Complete Structure

```python
try:
    risky_code()

except SomeException as error:
    handle_error(error)

else:
    success_code()

finally:
    cleanup_code()
```

---

## Raise

```python
raise ValueError("Invalid value")
```

---

## Custom Exception

```python
class MyError(Exception):
    pass
```

---

## Re-raise

```python
try:
    risky_code()

except Exception:
    raise
```

---

## Exception Chaining

```python
try:
    risky_code()

except ValueError as error:
    raise RuntimeError("Operation failed") from error
```

---

# ⭐ Final Revision Notes

```text
1. Exception = abnormal condition during execution.

2. try = contains risky code.

3. except = handles exceptions.

4. else = runs when try succeeds.

5. finally = runs regardless of success/failure.

6. raise = manually raises an exception.

7. as = stores the exception object.

8. Custom exceptions usually inherit from Exception.

9. Use specific exceptions instead of bare except.

10. Multiple except blocks are allowed.

11. More specific exceptions should come before
    broader exceptions.

12. Exception chaining:
       raise NewError(...) from old_error

13. Re-raise:
       raise

14. ValueError = invalid value.

15. TypeError = inappropriate type/operation.

16. ZeroDivisionError = division by zero.

17. IndexError = invalid sequence index.

18. KeyError = dictionary key doesn't exist.

19. FileNotFoundError = file doesn't exist.

20. AttributeError = attribute doesn't exist.

21. NameError = name is not defined.

22. AssertionError = assert condition is false.

23. Exception handling makes programs more robust.

24. Don't silently ignore exceptions.

25. Keep try blocks small.

26. Use finally for cleanup.

27. For files, prefer:
       with open(...)

28. Custom exceptions make application-specific
    errors clearer.

29. assert is mainly for development/internal
    assumptions, not user-input validation.

30. Don't normally catch BaseException.
```

---

# 🏁 One-Line Memory Trick

```text
try     → TRY this code
except  → EXCEPT when it fails
else    → ELSE when it succeeds
finally → FINALLY do this anyway
raise   → RAISE an error yourself
```

### The core pattern to remember:

```python
try:
    # risky operation

except SpecificException as error:
    # handle error

else:
    # runs if successful

finally:
    # always runs
```

**This is the foundation of Python exception handling.**
