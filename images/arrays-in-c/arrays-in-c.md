# Arrays in C

## Introduction

An array is a linear data structure that stores a fixed number of elements of the same data type in contiguous memory locations. Each element in an array is identified by an index, allowing direct access to any element.

Arrays are widely used when multiple values of the same type need to be stored and processed efficiently.

### Key Features

- Stores elements of the same data type.
- Elements are stored in contiguous memory locations.
- Provides random access using indexes.
- Has a fixed size after declaration.
- Supports efficient traversal and modification.

# Basic Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {2, 4, 6, 8, 10};

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### Output
2 4 6 8 10

### Explanation

The array stores five integer values. Each element is accessed using its index and printed using a loop.

# Properties of Arrays

- All elements have the same data type.
- Elements are stored in contiguous memory locations.
- Indexing starts from 0.
- Array size is fixed after declaration.
- Supports random access.

# Declaring an Array

Array declaration specifies the data type, array name, and size.

## Syntax

```c
data_type array_name[size];
```

## Example

```c
int marks[5];
```

This creates an integer array capable of storing five elements.

# Initializing an Array

Values can be assigned during declaration.

## Example

```c
int marks[5] = {85, 90, 78, 92, 88};
```

### Partial Initialization

```c
int arr[5] = {1, 2};
```

Remaining elements automatically become zero.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[5] = {1, 2};

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### Output
1 2 0 0 0

### Explanation

Only the first two elements are initialized explicitly. The remaining elements are initialized to zero.

# Declaring and Initializing Together

The compiler automatically determines the size.

```c
int arr[] = {10, 20, 30, 40, 50};
```

# Accessing Array Elements

Elements are accessed using indexes enclosed in square brackets.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[5] = {2, 4, 6, 8, 10};

    printf("%d\n", arr[0]);
    printf("%d\n", arr[2]);
    printf("%d", arr[4]);

    return 0;
}
```

### Output
2
6
10

### Explanation

Index starts from 0, so `arr[0]` refers to the first element.

# Updating Array Elements

Array values can be modified using assignment.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[3] = {10, 20, 30};

    arr[1] = 50;

    printf("%d", arr[1]);

    return 0;
}
```

### Output
50

### Explanation

The second element originally stored 20 and is updated to 50.

# Array Traversal

Traversal means visiting every element of the array.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[5] = {5, 10, 15, 20, 25};

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### Output
5 10 15 20 25

### Explanation

The loop visits each element one by one and prints it.

# Reverse Traversal

## Example

```c
#include <stdio.h>

int main()
{
    int arr[5] = {5, 10, 15, 20, 25};

    for (int i = 4; i >= 0; i--)
    {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### Output
25 20 15 10 5

### Explanation

Elements are visited from the last index to the first index.

# Finding Array Size

The `sizeof()` operator can determine the number of elements.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[] = {10, 20, 30, 40, 50};

    int size = sizeof(arr) / sizeof(arr[0]);

    printf("%d", size);

    return 0;
}
```

### Output
5

### Explanation

`sizeof(arr)` returns the total size in bytes, and dividing by the size of one element gives the number of elements.

# Memory Representation of Arrays

Suppose:

```c
int arr[4] = {10, 20, 30, 40};
```

Memory representation:

```text
Index      Value
0           10
1           20
2           30
3           40
```

The elements are stored in contiguous memory locations.

# Types of Arrays

## One-Dimensional Array

Stores data in a single row.

```c
int arr[5];
```

## Two-Dimensional Array

Stores data in rows and columns.

```c
int matrix[3][3];
```

## Multidimensional Array

Stores data in more than two dimensions.

```c
int arr[2][3][4];
```

# Advantages of Arrays

1. Easy to access elements using indexes.
2. Stores multiple values under one name.
3. Supports random access.
4. Efficient memory usage.
5. Simplifies traversal using loops.

# Limitations

1. Size is fixed after declaration.
2. Can store only one data type.
3. Insertion and deletion are costly.
4. Wastage of memory may occur.
5. Out-of-bound access causes undefined behavior.

# Applications of Arrays

- Storing marks of students.
- Matrix representation.
- Searching algorithms.
- Sorting algorithms.
- Implementing stacks and queues.
- Dynamic programming.
- Image processing.
- String manipulation.

# Summary

An array in C is a linear data structure that stores a fixed number of elements of the same data type in contiguous memory locations. Arrays support random access, making retrieval and modification efficient. Elements are accessed using indexes beginning from zero. Arrays are extensively used in searching, sorting, matrix operations, and implementing other data structures. Although arrays provide fast access and simple traversal, their fixed size and costly insertion and deletion operations are important limitations.

