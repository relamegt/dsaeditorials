# Multidimensional Arrays in C - 2D and 3D Arrays

## Introduction

A multidimensional array is an array that contains more than one dimension. It allows data to be arranged in rows, columns, and higher dimensions. The most commonly used multidimensional arrays are two-dimensional (2D) arrays and three-dimensional (3D) arrays.

A 2D array can be visualized as a table consisting of rows and columns, while a 3D array can be imagined as multiple 2D arrays stacked together.

### Key Features

- Stores elements of the same data type.
- Supports multiple dimensions.
- Elements are stored in contiguous memory locations.
- Provides direct access using indexes.
- Useful for matrices, tables, and grids.

# Syntax

The general syntax of a multidimensional array is:

```c
data_type array_name[size1][size2]...[sizeN];
```

### Example

```c
int matrix[3][4];
int cube[2][3][4];
```

## Size of Multidimensional Arrays

The total number of elements equals the product of all dimensions.

### Example

```c
int arr[10][20];
```

Number of elements:

```text
10 × 20 = 200
```

If an integer occupies 4 bytes:

```text
Total Size = 10 × 20 × 4 = 800 bytes
```

# Types of Multidimensional Arrays

1. Two-Dimensional Array (2D Array)
2. Three-Dimensional Array (3D Array)

# Two-Dimensional Arrays (2D Arrays)

A two-dimensional array consists of rows and columns and can be represented like a matrix.

```text
Column →
      0    1    2
0    10   20   30
1    40   50   60
2    70   80   90
↑
Row
```

## Declaration of 2D Array

### Syntax

```c
data_type array_name[rows][columns];
```

### Example

```c
int marks[3][4];
```

This creates a table with 3 rows and 4 columns.

# Initialization of 2D Arrays

## Method 1

```c
int arr[3][4] = {
    1, 2, 3, 4,
    5, 6, 7, 8,
    9, 10, 11, 12
};
```

## Method 2

```c
int arr[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

## Example

```c
#include <stdio.h>

int main()
{
    int marks[2][3] = {
        {85, 90, 88},
        {76, 95, 82}
    };

    printf("%d", marks[1][2]);

    return 0;
}
```

### Output
82

### Explanation

The element at row 1 and column 2 contains the value 82.

# Accessing Elements of 2D Array

### Syntax

```c
array_name[row][column]
```

### Example

```c
#include <stdio.h>

int main()
{
    int arr[2][2] = {
        {10, 20},
        {30, 40}
    };

    printf("%d\n", arr[0][1]);
    printf("%d", arr[1][0]);

    return 0;
}
```

### Output
20
30

### Explanation

`arr[0][1]` represents the first row and second column, while `arr[1][0]` represents the second row and first column.

# Traversing a 2D Array

Nested loops are used to visit every element.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[3][2] = {
        {1, 2},
        {3, 4},
        {5, 6}
    };

    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 2; j++)
        {
            printf("%d ", arr[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

### Output
1 2
3 4
5 6

### Explanation

The outer loop traverses rows and the inner loop traverses columns.

# How 2D Arrays are Stored in Memory

Elements of a 2D array are stored continuously in memory. C uses **Row Major Order**, which means elements are stored row by row.

Consider:

```c
int arr[2][3] = {
    {10, 20, 30},
    {40, 50, 60}
};
```

Memory arrangement:

```text
10 20 30 40 50 60
```

The first row is stored completely, followed by the second row.

# Passing 2D Arrays to Functions

When passing a 2D array to a function, the number of columns must be specified.

## Example

```c
#include <stdio.h>

void display(int arr[][3], int rows)
{
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            printf("%d ", arr[i][j]);
        }

        printf("\n");
    }
}

int main()
{
    int arr[2][3] = {
        {10, 20, 30},
        {40, 50, 60}
    };

    display(arr, 2);

    return 0;
}
```

### Output
10 20 30
40 50 60

### Explanation

The function receives the array and prints every element using nested loops.

# Three-Dimensional Arrays (3D Arrays)

A three-dimensional array is a collection of multiple two-dimensional arrays.

```text
Layer 0

1 2
3 4

Layer 1

5 6
7 8
```

## Declaration of 3D Array

### Syntax

```c
data_type array_name[depth][rows][columns];
```

### Example

```c
int cube[2][3][2];
```

This array contains:

- 2 layers
- 3 rows per layer
- 2 columns per row

Total elements:

```text
2 × 3 × 2 = 12
```

# Initialization of 3D Arrays

## Method 1

```c
int arr[2][2][2] = {
    {
        {1, 2},
        {3, 4}
    },
    {
        {5, 6},
        {7, 8}
    }
};
```

# Accessing Elements of 3D Arrays

### Syntax

```c
array_name[layer][row][column]
```

## Example

```c
#include <stdio.h>

int main()
{
    int arr[2][2][2] = {
        {
            {1, 2},
            {3, 4}
        },
        {
            {5, 6},
            {7, 8}
        }
    };

    printf("%d", arr[1][0][1]);

    return 0;
}
```

### Output
6

### Explanation

`arr[1][0][1]` means:

- Layer 1
- Row 0
- Column 1

Hence, the value printed is 6.

# Traversing a 3D Array

Three nested loops are required.

## Example

```c
#include <stdio.h>

int main()
{
    int arr[2][2][2] = {
        {
            {1, 2},
            {3, 4}
        },
        {
            {5, 6},
            {7, 8}
        }
    };

    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 2; j++)
        {
            for (int k = 0; k < 2; k++)
            {
                printf("%d ", arr[i][j][k]);
            }

            printf("\n");
        }

        printf("\n");
    }

    return 0;
}
```

### Output
1 2
3 4
5 6
7 8

### Explanation

The outer loop traverses layers, the middle loop traverses rows, and the inner loop traverses columns.

# Storage of 3D Arrays in Memory

Like 2D arrays, 3D arrays are also stored continuously in memory. C stores them in row-major order layer by layer.

Consider:

```c
int arr[2][2][2] = {
    {
        {1, 2},
        {3, 4}
    },
    {
        {5, 6},
        {7, 8}
    }
};
```

Memory arrangement:

```text
1 2 3 4 5 6 7 8
```

The first layer is stored completely before the second layer.

# Passing 3D Arrays to Functions

When passing a 3D array to a function, all dimensions except the first one must be specified.

## Example

```c
#include <stdio.h>

void display(int arr[][2][2], int depth)
{
    for (int i = 0; i < depth; i++)
    {
        for (int j = 0; j < 2; j++)
        {
            for (int k = 0; k < 2; k++)
            {
                printf("%d ", arr[i][j][k]);
            }

            printf("\n");
        }

        printf("\n");
    }
}

int main()
{
    int arr[2][2][2] = {
        {
            {1, 2},
            {3, 4}
        },
        {
            {5, 6},
            {7, 8}
        }
    };

    display(arr, 2);

    return 0;
}
```

### Output
1 2
3 4
5 6
7 8

### Explanation

The array is passed to the function, and three nested loops are used to access all elements.

# Difference Between 2D and 3D Arrays

| Feature | 2D Array | 3D Array |
| --- | --- | --- |
| Dimensions | 2 | 3 |
| Representation | Rows and Columns | Layers, Rows and Columns |
| Number of Indexes | Two | Three |
| Traversal | Two loops | Three loops |
| Example | Matrix | Collection of matrices |

# Applications of Multidimensional Arrays

1. Matrix operations.
2. Image processing.
3. Representation of tables and spreadsheets.
4. Storing game boards.
5. Scientific and mathematical computations.
6. Graphics and animations.
7. Database management.
8. Simulation and modeling.

# Advantages

1. Organizes data in tabular form.
2. Supports fast random access.
3. Efficient memory utilization.
4. Useful for matrices and grids.
5. Simplifies complex calculations.

# Limitations

1. Size is fixed after declaration.
2. Memory requirement increases rapidly with dimensions.
3. Insertion and deletion are difficult.
4. Large multidimensional arrays may waste memory.
5. More dimensions make programs harder to understand.

# Summary

A multidimensional array is an array with two or more dimensions. The most commonly used types are 2D and 3D arrays. A 2D array represents rows and columns, while a 3D array represents layers, rows, and columns. Elements are stored contiguously in memory in row-major order, providing efficient random access. Multidimensional arrays are widely used in matrix operations, image processing, graphics, scientific computations, and many real-world applications.

