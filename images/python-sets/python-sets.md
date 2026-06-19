# Python Sets

## Introduction

A set is a built-in Python data structure used to store a collection of unique elements. Sets are unordered and mutable, meaning elements can be added or removed, but duplicate values are automatically eliminated. Sets are widely used for membership testing and mathematical set operations.

### Key Features

- Stores only unique elements.
- Unordered collection.
- Mutable data structure.
- Supports fast searching and insertion.
- Automatically removes duplicate values.
- Supports mathematical operations like union and intersection.
- Can store multiple data types.

# Why Use Sets?

Sets are useful when duplicate values are not needed and when fast lookup operations are required.

### Example

```python
technologies = {"Python", "Java", "C++"}

print(technologies)
```

### Output
{'Python', 'Java', 'C++'}

### Explanation

The set stores unique values. The order of elements may vary.

# Creating Sets

Sets can be created in multiple ways.

## 1. Using Curly Braces

### Example

```python
courses = {"Python", "Java", "SQL"}

print(courses)
```

### Output
{'Python', 'Java', 'SQL'}

### Explanation

Curly braces create a set containing unique values.

## 2. Using set() Constructor

### Example

```python
letters = set(["A", "B", "C", "D"])

print(letters)
```

### Output
{'A', 'B', 'C', 'D'}

### Explanation

The `set()` function converts other iterables into a set.

# Duplicate Values are Removed Automatically

### Example

```python
topics = {
    "Python",
    "Java",
    "Python",
    "SQL"
}

print(topics)
```

### Output
{'Python', 'Java', 'SQL'}

### Explanation

Duplicate values are removed automatically.

# Heterogeneous Elements

Sets can store different data types.

### Example

```python
data = {
    "AlphaKnowledge",
    100,
    9.24,
    True
}

print(data)
```

### Output
{'AlphaKnowledge', 100, 9.24, True}

### Explanation

A set can contain strings, integers, floating-point numbers, and boolean values.

# Frozen Sets

A frozenset is an immutable version of a set.

### Example

```python
languages = frozenset(
    ["Python", "Java", "SQL"]
)

print(languages)
```

### Output
frozenset({'Python', 'Java', 'SQL'})

### Explanation

Elements inside a frozenset cannot be modified.

# Adding Elements

## add()

Adds a new element to the set.

### Example

```python
skills = {"Python", "Java"}

skills.add("SQL")

print(skills)
```

### Output
{'Python', 'Java', 'SQL'}

### Explanation

The new element is added if it does not already exist.

## update()

Adds multiple elements.

### Example

```python
skills = {"Python"}

skills.update(
    ["Java", "SQL"]
)

print(skills)
```

### Output
{'Python', 'Java', 'SQL'}

### Explanation

Multiple elements are added at once.

# Removing Elements

## remove()

Removes a specific element.

### Example

```python
subjects = {
    "Python",
    "Java",
    "SQL"
}

subjects.remove("Java")

print(subjects)
```

### Output
{'Python', 'SQL'}

### Explanation

The specified element is removed.

## discard()

Removes an element without raising an error if it is absent.

### Example

```python
subjects = {
    "Python",
    "Java",
    "SQL"
}

subjects.discard("Java")

print(subjects)
```

### Output
{'Python', 'SQL'}

## pop()

Removes an arbitrary element.

### Example

```python
languages = {
    "Python",
    "Java",
    "SQL"
}

removed = languages.pop()

print(removed)

print(languages)
```

### Output
Python
{'Java', 'SQL'}

### Explanation

The removed element may vary because sets are unordered.

## clear()

Removes all elements.

### Example

```python
numbers = {
    10,
    20,
    30
}

numbers.clear()

print(numbers)
```

### Output
set()

### Explanation

The set becomes empty.

# Membership Testing

### Example

```python
courses = {
    "Python",
    "Java",
    "SQL"
}

print("Python" in courses)

print("C++" in courses)
```

### Output
True
False

### Explanation

The `in` operator checks whether an element exists.

# Iterating Through Sets

### Example

```python
trainers = {
    "Akash Dangudubiyyapu",
    "Mohit Chandaluri",
    "Abhiram Gopisetti"
}

for trainer in trainers:
    print(trainer)
```

### Output
Akash Dangudubiyyapu
Mohit Chandaluri
Abhiram Gopisetti

### Explanation

Elements are accessed one by one using a loop.

# Set Operations

## Union

Combines all unique elements.

### Example

```python
backend = {
    "Python",
    "Java"
}

database = {
    "SQL",
    "Python"
}

print(
    backend.union(database)
)
```

### Output
{'Python', 'Java', 'SQL'}

### Explanation

Union returns all distinct elements.

## Intersection

Returns common elements.

### Example

```python
batch1 = {
    "Python",
    "Java",
    "SQL"
}

batch2 = {
    "Python",
    "C++"
}

print(
    batch1.intersection(batch2)
)
```

### Output
{'Python'}

### Explanation

Only common elements are returned.

## Difference

Returns elements present only in the first set.

### Example

```python
first = {
    "Python",
    "Java",
    "SQL"
}

second = {
    "Java"
}

print(
    first.difference(second)
)
```

### Output
{'Python', 'SQL'}

### Explanation

Elements present in the second set are excluded.

## Symmetric Difference

Returns elements present in only one set.

### Example

```python
a = {
    "Python",
    "Java"
}

b = {
    "Java",
    "SQL"
}

print(
    a.symmetric_difference(b)
)
```

### Output
{'Python', 'SQL'}

### Explanation

Common elements are removed.

# Subset and Superset

### Example

```python
a = {1, 2}

b = {1, 2, 3, 4}

print(
    a.issubset(b)
)

print(
    b.issuperset(a)
)
```

### Output
True
True

### Explanation

- `issubset()` checks whether all elements exist in another set.
- `issuperset()` checks whether a set contains all elements of another set.

# Common Set Methods

## len()

Returns the number of elements.

### Example

```python
values = {
    10,
    20,
    30
}

print(len(values))
```

### Output
3

## copy()

Creates a shallow copy.

### Example

```python
a = {
    "Python",
    "Java"
}

b = a.copy()

print(b)
```

### Output
{'Python', 'Java'}

# Advantages of Sets

1. Automatically remove duplicate values.
2. Fast searching and lookup.
3. Efficient insertion and deletion.
4. Support mathematical operations.
5. Can store different data types.
6. Useful for membership testing.

# Limitations of Sets

1. Elements are unordered.
2. Indexing and slicing are not supported.
3. Duplicate values cannot be stored.
4. Mutable elements like lists cannot be stored.

# Applications of Sets

- Removing duplicate data.
- Membership testing.
- Finding common elements.
- Mathematical operations.
- Data analysis and filtering.
- Database operations.

# Common Set Methods

| Method | Description |
| --- | --- |
| `add()` | Adds an element |
| `update()` | Adds multiple elements |
| `remove()` | Removes an element |
| `discard()` | Removes an element safely |
| `pop()` | Removes a random element |
| `clear()` | Removes all elements |
| `copy()` | Creates a copy |
| `union()` | Combines sets |
| `intersection()` | Returns common elements |
| `difference()` | Returns unique elements |
| `symmetric_difference()` | Returns non-common elements |
| `issubset()` | Checks subset relationship |
| `issuperset()` | Checks superset relationship |

# Summary

Sets are mutable collections that store unique elements and support fast lookup operations. They automatically eliminate duplicates and provide powerful operations such as union, intersection, difference, and subset testing. Sets are commonly used in data processing, membership testing, and removing duplicate values efficiently.

