# Polymorphism in C++

Polymorphism is one of the four fundamental pillars of Object-Oriented Programming (OOP). The word **Polymorphism** comes from two Greek words:

- **Poly** → Many
- **Morph** → Forms

Therefore, polymorphism means **"many forms"**.

In C++, polymorphism allows the same function name, method, or operator to perform different tasks depending on the context in which it is used.

In simple words, a single interface can have multiple implementations.

For example, different types of vehicles may have the same function called `startEngine()`, but each vehicle starts differently.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-c/1781090538647-e12d5d98-4aec-4184-9223-cf2ccc308675.png)

Although the function name is the same, the behavior changes depending on the object.

# Why Do We Need Polymorphism?

Without polymorphism, developers would need to create separate function names for similar operations.

Example:

```cpp
startCar();
startBike();
startTruck();
```

With polymorphism:

```cpp
startEngine();
```

The same function name can work differently for different objects.

Benefits include:

- Improves code reusability.
- Makes programs easier to maintain.
- Reduces code duplication.
- Makes applications more scalable.
- Supports flexible software design.

# Types of Polymorphism

Polymorphism in C++ is broadly divided into two categories:

1. Compile-Time Polymorphism
2. Run-Time Polymorphism

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-c/1781090595523-24b8e889-68a7-45db-89f7-ebe5326ef140.png)

# 1. Compile-Time Polymorphism

Compile-Time Polymorphism is also called:

- Static Polymorphism
- Early Binding

In this type, the compiler determines which function to call during compilation itself.

This type of polymorphism is faster because decisions are made before program execution.

Compile-Time Polymorphism is achieved using:

- Function Overloading
- Operator Overloading

# Function Overloading

Function Overloading allows multiple functions to have the same name but different parameter lists.

The difference may be in:

- Number of parameters
- Data type of parameters
- Order of parameters

The compiler decides which function to call based on the arguments provided.

## Real-World Example

Suppose an automobile company wants to calculate the price of vehicles.

The same function name `calculatePrice()` can be used for different vehicle types.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-c/1781090631986-5e060e1b-dd22-473a-91d9-9085c26add3c.png)

## Example Code

```cpp
#include <iostream>
using namespace std;

class VehiclePrice
{
public:

    void calculatePrice(int price)
    {
        cout << "Car Price: "
             << price << endl;
    }

    void calculatePrice(double price)
    {
        cout << "Bike Price: "
             << price << endl;
    }
};

int main()
{
    VehiclePrice vehicle;

    vehicle.calculatePrice(800000);

    vehicle.calculatePrice(95000.50);

    return 0;
}
```

### Output

```text
Car Price: 800000
Bike Price: 95000.5
```

The compiler determines which version of `calculatePrice()` should execute based on the argument type.

This decision happens during compilation.

# How Function Overloading Works

When the compiler sees:

```cpp
vehicle.calculatePrice(800000);
```

it searches for:

```cpp
void calculatePrice(int);
```

When it sees:

```cpp
vehicle.calculatePrice(95000.50);
```

it searches for:

```cpp
void calculatePrice(double);
```

Thus, the correct function is selected automatically.

---

# Operator Overloading

Operator Overloading allows existing operators to work with user-defined classes.

Normally, operators work with built-in data types.

For example:

```cpp
10 + 20
```

Here, `+` adds integers.

Similarly:

```cpp
"Hello" + "World"
```

can concatenate strings.

C++ allows programmers to define how operators should behave for custom objects.

---

# Real-World Example

Suppose we have a Vehicle class that stores vehicle prices.

Using operator overloading, two vehicle prices can be combined using the `+` operator.

---

## Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    int price;

    Vehicle(int p)
    {
        price = p;
    }

    Vehicle operator+(Vehicle& obj)
    {
        return Vehicle(price + obj.price);
    }
};

int main()
{
    Vehicle car(800000);
    Vehicle bike(100000);

    Vehicle total = car + bike;

    cout << "Total Price: "
         << total.price;

    return 0;
}
```

### Output

```text
Total Price: 900000
```

The overloaded `+` operator allows objects to behave like built-in data types.

This improves readability and usability.

---

# Compile-Time Polymorphism Characteristics

- Faster execution.
- Binding occurs during compilation.
- No virtual functions required.
- Less runtime overhead.
- Easier for small applications.

---

# 2. Run-Time Polymorphism

Run-Time Polymorphism is also called:

- Dynamic Polymorphism
- Late Binding

In this type, the decision about which function to execute is made while the program is running.

This is achieved using:

- Virtual Functions
- Function Overriding

Run-time polymorphism provides flexibility because the actual object determines which function executes.

---

# Real-Life Illustration

Consider different vehicle types.

Every vehicle has a function called:

```cpp
startEngine()
```

However:

- Car starts differently.
- Bike starts differently.
- Truck starts differently.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/polymorphism-in-c/1781090090576-5e060e1b-dd22-473a-91d9-9085c26add3c.png)

Even though the function name is identical, the behavior changes according to the object.

This is runtime polymorphism.

# Function Overriding

Function Overriding occurs when a derived class provides its own implementation of a function that already exists in the base class.

For runtime polymorphism:

- The base class function must be declared as `virtual`.
- The derived class must override that function.

# Example Code

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    virtual void startEngine()
    {
        cout << "Vehicle Engine Started"
             << endl;
    }
};

class Car : public Vehicle
{
public:

    void startEngine() override
    {
        cout << "Car Engine Started"
             << endl;
    }
};

class Bike : public Vehicle
{
public:

    void startEngine() override
    {
        cout << "Bike Engine Started"
             << endl;
    }
};

int main()
{
    Vehicle* vehiclePtr;

    Car car;

    vehiclePtr = &car;

    vehiclePtr->startEngine();

    return 0;
}
```

### Output
Car Engine Started

### 

Although the pointer type is `Vehicle`, the function of the `Car` object executes because the decision is made at runtime.

# Understanding Virtual Functions

A virtual function tells the compiler:

```text
"Do not decide now.
Decide at runtime
based on the actual object."
```

Example:

```cpp
virtual void startEngine();
```

Without the `virtual` keyword, the base class version would always execute.

# Another Runtime Example

```cpp
#include <iostream>
using namespace std;

class Vehicle
{
public:

    virtual void showType()
    {
        cout << "Generic Vehicle";
    }
};

class Truck : public Vehicle
{
public:

    void showType() override
    {
        cout << "Heavy Truck";
    }
};

int main()
{
    Vehicle* ptr;

    Truck truck;

    ptr = &truck;

    ptr->showType();

    return 0;
}
```

### Output
Heavy Truck

### 

The overridden function executes dynamically at runtime.

# Compile-Time vs Run-Time Polymorphism

| Compile-Time Polymorphism | Run-Time Polymorphism |
| --- | --- |
| Also called Static Polymorphism | Also called Dynamic Polymorphism |
| Binding occurs during compilation | Binding occurs during execution |
| Faster execution | Slightly slower |
| Achieved using Function Overloading | Achieved using Function Overriding |
| No virtual functions needed | Virtual functions required |
| Less flexible | More flexible |
| Compiler decides function call | Runtime decides function call |

# Advantages of Polymorphism

### Code Reusability

The same interface can be reused for different objects.

### Better Maintainability

Changes can be made without affecting existing code.

### Extensibility

New derived classes can be added easily.

### Cleaner Code

Developers can work with common interfaces instead of multiple function names.

### Flexibility

Objects can behave differently using the same function call.

# Real-World Applications of Polymorphism

Polymorphism is widely used in:

- Vehicle Management Systems
- Game Development
- Banking Applications
- E-Commerce Platforms
- GUI Frameworks
- Hospital Management Systems
- Online Learning Platforms
- Payment Gateway Systems

For example, in a Vehicle Management System, different vehicles such as Cars, Bikes, and Trucks may all use the same function name like `startEngine()`, but each vehicle provides its own implementation.

# Summary

Polymorphism is the ability of a function, method, or operator to behave differently depending on the context or object being used. It is one of the most important concepts in Object-Oriented Programming because it improves flexibility, reusability, and maintainability. C++ supports two main types of polymorphism: Compile-Time Polymorphism, achieved through Function Overloading and Operator Overloading, and Run-Time Polymorphism, achieved through Virtual Functions and Function Overriding. By using polymorphism, developers can create scalable and efficient applications while writing cleaner and more reusable code.




