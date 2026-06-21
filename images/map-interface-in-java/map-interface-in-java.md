# Map Interface in Java

## Introduction

In Java, the **Map** interface is a member of the Java Collections Framework and resides in the `java.util` package. Unlike standard collection interfaces (like `List` and `Set`), `Map` does not inherit from the `Collection` interface. Instead, it represents a structure that maps unique keys to values. Each key in a `Map` can map to at most one value.

Key features of the `Map` interface include:

- **Key-Value Pair Storage**: Holds data as mappings (entries) of key-value associations.
- **Key Uniqueness**: Keys must be unique. Duplicate keys are not allowed, but values can be duplicated.
- **Null Key/Value Support**: Depending on the implementation, maps can support null values and a null key (e.g., `HashMap` and `LinkedHashMap` support them, while `TreeMap` does not support a null key when natural ordering is used).
- **Performance**: Offers highly efficient retrieval, insertion, and deletion operations based on keys.
- **Synchronization**: Core map implementations are not synchronized. For thread-safe environments, use `ConcurrentHashMap` or wrap existing maps using `Collections.synchronizedMap()`.

## Basic Code Demo

The following program instantiates a `Map` using `HashMap`, inserts entries of name strings and integers, and prints the map.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a Map using HashMap
        Map<String, Integer> m = new HashMap<>();

        // Adding key-value pairs to the map
        m.put("mohit", 1);
        m.put("akash", 2);
        m.put("AlphaKnowledge", 3);

        System.out.println("Map elements: " + m);
    }
}
```

### Output
Map elements: {mohit=1, akash=2, AlphaKnowledge=3}

### Explanation

- A `Map` named `m` is initialized using `HashMap`.
- String keys representing names are mapped to unique integer values using `put()`.
- The print statement outputs the map entries as key-value pairs. Since `HashMap` does not guarantee ordering, elements can appear in arbitrary order.

## Hierarchy of Map Interface

The hierarchy diagram below illustrates how the `Map` interface and its child interfaces and implementing classes are organized:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/map-interface-in-java/1782027107098-8369bfb3-43be-4d83-bbd6-49f83bac89b0.png)

## Implemented Classes of Map Interface

The most commonly used concrete implementations of the `Map` interface include:

- **HashMap**: Stores key-value mappings using hashing algorithms. It provides fast $O(1)$ lookup, insertion, and deletion times, but does not maintain any order.
- **LinkedHashMap**: Extends `HashMap` and uses a doubly-linked list running through all its entries to maintain insertion order.
- **TreeMap**: Implements the `SortedMap` and `NavigableMap` interfaces. It stores elements in a sorted tree structure (Red-Black tree) based on natural ordering or a custom comparator.
- **Hashtable**: A legacy, synchronized implementation of the `Map` interface that is thread-safe but does not allow null keys or values.

## Performing Various Operations on Map

The following examples demonstrate common map tasks using the `HashMap` implementation and elements such as names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and the platform `AlphaKnowledge`.

### 1. Adding Elements

Keys and values are inserted using the `put(K key, V value)` method. Duplicate keys overwrite previous entries, whereas duplicate values are fully supported.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Map<Integer, String> hm1 = new HashMap<>();
        Map<Integer, String> hm2 = new HashMap<>();

        // Inserting elements
        hm1.put(1, "AlphaKnowledge");
        hm1.put(2, "mohit");
        hm1.put(3, "akash");

        hm2.put(1, "AlphaKnowledge");
        hm2.put(2, "mohit");
        hm2.put(3, "akash");

        System.out.println("Map 1: " + hm1);
        System.out.println("Map 2: " + hm2);
    }
}
```

### Output
Map 1: {1=AlphaKnowledge, 2=mohit, 3=akash}
Map 2: {1=AlphaKnowledge, 2=mohit, 3=akash}

### Explanation

- Two maps are initialized and key-value pairs are added using `put()`.
- Primitive values (like `1`, `2`, `3`) are automatically boxed into `Integer` objects.

### 2. Changing Elements

To update the value associated with a key, call `put()` with the existing key and the new value. The old value is overwritten.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Map<Integer, String> hm = new HashMap<>();

        hm.put(1, "mohit");
        hm.put(2, "mohit"); // Duplicate value
        hm.put(3, "akash");

        System.out.println("Initial Map: " + hm);

        // Update the value associated with key 2
        hm.put(2, "AlphaKnowledge");

        System.out.println("Updated Map: " + hm);
    }
}
```

### Output
Initial Map: {1=mohit, 2=mohit, 3=akash}
Updated Map: {1=mohit, 2=AlphaKnowledge, 3=akash}

### Explanation

- Initial map contains two entries with duplicate values (`"mohit"`).
- Calling `hm.put(2, "AlphaKnowledge")` updates the mapping for key `2` from `"mohit"` to `"AlphaKnowledge"`.

### 3. Removing Elements

Mappings can be deleted using `remove(Object key)`, which removes the key and its corresponding value from the map.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Map<Integer, String> hm = new HashMap<>();

        hm.put(1, "AlphaKnowledge");
        hm.put(2, "mohit");
        hm.put(3, "akash");
        hm.put(4, "hemesh");

        System.out.println("Before Removal: " + hm);

        // Remove mapping for key 4
        hm.remove(4);

        System.out.println("After Removal: " + hm);
    }
}
```

### Output
Before Removal: {1=AlphaKnowledge, 2=mohit, 3=akash, 4=hemesh}
After Removal: {1=AlphaKnowledge, 2=mohit, 3=akash}

### Explanation

- The map is populated with four entries.
- `hm.remove(4)` deletes the key-value pair associated with key `4` (`"hemesh"`), leaving three entries in the map.

### 4. Iterating through the Map

You can iterate through a map's entries by accessing its entry set with `entrySet()` and traversing it using a for-each loop.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        Map<Integer, String> hm = new HashMap<>();

        hm.put(1, "AlphaKnowledge");
        hm.put(2, "mohit");
        hm.put(3, "akash");

        for (Map.Entry<Integer, String> entry : hm.entrySet()) {
            int key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + " : " + value);
        }
    }
}
```

### Output
1 : AlphaKnowledge
2 : mohit
3 : akash

### Explanation

- `entrySet()` returns a Set view of all mappings (`Map.Entry<Integer, String>`) contained in the map.
- The loop calls `getKey()` and `getValue()` on each entry to print keys and values.

## Methods in Java Map Interface

The `Map` interface defines a wide variety of APIs to query, mutate, and manage mappings:

| Method | Description |
| --- | --- |
| `clear()` | Removes all mappings from this map. |
| `containsKey(Object key)` | Returns `true` if this map contains a mapping for the specified key. |
| `containsValue(Object value)` | Returns `true` if this map maps one or more keys to the specified value. |
| `entrySet()` | Returns a `Set` view of the mappings contained in this map. |
| `equals(Object o)` | Compares the specified object with this map for equality. |
| `get(Object key)` | Returns the value to which the specified key is mapped, or `null`. |
| `hashCode()` | Returns the hash code value for this map. |
| `isEmpty()` | Returns `true` if this map contains no key-value mappings. |
| `keySet()` | Returns a `Set` view of the keys contained in this map. |
| `put(K key, V value)` | Associates the specified value with the specified key in this map. |
| `putAll(Map<? extends K, ? extends V> m)` | Copies all mappings from the specified map to this map. |
| `remove(Object key)` | Removes the mapping for a key from this map if it is present. |
| `size()` | Returns the number of key-value mappings in this map. |
| `values()` | Returns a `Collection` view of the values contained in this map. |
| `getOrDefault(Object key, V defaultValue)` | Returns the value mapped to the key, or `defaultValue` if the mapping doesn't exist. |
| `merge(K key, V value, BiFunction<? super V, ? super V, ? extends V> remappingFunction)` | Merges a new value with an existing value using a bi-function. |
| `putIfAbsent(K key, V value)` | Associates the key with the value only if the key is not already mapped. |

# Summary

The Java Map interface provides an essential key-value mapping structure outside of the default Collection hierarchy, facilitating rapid $O(1)$ and $O(\log n)$ data retrieval, update, and deletion tasks based on unique keys. Supported by highly optimized implementations like HashMap, insertion-ordered LinkedHashMap, and sorted TreeMap, it offers versatile storage choices matching strict ordering or hashing guidelines. While it permits single null keys and duplicates amongst stored values depending on concrete implementations, its robust method catalog, entrySet traversals, and modern utility functions like getOrDefault make it a central building block for object lookup systems, caching solutions, and database mappings in Java.




