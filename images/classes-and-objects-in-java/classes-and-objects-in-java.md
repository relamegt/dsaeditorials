# Classes and Objects in Java

## Introduction

In the world of software engineering, Object-Oriented Programming (OOP) was designed to solve the limitations of procedural programming by structuring software around real-world entities rather than logical functions alone. The most fundamental building blocks of this paradigm in Java are **Classes** and **Objects**.

A program in Java can be thought of as a collection of coordinating objects that communicate by invoking methods on one another. Transitioning to an object-oriented mindset requires understanding that code is not merely a sequence of instructions, but an ecosystem of independent entities that maintain their own data (state) and define their own operations (behavior). By organizing programs around classes and objects, developers can create applications that are modular, secure, easy to test, and highly scalable.

## Real-Life Analogy: The Car Blueprint and the Real Car

To understand the relationship between a class and an object, consider the automotive industry:

- A car manufacturer first designs a **blueprint** of a car. This blueprint specifies the dimensions, engine model, seat count, and electrical circuits. The blueprint itself is not a car; you cannot drive it, and it does not take up space in a garage. This blueprint represents a **Class**.
- From this single blueprint, the factory manufactures thousands of **physical cars** (e.g., a red sedan, a blue SUV). Each physical car is real, takes up space on the road, has a current fuel level, and can be driven. These physical cars represent **Objects**.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/classes-and-objects-in-java/1781936353911-557783bd-3e89-4332-9380-e3089b38f5bf.png)

# What is a Class?

A **Class** is a user-defined template or blueprint from which objects are created. It defines the structure, variables, and methods that the created objects will possess.

From a memory perspective, a class is a static logical construct. When you define a class in Java, the JVM loads the class metadata into a special memory area called the **Metaspace** (or **PermGen** in older Java versions). No runtime memory is allocated in the Heap for instance variables until you create an actual object from that class.

## Syntax of a Class

A class definition in Java is declared using the `class` keyword and can contain variables, methods, constructors, initialization blocks, and nested classes:

```java
class ClassName {

    // 1. Instance Variables (State)
    // 2. Methods (Behavior)
    // 3. Constructors (Initialization)
    // 4. Initialization Blocks (Static/Instance)
    // 5. Nested Classes or Interfaces
}
```

## Detailed Example: Student Class

Let's look at a complete example defining a class representing a student, instantiating it, and displaying its data:

```java
class Student {

    int rollNo;
    String name;

    void display() {
        System.out.println(rollNo + " - " + name);
    }
}

public class Main {

    public static void main(String[] args) {

        Student s1 = new Student();

        s1.rollNo = 101;
        s1.name = "Mohit";

        s1.display();
    }
}
```

### Output
101 - Mohit

### Explanation

- `Student` is the class name, representing our custom blueprint.
- `rollNo` and `name` are instance variables representing the attributes a student object holds.
- `display()` is an instance method defining the behavior of the student.
- In the `Main` class, `new Student()` instantiates a physical object of the Student class, and its address is assigned to the reference variable `s1`.

# Components of a Class

A robust class structure in Java can contain the following five components:

| Component | Technical Description | Purpose |
| --- | --- | --- |
| **Variables (Fields)** | Data fields that store the state of the object. Can be instance variables (unique to each object) or static variables (shared across all objects of the class). | Represent the data or attributes of the object. |
| **Methods** | Blocks of code that define the actions or behaviors an object can perform. | Implement operations, calculations, and data updates. |
| **Constructors** | Special blocks of code called during object instantiation to initialize variables. They do not have return types. | Ensure objects start in a valid, fully initialized state. |
| **Blocks** | Blocks of code enclosed in braces `{}`. Can be Instance Initializer Blocks (run during object creation) or Static Blocks (run when class is loaded). | Used for complex initialization logic. |
| **Nested Classes / Interfaces** | A class or interface defined inside another class to logically group components. | Improve helper class containment and encapsulation. |

# What is an Object?

An **Object** is a basic unit of Object-Oriented Programming and represents a physical or logical real-world entity. It is an instance of a class that is allocated space in Heap memory.

## Characteristics of an Object

An object is defined by three essential characteristics:

### 1. State (Attributes)

The state of an object is represented by its attributes or properties. It reflects the current values stored in the object's instance variables. For example, a student object's state might be `name = "Mohit"` and `rollNo = 101`.

### 2. Behavior (Methods)

The behavior of an object is represented by its methods. It defines the operations the object can perform and how it responds to requests. For example, a student object's behavior might be `study()` or `payFees()`.

### 3. Identity

The identity of an object is a unique key or address that distinguishes it from all other objects of the same type. The JVM maintains this identity internally (typically using the object's memory address). Even if two student objects have identical values for `name` and `rollNo`, they remain distinct objects with unique identities in memory.

## Detailed Example: Smartphone Object

Let's model a smartphone to see state, behavior, and identity in action:

```java
class Smartphone {

    String brand;
    String model;

    void makeCall(String contactName) {
        System.out.println(brand + " " + model + " is calling " + contactName);
    }
}

public class Main {

    public static void main(String[] args) {

        Smartphone phone1 = new Smartphone();
        phone1.brand = "Apple";
        phone1.model = "iPhone 15";

        Smartphone phone2 = new Smartphone();
        phone2.brand = "Samsung";
        phone2.model = "Galaxy S23";

        phone1.makeCall("Mohit");
        phone2.makeCall("Akash");
    }
}
```

### Output
Apple iPhone 15 is calling Mohit
Samsung Galaxy S23 is calling Akash

### Explanation

We created two distinct objects (`phone1` and `phone2`) from the `Smartphone` class. Each maintains its own independent state (`brand` and `model`) and performs behaviors unique to its instance.

# Memory Representation

Understanding how Java manages memory for classes and objects is essential for writing efficient, leak-free applications. The JVM uses two primary memory areas:

- **Stack Memory**: Used to store local variables and references to objects. When you declare `Student s1;`, the reference variable `s1` is allocated in the Stack.
- **Heap Memory**: Used to store the actual object data. When you call `new Student()`, the object is allocated in the Heap, and its address is returned to the Stack reference variable.

### Memory Representation Diagram

```text
STACK MEMORY                               HEAP MEMORY
 ┌──────────────┐                        ┌──────────────────────────────┐
 │  main() frame│                        │                              │
 │              │                        │   Student Object             │
 │  s1 Reference├───────────────────────►│  ┌────────────────────────┐  │
 │  (Address 1) │                        │  │ rollNo = 101           │  │
 │              │                        │  │ name = "Mohit"         │  │
 │  s2 Reference├────────────┐           │  └────────────────────────┘  │
 │  (Address 2) │            │           │                              │
 └──────────────┘            │           │   Student Object             │
                             │           │  ┌────────────────────────┐  │
                             └──────────►│  │ rollNo = 102           │  │
                                         │  │ name = "Akash"         │  │
                                         │  └────────────────────────┘  │
                                         └──────────────────────────────┘
```

When an object in the Heap has no references pointing to it in the Stack (e.g., if you assign `s1 = null;`), it becomes unreachable and is marked for deletion by Java's automatic Garbage Collector.

# Object Instantiation

The process of creating an object is known as **Instantiation**. In Java, instantiation is a three-step process:

## Step 1: Declaration

Declares a reference variable with a class type. This does not allocate memory for the object yet.

```java
Student s1;
```

- **Memory Status**: A reference variable `s1` is created on the stack, initialized with a value of `null`.

## Step 2: Creation

Allocates physical memory in the Heap for the object's attributes. This is triggered by the `new` keyword.

```java
s1 = new Student();
```

- **Memory Status**: The `new` keyword allocates space for instance variables in Heap memory and calls the class constructor to set default values.

## Step 3: Initialization

Assigns custom values to the allocated instance fields.

```java
s1.name = "Mohit";
s1.rollNo = 101;
```

- **Memory Status**: The memory slots in the Heap are populated with the actual data values (`"Mohit"`, `101`).

# Complete Example: Instantiation Steps

```java
class Book {

    String title;
    double price;

    void displayDetails() {
        System.out.println(title + " - $" + price);
    }
}

public class Main {

    public static void main(String[] args) {

        // 1. Declaration
        Book myBook;

        // 2. Creation and Initialization
        myBook = new Book();
        myBook.title = "Java Programming Guide";
        myBook.price = 45.99;

        myBook.displayDetails();
    }
}
```

### Output
Java Programming Guide - $45.99

# Object Initialization Styles

Java supports three ways to initialize objects:

1. **Using a Reference Variable**: Assigning values directly to fields (e.g., `s1.name = "Mohit"`). This violates encapsulation but is common in simple scripts.
2. **Using a Method**: Initializing variables inside a custom method (commonly helper setter methods).
3. **Using a Constructor**: Initializing fields during object creation. This is the most standard, clean, and robust design.

## Example: Constructor vs Setter Methods

This example demonstrates both constructor and method-based initialization:

```java
class Course {

    String title;
    String instructor;

    // Style A: Constructor Initialization
    Course(String title, String instructor) {
        this.title = title;
        this.instructor = instructor;
    }

    // Style B: Method Initialization
    void updateInstructor(String newInstructor) {
        this.instructor = newInstructor;
    }

    void display() {
        System.out.println(title + " taught by " + instructor);
    }
}

public class Main {

    public static void main(String[] args) {

        // Initialize using Constructor
        Course c1 = new Course("Java OOP Concepts", "AlphaKnowledge");
        c1.display();

        // Update / Initialize using Method
        c1.updateInstructor("Professor Mohit");
        c1.display();
    }
}
```

### Output
Java OOP Concepts taught by AlphaKnowledge
Java OOP Concepts taught by Professor Mohit

# Ways to Create Objects in Java

Java is a highly dynamic language and supports five different ways to create objects, depending on runtime requirements:

## 1. Using the new Keyword

The most common and straightforward method. It allocates memory and executes the constructor.

```java
Student s = new Student();
```

## 2. Using Reflection (Class.newInstance)

Allows creating objects dynamically at runtime when the class name is determined as a String. This is heavily used by frameworks like Spring, Hibernate, and JUnit to load classes dynamically.

```java
class DatabaseDriver {

    public DatabaseDriver() {
        System.out.println("Driver Object Initialized Dynamically.");
    }
}

public class Main {

    public static void main(String[] args) throws Exception {

        // Dynamic Loading of Class using Reflection
        Class<?> cls = Class.forName("DatabaseDriver");
        DatabaseDriver driver = (DatabaseDriver) cls.getDeclaredConstructor().newInstance();
    }
}
```

### Output
Driver Object Initialized Dynamically.

## 3. Using the clone() Method

Creates a bit-wise copy of an existing object without running constructor logic. The class must implement the `Cloneable` marker interface, otherwise it throws a `CloneNotSupportedException`.

```java
class Course implements Cloneable {

    String name;

    Course(String name) {
        this.name = name;
    }

    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

public class Main {

    public static void main(String[] args) throws Exception {

        Course c1 = new Course("Java Programming");
        Course c2 = (Course) c1.clone();

        System.out.println("Cloned Course: " + c2.name);
    }
}
```

### Output
Cloned Course: Java Programming

## 4. Using Deserialization

Reconstructs an object from a serialized byte stream (e.g., reading an object saved in a file or sent across a network). It reads the class structure and values, recreating the object in the Heap without calling constructors.

```java
// Recreating object from an input stream
Student student = (Student) ois.readObject();
```

# Anonymous Objects

An **Anonymous Object** is an object created without storing its memory reference in a variable. It is created simply to perform a one-time execution and is immediately eligible for garbage collection afterwards.

## Example of Anonymous Objects

```java
class LoggingService {

    void logAlert(String message) {
        System.out.println("ALERT: " + message);
    }
}

public class Main {

    public static void main(String[] args) {

        // Creating and using an anonymous object
        new LoggingService().logAlert("Unusual system login detected.");
    }
}
```

### Output
ALERT: Unusual system login detected.

## Advantages of Anonymous Objects

- **Saves Heap/Stack Space**: Since no reference variable is stored on the Stack, the memory is reclaimed by the garbage collector immediately.
- **Reduces Boilerplate Code**: Useful when you only need to call a single method once and do not need to preserve object state.

# Class vs Object Comparison

| Feature | Class | Object |
| --- | --- | --- |
| **Definition** | A logical template or blueprint that defines state and behaviors. | A physical instance of a class containing real data values. |
| **Memory Allocation** | Does not occupy heap memory for fields. Loaded into Metaspace. | Occupies space in Heap memory for instance variables. |
| **Declaration Keyword** | Defined using the `class` keyword. | Created using the `new` keyword, reflection, or cloning. |
| **Existence** | Exists as static source code definition before compilation. | Exists dynamically at runtime in the JVM memory space. |
| **Quantity** | There is only one class template defined in source code. | A single class can be used to instantiate infinite objects. |

# Real-Life Association Matrix

| Class Name | Real-World Object Instantiations | Properties (State) | Behaviors (Methods) |
| --- | --- | --- | --- |
| **Bank Account** | Account No: 12345, Account No: 67890 | Balance, Account Holder | `deposit()`, `withdraw()`, `checkBalance()` |
| **Employee** | Rahul, Priya, Kiran | Salary, Department, ID | `work()`, `calculateSalary()`, `takeLeave()` |
| **Car** | BMW (Red), Audi (Black), Mercedes (Silver) | Speed, Fuel Level, Gear | `accelerate()`, `applyBrakes()`, `shiftGear()` |
| **Course** | Java Programming, Python Bootcamp | Price, Duration, Instructor | `enrollStudent()`, `startCourse()` |

# Common Developer Mistakes

### 1. Declaring References Without Initializing (NullPointerException)

```java
Student s;
s.display();
```

❌ Runtime Error: `NullPointerException` because the reference variable `s` has a value of `null` and does not point to an object in the Heap.

### Correct Implementation

```java
Student s = new Student();
s.display();
```

✅ Object created and reference assigned before calling methods.

# Summary

Classes and Objects form the foundation of Java Object-Oriented Programming. A class acts as a blueprint that defines properties and behaviors, while an object is a real instance of that blueprint containing actual data. Objects are created through instantiation using the `new` keyword, constructors, reflection, cloning, or deserialization. Understanding classes and objects is essential because all advanced OOP concepts such as inheritance, polymorphism, abstraction, and encapsulation are built on top of them.




