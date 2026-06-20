# Encapsulation in Java

## Introduction

**Encapsulation** is one of the four fundamental pillars of Object-Oriented Programming (OOP) in Java. It is defined as the process of binding data variables (state) and the methods that operate on them (behaviors) together into a single, cohesive unit called a class, while restricting direct access to the internal data components.

In simple terms:

> Encapsulation acts as a **protective capsule** that prevents class variables from being accessed arbitrarily by external code, enforcing all interactions to go through controlled interfaces.

By locking down data visibility, encapsulation protects the internal state of an object and ensures that data changes are validated, consistent, and secure.

## Why Do We Need Encapsulation?

In software development, allowing external objects to modify a class's internal fields directly introduces severe structural risks:

- **Invalid Data States**: External code can assign invalid values (e.g., setting a database port to a negative number or a person's age to `150`).
- **Tight Coupling**: If internal field names or data types change, every external class referencing those fields directly will break.
- **Security Vulnerabilities**: Sensitive information like passwords, account numbers, or internal states can be read or modified without authorization.

Encapsulation resolves these issues by:

- **Protecting Data**: Restricting direct access using private modifiers.
- **Input Validation**: Enforcing boundary checks inside setter methods before updating variables.
- **Loose Coupling**: Allowing developers to change internal data structures without affecting client code that relies on the class's public methods.
- **Code Maintenance**: Isolating data mutations to specific getter and setter checkpoints, making debugging and tracing changes easier.

## Real-Life Example

### Bank Account

Consider a bank account management system. A customer needs to perform actions like depositing money, withdrawing money, and checking their balance. The customer should not have direct write access to the underlying `balance` variable (e.g., they cannot execute `account.balance = 1000000;`). Instead, they must interact with the account through public methods which perform balance calculations and transaction auditing before updating the balance.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/encapsulation-in-java/1781954332423-968597d4-da05-4468-bef3-a8eb5cd6bfb0.png)

By hiding the balance variable and exposing only authorized methods, the system maintains financial audit integrity.

## How Encapsulation is Achieved in Java

To implement encapsulation in a class, follow these two fundamental steps:

1. **Private Data Members**: Declare all instance variables of the class with the `private` access modifier. This prevents outside classes from accessing the fields directly.
2. **Public Accessor Methods**: Provide `public` getter and setter methods to read and write the field values, respectively, applying business rules where necessary.

## Basic Example

```java
class Student {
    private String name;

    // Public setter to update the value
    public void setName(String name) {
        this.name = name;
    }

    // Public getter to read the value
    public String getName() {
        return name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.setName("Mohit");
        System.out.println(s.getName());
    }
}
```

### Output
Mohit

### Explanation

- The `name` variable is marked `private`, meaning `s.name = "Mohit"` would cause a compilation error if attempted in the `Main` class.
- The public method `setName()` acts as the write interface.
- The public method `getName()` acts as the read interface.

## Example: AlphaKnowledge Student Portal

```java
class Student {
    private String studentName;

    public void setStudentName(String studentName) {
        this.studentName = studentName;
    }

    public String getStudentName() {
        return studentName;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.setStudentName("Mohit");
        System.out.println("Student: " + s.getStudentName());
    }
}
```

### Output
Student: Mohit

## Example with Validation

The core benefit of using accessor methods over public fields is the ability to validate data before updating an object's state.

```java
class Employee {
    private int age;

    public void setAge(int age) {
        // Enforcing boundary validations
        if (age >= 18 && age <= 65) {
            this.age = age;
        } else {
            System.out.println("Invalid Age: Age must be between 18 and 65.");
        }
    }

    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee e = new Employee();

        // Attempting to set an invalid age
        e.setAge(15);
        System.out.println("Age: " + e.getAge());

        // Setting a valid age
        e.setAge(30);
        System.out.println("Age: " + e.getAge());
    }
}
```

### Output
Invalid Age: Age must be between 18 and 65.
Age: 0
Age: 30

### Explanation

The setter method acts as a gatekeeper. By passing an invalid age of `15`, the validation check fails, printing an error message and leaving the private variable unmodified (at its default value of `0`).

## Example: AlphaKnowledge Course Management

```java
class Course {
    private String courseName;
    private int fee;

    public void setCourseName(String courseName) {
        this.courseName = courseName;
    }

    public String getCourseName() {
        return courseName;
    }

    public void setFee(int fee) {
        // Validating fee amount
        if (fee > 0) {
            this.fee = fee;
        } else {
            System.out.println("Invalid Fee: Fee must be positive.");
        }
    }

    public int getFee() {
        return fee;
    }
}

public class Main {
    public static void main(String[] args) {
        Course c = new Course();
        c.setCourseName("Java Programming");
        c.setFee(4999);

        System.out.println(c.getCourseName());
        System.out.println(c.getFee());
    }
}
```

### Output
Java Programming
4999

## Getters and Setters

Accessors (getters) and mutators (setters) follow standard design patterns defined by the **JavaBeans Specification**:

### Getter Methods

A getter retrieves the current value of a private variable.

- **Naming Convention**: Starts with the prefix `get` followed by the variable name with its first letter capitalized (e.g., `getName()`). For boolean variables, the prefix `is` is preferred (e.g., `isActive()`).
- **Return Type**: Matches the data type of the underlying private field.

```java
public DataType getVariable() {
    return variable;
}
```

### Setter Methods

A setter updates the value of a private variable.

- **Naming Convention**: Starts with the prefix `set` followed by the variable name with its first letter capitalized (e.g., `setName()`).
- **Return Type**: Always returns `void`.
- **Parameter**: Accepts a single parameter of the same data type as the variable.

```java
public void setVariable(DataType value) {
    variable = value;
}
```

## Encapsulation Using Multiple Objects

Encapsulation ensures that each object maintains its own independent state.

```java
class Student {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Mohit");
        Student s2 = new Student("Akash");
        Student s3 = new Student("Hemesh");

        System.out.println(s1.getName());
        System.out.println(s2.getName());
        System.out.println(s3.getName());
    }
}
```

### Output
Mohit
Akash
Hemesh

## Read-Only Class

A class is considered **read-only** if it provides public getter methods but no public setter methods. Once the object is initialized (typically via the constructor), its state cannot be modified by external classes.

### Use Cases

- **Configuration Files**: Storing environment keys, database endpoints, or fixed credentials that must remain unchanged during application execution.
- **Immutable Objects**: Modeling domain entities whose identity should never change once created (e.g., `LocalDate` instances).

```java
class Company {
    private String companyName = "AlphaKnowledge";

    // Only getter is provided, preventing modifications
    public String getCompanyName() {
        return companyName;
    }
}
```

## Write-Only Class

A class is considered **write-only** if it provides public setter methods but no public getter methods. External classes can update the state but cannot inspect it.

### Use Cases

- **Security Credentials**: Storing passwords, cryptographical keys, or tokens. A user can set a new password, but no client class can read the password back out.
- **Telemetry Data Loggers**: Submitting application metrics or logs to an internal buffer.

```java
class PasswordStore {
    private String password;

    // Only setter is provided, preventing external reads
    public void setPassword(String password) {
        this.password = password;
    }
}
```

## Encapsulation and Access Modifiers

Java access modifiers define the visibility constraints used to enforce encapsulation:

| Access Modifier | Same Class | Same Package | Subclass | Outside Package |
| --- | --- | --- | --- | --- |
| `private` | Yes | No | No | No |
| Default (no keyword) | Yes | Yes | No | No |
| `protected` | Yes | Yes | Yes | No (unless inherited) |
| `public` | Yes | Yes | Yes | Yes |

- **`private`**: Enforces strict encapsulation. Access is restricted exclusively to the declaring class.
- **Default (package-private)**: Access is open to all classes defined within the same package, but hidden from external packages.
- **`protected`**: Grants access to classes in the same package and subclasses located in different packages.
- **`public`**: Exposes the member to all classes across all packages.

## Data Hiding vs. Encapsulation

While frequently used interchangeably, Data Hiding is a subset of Encapsulation:

| Feature | Data Hiding | Encapsulation |
| --- | --- | --- |
| **Core Definition** | Hiding instance variables from direct visibility. | Wrapping variables and methods together in a single unit. |
| **Primary Focus** | Security and access restriction. | System structure, modularity, and data validation. |
| **Implementation** | Achieved using access modifiers (principally `private`). | Achieved using classes, modifiers, and public accessors. |
| **Methods Included** | No. Only hides the state properties. | Yes. Integrates data properties with behavioral operations. |

## Encapsulation vs. Abstraction

Understanding the division of labor between Encapsulation and Abstraction is key to good OOP design:

| Feature | Encapsulation | Abstraction |
| --- | --- | --- |
| **Objective** | Hides the state data (information hiding). | Hides the implementation complexity (detail hiding). |
| **Focus** | How an object secures and validates its data. | What an object does (exposing contracts/interfaces). |
| **Mechanism** | Access modifiers, getters, and setters. | Abstract classes and interfaces. |
| **Example** | Making database connection fields private. | Exposing a simple `connect()` method signature. |

## Advantages of Encapsulation

- **Data Security**: Restricts access to sensitive variables, protecting them from corruption.
- **Granular Control**: Allows class designers to make fields read-only, write-only, or read-write.
- **System Flexibility**: You can modify the internal data types or variable structures without breaking external application components.
- **Input Validation**: Ensures only valid states are persisted, maintaining system stability.
- **Easier Testing**: Standardizing data entries through getters/setters makes it easier to write unit tests and mock behaviors.

## Disadvantages of Encapsulation

- **Boilerplate Code**: Declaring getters and setters for numerous fields increases code verbosity (resolved in modern Java using tools like Lombok annotations or Record types).
- **Performance Overhead**: Calling accessor methods adds a minor stack frame overhead compared to direct field reads, though this is heavily optimized by JVM runtime compilers (inlining).
- **Initial Planning Overhead**: Requires developers to structure their classes and access permissions carefully from the beginning.

## Common Mistakes

### 1. Making Instance Variables Public

Declaring variables as public allows direct external modifications, bypassing all security and validation checks.

```java
class Student {
    public String name; // ❌ Wrong: breaks encapsulation
}
```

### 2. No Validation in Setters

Providing setters that assign inputs directly to variables without validations defeats the purpose of encapsulation.

```java
public void setAge(int age) {
    this.age = age; // ❌ Weak: permits invalid values like -5 or 999
}
```

### 3. Returning Mutable References Directly (Escaping References)

Returning a reference to a mutable object (like a `java.util.List`, `java.util.Date`, or custom object) from a getter breaks encapsulation. External classes can retrieve the reference and modify the object's contents directly, bypassing the class's setters.

```java
import java.util.List;
import java.util.ArrayList;

class Course {
    private List<String> studentList = new ArrayList<>();

    // ❌ Vulnerable: Returns direct reference to mutable list
    public List<String> getStudentList() {
        return studentList;
    }
}

public class Main {
    public static void main(String[] args) {
        Course c = new Course();
        // External code modifies private list directly!
        c.getStudentList().add("Mohit"); 
    }
}
```

### Correct Implementation

To prevent escaping references, return a **defensive copy** or wrap the collection in an unmodifiable wrapper:

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;

class Course {
    private List<String> studentList = new ArrayList<>();

    // ✅ Secure: Returns a read-only view of the list
    public List<String> getStudentList() {
        return Collections.unmodifiableList(studentList);
    }
}
```

## 

## Advantages of Encapsulation Over Public Variables

| Public Variables | Encapsulation |
| --- | --- |
| **No Security**: Any external class can read and overwrite the variable. | **High Security**: Private fields are hidden from outside modifications. |
| **No Validation**: Accepts any data type value assigned directly. | **Validation**: Mutators validate data limits before persisting. |
| **Tight Coupling**: Renaming fields breaks all client code references. | **Loose Coupling**: Field names can change without impact on public methods. |
| **Risk of Corrupt State**: Field values can easily enter invalid states. | **Data Protection**: Enforces consistent and valid object states. |

## Summary

Encapsulation is the process of binding data and methods together into a single unit while restricting direct access to the data. It is achieved using private variables and public getter/setter methods. Encapsulation improves security, validation, maintainability, flexibility, and code organization. It is one of the most important OOP principles and is widely used in real-world applications such as banking systems, student management systems, and enterprise software to protect and control access to data.




