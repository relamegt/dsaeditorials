# String Class in Java

## Introduction

The `String` class in Java is used to store and manipulate textual data. A string represents a sequence of Unicode characters enclosed within double quotation marks.

Strings are among the most frequently used objects in Java applications, including web development, mobile applications, databases, and software systems.

### Key Features

- Stores text using Unicode characters.
- Immutable in nature.
- Stored in the String Pool for memory optimization.
- Thread-safe due to immutability.
- Provides numerous built-in methods for string manipulation.
- Part of the `java.lang` package.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

# Creating Strings in Java

There are two common ways to create strings.

## 1. Using String Literal

String literals are stored in the String Constant Pool.

```java
String company = "AlphaKnowledge";
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

### Explanation

The JVM first checks the String Pool. If the string already exists, the existing object is reused instead of creating a new one.

## 2. Using new Keyword

Using `new` creates a separate object in heap memory.

```java
String company =
        new String("AlphaKnowledge");
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company =
            new String("AlphaKnowledge");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

### Explanation

A new object is always created in heap memory even if the same text already exists in the String Pool.

# String Constant Pool (SCP)

The **String Constant Pool (SCP)**, also known as the String Pool, is a special cached memory area inside the Java Heap. It is used by the JVM to store String objects created as literals.

## Detailed Explanation of String Literal Storage

When a String literal is created:

1. The JVM checks the String Constant Pool.
2. If the string value already exists in the pool, the JVM returns a reference to the existing pooled instance.
3. If the string value does not exist, a new String object is instantiated in the pool, and its reference is returned.

This reuse of instances avoids creating duplicate String objects with the same character sequence.

### Example: Literal Sharing

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "AlphaKnowledge";
        String s2 = "AlphaKnowledge";
        System.out.println(s1 == s2);
    }
}
```

### Output
true

### Explanation

Only one String object is created in the SCP. Both `s1` and `s2` reference the same object, so the reference comparison `==` returns `true`.

## Heap vs String Pool

Understanding the difference between the general Heap memory and the String Constant Pool is crucial:

| Feature | general Heap memory | String Constant Pool (SCP) |
| --- | --- | --- |
| **Object Creation** | `new String("value")` always creates a new object. | String literals reuse existing objects. |
| **Location** | Part of general Heap memory. | Special cached area within Heap memory (Java 7+). |
| **Duplicate Objects** | Allows duplicates of same value. | No duplicate values allowed. |
| **Garbage Collection** | Standard garbage collection rules apply. | Garbage collected less frequently, optimized for persistence. |

## Memory Optimization

The primary purpose of the String Pool is memory optimization:

- **Reduces Memory Footprint**: Since strings are immutable and heavily used, reusing identical string literals saves significant heap memory.
- **Reduces Garbage Collection Overhead**: Fewer objects are allocated, which reduces the frequency and duration of garbage collection cycles, boosting application performance.

## String Creation Methods

Let's compare the memory allocation of two different creation methods:

### Method 1: String s1 = "AlphaKnowledge";

- The JVM searches the SCP for `"AlphaKnowledge"`.
- If found, it references the existing object.
- If not found, it creates one object in the SCP.
- **Objects Created**: 0 or 1.

### Method 2: String s2 = new String("AlphaKnowledge");

- The `new` keyword explicitly allocates a new String object in the general Heap memory.
- In addition, the literal `"AlphaKnowledge"` is checked against the SCP; if it is not in the SCP, a new object is also created in the SCP.
- **Objects Created**: 1 or 2.

### Memory Representation

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/string-class-in-java/1781861357945-8d5095c5-68ee-4b67-af20-3fe355719c49.png)

### Code Example: Creation Methods Comparison

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "AlphaKnowledge";
        String s2 = new String("AlphaKnowledge");
        System.out.println(s1 == s2);
    }
}
```

### Output
false

### Explanation

- `s1` references the object inside the String Constant Pool.
- `s2` references a completely separate object in general Heap memory.
- Since they point to different memory addresses, `s1 == s2` is `false`.

# Key Feature 1: Immutability

A String object cannot be modified after creation.

Whenever a modification appears to happen, Java creates a new String object instead.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company =
                "Alpha";

        company.concat("Knowledge");

        System.out.println(company);
    }
}
```

### Output
Alpha

### Explanation

`concat()` creates a new string object.

Since the new object is not assigned back, the original string remains unchanged.

## Correct Way

```java
public class Main {

    public static void main(String[] args) {

        String company =
                "Alpha";

        company =
            company.concat("Knowledge");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

# Key Feature 2: Thread Safety

Strings are naturally thread-safe because they cannot be modified.

Multiple threads can safely access the same String object without synchronization.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company =
                "AlphaKnowledge";

        Runnable task = () ->
            System.out.println(company);

        new Thread(task).start();
        new Thread(task).start();
    }
}
```

### Output
AlphaKnowledge
AlphaKnowledge

### Explanation

Both threads safely access the same String object.

# Key Feature 3: Utility Methods

The String class contains many built-in methods.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company =
                "AlphaKnowledge";

        System.out.println(
            company.length());

        System.out.println(
            company.toUpperCase());
    }
}
```

### Output
14
ALPHAKNOWLEDGE

# Key Feature 4: Implemented Interfaces

The `String` class implements several important interfaces that define its behavior in the Java ecosystem.

## 1. CharSequence Interface

The `CharSequence` interface represents a readable, uniform sequence of character values.

- **Purpose**: It provides a unified, read-only interface for different types of character sequences.
- **Common Methods**:
- `length()`: Returns the number of characters.
- `charAt(int index)`: Returns the character at the specified index.
- `subSequence(int start, int end)`: Returns a new `CharSequence` that is a subsequence of this sequence.
- `toString()`: Returns a string containing the characters in this sequence.

| Implementing Class | Mutability | Thread Safety |
| --- | --- | --- |
| `String` | Immutable | Thread-Safe |
| `StringBuilder` | Mutable | Non-Thread-Safe (Faster) |
| `StringBuffer` | Mutable | Thread-Safe (Synchronized) |

## 2. Comparable&lt;String&gt; Interface

The `Comparable<String>` interface is used to order the objects of user-defined classes.

- **Purpose**: It allows objects to be compared lexicographically (alphabetically).
- **Key Method**: `compareTo(String anotherString)` compares two strings lexicographically based on the Unicode value of each character. It returns:
- A negative integer if this string lexicographically precedes the argument string.
- Zero if the strings are equal.
- A positive integer if this string lexicographically follows the argument string.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String company = "AlphaKnowledge";
        System.out.println(company.compareTo("BetaKnowledge"));
    }
}
```

### Output
Negative Value

### Explanation

Alphabetically `"AlphaKnowledge"` comes before `"BetaKnowledge"`, so a negative value is returned.

## 3. Serializable Interface

The `Serializable` interface is a marker interface (no methods) belonging to the `java.io` package.

- **Purpose**: It enables JVM to convert a String object into a sequence of bytes (Serialization) so it can be saved to a file, database, or sent over a network. It also allows restoring the byte stream back to a String object (Deserialization).

# String Constructors

Java provides multiple constructors for creating strings from different sources.

## Constructor Using String

```java
public class Main {

    public static void main(String[] args) {

        String company =
            new String("AlphaKnowledge");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

## Constructor Using Character Array

```java
public class Main {

    public static void main(String[] args) {

        char[] arr =
        {'A','l','p','h','a'};

        String company =
            new String(arr);

        System.out.println(company);
    }
}
```

### Output
Alpha

## Constructor Using Byte Array

```java
public class Main {

    public static void main(String[] args) {

        byte[] arr =
        {65,108,112,104,97};

        String company =
            new String(arr);

        System.out.println(company);
    }
}
```

### Output
Alpha

# Commonly Used String Constructors

| Constructor | Description |
| --- | --- |
| `String()` | Creates an empty String object. |
| `String(String original)` | Creates a new String representing the same sequence of characters as the argument. |
| `String(char[] value)` | Allocates a new String representing the character sequence currently contained in the character array. |
| `String(char[] value, int offset, int count)` | Allocates a new String containing characters from a subarray of the character array. |
| `String(byte[] bytes)` | Constructs a new String by decoding the specified byte array using the platform's default charset. |
| `String(byte[] bytes, Charset charset)` | Constructs a new String by decoding the specified byte array using the specified Charset. |
| `String(byte[] bytes, int offset, int length)` | Constructs a new String by decoding the specified byte subarray using the platform's default charset. |
| `String(StringBuilder builder)` | Allocates a new String containing the sequence of characters currently in the StringBuilder. |
| `String(StringBuffer buffer)` | Allocates a new String containing the sequence of characters currently in the StringBuffer. |

# Summary

The String class is one of the most important classes in Java and is used to store textual information. Strings are immutable, thread-safe, and optimized through the String Pool mechanism. Java provides multiple constructors and numerous built-in methods that make text processing simple and efficient. Understanding the String class is essential because it is heavily used in real-world applications such as web development, APIs, databases, file handling, and software systems.




