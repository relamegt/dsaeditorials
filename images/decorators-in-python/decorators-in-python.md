# Decorators in Python

## Introduction

Decorators are a powerful feature in Python used to modify or extend the behavior of functions and methods without changing their original code. A decorator is simply a function that takes another function as input and returns a new function with additional functionality.

Decorators are commonly used for logging, authentication, caching, validation, timing execution, and many other tasks. They promote code reusability and help separate additional functionality from business logic.

### Key Features

- Modify functions without changing their source code.
- Functions are treated as first-class objects.
- Built using higher-order functions.
- Support reusable and modular code.
- Can accept functions with arguments.
- Multiple decorators can be applied together.
- Commonly used for logging, caching, and authentication.

# Why Use Decorators?

Decorators allow adding functionality before or after a function executes without modifying the original function itself.

### Example

```python
def decorator(func):

    def wrapper():

        print("Before calling function")

        func()

        print("After calling function")

    return wrapper

@decorator
def greet():

    print("Hello, World!")

greet()
```

### Output
Before calling function
Hello, World!
After calling function

### Explanation

The decorator wraps the original function and adds extra statements before and after its execution.

# How Decorators Work

Decorators work because functions are first-class objects in Python.

### Example

```python
def greet():

    print("Hello")

fun = greet

fun()
```

### Output
Hello

### Explanation

Functions can be assigned to variables and called using those variables.

# Syntax of Decorators

### Syntax

```python
def decorator_name(function):

    def wrapper():

        statements

        function()

        statements

    return wrapper

@decorator_name
def function_name():

    statements
```

### Explanation

- The decorator takes a function as input.
- It defines an inner function called wrapper.
- Additional code is executed inside wrapper.
- The wrapper function is returned.

# Decorator with Parameters

Decorators often need to work with functions that accept arguments. For this, `*args` and `**kwargs` are used.

### Example

```python
def decorator(func):

    def wrapper(*args, **kwargs):

        print("Before execution")

        result = func(*args, **kwargs)

        print("After execution")

        return result

    return wrapper

@decorator
def add(a, b):

    return a + b

print(add(5, 3))
```

### Output
Before execution
After execution
8

### Explanation

The wrapper accepts any number of positional and keyword arguments and forwards them to the original function.

# Higher-Order Functions

Decorators are higher-order functions because they take functions as arguments and return functions.

### Example

```python
def apply(function, value):

    return function(value)

def square(x):

    return x * x

print(apply(square, 5))
```

### Output
25

### Explanation

The function `apply()` receives another function and executes it.

# Function Decorators

Function decorators enhance ordinary functions.

### Example

```python
def simple_decorator(func):

    def wrapper():

        print("Starting function")

        func()

        print("Function completed")

    return wrapper

@simple_decorator
def greet():

    print("Hello, Python!")

greet()
```

### Output
Starting function
Hello, Python!
Function completed

### Explanation

The decorator executes additional code before and after the original function.

# Method Decorators

Method decorators work with class methods and handle the `self` parameter.

### Example

```python
def method_decorator(func):

    def wrapper(self):

        print("Before method")

        func(self)

        print("After method")

    return wrapper

class Student:

    @method_decorator
    def show(self):

        print("Student Method")

obj = Student()

obj.show()
```

### Output
Before method
Student Method
After method

### Explanation

The wrapper accepts `self`, allowing decorators to work with instance methods.

# Class Decorators

Class decorators modify or enhance classes.

### Example

```python
def add_name(cls):

    cls.class_name = cls.__name__

    return cls

@add_name
class Person:

    pass

print(Person.class_name)
```

### Output
Person

### Explanation

The decorator adds a new attribute named `class_name` to the class.

# Built-in Decorators

Python provides several built-in decorators.

## 1. @staticmethod

Used when a method does not depend on object instances.

### Example

```python
class Math:

    @staticmethod
    def add(a, b):

        return a + b

print(Math.add(5, 7))
```

### Output
12

### Explanation

Static methods can be called directly through the class.

## 2. @classmethod

Used when a method works with the class itself.

### Example

```python
class Employee:

    increment = 1.05

    @classmethod
    def set_increment(cls, value):

        cls.increment = value

Employee.set_increment(1.10)

print(Employee.increment)
```

### Output
1.1

### Explanation

Class methods receive the class as the first argument using `cls`.

## 3. @property

Used to access methods like attributes.

### Example

```python
class Circle:

    def __init__(self, radius):

        self.radius = radius

    @property
    def area(self):

        return 3.14 * self.radius * self.radius

c = Circle(5)

print(c.area)
```

### Output
78.5

### Explanation

The method `area()` can be accessed without parentheses.

# Chaining Multiple Decorators

Multiple decorators can be applied to the same function.

### Example

```python
def decor1(func):

    def wrapper():

        return func() * 2

    return wrapper

def decor2(func):

    def wrapper():

        return func() ** 2

    return wrapper

@decor2
@decor1
def number():

    return 10

print(number())
```

### Output
400

### Explanation

Execution happens from bottom to top.

1. `number()` returns 10.
2. `decor1` multiplies by 2 to produce 20.
3. `decor2` squares the result to produce 400.

# Practical Applications of Decorators

## Logging

### Example

```python
def logger(func):

    def wrapper():

        print("Function started")

        func()

        print("Function ended")

    return wrapper

@logger
def display():

    print("Displaying data")

display()
```

### Output
Function started
Displaying data
Function ended

## Timing Execution

### Example

```python
import time

def timer(func):

    def wrapper():

        start = time.time()

        func()

        end = time.time()

        print(end - start)

    return wrapper

@timer
def task():

    for i in range(1000000):

        pass

task()
```

### Output
0.0...

### Explanation

The decorator measures execution time.

# Advantages of Decorators

1. Improve code reusability.
2. Avoid modifying original functions.
3. Promote modular programming.
4. Separate additional functionality from business logic.
5. Simplify logging and authentication.
6. Reduce code duplication.

# Limitations of Decorators

1. Can make debugging difficult.
2. Multiple nested decorators may reduce readability.
3. Incorrect wrappers can hide function metadata.
4. Extra layers introduce slight overhead.

# Applications of Decorators

- Logging
- Authentication
- Authorization
- Caching
- Memoization
- Input validation
- Performance measurement
- Retry mechanisms
- Web frameworks such as Flask and Django

# Decorators vs Normal Functions

| Feature | Decorators | Normal Functions |
| --- | --- | --- |
| Purpose | Enhance existing functions | Perform specific tasks |
| Input | Functions | Any data |
| Output | Modified functions | Values |
| Reusability | High | Moderate |
| Common Uses | Logging, caching, authentication | General programming |

# Summary

Decorators are functions that modify or extend the behavior of other functions without changing their source code. They rely on first-class functions and higher-order functions, making Python highly flexible and expressive. Decorators are widely used for logging, authentication, caching, validation, and performance monitoring. Built-in decorators such as `@staticmethod`, `@classmethod`, and `@property` provide additional functionality for classes. Understanding decorators is essential for writing clean, reusable, and maintainable Python programs.

