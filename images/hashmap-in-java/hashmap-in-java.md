# HashMap in Java

## Introduction

A **HashMap** in Java is a member of the Java Collections Framework and implements the `Map` interface. It stores elements in key-value pairs, where keys must be unique, and values can be duplicated. 

Key features of the `HashMap` class include:

- **Hashing Backend**: Internally utilizes hashing algorithms, facilitating highly efficient key-based retrieval, insertion, and removal with an average-case time complexity of $O(1)$.
- **No Thread Safety**: It is not synchronized. To make it thread-safe, wrap it externally using `Collections.synchronizedMap()` or use `ConcurrentHashMap`.
- **Unordered Collection**: Does not guarantee insertion order. Iteration order may vary when running the program. To preserve insertion order, use `LinkedHashMap`; to preserve sorted key order, use `TreeMap`.
- **Null Key/Value Support**: Allows at most one `null` key and multiple `null` values. Adding a `null` key multiple times overwrites the previous value.
- **Declaration**:

`````java
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable
```

## Basic Code Demo

The following program creates a `HashMap` mapping names (String keys) to ages (Integer values), inserts entries, and prints them.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a HashMap
        HashMap<String, Integer> hashMap = new HashMap<>();

        // Add elements to the HashMap
        hashMap.put("mohit", 25);
        hashMap.put("akash", 30);
        hashMap.put("hemesh", 35);

        // Iterate through the HashMap
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

### Output
mohit -> 25
akash -> 30
hemesh -> 35

### Explanation

- A `HashMap` named `hashMap` is initialized.
- Three unique string keys represent names, mapping to their respective age values using `put()`.
- The entry set is traversed using a for-each loop, displaying the key-value mappings. Because `HashMap` is unordered, iteration sequence may vary.

## Hierarchy of HashMap in Java

The hierarchy diagram below illustrates how `HashMap` extends `AbstractMap` and implements the `Map` interface:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/hashmap-in-java/1782027347203-ac7de39a-8260-429a-b7da-561e9412dbd4.png)

## Capacity and Resizing of HashMap

- **Capacity**: The total number of buckets currently available in the underlying hash table. The default initial capacity is **16**.
- **Resizing**: When the bucket fill level exceeds the designated load factor threshold, the capacity is automatically doubled. This resizing uses the formula: $	ext{New Capacity} = 	ext{Old Capacity} 	imes 2$.
- **Load Factor**: A measure defining how full the hash table can get before dynamic resizing occurs. The default load factor is **0.75**, which balances time and memory usage.

## Constructors of HashMap

Java provides four constructors to initialize a `HashMap`:

### 1. Default Constructor: HashMap()

Creates an empty map with the default initial capacity (16) and default load factor (0.75).

```java
HashMap<K, V> hm = new HashMap<>();
```

### 2. Capacity Constructor: HashMap(int initialCapacity)

Creates an empty map with the specified initial capacity and default load factor (0.75).

```java
HashMap<K, V> hm = new HashMap<>(initialCapacity);
```

### 3. Tuning Constructor: HashMap(int initialCapacity, float loadFactor)

Creates an empty map with the specified initial capacity and load factor.

```java
HashMap<K, V> hm = new HashMap<>(initialCapacity, loadFactor);
```

### 4. Map Constructor: HashMap(Map&lt;? extends K, ? extends V&gt; m)

Creates a new map initialized with the same mappings as the specified map.

```java
Map<Integer, String> map = new HashMap<>();
HashMap<Integer, String> hm = new HashMap<>(map);
```

## Performing Various Operations on HashMap

The following examples demonstrate common map tasks using the `HashMap` implementation and elements such as names (`mohit`, `akash`, `hemesh`, `abhiram`, `hemanth`) and the platform `AlphaKnowledge`.

### 1. Adding Elements

Elements are inserted using `put(K key, V value)`. Duplicate keys will overwrite existing values.

```java
import java.util.HashMap;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Add elements using put method
        HashMap<Integer, String> hm1 = new HashMap<>();
        HashMap<Integer, String> hm2 = new HashMap<>();

        hm1.put(1, "AlphaKnowledge");
        hm1.put(2, "mohit");
        hm1.put(3, "akash");

        hm2.put(1, "AlphaKnowledge");
        hm2.put(2, "mohit");
        hm2.put(3, "akash");

        System.out.println("Mappings of HashMap hm1: " + hm1);
        System.out.println("Mappings of HashMap hm2: " + hm2);
    }
}
```

### Output
Mappings of HashMap hm1: {1=AlphaKnowledge, 2=mohit, 3=akash}
Mappings of HashMap hm2: {1=AlphaKnowledge, 2=mohit, 3=akash}

### Explanation

- Unique integer keys map to string values.
- Printing the map displays key-value entries enclosed in curly braces.

### 2. Accessing Elements

Retrieve a value mapped to a given key using the `get(Object key)` method. It returns `null` if the key is not present.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        HashMap<String, Integer> hashMap = new HashMap<>();

        hashMap.put("mohit", 25);
        hashMap.put("akash", 30);
        hashMap.put("hemesh", 35);

        // Access elements using get()
        System.out.println("Age of mohit: " + hashMap.get("mohit"));
        System.out.println("Age of akash: " + hashMap.get("akash"));

        System.out.println("All entries:");
        for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

### Output
Age of mohit: 25
Age of akash: 30
All entries:
mohit -> 25
akash -> 30
hemesh -> 35

### Explanation

- `get("mohit")` returns `25`.
- Iterating using `entrySet()` displays all active key-value pairs.

### 3. Changing Elements

Update a value by calling `put()` with the same key. The new value replaces the old value.

```java
import java.util.HashMap;

public class AlphaKnowledge {
    public static void main(String[] args) {
        HashMap<Integer, String> hm = new HashMap<>();

        hm.put(1, "mohit");
        hm.put(2, "mohit"); // Duplicate value is allowed
        hm.put(3, "akash");

        System.out.println("Initial Map: " + hm);

        // Overwrite value for key 2
        hm.put(2, "AlphaKnowledge");

        System.out.println("Updated Map: " + hm);
    }
}
```

### Output
Initial Map: {1=mohit, 2=mohit, 3=akash}
Updated Map: {1=mohit, 2=AlphaKnowledge, 3=akash}

### Explanation

- The duplicate value `"mohit"` is stored for keys `1` and `2`.
- Updating key `2` changes its value to `"AlphaKnowledge"`.

### 4. Removing Elements

Remove a key-value mapping from the map using the `remove(Object key)` method.

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

        System.out.println("Mappings of HashMap: " + hm);

        // Remove element with key 4
        hm.remove(4);

        System.out.println("Mappings after removal: " + hm);
    }
}
```

### Output
Mappings of HashMap: {1=AlphaKnowledge, 2=mohit, 3=akash, 4=hemesh}
Mappings after removal: {1=AlphaKnowledge, 2=mohit, 3=akash}

### Explanation

- `hm.remove(4)` deletes key `4` along with its mapped value `"hemesh"`.

### 5. Traversal of Java HashMap

Traverse the entries of a `HashMap` using a for-each loop and the `entrySet()` method.

```java
import java.util.HashMap;
import java.util.Map;

public class AlphaKnowledge {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        map.put("vaibhav", 20);
        map.put("mohit", 10);
        map.put("akash", 30);

        for (Map.Entry<String, Integer> e : map.entrySet()) {
            System.out.println("Key: " + e.getKey() + " Value: " + e.getValue());
        }
    }
}
```

### Output
Key: vaibhav Value: 20
Key: mohit Value: 10
Key: akash Value: 30

### Explanation

- Loop iterates through `map.entrySet()` and outputs each key-value pair.

## Time and Space Complexity

HashMap operations offer highly optimized efficiency. In the worst case (due to hash collisions), operations take $O(n)$ time. In Java 8 and later, this is optimized to $O(\log n)$ by converting linked list buckets to balanced Red-Black trees when the bucket size exceeds a treeification threshold of **8**.

| Operation | Time Complexity | Space Complexity |
| --- | --- | --- |
| **Adding elements** | $O(1)$ | $O(1)$ |
| **Removing elements** | $O(1)$ | $O(1)$ |
| **Accessing elements** | $O(1)$ | $O(1)$ |

## Methods of HashMap

The `HashMap` class defines various methods to inspect, query, and mutate mapping records:

| Method | Description |
| --- | --- |
| `clear()` | Removes all mappings from this map. |
| `clone()` | Returns a shallow copy of this `HashMap` instance. |
| `compute(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | Computes a mapping for the specified key and its current mapped value. |
| `computeIfAbsent(K key, Function<? super K,? extends V> mappingFunction)` | Adds computed value if the key is absent or mapped to `null`. |
| `computeIfPresent(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | Computes a new mapping only if the key is already present. |
| `containsKey(Object key)` | Returns `true` if this map contains a mapping for the specified key. |
| `containsValue(Object value)` | Returns `true` if this map maps one or more keys to the specified value. |
| `entrySet()` | Returns a `Set` view of the mappings contained in this map. |
| `get(Object key)` | Returns the value to which the specified key is mapped, or `null`. |
| `isEmpty()` | Returns `true` if this map contains no key-value mappings. |
| `keySet()` | Returns a `Set` view of the keys contained in this map. |
| `merge(K key, V value, BiFunction<? super V,? super V,? extends V> remappingFunction)` | Merges a new value with an existing value using a bi-function. |
| `put(K key, V value)` | Associates the specified value with the specified key in this map. |
| `putAll(Map<? extends K,? extends V> m)` | Copies all mappings from the specified map to this map. |
| `remove(Object key)` | Removes the mapping for the specified key from this map if present. |
| `size()` | Returns the number of key-value mappings in this map. |
| `values()` | Returns a `Collection` view of the values contained in this map. |

### Methods Inherited From Class java.util.AbstractMap

- `equals(Object o)`: Compares the specified object with this map for equality.
- `hashCode()`: Returns the hash code value for this map.
- `toString()`: Returns a string representation of this map.

### Methods Inherited From Interface java.util.Map

- `equals(Object o)`: Compares the specified object with this map for equality.
- `forEach(BiConsumer<? super K,? super V> action)`: Performs the given action for each entry.
- `getOrDefault(Object key, V defaultValue)`: Returns the mapped value, or `defaultValue` if the key is not mapped.
- `hashCode()`: Returns the hash code value for this map.
- `putIfAbsent(K key, V value)`: Associates key with value only if not already mapped.
- `remove(Object key, Object value)`: Removes entry only if currently mapped to specified value.
- `replace(K key, V value)`: Replaces entry only if currently mapped to some value.
- `replace(K key, V oldValue, V newValue)`: Replaces entry only if currently mapped to specified value.
- `replaceAll(BiFunction<? super K,? super V,? extends V> function)`: Replaces each entry's value with the result of invoking the given function.

# Summary

The Java HashMap class implements the Map interface to offer a high-performance hash table storage model for unique key-to-value associations. Backed by dynamic resizing (doubling capacity based on load factor thresholds) and Java 8's collision treeification optimization, it ensures efficient average-case constant-time $O(1)$ operations for key inserts, retrievals, and removals. While it does not guarantee any specific mapping iteration sequence, allows at most one null key, and remains unsynchronized unless wrapped externally, its extensive API options and ease of traversal make it the standard mapping data structure in modern Java software developments.




