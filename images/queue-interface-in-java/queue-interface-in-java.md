# Queue Interface In Java

## Introduction

The **Queue** interface in Java is a member of the Java Collections Framework and is located in the `java.util` package. Extending the core `Collection` interface, it represents a linear structure designed for holding elements prior to processing. Typically, elements in a queue are processed according to a specific ordering, most commonly **FIFO (First-In-First-Out)**.

Key features of the `Queue` interface include:

- **Ordering Semantics**: While standard queues follow FIFO ordering (e.g., `LinkedList` and `ArrayDeque`), priority queues order elements based on natural sorting or a custom comparator.
- **No Direct Indexed Access**: Elements cannot be retrieved by index like lists. Instead, operations focus on the head (front) and tail (rear) of the queue.
- **Duplicate Support**: Standard implementations of the `Queue` interface allow storing duplicate elements.
- **Instantiation**: Since `Queue` is an interface, it cannot be instantiated directly. Instead, concrete implementations like `LinkedList`, `ArrayDeque`, or `PriorityQueue` must be used.

## Basic Code Demo

The following program creates a `PriorityQueue` of integers, inserts elements, and prints the queue. It demonstrates that elements are ordered based on priority (natural ascending order by default) rather than insertion order.

```java
import java.util.PriorityQueue;
import java.util.Queue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a PriorityQueue of Integers
        Queue<Integer> pq = new PriorityQueue<>();

        // Adding elements to the PriorityQueue
        pq.add(50);
        pq.add(20);
        pq.add(40);
        pq.add(10);
        pq.add(30);

        // Display the PriorityQueue elements
        System.out.println("PriorityQueue elements: " + pq);
    }
}
```

### Output
PriorityQueue elements: [10, 20, 40, 50, 30]

### Explanation

- A `PriorityQueue` of integers is created and elements are added.
- Although the elements are inserted in the order `50, 20, 40, 10, 30`, the output shows them arranged in their binary heap representation where the head of the queue (`10`) is the smallest element.
- When traversing or polling, elements are returned in ascending order.

## Hierarchy of Queue Interface

The hierarchy diagram below shows how the `Queue` interface fits within the Java Collections Framework and is implemented by concrete classes:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/queue-interface-in-java/1782026410986-3ac5cd09-122e-495e-bfc5-abf12f3c2b67.png)

## Common Implementations of Queue Interface

The Java Collections Framework offers several standard implementations of the `Queue` interface:

- **LinkedList**: Implements both `List` and `Deque` interfaces. It allows `null` elements and behaves as a standard FIFO queue when referenced via the `Queue` interface.
- **ArrayDeque**: A resizable array-backed double-ended queue. It performs faster than `LinkedList` for queue operations and does not permit `null` values.
- **PriorityQueue**: A heap-backed priority queue that processes elements according to natural order or custom sorting. It does not allow `null` values.
- **ConcurrentLinkedQueue**: A thread-safe, lock-free, non-blocking queue implementation designed for high-concurrency environments.
- **BlockingQueue**: A sub-interface of `Queue` supporting operations that wait for the queue to become non-empty when retrieving an element, or wait for space to become available when storing an element.

## Performing Various Operations on Queue

The following examples demonstrate common queue tasks using the `PriorityQueue` implementation and elements such as names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and the platform `AlphaKnowledge`.

### 1. Adding Elements

Elements can be added using the `add(E e)` method. Duplicate elements are permitted.

```java
import java.util.PriorityQueue;
import java.util.Queue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Queue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        System.out.println("Queue: " + pq);
    }
}
```

### Output
Queue: [AlphaKnowledge, mohit, akash]

### Explanation

- A `PriorityQueue` of strings is initialized.
- Three strings are added. Lexicographical ordering determines their internal positions, sorting `"AlphaKnowledge"` to the head.

### 2. Removing Elements

Elements are deleted using `remove(Object o)`, which deletes the first occurrence of the element. Alternatively, `poll()` is used to retrieve and remove the head of the queue.

```java
import java.util.PriorityQueue;
import java.util.Queue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Queue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        System.out.println("Initial Queue: " + pq);

        // Remove specific element
        pq.remove("mohit");
        System.out.println("After Remove: " + pq);

        // Retrieve and remove head
        System.out.println("Poll Method: " + pq.poll());
        System.out.println("Final Queue: " + pq);
    }
}
```

### Output
Initial Queue: [AlphaKnowledge, mohit, akash]
After Remove: [AlphaKnowledge, akash]
Poll Method: AlphaKnowledge
Final Queue: [akash]

### Explanation

- `"mohit"` is removed from the queue using `remove()`.
- `poll()` removes and returns the head element `"AlphaKnowledge"`, leaving only `"akash"`.

### 3. Accessing Elements

You can view the head element without removing it by calling `peek()` or `element()`.

```java
import java.util.PriorityQueue;
import java.util.Queue;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Queue<String> pq = new PriorityQueue<>();

        pq.add("mohit");
        pq.add("akash");
        pq.add("AlphaKnowledge");

        // Accessing the head element
        System.out.println("Head using peek(): " + pq.peek());      
        System.out.println("Head using element(): " + pq.element()); 

        System.out.println("Queue after accessing: " + pq);
    }
}
```

### Output
Head using peek(): AlphaKnowledge
Head using element(): AlphaKnowledge
Queue after accessing: [AlphaKnowledge, mohit, akash]

### Explanation

- Both `peek()` and `element()` return `"AlphaKnowledge"` (the current head).
- The print statement confirms that the element remains in the queue.

### 4. Iterating the Queue

The elements of a queue can be traversed using a type-safe `Iterator`.

```java
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Queue<String> pq = new PriorityQueue<>();

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

- The iterator traverses the backing structure, retrieving and displaying elements sequentially.

## Methods of Queue Interface

The `Queue` interface defines methods that either throw an exception or return a special value (like `null` or `false`) if an operation fails:

| Operation | Throws Exception | Returns Special Value |
| --- | --- | --- |
| **Insert** | `add(e)` | `offer(e)` |
| **Remove** | `remove()` | `poll()` |
| **Examine** | `element()` | `peek()` |

Below is a lookup table describing the core methods of `Queue` and its sub-interfaces:

| Method | Description |
| --- | --- |
| `add(E e)` | Inserts the specified element; throws `IllegalStateException` if insertion fails. |
| `offer(E e)` | Inserts the specified element; returns `false` if insertion fails. |
| `remove()` | Removes and returns the head of the queue; throws `NoSuchElementException` if empty. |
| `poll()` | Removes and returns the head; returns `null` if empty. |
| `element()` | Retrieves, but does not remove, the head; throws `NoSuchElementException` if empty. |
| `peek()` | Retrieves, but does not remove, the head; returns `null` if empty. |
| `size()` | Returns the number of elements in the queue. |
| `isEmpty()` | Returns `true` if the queue contains no elements. |
| `contains(Object o)` | Returns `true` if the queue contains the specified element. |
| `iterator()` | Returns an iterator over the elements in the queue. |
| `toArray()` | Converts the queue elements into an array. |
| `addFirst(E e)` | Inserts element at the front (Deque only). |
| `addLast(E e)` | Inserts element at the end (Deque only). |
| `offerFirst(E e)` | Inserts element at the front; returns `false` if fails (Deque only). |
| `offerLast(E e)` | Inserts element at the end; returns `false` if fails (Deque only). |
| `removeFirst()` | Removes and returns the first element (Deque only). |
| `removeLast()` | Removes and returns the last element (Deque only). |
| `pollFirst()` | Removes and returns the first element; returns `null` if empty (Deque only). |
| `pollLast()` | Removes and returns the last element; returns `null` if empty (Deque only). |
| `getFirst()` | Retrieves, but does not remove, the first element (Deque only). |
| `getLast()` | Retrieves, but does not remove, the last element (Deque only). |
| `peekFirst()` | Retrieves, but does not remove, the first element; returns `null` if empty (Deque only). |
| `peekLast()` | Retrieves, but does not remove, the last element; returns `null` if empty (Deque only). |
| `put(E e)` | Inserts element, waiting if necessary (BlockingQueue only). |
| `take()` | Removes and returns head element, waiting if empty (BlockingQueue only). |

# Summary

The Java Queue interface extends the Collection interface to represent a container designed for holding elements prior to processing in a structured order. Standard implementations like LinkedList, ArrayDeque, and PriorityQueue offer diverse behaviors ranging from traditional first-in-first-out sequencing to heap-based priority sorting. While it does not support indexed element access and limits concurrent operations unless explicitly synchronized or managed via BlockingQueue constructs, its distinct dual-api design (throwing exceptions versus returning special values for boundary operations) makes it a versatile tool for implementing buffers, producer-consumer pipelines, and scheduling tasks in Java systems.




