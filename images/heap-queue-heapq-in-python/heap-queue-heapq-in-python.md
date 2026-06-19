# Heap Queue (heapq) in Python

## Introduction

A heap queue, also known as a priority queue, is a specialized tree-based data structure that allows efficient retrieval of the smallest or highest-priority element. Python provides the built-in `heapq` module to perform heap operations efficiently.

By default, Python implements a **min-heap**, where the smallest element is always placed at the root.

### Key Features

- Fast insertion and deletion.
- Smallest element is always available at the root.
- Implemented using lists.
- Efficient priority queue implementation.
- Supports merging and replacement operations.

# Why Use Heap Queue?

Heap queues are useful when elements need to be processed according to priority.

### Applications

- Task scheduling.
- Dijkstra's shortest path algorithm.
- Priority queues.
- Event simulation.
- Data stream processing.
- Finding largest or smallest elements efficiently.

# Creating a Heap

The `heapify()` function converts a normal list into a heap.

### Example

```python
import heapq

scores = [45, 20, 60, 10, 35]

heapq.heapify(scores)

print(scores)
```

### Output
[10, 20, 60, 45, 35]

### Explanation

`heapify()` rearranges the list so that the smallest element becomes the root.

# Important Heap Operations

| Operation | Function |
| --- | --- |
| Create Heap | `heapify()` |
| Insert Element | `heappush()` |
| Remove Minimum | `heappop()` |
| View Minimum | `heap[0]` |
| Push and Pop | `heappushpop()` |
| Replace Root | `heapreplace()` |
| Largest Elements | `nlargest()` |
| Smallest Elements | `nsmallest()` |
| Merge Heaps | `merge()` |

# Accessing Minimum Element

### Example

```python
import heapq

values = [18, 8, 40, 25]

heapq.heapify(values)

print(values[0])
```

### Output
8

### Explanation

The root element contains the smallest value.

# Inserting Elements

Use `heappush()` to add an element while maintaining heap properties.

### Example

```python
import heapq

numbers = [20, 40, 50]

heapq.heapify(numbers)

heapq.heappush(numbers, 10)

print(numbers)
```

### Output
[10, 20, 50, 40]

### Explanation

The new value is inserted and the heap is rearranged automatically.

# Removing the Smallest Element

Use `heappop()` to remove the root element.

### Example

```python
import heapq

data = [12, 30, 25, 50]

heapq.heapify(data)

smallest = heapq.heappop(data)

print(smallest)
print(data)
```

### Output
12
[25, 30, 50]

### Explanation

The smallest element is removed and the heap is adjusted.

# Push and Pop Simultaneously

`heappushpop()` inserts an element and removes the smallest element in one operation.

### Example

```python
import heapq

marks = [15, 25, 35, 45]

heapq.heapify(marks)

result = heapq.heappushpop(marks, 10)

print(result)
print(marks)
```

### Output
10
[15, 25, 35, 45]

### Explanation

10 is inserted and immediately removed because it is the smallest element.

# Replacing the Root Element

`heapreplace()` removes the smallest element and inserts a new one.

### Example

```python
import heapq

numbers = [5, 15, 25, 35]

heapq.heapify(numbers)

removed = heapq.heapreplace(numbers, 12)

print(removed)
print(numbers)
```

### Output
5
[12, 15, 25, 35]

### Explanation

5 is removed and 12 becomes part of the heap.

# Finding Largest Elements

Use `nlargest()`.

### Example

```python
import heapq

values = [90, 60, 75, 100, 45, 80]

largest = heapq.nlargest(3, values)

print(largest)
```

### Output
[100, 90, 80]

### Explanation

The three largest elements are returned.

# Finding Smallest Elements

Use `nsmallest()`.

### Example

```python
import heapq

values = [90, 60, 75, 100, 45, 80]

smallest = heapq.nsmallest(3, values)

print(smallest)
```

### Output
[45, 60, 75]

### Explanation

The three smallest values are returned.

# Using Heap as a Max Heap

Python supports min-heaps by default. To simulate a max heap, store negative values.

### Example

```python
import heapq

nums = [10, 30, 50, 20]

max_heap = [-num for num in nums]

heapq.heapify(max_heap)

print(-max_heap[0])
```

### Output
50

### Explanation

Negative values convert the min-heap into a max-heap.

# Merging Sorted Lists

Use `merge()` to combine sorted sequences.

### Example

```python
import heapq

first = [10, 20, 30]

second = [15, 25, 35]

result = list(heapq.merge(first, second))

print(result)
```

### Output
[10, 15, 20, 25, 30, 35]

### Explanation

The merged sequence remains sorted.

# Priority Queue Example

### Example

```python
import heapq

tasks = []

heapq.heappush(tasks, (2, "Mohit Chandaluri"))
heapq.heappush(tasks, (1, "Akash Dangudubiyyapu"))
heapq.heappush(tasks, (3, "Abhiram Gopisetti"))

while tasks:
    print(heapq.heappop(tasks))
```

### Output
(1, 'Akash Dangudubiyyapu')
(2, 'Mohit Chandaluri')
(3, 'Abhiram Gopisetti')

### Explanation

Tasks are processed according to priority values.

# heapreplace() vs heappushpop()

| heapreplace() | heappushpop() |
| --- | --- |
| Removes root first | Inserts first |
| New element always remains | New element may be removed |
| Useful when replacement is required | Useful for maintaining heap size |

# Advantages

1. Fast insertion and deletion.
2. Efficient priority queue implementation.
3. Memory efficient.
4. Built-in support through `heapq`.
5. Useful for graph algorithms and scheduling.

# Limitations

1. No direct access to middle elements.
2. Does not automatically sort all values.
3. Not suitable for random access operations.
4. Traversing elements is not straightforward.

# Applications

- Priority queues.
- Task scheduling.
- Event handling.
- Shortest path algorithms.
- Data streaming.
- Top-k element problems.
- CPU process scheduling.

# Common Functions

| Function | Description |
| --- | --- |
| `heapify()` | Converts list into heap |
| `heappush()` | Inserts element |
| `heappop()` | Removes smallest element |
| `heappushpop()` | Push and pop together |
| `heapreplace()` | Replace root |
| `nlargest()` | Finds largest values |
| `nsmallest()` | Finds smallest values |
| `merge()` | Merges sorted iterables |

# Summary

The `heapq` module provides an efficient way to implement heap queues and priority queues in Python. It supports insertion, deletion, replacement, merging, and finding largest or smallest elements efficiently. Heap queues are widely used in scheduling systems, graph algorithms, simulations, and many optimization problems.

