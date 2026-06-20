# Polymorphism in Java

## Introduction

**Polymorphism** is one of the four core pillars of Object-Oriented Programming (OOP) in Java. The term is derived from two Greek words: **poly** (meaning "many") and **morph** (meaning "forms").

In software development, polymorphism represents the capability of a single entity (such as a method, an object, or an interface) to behave differently or take on multiple forms depending on the context in which it is executed. It allows developers to write highly flexible, decoupled, and extensible code by separating system specifications from concrete execution actions.

### Key Features

- **Unified Interface**: One interface can have multiple concrete class implementations.
- **Code Reusability**: Enables the same methods or components to operate on different object types, reducing code duplication.
- **Architecture Flexibility**: New subclasses can be integrated into the system hierarchy without modifying existing client-facing code.
- **Dynamic Binding**: Executes the correct subclass method at runtime based on the actual object instance on the heap.

## Real-Life Example

Consider the **AlphaKnowledge Learning Platform**.

The platform coordinates various instructors who teach different subjects. All instructors perform the same high-level action: **`teach()`**.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-java/1781956433956-7ee3fb6b-5281-4a8d-8088-dde3c38adc90.png)

Although the client code calls the same method name `teach()`, the actual behavior differs: the `JavaTrainer` teaches Java syntax, the `PythonTrainer` explains Python libraries, and the `WebTrainer` demonstrates HTML/CSS layout methods. This is polymorphism in action: a single instruction (`teach()`) results in different outcomes depending on the specific object receiving the call.

## Basic Example of Polymorphism

```java
class Trainer {
    void teach() {
        System.out.println("Teaching a course");
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
        // Upcasting: parent reference pointing to child object
        Trainer t = new JavaTrainer();
        t.teach();
    }
}
```

### Output
Teaching Java

### Explanation

- `Trainer` is the superclass.
- `JavaTrainer` is the subclass that overrides `teach()`.
- Upcasting stores the `JavaTrainer` object in a `Trainer` reference variable `t`.
- At runtime, the JVM inspects the actual object type on the heap and executes `JavaTrainer`'s overridden method.

## Types of Polymorphism in Java

Java supports two major classifications of polymorphism:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-java/1781956396522-42e2dce1-3d32-47e5-aabb-629d1698afcb.png)

## 1. Compile-Time Polymorphism

Compile-Time Polymorphism is also known as **Static Polymorphism** or **Early Binding**. In this model, the Java compiler determines exactly which method or constructor signature to execute during compilation, based on compile-time types.

Compile-time polymorphism is achieved using:

- **Method Overloading**
- **Constructor Overloading**

## Method Overloading

Method Overloading occurs when a single class defines multiple methods with the identical name but different parameter lists.

### Rules of Method Overloading

For the compiler to distinguish overloaded methods, the parameter lists must differ in one of the following ways:

1. **Number of Parameters**: E.g., `add(int, int)` vs. `add(int, int, int)`.
2. **Data Types of Parameters**: E.g., `multiply(int, int)` vs. `multiply(double, double)`.
3. **Order of Parameters**: E.g., `print(String, int)` vs. `print(int, String)`.

> The return type and thrown exceptions list are **not** part of a method's signature. Declaring two methods with the same name and parameters but different return types will trigger a compile-time error.

### Automatic Type Promotion in Overload Resolution

When an overloaded method is called, if the compiler cannot find an exact match for the arguments passed, it attempts to resolve the call by promoting the arguments to the next wider compatible type:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-java/1781956358870-bbfab6c5-1450-4962-bfc3-2c287bfdb972.png)

```text
byte ──► short ──► int ──► long ──► float ──► double
                     ▲
                     │
                    char
```

For example, if you call `add(5, 5)` (which are integers) and only `add(long, long)` is defined, the compiler will automatically promote the `int` arguments to `long` and execute the method. If no promotion matches, the compiler attempts autoboxing and varargs resolution.

### Example 1: Different Number of Parameters

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator c = new Calculator();
        System.out.println(c.add(10, 20));
        System.out.println(c.add(10, 20, 30));
    }
}
```

### Output
30
60

### Example 2: Different Data Types

```java
class Calculator {
    int multiply(int a, int b) {
        return a * b;
    }

    double multiply(double a, double b) {
        return a * b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator c = new Calculator();
        System.out.println(c.multiply(5, 4));
        System.out.println(c.multiply(5.5, 2.0));
    }
}
```

### Output
20
11.0

## Constructor Overloading

Constructors can be overloaded in the same manner as methods, allowing objects to be initialized differently depending on the input values available.

### Example

```java
class Student {
    String name;
    int age;

    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student("Mohit", 20);

        s1.display();
        s2.display();
    }
}
```

### Output
Unknown 0
Mohit 20

## Runtime Polymorphism

Runtime Polymorphism is also known as **Dynamic Polymorphism** or **Late Binding**. In this model, the determination of which method to execute is resolved dynamically by the Java Virtual Machine (JVM) during program execution, based on the runtime type of the object.

Runtime polymorphism is achieved using:

- **Method Overriding**

## Method Overriding

Method Overriding occurs when a subclass provides a specific implementation for a method that has already been defined in its parent class.

### Example 1: Course Trainers

```java
class Trainer {
    void teach() {
        System.out.println("Teaching Course");
    }
}

class JavaTrainer extends Trainer {
    @Override
    void teach() {
        System.out.println("Teaching Java");
    }
}

class PythonTrainer extends Trainer {
    @Override
    void teach() {
        System.out.println("Teaching Python");
    }
}

public class Main {
    public static void main(String[] args) {
        Trainer t;

        t = new JavaTrainer();
        t.teach();

        t = new PythonTrainer();
        t.teach();
    }
}
```

### Output
Teaching Java
Teaching Python

## Runtime Method Dispatch

**Runtime Method Dispatch** (or Dynamic Method Dispatch) is the process by which the JVM resolves overridden method calls at runtime.

### How Dynamic Method Dispatch Works Under the Hood

1. **Compilation Phase**: The compiler checks the declared reference type. If the method exists in the reference class, the code compiles successfully (static validation).
2. **Runtime Execution**: When the JVM encounters the method call, it checks the actual object instance stored on the heap.
3. **vtable Lookup**: The JVM accesses the object's class metadata and traverses its Virtual Method Table (**vtable**). The vtable maps method signatures to their execution addresses. If the subclass overrides the method, the vtable points to the child class's overridden method address; otherwise, it falls back to the parent class's method address.
4. **Execution**: The JVM executes the method at the resolved address, achieving dynamic runtime behavior.

### Example

```java
class Employee {
    void work() {
        System.out.println("Employee Working");
    }
}

class Developer extends Employee {
    @Override
    void work() {
        System.out.println("Developer Writing Code");
    }
}

public class Main {
    public static void main(String[] args) {
        // Reference type is Employee, but object type is Developer
        Employee e = new Developer();
        e.work();
    }
}
```

### Output
Developer Writing Code

## Practical Example Using AlphaKnowledge

```java
class Course {
    void startCourse() {
        System.out.println("Course Started");
    }
}

class JavaCourse extends Course {
    @Override
    void startCourse() {
        System.out.println("Java Course Started");
    }
}

class PythonCourse extends Course {
    @Override
    void startCourse() {
        System.out.println("Python Course Started");
    }
}

public class Main {
    public static void main(String[] args) {
        Course c;

        c = new JavaCourse();
        c.startCourse();

        c = new PythonCourse();
        c.startCourse();
    }
}
```

### Output
Java Course Started
Python Course Started

## Rules for Method Overriding

To override a method in Java, the subclass implementation must comply with the following rules:

### Allowed

- **Identical Signature**: The method name and parameter types must match the superclass method exactly.
- **Covariant Return Types**: The return type can be a subclass of the type returned by the parent method.
- **Wider Access Modifiers**: The overriding method can have a more permissive access modifier (e.g., changing `protected` to `public`).

### Not Allowed

- **Narrower Access Modifiers**: You cannot reduce the visibility of the parent method (e.g., changing `public` to `private` will throw a compilation error).
- **Private Methods**: Private methods are bound to their class and cannot be overridden.
- **Final Methods**: Final methods cannot be overridden by subclasses.
- **Static Methods**: Static methods cannot be overridden. If a subclass defines a static method with the same signature, it hides the parent method (method hiding), which is resolved at compile time.

## Polymorphism with Interfaces

Interfaces define pure behavioral contracts and are the primary tool used to implement loose coupling and polymorphism in Java systems.

### Example

```java
interface Learner {
    void learn();
}

class Mohit implements Learner {
    public void learn() {
        System.out.println("Mohit is learning Java");
    }
}

class Akash implements Learner {
    public void learn() {
        System.out.println("Akash is learning Python");
    }
}

public class Main {
    public static void main(String[] args) {
        Learner l;

        l = new Mohit();
        l.learn();

        l = new Akash();
        l.learn();
    }
}
```

### Output
Mohit is learning Java
Akash is learning Python

## Polymorphism with Abstract Classes

Abstract classes allow you to combine shared state structures with abstract method contracts to achieve polymorphism.

### Example

```java
abstract class Course {
    abstract void learn();
}

class JavaCourse extends Course {
    void learn() {
        System.out.println("Learning Java");
    }
}

class WebCourse extends Course {
    void learn() {
        System.out.println("Learning Web Development");
    }
}

public class Main {
    public static void main(String[] args) {
        Course c;

        c = new JavaCourse();
        c.learn();

        c = new WebCourse();
        c.learn();
    }
}
```

### Output
Learning Java
Learning Web Development

## Polymorphism vs Method Overloading vs Method Overriding

| Feature | Method Overloading | Method Overriding |
| --- | --- | --- |
| **Polymorphism Type** | Compile-Time Polymorphism. | Runtime Polymorphism. |
| **Scope** | Occurs within the same class. | Occurs across parent and child classes. |
| **Method Name** | Must be identical. | Must be identical. |
| **Parameters** | Must be different. | Must be identical. |
| **Return Type** | Can be different. | Must be identical or covariant. |
| **Binding Time** | Resolved at compile time (Static Binding). | Resolved at runtime (Dynamic Binding). |
| **Performance** | Faster (no runtime lookup overhead). | Slightly slower (requires vtable lookups). |

## Advantages of Polymorphism

- **Code Reusability**: Allows common logic to operate on a wide variety of object classes.
- **System Extensibility**: New subclasses can be added to the inheritance hierarchy without modifying existing client code.
- **Improved Maintainability**: Decoupled interface definitions from concrete code implementation details make changes easier to manage.
- **Flexible Dynamic Behavior**: The system changes its execution path at runtime based on the specific subclass instance currently active.

## Limitations of Polymorphism

- **Design Complexity**: Managing numerous interfaces, abstract classes, and inheritance levels makes the codebase harder to trace.
- **Minor Performance Overhead**: Resolving methods dynamically at runtime requires looking up vtable references, which is slightly slower than static calls (though heavily optimized by modern JVMs).
- **Debugging Difficulty**: Stepping through code in a debugger can be difficult because the method definition you land on during compile time may not be the one executed at runtime.

## Common Mistakes

### 1. Confusing Overloading with Overriding

Overloading requires different parameters; overriding requires identical parameters.

```java
// Overloading (same class, different parameters)
void show(int a) {}
void show(double a) {}
```

### 2. Forgetting the `@Override` Annotation

Omitting the `@Override` annotation can lead to bugs where spelling errors in subclass method names result in the method being overloaded instead of overridden.

```java
// ❌ Dangerous: Spelling mistake turns override into overload
@Override
void teachh() {}
```

### 3. Using Parent References with Parent Instances

Declaring a parent reference variable pointing to a parent class instance does not demonstrate polymorphism, as there are no overridden methods to dispatch.

```java
// ❌ Static binding: executes Trainer class method directly
Trainer t = new Trainer(); 
t.teach();
```

### Correct Implementation

To leverage runtime polymorphism, declare a parent reference pointing to a child object instance:

```java
// ✅ Dynamic binding: executes JavaTrainer method at runtime
Trainer t = new JavaTrainer(); 
t.teach();
```

## Interview-Oriented Quick Comparison

| Feature | Compile-Time Polymorphism | Runtime Polymorphism |
| --- | --- | --- |
| **Alternative Names** | Static Polymorphism / Early Binding. | Dynamic Polymorphism / Late Binding. |
| **Resolution Phase** | Resolved during the compilation phase. | Resolved during the execution phase. |
| **Achieved By** | Method Overloading / Constructor Overloading. | Method Overriding (Inheritance/Interfaces). |
| **Performance Profile** | Faster execution (resolved early). | Minor dynamic lookup overhead (vtable search). |
| **Architectural Flexibility** | Lower flexibility (behavior is fixed at compile time). | High flexibility (behaviors resolve at runtime). |

## Summary

Polymorphism is a core OOP concept that allows a single entity to take multiple forms. In Java, it is achieved through **Method Overloading (Compile-Time Polymorphism)** and **Method Overriding (Runtime Polymorphism)**. It improves code reusability, flexibility, maintainability, and scalability. Polymorphism enables developers to write generic code that works with multiple object types, making applications easier to extend and manage. It is widely used with inheritance, interfaces, and abstract classes to build powerful and flexible object-oriented applications.




