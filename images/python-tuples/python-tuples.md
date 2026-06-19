# Python Tuples

## Introduction

A tuple is an ordered collection of elements that cannot be modified after creation. Tuples are similar to lists, but unlike lists, they are immutable. They can store multiple values of different data types and preserve the insertion order of elements.

### Key Features

- Tuples are immutable.
- Elements maintain insertion order.
- Support indexing and slicing.
- Allow duplicate values.
- Can store different data types.
- Support nested tuples.
- Consume less memory than lists.

# Why Use Tuples?

Tuples are useful when data should remain unchanged after creation. They provide better performance and are commonly used for storing fixed collections of values.

### Example

```python
scores = (85, 90, 95)

print(scores)
```

### Output
(85, 90, 95)

### Explanation

The tuple stores multiple values inside parentheses.

# Creating Tuples

Tuples can be created in several ways.

## 1. Creating an Empty Tuple

### Example

```python
data = ()

print(data)
```

### Output
()

### Explanation

Empty parentheses create an empty tuple.

## 2. Using Parentheses

### Example

```python
courses = ("Python", "Java")

print(courses)
```

### Output
('Python', 'Java')

### Explanation

Elements are enclosed inside parentheses and separated by commas.

## 3. Using tuple() Constructor

### Example

```python
numbers = [10, 20, 30]

values = tuple(numbers)

letters = tuple("CODE")

print(values)
print(letters)
```

### Output
(10, 20, 30)
('C', 'O', 'D', 'E')

### Explanation

The `tuple()` function converts iterable objects into tuples.

# Creating Tuples with Mixed Data Types

### Example

```python
details = (
    "Akash Dangudubiyyapu",
    23,
    9.24,
    True
)

print(details)
```

### Output
('Akash Dangudubiyyapu', 23, 9.24, True)

### Explanation

A tuple can store values of different types.

# Accessing Elements

Elements are accessed using indexing.

### Example

```python
languages = (
    "Python",
    "Java",
    "C++"
)

print(languages[0])

print(languages[-1])
```

### Output
Python
C++

### Explanation

- Index 0 refers to the first element.
- Index -1 refers to the last element.

# Tuple Slicing

Slicing extracts a portion of a tuple.

### Example

```python
numbers = (
    10,
    20,
    30,
    40,
    50
)

print(numbers[1:4])

print(numbers[:3])

print(numbers[2:])

print(numbers[::-1])
```

### Output
(20, 30, 40)
(10, 20, 30)
(30, 40, 50)
(50, 40, 30, 20, 10)

### Explanation

Slicing creates a new tuple containing selected elements.

# Tuple Unpacking

Tuple elements can be assigned directly to variables.

### Example

```python
mentor = (
    "Mohit Chandaluri",
    "Python",
    8
)

name, subject, experience = mentor

print(name)
print(subject)
print(experience)
```

### Output
Mohit Chandaluri
Python
8

### Explanation

Each element is assigned to a corresponding variable.

# Tuple Unpacking with *

### Example

```python
values = (
    10,
    20,
    30,
    40,
    50
)

first, *middle, last = values

print(first)
print(middle)
print(last)
```

### Output
10
[20, 30, 40]
50

### Explanation

The `*` operator collects multiple values into a list.

# Concatenating Tuples

Tuples can be combined using the `+` operator.

### Example

```python
a = (
    1,
    2
)

b = (
    3,
    4
)

print(a + b)
```

### Output
(1, 2, 3, 4)

### Explanation

Concatenation creates a new tuple containing elements from both tuples.

# Repeating Tuples

The `*` operator repeats a tuple.

### Example

```python
values = (
    "AlphaKnowledge",
)

print(values * 3)
```

### Output
('AlphaKnowledge', 'AlphaKnowledge', 'AlphaKnowledge')

### Explanation

The tuple is repeated three times.

# Membership Testing

The `in` operator checks whether an element exists.

### Example

```python
students = (
    "Akash Dangudubiyyapu",
    "Abhiram Gopisetti",
    "Adapa Hemesh"
)

print("Abhiram Gopisetti" in students)

print("Hemanth Akhil" in students)
```

### Output
True
False

### Explanation

The `in` operator returns `True` if the element exists.

# Iterating Through Tuples

Tuples can be traversed using loops.

### Example

```python
trainers = (
    "Mohit Chandaluri",
    "Hemanth Akhil",
    "Adapa Hemesh"
)

for trainer in trainers:
    print(trainer)
```

### Output
Mohit Chandaluri
Hemanth Akhil
Adapa Hemesh

### Explanation

The loop accesses one element at a time.

# Nested Tuples

A tuple can contain another tuple.

### Example

```python
matrix = (
    (1, 2),
    (3, 4)
)

print(matrix[0])

print(matrix[1][1])
```

### Output
(1, 2)
4

### Explanation

Multiple indexes are used to access inner elements.

# Deleting a Tuple

Individual elements cannot be deleted because tuples are immutable. However, an entire tuple can be removed.

### Example

```python
data = (
    1,
    2,
    3
)

del data
```

### Explanation

After deletion, the variable no longer exists.

# Common Tuple Methods

## len()

Returns the number of elements.

### Example

```python
numbers = (
    10,
    20,
    30,
    40
)

print(len(numbers))
```

### Output
4

## count()

Returns the number of occurrences of a value.

### Example

```python
numbers = (
    5,
    8,
    5,
    10
)

print(numbers.count(5))
```

### Output
2

## index()

Returns the position of an element.

### Example

```python
numbers = (
    100,
    200,
    300
)

print(numbers.index(200))
```

### Output
1

# Advantages of Tuples

1. Immutable and secure.
2. Consume less memory.
3. Faster than lists.
4. Support indexing and slicing.
5. Can store multiple data types.
6. Suitable for fixed collections.

# Limitations of Tuples

1. Elements cannot be modified.
2. Insertion and deletion are not possible.
3. Fewer built-in methods compared to lists.
4. Not suitable when data changes frequently.

# Applications of Tuples

- Storing coordinates.
- Returning multiple values from functions.
- Database records.
- Fixed configuration values.
- Dictionary keys.
- Packing and unpacking data.

# Common Tuple Methods

| Method | Description |
| --- | --- |
| `count()` | Counts occurrences of an element |
| `index()` | Returns the index of an element |
| `len()` | Returns the number of elements |

# Summary

Tuples are immutable, ordered collections used to store multiple values in Python. They support indexing, slicing, iteration, unpacking, and a few built-in methods. Since tuples cannot be modified after creation, they are suitable for storing fixed collections of data and provide better performance and memory efficiency compared to lists.

