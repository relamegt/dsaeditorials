# Dynamic Memory Allocation in C

## Introduction

Dynamic Memory Allocation (DMA) is the process of allocating and releasing memory during program execution. Unlike static memory allocation, where memory size is fixed at compile time, dynamic memory allocation allows programs to request memory according to their requirements at runtime.

Dynamic memory is allocated from the heap segment and remains available until it is explicitly released by the programmer. This flexibility makes dynamic memory allocation essential for creating variable-sized arrays, linked lists, trees, graphs, and other dynamic data structures.

The C Standard Library provides four functions for dynamic memory management:

- `malloc()`
- `calloc()`
- `realloc()`
- `free()`

These functions are declared in the `<stdlib.h>` header file.

## Why Use Dynamic Memory Allocation?

Dynamic memory allocation provides several advantages:

- Memory can be allocated during execution.
- Array sizes can change dynamically.
- Efficient utilization of memory.
- Suitable for large data structures.
- Memory persists beyond function execution.
- Supports linked lists, trees, and graphs.

# Static vs Dynamic Memory Allocation

| Feature | Static Allocation | Dynamic Allocation |
| --- | --- | --- |
| Allocation Time | Compile Time | Runtime |
| Memory Area | Stack | Heap |
| Size | Fixed | Variable |
| Flexibility | Low | High |
| Release | Automatic | Manual |
| Functions Required | No | Yes |

# malloc()

The `malloc()` function allocates a block of memory of a specified size. The allocated memory contains garbage values because it is not initialized.

### Syntax

```c
void *malloc(size_t size);
```

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(5 * sizeof(int));

    if (ptr == NULL) {

        printf("Memory Allocation Failed");

        return 0;
    }

    for (int i = 0; i < 5; i++) {

        ptr[i] = (i + 1) * 10;
    }

    for (int i = 0; i < 5; i++) {

        printf("%d ", ptr[i]);
    }

    free(ptr);

    return 0;
}
```

### Output
10 20 30 40 50

### Explanation

Memory for five integers is allocated dynamically. Values are stored and printed, and the memory is released using `free()`.

# Using sizeof() with malloc()

Using `sizeof()` makes programs portable across different architectures.

## Example

```c
int *ptr;

ptr = (int *)malloc(sizeof(int) * 10);
```

This allocates memory for ten integers irrespective of the size of an integer on the system.

# Checking Allocation Failure

Memory allocation can fail if sufficient memory is unavailable.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(1000000000 * sizeof(int));

    if (ptr == NULL) {

        printf("Allocation Failed");

        return 0;
    }

    free(ptr);

    return 0;
}
```

### Output
Allocation Failed

### Explanation

`malloc()` returns `NULL` if memory allocation fails.

# calloc()

The `calloc()` function allocates memory and initializes all bytes to zero.

### Syntax

```c
void *calloc(size_t numberOfElements,
             size_t sizeOfElement);
```

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)calloc(5, sizeof(int));

    if (ptr == NULL) {

        printf("Allocation Failed");

        return 0;
    }

    for (int i = 0; i < 5; i++) {

        printf("%d ", ptr[i]);
    }

    free(ptr);

    return 0;
}
```

### Output
0 0 0 0 0

### Explanation

Unlike `malloc()`, memory allocated using `calloc()` is initialized to zero.

# Difference Between malloc() and calloc()

| Feature | malloc() | calloc() |
| --- | --- | --- |
| Initialization | Garbage Values | Zero Initialization |
| Parameters | One | Two |
| Speed | Faster | Slightly Slower |
| Memory Allocation | Single Block | Multiple Blocks |

# free()

The `free()` function releases dynamically allocated memory back to the operating system.

### Syntax

```c
free(pointer);
```

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    *ptr = 100;

    printf("%d\n", *ptr);

    free(ptr);

    ptr = NULL;

    return 0;
}
```

### Output
100

### Explanation

After freeing memory, the pointer is set to `NULL` to avoid dangling pointers.

# realloc()

The `realloc()` function changes the size of previously allocated memory.

### Syntax

```c
void *realloc(void *pointer,
              size_t newSize);
```

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(5 * sizeof(int));

    ptr = (int *)realloc(ptr, 10 * sizeof(int));

    if (ptr == NULL) {

        printf("Reallocation Failed");

        return 0;
    }

    printf("Memory Expanded");

    free(ptr);

    return 0;
}
```

### Output
Memory Expanded

### Explanation

The memory block originally containing space for five integers is expanded to hold ten integers.

# Safe Usage of realloc()

Using a temporary pointer prevents memory leaks.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(5 * sizeof(int));

    int *temp;

    temp = (int *)realloc(ptr, 10 * sizeof(int));

    if (temp != NULL) {

        ptr = temp;
    }

    free(ptr);

    return 0;
}
```

### Explanation

If `realloc()` fails, the original pointer remains valid.

# Creating a Dynamic Array

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int n = 5;

    int *marks;

    marks = (int *)malloc(n * sizeof(int));

    for (int i = 0; i < n; i++) {

        marks[i] = (i + 1) * 5;
    }

    for (int i = 0; i < n; i++) {

        printf("%d ", marks[i]);
    }

    free(marks);

    return 0;
}
```

### Output
5 10 15 20 25

# Dynamic Memory with Student Marks

Suppose Akash Dangudubiyyapu wants to store marks of Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *marks;

    marks = (int *)malloc(5 * sizeof(int));

    marks[0] = 90;
    marks[1] = 85;
    marks[2] = 88;
    marks[3] = 92;
    marks[4] = 95;

    for (int i = 0; i < 5; i++) {

        printf("%d ", marks[i]);
    }

    free(marks);

    return 0;
}
```

### Output
90 85 88 92 95

# Memory Leak

A memory leak occurs when dynamically allocated memory is not released.

## Incorrect Example

```c
int *ptr;

ptr = (int *)malloc(sizeof(int));

ptr = NULL;
```

Here, allocated memory becomes inaccessible because it is never freed.

## Correct Example

```c
free(ptr);

ptr = NULL;
```

# Dangling Pointer

A dangling pointer refers to memory that has already been deallocated.

## Example

```c
int *ptr;

ptr = (int *)malloc(sizeof(int));

free(ptr);
```

After calling `free()`, the pointer becomes invalid.

Setting it to `NULL` prevents accidental access.

# Common Errors in Dynamic Memory Allocation

1. Memory leaks.
2. Dangling pointers.
3. Double freeing memory.
4. Accessing memory beyond allocated size.
5. Forgetting to check for `NULL`.
6. Using freed memory.

# Applications of Dynamic Memory Allocation

Dynamic memory allocation is used in:

1. Linked lists.
2. Trees.
3. Graphs.
4. Dynamic arrays.
5. Queues.
6. Stacks.
7. File systems.
8. Operating systems.
9. Databases.
10. Compiler design.

# Advantages of Dynamic Memory Allocation

1. Efficient memory utilization.
2. Flexible memory size.
3. Suitable for dynamic data structures.
4. Memory persists after function completion.
5. Supports runtime memory management.
6. Reduces memory wastage.

# Limitations of Dynamic Memory Allocation

1. Requires manual memory management.
2. Memory leaks may occur.
3. Incorrect usage causes segmentation faults.
4. Allocation and deallocation are slower than stack memory.
5. Heap fragmentation may occur.

# Summary

Dynamic memory allocation in C allows memory to be allocated, resized, and released during program execution. The functions `malloc()`, `calloc()`, `realloc()`, and `free()` provide powerful mechanisms for managing memory dynamically. Proper use of these functions enables efficient memory utilization and supports advanced data structures, while improper usage may lead to memory leaks, dangling pointers, and undefined behavior. Understanding dynamic memory allocation is essential for mastering C programming and system-level software development.

