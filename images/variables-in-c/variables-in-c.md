# Variables in C

## Introduction

A variable in C is a named memory location used to store data that can be accessed and modified during program execution. Variables make it easier to work with data without needing to remember actual memory addresses. Every variable has a name, a data type, and a value.

C provides several data types such as `int`, `char`, `float`, and `double` to store different kinds of information. Before a variable is used, it must be declared so that the compiler knows what type of data it will contain.

### Key Features

- Variables store values in memory.
- Each variable has a unique name within its scope.
- Variables are associated with a specific data type.
- Values stored in variables can be modified during execution.
- Multiple variables of the same type can be declared in one statement.

# Declaring Variables

To create a variable in C, specify the data type followed by the variable name.

### Syntax

```c
data_type variable_name;
```

### Example

```c
int age;
float percentage;
char grade;
```

# Creating Variables

```c
#include <stdio.h>

int main()
{
    int age = 20;
    float height = 5.8;
    char grade = 'A';

    printf("Age: %d\n", age);
    printf("Height: %.1f\n", height);
    printf("Grade: %c", grade);

    return 0;
}
```

### Output
Age: 20
Height: 5.8
Grade: A

### Explanation

- `age` stores an integer value.
- `height` stores a decimal value.
- `grade` stores a single character.

# Rules for Naming Variables

A variable name must follow these rules:

1. It can contain letters, digits, and underscores.
2. It must begin with an alphabet or underscore.
3. It cannot start with a digit.
4. Spaces are not allowed.
5. Keywords cannot be used as variable names.
6. Variable names are case-sensitive.
7. Variable names should be meaningful and descriptive.

# Variable Initialization

Assigning the first value to a variable is called initialization.

## Initialization During Declaration

```c
#include <stdio.h>

int main()
{
    int marks = 95;
    float cgpa = 9.24;

    printf("%d\n", marks);
    printf("%.2f", cgpa);

    return 0;
}
```

### Output
95
9.24

## Initialization After Declaration

```c
#include <stdio.h>

int main()
{
    char section;

    section = 'B';

    printf("%c", section);

    return 0;
}
```

### Output
B

### Explanation

Variables can be initialized either while declaring them or later using the assignment operator (`=`).

# Accessing Variables

Values stored inside variables can be accessed using their names.

```c
#include <stdio.h>

int main()
{
    int rollNumber = 25;

    printf("%d", rollNumber);

    return 0;
}
```

### Output
25

### Explanation

The variable name acts as a reference to the value stored in memory.

# Updating Variable Values

The value stored inside a variable can be changed at any time.

```c
#include <stdio.h>

int main()
{
    int score = 50;

    printf("Initial Score: %d\n", score);

    score = 80;

    printf("Updated Score: %d\n", score);

    score = score + 10;

    printf("Final Score: %d", score);

    return 0;
}
```

### Output
Initial Score: 50
Updated Score: 80
Final Score: 90

### Explanation

The assignment operator updates the value stored in the variable.

# Using Variables in Expressions

Variables can participate in arithmetic expressions.

```c
#include <stdio.h>

int main()
{
    int a = 30;
    int b = 20;

    int sum = a + b;
    int product = a * b;

    printf("Sum = %d\n", sum);
    printf("Product = %d", product);

    return 0;
}
```

### Output
Sum = 50
Product = 600

### Explanation

The values stored in variables are used during calculations, and the results are stored in other variables.

# Declaring Multiple Variables

Multiple variables of the same data type can be declared in a single statement.

```c
#include <stdio.h>

int main()
{
    int physics = 85, chemistry = 90, mathematics = 95;

    printf("%d %d %d",
           physics,
           chemistry,
           mathematics);

    return 0;
}
```

### Output
85 90 95

# Memory Allocation for Variables

Each variable occupies memory according to its data type.

The `sizeof()` operator can be used to determine the size occupied by a variable.

```c
#include <stdio.h>

int main()
{
    int age = 21;

    printf("%zu bytes", sizeof(age));

    return 0;
}
```

### Output
4 bytes

### Explanation

The actual size depends on the system and compiler, but an integer generally occupies 4 bytes.

# Common Data Types and Their Sizes

| Data Type | Typical Size |
| --- | --- |
| char | 1 byte |
| int | 4 bytes |
| float | 4 bytes |
| double | 8 bytes |
| long int | 8 bytes |

# Declaration vs Definition

| Feature | Declaration | Definition |
| --- | --- | --- |
| Purpose | Tells the compiler that a variable exists | Allocates memory |
| Memory Allocation | No | Yes |
| Example | extern int age; | int age = 20; |

# Advantages of Variables

1. Provide meaningful names for memory locations.
2. Simplify program development.
3. Allow values to be modified dynamically.
4. Improve readability and maintainability.
5. Support arithmetic and logical operations.

# Limitations

1. Uninitialized variables contain garbage values.
2. Incorrect data types may lead to unexpected results.
3. Variables occupy memory resources.
4. Improper naming reduces code readability.

# Summary

Variables are named memory locations used to store and manipulate data in C programs. They enable programmers to work with values efficiently without dealing with actual memory addresses. Every variable has a data type, a name, and a value. Understanding variable declaration, initialization, modification, and memory allocation is essential for writing efficient and maintainable C programs.

