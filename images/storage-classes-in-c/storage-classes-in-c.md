# Storage Classes in C

## Introduction

Storage classes in C determine the lifetime, scope, visibility, and storage location of variables and functions. They specify where a variable is stored, how long it exists during program execution, and where it can be accessed.

The four storage classes in C are:

- `auto`
- `static`
- `register`
- `extern`

## Why Storage Classes are Needed?

Storage classes help to:

- Control variable scope.
- Define variable lifetime.
- Manage memory efficiently.
- Share variables among files.
- Preserve values when required.

## Types of Storage Classes

| Storage Class | Scope | Default Value | Memory Location | Lifetime |
| --- | --- | --- | --- | --- |
| auto | Local | Garbage value | Stack (RAM) | Until block ends |
| static | Local/Global | 0 | Data Segment | Entire program |
| register | Local | Garbage value | CPU Register or RAM | Until block ends |
| extern | Global | 0 | Data Segment | Entire program |

# auto Storage Class

The `auto` storage class is the default for all local variables declared inside functions or blocks.

## Properties

- Scope: Local
- Default value: Garbage value
- Memory location: Stack
- Lifetime: Till the end of the block

## Example

```c
#include <stdio.h>

int main() {

    auto int number = 25;

    printf("%d", number);

    return 0;
}
```

### Output
25

### Explanation

`number` is a local variable. Since local variables are automatically of type `auto`, explicitly writing `auto` is optional.

## Characteristics

- Exists only inside the block.
- Created when the block starts.
- Destroyed when the block ends.

# static Storage Class

A static variable retains its value between function calls. It is initialized only once and remains in memory throughout the execution of the program.

## Properties

- Scope: Local or Global
- Default value: 0
- Memory location: Data segment
- Lifetime: Entire program

## Example

```c
#include <stdio.h>

void counter() {

    static int count = 0;

    count++;

    printf("Count = %d\n", count);
}

int main() {

    counter();
    counter();
    counter();

    return 0;
}
```

### Output
Count = 1
Count = 2
Count = 3

### Explanation

The variable `count` is initialized only once. Its value is preserved after each function call.

## Characteristics

- Value is retained between function calls.
- Initialized only once.
- Exists until program termination.

# register Storage Class

The `register` storage class suggests the compiler store a variable in a CPU register for faster access.

## Properties

- Scope: Local
- Default value: Garbage value
- Memory location: CPU register or RAM
- Lifetime: Till the end of the block

## Example

```c
#include <stdio.h>

int main() {

    register int i;

    for (i = 1; i <= 5; i++) {
        printf("%d ", i);
    }

    return 0;
}
```

### Output
1 2 3 4 5

### Explanation

The compiler attempts to place variable `i` in a CPU register for faster execution. However, the compiler may ignore this request if registers are unavailable.

## Characteristics

- Used for frequently accessed variables.
- Faster access compared to memory variables.
- Address operator (`&`) cannot be used with register variables.

### Invalid Example

```c
#include <stdio.h>

int main() {

    register int number = 10;

    printf("%p", &number);

    return 0;
}
```

### Output
Compilation Error

### Explanation

Register variables do not have a guaranteed memory address, so the address operator cannot be applied.

# extern Storage Class

The `extern` storage class indicates that a variable or function is defined elsewhere and can be accessed from multiple source files.

## Properties

- Scope: Global
- Default value: 0
- Memory location: Data segment
- Lifetime: Entire program

## Example

### file1.c

```c
int totalStudents = 150;
```

### file2.c

```c
#include <stdio.h>

extern int totalStudents;

int main() {

    printf("%d", totalStudents);

    return 0;
}
```

### Output
150

### Explanation

`extern` informs the compiler that the variable is defined in another file. The linker combines both files during compilation.

### Compilation Command

```bash
gcc file1.c file2.c -o program
```

## Characteristics

- Used for sharing variables among files.
- Does not allocate memory.
- Refers to an existing variable.

# Comparison of Storage Classes

| Feature | auto | static | register | extern |
| --- | --- | --- | --- | --- |
| Scope | Local | Local/Global | Local | Global |
| Lifetime | Block execution | Entire program | Block execution | Entire program |
| Default Value | Garbage | 0 | Garbage | 0 |
| Memory Location | Stack | Data segment | Register or RAM | Data segment |
| Value Retained | No | Yes | No | Yes |
| Address Operator Allowed | Yes | Yes | No | Yes |

# Memory Representation

```Code
Stack
 ├── auto variables
 └── register variables

Data Segment
 ├── static variables
 └── extern variables
```

# Advantages of Storage Classes

- Controls variable visibility.
- Optimizes memory usage.
- Allows sharing variables among files.
- Preserves variable values when needed.
- Improves program organization.

# Limitations

- Incorrect use of `extern` may cause linker errors.
- Register allocation depends on the compiler.
- Static variables occupy memory throughout program execution.
- Excessive use of global variables reduces modularity.

# Summary

Storage classes in C define the scope, lifetime, visibility, and memory location of variables. The `auto` storage class is the default for local variables, `static` preserves values throughout program execution, `register` suggests faster access through CPU registers, and `extern` allows variables and functions to be shared across multiple source files. Proper use of storage classes helps in writing efficient, organized, and maintainable C programs.

