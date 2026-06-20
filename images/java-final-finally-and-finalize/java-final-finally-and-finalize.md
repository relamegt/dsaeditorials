# Java final, finally and finalize()

## Introduction

In the Java programming language, **final**, **finally**, and **finalize()** are three distinct constructs that frequently cause confusion among developers due to their linguistic similarities. Despite their naming overlap, they belong to entirely different namespaces, serve independent compiler or runtime roles, and operate at different stages of the application lifecycle.

- **final**: A keyword used as a modifier to apply immutability or inheritance restrictions to variables, methods, and classes.
- **finally**: A structural block used in exception handling to guarantee resource cleanup and execution of critical code.
- **finalize()**: A lifecycle method inherited from the `Object` class that the JVM garbage collector runs before reclaiming an object's memory.

Understanding the compilation rules, runtime pathways, and diagnostic differences of these three components is essential for designing robust, secure, and resource-efficient Java programs.

# Overview

| Feature | final | finally | finalize() |
| --- | --- | --- | --- |
| **Type** | Keyword (Access modifier). | Structural block (Statement). | Lifecycle method (`java.lang.Object`). |
| **Purpose** | Prevents variable modification, method overriding, and class inheritance. | Guarantees resource release and cleanup after a try-catch structure. | Executes garbage collection hook activities before memory reclamation. |
| **Execution Context** | Checked during compilation; enforced at runtime. | Executes during exception handling (successful or aborted runs). | Executed asynchronously by the JVM Garbage Collector. |
| **Current Status** | Standard feature; highly recommended. | Standard feature; highly recommended. | **Deprecated since Java 9**; avoid in modern code. |

# final Keyword

The **final** keyword is a non-access modifier in Java used to restrict modification and enforce immutability at the variable, method, or class level. It provides compilation checks to ensure that constant values are not modified, security contracts are not broken, and classes are not modified in ways that compromise system security.

# 1. Final Variable

When a variable is declared with the `final` keyword, it can only be assigned a value once. Any subsequent attempts to reassign a value to that variable result in a compile-time error.

## Syntax

```java
final int MAX_STUDENTS = 100;
```

## Example: Final Variable

```java
public class AlphaKnowledge {
    public static void main(String[] args) {
        final int MAX_COURSES = 10;
        System.out.println("Maximum Courses: " + MAX_COURSES);

        // Attempting to reassign a final variable causes a compilation error
        // MAX_COURSES = 20; 
    }
}
```

### Output
Maximum Courses: 10

### Explanation

- **Value Immobility**: The variable `MAX_COURSES` is initialized to 10.
- **Compiler Check**: The compiler blocks any compilation of assignments targeting `MAX_COURSES` after its first initialization.

# Real-Life Example

Consider an billing module on the AlphaKnowledge platform. The platform charges a fixed subscription registration fee that must remain constant throughout runtime:

```java
final double REGISTRATION_FEE = 499.0;
```

Declaring the fee as final prevents accidental reassignments in calculations, keeping transaction processing secure.

# Blank Final Variable

A **blank final variable** is a final variable that is declared without an initial value. In Java, a blank final variable must be initialized before the object's construction completes. For instance variables, it must be initialized in all constructors or instance initialization blocks. For static variables, it must be initialized inside static initialization blocks.

## Example

```java
class Student {
    // Blank final instance variable
    final int studentId;

    // Initialization inside constructor
    Student(int id) {
        studentId = id;
    }

    void display() {
        System.out.println("Student ID: " + studentId);
    }
}

public class Main {
    public static void main(String[] args) {
        Student mohit = new Student(101);
        mohit.display();
    }
}
```

### Output
Student ID: 101

# Final Reference Variable

When a reference variable is declared `final`, it cannot be reassigned to point to another object in memory. However, the internal state or data members of the referenced object itself **can still be modified**.

## Example

```java
import java.util.ArrayList;

public class Demo {
    public static void main(String[] args) {
        final ArrayList<String> students = new ArrayList<>();

        // Modifying object contents is allowed
        students.add("Mohit");
        students.add("Akash");
        System.out.println("Student list: " + students);

        // Attempting to reassign reference variable causes compilation error
        // students = new ArrayList<>(); 
    }
}
```

### Output
Student list: [Mohit, Akash]

### Explanation

- **Reference Lock**: The variable `students` is locked to point to a specific `ArrayList` instance on the Heap.
- **Content Mutability**: We can freely call modification methods like `add()`, `remove()`, or `set()` on the array list because they modify the object's internal array state, not the reference variable itself.

# 2. Final Method

A method declared with the `final` keyword cannot be overridden by subclass methods. This is used when the base class method implementation is critical and should not be modified by subclass definitions.

## Example

```java
class Course {
    final void showPlatform() {
        System.out.println("Platform: AlphaKnowledge");
    }
}

class JavaCourse extends Course {
    // Attempting to override causes a compilation error
    // void showPlatform() { System.out.println("Overridden"); }
}
```

### Explanation

- The method `showPlatform()` in class `Course` is declared as final.
- Subclasses like `JavaCourse` can call `showPlatform()`, but they cannot redefine its implementation.
- **Compiler Optimization**: The compiler can optimize final methods by using inline expansion (inlining), replacing method calls directly with the method body to reduce execution overhead.

# Why Use Final Methods?

- **Security**: Prevents malicious actors from subclassing core system API classes and overriding methods to return compromised values.
- **Consistent Behavior**: Guarantees that essential platform contracts remain uniform across all child implementations.
- ** accidental overriding prevention**: Prevents junior developers from accidentally overriding helper utility methods.

# 3. Final Class

A class declared with the `final` keyword cannot be extended (inherited) by any other class. This prevents sub-classing.

## Example

```java
final class Platform {
    void display() {
        System.out.println("Welcome to AlphaKnowledge");
    }
}

// Attempting to extend a final class causes a compilation error
// class OnlinePlatform extends Platform {}
```

### Explanation

- The class `Platform` is final, which means it cannot serve as a parent class.
- **Core Java Examples**: Java's standard utility classes like `java.lang.String` and type wrapper classes (such as `Integer`, `Double`, `Boolean`) are final classes. This ensures that their immutable security behavior cannot be overridden.

# Advantages of final

- **Improves Security**: Critical algorithms and class patterns cannot be modified or subclassed.
- **Supports Constant Definitions**: Allows declaring immutable constants within variable namespaces.
- **Thread Safety**: Objects with only final fields are immutable, making them inherently thread-safe without requiring locks.
- **Enables JVM Optimizations**: Provides the JVM compiler context to optimize code paths, inline methods, and cache variable values.

# finally Block

The **finally** block is a control flow structure in Java used in exception handling. It is paired with try-catch blocks to guarantee the execution of a block of code, regardless of whether exceptions are raised or resolved.

# Syntax

```java
try {
    // Risky code
} catch (Exception e) {
    // Exception recovery
} finally {
    // Code that executes under all conditions
}
```

# Why Use finally?

In Java, system resources like file streams, database connections, and network sockets are system handles. If they are not closed properly after use, they remain open, leading to memory leaks and resource exhaustion. Placing resource closing statements inside the finally block ensures they are executed even if a runtime exception halts method execution halfway.

# Example: finally Block

```java
public class AlphaKnowledge {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // Raises ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero is not allowed.");
        } finally {
            System.out.println("Finally block: Resource cleanup operations completed.");
        }
    }
}
```

### Output
Error: Division by zero is not allowed.
Finally block: Resource cleanup operations completed.

# Example: No Exception

```java
public class Demo {
    public static void main(String[] args) {
        try {
            System.out.println("Course loaded successfully.");
        } finally {
            System.out.println("Finally block: Database connections closed.");
        }
    }
}
```

### Output
Course loaded successfully.
Finally block: Database connections closed.

### Explanation

- The try block executes without throwing any exceptions.
- Since no catch blocks are defined, execution flows directly into the `finally` block before continuing below the block.

# finally with try Only

In Java, catching exceptions is not always mandatory. A `try` block can be paired directly with a `finally` block, omitting the `catch` block. This structure is used when a method needs to ensure resource cleanup, but delegates exception handling to caller methods in the call stack.

```java
public class Demo {
    static void process() {
        try {
            System.out.println("Processing transaction data...");
        } finally {
            System.out.println("Cleanup completed: Locks released.");
        }
    }

    public static void main(String[] args) {
        process();
    }
}
```

### Output
Processing transaction data...
Cleanup completed: Locks released.

# Cases Where finally May Not Execute

The finally block is designed to run under almost all scenarios, but there are three rare runtime events where it is bypassed:

## 1. System.exit() Execution

If the application invokes `System.exit(int status)` inside the try or catch blocks, the JVM shuts down immediately. This halts all threads, preventing the finally block from executing.

```java
try {
    System.exit(0);
} finally {
    System.out.println("This message will never print.");
}
```

## 2. JVM Crash or Hardware Failures

If the JVM encounters a fatal error, such as a stack overflow in native memory, or the operating system terminates the process forcefully, the program stops instantly.

## 3. Infinite Loops

If the try or catch block enters an infinite loop or gets blocked in an indefinite wait state, the execution pointer will never exit to reach the finally block.

# Internal Working of finally

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-final-finally-and-finalize/1781961037288-bb27ac36-92c2-470e-b76c-92193647d505.png)

# finalize() Method

The **finalize()** method is a protected method defined in the `java.lang.Object` class. Historically, the Java garbage collector invokes this method on an object when it determines that there are no more references to the object, just before reclaiming its memory.

# Syntax

```java
protected void finalize() throws Throwable {
    // Resource release hooks (e.g. closing files or sockets)
}
```

# Important Note: Deprecation of finalize()

> *!WARNING:* The `finalize()` method has been **deprecated since Java 9** due to performance, reliability, and security concerns. Modern Java applications should never implement `finalize()`.

### Preferred Modern Alternatives

- **Try-With-Resources**: Automatically closes classes implementing `java.lang.AutoCloseable`.
- **Explicit Cleaners/Phantom References**: Using `java.lang.ref.Cleaner` provides a cleaner resource release mechanism that does not impact GC performance.

# Example: finalize()

```java
public class Student {
    @Override
    protected void finalize() {
        System.out.println("Lifecycle Hook: Object memory is being reclaimed by Garbage Collector.");
    }

    public static void main(String[] args) {
        Student mohit = new Student();
        mohit = null; // Object is now eligible for Garbage Collection

        System.gc(); // Suggesting JVM to run Garbage Collector
        System.out.println("Program execution completed.");
    }
}
```

### Possible Output

Program execution completed.
Lifecycle Hook: Object memory is being reclaimed by Garbage Collector.

### Explanation

- Assigning `mohit = null` makes the `Student` object eligible for garbage collection.
- Calling `System.gc()` suggests that the JVM run garbage collection.
- **GC Unpredictability**: The timing of garbage collection is determined by the JVM. As a result, the `finalize()` method execution order may vary, and it might not execute before the program terminates.

# Why finalize() Is Deprecated

- **Unpredictable Execution**: Java does not guarantee when (or even if) the garbage collector will run. Therefore, cleanup logic in `finalize()` might be delayed indefinitely.
- **Performance Overhead**: Objects overriding `finalize()` require extra work from the garbage collector, slowing down memory allocation and reclamation cycles.
- **Security Risks**: Malicious subclasses can hijack finalize methods to save themselves from garbage collection, leading to memory leaks and security vulnerabilities.
- **Exceptions Swallowed**: Any exception thrown by the `finalize()` method is caught and ignored by the garbage collector, hiding errors.

# Modern Alternative: Try-With-Resources

Instead of relying on garbage collection hooks, modern applications use try-with-resources to clean up system resources deterministically:

```java
import java.io.*;

public class Demo {
    public static void main(String[] args) {
        // Automatically closes the resource when try exits
        try (FileReader file = new FileReader("course_data.txt")) {
            System.out.println("Processing course data...");
        } catch (IOException e) {
            System.out.println("Error reading file.");
        }
    }
}
```

# Comparison: final vs finally vs finalize()

| Feature | final | finally | finalize() |
| --- | --- | --- | --- |
| **Type** | Keyword. | Block. | Method. |
| **Applied To** | Variables, methods, and classes. | try-catch structures. | Objects. |
| **Purpose** | Restricts modifications, overriding, and inheritance. | Enforces resource cleanup after exception blocks. | Performs cleanup operations before garbage collection. |
| **Inheritance Relation** | Prevents method overriding and subclassing. | No relation. | Inherited from `Object` class; can be overridden. |
| **Exception Handling** | No relation. | Primary component of exception handling. | No relation. |
| **Garbage Collection** | No relation. | No relation. | Executed by the JVM garbage collector. |
| **Execution Time** | Handled during compilation and execution. | Run immediately after try-catch blocks exit. | Unpredictable timing; run during GC sweeps. |

# Real-Life Analogy

Consider Mohit studying on the AlphaKnowledge platform:

### final

Student ID Card Number = 101
Once assigned, it is unique and cannot be modified.

### finally

Enter Classroom → Attend Lecture → Clean Up Table
Cleaning up the table occurs whether the student enjoyed the lecture or had to leave early due to an emergency.

### finalize()

Student withdraws from university → Librarian cleans out the locker
The locker is cleared by university staff after the student has left the campus.

# Common Mistakes

## Trying to Modify a Final Variable

Attempting to modify the value of a final variable after it has been initialized causes a compile-time error:

```java
final int age = 20;
// age = 25; // Compiler Error: cannot assign a value to final variable
```

## Assuming finalize() Always Runs

Assuming that the JVM will execute the `finalize()` method before the application exits is a common mistake. Resource cleanup should never be placed in this method.

## Using finally for Business Logic Modifications

Putting modifications to business variables inside the `finally` block can cause subtle bugs. The finally block should be reserved strictly for resource cleanup and safety checks:

```java
// Bad practice: modifying business state inside finally
finally {
    marks = marks + 10;
}
```

# Best Practices

### Use final for Constants

Declare variables as `final` when their value should not change. This improves code readability and prevents bugs:

```java
final double PI = 3.14159;
```

### Use finally for Resource Cleanup

Always use the `finally` block or try-with-resources statements to close database connections and file streams:

```java
finally {
    connection.close();
}
```

### Avoid finalize()

Never use `finalize()` for resource cleanup. Use try-with-resources or the `AutoCloseable` interface instead.

### Prefer Immutable Objects

Declare instance fields as `final` where possible to support thread safety and design immutable classes.

# Summary

In Java, final, finally, and finalize() are completely different concepts despite having similar names. The final keyword is used to restrict modification of variables, methods, and classes. The finally block is used in exception handling and executes regardless of whether an exception occurs, making it ideal for cleanup tasks. The finalize() method belongs to the Object class and is invoked by the Garbage Collector before object destruction, although it has been deprecated since Java 9 due to reliability and performance concerns. Understanding these differences helps developers write safer, cleaner, and more maintainable Java applications.




