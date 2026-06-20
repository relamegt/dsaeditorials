# Inheritance in Java

## Introduction

**Inheritance** is one of the four fundamental pillars of Object-Oriented Programming (OOP) in Java. It is a powerful mechanism that allows a new class (subclass) to acquire the properties (state variables) and behaviors (methods) of an existing class (superclass).

By using inheritance, developers can define a common baseline class and extend it into specialized classes without rewriting code. This design approach promotes **code reusability**, simplifies **maintainability**, and increases system **extensibility**.

### Key Points

- **Code Reusability**: Subclasses inherit all non-private fields and methods from the parent class automatically, preventing redundant code declarations.
- **IS-A Relationship**: Establishes a hierarchical relationship between the superclass and subclass (e.g., `JavaCourse` IS-A `Course`).
- **Member Access**: A child class inherits the parent's public and protected members directly.
- **Polymorphism**: Facilitates runtime polymorphism through method overriding and dynamic method dispatch.
- **Hierarchy Modeling**: Allows developers to model real-world relationships in a structured and logical class organization.

## Real-Life Example

Consider an online learning platform called **AlphaKnowledge**.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781954738212-644a8a47-ac93-476d-87e8-ed1df76adcbe.png)

Every course on the platform shares common properties, such as a `courseName`, `instructorName`, and `duration`, along with operations like `startCourse()`. Instead of duplicating these fields and methods across every course class, we declare them once in a general parent class named `Course`. The specialized course classes then extend `Course` and inherit all its properties, leaving them free to define only their unique parameters (like compiling environments or specialized compilers).

## Syntax of Inheritance

In Java, inheritance is implemented using the **`extends`** keyword. The keyword signifies that the subclass is extending the capabilities and scope of the parent class.

```java
class Parent {
    // Parent fields and methods
}

class Child extends Parent {
    // Child inherits all non-private members of Parent
    // Child can define additional fields and methods
}
```

## Basic Inheritance Example

```java
class Course {
    void platform() {
        System.out.println("AlphaKnowledge Learning Platform");
    }
}

class JavaCourse extends Course {
    void courseName() {
        System.out.println("Java Programming");
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse c = new JavaCourse();

        // Calling inherited parent method
        c.platform();

        // Calling child method
        c.courseName();
    }
}
```

### Output
AlphaKnowledge Learning Platform
Java Programming

### Explanation

- `Course` is the superclass (parent) defining the baseline method `platform()`.
- `JavaCourse` is the subclass (child) extending `Course`.
- When `new JavaCourse()` is instantiated, the child object directly inherits the `platform()` behavior from its parent class.

## Important Terminologies

Understanding these standard object-oriented terms is crucial:

| Term | Alternate Names | Description |
| --- | --- | --- |
| **Superclass** | Parent Class / Base Class | The existing class whose members are inherited by another class. |
| **Subclass** | Child Class / Derived Class | The new class that inherits members from the superclass. |
| **`extends`** | Inheritance Keyword | The Java keyword used to establish an inheritance relationship. |
| **IS-A Relationship** | Hierarchy Link | The logical test used to verify inheritance (e.g., `Car` IS-A `Vehicle`). |

## Types of Inheritance in Java

Java supports different types of inheritance structures to model class behaviors:

1. **Single Inheritance**: A subclass inherits from a single superclass.
2. **Multilevel Inheritance**: A subclass inherits from a parent class, which in turn inherits from another class (inheritance chain).
3. **Hierarchical Inheritance**: Multiple subclasses inherit from the same single superclass.
4. **Multiple Inheritance (Achieved via Interfaces)**: A class implements multiple interfaces, inheriting behavioral contracts from each.
5. **Hybrid Inheritance (Achieved via Interfaces)**: A combination of two or more inheritance types.

**Why Java Class Inheritance is Restricted (The Diamond Problem)**

Java does **not** support multiple inheritance with classes (i.e., a class cannot extend more than one class: `class D extends B, C` is illegal). This restriction prevents the **Diamond Problem**:

If Class B and Class C override a method `work()` inherited from Class A, and Class D extends both B and C without overriding `work()`, calling `d.work()` creates a compile-time conflict. The compiler cannot resolve which overridden version of `work()` Class D should inherit:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955734175-fb2b7cb9-08b8-4d38-a663-db7dc043c7f6.png)

To eliminate this ambiguity, Java restricts class inheritance to single parent classes. Multiple interfaces are permitted because interfaces historically did not contain state or implementations. For Java 8 default method conflicts, compilation fails and forces the developer to manually override the conflict in the class.

## 1. Single Inheritance

In Single Inheritance, a child class extends exactly one parent class.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955632762-33fe1e25-8fdd-4f6b-aa50-900206b49841.png)

### Example

```java
class Course {
    void platform() {
        System.out.println("AlphaKnowledge");
    }
}

class JavaCourse extends Course {
    void startCourse() {
        System.out.println("Java Course Started");
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse j = new JavaCourse();
        j.platform();
        j.startCourse();
    }
}
```

### Output
AlphaKnowledge
Java Course Started

## 2. Multilevel Inheritance

In Multilevel Inheritance, a class extends an intermediate subclass, forming an inheritance chain.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955600279-e20c4a5f-82bf-4684-b650-6a862133500d.png)

### Example

```java
class Course {
    void platform() {
        System.out.println("AlphaKnowledge");
    }
}

class ProgrammingCourse extends Course {
    void category() {
        System.out.println("Programming Category");
    }
}

class JavaCourse extends ProgrammingCourse {
    void courseName() {
        System.out.println("Java Programming");
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse j = new JavaCourse();
        j.platform();  // Inherited from Course
        j.category();  // Inherited from ProgrammingCourse
        j.courseName(); // Declared in JavaCourse
    }
}
```

### Output
AlphaKnowledge
Programming Category
Java Programming

## 3. Hierarchical Inheritance

In Hierarchical Inheritance, multiple child classes extend the same parent class, establishing distinct sibling classes.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955564977-d07efc26-07f9-477a-9664-8b6da8978481.png)

**Example**

```java
class Course {
    void platform() {
        System.out.println("AlphaKnowledge");
    }
}

class JavaCourse extends Course {
    void javaInfo() {
        System.out.println("Java Course");
    }
}

class PythonCourse extends Course {
    void pythonInfo() {
        System.out.println("Python Course");
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse j = new JavaCourse();
        PythonCourse p = new PythonCourse();

        j.platform();
        j.javaInfo();

        p.platform();
        p.pythonInfo();
    }
}
```

### Output
AlphaKnowledge
Java Course
AlphaKnowledge
Python Course

## 4. Multiple Inheritance Through Interfaces

Java achieves multiple inheritance behavior by allowing a class to implement multiple interfaces.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955454539-f74acafe-e43e-45c6-bd2d-e982e4c01304.png)

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

## 5. Hybrid Inheritance

Hybrid inheritance is a combination of two or more inheritance structures (e.g., combining hierarchical class structures with interface implementations).

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955377539-033fa631-10f6-4a08-bb5d-8b229ca6dd01.png)

### Example

```java
class Course {
    void platform() {
        System.out.println("AlphaKnowledge");
    }
}

interface Certificate {
    default void certificate() {
        System.out.println("Certificate Available");
    }
}

class JavaCourse extends Course implements Certificate {
    void courseName() {
        System.out.println("Java Programming");
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse j = new JavaCourse();
        j.platform();
        j.courseName();
        j.certificate(); // Inherited default method from interface
    }
}
```

### Output
AlphaKnowledge
Java Programming
Certificate Available

## Constructor Inheritance & Chaining

An important rule in Java is that **subclass constructors do not inherit superclass constructors**. Because constructors are specific to initializing their own class variables, they cannot be inherited like standard methods.

### Constructor Chaining Mechanics

Although parent constructors are not inherited, the subclass constructor **must** invoke the superclass constructor as the absolute first step of object instantiation. This process is called **constructor chaining**:

1. **Implicit `super()` Call**: If you do not write an explicit call to the parent constructor, the Java compiler automatically inserts an implicit, parameterless call to `super()` as the first statement in the child constructor.
2. **Missing Default Constructor Pitfall**: If a parent class declares only parameterized constructors (meaning it does not contain a default, parameterless constructor), the compiler cannot insert the default `super()` call. The subclass constructor must explicitly invoke the parent constructor using `super(arguments)` on the first line. Failing to do so triggers a compile-time error.

### Example

```java
class Course {
    Course() {
        System.out.println("Course Constructor");
    }
}

class JavaCourse extends Course {
    JavaCourse() {
        // Implicit super() is automatically inserted here by the compiler
        System.out.println("JavaCourse Constructor");
    }
}

public class Main {
    public static void main(String[] args) {
        new JavaCourse();
    }
}
```

### Output
Course Constructor
JavaCourse Constructor

## Method Overriding in Inheritance

**Method Overriding** occurs when a subclass provides a specific implementation for a method that is already declared in its superclass. This allows the child class to customize parent behaviors.

### Rules of Method Overriding

To override a parent method successfully, the subclass implementation must follow these rules:

1. **Identical Signature**: The method name and parameter types must match the parent method exactly.
2. **Covariant Return Types**: The return type can be identical to the parent method's return type, or a subclass of it (e.g., if parent returns `Number`, child can return `Integer`).
3. **Access Modifier Rules**: The subclass method cannot reduce the visibility of the parent method. If the parent method is `protected`, the child method must be `protected` or `public`. It cannot be marked as private or default.
4. **Exception Handling**: The overriding method cannot throw broader or new checked exceptions than those declared by the superclass method.
5. **Final/Static Constraints**: Methods marked as `final` or `static` cannot be overridden.

### The `@Override` Annotation

Always annotate overridden methods with `@Override`. This annotation instructs the compiler to verify that the method matches a signature in the superclass, preventing spelling mistakes and accidental method overloading.

### Example

```java
class Trainer {
    void teach() {
        System.out.println("General Teaching");
    }
}

class JavaTrainer extends Trainer {
    @Override
    void teach() {
        System.out.println("Teaching Java");
    }
}

public class Main {
    public static void main(String[] args) {
        Trainer t = new JavaTrainer(); // Polymorphism
        t.teach();
    }
}
```

### Output
Teaching Java

## The super Keyword

The **`super`** keyword is a reference variable used in subclass implementations to access members of the parent class directly.

### The Three Uses of `super`

1. **Access Parent Fields**: Resolve shadowing when subclass instance variables have the same name as parent fields (`super.variableName`).
2. **Call Parent Methods**: Execute the parent's version of a method that the child has overridden (`super.methodName()`).
3. **Invoke Parent Constructors**: Call the parent constructor from the subclass constructor (`super(arguments)`).

### Example

```java
class Course {
    String platform = "AlphaKnowledge";
}

class JavaCourse extends Course {
    String platform = "Java Academy";

    void display() {
        // 'platform' refers to local child field
        System.out.println("Child Platform: " + platform);

        // 'super.platform' refers to parent field
        System.out.println("Parent Platform: " + super.platform);
    }
}

public class Main {
    public static void main(String[] args) {
        JavaCourse j = new JavaCourse();
        j.display();
    }
}
```

### Output
Child Platform: Java Academy
Parent Platform: AlphaKnowledge

## IS-A Relationship & instanceof

Inheritance represents a strict **IS-A** relationship. If class `Dog` extends class `Animal`, it is physically correct to say "a Dog IS-A Animal".

### The `instanceof` Operator and Safe Downcasting

The `instanceof` operator evaluates whether an object reference belongs to a specific class type or inherits from it, returning a boolean result. This operator is crucial for performing **safe downcasting** (casting a parent reference back to a child reference type). Attempting to downcast an object reference without verifying its type using `instanceof` can trigger a `ClassCastException` at runtime.

### Example

```java
class Student {
}

class Mohit extends Student {
}

public class Main {
    public static void main(String[] args) {
        Student s = new Mohit(); // Upcasting (implicitly safe)

        // Verifying type before downcasting
        if (s instanceof Mohit) {
            Mohit m = (Mohit) s; // Safe downcasting
            System.out.println("Downcasting completed safely.");
        }

        System.out.println("s instanceof Mohit: " + (s instanceof Mohit));
        System.out.println("s instanceof Student: " + (s instanceof Student));
    }
}
```

### Output
Downcasting completed safely.
s instanceof Mohit: true
s instanceof Student: true

## What Can a Subclass Do?

A subclass inherits non-private members and can perform the following modifications:

- **Use Inherited Fields**: Read and update non-private parent variables directly.
- **Use Inherited Methods**: Call non-private parent operations.
- **Override Methods**: Replace parent method behaviors with custom subclass implementations.
- **Add New Fields**: Declare variables unique to the subclass.
- **Add New Methods**: Define operations unique to the subclass.
- **Invoke Super Constructors**: Call parameterized or default parent constructors using `super()`.

## Advantages of Inheritance

- **Code Reusability**: Eliminates redundant declarations by inheriting common features from parent templates.
- **Clean System Hierarchies**: Establishes logical relationships, organizing classes from general categories to specific structures.
- **Simpler Maintenance**: Updates or bug fixes in the parent class propagate to all subclasses automatically.
- **Polymorphic Flexibility**: Allows programs to write clean interfaces that operate on parent reference variables while executing subclass implementations at runtime.

## Limitations of Inheritance

- **Tight Coupling**: Subclasses depend heavily on parent class structures. If the parent class changes, child classes may break.
- **Increased Complexity**: Deep or nested inheritance chains are difficult to read and manage.
- **Fragile Base Class Issue**: Modifications in base classes can lead to unexpected runtime side effects in distant subclasses.
- **Loss of Flexibility**: Inheritance is resolved statically at compile time; you cannot change an object's parent class at runtime.

## Common Mistakes

### 1. Creating Deep Inheritance Nesting

Creating deep, multi-level class chains makes code comprehension and debugging difficult.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-java/1781955304885-aa608c2a-1ff4-4028-8a80-c7b8268a553f.png)

### 2. Using Inheritance for Code Sharing Only

Inheritance should only be used if a logical **IS-A** relationship exists. If you only want to reuse code from class A inside class B without establishing an IS-A relationship, use **composition** instead of inheritance.

```java
class Engine {
    void start() {}
}

// ❌ Wrong: A Car IS-A Engine is logically incorrect
class Car extends Engine {}
```

### 3. Forgetting Method Overriding Rules

Attempting to override a parent method while slightly altering parameter signatures results in method overloading instead of overriding. Always use the `@Override` annotation to catch signature mismatches at compile time.

## Inheritance vs Composition

Understanding when to use Inheritance (IS-A) versus Composition (HAS-A) is a key software design consideration.

### The "Composition over Inheritance" Principle

- **Inheritance (IS-A)**: Binds subclasses to superclasses at compile time. It is known as "white-box reuse" because parent details are visible to subclasses. It creates tight coupling and can break encapsulation if parent details are modified.
- **Composition (HAS-A)**: Involves referencing helper objects inside classes. It is known as "black-box reuse" because helper details remain hidden. It creates loose coupling and allows you to change helper implementations dynamically at runtime.

| Feature | Inheritance | Composition |
| --- | --- | --- |
| **Relationship** | IS-A (e.g., `JavaCourse` IS-A `Course`). | HAS-A (e.g., `Course` HAS-A `Trainer`). |
| **Binding Time** | Resolved statically at compile time. | Resolved dynamically at runtime. |
| **Coupling Level** | Tightly coupled (child depends on parent). | Loosely coupled (classes interact via public interfaces). |
| **Flexibility** | Less flexible (parent hierarchy is fixed). | Highly flexible (helpers can be swapped at runtime). |

## Summary

*Inheritance** is a fundamental OOP concept that allows one class to acquire the properties and behaviors of another class. It establishes an **IS-A relationship**, promotes code reusability, supports polymorphism, and helps build organized class hierarchies. Java supports **Single**, **Multilevel**, **Hierarchical**, **Multiple (through Interfaces)**, and **Hybrid (through Interfaces)** inheritance. While inheritance reduces code duplication and improves maintainability, it should be used carefully to avoid overly complex class hierarchies and tight coupling between classes.




