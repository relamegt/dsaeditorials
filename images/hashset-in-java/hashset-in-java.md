# HashSet in Java

## Introduction

A **HashSet** in Java is a prominent concrete implementation of the `Set` interface, residing in the `java.util` package. It is designed to store unique elements and relies on a hash table backing structure to achieve outstanding performance.

Key features of the `HashSet` class include:

- **No Duplicates Allowed**: Duplicate elements are silently filtered out during insertion.
- **HashMap Internal Backend**: Internally, `HashSet` uses a `HashMap` instance to store its objects. Elements added to the `HashSet` are stored as keys in the backing map with a dummy constant value.
- **Unordered Semantics**: Does not guarantee any specific iteration order. The order of elements is determined by hashing values and can change over time.
- **Implements Core Interfaces**: Implements the `Set` interface, along with `Serializable` (for object saving/loading) and `Cloneable` (for shallow copying).
- **Not Thread-Safe**: It is not synchronized. Under multi-threaded access, it must be synchronized externally (typically using `Collections.synchronizedSet()`).
- **Object Storage Only**: Does not support primitive data types directly. Wrapper classes must be utilized instead.

## Basic Code Demo

The following program instantiates a `HashSet` of integers, adds elements (including a duplicate), and outputs its size and contents.

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Instantiate an object of HashSet
        HashSet<Integer> hs = new HashSet<>();

        // Adding elements
        hs.add(10);
        hs.add(20);
        hs.add(10);

        System.out.println("HashSet Size: " + hs.size());
        System.out.println("Elements in HashSet: " + hs);
    }
}
```

### Output
HashSet Size: 2
Elements in HashSet: [20, 10]

### Explanation

- A `HashSet` named `hs` is created to store integers.
- The numbers `10` and `20` are successfully added. The duplicate `10` addition is ignored since `HashSet` enforces uniqueness.
- The size of the set is `2`, and printing the set displays the unique elements `[20, 10]` (order can be arbitrary).

## Hierarchy Diagram of HashSet

The hierarchy diagram below shows how `HashSet` inherits from `Set`, `Collection`, and `Iterable`:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/hashset-in-java/1782024646678-f66a52d8-4556-46a5-af59-19e7b5f40973.png)

## Capacity of HashSet

- **Capacity**: Represents the number of buckets in the underlying hash table.
- **Default Initial Capacity**: The default capacity when using the parameterless constructor is **16**.
- **Automatic Resizing**: When the number of stored elements exceeds the designated threshold, the backing table capacity is automatically doubled. This is calculated using the formula: $\text{New Capacity} = \text{Old Capacity} \times 2$.

## Collision in HashSet

Since `HashSet` uses hashing, multiple elements can compute the same hash code and map to the same bucket in the backing table, resulting in a **Collision**.

- **Java 7 and earlier**: Handled collisions by chaining elements in a singly-linked list within each bucket.
- **Java 8 and later**: Optimized this by converting the linked list into a balanced **Red-Black Tree** once the number of elements in a single bucket exceeds a threshold of **8** (treeification). It converts back to a linked list if the bucket size drops below **6** (untreeification). This improves worst-case lookup performance from $O(n)$ to $O(\log n)$.

## Load Factor & Resizing Threshold

- **Load Factor**: A measure defining how full the hash table can get before its capacity is dynamically doubled. The default load factor is **0.75**, balancing search speed and memory usage.
- **Threshold**: The exact element count that triggers table resizing. It is computed using the formula: $\text{Threshold} = \text{Capacity} \times \text{Load Factor}$. For default parameters, the threshold is: $16 \times 0.75 = 12 \text{ elements}$.

## Constructors of HashSet class

Java provides four constructors to initialize a `HashSet`:

### 1. Default Constructor: HashSet()

Creates an empty set with default capacity (16) and load factor (0.75).

```java
HashSet<String> set = new HashSet<>();
```

### 2. Capacity Constructor: HashSet(int initialCapacity)

Creates an empty set with the specified initial capacity and default load factor (0.75).

```java
HashSet<String> set = new HashSet<>(32);
```

### 3. Tuning Constructor: HashSet(int initialCapacity, float loadFactor)

Creates an empty set with the given initial capacity and load factor.

```java
HashSet<String> set = new HashSet<>(32, 0.85f);
```

### 4. Collection Constructor: HashSet(Collection&lt;? extends E&gt; c)

Creates a set populated with elements from the specified collection, automatically filtering duplicates.

```java
HashSet<String> set = new HashSet__(otherCollection);
```

## Performing Various Operations on HashSet

The following examples demonstrate common `HashSet` tasks using simple names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and platforms like `AlphaKnowledge`.

### 1. Adding Elements in HashSet

You can add elements using `add(E element)`. Duplicate items are ignored.

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Creating an empty HashSet of string entities
        HashSet<String> hs = new HashSet<>();

        // Adding elements using add() method
        hs.add("AlphaKnowledge");
        hs.add("mohit");
        hs.add("akash");

        System.out.println("HashSet : " + hs);
    }
}
```

### Output
HashSet : [mohit, AlphaKnowledge, akash]

### Explanation

- A string `HashSet` is created.
- Three unique elements are added. The output displays the unique items in unordered sequence.

### 2. Removing Elements in HashSet

Elements are deleted using `remove(Object o)`.

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        HashSet<String> hs = new HashSet<>();

        // Adding elements using add() method
        hs.add("AlphaKnowledge");
        hs.add("mohit");
        hs.add("akash");
        hs.add("hemesh");
        hs.add("hemanth");
        hs.add("abhiram");

        System.out.println("HashSet : " + hs);

        // Removing the element hemanth
        hs.remove("hemanth");

        // Printing the updated HashSet elements
        System.out.println("HashSet after removing element : " + hs);

        // Returns false if the element is not present
        System.out.println("hemanth exists in Set : " + hs.remove("hemanth"));
    }
}
```

### Output
HashSet : [akash, hemesh, mohit, abhiram, AlphaKnowledge, hemanth]
HashSet after removing element : [akash, hemesh, mohit, abhiram, AlphaKnowledge]
hemanth exists in Set : false

### Explanation

- Six unique elements are added to the set.
- `hs.remove("hemanth")` deletes `"hemanth"` from the backing map keys.
- The subsequent remove call returns `false` since `"hemanth"` is no longer present.

### 3. Iterating through the HashSet

You can traverse elements using `Iterator` or enhanced `for-each` loops.

```java
import java.util.HashSet;
import java.util.Iterator;

public class Main {
    public static void main(String[] args) {
        // Create a HashSet of Strings
        HashSet<String> hs = new HashSet<>();

        // Add elements to the HashSet
        hs.add("mohit");
        hs.add("akash");
        hs.add("AlphaKnowledge");
        hs.add("hemesh");
        hs.add("hemanth");

        // Using iterator() method to iterate Over the HashSet
        System.out.print("Using iterator : ");
        Iterator<String> iterator = hs.iterator();

        // Traversing HashSet
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + ", ");
        }

        System.out.println();

        // Using enhanced for loop to iterate Over the HashSet
        System.out.print("Using enhanced for loop : ");
        for (String element : hs) {
            System.out.print(element + " , ");
        }
    }
}
```

### Output
Using iterator : mohit, akash, AlphaKnowledge, hemesh, hemanth, 
Using enhanced for loop : mohit , akash , AlphaKnowledge , hemesh , hemanth ,

### Explanation

- The program iterates through the unique elements sequentially.
- The output displays the elements using both iteration strategies.

## Methods of HashSet

Below is a lookup table of the core methods defined in the `HashSet` class:

| Method | Description |
| --- | --- |
| `add(E e)` | Adds the specified element to this set if not already present. Returns `true` if added. |
| `clear()` | Removes all elements from the set. |
| `contains(Object o)` | Returns `true` if the specified element is present in this set. |
| `remove(Object o)` | Removes the specified element from this set if present. |
| `iterator()` | Returns an iterator over the elements in the set. |
| `isEmpty()` | Returns `true` if the set contains zero elements. |
| `size()` | Returns the number of elements in the set. |
| `clone()` | Returns a shallow copy of the `HashSet` instance. |

## Differences between HashSet and HashMap

Although `HashSet` uses `HashMap` internally, they serve different data needs:

| Basis | HashSet | HashMap |
| --- | --- | --- |
| **Implementation** | Implements the `Set` interface. | Implements the `Map` interface. |
| **Duplicates** | Does not allow duplicate values. | Does not allow duplicate keys. A duplicate key overwrites its existing value. |
| **Number of Objects** | Requires only a single object parameter: `add(Object o)`. | Requires key-value parameters: `put(K key, V value)`. |
| **Internal Working** | Uses a `HashMap` internally, storing elements as keys with a dummy value object (`PRESENT`). | Uses hashing algorithms to store key-value pair structures. |
| **Performance** | Practically identical to `HashMap` since it is backed by it. | High-performance hashing. |
| **Insertion Method** | Uses the `add()` method. | Uses the `put()` method. |

# Summary

The Java HashSet class implements the Set interface, wrapping a HashMap internally to provide high-performance, unique object collections. Supported by automatic resizing (doubling capacity on threshold limit), collision mitigation via chaining and balanced Red-Black tree conversion in Java 8+, it allows developers to quickly add, search, delete, and iterate elements. While it does not guarantee element ordering and is not thread-safe, its constant-time $O(1)$ performance for fundamental operations makes it an essential data structure in standard Java applications.




