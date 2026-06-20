# String vs StringBuilder vs StringBuffer in Java

## Introduction

Java provides three important classes for handling textual data:

1. **String**
2. **StringBuilder**
3. **StringBuffer**

All three are used to store and manipulate sequences of characters, but they differ significantly in terms of mutability, performance, memory usage, and thread safety.

Choosing the correct class can greatly improve application performance and memory efficiency.

# String Class

A **String** is an immutable sequence of characters.

Once a String object is created, its content cannot be modified. Any operation that appears to modify a string actually creates a new String object.

## Example

```java
public class Main {
    public static void main(String[] args) {

        String course = "AlphaKnowledge";

        course.concat(" Java");

        System.out.println(course);
    }
}
```

### Output
AlphaKnowledge

### Explanation

The `concat()` method creates a new string object:

```text
AlphaKnowledge Java
```

However, this new object is not assigned back to the variable, so the original string remains unchanged.

Because Strings are immutable, modifications always create new objects.

## String Memory Example

```java
public class Main {
    public static void main(String[] args) {

        String name = "Mohit";

        name = name + " Kumar";

        System.out.println(name);
    }
}
```

### Output
Mohit Kumar

### Internally

```text
Object 1 → Mohit
Object 2 → Mohit Kumar
```

A new object is created after modification.

## Advantages of String

- Immutable and secure
- Thread-safe
- Supports String Pool optimization
- Easy to use
- Suitable for constant text

## Limitations of String

- Creates new objects for every modification
- Higher memory consumption
- Slower for repeated concatenation

# StringBuilder Class

`StringBuilder` is a mutable sequence of characters introduced in Java 5.

Unlike String, it modifies the existing object instead of creating new objects.

It is designed for high-performance string manipulation in single-threaded applications.

## Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder("AlphaKnowledge");

        sb.append(" Java");

        System.out.println(sb);
    }
}
```

### Output
AlphaKnowledge Java

### Explanation

The `append()` method directly modifies the existing object.

No new object is created.

## Example: Building Student Information

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        sb.append("Name: Mohit");
        sb.append(", Branch: CSE");
        sb.append(", College: AlphaKnowledge Academy");

        System.out.println(sb);
    }
}
```

### Output
Name: Mohit, Branch: CSE, College: AlphaKnowledge Academy

## Advantages of StringBuilder

- Mutable
- Fast execution
- Memory efficient
- Ideal for loops
- No synchronization overhead

## Limitations of StringBuilder

- Not thread-safe
- Cannot be safely shared across threads

# StringBuffer Class

`StringBuffer` is also a mutable sequence of characters.

It works similarly to StringBuilder but provides thread safety through synchronization.

It is suitable for multithreaded applications.

## Example

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer("AlphaKnowledge");

        sb.append(" Java");

        System.out.println(sb);
    }
}
```

### Output
AlphaKnowledge Java

### Explanation

The `append()` method modifies the existing object.

Unlike StringBuilder, all operations are synchronized, making it safe for multiple threads.

## Example: Employee Information

```java
public class Main {
    public static void main(String[] args) {

        StringBuffer sb =
                new StringBuffer();

        sb.append("Employee: Akash");
        sb.append(", Department: Development");
        sb.append(", Company: AlphaKnowledge");

        System.out.println(sb);
    }
}
```

### Output
Employee: Akash, Department: Development, Company: AlphaKnowledge

# Object Creation Comparison

## String

```java
String s = "Java";
s += " Programming";
s += " Language";
```

### Internally

```text
Object 1 → Java
Object 2 → Java Programming
Object 3 → Java Programming Language
```

Three objects are created.

## StringBuilder

```java
StringBuilder sb =
        new StringBuilder("Java");

sb.append(" Programming");
sb.append(" Language");
```

### Internally

```text
Single object modified repeatedly
```

Only one object is used.

## StringBuffer

```java
StringBuffer sb =
        new StringBuffer("Java");

sb.append(" Programming");
sb.append(" Language");
```

### Internally

```text
Single synchronized object modified repeatedly
```

Only one object is used.

# Performance Example

## Using String

```java
public class Main {
    public static void main(String[] args) {

        String str = "";

        for(int i = 1; i <= 1000; i++) {
            str += i;
        }

        System.out.println("Done");
    }
}
```

Creates thousands of temporary objects.

## Using StringBuilder

```java
public class Main {
    public static void main(String[] args) {

        StringBuilder sb =
                new StringBuilder();

        for(int i = 1; i <= 1000; i++) {
            sb.append(i);
        }

        System.out.println("Done");
    }
}
```

Much faster because the same object is reused.

# When Should You Use Which?

## Use String When

- Text will not change frequently
- Constants are required
- Configuration values
- Names, IDs, fixed messages

### Example

```java
String company = "AlphaKnowledge";
```

## Use StringBuilder When

- Frequent modifications are required
- Single-threaded applications
- Loops with repeated concatenation

### Example

```java
StringBuilder report =
        new StringBuilder();
```

## Use StringBuffer When

- Multiple threads access the same object
- Thread safety is required
- Concurrent applications

### Example

```java
StringBuffer sharedData =
        new StringBuffer();
```

# String vs StringBuilder vs StringBuffer

| Feature | String | StringBuilder | StringBuffer |
| --- | --- | --- | --- |
| Mutability | Immutable | Mutable | Mutable |
| Object Creation | Creates new objects | Modifies existing object | Modifies existing object |
| Thread Safety | Yes (Immutable) | No | Yes |
| Synchronization | Not Required | No | Yes |
| Performance | Slowest | Fastest | Moderate |
| Memory Usage | Highest | Lowest | Low |
| Suitable for Loops | No | Yes | Yes |
| Multi-threading | Safe | Unsafe | Safe |
| Introduced In | Java 1.0 | Java 5 | Java 1.0 |
| Best Use Case | Fixed Text | Single-threaded Updates | Multi-threaded Updates |

# Quick Comparison Table

| Requirement | Recommended Class |
| --- | --- |
| Constant Text | String |
| Frequent Concatenation | StringBuilder |
| High Performance | StringBuilder |
| Thread Safety | StringBuffer |
| Shared Data Between Threads | StringBuffer |
| Memory Optimization | StringBuilder |
| Immutable Data | String |

# Summary

Java provides three major classes for text manipulation: **String**, **StringBuilder**, and **StringBuffer**. A String is immutable and best suited for fixed data that does not change. StringBuilder is mutable, fast, and ideal for single-threaded applications that require frequent modifications. StringBuffer is also mutable but synchronized, making it suitable for multithreaded environments where thread safety is important. In modern Java applications, StringBuilder is generally preferred for most dynamic string operations, while String should be used for constant text and StringBuffer only when synchronization is required.




