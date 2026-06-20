# StringBuilder Class in Java

## Introduction

`StringBuilder` is a mutable sequence of characters available in the `java.lang` package. Unlike the `String` class, which creates a new object whenever its content is modified, `StringBuilder` allows direct modification of the existing object.

It is designed for high-performance string manipulation in single-threaded applications. Whenever a program performs frequent operations such as concatenation, insertion, deletion, or replacement of text, `StringBuilder` is generally preferred over `String`.

### Key Features

- Mutable sequence of characters
- Faster than String for repeated modifications
- Does not create new objects during updates
- Not synchronized (not thread-safe)
- More efficient than StringBuffer in single-threaded applications
- Automatically expands its capacity when required
- Available in the `java.lang` package

# Why StringBuilder?

## Problem with String

When using String objects, every modification creates a new object.

### Example

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

### Memory Usage

```text
Object 1 -> AlphaKnowledge
Object 2 -> AlphaKnowledge Java
Object 3 -> AlphaKnowledge Java Programming
Object 4 -> AlphaKnowledge Java Programming Course
```

Multiple objects are created unnecessarily.

## Solution Using StringBuilder

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb = new StringBuilder();

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
Only one object is modified repeatedly.

# Hierarchy of StringBuilder

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stringbuilder-class-in-java/1781931233458-6ec6ac0c-3e74-42c6-8b96-59bae3813a28.png)

### Interfaces Implemented

- Serializable
- CharSequence

# Constructors of StringBuilder

StringBuilder provides multiple constructors for different situations.

## 1. StringBuilder()

Creates an empty StringBuilder with default capacity 16.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        sb.append("Mohit");

        System.out.println(sb);
    }
}
```

### Output
Mohit

## 2. StringBuilder(int capacity)

Creates an empty StringBuilder with specified capacity.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder(50);

        sb.append("AlphaKnowledge");

        System.out.println(sb);
        System.out.println(sb.capacity());
    }
}
```

### Output
AlphaKnowledge
50

## 3. StringBuilder(String str)

Creates a StringBuilder initialized with a String.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Java");

        sb.append(" Programming");

        System.out.println(sb);
    }
}
```

### Output
Java Programming

## 4. StringBuilder(CharSequence cs)

Creates a StringBuilder from a CharSequence.

### Example

```java
public class Main {
    public static void main(String[] args) {

        CharSequence cs =
                "AlphaKnowledge";

        StringBuilder sb =
                new StringBuilder(cs);

        sb.append(" Academy");

        System.out.println(sb);
    }
}
```

### Output
AlphaKnowledge Academy

# Capacity of StringBuilder

Capacity indicates how many characters can be stored before memory expansion occurs.

### Formula

```text
New Capacity = (Old Capacity × 2) + 2
```

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        System.out.println(sb.capacity());

        sb.append("Java");

        System.out.println(sb.capacity());

        sb.append(" Programming Language Course For Beginners");

        System.out.println(sb.capacity());
    }
}
```

### Output
16
16
34

# Commonly Used Methods

## 1. append()

Adds text at the end.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Mohit");

        sb.append(" Kumar");

        System.out.println(sb);
    }
}
```

### Output
Mohit Kumar

## 2. insert()

Inserts text at a specific position.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Akash");

        sb.insert(5, " Kumar");

        System.out.println(sb);
    }
}
```

### Output
Akash Kumar

## 3. replace()

Replaces characters between indexes.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Mohit");

        sb.replace(0, 5, "Hemesh");

        System.out.println(sb);
    }
}
```

### Output
Hemesh

## 4. delete()

Deletes a range of characters.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        sb.delete(5, 14);

        System.out.println(sb);
    }
}
```

### Output
Alpha

## 5. deleteCharAt()

Deletes a single character.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Abhiram");

        sb.deleteCharAt(2);

        System.out.println(sb);
    }
}
```

### Output
Abiram

## 6. reverse()

Reverses the string.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Mohit");

        sb.reverse();

        System.out.println(sb);
    }
}
```

### Output
tihoM

## 7. length()

Returns total number of characters.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        System.out.println(sb.length());
    }
}
```

### Output
14

## 8. capacity()

Returns current capacity.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        System.out.println(sb.capacity());
    }
}
```

### Output
16

## 9. charAt()

Returns character at specified index.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        System.out.println(sb.charAt(0));
    }
}
```

### Output
A

## 10. setCharAt()

Changes a character at a specific index.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Mohit");

        sb.setCharAt(0, 'R');

        System.out.println(sb);
    }
}
```

### Output
Rohit

## 11. substring()

Extracts part of a string.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        System.out.println(
                sb.substring(5));
    }
}
```

### Output
Knowledge

## 12. ensureCapacity()

Ensures minimum capacity.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        sb.ensureCapacity(100);

        System.out.println(sb.capacity());
    }
}
```

### Output
100

## 13. indexOf()

Returns first occurrence of a substring.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        System.out.println(
                sb.indexOf("Know"));
    }
}
```

### Output
5

## 14. lastIndexOf()

Returns last occurrence of a substring.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("Java Java Java");

        System.out.println(
                sb.lastIndexOf("Java"));
    }
}
```

### Output
10

## 15. toString()

Converts StringBuilder to String.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        String str = sb.toString();

        System.out.println(str);
    }
}
```

### Output
AlphaKnowledge

## 16. trimToSize()

Reduces unused memory allocation.

### Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder(100);

        sb.append("Java");

        sb.trimToSize();

        System.out.println(sb.capacity());
    }
}
```

### Output
4

# Additional Important Methods

| Method | Description |
| --- | --- |
| append() | Adds text at the end |
| insert() | Inserts text at specified index |
| replace() | Replaces characters |
| delete() | Removes characters |
| deleteCharAt() | Removes a single character |
| reverse() | Reverses the sequence |
| length() | Returns length |
| capacity() | Returns capacity |
| charAt() | Returns character at index |
| setCharAt() | Updates character |
| substring() | Extracts substring |
| ensureCapacity() | Ensures minimum capacity |
| indexOf() | Finds first occurrence |
| lastIndexOf() | Finds last occurrence |
| toString() | Converts to String |
| trimToSize() | Reduces unused capacity |

# StringBuilder vs String

| Feature | String | StringBuilder |
| --- | --- | --- |
| Mutable | No | Yes |
| Object Creation | Creates new objects | Modifies existing object |
| Performance | Slower | Faster |
| Memory Usage | Higher | Lower |
| Suitable For | Fixed text | Dynamic text |

# StringBuilder vs StringBuffer

| Feature | StringBuilder | StringBuffer |
| --- | --- | --- |
| Thread Safe | No | Yes |
| Synchronization | No | Yes |
| Performance | Faster | Slower |
| Single Threaded Programs | Best Choice | Good |
| Multi Threaded Programs | Not Recommended | Best Choice |

# Advantages of StringBuilder

1. Faster string manipulation.
2. Memory efficient.
3. No unnecessary object creation.
4. Ideal for loops and repeated concatenation.
5. Automatically expands capacity.
6. Simple and easy to use.
7. Better performance than StringBuffer.

# Limitations of StringBuilder

1. Not thread-safe.
2. Cannot be safely shared across multiple threads.
3. Requires external synchronization in multithreaded applications.
4. Less suitable than StringBuffer when thread safety is required.

# Summary

StringBuilder is a mutable and high-performance class used for efficient string manipulation in Java. It allows modifications without creating new objects, making it significantly faster than String when performing repeated updates. Because it is not synchronized, it provides better performance than StringBuffer in single-threaded applications. Common methods such as append(), insert(), replace(), delete(), reverse(), substring(), and toString() make StringBuilder one of the most important classes for dynamic text processing in Java.




