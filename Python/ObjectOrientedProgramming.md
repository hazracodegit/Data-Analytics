# 🐍 Python OOP — Complete Revision Notes

Object-Oriented Programming (**OOP**) is a programming approach where we organize programs around **objects and classes**.

Python supports OOP and provides concepts such as:

* Class
* Object
* Attributes
* Methods
* Constructor
* Instance variables
* Class variables
* Instance methods
* Class methods
* Static methods
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction
* Method overriding
* Method overloading concepts
* Magic/Dunder methods
* Composition
* Aggregation
* Association
* Abstract classes
* Properties
* Getters and setters

---

# 📚 Table of Contents

1. [What is OOP?](#-what-is-oop)
2. [Why OOP?](#-why-use-oop)
3. [Class](#-class)
4. [Object](#-object)
5. [Class and Object Example](#-class-and-object-example)
6. [Attributes](#-attributes)
7. [Methods](#-methods)
8. [self](#-self)
9. [Constructor](#-constructor)
10. [**init**()](#-init)
11. [Instance Variables](#-instance-variables)
12. [Class Variables](#-class-variables)
13. [Instance Methods](#-instance-methods)
14. [Class Methods](#-class-methods)
15. [Static Methods](#-static-methods)
16. [Method Types Comparison](#-method-types-comparison)
17. [Encapsulation](#-encapsulation)
18. [Public Members](#-public-members)
19. [Protected Convention](#-protected-convention)
20. [Private Members](#-private-members)
21. [Name Mangling](#-name-mangling)
22. [Getters and Setters](#-getters-and-setters)
23. [Property](#-property)
24. [Inheritance](#-inheritance)
25. [Types of Inheritance](#-types-of-inheritance)
26. [Single Inheritance](#-single-inheritance)
27. [Multilevel Inheritance](#-multilevel-inheritance)
28. [Multiple Inheritance](#-multiple-inheritance)
29. [Hierarchical Inheritance](#-hierarchical-inheritance)
30. [Hybrid Inheritance](#-hybrid-inheritance)
31. [super()](#-super)
32. [Method Overriding](#-method-overriding)
33. [Polymorphism](#-polymorphism)
34. [Duck Typing](#-duck-typing)
35. [Operator Overloading](#-operator-overloading)
36. [Method Overloading](#-method-overloading)
37. [Abstraction](#-abstraction)
38. [Abstract Classes](#-abstract-classes)
39. [Abstract Methods](#-abstract-methods)
40. [abc Module](#-abc-module)
41. [Magic/Dunder Methods](#-magicdunder-methods)
42. [**str**](#-str)
43. [**repr**](#-repr)
44. [**len**](#-len)
45. [**eq**](#-eq)
46. [**add**](#-add)
47. [Composition](#-composition)
48. [Aggregation](#-aggregation)
49. [Association](#-association)
50. [Class Object vs Instance Object](#-class-object-vs-instance-object)
51. [isinstance()](#-isinstance)
52. [issubclass()](#-issubclass)
53. [MRO](#-mro)
54. [super() and MRO](#-super-and-mro)
55. [Object Lifecycle](#-object-lifecycle)
56. [Destructor](#-destructor)
57. [Copying Objects](#-copying-objects)
58. [Shallow Copy](#-shallow-copy)
59. [Deep Copy](#-deep-copy)
60. [Dataclasses](#-dataclasses)
61. [Complete OOP Example](#-complete-oop-example)
62. [Common Mistakes](#-common-mistakes)
63. [Interview Questions](#-interview-questions)
64. [Practice Programs](#-practice-programs)
65. [Quick Revision](#-quick-revision)

---

# 🧠 What is OOP?

**Object-Oriented Programming** is a programming paradigm based on objects.

An object contains:

```text
Object
 ├── Data
 │    ↓
 │  Attributes
 │
 └── Behavior
      ↓
    Methods
```

For example, a car has:

```text
Data:
    color
    brand
    speed

Behavior:
    start()
    stop()
    accelerate()
```

In Python, we can represent this using a class.

---

# 🎯 Why Use OOP?

OOP helps us build:

* Large applications
* Maintainable applications
* Reusable code
* Modular code
* Scalable systems

Main advantages:

### 1. Reusability

Classes can be reused.

### 2. Maintainability

Code is organized into logical units.

### 3. Security

Encapsulation can control access to internal state.

### 4. Extensibility

Inheritance allows existing classes to be extended.

### 5. Flexibility

Polymorphism allows common interfaces for different objects.

---

# 🏗️ Class

A **class** is a blueprint/template for creating objects.

Syntax:

```python
class ClassName:
    # attributes
    # methods
    pass
```

Example:

```python
class Student:
    pass
```

Here:

```text
Student → Class
```

---

# 📦 Object

An **object** is an instance of a class.

Example:

```python
class Student:
    pass


student1 = Student()
student2 = Student()
```

Here:

```text
Student
   │
   ├── student1
   └── student2
```

Both are objects of the `Student` class.

---

# 🔥 Class and Object Example

```python
class Student:

    def display(self):
        print("I am a student")


student1 = Student()

student1.display()
```

Output:

```text
I am a student
```

---

# 🏷️ Attributes

Attributes represent the **data/state** of an object or class.

Example:

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Create object:

```python
student = Student("Rahul", 20)

print(student.name)
print(student.age)
```

Output:

```text
Rahul
20
```

---

# ⚙️ Methods

Methods are functions defined inside a class.

```python
class Student:

    def study(self):
        print("Student is studying")


student = Student()

student.study()
```

Output:

```text
Student is studying
```

---

# ⭐ self

`self` refers to the **current instance**.

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student1 = Student("Rahul")
student2 = Student("Anita")

student1.display()
student2.display()
```

Output:

```text
Rahul
Anita
```

Here:

```text
student1.display()
       ↓
self = student1

student2.display()
       ↓
self = student2
```

### Important

`self` is a naming convention for the instance reference. It is not a Python keyword.

---

# 🏗️ Constructor

A constructor is commonly used to initialize an object's state when the object is created.

In Python, this is typically done using:

```python
__init__()
```

Example:

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age


student = Student("Rahul", 20)
```

When the object is created, Python calls `__init__()` to initialize it.

---

# 🔧 **init**()

Example:

```python
class Employee:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary


employee = Employee("John", 50000)

print(employee.name)
print(employee.salary)
```

Output:

```text
John
50000
```

---

# 📌 Instance Variables

Instance variables belong to individual objects.

Example:

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Each object has its own values:

```python
s1 = Student("Rahul", 20)
s2 = Student("Anita", 21)

print(s1.name)
print(s2.name)
```

Output:

```text
Rahul
Anita
```

Changing one does not normally change the other:

```python
s1.age = 25

print(s1.age)
print(s2.age)
```

Output:

```text
25
21
```

---

# 🏫 Class Variables

A class variable is associated with the class and is shared unless an instance creates/shadows an attribute with the same name.

Example:

```python
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name


s1 = Student("Rahul")
s2 = Student("Anita")

print(s1.school)
print(s2.school)
print(Student.school)
```

Output:

```text
ABC School
ABC School
ABC School
```

---

# ⚠️ Class Variable Example

```python
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name


s1 = Student("Rahul")
s2 = Student("Anita")

Student.school = "XYZ School"

print(s1.school)
print(s2.school)
```

Output:

```text
XYZ School
XYZ School
```

Both see the changed class attribute unless they have their own instance attribute named `school`.

---

# 🔄 Instance Methods

Instance methods operate on an instance.

They normally take:

```python
self
```

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


s = Student("Rahul")

s.display()
```

---

# 🏫 Class Methods

A class method operates on the class rather than a particular instance.

It uses:

```python
@classmethod
```

and conventionally receives:

```python
cls
```

Example:

```python
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school


print(Student.school)

Student.change_school("XYZ School")

print(Student.school)
```

Output:

```text
ABC School
XYZ School
```

---

# ⚡ Static Methods

A static method does not automatically receive `self` or `cls`.

Use:

```python
@staticmethod
```

Example:

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

Output:

```text
30
```

Static methods are useful when functionality logically belongs to a class but does not need instance or class state.

---

# 📊 Method Types Comparison

| Method          | Decorator       | First Parameter    | Access                |
| --------------- | --------------- | ------------------ | --------------------- |
| Instance method | None            | `self`             | Instance state        |
| Class method    | `@classmethod`  | `cls`              | Class state           |
| Static method   | `@staticmethod` | None automatically | Neither automatically |

Example:

```python
class Demo:

    def instance_method(self):
        print("Instance method")

    @classmethod
    def class_method(cls):
        print("Class method")

    @staticmethod
    def static_method():
        print("Static method")
```

---

# 🔐 Encapsulation

Encapsulation means **bundling data and methods together and controlling how internal state is accessed or modified**.

Python does not enforce private access in the same way as some languages, but it provides conventions and mechanisms.

---

# 🟢 Public Members

Public members can be accessed normally.

```python
class Student:

    def __init__(self, name):
        self.name = name


student = Student("Rahul")

print(student.name)
```

---

# 🟡 Protected Convention

A single underscore indicates an internal/protected-by-convention member.

```python
class Student:

    def __init__(self):
        self._marks = 90
```

It can still technically be accessed:

```python
student = Student()

print(student._marks)
```

The underscore communicates:

> "This is intended for internal use/subclass use."

It is a convention, not strict access control.

---

# 🔴 Private Members

Double underscore triggers **name mangling**.

```python
class Student:

    def __init__(self):
        self.__marks = 90
```

Direct access:

```python
student = Student()

# print(student.__marks)
```

This normally raises an `AttributeError`.

---

# 🔍 Name Mangling

Python internally transforms:

```python
__marks
```

approximately into:

```text
_ClassName__marks
```

Example:

```python
class Student:

    def __init__(self):
        self.__marks = 90


student = Student()

print(student._Student__marks)
```

Output:

```text
90
```

This demonstrates that Python's `__private` mechanism is **name mangling**, not absolute security.

---

# 🎛️ Getters and Setters

Getters and setters are methods used to read or modify internal data.

Example:

```python
class Student:

    def __init__(self, marks):
        self.__marks = marks

    def get_marks(self):
        return self.__marks

    def set_marks(self, marks):
        if 0 <= marks <= 100:
            self.__marks = marks
        else:
            print("Invalid marks")


student = Student(80)

print(student.get_marks())

student.set_marks(95)

print(student.get_marks())
```

Output:

```text
80
95
```

---

# ⭐ @property

Python provides a cleaner way to implement controlled attribute access.

```python
class Student:

    def __init__(self, marks):
        self.__marks = marks

    @property
    def marks(self):
        return self.__marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self.__marks = value
        else:
            raise ValueError("Marks must be between 0 and 100")


student = Student(80)

print(student.marks)

student.marks = 95

print(student.marks)
```

This gives attribute-like syntax:

```python
student.marks
```

instead of:

```python
student.get_marks()
```

---

# 🧬 Inheritance

Inheritance allows a child class to **reuse and extend** functionality from a parent class.

Example:

```python
class Animal:

    def eat(self):
        print("Animal eats")


class Dog(Animal):

    def bark(self):
        print("Dog barks")


dog = Dog()

dog.eat()
dog.bark()
```

Output:

```text
Animal eats
Dog barks
```

Here:

```text
Animal
   ↑
   │
  Dog
```

---

# 👨‍👦 Parent and Child Classes

Terminology:

```text
Parent class
    ↓
Base class
    ↓
Superclass
```

and:

```text
Child class
    ↓
Derived class
    ↓
Subclass
```

Example:

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

`Animal` → Parent/Base class

`Dog` → Child/Derived class

---

# 1️⃣ Single Inheritance

One child inherits from one parent.

```text
Animal
   ↓
 Dog
```

Example:

```python
class Animal:

    def eat(self):
        print("Eating")


class Dog(Animal):

    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

---

# 2️⃣ Multilevel Inheritance

Inheritance occurs across multiple levels.

```text
Animal
   ↓
 Mammal
   ↓
  Dog
```

Example:

```python
class Animal:

    def eat(self):
        print("Eating")


class Mammal(Animal):

    def walk(self):
        print("Walking")


class Dog(Mammal):

    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.walk()
dog.bark()
```

---

# 3️⃣ Multiple Inheritance

One child inherits from multiple parent classes.

```text
Father     Mother
   \         /
    \       /
     Child
```

Example:

```python
class Father:

    def skills(self):
        print("Driving")


class Mother:

    def cooking(self):
        print("Cooking")


class Child(Father, Mother):
    pass


child = Child()

child.skills()
child.cooking()
```

Output:

```text
Driving
Cooking
```

---

# 4️⃣ Hierarchical Inheritance

Multiple child classes inherit from one parent.

```text
       Animal
       /    \
     Dog    Cat
```

Example:

```python
class Animal:

    def eat(self):
        print("Eating")


class Dog(Animal):

    def bark(self):
        print("Barking")


class Cat(Animal):

    def meow(self):
        print("Meowing")
```

---

# 5️⃣ Hybrid Inheritance

Hybrid inheritance combines multiple inheritance patterns.

Example:

```text
        A
       / \
      B   C
       \ /
        D
```

Python resolves complex inheritance using its Method Resolution Order (MRO).

---

# ⭐ super()

`super()` is used to access functionality from a parent class according to the inheritance hierarchy/MRO.

Example:

```python
class Animal:

    def __init__(self):
        print("Animal constructor")


class Dog(Animal):

    def __init__(self):
        super().__init__()
        print("Dog constructor")


dog = Dog()
```

Output:

```text
Animal constructor
Dog constructor
```

---

# 🔥 super() with Parameters

```python
class Person:

    def __init__(self, name):
        self.name = name


class Student(Person):

    def __init__(self, name, marks):
        super().__init__(name)
        self.marks = marks


student = Student("Rahul", 90)

print(student.name)
print(student.marks)
```

Output:

```text
Rahul
90
```

---

# 🔄 Method Overriding

When a child class provides its own implementation of an inherited method, it overrides the inherited implementation.

```python
class Animal:

    def sound(self):
        print("Animal sound")


class Dog(Animal):

    def sound(self):
        print("Bark")


dog = Dog()

dog.sound()
```

Output:

```text
Bark
```

---

# 🌀 Polymorphism

Polymorphism means **one interface can work with different types of objects**.

Example:

```python
class Dog:

    def sound(self):
        print("Bark")


class Cat:

    def sound(self):
        print("Meow")


def make_sound(animal):
    animal.sound()


dog = Dog()
cat = Cat()

make_sound(dog)
make_sound(cat)
```

Output:

```text
Bark
Meow
```

The same:

```python
make_sound()
```

works with different object types.

---

# 🦆 Duck Typing

Python uses a form of dynamic typing often described as **duck typing**.

The idea:

> If an object provides the required behavior, its exact class may not matter.

Example:

```python
class Dog:

    def speak(self):
        print("Bark")


class Person:

    def speak(self):
        print("Hello")


def speak(obj):
    obj.speak()


speak(Dog())
speak(Person())
```

Output:

```text
Bark
Hello
```

The function only cares that the object provides:

```python
speak()
```

---

# ➕ Operator Overloading

Python allows classes to define how operators behave for their objects using special methods.

Example:

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Number(self.value + other.value)


n1 = Number(10)
n2 = Number(20)

result = n1 + n2

print(result.value)
```

Output:

```text
30
```

Here:

```text
+
↓
__add__()
```

---

# 🔢 Common Operator Overloading Methods

| Operator | Method           |
| -------- | ---------------- |
| `+`      | `__add__()`      |
| `-`      | `__sub__()`      |
| `*`      | `__mul__()`      |
| `/`      | `__truediv__()`  |
| `//`     | `__floordiv__()` |
| `%`      | `__mod__()`      |
| `**`     | `__pow__()`      |
| `==`     | `__eq__()`       |
| `!=`     | `__ne__()`       |
| `<`      | `__lt__()`       |
| `>`      | `__gt__()`       |
| `<=`     | `__le__()`       |
| `>=`     | `__ge__()`       |

---

# ⚠️ Method Overloading

In languages such as Java or C++, you can define multiple methods with the same name but different parameter lists.

Python does **not** support traditional compile-time method overloading in the same way.

This:

```python
class Calculator:

    def add(self, a):
        return a

    def add(self, a, b):
        return a + b
```

does not create two overloaded methods.

The second definition replaces the first.

---

# ✅ How to Simulate Method Overloading

## Default Arguments

```python
class Calculator:

    def add(self, a, b=0):
        return a + b


calc = Calculator()

print(calc.add(10))
print(calc.add(10, 20))
```

Output:

```text
10
30
```

---

## `*args`

```python
class Calculator:

    def add(self, *numbers):
        return sum(numbers)


calc = Calculator()

print(calc.add(10))
print(calc.add(10, 20))
print(calc.add(10, 20, 30))
```

Output:

```text
10
30
60
```

---

# 🎭 Abstraction

Abstraction means exposing the essential interface while hiding implementation details.

Example:

```text
User
 ↓
withdraw()
 ↓
Bank system handles internal details
```

The user does not need to know every internal operation.

Python supports abstraction using mechanisms such as:

```text
abc module
abstract base classes
abstract methods
```

---

# 🏛️ Abstract Classes

An abstract class is intended to provide a common interface for subclasses and may contain abstract methods.

Python provides this through the `abc` module.

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass
```

You generally cannot instantiate an abstract class while required abstract methods remain unimplemented.

---

# 🔨 Abstract Methods

An abstract method declares functionality that subclasses are expected to implement.

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass


class Dog(Animal):

    def sound(self):
        print("Bark")


dog = Dog()

dog.sound()
```

Output:

```text
Bark
```

---

# 📦 abc Module

Import:

```python
from abc import ABC, abstractmethod
```

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


class Car(Vehicle):

    def start(self):
        print("Car starts")


car = Car()

car.start()
```

---

# ✨ Magic / Dunder Methods

Special methods surrounded by double underscores are commonly called **dunder methods**.

Example:

```python
__init__
__str__
__repr__
__len__
__eq__
__add__
```

They allow classes to integrate with Python's language features.

---

# ⭐ **init**()

Used to initialize an object.

```python
class Student:

    def __init__(self, name):
        self.name = name
```

---

# 🖨️ **str**()

Controls the human-readable string representation of an object.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student: {self.name}"


student = Student("Rahul")

print(student)
```

Output:

```text
Student: Rahul
```

---

# 🔍 **repr**()

Provides a representation intended to be useful for debugging/development.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Student({self.name!r})"


student = Student("Rahul")

print(repr(student))
```

Output:

```text
Student('Rahul')
```

A good `__repr__` often aims to be unambiguous and informative.

---

# 📏 **len**()

Defines behavior for:

```python
len(object)
```

Example:

```python
class Team:

    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)


team = Team(["A", "B", "C"])

print(len(team))
```

Output:

```text
3
```

---

# ⚖️ **eq**()

Defines equality comparison:

```python
==
```

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __eq__(self, other):
        return self.name == other.name


s1 = Student("Rahul")
s2 = Student("Rahul")

print(s1 == s2)
```

Output:

```text
True
```

---

# ➕ **add**()

Defines behavior for:

```python
+
```

Example:

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value


n1 = Number(10)
n2 = Number(20)

print(n1 + n2)
```

Output:

```text
30
```

---

# 🤝 Composition

Composition represents a strong **has-a** relationship where an object contains another object as part of its implementation.

Example:

```text
Car
 ↓
Engine
```

```python
class Engine:

    def start(self):
        print("Engine started")


class Car:

    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
        print("Car started")


car = Car()

car.start()
```

Output:

```text
Engine started
Car started
```

---

# 🤝 Aggregation

Aggregation is also a **has-a** relationship, but the contained object can exist independently of the container.

Example:

```python
class Teacher:

    def __init__(self, name):
        self.name = name


class Department:

    def __init__(self, teacher):
        self.teacher = teacher


teacher = Teacher("John")

department = Department(teacher)

print(department.teacher.name)
```

The `Teacher` object can exist independently of `Department`.

---

# 🔗 Association

Association means objects are related or interact with each other.

Example:

```python
class Student:

    def study(self):
        print("Student is studying")


class Teacher:

    def teach(self, student):
        print("Teacher is teaching")
        student.study()


student = Student()
teacher = Teacher()

teacher.teach(student)
```

The objects interact, but neither necessarily owns the other.

---

# 📊 Association vs Aggregation vs Composition

| Relationship | Meaning                                 |
| ------------ | --------------------------------------- |
| Association  | Objects are related/interact            |
| Aggregation  | Weak has-a relationship                 |
| Composition  | Stronger ownership/part-of relationship |

Simple memory trick:

```text
Association  → uses/knows
Aggregation  → has
Composition  → owns/contains
```

---

# 🔎 isinstance()

Checks whether an object is an instance of a class or compatible subclass.

```python
class Animal:
    pass


class Dog(Animal):
    pass


dog = Dog()

print(isinstance(dog, Dog))
print(isinstance(dog, Animal))
```

Output:

```text
True
True
```

---

# 🔎 issubclass()

Checks whether one class is a subclass of another.

```python
class Animal:
    pass


class Dog(Animal):
    pass


print(issubclass(Dog, Animal))
```

Output:

```text
True
```

---

# 🧭 MRO

MRO stands for:

**Method Resolution Order**

It determines the order in which Python searches classes for attributes and methods.

Example:

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass


print(C.mro())
```

Conceptually:

```text
C
↓
B
↓
A
↓
object
```

---

# 🔀 MRO with Multiple Inheritance

Example:

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        print("B")


class C(A):
    def show(self):
        print("C")


class D(B, C):
    pass


d = D()

d.show()

print(D.mro())
```

Python uses its MRO algorithm to determine which implementation is found first.

---

# ⭐ super() and MRO

`super()` does not simply mean "call my immediate parent."

It means:

> Continue attribute/method lookup according to the class's MRO.

This is especially important in multiple inheritance.

Example:

```python
class A:

    def show(self):
        print("A")


class B(A):

    def show(self):
        print("B")
        super().show()


class C(A):

    def show(self):
        print("C")
        super().show()


class D(B, C):
    pass


d = D()

d.show()
```

Output:

```text
B
C
A
```

This happens because of MRO.

---

# ♻️ Object Lifecycle

A simplified object lifecycle is:

```text
Class definition
      ↓
Object creation
      ↓
__new__()
      ↓
__init__()
      ↓
Object usage
      ↓
Object becomes unreachable
      ↓
Garbage collection / destruction
```

---

# 🏗️ **new**()

`__new__()` is responsible for creating/returning a new instance.

`__init__()` initializes an already-created instance.

Example:

```python
class Student:

    def __new__(cls, name):
        print("__new__ called")
        return super().__new__(cls)

    def __init__(self, name):
        print("__init__ called")
        self.name = name


student = Student("Rahul")
```

Output:

```text
__new__ called
__init__ called
```

For normal classes, you usually only need to define `__init__()`.

---

# 🗑️ Destructor — **del**()

Python provides:

```python
__del__()
```

which may be called when an object is being finalized.

Example:

```python
class Demo:

    def __del__(self):
        print("Object finalized")


obj = Demo()

del obj
```

Important:

* Do not rely on `__del__()` for critical resource cleanup.
* Timing of finalization can depend on the implementation and object lifetime.
* For files, sockets, database connections, etc., prefer context managers such as `with`.

---

# 📋 Copying Objects

Python provides:

```python
copy
```

module.

Two important concepts:

```text
Shallow Copy
Deep Copy
```

---

# 📄 Shallow Copy

A shallow copy creates a new outer object but does not recursively copy nested objects.

```python
import copy


original = [[1, 2], [3, 4]]

shallow = copy.copy(original)

print(original is shallow)
print(original[0] is shallow[0])
```

Output:

```text
False
True
```

The outer list is different, but the nested list is shared.

---

# 📚 Deep Copy

A deep copy recursively copies nested objects.

```python
import copy


original = [[1, 2], [3, 4]]

deep = copy.deepcopy(original)

print(original is deep)
print(original[0] is deep[0])
```

Output:

```text
False
False
```

---

# 🧮 Dataclasses

Python provides the `dataclasses` module to reduce boilerplate for classes primarily used to store data.

Example:

```python
from dataclasses import dataclass


@dataclass
class Student:
    name: str
    age: int
    marks: float


student = Student("Rahul", 20, 90.5)

print(student)
```

Output resembles:

```text
Student(name='Rahul', age=20, marks=90.5)
```

Dataclasses can automatically provide useful methods such as an initializer and representation, depending on configuration.

---

# ⚙️ Dataclass Example

```python
from dataclasses import dataclass


@dataclass
class Product:
    name: str
    price: float


p1 = Product("Laptop", 50000)

print(p1.name)
print(p1.price)
```

---

# 🏗️ Complete OOP Example

Let's build a small banking system.

```python
from abc import ABC, abstractmethod


class Account(ABC):

    bank_name = "ABC Bank"

    def __init__(self, account_number, owner, balance=0):
        self.account_number = account_number
        self.owner = owner
        self.__balance = balance

    @property
    def balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")

        self.__balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")

        if amount > self.__balance:
            raise ValueError("Insufficient balance")

        self.__balance -= amount

    @abstractmethod
    def account_type(self):
        pass

    def __str__(self):
        return (
            f"{self.account_type()} | "
            f"Owner: {self.owner} | "
            f"Balance: {self.balance}"
        )


class SavingsAccount(Account):

    def account_type(self):
        return "Savings Account"


class CurrentAccount(Account):

    def account_type(self):
        return "Current Account"


savings = SavingsAccount(
    "1001",
    "Rahul",
    10000
)

current = CurrentAccount(
    "1002",
    "Anita",
    20000
)

savings.deposit(5000)
savings.withdraw(2000)

current.deposit(10000)

print(savings)
print(current)
```

Output:

```text
Savings Account | Owner: Rahul | Balance: 13000
Current Account | Owner: Anita | Balance: 30000
```

This single example demonstrates:

```text
Class
Object
Constructor
Instance variables
Class variables
Encapsulation
Private attribute
Property
Inheritance
Abstraction
Abstract method
Method overriding
Polymorphism
Magic method
Validation
```

---

# 🧠 Four Pillars of OOP

The four commonly taught pillars are:

```text
             OOP
              │
     ┌────────┼────────┐
     │        │        │
Encapsulation Inheritance Polymorphism
              │
          Abstraction
```

More clearly:

## 1. Encapsulation

Bundling state and behavior together and controlling access to internal state.

```python
class Account:

    def __init__(self):
        self.__balance = 0
```

---

## 2. Inheritance

Creating a new class based on an existing class.

```python
class Dog(Animal):
    pass
```

---

## 3. Polymorphism

Different objects can respond to the same interface.

```python
dog.sound()
cat.sound()
```

---

## 4. Abstraction

Expose essential operations while hiding implementation details.

```python
from abc import ABC, abstractmethod
```

---

# 🧠 Class vs Object

| Class                      | Object                         |
| -------------------------- | ------------------------------ |
| Blueprint                  | Instance                       |
| Defines structure/behavior | Represents a concrete instance |
| Logical definition         | Runtime entity                 |
| Example: `Student`         | Example: `student1`            |
| Created using `class`      | Created by calling the class   |

Example:

```python
class Student:
    pass


student1 = Student()
```

```text
Student  → Class
student1 → Object
```

---

# 🧠 Instance Variable vs Class Variable

| Instance Variable                  | Class Variable                             |
| ---------------------------------- | ------------------------------------------ |
| Associated with instance           | Associated with class                      |
| Usually `self.variable`            | Usually `Class.variable` or `cls.variable` |
| Each object can have its own value | Shared class-level value unless shadowed   |
| Example: name                      | Example: school                            |

---

# 🧠 Instance Method vs Class Method vs Static Method

```text
Instance Method
      ↓
Uses self
      ↓
Works with object state


Class Method
      ↓
Uses cls
      ↓
Works with class state


Static Method
      ↓
No automatic self/cls
      ↓
Utility related to class
```

---

# ⚠️ Common OOP Mistakes

## Mistake 1 — Forgetting self

Wrong:

```python
class Student:

    def display():
        print("Hello")
```

Correct:

```python
class Student:

    def display(self):
        print("Hello")
```

---

## Mistake 2 — Forgetting `self.`

Wrong:

```python
class Student:

    def __init__(self, name):
        name = name
```

Correct:

```python
class Student:

    def __init__(self, name):
        self.name = name
```

---

## Mistake 3 — Confusing Class and Object

```python
class Student:
    pass


student = Student()
```

Remember:

```text
Student → class
student → object
```

---

## Mistake 4 — Incorrect Constructor

Correct:

```python
def __init__(self):
    pass
```

Not:

```python
def init(self):
    pass
```

---

## Mistake 5 — Confusing `__str__` and `__repr__`

```text
__str__  → human-readable representation
__repr__ → developer/debug representation
```

---

## Mistake 6 — Thinking `__private` Means Absolute Security

Python's double underscore causes name mangling.

It is not a security boundary.

---

## Mistake 7 — Forgetting `super()`

When a child class needs parent initialization:

```python
class Child(Parent):

    def __init__(self):
        super().__init__()
```

---

# 🎯 Interview Questions

### 1. What is OOP?

OOP is a programming paradigm based on objects containing state and behavior.

---

### 2. What is a class?

A class is a blueprint/template used to create objects.

---

### 3. What is an object?

An object is an instance of a class.

---

### 4. What is self?

`self` is the conventional reference to the current instance.

---

### 5. What is `__init__()`?

It is the initializer method that runs after an instance is created to initialize its state.

---

### 6. What is inheritance?

Inheritance allows a class to reuse and extend functionality from another class.

---

### 7. What is polymorphism?

Polymorphism allows a common interface to work with different object types.

---

### 8. What is encapsulation?

Encapsulation combines data and behavior and provides controlled access to internal state.

---

### 9. What is abstraction?

Abstraction focuses on essential interfaces while hiding unnecessary implementation details.

---

### 10. What is method overriding?

When a subclass provides its own implementation of an inherited method.

---

### 11. Does Python support method overloading?

Python does not provide traditional compile-time method overloading based solely on parameter lists. Default arguments, `*args`, or other techniques can provide similar flexibility.

---

### 12. What is multiple inheritance?

When one class inherits from more than one parent class.

```python
class C(A, B):
    pass
```

---

### 13. What is MRO?

MRO is the order in which Python searches classes for methods and attributes.

---

### 14. What is `super()`?

`super()` provides access to the next implementation in the class's MRO.

---

### 15. What is a static method?

A method that does not automatically receive an instance or class reference.

---

### 16. What is a class method?

A method that receives the class as its first conventional parameter, usually `cls`.

---

### 17. What is a magic method?

A special method with a double-underscore naming convention that integrates objects with Python language operations.

---

### 18. What is operator overloading?

Defining how operators behave for custom objects using special methods.

---

### 19. What is composition?

Building an object using other objects as components.

---

### 20. What is duck typing?

Using an object's available behavior rather than requiring a specific declared type.

---

# 🧪 Practice Programs

## Beginner

1. Create a `Student` class.
2. Create a `Car` class.
3. Create a `BankAccount` class.
4. Create a `Employee` class.
5. Use constructors.
6. Create instance variables.
7. Create class variables.
8. Create instance methods.
9. Create class methods.
10. Create static methods.

---

## Intermediate

11. Create a student management system.
12. Create a bank account system.
13. Create a library management system.
14. Implement single inheritance.
15. Implement multilevel inheritance.
16. Implement multiple inheritance.
17. Implement hierarchical inheritance.
18. Demonstrate method overriding.
19. Demonstrate polymorphism.
20. Implement encapsulation.

---

## Advanced

21. Create an abstract payment system.
22. Implement operator overloading.
23. Implement custom `__str__`.
24. Implement custom `__repr__`.
25. Create a class hierarchy using MRO.
26. Build a banking application using OOP.
27. Build an e-commerce application using OOP.
28. Build a library management application.
29. Build a vehicle management system.
30. Build a complete student management system.

---

# 🏆 OOP Revision Cheat Sheet

```text
CLASS
→ Blueprint for objects

OBJECT
→ Instance of a class

ATTRIBUTE
→ Data associated with an object/class

METHOD
→ Function defined inside a class

self
→ Current instance reference

__init__()
→ Initializes instance state

INSTANCE VARIABLE
→ Per-object state

CLASS VARIABLE
→ Class-level shared state

INSTANCE METHOD
→ Uses self

CLASS METHOD
→ Uses cls

STATIC METHOD
→ No automatic self/cls

ENCAPSULATION
→ Bundle/control access to state and behavior

PUBLIC
→ Normal attribute

_PROTECTED
→ Internal-use convention

__PRIVATE
→ Name mangling

INHERITANCE
→ Reuse/extend parent class

super()
→ Access next implementation in MRO

OVERRIDING
→ Child replaces inherited implementation

POLYMORPHISM
→ Common interface, different behavior

DUCK TYPING
→ Behavior matters more than declared type

ABSTRACTION
→ Essential interface, hidden implementation

ABC
→ Abstract Base Class support

@abstractmethod
→ Declares abstract method

OPERATOR OVERLOADING
→ Define operator behavior for objects

__str__()
→ Human-readable representation

__repr__()
→ Developer/debug representation

__len__()
→ Behavior for len()

__eq__()
→ Behavior for ==

__add__()
→ Behavior for +

COMPOSITION
→ Strong has-a/part-of relationship

AGGREGATION
→ Weaker has-a relationship

ASSOCIATION
→ Objects interact/are related

isinstance()
→ Check object's type relationship

issubclass()
→ Check class inheritance relationship

MRO
→ Method Resolution Order

__new__()
→ Creates/returns instance

__del__()
→ Finalization hook; don't rely on it for critical cleanup

DATACLASS
→ Convenient data-focused class generation
```

---

# 🔥 Most Important Code Patterns

## Class + Object

```python
class Student:

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student = Student("Rahul")

student.display()
```

---

## Inheritance

```python
class Animal:

    def eat(self):
        print("Eating")


class Dog(Animal):

    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

---

## Overriding

```python
class Animal:

    def sound(self):
        print("Animal sound")


class Dog(Animal):

    def sound(self):
        print("Bark")
```

---

## Polymorphism

```python
class Dog:

    def sound(self):
        print("Bark")


class Cat:

    def sound(self):
        print("Meow")


for animal in [Dog(), Cat()]:
    animal.sound()
```

---

## Encapsulation

```python
class BankAccount:

    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance
```

---

## Abstraction

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass
```

---

## Class Method

```python
class Student:

    school = "ABC"

    @classmethod
    def change_school(cls, name):
        cls.school = name
```

---

## Static Method

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b
```

---

## Operator Overloading

```python
class Number:

    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value
```

---

# 🎓 Final OOP Checklist

Before considering Python OOP complete, make sure you can explain and code:

* [ ] What is OOP?
* [ ] Advantages of OOP
* [ ] Class
* [ ] Object
* [ ] Attributes
* [ ] Methods
* [ ] `self`
* [ ] `__init__()`
* [ ] Instance variables
* [ ] Class variables
* [ ] Instance methods
* [ ] Class methods
* [ ] Static methods
* [ ] Encapsulation
* [ ] Public members
* [ ] Protected convention
* [ ] Private members
* [ ] Name mangling
* [ ] Getters
* [ ] Setters
* [ ] `@property`
* [ ] Inheritance
* [ ] Single inheritance
* [ ] Multilevel inheritance
* [ ] Multiple inheritance
* [ ] Hierarchical inheritance
* [ ] Hybrid inheritance
* [ ] `super()`
* [ ] Method overriding
* [ ] Polymorphism
* [ ] Duck typing
* [ ] Operator overloading
* [ ] Method overloading limitations
* [ ] Abstraction
* [ ] Abstract classes
* [ ] Abstract methods
* [ ] `ABC`
* [ ] `@abstractmethod`
* [ ] Magic/dunder methods
* [ ] `__str__()`
* [ ] `__repr__()`
* [ ] `__len__()`
* [ ] `__eq__()`
* [ ] `__add__()`
* [ ] Composition
* [ ] Aggregation
* [ ] Association
* [ ] `isinstance()`
* [ ] `issubclass()`
* [ ] MRO
* [ ] `__new__()`
* [ ] `__del__()`
* [ ] Shallow copy
* [ ] Deep copy
* [ ] Dataclasses

---

# 🏁 Final Mental Model

```text
                         OOP
                          │
             ┌────────────┼────────────┐
             │            │            │
           CLASS        OBJECT       METHODS
             │            │
             │       ┌────┴────┐
             │       │         │
         Attributes  State   Behavior
             │
      ┌──────┴───────┐
      │              │
 Instance          Class
 Variables        Variables
      │
      └──────────────┐
                     │
                 INHERITANCE
                     │
              ┌──────┴──────┐
              │             │
           Override      super()
              │
              ↓
         POLYMORPHISM
              │
              ↓
         ABSTRACTION
              │
              ↓
        ENCAPSULATION
```

## ⭐ One-Line Memory Trick

```text
Class       → Blueprint
Object      → Instance
self        → Current object
__init__    → Initialize object
Inheritance → Reuse/extend
super()     → Continue through inheritance hierarchy
Override    → Replace inherited behavior
Polymorphism→ Same interface, different behavior
Encapsulation→ Control internal state
Abstraction → Hide implementation details
ABC         → Abstract interface
MRO         → Method lookup order
Dunder      → Special Python behavior
Composition → Has-a / part-of
```

**Master these concepts and you have the core Python OOP foundation needed for interviews, projects, and frameworks such as Django and Flask.**
