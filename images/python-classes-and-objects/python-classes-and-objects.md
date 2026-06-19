# Python Classes and Objects

## Introduction

Classes and objects are fundamental concepts of Object-Oriented Programming (OOP). A class acts as a blueprint that defines the properties and behaviors of objects. An object is an instance created from a class. Using classes and objects helps organize code, improve reusability, and simplify maintenance.

### Key Features

- Classes act as blueprints for creating objects.
- Objects store their own data and behavior.
- Multiple objects can be created from the same class.
- Constructors initialize object data automatically.
- Special methods can customize object behavior.

## Why Classes and Objects?

Without classes, managing related data and functions becomes difficult. Classes allow us to group them together in a structured way.

### Example Without Classes

```python
name = "Akash Dangudubiyyapu"
age = 22

print(name)
print(age)
```

### Output
Akash Dangudubiyyapu
22

### Limitation

As the amount of data grows, managing separate variables becomes difficult. Classes provide a better way to organize related information.

# Creating a Class

A class is defined using the `class` keyword. It contains attributes and methods that describe the behavior of objects.

### Example

```python
class Student:
    course = "Python"
```

### Explanation

- `Student` is the class name.
- `course` is a class attribute shared by all objects.

# Creating Objects

An object is created by calling the class.

### Example

```python
class Student:
    course = "Python"

student1 = Student()

print(student1.course)
```

### Output
Python

### Explanation

`student1` is an object of the `Student` class and can access the class attribute using the dot operator.

# Initializing Objects with **init**()

The `__init__()` method is automatically executed whenever an object is created. It initializes object-specific data.

### Example

```python
class Student:
    institute = "AlphaKnowledge"

    def __init__(self, name, age):
        self.name = name
        self.age = age

student1 = Student(
    "Akash Dangudubiyyapu",
    22
)

print(student1.name)
print(student1.institute)
```

### Output
Akash Dangudubiyyapu
AlphaKnowledge

### Explanation

- `self` refers to the current object.
- `name` and `age` are instance attributes.
- `institute` is a class attribute shared by all objects.

# Multiple Objects

A class can create multiple objects, each having different data.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

student1 = Student("Mohit Chandaluri")
student2 = Student("Abhiram Gopisetti")

print(student1.name)
print(student2.name)
```

### Output
Mohit Chandaluri
Abhiram Gopisetti

### Explanation

Each object stores its own value independently.

# Using Methods

Methods define the behavior of objects.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print("Student:", self.name)

student1 = Student("Adapa Hemesh")

student1.display()
```

### Output
Student: Adapa Hemesh

### Explanation

The `display()` method uses the current object through `self`.

# **str**() Method

The `__str__()` method provides a readable representation of an object.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old"

student = Student(
    "Hemanth Akhil",
    23
)

print(student)
```

### Output
Hemanth Akhil is 23 years old

### Explanation

When the object is printed, Python automatically calls the `__str__()` method.

# Difference Between Class and Object

| Class | Object |
| --- | --- |
| Blueprint for creating objects | Instance of a class |
| Defines attributes and methods | Uses attributes and methods |
| Created using the `class` keyword | Created by calling the class |
| Does not occupy memory for instance data | Stores actual data |

# Advantages of Classes and Objects

1. Improve code organization.
2. Promote code reusability.
3. Simplify maintenance.
4. Support Object-Oriented Programming concepts.
5. Make programs modular and scalable.

# Limitations

1. Simple programs may not require classes.
2. Improper design can increase complexity.
3. Large class hierarchies can become difficult to maintain.

# Summary

Classes and objects are the building blocks of Object-Oriented Programming in Python. A class acts as a blueprint, while objects are instances created from that blueprint. Constructors initialize object data, methods define behavior, and special methods like `__str__()` provide customized output. Understanding classes and objects is essential for developing structured, reusable, and scalable Python applications.

