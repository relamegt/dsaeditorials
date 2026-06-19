# *args and **kwargs in Python

## Introduction

Functions in Python usually accept a fixed number of arguments. However, in some situations, the exact number of arguments is unknown beforehand. Python provides two special mechanisms, `*args` and `**kwargs`, which allow functions to accept a variable number of arguments.

The `*args` syntax collects multiple positional arguments into a tuple, while `**kwargs` collects multiple keyword arguments into a dictionary. These features make functions more flexible and reusable.

### Key Features

- Allow functions to accept an arbitrary number of arguments.
- `*args` stores positional arguments as a tuple.
- `**kwargs` stores keyword arguments as a dictionary.
- Increase flexibility and code reusability.
- Useful when the number of arguments is unknown.
- Commonly used in APIs, decorators, and frameworks.

# Why Use *args and **kwargs?

Sometimes, we do not know how many values a function will receive. Instead of creating many functions with different numbers of parameters, Python provides `*args` and `**kwargs` to handle such situations efficiently.

### Example

```python
def add(*args):

    return sum(args)

print(add(5, 10, 15))
```

### Output
30

### Explanation

All arguments are collected into a tuple and passed to the `sum()` function.

# Understanding *args

The `*args` syntax allows a function to receive any number of positional arguments.

### Syntax

```python
def function_name(*args):

    statements
```

### Explanation

- The `*` symbol packs multiple positional arguments into a tuple.
- The name `args` is conventional, but any valid identifier can be used.

# Printing Multiple Values Using *args

### Example

```python
def display(*args):

    for value in args:
        print(value)

display("Python", "Java", "C++")
```

### Output
Python
Java
C++

### Explanation

All values passed to the function are stored inside a tuple and printed one by one.

# Multiplication Using *args

### Example

```python
def multiply(*args):

    result = 1

    for num in args:
        result *= num

    return result

print(multiply(2, 3, 4))
```

### Output
24

### Explanation

The function accepts multiple numbers and multiplies them together.

# Finding Maximum Value Using *args

### Example

```python
def maximum(*args):

    return max(args)

print(maximum(15, 40, 25, 60))
```

### Output
60

### Explanation

The values are packed into a tuple and the `max()` function returns the largest element.

# Type of *args

### Example

```python
def demo(*args):

    print(type(args))

demo(10, 20, 30)
```

### Output
<class 'tuple'>

### Explanation

Python stores positional arguments inside a tuple.

# Understanding **kwargs

The `**kwargs` syntax allows a function to receive any number of keyword arguments.

### Syntax

```python
def function_name(**kwargs):

    statements
```

### Explanation

Keyword arguments are stored as key-value pairs inside a dictionary.

# Printing Keyword Arguments

### Example

```python
def details(**kwargs):

    for key, value in kwargs.items():
        print(key, "=", value)

details(
    name="Alice",
    age=22,
    city="London"
)
```

### Output
name = Alice
age = 22
city = London

### Explanation

Keyword arguments are stored inside a dictionary and accessed using the `items()` method.

# Type of **kwargs

### Example

```python
def example(**kwargs):

    print(type(kwargs))

example(a=1, b=2)
```

### Output
<class 'dict'>

### Explanation

Python stores keyword arguments as dictionaries.

# Creating a Profile Using **kwargs

### Example

```python
def profile(**kwargs):

    for key, value in kwargs.items():

        print(key, ":", value)

profile(
    Name="Emma",
    Age=20,
    Course="Python"
)
```

### Output
Name : Emma
Age : 20
Course : Python

### Explanation

The function accepts any number of keyword arguments and prints them dynamically.

# Combining *args and **kwargs

Both `*args` and `**kwargs` can be used together in the same function.

### Syntax

```python
def function_name(*args, **kwargs):

    statements
```

# Using Both *args and **kwargs

A function can accept both positional and keyword arguments together. Positional arguments are stored inside a tuple and keyword arguments are stored inside a dictionary.

### Example

```python
def student_info(*args, **kwargs):

    print("Subjects:", args)
    print("Details:", kwargs)

student_info(
    "Math",
    "Science",
    "English",
    Name="Alice",
    Age=20,
    City="New York"
)
```

### Output
Subjects: ('Math', 'Science', 'English')
Details: {'Name': 'Alice', 'Age': 20, 'City': 'New York'}

### Explanation

- `*args` collects positional arguments into a tuple.
- `**kwargs` collects keyword arguments into a dictionary.

# Order of Parameters

When defining functions with different types of parameters, the order should be maintained properly.

### Syntax

```python
def function_name(
        normal_arguments,
        *args,
        **kwargs):

    statements
```

### Explanation

Python expects regular parameters first, followed by `*args`, and finally `**kwargs`.

# Unpacking Arguments with *

The `*` operator can unpack elements from a list or tuple and pass them as separate arguments.

### Example

```python
def add(a, b, c):

    return a + b + c

numbers = [10, 20, 30]

print(add(*numbers))
```

### Output
60

### Explanation

The elements inside the list are unpacked and assigned to parameters `a`, `b`, and `c`.

# Unpacking Dictionary with **

The `**` operator unpacks dictionary items and passes them as keyword arguments.

### Example

```python
def details(name, age):

    print(name)
    print(age)

data = {
    "name": "Alex",
    "age": 25
}

details(**data)
```

### Output
Alex
25

### Explanation

Dictionary keys are matched with function parameter names.

# Passing Extra Positional Arguments

### Example

```python
def display(name, *marks):

    print(name)
    print(marks)

display("John", 80, 90, 95)
```

### Output
John
(80, 90, 95)

### Explanation

The first value is assigned to `name`, while the remaining values are stored inside the tuple `marks`.

# Passing Extra Keyword Arguments

### Example

```python
def employee(name, **details):

    print(name)
    print(details)

employee(
    "David",
    age=30,
    city="Paris"
)
```

### Output
David
{'age': 30, 'city': 'Paris'}

### Explanation

The extra keyword arguments are packed into a dictionary.

# Applications of *args and **kwargs

Some common uses include:

- Writing flexible functions.
- Creating decorators.
- Building APIs.
- Logging utilities.
- Framework development.
- Wrapper functions.
- Dynamic function calls.

# Difference Between *args and **kwargs

| Feature | *args* | *kwargs |
| --- | --- | --- |
| Accepts | Positional arguments | Keyword arguments |
| Symbol Used | * | ** |
| Data Type | Tuple | Dictionary |
| Access Method | Indexing | Keys |
| Example | (10, 20, 30) | {'a':1, 'b':2} |

# Advantages of *args and **kwargs

1. Accept unlimited arguments.
2. Increase flexibility.
3. Reduce code duplication.
4. Improve code reusability.
5. Useful for dynamic programming.
6. Simplify API design.

# Limitations

1. Excessive use may reduce readability.
2. Difficult to understand for beginners.
3. Debugging becomes harder with many arguments.
4. Argument names are not explicit with `*args`.

# Common Mistakes

## Forgetting * Symbol

### Incorrect

```python
def fun(args):

    pass
```

### Correct

```python
def fun(*args):

    pass
```

## Forgetting ** Symbol

### Incorrect

```python
def fun(kwargs):

    pass
```

### Correct

```python
def fun(**kwargs):

    pass
```

## Wrong Parameter Order

### Incorrect

```python
def fun(**kwargs, *args):

    pass
```

### Correct

```python
def fun(*args, **kwargs):

    pass
```

# When to Use *args and **kwargs?

Use them when:

- The number of arguments is unknown.
- Creating reusable functions.
- Building decorators and wrappers.
- Writing libraries and frameworks.
- Designing flexible APIs.

# Summary

`*args` and `**kwargs` provide a powerful mechanism for accepting variable numbers of arguments in Python functions. The `*args` syntax collects positional arguments into a tuple, whereas `**kwargs` stores keyword arguments inside a dictionary. They help create flexible, reusable, and dynamic functions and are widely used in decorators, APIs, and frameworks. Understanding these concepts is essential for writing advanced and maintainable Python programs.

