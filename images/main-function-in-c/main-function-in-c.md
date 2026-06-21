# main Function in C

## Introduction

The `main()` function is the entry point of every C program. Program execution begins from this function, and when the `main()` function finishes execution, the program terminates.

Every C program must contain exactly one `main()` function. It acts as the bridge between the operating system and the user-defined code. The operating system invokes `main()`, and the statements inside it are executed sequentially.

### Key Features

- Execution of a C program starts from `main()`.
- Every C program must contain one `main()` function.
- It can accept command-line arguments.
- It usually returns an integer value to the operating system.
- Returning `0` indicates successful execution.

# Basic Example

```c
#include <stdio.h>

int main()
{
    printf("Welcome to AlphaKnowledge");

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The operating system calls `main()`, which prints the message and returns `0`, indicating successful execution.

# Why is main() Necessary?

If a program does not contain the `main()` function, the compiler cannot determine where execution should begin.

## Example Without main()

```c
#include <stdio.h>

void display()
{
    printf("Hello");
}
```

### Output
Undefined reference to main
Compilation failed

### Explanation

Since there is no `main()` function, the linker cannot find the starting point of the program.

# Syntax of main()

There are two commonly used forms of the `main()` function.

## Without Command-Line Arguments

```c
int main()
{
    // statements

    return 0;
}
```

or

```c
int main(void)
{
    // statements

    return 0;
}
```

## With Command-Line Arguments

```c
int main(int argc, char *argv[])
{
    // statements

    return 0;
}
```

# Components of main()

## Return Type

The return type specifies the type of value returned to the operating system.

```c
int main()
```

The `int` return type is recommended by the C standard.

## Function Name

The function name must be `main`.

```c
main()
```

Program execution always starts from this function.

## Parameters

Parameters allow the operating system to pass information to the program.

```c
int argc, char *argv[]
```

- `argc` stores the number of command-line arguments.
- `argv` stores the arguments themselves.

## Return Statement

```c
return 0;
```

Returning `0` indicates successful execution.

# Types of main() in C

There are three commonly encountered forms.

## 1. main() with int Return Type

This is the recommended and standard form.

### Example

```c
#include <stdio.h>

int main()
{
    printf("Programming in C");

    return 0;
}
```

### Output
Programming in C

### Explanation

The function prints a message and returns `0`.

# 2. main() with void Return Type

Some compilers support `void main()`, but it is not recommended because it violates the C standard.

## Example

```c
#include <stdio.h>

void main()
{
    printf("Learning C");
}
```

### Output
Learning C

### Explanation

Although some compilers allow this form, using `int main()` is preferred.

# 3. main() with Command-Line Arguments

Command-line arguments allow users to pass information when executing the program.

## Syntax

```c
int main(int argc, char *argv[])
```

### Meaning

- `argc` → Argument Count
- `argv` → Argument Vector

## Example

```c
#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Total Arguments = %d\n", argc);

    for (int i = 0; i < argc; i++)
    {
        printf("%s\n", argv[i]);
    }

    return 0;
}
```

Suppose the program is executed as:

```input
program Akash Mohit Abhiram
```

### Output
Total Arguments = 4
program
Akash
Mohit
Abhiram

### Explanation

The program name itself is counted as the first argument.

# Return Values of main()

The return value informs the operating system about program execution status.

| Return Value | Meaning |
| --- | --- |
| 0 | Successful execution |
| Non-zero value | Error or abnormal termination |

## Example

```c
#include <stdio.h>

int main()
{
    printf("Program Executed Successfully");

    return 0;
}
```

### Output
Program Executed Successfully

# Execution Flow of main()

```text
Operating System
        ↓
     main()
        ↓
Statements Execute
        ↓
return 0
        ↓
Program Terminates
```

# Important Points

- There can be only one `main()` function in a C program.
- Program execution always begins with `main()`.
- `int main()` is the standard form.
- The operating system calls `main()`.
- Returning `0` indicates successful execution.
- Command-line arguments are received through `argc` and `argv`.

# Advantages of main()

1. Provides a well-defined entry point.
2. Communicates execution status to the operating system.
3. Supports command-line arguments.
4. Improves program structure.
5. Makes program execution standardized.

# Limitations

1. Only one `main()` function is allowed.
2. Program execution cannot start from another function.
3. Non-standard forms like `void main()` are compiler-dependent.
4. Command-line arguments may be difficult for beginners to understand.

# Summary

The `main()` function is the starting point of every C program. It is invoked by the operating system and controls the execution of the program. The standard form `int main()` is recommended because it returns an execution status to the operating system. The `main()` function can also accept command-line arguments using `argc` and `argv`, allowing users to pass external data to the program. Understanding the role and structure of `main()` is essential because every C program begins and ends through this function.

