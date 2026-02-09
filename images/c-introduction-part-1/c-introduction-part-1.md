# C++ Introduction Part-1

## What is Programming?

  **Programming**   is the process of giving instructions to a computer to solve a problem or perform a task.

A computer itself is dumb—it only understands   **machine-level instructions**  . Programming languages act as a   **bridge between human logic and machine execution**  .

📌   **Real-life analogy**  
Think of programming like giving step-by-step cooking instructions.
If steps are wrong or unclear → dish fails.
Same with programs.

---

Uses extraction operator  `>>` 

Reads from keyboard → memory

📌  **Stream concept** 

Data flows like water:

Keyboard → Memory ( `cin` )

Memory → Screen ( `cout` )

## What is C++?

  **C++**   is a   **general-purpose programming language**   developed by   **Bjarne Stroustrup**   as an extension of the C language.

It combines:
Speed of low-level languagesAbstraction of high-level languagesObject-Oriented Programming (OOP)

📌   **Why C++ still matters**  
Gives full control over memoryExtremely fast executionUsed where performance is critical

---

## Features of C++

High Performance (close to hardware)Object-Oriented (classes, objects, inheritance)Supports Procedural + OOPManual Memory ControlSTL (Standard Template Library)

---

## Where is C++ Used?

### 🔹 Placements & Interviews

Strong base language for DSACommon in product-based companies

### 🔹 Competitive Programming

Fast I/OSTL makes problem solving efficient

### 🔹 System Software

Operating SystemsGame EnginesCompilersDatabases

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

🔹   `#include`  
Preprocessor directiveImports input/output functionality

🔹   `main()`  
Program execution starts hereOS calls main() automatically

🔹   `return 0;`  
Signals successful execution to OS

---

## Preprocessor Directives & Macros

What is   `#include`  ?
Copies content of header file before compilation

### Header Files

iostream → input/outputcmath → math functionscstring → string functions

---

## Macros

  *`#define PI 3.14`*  

📌   **Why macros are used**  
Constant valuesFaster replacement (no memory allocation)

---

## Identifiers & Keywords

Identifiers

Names given to:
VariablesFunctionsClasses

```cpp
int studentAge;
float averageMarks;
```

Rules
Letters, digits, _ onlyCannot start with digitNo keywordsCase-sensitive

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

Output –   `cout` 

```cpp
cout << "Hello";
```

Uses insertion operator  "<<"Sends data to output stream

---

### Input –   `cin`

```cpp
int age;
cin >> age;
```

Uses extraction operator ">>"Reads from keyboard → memory

📌   **Stream concept**  
Data flows like water:
Keyboard → Memory ("cin")Memory → Screen ("cout")

<approaches>
## Approach




</approaches>



#
