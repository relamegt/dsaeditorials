# OrderedDict in Python

## Introduction

`OrderedDict` is a specialized dictionary available in the `collections` module. It stores key-value pairs while preserving the order in which keys are inserted. Although normal dictionaries maintain insertion order in modern Python versions, `OrderedDict` provides additional features for controlling and manipulating the order of keys.

### Key Features

- Preserves insertion order.
- Supports order-sensitive equality checks.
- Allows moving keys to the beginning or end.
- Can remove items from either end.
- Useful for implementing caches and queues.
- Provides extra control over key ordering.

# Why Use OrderedDict?

`OrderedDict` is useful when the sequence of items is important and when additional ordering operations are required.

### Applications

- LRU cache implementation.
- Task scheduling.
- Queue management.
- Data serialization.
- Maintaining logs and histories.

# Creating an OrderedDict

### Example

```python
from collections import OrderedDict

details = OrderedDict()

details["Akash Dangudubiyyapu"] = "Python"
details["Mohit Chandaluri"] = "Java"
details["Abhiram Gopisetti"] = "C++"

print(details)
```

### Output
OrderedDict([('Akash Dangudubiyyapu', 'Python'), ('Mohit Chandaluri', 'Java'), ('Abhiram Gopisetti', 'C++')])

### Explanation

Items are stored in the same order in which they are inserted.

# OrderedDict vs Dictionary

Both preserve insertion order, but OrderedDict offers more control.

### Example

```python
from collections import OrderedDict

normal_dict = {}

normal_dict["Akhil"] = 10
normal_dict["Hemanth"] = 20

ordered_dict = OrderedDict()

ordered_dict["Adapa Hemesh"] = 100
ordered_dict["Akash Dangudubiyyapu"] = 200

print(normal_dict)
print(ordered_dict)
```

### Output
{'Akhil': 10, 'Hemanth': 20}
OrderedDict([('Adapa Hemesh', 100), ('Akash Dangudubiyyapu', 200)])

### Explanation

Both preserve insertion order, but OrderedDict provides additional ordering operations.

# Insertion Order Preservation

### Example

```python
from collections import OrderedDict

subjects = OrderedDict()

subjects["Python"] = 95
subjects["Java"] = 90
subjects["C++"] = 88

for key, value in subjects.items():
    print(key, value)
```

### Output
Python 95
Java 90
C++ 88

### Explanation

The items are displayed in the order they were inserted.

# Updating Values Does Not Change Order

### Example

```python
from collections import OrderedDict

scores = OrderedDict([
    ("Akash Dangudubiyyapu", 90),
    ("Mohit Chandaluri", 85),
    ("Abhiram Gopisetti", 88)
])

scores["Mohit Chandaluri"] = 95

for key, value in scores.items():
    print(key, value)
```

### Output
Akash Dangudubiyyapu 90
Mohit Chandaluri 95
Abhiram Gopisetti 88

### Explanation

Updating a value does not affect the original key position.

# Equality Checks Consider Order

### Example

```python
from collections import OrderedDict

first = OrderedDict([
    ("Python", 1),
    ("Java", 2)
])

second = OrderedDict([
    ("Java", 2),
    ("Python", 1)
])

print(first == second)
```

### Output
False

### Explanation

Although the keys and values are the same, their order differs.

# Reversing an OrderedDict

### Example

```python
from collections import OrderedDict

languages = OrderedDict([
    ("Python", 1),
    ("Java", 2),
    ("C++", 3)
])

reverse_dict = OrderedDict(reversed(list(languages.items())))

for key, value in reverse_dict.items():
    print(key, value)
```

### Output
C++ 3
Java 2
Python 1

### Explanation

A new OrderedDict is created with reversed order.

# Removing the Last Item

## popitem()

### Example

```python
from collections import OrderedDict

marks = OrderedDict([
    ("Akhil", 70),
    ("Hemanth", 80),
    ("Adapa Hemesh", 90)
])

item = marks.popitem()

print(item)
print(marks)
```

### Output
('Adapa Hemesh', 90)
OrderedDict([('Akhil', 70), ('Hemanth', 80)])

### Explanation

The last inserted item is removed.

# Removing the First Item

### Example

```python
from collections import OrderedDict

marks = OrderedDict([
    ("Akhil", 70),
    ("Hemanth", 80),
    ("Adapa Hemesh", 90)
])

item = marks.popitem(last=False)

print(item)
print(marks)
```

### Output
('Akhil', 70)
OrderedDict([('Hemanth', 80), ('Adapa Hemesh', 90)])

### Explanation

Setting `last=False` removes the first item.

# Moving Keys to the End

## move_to_end()

### Example

```python
from collections import OrderedDict

data = OrderedDict([
    ("Python", 1),
    ("Java", 2),
    ("C++", 3)
])

data.move_to_end("Python")

print(data)
```

### Output
OrderedDict([('Java', 2), ('C++', 3), ('Python', 1)])

### Explanation

The key "Python" moves to the end.

# Moving Keys to the Beginning

### Example

```python
from collections import OrderedDict

data = OrderedDict([
    ("Python", 1),
    ("Java", 2),
    ("C++", 3)
])

data.move_to_end("C++", last=False)

print(data)
```

### Output
OrderedDict([('C++', 3), ('Python', 1), ('Java', 2)])

### Explanation

The key "C++" moves to the beginning.

# Deleting and Re-Inserting Keys

### Example

```python
from collections import OrderedDict

students = OrderedDict([
    ("Akash Dangudubiyyapu", 1),
    ("Mohit Chandaluri", 2),
    ("Abhiram Gopisetti", 3)
])

students.pop("Mohit Chandaluri")

students["Mohit Chandaluri"] = 2

print(students)
```

### Output
OrderedDict([('Akash Dangudubiyyapu', 1), ('Abhiram Gopisetti', 3), ('Mohit Chandaluri', 2)])

### Explanation

After reinsertion, the key moves to the end.

# Common OrderedDict Methods

| Method | Description |
| --- | --- |
| `items()` | Returns key-value pairs |
| `keys()` | Returns all keys |
| `values()` | Returns all values |
| `popitem()` | Removes first or last item |
| `move_to_end()` | Moves a key to front or end |
| `update()` | Updates dictionary values |
| `clear()` | Removes all items |
| `copy()` | Creates a copy |

# OrderedDict vs Dictionary

| Feature | Dictionary | OrderedDict |
| --- | --- | --- |
| Preserves insertion order | Yes | Yes |
| Reorder keys | No | Yes |
| Pop first item | No | Yes |
| Order-sensitive equality | No | Yes |
| Performance | Faster | Slightly slower |

# Advantages of OrderedDict

1. Preserves insertion order.
2. Supports reordering of keys.
3. Allows removing items from both ends.
4. Suitable for cache implementations.
5. Supports order-sensitive comparison.

# Limitations of OrderedDict

1. Slightly slower than normal dictionaries.
2. Consumes more memory.
3. Additional features are rarely needed in simple applications.

# Applications of OrderedDict

- LRU Cache.
- Task management systems.
- Maintaining logs.
- Data serialization.
- Scheduling applications.
- Ordered configurations.

# Summary

`OrderedDict` is a dictionary subclass available in the `collections` module that preserves insertion order and provides advanced operations for rearranging keys. It is especially useful in cache systems, task scheduling, and situations where the order of key-value pairs is important.

