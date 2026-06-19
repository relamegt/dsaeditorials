# Python List Comprehension

## Introduction

List comprehension is a concise and powerful way to create new lists from existing iterables. It combines looping, optional filtering, and expression evaluation into a single line, making code shorter, cleaner, and easier to read.

### Key Features

- Creates lists in a compact form.
- Supports conditions and filtering.
- Works with lists, tuples, strings, and ranges.
- Can replace many simple for loops.
- Improves readability and reduces code length.

# Why Use List Comprehension?

List comprehension helps create lists quickly without manually using loops and append() statements.

### Example

```python
numbers = [3, 6, 9, 12]

squares = [num ** 2 for num in numbers]

print(squares)
```

### Output
[9, 36, 81, 144]

### Explanation

Each element is squared and stored in a new list.

# Syntax

```python
[expression for item in iterable if condition]
```

### Components

- **expression** → operation performed on each element.
- **item** → current element from iterable.
- **iterable** → list, tuple, range, string, etc.
- **condition** → optional filter.

# Creating Lists Using Range

### Example

```python
values = [value for value in range(1, 6)]

print(values)
```

### Output
[1, 2, 3, 4, 5]

### Explanation

Numbers from 1 to 5 are generated and stored in a list.

# List Comprehension with Conditions

## Example 1: Even Numbers

```python
numbers = [5, 8, 11, 14, 17, 20]

evens = [num for num in numbers if num % 2 == 0]

print(evens)
```

### Output
[8, 14, 20]

### Explanation

Only even numbers are selected.

## Example 2: Values Greater Than 50

```python
marks = [45, 78, 52, 90, 34, 67]

high_scores = [mark for mark in marks if mark > 50]

print(high_scores)
```

### Output
[78, 52, 90, 67]

### Explanation

Only values greater than 50 are included.

# Transforming Elements

### Example

```python
ages = [18, 21, 24, 27]

updated_ages = [age + 1 for age in ages]

print(updated_ages)
```

### Output
[19, 22, 25, 28]

### Explanation

Each element is increased by one.

# Working with Strings

### Example

```python
names = [
    "Akash Dangudubiyyapu",
    "Mohit Chandaluri",
    "Abhiram Gopisetti"
]

uppercase_names = [name.upper() for name in names]

print(uppercase_names)
```

### Output
['AKASH DANGUDUBIYYAPU', 'MOHIT CHANDALURI', 'ABHIRAM GOPISETTI']

### Explanation

Every string is converted into uppercase.

# Using If-Else in List Comprehension

### Example

```python
numbers = [10, 15, 20, 25]

labels = ["Even" if num % 2 == 0 else "Odd" for num in numbers]

print(labels)
```

### Output
['Even', 'Odd', 'Even', 'Odd']

### Explanation

The expression returns "Even" for even numbers and "Odd" otherwise.

# Nested List Comprehension

### Example

```python
pairs = [(row, col)
         for row in range(1, 4)
         for col in range(1, 4)]

print(pairs)
```

### Output
[(1, 1), (1, 2), (1, 3), (2, 1), (2, 2), (2, 3), (3, 1), (3, 2), (3, 3)]

### Explanation

Two loops are combined to generate coordinate pairs.

# Flattening Nested Lists

### Example

```python
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]

flat_list = [item for row in matrix for item in row]

print(flat_list)
```

### Output
[1, 2, 3, 4, 5, 6]

### Explanation

All inner lists are converted into a single list.

# List Comprehension with Strings

### Example

```python
text = "AlphaKnowledge"

letters = [char for char in text]

print(letters)
```

### Output
['A', 'l', 'p', 'h', 'a', 'K', 'n', 'o', 'w', 'l', 'e', 'd', 'g', 'e']

### Explanation

Each character becomes an element of the list.

# Traditional Loop vs List Comprehension

## Using a For Loop

```python
numbers = [2, 4, 6]

result = []

for num in numbers:
    result.append(num * 2)

print(result)
```

### Output
[4, 8, 12]

## Using List Comprehension

```python
numbers = [2, 4, 6]

result = [num * 2 for num in numbers]

print(result)
```

### Output
[4, 8, 12]

### Explanation

List comprehension performs the same operation with less code.

# Advantages of List Comprehension

1. Short and readable.
2. Reduces the number of lines of code.
3. Faster than many traditional loops.
4. Supports filtering with conditions.
5. Simplifies list creation.

# Limitations of List Comprehension

1. Complex expressions reduce readability.
2. Not suitable for very complicated logic.
3. Deep nesting can make code difficult to understand.

# Applications of List Comprehension

- Generating lists from ranges.
- Filtering values.
- Transforming data.
- Processing strings.
- Flattening matrices.
- Data preprocessing.
- Mathematical computations.

# For Loop vs List Comprehension

| For Loop | List Comprehension |
| --- | --- |
| Multiple lines | Single line |
| Uses append() | Creates list directly |
| Better for complex logic | Better for concise operations |
| More verbose | More readable for simple tasks |

# Summary

List comprehension provides a simple and elegant way to create lists in Python. It combines looping, filtering, and expression evaluation into a compact syntax, making programs shorter, cleaner, and easier to maintain.

