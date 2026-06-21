# Memory Leak in C

## Introduction

A memory leak occurs when dynamically allocated memory is not released after it is no longer needed. In C, memory allocated using functions such as `malloc()`, `calloc()`, or `realloc()` resides in the heap segment and remains occupied until it is explicitly released using `free()`.

If a program continuously allocates memory without freeing it, the amount of available memory gradually decreases. Over time, this can slow down the application, increase memory usage, and eventually lead to program crashes or system instability.

Memory leaks are especially dangerous in long-running programs such as web servers, databases, operating systems, and embedded systems.

## Why Do Memory Leaks Occur?

Memory leaks generally occur because:

- Dynamically allocated memory is never released.
- The pointer to allocated memory is lost.
- A pointer is overwritten before freeing the old memory.
- Improper use of dynamic memory functions.
- Exceptions or unexpected program termination prevent cleanup.

# Dynamic Memory Allocation Recap

Memory allocated using the following functions must be released manually:

| Allocation Function | Release Function |
| --- | --- |
| malloc() | free() |
| calloc() | free() |
| realloc() | free() |

Failure to call `free()` results in memory leaks.

# Example of Memory Leak

Consider the following program.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    *ptr = 100;

    printf("%d", *ptr);

    return 0;
}
```

### Output
100

### Problem

The memory allocated using `malloc()` is never released. When the program terminates, the operating system may reclaim the memory, but in long-running applications this leads to memory leaks.

# Correct Program

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

The allocated memory is released using `free()`, preventing memory leaks.

# Common Causes of Memory Leaks

## 1. Forgetting to Call free()

### Example

```c
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    return 0;
}
```

### Problem

Memory is allocated but never released.

---

## 2. Losing Pointer Reference

### Example

```c
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    ptr = NULL;

    return 0;
}
```

### Problem

The original address is lost and cannot be freed.

---

## 3. Overwriting Existing Pointer

### Example

```c
#include <stdlib.h>

int main() {

    int *ptr;

    ptr = (int *)malloc(sizeof(int));

    ptr = (int *)malloc(sizeof(int));

    return 0;
}
```

### Problem

The first memory block becomes inaccessible, causing a leak.

---

## 4. Incorrect Use of realloc()

### Example

```c
ptr = realloc(ptr, newSize);
```

If `realloc()` fails, it returns `NULL`, causing the original pointer to be lost.

### Safer Approach

```c
temp = realloc(ptr, newSize);

if (temp != NULL) {

    ptr = temp;
}
```

# Real-Life Example

Suppose Akash Dangudubiyyapu develops a student management system for Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

For every student record, memory is allocated dynamically.

```c
student = malloc(sizeof(Student));
```

If the records are deleted but `free(student)` is not called, memory usage continuously increases. After handling thousands of students, the application may consume excessive memory and eventually crash.

# Memory Leak Inside Loops

## Incorrect Program

```c
#include <stdlib.h>

int main() {

    while (1) {

        int *ptr;

        ptr = (int *)malloc(sizeof(int));
    }

    return 0;
}
```

### Problem

New memory is allocated repeatedly, but none is freed.

This causes memory consumption to increase indefinitely.

## Correct Program

```c
#include <stdlib.h>

int main() {

    while (1) {

        int *ptr;

        ptr = (int *)malloc(sizeof(int));

        free(ptr);
    }

    return 0;
}
```

# Memory Leak with Arrays

## Incorrect Program

```c
#include <stdlib.h>

int main() {

    int *arr;

    arr = (int *)malloc(10 * sizeof(int));

    return 0;
}
```

### Problem

Array memory is never released.

## Correct Program

```c
#include <stdlib.h>

int main() {

    int *arr;

    arr = (int *)malloc(10 * sizeof(int));

    free(arr);

    arr = NULL;

    return 0;
}
```

# How to Avoid Memory Leaks?

## 1. Always Use free()

Whenever memory is allocated, ensure that it is eventually released.

```c
free(ptr);
```

---

## 2. Set Pointer to NULL

After freeing memory:

```c
free(ptr);

ptr = NULL;
```

This prevents dangling pointers.

---

## 3. Avoid Overwriting Pointers

Incorrect:

```c
ptr = malloc(sizeof(int));

ptr = malloc(sizeof(int));
```

Correct:

```c
free(ptr);

ptr = malloc(sizeof(int));
```

---

## 4. Use Temporary Pointer with realloc()

```c
temp = realloc(ptr, newSize);

if (temp != NULL) {

    ptr = temp;
}
```

---

## 5. Release Memory Before Program Exit

Before terminating the program, free all allocated memory blocks.

# Detecting Memory Leaks

Several tools help identify memory leaks.

| Tool | Platform |
| --- | --- |
| Valgrind | Linux |
| AddressSanitizer | GCC, Clang |
| Visual Studio Diagnostic Tools | Windows |
| Dr. Memory | Cross Platform |

# Memory Leak vs Dangling Pointer

| Feature | Memory Leak | Dangling Pointer |
| --- | --- | --- |
| Cause | Memory not freed | Memory freed but pointer still exists |
| Memory Status | Occupied | Released |
| Accessibility | Lost | Invalid |
| Effect | High memory usage | Undefined behavior |
| Solution | free() | Set pointer to NULL |

# Consequences of Memory Leaks

1. Increased memory consumption.
2. Reduced system performance.
3. Application slowdown.
4. Program crashes.
5. System instability.
6. Resource exhaustion.
7. Poor user experience.

# Advantages of Proper Memory Management

1. Better performance.
2. Efficient memory usage.
3. Increased application stability.
4. Prevention of crashes.
5. Improved reliability.
6. Reduced resource wastage.

# Best Practices

1. Pair every `malloc()` with `free()`.
2. Pair every `calloc()` with `free()`.
3. Pair every successful `realloc()` with `free()`.
4. Set pointers to `NULL` after freeing.
5. Use temporary pointers during reallocation.
6. Check allocation failures.
7. Test programs with memory debugging tools.

# Summary

A memory leak occurs when dynamically allocated memory is not released after use. In C, memory obtained using `malloc()`, `calloc()`, or `realloc()` must be explicitly released using `free()`. Memory leaks gradually consume available memory and can cause performance degradation or application crashes. Proper memory management practices, careful pointer handling, and debugging tools help programmers write efficient and reliable C programs.

