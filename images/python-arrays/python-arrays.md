# Python Arrays

## Introduction

An array is a linear data structure used to store multiple elements of the same data type in contiguous memory locations. Python provides arrays through the `array` module, which offers memory-efficient storage for homogeneous data. Arrays are commonly used when working with large collections of numbers.

### Key Features

- Stores elements of the same data type.
- Memory efficient.
- Supports indexing and slicing.
- Dynamic in size.
- Faster than lists for numerical storage.
- Supports insertion, deletion, and searching operations.
- Provides various built-in methods.

# Why Use Arrays?

Arrays are useful when storing many values of the same type while using less memory compared to lists.

### Example

```python
import array as arr

scores = arr.array(
    'i',
    [85, 90, 95]
)

print(scores)
```

### Output
array('i', [85, 90, 95])

### Explanation

The array stores integer values using the typecode `'i'`.

# Creating Arrays

Arrays are created using the `array()` function.

### Example

```python
import array as arr

marks = arr.array(
    'i',
    [70, 80, 90]
)

print(marks)
```

### Output
array('i', [70, 80, 90])

### Explanation

The typecode `'i'` represents integer values.

# Common Typecodes

| Typecode | Data Type |
| --- | --- |
| `'i'` | Integer |
| `'f'` | Float |
| `'d'` | Double |
| `'b'` | Signed Integer |

# Accessing Elements

Array elements are accessed using indexes.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30, 40]
)

print(numbers[0])

print(numbers[2])
```

### Output
10
30

### Explanation

Indexing starts from 0.

# Negative Indexing

### Example

```python
import array as arr

values = arr.array(
    'i',
    [100, 200, 300]
)

print(values[-1])

print(values[-2])
```

### Output
300
200

### Explanation

Negative indexes access elements from the end.

# Adding Elements

## append()

Adds an element at the end.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [1, 2, 3]
)

numbers.append(4)

print(numbers)
```

### Output
array('i', [1, 2, 3, 4])

### Explanation

The new element is added at the end.

## insert()

Adds an element at a specified index.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 30]
)

numbers.insert(1, 20)

print(numbers)
```

### Output
array('i', [10, 20, 30])

### Explanation

The value 20 is inserted at index 1.

## extend()

Adds multiple elements.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [1, 2, 3]
)

numbers.extend(
    [4, 5]
)

print(numbers)
```

### Output
array('i', [1, 2, 3, 4, 5])

### Explanation

Multiple values are appended to the array.

# Updating Elements

Elements can be modified using indexing.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30]
)

numbers[1] = 25

print(numbers)
```

### Output
array('i', [10, 25, 30])

### Explanation

The element at index 1 is updated.

# Removing Elements

## remove()

Removes the first occurrence of a value.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30]
)

numbers.remove(20)

print(numbers)
```

### Output
array('i', [10, 30])

### Explanation

The value 20 is removed.

## pop()

Removes an element by index.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30]
)

numbers.pop()

print(numbers)
```

### Output
array('i', [10, 20])

### Explanation

The last element is removed.

# Slicing Arrays

Slicing extracts a range of elements.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30, 40, 50]
)

print(numbers[1:4])

print(numbers[:3])

print(numbers[2:])
```

### Output
array('i', [20, 30, 40])
array('i', [10, 20, 30])
array('i', [30, 40, 50])

### Explanation

Slicing creates a new array containing selected elements.

# Searching Elements

The `index()` method finds the position of an element.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [5, 10, 15, 20]
)

print(
    numbers.index(15)
)
```

### Output
2

### Explanation

The value 15 is present at index 2.

# Iterating Through Arrays

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [100, 200, 300]
)

for value in numbers:
    print(value)
```

### Output
100
200
300

### Explanation

The loop accesses each element one by one.

# Counting Occurrences

The `count()` method returns the number of occurrences.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [1, 2, 1, 3, 1]
)

print(
    numbers.count(1)
)
```

### Output
3

### Explanation

The value 1 appears three times.

# Reversing Arrays

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [1, 2, 3, 4]
)

numbers.reverse()

print(numbers)
```

### Output
array('i', [4, 3, 2, 1])

### Explanation

The order of elements is reversed.

# Array Type Conversion

Arrays can be converted to lists.

### Example

```python
import array as arr

numbers = arr.array(
    'i',
    [10, 20, 30]
)

print(
    numbers.tolist()
)
```

### Output
[10, 20, 30]

### Explanation

The array is converted into a Python list.

# NumPy Arrays

NumPy arrays are widely used for numerical computations.

### Example

```python
import numpy as np

values = np.array(
    [2, 4, 6]
)

print(values * 2)
```

### Output
[ 4  8 12 ]

### Explanation

Operations are applied element-wise.

# Advantages of Arrays

1. Memory efficient.
2. Faster numerical operations.
3. Store homogeneous data.
4. Support indexing and slicing.
5. Dynamic in size.
6. Suitable for large datasets.

# Limitations of Arrays

1. Store only one data type.
2. Less flexible than lists.
3. Require importing the `array` module.
4. Insertions in the middle are costly.

# Applications of Arrays

- Storing numerical data.
- Scientific computing.
- Statistical analysis.
- Matrix operations.
- Signal processing.
- Data analysis.

# Common Array Methods

| Method | Description |
| --- | --- |
| `append()` | Adds an element |
| `insert()` | Inserts an element |
| `extend()` | Adds multiple elements |
| `remove()` | Removes a value |
| `pop()` | Removes an element |
| `count()` | Counts occurrences |
| `index()` | Finds element position |
| `reverse()` | Reverses elements |
| `tolist()` | Converts array to list |

# Summary

Arrays are memory-efficient linear data structures used to store homogeneous data. Python provides arrays through the `array` module and also supports powerful numerical arrays using NumPy. Arrays support indexing, slicing, insertion, deletion, searching, and various built-in methods, making them suitable for scientific and numerical applications.

