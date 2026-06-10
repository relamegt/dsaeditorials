# Dynamic Memory Allocation in C++ using `new` and `delete`

In C++, memory can be allocated in two ways:

1. **Static Memory Allocation**
2. **Dynamic Memory Allocation**

When variables are declared normally inside functions, memory is allocated automatically on the **stack**. The compiler decides the memory requirements during compilation.

However, there are situations where the amount of memory required is not known until the program is running. In such cases, dynamic memory allocation is used.

Dynamic memory allocation allows a program to request memory during runtime from a memory region called the **heap** (or free store).

C++ provides two special operators for dynamic memory management:

- `new` → Allocates memory dynamically.
- `delete` → Releases dynamically allocated memory.

Dynamic memory allocation gives programmers greater flexibility and control over memory usage.

## Why Do We Need Dynamic Memory Allocation?

Consider a situation where a program asks the user how many marks need to be stored.

### Example Scenario

```text
Enter number of subjects: 5
```

The program cannot know beforehand how many subjects the user will enter.

Since the size is determined during execution, dynamic memory allocation becomes necessary.

Dynamic memory allocation is commonly used in:

- Variable-sized arrays
- Linked Lists
- Stacks
- Queues
- Trees
- Graphs
- Database systems
- Operating systems

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/dynamic-memory-allocation-in-c-using-new-and-delete/1781077613600-144ab91f-4f99-4e68-a54e-c12ab1374e2d.png)

## Stack Memory vs Heap Memory

Understanding the difference between stack and heap memory is important.

| Feature | Stack Memory | Heap Memory |
| --- | --- | --- |
| Allocation | Automatic | Manual |
| Managed By | Compiler | Programmer |
| Size | Limited | Larger |
| Speed | Faster | Slightly Slower |
| Lifetime | Until scope ends | Until deleted |
| Flexibility | Fixed | Dynamic |

### Stack Example

```cpp
int age = 20;
```

Memory is automatically allocated and released.

### Heap Example

```cpp
int* ptr = new int;
```

Memory remains allocated until explicitly deleted.

## The `new` Operator

The `new` operator is used to allocate memory dynamically from the heap.

When memory is successfully allocated:

- Memory block is created.
- Address of the memory block is returned.
- Address is stored in a pointer.

### Syntax

```cpp
pointer = new dataType;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* marks = new int;

    *marks = 95;

    cout << *marks;

    return 0;
}
```

### Output
95

### 

The `new` operator allocates memory for one integer and returns its address.

The pointer `marks` stores that address.

The value is accessed using the dereference operator (`*`).

## Dynamic Initialization using `new`

Values can also be initialized while allocating memory.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* score = new int(100);

    cout << *score;

    return 0;
}
```

### Output
100

### 

Here:

```cpp
new int(100)
```

allocates memory and initializes it with the value 100.

## Understanding Memory Representation

Consider:

### Example Code

```cpp
int* ptr = new int(50);
```

Memory representation:

```text
ptr
 |
 v

+-------+
|  50   |
+-------+
```

The pointer stores the address of the allocated memory block.

The actual value is stored in the heap memory.

## Allocating Arrays Dynamically

The `new` operator can also allocate memory for multiple elements.

### Syntax

```cpp
new dataType[size];
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* marks = new int[5];

    marks[0] = 90;
    marks[1] = 85;
    marks[2] = 88;
    marks[3] = 91;
    marks[4] = 95;

    for(int i = 0; i < 5; i++)
    {
        cout << marks[i] << " ";
    }

    return 0;
}
```

### Output
90 85 88 91 95

### 

The memory for five integers is allocated dynamically.

## Dynamic Array Initialization

Arrays can also be initialized directly.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* numbers = new int[5]
    {
        10, 20, 30, 40, 50
    };

    for(int i = 0; i < 5; i++)
    {
        cout << numbers[i] << " ";
    }

    return 0;
}
```

### Output
10 20 30 40 50

### 

This provides both allocation and initialization in a single statement.

## What Happens When Memory Allocation Fails?

Sometimes sufficient memory may not be available.

In such situations, the `new` operator throws a `std::bad_alloc` exception.

### Example Code

```cpp
int* ptr = new int;
```

If allocation fails:

```text
std::bad_alloc
```

is thrown.

## Using `nothrow`

Instead of throwing an exception, `new` can return `nullptr`.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* ptr = new(nothrow) int;

    if(ptr == nullptr)
    {
        cout << "Memory Allocation Failed";
    }

    return 0;
}
```

### Output

```text
Memory Allocation Failed
```

This approach is useful when exceptions are not desired.

## The `delete` Operator

Memory allocated using `new` remains allocated until it is explicitly released.

The `delete` operator releases memory allocated dynamically.

### Syntax

```cpp
delete pointer;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* marks = new int(90);

    cout << *marks << endl;

    delete marks;

    return 0;
}
```

### Output
90

### 

After `delete`, the memory is returned to the heap and becomes available for future allocations.

## Why is `delete` Important?

If dynamically allocated memory is not released:

- Memory remains occupied.
- Available heap memory decreases.
- Program performance suffers.
- Memory leaks occur.

Therefore every `new` should have a corresponding `delete`.

## Deleting Dynamic Arrays

Arrays allocated using `new[]` must be deallocated using `delete[]`.

### Syntax

```cpp
delete[] pointer;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* marks = new int[3]
    {
        75, 80, 85
    };

    for(int i = 0; i < 3; i++)
    {
        cout << marks[i] << " ";
    }

    delete[] marks;

    return 0;
}
```

### Output
75 80 85

### 

Using ordinary `delete` for arrays leads to undefined behavior.

## Common Dynamic Memory Errors

Dynamic memory management is powerful but can also introduce serious bugs.

## Memory Leak

A memory leak occurs when allocated memory is never released.

### Example Code

```cpp
int* ptr = new int(50);
```

If `delete ptr;` is never executed, memory remains occupied until the program terminates.

### Problem

```text
Memory Allocated
      ↓
Pointer Lost
      ↓
Memory Cannot Be Recovered
```

### Solution

Always release memory using `delete`.

```cpp
delete ptr;
```

Modern C++ recommends using smart pointers to avoid memory leaks.

## Dangling Pointer

A dangling pointer points to memory that has already been deleted.

### Example Code

```cpp
int* ptr = new int(50);

delete ptr;

cout << *ptr;
```

This causes undefined behavior.

Possible results:

- Garbage values
- Program crash
- Segmentation fault

### Solution

Assign `nullptr` after deletion.

```cpp
delete ptr;
ptr = nullptr;
```

Now the pointer clearly indicates that it does not point anywhere.

## Double Deletion

Deleting the same memory block twice causes undefined behavior.

### Example Code

```cpp
int* ptr = new int(50);

delete ptr;
delete ptr;
```

This may crash the program.

### Solution

```cpp
delete ptr;
ptr = nullptr;
```

A `nullptr` can safely be deleted again.

## Mixing `new/delete` with `malloc/free`

C++ supports C-style memory allocation functions.

### C Functions

```cpp
malloc()
calloc()
realloc()
free()
```

These functions should not be mixed with `new` and `delete`.

### Wrong Example

```cpp
int* ptr = new int;

free(ptr);
```

or

```cpp
int* ptr =
    (int*)malloc(sizeof(int));

delete ptr;
```

Both are incorrect.

### Correct Usage

```cpp
new  → delete
```

```cpp
new[] → delete[]
```

```cpp
malloc() → free()
```

Memory allocation and deallocation methods must always match.

## Placement New

Normally, the `new` operator:

1. Allocates memory.
2. Constructs an object.

Placement new separates these operations.

It allows an object to be created inside an already allocated memory block.

### Example Code

```cpp
#include <iostream>
#include <new>
using namespace std;

int main()
{
    char buffer[sizeof(int)];

    int* ptr =
        new(buffer) int(100);

    cout << *ptr;

    return 0;
}
```

### Output
100

### 

Placement new is mainly used in:

- Memory pools
- Custom allocators
- Game engines
- Operating systems
- Embedded systems

It is considered an advanced C++ feature.

## Best Practices for Dynamic Memory Allocation

- Always initialize pointers.
- Always delete dynamically allocated memory.
- Use `delete[]` for arrays.
- Set pointers to `nullptr` after deletion.
- Avoid mixing allocation methods.
- Prefer smart pointers whenever possible.
- Minimize manual memory management.

## Summary

Dynamic memory allocation allows programs to allocate memory during runtime using the heap. The `new` operator allocates memory dynamically and returns its address, while the `delete` operator releases that memory when it is no longer needed. Dynamic memory is essential for variable-sized data structures and runtime flexibility, but improper handling can lead to memory leaks, dangling pointers, and program crashes. Following proper memory management practices ensures efficient and safe C++ programs.




