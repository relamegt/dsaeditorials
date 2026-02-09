# C++ Introduction Part-1

## What is Programming?

 **Programming**  is the process of giving instructions to a computer to solve a problem or perform a task.

A computer itself is dumb—it only understands  **machine-level instructions** . Programming languages act as a  **bridge between human logic and machine execution** .

 **Real-life analogy** 
Think of programming like giving step-by-step cooking instructions.
If steps are wrong or unclear → dish fails.
Same with programs.

---

## What is C++?

 **C++**  is a  **general-purpose programming language**  developed by  **Bjarne Stroustrup**  as an extension of the C language.

It combines:

Speed of low-level languages

Abstraction of high-level languages

Object-Oriented Programming (OOP)

 **Why C++ still matters** 

Gives  **full control over memory** 

Extremely  **fast execution** 

Used where  **performance is critical** 

---

## Features of C++

 **High Performance**  (close to hardware)

 **Object-Oriented**  (classes, objects, inheritance)

 **Supports Procedural + OOP** 

 **Manual Memory Control** 

 **STL (Standard Template Library)** 

---

## Where is C++ Used?

### 🔹 Placements & Interviews

Strong base language for  **DSA** 

Common in product-based companies

### 🔹 Competitive Programming

Fast I/O

STL makes problem solving efficient

### 🔹 System Software

Operating Systems

Game Engines

Compilers

Databases

---

## How C++ Code Runs

![Editorial Image](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-introduction-part-1/1770628599435-Screenshot_2026-02-09_144418.png)

## Structure of a C++ Program

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World";
    return 0;
}
```

### Output
Hello World

## Breakdown

🔹  `#include <iostream>` 

Preprocessor directive

Imports input/output functionality

🔹  `main()` 

Program execution  **starts here** 

OS calls  `main()`  automatically

🔹  `return 0;` 

Signals successful execution to OS

---

## Preprocessor Directives & Macros

What is  `#include` ?

Copies content of header file  **before compilation** 

### Header Files

 `iostream`  → input/output

 `cmath`  → math functions

 `cstring`  → string functions

---

## Macros

 *`#define PI 3.14`* 

 **Why macros are used** 

Constant values

Faster replacement (no memory allocation)

---

## Identifiers & Keywords

Identifiers

Names given to:

Variables

Functions

Classes

```cpp
int studentAge;
float averageMarks;
```

Rules

Letters, digits,  `_`  only

Cannot start with digit

No keywords

Case-sensitive

### Naming Conventions

| Entity | Style |
| --- | --- |
| Variables | camelCase |
| Functions | camelCase |
| Classes | PascalCase |

### Keywords vs Identifiers

| Keywords | Identifiers |
| --- | --- |
| Reserved | User-defined |
| Define behavior | Name entities |
| int, while | count, sum |

---

## Input & Output (I/O)

Output –  `cout` 

```cpp
cout << "Hello";
```

Uses insertion operator   `<<` Sends data to output stream

---

### Input –  `cin`

```cpp
int age;
cin >> age;
```

Uses extraction operator  `>>` 

Reads from keyboard → memory

 **Stream concept** 
Data flows like water:

Keyboard → Memory ( `cin` )

Memory → Screen ( `cout` )

---

## Variables, Memory & Naming Rules

### What is a Variable?

A variable is a  **named memory location** .

int x = 10;

 

  **Memory insight** 

 `x`  is just a label

Actual value stored in RAM

---

### Declaration vs Initialization

```cpp
int a;        // declaration
a = 5;        // initialization

int b = 10;   // both
```

---

## Data Types & Type Modifiers

### Primitive Data Types

| Type | Size (approx) |
| --- | --- |
| int | 4 bytes |
| float | 4 bytes |
| double | 8 bytes |
| char | 1 byte |
| bool | 1 byte |

---

### Type Modifiers

unsigned int x;

 `long long y;`  

 

---

## Constants & Type Casting

### Constants

const int MAX = 100;

### Type Casting

Implicit

 `int a = 10;
double b = a; // automatic` 

Explicit

 `double x = 9.8;
int y = (int)x; // forced` 

 **** 

 ***Explicit casting = programmer taking responsibility.***




