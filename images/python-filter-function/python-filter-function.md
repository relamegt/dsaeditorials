# Python filter() Function

## Introduction

The `filter()` function in Python is a built-in function used to extract elements from an iterable based on a given condition. It evaluates each element using a function and keeps only those elements for which the function returns `True`.

Unlike `map()`, which transforms every element, `filter()` removes unwanted elements and returns only the matching ones.

### Key Features

- Selects elements based on a condition.
- Returns a filter object (iterator).
- Works with lists, tuples, sets, and other iterables.
- Supports lambda functions and user-defined functions.
- Helps write concise and readable code.
- Useful for data filtering and cleaning.

# Why Use filter()?

Suppose we want only even numbers from a list. Instead of using loops and conditions manually, `filter()` performs this operation efficiently.

### Example

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(
    lambda x: x % 2 == 0,
    numbers
)

print(list(result))
```

### Output
[2, 4, 6]

### Explanation

The lambda function checks whether a number is divisible by 2. The `filter()` function keeps only those numbers for which the condition is true.

# Syntax of filter()

### Syntax

```Code
filter(function, iterable)
```

### Parameters

- **function** : Function that tests each element.
- **iterable** : List, tuple, set, or any iterable object.

### Return Value

Returns a filter object containing elements that satisfy the condition.

# Using filter() with a User-Defined Function

### Example

```python
def even(num):
    return num % 2 == 0

numbers = [1, 2, 3, 4, 5, 6]

result = filter(
    even,
    numbers
)

print(list(result))
```

### Output
[2, 4, 6]

### Explanation

The function `even()` checks each element and returns `True` only for even numbers.

# Using filter() with Lambda Functions

### Example

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(
    lambda x: x % 3 == 0,
    numbers
)

print(list(result))
```

### Output
[3, 6]

### Explanation

The lambda function selects numbers divisible by 3.

# Filtering Strings by Length

### Example

```python
fruits = [
    "apple",
    "banana",
    "cherry",
    "kiwi",
    "grape"
]

result = filter(
    lambda word: len(word) > 5,
    fruits
)

print(list(result))
```

### Output
['banana', 'cherry']

### Explanation

Only strings having more than five characters are included.

# Filtering Positive Numbers

### Example

```python
numbers = [-5, 3, -1, 10, 7, -2]

result = filter(
    lambda x: x > 0,
    numbers
)

print(list(result))
```

### Output
[3, 10, 7]

### Explanation

The lambda expression selects only positive values.

# Removing Empty Strings

### Example

```python
words = [
    "Python",
    "",
    "Programming",
    "",
    "Language"
]

result = filter(
    None,
    words
)

print(list(result))
```

### Output
['Python', 'Programming', 'Language']

### Explanation

Passing `None` removes all falsy values such as empty strings.

# Filtering Names Starting with a Particular Letter

### Example

```python
names = [
    "Alice",
    "Andrew",
    "Bob",
    "Alex",
    "John"
]

result = filter(
    lambda name: name.startswith("A"),
    names
)

print(list(result))
```

### Output
['Alice', 'Andrew', 'Alex']

### Explanation

Only names beginning with the letter 'A' are retained.

# Removing None and Zero Values

### Example

```python
values = [
    "Python",
    None,
    0,
    "",
    25,
    "AI"
]

result = filter(
    None,
    values
)

print(list(result))
```

### Output
['Python', 25, 'AI']

### Explanation

Falsy values such as `None`, `0`, and empty strings are removed automatically.

# filter() vs Loop

| Feature | filter() | Loop |
| --- | --- | --- |
| Code Length | Short | Longer |
| Readability | High | Moderate |
| Automatic Filtering | Yes | Manual |
| Functional Programming | Yes | No |
| Performance | Efficient | Efficient |

# Advantages of filter()

1. Produces concise code.
2. Removes unwanted elements efficiently.
3. Works well with lambda functions.
4. Improves readability.
5. Supports functional programming.

# Limitations of filter()

1. Returns a filter object instead of a list.
2. Complex conditions may reduce readability.
3. Beginners may find lambda expressions difficult.
4. Nested filter functions can become hard to understand.

# Applications of filter()

- Selecting even and odd numbers.
- Removing invalid values.
- Cleaning datasets.
- Filtering strings and text.
- Searching records based on conditions.
- Functional programming.

# Summary

The `filter()` function is used to extract elements that satisfy a given condition. It applies a function to each element of an iterable and returns only those values for which the function returns `True`. Combined with lambda expressions, `filter()` provides a concise and powerful way to perform data filtering and is widely used in Python programming.

