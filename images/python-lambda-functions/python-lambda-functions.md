# Python Lambda Functions

## Introduction

Lambda functions are small anonymous functions in Python that are created without using the `def` keyword. They are useful for short, simple operations that are needed temporarily. Since lambda functions consist of only one expression, they automatically return the result without requiring a `return` statement.

Lambda functions are commonly used with functions such as `map()`, `filter()`, and `reduce()`, making code shorter and more readable.

### Key Features

- Anonymous functions without names.
- Created using the `lambda` keyword.
- Contain only one expression.
- Automatically return the result.
- Useful for short and simple operations.
- Frequently used with higher-order functions.

# Why Use Lambda Functions?

Lambda functions provide a compact way to define small functions without creating a complete function definition using `def`.

### Example

```Code
text = "AlphaKnowledge"

upper = lambda x: x.upper()

print(upper(text))
```

### Output
ALPHAKNOWLEDGE

### Explanation

The lambda function accepts a string and converts it to uppercase using the `upper()` method.

# Syntax of Lambda Functions

Lambda functions are created using the following syntax.

### Syntax

```Code
lambda arguments: expression
```

### Explanation

- `lambda` specifies an anonymous function.
- Arguments are input parameters.
- The expression is evaluated and returned automatically.

# Basic Lambda Function

### Example

```Code
square = lambda x: x * x

print(square(6))
```

### Output
36

### Explanation

The lambda function takes one number and returns its square.

# Lambda with Multiple Arguments

### Example

```Code
multiply = lambda x, y: x * y

print(multiply(4, 5))
```

### Output
20

### Explanation

The lambda function accepts two arguments and returns their product.

# Conditional Expressions Using Lambda

Lambda functions can include conditional expressions.

### Example

```Code
check = lambda x: (
    "Positive"
    if x > 0
    else "Negative"
    if x < 0
    else "Zero"
)

print(check(5))
print(check(-3))
print(check(0))
```

### Output
Positive
Negative
Zero

### Explanation

The lambda function checks whether a number is positive, negative, or zero using nested conditional expressions.

# Lambda with List Comprehension

Lambda expressions can be combined with list comprehensions.

### Example

```Code
functions = [
    lambda value=x: value * 10
    for x in range(1, 5)
]

for fun in functions:
    print(fun())
```

### Output
10
20
30
40

### Explanation

Each lambda stores its corresponding value and multiplies it by 10.

# Returning Multiple Values

Although a lambda function contains only one expression, it can return multiple values using tuples.

### Example

```Code
calculate = lambda x, y: (
    x + y,
    x * y
)

result = calculate(3, 4)

print(result)
```

### Output
(7, 12)

### Explanation

The lambda function performs addition and multiplication and returns both results as a tuple.

# Lambda with filter()

The `filter()` function selects elements that satisfy a condition.

### Example

```Code
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = filter(
    lambda x: x % 2 == 0,
    numbers
)

print(list(even_numbers))
```

### Output
[2, 4, 6]

### Explanation

The lambda expression checks whether a number is divisible by 2. The `filter()` function keeps only even numbers.

# Lambda with map()

The `map()` function applies an operation to every element in a sequence.

### Example

```Code
numbers = [1, 2, 3, 4]

double_numbers = map(
    lambda x: x * 2,
    numbers
)

print(list(double_numbers))
```

### Output
[2, 4, 6, 8]

### Explanation

Each number in the list is doubled using the lambda function.

# Lambda with reduce()

The `reduce()` function repeatedly combines elements to produce a single value.

### Example

```Code
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(
    lambda x, y: x * y,
    numbers
)

print(result)
```

### Output
24

### Explanation

The lambda function multiplies two elements at a time until one final value remains.

# Sorting Using Lambda Functions

Lambda functions are frequently used for custom sorting.

### Example

```Code
students = [
    ("John", 85),
    ("Emma", 92),
    ("Alex", 78)
]

students.sort(
    key=lambda x: x[1]
)

print(students)
```

### Output
[('Alex', 78), ('John', 85), ('Emma', 92)]

### Explanation

The list is sorted according to the second element of each tuple, which represents marks.

# Lambda vs Regular Functions

| Feature | Lambda Function | Regular Function |
| --- | --- | --- |
| Definition | Uses `lambda` keyword | Uses `def` keyword |
| Name | Anonymous | Named |
| Statements | One expression only | Multiple statements allowed |
| Return Statement | Automatic | Explicit return |
| Readability | Suitable for short tasks | Suitable for complex tasks |
| Reusability | Limited | High |

# Advantages of Lambda Functions

1. Short and concise syntax.
2. No need for explicit return statements.
3. Useful with `map()`, `filter()`, and `reduce()`.
4. Makes code compact and readable.
5. Convenient for temporary functions.

# Limitations of Lambda Functions

1. Can contain only one expression.
2. Cannot include multiple statements.
3. Difficult to debug for complex operations.
4. Less readable when expressions become large.

# Applications of Lambda Functions

- Data transformation with `map()`
- Filtering data with `filter()`
- Reducing sequences with `reduce()`
- Custom sorting
- Event handling
- Functional programming
- List comprehensions
- Temporary calculations

# Summary

Lambda functions are anonymous functions created using the `lambda` keyword. They provide a compact way to write short functions and automatically return the result of a single expression. Lambda functions are especially useful when used with higher-order functions such as `map()`, `filter()`, and `reduce()`. Although they improve code conciseness, regular functions are preferred for larger and more complex tasks because of better readability and maintainability.

