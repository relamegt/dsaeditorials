# Pointer Arithmetic in C

## Introduction

Pointer arithmetic refers to the set of arithmetic operations that can be performed on pointers in C. Since a pointer stores the address of a variable rather than the value itself, arithmetic operations on pointers behave differently from ordinary mathematical operations.

When a pointer is incremented or decremented, the address changes by the size of the data type it points to. This feature allows programmers to efficiently traverse arrays, manipulate memory, and implement advanced data structures.

Only a limited set of arithmetic operations are valid on pointers:

- Increment and decrement operations.
- Addition of an integer to a pointer.
- Subtraction of an integer from a pointer.
- Subtraction of two pointers of the same type.
- Comparison of pointers.

## Why Use Pointer Arithmetic?

Pointer arithmetic provides several advantages:

- Enables efficient traversal of arrays.
- Simplifies memory access.
- Reduces the need for index variables.
- Improves performance in many low-level operations.
- Plays an important role in dynamic memory management and data structures.

# Increment and Decrement of Pointers

When a pointer is incremented, it moves to the next memory location corresponding to the size of the data type.

Similarly, when a pointer is decremented, it moves to the previous memory location.

For example:

- An `int` pointer moves by 4 bytes on most systems.
- A `char` pointer moves by 1 byte.
- A `double` pointer usually moves by 8 bytes.

## Example

```c
#include <stdio.h>

int main() {

    int marks[] = {75, 80, 85};

    int *ptr = marks;

    printf("%d\n", *ptr);

    ptr++;

    printf("%d\n", *ptr);

    ptr--;

    printf("%d\n", *ptr);

    return 0;
}
```

### Output
75
80
75

### Explanation

Initially, the pointer points to the first element. After incrementing, it points to the second element. Decrementing restores it to the first element.

# Addition of Integer to Pointer

Adding an integer to a pointer moves the pointer forward by that many elements, not by bytes.

## Example

```c
#include <stdio.h>

int main() {

    int scores[] = {45, 60, 75, 90, 95};

    int *ptr = scores;

    ptr = ptr + 3;

    printf("%d", *ptr);

    return 0;
}
```

### Output
90

### Explanation

The pointer initially points to 45. After adding 3, it skips three integer elements and reaches 90.

# Subtraction of Integer from Pointer

Subtracting an integer from a pointer moves the pointer backward.

## Example

```c
#include <stdio.h>

int main() {

    int values[] = {10, 20, 30, 40, 50};

    int *ptr = values + 4;

    ptr = ptr - 2;

    printf("%d", *ptr);

    return 0;
}
```

### Output
30

### Explanation

The pointer initially points to 50. Subtracting 2 moves it back to the element containing 30.

# Subtraction of Two Pointers

Two pointers of the same type can be subtracted. The result indicates the number of elements between them.

## Example

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int *start = &numbers[1];
    int *end = &numbers[4];

    int distance = end - start;

    printf("%d", distance);

    return 0;
}
```

### Output
3

### Explanation

There are three integer positions between index 1 and index 4.

# Comparison of Pointers

Pointers can be compared using relational operators.

Common operators are:

- `==`
- `!=`
- `<`
- `>`
- `<=`
- `>=`

## Example

```c
#include <stdio.h>

int main() {

    int data[] = {100, 200, 300};

    int *ptr1 = data;
    int *ptr2 = &data[0];

    if (ptr1 == ptr2) {
        printf("Pointers are equal");
    }
    else {
        printf("Pointers are not equal");
    }

    return 0;
}
```

### Output
Pointers are equal

### Explanation

Both pointers contain the address of the first element of the array.

# Comparison with NULL Pointer

A pointer can be checked against `NULL` before accessing memory.

## Example

```c
#include <stdio.h>

int main() {

    int *ptr = NULL;

    if (ptr == NULL) {
        printf("Pointer is NULL");
    }
    else {
        printf("Pointer contains an address");
    }

    return 0;
}
```

### Output
Pointer is NULL

### Explanation

Since the pointer does not point to any valid memory location, it contains `NULL`.

# Pointer Arithmetic on Arrays

Array names behave like constant pointers to their first element.

Pointer arithmetic makes array traversal simple and efficient.

## Example

```c
#include <stdio.h>

int main() {

    int marks[] = {70, 80, 90, 95, 100};

    int *ptr = marks;

    for (int i = 0; i < 5; i++) {

        printf("%d ", *ptr);

        ptr++;
    }

    return 0;
}
```

### Output
70 80 90 95 100

### Explanation

After each iteration, the pointer moves to the next element of the array.

# Pointer Arithmetic on Character Arrays

Character pointers move one byte at a time.

## Example

```c
#include <stdio.h>

int main() {

    char name[] = "Akash";

    char *ptr = name;

    while (*ptr != '\0') {

        printf("%c ", *ptr);

        ptr++;
    }

    return 0;
}
```

### Output
A k a s h

### Explanation

Each increment moves the pointer to the next character because the size of `char` is one byte.

# Traversing Arrays Using Pointer Notation

Array indexing and pointer notation are equivalent.

## Example

```c
#include <stdio.h>

int main() {

    int ages[] = {21, 22, 23, 24};

    int *ptr = ages;

    for (int i = 0; i < 4; i++) {

        printf("%d ", *(ptr + i));
    }

    return 0;
}
```

### Output
21 22 23 24

### Explanation

`*(ptr + i)` accesses the same element as `ages[i]`.

# Pointer Arithmetic with 2D Arrays

Pointers can also be used to traverse multidimensional arrays.

## Example

```c
#include <stdio.h>

int main() {

    int marks[2][3] = {
        {70, 75, 80},
        {85, 90, 95}
    };

    int *ptr = &marks[0][0];

    for (int i = 0; i < 6; i++) {

        printf("%d ", *(ptr + i));
    }

    return 0;
}
```

### Output
70 75 80 85 90 95

### Explanation

The 2D array elements are stored continuously in memory. Incrementing the pointer accesses each element sequentially.

# Valid Pointer Operations

The following operations are valid:

- Increment a pointer.
- Decrement a pointer.
- Add an integer to a pointer.
- Subtract an integer from a pointer.
- Compare pointers.
- Subtract two pointers of the same type.

## Example

```c
int *ptr;

ptr++;
ptr--;
ptr = ptr + 5;
ptr = ptr - 2;
```

# Invalid Pointer Operations

Certain operations are not allowed.

- Addition of two pointers.
- Multiplication of pointers.
- Division of pointers.
- Modulus operation on pointers.

## Invalid Examples

```c
ptr1 + ptr2;
ptr1 * ptr2;
ptr1 / ptr2;
ptr1 % ptr2;
```

These operations do not have any meaningful interpretation in memory addressing and therefore are not supported.

# Real-Life Example

Suppose Akash Dangudubiyyapu stores marks of students Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil in an array. Instead of using indices, he can use a pointer to move from one student's marks to the next efficiently.

Pointer arithmetic makes such traversal simple and fast.

# Advantages of Pointer Arithmetic

1. Provides efficient array traversal.
2. Simplifies memory manipulation.
3. Reduces dependence on index variables.
4. Useful in dynamic memory allocation.
5. Helps in implementing data structures such as linked lists, stacks, queues, and trees.
6. Improves execution speed in low-level programs.

# Limitations of Pointer Arithmetic

1. Incorrect arithmetic may lead to undefined behavior.
2. Accessing invalid memory locations can crash the program.
3. Pointer misuse can create security vulnerabilities.
4. Debugging pointer-related issues is often difficult.
5. Some arithmetic operations are prohibited.

# Summary

Pointer arithmetic in C allows programmers to manipulate memory addresses efficiently. Operations such as increment, decrement, addition, subtraction, and comparison enable easy traversal of arrays and dynamic memory structures. Since pointer arithmetic depends on the size of the data type being referenced, understanding how addresses change is essential for writing efficient and reliable C programs. Proper use of pointer arithmetic provides flexibility and performance, while careless usage may result in undefined behavior and memory errors.

