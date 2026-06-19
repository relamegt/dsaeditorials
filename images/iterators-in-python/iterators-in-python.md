# Iterators in Python

## Introduction

An iterator in Python is an object that allows elements of a collection to be accessed one at a time. Iterators follow the iterator protocol, which consists of two special methods:

- `__iter__()` : Returns the iterator object itself.
- `__next__()` : Returns the next element and raises `StopIteration` when no elements remain.

Iterators help process data efficiently without loading all elements into memory at once.

### Key Features

- Process elements one at a time.
- Support lazy evaluation.
- Consume less memory.
- Work with loops and generators.
- Keep track of traversal automatically.

## Why Iterators?

Normally, collections such as lists and strings contain multiple elements. Iterators allow accessing these elements sequentially without managing indexes manually.

### Example Without Iterator

```python
colors = [
    "Red",
    "Green",
    "Blue"
]

print(colors[0])
print(colors[1])
print(colors[2])
```

### Output
Red
Green
Blue

### Limitation

Accessing elements using indexes becomes difficult for large or dynamically generated data.

# Built-in Iterators

Python automatically provides iterators for strings, lists, tuples, dictionaries and sets.

### Example

```python
city = "DELHI"

itr = iter(city)

print(next(itr))
print(next(itr))
print(next(itr))
```

### Output
D
E
L

### Explanation

- `iter()` converts the string into an iterator.
- `next()` returns one character at a time.
- The iterator remembers its current position.

# Iterating Through a List

### Example

```python
languages = [
    "Python",
    "Java",
    "C++"
]

itr = iter(
    languages
)

print(next(itr))
print(next(itr))
print(next(itr))
```

### Output
Python
Java
C++

### Explanation

The iterator returns each element one after another until all elements are exhausted.

# Creating a Custom Iterator

Custom iterators are created by implementing `__iter__()` and `__next__()` methods.

### Example

```python
class MultiplesOfThree:

    def __init__(self, limit):
        self.limit = limit
        self.number = 3

    def __iter__(self):
        return self

    def __next__(self):

        if self.number > self.limit:
            raise StopIteration

        value = self.number
        self.number += 3

        return value

obj = MultiplesOfThree(
    15
)

for num in obj:
    print(num)
```

### Output
3
6
9
12
15

### Explanation

- `__iter__()` returns the iterator object.
- `__next__()` returns multiples of 3.
- When the limit is exceeded, `StopIteration` is raised.

# Using next()

The `next()` function retrieves one element at a time.

### Example

```python
subjects = [
    "Math",
    "Science",
    "English"
]

itr = iter(
    subjects
)

print(next(itr))
print(next(itr))
```

### Output
Math
Science

### Explanation

Each call to `next()` moves the iterator forward by one position.

# StopIteration Exception

When an iterator reaches the end, Python raises `StopIteration`.

### Example

```python
numbers = [
    50,
    100
]

itr = iter(
    numbers
)

while True:

    try:
        print(
            next(itr)
        )

    except StopIteration:
        print(
            "Iteration Finished"
        )
        break
```

### Output
50
100
Iteration Finished

### Explanation

The exception indicates that there are no more elements left in the iterator.

# Iterator vs Iterable

An iterable is an object that can create an iterator, while an iterator is responsible for returning elements one by one.

### Example

```python
books = [
    "DSA",
    "DBMS",
    "OS"
]

itr = iter(
    books
)

print(next(itr))
print(next(itr))
print(next(itr))
```

### Output
DSA
DBMS
OS

### Explanation

- `books` is an iterable.
- `itr` is an iterator.
- `next()` fetches individual elements.

# Difference Between Iterable and Iterator

| Feature | Iterable | Iterator |
| --- | --- | --- |
| Definition | Collection that can return an iterator | Object that traverses elements |
| Special Method | `__iter__()` | `__iter__()` and `__next__()` |
| Examples | List, Tuple, String, Set | Object returned by `iter()` |
| Supports next() | No | Yes |

# Advantages of Iterators

1. Memory efficient.
2. Support lazy evaluation.
3. Process large datasets easily.
4. Maintain traversal state automatically.
5. Integrate well with generators and loops.

# Limitations

1. Elements cannot be revisited unless a new iterator is created.
2. Iterators move only in forward direction.
3. Once exhausted, they cannot be reset automatically.

# Summary

Iterators are objects that allow sequential access to elements of a collection. They implement the `__iter__()` and `__next__()` methods and provide efficient memory usage through lazy evaluation. Python provides built-in iterators for collections and also allows developers to create custom iterators for specialized tasks.

