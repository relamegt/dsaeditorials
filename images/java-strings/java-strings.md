# Java Strings

A `String` in Java is an object used to store a sequence of characters enclosed in double quotes. Java strings use UTF-16 encoding and provide methods for handling text data.

- Each character in a string is stored using 16-bit Unicode (UTF-16) encoding.
- Strings are immutable, meaning their value cannot be changed after creation.
- Java provides a rich API for manipulation, comparison, and concatenation of strings.

### Example

```java
public class Main {
    public static void main(String args[]) {
        String name = "AlphaKnowledge";
        String num = "1234";
        String str = new String("AlphaKnowledge");

        System.out.println(name);
        System.out.println(num);
        System.out.println(str);
    }
}
```

### Output
AlphaKnowledge
1234
AlphaKnowledge

## Ways of Creating a Java String

There are two ways to create a string in Java.

### 1. String literal

A string literal is written directly inside double quotes. This helps Java reuse existing string objects when possible.

### Example

```java
String str = "AlphaKnowledge";
```

### 2. Using new keyword

Using the `new` keyword creates a new object in heap memory, even if the same string already exists in the pool.

- One object is created in heap memory.
- The string literal is stored in the string pool if not already present.
- The reference variable points to the heap object, not the pool.

### Example

```java
String str = new String("AlphaKnowledge");
```

## Interfaces and Classes in Strings in Java

## CharSequence Interface

`CharSequence` is used for representing a sequence of characters in Java. It provides basic methods such as `length()`, `charAt()`, `subSequence()`, and `toString()`.

Classes that implement `CharSequence` include `String`, `StringBuffer`, `StringBuilder`, and `StringTokenizer`.

### 1. String

`String` is an immutable class in Java, which means that once a `String` object is created, its value cannot be changed. If you want to modify a string, a new `String` object is created and the original remains unchanged.

### Syntax

```java
String str = "alphaknowledge";
String str2 = new String("alphaknowledge");
```

### 2. StringBuffer

`StringBuffer` is a mutable class. It is thread safe and is used in multithreaded environments where one object is shared among multiple threads. Because it is synchronized, it has extra overhead.

### Syntax

```java
StringBuffer demoString = new StringBuffer("AlphaKnowledge");
```

### 3. StringBuilder

`StringBuilder` is an alternative to `String` and `StringBuffer`. It creates a mutable sequence of characters and is not thread safe. It is mainly used for single-threaded programs.

### Syntax

```java
StringBuilder demoString = new StringBuilder();
demoString.append("AlphaKnowledge");
```

### 4. StringTokenizer

`StringTokenizer` is used to break a string into tokens.

A `StringTokenizer` object internally maintains a current position within the string to be tokenized. Some operations advance this current position past the characters processed. A token is returned by taking a substring of the string that was used to create the `StringTokenizer` object.

### Syntax

```java
StringTokenizer st = new StringTokenizer("Java String Example");
```

## Immutable String in Java

In Java, string objects are immutable. Immutable simply means unmodifiable or unchangeable. Once a string object is created, its data or state cannot be changed, but a new string object is created.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String s = "Akash";

        s.concat(" Mohit");

        System.out.println(s);
    }
}
```

### Output
Akash

Here, `Akash` is not changed, but a new object is created with `Akash Mohit`. That is why a string is known as immutable.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String name = "Akash";
        name = name.concat(" Mohit");
        System.out.println(name);
    }
}
```

### Output
Akash Mohit

## How Strings are Stored in Java Memory

## String literal

Whenever a `String` object is created as a literal, the object is created in the string constant pool. This allows JVM to optimize the initialization of string literals. The string constant pool is present in the heap.

### Example 1

```java
String str1 = "Hello";
```

### Example 2

```java
String str1 = "Hello";
String str2 = "Hello";
```

## Using new Keyword

Strings can also be created using the `new` keyword, which allocates a new object in heap memory. However, the string literal inside it is still stored in the String Constant Pool if not already present.

### Example 1

```java
String str1 = new String("Akash");
String str2 = new String("Mohit");
```

The `intern()` method returns a reference from the string constant pool. If the string is not already present in the pool, it is added. Otherwise, the existing reference from the pool is returned.

### Example 2

```java
String internedString = demoString.intern();
```

It is preferred to use string literals as it allows JVM to optimize memory allocation.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String name = "AlphaKnowledge";
        String newString = new String("AlphaKnowledge");

        System.out.println("String name = " + name);
        System.out.println("String newString = " + newString);
    }
}
```

### Output
String name = AlphaKnowledge
String newString = AlphaKnowledge

**Note:** All `String` objects are stored in heap memory. The String Constant Pool is a special area inside the heap used to store unique string literals.

## String Pool Migration from PermGen to the Normal Heap

Before Java 7, the String Constant Pool was stored in PermGen space, which had limited memory. From Java 7 onwards, it was moved to the heap to overcome these limitations and improve memory management.

- PermGen space had limited size, causing issues with many string objects.
- Moving the pool to heap provided more memory and flexibility.
- Using `new` always creates a new object in heap, even if the same string exists in the pool.

### Example

```java
String demoString = new String("Abhiram");
```

### Example

```java
public class Main {
    public static void main(String args[]) {
        String s1 = "TAT";
        String s2 = "TAT";

        String s3 = new String("TAT");
        String s4 = new String("TAT");

        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s3);
        System.out.println(s4);
    }
}
```

### Output
TAT
TAT
TAT
TAT

## JVM Memory Area

**Note:** All objects in Java are stored in a heap. The reference variable points to the object stored in the stack area, or they can be contained in other objects which puts them in the heap area also.

### Example 1

```java
public class Main {
    public static void main(String args[]) {
        byte ascii[] = { 65, 75, 65 };

        String firstString = new String(ascii);
        System.out.println(firstString);

        String secondString = new String(ascii, 1, 2);
        System.out.println(secondString);
    }
}
```

### Output
AKA
KA

### Example 2

```java
public class Main {
    public static void main(String args[]) {
        char characters[] = { 'A', 'k', 'a' };

        String firstString = new String(characters);
        String secondString = new String(firstString);

        System.out.println(firstString);
        System.out.println(secondString);
    }
}
```

### Output
Aka
Aka

## Why Java Strings are Immutable?

In Java, strings are immutable, meaning their values cannot be changed once created. If you try to modify a string using methods like `concat()` or `replace()`, a new string object is created instead of altering the original one.

- Strings are stored in a String Pool, allowing reuse of objects and reducing memory overhead.
- Multiple threads can safely share the same string object without synchronization.
- Immutable strings have a consistent hash code, making them reliable for use in collections like `HashMap`.

## Example Demonstrating Immutability

### Example

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = "Hello";

        System.out.println("s1 == s2: " + (s1 == s2));

        s1 = s1.concat(" World");

        System.out.println("s1: " + s1);
        System.out.println("s2: " + s2);
        System.out.println("s1 == s2: " + (s1 == s2));

        String s3 = new String("Hello");

        System.out.println("s2 == s3: " + (s2 == s3));
        System.out.println("s2.equals(s3): " + s2.equals(s3));
    }
}
```

### Output
s1 == s2: true
s1: Hello World
s2: Hello
s1 == s2: false
s2 == s3: false
s2.equals(s3): true

### Explanation

- `s1` and `s2` initially point to the same object in the String Pool.
- After `s1.concat(" World")`, a new string object is created for `Hello World`.
- `s3` is created using `new String("Hello")` and stored in the heap, separate from the String Pool.
- `==` checks reference equality, so `s2 == s3` is false.
- `equals()` checks content equality, so `s2.equals(s3)` is true.

## Why Strings Are Designed to Be Immutable

- **Memory Efficiency:** The String Pool allows multiple references to share the same string object safely.
- **Thread Safety:** Immutable objects are inherently safe for multi-threaded access.
- **Hashcode Reliability:** Strings are commonly used as keys in `HashMap`; immutability ensures the hashcode remains consistent.
- **Performance Optimization:** JVM can optimize immutable strings, including interning, which saves memory and improves speed.

## Java String concat() Method

The `concat()` method in Java is used to append one string to another and returns a new combined string. It does not modify the original string since strings are immutable.

- Used to concatenate or join two strings.
- Returns a new string as the result.
- Throws `NullPointerException` if the argument is null.

### Example

```java
public class Main {
    public static void main(String args[]) {
        String s = "Alpha";
        s = s.concat("Knowledge");
        System.out.println(s);
    }
}
```

### Output
AlphaKnowledge

## Syntax

```java
public String concat(String s);
```

## Parameters

A string to be concatenated at the end of the other string.

## Return Value

Concatenated combined string.

## Exception

`NullPointerException` when the argument string is null.

## Java String concat() Examples

There are many ways to use the `concat()` method in Java.

### Example

```java
public class Main {
    public static void main(String args[]) {
        String s1 = "Alpha";
        String s2 = "Knowledge";

        s1 = s1.concat(s2);

        System.out.println(s1);
    }
}
```

### Output
AlphaKnowledge

### Example

```java
public class Main {
    public static void main(String args[]) {
        String s1 = "Akash-";
        String s2 = "Mohit-";

        String s3 = s1.concat(s2);
        System.out.println(s3);

        String s4 = "Abhiram";
        String s5 = s3.concat(s4);
        System.out.println(s5);
    }
}
```

### Output
Akash-Mohit-
Akash-Mohit-Abhiram

**Note:** Strings are immutable in Java, so every concatenation creates a new string object instead of modifying the existing one.

### Example

```java
public class Main {
    public static void main(String args[]) {
        String s1 = "Alpha-";
        String s2 = null;

        String s3 = s1.concat(s2);

        System.out.println(s3);
    }
}
```

### Output
Exception in thread "main" java.lang.NullPointerException

### Example

```java
public class ReverseString {
    public static void main(String[] args) {
        String a = "Akash";
        String b = "";

        for (int i = a.length() - 1; i >= 0; i--) {
            char ch = a.charAt(i);
            String ch1 = Character.toString(ch);
            b = b.concat(ch1);
        }

        System.out.println(a);
        System.out.println(b);
    }
}
```

### Output
Akash
hsakA



###
