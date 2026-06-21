# List Interface in Java

## Introduction

The **List Interface** in Java extends the root `Collection` interface and is a core component of the `java.util` package. It represents an ordered sequence of elements, often referred to as a sequence. The `List` interface gives developers precise control over where each element is inserted in the list and allows retrieving elements by their integer position (index).

Key characteristics of the `List` interface include:

- **Maintains Insertion Order**: Elements are stored and accessed in the exact order they are added.
- **Allows Duplicate Elements**: Unlike Sets, Lists permit multiple occurrences of identical elements.
- **Index-Based Operations**: Elements can be inserted, retrieved, updated, and removed using their 0-indexed positions.
- **Bidirectional Traversal**: Supports both forward and backward traversal using the `ListIterator` interface.

## Syntax & Declaration

To declare a list, you define a reference variable of type `List` and assign it to an instance of an implementation class (most commonly `ArrayList` or `LinkedList`):

```java
List<Type> list = new ArrayList<Type>();
```

At the JCF framework level, the interface declaration is generic:

```java
public interface List<E> extends Collection<E>
```

Here, `E` represents the type of elements stored in the list.

## Object Creation of List Interface

Since `List` is an interface, it cannot be instantiated directly. A list is created by instantiating one of its concrete implementation classes. The following code demonstrates instantiating a list of programming languages using `ArrayList` and iterating through its elements using an enhanced `for-each` loop.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        // Creating a List of Strings using ArrayList
        List<String> list = new ArrayList<>();

        // Adding elements to the List
        list.add("Java");
        list.add("Python");
        list.add("DSA");
        list.add("C++");

        System.out.println("Elements of List are:");

        // Iterating through the list
        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

### Output
Elements of List are:
Java
Python
DSA
C++

### Explanation

- The program instantiates a dynamic resizable array class `ArrayList` and stores its reference in a `List<String>` interface type.
- Elements are added sequentially to the end of the list using the `.add()` method.
- The enhanced `for-each` loop iterates over the list elements, displaying them one by one while preserving their insertion order.

## Hierarchy of List Interface

The `List` interface extends `Collection` which in turn extends the `Iterable` interface:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/list-interface-in-java/1782021341064-b3e3f3c0-f79c-4fde-84db-01905c7d8c12.png)

The primary concrete implementation classes of the `List` interface include:

- **ArrayList**: Backed by a dynamically resizing array. It provides fast $O(1)$ random access by index but slower $O(n)$ insertion and deletion operations when elements must be shifted.
- **LinkedList**: Backed by a doubly-linked list. It provides efficient $O(1)$ insertion and deletion at the cost of slower $O(n)$ index-based lookup times.
- **Vector**: A legacy, synchronized resizable array. It is thread-safe, but its locking mechanism introduces runtime overhead, making it slower than `ArrayList` in single-threaded environments.
- **Stack**: Extends `Vector` and implements standard Last-In-First-Out (LIFO) stack operations (e.g., `push()`, `pop()`, `peek()`).

## Java List Operations

The following sections illustrate frequently used operations on lists using `ArrayList` implementations.

### 1. Adding Elements

You can append elements to the end of the list using `add(E element)` or insert them at a specific index using `add(int index, E element)`.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        // Adding elements to list
        list.add("AlphaKnowledge");
        list.add("AlphaKnowledge");
        list.add(1, "AK");

        System.out.println(list);
    }
}
```

### Output
[AlphaKnowledge, AK, AlphaKnowledge]

### Explanation

- The first two `.add("AlphaKnowledge")` calls append the strings at index `0` and `1`.
- `list.add(1, "AK")` inserts the string `"AK"` at index `1`, shifting the second `"AlphaKnowledge"` element to index `2`.
- Note: Attempting to insert an element at a non-existent index (e.g., calling `add(5, "Item")` when the list size is `0`) throws an `IndexOutOfBoundsException`. Elements must be added sequentially or within the boundaries of the list's size.

### 2. Updating Elements

Elements are updated by replacing an existing element at a specific index using the `set(int index, E element)` method.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        // Creating a list of strings
        List<String> list = new ArrayList<>();

        // Adding elements
        list.add("AlphaKnowledge");
        list.add("AlphaKnowledge");
        list.add(1, "AlphaKnowledge");

        System.out.println("Initial ArrayList " + list);

        // Setting (updating) element at index 1 using set() method
        list.set(1, "AK");

        System.out.println("Updated ArrayList " + list);
    }
}
```

### Output
Initial ArrayList [AlphaKnowledge, AlphaKnowledge, AlphaKnowledge]
Updated ArrayList [AlphaKnowledge, AK, AlphaKnowledge]

### Explanation

- The list is initially populated with three instances of the string `"AlphaKnowledge"`.
- `list.set(1, "AK")` replaces the element at index `1` with `"AK"`.
- The size of the list remains unchanged, and only the targeted index is updated.

### 3. Searching Elements

Searching lists is performed using `indexOf(Object o)` (finds the first occurrence) and `lastIndexOf(Object o)` (finds the last occurrence).

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();

        // Add integers to the list
        list.add(10);
        list.add(20);
        list.add(30);
        list.add(20);

        // Find first occurrence of element 20
        int firstIndex = list.indexOf(20);
        System.out.println("First Occurrence of 20 is at Index: " + firstIndex);

        // Find last occurrence of element 20
        int lastIndex = list.lastIndexOf(20);
        System.out.println("Last Occurrence of 20 is at Index: " + lastIndex);
    }
}
```

### Output
First Occurrence of 20 is at Index: 1
Last Occurrence of 20 is at Index: 3

### Explanation

- The list is populated with elements where the number `20` occurs at index `1` and index `3`.
- `list.indexOf(20)` returns the lowest index (`1`) containing the element.
- `list.lastIndexOf(20)` returns the highest index (`3`) containing the element. If an element is not found, both methods return `-1`.

### 4. Removing Elements

You can remove elements from a list by specifying their index via `remove(int index)` or by value via `remove(Object o)`.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        // Adding elements
        list.add("AlphaKnowledge");
        list.add("AlphaKnowledge");

        // Insert 'AK' at index 1
        list.add(1, "AK");

        System.out.println("Initial ArrayList " + list);

        // Remove element present at index 1
        list.remove(1);
        System.out.println("After the Index Removal " + list);

        // Remove the first occurrence of the object "AlphaKnowledge"
        list.remove("AlphaKnowledge");
        System.out.println("After the Object Removal " + list);
    }
}
```

### Output
Initial ArrayList [AlphaKnowledge, AK, AlphaKnowledge]
After the Index Removal [AlphaKnowledge, AlphaKnowledge]
After the Object Removal [AlphaKnowledge]

### Explanation

- The list starts as `[AlphaKnowledge, AK, AlphaKnowledge]`.
- `list.remove(1)` removes the item `"AK"` at index `1`, shifting the trailing elements left.
- `list.remove("AlphaKnowledge")` searches the list sequentially and deletes the first matching instance (at index `0`), leaving only a single `"AlphaKnowledge"` string in the list.

### 5. Accessing Elements

You can access elements at specific indices using `get(int index)`.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        // Adding elements to list
        list.add("AlphaKnowledge");
        list.add("AK");
        list.add("AlphaKnowledge");

        // Accessing elements using get() method
        String first = list.get(0);
        String second = list.get(1);
        String third = list.get(2);

        System.out.println(first);
        System.out.println(second);
        System.out.println(third);
        System.out.println(list);
    }
}
```

### Output
AlphaKnowledge
AK
AlphaKnowledge
[AlphaKnowledge, AK, AlphaKnowledge]

### Explanation

- Three strings are retrieved sequentially from index `0`, `1`, and `2` using the `.get()` method.
- The values are printed individually, followed by the complete list.

### 6. Checking for Presence of Elements

You can check if a list contains a specific element using `contains(Object o)`.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        // Adding elements to list
        list.add("AlphaKnowledge");
        list.add("AK");
        list.add("AlphaKnowledge");

        // Checking if element is present using contains() method
        boolean isPresent = list.contains("AlphaKnowledge");

        // Printing the result
        System.out.println("Is AlphaKnowledge present in the list? " + isPresent);
    }
}
```

### Output
Is AlphaKnowledge present in the list? true

### Explanation

- `list.contains("AlphaKnowledge")` returns `true` because the string exists in the list.

## Iterating over List Interface in Java

For larger datasets, lists can be traversed using index-based loops or enhanced loops.

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        // Adding elements
        list.add("AlphaKnowledge");
        list.add("AlphaKnowledge");
        list.add(1, "AK");

        // Using standard for loop for iteration
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + " ");
        }

        System.out.println();

        // Using for-each loop for iteration
        for (String str : list) {
            System.out.print(str + " ");
        }
    }
}
```

### Output
AlphaKnowledge AK AlphaKnowledge 
AlphaKnowledge AK AlphaKnowledge

### Explanation

- The standard `for` loop uses the list size and retrieves elements sequentially via `.get(i)`.
- The enhanced `for-each` loop hides the index mechanics and iterates directly through the underlying iterator structure.

## Complexity of List Interface in Java

The time and space complexities for basic list operations are summarized below:

| Operation | Time Complexity | Space Complexity |
| --- | --- | --- |
| **Adding Element** | $O(1)$ amortized for `ArrayList` (appending). $O(n)$ if inserting at arbitrary indices due to shifting. | $O(1)$ |
| **Removing Element** | $O(n)$ due to shifting elements left (in `ArrayList`) or searching nodes (in `LinkedList`). | $O(1)$ |
| **Replacing Element** | $O(1)$ index lookup and replacement (in `ArrayList`). | $O(1)$ |
| **Traversing List** | $O(n)$ to visit all elements. | $O(1)$ |

## Methods of the List Interface

Below is a summary of the core methods defined by the `List` interface:

| Method | Description |
| --- | --- |
| `add(int index, E element)` | Inserts the specified element at the specified index. |
| `add(E element)` | Appends the element to the end of the list. |
| `addAll(int index, Collection<? extends E> c)` | Inserts all elements of the collection at the specified index. |
| `size()` | Returns the number of elements in the list. |
| `clear()` | Removes all elements from the list. |
| `remove(int index)` | Removes the element at the specified index and shifts trailing elements left. |
| `remove(Object o)` | Removes the first occurrence of the specified object. |
| `get(int index)` | Returns the element at the specified index. |
| `set(int index, E element)` | Replaces the element at the specified index with the new element, returning the replaced element. |
| `indexOf(Object o)` | Returns the index of the first occurrence of the element, or `-1`. |
| `lastIndexOf(Object o)` | Returns the index of the last occurrence of the element, or `-1`. |
| `equals(Object o)` | Compares the specified object with this list for equality. |
| `hashCode()` | Returns the hash code value for the list. |
| `isEmpty()` | Returns `true` if the list contains zero elements. |
| `contains(Object o)` | Returns `true` if the list contains the specified element. |
| `containsAll(Collection<?> c)` | Returns `true` if the list contains all elements of the target collection. |
| `sort(Comparator<? super E> c)` | Sorts the list based on the rules specified by the comparator. |

## List vs Set

Although both interfaces inherit from the parent `Collection` interface, they enforce different data models:

| Feature | List | Set |
| --- | --- | --- |
| **Element Order** | Ordered sequence. It guarantees that the elements are stored in insertion order. | Unordered collection (except for implementations like `LinkedHashSet` or `TreeSet`). |
| **Duplicates** | Permits duplicate elements. | Strictly prohibits duplicate elements. |
| **Index Access** | Supports index-based access using positional integers (e.g., `get(index)`). | Position-based lookup is not supported. |
| **Null Elements** | Allows storing multiple `null` elements. | Allows storing at most one `null` element (hash-sets) or none (tree-sets). |
| **Common Implementations** | `ArrayList`, `LinkedList`, `Vector`, `Stack`. | `HashSet`, `LinkedHashSet`, `TreeSet`. |

# Summary

The Java List interface is a sub-interface of Collection that manages ordered sequences of objects and permits duplicate elements. Concrete classes like ArrayList and LinkedList implement this interface to support dynamic sizing, sequential storage, and index-based operations. Developers can add, update, remove, search, and iterate over items using dedicated methods like add, set, remove, indexOf, and get. Understanding the differences in implementation complexities between ArrayList (array-backed) and LinkedList (node-linked), as well as contrasting List ordered semantics with Set uniqueness, is key to selecting the appropriate data structures in Java.




