# Java Methods, Static vs Instance Methods, and Access Modifiers in Java

Java methods are blocks of code that perform a specific task. They help organize logic, reduce repetition, and make programs easier to read and maintain.

This article covers:

- Java methods
- static methods and instance methods
- access modifiers in Java

## Java Methods

A method in Java is a named block of code that runs when it is called. Every method in Java must belong to a class.

### Why Methods Are Useful

![Advantages of Methods](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-methods-static-vs-instance-methods-and-access-modifiers-in-java/1781016956815-why_methods.png)

Methods help in many ways:

- code reusability
- better organization
- improved readability
- easier maintenance

Instead of writing the same logic again and again, you can place it in a method and call it whenever needed.

## Syntax of a Java Method

```java
returnType methodName(parameters) {
    // method body
    return value;
}
```

If a method does not return anything, use `void` as the return type.

## Parts of a Method

A method declaration usually includes:

- modifier
- return type
- method name
- parameter list
- method body

### Example

```java
public class Main {
    public void printMessage() {
        System.out.println("Hello, AlphaKnowledge!");
    }

    public static void main(String[] args) {
        Main obj = new Main();
        obj.printMessage();
    }
}
```

### Output
Hello, AlphaKnowledge!

In this example, `printMessage()` is a simple method with no parameters and no return value.

## Method Parameters and Return Values

Methods can take input values called parameters, and they can also return a result.

### Example

```java
public class Main {
    public int addNumbers(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Main obj = new Main();
        int result = obj.addNumbers(10, 20);
        System.out.println("Result: " + result);
    }
}
```

### Output
Result: 30

## Method Signature

A method signature consists of:

- method name
- number of parameters
- type of parameters
- order of parameters

The return type is not part of the method signature.

### Example

```java
max(int a, int b)
```

This signature shows:

- method name: `max`
- parameter count: 2
- parameter types: `int`, `int`

## Naming Methods in Java

Method names should follow these rules:

- start with a lowercase verb
- use camelCase for multi-word names
- clearly describe the action

### Good Examples

- `printDetails()`
- `calculateTotal()`
- `setName()`
- `showMessage()`

## Types of Methods in Java

Java methods are commonly grouped into:

1. Predefined methods
2. User-defined methods
3. Static methods
4. Instance methods

![Types of Methods](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-methods-static-vs-instance-methods-and-access-modifiers-in-java/1781017018381-types_of_methods.png)

## 1. Predefined Methods

Predefined methods are already available in Java libraries.

### Example

```java
public class Main {
    public static void main(String[] args) {
        double value = Math.random();
        System.out.println(value);
    }
}
```

### Output
A random decimal value will be printed

Examples of predefined methods include:

- `Math.random()`
- `System.out.println()`
- `hashCode()`

## 2. User-Defined Methods

User-defined methods are created by the programmer based on program requirements.

### Example

```java
public class Main {
    void greet() {
        System.out.println("Welcome to AlphaKnowledge");
    }

    public static void main(String[] args) {
        Main obj = new Main();
        obj.greet();
    }
}
```

### Output
Welcome to AlphaKnowledge

## Static Method in Java

A static method belongs to the class, not to any specific object. It can be called without creating an object.

### Key Points About Static Methods

- declared using the `static` keyword
- belong to the class
- can be called using the class name
- can access only static members directly
- cannot use `this`

### Example

```java
public class Main {
    public static void greet() {
        System.out.println("Hello, Akash!");
    }

    public static void main(String[] args) {
        greet();
        Main.greet();
    }
}
```

### Output
Hello, Akash!
Hello, Akash!

## Instance Method in Java

An instance method belongs to an object of a class. To call it, you need to create an object first.

### Key Points About Instance Methods

- belong to an object
- require object creation
- can access instance variables and methods
- can also access static members
- can use the `this` keyword

### Example

```java
class Student {
    String name = "";

    public void setName(String name) {
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.setName("Mohit");
        System.out.println(s1.name);
    }
}
```

### Output
Mohit

## Static Method vs Instance Method

| Feature | Static Method | Instance Method |
| --- | --- | --- |
| Belongs To | Class | Object |
| Object Needed | No | Yes |
| Access | Only static members directly | Static and instance members |
| `this` keyword | Not allowed | Allowed |
| Use Case | Common utility logic | Object-specific behavior |

## Calling Different Types of Methods

Methods can be called in different ways depending on their type.

## Calling a User-Defined Method

```java
public class Main {
    void hello() {
        System.out.println("This is a user-defined method.");
    }

    public static void main(String[] args) {
        Main obj = new Main();
        obj.hello();
    }
}
```

### Output
This is a user-defined method.

## Calling a Static Method

```java
class Helper {
    static void show() {
        System.out.println("Static method called");
    }
}

public class Main {
    public static void main(String[] args) {
        Helper.show();
    }
}
```

### Output
Static method called

## Calling a Predefined Method

```java
public class Main {
    public static void main(String[] args) {
        Main obj = new Main();
        System.out.println(obj.hashCode());
    }
}
```

### Output
A numeric hash code will be printed

## Calling an Abstract Method

Abstract methods do not have a body and must be implemented in a subclass.

### Example

```java
abstract class Portal {
    abstract void showName(String name);
}

public class Main extends Portal {
    @Override
    void showName(String name) {
        System.out.println(name);
    }

    public static void main(String[] args) {
        Main obj = new Main();
        obj.showName("AlphaKnowledge");
    }
}
```

### Output
AlphaKnowledge

## Method Call Stack in Java

When a method is called, Java creates a new stack frame for it in the call stack. After the method finishes, its frame is removed, and control returns to the caller.

The call stack works in LIFO order, which means Last In, First Out.

### Example

```java
public class Main {

    public static void methodC() {
        System.out.println("In Method C");
    }

    public static void methodB() {
        methodC();
        System.out.println("In Method B");
    }

    public static void methodA() {
        methodB();
        System.out.println("In Method A");
    }

    public static void main(String[] args) {
        methodA();
    }
}
```

### Output
In Method C
In Method B
In Method A

This shows that `methodA()` calls `methodB()`, and `methodB()` calls `methodC()`. After `methodC()` finishes, control returns step by step.

![Method Call Stack](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-methods-static-vs-instance-methods-and-access-modifiers-in-java/1781017131106-method_call_stack.png)

## Access Modifiers in Java

Access modifiers control the visibility and accessibility of classes, methods, and variables.

Java provides four access modifiers:

- `private`
- default
- `protected`
- `public`

These help enforce encapsulation and control how different parts of the program interact.

## 1. Private Access Modifier

The `private` modifier allows access only within the same class.

### Example

```java
class Person {
    private String name;

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.setName("Abhiram");
        System.out.println(p.getName());
    }
}
```

### Output
Abhiram

Direct access to `name` from outside the class is not allowed.

## 2. Default Access Modifier

If no access modifier is specified, the member gets default access. It can be accessed only within the same package.

### Example

```java
class Car {
    String model;
}

public class Main {
    public static void main(String[] args) {
        Car c = new Car();
        c.model = "Sedan";
        System.out.println(c.model);
    }
}
```

### Output
Sedan

## 3. Protected Access Modifier

The `protected` modifier allows access:

- within the same package
- in subclasses from different packages

### Example

```java
class Vehicle {
    protected int speed = 100;
}

class Bike extends Vehicle {
    void showSpeed() {
        System.out.println(speed);
    }
}

public class Main {
    public static void main(String[] args) {
        Bike b = new Bike();
        b.showSpeed();
    }
}
```

### Output
100

## 4. Public Access Modifier

The `public` modifier allows access from anywhere in the program.

### Example

```java
class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(MathUtils.add(5, 10));
    }
}
```

### Output
15

## Access Modifiers Summary Table

| Access Modifier | Same Class | Same Package | Subclass in Different Package | Anywhere |
| --- | --- | --- | --- | --- |
| `private` | Yes | No | No | No |
| default | Yes | Yes | No | No |
| `protected` | Yes | Yes | Yes | No |
| `public` | Yes | Yes | Yes | Yes |

## When to Use Which Access Modifier

- Use `private` for internal data that should be hidden
- Use default for package-level helpers
- Use `protected` when subclasses need access
- Use `public` for features that must be accessible everywhere

## Common Mistakes

### 1. Calling an instance method without an object

```java
public class Main {
    void show() {
        System.out.println("Hello");
    }

    public static void main(String[] args) {
        // show(); // Error
    }
}
```

An instance method needs an object.

### 2. Accessing instance data directly inside a static method

```java
public class Main {
    int value = 10;

    public static void display() {
        // System.out.println(value); // Error
    }
}
```

A static method cannot directly access non-static data.

### 3. Trying to access private members outside the class

```java
class Account {
    private int balance = 5000;
}
```

Private members are only visible within their own class.

## Complete Example

```java
class Student {
    private String name;

    public void setName(String name) {
        this.name = name;
    }

    public void showName() {
        System.out.println("Student Name: " + name);
    }

    public static void showPlatform() {
        System.out.println("Platform: AlphaKnowledge");
    }
}

public class Main {
    public static void main(String[] args) {
        Student.showPlatform();

        Student s1 = new Student();
        s1.setName("Akash");
        s1.showName();
    }
}
```

### Output
Platform: AlphaKnowledge
Student Name: Akash

##



###
