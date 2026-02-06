# C++ Introduction Part-1

# Introduction to C++

 **C++**  is a  **general-purpose, high-level programming language**  developed by  **Bjarne Stroustrup**  as an extension of the C language. It supports  **procedural, object-oriented, and generic programming** , making it powerful and flexible. C++ is widely used for system software, game development, competitive programming, embedded systems, and performance-critical applications.

---

# Structure of a C++ Program

A C++ program follows a well-defined structure:

1. Documentation / Comments
2. Preprocessor directives
3. Global declarations
4. main() function
5. User-defined functions (optional)

### Basic Structure Example

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello World";
    return 0;
}
```
### Output
Hello World

---

# How Does a C++ Program Run?

The execution of a C++ program happens in the following steps:

1. PreprocessingHandles #include, #define, macros
2. CompilationConverts source code into object code
3. LinkingLinks libraries and object files
4. ExecutionFinal executable runs starting from main()

---

# Preprocessor Directives

Preprocessor directives begin with  `#`  and are processed  **before compilation** .

### Common Preprocessor Directives:

- #include – Includes header files
- #define – Defines macros
- #undef – Undefines a macro
- #ifdef, #ifndef, #endif – Conditional compilation

Example:
 `#include <iostream>
#define PI 3.14` 

---

# Macros

A  **macro**  is a symbolic constant or code fragment defined using  `#define` .

### Example:
 `#define MAX 100` 
Macros do not follow data type rules and are replaced directly by the preprocessor.

---

# The  `main()`  Function

- main() is the entry point of every C++ program
- Program execution always starts from main()

### Syntax:
 `int main() {
    // statements
    return 0;
}` 
- int → return type
- return 0 → indicates successful execution

---

# Namespace

A  **namespace**  is used to avoid name conflicts in large programs.

### Example:
 `using namespace std;` 
- std is the standard C++ namespace
- Without it, we must write std::cout, std::cin

---

# Identifiers

Identifiers are  **names given to variables, functions, arrays, etc.** 

### Rules:

- Can contain letters, digits, underscore
- Must begin with a letter or underscore
- Cannot be a keyword
- Case-sensitive

Valid:  `sum` ,  `_count` ,  `total1` 
Invalid:  `1num` ,  `float` ,  `total-value` 

---

# Keywords

Keywords are  **reserved words**  with predefined meaning in C++.

Examples:
 `int` ,  `float` ,  `if` ,  `else` ,  `for` ,  `while` ,  `return` ,  `class` ,  `const` 

👉 Keywords  **cannot be used as identifiers** .

---

# Input and Output in C++

C++ uses  **stream-based I/O**  from  `<iostream>` .

- cin → input
- cout → output

### Example:
 `int x;
cin >> x;
cout << x;` 
- << → extraction operator
- << → insertion operator

---

# Variables

A  **variable**  is a named memory location used to store data.

### Declaration:
 `int age;
float salary;` 
### Initialization:
 `int age = 20;` 

---

# Data Types in C++

## Basic Data Types:

- int – integers
- float – decimal values
- double – high-precision decimals
- char – characters
- bool – true/false

## Derived Data Types:

- Arrays
- Pointers
- Functions

## User-Defined Data Types:

- struct
- union
- enum
- class

---

# Comments in C++

Comments are used to  **explain code**  and are ignored by the compiler.

### Types of Comments:

// Single Line Comment

/* Line1

Line2 */

---

# Constants

Constants are values that  **cannot be changed**  during program execution.

### Using  `const` :
 `const int MAX = 100;` 
### Using  `#define` :
 `#define PI 3.14` 

---

# Type Casting

Type casting is the  **conversion of one data type into another** .

## Implicit Type Casting

Done automatically by the compiler.
 `int x = 10;
float y = x;` 
## Explicit Type Casting

Done manually by the programmer.
 `float avg = (float)sum / count;` 
#

<approaches>
## Approach



</approaches>




