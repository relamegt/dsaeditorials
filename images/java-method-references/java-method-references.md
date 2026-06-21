# Java Method References

## Introduction

**Java Method References** are a shorthand way to refer to an existing method without invoking it. Introduced in Java 8, they serve as a clean alternative to lambda expressions, making code shorter, cleaner, and more readable. Method references leverage the double colon (`::`) operator and are used in conjunction with functional interfaces.

Key features of method references include:

- **Concise Alternative**: Reduces boilerplate code by replacing lambda expressions that simply call a single existing method.
- **Improved Readability**: Makes the code more intuitive by referencing methods directly by name.
- **Pass-Through Mapping**: Used when a lambda expression acts only as a pass-through call, forwarding its inputs directly to an existing method.

## Basic Code Demo

The following program creates a list of name strings and uses a static method reference to print each name sequentially.

```java
import java.util.Arrays;

public class AlphaKnowledge {
    // Static print method
    public static void print(String s) {
        System.out.println(s);
    }

    public static void main(String[] args) {
        String[] names = {"mohit", "akash", "AlphaKnowledge"};

        // Using method reference to print each name
        Arrays.stream(names).forEach(AlphaKnowledge::print);
    }
}
```

### Output
mohit
akash
AlphaKnowledge

### Explanation

- A static method `print(String s)` is defined within the `AlphaKnowledge` class.
- An array containing name strings is created.
- `Arrays.stream(names).forEach(AlphaKnowledge::print)` utilizes the method reference to direct each stream element to the `print()` method, executing it sequentially.

## Syntax of Method References

Method references can be written using three primary syntaxes:

- **Static Method**: `ClassName::staticMethodName`
- **Instance Method**: `objectReference::instanceMethod`
- **Constructor**: `ClassName::new`

## Types of Method References

Java supports four types of method references:

### 1. Reference to a Static Method

A static method reference is used to refer to a static method of a class, replacing a lambda expression that calls a static method.

- Accesses methods using the class name.
- The referenced method must be `static`.
- Syntax: `ClassName::staticMethodName`

```java
import java.util.Arrays;
import java.util.List;

class MathUtil {
    static void square(int n) {
        System.out.println(n * n);
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(2, 3, 4);
        list.forEach(MathUtil::square);
    }
}
```

### Output
4
9
16

### Explanation

- `square(int n)` is a static method in `MathUtil`.
- `list.forEach(MathUtil::square)` directs each list element to the static method, equivalent to the lambda `n -> MathUtil.square(n)`.

### 2. Reference to an Instance Method of a Particular Object

Refers to a non-static method of a specific, already-instantiated object.

- Uses an existing object reference.
- The referenced method must be non-static.
- Syntax: `objectReference::instanceMethod`

```java
import java.util.Arrays;
import java.util.List;

class Printer {
    void print(String msg) {
        System.out.println(msg);
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        Printer printer = new Printer();
        List<String> data = Arrays.asList("Tesla", "BMW", "AlphaKnowledge");

        data.forEach(printer::print);
    }
}
```

### Output
Tesla
BMW
AlphaKnowledge

### Explanation

- `printer` is an instance of the `Printer` class.
- The instance method reference `printer::print` is passed to `forEach()`, sending each list element to `printer.print(msg)`.

### 3. Reference to an Instance Method of an Arbitrary Object

Refers to an instance method of an arbitrary object of a particular class. The object on which the method is called is determined at runtime.

- Uses the class name instead of an object instance.
- Frequently used with the Stream API to process elements individually.
- Syntax: `ClassName::instanceMethod`

```java
import java.util.Arrays;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("mohit", "akash", "hemesh");

        names.stream()
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

### Output
MOHIT
AKASH
HEMESH

### Explanation

- `String::toUpperCase` maps each string in the stream to its uppercase equivalent. The method is called on each string instance dynamically.
- `System.out::println` displays each mapped uppercase string.

### 4. Reference to a Constructor

Replaces a lambda expression that instantiates a new object using a functional interface.

- Uses the `new` keyword.
- Primarily used with functional interfaces like `Supplier` or `Function`.
- Syntax: `ClassName::new`

```java
import java.util.function.Supplier;

class Student {
    Student() {
        System.out.println("Student object created");
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        Supplier<Student> supplier = Student::new;
        supplier.get();
    }
}
```

### Output
Student object created

### Explanation

- `Supplier<Student>` defines a functional interface.
- The constructor reference `Student::new` points to the default constructor. Calling `supplier.get()` triggers instantiation and outputs the creation message.

## Method References and Functional Interfaces

Method references are compatible only with functional interfaces containing exactly one abstract method.

- The parameter types and return type of the referenced method must match the signature of the abstract method.
- They are commonly used with standard functional interfaces such as `Consumer`, `Supplier`, `Function`, and `Predicate`.
- They are highly useful for sorting collections, for example:

`````java
List<String> list = Arrays.asList("Tesla", "BMW", "AlphaKnowledge");
  list.sort(String::compareToIgnoreCase);
```

# Summary

Java Method References, introduced in Java 8, provide a highly readable and clean shorthand notation using the double colon :: operator to reference existing methods or constructors without executing them. By serving as direct pass-through alternatives to lambda expressions that simply forward their parameters, they facilitate static method references, instance method references on specific or arbitrary objects, and constructor creations. Working strictly in tandem with functional interfaces like Consumer, Supplier, and Function, method references minimize boilerplate code and streamline collection sorting and stream-based data transformations in Java applications.




