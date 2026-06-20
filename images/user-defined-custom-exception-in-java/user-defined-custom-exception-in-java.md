# User-Defined Custom Exception in Java

## Introduction

In Java, exception handling is a vital feature for managing runtime anomalies. While the Java Standard Library provides a comprehensive set of built-in exception classes (such as `NullPointerException`, `ArithmeticException`, and `IOException`), these generic classes often fail to describe application-specific business errors accurately. In real-world enterprise software, errors are rarely as simple as division by zero or a missing file; instead, they represent violations of business rules.

To address this, Java allows programmers to define their own exception classes, known as **User-Defined Custom Exceptions**. A custom exception is a class created by the developer to represent domain-specific errors. Examples include:

- **InsufficientBalanceException**: Thrown when a banking client attempts to withdraw more money than they possess.
- **InvalidAgeException**: Raised when an underage user attempts to register for age-restricted activities.
- **LowAttendanceException**: Raised when a student's attendance falls below the required threshold for exams.
- **ProductOutOfStockException**: Thrown in e-commerce systems when an item is unavailable for purchase.

By creating custom exception classes, developers can write self-documenting code, provide meaningful diagnostics, and manage business-rule violations in a clean, professional manner.

# Why Do We Need Custom Exceptions?

Consider a student registration module at **AlphaKnowledge Institute** where the system requires students to be at least 18 years old.

```java
public class Registration {
    public static void main(String[] args) {
        int age = 15;
        if (age < 18) {
            System.out.println("Error");
        }
    }
}
```

### Output
Error

### Problems with this Approach

- **Lacks Context**: The console output "Error" does not explain the cause or nature of the validation failure.
- **No Object Representation**: No exception object is generated or thrown, meaning the failure cannot be bubbled up to parent methods or logged in a structured call stack trace.
- **Tightly Coupled**: Business validation logic and error-handling logic are mixed together, making the code harder to scale.

# Solution: Custom Exception

By replacing the console output with a custom exception throw, we improve the program's structure:

```java
throw new InvalidAgeException("Age must be 18 or above");
```

This approach provides:

- **Self-Documenting Code**: The class name `InvalidAgeException` immediately explains the error condition.
- **Separation of Concerns**: Business rule validation throws the error, while caller try-catch blocks manage the recovery.
- **Structured Diagnostics**: The exception captures the call stack trace and detail messages, making debugging straightforward.

# What is a Custom Exception?

A user-defined custom exception is simply a Java class that inherits from an existing exception class in the Java Exception Hierarchy. Depending on whether you want the exception to be checked at compile-time or runtime, your class will extend:

- **java.lang.Exception**: To create a **Checked Exception**.
- **java.lang.RuntimeException**: To create an **Unchecked Exception**.

### Basic Syntax

```java
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        // Delegate message string initialization to the parent Exception constructor
        super(message);
    }
}
```

# Types of Custom Exceptions

Java supports two categories of custom exceptions, each serving a different architectural role:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/user-defined-custom-exception-in-java/1781961484612-d097a35a-9de7-4a02-941f-a43eca8323ee.png)

## 1. Checked Custom Exceptions

Checked custom exceptions extend the `Exception` class directly. The compiler checks these exceptions during compilation. If a method throws a checked exception, the compiler requires that the method either handle it using try-catch blocks or declare it in the method header using the `throws` keyword.

- **Use Case**: Used for recoverable operational failures, such as file access drops or network drops, where the application must recover or retry.

## 2. Unchecked Custom Exceptions

Unchecked custom exceptions extend the `RuntimeException` class. The compiler does not verify these exceptions at compile-time. Handling or declaring unchecked exceptions is optional.

- **Use Case**: Used for programming errors, API contract violations, or unrecoverable system states where program continuation is not possible.

# Creating a Custom Exception

To implement a custom exception class in Java:

1. **Create Class**: Define a new class naming it descriptively, always suffixing with `Exception`.
2. **Extend Superclass**: Extend `Exception` (checked) or `RuntimeException` (unchecked).
3. **Define Constructor**: Implement a constructor accepting a `String message` and delegate it using `super(message)`.
4. **Trigger throw**: Use the `throw new CustomException("Message")` statement to raise the error in your validation logic.

# Example 1: Invalid Age Exception (Checked Exception)

### Custom Exception Class

```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

### Main Program

```java
public class RegistrationSystem {
    // Declaring checked exception using throws
    static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or above.");
        }
        System.out.println("Registration Successful");
    }

    public static void main(String[] args) {
        try {
            validateAge(16);
        } catch (InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Age must be 18 or above.

# Example 2: Student Marks Validation

### Custom Exception

```java
class InvalidMarksException extends Exception {
    public InvalidMarksException(String message) {
        super(message);
    }
}
```

### Main Program

```java
public class Student {
    static void validateMarks(int marks) throws InvalidMarksException {
        if (marks < 0 || marks > 100) {
            throw new InvalidMarksException("Marks must be between 0 and 100");
        }
        System.out.println("Marks Accepted");
    }

    public static void main(String[] args) {
        try {
            validateMarks(150);
        } catch (InvalidMarksException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Marks must be between 0 and 100

# Example 3: Attendance Validation

### Custom Exception

```java
class LowAttendanceException extends Exception {
    public LowAttendanceException(String message) {
        super(message);
    }
}
```

### Main Program

```java
public class AttendanceSystem {
    static void checkAttendance(int attendance) throws LowAttendanceException {
        if (attendance < 75) {
            throw new LowAttendanceException("Attendance below 75%");
        }
        System.out.println("Eligible for Exams");
    }

    public static void main(String[] args) {
        try {
            checkAttendance(68);
        } catch (LowAttendanceException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Attendance below 75%

# Example 4: Insufficient Balance Exception

### Custom Exception

```java
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}
```

### Main Program

```java
public class BankAccount {
    static void withdraw(double balance, double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient Balance");
        }
        System.out.println("Withdrawal Successful");
    }

    public static void main(String[] args) {
        try {
            withdraw(5000, 7000);
        } catch (InsufficientBalanceException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Insufficient Balance

# Unchecked Custom Exception

Unchecked custom exceptions extend `RuntimeException`. They are checked at runtime and do not require declaration in method headers.

## Example: Invalid Password Exception

### Custom Exception

```java
class InvalidPasswordException extends RuntimeException {
    public InvalidPasswordException(String message) {
        super(message);
    }
}
```

### Main Program

```java
public class LoginSystem {
    static void validatePassword(String password) {
        if (password.length() < 8) {
            throw new InvalidPasswordException("Password too short");
        }
        System.out.println("Valid Password");
    }

    public static void main(String[] args) {
        // Handling is optional; unchecked exception will bubble to JVM if unhandled
        validatePassword("abc");
    }
}
```

### Output
Exception in thread "main" InvalidPasswordException: Password too short
	at LoginSystem.validatePassword(LoginSystem.java:5)
	at LoginSystem.main(LoginSystem.java:11)

# Using throws with Custom Exception

Checked custom exceptions must be declared in the method signature using the `throws` keyword. This informs calling classes that invoking this method might raise this checked exception type:

```java
static void validateAge(int age) throws InvalidAgeException
```

# Using throw with Custom Exception

The `throw` keyword is used inside the method validation body to manually trigger the exception, instantiating the exception object using the `new` keyword:

```java
throw new InvalidAgeException("Age must be 18 or above");
```

# Custom Exception with Multiple Constructors

For robust design, custom exceptions should provide multiple constructors. This allows wrapping other exceptions (exception chaining) or raising default errors without detail messages:

```java
class InvalidEmployeeException extends Exception {
    // Default constructor
    public InvalidEmployeeException() {
        super();
    }

    // Message constructor
    public InvalidEmployeeException(String message) {
        super(message);
    }

    // Chaining constructor: wraps another throwable cause
    public InvalidEmployeeException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

# Real-World Example: AlphaKnowledge Student Portal

Here is a practical integration of checked custom exceptions inside a student validation workflow:

```java
class InvalidStudentIdException extends Exception {
    public InvalidStudentIdException(String message) {
        super(message);
    }
}

public class StudentPortal {
    static void verifyStudentId(int id) throws InvalidStudentIdException {
        if (id <= 0) {
            throw new InvalidStudentIdException("Student ID must be positive");
        }
        System.out.println("Student Verified");
    }

    public static void main(String[] args) {
        try {
            verifyStudentId(-101);
        } catch (InvalidStudentIdException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Student ID must be positive

# Internal Working

When a custom exception is thrown, the JVM executes its standard stack trace capture and catch block search:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/user-defined-custom-exception-in-java/1781961595924-47356bf0-8a8c-45fa-9a3c-a320502ba105.png)

     

# Checked vs Unchecked Custom Exceptions

| Feature | Checked Exception | Unchecked Exception |
| --- | --- | --- |
| **Parent Class** | `java.lang.Exception` | `java.lang.RuntimeException` |
| **Compile-Time Check** | Enforced by the compiler. | Not verified at compile-time. |
| **Mandatory Handling** | Yes (must catch or declare `throws`). | No (optional handling). |
| **throws Signature** | Required in the throwing method's signature. | Not required. |
| **Primary Use Case** | Recoverable business logic errors. | Programming mistakes or logical failures. |

# Advantages of Custom Exceptions

- **Meaningful Diagnostics**: Error classes match business terms (e.g. `LowAttendanceException`), making logs easy to parse.
- **Better Debugging**: Stack traces show the exact domain exception name, pointing directly to the business rule violation.
- **Improved Maintainability**: Separates validation rules from exception handling, allowing updates to validation checks without modifying error reporting paths.
- **Separation of Concerns**: Business validation logic throws the error, while the caller layer handles the recovery.

# Limitations of Custom Exceptions

- **Additional Classes**: Requires creating new classes, increasing class counts.
- **Increased Complexity**: Overusing custom exceptions for trivial bugs can make the codebase harder to maintain.
- **Overuse Risk**: Creating unique custom exception classes for minor variations of identical errors is an anti-pattern.

# Best Practices

### Use Specific Names

Name your custom exception classes clearly to reflect the business error, and always suffix the class name with `Exception`.

- **Good**: `InvalidAgeException`, `InsufficientBalanceException`, `LowAttendanceException`.
- **Bad**: `MyException`, `UserError`.

### Provide Meaningful Messages

When throwing the exception, pass detail messages explaining the parameters that caused the failure:

```java
throw new InvalidMarksException("Marks must be between 0 and 100");
```

### Extend Correct Parent Class

Extend `Exception` for recoverable situations (where the caller can take corrective action) and `RuntimeException` for programming mistakes or unrecoverable system failures.

### Keep Exception Classes Simple

Do not add complex business logic or methods inside custom exception classes. They should remain simple message and stack trace wrappers.

# 

# Summary

A User-Defined Custom Exception is an exception created by the programmer to represent application-specific errors that cannot be effectively handled using Java's built-in exceptions. Custom exceptions improve code readability, debugging, maintainability, and error reporting by providing meaningful exception names and messages. They can be classified into checked exceptions (extending Exception) and unchecked exceptions (extending RuntimeException). Custom exceptions are widely used in real-world applications such as banking systems, student portals, inventory management systems, and authentication modules to represent business logic errors in a clean and professional manner.




