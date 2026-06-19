# Constructors in Python

## Introduction

Constructors are special methods used to initialize objects when they are created from a class. They help assign initial values to object attributes and prepare objects for use. In Python, constructors are primarily implemented using the `__init__()` method. Object creation itself is handled by `__new__()`, while `__init__()` initializes the created object.

### Key Features

- Automatically called when an object is created.
- Initialize object attributes with values.
- Support both default and parameterized initialization.
- Improve code organization and readability.
- Enable creation of objects with different data.

## Why Constructors?

Constructors eliminate the need to assign values manually after creating an object.

### Example Without Constructor

```python
class Student:
    pass

student = Student()

student.name = "Akash Dangudubiyyapu"
student.age = 22

print(student.name)
print(student.age)
```

### Output
Akash Dangudubiyyapu
22

### Limitation

Values must be assigned manually every time an object is created. Constructors automate this process.

# **new**() Method

The `__new__()` method creates and returns a new object. It is executed before `__init__()`.

### Syntax

```python
class ClassName:
    def __new__(cls):
        instance = super().__new__(cls)
        return instance
```

### Explanation

- `__new__()` creates the object.
- It returns the newly created instance.
- It is rarely overridden in normal programs.

# **init**() Method

The `__init__()` method initializes the object after it has been created.

### Syntax

```python
class ClassName:
    def __init__(self):
        pass
```

### Explanation

- `__init__()` initializes object attributes.
- It is automatically called after object creation.
- It returns `None`.

# Difference Between **new**() and **init**()

| Feature | **new**() | **init**() |
| --- | --- | --- |
| Purpose | Creates object | Initializes object |
| Called | Before initialization | After object creation |
| Return Value | Object instance | None |
| Usage | Rarely overridden | Frequently used |
| Main Purpose | Memory allocation | Assigning attribute values |

# Default Constructor

A default constructor does not accept additional arguments except `self`. It initializes objects with predefined values.

### Example

```python
class Course:
    def __init__(self):
        self.platform = "AlphaKnowledge"
        self.language = "Python"

course = Course()

print(course.platform)
print(course.language)
```

### Output
AlphaKnowledge
Python

### Explanation

- The constructor automatically assigns default values.
- No arguments are passed while creating the object.
- The object receives predefined values.

# Parameterized Constructor

A parameterized constructor accepts arguments and initializes objects with custom values.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

student = Student(
    "Mohit Chandaluri",
    23
)

print(student.name)
print(student.age)
```

### Output
Mohit Chandaluri
23

### Explanation

- The constructor receives values during object creation.
- These values are stored inside instance attributes.
- Different objects can have different data.

# Creating Multiple Objects

A single class can create multiple objects using the same constructor.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

student1 = Student("Abhiram Gopisetti")
student2 = Student("Adapa Hemesh")
student3 = Student("Hemanth Akhil")

print(student1.name)
print(student2.name)
print(student3.name)
```

### Output
Abhiram Gopisetti
Adapa Hemesh
Hemanth Akhil

### Explanation

Each object stores its own data independently while sharing the same class structure.

# Constructor with Methods

Constructors are often used together with methods.

### Example

```python
class Mentor:
    def __init__(self, name):
        self.name = name

    def display(self):
        print("Mentor:", self.name)

mentor = Mentor("Mohit Chandaluri")

mentor.display()
```

### Output
Mentor: Mohit Chandaluri

### Explanation

The constructor initializes the object, and the method uses the initialized data.

# Advantages of Constructors

1. Automatically initialize object attributes.
2. Reduce repetitive code.
3. Improve readability and maintainability.
4. Support multiple objects with different values.
5. Simplify object creation.

# Limitations

1. Incorrect arguments can cause runtime errors.
2. Complex constructors may reduce readability.
3. Large classes may require multiple parameters.

# Summary

Constructors are special methods that initialize objects in Python. The `__new__()` method creates an object, while `__init__()` initializes it with values. Constructors can be default or parameterized, allowing objects to be created with predefined or custom data. Understanding constructors is essential for building organized, reusable, and scalable object-oriented programs.

