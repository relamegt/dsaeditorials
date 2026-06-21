# ArrayList in Java

## Introduction

An **ArrayList** in Java is a dynamically resizable array implementation provided by the Java Collections Framework (JCF) within the `java.util` package. Unlike standard Java arrays, which have a fixed size that must be declared at instantiation, the capacity of an `ArrayList` grows and shrinks automatically as elements are inserted or removed from the list.

Key features of the `ArrayList` class include:

- **Index-Based Access**: Elements are stored in contiguous memory positions and can be accessed using their 0-indexed positions, similar to standard arrays.
- **Permits Duplicates**: Multiple occurrences of identical objects can coexist within the same list.
- **Preserves Insertion Order**: Elements are returned in the exact chronological sequence in which they were added.
- **Not Thread-Safe**: By default, `ArrayList` is not synchronized. Under concurrent multi-threaded environments, it must be wrapped using `Collections.synchronizedList()` or accessed using concurrent classes like `CopyOnWriteArrayList`.

## Basic Code Demo

The following program demonstrates how to create a basic `ArrayList` storing integers, append elements, and print the resulting collection.

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Creating an ArrayList
        ArrayList<Integer> numbers = new ArrayList<>();

        // Adding Elements in ArrayList
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        // Printing ArrayList
        System.out.println(numbers);
    }
}
```

### Output
[10, 20, 30]

### Explanation

- An `ArrayList` of type `Integer` is initialized.
- Three numeric values (`10`, `20`, `30`) are added sequentially to the list using the `.add()` method.
- The list automatically preserves the order of elements and prints them as a formatted string representation: `[10, 20, 30]`.

## Primitive Types Warning

An `ArrayList` stores object references on the Heap. Consequently, it cannot hold primitive data types (like `int`, `double`, `char`, or `boolean`) directly. When declaring an `ArrayList` for primitives, you must use their corresponding object Wrapper classes:

| Primitive Type | Wrapper Class |
| --- | --- |
| `int` | `java.lang.Integer` |
| `double` | `java.lang.Double` |
| `char` | `java.lang.Character` |
| `boolean` | `java.lang.Boolean` |

Java utilizes **Autoboxing** and **Unboxing** to automatically convert between primitives and their wrapper objects at runtime, allowing statements like `list.add(10)` to compile successfully.

## Hierarchy of ArrayList

The `ArrayList` class implements the `List` interface, which is a sub-interface of `Collection`:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arraylist-in-java/1782021614780-f423fdee-3d44-44a0-b122-2ac42a470033.png)

Additionally, `ArrayList` implements `RandomAccess` (indicating it supports fast, constant-time indexing), `Cloneable` (permitting shallow copying), and `Serializable` (permitting object serialization).

## ArrayList Constructors in Java

Java provides three constructors to initialize an `ArrayList` depending on the use case:

### 1. Default Constructor: ArrayList()

Creates an empty `ArrayList` with an initial capacity of ten elements.

```java
ArrayList<Integer> arr = new ArrayList<>();
```

### 2. Collection Constructor: ArrayList(Collection&lt;? extends E&gt; c)

Creates an `ArrayList` containing the elements of the specified collection, in the order they are returned by the collection's iterator.

```java
ArrayList<String> arr = new ArrayList<>(otherCollection);
```

### 3. Capacity Constructor: ArrayList(int initialCapacity)

Creates an empty `ArrayList` with the specified initial capacity. This prevents repeated internal resizing if the number of elements is known beforehand.

```java
ArrayList<Double> arr = new ArrayList__(20);
```

## Operations of ArrayList

The following code illustrates the core operations of inserting, deleting, and updating elements in an `ArrayList`.

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Creating an ArrayList of String type
        ArrayList<String> list = new ArrayList<>();

        // 1. Adding elements to ArrayList at the end
        list.add("AlphaKnowledge");
        list.add("AlphaKnowledge");

        System.out.println("Original List : " + list);

        // Adding Elements at a specific index
        list.add(1, "AK");

        System.out.println("After Adding element at index 1 : " + list);

        // 2. Removing Element using index
        list.remove(0);

        System.out.println("Element removed from index 0 : " + list);

        // Removing Element using the value match
        list.remove("AlphaKnowledge");

        System.out.println("Element AlphaKnowledge removed : " + list);

        // 3. Updating value at index 0
        list.set(0, "AlphaKnowledge");

        System.out.println("List after updation of value : " + list);
    }
}
```

### Output
Original List : [AlphaKnowledge, AlphaKnowledge]
After Adding element at index 1 : [AlphaKnowledge, AK, AlphaKnowledge]
Element removed from index 0 : [AK, AlphaKnowledge]
Element AlphaKnowledge removed : [AK]
List after updation of value : [AlphaKnowledge]

### Explanation

- The list starts as `[AlphaKnowledge, AlphaKnowledge]`.
- `list.add(1, "AK")` inserts `"AK"` at index `1`, shifting the second `"AlphaKnowledge"` to index `2`.
- `list.remove(0)` deletes the element at index `0` (`"AlphaKnowledge"`), leaving `[AK, AlphaKnowledge]`.
- `list.remove("AlphaKnowledge")` searches the list and deletes the first occurrence of `"AlphaKnowledge"`, leaving `[AK]`.
- `list.set(0, "AlphaKnowledge")` overwrites the element at index `0` (`"AK"`) with `"AlphaKnowledge"`.

## Internal Implementation

Internally, `ArrayList` wraps a standard Java array that is dynamically re-allocated when capacity is reached.

### 1. Backing Array Structure

An `ArrayList` uses an internal array (`transient Object[] elementData`) to store its objects. Contiguous memory allocation allows fast indexing in $O(1)$ time complexity using `get(index)` and `set(index, element)`.

### 2. Automatic Resizing Mechanics

When an element is added and the backing array is full, the list resizes itself:

1. It calculates the new capacity using the formula:

   $$\text{New Capacity} = \text{Old Capacity} + (\text{Old Capacity} \gg 1)$$
   This increases the capacity by exactly **50%** of the current array size.

1. It allocates a new, larger array of the calculated capacity.
2. It copies all elements from the old array to the new array using `Arrays.copyOf()`.
3. It sets `elementData` to reference the new array, allowing the garbage collector to reclaim the old array.

### 3. Element Shifting

Inserting or removing elements at arbitrary indices (e.g. `add(index, element)` or `remove(index)`) requires element shifting:

- **Insertion**: Elements from the target index to the end are shifted to the right by one position using `System.arraycopy()` before the new element is inserted.
- **Deletion**: Elements to the right of the deleted index are shifted left by one position to fill the gap.

## Capacity vs Size Management

- **Size**: Represents the number of elements currently stored in the `ArrayList` (accessible via `size()`).
- **Capacity**: Represents the length of the internal array backing the list. It is always greater than or equal to the size. Resizing only happens when the size exceeds capacity.

## Complexity of Java ArrayList

The complexity of common operations is outlined below:

| Operation | Time Complexity | Space Complexity |
| --- | --- | --- |
| **Inserting Element at the end** | $O(1)$ amortized. Resizing takes $O(n)$, but happens infrequently. | $O(1)$ |
| **Inserting Element at specific index** | $O(n)$ because elements must be shifted right. | $O(1)$ |
| **Removing an Element** | $O(n)$ because elements must be shifted left to fill the gap. | $O(1)$ |
| **Replacing Elements (set)** | $O(1)$ constant-time lookup and write. | $O(1)$ |
| **Traversing Elements** | $O(n)$ to visit all elements. | $O(1)$ |

## Methods of ArrayList

Below is a lookup table of the most common methods available in the `ArrayList` class:

| Method | Description |
| --- | --- |
| `add(int index, E element)` | Inserts the specified element at the specified index, shifting trailing elements right. |
| `add(E e)` | Appends the specified element to the end of the list. |
| `addAll(Collection<? extends E> c)` | Appends all elements from the collection to the end of the list. |
| `addAll(int index, Collection<? extends E> c)` | Inserts all elements from the collection starting at the specified index. |
| `clear()` | Removes all elements from the list, resetting size to zero. |
| `clone()` | Returns a shallow copy of the `ArrayList` instance. |
| `contains(Object o)` | Returns `true` if the list contains the specified element. |
| `ensureCapacity(int minCapacity)` | Increases the capacity of the instance to hold at least the specified minimum capacity. |
| `forEach(Consumer<? super E> action)` | Performs the given action for each element until all elements are processed. |
| `get(int index)` | Returns the element at the specified index. |
| `indexOf(Object o)` | Returns the index of the first occurrence of the element, or `-1`. |
| `isEmpty()` | Returns `true` if the list contains zero elements. |
| `lastIndexOf(Object o)` | Returns the index of the last occurrence of the element, or `-1`. |
| `listIterator()` | Returns a bidirectional list iterator over the elements. |
| `listIterator(int index)` | Returns a list iterator starting at the specified index. |
| `remove(int index)` | Removes the element at the specified index. |
| `remove(Object o)` | Removes the first occurrence of the specified element. |
| `removeAll(Collection<?> c)` | Removes all elements present in the specified collection. |
| `removeIf(Predicate<? super E> filter)` | Removes all elements that satisfy the specified predicate. |
| `removeRange(int fromIndex, int toIndex)` | Removes elements whose index is between `fromIndex` (inclusive) and `toIndex` (exclusive). |
| `retainAll(Collection<?> c)` | Retains only elements present in the specified collection. |
| `set(int index, E element)` | Replaces the element at the specified index with the new element. |
| `size()` | Returns the number of elements in the list. |
| `spliterator()` | Creates a late-binding and fail-fast `Spliterator` over the elements. |
| `subList(int fromIndex, int toIndex)` | Returns a view of the portion of this list between `fromIndex` (inclusive) and `toIndex` (exclusive). |
| `toArray()` | Converts the list elements into an object array. |
| `toArray(T[] a)` | Converts the list elements into a typed array. |
| `trimToSize()` | Trims the capacity of the `ArrayList` instance to match its current size. |

# Summary

The Java ArrayList is a dynamically resizing implementation of the List interface, wrapping a contiguous Object array to combine array-like fast indexing with dynamic capacity management. When the backing array becomes full, the list automatically grows its capacity by 50% and copies elements to a new array structure. It allows duplicate elements and maintains insertion order, but is not thread-safe and requires shifting operations during insertions or deletions at arbitrary index positions. By using wrapper classes for primitives and leveraging its rich set of built-in API methods, developers can easily build efficient, dynamically sized collections in Java.




