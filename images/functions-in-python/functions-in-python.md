# Functions in Python

## Introduction

Functions are reusable blocks of code designed to perform a specific task. Instead of writing the same code multiple times, a function allows programmers to define the code once and execute it whenever needed. Functions improve code readability, reduce duplication, and make programs easier to maintain.

Python provides built-in functions such as `print()` and `len()`, and also allows programmers to create user-defined functions using the `def` keyword.

### Key Features

- Promote code reusability.
- Improve readability and organization.
- Reduce code duplication.
- Accept input through parameters.
- Return values to the caller.
- Support different types of arguments.
- Allow nested and recursive definitions.

# Why Use Functions?

Functions help break a large program into smaller and manageable sections. This makes code easier to understand and maintain.

### Example Without Functions

```python
print("Welcome to AlphaKnowledge")
print("Welcome to AlphaKnowledge")
print("Welcome to AlphaKnowledge")
```

### Output
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge

### Limitation

The same statement is repeated multiple times. If the message changes, every occurrence must be modified.

# Defining a Function

A function is defined using the `def` keyword followed by the function name and parentheses.

### Syntax

```python
def function_name():
    # function body
```

### Example

```python
def greet():
    print("Welcome to AlphaKnowledge")
```

### Explanation

The function `greet()` contains a statement that executes whenever the function is called.

# Calling a Function

A function executes only when it is called.

### Example

```python
def greet():
    print("Welcome to AlphaKnowledge")

greet()
```

### Output
Welcome to AlphaKnowledge

### Explanation

The function name followed by parentheses invokes the function.

# Function Parameters and Arguments

Parameters receive values passed to a function. These values are called arguments.

### Example

```python
def square(num):
    print(num * num)

square(5)
```

### Output
25

### Explanation

The value `5` is passed as an argument to parameter `num`.

# Returning Values

Functions can return results using the `return` statement.

### Example

```python
def cube(num):
    return num ** 3

result = cube(3)

print(result)
```

### Output
27

### Explanation

The `return` statement sends the calculated value back to the caller.

# Default Arguments

Default arguments provide predefined values when no argument is supplied.

### Example

```python
def student(name="Akash"):
    print("Student:", name)

student()
student("Abhiram")
```

### Output
Student: Akash
Student: Abhiram

### Explanation

If no value is passed, Python uses the default value.

# Positional Arguments

Values are assigned according to their order.

### Example

```python
def details(name, age):
    print(name)
    print(age)

details("Akash", 22)
```

### Output
Akash
22

### Explanation

The first value is assigned to `name`, and the second value is assigned to `age`.

# Keyword Arguments

Arguments can be passed using parameter names.

### Example

```python
def details(name, age):
    print(name)
    print(age)

details(age=22, name="Akash")
```

### Output
Akash
22

### Explanation

Order does not matter when parameter names are used.

# Arbitrary Arguments Using *args

`*args` allows a function to accept multiple positional arguments.

### Example

```python
def numbers(*args):
    for value in args:
        print(value)

numbers(10, 20, 30)
```

### Output
10
20
30

### Explanation

All arguments are stored as a tuple.

# Arbitrary Keyword Arguments Using **kwargs

`**kwargs` accepts multiple keyword arguments.

### Example

```python
def student(**kwargs):
    for key, value in kwargs.items():
        print(key, ":", value)

student(name="Akash", age=22)
```

### Output
name : Akash
age : 22

### Explanation

Keyword arguments are stored inside a dictionary.

# Nested Functions

Functions can be defined inside other functions.

### Example

```python
def outer():

    def inner():
        print("Inside Inner Function")

    inner()

outer()
```

### Output
Inside Inner Function

### Explanation

The inner function exists within the outer function and is called from inside it.

# Variable Scope

Variables inside functions are local variables and cannot be accessed outside the function.

### Example

```python
def demo():
    x = 100
    print(x)

demo()
```

### Output
100

### Explanation

The variable `x` exists only inside the function.

# Lambda Functions

Lambda functions are anonymous functions written in a single line.

### Example

```python
square = lambda x: x * x

print(square(6))
```

### Output
36

### Explanation

Lambda functions are useful for short and simple operations.

# Recursive Functions

A recursive function calls itself until a condition is satisfied.

### Example

```python
def factorial(n):

    if n == 1:
        return 1

    return n * factorial(n - 1)

print(factorial(5))
```

### Output
120

### Explanation

Each function call multiplies the current value by the factorial of the previous number.

# Pass by Object Reference

Python passes references to objects rather than copies.

### Example

```python
def modify(lst):
    lst[0] = 100

numbers = [10, 20, 30]

modify(numbers)

print(numbers)
```

### Output
[100, 20, 30]

### Explanation

Lists are mutable, so modifications inside the function affect the original object.

# Built-in Functions

Python provides many built-in functions.

| Function | Purpose |
| --- | --- |
| print() | Displays output |
| input() | Reads input |
| len() | Returns length |
| type() | Returns data type |
| max() | Returns maximum value |
| min() | Returns minimum value |
| sum() | Returns sum of elements |

### Example

```python
numbers = [10, 20, 30]

print(len(numbers))
print(max(numbers))
print(sum(numbers))
```

### Output
3
30
60

# Advantages of Functions

1. Reduce code repetition.
2. Improve readability.
3. Make debugging easier.
4. Simplify maintenance.
5. Promote modular programming.
6. Allow code reuse across projects.

# Limitations

1. Excessive function calls may increase overhead.
2. Deep recursion can cause stack overflow.
3. Improper parameter handling may introduce errors.
4. Too many small functions can reduce readability.

# Summary

Functions are reusable blocks of code that perform specific tasks. They help organize programs into smaller modules and improve maintainability. Python supports different types of arguments, return values, nested functions, lambda functions, and recursion. Understanding functions is essential for writing efficient, modular, and reusable programs.

