# throw and throws in Java

## Introduction

In the Java programming language, exception handling is a core feature designed to build robust, fault-tolerant applications by managing runtime anomalies gracefully. Two primary constructs used to control the lifecycle and propagation of exceptions are the **throw** and **throws** keywords. Although linguistically similar, they serve completely different purposes in code execution and compilation contracts:

- **throw**: Used to explicitly generate and throw an exception object from within a method body, halting current execution flow and transferring control to an exception handler.
- **throws**: Used in a method signature to declare the types of checked exceptions a method might throw during its execution, shifting the responsibility of exception handling onto the calling method.

Understanding when and how to implement these keywords is fundamental to defining API contracts, writing custom validation routines, and handling external resource failures correctly.

# Why Do We Need throw and throws?

Consider a student enrollment portal on the **AlphaKnowledge** platform:

- **Validation requirement**: Students must be at least 18 years old to register for advanced courses. If **Mohit** enters his age as 15, the program should not silently process this invalid state. We use the `throw` keyword to manually instantiate an exception and reject the registration.
- **Checked exception contract**: When a method performs database or file operations, the compiler requires that the method handle or declare potential failures (like file-not-found errors). The method uses `throws` to warn the caller that it might encounter these checked exception paths.

Together, these keywords allow developers to raise validation errors dynamically and declare clear method contracts for callers.

# throw Keyword

The **throw** keyword in Java is used to explicitly throw a single exception object. This exception object can belong to a built-in class (like `ArithmeticException` or `IllegalArgumentException`) or a developer-defined custom exception class.

## Syntax

```java
throw new ExceptionName("Detailed error message string");
```

## Key Points of throw

- **Statement Level**: Used inside method bodies or execution blocks.
- **Single Instance**: Throws exactly one exception object at a time.
- **Execution Halt**: Once a `throw` statement executes, the JVM halts the current execution path immediately. Any statements directly below `throw` inside that block are unreachable, causing a compile-time error.
- **Requires Throwable**: Can only throw classes that extend the `java.lang.Throwable` superclass.
- **Checked and Unchecked**: Works with both checked exceptions (must be caught or declared) and unchecked exceptions (can run without compiler checks).

# Example 1: Basic throw

```java
public class AlphaKnowledge {
    public static void main(String[] args) {
        // Manually throwing an ArithmeticException
        throw new ArithmeticException("Custom Arithmetic Error");
    }
}
```

### Output
Exception in thread "main" java.lang.ArithmeticException: Custom Arithmetic Error
	at AlphaKnowledge.main(AlphaKnowledge.java:4)

### Explanation

- The program instantiates a new `ArithmeticException` object containing the message "Custom Arithmetic Error".
- The `throw` keyword passes the exception object to the JVM.
- Since the exception is not caught within a try-catch block, the JVM terminates the thread and prints the call stack trace.

# Example 2: Division by Zero Check

```java
public class DivisionDemo {
    public static void main(String[] args) {
        int numerator = 100;
        int denominator = 0;

        if (denominator == 0) {
            // Preventing division by zero by throwing a custom message
            throw new ArithmeticException("Division by zero is not allowed");
        }

        System.out.println(numerator / denominator);
    }
}
```

### Output
Exception in thread "main" java.lang.ArithmeticException: Division by zero is not allowed
	at DivisionDemo.main(DivisionDemo.java:8)

# Example 3: Student Age Validation

```java
public class StudentValidation {
    static void checkAge(int age) {
        if (age < 18) {
            // Throwing IllegalArgumentException when age checks fail
            throw new IllegalArgumentException("Student must be 18 or older");
        }
        System.out.println("Admission Approved");
    }

    public static void main(String[] args) {
        checkAge(15);
    }
}
```

### Output
Exception in thread "main" java.lang.IllegalArgumentException: Student must be 18 or older
	at StudentValidation.checkAge(StudentValidation.java:5)
	at StudentValidation.main(StudentValidation.java:12)

# Example 4: Handling throw with try-catch

In production code, thrown exceptions are caught in caller blocks to keep the application running:

```java
public class AdmissionSystem {
    static void verifyAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Invalid Age");
        }
    }

    public static void main(String[] args) {
        try {
            verifyAge(16);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }

        System.out.println("Program Continues");
    }
}
```

### Output
Invalid Age
Program Continues

### Explanation

- The `verifyAge` method throws an exception.
- The calling method `main` intercepts this exception inside a try-catch block.
- The catch block logs or prints the error, and execution continues below the catch block.

# Rethrowing an Exception

Rethrowing occurs when a caught exception is thrown again from a catch block. This is useful when a method needs to perform some intermediate cleanup or logging operations before passing the exception up the call stack.

```java
public class Demo {
    static void process() {
        try {
            throw new NullPointerException("Demo Error");
        } catch (NullPointerException e) {
            System.out.println("Caught Inside Method: Logging error state.");
            // Rethrowing the caught exception object
            throw e; 
        }
    }

    public static void main(String[] args) {
        try {
            process();
        } catch (NullPointerException e) {
            System.out.println("Caught in Main: Handled rethrown exception.");
        }
    }
}
```

### Output
Caught Inside Method: Logging error state.
Caught in Main: Handled rethrown exception.

# throws Keyword

The **throws** keyword is used in method signatures to declare checked exceptions that a method might throw during its execution. It acts as a compiler contract, warning calling methods that they must either handle the exception (using try-catch) or further declare it in their own method signatures using `throws`.

## Syntax

```java
returnType methodName() throws ExceptionClass1, ExceptionClass2 {
    // Method body
}
```

## Key Points of throws

- **Signature Level**: Used in method declarations.
- **Declares Types**: Lists potential checked exception classes, not exception objects.
- **Checked Focus**: Primarily used to satisfy compiler checks for checked exceptions. Declaring runtime (unchecked) exceptions is not required.
- **Delegates Responsibility**: Tells the compiler that the method will not handle these exceptions locally, shifting the handling responsibility to the caller.

# Why Use throws?

Certain system failures (like file missing, database down, or thread interruption) are represented by checked exceptions. Java requires developers to handle or declare these exceptions at compile-time. If a method does not handle a checked exception locally, it must declare it using `throws` to compile.

# Example 1: Using throws

```java
class Demo {
    // Thread.sleep throws a checked InterruptedException
    static void pause() throws InterruptedException {
        Thread.sleep(2000);
        System.out.println("Process Completed");
    }

    public static void main(String[] args) throws InterruptedException {
        pause();
    }
}
```

### Output
Process Completed

### Explanation

- The `Thread.sleep` method throws an `InterruptedException` (a checked exception).
- The `pause` method declares `throws InterruptedException` in its signature, satisfying the compiler.
- The calling `main` method also declares `throws InterruptedException` in its signature, delegating the exception up to the JVM.

# Example 2: Reading File Using throws

```java
import java.io.*;

public class FileDemo {
    // FileReader constructor and file.close() throw checked IOExceptions
    static void readFile() throws IOException {
        FileReader file = new FileReader("data.txt");
        file.close();
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("File Error: The requested data configuration file is missing.");
        }
    }
}
```

### Output
File Error: The requested data configuration file is missing.

# Example 3: Multiple Exceptions

```java
import java.io.*;

public class Demo {
    static void process() throws IOException, ClassNotFoundException {
        System.out.println("Processing file and class definitions...");
    }

    public static void main(String[] args) {
        try {
            process();
        } catch (Exception e) {
            System.out.println("Handled: Captured exception thrown by process.");
        }
    }
}
```

### Output
Processing file and class definitions...

# Combining throw and throws

Both keywords are frequently used together. The `throw` keyword is used within a method body to trigger a checked exception, while the `throws` keyword is used in the method signature to declare it.

```java
class StudentAdmission {
    // verifyAge throws Exception, so it must declare it using throws
    static void verifyAge(int age) throws Exception {
        if (age < 18) {
            throw new Exception("Age must be 18 or above");
        }
        System.out.println("Admission Approved");
    }

    public static void main(String[] args) {
        try {
            verifyAge(15);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Age must be 18 or above

# User-Defined Exception Example

Java allows developers to create custom exceptions to handle specific business logic requirements. Custom exceptions extending the `Exception` class are checked exceptions and must use the throw/throws combination.

## Step 1: Create Exception Class

```java
class InvalidMarksException extends Exception {
    public InvalidMarksException(String message) {
        // Pass message to parent Exception class
        super(message);
    }
}
```

## Step 2: Use throw and throws

```java
class Student {
    static void checkMarks(int marks) throws InvalidMarksException {
        if (marks < 0 || marks > 100) {
            throw new InvalidMarksException("Marks must be between 0 and 100");
        }
        System.out.println("Valid Marks");
    }

    public static void main(String[] args) {
        try {
            checkMarks(150);
        } catch (InvalidMarksException e) {
            System.out.println("Custom Error caught: " + e.getMessage());
        }
    }
}
```

### Output
Custom Error caught: Marks must be between 0 and 100

# Internal Working of throw

The JVM processes `throw` statements by searching for an active catch handler:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/throw-and-throws-in-java/1781961333332-4cd0f403-741a-4a1a-bf5f-ed5fcc4acc39.png)

       

# Internal Working of throws

The `throws` keyword defines caller propagation boundaries:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/throw-and-throws-in-java/1781961406974-c6011078-e273-4823-882f-df0b46654492.png)

 

# Common Checked Exceptions

| Exception Class | Description |
| --- | --- |
| **IOException** | Thrown when an input/output operation fails. |
| **SQLException** | Thrown when database queries or connection configurations fail. |
| **InterruptedException** | Thrown when a thread is interrupted while waiting or sleeping. |
| **ClassNotFoundException** | Thrown when the JVM tries to load a class by its string name but cannot find it. |
| **ParseException** | Thrown when a string parsing operation fails. |

# Common Unchecked Exceptions

| Exception Class | Description |
| --- | --- |
| **ArithmeticException** | Occurs during invalid mathematical calculations, like integer division by zero. |
| **NullPointerException** | Occurs when calling methods on reference variables that point to null. |
| **ArrayIndexOutOfBoundsException** | Occurs when accessing indices outside array boundaries. |
| **NumberFormatException** | Occurs when converting invalid alphanumeric string characters into numeric types. |
| **IllegalArgumentException** | Thrown to indicate that a method has been passed an illegal or inappropriate argument. |

# throw vs throws

| Feature | throw | throws |
| --- | --- | --- |
| **Purpose** | Used to explicitly throw an exception object. | Used in method signatures to declare possible checked exceptions. |
| **Location** | Used inside method bodies (statement level). | Used in method signatures (method declaration level). |
| **Target Type** | Followed by an exception instance (object). | Followed by exception class names (types). |
| **Quantity** | Can throw only one exception instance at a time. | Can declare multiple comma-separated exception classes. |
| **Keyword Usage** | Used with the `new` keyword to instantiate exceptions. | Used directly in the method declaration header. |
| **Execution Impact** | Halts current block execution instantly. | Does not impact execution path on its own. |
| **Checked Exceptions** | Works with both checked and unchecked exceptions. | Primarily used with checked exceptions. |
| **Unchecked Exceptions** | Commonly used to throw runtime exceptions. | Not required to declare unchecked runtime exceptions. |

# Real-Life Analogy

Consider Mohit enrolling in a university course on AlphaKnowledge:

### throw Analogy

Mohit enters his age as 15 inside the registration form. The registration system checks the age validation rules, immediately rejects the application, and throws an error stating "Age validation failed". This represents the `throw` keyword.

### throws Analogy

Before processing registration forms, the university course catalog informs administrators that the processing system might fail due to database drops or connection losses. The system does not fix database errors itself; it warns callers that a connection error may occur. This represents the `throws` keyword.

# Common Mistakes

## Mistake 1: Using throw with an Exception Class Name

The `throw` keyword must be followed by an instance of an exception object, not the class name itself.

```java
// Wrong: Causes compilation error
// throw ArithmeticException;

// Correct
throw new ArithmeticException("Error message");
```

## Mistake 2: Ignoring Checked Exceptions

If a method contains code that throws checked exceptions, it must either handle them inside a try-catch block or declare them in its method signature using `throws`. Failing to do so causes a compilation error.

```java
// Wrong: Compiler error - unhandled InterruptedException
// void delay() { Thread.sleep(1000); }

// Correct
void delay() throws InterruptedException { Thread.sleep(1000); }
```

## Mistake 3: Using throws Instead of throw

Using `throws` to raise an exception object inside a method body is a syntax error.

```java
// Wrong: Syntax error inside method
// void process() { throws new IOException(); }

// Correct
void process() { throw new IOException("Error"); }
```

# Best Practices

### Use throw for Input Validation

Use the `throw` keyword to validate method arguments, throwing unchecked exceptions like `IllegalArgumentException` early.

```java
if (age < 18) {
    throw new IllegalArgumentException("Age validation failed.");
}
```

### Use throws for Checked Exceptions

Always declare checked exceptions using the `throws` keyword when a method cannot recover from them locally, delegating recovery tasks to the calling layer.

```java
public void readFile() throws IOException
```

### Prefer Specific Exception Classes

When throwing exceptions, prefer specific subclasses (such as `IllegalArgumentException` or `FileNotFoundException`) over generic parent classes (like `Exception` or `Throwable`). This provides callers with clearer context.

### Create Custom Exceptions for Business Domain Validation

Implement custom exceptions that extend `Exception` (checked) or `RuntimeException` (unchecked) to manage specific validation failures in your domain logic.

# Interview Questions

### Q1. What is the difference between throw and throws?

`throw` is used to explicitly throw an exception object inside a method body, whereas `throws` is used in method signatures to declare checked exceptions that the method might throw.

### Q2. Can throw be used with checked exceptions?

Yes. When throwing a checked exception object inside a method, the method must either catch it or declare it in its signature using `throws`.

### Q3. Can throws declare multiple exceptions?

Yes, multiple exceptions can be declared in a method signature using a comma-separated list:

```java
throws IOException, SQLException
```

### Q4. Which keyword creates an exception object?

Neither keyword creates the object. The `new` keyword is used to instantiate exception objects, while `throw` is used to throw them.

### Q5. Is throws mandatory for unchecked exceptions?

No. Unchecked exceptions (subclasses of `RuntimeException` or `Error`) do not need to be declared in method signatures using `throws`.

# Summary

The throw keyword is used to explicitly generate an exception object and interrupt normal program execution, while the throws keyword is used in a method declaration to inform callers that a method may generate one or more exceptions. The throw keyword works with both checked and unchecked exceptions and is commonly used for validation and custom exceptions. The throws keyword is mainly used with checked exceptions and delegates exception handling responsibility to the caller. Together, throw and throws form an essential part of Java's exception handling mechanism and help developers build reliable and maintainable applications.




