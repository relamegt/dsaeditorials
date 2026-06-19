# Python OOP Concepts

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm that organizes code using classes and objects. It helps developers create reusable, modular, and maintainable applications by modeling real-world entities and their behavior.

OOP focuses on combining data and functions into a single unit called an object.

### Features of OOP

- Organizes programs using classes and objects.
- Promotes code reusability.
- Supports modular programming.
- Makes code easier to maintain.
- Provides abstraction and security.
- Enables inheritance and polymorphism.

---

# What is a Class?

A class is a blueprint used to create objects. It defines the attributes and methods that its objects will have.

### Characteristics of a Class

- Created using the `class` keyword.
- Contains variables and methods.
- Acts as a template for objects.
- Supports code reuse.

## Creating a Class

```python
class Student:
    college = "AlphaKnowledge"

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

### Explanation

- `Student` is the class name.
- `college` is a class attribute shared by all objects.
- `__init__()` is the constructor.
- `self.name` and `self.age` are instance attributes.

---

# What is an Object?

An object is an instance of a class. It contains data and can perform operations defined inside the class.

### Components of an Object

1. State (Attributes)
2. Behavior (Methods)
3. Identity

## Creating Objects

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

student1 = Student("Akash Dangudubiyyapu", 22)

print(student1.name)
print(student1.age)
```

### Output
Akash Dangudubiyyapu
22

### Explanation

The object `student1` stores its own values for name and age.

---

# Attributes in OOP

Attributes are variables associated with classes and objects.

## Class Attributes

Shared among all objects.

```python
class Student:
    platform = "AlphaKnowledge"
```

## Instance Attributes

Unique to each object.

```python
class Student:

    def __init__(self, name):
        self.name = name
```

---

# Methods in OOP

Methods are functions defined inside a class.

```python
class Student:

    def __init__(self, name):
        self.name = name

    def display(self):
        print("Name:", self.name)

student = Student("Mohit Chandaluri")
student.display()
```

### Output
Name: Mohit Chandaluri

---

# Constructor in Python

A constructor initializes object data automatically when an object is created.

```python
class Employee:

    def __init__(self, name):
        self.name = name

emp = Employee("Abhiram Gopisetti")
print(emp.name)
```

### Output
Abhiram Gopisetti

---

# Four Pillars of OOP

Object-Oriented Programming is built on four fundamental concepts:

1. Inheritance
2. Polymorphism
3. Encapsulation
4. Abstraction

---

# Inheritance

Inheritance allows one class to acquire properties and methods from another class.

## Example

```python
class Person:

    def speak(self):
        print("Person can speak")

class Student(Person):
    pass

obj = Student()
obj.speak()
```

### Output
Person can speak

### Benefits

- Code reusability.
- Hierarchical relationships.
- Reduced duplication.

---

# Types of Inheritance

## Single Inheritance

```python
class A:
    pass

class B(A):
    pass
```

## Multilevel Inheritance

```python
class A:
    pass

class B(A):
    pass

class C(B):
    pass
```

## Multiple Inheritance

```python
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

## Hierarchical Inheritance

```python
class A:
    pass

class B(A):
    pass

class C(A):
    pass
```

---

# Polymorphism

Polymorphism means one interface with multiple behaviors.

## Example

```python
class Cat:

    def sound(self):
        print("Meow")

class Dog:

    def sound(self):
        print("Bark")

animals = [Cat(), Dog()]

for animal in animals:
    animal.sound()
```

### Output
Meow
Bark

### Advantages

- Flexibility.
- Easier maintenance.
- Better code reuse.

---

# Encapsulation

Encapsulation combines data and methods into a single unit and restricts direct access.

## Example

```python
class Account:

    def __init__(self):
        self.__balance = 10000

    def get_balance(self):
        return self.__balance

obj = Account()

print(obj.get_balance())
```

### Output
10000

### Benefits

- Data security.
- Controlled access.
- Better maintainability.

---

# Abstraction

Abstraction hides implementation details and shows only essential information.

## Example

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):

    def area(self):
        return 20

obj = Rectangle()
print(obj.area())
```

### Output
20

### Advantages

- Simplifies complexity.
- Improves readability.
- Enhances security.

---

# Access Specifiers

## Public Members

```python
class Student:

    def __init__(self):
        self.name = "Akhil"
```

Accessible everywhere.

---

## Protected Members

```python
class Student:

    def __init__(self):
        self._name = "Adapa Hemesh"
```

Intended for internal use.

---

## Private Members

```python
class Student:

    def __init__(self):
        self.__name = "Hemanth"
```

Cannot be accessed directly outside the class.

---

# Instance Methods

```python
class Student:

    def show(self):
        print("Instance Method")
```

---

# Class Methods

```python
class Student:

    college = "AlphaKnowledge"

    @classmethod
    def display(cls):
        print(cls.college)
```

---

# Static Methods

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b

print(Calculator.add(5, 10))
```

### Output
15

---

# Advantages of OOP

1. Code reusability.
2. Easier maintenance.
3. Improved modularity.
4. Better security.
5. Reduced redundancy.
6. Scalability.
7. Real-world modeling.

---

# Limitations of OOP

1. Requires more memory.
2. Initial design takes time.
3. Can increase program complexity.
4. Not suitable for every problem.

---

# Applications of OOP

- Web Development
- Game Development
- GUI Applications
- Banking Systems
- Management Systems
- E-Commerce Platforms
- Machine Learning Projects

---

# Summary

Object-Oriented Programming is a methodology that organizes software using classes and objects. It provides four major principles—inheritance, polymorphism, encapsulation, and abstraction—which help developers build modular, reusable, secure, and maintainable applications.

