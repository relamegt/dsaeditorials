# LinkedList in Java

## Introduction

A **LinkedList** in Java is a linear data structure implemented within the Java Collections Framework (JCF) under the `java.util` package. Unlike standard arrays or `ArrayList`, which store elements in contiguous blocks of memory, a `LinkedList` stores its elements as independent objects called **Nodes**. 

Internally, it is implemented as a **Doubly-Linked List**. Each Node consists of three parts:

1. **Data**: The actual value or reference to the object stored.
2. **Previous Pointer**: A reference pointing to the preceding node in the list.
3. **Next Pointer**: A reference pointing to the subsequent node in the list.

Key characteristics of the `LinkedList` class include:

- **Dynamic Sizing**: The size of a `LinkedList` grows and shrinks dynamically at runtime without requiring re-allocation or copying of a backing array.
- **Preserves Insertion Order**: Retains the sequential order in which elements are inserted.
- **Permits Duplicates**: Allows multiple occurrences of identical elements.
- **Not Thread-Safe**: By default, `LinkedList` is not synchronized. It can be wrapped for thread safety using `Collections.synchronizedList()`.
- **Fast Insert/Delete Performance**: Inserting or deleting elements at arbitrary positions (especially the beginning or end) only requires updating node pointers, performing in $O(1)$ constant time once the position is located.

## Basic Code Demo

The following program demonstrates how to create a basic `LinkedList` of cars, append elements, and print the list.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // Creating a LinkedList of cars
        LinkedList<String> cars = new LinkedList<>();

        // Adding elements to the LinkedList using add() method
        cars.add("Tesla");
        cars.add("BMW");
        cars.add("Audi");
        cars.add("Toyota");
        cars.add("Ford");

        System.out.println(cars);
    }
}
```

### Output
[Tesla, BMW, Audi, Toyota, Ford]

### Explanation

- A `LinkedList` of type `String` representing car brands is initialized.
- Five elements (`"Tesla"` to `"Ford"`) are appended to the list using the `.add()` method.
- The list maintains their insertion order and prints them as a formatted string representation: `[Tesla, BMW, Audi, Toyota, Ford]`.
- Note: LinkedList nodes cannot be accessed directly by index in $O(1)$ time; elements must be accessed by traversing from the head or tail to the target index, taking $O(n)$ time.

## Hierarchy of LinkedList

The `LinkedList` class implements both the `List` and `Deque` (Double-Ended Queue) interfaces:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linkedlist-in-java/1782022020669-b2e7ddca-fc16-4039-93b5-34b40473e16f.png)

By implementing `Deque`, a `LinkedList` can also be used as a Stack (LIFO) or a Queue (FIFO), providing standard double-ended queue operations.

## Constructors of LinkedList

The `LinkedList` class provides two standard constructors:

### 1. Default Constructor: LinkedList()

Creates an empty linked list.

```java
LinkedList<String> list = new LinkedList<>();
```

### 2. Collection Constructor: LinkedList(Collection&lt;? extends E&gt; c)

Creates an ordered linked list initialized with elements from the specified collection, in the order they are returned by the collection's iterator.

```java
LinkedList<String> list = new LinkedList__(otherCollection);
```

## Performing Different Operations on LinkedList

The following sections illustrate frequently used operations on a `LinkedList` using the simple names `mohit`, `akash`, `hemesh`, and `abhiram`.

### 1. Adding Elements

You can append elements to the end of the list using `add(E element)` or insert them at a specific index using `add(int index, E element)`.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        list.add("mohit");
        list.add("hemesh");
        list.add(1, "akash");

        System.out.println(list);
    }
}
```

### Output
[mohit, akash, hemesh]

### Explanation

- The list is initialized. Two elements (`"mohit"` and `"hemesh"`) are added sequentially.
- `list.add(1, "akash")` inserts the name `"akash"` at index `1`, updating node references so that `"mohit"` points to `"akash"`, and `"akash"` points to `"hemesh"`.

### 2. Updating Elements

Elements are updated by replacing an existing element at a specific index using the `set(int index, E element)` method.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        list.add("mohit");
        list.add("abhiram");
        list.add(1, "mohit");

        System.out.println("Initial LinkedList " + list);

        list.set(1, "akash");

        System.out.println("Updated LinkedList " + list);
    }
}
```

### Output
Initial LinkedList [mohit, mohit, abhiram]
Updated LinkedList [mohit, akash, abhiram]

### Explanation

- The list is initially populated with `"mohit"`, `"mohit"`, and `"abhiram"`.
- `list.set(1, "akash")` locates the node at index `1` and updates its internal data payload to `"akash"`.

### 3. Removing Elements

You can remove elements from a linked list by index using `remove(int index)` or by value match using `remove(Object o)`.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        list.add("mohit");
        list.add("hemesh");
        list.add(1, "akash");

        System.out.println("Initial LinkedList " + list);

        // Remove element present at index 1
        list.remove(1);
        System.out.println("After the Index Removal " + list);

        // Remove the first occurrence of the object "mohit"
        list.remove("mohit");
        System.out.println("After the Object Removal " + list);
    }
}
```

### Output
Initial LinkedList [mohit, akash, hemesh]
After the Index Removal [mohit, hemesh]
After the Object Removal [hemesh]

### Explanation

- The list starts as `[mohit, akash, hemesh]`.
- `list.remove(1)` removes `"akash"` by updating adjacent node references to point to each other directly, bypassing the removed node.
- `list.remove("mohit")` searches sequentially from the head and removes the first node containing `"mohit"`, leaving only `"hemesh"`.

### 4. Iterating a LinkedList

Traversing a linked list can be performed using index loops or enhanced loops.

> *!WARNING:* Using `get(i)` inside a standard index loop is an **anti-pattern** for LinkedList. Because a linked list does not support index indexing, each `get(i)` call must traverse the list from the head, resulting in $O(n^2)$ time complexity for large lists. Always use an enhanced `for-each` loop or an `Iterator` for traversal, which performs in $O(n)$ time.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        list.add("mohit");
        list.add("hemesh");
        list.add(1, "akash");

        // Basic for loop with get(index) - O(n^2) warning
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + " ");
        }

        System.out.println();

        // Enhanced for-each loop (Recommended - O(n))
        for (String name : list) {
            System.out.print(name + " ");
        }
    }
}
```

### Output
mohit akash hemesh 
mohit akash hemesh

### Explanation

- The first loop accesses elements via `.get(i)`. For small collections, this is acceptable, but for large collections, it causes performance bottlenecks.
- The second loop uses the enhanced `for-each` loop, which uses the list's internal iterator to traverse node connections sequentially, maintaining $O(n)$ time complexity.

## Real-World Usage of LinkedList

- **Queue & Deque Implementations**: Since `LinkedList` implements the `Queue` and `Deque` interfaces, it is ideal for First-In-First-Out (FIFO) buffers or double-ended queuing (e.g., job scheduling, message queues).
- **Undo / Redo Buffers**: Software applications (like text editors) store history as nodes in a linked list structure. Inserting or removing the latest changes at the tail is extremely fast and dynamic.
- **Browser History**: Forward and backward navigation history can be managed using a doubly-linked list, where the active page is a node and clicking back/forward updates the active node pointer.

## Methods for Java LinkedList

Below is a lookup table of the most common methods available in the `LinkedList` class:

| Method | Description |
| --- | --- |
| `add(int index, E element)` | Inserts the specified element at the specified index. |
| `add(E e)` | Appends the specified element to the end of this list. |
| `addAll(int index, Collection<? extends E> c)` | Inserts all elements of the collection starting at the specified index. |
| `addAll(Collection<? extends E> c)` | Appends all elements of the collection to the end of the list. |
| `addFirst(E e)` | Inserts the specified element at the beginning of this list. |
| `addLast(E e)` | Appends the specified element to the end of this list. |
| `clear()` | Removes all of the elements from this list. |
| `clone()` | Returns a shallow copy of this `LinkedList`. |
| `contains(Object o)` | Returns `true` if this list contains the specified element. |
| `descendingIterator()` | Returns an iterator over the elements in this deque in reverse sequential order. |
| `element()` | Retrieves, but does not remove, the head (first element) of this list. |
| `get(int index)` | Returns the element at the specified position in this list. |
| `getFirst()` | Returns the first element in this list. |
| `getLast()` | Returns the last element in this list. |
| `indexOf(Object o)` | Returns the index of the first occurrence of the specified element, or `-1`. |
| `lastIndexOf(Object o)` | Returns the index of the last occurrence of the specified element, or `-1`. |
| `listIterator(int index)` | Returns a list-iterator over the elements starting at the specified index. |
| `offer(E e)` | Adds the specified element as the tail (last element) of this list. |
| `offerFirst(E e)` | Inserts the specified element at the front of this list. |
| `offerLast(E e)` | Inserts the specified element at the end of this list. |
| `peek()` | Retrieves, but does not remove, the head (first element) of this list. |
| `peekFirst()` | Retrieves, but does not remove, the first element of this list, or returns `null` if empty. |
| `peekLast()` | Retrieves, but does not remove, the last element of this list, or returns `null` if empty. |
| `poll()` | Retrieves and removes the head (first element) of this list. |
| `pollFirst()` | Retrieves and removes the first element of this list, or returns `null` if empty. |
| `pollLast()` | Retrieves and removes the last element of this list, or returns `null` if empty. |
| `pop()` | Pops an element from the stack represented by this list. |
| `push(E e)` | Pushes an element onto the stack represented by this list. |
| `remove()` | Retrieves and removes the head (first element) of this list. |
| `remove(int index)` | Removes the element at the specified position in this list. |
| `remove(Object o)` | Removes the first occurrence of the specified element from this list, if present. |
| `removeFirst()` | Removes and returns the first element from this list. |
| `removeFirstOccurrence(Object o)` | Removes the first occurrence of the specified element in this list. |
| `removeLast()` | Removes and returns the last element from this list. |
| `removeLastOccurrence(Object o)` | Removes the last occurrence of the specified element in this list. |
| `set(int index, E element)` | Replaces the element at the specified position in this list with the specified element. |
| `size()` | Returns the number of elements in this list. |
| `spliterator()` | Creates a late-binding and fail-fast `Spliterator` over the elements in this list. |
| `toArray()` | Returns an array containing all of the elements in this list in proper sequence. |
| `toArray(T[] a)` | Returns an array containing all of the elements in this list in proper sequence of the specified array type. |
| `toString()` | Returns the string representation of this list. |

## ArrayList vs LinkedList

The key differences between `ArrayList` and `LinkedList` are summarized below:

| Feature | ArrayList | LinkedList |
| --- | --- | --- |
| **Underlying Structure** | Dynamic Array (contiguous memory). | Doubly-Linked List (node connections). |
| **Random Access** | Fast. $O(1)$ time complexity using indices. | Slow. $O(n)$ time complexity as it must traverse nodes. |
| **Memory Overhead** | Lower. Only stores data elements (though there may be unused array slots). | Higher. Stores data along with previous and next node pointers. |
| **Iteration Speed** | Faster due to memory locality and array storage. | Slower because node connections are scattered in memory. |
| **Insertion & Deletion** | Slower. Requires element shifting ($O(n)$ complexity) if not done at the end. | Faster. Once located, inserting/deleting is an $O(1)$ pointer update. |
| **Cache Efficiency** | Cache-friendly. Contiguous memory allocation utilizes CPU caches. | Poor cache efficiency. Nodes are scattered in heap memory, causing cache misses. |

# Summary

The Java LinkedList is a doubly-linked node list implementation of the List and Deque interfaces, storing data in non-contiguous heap positions linked by preceding and succeeding pointer references. This architecture allows dynamic sizing and $O(1)$ insertions or removals without array copying, making it highly efficient for queue buffers, browser history, and undo operations. However, this pointer-heavy structure has higher memory overhead, lacks random indexing access, and has lower iteration performance compared to ArrayList. Understanding these architectural trade-offs is essential for selecting the correct list implementation for Java applications.




