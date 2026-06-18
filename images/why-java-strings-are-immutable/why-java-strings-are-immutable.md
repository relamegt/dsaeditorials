# Why Java Strings are Immutable?

## Introduction

In JAVA **String** in Java is immutable, which means once a String object is created, its value cannot be changed. Any operation that appears to modify a String actually creates a new String object.

Immutability is one of the most important features of Java Strings and is responsible for better security, memory optimization, thread safety, and performance.

### Key Points

- Strings cannot be modified after creation.
- Modification operations create new String objects.
- String Pool optimization is possible because Strings are immutable.
- Multiple threads can safely share the same String object.

Suppose AlphaKnowledge stores its website name in a String.

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        company.concat(" Learning Platform");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

## Explanation

- Initially, `company` points to `"AlphaKnowledge"`.
- `concat()` creates a new String `"AlphaKnowledge Learning Platform"`.
- The original String remains unchanged.
- Since the new String is not assigned back, it is discarded.
- Therefore the output remains `"AlphaKnowledge"`.

### Memory Representation

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/why-java-strings-are-immutable/1781780303459-d2f5a970-cd5e-43bc-ba78-536330b82c03.png)

### 

# How to Modify a String?

Since Strings are immutable, modifications require assigning the result back to a variable.

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        company = company.concat(" Learning Platform");

        System.out.println(company);
    }
}
```

## Output

AlphaKnowledge Learning Platform

## Explanation

- `concat()` creates a new String.
- The reference variable is updated.
- Now `company` points to the new String object.

# Why Did Java Make Strings Immutable?

Java designers intentionally made Strings immutable for several reasons.

## 1. Security

Strings are widely used for storing:

- Passwords
- Database URLs
- API Keys
- File Paths
- Website URLs

### Example

```java
String website =
"https://alphaknowledge.in";
```

If Strings were mutable, any code could modify this URL after validation.

```java
website = "https://fakewebsite.com";
```

This could create serious security issues.

### Benefits

- Protects sensitive information.
- Prevents accidental modifications.
- Makes applications more secure.

## 2. String Pool Optimization

Java stores String literals in a special memory area called the **String Constant Pool**.

### Example

```java
String s1 = "AlphaKnowledge";
String s2 = "AlphaKnowledge";
```

### 

Because Strings are immutable, both variables can safely share the same object.

### Benefits

- Saves memory.
- Reduces duplicate objects.
- Improves JVM performance.

## 3. Thread Safety

Imagine multiple users accessing AlphaKnowledge simultaneously.

```java
String platform = "AlphaKnowledge";
```

Thread 1:

```java
System.out.println(platform);
```

Thread 2:

```java
System.out.println(platform);
```

Both threads safely use the same String object.

### Why?

Because no thread can modify it.

### Benefits

- No synchronization required.
- Faster execution.
- Safe sharing across threads.

## 4. HashCode Caching

Strings are frequently used as keys in collections.

### Example

```java
HashMap<String, Integer> courses =
new HashMap<>();

courses.put("Java", 1200);
```

HashMap relies heavily on hash codes.

Since Strings are immutable:

- HashCode never changes.
- Java computes it once and reuses it.

### Benefits

- Faster searching.
- Better HashMap performance.
- Efficient retrieval operations.

## 5. Better Memory Management

Immutable Strings can be reused safely.

### Example

```java
String s1 = "AlphaKnowledge";
String s2 = "AlphaKnowledge";
String s3 = "AlphaKnowledge";
```

Only one String object exists in memory.

### Benefits

- Less memory consumption.
- Reduced garbage collection.
- Better JVM optimization.

# Real-World Example

Suppose AlphaKnowledge stores its support email.

```java
String email =
"support@alphaknowledge.com";
```

Many parts of the application may use this email:

- Contact Page
- Feedback Module
- Notification System
- Help Desk

Since Strings are immutable:

- No module can accidentally modify the email.
- All modules always receive the correct value.

# Example Showing New Object Creation

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        String updated =
            company.concat(" Academy");

        System.out.println(company);
        System.out.println(updated);
    }
}
```

## Output

AlphaKnowledge
AlphaKnowledge Academy

## Explanation

Two separate String objects exist:

```text
company  ─► AlphaKnowledge

updated  ─► AlphaKnowledge Academy
```

The original object remains unchanged.

# String Pool Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "AlphaKnowledge";
        String s2 = "AlphaKnowledge";

        System.out.println(s1 == s2);
    }
}
```

## Output

true

## Explanation

Both references point to the same pooled object.

# Using new Keyword

```java
public class Main {

    public static void main(String[] args) {

        String s1 =
            new String("AlphaKnowledge");

        String s2 =
            new String("AlphaKnowledge");

        System.out.println(s1 == s2);
    }
}
```

## Output

false

## Explanation

Each `new String()` creates a separate heap object.

# Advantages of Immutable Strings

| Advantage | Description |
| --- | --- |
| Security | Protects sensitive information |
| Thread Safety | Safe for concurrent access |
| String Pooling | Allows object reuse |
| HashCode Caching | Improves collection performance |
| Reliability | Values remain constant |
| Easy Sharing | Same object can be reused safely |

# Disadvantages of Immutable Strings

| Disadvantage | Description |
| --- | --- |
| Extra Objects | Every modification creates a new object |
| Higher Memory Usage | Frequent modifications create temporary objects |
| Slower Updates | Repeated modifications reduce performance |

# String vs StringBuilder

| Feature | String | StringBuilder |
| --- | --- | --- |
| Mutable | No | Yes |
| Thread Safe | Yes (Immutable) | No |
| Modification Speed | Slower | Faster |
| Memory Efficient for Updates | No | Yes |
| Best Use Case | Fixed Text | Frequently Changing Text |

# Example: StringBuilder

Suppose AlphaKnowledge updates course details repeatedly.

```java
public class Main {

    public static void main(String[] args) {

        StringBuilder course =
            new StringBuilder("Java");

        course.append(" Programming");
        course.append(" Course");

        System.out.println(course);
    }
}
```

## Output

Java Programming Course

## Explanation

- StringBuilder modifies the same object.
- No additional String objects are created.
- More efficient for repeated modifications.

# Interview Questions

| Question | Answer |
| --- | --- |
| What is immutability? | Object cannot be modified after creation |
| Are Java Strings immutable? | Yes |
| Why are Strings immutable? | Security, Thread Safety, Pooling, Performance |
| Does concat() modify the original String? | No |
| Which class is used for mutable strings? | StringBuilder |
| Where are String literals stored? | String Constant Pool |
| Can multiple references share one String object? | Yes |
| Why is String used as HashMap key? | Because its hash code remains constant |

- # Summar

Java Strings are immutable objects whose contents cannot be changed after creation, meaning any modification operation dynamically creates a new String object. This immutability allows for memory optimization through the String Constant Pool, where literals can be shared safely across references. In addition, immutable Strings enhance security, ensure thread safety without synchronization, and improve performance for HashMap operations by caching hash codes. For applications requiring frequent string updates, using mutable classes like `StringBuilder` is recommended to prevent excessive object allocation.ng.afety, memory management, and HashMap performance.

- String literals are shared safely through the String Constant Pool.
- For frequent modifications, use **StringBuilder** instead of String.




