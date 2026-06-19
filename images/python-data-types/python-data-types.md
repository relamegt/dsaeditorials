# Python Data Types

## Introduction

Data types in Python define the kind of value stored in a variable and determine the operations that can be performed on that data. Since everything in Python is treated as an object, every value belongs to a specific data type.

Data types help Python efficiently store and process information and ensure that only valid operations are performed on compatible values.

### Key Features

- Every value in Python has a data type.
- Python automatically determines the data type based on the assigned value.
- Supports numeric, sequence, boolean, set, and dictionary types.
- Objects of different data types support different operations.
- Everything in Python is an object.

## Why Data Types?

Data types allow Python to understand how values should be stored and manipulated.

### Example

```python
x = 50
x = 60.5
x = "Hello World"
x = ["Python", "Programming"]
x = ("Python", "Programming")

print(x)
```

### Output
('Python', 'Programming')

### Explanation

The variable `x` changes its type with each assignment. Python dynamically updates the data type according to the assigned value.

# Numeric Data Types

Numeric data types are used to represent numbers.

Python supports three numeric types:

- `int`
- `float`
- `complex`

## Integer (int)

Integers represent whole numbers without decimal points.

### Example

```python
num = 100

print(type(num))
```

### Output
<class 'int'>

## Float

Floating-point numbers contain decimal values.

### Example

```python
price = 99.99

print(type(price))
```

### Output
<class 'float'>

## Complex

Complex numbers contain real and imaginary parts.

### Example

```python
c = 3 + 4j

print(type(c))
```

### Output
<class 'complex'>

# Sequence Data Types

Sequence types store ordered collections of values.

Python provides:

1. String
2. List
3. Tuple

## String

Strings store textual data.

### Example

```python
s = "Welcome to AlphaKnowledge"

print(s)
print(type(s))
print(s[0])
print(s[-1])
```

### Output
Welcome to AlphaKnowledge
<class 'str'>
W
e

### Explanation

Strings are ordered sequences of characters and support indexing.

## List

Lists are ordered and mutable collections.

### Example

```python
numbers = [10, 20, 30]

print(numbers)
print(numbers[1])
```

### Output
[10, 20, 30]
20

### Explanation

Lists allow modification of elements after creation.

## Tuple

Tuples are ordered and immutable collections.

### Example

```python
data = ("Python", "Java", "C")

print(type(data))
print(data[0])
```

### Output
<class 'tuple'>
Python

### Explanation

Tuple elements cannot be modified after creation.

# Boolean Data Type

Boolean values represent logical truth values.

Possible values are:

- True
- False

### Example

```python
print(type(True))
print(type(False))
```

### Output
<class 'bool'>
<class 'bool'>

## Truthy and Falsy Values

Values can behave as either True or False.

### Example

```python
if 1:
    print("1 is truthy")

if not 0:
    print("0 is falsy")
```

### Output
1 is truthy
0 is falsy

### Explanation

Non-zero values are generally truthy, while zero is falsy.

# Set Data Type

Sets are unordered collections containing unique elements.

### Example

```python
s = {"a", "a", "b", "c"}

print(s)
```

### Output
{'a', 'b', 'c'}

### Explanation

Duplicate elements are automatically removed from a set.

## Iterating Through a Set

### Example

```python
languages = {"Python", "Java", "C"}

for i in languages:
    print(i)
```

### Output
Python
Java
C

### Note

Since sets are unordered, the order of output may vary.

# Dictionary Data Type

Dictionaries store data in key-value pairs.

### Example

```python
student = {
    1: "Akash",
    2: "Hemesh",
    3: "Abhiram"
}

print(student[1])
print(student.get(2))
```

### Output
Akash
Hemesh

### Explanation

Dictionary values are accessed using keys.

# Important Data Type Functions

## 1. type()

Returns the type of an object.

### Example

```python
x = 10

print(type(x))
```

### Output
<class 'int'>

## 2. len()

Returns the number of elements.

### Example

```python
name = "Python"

print(len(name))
```

### Output
6

## 3. list()

Converts values into a list.

### Example

```python
data = list((1, 2, 3))

print(data)
```

### Output
[1, 2, 3]

## 4. tuple()

Converts values into a tuple.

### Example

```python
numbers = tuple([10, 20, 30])

print(numbers)
```

### Output
(10, 20, 30)

## 5. set()

Creates a set.

### Example

```python
s = set([1, 2, 2, 3])

print(s)
```

### Output
{1, 2, 3}

## 6. dict()

Creates a dictionary.

### Example

```python
d = dict(name="Akash", age=22)

print(d)
```

### Output
{'name': 'Akash', 'age': 22}

# Mutable vs Immutable Data Types

| Mutable | Immutable |
| --- | --- |
| List | Integer |
| Set | Float |
| Dictionary | String |
| — | Tuple |
| — | Boolean |
| — | Complex |

# Advantages of Data Types

1. Help Python manage memory efficiently.
2. Ensure valid operations are performed.
3. Support different kinds of information.
4. Improve readability and maintainability.
5. Provide flexibility through dynamic typing.
6. Allow powerful built-in operations.

# Limitations

1. Dynamic typing may cause runtime errors.
2. Mutable objects can accidentally change.
3. Different data types support different operations, which may confuse beginners.
4. Type mismatches can lead to exceptions.

# Summary

Data types define the nature of values stored in Python variables. Python provides numeric types (`int`, `float`, `complex`), sequence types (`str`, `list`, `tuple`), boolean values (`True`, `False`), sets, and dictionaries. Since Python is dynamically typed, variables can change their data type during execution. Understanding data types is essential because they determine how values are stored, manipulated, and processed within Python programs.

