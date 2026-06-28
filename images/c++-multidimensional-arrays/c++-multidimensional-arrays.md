# C++ Multidimensional Arrays

A multidimensional array in C++ is an array that contains more than one dimension, meaning its elements are organized along multiple axes rather than a single linear sequence. The two most widely used forms are:

- **Two-Dimensional (2D) Array:** Elements arranged in rows and columns, like a grid or matrix.
- **Three-Dimensional (3D) Array:** A collection of 2D arrays stacked along a depth axis, forming a cuboid structure.

Higher dimensions are possible but become increasingly complex to manage, so 2D and 3D arrays cover the majority of practical use cases.

## Syntax

```Cpp
data_type array_name[s1][s2]...[sn];
```

where `s1, s2, ..., sn` represent the size of each dimension.

```Cpp
int two_d[2][4];        // 2 rows, 4 columns
int three_d[2][4][8];   // 2 layers, 4 rows, 8 columns
```

## Array Size

The total number of elements in a multidimensional array is the product of all its dimension sizes — analogous to calculating area for 2D and volume for 3D.

```Cpp
int arr[2][4];
// Total elements = 2 * 4 = 8
// Size in bytes  = 8 * sizeof(int) = 8 * 4 = 32 bytes
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    int arr[2][4];
    cout << sizeof(arr) << " bytes" << endl;  
    return 0;
}
```

### Output
32 bytes

## Two-Dimensional (2D) Array

### Creating and Initializing a 2D Array

```Cpp
// With nested braces (explicit rows)
int arr[2][4] = {{0, 1, 2, 3}, {4, 5, 6, 7}};

// Without nesting (sequential fill)
int arr2[2][4] = {0, 1, 2, 3, 4, 5, 6, 7};

// Zero initialization
int arr3[2][4] = {0};
```

When using nested braces, each inner brace group corresponds to one row. Without nesting, elements fill the array row by row from left to right. Note that zero-initialization using `= {0}` works only for `0` — other values require explicit assignment.

Partial initialization (fewer values than total elements) is allowed; unspecified elements default to `0`. Specifying more values than the array can hold is a compile-time error.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-multidimensional-arrays/1782641704263-WhatsApp_Image_2026-06-28_at_3.42.57_PM.jpeg)

### Accessing and Updating Elements

Elements are accessed using two indices: `arr[row][column]`. Indexing starts at 0. Accessing outside the valid range causes undefined behavior (often a segmentation fault).

Valid index ranges:

- Row: `0 ≤ i ≤ (row_size - 1)`
- Column: `0 ≤ j ≤ (col_size - 1)`

```Cpp
#include <iostream>
using namespace std;

int main() {
    int arr[2][4] = {0, 1, 2, 3, 4, 5, 6, 7};

    cout << arr[0][2] << endl;  // 3rd element of row 0 → 2
    cout << arr[1][0] << endl;  // 1st element of row 1 → 4

    arr[0][2] = 22;
    cout << arr[0][2] << endl;  // Updated → 22

    arr[1][0] = 99;
    cout << arr[1][0] << endl;  // Updated → 99
    return 0;
}
```

### Output
2
4
22
99

### Traversing a 2D Array

Two nested loops are required — the outer loop iterates over rows, the inner loop iterates over columns within each row.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int arr[2][4] = {0, 1, 2, 3, 4, 5, 6, 7};

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 4; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}
```

### Output
0 1 2 3 
4 5 6 7

## Three-Dimensional (3D) Array

A 3D array adds a depth dimension on top of the row-column structure of a 2D array. Conceptually, it is a stack of 2D arrays layered along the depth axis.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-multidimensional-arrays/1782641765053-WhatsApp_Image_2026-06-28_at_3.45.47_PM.jpeg)

### Creating and Initializing a 3D Array

```Cpp
int arr[2][2][3];  // 2 layers, 2 rows per layer, 3 columns per row

// With full nesting
int arr2[2][2][3] = {
    {{0, 1, 2}, {3, 4, 5}},
    {{6, 7, 8}, {9, 10, 11}}
};

// Sequential fill (no nesting)
int arr3[2][2][3] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};

// Zero initialization
int arr4[2][2][3] = {0};
```

Total elements = `2 × 2 × 3 = 12`.

### Accessing and Updating Elements

Three indices are used: `arr[depth][row][column]`.

Valid index ranges:

- Depth: `0 ≤ i ≤ (depth_size - 1)`
- Row: `0 ≤ j ≤ (row_size - 1)`
- Column: `0 ≤ k ≤ (col_size - 1)`

```Cpp
#include <iostream>
using namespace std;

int main() {
    int arr[2][2][3] = {
        {{0, 1, 2}, {3, 4, 5}},
        {{6, 7, 8}, {9, 10, 11}}
    };

    cout << arr[0][1][2] << endl;  // depth=0, row=1, col=2 → 5
    cout << arr[1][0][1] << endl;  // depth=1, row=0, col=1 → 7

    arr[0][1][2] = 22;
    cout << arr[0][1][2] << endl;  // Updated → 22

    arr[1][0][1] = 99;
    cout << arr[1][0][1] << endl;  // Updated → 99
    return 0;
}
```

### Output
5
7
22
99

### Traversing a 3D Array

Three nested loops are needed — one for depth, one for rows, one for columns.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int arr[2][2][3] = {
        {{0, 1, 2}, {3, 4, 5}},
        {{6, 7, 8}, {9, 10, 11}}
    };

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 3; k++) {
                cout << arr[i][j][k] << " ";
            }
            cout << endl;
        }
    }
    return 0;
}
```

### Output
0 1 2 
3 4 5 
6 7 8 
9 10 11

## Passing Multidimensional Arrays to Functions

### Passing a 2D Array

When passing a 2D array to a function, all dimensions except the first must be specified in the function signature. The first dimension (row count) can be omitted.

```Cpp
#include <iostream>
using namespace std;

void print2D(int arr[][3], int rows) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
    print2D(arr, 2);
    return 0;
}
```

### Output
1 2 3 
4 5 6

### Passing a 3D Array

For a 3D array, the second and third dimension sizes must be explicitly specified in the function signature.

```Cpp
#include <iostream>
using namespace std;

void print3D(int arr[][3][4], int depth) {
    for (int i = 0; i < depth; i++) {
        for (int j = 0; j < 3; j++) {
            for (int k = 0; k < 4; k++) {
                cout << arr[i][j][k] << " ";
            }
            cout << endl;
        }
    }
}

int main() {
    int arr[2][3][4] = {
        {{1,2,3,4},{5,6,7,8},{9,10,11,12}},
        {{13,14,15,16},{17,18,19,20},{21,22,23,24}}
    };
    print3D(arr, 2);
    return 0;
}
```

### Output
1 2 3 4 
5 6 7 8 
9 10 11 12 
13 14 15 16 
17 18 19 20 
21 22 23 24

## 2D vs 3D Array — Quick Comparison

| Feature | 2D Array | 3D Array |
| --- | --- | --- |
| **Dimensions** | Row × Column | Depth × Row × Column |
| **Visualization** | Table / Grid | Stack of Tables |
| **Access Syntax** | `arr[i][j]` | `arr[i][j][k]` |
| **Traversal Loops** | 2 nested loops | 3 nested loops |
| **Function Signature** | Specify column count | Specify row and column counts |

> **Note:** When passing a multidimensional array to a function in C++, the first dimension size can always be omitted since C++ treats arrays as pointers to their first element. All subsequent dimension sizes must be specified so the compiler can correctly compute element offsets. Using `std::vector<std::vector<T>>` or `std::array` avoids this constraint and is preferred for dynamically sized multidimensional data.

## Summary

C++ multidimensional arrays extend the single-dimension array concept by organizing elements along two or more axes. A 2D array uses row and column indices, traversed with two nested loops. A 3D array adds a depth axis, requiring three nested loops. The total element count is always the product of all dimension sizes. When passing multidimensional arrays to functions, all dimension sizes beyond the first must be explicitly declared in the function signature. For more flexible multidimensional containers, `std::vector` nesting is preferred over raw C-style multidimensional arrays.




