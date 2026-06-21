# PriorityQueue in Java

## Introduction

A **PriorityQueue** in Java is an unbounded queue implementation based on a priority heap data structure. It is part of the `java.util` package and inherits from the `AbstractQueue` class while implementing the `Queue` interface. Unlike standard queues that process elements in FIFO (First-In-First-Out) order, a `PriorityQueue` processes elements according to their priority. By default, it orders elements according to their natural ordering (forming a min-heap where the smallest value is at the head), but a custom `Comparator` can be provided at queue construction time to define different priorities (such as a max-heap).

Key features of the `PriorityQueue` class include:

- **Priority-Based Ordering**: Elements are sorted based on priority instead of their insertion order.
- **Unbounded Capacity**: Automatically grows in size as elements are added.
- **Binary Heap Backend**: Internally implemented as a binary heap structure, offering logarithmic time complexity $O(\log n)$ for enqueueing and dequeueing operations (`add()`, `offer()`, `poll()`, `remove()`) and constant time $O(1)$ for inspection (`peek()`, `element()`).
- **No Null Elements**: Insertion of `null` values is not permitted and throws a `NullPointerException` because elements must be compared with existing elements to determine priority.
- **Not Thread-Safe**: It is not synchronized. For thread-safe priority-based scheduling, use `PriorityBlockingQueue`.

## Basic Code Demo

The following program creates a `PriorityQueue` of integers, adds elements, and prints the highest-priority element (which is the smallest integer by default).

```java
import java.util.PriorityQueue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a Priority Queue (Min-Heap by default)
        PriorityQueue<Integer> p = new PriorityQueue<>();

        // Add elements to the queue
        p.add(3);
        p.add(10);
        p.add(7);
        p.add(2);

        // Print the head of the queue
        System.out.println("Head of Queue: " + p.peek());
    }
}
```

### Output
Head of Queue: 2

### Explanation

- A `PriorityQueue` named `p` is initialized.
- Integers `3`, `10`, `7`, and `2` are added. Because natural sorting is used, `2` has the highest priority (the smallest value) and resides at the head of the queue.
- Calling `peek()` accesses the head element without removing it, printing `2`.

## Hierarchy of PriorityQueue

The hierarchy diagram below illustrates how `PriorityQueue` inherits from the core collection classes and implements the `Queue` interface:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/priorityqueue-in-java/1782026640947-1820d3e0-0193-4e3f-bd94-5c7a1db82233.png)

## Constructors of PriorityQueue

Java provides several constructors to initialize a `PriorityQueue`:

### 1. Default Constructor: PriorityQueue()

Creates a priority queue with the default initial capacity (11) that orders its elements according to their natural ordering.

```java
PriorityQueue<String> pq = new PriorityQueue<>();
```

### 2. Capacity Constructor: PriorityQueue(int initialCapacity)

Creates a priority queue with the specified initial capacity that orders its elements according to their natural ordering.

```java
PriorityQueue<String> pq = new PriorityQueue<>(initialCapacity);
```

### 3. Comparator Constructor: PriorityQueue(Comparator&lt;? super E&gt; comparator)

Creates a priority queue with the default initial capacity (11) whose elements are ordered according to the specified custom comparator.

```java
Comparator<Integer> maxHeapComparator = (a, b) -> b - a;
PriorityQueue<Integer> pq = new PriorityQueue<>(maxHeapComparator);
```

### 4. Tuning Constructor: PriorityQueue(int initialCapacity, Comparator&lt;? super E&gt; comparator)

Creates a priority queue with the specified initial capacity that orders its elements according to the specified comparator.

```java
PriorityQueue<String> pq = new PriorityQueue<>(20, customComparator);
```

## Performing Various Operations on PriorityQueue

The following examples demonstrate common priority queue operations using simple names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`), cars (`Tesla`, `BMW`, `Audi`, `Toyota`, `Ford`), and the platform `AlphaKnowledge`.

### 1. Adding Elements

Elements are added using the `add(E e)` method. The elements are internally arranged in a binary heap.

```java
import java.util.PriorityQueue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < 3; i++) {
            pq.add(i);
            pq.add(1);
        }

        System.out.println("Queue representation: " + pq);
    }
}
```

### Output
Queue representation: [0, 1, 1, 1, 2, 1]

### Explanation

- The loop inserts numbers `0`, `1`, `1`, `1`, `2`, `1`.
- The print statement displays the queue elements. Note that the output `[0, 1, 1, 1, 2, 1]` represents the underlying binary tree (heap) layout, rather than a fully sorted list. The smallest element (`0`) resides correctly at the root (index 0).

### 2. Removing Elements

Elements are deleted using `remove(Object o)` to delete a specific item. Alternatively, `poll()` is used to retrieve and remove the head (highest-priority) element.

```java
import java.util.PriorityQueue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        PriorityQueue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        System.out.println("Initial PriorityQueue: " + pq);

        // Remove a specific element
        pq.remove("mohit");
        System.out.println("After Remove: " + pq);

        // Poll the head element
        System.out.println("Poll Method: " + pq.poll());
        System.out.println("Final PriorityQueue: " + pq);
    }
}
```

### Output
Initial PriorityQueue: [AlphaKnowledge, mohit, akash]
After Remove: [AlphaKnowledge, akash]
Poll Method: AlphaKnowledge
Final PriorityQueue: [akash]

### Explanation

- `pq.remove("mohit")` searches and deletes the string `"mohit"` from the priority queue.
- `pq.poll()` retrieves and deletes `"AlphaKnowledge"`, which is lexicographically the smallest element (highest priority), leaving only `"akash"`.

### 3. Accessing the Elements

To retrieve the highest-priority element without removing it, use the `peek()` method.

```java
import java.util.PriorityQueue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        PriorityQueue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        System.out.println("PriorityQueue: " + pq);

        // Using the peek() method
        String element = pq.peek();
        System.out.println("Accessed Element: " + element);
    }
}
```

### Output
PriorityQueue: [AlphaKnowledge, mohit, akash]
Accessed Element: AlphaKnowledge

### Explanation

- Calling `peek()` reads the root element `"AlphaKnowledge"`.
- The backing queue is left unchanged.

### 4. Iterating the PriorityQueue

Traversing a priority queue with an `Iterator` does not guarantee elements are returned in priority order. To process elements sequentially by priority, they must be polled.

```java
import java.util.PriorityQueue;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        PriorityQueue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        Iterator<String> iterator = pq.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
        System.out.println();
    }
}
```

### Output
AlphaKnowledge mohit akash

### Explanation

- The iterator traverses the underlying array, displaying elements as they reside in memory (in heap-order).

## Methods of PriorityQueue

The `PriorityQueue` class inherits methods from `Collection`, `Queue`, `AbstractQueue`, and `AbstractCollection`:

| Method | Description |
| --- | --- |
| `add(E e)` | Inserts the specified element into this priority queue. |
| `clear()` | Removes all elements from this priority queue. |
| `comparator()` | Returns the comparator used to sort elements, or `null` for natural order. |
| `contains(Object o)` | Returns `true` if this queue contains the specified element. |
| `forEach(Consumer<? super E> action)` | Performs the given action for each element. |
| `iterator()` | Returns an iterator over the elements in this queue. |
| `offer(E e)` | Inserts the specified element into this priority queue. |
| `remove(Object o)` | Removes a single instance of the specified element from this queue, if present. |
| `removeAll(Collection<?> c)` | Removes all of this collection's elements that are also contained in `c`. |
| `removeIf(Predicate<? super E> filter)` | Removes all elements that satisfy the given predicate. |
| `retainAll(Collection<?> c)` | Retains only the elements in this collection that are contained in `c`. |
| `spliterator()` | Creates a late-binding and fail-fast `Spliterator` over the elements. |
| `toArray()` | Returns an array containing all of the elements in this queue. |
| `toArray(T[] a)` | Returns an array containing all elements, utilizing the runtime type of `a`. |
| `peek()` | Retrieves, but does not remove, the head of this queue, or returns `null` if empty. |
| `poll()` | Retrieves and removes the head of this queue, or returns `null` if empty. |
| `element()` | Retrieves, but does not remove, the head of this queue. |
| `remove()` | Retrieves and removes the head of this queue. |
| `containsAll(Collection<?> c)` | Returns `true` if this collection contains all of the elements in `c`. |
| `isEmpty()` | Returns `true` if this collection contains no elements. |
| `size()` | Returns the number of elements in this collection. |
| `toString()` | Returns a string representation of this collection. |

# Summary

The Java PriorityQueue class implements the Queue interface, extending AbstractQueue and backing itself with a binary heap data structure to order elements according to natural sorting or a user-defined comparator. Offering logarithmic-time complexity $O(\log n)$ for insertion and removal operations along with constant-time $O(1)$ head inspections, it provides an efficient way to manage task prioritization. While it does not support null values to avoid comparison issues and its iterator does not guarantee elements are traversed in priority order, it remains the standard implementation for building min-heaps, max-heaps, and scheduling algorithms in Java applications.\n




