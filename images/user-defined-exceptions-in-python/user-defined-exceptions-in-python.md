# User-defined Exceptions in Python

## Introduction

User-defined exceptions allow developers to create custom error types that represent application-specific problems. By creating custom exceptions, programs can provide meaningful error messages and handle unusual situations more effectively.

A user-defined exception is created by defining a class that inherits from Python's built-in `Exception` class or one of its subclasses.

### Key Features

- Allows creation of application-specific errors.
- Improves readability and maintainability.
- Provides meaningful error messages.
- Supports custom attributes and methods.
- Enables separate handling of special conditions.

## Why User-defined Exceptions?

Built-in exceptions handle common problems, but many applications require custom errors that better describe specific situations.

### Example

```python
class InvalidMarksError(Exception):

    pass

marks = -10

if marks < 0:

    raise InvalidMarksError(
        "Marks cannot be negative."
    )
```

### Output
Traceback (most recent call last):
...
InvalidMarksError: Marks cannot be negative.

### Explanation

The program creates a custom exception and raises it when marks become negative.

# Steps to Create User-defined Exceptions

1. Create a class that inherits from `Exception`.
2. Raise the exception using the `raise` keyword.
3. Handle the exception using `try-except`.

## Creating a Simple User-defined Exception

### Example

```python
class InvalidQuantityError(Exception):

    pass

try:

    raise InvalidQuantityError(
        "Quantity cannot be zero."
    )

except InvalidQuantityError as error:

    print(error)
```

### Output
Quantity cannot be zero.

### Explanation

The custom exception is raised and then handled using `try-except`.

# Custom Exception with Attributes

Custom exceptions can store additional information.

### Example

```python
class InvalidTemperatureError(
        Exception
):

    def __init__(
            self,
            temperature
    ):

        self.temperature = temperature

        super().__init__(
            "Temperature must be between 0 and 50."
        )

try:

    temperature = 70

    if temperature > 50:

        raise InvalidTemperatureError(
            temperature
        )

except InvalidTemperatureError as error:

    print(error)
```

### Output
Temperature must be between 0 and 50.

### Explanation

The exception stores temperature information and provides a meaningful message.

# Overriding **str**()

The `__str__()` method can be overridden to customize error messages.

### Example

```python
class InvalidRollNumberError(
        Exception
):

    def __init__(
            self,
            roll_number
    ):

        self.roll_number = roll_number

    def __str__(self):

        return (
            f"Roll number "
            f"{self.roll_number} "
            f"is invalid."
        )

try:

    raise InvalidRollNumberError(
        501
    )

except InvalidRollNumberError as error:

    print(error)
```

### Output
Roll number 501 is invalid.

### Explanation

The `__str__()` method returns a custom message whenever the exception object is printed.

# Raising User-defined Exceptions

Exceptions are raised using the `raise` keyword.

### Example

```python
class LowBalanceError(
        Exception
):

    pass

balance = 400

try:

    if balance < 500:

        raise LowBalanceError(
            "Minimum balance required is ₹500."
        )

except LowBalanceError as error:

    print(error)
```

### Output
Minimum balance required is ₹500.

### Explanation

When balance becomes less than ₹500, a custom exception is raised.

# Handling User-defined Exceptions

User-defined exceptions are handled just like built-in exceptions.

### Example

```python
class InvalidPasswordError(
        Exception
):

    pass

try:

    password = "abc"

    if len(password) < 8:

        raise InvalidPasswordError(
            "Password is too short."
        )

except InvalidPasswordError as error:

    print(error)
```

### Output
Password is too short.

### Explanation

The custom exception is caught and handled using an `except` block.

# Custom Exception with Error Code

Additional information can be stored inside exceptions.

### Example

```python
class ProductUnavailableError(
        Exception
):

    def __init__(
            self,
            code,
            message
    ):

        self.code = code

        self.message = message

    def __str__(self):

        return (
            f"[{self.code}] "
            f"{self.message}"
        )

try:

    raise ProductUnavailableError(
        101,
        "Product is out of stock."
    )

except ProductUnavailableError as error:

    print(error)
```

### Output
[101] Product is out of stock.

### Explanation

The exception stores an error code and message, providing detailed information.

# Inheriting from Standard Exceptions

Custom exceptions can inherit from built-in exception classes.

### Example

```python
class InvalidPriceError(
        ValueError
):

    pass

try:

    price = -250

    if price < 0:

        raise InvalidPriceError(
            "Price cannot be negative."
        )

except InvalidPriceError as error:

    print(error)
```

### Output
Price cannot be negative.

### Explanation

`InvalidPriceError` inherits from `ValueError`, making it a specialized value-related exception.

# Real-world Example: Invalid Coupon Code

### Example

```python
class InvalidCouponError(
        Exception
):

    def __init__(
            self,
            coupon
    ):

        self.coupon = coupon

    def __str__(self):

        return (
            f"{self.coupon} "
            f"is not a valid coupon."
        )

try:

    coupon = "SAVE999"

    if coupon != "ALPHA50":

        raise InvalidCouponError(
            coupon
        )

except InvalidCouponError as error:

    print(error)
```

### Output
SAVE999 is not a valid coupon.

### Explanation

The custom exception provides a clear message when an invalid coupon is entered.

# When to Use User-defined Exceptions?

User-defined exceptions are useful when:

- Handling application-specific errors.
- Providing meaningful error messages.
- Separating different categories of errors.
- Improving debugging and maintenance.
- Making programs more readable.

# Advantages of User-defined Exceptions

1. Improve code readability.
2. Provide descriptive error messages.
3. Simplify debugging.
4. Support structured error handling.
5. Make applications easier to maintain.

# Limitations

1. Too many custom exceptions may increase complexity.
2. Improper handling can hide bugs.
3. Additional classes increase code size.

# Summary

User-defined exceptions allow developers to create application-specific errors by inheriting from Python's `Exception` class or its subclasses. They provide meaningful messages, support additional information through attributes, and improve the maintainability and readability of programs. Custom exceptions are especially useful when built-in exceptions do not adequately represent the problem being handled.

