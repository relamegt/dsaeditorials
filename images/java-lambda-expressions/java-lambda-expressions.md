# Java Lambda Expressions

## Introduction

**Lambda expressions**, introduced in Java 8, allow developers to write concise, functional-style code by representing anonymous functions. They enable passing code blocks as parameters or assigning them to variables, resulting in cleaner, more readable, and highly maintainable programs.

Key features of lambda expressions include:

- **Functional Interface Target**: Lambda expressions provide concrete implementations for functional interfaces (interfaces with exactly one abstract method).
- **Code as Data**: Enable passing functional routines as arguments to other methods.
- **Variable Access Boundary**: Lambdas can access only `final` or effectively `final` local variables from their enclosing scope.
- **Exception Boundary**: Lambdas cannot throw checked exceptions unless the target functional interface declares them.
- **Syntax**:

`````java
(parameters) -> {
      // multiple statements
  }
```

## Basic Code Demo

The following program creates a custom functional interface `Add` and uses a lambda expression to implement addition of two numbers.

```java
interface Add {
    int addition(int a, int b);
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Lambda expression to add two numbers
        Add add = (a, b) -> a + b;

        int result = add.addition(10, 20);
        System.out.println("Sum: " + result);
    }
}
```

### Output
Sum: 30

### Explanation

- A functional interface `Add` is declared with a single abstract method `addition(int a, int b)`.
- In `AlphaKnowledge`, the lambda `(a, b) -> a + b` provides the execution logic.
- Calling `add.addition(10, 20)` invokes the lambda and outputs the sum.

## Functional Interface

A functional interface has exactly one abstract method. Lambda expressions provide its implementation. The `@FunctionalInterface` annotation is optional but recommended to enforce this rule at compile time.

- A functional interface can contain multiple `default` and `static` methods.
- It is mainly used with lambda expressions and method references to enable functional programming in Java.

```java
@FunctionalInterface
interface FuncInterface {
    void abstractFun(int x);
    default void normalFun() {
        System.out.println("Hello");
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        FuncInterface fobj = (int x) -> System.out.println(2 * x);
        fobj.abstractFun(5);
    }
}
```

### Output
10

### Explanation

- `FuncInterface` defines one abstract method `abstractFun` and a default method `normalFun`.
- The lambda `(int x) -> System.out.println(2 * x)` implements the abstract method.
- Invoking `abstractFun(5)` executes the block, printing `10`.

## Types of Lambda Parameters

Lambda expressions can accept different parameter configurations:

### 1. Lambda with Zero Parameters

Lambda expressions without any input arguments.

```java
@FunctionalInterface
interface ZeroParameter {
    void display();
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Lambda expression with zero parameters
        ZeroParameter zeroParamLambda = () -> System.out.println("This is a zero-parameter lambda expression!");

        // Invoke the method
        zeroParamLambda.display();
    }
}
```

### Output
This is a zero-parameter lambda expression!

### Explanation

- `zeroParamLambda` implements `ZeroParameter` using empty parentheses `()`, executing a print statement on invocation.

### 2. Lambda with a Single Parameter

Takes one input argument; parentheses around the parameter are optional.

```java
import java.util.ArrayList;

public class AlphaKnowledge {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);

        System.out.println("All elements:");
        list.forEach(n -> System.out.println(n));

        System.out.println("Even elements:");
        list.forEach(n -> {
            if (n % 2 == 0) {
                System.out.println(n);
            }
        });
    }
}
```

### Output
All elements:
1
2
3
Even elements:
2

### Explanation

- The `forEach()` method uses the `Consumer<T>` functional interface, which takes a single parameter.
- The lambda expression `n -> System.out.println(n)` omits parentheses for conciseness.

### 3. Lambda Expression with Multiple Parameters

Takes more than one input; parentheses are required around the parameter list.

```java
@FunctionalInterface
interface Functional {
    int operation(int a, int b);
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Using lambda expressions to define operations
        Functional add = (a, b) -> a + b;
        Functional multiply = (a, b) -> a * b;

        // Using the operations
        System.out.println(add.operation(6, 3));  
        System.out.println(multiply.operation(4, 5));  
    }
}
```

### Output
9
20

### Explanation

- The `Functional` interface requires two inputs.
- Lambdas `(a, b) -> a + b` and `(a, b) -> a * b` provide implementations, returning sum and product respectively.

## Examples in Collections / Streams

Lambda expressions are widely used with Java Collections and Streams for concise operations.

```java
import java.util.Arrays;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("mohit", "akash", "hemesh", "AlphaKnowledge");

        System.out.println("All names:");
        names.forEach(name -> System.out.println(name));

        System.out.println("\nNames starting with 'a' or 'A':");
        names.stream()
            .filter(n -> n.toLowerCase().startsWith("a"))
            .map(n -> n.toUpperCase())
            .forEach(System.out::println);
    }
}
```

### Output
All names:
mohit
akash
hemesh
AlphaKnowledge

Names starting with 'a' or 'A':
AKASH
ALPHAKNOWLEDGE

### Explanation

- A stream is obtained from the `names` list.
- `filter()` uses a predicate lambda to filter entries starting with `"a"`.
- `map()` applies a mapping lambda to convert elements to uppercase.
- `forEach()` prints the matching elements.

## Method References in Java

Method references are a shorthand syntax for writing lambda expressions that execute a single method. They leverage the double colon operator (`::`) to reference existing methods or constructors by name, improving code readability.

### Types of Method References

1. **Static Method Reference**: Reference to a static method of a class. Syntax: `ContainingClass::staticMethodName` (e.g., `Integer::compare`).
2. **Instance Method Reference of a Particular Object**: Reference to an instance method on a specific object reference. Syntax: `containingObject::instanceMethodName` (e.g., `System.out::println`).
3. **Instance Method Reference of an Arbitrary Object of a Particular Type**: Reference to an instance method on any arbitrary instance. Syntax: `ContainingType::methodName` (e.g., `String::toUpperCase`).
4. **Constructor Reference**: Reference to a class constructor to instantiate new objects. Syntax: `ClassName::new` (e.g., `ArrayList::new`).

### Code Example

The following program creates a list of car brands and uses an instance method reference on `System.out` to print each entry.

```java
import java.util.ArrayList;
import java.util.List;

public class AlphaKnowledge {
    public static void main(String[] args) {
        List<String> cars = new ArrayList<>();
        cars.add("Tesla");
        cars.add("BMW");
        cars.add("AlphaKnowledge");

        // Using Method Reference (System.out::println) to iterate and print
        System.out.println("Car list:");
        cars.forEach(System.out::println);
    }
}
```

### Output
Car list:
Tesla
BMW
AlphaKnowledge

### Explanation

- A list of car brands is initialized.
- `cars.forEach(System.out::println)` uses a method reference pointing to `println()` on the `System.out` object. This is equivalent to the lambda expression `n -> System.out.println(n)`.

## Advantages of Lambda Expressions

- **Concise Code**: Reduces boilerplate compared to anonymous inner classes.
- **Functional Programming**: Treats functions as first-class citizens.
- **Improved Readability**: Leads to highly readable, linear code structures.
- **Enhanced Collections and Streams**: Simplifies complex iterations, filtering, and mapping tasks.

## Common Built-in Functional Interfaces

Java provides standard functional interfaces in the `java.util.function` package:

| Interface | Method | Purpose |
| --- | --- | --- |
| `Predicate<T>` | `boolean test(T t)` | Tests a given condition and returns true or false. |
| `Consumer<T>` | `void accept(T t)` | Performs an action on the given argument without returning a result. |
| `Supplier<T>` | `T get()` | Generates a result without taking any input. |
| `Comparator<T>` | `int compare(T o1, T o2)` | Compares two objects to determine their order. |
| `Comparable<T>` | `int compareTo(T o)` | Defines the natural ordering for objects of a class. |

## Validity Check: Example Lambda Expressions

| Expression | Validity | Reason |
| --- | --- | --- |
| `() -> {}` | Valid | No parameters, empty body. |
| `() -> "AlphaKnowledge"` | Valid | Single expression returns a string value. |
| `() -> { return "AlphaKnowledge"; }` | Valid | Correct use of braces with return keyword. |
| `(Integer i) -> { return "AlphaKnowledge" + i; }` | Valid | Correct syntax with explicitly typed parameter. |
| `(String s) -> { return "AlphaKnowledge"; }` | Valid | Unused parameter but syntax is valid. |
| `() -> { return "Hello" }` | Invalid | Missing semicolon after return statement. |
| `x -> { return x + 1; }` | Invalid | Invalid if context is ambiguous and type cannot be inferred. |
| `(int x, y) -> x + y` | Invalid | If one parameter has an explicit type, all parameters must specify types. |

# Summary

The Java Lambda expression feature, introduced in Java 8, serves as a cornerstone for functional programming by providing a lightweight syntax to implement functional interfaces directly without creating anonymous inner classes. By allowing code blocks to be assigned to variables, passed as method arguments, or executed dynamically within collection pipelines and stream chains, it significantly reduces boilerplate code and improves code readability. While lambdas require target type context for parameter inference and restrict local variable modifications to effectively final references, their synergy with built-in functional interfaces like Predicate, Consumer, and Supplier makes them indispensable for writing clean, modular, and maintainable Java applications.




