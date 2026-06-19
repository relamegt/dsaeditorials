# Deque in Python

## Introduction

A deque (Double-Ended Queue) is a linear data structure that allows insertion and deletion of elements from both the front and the rear efficiently. Python provides deque through the `collections` module.

Unlike lists, deques provide faster operations at both ends and can act as both stacks and queues.

### Key Features

- Supports insertion from both ends.
- Supports deletion from both ends.
- Faster than lists for front operations.
- Can be used as Stack (LIFO).
- Can be used as Queue (FIFO).
- Dynamically resizable.
- Provides rotation and reversal operations.

# Why Use Deque?

Deques are useful when data needs to be inserted or removed frequently from both sides.

### Applications

- Task scheduling.
- Browser history management.
- Sliding window problems.
- Undo and redo operations.
- Queue implementation.
- Stack implementation.

# Creating a Deque

A deque is created using the `deque()` function from the collections module.

### Example

```python
from collections import deque

students = deque(["Akash Dangudubiyyapu", "Mohit Chandaluri", "Abhiram Gopisetti"])

print(students)
```

### Output
deque(['Akash Dangudubiyyapu', 'Mohit Chandaluri', 'Abhiram Gopisetti'])

### Explanation

The `deque()` function creates a double-ended queue containing three elements.

# Accessing Elements

Deque supports indexing like lists.

### Example

```python
from collections import deque

dq = deque([100, 200, 300, 400])

print(dq[0])
print(dq[-1])
```

### Output
100
400

### Explanation

- Index 0 accesses the first element.
- Index -1 accesses the last element.

# Adding Elements

## append()

Adds an element to the right side.

### Example

```python
from collections import deque

dq = deque([10, 20, 30])

dq.append(40)

print(dq)
```

### Output
deque([10, 20, 30, 40])

### Explanation

40 is inserted at the rear.

# Adding Elements to the Front

## appendleft()

Adds an element to the left side.

### Example

```python
from collections import deque

dq = deque([20, 30, 40])

dq.appendleft(10)

print(dq)
```

### Output
deque([10, 20, 30, 40])

### Explanation

10 is inserted at the front.

# Adding Multiple Elements

## extend()

Adds multiple values to the right side.

### Example

```python
from collections import deque

dq = deque([1, 2])

dq.extend([3, 4, 5])

print(dq)
```

### Output
deque([1, 2, 3, 4, 5])

### Explanation

Three elements are added to the rear.

# Adding Multiple Elements to the Front

## extendleft()

Adds elements to the left side.

### Example

```python
from collections import deque

dq = deque([30, 40])

dq.extendleft([20, 10])

print(dq)
```

### Output
deque([10, 20, 30, 40])

### Explanation

Elements are inserted from left to right, causing the sequence to appear reversed.

# Removing Specific Elements

## remove()

Removes the first occurrence of an element.

### Example

```python
from collections import deque

dq = deque([5, 10, 15, 10])

dq.remove(10)

print(dq)
```

### Output
deque([5, 15, 10])

### Explanation

Only the first occurrence of 10 is removed.

# Removing from the Rear

## pop()

Removes and returns the last element.

### Example

```python
from collections import deque

dq = deque([10, 20, 30])

value = dq.pop()

print(value)
print(dq)
```

### Output
30
deque([10, 20])

### Explanation

The element at the rear is removed.

# Removing from the Front

## popleft()

Removes and returns the first element.

### Example

```python
from collections import deque

dq = deque([10, 20, 30])

value = dq.popleft()

print(value)
print(dq)
```

### Output
10
deque([20, 30])

### Explanation

The first element is removed.

# Clearing the Deque

## clear()

Removes all elements.

### Example

```python
from collections import deque

dq = deque([1, 2, 3])

dq.clear()

print(dq)
```

### Output
deque([])

### Explanation

The deque becomes empty.

# Finding Length

## len()

Returns the total number of elements.

### Example

```python
from collections import deque

dq = deque([100, 200, 300, 400])

print(len(dq))
```

### Output
4

### Explanation

There are four elements in the deque.

# Counting Elements

## count()

Returns how many times an element appears.

### Example

```python
from collections import deque

dq = deque([5, 10, 5, 20, 5])

print(dq.count(5))
```

### Output
3

### Explanation

5 appears three times.

# Rotating a Deque

## rotate()

Moves elements circularly.

### Example

```python
from collections import deque

dq = deque([1, 2, 3, 4])

dq.rotate(1)

print(dq)
```

### Output
deque([4, 1, 2, 3])

### Explanation

The last element moves to the beginning.

# Reversing a Deque

## reverse()

Reverses the order of elements.

### Example

```python
from collections import deque

dq = deque([10, 20, 30, 40])

dq.reverse()

print(dq)
```

### Output
deque([40, 30, 20, 10])

### Explanation

The order of elements becomes reversed.

# Using Deque as a Stack

### Example

```python
from collections import deque

stack = deque()

stack.append("Akash Dangudubiyyapu")
stack.append("Mohit Chandaluri")
stack.append("Abhiram Gopisetti")

print(stack.pop())
```

### Output
Abhiram Gopisetti

### Explanation

The last inserted element is removed first, following LIFO order.

# Using Deque as a Queue

### Example

```python
from collections import deque

queue = deque()

queue.append("Adapa Hemesh")
queue.append("Hemanth")
queue.append("Akhil")

print(queue.popleft())
```

### Output
Adapa Hemesh

### Explanation

The first inserted element is removed first, following FIFO order.

# Advantages of Deque

1. Fast insertion at both ends.
2. Fast deletion at both ends.
3. Efficient implementation of stacks and queues.
4. Dynamically resizable.
5. Provides rotation and reversal operations.

# Limitations of Deque

1. Random access is slower than lists.
2. Does not support slicing directly.
3. Middle element operations are slower.

# Applications of Deque

- Queue implementation.
- Stack implementation.
- Browser history.
- Undo and redo systems.
- Sliding window problems.
- CPU scheduling.
- Real-time data processing.

# Common Deque Methods

| Method | Description |
| --- | --- |
| `append()` | Add element at rear |
| `appendleft()` | Add element at front |
| `extend()` | Add multiple elements at rear |
| `extendleft()` | Add multiple elements at front |
| `remove()` | Remove first occurrence |
| `pop()` | Remove from rear |
| `popleft()` | Remove from front |
| `clear()` | Remove all elements |
| `count()` | Count occurrences |
| `rotate()` | Rotate elements |
| `reverse()` | Reverse elements |

# Summary

Deque is a double-ended queue provided by the `collections` module. It supports efficient insertion and deletion from both the front and rear. Deques are commonly used for implementing stacks, queues, scheduling systems, and sliding window algorithms due to their speed and flexibility.

