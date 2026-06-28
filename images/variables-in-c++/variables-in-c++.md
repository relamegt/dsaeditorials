# Variables in C++

## Introduction

A variable in C++ is a named memory location used to store data that can be read and modified at any point during program execution. Instead of working with raw memory addresses, programmers assign descriptive names to storage locations through variables, making code far more readable and maintainable.

Every variable in C++ has three essential properties: a **name** (the identifier used to refer to it), a **data type** (which determines what kind of value it holds and how much memory it occupies), and a **value** (the actual data stored). C++ provides several built-in data types — `int`, `char`, `float`, `double`, `bool`, and more — to accommodate different categories of data.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/variables-in-c/1782643044679-ChatGPT_Image_Jun_9%2C_2026%2C_01_18_57_PM.png)

### Key Features

- Variables serve as labeled containers for values stored in memory.
- Each variable name must be unique within its scope.
- The data type of a variable cannot change after declaration.
- Variable values can be updated at any point during execution.
- Multiple variables of the same type can be declared in a single statement.

## Declaring Variables

A variable declaration tells the compiler the variable's name and the type of data it will hold. Memory is allocated at this point.

```Cpp
data_type variable_name;
```

```Cpp
int age;
float percentage;
char grade;
bool isActive;
```

## Creating and Initializing Variables

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 20;
    float height = 5.8;
    char grade = 'A';

    cout << "Age    : " << age    << endl;
    cout << "Height : " << height << endl;
    cout << "Grade  : " << grade  << endl;

    return 0;
}
```

### Output
Age    : 20
Height : 5.8
Grade  : A

* `age` stores a whole number.
* `height` stores a decimal value.
* `grade` stores a single character enclosed in single quotes.

## Rules for Naming Variables

Variable names in C++ follow the same rules as all identifiers:

1. May contain letters (`A–Z`, `a–z`), digits (`0–9`), and underscores (`_`).
2. Must begin with a letter or an underscore — not a digit.
3. Spaces are not permitted inside a variable name.
4. C++ reserved keywords (`int`, `while`, `return`, `class`) cannot be used as variable names.
5. Variable names are **case-sensitive** — `score`, `Score`, and `SCORE` are three different variables.
6. Names should be descriptive and clearly reflect the variable's purpose.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/variables-in-c/1782642960344-ChatGPT_Image_Jun_9%2C_2026%2C_01_09_03_PM.png)

## Variable Initialization

Assigning the very first value to a variable is called **initialization**. In C++, uninitialized variables hold indeterminate (garbage) values, which can produce unpredictable results if read before being set.

### Initialization at Declaration

```Cpp
#include <iostream>
using namespace std;

int main() {
    int marks = 95;
    float cgpa = 9.24;

    cout << marks << endl;
    cout << cgpa  << endl;

    return 0;
}
```

### Output
95
9.24

### Initialization After Declaration

```Cpp
#include <iostream>
using namespace std;

int main() {
    char section;
    section = 'B';     // Assigned after declaration

    cout << section << endl;

    return 0;
}
```

### Output
B

Variables can receive their first value either at the point of declaration or through a later assignment statement — both approaches are valid in C++.

## Accessing Variables

Once a value is stored in a variable, it can be retrieved simply by using the variable's name anywhere in the program.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int rollNumber = 25;
    cout << rollNumber << endl;
    return 0;
}
```

### Output
25

The variable name acts as a symbolic reference to its memory location. The compiler translates the name into the correct address automatically.

## Updating Variable Values

A variable's stored value can be overwritten at any time using the assignment operator (`=`). The new value replaces the old one completely.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int score = 50;

    cout << "Initial Score : " << score << endl;

    score = 80;
    cout << "Updated Score : " << score << endl;

    score = score + 10;
    cout << "Final Score   : " << score << endl;

    return 0;
}
```

### Output
Initial Score : 50
Updated Score : 80
Final Score   : 90

The third assignment (`score = score + 10`) reads the current value of `score`, adds 10, and stores the result back into the same variable.

## Using Variables in Expressions

Variables participate freely in arithmetic and logical expressions. Results of computations can be stored in new variables.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int a = 30;
    int b = 20;

    int sum     = a + b;
    int product = a * b;
    int diff    = a - b;

    cout << "Sum     = " << sum     << endl;
    cout << "Product = " << product << endl;
    cout << "Diff    = " << diff    << endl;

    return 0;
}
```

### Output
Sum     = 50
Product = 600
Diff    = 10

## Declaring Multiple Variables

Several variables of the same type can be declared and initialized together in a single statement, separated by commas.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int physics = 85, chemistry = 90, mathematics = 95;

    cout << physics     << " "
         << chemistry   << " "
         << mathematics << endl;

    return 0;
}
```

### Output
85 90 95

## Memory Allocation for Variables

Each variable occupies a specific amount of memory determined by its data type. The `sizeof()` operator returns the number of bytes allocated to a variable or type.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 21;
    double salary = 45000.75;
    char grade = 'A';

    cout << "int    : " << sizeof(age)    << " bytes" << endl;
    cout << "double : " << sizeof(salary) << " bytes" << endl;
    cout << "char   : " << sizeof(grade)  << " bytes" << endl;

    return 0;
}
```

### Output
int    : 4 bytes
double : 8 bytes
char   : 1 bytes

## Common Data Types and Their Typical Sizes

| Data Type | Typical Size | Description |
| --- | --- | --- |
| `char` | 1 byte | Single character |
| `bool` | 1 byte | True or false |
| `int` | 4 bytes | Whole numbers |
| `float` | 4 bytes | Single-precision decimal |
| `double` | 8 bytes | Double-precision decimal |
| `long int` | 8 bytes | Large whole numbers |

## Declaration vs Definition

| Feature | Declaration | Definition |
| --- | --- | --- |
| **Purpose** | Informs the compiler a variable exists | Allocates memory for the variable |
| **Memory Allocated?** | No | Yes |
| **Example** | `extern int age;` | `int age = 20;` |

In most C++ programs, a plain `int age = 20;` acts as both a declaration and a definition simultaneously.

## Advantages of Variables

1. Assign meaningful names to raw memory locations.
2. Allow values to be read, updated, and reused throughout a program.
3. Participate in arithmetic, logical, and relational expressions.
4. Improve code readability compared to using literal values everywhere.
5. Enable dynamic behavior — the same code can work with different data each run.

## Limitations

1. Uninitialized variables hold garbage values that can cause incorrect program behavior.
2. Using the wrong data type for a value may produce silent data loss (e.g., storing 3.7 in an `int` gives 3).
3. Every variable consumes memory — excessive use of large types increases the program's memory footprint.
4. Poorly chosen variable names significantly reduce code readability and maintainability.

> **Note:** In C++, it is strongly recommended to initialize every variable at the point of declaration. Unlike some languages that automatically set variables to zero or null, C++ leaves uninitialized local variables with whatever random data happens to be at that memory address. Always assign a starting value to avoid reading garbage data.

## Summary

A variable in C++ is a named, typed memory location that stores a value throughout program execution. Variables are declared with a data type and a name, and can be initialized at declaration or later through assignment. Their values can be updated at any time and used freely in expressions and calculations. The `sizeof()` operator reveals how much memory each data type occupies. C++ supports multiple simultaneous declarations of the same type and distinguishes between declarations (which inform the compiler) and definitions (which allocate memory). Writing well-named, properly initialized variables is a foundational practice in every C++ program.




