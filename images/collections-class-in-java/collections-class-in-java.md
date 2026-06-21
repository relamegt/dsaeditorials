# Collections Class in Java

## Introduction

The Java Collections Framework (JCF) is a unified architecture that represents and manipulates collections of objects. Within this framework, Java provides the **Collections** class (located in the `java.util` package), which serves as a utility class consisting exclusively of `static` methods. These methods operate on or return collections, providing powerful, ready-made algorithms for sorting, searching, modifying, synchronizing, and wrapping collections.

It is important to distinguish the `Collections` utility class from the `Collection` interface:

- **Collection Interface**: The root interface of the collection hierarchy (e.g., `List`, `Set`, `Queue` inherit from it). It defines core methods like `add()`, `remove()`, and `size()`.
- **Collections Class**: A final helper class containing utility algorithms that perform operations on collections. It has a private constructor to prevent instantiation.

## Collection Interface vs Collections Class

The differences between the `Collection` interface and the `Collections` utility class are summarized below:

| Feature | Collection Interface | Collections Class |
| --- | --- | --- |
| **Type** | Interface | Utility Class |
| **Package** | `java.util.Collection` | `java.util.Collections` |
| **Purpose** | Serves as the root interface for the collection hierarchy. | Contains static utility methods to operate on collections. |
| **Instantiation** | Cannot be instantiated directly (must be implemented by a concrete class). | Cannot be instantiated (contains a private constructor). |
| **Methods** | Instance methods (e.g., `add()`, `remove()`, `clear()`). | Exclusively static methods (e.g., `sort()`, `reverse()`). |

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/collections-class-in-java/1782020768828-9c3f366e-1fbd-435e-a071-29a998528a25.png)

## Collections Class Declaration

At the language level, the `Collections` class is declared as a final utility class extending `java.lang.Object`.

```java
public final class Collections extends Object
```

Key structural characteristics include:

- It extends the base `Object` class.
- The class is marked `final`, meaning it cannot be subclassed.
- The constructor is declared `private` to prevent client code from instantiating it (`new Collections()`), as all its capabilities are exposed via class-level static methods.

## Java Collections Classes Hierarchy

The Java Collections Framework contains interfaces (which define the contract for different collection types) and concrete class implementations (which provide the data structures). Below is a detailed breakdown of the primary concrete classes organized by their parent interfaces:

### 1. List Implemented Classes

Lists are ordered sequences of elements that maintain insertion order and permit duplicate values.

- **ArrayList**: A resizable array implementation. It provides fast $O(1)$ random access by index but slower $O(n)$ insertions and deletions in the middle of the list due to element shifting.
- **LinkedList**: Implements a doubly-linked list. It provides fast $O(1)$ insertions and deletions because it only requires updating node pointers, but slower $O(n)$ sequential search times. It can also act as a Queue or Deque.
- **Vector**: A legacy, synchronized resizable array. It is thread-safe, but its synchronized methods introduce thread overhead, making it slower than `ArrayList` in single-threaded environments.
- **Stack**: Extends `Vector` and implements a classic Last-In-First-Out (LIFO) stack structure. It provides operations like `push()`, `pop()`, and `peek()`.

### 2. Set Implemented Classes

Sets represent mathematical sets that do not permit duplicate elements.

- **HashSet**: Backed by a `HashMap` hash table. It does not maintain any order of elements and offers constant-time $O(1)$ performance for basic operations (add, remove, contains).
- **LinkedHashSet**: Extends `HashSet` but maintains a doubly-linked list running through all its entry nodes. This maintains insertion order, meaning elements are retrieved in the order they were added.
- **TreeSet**: Implements `NavigableSet` and is backed by a Red-Black tree. Elements are stored in sorted, ascending order according to their natural ordering or a custom comparator. Basic operations perform in $O(\log n)$ time.

### 3. Queue Implemented Classes

Queues are designed for holding elements prior to processing, typically ordering elements in a First-In-First-Out (FIFO) manner.

- **PriorityQueue**: An unbounded queue based on a priority heap. Elements are ordered naturally or via a custom comparator, meaning the head is always the smallest or largest element. It does not allow null elements.
- **ArrayDeque**: A resizable-array implementation of the `Deque` (Double-Ended Queue) interface. It can function as a fast FIFO queue or a LIFO stack, offering better performance than `Stack` and `LinkedList`.

### 4. Map Implemented Classes

Maps store key-value associations. Keys must be unique, and each key maps to exactly one value. Although not inheriting from the `Collection` interface, Maps are a core part of the JCF.

- **HashMap**: Uses a hash table to store associations. It allows a single null key and multiple null values, providing $O(1)$ performance for search and update operations. It does not guarantee any iteration order.
- **LinkedHashMap**: Extends `HashMap` and maintains a doubly-linked list. It preserves insertion order or access order (for LRU cache implementations).
- **TreeMap**: Implements the `SortedMap` interface and uses a Red-Black tree structure. Keys are sorted in ascending order.
- **Hashtable**: A legacy, synchronized map that is thread-safe but does not permit null keys or values.
- **WeakHashMap**: A map implementation with weak keys. An entry is automatically removed when its key is no longer in ordinary use, preventing memory leaks in cache scenarios.
- **IdentityHashMap**: Compares keys using reference-equality (`==`) rather than value-equality (`equals()`).
- **ConcurrentHashMap**: A highly concurrent, thread-safe map that uses lock striping. It allows multiple threads to read and write concurrently without locking the entire map.

### 5. Abstract Base Classes

These skeletal implementations simplify writing custom collections by providing default implementations for most methods:

- **AbstractCollection**: Implements core collection methods, leaving only `iterator()` and `size()` to be defined.
- **AbstractList**: Implements `List`, requiring subclasses to only define `get(int)` and `size()`.
- **AbstractSet**: Extends `AbstractCollection` and overrides `equals()` and `hashCode()` to ensure proper set behavior.
- **AbstractMap**: Provides a basic implementation of the `Map` interface.
- **AbstractQueue**: Extends `AbstractCollection` and provides skeletal implementations for basic queue operations.

## Examples of Collections Operations

Here are complete, runnable examples demonstrating common collection operations using different scenarios and unique variables to avoid duplication.

### Example 1: Adding Elements

Adding multiple elements efficiently to a collection using the `Collections.addAll()` helper.

```java
import java.util.ArrayList;
import java.util.Collections;

public class EnvironmentRegistry {
    public static void main(String[] args) {
        ArrayList<String> environments = new ArrayList<>();
        environments.add("Production");
        environments.add("Staging");

        // Add multiple server tags at once using the Collections utility class
        Collections.addAll(environments, "QA-Testing", "Local-Dev", "CI-Sandbox");

        System.out.println("Active Environments: " + environments);
    }
}
```

### Output
Active Environments: [Production, Staging, QA-Testing, Local-Dev, CI-Sandbox]

### Explanation

- The class `EnvironmentRegistry` initializes a dynamic `ArrayList` of strings.
- Individual strings `"Production"` and `"Staging"` are added using the standard `.add()` method.
- The `Collections.addAll()` utility method takes the target collection as the first parameter, followed by a varargs list of items, adding all of them in a single, highly optimized instruction.
- The output displays the final collection containing all five items in insertion order.

### Example 2: Deleting Elements

Removing elements from a collection by specifying their value or index.

```java
import java.util.ArrayList;

public class InventoryManager {
    public static void main(String[] args) {
        ArrayList<String> inventory = new ArrayList<>();
        inventory.add("Laser Scanner");
        inventory.add("Thermal Printer");
        inventory.add("Barcode Decoder");
        inventory.add("Label Applicator");

        // Remove a specific element by matching its value
        inventory.remove("Thermal Printer");

        // Remove the element currently at index 0 (which is now 'Laser Scanner')
        inventory.remove(0);

        System.out.println("Remaining Inventory: " + inventory);
    }
}
```

### Output
Remaining Inventory: [Barcode Decoder, Label Applicator]

### Explanation

- The `InventoryManager` class initializes an `ArrayList` representing equipment.
- `inventory.remove("Thermal Printer")` searches the list for a matching string and removes it. The remaining elements shift left to fill the gap.
- `inventory.remove(0)` deletes the item at index `0`. At this point, `"Laser Scanner"` occupies index `0`, so it is removed.
- The final print statement shows that only the remaining two items are left in the list.

### Example 3: Searching Elements

Checking if a specific element exists in a collection using the list's containment features.

```java
import java.util.ArrayList;

public class AuthorizationSearch {
    public static void main(String[] args) {
        ArrayList<String> roles = new ArrayList<>();
        roles.add("Administrator");
        roles.add("ContentManager");
        roles.add("BillingEditor");
        roles.add("SecurityAuditor");

        // Search check
        boolean isAuditorPresent = roles.contains("SecurityAuditor");
        if (isAuditorPresent) {
            System.out.println("Access control verification: SecurityAuditor role exists.");
        }
    }
}
```

### Output
Access control verification: SecurityAuditor role exists.

### Explanation

- The program creates a list of user access roles.
- `roles.contains("SecurityAuditor")` checks whether the specified element exists by iterating through the collection and checking value equality.
- Since a matching role is found, the program prints the confirmation message.

### Example 4: Updating Elements

Updating or replacing elements at specific indices in a collection.

```java
import java.util.ArrayList;

public class ConfigurationUpdate {
    public static void main(String[] args) {
        ArrayList<String> hostnames = new ArrayList<>();
        hostnames.add("db-primary.internal");
        hostnames.add("cache-replica.internal");
        hostnames.add("auth-service.internal");

        // Replace the hostname at index 0 with a backup disaster recovery endpoint
        hostnames.set(0, "db-dr-failover.internal");

        System.out.println("Updated Configuration: " + hostnames);
    }
}
```

### Output
Updated Configuration: [db-dr-failover.internal, cache-replica.internal, auth-service.internal]

### Explanation

- A list of server hostnames is defined and populated.
- `hostnames.set(0, "db-dr-failover.internal")` overwrites the item at index `0` with the new server address, keeping all other indices unchanged.
- The output displays the modified list with the new value at index `0`.

### Example 5: Sorting a Collection

Sorting the elements of a list alphabetically using the `Collections.sort()` utility.

```java
import java.util.ArrayList;
import java.util.Collections;

public class UsernameSorter {
    public static void main(String[] args) {
        ArrayList<String> usernames = new ArrayList<>();
        usernames.add("zack");
        usernames.add("alex");
        usernames.add("julia");
        usernames.add("marcus");

        // Sort the collection in ascending alphabetical order
        Collections.sort(usernames);

        System.out.println("Sorted Usernames: " + usernames);
    }
}
```

### Output
Sorted Usernames: [alex, julia, marcus, zack]

### Explanation

- The list `usernames` is initialized with unsorted lowercase strings.
- `Collections.sort(usernames)` sorts the elements according to their natural ordering (alphabetical order for Strings, which implement `Comparable`).
- The output displays the usernames sorted from A to Z.

## Comparable vs Comparator in Sorting

Sorting objects in Java is executed via two standard interfaces: `Comparable` and `Comparator`. The `Collections.sort()` utility method leverages these to sort collections of custom objects.

### 1. Comparable Interface

- **Package**: `java.lang`
- **Method**: `public int compareTo(T o)`
- **Sorting Type**: Defines the **natural ordering** of objects (e.g. sorting numbers numerically, strings alphabetically).
- **Implementation**: The class whose objects need sorting must implement `Comparable` and override `compareTo()`. This modifies the class structure directly.

### 2. Comparator Interface

- **Package**: `java.util`
- **Method**: `public int compare(T o1, T o2)`
- **Sorting Type**: Defines a **custom ordering** strategy (e.g. sorting strings by length, or products by rating).
- **Implementation**: Written as an external, independent class or inline lambda/anonymous inner class. It does not modify the target object class itself.

### Code Example: Custom Sorting with Comparator

The following example demonstrates sorting a list of custom `SoftwareProduct` objects by rating in descending order.

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class SoftwareProduct {
    private String name;
    private double rating;

    public SoftwareProduct(String name, double rating) {
        this.name = name;
        this.rating = rating;
    }

    public String getName() {
        return name;
    }

    public double getRating() {
        return rating;
    }

    @Override
    public String toString() {
        return name + " (" + rating + ")";
    }
}

public class ProductRatingSorter {
    public static void main(String[] args) {
        ArrayList<SoftwareProduct> products = new ArrayList<>();
        products.add(new SoftwareProduct("Compiler-IDE", 4.2));
        products.add(new SoftwareProduct("Database-Gui", 4.8));
        products.add(new SoftwareProduct("API-Tester", 4.5));

        // Sort using Collections.sort with an inline Comparator for descending sorting
        Collections.sort(products, new Comparator<SoftwareProduct>() {
            @Override
            public int compare(SoftwareProduct p1, SoftwareProduct p2) {
                return Double.compare(p2.getRating(), p1.getRating());
            }
        });

        System.out.println("Sorted Products by Rating: " + products);
    }
}
```

### Output
Sorted Products by Rating: [Database-Gui (4.8), API-Tester (4.5), Compiler-IDE (4.2)]

### Explanation

- A custom class `SoftwareProduct` stores fields `name` and `rating` but does not implement `Comparable`.
- To sort the list, we call `Collections.sort(products, Comparator)` by supplying an anonymous `Comparator` implementing `compare(p1, p2)`.
- We use `Double.compare(p2.getRating(), p1.getRating())` to order the products descending (from highest to lowest rating).
- The resulting list displays products sorted according to their rating score.

## Synchronized vs Concurrent Collections

In multi-threaded Java applications, standard collections (like `ArrayList` and `HashMap`) are not thread-safe and can throw `ConcurrentModificationException` under parallel access. The Java runtime offers two distinct strategies to handle concurrent collections:

### 1. Synchronized Wrappers (Collections Class)

Methods like `Collections.synchronizedList()` and `Collections.synchronizedMap()` return thread-safe views of target collections.

- **Locking Level**: Locks the entire backing collection during read or write operations using a single mutex monitor lock.
- **Thread Access**: Only one thread can perform operations at a time. This introduces severe synchronization bottlenecks under heavy read/write contention.
- **Iteration**: Iterator traversal is not implicitly thread-safe. Synchronization block wrappers must be used to lock the collection during iterator loops.

### 2. Concurrent Collections (java.util.concurrent)

Classes like `ConcurrentHashMap` and `CopyOnWriteArrayList` provide built-in concurrent access models.

- **Locking Level**: Fine-grained partition locking (lock striping in `ConcurrentHashMap`) or lock-free read optimizations.
- **Thread Access**: Multiple threads can safely read and write concurrently without blocking one another.
- **Iteration**: Iterators are fail-safe, operating on snapshots of elements, and do not throw `ConcurrentModificationException`.

## Unmodifiable vs Immutable Collections

Developers often need to protect collections from unauthorized client modification. Java distinguishes between unmodifiable wrappers and immutable collections:

### 1. Unmodifiable Collections (Collections Class)

Methods like `Collections.unmodifiableList(list)` create a read-only wrapper around a pre-existing collection.

- **Direct Modification**: Calling mutating methods (`add()`, `remove()`) on the returned wrapper throws an `UnsupportedOperationException`.
- **Indirect Modification**: The wrapper remains tied to the original backing collection. If the backing collection is modified, those changes will reflect inside the unmodifiable wrapper.

### 2. Immutable Collections (Java 9+ Factory Methods)

Methods like `List.of()`, `Set.of()`, or `Map.of()` create completely independent, immutable collections.

- **Direct Modification**: Throws `UnsupportedOperationException`.
- **Indirect Modification**: There is no backing collection. The data elements are copied into an immutable internal array, meaning its contents can never be modified.

## Methods of Collections Class

The `Collections` class contains a wide variety of static helper methods. Below is a comprehensive lookup table of these methods and their descriptions:

| Method | Description |
| --- | --- |
| `addAll(Collection<? super T> c, T... elements)` | Inserts all specified elements into the target collection. |
| `asLifoQueue(Deque<T> deque)` | Returns a view of a `Deque` as a Last-in-first-out (LIFO) Queue. |
| `binarySearch(List<? extends Comparable> list, T key)` | Searches the key using a binary search algorithm. The list must be pre-sorted in ascending order. |
| `binarySearch(List<? extends T> list, T key, Comparator<? super T> c)` | Searches the list for the object using binary search with a custom comparator. |
| `checkedCollection(Collection<E> c, Class<E> type)` | Returns a dynamically typesafe view of the specified collection. |
| `checkedList(List<E> list, Class<E> type)` | Returns a dynamically typesafe view of the specified list. |
| `checkedMap(Map<K,V> m, Class<K> keyType, Class<V> valueType)` | Returns a dynamically typesafe view of the specified map. |
| `checkedNavigableMap(NavigableMap<K,V> m, Class<K> keyType, Class<V> valueType)` | Returns a dynamically typesafe view of the specified navigable map. |
| `checkedNavigableSet(NavigableSet<E> s, Class<E> type)` | Returns a dynamically typesafe view of the specified navigable set. |
| `checkedQueue(Queue<E> queue, Class<E> type)` | Returns a dynamically typesafe view of the specified queue. |
| `checkedSet(Set<E> s, Class<E> type)` | Returns a dynamically typesafe view of the specified set. |
| `checkedSortedMap(SortedMap<K,V> m, Class<K> keyType, Class<V> valueType)` | Returns a dynamically typesafe view of the specified sorted map. |
| `checkedSortedSet(SortedSet<E> s, Class<E> type)` | Returns a dynamically typesafe view of the specified sorted set. |
| `copy(List<? super T> dest, List<? extends T> src)` | Copies all elements from the source list into the destination list. The destination list must be at least as long as the source. |
| `disjoint(Collection<?> c1, Collection<?> c2)` | Returns `true` if the two specified collections have no elements in common. |
| `emptyEnumeration()` | Returns an empty `Enumeration` that contains no elements. |
| `emptyIterator()` | Returns an empty `Iterator` that contains no elements. |
| `emptyList()` | Returns an immutable empty `List`. |
| `emptyListIterator()` | Returns an empty `ListIterator` that has no elements. |
| `emptyMap()` | Returns an immutable empty `Map`. |
| `emptyNavigableMap()` | Returns an immutable empty `NavigableMap`. |
| `emptyNavigableSet()` | Returns an immutable empty `NavigableSet`. |
| `emptySet()` | Returns an immutable empty `Set`. |
| `emptySortedMap()` | Returns an immutable empty `SortedMap`. |
| `emptySortedSet()` | Returns an immutable empty `SortedSet`. |
| `enumeration(Collection<T> c)` | Returns an `Enumeration` view over the specified collection. |
| `fill(List<? super T> list, T obj)` | Replaces all elements of the specified list with the specified element object. |
| `frequency(Collection<?> c, Object o)` | Returns the count of elements in the specified collection equal to the object. |
| `indexOfSubList(List<?> source, List<?> target)` | Returns the starting index of the first occurrence of the target list within the source, or `-1`. |
| `lastIndexOfSubList(List<?> source, List<?> target)` | Returns the starting index of the last occurrence of the target list within the source, or `-1`. |
| `list(Enumeration<T> e)` | Returns an `ArrayList` containing the elements returned by the specified enumeration. |
| `max(Collection<? extends T> coll)` | Returns the maximum element of the collection according to natural ordering. |
| `max(Collection<? extends T> coll, Comparator<? super T> comp)` | Returns the maximum element of the collection based on the custom comparator. |
| `min(Collection<? extends T> coll)` | Returns the minimum element of the collection according to natural ordering. |
| `min(Collection<? extends T> coll, Comparator<? super T> comp)` | Returns the minimum element of the collection based on the custom comparator. |
| `nCopies(int n, T o)` | Returns an immutable list consisting of `n` copies of the specified object. |
| `newSetFromMap(Map<E,Boolean> map)` | Returns a set backed by the specified map. |
| `replaceAll(List<T> list, T oldVal, T newVal)` | Replaces all occurrences of the specified old value in the list with the new value. |
| `reverse(List<?> list)` | Reverses the order of the elements in the specified list. |
| `reverseOrder()` | Returns a comparator that imposes the reverse of the natural ordering on Comparable objects. |
| `reverseOrder(Comparator<T> cmp)` | Returns a comparator that imposes the reverse ordering of the specified comparator. |
| `rotate(List<?> list, int distance)` | Rotates the elements in the list by the specified distance. |
| `shuffle(List<?> list)` | Randomly permutes the list using a default source of randomness. |
| `shuffle(List<?> list, Random rnd)` | Randomly permutes the list using the specified source of randomness. |
| `singleton(T o)` | Returns an immutable set containing only the specified object. |
| `singletonList(T o)` | Returns an immutable list containing only the specified object. |
| `singletonMap(K key, V value)` | Returns an immutable map mapping only the specified key to the specified value. |
| `sort(List<T> list)` | Sorts the specified list into ascending order according to natural ordering. |
| `sort(List<T> list, Comparator<? super T> c)` | Sorts the specified list according to the order induced by the custom comparator. |
| `swap(List<?> list, int i, int j)` | Swaps the elements at the specified indices in the list. |
| `synchronizedCollection(Collection<T> c)` | Returns a synchronized (thread-safe) collection backed by the specified collection. |
| `synchronizedList(List<T> list)` | Returns a synchronized (thread-safe) list backed by the specified list. |
| `synchronizedMap(Map<K,V> m)` | Returns a synchronized (thread-safe) map backed by the specified map. |
| `synchronizedNavigableMap(NavigableMap<K,V> m)` | Returns a synchronized (thread-safe) navigable map backed by the specified navigable map. |
| `synchronizedNavigableSet(NavigableSet<T> s)` | Returns a synchronized (thread-safe) navigable set backed by the specified navigable set. |
| `synchronizedSet(Set<T> s)` | Returns a synchronized (thread-safe) set backed by the specified set. |
| `synchronizedSortedMap(SortedMap<K,V> m)` | Returns a synchronized (thread-safe) sorted map backed by the specified sorted map. |
| `synchronizedSortedSet(SortedSet<T> s)` | Returns a synchronized (thread-safe) sorted set backed by the specified sorted set. |
| `unmodifiableCollection(Collection<? extends T> c)` | Returns an unmodifiable (read-only) view of the specified collection. |
| `unmodifiableList(List<? extends T> list)` | Returns an unmodifiable (read-only) view of the specified list. |
| `unmodifiableNavigableMap(NavigableMap<K,? extends V> m)` | Returns an unmodifiable (read-only) view of the specified navigable map. |
| `unmodifiableNavigableSet(NavigableSet<T> s)` | Returns an unmodifiable (read-only) view of the specified navigable set. |
| `unmodifiableSet(Set<? extends T> s)` | Returns an unmodifiable (read-only) view of the specified set. |
| `unmodifiableSortedMap(SortedMap<K,? extends V> m)` | Returns an unmodifiable (read-only) view of the specified sorted map. |
| `unmodifiableSortedSet(SortedSet<T> s)` | Returns an unmodifiable (read-only) view of the specified sorted set. |

# Summary

The Java Collections class is a final utility helper containing static methods that implement fundamental algorithms for manipulating collections, such as sorting, searching, copying, shuffling, and wrapping. Unlike the Collection interface which defines the base structure of objects, the Collections class cannot be instantiated and consists exclusively of static helper methods that operate on lists, sets, queues, and maps. Through its robust set of operations, it provides developers with standardized algorithms that improve code readability, memory efficiency, and execution performance without requiring manual algorithm implementation.




