# Keywords in C

## Introduction

Keywords in C are predefined words that have special meanings recognized by the compiler. They are fundamental components of the C language syntax and are used to define data types, control program flow, manage memory, and perform other important operations. Since keywords already have reserved meanings, they cannot be used as variable names, function names, structure names, or any other identifiers.

Different versions of the C standard introduce additional keywords, but the core concept remains the same: keywords help the compiler understand the structure and behavior of a program.

### Key Features

- Keywords have predefined meanings in the C language.
- They are reserved words recognized by the compiler.
- Keywords cannot be used as identifiers.
- C is case-sensitive, so `if` and `IF` are treated differently.
- Various keywords are used for data types, loops, storage classes, and user-defined types.

# Why Use Keywords?

Keywords form the building blocks of C programs. They allow programmers to declare variables, control execution flow, define custom data types, and manage storage efficiently.

Without keywords, the compiler would not be able to interpret the instructions written by the programmer.

# Example of Keywords

The following program demonstrates the use of several keywords:

```c
#include <stdio.h>

int main()
{
    int marks = 95;

    if (marks >= 50)
    {
        printf("Result: Pass");
    }
    else
    {
        printf("Result: Fail");
    }

    return 0;
}
```

### Output
Result: Pass

### Explanation

In the above program:

- `int` specifies an integer data type.
- `if` checks whether the condition is true.
- `else` executes when the condition is false.
- `return` terminates the function and returns control to the operating system.

# Important Points About Keywords

- Keywords are reserved words and have predefined meanings.
- They cannot be used as variable names or function names.
- C is case-sensitive.
- The number of keywords varies depending on the C standard.
- ANSI C (C89/C90) defines 32 keywords.
- Modern standards such as C99, C11, and C23 introduce additional keywords.

# What Happens If We Use a Keyword as an Identifier?

Attempting to use a keyword as a variable name produces a compilation error.

## Example

```c
#include <stdio.h>

int main()
{
    int return = 10;

    printf("%d", return);

    return 0;
}
```

### Output
Compilation Error

### Explanation

`return` is a reserved keyword in C. Since it already has a predefined meaning, it cannot be used as a variable name.

# Categories of Keywords in C

## 1. Data Type Keywords

These keywords are used to specify the type of data stored in variables.

| Keyword | Description |
| --- | --- |
| char | Stores a character value |
| int | Stores integer values |
| float | Stores single-precision decimal values |
| double | Stores double-precision decimal values |
| void | Represents no value |
| short | Represents short integers |
| long | Represents long integers |
| signed | Represents signed values |
| unsigned | Represents unsigned values |

### Example

```c
#include <stdio.h>

int main()
{
    int age = 21;
    float percentage = 92.5;

    printf("%d\n", age);
    printf("%.1f", percentage);

    return 0;
}
```

### Output
21
92.5

# 2. Control Flow Keywords

These keywords determine the order of execution of statements.

| Keyword | Purpose |
| --- | --- |
| if | Executes code conditionally |
| else | Executes alternative statements |
| switch | Selects among multiple choices |
| case | Defines a branch inside switch |
| default | Executes if no case matches |
| for | Creates a loop |
| while | Repeats while a condition is true |
| do | Executes loop at least once |
| break | Terminates loop or switch |
| continue | Skips current iteration |
| goto | Transfers control to another statement |
| return | Exits a function |

### Example

```c
#include <stdio.h>

int main()
{
    int i;

    for (i = 1; i <= 3; i++)
    {
        printf("%d ", i);
    }

    return 0;
}
```

### Output
1 2 3

# 3. Storage Class Keywords

These keywords control the lifetime and visibility of variables.

| Keyword | Description |
| --- | --- |
| auto | Local variable storage |
| register | Suggests storage in CPU register |
| static | Preserves value between function calls |
| extern | Refers to variables defined elsewhere |

### Example

```c
static int count = 0;
```

# 4. User-Defined Type Keywords

These keywords help create custom data types.

| Keyword | Description |
| --- | --- |
| struct | Defines structures |
| union | Defines unions |
| enum | Defines enumerations |
| typedef | Creates aliases for existing types |

### Example

```c
struct Student
{
    int rollNo;
    char grade;
};
```

# 5. Qualifier Keywords

These keywords modify the behavior of variables.

| Keyword | Description |
| --- | --- |
| const | Creates read-only variables |
| volatile | Indicates unexpected changes |
| restrict | Provides exclusive pointer access |

### Example

```c
const float PI = 3.14159;
```

# 6. Utility Keywords

These keywords perform special operations.

| Keyword | Description |
| --- | --- |
| sizeof | Returns memory size in bytes |

### Example

```c
#include <stdio.h>

int main()
{
    printf("%lu", sizeof(int));

    return 0;
}
```

### Output
4

# Commonly Used Keywords

Some frequently used keywords include:

```text
int
float
char
double
void
if
else
switch
case
for
while
do
break
continue
return
struct
union
enum
typedef
static
extern
const
sizeof
```

# Difference Between Keywords and Identifiers

| Feature | Keywords | Identifiers |
| --- | --- | --- |
| Meaning | Reserved words | User-defined names |
| Purpose | Define language syntax | Name variables and functions |
| Modification | Fixed | User-defined |
| Quantity | Limited | Unlimited |
| Examples | int, return, if | marks, totalSalary, calculateSum |

# Advantages of Keywords

1. Provide standard syntax for programming.
2. Make programs easier to understand.
3. Help the compiler interpret instructions correctly.
4. Enable structured and efficient coding.
5. Support control flow, data types, and memory management.

# Limitations

1. Keywords cannot be used as identifiers.
2. Beginners may find many keywords difficult to memorize.
3. Some keywords are rarely used in practical programs.

# Summary

Keywords are reserved words that form the foundation of the C programming language. They provide predefined instructions for data types, loops, conditional statements, storage classes, and user-defined types. Since keywords have special meanings, they cannot be used as identifiers. Understanding keywords is essential because they define the syntax and behavior of every C program and help programmers write structured and efficient code.

