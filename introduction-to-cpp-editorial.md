# Introduction to CPP

C++ is a powerful, general-purpose programming language created by **Bjarne Stroustrup**. It was designed as an extension of the **C language** by adding **object-oriented programming (OOP)** features. Because of its speed and flexibility, C++ is widely used in software development, games, operating systems, and competitive programming.

## Main Features of C++

## 

<img src="https://github.com/relamegt/dsaeditorials/blob/main/images/introduction-to-cpp/1766042108592_main_features_of_C_.png" style="max-width:100%;height:auto;"/>

## 1. Simple and Structured

C++ programs can be divided into small logical parts. It also provides a rich standard library and many built-in data types, making programming easier and organized.

### 2. Machine Independent

A C++ program can run on different machines as long as a suitable compiler is available.

### 3. Low-Level Access

C++ allows direct interaction with memory and hardware resources, which makes it ideal for system programming.

### 4. Fast Execution

C++ programs run very fast because there is minimal overhead during execution.

### 5. Object-Oriented

C++ supports classes, objects, inheritance, and polymorphism, which help in building large, reusable, and maintainable applications.

## First C++ Program

Below is a basic C++ program that prints **Hello, World!** on the screen.

```
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

**Output**

```
Hello, World!
```

## Structure of a C++ Program

A C++ program follows a fixed structure:

### 1. Header File

```
#include <iostream>
```

This includes input/output tools like `cin` and `cout`.

### 2. Namespace

```
using namespace std;
```

This allows us to use standard names like `cout` without writing `std::cout`.

### 3. Main Function

```
int main() {
    // code
}
```

Execution of a C++ program always starts from `main()`.

### 4. Statements

```
cout << "Hello World";
```

Statements perform actions such as printing output.

### 5. Return Statement

```
return 0;
```

Indicates successful execution of the program.

## History of C++

C++ was developed in **1979 at Bell Labs** by **Bjarne Stroustrup**. It was first called **“C with Classes”** and later renamed **C++** in 1983.
Over the years, C++ evolved through standards like **C++98, C++11, C++17, C++20, and C++23**, adding modern features while maintaining high performance.

# C++ Identifiers

**Last Updated: 15 Sep, 2025**
**Alpha Knowledge**

Identifiers are **names given by programmers** to variables, functions, classes, and other program elements.

### Example

```
int value = 10;     // variable identifier
void show() {}     // function identifier
```

Here, `value` and `show` are identifiers.

## Rules for Naming Identifiers

- Can contain letters, digits, and underscores
- Must start with a letter or underscore
- Cannot use C++ keywords
- Must be unique in their scope
- Case-sensitive (`Total` and `total` are different)

<img src="https://github.com/relamegt/dsaeditorials/blob/main/images/introduction-to-cpp/naming%20rules%20final.png" style="max-width:100%;height:auto;"/>

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
- Example: `studentAge`, `totalMarks`

### Functions

- camelCase with verbs
- Example: `getData()`, `calculateSum()`

### Classes

- PascalCase
- Example: `Student`, `Car`

# C++ Keywords

**Last Updated: 17 Sep, 2025**
**Alpha Knowledge**

Keywords are **reserved words** with predefined meanings. They cannot be used as identifiers.

### Example

```
int age = 18;

if (age >= 18) {
    cout << "Adult";
}
```

### Using a Keyword as Identifier (Error)

```
int return = 5;  // Invalid
```

## Keywords vs Identifiers

| Keywords | Identifiers |
| --- | --- |
| Reserved words | User-defined names |
| Fixed meaning | Programmer-defined |
| Lowercase only | Upper or lowercase |
| Example: int, if | Example: count, sum1 |

# Variables in C++

**Last Updated: 08 Oct, 2025**
**Alpha Knowledge**

A variable is a **named memory location** used to store data.

### Example

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

The value of `MAX` cannot be changed.

## Variable Scope

The scope defines **where a variable can be used** in a program (inside a block, function, or globally).

# Data Types in C++

**Last Updated: 10 Oct, 2025**
**Alpha Knowledge**

Data types define **what kind of data** a variable can store.

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

Used for functions that return nothing:

```
void display() {
    cout << "Hello";
}
```

## Type Safety in C++

C++ is **strongly typed**, meaning variables must store values of the correct type.

```
bool flag = 10.5;  
cout << flag;   // Output: 1
```

## Type Conversion

```
char ch = 'A';
int value = ch;
cout << value;   // Output: 65
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

Modifiers change the size or range of data types:

```
short int a;
long int b;
unsigned int c;
long long int d;
```

###
