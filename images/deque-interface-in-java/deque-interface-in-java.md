# Deque Interface in Java

## Introduction

The **Deque** (Double-Ended Queue) interface in Java is a member of the Java Collections Framework and is located in the `java.util` package. Extending the `Queue` interface, a `Deque` represents a linear collection that supports the insertion, removal, and retrieval of elements from both ends. The name "Deque" is short for "Double-Ended Queue" and is typically pronounced as "deck."

Key features of the `Deque` interface include:

- **Bi-directional Operations**: Elements can be added, inspected, and removed from both the front (head) and the rear (tail).
- **Dual Functionality**: It can be used as a FIFO (First-In-First-Out) queue or as a LIFO (Last-In-First-Out) stack.
- **Common Implementations**: Standard implementations include `ArrayDeque` (resizable array-backed) and `LinkedList` (doubly-linked list).
- **No Direct Indexed Access**: Elements cannot be directly accessed by index, unlike standard list collections.

## Basic Code Demo

The following program creates a `Deque` using `ArrayDeque`, inserts elements at both ends, removes them, and prints the result.

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a Deque of Strings
        Deque<String> d = new ArrayDeque<>();

        // Add elements to both ends
        d.addFirst("Tesla");
        d.addLast("BMW");

        // Remove elements from both ends
        String f = d.removeFirst();
        String l = d.removeLast();

        // Displaying the Deque
        System.out.println("First: " + f + ", Last: " + l);
    }
}
```

### Output
First: Tesla, Last: BMW

### Explanation

- A deque instance `d` is instantiated using the `ArrayDeque` implementation.
- `"Tesla"` is added to the front using `addFirst()`, and `"BMW"` is added to the tail using `addLast()`.
- `removeFirst()` retrieves and removes `"Tesla"`, while `removeLast()` retrieves and removes `"BMW"`.
- The print statement displays `First: Tesla, Last: BMW`.

## Hierarchy of Deque Interface

The hierarchy diagram below shows how the `Deque` interface extends `Queue` and is implemented by classes like `ArrayDeque` and `LinkedList`:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/deque-interface-in-java/1782026998127-6e6984d3-7552-49f4-b3b6-c15857048b1e.png)

## Common Implementation Classes

The three most frequently used implementations of the `Deque` interface are:

- **ArrayDeque**: A resizable array implementation. It is highly efficient for head/tail insertions and removals and is generally faster than `Stack` and `LinkedList`. It does not allow `null` values.
- **LinkedList**: A doubly-linked list implementation. It allows `null` elements and is ideal when pointer-based sequential insertions and removals are needed.
- **ConcurrentLinkedDeque**: A thread-safe, lock-free, concurrent double-ended queue based on linked nodes.

## Performing Various Operations on Deque

The following examples demonstrate common deque tasks using the `ArrayDeque` implementation and elements such as names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and the platform `AlphaKnowledge`.

### 1. Adding Elements

Elements can be added using `add()`, `addFirst()`, or `addLast()`, allowing insertions at either the head or tail.

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Initializing a deque
        Deque<String> dq = new ArrayDeque<>();

        // add methods to insert elements
        dq.add("mohit");            // Adds at tail
        dq.addFirst("AlphaKnowledge"); // Adds at head
        dq.addLast("akash");        // Adds at tail

        System.out.println("Deque Elements: " + dq);
    }
}
```

### Output
Deque Elements: [AlphaKnowledge, mohit, akash]

### Explanation

- An `ArrayDeque` is initialized.
- `"mohit"` is added (default tail insertion), then `"AlphaKnowledge"` is inserted at the front, and finally `"akash"` is inserted at the tail.
- The output displays the elements in double-ended insertion order: `[AlphaKnowledge, mohit, akash]`.

### 2. Removing Elements

Elements can be removed from either end using `removeFirst()`, `removeLast()`, `pop()`, or `poll()` methods.

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Initializing a deque
        Deque<String> dq = new ArrayDeque<>();

        // Adding elements
        dq.add("mohit");
        dq.addFirst("AlphaKnowledge");
        dq.addLast("akash");

        System.out.println("Initial Deque: " + dq);

        // Remove elements using different methods
        System.out.println("Popped (from head): " + dq.pop());
        System.out.println("Polled (from head): " + dq.poll());
        System.out.println("Polled First (from head): " + dq.pollFirst());
        System.out.println("Polled Last (from tail): " + dq.pollLast());
    }
}
```

### Output
Initial Deque: [AlphaKnowledge, mohit, akash]
Popped (from head): AlphaKnowledge
Polled (from head): mohit
Polled First (from head): akash
Polled Last (from tail): null

### Explanation

- `"AlphaKnowledge"` (current head) is popped using `pop()`.
- `"mohit"` (new head) is retrieved and removed using `poll()`.
- `"akash"` (remaining element at head) is removed via `pollFirst()`.
- A final call to `pollLast()` returns `null` because the deque is now empty.

### 3. Iterating through the Deque

A deque can be traversed from head to tail using a standard `iterator()`, or in reverse order (tail to head) using a `descendingIterator()`.

```java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Initialize Deque
        Deque<String> dq = new ArrayDeque<>();
        dq.add("mohit");
        dq.addFirst("AlphaKnowledge");
        dq.addLast("akash");
        dq.add("hemesh");

        // Type-safe forward iteration
        System.out.print("Forward Iteration: ");
        for (Iterator<String> itr = dq.iterator(); itr.hasNext();) {
            System.out.print(itr.next() + " ");
        }
        System.out.println();

        // Type-safe reverse iteration
        System.out.print("Reverse Iteration: ");
        for (Iterator<String> itr = dq.descendingIterator(); itr.hasNext();) {
            System.out.print(itr.next() + " ");
        }
        System.out.println();
    }
}
```

### Output
Forward Iteration: AlphaKnowledge mohit akash hemesh 
Reverse Iteration: hemesh akash mohit AlphaKnowledge

### Explanation

- Forward iteration prints the deque elements starting from the head down to the tail.
- Reverse iteration uses `descendingIterator()` to print elements starting from the tail up to the head.

## Methods of Deque Interface

The `Deque` interface offers two sets of methods for adding, removing, and inspecting elements. One set throws an exception if the operation fails, while the other returns a special value (such as `null` or `false`):

| Operation | Throws Exception (First End) | Returns Special Value (First End) | Throws Exception (Last End) | Returns Special Value (Last End) |
| --- | --- | --- | --- | --- |
| **Insert** | `addFirst(e)` | `offerFirst(e)` | `addLast(e)` | `offerLast(e)` |
| **Remove** | `removeFirst()` | `pollFirst()` | `removeLast()` | `pollLast()` |
| **Examine** | `getFirst()` | `peekFirst()` | `getLast()` | `peekLast()` |

Below is a lookup table describing the core methods of the `Deque` interface:

| Method | Description |
| --- | --- |
| `addFirst(E e)` | Inserts the specified element at the front (head) of this deque. |
| `addLast(E e)` | Inserts the specified element at the end (tail) of this deque. |
| `offerFirst(E e)` | Inserts the specified element at the front; returns `false` if insertion fails. |
| `offerLast(E e)` | Inserts the specified element at the end; returns `false` if insertion fails. |
| `add(E e)` | Adds the specified element at the tail of this deque. |
| `offer(E e)` | Adds the specified element at the tail; returns `false` if insertion fails. |
| `removeFirst()` | Removes and returns the first element; throws `NoSuchElementException` if empty. |
| `removeLast()` | Removes and returns the last element; throws `NoSuchElementException` if empty. |
| `pollFirst()` | Removes and returns the first element; returns `null` if empty. |
| `pollLast()` | Removes and returns the last element; returns `null` if empty. |
| `poll()` | Removes and returns the head element; returns `null` if empty. |
| `getFirst()` | Retrieves, but does not remove, the first element; throws exception if empty. |
| `getLast()` | Retrieves, but does not remove, the last element; throws exception if empty. |
| `peekFirst()` | Retrieves, but does not remove, the first element; returns `null` if empty. |
| `peekLast()` | Retrieves, but does not remove, the last element; returns `null` if empty. |
| `peek()` | Retrieves, but does not remove, the head element; returns `null` if empty. |
| `push(E e)` | Pushes an element onto the stack represented by this deque (inserts at the head). |
| `pop()` | Pops an element from the stack represented by this deque (removes from the head). |

# Summary

The Java Deque interface extends the Queue interface to define a double-ended queue, supporting efficient element insertion, retrieval, and deletion from both the front and rear endpoints. Frequently implemented by ArrayDeque and LinkedList classes, it serves as a highly versatile structure that can be operated as a first-in-first-out queue or a last-in-first-out stack. While it incurs slight performance and memory differences depending on whether it relies on dynamic array resizing or linked-node traversal, its comprehensive method contract and support for bi-directional iterators make it an essential tool for implementing sliding windows, double-ended buffers, and history logs in Java programs.




