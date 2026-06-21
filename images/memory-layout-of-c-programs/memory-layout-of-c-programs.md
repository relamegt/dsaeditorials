# Memory Layout of C Programs

## Introduction

When a C program executes, the operating system allocates memory to different parts of the program. This organization of memory is known as the memory layout of a C program. Understanding memory layout helps programmers manage memory efficiently, optimize performance, and avoid issues such as memory leaks, stack overflow, and segmentation faults.

The memory of a running C program is generally divided into the following segments:

- Text Segment
- Initialized Data Segment
- Uninitialized Data Segment (BSS)
- Heap Segment
- Stack Segment

Each segment has a specific purpose and behaves differently during program execution.

## Overall Memory Layout

A typical memory organization looks like:

```text
--------------------------
|        Stack           |
|   (Local Variables)    |
|         ↓              |
--------------------------
|                         |
|       Free Space        |
|                         |
--------------------------
|         Heap            |
|  (Dynamic Allocation)   |
|         ↑               |
--------------------------
|     BSS Segment         |
| (Uninitialized Data)    |
--------------------------
| Initialized Data        |
| (Global & Static Data)  |
--------------------------
|      Text Segment       |
|  (Program Instructions) |
--------------------------
```

# Why Understand Memory Layout?

Understanding memory layout helps in:

- Efficient memory utilization.
- Debugging segmentation faults.
- Preventing memory leaks.
- Understanding dynamic memory allocation.
- Writing optimized programs.
- Learning system programming concepts.

# Text Segment

The text segment, also called the code segment, contains executable instructions of the program.

### Characteristics

- Stores compiled machine instructions.
- Usually read-only.
- Shared among multiple processes.
- Size depends on the program code.

## Example

```c
#include <stdio.h>

void display() {

    printf("Welcome to AlphaKnowledge");

}

int main() {

    display();

    return 0;
}
```

### Explanation

The machine instructions corresponding to `main()` and `display()` are stored in the text segment.

# Initialized Data Segment

This segment stores global and static variables that are initialized by the programmer.

### Characteristics

- Stores initialized global variables.
- Stores initialized static variables.
- Values remain throughout program execution.

## Example

```c
#include <stdio.h>

int totalStudents = 100;

int main() {

    static int passCount = 80;

    printf("%d\n", totalStudents);

    printf("%d", passCount);

    return 0;
}
```

### Output
100
80

### Explanation

Both variables are initialized before execution and remain available until the program terminates.

# Uninitialized Data Segment (BSS)

The BSS segment stores global and static variables that are declared without initialization.

These variables are automatically initialized to zero.

### Characteristics

- Stores uninitialized global variables.
- Stores uninitialized static variables.
- Variables are initialized to zero by the system.

## Example

```c
#include <stdio.h>

int count;

int main() {

    static int marks;

    printf("%d\n", count);

    printf("%d", marks);

    return 0;
}
```

### Output
0
0

### Explanation

Although no values are assigned, both variables contain zero because they belong to the BSS segment.

# Heap Segment

The heap is used for dynamic memory allocation during runtime.

Functions used:

- malloc()
- calloc()
- realloc()
- free()

### Characteristics

- Grows upward.
- Managed manually by the programmer.
- Memory persists until explicitly released.
- Shared among functions.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    *ptr = 95;

    printf("%d", *ptr);

    free(ptr);

    return 0;
}
```

### Output
95

### Explanation

Memory is allocated dynamically using `malloc()` and released using `free()`.

# Stack Segment

The stack stores:

- Local variables.
- Function parameters.
- Return addresses.
- Temporary data.

### Characteristics

- Grows downward.
- Managed automatically.
- Memory is released when functions terminate.
- Faster than heap memory.

## Example

```c
#include <stdio.h>

void display() {

    int marks = 90;

    printf("%d", marks);

}

int main() {

    display();

    return 0;
}
```

### Output
90

### Explanation

The variable `marks` exists only while the function `display()` is executing.

# Memory Layout Example

Consider the following program.

```c
#include <stdio.h>
#include <stdlib.h>

int totalStudents = 500;

int uninitializedVariable;

void show() {

    int localVar = 20;

    printf("%d", localVar);

}

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    *ptr = 50;

    show();

    free(ptr);

    return 0;
}
```

### Memory Distribution

| Variable/Function | Segment |
| --- | --- |
| show() | Text Segment |
| main() | Text Segment |
| totalStudents | Initialized Data Segment |
| uninitializedVariable | BSS Segment |
| ptr allocated memory | Heap Segment |
| localVar | Stack Segment |

# Stack vs Heap

| Feature | Stack | Heap |
| --- | --- | --- |
| Allocation | Automatic | Manual |
| Speed | Faster | Slower |
| Memory Size | Limited | Large |
| Lifetime | Function Scope | Until free() |
| Management | Compiler | Programmer |
| Direction | Downward | Upward |

# Initialized Data vs BSS Segment

| Feature | Initialized Data Segment | BSS Segment |
| --- | --- | --- |
| Initialization | User Initialized | Automatically Zero |
| Variables | Global and Static | Global and Static |
| Lifetime | Entire Program | Entire Program |
| Memory Allocation | During Program Load | During Program Load |

# Verifying Memory Layout Using Addresses

Different segments occupy different address ranges.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int globalVar = 66;

int uninitializedVar;

void display() {

    int localVar = 10;

    printf("Local Variable Address: %p\n", &localVar);

}

int main() {

    int *ptr = (int *)malloc(sizeof(int));

    printf("Function Address: %p\n", display);

    printf("Global Variable Address: %p\n", &globalVar);

    printf("BSS Variable Address: %p\n", &uninitializedVar);

    printf("Heap Address: %p\n", ptr);

    display();

    free(ptr);

    return 0;
}
```

### Output
Function Address: Different Address
Global Variable Address: Different Address
BSS Variable Address: Different Address
Heap Address: Different Address
Local Variable Address: Different Address

### Explanation

Each segment occupies different memory locations, so the addresses vary.

# Growth of Heap and Stack

```text
Higher Addresses
-----------------
|     Stack      |
|        ↓        |
-----------------
|   Free Space    |
-----------------
|        ↑        |
|      Heap       |
-----------------
|      BSS        |
-----------------
| Initialized Data|
-----------------
|   Text Segment  |
-----------------
Lower Addresses
```

The stack grows downward while the heap grows upward.

# Real-Life Example

Suppose Akash Dangudubiyyapu develops a student management system for Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

- Program instructions are stored in the Text Segment.
- Global student count is stored in the Data Segment.
- Uninitialized attendance variables are stored in the BSS Segment.
- Dynamically allocated student records reside in the Heap.
- Local variables inside functions are placed in the Stack.

This organization helps the operating system efficiently manage memory during execution.

# Advantages of Memory Segmentation

1. Organizes program memory efficiently.
2. Improves execution speed.
3. Enables dynamic memory allocation.
4. Prevents accidental code modification.
5. Supports recursion using stack frames.
6. Simplifies memory management.

# Common Errors Related to Memory Layout

1. Stack Overflow.
2. Memory Leaks.
3. Segmentation Fault.
4. Dangling Pointers.
5. Double Free Errors.
6. Buffer Overflow.

# Summary

The memory layout of a C program divides memory into multiple segments, including the Text Segment, Initialized Data Segment, BSS Segment, Heap Segment, and Stack Segment. Each segment has a distinct purpose and behaves differently during program execution. Understanding memory layout is essential for dynamic memory management, debugging, optimization, and advanced topics such as operating systems and system programming.

