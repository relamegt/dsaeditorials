# Python Dictionary

## Introduction

A dictionary is a built-in data structure used to store data in the form of key-value pairs. Each key must be unique and immutable, while values can be of any data type. Dictionaries allow fast retrieval of data using keys instead of numerical indexes.

### Key Features

- Stores data as key-value pairs.
- Keys are unique.
- Values can be of any data type.
- Mutable and dynamic.
- Maintains insertion order.
- Supports nested dictionaries.
- Provides fast lookup using keys.

# Why Use Dictionaries?

Dictionaries are useful when data needs to be accessed using meaningful names instead of positions. They are commonly used for storing records, configurations, and mappings.

### Example

```python
student = {
    "name": "Akash Dangudubiyyapu",
    "course": "Python"
}

print(student)
```

### Output
{'name': 'Akash Dangudubiyyapu', 'course': 'Python'}

### Explanation

The dictionary stores information in key-value format.

# Creating Dictionaries

Dictionaries can be created in different ways.

## 1. Using Curly Braces

### Example

```python
marks = {
    "maths": 92,
    "science": 88
}

print(marks)
```

### Output
{'maths': 92, 'science': 88}

### Explanation

Curly braces are used to define key-value pairs.

## 2. Using dict() Constructor

### Example

```python
employee = dict(
    name="Mohit Chandaluri",
    role="Developer"
)

print(employee)
```

### Output
{'name': 'Mohit Chandaluri', 'role': 'Developer'}

### Explanation

The `dict()` function creates a dictionary from keyword arguments.

# Accessing Dictionary Elements

Values are accessed using keys.

### Example

```python
profile = {
    "name": "Abhiram Gopisetti",
    "age": 22
}

print(profile["name"])

print(profile.get("age"))
```

### Output
Abhiram Gopisetti
22

### Explanation

- Square brackets directly access a value.
- `get()` safely retrieves a value.

# Adding Elements

New key-value pairs can be added using assignment.

### Example

```python
person = {
    "name": "Adapa Hemesh"
}

person["city"] = "Vijayawada"

print(person)
```

### Output
{'name': 'Adapa Hemesh', 'city': 'Vijayawada'}

### Explanation

A new key-value pair is added to the dictionary.

# Updating Elements

Existing values can be modified.

### Example

```python
course = {
    "title": "Python Basics",
    "level": "Beginner"
}

course["level"] = "Intermediate"

print(course)
```

### Output
{'title': 'Python Basics', 'level': 'Intermediate'}

### Explanation

The value associated with the key `level` is updated.

# Removing Elements

Python provides several methods for deleting items.

## 1. del Statement

### Example

```python
details = {
    "name": "Hemanth Akhil",
    "age": 23
}

del details["age"]

print(details)
```

### Output
{'name': 'Hemanth Akhil'}

## 2. pop()

### Example

```python
data = {
    "python": 95,
    "java": 88
}

score = data.pop("java")

print(score)

print(data)
```

### Output
88
{'python': 95}

### Explanation

`pop()` removes the key and returns its value.

## 3. popitem()

### Example

```python
subjects = {
    "python": 1,
    "java": 2
}

print(subjects.popitem())
```

### Output
('java', 2)

### Explanation

`popitem()` removes and returns the last inserted pair.

## 4. clear()

### Example

```python
languages = {
    "python": 1,
    "cpp": 2
}

languages.clear()

print(languages)
```

### Output
{}

### Explanation

All items are removed from the dictionary.

# Iterating Through Dictionaries

## 1. Iterating Through Keys

### Example

```python
skills = {
    "python": 1,
    "java": 2
}

for key in skills:
    print(key)
```

### Output
python
java

### Explanation

The loop accesses dictionary keys.

## 2. Iterating Through Values

### Example

```python
ratings = {
    "Python": 5,
    "Java": 4
}

for value in ratings.values():
    print(value)
```

### Output
5
4

### Explanation

The loop accesses dictionary values.

## 3. Iterating Through Key-Value Pairs

### Example

```python
courses = {
    "Python": "AlphaKnowledge",
    "Java": "AlphaKnowledge"
}

for key, value in courses.items():
    print(key, value)
```

### Output
Python AlphaKnowledge
Java AlphaKnowledge

### Explanation

The `items()` method returns key-value pairs.

# Nested Dictionaries

A dictionary can contain another dictionary.

### Example

```python
academy = {
    "trainer": {
        "name": "Akash Dangudubiyyapu",
        "specialization": "Python"
    }
}

print(academy["trainer"]["name"])
```

### Output
Akash Dangudubiyyapu

### Explanation

Nested dictionaries allow storing structured information.

# Dictionary Membership Testing

The `in` operator checks whether a key exists.

### Example

```python
platform = {
    "name": "AlphaKnowledge",
    "category": "Education"
}

print("name" in platform)

print("rating" in platform)
```

### Output
True
False

### Explanation

The operator checks for keys, not values.

# Common Dictionary Methods

## len()

Returns the number of key-value pairs.

### Example

```python
data = {
    "a": 10,
    "b": 20,
    "c": 30
}

print(len(data))
```

### Output
3

## keys()

Returns all keys.

### Example

```python
details = {
    "name": "Mohit Chandaluri",
    "age": 24
}

print(details.keys())
```

### Output
dict_keys(['name', 'age'])

## values()

Returns all values.

### Example

```python
details = {
    "python": 90,
    "java": 80
}

print(details.values())
```

### Output
dict_values([90, 80])

## items()

Returns key-value pairs.

### Example

```python
details = {
    "name": "Abhiram Gopisetti",
    "age": 22
}

print(details.items())
```

### Output
dict_items([('name', 'Abhiram Gopisetti'), ('age', 22)])

## update()

Updates dictionary items.

### Example

```python
info = {
    "name": "Adapa Hemesh"
}

info.update({
    "city": "Hyderabad"
})

print(info)
```

### Output
{'name': 'Adapa Hemesh', 'city': 'Hyderabad'}

# Dictionary Comprehension

Dictionary comprehension provides a concise way to create dictionaries.

### Example

```python
squares = {
    number: number ** 2
    for number in range(1, 6)
}

print(squares)
```

### Output
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

### Explanation

Each number becomes a key and its square becomes the value.

# Advantages of Dictionaries

1. Fast data retrieval.
2. Dynamic and mutable.
3. Supports nested structures.
4. Stores multiple data types.
5. Keys provide meaningful access.
6. Efficient for lookup operations.

# Limitations of Dictionaries

1. Keys must be unique.
2. Mutable keys are not allowed.
3. Consume more memory than lists.
4. Searching values is slower than searching keys.

# Applications of Dictionaries

- Student records.
- User profiles.
- Configuration settings.
- JSON data handling.
- Database-like structures.
- Caching and mappings.

# Common Dictionary Methods

| Method | Description |
| --- | --- |
| `get()` | Returns value for a key |
| `keys()` | Returns all keys |
| `values()` | Returns all values |
| `items()` | Returns key-value pairs |
| `update()` | Updates dictionary |
| `pop()` | Removes a key and returns its value |
| `popitem()` | Removes last key-value pair |
| `clear()` | Removes all items |
| `copy()` | Creates a shallow copy |

# Summary

A dictionary is a mutable data structure used to store information as key-value pairs. It provides fast access to values through keys, supports dynamic updates, and allows nested structures. Dictionaries are widely used in Python for representing records, configurations, mappings, and structured data.

