# Object-Oriented Programming (OOP) in C++

Object-Oriented Programming (OOP) is a programming paradigm that organizes programs around **objects and classes** instead of only functions and procedures. It allows programmers to model real-world entities in software, making programs easier to design, maintain, reuse, and extend.

In C++, OOP is one of the most important concepts and is widely used in software development. Rather than writing programs as a collection of independent functions, OOP groups related data and functions together inside classes.

OOP helps developers create programs that are:

- Modular
- Reusable
- Secure
- Scalable
- Easy to maintain

Large software systems such as vehicle management systems, banking applications, hospital management systems, game engines, and enterprise software heavily rely on OOP concepts.

# Why Do We Need OOP?

Before Object-Oriented Programming, most applications were developed using **Procedural Programming**.

In procedural programming:

- Data and functions are separate.
- Large programs become difficult to manage.
- Code duplication increases.
- Security becomes harder to maintain.
- Reusability is limited.

As software projects grew larger, these problems became more noticeable.

Object-Oriented Programming was introduced to overcome these limitations by organizing software into logical units called classes and objects.

OOP provides:

- Better code organization.
- Improved code reusability.
- Data security through encapsulation.
- Easier debugging and maintenance.
- Faster development of large applications.

# Real-World Analogy of OOP

Consider a **Vehicle**.

Every vehicle has certain characteristics and behaviors.

### Properties

- Brand
- Color
- Fuel Type
- Top Speed
- Model

### Behaviors

- Start
- Stop
- Accelerate
- Brake
- Display Information

A Vehicle represents a **Class** because it acts as a blueprint.

An actual car created from this blueprint becomes an **Object**.

```text
Class → Vehicle

Object → MyCar
```

For example:

```text
Brand      : Toyota
Color      : Violet
Fuel Type  : Petrol
Top Speed  : 160 km/h
```

The object contains actual values while the class only defines what properties and behaviors should exist.

# Basic Concepts of OOP

Object-Oriented Programming is built around six major concepts:

1. Class
2. Object
3. Encapsulation
4. Abstraction
5. Inheritance
6. Polymorphism

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781082260412-ef225b87-dae5-488b-a6b9-6ed40bd05179.png)

These concepts work together to create flexible and maintainable software systems.

# Class

A **Class** is a blueprint or template used to create objects.

It defines:

- What data an object can store.
- What actions an object can perform.

A class itself does not occupy memory.

Memory is allocated only when objects are created from the class.

## Components of a Class

A class consists of:

### Class Name

The name used to identify the class.

### Data Members

Variables declared inside the class.

They represent the properties of an object.

### Member Functions

Functions declared inside the class.

They define the behavior of an object.

### Access Specifiers

Control accessibility of members.

- public
- private
- protected

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781081726039-557783bd-3e89-4332-9380-e3089b38f5bf.png)

## Syntax of a Class

```cpp
class ClassName
{
    access_specifier:

        data_members;

        member_functions;
};
```

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    string brand;
    string color;

    void displayInfo()
    {
        cout << "Brand: " << brand << endl;
        cout << "Color: " << color << endl;
    }
};

int main()
{
    Vehicle myCar;

    myCar.brand = "Toyota";
    myCar.color = "Violet";

    myCar.displayInfo();

    return 0;
}
```

### Output
Brand: Toyota
Color: Violet

### 

The class acts as a blueprint while the object stores actual values.

# Object

An **Object** is an instance of a class.

When an object is created:

- Memory is allocated.
- Data members receive storage.
- Member functions become accessible.

Objects represent real-world entities.

For example:

```cpp
Vehicle myCar;
```

Here:

- Vehicle → Class
- myCar → Object

## Characteristics of an Object

### State

Represents current values of object properties.

Example:

```text
Brand : Toyota
Color : Violet
```

### Behavior

Represents actions performed by the object.

Example:

```text
start()
stop()
accelerate()
```

### Identity

Every object has its own unique existence in memory.

Even if two cars have the same brand and color, they are separate objects.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    string brand;

    void start()
    {
        cout << brand << " Started";
    }
};

int main()
{
    Vehicle myCar;

    myCar.brand = "Toyota";

    myCar.start();

    return 0;
}
```

### Output
Toyota Started

### 

# Access Specifiers

Access specifiers determine how class members can be accessed.

C++ provides three access specifiers.

## Public

Members can be accessed from anywhere.

## Private

Members can only be accessed inside the class.

```cpp
private:
```

## Protected

Members can be accessed inside the class and derived classes.

```cpp
protected:
```

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
private:
    int speed;

public:
    void setSpeed(int s)
    {
        speed = s;
    }

    int getSpeed()
    {
        return speed;
    }
};

int main()
{
    Vehicle myCar;

    myCar.setSpeed(120);

    cout << myCar.getSpeed();

    return 0;
}
```

### Output
120

### 

The variable speed is hidden from direct access.

# Four Pillars of OOP

The four pillars of Object-Oriented Programming are:

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781082200203-ChatGPT_Image_Jun_10%2C_2026%2C_02_32_25_PM.png)

These concepts are responsible for the power and flexibility of OOP.

# Encapsulation

Encapsulation means combining data and functions into a single unit and restricting direct access to data.

It acts as a protective shield around the data.

Instead of allowing direct modification, controlled access is provided through public methods.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781082079097-6220a06a-f079-48d1-a9eb-c2e33a93e9d4.png)

## Why Encapsulation?

Without encapsulation:

- Anyone can modify important data.
- Data integrity can be compromised.
- Programs become difficult to maintain.

Encapsulation solves these problems by controlling access.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
private:
    int speed;

public:
    void setSpeed(int s)
    {
        speed = s;
    }

    int getSpeed()
    {
        return speed;
    }
};

int main()
{
    Vehicle myCar;

    myCar.setSpeed(140);

    cout << "Speed: "
         << myCar.getSpeed();

    return 0;
}
```

### Output
Speed: 140

### 

The speed variable cannot be modified directly.

# Abstraction

Abstraction means hiding implementation details and showing only essential features to the user.

The user knows:

```text
What the object does
```

but does not know:

```text
How it does it
```

## Real-World Example

When driving a car:

- You press the Start button.
- The engine starts.

You do not need to know:

- Fuel injection process
- Spark plug operation
- Engine combustion

All those details are hidden.

This is abstraction.

## Achieving Abstraction in C++

Abstraction is achieved using:

- Abstract Classes
- Pure Virtual Functions

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    virtual void startEngine() = 0;
};

class Car : public Vehicle
{
public:
    void startEngine()
    {
        cout << "Starting Car Engine";
    }
};

int main()
{
    Car myCar;

    myCar.startEngine();

    return 0;
}
```

### Output
Starting Car Engine

### 

The user only uses `startEngine()`  without seeing internal implementation.

# Inheritance

Inheritance allows one class to acquire properties and behaviors of another class.

It creates an **"is-a" relationship**.

For example:

```text
Car is a Vehicle
```

Therefore Car can inherit properties and behaviors from Vehicle.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781082353771-67efdfca-b6a3-430a-bb0e-b55127749b9f.png)

## Benefits of Inheritance

- Code Reusability
- Reduced Duplication
- Easier Maintenance
- Better Organization

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    void start()
    {
        cout << "Vehicle Started";
    }
};

class Car : public Vehicle
{
};

int main()
{
    Car myCar;

    myCar.start();

    return 0;
}
```

### Output
Vehicle Started

### 

The Car class automatically gets access to the start() function.

## Types of Inheritance

C++ supports:

- Single Inheritance
- Multiple Inheritance
- Multilevel Inheritance
- Hierarchical Inheritance
- Hybrid Inheritance

# Polymorphism

The word Polymorphism comes from:

```text
Poly  → Many
Morph → Forms
```

It means:

```text
One Interface
Multiple Behaviors
```

The same function can behave differently depending on the object calling it.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/object-oriented-programming-oop-in-c/1781082398597-24b8e889-68a7-45db-89f7-ebe5326ef140.png)

## Types of Polymorphism

### Compile-Time Polymorphism

Achieved using:

- Function Overloading
- Operator Overloading

### Run-Time Polymorphism

Achieved using:

- Virtual Functions
- Function Overriding

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    virtual void start()
    {
        cout << "Vehicle Started";
    }
};

class Car : public Vehicle
{
public:
    void start() override
    {
        cout << "Car Started";
    }
};

class Bike : public Vehicle
{
public:
    void start() override
    {
        cout << "Bike Started";
    }
};

int main()
{
    Vehicle* vehicle;

    Car myCar;

    vehicle = &myCar;

    vehicle->start();

    return 0;
}
```

### Output
Car Started

### 

Although the pointer type is Vehicle, the Car version of start() executes.

This is runtime polymorphism.

# Advantages of OOP

Object-Oriented Programming provides several advantages over procedural programming.

- Better code organization.
- Improved readability.
- Easier debugging.
- Better security.
- Increased code reusability.
- Faster development.
- Easier maintenance.
- Improved scalability.
- Reduced code duplication.
- Real-world modeling capability.

# OOP vs Procedural Programming

| Feature | Procedural Programming | Object-Oriented Programming |
| --- | --- | --- |
| Focus | Functions | Objects |
| Data Security | Low | High |
| Reusability | Limited | High |
| Scalability | Difficult | Easy |
| Maintenance | Difficult | Easier |
| Modularity | Low | High |

# Applications of OOP

Object-Oriented Programming is widely used in:

- Vehicle Management Systems
- Banking Applications
- Hospital Management Systems
- Library Management Systems
- E-Commerce Platforms
- Mobile Applications
- Desktop Software
- Game Development
- Enterprise Applications
- Simulation Software

# Situations Where OOP May Not Be Suitable

OOP may not be the best choice when:

- Programs are extremely small.
- Memory usage must be minimal.
- Performance is the highest priority.
- Low-level system programming is required.

# Summary

Object-Oriented Programming (OOP) is a programming paradigm that organizes software around classes and objects. A class acts as a blueprint, while objects are real instances created from that blueprint. OOP is built upon four major pillars: Encapsulation, Abstraction, Inheritance, and Polymorphism. These concepts help developers create modular, reusable, secure, and scalable applications. By modeling real-world entities such as vehicles, OOP makes software easier to understand, develop, maintain, and extend.




