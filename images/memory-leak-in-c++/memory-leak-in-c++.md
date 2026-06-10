# Memory Leak in C++

A **memory leak** occurs when dynamically allocated memory is not released after it is no longer needed. As a result, the allocated memory remains occupied and unavailable for reuse, even though the program no longer has access to it.

Memory leaks are one of the most common problems in C++ programs that use dynamic memory allocation. Since C++ does not provide automatic garbage collection like some other programming languages, programmers are responsible for manually managing memory using `new` and `delete`.

If allocated memory is not properly deallocated, the program gradually consumes more memory, which can lead to performance degradation, resource exhaustion, and application crashes.

## Why Do Memory Leaks Occur?

When memory is allocated dynamically using the `new` operator, it remains allocated until it is explicitly released using the `delete` operator.

If the program loses access to the allocated memory before releasing it, that memory becomes unreachable. Since there is no way to access it again, it cannot be freed, resulting in a memory leak.

### Example Code

```cpp
#include <iostream>
using namespace std;

void storeMarks()
{
    int* marks = new int[5];

    marks[0] = 90;
    marks[1] = 85;
    marks[2] = 88;
    marks[3] = 92;
    marks[4] = 95;

    return;
}

int main()
{
    storeMarks();

    return 0;
}
```

### Explanation

In this example:

- Memory for an array of 5 integers is allocated dynamically.
- The pointer `marks` stores the address of that memory.
- When the function ends, the local pointer variable is destroyed.
- The dynamically allocated memory still exists in the heap.
- Since the address is lost, the memory can no longer be accessed or released.

This memory remains occupied until the program terminates, creating a memory leak.

## Understanding Memory Leak Visually

Consider the following allocation:

```cpp
int* ptr = new int(100);
```

Memory representation:

```text
ptr
 |
 v

+--------+
|  100   |
+--------+
```

Now suppose the pointer is lost:

```cpp
ptr = nullptr;
```

Memory representation:

```text
ptr --> nullptr

+--------+
|  100   |
+--------+
```

The memory block still exists, but no pointer refers to it anymore.

Since the address is lost, the memory cannot be released.

This is a memory leak.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/memory-leak-in-c/1781077790091-ChatGPT_Image_Jun_10%2C_2026%2C_01_19_15_PM.png)

## Common Causes of Memory Leaks

### Forgetting to Use `delete`

The most common reason for memory leaks is allocating memory with `new` but never releasing it.

### Example Code

```cpp
int* age = new int(20);

// Forgot to delete memory
```

The memory remains allocated until the program ends.

### Overwriting a Pointer

A memory leak can occur if a pointer is assigned a new address before releasing the old memory.

### Example Code

```cpp
int* ptr = new int(50);

ptr = new int(100);
```

The address of the first memory block is lost permanently.

Only the second allocation remains accessible.

### Returning Before Deallocation

Sometimes a function returns before releasing allocated memory.

### Example Code

```cpp
void processData()
{
    int* data = new int[10];

    return;

    delete[] data;
}
```

The `delete` statement is never executed.

### Exception Handling Issues

Memory leaks may occur if an exception is thrown before memory is released.

### Example Code

```cpp
int* ptr = new int[100];

throw "Error";
```

Since program control jumps immediately, memory is never released.

Modern C++ solves this problem using smart pointers.

## Consequences of Memory Leaks

Memory leaks can cause serious problems, especially in large applications.

### Reduced Performance

Leaked memory cannot be reused.

As more memory becomes unavailable, the operating system has less free memory to work with.

This can slow down both the application and the entire system.

### Increased Memory Consumption

Every leaked block increases the program's memory usage.

Over time, memory consumption continues to grow unnecessarily.

### Program Instability

When memory becomes scarce, programs may begin to behave unpredictably.

Possible symptoms include:

- Slow execution
- Unexpected behavior
- Random crashes

### Resource Exhaustion

Memory is a limited resource.

Large memory leaks may eventually consume all available RAM.

When this happens, new memory allocations start failing.

### Problems in Long-Running Applications

Memory leaks are particularly dangerous in applications that run continuously.

Examples include:

- Web servers
- Database servers
- Operating systems
- Background services
- Network applications

Even a small leak can become a major issue after days or weeks of continuous execution.

## Detecting Memory Leaks

Finding memory leaks manually can be difficult, especially in large programs.

Developers often use specialized debugging tools to detect leaks.

Popular tools include:

### Valgrind

Valgrind is a powerful memory debugging tool available on Linux systems.

It can:

- Detect memory leaks
- Identify invalid memory access
- Detect use-after-free errors
- Analyze memory usage

### AddressSanitizer (ASan)

AddressSanitizer is a compiler-based memory debugging tool.

It helps detect:

- Memory leaks
- Buffer overflows
- Dangling pointers
- Heap corruption

### IDE Debugging Tools

Many modern IDEs provide built-in memory analysis tools.

Examples include:

- Visual Studio Memory Diagnostics
- CLion Memory Profiler
- Xcode Instruments

## How to Prevent Memory Leaks?

Preventing memory leaks is much easier than fixing them later.

Following good programming practices can significantly reduce memory-related problems.

### Always Pair `new` with `delete`

Every memory allocation should have a matching deallocation.

### Example Code

```cpp
int* score = new int(95);

delete score;
```

This is the most basic rule of dynamic memory management.

### Use `delete[]` for Arrays

Arrays allocated using `new[]` must be released using `delete[]`.

### Example Code

```cpp
int* marks = new int[5];

delete[] marks;
```

Using ordinary `delete` on arrays leads to undefined behavior.

### Set Pointers to `nullptr`

After deleting memory, assign `nullptr` to the pointer.

### Example Code

```cpp
delete ptr;
ptr = nullptr;
```

This prevents accidental access to invalid memory.

### Use Smart Pointers

Modern C++ strongly recommends smart pointers instead of raw pointers.

Smart pointers automatically release memory when objects go out of scope.

Common smart pointers include:

- `unique_ptr`
- `shared_ptr`
- `weak_ptr`

### Example Code

```cpp
#include <memory>

unique_ptr<int> ptr =
    make_unique<int>(100);
```

Memory is automatically released when the smart pointer is destroyed.

### Apply RAII Principle

RAII stands for:

```text
Resource Acquisition Is Initialization
```

The idea is to tie resource management to object lifetime.

When the object is destroyed, its resources are automatically released.

This technique greatly reduces memory leaks.

## Memory Leak vs Dangling Pointer

Many beginners confuse memory leaks and dangling pointers.

| Feature | Memory Leak | Dangling Pointer |
| --- | --- | --- |
| Memory Exists | Yes | No |
| Memory Accessible | No | Pointer Exists |
| Cause | Lost Address | Deleted Memory |
| Result | Wasted Memory | Undefined Behavior |

### Memory Leak Example

```cpp
int* ptr = new int(50);

ptr = nullptr;
```

Memory exists but cannot be accessed.

### Dangling Pointer Example

```cpp
int* ptr = new int(50);

delete ptr;
```

Pointer still exists but points to invalid memory.

## Real-World Example

Imagine renting a hotel room.

- Booking a room is like allocating memory.
- Checking out is like releasing memory.
- Forgetting to check out means the room remains reserved even though nobody uses it.

Other guests cannot use that room.

Similarly, leaked memory remains occupied even though the program no longer needs it.

## Best Practices

- Always initialize pointers.
- Release memory as soon as it is no longer needed.
- Use `delete` for single objects.
- Use `delete[]` for arrays.
- Set pointers to `nullptr` after deletion.
- Avoid excessive use of raw pointers.
- Prefer smart pointers whenever possible.
- Use memory analysis tools regularly.
- Follow RAII principles.

# Summary

A memory leak occurs when dynamically allocated memory is not released after it is no longer required. Since C++ does not provide automatic garbage collection, programmers must manually manage memory using `new` and `delete`. Memory leaks can lead to increased memory consumption, reduced performance, resource exhaustion, and application crashes, especially in long-running programs. They commonly occur due to forgotten deallocation, overwritten pointers, early function returns, or exception handling issues. Modern C++ minimizes memory leaks through smart pointers, RAII principles, and memory debugging tools such as Valgrind and AddressSanitizer.




