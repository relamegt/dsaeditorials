# StringBuffer Class in Java

## Introduction

The `StringBuffer` class in Java is a peer class of `String` that provides much of the functionality of strings. However, unlike the immutable `String` class, `StringBuffer` represents a mutable, growable, and writable sequence of characters. It belongs to the `java.lang` package and has been available since JDK 1.0.

Internally, `StringBuffer` stores characters in a dynamically resizable array. When modifications are performed, they affect the internal character array directly, modifying the existing object in memory. In addition, all public methods of `StringBuffer` are synchronized, which makes it safe for use by multiple threads concurrently, but introduces some performance overhead in single-threaded scenarios.

### Key Features

- **Mutability**: The sequence of characters can be modified after creation (append, insert, replace, delete).
- **Thread-Safety**: It is synchronized, meaning multiple threads cannot access its methods simultaneously, preventing data inconsistency.
- **Performance Efficiency**: It modifies the existing buffer without creating new temporary objects, reducing heap memory allocation and garbage collection overhead.
- **Interface Implementation**: Implements `Serializable` (marker interface for object serialization), `CharSequence` (readable character sequence), and `Appendable` (ability to append characters).

## Why Use StringBuffer?

In Java, `String` objects are immutable. Any modification (like using the `+` operator or `concat()`) results in the creation of a new `String` object in memory. When string modifications are performed repeatedly (e.g., inside loops), this behavior degrades performance and wastes memory.

### Example Using String

```java
public class Main {
    public static void main(String[] args) {

        String course = "AlphaKnowledge";

        course = course + " Java";
        course = course + " Programming";
        course = course + " Course";

        System.out.println(course);
    }
}
```

### Output
AlphaKnowledge Java Programming Course

### Problem

In the above example, the JVM performs the following operations:

1. Allocates the initial object `"AlphaKnowledge"`.
2. Concatenates `" Java"`, creating a new object `"AlphaKnowledge Java"` and discarding the original.
3. Concatenates `" Programming"`, creating a new object `"AlphaKnowledge Java Programming"`.
4. Concatenates `" Course"`, creating the final object `"AlphaKnowledge Java Programming Course"`.

This creates four distinct String objects in memory, leaving three of them eligible for Garbage Collection. This causes significant memory fragmentation and GC overhead, especially during intensive text processing.

## Using StringBuffer

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer();

        sb.append("AlphaKnowledge");
        sb.append(" Java");
        sb.append(" Programming");
        sb.append(" Course");

        System.out.println(sb);
    }
}
```

### Output
AlphaKnowledge Java Programming Course

### Explanation

Only a single `StringBuffer` object is created and modified in memory. Characters are appended directly to its internal array, avoiding the overhead of creating temporary objects.

# Interface Hierarchy

The `StringBuffer` class is part of an inheritance hierarchy that enables mutable string structures:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stringbuffer-class-in-java/1781862495365-6ec6ac0c-3e74-42c6-8b96-59bae3813a28.png)

- **Object**: The root class of the Java class hierarchy.
- **AbstractStringBuilder**: A package-private abstract class that provides the common implementation for mutable character sequence storage (used by both `StringBuffer` and `StringBuilder`).
- **Interfaces Implemented**:
- `Serializable`: Enables the state of a `StringBuffer` instance to be serialized and deserialized.
- `CharSequence`: Provides read-only access to the sequence of characters.
- `Appendable`: Specifies methods to append characters and character sequences.

# Constructors of StringBuffer

Java provides four constructors to initialize `StringBuffer` objects with varying initial capacities.

## 1. StringBuffer()

Creates an empty string buffer with a default initial capacity of 16 characters.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer();

        sb.append("Mohit");

        System.out.println(sb);
    }
}
```

### Output
Mohit

## 2. StringBuffer(int capacity)

Creates an empty string buffer with the specified initial capacity. This is useful when the approximate length of the final string is known beforehand, preventing unnecessary buffer re-allocations.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer(50);

        sb.append("AlphaKnowledge");

        System.out.println(sb);
        System.out.println(sb.capacity());
    }
}
```

### Output
AlphaKnowledge
50

## 3. StringBuffer(String str)

Creates a string buffer initialized with the content of the specified string. The initial capacity of the buffer is set to `str.length() + 16`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Java");

        sb.append(" Programming");

        System.out.println(sb);
    }
}
```

### Output
Java Programming

## 4. StringBuffer(CharSequence seq)

Creates a string buffer initialized with the characters of the specified `CharSequence`. The initial capacity of the buffer is set to `seq.length() + 16`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        CharSequence cs = "Alpha";
        StringBuffer sb = new StringBuffer(cs);

        System.out.println(sb);
        System.out.println(sb.capacity());
    }
}
```

### Output
Alpha
21

# Capacity of StringBuffer

The **capacity** of a `StringBuffer` represents the number of characters it can store without allocating additional memory. When the number of characters exceeds the current capacity, the JVM automatically allocates a new internal array and copies the existing characters.

### Growth Formula

When a capacity expansion occurs, the new capacity is determined by:

```text
New Capacity = (Old Capacity × 2) + 2
```

If this expanded capacity is still insufficient for the new text, the capacity is set to the exact length of the new content.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer();

        System.out.println(sb.capacity());

        sb.append("Hello");

        System.out.println(sb.capacity());

        sb.append("Java Programming Course for Beginners");

        System.out.println(sb.capacity());
    }
}
```

### Output
16
16
34

# Important Methods of StringBuffer

The `StringBuffer` class offers a wide range of synchronized methods for string editing and query operations.

## 1. append()

Appends the string representation of the argument to the end of the character sequence. It has overloaded versions for primitive types, character arrays, objects, and strings.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Mohit");

        sb.append(" Kumar");

        System.out.println(sb);
    }
}
```

### Output
Mohit Kumar

## 2. insert()

Inserts the string representation of the argument at the specified offset index. Overloaded for various data types.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Akash");

        sb.insert(5, " Kumar");

        System.out.println(sb);
    }
}
```

### Output
Akash Kumar

## 3. replace()

Replaces the characters in a substring of this `StringBuffer` with characters in the specified `String`. The substring begins at the specified `start` index and extends to the character at index `end - 1`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Mohit");

        sb.replace(0, 5, "Hemesh");

        System.out.println(sb);
    }
}
```

### Output
Hemesh

## 4. delete()

Removes the characters in a substring of this sequence. The substring begins at the specified `start` index and extends to the character at index `end - 1`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        sb.delete(5, 14);

        System.out.println(sb);
    }
}
```

### Output
Alpha

## 5. deleteCharAt()

Removes the `char` at the specified position in this sequence, shifting subsequent characters to the left.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Abhiram");

        sb.deleteCharAt(2);

        System.out.println(sb);
    }
}
```

### Output
Abiram

## 6. reverse()

Causes this character sequence to be replaced by the reverse of the sequence.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Mohit");

        sb.reverse();

        System.out.println(sb);
    }
}
```

### Output
tihoM

## 7. length()

Returns the length (character count) of this sequence.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        System.out.println(sb.length());
    }
}
```

### Output
14

## 8. capacity()

Returns the current capacity of the internal buffer.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer();

        System.out.println(sb.capacity());
    }
}
```

### Output
16

## 9. charAt()

Returns the `char` value at the specified index.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        System.out.println(sb.charAt(0));
    }
}
```

### Output
A

## 10. setCharAt()

The character at the specified index is set to `ch`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Mohit");

        sb.setCharAt(0, 'R');

        System.out.println(sb);
    }
}
```

### Output
Rohit

## 11. ensureCapacity()

Ensures that the capacity is at least equal to the specified minimum. If the current capacity is less than the argument, a new internal buffer is allocated with a larger capacity.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer();

        sb.ensureCapacity(100);

        System.out.println(sb.capacity());
    }
}
```

### Output
100

## 12. setLength()

Sets the length of the character sequence. If the new length is less than the current length, the sequence is truncated. If the new length is greater, null characters (`\u0000`) are appended.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        sb.setLength(5);

        System.out.println(sb);
    }
}
```

### Output
Alpha

## 13. substring()

Returns a new `String` that contains a subsequence of characters currently contained in this character sequence starting from the start index to the end.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        System.out.println(sb.substring(5));
    }
}
```

### Output
Knowledge

## 14. indexOf()

Returns the index within this string of the first occurrence of the specified substring.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        System.out.println(sb.indexOf("Know"));
    }
}
```

### Output
5

## 15. lastIndexOf()

Returns the index within this string of the last occurrence of the specified substring.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("Java Java Java");

        System.out.println(sb.lastIndexOf("Java"));
    }
}
```

### Output
10

## 16. toString()

Returns a string representing the data in this sequence. A new `String` object is allocated and initialized to contain the character sequence currently represented by this `StringBuffer`.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        String str = sb.toString();

        System.out.println(str);
    }
}
```

### Output
AlphaKnowledge

## 17. trimToSize()

Attempts to reduce storage used for the character sequence. If the buffer is larger than necessary to hold its current sequence of characters, it is resized to fit the current characters exactly, releasing unused heap memory.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb = new StringBuffer(100);

        sb.append("Java");

        sb.trimToSize();

        System.out.println(sb.capacity());
    }
}
```

### Output
4

# String vs StringBuffer

The trade-offs between `String` and `StringBuffer` center around mutability, performance, and memory utilization:

| Feature | String | StringBuffer |
| --- | --- | --- |
| **Mutability** | Immutable (cannot be modified after creation). | Mutable (modifiable in-place). |
| **Thread Safety** | Thread-safe by design due to immutability. | Thread-safe through synchronized methods. |
| **Performance for Updates** | Slower (creates multiple objects during update). | Faster (modifies the same buffer object). |
| **Memory Usage** | Higher (creates multiple temp objects). | Lower (reuses the same memory buffer). |
| **Object Creation** | Multiple objects are allocated in SCP/Heap. | A single resizable object is allocated in Heap. |
| **Best Use Case** | Fixed text, configuration, HashMap keys. | Heavy modifications, dynamic string compilation. |

# StringBuffer vs StringBuilder

While both represent mutable character sequences, their synchronization leads to different performance profiles:

| Feature | StringBuffer | StringBuilder |
| --- | --- | --- |
| **Thread Safety** | Thread-safe (methods are synchronized). | Non-thread-safe (methods are unsynchronized). |
| **Synchronization** | Yes (incurs locking overhead). | No (no locking overhead). |
| **Speed** | Slower (due to synchronization thread locks). | Faster (no thread locking overhead). |
| **Multi-threading** | Recommended for shared buffers between threads. | Not recommended for multi-threaded environments. |
| **Single-threading** | Good. | Best (highest speed performance). |

# Advantages of StringBuffer

1. **Mutable and Flexible**: Allows in-place text modification, avoiding object creation cascades.
2. **Thread-Safe**: Can be safely shared between multiple threads because all core editing methods are synchronized.
3. **Efficient for Repeated Modifications**: Reduces the number of object allocations in Heap memory during string building operations.
4. **Reduces Memory Wastage**: Reuses a single character array container, preventing garbage collection clutter.
5. **Supports Rich Editing Methods**: Provides built-in methods for complex operations such as reverse, insert, delete, and substring.
6. **Suitable for Dynamic Text Generation**: Ideal for logging systems, SQL query assembly, and document building templates.

# Limitations of StringBuffer

1. **Slower than StringBuilder**: The synchronization overhead in each method call makes it slower than `StringBuilder` in single-threaded contexts.
2. **Synchronization Overhead**: Explicit method locking consumes extra CPU resources.
3. **Not Ideal for Single-Threaded Programs**: In modern Java, standard string processing happens in single threads, where `StringBuilder` is almost always preferred due to zero locking overhead.

# Summary

StringBuffer is a mutable, synchronized, and thread-safe class used for efficient string manipulation in Java. Unlike the immutable `String` class, it allows developers to perform operations like append, insert, replace, and delete directly on the same memory object. While synchronization makes `StringBuffer` highly suited for concurrent execution environments, it introduces a slight performance overhead, making its unsynchronized counterpart, `StringBuilder`, the standard choice for single-threaded modifications. Understanding the differences in mutability, thread safety, and performance allows Java programmers to optimize their memory usage and application speed.




