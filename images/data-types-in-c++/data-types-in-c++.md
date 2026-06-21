# Data Types in C++

## Introduction

Data types are one of the fundamental concepts in C++ programming. Every variable in C++ must have an associated data type that specifies what kind of value it can store, how much memory it occupies, and which operations can be performed on it.

Different data types are designed to represent different kinds of information, such as integers, characters, booleans, decimal numbers, and user-defined classes. Choosing an appropriate data type helps improve memory utilization and program efficiency.

### Key Features

- Define the type of data stored in variables.
- Determine the amount of memory allocated.
- Specify the range of values a variable can hold.
- Control the operations that can be performed on data.
- Help in writing efficient and reliable programs.

# Classification of Data Types in C++

Data types in C++ are broadly classified into three categories:

1. Primitive Data Types
2. Derived Data Types
3. User-Defined Data Types

# Primitive Data Types

Primitive data types are built-in data types provided by the C++ language. They are used to store simple values such as integers, characters, truth values, and decimal numbers.

## Integer Data Type

The `int` data type is used to store whole numbers.

### Features

- Stores positive, negative, and zero values.
- Typical size: 4 bytes.
- Does not contain fractional parts.

### Example

```cpp
#include <iostream>

int main()
{
    int marks = 95;

    std::cout << "Marks = " << marks << std::endl;

    return 0;
}
```

### Output
Marks = 95

### Explanation

- The variable `marks` stores an integer value.
- Standard output stream `std::cout` is used to display the output.

## Character Data Type

The `char` data type stores a single character.

### Features

- Typical size: 1 byte.
- Characters are enclosed within single quotes.

### Example

```cpp
#include <iostream>

int main()
{
    char grade = 'A';

    std::cout << "Grade = " << grade << std::endl;

    return 0;
}
```

### Output
Grade = A

### Explanation

- The variable `grade` stores a single character.
- The standard character is outputted directly via `std::cout`.

## Boolean Data Type

The `bool` data type stores boolean values of `true` or `false`.

### Features

- Typical size: 1 byte.
- Useful for condition testing and logical operations.

### Example

```cpp
#include <iostream>

int main()
{
    bool isPassed = true;

    std::cout << "Passed = " << std::boolalpha << isPassed << std::endl;

    return 0;
}
```

### Output
Passed = true

### Explanation

- The variable `isPassed` is initialized to `true`.
- The manipulator `std::boolalpha` is used to output the text "true" instead of the numeric representation "1".

## Float Data Type

The `float` data type stores decimal numbers with single precision.

### Features

- Typical size: 4 bytes.
- Suitable for storing fractional values.

### Example

```cpp
#include <iostream>

int main()
{
    float percentage = 92.75f;

    std::cout << "Percentage = " << percentage << std::endl;

    return 0;
}
```

### Output
Percentage = 92.75

### Explanation

- The float literal suffix `f` is appended to specify a single-precision value.

## Double Data Type

The `double` data type provides higher precision compared to `float`.

### Features

- Typical size: 8 bytes.
- Stores large decimal values accurately.

### Example

```cpp
#include <iostream>

int main()
{
    double cgpa = 9.2456;

    std::cout << "CGPA = " << cgpa << std::endl;

    return 0;
}
```

### Output
CGPA = 9.2456

### Explanation

- The `double` type provides greater precision than `float`.

## Void Data Type

The `void` data type represents the absence of a value.

### Example

```cpp
#include <iostream>

void greet()
{
    std::cout << "Welcome to AlphaKnowledge" << std::endl;
}

int main()
{
    greet();

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

- The function `greet()` does not return any value, so its return type is specified as `void`.

# Derived Data Types

Derived data types are created from primitive data types.

## Arrays

An array stores multiple elements of the same type in contiguous memory locations.

### Example

```cpp
int marks[5] = {90, 85, 95, 88, 92};
```

## Pointers

Pointers store the address of another variable.

### Example

```cpp
int age = 20;
int *ptr = &age;
```

## References

References serve as aliases for existing variables.

### Example

```cpp
int age = 20;
int &ref = age;
```

## Functions

Functions perform specific tasks and may return values.

### Example

```cpp
int add(int a, int b)
{
    return a + b;
}
```

# User-Defined Data Types

User-defined data types allow programmers to create custom data structures.

## Structure

A structure groups related variables of different data types under a single name.

### Example

```cpp
struct Student
{
    char name[30];
    int age;
};
```

## Class

A class is a blueprint for objects in object-oriented programming.

### Example

```cpp
class Student
{
public:
    std::string name;
    int age;
};
```

## Union

A union allows multiple members to share the same memory location.

### Example

```cpp
union Data
{
    int number;
    float value;
};
```

## Enumeration

Enumeration defines named integer constants.

### Example

```cpp
enum Day
{
    MON,
    TUE,
    WED,
    THU,
    FRI
};
```

# Size of Data Types

The `sizeof()` operator returns the size occupied by a data type or variable in bytes.

### Example

```cpp
#include <iostream>

int main()
{
    std::cout << "Size of int = " << sizeof(int) << " bytes" << std::endl;
    std::cout << "Size of char = " << sizeof(char) << " byte" << std::endl;
    std::cout << "Size of float = " << sizeof(float) << " bytes" << std::endl;
    std::cout << "Size of double = " << sizeof(double) << " bytes" << std::endl;

    return 0;
}
```

### Output
Size of int = 4 bytes
Size of char = 1 byte
Size of float = 4 bytes
Size of double = 8 bytes

### Explanation

- The size of a data type depends on the system architecture and compiler implementation.

# Data Type Modifiers

Modifiers are used to alter the size or range of certain primitive data types.

| Modifier | Purpose |
| --- | --- |
| short | Reduces size |
| long | Increases size |
| signed | Stores positive and negative values |
| unsigned | Stores only non-negative values |

### Example

```cpp
unsigned int population = 1500000;
long int distance = 100000;
```

# Typical Sizes of Primitive Data Types

| Data Type | Typical Size | Range / Description |
| --- | --- | --- |
| bool | 1 byte | `true` or `false` |
| char | 1 byte | Character representation |
| int | 4 bytes | Integer representation |
| float | 4 bytes | Single-precision floating point |
| double | 8 bytes | Double-precision floating point |

# Advantages of Proper Data Types

1. Improve memory efficiency.
2. Increase program performance.
3. Prevent invalid operations.
4. Enhance code readability.
5. Allow proper handling of different kinds of data.

# Limitations

1. Data type sizes may vary across systems.
2. Incorrect type selection may waste memory.
3. Overflow can occur when values exceed the allowed range.
4. Type conversions may lead to loss of precision.

# Summary

Data types in C++ define the nature, size, and range of data stored in variables. They are classified into primitive, derived, and user-defined data types. Primitive types such as int, char, bool, float, double, and void form the basis of data representation, while arrays, pointers, references, structures, classes, unions, and enumerations provide more advanced ways to organize and manipulate data. Understanding data types is essential for writing efficient, reliable, and memory-conscious C++ programs.\n




