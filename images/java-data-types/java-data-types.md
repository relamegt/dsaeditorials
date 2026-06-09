# Java Data Types

In Java, a **data type** tells the program what kind of value a variable can store. It also helps Java decide how much memory is needed and what operations are allowed on that value.

For example:

- a whole number uses one data type
- a decimal number uses another
- a single character uses another
- text uses another

![Data Types](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-data-types/1781010496692-datatypes.png)

## Why Data Types Are Important

Data types are important because they help Java:

- store data correctly
- use memory properly
- prevent wrong operations
- check mistakes early

### Basic Syntax

```java
dataType variableName = value;
```

### Example

```java
int age = 20;
```

Here:

- `int` is the data type
- `age` is the variable name
- `20` is the value

## Types of Data Types in Java

Java data types are mainly divided into **two groups**:

1. Primitive data types
2. Non-primitive data types

## 1. Primitive Data Types

Primitive data types store simple values directly.

Java has **8 primitive data types**:

- `byte`
- `short`
- `int`
- `long`
- `float`
- `double`
- `char`
- `boolean`

## Primitive Data Types Table

| Type | Description | Default | Size | Example | Range |
| --- | --- | --- | --- | --- | --- |
| boolean | Logical values | false | Not JVM-defined | true, false | true or false |
| byte | 8-bit signed integer | 0 | 1 byte | 10 | -128 to 127 |
| char | 16-bit Unicode character | \u0000 | 2 bytes | 'A', '\u0041' | 0 to 65,535 |
| short | 16-bit signed integer | 0 | 2 bytes | 2000 | -32,768 to 32,767 |
| int | 32-bit signed integer | 0 | 4 bytes | 1000, -500 | -2,147,483,648 to 2,147,483,647 |
| long | 64-bit signed integer | 0L | 8 bytes | 123456789L | ±9.22e18 |
| float | 32-bit floating point | 0.0f | 4 bytes | 3.14f | ~6–7 digits precision |
| double | 64-bit floating point | 0.0d | 8 bytes | 3.14159d | ~15–16 digits precision |

## 1. boolean

The `boolean` data type stores only two values:

- `true`
- `false`

It is mostly used in conditions and decisions.

### Example

```java
public class Main {
    public static void main(String[] args) {
        boolean isJavaEasy = true;
        boolean isAkashSleeping = false;

        System.out.println("Is Java easy? " + isJavaEasy);
        System.out.println("Is Akash sleeping? " + isAkashSleeping);
    }
}
```

### Output
Is Java easy? true
Is Akash sleeping? false

## **2. byte**

The `byte` data type is used for small whole numbers.

### Example

```java
public class Main {
    public static void main(String[] args) {
        byte marks = 95;
        byte temperature = -10;

        System.out.println("Marks: " + marks);
        System.out.println("Temperature: " + temperature);
    }
}
```

## 3. short

The `short` data type is used for whole numbers that are bigger than `byte` but smaller than `int`.

### Example

```java
public class Main {
    public static void main(String[] args) {
        short students = 1200;
        short rooms = 150;

        System.out.println("Students: " + students);
        System.out.println("Rooms: " + rooms);
    }
}
```

## 4. int

The `int` data type is the most commonly used data type for whole numbers.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int akashAge = 21;
        int mohitMarks = 450;

        System.out.println("Akash Age: " + akashAge);
        System.out.println("Mohit Marks: " + mohitMarks);
    }
}
```

## 5. long

The `long` data type is used for very large whole numbers.

A `long` value usually ends with `L`.

### Example

```java
public class Main {
    public static void main(String[] args) {
        long worldPopulation = 7800000000L;
        long websiteVisitors = 25000000000L;

        System.out.println("World Population: " + worldPopulation);
        System.out.println("Website Visitors: " + websiteVisitors);
    }
}
```

## 6. float

The `float` data type is used for decimal numbers.

A `float` value ends with `f`.

### Example

```java
public class Main {
    public static void main(String[] args) {
        float productPrice = 99.5f;
        float discount = 12.5f;

        System.out.println("Product Price: " + productPrice);
        System.out.println("Discount: " + discount);
    }
}
```

## 7. double

The `double` data type is also used for decimal numbers, but it is more precise than `float`.

In Java, decimal numbers are usually treated as `double` by default.

### Example

```java
public class Main {
    public static void main(String[] args) {
        double pi = 3.1415926535;
        double accountBalance = 25000.75;

        System.out.println("Pi: " + pi);
        System.out.println("Account Balance: " + accountBalance);
    }
}
```

## 8. char

The `char` data type stores only **one character**.

The character must be written inside single quotes.

### Example

```java
public class Main {
    public static void main(String[] args) {
        char grade = 'A';
        char section = 'B';

        System.out.println("Grade: " + grade);
        System.out.println("Section: " + section);
    }
}
```

## Primitive Data Types Summary

| Type | Stores | Example |
| --- | --- | --- |
| boolean | true or false | true |
| byte | small whole number | 25 |
| short | medium whole number | 1200 |
| int | normal whole number | 50000 |
| long | very large whole number | 7800000000L |
| float | decimal number | 5.5f |
| double | more precise decimal number | 99.999 |
| char | one character | 'A' |

## 2. Non-Primitive Data Types

Non-primitive data types do not store the actual value directly in the same way as primitives. They usually store a reference to an object.

Common non-primitive types include:

- `String`
- Arrays
- Classes
- Objects
- Interfaces

## String

`String` is used to store text.

Text is written inside double quotes.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String websiteName = "AlphaKnowledge";
        String studentName = "Abhiram";

        System.out.println("Website Name: " + websiteName);
        System.out.println("Student Name: " + studentName);
    }
}
```

## Array

An array stores multiple values of the same type in a single variable.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int[] scores = {85, 90, 95};
        String[] names = {"Akash", "Mohit", "Abhiram"};

        System.out.println("First Score: " + scores);
        System.out.println("Second Name: " + names);[4]
    }
}
```

## Class

A class is a blueprint used to create objects.

### Example

```java
class Student {
    String name;
    int age;
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Akash";
        s1.age = 21;

        System.out.println("Name: " + s1.name);
        System.out.println("Age: " + s1.age);
    }
}
```

## Object

An object is a real instance created from a class.

In the previous example:

```java
Student s1 = new Student();
```

`s1` is an object.

## Interface

An interface is used to define rules that a class can follow.

### Example

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Woof");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();
    }
}
```

## Primitive vs Non-Primitive

| Feature | Primitive Data Types | Non-Primitive Data Types |
| --- | --- | --- |
| Stores | Simple values | References to objects |
| Size | Fixed | Usually not fixed |
| Examples | int, char, double | String, array, class |
| Created by | Built into Java | Built into Java or created by programmer |

## Example Program with Different Data Types

```java
public class Main {
    public static void main(String[] args) {
        String platformName = "AlphaKnowledge";
        String studentName = "Mohit";
        int age = 22;
        double score = 89.5;
        char grade = 'A';
        boolean isPassed = true;

        System.out.println("Platform: " + platformName);
        System.out.println("Student: " + studentName);
        System.out.println("Age: " + age);
        System.out.println("Score: " + score);
        System.out.println("Grade: " + grade);
        System.out.println("Passed: " + isPassed);
    }
}
```

### Output
Platform: AlphaKnowledge
Student: Mohit
Age: 22
Score: 89.5
Grade: A
Passed: true

## **Which Data Type Should You Use?**

Use the data type based on the kind of value you want to store.

| If you want to store | Use |
| --- | --- |
| Whole numbers | int |
| Very large whole numbers | long |
| Decimal numbers | double |
| One character | char |
| True or false | boolean |
| Text | String |

## Beginner Tips

- Use `int` for most whole numbers
- Use `double` for most decimal numbers
- Use `char` only for one character
- Use `String` for words and sentences
- Use `boolean` for yes/no or true/false values
- Do not confuse `char` and `String`

### Example

```java
char letter = 'A';
String word = "A";
```

These are not the same.

## Final Note

Java data types help the language understand what kind of value you want to store. If you learn data types properly, working with variables, input, conditions, and calculations becomes much easier.



###
