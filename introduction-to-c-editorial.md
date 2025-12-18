# Introduction to C++

Introduction to C++

C++ is a **general-purpose programming language** developed by **Bjarne Stroustrup**. It was created as an extension of the **C language** by adding **object-oriented programming (OOP)** features.
Because of its **high speed and control**, C++ is widely used in **software development, game engines, operating systems, embedded systems, and competitive programming**.

## Main Features of C++

<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/introduction-to-c/1766083914594_main_features_of_C_.png" style="max-width:100%;height:auto;"/>

### 1. Simple and Structured

C++ allows programs to be divided into **small logical blocks** using functions and classes.
It provides a **rich standard library** and many built-in data types, which makes programs easy to organize and maintain.

### 2. Machine Independent

A C++ program can run on different machines **without changing the code**, as long as a suitable compiler is available for that system.

### 3. Low-Level Access

C++ provides **direct access to memory** using pointers.
This makes it suitable for **system-level programming** like operating systems and device drivers.

### 4. Fast Execution

C++ programs execute very fast because there is **very little runtime overhead**.
This is why it is preferred in **performance-critical applications**.

### 5. Object-Oriented Programming

C++ supports **classes, objects, inheritance, polymorphism, encapsulation, and abstraction**, which help in building **large, reusable, and scalable applications**.

## First C++ Program

Below is a simple C++ program that prints **Hello, World!**

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

**Output:**

```
Hello, World!
```

## Structure of a C++ Program

Every C++ program follows a standard structure.

### 1. Header File

```
#include <iostream>
```

This header file provides input and output objects like *`cin`* and *`cout`*.

### 2. Namespace

```
using namespace std;
```

This allows us to use standard names like *`cout`* directly instead of *`std::cout`*.

### 3. Main Function

```
int main() {
    // program code
}
```

Program execution **always starts from the *`main()`* function**.

### 4. Statements

```
cout << "Hello World";
```

Statements perform actions such as **printing output or processing data**.

### 5. Return Statement

```
return 0;
```

This tells the operating system that the program executed **successfully**.

## History of C++

C++ was developed in **1979 at Bell Labs** by **Bjarne Stroustrup**.
Initially, it was called **“C with Classes”** and later renamed **C++** in **1983**.

Over time, C++ evolved through standards like **C++98, C++11, C++14, C++17, C++20, and C++23**, adding modern features while maintaining performance.

# C++ Identifiers

**Last Updated: 15 Sep, 2025**
**Alpha Knowledge**

Identifiers are **names given by programmers** to program elements like variables, functions, and classes.

## Example of Identifiers

```
int value = 10;     // variable identifier
void show() {}     // function identifier
```

Here, *`value`* and *`show`* are identifiers.

## Rules for Naming Identifiers

- Can contain letters, digits, and underscores
- Must start with a letter or underscore
- Cannot use C++ keywords
- Must be unique within scope
- Case-sensitive (Total and total are different)

## Valid Identifier Example

```
#include <iostream>
using namespace std;

class Car {
    string brand;
    int year;
};

void add(int a, int b) {
    int sum = a + b;
    cout << sum;
}

int main() {
    int age = 20;
    add(5, 7);
    return 0;
}
```

**Output**

```
12
```

## Identifier Naming Conventions (Recommended)

### Variables

- camelCase
- Example: studentAge, totalMarks

### Functions

- camelCase with verbs
- Example: getData(), calculateSum()

### Classes

- PascalCase
- Example: Student, Car

# C++ Keywords

**Last Updated: 17 Sep, 2025**
**Alpha Knowledge**

Keywords are **reserved words** that have predefined meanings in C++.
They **cannot be used as identifiers**.

## Keyword Example

```
int age = 18;

if (age >= 18) {
    cout << "Adult";
}
```

## Invalid Use of Keyword

```
int return = 5;   // ❌ Invalid
```

## Keywords vs Identifiers

| Keywords | Identifiers |
| --- | --- |
| Reserved words | User-defined names |
| Fixed meaning | Meaning decided by programmer |
| Always lowercase | Can be uppercase or lowercase |
| Example: int, if | Example: count, sum1 |

# Variables in C++

**Last Updated: 08 Oct, 2025**
**Alpha Knowledge**

A variable is a **named memory location** used to store data.

## Variable Example

```
int number = 5;
cout << number;
```

## Declaring Variables

```
int a;
int x, y, z;
```

## Initializing Variables

```
int num = 10;
```

## Updating Variables

```
int num = 3;
num = 7;
```

## Constant Variables

```
const int MAX = 100;
```

The value of *`MAX`* **cannot be changed**.

## Variable Scope

Scope defines **where a variable can be accessed** — inside a block, function, or globally.

# Data Types in C++

**Last Updated: 10 Oct, 2025**
**Alpha Knowledge**

Data types specify **what type of data** a variable can store.

## 1. Character (char)

```
char grade = 'A';
cout << grade;
```

## 2. Integer (int)

```
int count = 25;
cout << count;
```

## 3. Boolean (bool)

```
bool isPassed = true;
cout << isPassed;
```

## 4. Float (float)

```
float price = 45.6;
cout << price;
```

## 5. Double (double)

```
double pi = 3.14159;
cout << pi;
```

## 6. Void (void)

Used for functions that **do not return a value**.

```
void display() {
    cout << "Hello";
}
```

## Type Safety in C++

C++ is **strongly typed**, meaning variables should store values of the correct type.

```
bool flag = 10.5;
cout << flag;
```

**Output**

```
1
```

## Type Conversion

```
char ch = 'A';
int value = ch;
cout << value;
```

**Output**

```
65
```

## Size of Data Types

```
cout << sizeof(int);
cout << sizeof(char);
cout << sizeof(float);
cout << sizeof(double);
```

**Typical Output**

```
4
1
4
8
```

## Data Type Modifiers

Modifiers change the **size or range** of data types.

```
short int a;
long int b;
unsigned int c;
long long int d;
```
