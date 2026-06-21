# Pointers in C

## Introduction

A pointer is a variable that stores the memory address of another variable. Instead of storing a value directly, a pointer stores the address where the value is located in memory. Pointers are one of the most powerful features of C and are widely used for memory management, arrays, strings, functions, and dynamic data structures.

### Key Features

- Stores memory addresses instead of values.
- Enables direct memory access.
- Supports dynamic memory allocation.
- Used in arrays, strings, structures, and functions.
- Helps implement complex data structures efficiently.

# Declaring a Pointer

A pointer is declared using the `*` operator.

## Syntax

```c
data_type *pointer_name;
```

### Example

```c
int *ptr;
char *ch;
float *fp;
```

Here:

- `ptr` points to an integer.
- `ch` points to a character.
- `fp` points to a float.

# Initializing a Pointer

A pointer is initialized using the address operator `&`.

## Example

```c
#include <stdio.h>

int main()
{
    int num = 10;

    int *ptr = &num;

    printf("%p", ptr);

    return 0;
}
```

### Output
Memory address of num (Hexadecimal value)

### Explanation

The address operator `&` returns the address of `num`, which is stored inside `ptr`.

# Dereferencing a Pointer

Dereferencing means accessing the value stored at the address contained in the pointer.

The dereference operator is `*`.

## Example

```c
#include <stdio.h>

int main()
{
    int num = 50;

    int *ptr = &num;

    printf("%d", *ptr);

    return 0;
}
```

### Output
50

### Explanation

`ptr` stores the address of `num`, and `*ptr` gives the value stored at that address.

# Address Operator (&)

The address operator returns the memory location of a variable.

## Example

```c
#include <stdio.h>

int main()
{
    int num = 25;

    printf("%p", &num);

    return 0;
}
```

### Output
Hexadecimal address

### Explanation

`&num` returns the address where `num` is stored.

# Pointer and Variable Relationship

```text
Variable        Value      Address
num             100        1000

Pointer ptr     1000
*ptr            100
```

# Size of Pointers

The size of pointers depends on the architecture of the system.

| Architecture | Pointer Size |
| --- | --- |
| 32-bit | 4 Bytes |
| 64-bit | 8 Bytes |

## Example

```c
#include <stdio.h>

int main()
{
    int *ptr1;
    char *ptr2;

    printf("%zu\n", sizeof(ptr1));
    printf("%zu", sizeof(ptr2));

    return 0;
}
```

### Output (64-bit System)

8
8

### Explanation

All pointer types occupy the same amount of memory because they only store addresses.

# NULL Pointer

A NULL pointer points to no memory location.

## Example

```c
#include <stdio.h>

int main()
{
    int *ptr = NULL;

    if(ptr == NULL)
    {
        printf("Pointer is NULL");
    }

    return 0;
}
```

### Output
Pointer is NULL

### Explanation

NULL pointers help avoid accessing invalid memory.

# Void Pointer

A void pointer is a generic pointer that can point to any data type.

## Example

```c
#include <stdio.h>

int main()
{
    int num = 20;

    void *ptr = &num;

    printf("%d", *(int *)ptr);

    return 0;
}
```

### Output
20

### Explanation

A void pointer must be typecast before dereferencing.

# Wild Pointer

A pointer that has not been initialized is called a wild pointer.

## Example

```c
int *ptr;
```

### Explanation

Wild pointers contain garbage addresses and may lead to crashes.

# Dangling Pointer

A pointer that points to deallocated memory is called a dangling pointer.

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *ptr = (int *)malloc(sizeof(int));

    free(ptr);

    ptr = NULL;

    return 0;
}
```

### Explanation

After freeing memory, assigning NULL prevents dangling pointers.

# Pointer Arithmetic

Arithmetic operations allowed on pointers include:

- Increment
- Decrement
- Addition
- Subtraction
- Comparison

## Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10,20,30};

    int *ptr = arr;

    printf("%d\n", *ptr);

    ptr++;

    printf("%d", *ptr);

    return 0;
}
```

### Output
10
20

### Explanation

`ptr++` moves the pointer to the next integer location.

# Constant Pointer

The address stored in a constant pointer cannot be changed.

## Syntax

```c
int *const ptr = &a;
```

## Example

```c
#include <stdio.h>

int main()
{
    int a = 10;

    int *const ptr = &a;

    *ptr = 50;

    printf("%d", a);

    return 0;
}
```

### Output
50

### Explanation

The pointer address remains fixed, but the value can be modified.

# Pointer to Constant

The value cannot be modified through the pointer.

## Syntax

```c
const int *ptr;
```

## Example

```c
#include <stdio.h>

int main()
{
    int a = 100;

    const int *ptr = &a;

    printf("%d", *ptr);

    return 0;
}
```

### Output
100

# Constant Pointer to Constant

Neither the address nor the value can be changed.

## Syntax

```c
const int *const ptr = &a;
```

# Function Pointer

A function pointer stores the address of a function.

## Example

```c
#include <stdio.h>

int add(int a, int b)
{
    return a + b;
}

int main()
{
    int (*ptr)(int, int);

    ptr = add;

    printf("%d", ptr(10, 20));

    return 0;
}
```

### Output
30

### Explanation

The function is called through its pointer.

# Double Pointer

A double pointer stores the address of another pointer.

## Example

```c
#include <stdio.h>

int main()
{
    int num = 10;

    int *ptr1 = &num;

    int **ptr2 = &ptr1;

    printf("%d", **ptr2);

    return 0;
}
```

### Output
10

### Explanation

`ptr2` points to `ptr1`, and `**ptr2` gives the actual value.

# Pointer to Array

## Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10,20,30};

    int *ptr = arr;

    printf("%d", *(ptr + 2));

    return 0;
}
```

### Output
30

# Array and Pointer Relationship

```text
arr[0]  = *(arr + 0)
arr[1]  = *(arr + 1)
arr[2]  = *(arr + 2)
```

The array name itself acts as a pointer to the first element.

# Advantages of Pointers

1. Supports dynamic memory allocation.
2. Makes array and string handling efficient.
3. Used in linked lists, trees, and graphs.
4. Reduces execution time.
5. Allows direct memory manipulation.
6. Supports callback functions.

# Limitations

1. Difficult for beginners.
2. Uninitialized pointers may cause segmentation faults.
3. Incorrect usage can corrupt memory.
4. Responsible for memory leaks.
5. Debugging pointer errors is challenging.

# Summary

Pointers are variables that store memory addresses. They enable direct memory access and form the foundation of dynamic memory allocation and advanced data structures in C. Important concepts include pointer declaration, initialization, dereferencing, pointer arithmetic, NULL pointers, void pointers, dangling pointers, function pointers, and multilevel pointers. Understanding pointers is essential because they provide efficiency and flexibility that are difficult to achieve with ordinary variables alone.

