# Java Strings

## Introduction

A **String** in Java is an object used to store a sequence of characters enclosed in double quotes (`"`). Strings are one of the most commonly used data types in Java and are represented by the `String` class from the `java.lang` package.

### Key Features of Strings

- Stores text as a sequence of Unicode characters (UTF-16 encoding).
- Strings are **immutable**, meaning their value cannot be changed after creation.
- Supports a large number of built-in methods for manipulation and comparison.
- Frequently used for storing names, messages, passwords, file paths, and textual data.

### Real-World Example

- Student Name → `"Akash"`
- Website Name → `"AlphaKnowledge"`
- Email Address → `"support@alphaknowledge.com"`
- Course Name → `"Java Programming"`

### Example

```java
public class Main {
    public static void main(String[] args) {

        String student = "Siddu";
        String platform = "AlphaKnowledge";

        System.out.println(student);
        System.out.println(platform);
    }
}
```

### Output
Siddu
AlphaKnowledge

### Explanation

- `"Siddu"` and `"AlphaKnowledge"` are String literals.
- Strings are enclosed within double quotes.
- Java stores them as String objects.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781689549471-b2a03090-7853-4b83-8404-7d1fa9045016.png)

# Creating Strings in Java

There are two common ways to create Strings.

## 1. String Literal (Recommended)

String literals are stored in the **String Constant Pool**.

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

- String is directly stored in the String Pool.
- Memory efficient because duplicate strings reuse the same object.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781690512577-cc4f0e49-0378-4e37-9b95-6b61d67d6495.png)

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781690585604-949d4482-66cc-442c-9487-de74140e5153.png)

## 2. Using new Keyword

Creates a new object in heap memory.

```java
public class Main {
    public static void main(String[] args) {

        String company = new String("AlphaKnowledge");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

### Explanation

- A new object is created in heap memory.
- Even if the same string already exists in the pool, a new object is created.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781690621737-949d4482-66cc-442c-9487-de74140e5153.png)

# String Literal vs new String()

| Feature | String Literal | new String() |
| --- | --- | --- |
| Memory Location | String Pool | Heap Memory |
| Duplicate Handling | Reuses existing object | Creates new object |
| Memory Efficient | Yes | No |
| Performance | Faster | Slightly Slower |
| Recommended | Yes | Only when required |

### Example

```java
public class Main {
    public static void main(String[] args) {

        String s1 = "Java";
        String s2 = "Java";

        String s3 = new String("Java");
        String s4 = new String("Java");

        System.out.println(s1 == s2);
        System.out.println(s3 == s4);
    }
}
```

### Output
true
false

### Explanation

- `s1` and `s2` point to the same pool object.
- `s3` and `s4` are different heap objects.

# CharSequence Interface

The **CharSequence** interface represents a readable sequence of characters.

### Common Methods

| Method | Description |
| --- | --- |
| length() | Returns length |
| charAt() | Returns character at index |
| subSequence() | Returns part of sequence |
| toString() | Converts to String |

### Classes Implementing CharSequence

| Class | Description |
| --- | --- |
| String | Immutable |
| StringBuilder | Mutable, Faster |
| StringBuffer | Mutable, Thread-Safe |
| StringTokenizer | Tokenizes strings |

# Mutable Strings and Tokenizers (StringBuilder, StringBuffer, StringTokenizer)

Unlike the standard `String` class which creates immutable string objects, Java provides two classes that represent modifiable sequences of characters: `StringBuilder` and `StringBuffer`. In addition, `StringTokenizer` is a utility class used to break strings into tokens.

- **StringBuilder Class:** Used when you need to make frequent modifications to a string. It is **not thread-safe** (non-synchronized), which makes it extremely fast. Preferred for single-threaded operations.
- **StringBuffer Class:** Similar to `StringBuilder`, but it is **thread-safe** (synchronized). Its methods are thread-safe, which introduces slightly more overhead, making it slower than `StringBuilder`.
- **StringTokenizer Class:** A legacy utility class from `java.util` that allows an application to break a string into tokens based on specified delimiters. It is generally recommended to use the `String.split()` method or regular expressions instead of this class in modern Java.

### Comparison Table

| Feature | String | StringBuilder | StringBuffer |
| --- | --- | --- | --- |
| **Mutability** | Immutable | Mutable | Mutable |
| **Thread Safety** | Thread-safe (due to immutability) | Non-thread-safe | Thread-safe (Synchronized methods) |
| **Performance** | Slower (copies string on change) | Fastest | Slower than StringBuilder |
| **Memory Allocation** | String Constant Pool & Heap | Heap only | Heap only |

### Code Example: StringBuilder & StringBuffer

```java
public class Main {
    public static void main(String[] args) {
        // StringBuilder Example
        StringBuilder sb1 = new StringBuilder("Java");
        sb1.append(" Programming"); // Modifies the same object in place
        System.out.println("StringBuilder: " + sb1);

        // StringBuffer Example
        StringBuffer sb2 = new StringBuffer("Java");
        sb2.append(" Security"); // Modifies the same object in place
        System.out.println("StringBuffer: " + sb2);
    }
}
```

### Output
StringBuilder: Java Programming
StringBuffer: Java Security

### Code Example: StringTokenizer

```java
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) {
        String data = "Java,Python,C++,JavaScript";
        StringTokenizer tokenizer = new StringTokenizer(data, ",");

        System.out.println("Tokenizing data:");
        while (tokenizer.hasMoreTokens()) {
            System.out.println("Token: " + tokenizer.nextToken());
        }
    }
}
```

### Output
Tokenizing data:
Token: Java
Token: Python
Token: C++
Token: JavaScript
# Immutable Strings in Java

Strings in Java are immutable.

Once a String object is created, its contents cannot be modified.

## Example

```java
public class Main {
    public static void main(String[] args) {

        String course = "Java";

        course.concat(" Programming");

        System.out.println(course);
    }
}
```

### Output
Java

### Explanation

- `concat()` creates a new String object.
- Original string remains unchanged.

## Updating the String Reference

```java
public class Main {
    public static void main(String[] args) {

        String course = "Java";

        course = course.concat(" Programming");

        System.out.println(course);
    }
}
```

### Output
Java Programming

### Explanation

- The returned String is reassigned.
- Now the variable points to the new object.

# Why Are Strings Immutable?

Java designers made Strings immutable because it improves:

- Security
- Thread Safety
- Caching
- Performance

### Real-World Example

Imagine a website URL:

```java
String url = "https://alphaknowledge.com";
```

If Strings were mutable, any code could modify the URL unexpectedly, causing security risks.

# String Constant Pool (SCP)

The String Constant Pool is a special memory area inside the heap where String literals are stored.

### Example

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

- Only one object is created.
- Both references point to the same object.

# JVM Memory Structure for Strings (Stack vs Heap vs SCP)

Understanding how Java manages strings in memory is crucial for writing efficient applications. The JVM divides memory into the Stack and Heap regions.

- **Stack Memory:** Stores local variables and reference variables. In the statement `String s1 = "Java";`, the reference variable `s1` is created on the Stack.
- **Heap Memory:** Stores all objects created at runtime.
- **String Constant Pool (SCP):** A special memory area within the Heap. Strings created as literals are stored in the SCP.

### Memory Representation

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781690348365-34c801ea-bd50-4e36-a7ec-e7dd57c11356.png)

When you write `String s1 = "Alpha";`, the JVM checks the SCP. If "Alpha" is already present, it returns the reference. Otherwise, it creates a new String in the SCP.
When you write `String s3 = new String("Alpha");`, a new String object is explicitly created in Heap memory outside the SCP, even if the literal "Alpha" already exists in the pool.

### Code Example

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "Alpha";
        String s2 = "Alpha";
        String s3 = new String("Alpha");

        System.out.println(s1 == s2); // true (points to same SCP instance)
        System.out.println(s1 == s3); // false (s3 is a separate heap instance)
    }
}
```

### Output
true
false

### Explanation

- Reference variables `s1`, `s2`, and `s3` are allocated on the Stack.
- `s1` and `s2` point directly to the `"Alpha"` object inside the String Constant Pool.
- `s3` points to a distinct String object in Heap memory, which itself refers to the `"Alpha"` literal in the pool for character data.

# Strings Using new Keyword

```java
public class Main {
    public static void main(String[] args) {

        String s1 = new String("AlphaKnowledge");
        String s2 = new String("AlphaKnowledge");

        System.out.println(s1 == s2);
    }
}
```

### Output
false

### Explanation

- Separate heap objects are created.
- References are different.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-strings/1781690401550-949d4482-66cc-442c-9487-de74140e5153.png)

# intern() Method

The `intern()` method adds a String to the String Pool and returns the pooled reference.

## Example

```java
public class Main {
    public static void main(String[] args) {

        String s1 = new String("Java");
        String s2 = s1.intern();

        String s3 = "Java";

        System.out.println(s2 == s3);
    }
}
```

### Output
true

### Explanation

- `intern()` returns the String Pool reference.
- Both references now point to the same pooled object.

# String Pool Migration

## Before Java 7

- String Pool stored in PermGen Memory.
- Limited memory size.

## Java 7 and Later

- String Pool moved to Heap Memory.
- Better memory management.
- Improved scalability.

# Creating Strings Using Character Array

```java
public class Main {
    public static void main(String[] args) {

        char[] letters = {'J', 'a', 'v', 'a'};

        String str = new String(letters);

        System.out.println(str);
    }
}
```

### Output
Java

### Explanation

- Character array is converted into a String object.

# Creating Strings Using Byte Array

```java
public class Main {
    public static void main(String[] args) {

        byte[] values = {65, 66, 67};

        String str = new String(values);

        System.out.println(str);
    }
}
```

### Output
ABC

### Explanation

- ASCII values are converted into characters.
- 65 → A
- 66 → B
- 67 → C

# Creating Strings from Another String

Java allows you to initialize a new String object using an existing String object. This creates a duplicate copy of the original string in Heap memory.

### Code Example

```java
public class Main {
    public static void main(String[] args) {
        String original = "Java";
        String duplicate = new String(original);

        System.out.println("Original: " + original);
        System.out.println("Duplicate: " + duplicate);
        System.out.println("Equal contents? " + original.equals(duplicate));
        System.out.println("Same object reference? " + (original == duplicate));
    }
}
```

### Output
Original: Java
Duplicate: Java
Equal contents? true
Same object reference? false

### Explanation

- `original` points to the literal `"Java"` in the String Constant Pool.
- `new String(original)` creates a completely new String object in the Heap area containing a copy of the same characters.
- Because they are in different memory addresses, reference comparison `==` returns `false`, while value comparison `equals()` returns `true`.

# Important String Methods

| Method | Description |
| --- | --- |
| length() | Returns string length |
| charAt() | Returns character at index |
| substring() | Extracts part of string |
| concat() | Joins strings |
| equals() | Compares contents |
| equalsIgnoreCase() | Case-insensitive comparison |
| toUpperCase() | Converts to uppercase |
| toLowerCase() | Converts to lowercase |
| trim() | Removes extra spaces |
| replace() | Replaces characters |
| contains() | Checks substring |
| startsWith() | Checks prefix |
| endsWith() | Checks suffix |

# Example of Common String Methods

```java
public class Main {
    public static void main(String[] args) {

        String platform = "AlphaKnowledge";

        System.out.println(platform.length());
        System.out.println(platform.toUpperCase());
        System.out.println(platform.contains("Knowledge"));
        System.out.println(platform.substring(5));
    }
}
```

### Output
14
ALPHAKNOWLEDGE
true
Knowledge
# Advantages of Strings

- Easy to use.
- Immutable and secure.
- Rich built-in API.
- Supports Unicode characters.
- Efficient memory usage through String Pool.

# Limitations of Strings

- Immutable nature may create extra objects.
- Frequent modifications can reduce performance.
- For heavy modifications, StringBuilder is preferred.

# Interview Questions

| Question | Answer |
| --- | --- |
| Are Strings objects in Java? | Yes |
| Are Strings immutable? | Yes |
| Where are String literals stored? | String Constant Pool |
| Which method adds String to pool? | intern() |
| Which is faster: StringBuilder or String? | StringBuilder for modifications |
| Does new String() create a new object every time? | Yes |
| What encoding is used by Java Strings? | UTF-16 |

# Summary

A String in Java represents a sequence of Unicode characters stored using UTF-16 encoding. Strings are immutable objects, meaning their values cannot be altered after creation. String literals are stored in the String Constant Pool (SCP) to optimize memory reuse, while using the `new` keyword allocates distinct objects directly in heap memory. The `intern()` method allows developers to fetch or store references dynamically in the SCP. While the Java String class provides a rich set of built-in manipulation methods, frequent string modifications can create excessive objects and degrade performance, making `StringBuilder` or `StringBuffer` the preferred choice for heavy string modifications.




