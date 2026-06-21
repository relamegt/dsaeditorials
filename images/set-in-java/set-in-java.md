# Set in Java

## Introduction

In Java, the **Set Interface** is a fundamental member of the Java Collections Framework (JCF), located in the `java.util` package. It represents a mathematical collection of unique elements, meaning it strictly prohibits duplicate values.

Key characteristics of the `Set` interface include:

- **No Duplicate Elements**: Storing a duplicate element is ignored.
- **Null Element Storage**: Set implementations can store at most one `null` element, with the exception of `TreeSet`, which does not allow `null` elements and throws a `NullPointerException`.
- **Order Guarantees**: By default, the basic `Set` interface does not guarantee any specific iteration order of its elements (e.g., `HashSet` is unordered, whereas `TreeSet` is sorted and `LinkedHashSet` preserves insertion order).
- **Efficient Operations**: Provides high-performance algorithms for searching, inserting, and deleting elements.

## Declaration

At the JCF framework level, the `Set` interface is declared as a generic interface extending `Collection`:

```java
public interface Set<E> extends Collection<E>
```

Here, `E` represents the type of elements stored in the set.

## Basic Code Demo

The following program demonstrates how to declare a `Set` using the `HashSet` implementation and print its contents.

```java
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        // Create a Set using HashSet
        Set<String> set = new HashSet<>();

        // Displaying the Set
        System.out.println("Set Elements: " + set);
    }
}
```

### Output
Set Elements: []

### Explanation

- The program instantiates a `HashSet` object and assigns it to a `Set<String>` reference.
- Since no elements have been added, the `HashSet` is printed as an empty set `[]`.
- The iteration order in `HashSet` is not guaranteed. If elements are added, they will be retrieved in an order determined by their hash codes.

## Hierarchy of Set Interface

The `Set` interface extends the `Collection` interface, which inherits from `Iterable`:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/set-in-java/1782022380034-d3ec113b-2fa9-47ef-86fd-2a68fe546af0.png)

The concrete classes that implement the `Set` interface include:

- **HashSet**: Stores elements in a hash table. It offers the best performance for basic operations but does not guarantee any iteration order. It allows storing a single `null` value.
- **EnumSet**: A highly efficient, specialized set implementation designed for Java `enum` keys. It is backed by a bit-vector and performs extremely fast.
- **LinkedHashSet**: A subclass of `HashSet` that maintains a doubly-linked list running through its elements. It preserves the insertion order of elements.
- **TreeSet**: Implements the `NavigableSet` interface and is backed by a Red-Black tree structure. It stores elements in sorted, ascending order. It does not allow `null` elements.

## Creating Set Objects

Because `Set` is an interface, objects cannot be created of the type set directly. You must use one of its concrete implementations:

```java
Set<String> set = new HashSet<>();
```

Using Generics restricts the type of elements that can be added to the set, enforcing compile-time type safety.

## Performing Various Operations on Set

The following sections illustrate frequently used operations on a `Set` using simple names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and platforms like `AlphaKnowledge`.

### 1. Adding Elements

Elements are inserted using the `add(E element)` method. If the element is already present, the set remains unmodified and returns `false`.

```java
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();

        // Adding elements to Set. Duplicate entries are automatically filtered out.
        set.add("mohit");
        set.add("mohit");
        set.add("akash");
        set.add("hemesh");

        System.out.println(set);
    }
}
```

### Output
[akash, hemesh, mohit]

### Explanation

- An empty set is initialized.
- The name `"mohit"` is added twice, followed by `"akash"` and `"hemesh"`.
- Because sets prohibit duplicates, only one instance of `"mohit"` is stored.
- The output displays the unique values. Since `HashSet` is unordered, elements may appear in an arbitrary sequence.

### 2. Accessing (Searching) Elements

To check if an element is present in the set, we use the `contains(Object o)` method.

```java
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Set<String> platforms = new HashSet<>();

        platforms.add("AlphaKnowledge");
        platforms.add("Coursera");
        platforms.add("Udemy");
        platforms.add("AlphaKnowledge");

        System.out.println("Set is " + platforms);

        String searchPlatform = "AlphaKnowledge";

        System.out.println("Contains " + searchPlatform + " " + platforms.contains(searchPlatform));
    }
}
```

### Output
Set is [Coursera, AlphaKnowledge, Udemy]
Contains AlphaKnowledge true

### Explanation

- A set of educational platforms is created. The duplicate `"AlphaKnowledge"` is ignored.
- The `.contains("AlphaKnowledge")` search returns `true` because `"AlphaKnowledge"` exists in the set.

### 3. Removing Elements

Elements are deleted from the set using the `remove(Object o)` method.

```java
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        // Declaring object of Set of type String
        Set<String> names = new HashSet<>();

        // Elements are added using add() method
        names.add("mohit");
        names.add("akash");
        names.add("hemesh");
        names.add("akash");
        names.add("abhiram");
        names.add("hemanth");

        System.out.println("Initial HashSet " + names);

        // Removing custom element using remove() method
        names.remove("akash");
        System.out.println("After removing element " + names);
    }
}
```

### Output
Initial HashSet [mohit, abhiram, akash, hemesh, hemanth]
After removing element [mohit, abhiram, hemesh, hemanth]

### Explanation

- A set is initialized with several names. Duplicate `"akash"` entries are filtered out upon insertion.
- `names.remove("akash")` searches the hash table and deletes the matching string `"akash"`.
- The printed output shows the set with `"akash"` removed.

### 4. Iterating Elements

You can traverse elements in a set using an enhanced `for-each` loop.

```java
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        // Creating object of Set and declaring String type
        Set<String> names = new HashSet<>();

        // Adding elements to Set
        names.add("mohit");
        names.add("akash");
        names.add("hemesh");
        names.add("akash");
        names.add("abhiram");
        names.add("hemanth");

        // Iterating through the Set via for-each loop
        for (String value : names) {
            System.out.print(value + ", ");
        }

        System.out.println();
    }
}
```

### Output
mohit, abhiram, akash, hemesh, hemanth,

### Explanation

- The enhanced `for-each` loop retrieves elements sequentially from the underlying iterator.
- Each unique name is printed followed by a comma.

## Methods of Set Interface

Below is a lookup table of the core methods defined in the `Set` interface:

| Method | Description |
| --- | --- |
| `add(E e)` | Adds the specified element to this set if it is not already present. Returns `true` if added. |
| `addAll(Collection<? extends E> c)` | Adds all elements from the specified collection to this set. |
| `clear()` | Removes all elements from this set. |
| `contains(Object o)` | Returns `true` if this set contains the specified element. |
| `containsAll(Collection<?> c)` | Returns `true` if this set contains all elements of the specified collection. |
| `hashCode()` | Returns the hash code value for this set. |
| `isEmpty()` | Returns `true` if this set contains zero elements. |
| `iterator()` | Returns an iterator over the elements in this set. |
| `remove(Object o)` | Removes the specified element from this set if it is present. |
| `removeAll(Collection<?> c)` | Removes from this set all of its elements that are contained in the specified collection. |
| `retainAll(Collection<?> c)` | Retains only the elements in this set that are contained in the specified collection. |
| `size()` | Returns the number of elements in this set. |
| `toArray()` | Returns an array containing all of the elements in this set. |
| `toArray(T[] a)` | Returns an array containing all of the elements in this set of the specified array type. |

# Summary

The Set interface in Java is a core component of JCF that represents collections of unique elements, strictly prohibiting duplicates. Implemented by classes like HashSet (hash table-backed), LinkedHashSet (insertion-ordered), and TreeSet (Red-Black tree-backed for sorted ordering), it provides highly efficient algorithms for search, insertion, and deletion. Standard operations like adding, checking existence, removing, and iterating elements are handled via straightforward API methods, making Set the collection of choice for mathematical grouping and duplicate filtering in Java applications.




