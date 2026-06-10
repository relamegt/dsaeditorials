# C++ Classes and Objects

Classes and Objects are the foundation of Object-Oriented Programming (OOP) in C++. Almost every OOP concept such as encapsulation, inheritance, abstraction, and polymorphism revolves around classes and objects.

In real life, we interact with various objects such as cars, bikes, smartphones, laptops, and employees. Each object has certain characteristics and performs specific actions.

For example, consider a vehicle:

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

In Object-Oriented Programming, such real-world entities are represented using **Classes and Objects**.

A **Class** acts as a blueprint that defines what properties and behaviors an object should have.

An **Object** is a real instance created from that blueprint.

```text
Class  → Vehicle

Object → MyCar
```

The class only defines the structure, whereas the object stores actual values and performs actions.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-classes-and-objects/1781086165441-557783bd-3e89-4332-9380-e3089b38f5bf.png)

# What is a Class?

A class is a user-defined data type that groups related data and functions into a single unit.

It acts as a blueprint for creating objects.

A class defines:

- What data an object can store.
- What operations an object can perform.
- How the object should behave.

A class itself does not occupy memory.

Memory is allocated only when objects are created from the class.

## Why Do We Need Classes?

Imagine creating details for hundreds of vehicles.

Without classes, we would have to create separate variables for every vehicle.

```cpp
string car1Brand;
string car1Color;

string car2Brand;
string car2Color;
```

This quickly becomes difficult to manage.

Instead, we can create a Vehicle class and generate as many vehicle objects as needed.

Classes help:

- Organize code.
- Reduce duplication.
- Improve reusability.
- Simplify maintenance.
- Model real-world entities efficiently.

# Components of a Class

A class mainly consists of two components.

## Data Members

Data members are variables declared inside a class.

They store information about an object.

For a Vehicle class:

```cpp
string brand;
string color;
int topSpeed;
```

These variables represent the state of a vehicle.

## Member Functions

Member functions define the actions that an object can perform.

Examples:

```cpp
start();
stop();
accelerate();
displayInfo();
```

These functions define the behavior of the object.

# Syntax of a Class

```cpp
class ClassName
{
public:

    // Data Members

    // Member Functions
};
```

# Creating a Class

The `class` keyword is used to define a class.

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
    return 0;
}
```

In this example:

- Vehicle is the class.
- brand and color are data members.
- displayInfo() is a member function.

No memory is allocated yet because no object has been created.

# What is an Object?

An object is an instance of a class.

When an object is created:

- Memory is allocated.
- Data members get storage.
- Member functions become accessible.

Objects represent actual entities.

For example:

```cpp
Vehicle myCar;
```

Here:

- Vehicle → Class
- myCar → Object

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-classes-and-objects/1781086250026-44f515e7-0c09-4596-b54e-52d7aac5eaa8.png)

# Characteristics of an Object

Every object has three important characteristics.

## State

State represents the current values stored inside an object.

Example:

```text
Brand      : Toyota
Color      : Violet
Fuel Type  : Petrol
```

These values describe the current state of the object.

## Behavior

Behavior represents the actions that the object can perform.

Examples:

```text
start()
stop()
accelerate()
brake()
```

These actions are implemented using member functions.

## Identity

Every object has a unique identity in memory.

Even if two vehicles have identical properties, they are still different objects because they occupy different memory locations.

# Creating Objects

Once a class is defined, objects can be created just like variables.

## Syntax

```cpp
ClassName objectName;
```

## Example

```cpp
Vehicle myCar;
```

This statement creates an object named myCar.

Memory is allocated for all data members inside the object.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-classes-and-objects/1781086301706-46830686-7262-49c7-a3c5-1c8371c29798.png)

# Accessing Class Members

Members of a class are accessed using the dot (`.`) operator.

### Syntax

```cpp
objectName.member;
```

For functions:

```cpp
objectName.functionName();
```

---

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    string brand;

    void displayBrand()
    {
        cout << "Brand: " << brand;
    }
};

int main()
{
    Vehicle myCar;

    myCar.brand = "Toyota";

    myCar.displayBrand();

    return 0;
}
```

### Output

```text
Brand: Toyota
```

The dot operator is used to access both data members and member functions.

# Complete Example of Class and Object

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    string brand;
    string color;
    string fuelType;

    void displayInfo()
    {
        cout << "Brand: " << brand << endl;
        cout << "Color: " << color << endl;
        cout << "Fuel Type: " << fuelType << endl;
    }
};

int main()
{
    Vehicle myCar;

    myCar.brand = "Toyota";
    myCar.color = "Violet";
    myCar.fuelType = "Petrol";

    myCar.displayInfo();

    return 0;
}
```

### Output
Brand: Toyota
Color: Violet
Fuel Type: Petrol

### 

This example demonstrates how a class defines a structure while an object stores actual data.

# Multiple Objects from the Same Class

One of the biggest advantages of classes is that multiple objects can be created from the same blueprint.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:
    string brand;

    void displayBrand()
    {
        cout << brand << endl;
    }
};

int main()
{
    Vehicle car1;
    Vehicle car2;

    car1.brand = "Toyota";
    car2.brand = "Honda";

    car1.displayBrand();
    car2.displayBrand();

    return 0;
}
```

### Output
Toyota
Honda

### 

Both objects share the same structure but store different values.

# Object Initialization

Objects can be initialized after creation by assigning values to their data members.

```cpp
Vehicle myCar;

myCar.brand = "Toyota";
myCar.color = "Violet";
```

This process is called object initialization.

For larger programs, constructors are generally used for initialization.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-classes-and-objects/1781086346031-958b4c39-5801-4248-a589-714102370907.png)

# Memory Representation of Objects

Consider the following class:

```cpp
class Vehicle
{
public:
    string brand;
    int topSpeed;
};
```

When an object is created:

```cpp
Vehicle myCar;
```

Memory is allocated for:

```text
myCar

Brand      → Toyota
Top Speed  → 160
```

Each object gets its own separate copy of data members.

However, member functions are shared among all objects.

This helps reduce memory usage.

# Class vs Object

| Class | Object |
| --- | --- |
| Blueprint or template. | Instance of a class. |
| Defines properties and behavior. | Stores actual values. |
| Does not occupy memory by itself. | Occupies memory when created. |
| Represents a general concept. | Represents a real entity. |
| Used to create objects. | Created from a class. |
| One class can create many objects. | Each object belongs to a class. |

# Real-World Example

Consider a Vehicle class.

```text
Class → Vehicle
```

Possible objects:

```text
Object 1 → MyCar
Object 2 → MyBike
Object 3 → DeliveryVan
```

All objects belong to the same class but contain different values.

```text
MyCar
Brand : Toyota
Color : Violet

MyBike
Brand : Yamaha
Color : Black

DeliveryVan
Brand : Tata
Color : White
```

The class provides the blueprint, while objects represent actual entities.

# Advantages of Classes and Objects

Using classes and objects offers several benefits.

- Better organization of code.
- Improved readability.
- Increased code reusability.
- Easier maintenance.
- Real-world modeling capability.
- Better scalability.
- Reduced code duplication.
- Foundation for advanced OOP concepts.

Classes and objects make programs more structured and easier to manage as project size increases.

# Summary

A class is a user-defined blueprint that defines the properties and behaviors of objects. It contains data members and member functions that together describe an entity. An object is an instance of a class that occupies memory and stores actual values. Classes help organize code, improve reusability, and model real-world systems effectively. Understanding classes and objects is essential because they form the foundation of Object-Oriented Programming and all advanced OOP concepts in C++.




