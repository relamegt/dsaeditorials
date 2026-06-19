# Python Lists

## Introduction

A list is a built-in data structure used to store an ordered collection of elements. Lists are dynamic, resizable, and capable of storing different types of data. Since lists are mutable, elements can be modified after creation, making them one of the most commonly used data structures in Python.

### Key Features

- Lists are mutable.
- Elements preserve insertion order.
- Support indexing and slicing.
- Can contain different data types.
- Allow duplicate values.
- Support nested lists.
- Dynamic in size.

# Why Use Lists?

Lists help store multiple values together and provide convenient methods for insertion, deletion, searching, and iteration.

### Example

```python
marks = [85, 90, 95]

print(marks)
```

### Output
[85, 90, 95]

### Explanation

The list stores multiple values inside square brackets.

# Creating Lists

Lists can be created in different ways.

## 1. Using Square Brackets

### Example

```python
numbers = [10, 20, 30]

courses = ["Python", "Java"]

print(numbers)
print(courses)
```

### Output
[10, 20, 30]
['Python', 'Java']

### Explanation

Square brackets provide the simplest way to create lists.

## 2. Using list() Constructor

### Example

```python
data = list((100, 200, "AlphaKnowledge", 9.24))

letters = list("CODE")

print(data)
print(letters)
```

### Output
[100, 200, 'AlphaKnowledge', 9.24]
['C', 'O', 'D', 'E']

### Explanation

The `list()` constructor converts iterable objects into lists.

## 3. Creating Lists with Repeated Elements

### Example

```python
values = [5] * 4

print(values)
```

### Output
[5, 5, 5, 5]

### Explanation

The multiplication operator repeats the element.

# Internal Representation of Lists

Python lists store references to objects instead of storing values directly.

### Example

```python
items = [100, 200, "Python"]

print(items[0])
print(items)
```

### Output
100
[100, 200, 'Python']

### Explanation

Lists can store different data types together.

# Accessing Elements

Elements are accessed using indexing.

### Example

```python
scores = [70, 80, 90]

print(scores[0])
print(scores[-1])
```

### Output
70
90

### Explanation

- Index 0 refers to the first element.
- Index -1 refers to the last element.

# List Slicing

Slicing extracts a portion of a list.

### Example

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
print(numbers[:3])
print(numbers[2:])
print(numbers[::-1])
```

### Output
[20, 30, 40]
[10, 20, 30]
[30, 40, 50]
[50, 40, 30, 20, 10]

### Explanation

Slicing creates a new list containing selected elements.

# Adding Elements

## 1. append()

### Example

```python
numbers = [1, 2]

numbers.append(3)

print(numbers)
```

### Output
[1, 2, 3]

### Explanation

`append()` adds an element at the end.

## 2. insert()

### Example

```python
numbers = [10, 30]

numbers.insert(1, 20)

print(numbers)
```

### Output
[10, 20, 30]

### Explanation

`insert()` adds an element at a specific index.

## 3. extend()

### Example

```python
numbers = [1, 2]

numbers.extend([3, 4])

print(numbers)
```

### Output
[1, 2, 3, 4]

### Explanation

`extend()` adds multiple elements.

# Updating Elements

### Example

```python
ages = [18, 20, 22]

ages[1] = 21

print(ages)
```

### Output
[18, 21, 22]

### Explanation

Lists are mutable, so elements can be modified.

# Removing Elements

## 1. remove()

### Example

```python
values = [5, 10, 15]

values.remove(10)

print(values)
```

### Output
[5, 15]

## 2. pop()

### Example

```python
values = [100, 200, 300]

values.pop()

print(values)
```

### Output
[100, 200]

## 3. del Statement

### Example

```python
values = [1, 2, 3]

del values[1]

print(values)
```

### Output
[1, 3]

## 4. clear()

### Example

```python
values = [10, 20, 30]

values.clear()

print(values)
```

### Output
[]

# Iterating Through Lists

### Example

```python
students = [
    "Akash Dangudubiyyapu",
    "Abhiram Gopisetti",
    "Adapa Hemesh"
]

for student in students:
    print(student)
```

### Output
Akash Dangudubiyyapu
Abhiram Gopisetti
Adapa Hemesh

### Explanation

The loop accesses one element at a time.

# Nested Lists

### Example

```python
matrix = [
    [1, 2],
    [3, 4]
]

print(matrix[0])
print(matrix[1][1])
```

### Output
[1, 2]
4

### Explanation

Multiple indexes are used to access inner elements.

# List Concatenation

### Example

```python
a = [1, 2]

b = [3, 4]

print(a + b)
```

### Output
[1, 2, 3, 4]

### Explanation

The `+` operator joins two lists.

# Repeating Lists

### Example

```python
values = [7, 8]

print(values * 3)
```

### Output
[7, 8, 7, 8, 7, 8]

### Explanation

The `*` operator repeats the list.

# Membership Testing

### Example

```python
marks = [85, 90, 95]

print(90 in marks)
print(100 in marks)
```

### Output
True
False

### Explanation

The `in` operator checks whether an element exists.

# Common List Methods

## len()

### Example

```python
numbers = [10, 20, 30, 40]

print(len(numbers))
```

### Output
4

## sort()

### Example

```python
numbers = [8, 2, 5, 1]

numbers.sort()

print(numbers)
```

### Output
[1, 2, 5, 8]

## reverse()

### Example

```python
numbers = [1, 2, 3]

numbers.reverse()

print(numbers)
```

### Output
[3, 2, 1]

## count()

### Example

```python
numbers = [5, 2, 5, 8]

print(numbers.count(5))
```

### Output
2

## index()

### Example

```python
numbers = [100, 200, 300]

print(numbers.index(200))
```

### Output
1

## copy()

### Example

```python
numbers = [10, 20, 30]

duplicate = numbers.copy()

print(duplicate)
```

### Output
[10, 20, 30]

# List Comprehension

### Example

```python
squares = [x * x for x in range(1, 6)]

print(squares)
```

### Output
[1, 4, 9, 16, 25]

### Explanation

Each number is squared and stored in a new list.

# Advantages of Lists

1. Dynamic and resizable.
2. Support different data types.
3. Preserve insertion order.
4. Allow duplicate values.
5. Support indexing and slicing.
6. Easy insertion and deletion.

# Limitations of Lists

1. Consume more memory.
2. Searching large lists is slower.
3. Middle insertions are costly.
4. Deep nesting can increase complexity.

# Applications of Lists

- Storing collections of values.
- Implementing stacks and queues.
- Matrix representation.
- Data analysis.
- Dynamic programming.
- Searching and sorting algorithms.

# Common List Methods

| Method | Description |
| --- | --- |
| `append()` | Adds an element at the end |
| `insert()` | Inserts an element at a position |
| `extend()` | Adds multiple elements |
| `remove()` | Removes first occurrence |
| `pop()` | Removes an element |
| `clear()` | Removes all elements |
| `sort()` | Sorts the list |
| `reverse()` | Reverses the list |
| `count()` | Counts occurrences |
| `index()` | Returns index |
| `copy()` | Creates a copy |

# Summary

Lists are mutable and ordered collections used to store multiple elements in Python. They support indexing, slicing, insertion, deletion, iteration, and numerous built-in methods. Because of their flexibility and dynamic nature, lists are among the most widely used data structures in Python.

