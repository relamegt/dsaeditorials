# Python Collections Counter

## Introduction

`Counter` is a specialized dictionary available in Python's `collections` module. It is designed to count the frequency of elements in an iterable such as lists, strings, tuples, or dictionaries. Instead of manually maintaining counts, Counter provides built-in functionality for efficient frequency analysis.

### Key Features

- Counts occurrences automatically.
- Works with lists, strings, tuples, and dictionaries.
- Returns 0 for missing elements.
- Supports arithmetic operations.
- Provides useful methods like `most_common()`, `update()`, and `subtract()`.

# Why Use Counter?

Counter simplifies frequency counting and reduces the amount of code required compared to ordinary dictionaries.

### Example

```python
from collections import Counter

languages = ["Python", "Java", "Python", "C++", "Python", "Java"]

counts = Counter(languages)

print(counts)
```

### Output
Counter({'Python': 3, 'Java': 2, 'C++': 1})

### Explanation

Counter automatically counts the occurrences of each element.

# Syntax

```python
from collections import Counter

Counter(iterable_or_mapping)
```

### Parameters

- **iterable** → List, tuple, string, etc.
- **mapping** → Dictionary containing counts.
- **keyword arguments** → Named values with counts.

### Return Type

Returns a Counter object.

# Creating a Counter

## From a List

### Example

```python
from collections import Counter

numbers = [10, 20, 20, 30, 30, 30]

counter_obj = Counter(numbers)

print(counter_obj)
```

### Output
Counter({30: 3, 20: 2, 10: 1})

### Explanation

Each number is counted automatically.

## From a String

### Example

```python
from collections import Counter

word = "alphaknowledge"

counter_obj = Counter(word)

print(counter_obj)
```

### Output
Counter({'a': 2, 'l': 2, 'e': 2, 'h': 1, 'p': 1, 'k': 1, 'n': 1, 'o': 1, 'w': 1, 'd': 1, 'g': 1})

### Explanation

Counter counts every character in the string.

## From a Dictionary

### Example

```python
from collections import Counter

counter_obj = Counter({
    "Python": 5,
    "Java": 3,
    "C++": 2
})

print(counter_obj)
```

### Output
Counter({'Python': 5, 'Java': 3, 'C++': 2})

### Explanation

Counter can also be initialized using a dictionary.

# Accessing Counter Elements

### Example

```python
from collections import Counter

scores = Counter([50, 60, 60, 70, 70, 70])

print(scores[50])
print(scores[60])
print(scores[70])
print(scores[80])
```

### Output
1
2
3
0

### Explanation

If an element does not exist, Counter returns 0 instead of raising an error.

# Why Counter is Better Than a Dictionary

- Missing keys return 0.
- Frequency counting requires less code.
- Built-in methods simplify operations.
- Supports arithmetic operations.
- Useful for data analysis and statistics.

# Counter Methods

## update()

Adds counts from another iterable.

### Example

```python
from collections import Counter

items = Counter(["Laptop", "Laptop", "Mouse"])

items.update(["Mouse", "Keyboard", "Keyboard"])

print(items)
```

### Output
Counter({'Laptop': 2, 'Mouse': 2, 'Keyboard': 2})

### Explanation

Counts are increased and new elements are added automatically.

# elements()

Returns an iterator containing repeated elements.

### Example

```python
from collections import Counter

marks = Counter([90, 90, 80, 70])

result = list(marks.elements())

print(result)
```

### Output
[90, 90, 80, 70]

### Explanation

Each value appears according to its frequency.

# most_common()

Returns the most frequently occurring elements.

### Example

```python
from collections import Counter

students = Counter([
    "Akash Dangudubiyyapu",
    "Mohit Chandaluri",
    "Akash Dangudubiyyapu",
    "Abhiram Gopisetti",
    "Akash Dangudubiyyapu"
])

print(students.most_common(2))
```

### Output
[('Akash Dangudubiyyapu', 3), ('Mohit Chandaluri', 1)]

### Explanation

The two most common elements are returned.

# Increasing Count Manually

### Example

```python
from collections import Counter

visits = Counter(["Monday", "Monday"])

visits["Tuesday"] += 1
visits["Monday"] += 2

print(visits)
```

### Output
Counter({'Monday': 4, 'Tuesday': 1})

### Explanation

Existing counts increase and missing keys start from 0.

# subtract()

Reduces counts using another iterable.

### Example

```python
from collections import Counter

inventory = Counter(["Book", "Book", "Pen", "Pen", "Pen"])

inventory.subtract(["Pen", "Book"])

print(inventory)
```

### Output
Counter({'Pen': 2, 'Book': 1})

### Explanation

Specified elements have their counts reduced.

# Arithmetic Operations

## Addition

### Example

```python
from collections import Counter

first = Counter([1, 1, 2])
second = Counter([2, 3])

print(first + second)
```

### Output
Counter({1: 2, 2: 2, 3: 1})

## Subtraction

### Example

```python
from collections import Counter

first = Counter([1, 1, 2, 3])
second = Counter([1, 3])

print(first - second)
```

### Output
Counter({1: 1, 2: 1})

## Intersection

### Example

```python
from collections import Counter

first = Counter([1, 1, 2, 3])
second = Counter([1, 2, 2, 4])

print(first & second)
```

### Output
Counter({1: 1, 2: 1})

### Explanation

Intersection keeps the minimum count of common elements.

## Union

### Example

```python
from collections import Counter

first = Counter([1, 1, 2])
second = Counter([1, 2, 2, 3])

print(first | second)
```

### Output
Counter({1: 2, 2: 2, 3: 1})

### Explanation

Union keeps the maximum count of each element.

# Applications of Counter

- Frequency analysis.
- Word counting.
- Character counting.
- Voting systems.
- Inventory management.
- Data analytics.
- Statistical computations.

# Common Counter Methods

| Method | Description |
| --- | --- |
| `update()` | Adds counts from another iterable |
| `elements()` | Returns repeated elements |
| `most_common()` | Returns most frequent elements |
| `subtract()` | Decreases counts |
| `clear()` | Removes all elements |
| `copy()` | Creates a copy |

# Advantages of Counter

1. Easy frequency counting.
2. Less code compared to dictionaries.
3. Missing keys return 0.
4. Supports arithmetic operations.
5. Provides useful built-in methods.

# Limitations of Counter

1. Works only with hashable elements.
2. Uses more memory than simple variables.
3. Ordering depends on insertion.

# Summary

`Counter` is a powerful subclass of dictionary available in the `collections` module. It simplifies counting operations, provides built-in frequency methods, supports arithmetic operations, and is widely used in text processing, analytics, statistics, and data science applications.

