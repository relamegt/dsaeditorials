# Smart Pointers in C++

A **smart pointer** is a special class in C++ that behaves like a normal pointer but automatically manages dynamically allocated memory. Smart pointers eliminate the need for manual `new` and `delete` operations and help prevent common memory-related problems such as memory leaks, dangling pointers, and resource mismanagement.

Smart pointers are available in the `<memory>` header file and are part of the C++ Standard Library.

## Smart Pointer as a Wrapper Around Raw Pointer

A smart pointer is a class that internally stores a raw pointer and automatically manages the lifetime of the dynamically allocated object.

- **Behaves like a raw pointer**: It supports normal pointer operations and can be dereferenced.
- **Operators supported**: Supports operator overloading for pointer syntax such as `*` (dereference) and `->` (member access).
- **Automatic deallocation**: Releases the associated memory dynamically when ownership ends.
- **No manual delete**: Eliminates the need for manual `delete` statements, preventing memory management errors.

### Conceptual Representation

Raw Pointer
     ↓
Smart Pointer Wrapper
     ↓
Automatic Memory Management

## Why Smart Pointers?

In traditional C++, memory allocated using `new` must be manually released using `delete`.

If the programmer forgets to call `delete`, the memory remains allocated until the program ends, causing a **memory leak**.

### Example: Problem with Raw Pointers

```cpp
#include <iostream>
using namespace std;

int main()
{
    while(true)
    {
        int* ptr = new int(100);

        // Memory is never released
    }

    return 0;
}
```

### Explanation

- Memory is allocated continuously using `new`.
- No `delete` statement is used.
- The allocated memory cannot be reused.
- The program eventually consumes all available memory.

This is one of the major reasons smart pointers were introduced.

## Benefits of Smart Pointers

- Automatic memory management.
- Prevent memory leaks.
- Reduce chances of dangling pointers.
- Improve code safety and reliability.
- Simplify resource management.
- Support RAII (Resource Acquisition Is Initialization).
- Improve exception safety.

## How Smart Pointers Work

A smart pointer stores a raw pointer internally and automatically releases the memory when it is no longer needed.

When the smart pointer goes out of scope:

1. Destructor is called.
2. Memory is automatically deallocated.
3. Resource cleanup occurs safely.

Object Created
      ↓
Smart Pointer Owns Object
      ↓
Pointer Goes Out Of Scope
      ↓
Destructor Executes
      ↓
Memory Released Automatically

### Automatic Memory Release on Scope Exit

When a smart pointer goes out of scope, its destructor automatically releases the managed resource.

- **Destructor execution**: Destructor functions are invoked automatically when a stack-allocated smart pointer goes out of scope.
- **Resource cleanup**: The memory containing the dynamically allocated object is automatically deleted inside the destructor.
- **Memory leak prevention**: Eliminates memory leaks completely since cleanup is guaranteed by the compiler.
- **RAII implementation**: Demonstrates the core idea of RAII by binding heap resource allocation to stack object lifetime.

#### Example

```cpp
{
    unique_ptr<int> ptr =
        make_unique<int>(100);
}
// Memory automatically released here
```

# Types of Smart Pointers

C++ provides four smart pointer types:

| Smart Pointer | Ownership |
| --- | --- |
| auto_ptr (Deprecated) | Single Ownership |
| unique_ptr | Exclusive Ownership |
| shared_ptr | Shared Ownership |
| weak_ptr | Non-Owning Reference |

# 1. auto_ptr (Deprecated)

`auto_ptr` was the first smart pointer introduced in C++.

It automatically released memory when it went out of scope.

However, ownership transfer behavior caused many unexpected bugs.

Because of these issues:

- Deprecated in C++11.
- Removed completely in C++17.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186490545-4ae97c95-c1c6-48db-a84f-9f90961d9714.png)

## Example

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main()
{
    auto_ptr<int> ptr1(new int(50));

    cout << *ptr1 << endl;

    auto_ptr<int> ptr2 = ptr1;

    cout << *ptr2;

    return 0;
}
```

### Output
50
50

### Explanation

When `ptr2` is assigned from `ptr1`, ownership transfers to `ptr2`.

After transfer:

ptr1 → NULL
ptr2 → Owns Object

This behavior was confusing and unsafe.

### Why auto_ptr Was Removed

- Ownership transfers unexpectedly.
- Can cause null pointer access.
- Not compatible with STL containers.
- Unsafe copy semantics.

# 2. unique_ptr

`unique_ptr` provides **exclusive ownership** of an object.

Only one `unique_ptr` can own an object at a time.

It is the most lightweight and efficient smart pointer.

## Real-World Example

Consider an **AlphaKnowledge Course Portal**.

A course dashboard belongs to only one active session at a time.

Similarly, a `unique_ptr` allows only one owner.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186544302-e2de658c-a6cc-4285-9e03-8804617413c7.png)

## Example

```cpp
#include <iostream>
#include <memory>
using namespace std;

class Course
{
public:
    string title;

    Course(string t)
    {
        title = t;
    }

    void display()
    {
        cout << "Course: " << title << endl;
    }
};

int main()
{
    unique_ptr<Course> course1 =
        make_unique<Course>("C++ Programming");

    course1->display();

    unique_ptr<Course> course2;

    course2 = move(course1);

    course2->display();

    return 0;
}
```

### Output
Course: C++ Programming
Course: C++ Programming

### Explanation

Ownership is transferred using `move()`.

Before Move

course1 → Object
course2 → NULL

After Move

course1 → NULL
course2 → Object

### Important Features

- Single ownership.
- Cannot be copied.
- Can be moved.
- Fastest smart pointer.
- Minimal memory overhead.

### Common Functions

| Function | Purpose |
| --- | --- |
| make_unique() | Create unique_ptr |
| release() | Release ownership |
| reset() | Replace managed object |
| get() | Get raw pointer |
| move() | Transfer ownership |

# 3. shared_ptr

A `shared_ptr` allows multiple pointers to share ownership of the same object.

It internally maintains a **reference count**.

Memory is released only when the reference count becomes zero.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186576707-945ffde0-2790-4525-ae74-83c06833fba4.png)

## Real-World Example

Consider an **AlphaKnowledge Online Course**.

Many students can access the same course content.

The course remains available until the last student exits.

This is similar to `shared_ptr`.

## Example

```cpp
#include <iostream>
#include <memory>
using namespace std;

class Course
{
public:
    Course()
    {
        cout << "Course Created" << endl;
    }

    ~Course()
    {
        cout << "Course Deleted" << endl;
    }
};

int main()
{
    shared_ptr<Course> student1 =
        make_shared<Course>();

    shared_ptr<Course> student2 = student1;

    cout << "Reference Count: "
         << student1.use_count();

    return 0;
}
```

### Output
Course Created
Reference Count: 2
Course Deleted

### Explanation

student1 → Course
student2 → Course

Reference Count = 2

Memory is deleted only when both pointers go out of scope.

### Common Functions

| Function | Purpose |
| --- | --- |
| make_shared() | Create shared_ptr |
| use_count() | Returns reference count |
| reset() | Release ownership |
| get() | Returns raw pointer |
| swap() | Exchange ownership |

### Advantages

- Multiple ownership.
- Automatic reference counting.
- Safe memory management.

### Disadvantages

- Slightly slower than unique_ptr.
- Additional memory required for reference count.

# 4. weak_ptr

A `weak_ptr` is a smart pointer that does not own the object.

It only observes an object managed by a `shared_ptr`.

It does not increase the reference count.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186615309-e209a90b-2dfe-4c67-b5e6-e66dcd2fde71.png)

## Why Do We Need weak_ptr?

### Circular Dependency Problem

Suppose two objects own each other using shared pointers.

Object A → Object B
Object B → Object A

Reference count never reaches zero.

As a result:

Memory Never Released
↓
Memory Leak

This problem is called **Circular Dependency**.

# Circular Ownership and Design Issues

Circular ownership is generally considered a design problem.

- **Reference Count Obstruction**: Two objects holding strong `shared_ptr` references to each other will keep each other's reference count at 1 or higher.
- **Leak Generation**: Since the reference count never drops to zero, the destructors are never invoked, causing memory leaks.
- **Cycle Breaking**: `weak_ptr` resolves this by referencing an object without taking ownership (not increasing the reference count), breaking the cycle.
- **Careful Ownership Design**: Designing ownership relationships cleanly is a critical task in large applications to manage object lifecycles safely.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186663567-9c72ec4e-a0d1-447d-a5d2-d52fb95bbabf.png)

### Circular Dependency (The Problem)

Reference Count Never Reaches Zero

### Breaking the Cycle (The Solution)

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/smart-pointers-in-c/1781186697228-9c72ec4e-a0d1-447d-a5d2-d52fb95bbabf.png)

shared_ptr
Object A ───► Object B

weak_ptr
Object B ───► Object A

Reference Count Can Reach Zero

## Example

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main()
{
    shared_ptr<int> ptr1 =
        make_shared<int>(100);

    weak_ptr<int> ptr2(ptr1);

    cout << "Reference Count: "
         << ptr1.use_count();

    return 0;
}
```

### Output
Reference Count: 1

### Explanation

Even though `ptr2` refers to the object:

shared_ptr count = 1

because weak pointers do not own memory.

### Accessing weak_ptr

A weak pointer must be converted into a shared pointer using `lock()`.

```cpp
shared_ptr<int> temp = ptr.lock();
```

# Checking weak_ptr Validity

A weak pointer may refer to an object that has already been destroyed, so we must verify its validity before dereferencing it.

```cpp
if(auto temp = ptr.lock())
{
    cout << *temp;
}
else
{
    cout << "Object No Longer Exists";
}
```

### Explanation

- **lock() Operation**: The `lock()` method attempts to create a temporary `shared_ptr` from the `weak_ptr`.
- **Alive Object**: If the underlying object is still alive, `lock()` returns a valid `shared_ptr`, increments the reference count temporarily, and enters the `if` block.
- **Destroyed Object**: If the object has already been destroyed, `lock()` returns an empty `shared_ptr` (evaluates to `false`), bypassing the block.

### Important Functions

| Function | Purpose |
| --- | --- |
| lock() | Convert to shared_ptr |
| expired() | Check if object exists |
| reset() | Remove reference |
| use_count() | View shared count |

#### Additional Note on weak_ptr::expired()

The `expired()` function checks if the referenced object is still alive.

- **Returns true**: If the managed object has already been destroyed.
- **Returns false**: If the object is still alive in memory.

```cpp
if(ptr.expired())
{
    cout << "Object Destroyed";
}
```

**When is it useful?**
It is useful for a quick check when you only need to know whether the object is still alive (e.g. cache validation or debugging) without needing to acquire ownership of it. Note that `expired()` is not thread-safe for making access decisions, so `lock()` should be used instead when you actually need to call methods on the target object.

# Memory Problems Solved by Smart Pointers

## Memory Leak

Occurs when memory is allocated but never released.

```cpp
int* ptr = new int(10);
```

No delete:

```cpp
delete ptr;
```

Result:
Memory Leak
Smart pointers automatically release memory.

---

## Dangling Pointer

Occurs when a pointer references memory that has already been freed.

```cpp
int* ptr = new int(10);

delete ptr;

cout << *ptr;
```

Result:
Undefined Behavior
Smart pointers prevent this problem.

## Wild Pointer

A pointer that is not initialized.

```cpp
int* ptr;
```

Contains garbage address.

Smart pointers are initialized safely.

# RAII and Smart Pointers

Smart pointers are based on the RAII principle.

## RAII

**Resource Acquisition Is Initialization**

Meaning:

- Resource acquired in constructor.
- Resource released in destructor.

Example:

```cpp
{
    unique_ptr<int> ptr =
        make_unique<int>(50);

} // Automatically deleted here
```

When the block ends:
Destructor Called
↓
Memory Released

# make_unique() vs new

### Traditional Method

```cpp
unique_ptr<int> ptr(
    new int(50));
```

### Recommended Method

```cpp
auto ptr =
    make_unique<int>(50);
```

### Why make_unique()?

- Safer.
- Cleaner syntax.
- Better exception handling.
- Recommended by modern C++ standards.

# make_shared() vs new

### Traditional

```cpp
shared_ptr<int> ptr(
    new int(100));
```

### Recommended

```cpp
auto ptr =
    make_shared<int>(100);
```

### Advantages

- Faster allocation.
- Better memory efficiency.
- Cleaner code.

# Smart Pointer Comparison Table

| Feature | unique_ptr | shared_ptr | weak_ptr |
| --- | --- | --- | --- |
| Ownership | Single | Shared | No Ownership |
| Copy Allowed | No | Yes | Yes |
| Move Allowed | Yes | Yes | Yes |
| Reference Counting | No | Yes | No |
| Automatic Deletion | Yes | Yes | No |
| Memory Overhead | Very Low | Moderate | Very Low |
| Best Use Case | Exclusive ownership | Shared resources | Breaking circular dependencies |

# Raw Pointer vs Smart Pointer

| Raw Pointer | Smart Pointer |
| --- | --- |
| Manual memory management | Automatic memory management |
| Uses new and delete | No manual delete required |
| Memory leaks possible | Prevents memory leaks |
| Dangling pointers possible | Much safer |
| Error-prone | Reliable |
| No ownership tracking | Ownership management built-in |
| Difficult in large projects | Ideal for modern applications |

# Best Practices

- Prefer `unique_ptr` whenever possible.
- Use `shared_ptr` only when multiple ownership is required.
- Use `weak_ptr` to avoid circular dependencies.
- Avoid raw `new` and `delete`.
- Use `make_unique()` and `make_shared()`.
- Follow RAII principles.
- Never use deprecated `auto_ptr`.

# Key Takeaways

- **Wrapper Design**: A smart pointer is a class that wraps a raw pointer to manage the lifetime of dynamically allocated objects.
- **Automatic Scope Cleanup**: Heap resource cleanup is bound to stack object scope; destructors automatically release resources on scope exit (RAII).
- **Exclusive vs Shared Ownership**: `unique_ptr` provides single ownership, while `shared_ptr` uses reference counting to share ownership.
- **Non-Owning weak_ptr**: `weak_ptr` acts as a non-owning observer to reference shared objects without increasing the reference count.
- **Cycle Breaking**: Circular ownership is a design problem that creates memory leaks; `weak_ptr` is used to break these ownership cycles.
- **Validity Verification**: We must check a `weak_ptr`'s validity using `lock()` to acquire safe shared access or check status using `expired()`.
- **Resource Safety**: Smart pointers resolve raw pointer issues such as memory leaks, dangling pointers, and uninitialized wild pointers.
- **Modern Standard**: Modern C++ development recommends using smart pointers and helper functions like `make_unique()` and `make_shared()`.

# Summary

A **smart pointer** in C++ is a template class that wraps a raw pointer to automate dynamic memory management based on the RAII (Resource Acquisition Is Initialization) principle, releasing heap resources automatically via its destructor on scope exit to prevent memory leaks, wild pointers, and dangling pointers. Modern C++ provides `unique_ptr` for exclusive ownership, `shared_ptr` for shared resource management using reference counting, and `weak_ptr` as a non-owning observer designed to break circular dependency ownership cycles. To safely interact with a `weak_ptr`, developers must verify its validity by checking if it has `expired()` or by calling `lock()` to temporarily acquire a strong `shared_ptr` referencing the alive object, making modern smart pointers and their helper factory functions a much safer and highly recommended practice over traditional manual raw memory allocation.




