# Double Pointer in C

## Introduction

A double pointer, also known as a pointer to pointer, is a pointer that stores the address of another pointer. The first pointer stores the address of a variable, while the second pointer stores the address of the first pointer. Double pointers are useful when working with dynamic memory allocation, arrays of strings, and modifying pointers inside functions.

### Key Features

- Stores the address of another pointer.
- Uses two dereference operators (`**`) to access the actual value.
- Supports dynamic memory allocation for multidimensional arrays.
- Used to pass pointers to functions.
- Commonly used in linked lists, trees, and other dynamic data structures.
- Supports multilevel pointers.

---

## Declaration of Double Pointer

A double pointer is declared using two asterisks (`**`).

### Syntax

```c
data_type **pointer_name;
```

### Example

```c
int **ptr;
char **str;
float **fptr;
```

### Explanation

- `int **ptr` stores the address of an integer pointer.
- `char **str` stores the address of a character pointer.
- `float **fptr` stores the address of a float pointer.

---

## Working of Double Pointer

A double pointer stores the address of a pointer, and that pointer stores the address of a variable.

### Example

```c
#include <stdio.h>

int main()
{
    int var = 10;

    int *ptr1 = &var;

    int **ptr2 = &ptr1;

    printf("var = %d\n", var);
    printf("*ptr1 = %d\n", *ptr1);
    printf("**ptr2 = %d", **ptr2);

    return 0;
}
```

### Output
10
10
10

### Explanation

- `ptr1` stores the address of `var`.
- `ptr2` stores the address of `ptr1`.
- `**ptr2` first accesses `ptr1`, then accesses the value stored in `var`.

---

## Memory Representation

```text
Variable        Value        Address

var              10          1000
ptr1             1000        2000
ptr2             2000        3000
```

```text
**ptr2 → *ptr1 → var → 10
```

---

## Size of Double Pointer

The size of a double pointer is the same as the size of any other pointer because it stores only an address.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 5;

    int *ptr = &num;

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

On a 64-bit system, both single pointers and double pointers occupy 8 bytes.

---

## Accessing Values Using Double Pointer

A double pointer requires two dereference operators to access the original value.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 100;

    int *ptr = &num;

    int **dptr = &ptr;

    printf("%d", **dptr);

    return 0;
}
```

### Output
100

### Explanation

The first `*` accesses the pointer `ptr`, and the second `*` accesses the value stored in `num`.

---

## Modifying a Variable Using Double Pointer

Changes made through a double pointer affect the original variable.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 20;

    int *ptr = &num;

    int **dptr = &ptr;

    **dptr = 50;

    printf("%d", num);

    return 0;
}
```

### Output
50

### Explanation

`**dptr` directly modifies the value stored in `num`.

---

## Double Pointer and Dynamic 2D Arrays

Double pointers are commonly used to create dynamic two-dimensional arrays.

### Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int rows = 2;
    int cols = 3;

    int **arr;

    arr = (int **)malloc(rows * sizeof(int *));

    for(int i = 0; i < rows; i++)
    {
        arr[i] = (int *)malloc(cols * sizeof(int));
    }

    int value = 1;

    for(int i = 0; i < rows; i++)
    {
        for(int j = 0; j < cols; j++)
        {
            arr[i][j] = value++;
        }
    }

    for(int i = 0; i < rows; i++)
    {
        for(int j = 0; j < cols; j++)
        {
            printf("%d ", arr[i][j]);
        }

        printf("\n");
    }

    for(int i = 0; i < rows; i++)
    {
        free(arr[i]);
    }

    free(arr);

    return 0;
}
```

### Output
1 2 3
4 5 6

### Explanation

Memory is allocated separately for rows and columns using a double pointer.

---

## Passing Array of Strings to a Function

Arrays of strings are internally arrays of character pointers and can be passed using double pointers.

### Example

```c
#include <stdio.h>

void display(char **arr, int n)
{
    for(int i = 0; i < n; i++)
    {
        printf("%s\n", arr[i]);
    }
}

int main()
{
    char *names[] = {
        "Alpha",
        "Knowledge",
        "Academy"
    };

    display(names, 3);

    return 0;
}
```

### Output
Alpha
Knowledge
Academy

### Explanation

Each element of the array is a pointer to a string, and the function receives it using a double pointer.

---

## Double Pointer as Function Argument

Double pointers are used when a function needs to modify the original pointer.

### Example

```c
#include <stdio.h>

void update(int **ptr)
{
    static int value = 100;

    *ptr = &value;
}

int main()
{
    int num = 10;

    int *ptr = &num;

    update(&ptr);

    printf("%d", *ptr);

    return 0;
}
```

### Output
100

### Explanation

The function modifies the address stored inside the pointer.

---

## Multilevel Pointers

C supports multiple levels of pointers.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 10;

    int *ptr = &num;

    int **ptr2 = &ptr;

    int ***ptr3 = &ptr2;

    printf("%d", ***ptr3);

    return 0;
}
```

### Output
10

### Explanation

Triple pointers store the address of double pointers. Any number of pointer levels can be created, although excessive levels make programs difficult to understand.

---

## Applications of Double Pointers

1. Dynamic memory allocation of 2D arrays.
2. Passing arrays of strings to functions.
3. Modifying pointers inside functions.
4. Implementing linked lists and trees.
5. Managing multidimensional data.
6. Working with command-line arguments.

---

## Advantages of Double Pointers

1. Enable dynamic multidimensional arrays.
2. Allow functions to modify pointers.
3. Efficient memory management.
4. Useful in complex data structures.
5. Reduce unnecessary copying of pointers.

---

## Limitations

1. Difficult to understand for beginners.
2. Multiple levels of indirection make code complex.
3. Incorrect usage may cause segmentation faults.
4. Debugging pointer-related errors becomes difficult.
5. Excessive pointer levels reduce code readability.

---

## Summary

A double pointer is a pointer that stores the address of another pointer. It is accessed using two dereference operators (`**`) and is widely used in dynamic memory allocation, multidimensional arrays, arrays of strings, and pointer manipulation inside functions. Double pointers provide flexibility and efficient memory handling, making them an important concept in advanced C programming.

