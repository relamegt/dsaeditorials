# LinkedHashSet in Java

## Introduction

A **LinkedHashSet** in Java is a hash table and doubly-linked list implementation of the `Set` interface. It is part of the `java.util` package and inherits from the `HashSet` class. While a standard `HashSet` does not guarantee any specific iteration order, a `LinkedHashSet` maintains the **insertion order** of its elements.

Key features of the `LinkedHashSet` class include:

- **Maintains Insertion Order**: Elements are traversed in the order they were inserted.
- **No Duplicates Allowed**: Stores only unique elements. Duplicate items are ignored upon insertion.
- **HashMap & LinkedList Backend**: Internally combines a `HashSet` (which is backed by a `HashMap`) with a doubly-linked list running through all of its entries to maintain insertion order.
- **Null Elements**: Allows at most one `null` element.
- **Performance**: Provides constant-time performance for basic operations like `add()`, `remove()`, and `contains()`, although slightly slower than `HashSet` due to the overhead of maintaining the linked list.
- **Not Thread-Safe**: It is not synchronized. If multiple threads access it concurrently, it must be synchronized externally using `Collections.synchronizedSet()`.

## Basic Code Demo

The following program instantiates a `LinkedHashSet` of car brands, adds elements (including a duplicate), and outputs the elements showing that insertion order is preserved.

```java
import java.util.LinkedHashSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a LinkedHashSet of car brands
        LinkedHashSet<String> cars = new LinkedHashSet<>();

        cars.add("Tesla");
        cars.add("BMW");
        cars.add("Audi");
        cars.add("Tesla"); // Duplicate element

        System.out.println("LinkedHashSet Elements: " + cars);
    }
}
```

### Output
LinkedHashSet Elements: [Tesla, BMW, Audi]

### Explanation

- A `LinkedHashSet` named `cars` is created to store strings.
- The car brands `Tesla`, `BMW`, and `Audi` are added. The second addition of `Tesla` is ignored because sets do not permit duplicates.
- The output displays the elements in the exact order they were first inserted: `[Tesla, BMW, Audi]`.

## Hierarchy of LinkedHashSet

The hierarchy diagram below illustrates how `LinkedHashSet` extends `HashSet` and implements the `Set` and `Collection` interfaces:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linkedhashset-in-java/1782025393141-ee012af6-3045-4d29-ad33-cccc02489adb.png)

## How LinkedHashSet Maintains Order

Unlike `HashSet`, which only uses a hash table, `LinkedHashSet` maintains a doubly-linked list running through all its entries. This linked list defines the iteration ordering, which is the order in which elements were inserted into the set.

- **Insertion**: When an element is added, it is placed into the hash table as usual, and also appended to the end of the doubly-linked list.
- **Re-insertion**: If an element is already present in the `LinkedHashSet` and is added again, the insertion order is not affected.
- **Removal & Re-insertion**: If an element is removed using `remove(Object o)` and then added back using `add(E e)`, it will be inserted at the end of the set, updating its position in the insertion order.

## Constructors of LinkedHashSet

Java provides four constructors to initialize a `LinkedHashSet`:

### 1. Default Constructor: LinkedHashSet()

Creates an empty set with a default initial capacity (16) and load factor (0.75).

```java
LinkedHashSet<String> set = new LinkedHashSet<>();
```

### 2. Collection Constructor: LinkedHashSet(Collection&lt;? extends E&gt; c)

Creates a set initialized with elements from the specified collection, maintaining their iteration order and filtering duplicates.

```java
LinkedHashSet<String> set = new LinkedHashSet<>(otherCollection);
```

### 3. Capacity Constructor: LinkedHashSet(int initialCapacity)

Creates an empty set with the specified initial capacity and default load factor (0.75).

```java
LinkedHashSet<String> set = new LinkedHashSet<>(32);
```

### 4. Tuning Constructor: LinkedHashSet(int initialCapacity, float loadFactor)

Creates an empty set with the specified initial capacity and load factor.

```java
LinkedHashSet<String> set = new LinkedHashSet<>(32, 0.85f);
```

## Performing Various Operations on LinkedHashSet

The following examples demonstrate common tasks using simple names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`), cars (`Tesla`, `BMW`, `Audi`, `Toyota`, `Ford`), and the platform `AlphaKnowledge`.

### 1. Adding Elements in LinkedHashSet

Elements are added using the `add(E e)` method. The iteration order is preserved.

```java
import java.util.LinkedHashSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Creating an empty LinkedHashSet
        LinkedHashSet<String> lh = new LinkedHashSet<>();

        // Adding elements to above Set
        lh.add("AlphaKnowledge");
        lh.add("mohit");
        lh.add("akash");
        lh.add("hemesh");

        System.out.println("LinkedHashSet : " + lh);
    }
}
```

### Output
LinkedHashSet : [AlphaKnowledge, mohit, akash, hemesh]

### Explanation

- A `LinkedHashSet` is initialized and several elements are added sequentially.
- The output displays the elements in the exact order of insertion: `[AlphaKnowledge, mohit, akash, hemesh]`.

### 2. Removing Elements in LinkedHashSet

Elements can be removed using the `remove(Object o)` method, which returns `true` if the element was successfully removed and `false` otherwise.

```java
import java.util.LinkedHashSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        LinkedHashSet<String> lh = new LinkedHashSet<>();

        // Adding elements
        lh.add("mohit");
        lh.add("akash");
        lh.add("hemesh");
        lh.add("abhiram");
        lh.add("hemanth");
        lh.add("AlphaKnowledge");

        System.out.println("Original LinkedHashSet: " + lh);

        // Removing the element mohit
        lh.remove("mohit");

        // Printing the updated Set
        System.out.println("After removing element: " + lh);

        // Returning false if the element is not present
        System.out.println("Removing mohit again: " + lh.remove("mohit"));
    }
}
```

### Output
Original LinkedHashSet: [mohit, akash, hemesh, abhiram, hemanth, AlphaKnowledge]
After removing element: [akash, hemesh, abhiram, hemanth, AlphaKnowledge]
Removing mohit again: false

### Explanation

- Elements are inserted, and they maintain their insertion order.
- The `remove("mohit")` method removes the element from both the internal hash table and the doubly-linked list.
- Attempting to remove `"mohit"` again returns `false` since it has already been deleted.

### 3. Iterating through the LinkedHashSet

You can iterate through the elements using an `Iterator` or the enhanced `for-each` loop.

```java
import java.util.LinkedHashSet;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        LinkedHashSet<String> lh = new LinkedHashSet<>();

        lh.add("Tesla");
        lh.add("BMW");
        lh.add("Audi");
        lh.add("Toyota");
        lh.add("Ford");

        // Iterating using Iterator
        System.out.print("Using iterator: ");
        Iterator<String> itr = lh.iterator();
        while (itr.hasNext()) {
            System.out.print(itr.next() + ", ");
        }

        System.out.println();

        // Iterating using enhanced for loop
        System.out.print("Using enhanced for loop: ");
        for (String car : lh) {
            System.out.print(car + ", ");
        }
        System.out.println();
    }
}
```

### Output
Using iterator: Tesla, BMW, Audi, Toyota, Ford, 
Using enhanced for loop: Tesla, BMW, Audi, Toyota, Ford,

### Explanation

- An iterator traverses the doubly-linked list from head to tail.
- Both methods yield the elements in their exact insertion order.

## Methods of LinkedHashSet

Since `LinkedHashSet` extends `HashSet` and implements the `Set` interface, it inherits all the standard methods of `Collection` and `Set`. It does not define any additional unique methods of its own.

| Method | Description |
| --- | --- |
| `add(E e)` | Adds the specified element to this set if not already present. |
| `addAll(Collection<? extends E> c)` | Adds all elements from the specified collection to the set. |
| `clear()` | Removes all elements from the set. |
| `contains(Object o)` | Checks if the set contains the specified element. |
| `containsAll(Collection<?> c)` | Checks if the set contains all elements from the given collection. |
| `remove(Object o)` | Removes the specified element from the set. |
| `removeAll(Collection<?> c)` | Removes all matching elements from the set. |
| `retainAll(Collection<?> c)` | Retains only elements present in both the set and the given collection. |
| `isEmpty()` | Checks if the set is empty. |
| `size()` | Returns the number of elements in the set. |
| `iterator()` | Returns an iterator over the elements in insertion order. |
| `toArray()` | Returns an array containing all elements in insertion order. |
| `spliterator()` | Creates a late-binding and fail-fast `Spliterator` over the elements. |

## Comparison: HashSet vs LinkedHashSet vs TreeSet

To understand when to use `LinkedHashSet`, it is helpful to compare it with other standard implementations of the `Set` interface:

| Feature | HashSet | LinkedHashSet | TreeSet |
| --- | --- | --- | --- |
| **Ordering** | Unordered (no guarantee of sequence). | Insertion order (maintained via doubly-linked list). | Sorted order (natural ordering or custom comparator). |
| **Underlying Structure** | Hash Table. | Hash Table + Doubly-linked list. | Red-Black Tree. |
| **Performance (Basic Ops)** | $O(1)$ constant time. | $O(1)$ constant time (slightly higher overhead than HashSet). | $O(\log n)$ logarithmic time. |
| **Null Elements** | Allows one `null` element. | Allows one `null` element. | Does not allow `null` (throws `NullPointerException`). |
| **Memory Consumption** | Low (only hash table entries). | Medium (requires additional pointers for doubly-linked list). | High (requires tree node pointers). |

# Summary

The Java LinkedHashSet class implements the Set interface, extending HashSet and using a doubly-linked list internally to preserve the insertion order of elements. By combining the quick lookup performance of a hash table with the sequential consistency of a linked list, it provides constant-time $O(1)$ operations for addition, removal, and search query tasks while ensuring predictable iteration patterns. Although it incurs slightly higher memory usage and performance overhead than a standard HashSet due to pointer maintenance, it is the collection of choice when duplicate prevention and insertion ordering are both required.




