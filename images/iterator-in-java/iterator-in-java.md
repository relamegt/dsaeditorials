# Iterator in Java

## Introduction

An **Iterator** in Java is a core cursor interface provided by the Java Collections Framework (JCF) within the `java.util` package. It is used to traverse or iterate through elements of a collection one by one.

Key features of the `Iterator` interface include:

- **Uni-directional Traversal**: Traverses elements in the forward direction only.
- **Safe Element Removal**: Provides a safe way to remove elements from the collection during traversal using the `remove()` method, avoiding `ConcurrentModificationException` issues.
- **Universal Cursor**: Applies universally to most collection types, including `List`, `Set`, and `Queue`.
- **Map Iteration**: Although a `Map` is part of the Collections Framework, it does not implement the `Collection` interface directly. However, an `Iterator` can be used on maps indirectly by obtaining set views via `keySet()`, `values()`, or `entrySet()`.
- **Declaration**:

`````java
public interface Iterator<E>
```

## Basic Code Demo

The following program creates an `ArrayList` of name strings, obtains an iterator, and prints each name.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create an ArrayList and add some elements
        ArrayList<String> al = new ArrayList<>();
        al.add("mohit");
        al.add("akash");
        al.add("AlphaKnowledge");

        // Obtain an iterator for the ArrayList
        Iterator<String> it = al.iterator();

        // Iterate through the elements and print each one
        while (it.hasNext()) {
            // Get the next element
            String name = it.next(); 
            System.out.println(name);      
        }
    }
}
```

### Output
mohit
akash
AlphaKnowledge

### Explanation

- An `ArrayList` named `al` is created and populated with name strings.
- An iterator object `it` is created by calling `al.iterator()`.
- The `while` loop checks if there is a next element with `it.hasNext()` and retrieves it with `it.next()`, printing `"mohit"`, `"akash"`, and `"AlphaKnowledge"` sequentially.

## Hierarchy of Iterator

`Iterator` is part of the `java.util` package. Collection classes implement the `Iterable` interface, which defines the `iterator()` method returning an `Iterator` instance:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterator-in-java/1782027578996-682dad27-9e5d-4270-85e1-08397c609701.png)

## Methods of Iterator Interface

The `Iterator` interface defines three primary methods:

### 1. hasNext()

Returns `true` if the iteration has more elements to traverse.

```java
boolean hasNext();
```

### 2. next()

Returns the next element in the iteration. It throws a `NoSuchElementException` if no more elements are present.

```java
E next();
```

### 3. remove()

Removes the last element returned by the iterator's `next()` call. This method can be called only once per call to `next()`. Calling it more than once without calling `next()` will throw an `IllegalStateException`.

```java
void remove();
```

Consider the following demonstration:

```java
Iterator<Integer> it = list.iterator();
it.next();
it.remove();  // Works fine
it.remove();  // Throws IllegalStateException
```

The `remove()` method can throw the following exceptions:

- **UnsupportedOperationException**: If the `remove` operation is not supported by the backing collection.
- **IllegalStateException**: If the `remove()` method is called before calling `next()`, or called more than once per `next()` call.

## Internal Working of Iterator

The cursor pointer moves step-by-step through the underlying collection structure during iteration:

- **Initial State**: The iterator cursor is positioned before the first element of the collection.
- **Step 1**: When calling `citiesIterator.hasNext()` and `citiesIterator.next()`, the cursor moves past the first element and returns it.
- **Step 2**: When calling `next()` again, the cursor moves past the second element and returns it.
- **Step 3**: This process repeats until the cursor reaches past the last element in the collection.
- **Final State**: Once the cursor points past the final element, calling `hasNext()` returns `false`.

Because the Java `Iterator` only moves in a forward direction, it is a uni-directional cursor. For bi-directional traversal (both forward and backward), use `ListIterator`.

## Example: Traverse and Remove Elements

The following program creates an `ArrayList` of integers, traverses it using an `Iterator`, and removes all odd numbers.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Creating an ArrayList of Integer type
        ArrayList<Integer> al = new ArrayList<>();

        // Adding elements to the ArrayList
        for (int i = 0; i < 10; i++) {
            al.add(i);
        }

        // Printing the original list
        System.out.println("Original List: " + al);

        // Creating an Iterator for the ArrayList
        Iterator<Integer> itr = al.iterator();

        // Iterating through the list and removing odd elements
        while (itr.hasNext()) {
            // Getting the next element
            int i = itr.next();  

            System.out.print(i + " ");  

            // Removing odd elements
            if (i % 2 != 0) {
                itr.remove();
            }
        }
        System.out.println();

        // Printing the modified list after removal of odd elements
        System.out.println("Modified List: " + al);
    }
}
```

### Output
Original List: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
0 1 2 3 4 5 6 7 8 9 
Modified List: [0, 2, 4, 6, 8]

### Explanation

- An `ArrayList` is filled with integers `0` through `9`.
- The `itr` iterator traverses the list, checking each element. When an odd integer is encountered (`i % 2 != 0`), it is deleted using `itr.remove()`.
- The final printed output shows that the original list has been modified to contain only even numbers.

# Summary

The Java Iterator interface represents a universal, uni-directional cursor designed to traverse collections sequentially in the forward direction. Supported across key Collections Framework subtypes like List, Set, and Queue, it enables safe element mutation during traversal via its remove method, avoiding the ConcurrentModificationExceptions that often occur when editing elements directly during iteration. While it requires indirect views like entrySet or keySet to iterate over Map structures and lacks the bi-directional capabilities of ListIterator, its clean methods hasNext and next make it the fundamental cursor implementation for general collection traversal in Java applications.




