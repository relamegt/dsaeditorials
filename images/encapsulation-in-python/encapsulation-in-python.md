# Encapsulation in Python

## Introduction

Encapsulation is one of the four fundamental principles of Object-Oriented Programming (OOP). It refers to the process of combining data and methods into a single unit and controlling access to internal data. Encapsulation helps protect data from unintended modifications and provides a secure way to interact with object attributes.

Python supports encapsulation using public, protected, and private members.

### Key Features

- Combines data and methods inside a class.
- Protects data from unauthorized access.
- Improves maintainability and readability.
- Provides controlled access using getter and setter methods.
- Helps achieve abstraction by hiding implementation details.

## Why Encapsulation?

Without encapsulation, object data can be modified directly, which may lead to incorrect or inconsistent values.

### Example Without Encapsulation

```python
class Product:

    def __init__(self):
        self.price = 2500

item = Product()

item.price = -1000

print(item.price)
```

### Output
-1000

### Limitation

The price becomes negative because there is no control over updating the value.

# Encapsulation Example

Encapsulation protects internal data by restricting direct access.

### Example

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.__marks = marks

student = Student(
    "Sai Teja",
    90
)

print(student.name)

print(student.__marks)
```

### Output
Sai Teja

AttributeError:
'Student' object has no attribute '__marks'

### Explanation

- `name` is a public attribute.
- `__marks` is a private attribute.
- Public attributes can be accessed directly.
- Private attributes cannot be accessed directly outside the class.

# Why Do We Need Encapsulation?

1. Protects object data.
2. Prevents accidental modifications.
3. Simplifies maintenance.
4. Provides controlled access to variables.
5. Makes programs more secure and modular.

# Access Specifiers

Python supports three types of access specifiers.

## 1. Public Members

Public members can be accessed from anywhere.

### Example

```python
class Teacher:

    def __init__(self, subject):
        self.subject = subject

    def show_subject(self):
        print(self.subject)

mentor = Teacher(
    "Python"
)

mentor.show_subject()

print(mentor.subject)
```

### Output
Python
Python

### Explanation

- `subject` is public.
- `show_subject()` is a public method.
- Both are accessible outside the class.

# 2. Protected Members

Protected members are intended to be used inside the class and its subclasses.

### Example

```python
class Device:

    def __init__(self, brand):
        self._brand = brand

class Laptop(Device):

    def display_brand(self):
        print(
            self._brand
        )

lap = Laptop(
    "Lenovo"
)

lap.display_brand()
```

### Output
Lenovo

### Explanation

- `_brand` is a protected attribute.
- It can be accessed inside derived classes.
- It should not be used directly outside the class hierarchy.

# 3. Private Members

Private members are accessible only inside the class.

### Example

```python
class Account:

    def __init__(self):
        self.__pin = 1234

    def show_pin(self):
        print(
            self.__pin
        )

user = Account()

user.show_pin()
```

### Output
1234

### Explanation

- `__pin` is private.
- It can be accessed only through methods of the same class.
- Direct access outside the class raises an error.

# Protected and Private Methods

Methods can also be protected and private.

### Example

```python
class SmartLight:

    def __init__(self):
        self.status = "OFF"

    def _display_status(self):
        print(
            self.status
        )

    def __switch_on(self):
        self.status = "ON"

    def turn_on(self):
        self.__switch_on()
        self._display_status()

lamp = SmartLight()

lamp.turn_on()
```

### Output
ON

### Explanation

- `_display_status()` is a protected method.
- `__switch_on()` is a private method.
- `turn_on()` is a public method that uses both internally.

# Getter and Setter Methods

Getter methods retrieve private data and setter methods update it safely.

### Example

```python
class Course:

    def __init__(self):
        self.__duration = 30

    def get_duration(self):
        return self.__duration

    def set_duration(self, days):

        if days > 0:
            self.__duration = days
        else:
            print(
                "Invalid Duration"
            )

python_course = Course()

print(
    python_course.get_duration()
)

python_course.set_duration(
    45
)

print(
    python_course.get_duration()
)
```

### Output
30
45

### Explanation

- `get_duration()` returns the private value.
- `set_duration()` updates the value after validation.
- Invalid values can be prevented.

# Name Mangling

Python internally changes private variable names to avoid accidental access.

### Example

```python
class Employee:

    def __init__(self):
        self.__id = 101

emp = Employee()

print(
    emp._Employee__id
)
```

### Output
101

### Explanation

Python internally converts `__id` into `_Employee__id`. This process is called name mangling.

# Advantages of Encapsulation

1. Protects sensitive data.
2. Improves code readability.
3. Supports modular programming.
4. Makes maintenance easier.
5. Allows validation through setter methods.

# Limitations

1. Adds extra methods to access data.
2. Slightly increases code complexity.
3. Excessive encapsulation may reduce flexibility.

# Summary

Encapsulation is an OOP principle that binds data and methods together while restricting direct access to internal details. Python implements encapsulation using public, protected, and private members. Getter and setter methods provide controlled access to private data, improving security, maintainability, and modularity of applications.

