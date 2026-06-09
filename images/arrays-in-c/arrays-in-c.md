# Arrays in C++

An array is a collection of elements of the same data type stored in contiguous memory locations. Arrays allow multiple values to be stored under a single variable name, making it easier to manage related data.

Instead of creating separate variables for similar data, an array allows all values to be stored together and accessed using an index.

For example, if we want to store marks of 5 students, creating 5 separate variables would be inconvenient. An array allows us to store all marks under one name.

Some important characteristics of arrays are:

- All elements must have the same data type.
- Elements are stored in contiguous memory locations.
- Array indexing starts from 0.
- Array size is fixed after declaration.
- Elements can be accessed directly using their index.

## Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[5] = {75, 82, 90, 68, 88};

    for(int i = 0; i < 5; i++)
    {
        cout << marks[i] << " ";
    }

    return 0;
}
```

### Output
75 82 90 68 88

# Time Complexity
O(n)

# Space Complexity
O(n)

### 

In this example:

- An integer array named `marks` is created.
- The array contains 5 elements.
- A loop is used to access and print each element.
- The first element is stored at index `0` and the last element at index `4`.

## Why Do We Need Arrays?

Consider storing marks of four students.

Without arrays:

```cpp
int Mohit = 85;
int Akash = 90;
int Hemesh = 78;
int Abhiram = 92;
```

This becomes difficult to manage when the number of students increases.

Using an array:

```cpp
int marks[4] = {85, 90, 78, 92};
```

Now all values are stored under a single name and can be accessed using indices.

Arrays make programs:

- Easier to manage.
- More readable.
- More efficient.
- Suitable for looping operations.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1781017201067-17.png)

## Declaration of an Array

An array is declared by specifying:

1. Data type
2. Array name
3. Array size

### Syntax

```cpp
data_type array_name[size];
```

### Example

```cpp
int marks[5];
```

This creates an array named `marks` capable of storing 5 integer values.

After declaration, memory is reserved for all elements.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1781017231170-18.png)

## Array Initialization

Initialization means assigning values to array elements.

### Example

```cpp
int marks[5] = {75, 82, 90, 68, 88};
```

The values are assigned sequentially:

| Index | Value |
| --- | --- |
| 0 | 75 |
| 1 | 82 |
| 2 | 90 |
| 3 | 68 |
| 4 | 88 |

### Array Without Explicit Size

The compiler can automatically determine the size.

```cpp
int marks[] = {75, 82, 90, 68, 88};
```

The size becomes 5 automatically.

## Partial Initialization

If fewer values are provided than the array size, the remaining elements are automatically initialized to 0.

### Example

```cpp
int marks[5] = {75, 82};
```

Memory representation:

| Index | Value |
| --- | --- |
| 0 | 75 |
| 1 | 82 |
| 2 | 0 |
| 3 | 0 |
| 4 | 0 |

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1781017625171-ChatGPT_Image_Jun_9%2C_2026%2C_08_36_48_PM.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[5] = {75, 82};

    for(int i = 0; i < 5; i++)
    {
        cout << marks[i] << " ";
    }

    return 0;
}
```

### Output
75 82 0 0 0

# Time Complexity
O(n)

# Space Complexity
O(n)

### 

## Initializing All Elements to Zero

All elements can be initialized to zero using:

```cpp
int marks[5] = {0};
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[5] = {0};

    for(int i = 0; i < 5; i++)
    {
        cout << marks[i] << " ";
    }

    return 0;
}
```

### Output
0 0 0 0 0

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1781017653897-21.png)

This method works specifically for zero initialization.

## Accessing Array Elements

Array elements are accessed using their index. Since arrays store elements in contiguous memory locations, any element can be accessed directly using its position.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/arrays-in-c/1781017730050-22.png)

### Syntax

```cpp
array_name[index]
```

### Example

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[] = {75, 82, 90, 68, 88};

    cout << marks[0] << endl;
    cout << marks[3];

    return 0;
}
```

### Output
75
68

# Time Complexity
O(1)

# Space Complexity
O(1)

### 

Here:

- `marks[0]` refers to the first element.
- `marks[3]` refers to the fourth element.

Remember that indexing starts from 0.

## Updating Array Elements

Array elements can be modified after they have been initialized. This process is known as **updating an array element**.

To update an element, we simply access the desired index and assign a new value using the assignment operator (`=`).

### Syntax

```cpp
array_name[index] = newValue;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[] = {75, 82, 90, 68, 88};

    marks[0] = 95;

    cout << marks[0];

    return 0;
}
```

### Output
95

# Time Complexity
O(1)

# Space Complexity
O(1)

### 

The value at index `0` changes from `75` to `95`.

## Traversing an Array

Traversing an array means accessing and processing each element of the array sequentially, one after another. Since array elements are stored in contiguous memory locations and are indexed from `0` to `size - 1`, loops provide an efficient way to visit every element.

Traversal is one of the most common operations performed on arrays. It is used when we need to display elements, calculate sums or averages, find maximum or minimum values, search for specific elements, or perform updates on multiple elements.

Typically, a loop variable starts from index `0` and continues until the last valid index of the array. During each iteration, the current element is accessed using its index and processed as required.

Both traditional `for` loops and range-based `for` loops can be used for array traversal, making it easy to work with all elements in an organized manner.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[] = {75, 82, 90, 68, 88};

    for(int i = 0; i < 5; i++)
    {
        cout << marks[i] << " ";
    }

    return 0;
}
```

### Output
75 82 90 68 88

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

The loop starts from index `0` and continues until the last element.

## Range-Based For Loop

Modern C++ provides a simpler and more readable way to traverse arrays using the **range-based for loop**. Introduced in C++11, this loop automatically visits each element of the array without requiring an index variable.

Unlike a traditional `for` loop, where we manually manage the starting index, ending condition, and increment operation, a range-based for loop directly accesses each element one by one. This makes the code shorter, cleaner, and less prone to indexing errors.

Range-based for loops are especially useful when the index position is not important and we only need to process the elements stored in the array. They improve code readability and reduce boilerplate code while providing the same functionality as a normal traversal loop.

The loop automatically starts from the first element and continues until the last element of the array has been processed.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[] = {75, 82, 90, 68, 88};

    for(int mark : marks)
    {
        cout << mark << " ";
    }

    return 0;
}
```

### Output
75 82 90 68 88

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

This loop automatically accesses every element without using indices.

## Finding the Size of an Array

The `sizeof()` operator can be used to determine the size of an array.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks[] = {75, 82, 90, 68, 88};

    cout << "Size of array: "
         << sizeof(marks) << endl;

    cout << "Size of one element: "
         << sizeof(marks[0]) << endl;

    int length =
        sizeof(marks) / sizeof(marks[0]);

    cout << "Number of elements: "
         << length;

    return 0;
}
```

### Output
Size of array: 20
Size of one element: 4
Number of elements: 5

# Time Complexity
O(1)

# Space Complexity
O(1)

### 

Explanation:

- Total array size = 20 bytes.
- One integer occupies 4 bytes.
- Number of elements = 20 ÷ 4 = 5.

## Array Memory Representation

One of the most important characteristics of an array is that its elements are stored in **contiguous (adjacent) memory locations**. This means that all elements of an array occupy consecutive memory addresses, allowing fast and efficient access to any element using its index.

When an array is created, the compiler allocates a continuous block of memory large enough to store all its elements. The name of the array represents the address of the first element, and the address of any other element can be calculated using its index.

For example, if an integer array contains 5 elements and each integer occupies 4 bytes of memory, then the elements will be stored one after another with a difference of 4 bytes between consecutive elements.

Because of this contiguous memory arrangement:

- Elements can be accessed directly using their indices.
- Accessing any element takes constant time, O(1).
- Arrays are memory efficient and cache friendly.
- Traversal operations become faster due to sequential memory access.

This memory organization is one of the main reasons arrays are widely used as the foundation for many other data structures such as vectors, stacks, queues, and matrices.

Consider:

```cpp
int marks[5] = {75, 82, 90, 68, 88};
```

Memory layout:

```text
Index:   0    1    2    3    4
Value:  75   82   90   68   88
```

Since elements are stored in contiguous memory locations, accessing elements is extremely fast.

## Advantages of Arrays

- Easy storage of multiple values.
- Fast element access using indices.
- Efficient memory utilization.
- Simple traversal using loops.
- Useful for implementing other data structures.

## Limitations of Arrays

- Fixed size after declaration.
- Can store only one data type.
- Insertion and deletion operations are costly.
- Risk of accessing invalid indices.
- Memory may be wasted if array size is larger than required.

## Common Mistake: Array Index Out of Bounds

One of the most common errors while working with arrays is accessing an element using an invalid index. This situation is known as **Array Index Out of Bounds**.

```cpp
int marks[5] = {75, 82, 90, 68, 88};

cout << marks[10];
```

This is invalid because index `10` does not exist.

Valid indices:

```text
0 to 4
```

Accessing an invalid index leads to undefined behavior.

## Summary

Arrays are one of the most fundamental data structures in C++. They store multiple values of the same data type in contiguous memory locations and allow direct access using indices. Arrays are easy to traverse, memory-efficient, and provide fast access to elements. However, their fixed size and inability to grow dynamically are important limitations. Understanding arrays is essential because many advanced data structures such as vectors, stacks, queues, and matrices are built upon the concept of arrays.




