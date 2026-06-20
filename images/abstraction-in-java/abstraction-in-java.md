# Abstraction in Java

## Introduction

**Abstraction** is one of the four core pillars of Object-Oriented Programming (OOP) in Java. It is the architectural process of hiding the internal, complex implementation details of a system and showing only the essential, high-level features to the user.

In simple terms:

> Abstraction focuses on **what an object does** rather than **how it does it**.

For example, when you use a mobile phone, you interact with a touchscreen interface to make calls, send texts, and launch applications. You do not need to understand the underlying electrical engineering, radio frequency modulations, or OS kernel scheduling that make those actions possible. The complexity is hidden behind a clean abstraction layer.

## Abstraction vs. Encapsulation

Abstraction and Encapsulation are closely related but serve distinct software design purposes:

| Feature | Abstraction | Encapsulation |
| --- | --- | --- |
| **Core Concept** | Focuses on hiding complex design details (what). | Focuses on hiding internal data state (how). |
| **Implementation** | Achieved using abstract classes and interfaces. | Achieved using access modifiers (`private`, `protected`) and getters/seters. |
| **Focus** | Complexity reduction at the system architecture level. | Data hiding and validation at the class level. |
| **Design Phase** | Occurs during the design/modeling phase. | Occurs during the implementation phase. |

## Why Do We Need Abstraction?

In large-scale application development, implementation structures can become extremely complex. Abstraction provides several critical benefits:

- **Modularity and Decoupling**: Separates the API contract from the concrete implementation, allowing different teams to work on subsystem components independently without introducing code conflicts.
- **Complexity Reduction**: Simplifies system interactions by exposing only high-level methods, reducing the cognitive load on developers using the API.
- **Code Maintainability**: If the internal implementation of a feature changes, the abstract interface remains identical, meaning no client code breaks.
- **Security**: Hides sensitive operational logic and business rules from external classes, exposing only safe execution points.

## Real-Life Example

### ATM Machine

When you withdraw cash from an ATM, you interact with a simple keypad and screen interface. You insert your card, input a PIN, select a withdrawal amount, and collect the cash. You do not see or need to understand how the bank's remote server verifies your credentials, how the database updates your account balance in real time, or how the physical dispenser mechanism separates bills. The user interface abstracts all of these background operations.

## Ways to Achieve Abstraction in Java

Java provides two mechanisms to implement abstraction:

1. **Abstract Class (Partial Abstraction)**: Can achieve 0% to 100% abstraction because it can contain both concrete methods (with implementations) and abstract methods (without implementations).
2. **Interface (Complete Abstraction)**: Achieves 100% behavior abstraction (prior to Java 8's default methods) because it defines pure signatures that implementing classes must satisfy.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/abstraction-in-java/1781953560073-3b13e44c-4b3d-4e12-9241-f3bd7e6543a2.png)

## 

## 1. Abstract Class

An **abstract class** is a class declared using the `abstract` keyword. It serves as a template or blueprint for other subclasses.

### Rules and Constraints

- **Instantiation**: An abstract class cannot be instantiated directly using the `new` keyword (e.g., `new AbstractClass()` will throw a compile error).
- **Abstract Methods**: If a class contains even one abstract method, the class itself **must** be declared abstract.
- **Method Restrictions**: Abstract methods cannot be marked as `private`, `static`, or `final` because they must be overridden and implemented by child classes.
- **Subclass Requirement**: Any class extending an abstract class must implement all inherited abstract methods, or else the subclass itself must also be declared abstract.

### Syntax

```java
abstract class ClassName {
    // Abstract method (no body)
    abstract void methodName();

    // Concrete method (has body)
    void concreteMethod() {
        System.out.println("This is a concrete method.");
    }
}
```

### Example: AlphaKnowledge Learning Platform

```java
abstract class Course {
    String platform;

    Course(String platform) {
        this.platform = platform;
    }

    abstract void startCourse();

    void displayPlatform() {
        System.out.println("Platform: " + platform);
    }
}

class JavaCourse extends Course {
    JavaCourse(String platform) {
        super(platform);
    }

    @Override
    void startCourse() {
        System.out.println("Java Course Started");
    }
}

public class Main {
    public static void main(String[] args) {
        Course c = new JavaCourse("AlphaKnowledge");
        c.displayPlatform();
        c.startCourse();
    }
}
```

### Output
Platform: AlphaKnowledge
Java Course Started

### Example: Student Management System

```java
abstract class Student {
    String name;

    Student(String name) {
        this.name = name;
    }

    abstract void displayDetails();
}

class EngineeringStudent extends Student {
    EngineeringStudent(String name) {
        super(name);
    }

    @Override
    void displayDetails() {
        System.out.println("Student Name: " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new EngineeringStudent("Mohit");
        s.displayDetails();
    }
}
```

### Output
Student Name: Mohit

## Abstract Methods

An **abstract method** is a method that is declared without an implementation (no curly braces, ending with a semicolon). It defines the signature (name, parameters, and return type) that subclasses must implement.

### Syntax

```java
abstract void display();
```

### Example: Employee Directory

```java
abstract class Employee {
    abstract void work();
}

class Developer extends Employee {
    @Override
    void work() {
        System.out.println("Writing Java Code");
    }
}

public class Main {
    public static void main(String[] args) {
        Employee e = new Developer();
        e.work();
    }
}
```

### Output
Writing Java Code

## Abstract Class with Constructor

Although you cannot instantiate an abstract class directly, it can contain a constructor. 

### Why Abstract Classes Have Constructors

Abstract constructors serve two primary purposes:

1. **Initialize Common State**: They allow you to initialize common instance fields shared by all subclasses.
2. **Enforce Construction Rules**: When a child class is instantiated using `new SubClass()`, the JVM chains the constructors, running the abstract superclass's constructor first (via `super()`) before executing the subclass constructor.

### Real-Time Example: Database Reader Engine

Suppose you are building a database reporting engine. Every reader needs a connection string, but the actual parsing logic depends on the specific database format. We use the abstract constructor to initialize the common connection string.

```java
abstract class DatabaseReader {
    String connectionString;

    // Constructor to initialize database connection settings
    DatabaseReader(String connectionString) {
        this.connectionString = connectionString;
        System.out.println("DatabaseReader configured with connection string.");
    }

    abstract void readData();
}

class MySQLReader extends DatabaseReader {
    MySQLReader(String connStr) {
        super(connStr); // Passes connection settings to parent constructor
    }

    @Override
    void readData() {
        System.out.println("Connecting to MySQL using: " + connectionString);
        System.out.println("Fetching records...");
    }
}

public class Main {
    public static void main(String[] args) {
        DatabaseReader reader = new MySQLReader("jdbc:mysql://localhost:3306/db");
        reader.readData();
    }
}
```

### Output
DatabaseReader configured with connection string.
Connecting to MySQL using: jdbc:mysql://localhost:3306/db
Fetching records...

### Constructor Invocation Flow Example

```java
abstract class Student {
    Student() {
        System.out.println("Student Constructor");
    }
}

class Mohit extends Student {
    Mohit() {
        System.out.println("Mohit Constructor");
    }
}

public class Main {
    public static void main(String[] args) {
        new Mohit();
    }
}
```

### Output
Student Constructor
Mohit Constructor

## 2. Interface

An **Interface** is a pure reference type in Java that specifies a set of behaviors a class must implement. It acts as a contract for what a class should do, without defining how it does it.

### Implicit Modifiers in Interfaces

To maintain a clean behavioral structure, the Java compiler automatically applies the following modifiers to interface members:

- **Fields**: Implicitly marked as `public static final`. They are constant fields and must be initialized immediately.
- **Methods**: Implicitly marked as `public abstract` (unless declared as `default`, `static`, or `private`).

### Interface Evolution (Java 8 and 9)

Interfaces have evolved to support functional programming and code reuse without breaking existing implementation structures:

- **Java 8 (Default & Static Methods)**:
- **Default Methods**: Marked with the `default` keyword, these methods can have a body. They allow interfaces to receive new methods without breaking older classes implementing that interface.
- **Static Methods**: These methods behave like utility methods inside the interface namespace and cannot be overridden by implementing classes.
- **Java 9 (Private Methods)**: Interfaces can contain `private` (both static and instance) helper methods. These are used to encapsulate common logic shared between multiple default or static methods without exposing the helper methods to external classes.

### Syntax

```java
interface Shape {
    void draw(); // Implicitly public abstract
}
```

### Example: AlphaKnowledge Courses

```java
interface Course {
    void startCourse();
}

class JavaCourse implements Course {
    public void startCourse() {
        System.out.println("Java Course Started");
    }
}

public class Main {
    public static void main(String[] args) {
        Course c = new JavaCourse();
        c.startCourse();
    }
}
```

### Output
Java Course Started

### Example: Team Members

```java
interface TeamMember {
    void role();
}

class Akash implements TeamMember {
    public void role() {
        System.out.println("Backend Developer");
    }
}

class Hemesh implements TeamMember {
    public void role() {
        System.out.println("Frontend Developer");
    }
}

public class Main {
    public static void main(String[] args) {
        TeamMember t1 = new Akash();
        TeamMember t2 = new Hemesh();

        t1.role();
        t2.role();
    }
}
```

### Output
Backend Developer
Frontend Developer

## Multiple Inheritance Using Interface

Java classes do not support multiple inheritance (extending more than one class) to avoid structural ambiguity. However, a single Java class can implement multiple interfaces, enabling behavioral multiple inheritance.

### The Diamond Problem and Interface Solutions

If a class was allowed to inherit from multiple parent classes, a conflict would arise if both parent classes defined a method with the same signature but different behaviors. The child class would not know which parent method implementation to execute:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/abstraction-in-java/1781953807196-fb2b7cb9-08b8-4d38-a663-db7dc043c7f6.png)

Interfaces bypass the Diamond Problem because they historically contained no implementation logic, only signatures. If a class implements two interfaces containing the same method signature, the class overrides the method once, resolving the implementation details. 

If both interfaces define a `default` method with the same signature, Java throws a compilation error. The developer must resolve this conflict manually by overriding the conflicting method and specifying which interface default method to call using the `SuperInterfaceName.super.methodName()` syntax.

### Example

```java
interface Coding {
    void code();
}

interface Presentation {
    void present();
}

class Mohit implements Coding, Presentation {
    public void code() {
        System.out.println("Writing Code");
    }

    public void present() {
        System.out.println("Giving Presentation");
    }
}

public class Main {
    public static void main(String[] args) {
        Mohit m = new Mohit();
        m.code();
        m.present();
    }
}
```

### Output
Writing Code
Giving Presentation

## Abstract Class vs Interface

| Feature | Abstract Class | Interface |
| --- | --- | --- |
| **Keyword** | Defined using `abstract class`. | Defined using `interface`. |
| **Constructor** | Can contain constructors. | Cannot contain constructors. |
| **Instance Fields** | Can contain instance fields (variables with any access modifier). | Cannot contain instance variables. Variables are implicitly `public static final`. |
| **Methods** | Can contain abstract, concrete, static, and final methods. | Can contain abstract, default, static, and private methods (since Java 9). |
| **Inheritance Limit** | A class can extend only one abstract class (single inheritance limit). | A class can implement multiple interfaces. |
| **Access Modifiers** | Can use any access modifier (`private`, `protected`, `public`) for its members. | All abstract, default, and static methods are implicitly `public`. |

## When to Use Abstract Class?

Use an abstract class when:

- **Shared State/Fields**: You need to define common instance variables (non-static, non-final fields) that child classes will inherit and modify.
- **Code Reusability**: Multiple related classes share a significant amount of identical concrete method logic.
- **Template Method Pattern**: You want to define an execution template containing some fixed concrete steps, leaving specific steps to be implemented by subclasses.

### Example: Vehicle Hierarchy

```text
Vehicle (Abstract Class: defines engineState, startEngine())
│
├── Car (Overridden features)
├── Bike (Overridden features)
└── Bus (Overridden features)
```

## When to Use Interface?

Use an interface when:

- **Polymorphic Contracts**: You want to define a behavioral contract across completely unrelated classes (e.g., `Comparable` can be implemented by both `Student` and `File`).
- **Multiple Inheritance**: A class needs to implement multiple API behaviors.
- **Loose Coupling**: You want to separate the system specifications from implementations completely.

### Example: Shapes Drawable System

```text
Drawable (Interface: defines draw())
│
├── Circle (Implements draw())
├── Rectangle (Implements draw())
└── Triangle (Implements draw())
```

## Common Mistakes

### 1. Creating an Instance of an Abstract Class

You cannot create an object of an abstract class directly.

```java
Shape s = new Shape(); // ❌ Compilation Error: Shape is abstract; cannot be instantiated
```

### 2. Forgetting to Implement Abstract Methods

A concrete subclass extending an abstract class must implement all abstract methods.

```java
class Circle extends Shape {
    // ❌ Compilation Error: Circle must implement the abstract method draw()
}
```

### 3. Reducing Access Visibility on Overrides

When overriding an interface method in a class, you **must** declare the overriding method as `public`. Interface methods are implicitly `public`. Since Java does not allow reducing the visibility of inherited methods, omitting the `public` keyword in the subclass will trigger a compilation error.

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    // ❌ Compilation Error: Cannot reduce the visibility of the inherited method from Shape
    void draw() { 
        System.out.println("Drawing");
    }
}
```

### Correct Implementation

```java
class Circle implements Shape {
    // ✅ Valid override using the public modifier
    public void draw() {
        System.out.println("Drawing");
    }
}
```

## Advantages of Abstraction

- **System Security**: Protects internal data and business rules from corruption by exposing only public methods.
- **Modularity**: Reduces dependencies between components, facilitating easy changes to internal implementations without impacting clients.
- **Cleaner API Interfaces**: Hides complex data transformations and operations, exposing simple method parameters to developers.
- **Scalability**: New subclasses can be added to the inheritance hierarchy with minimal code adjustments.

## Disadvantages of Abstraction

- **Increased Design Complexity**: Introducing interfaces and abstract parent classes increases the class count and overall design efforts.
- **Debugging Hurdles**: Tracing execution routes can become more difficult when methods are decoupled across multiple interfaces and inheritance layers.
- **Overuse Risks**: Creating abstract layers for small or single-use classes reduces code readability and introduces unnecessary boilerplate.

## Abstract Class vs Concrete Class

| Feature | Abstract Class | Concrete Class |
| --- | --- | --- |
| **Object Instantiation** | Not allowed directly. | Fully allowed using the `new` keyword. |
| **Abstract Methods** | Can declare abstract methods. | Cannot contain abstract methods. |
| **Subclass Dependency** | Must be inherited to be useful. | Can be used standalone. |
| **Final Modifier** | Cannot be marked as `final` (conflicts with inheritance). | Can be marked as `final` to prevent subclassing. |

## Real-World Example

### AlphaKnowledge Course System

In this real-life simulation, the abstract class `Course` defines standard properties (like `courseId`, `price`) and standard operations (like `purchaseCourse()`). The specific contents and execution behaviors (like `playVideo()`) are abstract and depend on the course type (such as `VideoCourse` or `InteractiveCodingCourse`).

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/abstraction-in-java/1781954006783-d7e7141b-11ad-4fa5-bd62-77f39ce8a7b5.png)

This model is a prime example of abstraction because students interact with courses through standard methods, while the concrete content delivery remains encapsulated within specific subclasses.

## Summary

Abstraction is the process of hiding implementation details and exposing only essential functionality. Java supports abstraction through Abstract Classes and Interfaces. Abstract classes are used when classes share common state and behavior, while interfaces are used to define common behavior across unrelated classes. Abstraction reduces complexity, improves maintainability, increases security, and helps build scalable real-world applications by focusing on what an object does rather than how it does it.




