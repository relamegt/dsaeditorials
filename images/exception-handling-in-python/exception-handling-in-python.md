# Exception Handling in Python

## Introduction

Exception handling is a mechanism that allows a program to detect and handle runtime errors gracefully instead of terminating unexpectedly. Python provides `try`, `except`, `else`, and `finally` blocks to manage exceptions and ensure reliable execution.

Exception handling helps programs recover from errors and continue execution whenever possible.

### Key Features

- Prevents abrupt program termination.
- Handles runtime errors safely.
- Improves reliability and maintainability.
- Supports cleanup operations.
- Allows custom exceptions to be created.

## Why Exception Handling?

Errors may occur during program execution because of invalid input, division by zero, missing files, or incorrect operations. Exception handling allows these situations to be managed gracefully.

### Example Without Exception Handling

```python
number = 25

result = number / 0

print(result)
```

### Output
ZeroDivisionError: division by zero

### Limitation

The program terminates immediately when an error occurs.

# Basic Exception Handling

The `try` block contains risky code, while the `except` block handles errors.

### Example

```python
try:

    amount = 5000

    result = amount / 0

except ZeroDivisionError:

    print(
        "Division by zero is not allowed."
    )
```

### Output
Division by zero is not allowed.

### Explanation

- The division operation raises a `ZeroDivisionError`.
- The `except` block catches the exception.
- The program continues without crashing.

# Syntax of Exception Handling

Python provides four keywords for handling exceptions.

```python
try:
    # Risky code

except SomeException:
    # Handle exception

else:
    # Executes if no exception occurs

finally:
    # Always executes
```

### Explanation

- `try` contains code that may raise an exception.
- `except` catches and handles exceptions.
- `else` runs when no exception occurs.
- `finally` executes regardless of exceptions.

# Using try, except, else and finally

### Example

```python
try:

    value = 20

    result = 100 / value

except ZeroDivisionError:

    print(
        "Cannot divide by zero."
    )

else:

    print(
        "Answer:",
        result
    )

finally:

    print(
        "Execution Finished"
    )
```

### Output
Answer: 5.0
Execution Finished

### Explanation

- Since no error occurs, the `else` block executes.
- The `finally` block always runs.

# Catching Specific Exceptions

Different exceptions can be handled separately.

### Example

```python
try:

    age = int("Python")

except ValueError:

    print(
        "Invalid number format."
    )

except ZeroDivisionError:

    print(
        "Division error occurred."
    )
```

### Output
Invalid number format.

### Explanation

Converting `"Python"` into an integer raises a `ValueError`.

# Handling Multiple Exceptions

Multiple exceptions can be grouped together.

### Example

```python
data = [
    "50",
    "AlphaKnowledge",
    100
]

try:

    total = int(data[0]) + int(data[1])

except (ValueError, TypeError):

    print(
        "Invalid data encountered."
    )

except IndexError:

    print(
        "Index out of range."
    )
```

### Output
Invalid data encountered.

### Explanation

The string `"AlphaKnowledge"` cannot be converted into an integer, resulting in a `ValueError`.

# Catch-All Exception

A generic exception handler catches unexpected exceptions.

### Example

```python
try:

    result = "Python" - 10

except:

    print(
        "Unexpected error occurred."
    )
```

### Output
Unexpected error occurred.

### Explanation

The operation raises a `TypeError`, which is caught by the generic handler.

# Raising Exceptions

The `raise` keyword allows exceptions to be generated manually.

### Example

```python
def set_temperature(temp):

    if temp < -50:

        raise ValueError(
            "Temperature is too low."
        )

    print(
        "Temperature Set"
    )

try:

    set_temperature(
        -80
    )

except ValueError as error:

    print(error)
```

### Output
Temperature is too low.

### Explanation

The function raises a `ValueError` when an invalid temperature is provided.

# Creating Custom Exceptions

User-defined exceptions can represent application-specific errors.

### Example

```python
class InvalidMarksError(
    Exception
):
    pass

def check_marks(mark):

    if mark > 100:

        raise InvalidMarksError(
            "Marks cannot exceed 100."
        )

try:

    check_marks(
        120
    )

except InvalidMarksError as error:

    print(error)
```

### Output
Marks cannot exceed 100.

### Explanation

A custom exception class is created to handle invalid marks.

# The finally Block

The `finally` block executes whether an exception occurs or not.

### Example

```python
try:

    print(
        10 / 0
    )

except ZeroDivisionError:

    print(
        "Division Error"
    )

finally:

    print(
        "Closing Resources"
    )
```

### Output
Division Error
Closing Resources

### Explanation

The `finally` block is always executed and is useful for cleanup tasks.

# Common Built-in Exceptions

| Exception | Cause |
| --- | --- |
| ZeroDivisionError | Division by zero |
| ValueError | Invalid value |
| TypeError | Unsupported operation |
| IndexError | Invalid index |
| KeyError | Missing dictionary key |
| FileNotFoundError | File does not exist |

# Errors vs Exceptions

| Feature | Error | Exception |
| --- | --- | --- |
| Occurrence | Program errors | Runtime issues |
| Handling | Difficult to recover | Can be handled |
| Example | SyntaxError | ValueError |
| Program Execution | Usually stops | Can continue |

# Advantages of Exception Handling

1. Prevents abrupt program termination.
2. Improves reliability.
3. Separates error-handling logic from normal code.
4. Simplifies debugging.
5. Supports custom exceptions.

# Limitations

1. Excessive exception handling may hide bugs.
2. Generic exception blocks make debugging harder.
3. Improper handling can increase code complexity.

# Summary

Exception handling enables Python programs to deal with runtime errors safely and efficiently. Using `try`, `except`, `else`, and `finally`, developers can create robust applications that continue execution even when unexpected situations occur. Python also allows raising exceptions manually and defining custom exceptions for application-specific requirements.

