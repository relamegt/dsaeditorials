# Pointer to Pointer in C

## Introduction

A pointer in C stores the address of a variable. Similarly, a pointer to pointer, also known as a double pointer, stores the address of another pointer. Since one pointer refers to another pointer, double pointers are often called multilevel pointers.

Double pointers are useful when working with dynamic memory allocation, arrays of strings, linked data structures, and functions that need to modify pointer variables.

A single pointer uses one asterisk (`*`) whereas a double pointer uses two asterisks (`**`).

```text
Variable  ←  Pointer  ←  Double Pointer
```

## Why Use Double Pointers?

Double pointers provide several advantages:

- Allow manipulation of pointer variables inside functions.
- Used in dynamic allocation of multidimensional arrays.
- Help manage arrays of strings.
- Simplify operations on linked data structures.
- Support multilevel memory references.

# Understanding Pointer to Pointer

Consider the following memory relationship:

```text
Value → Variable → Pointer → Double Pointer

50    → marks    → ptr    → dptr
```

- `marks` stores the actual value.
- `ptr` stores the address of `marks`.
- `dptr` stores the address of `ptr`.

## Example

```c
#include <stdio.h>

int main() {

    int marks = 95;

    int *ptr = &marks;

    int **dptr = &ptr;

    printf("%d\n", marks);

    printf("%d\n", *ptr);

    printf("%d", **dptr);

    return 0;
}
```

### Output
95
95
95

### Explanation

- `marks` contains the actual value.
- `*ptr` accesses the value stored in `marks`.
- `**dptr` first accesses `ptr`, then accesses the value stored by `ptr`.

# Address Representation

## Example

```c
#include <stdio.h>

int main() {

    int age = 21;

    int *ptr = &age;

    int **dptr = &ptr;

    printf("%p\n", &age);

    printf("%p\n", ptr);

    printf("%p", *dptr);

    return 0;
}
```

### Output
Address of age
Address of age
Address of age

### Explanation

All three expressions refer to the same memory location containing the variable `age`.

# Size of Double Pointer

A double pointer stores an address just like an ordinary pointer. Therefore, their sizes are generally equal on a given machine.

## Example

```c
#include <stdio.h>

int main() {

    int salary = 50000;

    int *ptr = &salary;

    int **dptr = &ptr;

    printf("%zu\n", sizeof(ptr));

    printf("%zu", sizeof(dptr));

    return 0;
}
```

### Output
8
8

### Explanation

On a 64-bit system, both pointers occupy 8 bytes. On other architectures, the size may vary.

# Accessing Data Using Double Pointer

A double pointer can indirectly access the original variable.

## Example

```c
#include <stdio.h>

int main() {

    int score = 80;

    int *ptr = &score;

    int **dptr = &ptr;

    printf("%d", **dptr);

    return 0;
}
```

### Output
80

### Explanation

`**dptr` first dereferences `dptr` to obtain `ptr`, then dereferences `ptr` to obtain the value stored in `score`.

# Modifying Variables Through Double Pointer

Double pointers can change the value of a variable indirectly.

## Example

```c
#include <stdio.h>

int main() {

    int number = 25;

    int *ptr = &number;

    int **dptr = &ptr;

    **dptr = 100;

    printf("%d", number);

    return 0;
}
```

### Output
100

### Explanation

Changing `**dptr` modifies the original variable because all references ultimately point to the same memory location.

# Pointer to Pointer with Character Variables

## Example

```c
#include <stdio.h>

int main() {

    char grade = 'A';

    char *ptr = &grade;

    char **dptr = &ptr;

    printf("%c", **dptr);

    return 0;
}
```

### Output
A

# Passing Pointer to Function

Double pointers are useful when a function needs to modify a pointer variable.

## Example

```c
#include <stdio.h>

void update(int **p) {

    static int value = 200;

    *p = &value;
}

int main() {

    int marks = 100;

    int *ptr = &marks;

    update(&ptr);

    printf("%d", *ptr);

    return 0;
}
```

### Output
200

### Explanation

The function receives the address of the pointer and changes where that pointer points.

# Dynamic Memory Allocation Using Double Pointer

Double pointers are commonly used to create dynamic two-dimensional arrays.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int rows = 2;
    int cols = 3;

    int **matrix;

    matrix = (int **)malloc(rows * sizeof(int *));

    for (int i = 0; i < rows; i++) {

        matrix[i] = (int *)malloc(cols * sizeof(int));
    }

    int value = 1;

    for (int i = 0; i < rows; i++) {

        for (int j = 0; j < cols; j++) {

            matrix[i][j] = value++;

        }
    }

    for (int i = 0; i < rows; i++) {

        for (int j = 0; j < cols; j++) {

            printf("%d ", matrix[i][j]);

        }

        printf("\n");
    }

    for (int i = 0; i < rows; i++) {

        free(matrix[i]);
    }

    free(matrix);

    return 0;
}
```

### Output
1 2 3
4 5 6

### Explanation

The first level stores row addresses, and each row contains dynamically allocated columns.

# Array of Strings Using Double Pointer

Arrays of strings are internally arrays of character pointers.

## Example

```c
#include <stdio.h>

void display(char **names, int n) {

    for (int i = 0; i < n; i++) {

        printf("%s\n", names[i]);
    }
}

int main() {

    char *students[] = {

        "Akash Dangudubiyyapu",
        "Mohit Chandaluri",
        "Abhiram Gopisetti"
    };

    display(students, 3);

    return 0;
}
```

### Output
Akash Dangudubiyyapu
Mohit Chandaluri
Abhiram Gopisetti

### Explanation

Each element of the array stores the address of a string, and the function receives those addresses using a double pointer.

# Triple Pointer in C

C also supports higher levels of pointers.

```text
Variable
    ↓
Pointer
    ↓
Double Pointer
    ↓
Triple Pointer
```

A triple pointer stores the address of a double pointer.

## Example

```c
#include <stdio.h>

int main() {

    int number = 50;

    int *ptr = &number;

    int **dptr = &ptr;

    int ***tptr = &dptr;

    printf("%d", ***tptr);

    return 0;
}
```

### Output
50

### Explanation

Three levels of dereferencing are used to reach the original variable.

# Applications of Double Pointers

Double pointers are widely used in:

1. Dynamic memory allocation.
2. Two-dimensional arrays.
3. Arrays of strings.
4. Linked lists and trees.
5. Functions that modify pointer variables.
6. File handling and buffer management.

# Advantages of Pointer to Pointer

1. Enables manipulation of pointer variables.
2. Useful for dynamic multidimensional arrays.
3. Supports complex data structures.
4. Reduces unnecessary copying.
5. Helps implement flexible memory management.
6. Provides multiple levels of indirection.

# Limitations of Pointer to Pointer

1. Programs become difficult to understand.
2. Multiple levels of dereferencing reduce readability.
3. Improper usage may cause segmentation faults.
4. Debugging multilevel pointers is challenging.
5. Excessive indirection increases program complexity.

# Real-Life Example

Suppose Akash Dangudubiyyapu maintains records of students Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil. A pointer can refer to a student's record, while a double pointer can refer to the pointer managing those records. This approach is useful when records need to be dynamically allocated or modified by different functions.

# Summary

A pointer to pointer in C is a multilevel pointer that stores the address of another pointer. It provides an additional level of indirection and is widely used in dynamic memory allocation, multidimensional arrays, arrays of strings, and advanced data structures. Although double pointers increase flexibility and efficiency, they should be used carefully because excessive indirection can make programs difficult to understand and maintain.

