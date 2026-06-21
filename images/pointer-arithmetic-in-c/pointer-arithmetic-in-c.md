# Pointer Arithmetic in C

## Introduction

Pointer arithmetic refers to the arithmetic operations that can be performed on pointers in C. Since pointers store memory addresses rather than actual values, pointer operations behave differently from normal arithmetic operations. When a pointer is incremented or decremented, the address changes according to the size of the data type it points to.

Pointer arithmetic is commonly used for traversing arrays, strings, dynamic memory blocks, and implementing complex data structures efficiently.

### Key Features

- Arithmetic operations are performed on memory addresses.
- Pointer movement depends on the size of the data type.
- Supports increment and decrement operations.
- Allows addition and subtraction of integers.
- Two pointers of the same type can be subtracted.
- Pointers can be compared using relational operators.
- Widely used for array traversal and memory manipulation.

---

## Valid Operations on Pointers

The following operations are allowed on pointers:

1. Increment and decrement of a pointer.
2. Addition of an integer to a pointer.
3. Subtraction of an integer from a pointer.
4. Subtraction of two pointers of the same type.
5. Comparison of pointers.
6. Comparison with NULL.

### Note

Memory addresses usually change every time a program runs because modern operating systems use Address Space Layout Randomization (ASLR) to improve security.

---

## Increment and Decrement of a Pointer

When a pointer is incremented, it moves to the next memory location according to the size of the data type.

Similarly, when a pointer is decremented, it moves to the previous memory location.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 10;

    int *ptr = &num;

    printf("%p\n", ptr);

    ptr++;

    printf("%p\n", ptr);

    ptr--;

    printf("%p", ptr);

    return 0;
}
```

### Output
Address of num
Next integer address
Original address

### Explanation

Since an integer occupies 4 bytes, incrementing the pointer increases its address by 4 bytes. Decrementing restores the original address.

---

## Addition of Integer to a Pointer

When an integer is added to a pointer, the integer is multiplied by the size of the data type and then added to the address.

### Formula

```text
New Address = Old Address + n × sizeof(data type)
```

### Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10, 20, 30, 40};

    int *ptr = arr;

    printf("%d\n", *ptr);

    ptr = ptr + 2;

    printf("%d", *ptr);

    return 0;
}
```

### Output
10
30

### Explanation

Adding 2 moves the pointer to the third element of the array.

---

## Subtraction of Integer from a Pointer

Subtracting an integer from a pointer moves it backward.

### Formula

```text
New Address = Old Address - n × sizeof(data type)
```

### Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10, 20, 30, 40};

    int *ptr = &arr[3];

    printf("%d\n", *ptr);

    ptr = ptr - 2;

    printf("%d", *ptr);

    return 0;
}
```

### Output
40
20

### Explanation

Subtracting 2 moves the pointer two integer locations backward.

---

## Subtraction of Two Pointers

Two pointers can be subtracted only if they point to elements of the same data type.

The result gives the number of elements between them.

### Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10, 20, 30, 40, 50};

    int *ptr1 = &arr[4];
    int *ptr2 = &arr[1];

    printf("%ld", ptr1 - ptr2);

    return 0;
}
```

### Output
3

### Explanation

The difference between the pointers indicates that three integer elements lie between them.

---

## Comparison of Pointers

Pointers can be compared using relational operators.

### Operators

- `==`
- `!=`
- `<`
- `>`
- `<=`
- `>=`

### Example

```c
#include <stdio.h>

int main()
{
    int arr[5];

    int *ptr1 = arr;
    int *ptr2 = &arr[0];

    if(ptr1 == ptr2)
    {
        printf("Pointers are equal");
    }

    return 0;
}
```

### Output
Pointers are equal

### Explanation

The array name points to the first element, therefore both pointers contain the same address.

---

## Comparison with NULL

Pointers of any type can be compared with NULL.

### Example

```c
#include <stdio.h>

int main()
{
    int *ptr = NULL;

    if(ptr == NULL)
    {
        printf("The pointer is NULL");
    }

    return 0;
}
```

### Output
The pointer is NULL

### Explanation

NULL indicates that the pointer is not pointing to any valid memory location.

---

## Pointer Arithmetic on Arrays

The array name acts as a pointer to the first element of the array.

### Relationship

```text
arr[0] = *(arr + 0)
arr[1] = *(arr + 1)
arr[2] = *(arr + 2)
```

### Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {1, 2, 3, 4, 5};

    int *ptr = arr;

    for(int i = 0; i < 5; i++)
    {
        printf("%d ", *ptr);
        ptr++;
    }

    return 0;
}
```

### Output
1 2 3 4 5

### Explanation

The pointer traverses the array by moving to the next element after each iteration.

---

## Pointer Arithmetic with Character Pointers

Since a character occupies one byte, incrementing a character pointer increases its address by one byte.

### Example

```c
#include <stdio.h>

int main()
{
    char str[] = "HELLO";

    char *ptr = str;

    while(*ptr != '\0')
    {
        printf("%c ", *ptr);
        ptr++;
    }

    return 0;
}
```

### Output
H E L L O

### Explanation

Each increment moves the pointer by one byte because characters occupy one byte in memory.

---

## Pointer Arithmetic with 2D Arrays

Pointers can also traverse multidimensional arrays because the elements are stored continuously in memory.

### Example

```c
#include <stdio.h>

int main()
{
    int arr[2][2] = {
        {1, 2},
        {3, 4}
    };

    int *ptr = (int *)arr;

    for(int i = 0; i < 4; i++)
    {
        printf("%d ", *(ptr + i));
    }

    return 0;
}
```

### Output
1 2 3 4

### Explanation

The entire 2D array is treated as a continuous block of memory and traversed using a pointer.

---

## Invalid Pointer Arithmetic Operations

The following operations are invalid:

- Addition of two pointers.
- Multiplication of pointers.
- Division of pointers.
- Modulus operation on pointers.

### Invalid Example

```c
int *ptr1;
int *ptr2;

ptr1 + ptr2;
```

### Explanation

Adding two addresses does not produce a meaningful memory location and is therefore not allowed.

---

## Advantages of Pointer Arithmetic

1. Simplifies array traversal.
2. Provides efficient memory access.
3. Reduces execution time.
4. Useful in dynamic memory allocation.
5. Makes implementation of data structures easier.
6. Supports manipulation of multidimensional arrays.

---

## Limitations

1. Only limited arithmetic operations are allowed.
2. Incorrect arithmetic can lead to undefined behavior.
3. Out-of-bounds access may cause segmentation faults.
4. Pointer arithmetic can be difficult for beginners.
5. Operations on unrelated pointers are invalid.

---

## Summary

Pointer arithmetic allows arithmetic operations on memory addresses stored in pointers. Valid operations include increment, decrement, addition and subtraction of integers, subtraction of two pointers of the same type, and pointer comparisons. Pointer arithmetic is extensively used for array traversal, strings, dynamic memory allocation, and advanced data structures. Understanding how pointer movement depends on the size of the data type is essential for writing efficient and reliable C programs.

