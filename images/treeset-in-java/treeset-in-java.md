# TreeSet in Java

## Introduction

A **TreeSet** is a class in Java that implements the `Set` interface and is backed by a `TreeMap` instance (specifically a Red-Black tree structure). It is part of the `java.util` package and implements the `SortedSet` and `NavigableSet` interfaces. Elements in a `TreeSet` are stored in a sorted, ascending order, either according to their natural ordering or via a custom `Comparator` provided at set creation time.

Key features of the `TreeSet` class include:

- **Automatic Sorting**: Elements are automatically sorted in ascending order upon insertion.
- **No Duplicates Allowed**: Stores only unique elements. Duplicate items are silently ignored.
- **Red-Black Tree Backend**: Under the hood, a `TreeSet` uses a Red-Black tree structure, which guarantees $O(\log n)$ time complexity for basic operations like `add()`, `remove()`, and `contains()`.
- **No Null Elements**: Does not permit `null` elements. Attempting to add `null` will throw a `NullPointerException` because elements must be compared with existing values to determine their sorted position.
- **Navigational Capabilities**: Implements `NavigableSet`, offering methods such as `higher()`, `lower()`, `ceiling()`, and `floor()`.
- **Not Thread-Safe**: It is not synchronized. If accessed concurrently by multiple threads, it should be wrapped externally using `Collections.synchronizedSet()`.

## Basic Code Demo

The following program instantiates a `TreeSet` of integers, adds elements (including a duplicate), and outputs the elements showing that they are automatically sorted and duplicates are removed.

```java
import java.util.TreeSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Instantiate a TreeSet of integers
        TreeSet<Integer> ts = new TreeSet<>();

        ts.add(10);
        ts.add(5);
        ts.add(20);
        ts.add(10); // Duplicate element (ignored)

        System.out.println("TreeSet Elements: " + ts);
    }
}
```

### Output
TreeSet Elements: [5, 10, 20]

### Explanation

- A `TreeSet` named `ts` is created to store integers.
- The numbers `10`, `5`, and `20` are added. The second addition of `10` is ignored because sets do not permit duplicates.
- The output displays the elements in sorted ascending order: `[5, 10, 20]`.

## Hierarchy of TreeSet

The hierarchy diagram below illustrates how `TreeSet` extends the collection interfaces:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/treeset-in-java/1782025534699-9eddfe9f-246f-410c-8b62-9e91f37ff6e7.png)

## 

## Natural Ordering vs Custom Sorting

To successfully insert objects into a `TreeSet`, the objects' class must either implement the `Comparable` interface (defining a natural sorting order), or an external `Comparator` must be passed to the constructor.

- **Comparable**: String and primitive wrapper classes (such as `Integer` and `Double`) implement `Comparable` by default, facilitating natural lexicographical and numerical sorting.
- **ClassCastException**: If you attempt to add custom objects that do not implement `Comparable` without providing a custom `Comparator`, a `ClassCastException` will be thrown at runtime.

## Constructors of TreeSet

Java provides four constructors to initialize a `TreeSet`:

### 1. Default Constructor: TreeSet()

Creates an empty set that sorts elements according to their natural ordering.

```java
TreeSet<String> ts = new TreeSet<>();
```

### 2. Comparator Constructor: TreeSet(Comparator&lt;? super E&gt; comparator)

Creates an empty set that sorts elements using the specified custom comparator.

```java
TreeSet<String> ts = new TreeSet<>(customComparator);
```

*(Wait, let's make sure we use `<>` instead of `__` here. Let's fix that in content string)*

### 3. Collection Constructor: TreeSet(Collection&lt;? extends E&gt; c)

Creates a set containing all elements of the specified collection, sorted in their natural order.

```java
TreeSet<String> ts = new TreeSet<>(otherCollection);
```

### 4. SortedSet Constructor: TreeSet(SortedSet&lt;E&gt; s)

Creates a set containing the same elements and preserving the same ordering as the specified `SortedSet`.

```java
TreeSet<String> ts = new TreeSet<>(sortedSet);
```

## Performing Various Operations on TreeSet

The following examples demonstrate common tasks using simple names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`), cars (`Tesla`, `BMW`, `Audi`, `Toyota`, `Ford`), and the platform `AlphaKnowledge`.

### 1. Adding Elements

Elements are added using the `add(E e)` method. The elements are automatically sorted ascendingly.

```java
import java.util.TreeSet;
import java.util.Set;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Creating an empty TreeSet
        Set<String> ts = new TreeSet<>();

        // Adding elements
        ts.add("hemesh");
        ts.add("akash");
        ts.add("mohit");
        ts.add("AlphaKnowledge");

        System.out.println("TreeSet Elements: " + ts);
    }
}
```

### Output
TreeSet Elements: [AlphaKnowledge, akash, hemesh, mohit]

### Explanation

- A `TreeSet` of strings is initialized.
- Four strings are added. Since uppercase characters have lower ASCII values than lowercase characters in lexicographical sorting, `"AlphaKnowledge"` is sorted to the front. The output shows `[AlphaKnowledge, akash, hemesh, mohit]`.

### 2. Accessing the Elements

Elements can be queried or retrieved using navigational methods such as `contains()`, `first()`, `last()`, `higher()`, and `lower()`.

```java
import java.util.TreeSet;
import java.util.NavigableSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        NavigableSet<String> ts = new TreeSet<>();

        ts.add("hemesh");
        ts.add("akash");
        ts.add("mohit");
        ts.add("AlphaKnowledge");

        System.out.println("Tree Set is " + ts);
        String check = "akash";

        // Check if string exists
        System.out.println("Contains " + check + ": " + ts.contains(check));

        // Get first and last elements
        System.out.println("First Value: " + ts.first());
        System.out.println("Last Value: " + ts.last());

        String val = "akash";
        // Get values strictly greater and smaller than "akash"
        System.out.println("Higher than " + val + ": " + ts.higher(val));
        System.out.println("Lower than " + val + ": " + ts.lower(val));
    }
}
```

### Output
Tree Set is [AlphaKnowledge, akash, hemesh, mohit]
Contains akash: true
First Value: AlphaKnowledge
Last Value: mohit
Higher than akash: hemesh
Lower than akash: AlphaKnowledge

### Explanation

- The program initializes a navigable tree set.
- `first()` retrieves the smallest element, and `last()` retrieves the largest.
- `higher("akash")` yields `"hemesh"` (the next greatest element), while `lower("akash")` returns `"AlphaKnowledge"` (the next smallest element).

### 3. Removing the Values

Elements can be deleted using `remove()`, or retrieved and removed from the ends using `pollFirst()` and `pollLast()`.

```java
import java.util.TreeSet;
import java.util.NavigableSet;

public class AlphaKnowledge {
    public static void main(String[] args) {
        NavigableSet<String> ts = new TreeSet<>();

        // Adding elements
        ts.add("mohit");
        ts.add("akash");
        ts.add("hemesh");
        ts.add("abhiram");
        ts.add("hemanth");
        ts.add("AlphaKnowledge");

        System.out.println("Initial TreeSet: " + ts);

        // Removing a specific element
        ts.remove("hemanth");
        System.out.println("After removing hemanth: " + ts);

        // Removing first element
        ts.pollFirst();
        System.out.println("After pollFirst: " + ts);

        // Removing last element
        ts.pollLast();
        System.out.println("After pollLast: " + ts);
    }
}
```

### Output
Initial TreeSet: [AlphaKnowledge, abhiram, akash, hemesh, hemanth, mohit]
After removing hemanth: [AlphaKnowledge, abhiram, akash, hemesh, mohit]
After pollFirst: [abhiram, akash, hemesh, mohit]
After pollLast: [abhiram, akash, hemesh]

### Explanation

- `remove("hemanth")` deletes the element.
- `pollFirst()` removes and returns `"AlphaKnowledge"` (the lowest element).
- `pollLast()` removes and returns `"mohit"` (the highest element).

### 4. Iterating the TreeSet

You can iterate through a `TreeSet` in sorted order using an enhanced `for` loop.

```java
import java.util.TreeSet;
import java.util.Set;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Set<String> ts = new TreeSet<>();

        ts.add("mohit");
        ts.add("akash");
        ts.add("hemesh");
        ts.add("abhiram");
        ts.add("hemanth");
        ts.add("AlphaKnowledge");

        for (String value : ts) {
            System.out.print(value + ", ");
        }
        System.out.println();
    }
}
```

### Output
AlphaKnowledge, abhiram, akash, hemesh, hemanth, mohit,

### Explanation

- The enhanced `for` loop traverses the Red-Black tree in-order, outputting elements in sorted order.

### 5. Using TreeSet with Custom Objects

When sorting objects of classes that do not implement `Comparable` (such as `StringBuffer`), a custom `Comparator` must be supplied to the constructor to define the sorting criteria.

```java
import java.util.TreeSet;
import java.util.Comparator;
import java.util.Set;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Creating a TreeSet with a custom Comparator for StringBuffer
        Set<StringBuffer> ts = new TreeSet<>(new Comparator<StringBuffer>() {
            @Override
            public int compare(StringBuffer sb1, StringBuffer sb2) {
                return sb1.toString().compareTo(sb2.toString());
            }
        });

        // Adding elements using StringBuffer
        ts.add(new StringBuffer("Tesla"));
        ts.add(new StringBuffer("BMW"));
        ts.add(new StringBuffer("Audi"));
        ts.add(new StringBuffer("Toyota"));
        ts.add(new StringBuffer("Ford"));

        System.out.println("Sorted via Custom Comparator: " + ts);
    }
}
```

### Output
Sorted via Custom Comparator: [Audi, BMW, Ford, Tesla, Toyota]

### Explanation

- Since `StringBuffer` does not implement `Comparable`, we define an anonymous custom `Comparator` to sort lexicographically by converting `StringBuffer` to `String`.
- The output contains the car brands sorted in ascending lexicographical order.

## Methods of TreeSet

Since `TreeSet` implements the `NavigableSet` and `SortedSet` interfaces, it supports a wide variety of retrieval and range query APIs:

| Method | Description |
| --- | --- |
| `add(E e)` | Adds the specified element to this set if not already present. |
| `addAll(Collection<? extends E> c)` | Adds all elements from the specified collection to the set. |
| `ceiling(E e)` | Returns the least element in this set greater than or equal to the given element, or `null`. |
| `clear()` | Removes all elements from the set. |
| `clone()` | Returns a shallow copy of this `TreeSet` instance. |
| `comparator()` | Returns the `Comparator` used to sort this set, or `null` if it uses natural ordering. |
| `contains(Object o)` | Returns `true` if the set contains the specified element. |
| `descendingIterator()` | Returns an iterator over the elements in this set in descending order. |
| `descendingSet()` | Returns a reverse-order view of the elements contained in this set. |
| `first()` | Returns the first (lowest) element currently in this set. |
| `floor(E e)` | Returns the greatest element in this set less than or equal to the given element, or `null`. |
| `headSet(E toElement)` | Returns a view of the portion of this set whose elements are strictly less than `toElement`. |
| `higher(E e)` | Returns the least element in this set strictly greater than the given element, or `null`. |
| `isEmpty()` | Returns `true` if the set contains zero elements. |
| `iterator()` | Returns an iterator over the elements in this set in ascending order. |
| `last()` | Returns the last (highest) element currently in this set. |
| `lower(E e)` | Returns the greatest element in this set strictly less than the given element, or `null`. |
| `pollFirst()` | Retrieves and removes the first (lowest) element, or returns `null` if this set is empty. |
| `pollLast()` | Retrieves and removes the last (highest) element, or returns `null` if this set is empty. |
| `remove(Object o)` | Removes the specified element from this set if present. |
| `size()` | Returns the number of elements in this set. |
| `spliterator()` | Creates a late-binding and fail-fast `Spliterator` over the elements. |
| `subSet(E fromElement, E toElement)` | Returns a view of the portion of this set ranging from `fromElement` (inclusive) to `toElement` (exclusive). |
| `tailSet(E fromElement)` | Returns a view of the portion of this set whose elements are greater than or equal to `fromElement`. |

# Summary

The Java TreeSet class implements the NavigableSet interface, inheriting from SortedSet and utilizing a Red-Black tree internally to store unique elements in automatic sorted order. Supported by dynamic sorting capabilities through natural ordering or custom comparators, it provides logarithmic-time $O(\log n)$ performance for key operations such as addition, deletion, and containment verification. While it does not permit null values to avoid comparison conflicts and is not synchronized by default, its rich navigational APIs like higher, floor, first, and last make it the standard collection for ordered set operations in Java applications.




