# Encapsulation in C++

Encapsulation is one of the four fundamental pillars of Object-Oriented Programming (OOP). It is the process of combining data members (variables) and member functions (methods) into a single unit called a class while restricting direct access to the internal data.

In simple terms, encapsulation means hiding an object's internal details and allowing controlled access only through well-defined methods.

Encapsulation helps protect data from unauthorized modification and ensures that objects remain in a valid state throughout their lifetime.

# Real-World Analogy of Encapsulation

Consider an ATM machine.

When you withdraw money from an ATM, you interact with buttons, menus, and options on the screen.

However, you do not know:

- How the ATM verifies your PIN.
- How it communicates with the bank server.
- How account balances are updated.
- How cash is dispensed internally.

You only use the services provided by the ATM.

The internal implementation remains hidden.

This is exactly how encapsulation works in programming.

```text
User
  ↓
Public Interface
  ↓
Private Data
```

The user can access functionality through public methods but cannot directly access or modify private data.

# Why Do We Need Encapsulation?

Imagine a Student class where marks are declared as public.

```cpp
class Student
{
public:
    int marks;
};
```

Now anyone can write:

```cpp
Student s1;

s1.marks = -500;
```

A student's marks can never be negative.

Allowing direct access can lead to invalid data and unpredictable program behavior.

Encapsulation solves this problem by hiding the data and allowing modifications only through controlled methods.

Benefits include:

- Protecting sensitive data.
- Preventing invalid values.
- Improving code organization.
- Making programs easier to maintain.
- Supporting data validation.
- Increasing software security.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/encapsulation-in-c/1781089544218-6220a06a-f079-48d1-a9eb-c2e33a93e9d4.png)

# How Encapsulation is Implemented in C++

Encapsulation is implemented using access specifiers.

The most commonly used access specifiers are:

- private
- public
- protected

The general approach is:

1. Keep data members private.
2. Provide public member functions.
3. Use getter methods to read data.
4. Use setter methods to modify data.

# Access Specifiers in Encapsulation

## Private

Private members can only be accessed inside the class.

```cpp
private:
    int marks;
```

External code cannot access private variables directly.

## Public

Public members can be accessed from anywhere in the program.

```cpp
public:
    void display();
```

Public methods act as controlled gateways to private data.

## Protected

Protected members can be accessed inside the class and by derived classes.

Protected is mainly used in inheritance.

# Basic Example of Encapsulation

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
private:

    string name;

public:

    void setName(string n)
    {
        name = n;
    }

    string getName()
    {
        return name;
    }
};

int main()
{
    Student s1;

    s1.setName("Mohit");

    cout << s1.getName();

    return 0;
}
```

### Output
Mohit

### 

The variable `name` is private and cannot be accessed directly.

Instead, access is provided through getter and setter methods.

# Understanding Getters and Setters

Getter and Setter methods are commonly used in encapsulation.

## Getter

A getter method returns the value of a private variable.

Example:

```cpp
string getName()
{
    return name;
}
```

The getter provides read access.

## Setter

A setter method modifies the value of a private variable.

Example:

```cpp
void setName(string n)
{
    name = n;
}
```

The setter provides controlled write access.

# Encapsulation with Validation

One of the biggest advantages of encapsulation is the ability to validate data before storing it.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
private:

    int marks;

public:

    void setMarks(int m)
    {
        if(m >= 0 && m <= 100)
        {
            marks = m;
        }
        else
        {
            cout << "Invalid Marks" << endl;
        }
    }

    int getMarks()
    {
        return marks;
    }
};

int main()
{
    Student s1;

    s1.setMarks(95);

    cout << s1.getMarks();

    return 0;
}
```

### Output
95

### 

Only valid marks between 0 and 100 are accepted.

Without encapsulation, invalid values could easily enter the system.

# Example: Bank Account System

Encapsulation is heavily used in banking applications.

## Example Code

```cpp
#include <iostream>
using namespace std;

class BankAccount
{
private:

    double balance;

public:

    void deposit(double amount)
    {
        if(amount > 0)
        {
            balance += amount;
        }
    }

    double getBalance()
    {
        return balance;
    }
};

int main()
{
    BankAccount account;

    account.deposit(5000);

    cout << "Balance: "
         << account.getBalance();

    return 0;
}
```

### Output
Balance: 5000

### 

The balance variable is hidden from direct access.

Only approved operations can modify it.

# Data Hiding Through Encapsulation

Data Hiding is one of the most important outcomes of encapsulation.

Example:

```cpp
class Student
{
private:
    int marks;
};
```

Attempting:

```cpp
Student s1;

s1.marks = 95;
```

produces an error because marks is private.

This prevents accidental or unauthorized modifications.

# Read-Only Encapsulation

Sometimes data should be visible but not modifiable.

In such situations, only a getter is provided.

## Example Code

```cpp
#include <iostream>
using namespace std;

class AlphaKnowledge
{
private:

    string portalCode =
        "AK2026";

public:

    string getPortalCode()
    {
        return portalCode;
    }
};

int main()
{
    AlphaKnowledge portal;

    cout << portal.getPortalCode();

    return 0;
}
```

### Output
AK2026

### 

The `portalCode` data member is declared as private, so it cannot be accessed directly from outside the `AlphaKnowledge` class. The public method `getPortalCode()` provides controlled access to the portal code while maintaining data security through encapsulation.

Since no setter exists, the value cannot be changed externally.

# Write-Only Encapsulation

Sometimes data should be modified but not displayed.

Only a setter method is provided.

## Example

```cpp
class Password
{
private:

    string password;

public:

    void setPassword(string p)
    {
        password = p;
    }
};
```

External code can set the password but cannot retrieve it.

This increases security.

# Encapsulation and Security

Encapsulation improves software security because:

- Sensitive information remains hidden.
- Unauthorized modifications are prevented.
- Validation can be applied before storing data.
- Internal implementation remains protected.

Examples:

- Banking systems
- Hospital management systems
- Student management systems
- Employee management systems
- Online payment systems

All use encapsulation extensively.

# Encapsulation vs Data Hiding

Many beginners confuse these two concepts.

Although related, they are not exactly the same.

| Encapsulation | Data Hiding |
| --- | --- |
| Bundles data and methods together. | Restricts access to data. |
| Achieved using classes. | Achieved using access specifiers. |
| Focuses on structure and organization. | Focuses on protection and security. |
| Supports data hiding. | Is a result of encapsulation. |

Data hiding is one benefit of encapsulation.

# Best Practices for Encapsulation

While designing classes:

- Keep data members private.
- Expose only necessary methods.
- Validate user input inside setters.
- Avoid making variables public unnecessarily.
- Provide only the access that users actually need.
- Use read-only properties whenever possible.
- Protect sensitive information.

These practices improve security and maintainability.

# Advantages of Encapsulation

### Data Security

Private data cannot be modified directly from outside the class.

### Better Control

Developers can control how data is accessed and modified.

### Improved Maintainability

Internal implementation can change without affecting external code.

### Reusability

Encapsulated classes can be reused in multiple applications.

### Flexibility

Validation rules can be updated without changing external code.

### Modularity

Related data and functions stay together in a single unit.

# Limitations of Encapsulation

Although extremely useful, encapsulation also has a few limitations.

### Additional Code

Getter and setter methods increase the amount of code.

### Slight Overhead

Function calls introduce a very small runtime overhead.

### Reduced Direct Access

Sometimes direct access may be simpler for very small programs.

However, these drawbacks are usually negligible compared to the benefits.

# Real-World Applications of Encapsulation

Encapsulation is used in almost every Object-Oriented application.

Examples include:

- Banking Systems
- ATM Software
- Student Management Systems
- Hospital Management Systems
- Library Management Systems
- Inventory Systems
- E-Commerce Applications
- Employee Management Systems

Without encapsulation, managing large applications would become difficult and error-prone.

# Summary

Encapsulation is the process of combining data members and member functions into a single unit while restricting direct access to internal data. It is implemented using access specifiers such as private, public, and protected. By using getter and setter methods, classes can provide controlled access to their data while preventing invalid modifications. Encapsulation improves security, maintainability, modularity, and code reusability, making it one of the most important principles of Object-Oriented Programming in C++.




