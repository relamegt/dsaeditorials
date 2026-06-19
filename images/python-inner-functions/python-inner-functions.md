# Python Inner Functions

## Introduction

An inner function, also called a nested function, is a function defined inside another function. Inner functions help organize code, hide implementation details, and access variables from the enclosing function. They are widely used in closures, decorators, and callback mechanisms.

Unlike regular functions, inner functions are local to the outer function and generally cannot be accessed directly from outside.

### Key Features

- Defined inside another function.
- Can access variables of the outer function.
- Follow the LEGB scope rule.
- Improve code organization and readability.
- Support closures and decorators.
- Hide helper logic from external access.

# Why Use Inner Functions?

Inner functions are useful when certain functionality is needed only within another function. They help encapsulate helper code and avoid unnecessary global functions.

### Example

```python
def outer(message):

    def inner():
        print(message)

    inner()

outer("Hello")
```

### Output
Hello

### Explanation

The function `inner()` is defined inside `outer()`. It accesses the variable `message` from the enclosing function and prints it.

# Syntax of Inner Functions

### Syntax

```Code
def outer_function():

    def inner_function():
        statements

    inner_function()
```

### Explanation

- The outer function contains another function definition.
- The inner function can access variables from the enclosing scope.
- The inner function can be called inside the outer function.

# Accessing Outer Variables

Inner functions can directly use variables defined in the enclosing function.

### Example

```python
def outer():

    msg = "Python Inner Functions"

    def inner():
        print(msg)

    inner()

outer()
```

### Output
Python Inner Functions

### Explanation

The variable `msg` belongs to the outer function, but the inner function can access it because of lexical scoping.

# LEGB Rule

Python searches variables in the following order:

1. Local Scope
2. Enclosing Scope
3. Global Scope
4. Built-in Scope

### Example

```python
name = "Global"

def outer():

    name = "Enclosing"

    def inner():
        print(name)

    inner()

outer()
```

### Output
Enclosing

### Explanation

Python first looks inside the local scope. Since no local variable exists inside `inner()`, it finds `name` in the enclosing scope.

# Modifying Outer Variables Using nonlocal

By default, inner functions cannot modify variables of the outer function. The `nonlocal` keyword allows modification.

### Example

```python
def outer():

    count = 10

    def inner():

        nonlocal count

        count = 20

        print(count)

    inner()

    print(count)

outer()
```

### Output
20
20

### Explanation

The keyword `nonlocal` tells Python to use the variable from the enclosing scope instead of creating a new local variable.

# Without nonlocal

### Example

```python
def outer():

    number = 5

    def inner():

        number = 10

        print(number)

    inner()

    print(number)

outer()
```

### Output
10
5

### Explanation

The variable inside `inner()` becomes local, leaving the outer variable unchanged.

# Returning Inner Functions

An inner function can be returned from the outer function.

### Example

```python
def outer(msg):

    def inner():
        print(msg)

    return inner

fun = outer("Welcome")

fun()
```

### Output
Welcome

### Explanation

The function `outer()` returns the function `inner()`, which can later be called using the variable `fun`.

# Closures

A closure is created when an inner function remembers variables from the outer function even after the outer function finishes execution.

### Example

```python
def multiplier(x):

    def multiply(y):
        return x * y

    return multiply

double = multiplier(2)

print(double(5))
```

### Output
10

### Explanation

Although `multiplier()` has finished execution, the inner function still remembers the value of `x`.

# Encapsulation Using Inner Functions

Inner functions help hide helper logic.

### Example

```python
def process_data(data):

    def clean():

        return [
            item.strip()
            for item in data
        ]

    return clean()

print(
    process_data(
        [" Python ", " AI "]
    )
)
```

### Output
['Python', 'AI']

### Explanation

The helper function `clean()` exists only inside `process_data()` and is inaccessible from outside.

# Using Inner Functions in Decorators

Decorators commonly use inner functions to add extra functionality.

### Example

```python
def logger(func):

    def wrapper(*args, **kwargs):

        print("Function Executed")

        return func(*args, **kwargs)

    return wrapper

@logger
def add(a, b):
    return a + b

print(add(3, 4))
```

### Output
Function Executed
7

### Explanation

The inner function `wrapper()` executes additional code before calling the original function.

# Multiple Inner Functions

A function can contain multiple inner functions.

### Example

```python
def calculator(a, b):

    def add():
        return a + b

    def subtract():
        return a - b

    print(add())
    print(subtract())

calculator(10, 5)
```

### Output
15
5

### Explanation

Both inner functions use variables from the enclosing function.

# Advantages of Inner Functions

1. Improve code organization.
2. Support encapsulation.
3. Reduce global namespace pollution.
4. Enable closures and decorators.
5. Increase code reusability.
6. Allow access to enclosing variables.

# Limitations of Inner Functions

1. Cannot be accessed directly from outside.
2. Excessive nesting reduces readability.
3. Debugging becomes difficult for deeply nested functions.
4. Slightly increases memory usage due to closures.

# Applications of Inner Functions

- Closures
- Decorators
- Callback functions
- Data processing
- Encapsulation of helper methods
- Functional programming
- Logging and monitoring
- Event handling

# Inner Functions vs Regular Functions

| Feature | Inner Function | Regular Function |
| --- | --- | --- |
| Definition | Inside another function | Defined independently |
| Scope | Local to outer function | Global or module scope |
| Access Outer Variables | Yes | No |
| Visibility | Limited | Accessible everywhere |
| Used For | Closures and decorators | General programming |

# Summary

Inner functions are functions defined inside another function. They help organize code, hide helper logic, and access variables from the enclosing scope. They follow the LEGB scope rule and play an important role in implementing closures and decorators. Inner functions provide cleaner and more maintainable code while supporting advanced programming techniques such as functional programming and callback mechanisms.

