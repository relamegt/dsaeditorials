# Exception Handling with Method Overriding in Java

## Introduction

Exception handling with method overriding is an important concept in Java that combines two Object-Oriented Programming concepts:

- Method Overriding
- Exception Handling

When a subclass overrides a method of its superclass, Java imposes certain rules on the exceptions that can be declared in the overridden method. These rules ensure type safety and prevent unexpected behavior during runtime.

# Why Are These Rules Needed?

Consider the following situation:

A superclass method promises that it throws only certain exceptions.

If the subclass suddenly throws completely different checked exceptions, code written using the superclass reference may fail unexpectedly.

To avoid this problem, Java restricts checked exceptions during method overriding.

# Important Rules

## Rule 1: Subclass Can Throw Same Exception

The overridden method can throw exactly the same exception as the parent method.

```java
import java.io.IOException;

class AlphaKnowledge {

    void display() throws IOException {
        System.out.println("Parent Method");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void display() throws IOException {
        System.out.println("Child Method");
    }
}
```

## Rule 2: Subclass Can Throw Child Exception

The subclass may throw a narrower (child) exception.

```java
import java.io.IOException;
import java.io.FileNotFoundException;

class AlphaKnowledge {

    void openFile() throws IOException {
        System.out.println("Opening File");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void openFile() throws FileNotFoundException {
        System.out.println("Opening Student File");
    }
}
```

### Why Allowed?

Because:

FileNotFoundException IS-A IOException
So the compiler considers it safe.

## Rule 3: Subclass Can Remove Exception Completely

The overridden method may choose not to throw any exception.

```java
import java.io.IOException;

class AlphaKnowledge {

    void startCourse() throws IOException {
        System.out.println("Course Started");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void startCourse() {
        System.out.println("Java Course Started");
    }
}
```

## Rule 4: Subclass Cannot Throw Broader Checked Exception

This is not allowed.

```java
import java.io.IOException;

class AlphaKnowledge {

    void display() throws IOException {
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void display() throws Exception {
    }
}
```

### Compile-Time Error

Exception is broader than IOException

### Reason

The parent method promises only IOException.

The child method cannot suddenly throw a larger exception hierarchy.

# Checked vs Unchecked Exceptions

Before understanding the rules, remember:

## Checked Exceptions

Checked exceptions are verified at compile time.

Examples:

```java
IOException
SQLException
ClassNotFoundException
InterruptedException
FileNotFoundException
```

## Unchecked Exceptions

Unchecked exceptions are checked during runtime.

Examples:

```java
ArithmeticException
NullPointerException
ArrayIndexOutOfBoundsException
NumberFormatException
IllegalArgumentException
```

# Problem 1: Parent Method Does Not Declare Any Exception

## Case 1: Child Declares Checked Exception

### Not Allowed

```java
import java.io.IOException;

class AlphaKnowledge {

    void learnJava() {
        System.out.println("Learning Java");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void learnJava() throws IOException {
        System.out.println("Advanced Java");
    }
}
```

### Result

Compile Time Error

### Reason

Parent method does not declare any checked exception.

Therefore child method cannot introduce a new checked exception.

## Case 2: Child Declares Unchecked Exception

### Allowed

```java
class AlphaKnowledge {

    void learnJava() {
        System.out.println("Learning Java");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void learnJava() throws ArithmeticException {

        System.out.println("Advanced Java");
    }
}

public class Main {

    public static void main(String[] args) {

        AlphaKnowledge obj = new Mohit();
        obj.learnJava();
    }
}
```

### Output
Advanced Java

### Why Allowed?

ArithmeticException is an unchecked exception.

Java does not restrict unchecked exceptions during overriding.

# Problem 2: Parent Method Declares Exception

## Case 1: Child Declares Unrelated Checked Exception

### Not Allowed

```java
import java.io.IOException;

class AlphaKnowledge {

    void project() throws IOException {
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void project() throws ClassNotFoundException {
    }
}
```

### Result

Compile Time Error

### Reason

ClassNotFoundException is not a child of IOException.

## Case 2: Child Declares Child Exception

### Allowed

```java
import java.io.IOException;
import java.io.FileNotFoundException;

class AlphaKnowledge {

    void readData() throws IOException {

        System.out.println("Reading Data");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void readData() throws FileNotFoundException {

        System.out.println("Reading Student Data");
    }
}

public class Main {

    public static void main(String[] args) throws Exception {

        AlphaKnowledge obj = new Mohit();
        obj.readData();
    }
}
```

### Output
Reading Student Data

## Case 3: Child Declares No Exception

### Allowed

```java
import java.io.IOException;

class AlphaKnowledge {

    void uploadProject() throws IOException {

        System.out.println("Project Uploaded");
    }
}

class Mohit extends AlphaKnowledge {

    @Override
    void uploadProject() {

        System.out.println("Java Project Uploaded");
    }
}

public class Main {

    public static void main(String[] args) {

        AlphaKnowledge obj = new Mohit();

        try {
            obj.uploadProject();
        }
        catch (IOException e) {

            System.out.println(e);
        }
    }
}
```

### Output
Java Project Uploaded

# Unchecked Exception Example

Unchecked exceptions can always be added in overridden methods.

```java
class Course {

    void enroll() {

        System.out.println("Student Enrolled");
    }
}

class JavaCourse extends Course {

    @Override
    void enroll() throws NullPointerException {

        System.out.println("Java Student Enrolled");

        throw new NullPointerException("Invalid Student");
    }
}

public class Main {

    public static void main(String[] args) {

        Course c = new JavaCourse();

        try {
            c.enroll();
        }
        catch (NullPointerException e) {

            System.out.println(e.getMessage());
        }
    }
}
```

### Output
Java Student Enrolled
Invalid Student

# Real-Life Example

Consider an online learning platform AlphaKnowledge.

Parent class:

```java
class Course {

    void submitAssignment() throws Exception {
    }
}
```

Child class:

```java
class JavaCourse extends Course {

    @Override
    void submitAssignment() throws FileNotFoundException {
    }
}
```

This is valid because:

FileNotFoundException
        ↓
IOException
        ↓
Exception
The child exception is smaller and safer.

# Rules Summary Table

| Parent Method | Child Method | Allowed? |
| --- | --- | --- |
| No Exception | No Exception | Yes |
| No Exception | Checked Exception | No |
| No Exception | Unchecked Exception | Yes |
| Checked Exception | Same Exception | Yes |
| Checked Exception | Child Exception | Yes |
| Checked Exception | Broader Exception | No |
| Checked Exception | No Exception | Yes |
| Unchecked Exception | Any Unchecked Exception | Yes |

# Advantages

- Maintains type safety.
- Prevents unexpected runtime failures.
- Makes inheritance more predictable.
- Ensures reliable polymorphic behavior.
- Improves code maintainability.

# Common Mistakes

### Mistake 1

Throwing a new checked exception in subclass.

```java
void method() throws SQLException
```

when parent throws nothing.

### Mistake 2

Throwing a broader checked exception.

```java
Parent -> IOException

Child -> Exception
```

### Mistake 3

Confusing checked and unchecked exceptions.

```remember
Checked Exceptions
→ Restricted

Unchecked Exceptions
→ Not Restricted
```

## Summary

Exception Handling with Method Overriding in Java defines the rules that control how exceptions can be declared when a subclass overrides a superclass method. Java allows a subclass to throw the same exception, a child exception, or no exception at all, but it does not allow a broader checked exception than the one declared in the superclass method. If the superclass method does not declare any checked exception, the subclass cannot introduce a new checked exception. However, unchecked exceptions such as ArithmeticException and NullPointerException can be freely used in overridden methods. These restrictions ensure type safety, maintain runtime polymorphism, and make programs more reliable and predictable.




