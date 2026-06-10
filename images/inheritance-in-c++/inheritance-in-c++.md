# Inheritance in C++

Inheritance is one of the most important concepts of Object-Oriented Programming (OOP). It allows one class to acquire the properties and behaviors of another class. In simple terms, inheritance enables developers to create a new class from an existing class, reducing code duplication and promoting code reusability.

Inheritance establishes an **"is-a" relationship** between classes.

For example:

```text
Car is a Vehicle
Bike is a Vehicle
Truck is a Vehicle
```

Since all vehicles share some common characteristics such as brand, speed, fuel type, and engine operations, these common features can be written once in a base class and reused by all derived classes.

# Why Do We Need Inheritance?

Imagine developing a Vehicle Management System.

Without inheritance:

```cpp
class Car
{
    string brand;
    int speed;

    void startEngine();
};

class Bike
{
    string brand;
    int speed;

    void startEngine();
};

class Truck
{
    string brand;
    int speed;

    void startEngine();
};
```

The same code is repeated multiple times.

With inheritance:

```cpp
class Vehicle
{
    string brand;
    int speed;

    void startEngine();
};
```

All vehicle types can inherit these common properties.

Benefits include:

- Code Reusability
- Reduced Code Duplication
- Easier Maintenance
- Better Organization
- Faster Development
- Improved Scalability

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091198182-67efdfca-b6a3-430a-bb0e-b55127749b9f.png)

# Basic Terminology

Before learning inheritance, it is important to understand two terms.

## Base Class

The class whose properties and methods are inherited by another class is called the **Base Class**, **Parent Class**, or **Super Class**.

Example:

```cpp
class Vehicle
{
};
```

Vehicle is the base class.

## Derived Class

The class that inherits properties and methods from another class is called the **Derived Class**, **Child Class**, or **Sub Class**.

Example:

```cpp
class Car : public Vehicle
{
};
```

Car is the derived class.

# Syntax of Inheritance

```cpp
class ChildClass : public ParentClass
{
    // Additional members
};
```

Where:

- `ChildClass` is the derived class.
- `ParentClass` is the base class.
- `public` is the inheritance access mode.

# How Inheritance Works?

When a derived class inherits a base class:

- It receives all accessible data members.
- It receives all accessible member functions.
- It can add new members.
- It can modify inherited behavior.
- It can override inherited functions.

Consider:

```cpp
class Vehicle
{
public:

    void startEngine()
    {
        cout << "Engine Started";
    }
};

class Car : public Vehicle
{
};
```

The Car class automatically gets access to:

```cpp
startEngine();
```

without rewriting the function.

# Types of Inheritance in C++

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091342276-c9426eea-8927-4510-9805-417989a8dd1e.png)

# 1. Single Inheritance

Single Inheritance occurs when one derived class inherits from one base class.

```text
Vehicle
   |
   |
  Car
```

This is the simplest form of inheritance.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091400466-ccb8283c-3fae-4f93-abdd-36a74217ac5d.png)

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    void displayType()
    {
        cout << "This is a Vehicle"
             << endl;
    }
};

class Car : public Vehicle
{
public:

    void displayCar()
    {
        cout << "This Vehicle is a Car";
    }
};

int main()
{
    Car car;

    car.displayType();
    car.displayCar();

    return 0;
}
```

### Output
This is a Vehicle
This Vehicle is a Car

### 

### Explanation

The Car class inherits the `displayType()` function from the Vehicle class.

Because of inheritance, the Car object can directly access functions defined in Vehicle.

# 2. Multiple Inheritance

Multiple Inheritance occurs when one class inherits from more than one base class.

```text
Engine
      \
       \
        SportsCar
       /
      /
Transmission
```

The derived class receives features from multiple parent classes.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091432260-2c9ecd22-04b6-4368-bbf7-a3502e671664.png)

## Example Code

```cpp
#include <iostream>
using namespace std;

class Engine
{
public:

    void startEngine()
    {
        cout << "Engine Started"
             << endl;
    }
};

class Transmission
{
public:

    void shiftGear()
    {
        cout << "Gear Shifted"
             << endl;
    }
};

class SportsCar : public Engine,
                  public Transmission
{
};

int main()
{
    SportsCar car;

    car.startEngine();

    car.shiftGear();

    return 0;
}
```

### Output
Engine Started
Gear Shifted

### 

### Explanation

SportsCar inherits features from both Engine and Transmission classes.

This allows a single object to access members from multiple parent classes.

# 3. Multilevel Inheritance

Multilevel Inheritance forms a chain of inheritance.

```text
Vehicle
   |
FourWheeler
   |
  Car
```

A class inherits another derived class.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091545295-430353f5-ed2d-438b-873c-1a8aa2565295.png)

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    void vehicleInfo()
    {
        cout << "Vehicle Information"
             << endl;
    }
};

class FourWheeler : public Vehicle
{
public:

    void wheelInfo()
    {
        cout << "Four Wheels"
             << endl;
    }
};

class Car : public FourWheeler
{
public:

    void carInfo()
    {
        cout << "Car Information";
    }
};

int main()
{
    Car car;

    car.vehicleInfo();

    car.wheelInfo();

    car.carInfo();

    return 0;
}
```

### Output
Vehicle Information
Four Wheels
Car Information

### 

### Explanation

The Car class inherits FourWheeler.

FourWheeler inherits Vehicle.

Therefore, Car automatically gets access to members of both classes.

# 4. Hierarchical Inheritance

Hierarchical Inheritance occurs when multiple classes inherit from the same base class.

```text
Vehicle
        /    |    \
       /     |     \
     Car    Bike   Truck
```

All child classes share common functionality from the parent class.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inheritance-in-c/1781091600268-7f6cc224-4d17-496d-ae60-e6e31a5cbc71.png)

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    void startEngine()
    {
        cout << "Engine Started"
             << endl;
    }
};

class Car : public Vehicle
{
};

class Bike : public Vehicle
{
};

class Truck : public Vehicle
{
};

int main()
{
    Car car;
    Bike bike;
    Truck truck;

    car.startEngine();
    bike.startEngine();
    truck.startEngine();

    return 0;
}
```

### Output
Engine Started
Engine Started
Engine Started

### 

### Explanation

Car, Bike, and Truck all inherit the startEngine() function from Vehicle.

The function is written only once and reused by all derived classes.

# 5. Hybrid Inheritance

Hybrid Inheritance combines two or more inheritance types.

Example:

```text
Vehicle
          /       \
         /         \
       Car        FareInfo
          \       /
           \     /
        ElectricCar
```

Hybrid inheritance is commonly used in large-scale applications where multiple relationships exist between classes.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    void vehicleInfo()
    {
        cout << "Vehicle Information"
             << endl;
    }
};

class FareInfo
{
public:

    void fareDetails()
    {
        cout << "Fare Details"
             << endl;
    }
};

class ElectricCar :
    public Vehicle,
    public FareInfo
{
};

int main()
{
    ElectricCar car;

    car.vehicleInfo();

    car.fareDetails();

    return 0;
}
```

### Output
Vehicle Information
Fare Details

### 

### Explanation

ElectricCar inherits features from both Vehicle and FareInfo.

This creates a combination of inheritance types known as Hybrid Inheritance.

# Access Modes in Inheritance

C++ provides three inheritance modes.

## Public Inheritance

```cpp
class Car : public Vehicle
{
};
```

Public members remain public.

Most commonly used.

## Protected Inheritance

```cpp
class Car : protected Vehicle
{
};
```

Public members become protected.

## Private Inheritance

```cpp
class Car : private Vehicle
{
};
```

Public and protected members become private.

Least commonly used.

# Advantages of Inheritance

## Code Reusability

Existing code can be reused without rewriting.

## Reduced Redundancy

Common functionality is written only once.

## Better Organization

Classes can be arranged logically.

## Easier Maintenance

Changes in the base class automatically reflect in derived classes.

## Supports Polymorphism

Inheritance is the foundation of runtime polymorphism.

## Scalability

New derived classes can be added easily.

# Limitations of Inheritance

## Tight Coupling

Changes in the base class may affect derived classes.

## Complex Hierarchies

Deep inheritance chains become difficult to understand.

## Reduced Flexibility

Inheritance relationships are fixed after design.

## Diamond Problem

Multiple inheritance can create ambiguity when two parent classes inherit the same base class.

C++ solves this using Virtual Inheritance.

# Real-World Applications of Inheritance

Inheritance is widely used in:

- Vehicle Management Systems
- Banking Applications
- Hospital Management Systems
- Online Shopping Platforms
- Airline Reservation Systems
- Employee Management Systems
- Game Development
- Educational Platforms like AlphaKnowledge

For example, in a Vehicle Management System:

```text
Vehicle
   |
--------------------------------
|              |              |
Car           Bike          Truck
```

All vehicle types share common functionality while maintaining their own specialized features.

# Summary

Inheritance is an Object-Oriented Programming concept that allows one class to acquire the properties and behaviors of another class. It promotes code reusability, reduces duplication, and helps create logical relationships between classes. C++ supports Single, Multiple, Multilevel, Hierarchical, and Hybrid Inheritance. By using inheritance, developers can build scalable, maintainable, and modular software systems while modeling real-world relationships effectively.




