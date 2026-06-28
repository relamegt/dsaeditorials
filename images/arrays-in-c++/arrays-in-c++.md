# Arrays in C++

## Introduction

An array is a fixed-size, sequential collection of elements of the same data type stored in contiguous memory locations. It allows you to group multiple related values under a single variable name and access them using integer indices, rather than declaring individual variables for each value.

Key characteristics:

- **Contiguous Storage:** Elements are placed next to each other in memory, enabling fast access.
- **Zero-based Indexing:** The first element is always accessed at index `0`, the second at index `1`, up to `size - 1`.
- **Fixed Size:** Once declared, the size of a standard array cannot be changed during program execution.

## Declaration of an Array

To declare an array in C++, you specify the data type of the elements, followed by the array name, and the number of elements inside square brackets `[]` (the subscript operator).

**Syntax:**

```Cpp
data_type array_name[size];
```

```Cpp
int primes[5]; // Declares an array of 5 integers
```

When declared without initialization, local arrays contain indeterminate (garbage) values.

## Initializing the Array

Initialization assigns starting values to the array elements at declaration.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1782645809380-18.png)

### Explicit Initialization

```Cpp
int primes[5] = {2, 3, 5, 7, 11};
```

Values are assigned sequentially: `primes[0]` is 2, `primes[1]` is 3, etc. The number of initializers must not exceed the array's declared size.

### Partial Initialization

```Cpp
int primes[5] = {2, 3}; // Elements 2 and 3 are set; remaining default to 0
```

Unspecified elements are automatically initialized to `0` by the compiler.

### Size Inference

```Cpp
int primes[] = {2, 3, 5, 7, 11}; // Size is automatically set to 5
```

If the size is omitted, the compiler sets the array size to match the number of initializers.

### Zero-Initialization Shorthand

```Cpp
int primes[5] = {0}; // All 5 elements are initialized to 0
```

## Basic Operations on Array Elements

### 1. Accessing Elements

You retrieve an element by placing its zero-based index inside square brackets next to the array name.

```Cpp
#include <iostream>
using namespace std;

int main() {
    double temperatures[] = {98.2, 98.6, 99.1, 97.9, 98.5};

    cout << "First temperature : " << temperatures[0] << endl;
    cout << "Third temperature : " << temperatures[2] << endl;

    return 0;
}
```

### Output
First temperature : 98.2
Third temperature : 99.1

Indices must satisfy the range `0 ≤ index < size`. Accessing indices outside this range causes undefined behavior.

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1782645853516-22.png)

### 2. Updating Elements

You can modify an element's value using the assignment operator (`=`).

```Cpp
#include <iostream>
using namespace std;

int main() {
    double temperatures[] = {98.2, 98.6, 99.1, 97.9, 98.5};

    temperatures[0] = 98.4; // Update the first element
    cout << "Updated temperature: " << temperatures[0] << endl;

    return 0;
}
```

### Output
Updated temperature: 98.4

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1782645889737-19.png)

### 3. Traversing an Array

Traversing refers to visiting every element in the array sequentially. This is typically done using a `for` loop or a range-based `for` loop.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int quantities[4] = {10, 20, 15, 30};

    // Standard loop traversal
    for (int i = 0; i < 4; i++) {
        cout << quantities[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### Output
10 20 15 30

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1782645928159-17.png)

### 4. Determining Array Size and Length

The `sizeof()` operator returns the total number of bytes allocated to an object or data type. Because arrays are contiguous, you can calculate the number of elements in an array by dividing the total size of the array by the size of a single element.

```Cpp
#include <iostream>
using namespace std;

int main() {
    double coordinates[] = {1.5, 2.5, 3.5, 4.5};

    cout << "Total array bytes : " << sizeof(coordinates) << endl;
    cout << "Single element bytes: " << sizeof(coordinates[0]) << endl;

    int length = sizeof(coordinates) / sizeof(coordinates[0]);
    cout << "Number of elements  : " << length << endl;

    return 0;
}
```

### Output
Total array bytes : 32
Single element bytes: 8
Number of elements  : 4

A `double` occupies 8 bytes on most systems, so a 4-element array of doubles consumes 32 bytes in total.

## Advantages of Arrays

- **Constant Time Access:** Direct access to any element in O(1) time using its index.
- **Cache Efficiency:** Contiguous memory layout benefits from CPU caching mechanisms.
- **Code Organization:** Groups multiple variables of the same type under a single descriptive name.

## Limitations

- **Static Size:** The capacity of a C-style array must be known at compile time and cannot change.
- **Insertion/Deletion Costs:** Inserting or deleting elements in the middle requires manual data shifting.
- **No Bounds Checking:** C++ does not check array boundaries at runtime, which can cause memory corruption if out-of-bound indices are used.

> **Note:** While raw C-style arrays are fully supported in C++, modern C++ codebases prefer `std::array` (for fixed-size arrays) or `std::vector` (for dynamically-sized arrays) from the Standard Template Library (STL). These containers provide safer access methods like `.at()`, which throws an exception on out-of-bounds index access, preventing memory corruption errors. C++ also supports multidimensional arrays in addition to single-dimension structures.

## Summary

An array in C++ is a contiguous collection of same-type elements accessible by zero-based indices in constant time. Once declared, an array's size is fixed. Elements can be initialized explicitly, partially, or implicitly via size inference. Common array operations include accessing, updating, and traversing elements. The total size of an array and the number of elements can be calculated using the `sizeof()` operator. While raw arrays offer high performance and simplicity, modern C++ applications prefer standard container classes like `std::array` or `std::vector` for improved safety and bounds checking.




