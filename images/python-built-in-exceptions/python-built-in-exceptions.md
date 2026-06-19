# Python Built-in Exceptions

## Introduction

Python provides several built-in exceptions that help identify and handle different types of runtime errors. These exceptions make programs more reliable and easier to debug by providing meaningful error information.

Built-in exceptions are organized in a hierarchy, where most exceptions inherit from the `Exception` class.

### Key Features

- Detects runtime errors automatically.
- Provides meaningful error messages.
- Supports structured exception handling.
- Helps prevent unexpected program termination.
- Allows different exceptions to be handled separately.

## Why Built-in Exceptions?

During program execution, unexpected situations may arise. Built-in exceptions help programs recognize these problems and respond appropriately.

### Example

```python
number = 100

try:

    result = number / 0

except ZeroDivisionError:

    print(
        "Cannot divide by zero."
    )
```

### Output
Cannot divide by zero.

### Explanation

Division by zero raises a `ZeroDivisionError`, which is handled safely using `try-except`.

# Common Built-in Exceptions

## 1. Exception

`Exception` is the base class for most built-in exceptions.

### Example

```python
try:

    raise Exception(
        "General exception occurred."
    )

except Exception as error:

    print(error)
```

### Output
General exception occurred.

### Explanation

The exception is raised manually and then handled.

# ZeroDivisionError

This exception occurs when a number is divided by zero.

### Example

```python
try:

    answer = 50 / 0

except ZeroDivisionError:

    print(
        "Division by zero is invalid."
    )
```

### Output
Division by zero is invalid.

### Explanation

Python raises a `ZeroDivisionError` because division by zero is mathematically undefined.

# ValueError

A `ValueError` occurs when a function receives an argument with an invalid value.

### Example

```python
try:

    marks = int(
        "AlphaKnowledge"
    )

except ValueError:

    print(
        "Invalid numeric value."
    )
```

### Output
Invalid numeric value.

### Explanation

The string `"AlphaKnowledge"` cannot be converted into an integer.

# TypeError

This exception occurs when incompatible data types are used together.

### Example

```python
try:

    total = "100" + 50

except TypeError:

    print(
        "Unsupported operation."
    )
```

### Output
Unsupported operation.

### Explanation

Strings and integers cannot be added directly.

# IndexError

Raised when an index is outside the valid range.

### Example

```python
subjects = [
    "Python",
    "Java",
    "SQL"
]

try:

    print(
        subjects[5]
    )

except IndexError:

    print(
        "Index is out of range."
    )
```

### Output
Index is out of range.

### Explanation

The list contains only three elements, so index 5 is invalid.

# KeyError

Raised when a dictionary key does not exist.

### Example

```python
student = {

    "name": "Akash",

    "cgpa": 9.24

}

try:

    print(
        student["age"]
    )

except KeyError:

    print(
        "Key not found."
    )
```

### Output
Key not found.

### Explanation

The dictionary does not contain the key `"age"`.

# NameError

Occurs when a variable is used before being defined.

### Example

```python
try:

    print(
        course_name
    )

except NameError:

    print(
        "Variable does not exist."
    )
```

### Output
Variable does not exist.

### Explanation

`course_name` has not been defined.

# AttributeError

Occurs when an object does not contain a requested attribute.

### Example

```python
number = 50

try:

    number.append(
        10
    )

except AttributeError:

    print(
        "Attribute not available."
    )
```

### Output
Attribute not available.

### Explanation

Integers do not support the `append()` method.

# FileNotFoundError

Raised when a requested file cannot be found.

### Example

```python
try:

    file = open(
        "notes.txt"
    )

except FileNotFoundError:

    print(
        "File does not exist."
    )
```

### Output
File does not exist.

### Explanation

Python cannot find the specified file.

# AssertionError

Occurs when an assertion condition fails.

### Example

```python
try:

    assert 5 > 10, \
    "Condition failed"

except AssertionError as error:

    print(error)
```

### Output
Condition failed

### Explanation

The condition evaluates to False, causing an `AssertionError`.

# OverflowError

Raised when a numeric operation exceeds supported limits.

### Example

```python
import math

try:

    result = math.exp(
        1000
    )

except OverflowError:

    print(
        "Number too large."
    )
```

### Output
Number too large.

### Explanation

The exponential value exceeds Python's floating-point limit.

# MemoryError

Occurs when there is insufficient memory available.

### Example

```python
try:

    values = [1] * (
        10 ** 12
    )

except MemoryError:

    print(
        "Insufficient memory."
    )
```

### Output
Insufficient memory.

### Explanation

The system cannot allocate enough memory for the operation.

# StopIteration

Raised when an iterator has no more elements.

### Example

```python
courses = iter(
    ["Python"]
)

try:

    print(
        next(courses)
    )

    print(
        next(courses)
    )

except StopIteration:

    print(
        "No more elements."
    )
```

### Output
Python
No more elements.

### Explanation

The iterator is exhausted after returning all values.

# ImportError

Raised when a module cannot be imported.

### Example

```python
try:

    import alphaknowledge

except ImportError:

    print(
        "Module not found."
    )
```

### Output
Module not found.

### Explanation

Python cannot locate the specified module.

# KeyboardInterrupt

Occurs when the user interrupts execution using Ctrl + C.

### Example

```python
try:

    while True:

        pass

except KeyboardInterrupt:

    print(
        "Program interrupted."
    )
```

### Output
Program interrupted.

### Explanation

The exception is raised when the user presses Ctrl + C.

# Built-in Exceptions Table

| Exception | Description |
| --- | --- |
| ZeroDivisionError | Division by zero |
| ValueError | Invalid value |
| TypeError | Incompatible types |
| IndexError | Invalid index |
| KeyError | Missing dictionary key |
| NameError | Undefined variable |
| AttributeError | Missing attribute |
| FileNotFoundError | File not found |
| AssertionError | Failed assertion |
| ImportError | Import failure |
| MemoryError | Insufficient memory |
| StopIteration | End of iteration |
| KeyboardInterrupt | User interruption |

# Advantages of Built-in Exceptions

1. Simplify debugging.
2. Provide meaningful error information.
3. Prevent unexpected crashes.
4. Support structured error handling.
5. Improve program reliability.

# Limitations

1. Improper handling may hide bugs.
2. Generic exception handling reduces debugging clarity.
3. Excessive exception handling increases code complexity.

# Summary

Python provides many built-in exceptions to represent different runtime errors. These exceptions help developers detect and handle problems effectively. Understanding common exceptions such as `ZeroDivisionError`, `ValueError`, `TypeError`, `IndexError`, and `FileNotFoundError` enables developers to create reliable and maintainable applications.

