# Java OOP (Object-Oriented Programming) Concepts

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of **objects**, which can contain data in the form of fields (attributes) and code in the form of procedures (methods). Java is designed as an object-oriented language where almost everything is structured around classes and objects.

In the real world, we are surrounded by objects: cars, smartphones, employees, bank accounts, and shopping carts. Each of these real-world entities has a state (what it knows or possesses) and a behavior (what it does). OOP allows programmers to model these real-world entities directly into software code, making the application modular, scalable, and easy to maintain.

### Why OOP is Essential?

- **Modularity**: Code is broken down into separate, self-contained objects, making development and troubleshooting easier.
- **Code Reusability**: Through inheritance and composition, developers can reuse existing code rather than writing it from scratch.
- **Security**: Encapsulation hides sensitive internal data, exposing only safe interaction boundaries.
- **Scalability**: Modeling code around objects allows systems to grow seamlessly as requirements expand.
- **Flexibility**: Polymorphism allows the same code interface to handle diverse implementations.

# Characteristics of OOP

The architecture of any Java OOP application is built upon several foundational pillars and object relationship patterns:

1. Class and Object (The Building Blocks)
2. Constructor (Initialization Logic)
3. Encapsulation (Data Protection)
4. Abstraction (Complexity Hiding)
5. Inheritance (Hierarchical Reusability)
6. Polymorphism (Multi-Form Behavior)
7. Association, Aggregation, and Composition (Object Relationships)

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933141767-ef225b87-dae5-488b-a6b9-6ed40bd05179.png)

# 1. Class

A **Class** is a user-defined blueprint or template from which individual objects are created. It represents the set of properties or methods that are common to all objects of one type. A class does not occupy physical memory space until an object is instantiated from it.

### Real-Time Example: House Blueprint

An architect draws a detailed blueprint of a house. The blueprint specifies the number of rooms, dimensions, wiring connections, and plumbing layouts.

- The blueprint itself is not a house; you cannot live in it, and it occupies no land.
- However, using this single blueprint, builders can construct multiple physical houses.
- The blueprint represents the **Class**, while the physical houses built on land represent the **Objects**.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933252156-7e47a8f4-e909-40b5-a768-35e562559f06.png)

### Example Code

```java
class House {

    String color;
    int numberOfRooms;

    void openMainDoor() {
        System.out.println("The door of the " + color + " house is now open.");
    }
}

public class Main {
    public static void main(String[] args) {

        House house1 = new House();

        house1.color = "Blue";
        house1.numberOfRooms = 4;

        house1.openMainDoor();
    }
}
```

### Output
The door of the Blue house is now open.

# 2. Object

An **Object** is a basic unit of Object-Oriented Programming and represents real-life entities. A typical Java program creates many objects, which interact by sending messages to one another. An object occupies memory space.

### Components of an Object

| Component | Description | Real-World Smartphone Analogy |
| --- | --- | --- |
| **State (Attributes)** | Represented by the data fields of an object. | Brand: Apple, Model: iPhone 15, Battery: 85%. |
| **Behavior (Methods)** | Represented by the functions/methods of an object. | `makeCall()`, `sendMessage()`, `takePhoto()`. |
| **Identity** | A unique name or address assigned to an object. | Unique IMEI number or JVM-assigned memory address. |

### Real-Time Example: Smartphone

When a manufacturer builds a phone, it uses the "Smartphone" blueprint. The physical phone in your hand is a unique object. It has a state (current battery percentage, stored contacts) and behaviors (ringing, vibration, displaying screens).

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933317035-557783bd-3e89-4332-9380-e3089b38f5bf.png)

### Example Code

```java
class Smartphone {

    String brand;
    int batteryPercentage;

    void checkPowerStatus() {
        System.out.println(brand + " phone battery is at " + batteryPercentage + "%.");
    }
}

public class Main {
    public static void main(String[] args) {

        Smartphone myPhone = new Smartphone();

        myPhone.brand = "Apple";
        myPhone.batteryPercentage = 85;

        myPhone.checkPowerStatus();
    }
}
```

### Output
Apple phone battery is at 85%.

# 3. Constructor

A **Constructor** is a block of code similar to a method that is called when an instance of an object is created. Unlike methods, constructors do not have a return type and share the exact name of the class.

### Real-Time Example: Bank Account Activation

When you open a bank account, the bank requires your name, ID document, and an initial deposit. The bank cannot activate an account in an uninitialized state (without an owner or account number). The constructor acts as the account opening process, forcing values to be assigned at the moment the object is created.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933395961-180c2259-8f12-4d03-aa9d-b9a27d434f89.png)

## Default Constructor

A default constructor has no parameters and is called automatically if no other constructor is defined.

### Example Code

```java
class BankAccount {

    String accountHolder;

    BankAccount() {
        accountHolder = "Unknown Guest";
        System.out.println("Default Guest Account Activated.");
    }
}

public class Main {
    public static void main(String[] args) {

        BankAccount acc = new BankAccount();
    }
}
```

### Output
Default Guest Account Activated.

## Parameterized Constructor

A constructor that accepts parameters to initialize attributes with specific custom values.

### Example Code

```java
class BankAccount {

    String accountHolder;
    double balance;

    BankAccount(String name, double initialDeposit) {
        this.accountHolder = name;
        this.balance = initialDeposit;
    }

    void showDetails() {
        System.out.println(accountHolder + " has a balance of $" + balance);
    }
}

public class Main {
    public static void main(String[] args) {

        BankAccount myAcc = new BankAccount("Mohit", 500.50);

        myAcc.showDetails();
    }
}
```

### Output
Mohit has a balance of $500.5

## Copy Constructor

Used to clone or create a duplicate of an existing object. While Java does not have a built-in copy constructor, it can be easily implemented manually by passing the object as a parameter.

### Example Code

```java
class BankAccount {

    String accountHolder;
    double balance;

    BankAccount(String name, double initialDeposit) {
        this.accountHolder = name;
        this.balance = initialDeposit;
    }

    BankAccount(BankAccount targetAccount) {
        this.accountHolder = targetAccount.accountHolder;
        this.balance = targetAccount.balance;
    }

    void showDetails() {
        System.out.println("Clone of " + accountHolder + " - Balance: $" + balance);
    }
}

public class Main {
    public static void main(String[] args) {

        BankAccount original = new BankAccount("Akash", 1200.0);
        BankAccount clone = new BankAccount(original);

        clone.showDetails();
    }
}
```

### Output
Clone of Akash - Balance: $1200.0

## Private Constructor

Restricts object instantiation from outside the class. This is commonly used in structural design patterns like the **Singleton Pattern**, ensuring that only one instance of a class ever exists in memory (e.g., a Database Connection manager).

### Example Code

```java
class DatabaseConnector {

    private static DatabaseConnector instance;

    private DatabaseConnector() {
        System.out.println("Connected to Database Server Instance.");
    }

    public static DatabaseConnector getInstance() {
        if (instance == null) {
            instance = new DatabaseConnector();
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {

        DatabaseConnector db1 = DatabaseConnector.getInstance();
        DatabaseConnector db2 = DatabaseConnector.getInstance();
    }
}
```

### Output
Connected to Database Server Instance.

### Explanation

Even though `getInstance()` is called twice, the constructor runs only once because the database connector implements a private constructor to prevent external object creation.

# 4. Encapsulation

**Encapsulation** is the mechanism of wrapping variable data and method codes together into a single unit (a class) and restricting direct access to some of the object's components. It is achieved by declaring variables as `private` and exposing them through `public` getter and setter methods.

### Real-Time Example: Capsule/ATM

- **Capsule**: A medical capsule hides the medicine powder inside its shell. The shell acts as the boundary (Encapsulation).
- **ATM machine**: An ATM encapsulates the cash storage and internal logic. You cannot reach inside the machine to manually update the cash balances. Instead, you interact with public buttons (Getters/Setters) to check balances and withdraw cash. The internal state remains secure.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933466032-6220a06a-f079-48d1-a9eb-c2e33a93e9d4.png)

### Example Code

```java
class Employee {

    private String name;
    private double salary;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        if (salary >= 0) {
            this.salary = salary;
        } else {
            System.out.println("Error: Salary cannot be negative.");
        }
    }
}

public class Main {
    public static void main(String[] args) {

        Employee emp = new Employee();

        emp.setName("Mohit");
        emp.setSalary(45000.0);

        System.out.println(emp.getName() + " earns $" + emp.getSalary());

        emp.setSalary(-500.0);
    }
}
```

### Output
Mohit earns $45000.0
Error: Salary cannot be negative.

### Explanation

By making variables private and using setters, we can perform input validation (like preventing negative salaries), securing data integrity.

# 5. Abstraction

**Abstraction** is the process of hiding implementation details and exposing only the essential features of an object. In Java, Abstraction is achieved using Abstract Classes (which can have abstract and concrete methods) and Interfaces (which enforce public contract declarations).

### Real-Time Example: Car Driving

When you drive a car, you push the accelerator pedal to speed up. You do not need to understand the internal mechanics of fuel combustion, throttle valves, or engine pistons. The pedals act as the abstract interface, hiding the complex engine logic.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933554331-5ae14b81-fa4d-4c8d-a144-2d06486ebd9c.png)

## Abstract Class vs Interface Comparison

| Feature | Abstract Class | Interface |
| --- | --- | --- |
| **Methods** | Can have abstract and concrete methods. | Mostly abstract methods (prior to Java 8). |
| **Multiple Inheritance** | A subclass can extend only one class. | A class can implement multiple interfaces. |
| **Constructor** | Can contain constructors. | Cannot contain constructors. |
| **Variables** | Can have instance variables of any type. | Variables are implicitly `public static final`. |

## Example Using Abstract Class

```java
abstract class CloudStorage {

    abstract void uploadFile(String fileName);

    void connect() {
        System.out.println("Connection established to cloud database.");
    }
}

class S3Storage extends CloudStorage {

    void uploadFile(String fileName) {
        System.out.println("Uploading " + fileName + " to Amazon S3 Bucket.");
    }
}

public class Main {
    public static void main(String[] args) {

        CloudStorage storage = new S3Storage();

        storage.connect();
        storage.uploadFile("document.pdf");
    }
}
```

### Output
Connection established to cloud database.
Uploading document.pdf to Amazon S3 Bucket.

## Example Using Interface

```java
interface PaymentGateway {

    void pay(double amount);
}

class StripePayment implements PaymentGateway {

    public void pay(double amount) {
        System.out.println("Processing credit card payment of $" + amount + " via Stripe.");
    }
}

public class Main {
    public static void main(String[] args) {

        PaymentGateway payment = new StripePayment();

        payment.pay(150.0);
    }
}
```

### Output
Processing credit card payment of $150.0 via Stripe.

# 6. Inheritance

**Inheritance** is a mechanism in which one class acquires the properties (variables) and behaviors (methods) of a parent class. It represents the **IS-A** relationship (Generalization to Specialization) and is implemented in Java using the `extends` keyword.

### Real-Time Example: Corporate Hierarchy

In a corporate software platform:

- A general class **Employee** contains attributes like `id`, `name`, and `salary`.
- Subclasses like **Developer** and **Manager** inherit these attributes.
- A Developer is an Employee, and a Manager is an Employee.
- Code defined in Employee is reused by all subclasses, preventing duplicate code.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933602628-9d7be607-65ef-468c-8c30-4c135840f2eb.png)

### Example Code

```java
class Employee {

    String name;
    double baseSalary;

    void displayRole() {
        System.out.print(name + " is an Employee. ");
    }
}

class Developer extends Employee {

    String codingLanguage;

    void showCodingSkills() {
        displayRole();
        System.out.println("Coding expertise: " + codingLanguage);
    }
}

public class Main {
    public static void main(String[] args) {

        Developer dev = new Developer();

        dev.name = "Mohit";
        dev.codingLanguage = "Java";

        dev.showCodingSkills();
    }
}
```

### Output
Mohit is an Employee. Coding expertise: Java

## Types of Inheritance

| Inheritance Type | Supported in Java? | Implementation Method |
| --- | --- | --- |
| **Single** | Yes | Subclass extends single base class. |
| **Multilevel** | Yes | Grandchild extends Child extends Parent. |
| **Hierarchical** | Yes | Multiple subclasses extend same parent. |
| **Multiple** | No (Directly) | Prevented due to Diamond Problem; implemented via Interfaces. |
| **Hybrid** | No (Directly) | Achieved by combining inheritance styles via Interfaces. |

## Multilevel Inheritance Example

```java
class Vehicle {

    void run() {
        System.out.println("Vehicle is traveling.");
    }
}

class Car extends Vehicle {

    void fuelType() {
        System.out.println("Uses gasoline fuel.");
    }
}

class ElectricCar extends Car {

    void batteryStatus() {
        run();
        fuelType();
        System.out.println("Electric charge: 95%.");
    }
}

public class Main {
    public static void main(String[] args) {

        ElectricCar Tesla = new ElectricCar();

        Tesla.batteryStatus();
    }
}
```

### Output
Vehicle is traveling.
Uses gasoline fuel.
Electric charge: 95%.

# 7. Polymorphism

**Polymorphism** (meaning "many forms") is the ability of an object, method, or reference variable to behave differently under different contexts.

### Real-Time Example: Human Roles

A person behaves differently based on context:

- At work, they act as an Employee.
- In a store, they act as a Customer.
- At home, they act as a Parent.
- The individual is the same, but the behavior changes dynamically.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-oop-object-oriented-programming-concepts/1781933668545-e12d5d98-4aec-4184-9223-cf2ccc308675.png)

## Types of Polymorphism

| Polymorphism Type | Method Used | Execution Phase |
| --- | --- | --- |
| **Compile-Time** | Method Overloading (same name, different arguments) | Resolved during Compilation. |
| **Runtime** | Method Overriding (subclass overrides parent method) | Resolved during Execution (Dynamic Dispatch). |

## Compile-Time Polymorphism (Method Overloading)

### Example Code

```java
class PaymentProcessor {

    void processPayment(double amount) {
        System.out.println("Processing cash payment of $" + amount);
    }

    void processPayment(double amount, String cardNo) {
        System.out.println("Processing credit card " + cardNo + " for $" + amount);
    }
}

public class Main {
    public static void main(String[] args) {

        PaymentProcessor processor = new PaymentProcessor();

        processor.processPayment(50.0);
        processor.processPayment(120.0, "1234-5678");
    }
}
```

### Output
Processing cash payment of $50.0
Processing credit card 1234-5678 for $120.0

## Runtime Polymorphism (Method Overriding)

### Example Code

```java
class Notification {

    void send() {
        System.out.println("Sending a generic notification alert.");
    }
}

class SMSNotification extends Notification {

    @Override
    void send() {
        System.out.println("Sending mobile text SMS alert.");
    }
}

public class Main {
    public static void main(String[] args) {

        Notification msg = new SMSNotification();

        msg.send();
    }
}
```

### Output
Sending mobile text SMS alert.

# Object Relationships

In addition to class inheritance, objects interact using association pathways that determine structural lifetimes.

## 8. Association

**Association** represents a broad connection relationship where objects have their own independent lifecycles. There is no ownership between them.

### Real-Time Example: Doctor and Patient

- A Doctor treats many Patients.
- A Patient visits many Doctors.
- Both are independent entities. If the doctor leaves the hospital, the patients still exist. If a patient leaves, the doctor continues practicing.

### Example Code

```java
class Doctor {

    String name;

    Doctor(String name) {
        this.name = name;
    }
}

class Patient {

    String name;
    Doctor doctor;

    Patient(String name, Doctor doctor) {
        this.name = name;
        this.doctor = doctor;
    }

    void showRelationship() {
        System.out.println("Patient " + name + " is treated by Dr. " + doctor.name);
    }
}

public class Main {
    public static void main(String[] args) {

        Doctor doc = new Doctor("Kumar");
        Patient pat = new Patient("Akash", doc);

        pat.showRelationship();
    }
}
```

### Output
Patient Akash is treated by Dr. Kumar

## 9. Aggregation

**Aggregation** represents a weak **HAS-A** relationship. It implies a relationship where a child can exist independently of the parent object.

### Real-Time Example: University and Professor

- A Department has Professors.
- The Department aggregates Professors.
- If the Department is closed down, the Professors continue to exist and can join other departments or universities.

### Example Code

```java
class Professor {

    String name;

    Professor(String name) {
        this.name = name;
    }
}

class Department {

    String deptName;
    Professor head;

    Department(String name, Professor prof) {
        this.deptName = name;
        this.head = prof;
    }

    void showHead() {
        System.out.println(head.name + " heads the " + deptName + " department.");
    }
}

public class Main {
    public static void main(String[] args) {

        Professor prof = new Professor("Hemesh");
        Department cs = new Department("Computer Science", prof);

        cs.showHead();
    }
}
```

### Output
Hemesh heads the Computer Science department.

## 10. Composition

**Composition** is a strong **HAS-A** relationship. It represents a strict dependency relationship where the child object cannot exist if the parent object is destroyed.

### Real-Time Example: Human Body and Heart

- A Human Body has a Heart.
- The Heart is composed within the Body.
- The Heart cannot exist independently outside the body, and if the Human Body is destroyed, the Heart object is also destroyed.

### Example Code

```java
class Heart {

    void beat() {
        System.out.println("Heart is pumping blood.");
    }
}

class Human {

    private final Heart heart;

    Human() {
        heart = new Heart(); // Created inside constructor - strict lifetime control
    }

    void breathe() {
        heart.beat();
        System.out.println("Human is breathing.");
    }
}

public class Main {
    public static void main(String[] args) {

        Human person = new Human();

        person.breathe();
    }
}
```

### Output
Heart is pumping blood.
Human is breathing.

# OOP vs Procedural Programming

| Feature | Object-Oriented Programming (OOP) | Procedural Programming |
| --- | --- | --- |
| **Core Entity** | Focuses on **Objects** (Data + Methods). | Focuses on **Functions** / Procedures. |
| **Security** | High (using Encapsulation to protect variables). | Low (variables are easily accessible). |
| **Data Flow** | Objects communicate using message passing. | Data travels globally through functions. |
| **Modeling** | Mimics real-world scenarios naturally. | Mimics algorithms and sequence paths. |
| **Modification** | Easy (modular design limits side effects). | Complex (changing global values breaks code). |
| **Code Reusability** | Very High (using Inheritance). | Low (functions are copy-pasted). |

# Advantages of OOP

1. **Modular Development**: Divides application logic into distinct, easy-to-manage object modules.
2. **Enhanced Security**: Prevents unauthorized external modification through data hiding.
3. **Easy Maintenance**: Updating or debugging an object does not cause bugs in unrelated parts of the code.
4. **Improved Reusability**: Classes can be inherited, reducing code duplication (DRY - Don't Repeat Yourself).
5. **Real-World Representation**: Makes mapping complex systems (like enterprise bank databases) intuitive.

# Limitations of OOP

1. **Higher Memory Usage**: Declaring classes, constructors, and allocating individual object references consumes more memory.
2. **Complexity for Small Apps**: Setting up class structures, packages, and inheritance paths is unnecessary overhead for simple scripts.
3. **Planning Requirements**: Designing interfaces, inheritance hierarchies, and class interactions requires deep upfront architectural planning.

# Summary

Object-Oriented Programming (OOP) is the foundation of Java development. It organizes software around classes and objects and provides powerful concepts such as Encapsulation, Abstraction, Inheritance, and Polymorphism. Additional relationships such as Association, Aggregation, and Composition help model real-world systems effectively. OOP improves code reusability, maintainability, scalability, and security, making it ideal for developing modern enterprise and large-scale software applications.




