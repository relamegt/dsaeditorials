# C++ Pointers

A pointer in C++ is a variable that stores the memory address of another variable. A normal variable directly stores a value such as `10`, `3.14`, or `'A'`, but a pointer stores the location in memory where that value exists. This feature makes pointers one of the most important and powerful parts of C++ because they allow direct access to memory.

Pointers are heavily used in dynamic memory allocation, linked data structures, arrays, function handling, and system-level programming. They give more control to the programmer, but that control also comes with responsibility. If pointers are used incorrectly, they can cause undefined behavior, crashes, or memory bugs.

To understand pointers clearly, remember these three ideas:

- A variable stores a value.
- A pointer stores the address of a variable.
- Dereferencing a pointer accesses the value stored at that address.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-pointers/1781022024718-ChatGPT_Image_Jun_9%2C_2026%2C_09_49_47_PM.png)

## Basic Pointer Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int marks = 88;
    int* ptr = &marks;

    cout << "marks = " << marks << endl;
    cout << "address of marks = " << &marks << endl;
    cout << "ptr stores = " << ptr << endl;
    cout << "value pointed by ptr = " << *ptr << endl;

    return 0;
}
```

### Output
marks = 88
address of marks = 0x7ffee3b5c8ac
ptr stores = 0x7ffee3b5c8ac
value pointed by ptr = 88

### **Explanation**

In this example, `marks` is a normal integer variable that stores the value `88`. The pointer `ptr` is declared as `int*`, which means it can only store the address of an integer variable. The expression `&marks` gives the memory address of `marks`, and that address is stored inside `ptr`.

When `ptr` is printed directly, the output is a memory address. When `*ptr*` *is printed, C++ goes to the memory location stored in `ptr` and reads the value present there. That is why* `ptr` prints `88`.

The exact address shown in the output will be different on every system and every run. What matters is that the address printed by `&marks` and `ptr` is the same, because `ptr` is storing the address of `marks`.

## Declaring a Pointer

The general syntax for declaring a pointer is:

```cpp
data_type* pointer_name;
```

Example:

```cpp
char* chPtr;
```

### Explanation

This declaration means `chPtr` is a pointer that can store the address of a `char` variable. The type of the pointer is very important because C++ needs to know what kind of data exists at the memory address.

For example:

- `int*` points to an integer
- `double*` points to a double
- `char*` points to a character

The type helps the compiler understand how many bytes to read when the pointer is dereferenced.

## Assigning an Address to a Pointer

A pointer usually gets a value using the address-of operator `&`.

```cpp
#include <iostream>
using namespace std;

int main() {
    double price = 149.5;
    double* p = &price;

    cout << "price = " << price << endl;
    cout << "address stored in p = " << p << endl;

    return 0;
}
```

### Output
price = 149.5
address stored in p = 0x7ffee3b5c8a0

### **Explanation**

The variable `price` stores a decimal value. The pointer `p` is declared as `double*`, so it is allowed to store the address of a `double` variable. The expression `&price` gives the address of `price`, and this address is assigned to `p`.

This is called pointer initialization. It is a good habit to initialize pointers at the moment they are declared, either with a valid address or with `nullptr`.

### Type Matching Rule

The pointer type and variable type must match.

Correct:

```cpp
int value = 7;
int* p = &value;
```

Incorrect:

```cpp
int value = 7;
float* p = &value;
```

The incorrect version causes a type mismatch because `p` expects the address of a `float`, but `value` is an `int`.

## Dereferencing a Pointer

Dereferencing means accessing the value stored at the memory address held by a pointer. The dereference operator is `*`.

```cpp
#include <iostream>
using namespace std;

int main() {
    int temperature = 31;
    int* ptr = &temperature;

    cout << "Address stored in ptr: " << ptr << endl;
    cout << "Value at that address: " << *ptr << endl;

    return 0;
}
```

### Possible Output

```text
Address stored in ptr: 0x7ffee3b5c89c
Value at that address: 31
```

### Explanation

This example clearly shows the difference between `ptr` and `*ptr`.

- `ptr` gives the address stored inside the pointer.
- `*ptr` gives the value stored at that address.

So if the pointer stores the address of `temperature`, dereferencing it gives the actual value of `temperature`. This is one of the most important ideas in pointers.

## Modifying a Variable Using a Pointer

One major advantage of pointers is that they allow direct modification of the original variable through its memory address.

```cpp
#include <iostream>
using namespace std;

int main() {
    int balance = 500;
    int* ptr = &balance;

    *ptr = 900;

    cout << "balance = " << balance << endl;
    cout << "*ptr = " << *ptr << endl;

    return 0;
}
```

### Output
balance = 900
*ptr = 900

### **Explanation**

Initially, `balance` contains `500`. Since `ptr` stores the address of `balance`, changing `*ptr` means changing the value present at `balance`'s memory location. That is why the original variable `balance` also becomes `900`.

This ability is very useful when functions need to modify original values without returning them.

## Changing the Address Stored in a Pointer

A pointer can later be updated to point to another variable of the same type.

```cpp
#include <iostream>
using namespace std;

int main() {
    int first = 11;
    int second = 22;

    int* ptr = &first;
    cout << "Initially: " << *ptr << endl;

    ptr = &second;
    cout << "After change: " << *ptr << endl;

    return 0;
}
```

### Output
Initially: 11
After change: 22

### **Explanation**

At first, `ptr` contains the address of `first`, so dereferencing it gives `11`. Later, the pointer is assigned the address of `second`, so dereferencing it now gives `22`.

This shows that a pointer is not permanently attached to one variable. It can be redirected to another memory location as long as the data type matches.

## Size of a Pointer

The size of a pointer depends mainly on system architecture, not on the type of data it points to.

- On a 64-bit system, pointers are usually 8 bytes.
- On a 32-bit system, pointers are usually 4 bytes.

```cpp
#include <iostream>
using namespace std;

int main() {
    int* p1;
    long long* p2;
    char* p3;

    cout << sizeof(p1) << endl;
    cout << sizeof(p2) << endl;
    cout << sizeof(p3) << endl;

    return 0;
}
```

### Typical Output on a 64-bit System

```text
8
8
8
```

### Explanation

Although `p1`, `p2`, and `p3` point to different data types, they all store addresses. Since an address has a fixed size on a given machine, all these pointers usually occupy the same number of bytes.

The data type still matters for dereferencing and pointer arithmetic, but not for the pointer's own storage size.

## Special Pointer Cases

### 1. Uninitialized Pointer

```cpp
int* ptr;
```

### Explanation

This pointer has not been given any valid address. It contains a garbage value, meaning a random memory address. Such a pointer is dangerous because dereferencing it may crash the program or produce unpredictable results.

This kind of pointer is often called a wild pointer. A better practice is to initialize the pointer immediately.

Safe version:

```cpp
int* ptr = nullptr;
```

### 2. Null Pointer

A null pointer intentionally points to nothing.

```cpp
#include <iostream>
using namespace std;

int main() {
    int* ptr = nullptr;

    if (ptr == nullptr) {
        cout << "ptr is not pointing to any valid object" << endl;
    }

    return 0;
}
```

### Output
ptr is not pointing to any valid object

### **Explanation**

`nullptr` is the modern C++ way to represent an empty pointer. It is much safer than leaving a pointer uninitialized. Before dereferencing a pointer, programs often check whether it is `nullptr`.

A null pointer does not point to usable memory, so dereferencing it is invalid.

### 3. Void Pointer

A `void*` pointer can store the address of any data type.

```cpp
#include <iostream>
using namespace std;

int main() {
    float pi = 3.14f;
    void* ptr = &pi;

    cout << *(static_cast<float*>(ptr)) << endl;

    return 0;
}
```

### Output
3.14

### **Explanation**

A `void` *is called a generic pointer because it can hold the address of any type. However, the compiler does not know what kind of data exists at that address. Because of this, a `void`* cannot be dereferenced directly.

Before using the value, the pointer must be converted back to the correct type using type casting. In this example, `ptr` is cast to `float*`, and then dereferenced.

### 4. Dangling Pointer

A dangling pointer points to memory that is no longer valid.

```cpp
#include <iostream>
using namespace std;

int* createPointer() {
    int localValue = 50;
    return &localValue;
}

int main() {
    int* ptr = createPointer();

    // Using *ptr here is unsafe
    return 0;
}
```

### Explanation

`localValue` is created inside the function `createPointer()`. Once the function ends, that variable is destroyed because it was a local variable. Returning its address means the pointer in `main()` now points to memory that is no longer valid.

This is called a dangling pointer. Accessing such memory leads to undefined behavior.

## Pointer Arithmetic

C++ allows certain arithmetic operations on pointers, especially when they point to array elements.

Common operations include:

- Incrementing a pointer
- Decrementing a pointer
- Adding an integer to a pointer
- Subtracting an integer from a pointer
- Subtracting two pointers of the same type
- Comparing pointers

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {4, 8, 12, 16};
    int* ptr = arr;

    cout << *ptr << endl;
    ptr++;
    cout << *ptr << endl;

    return 0;
}
```

### Output
4
8

### **Explanation**

In C++, the array name often behaves like a pointer to the first element. So `ptr = arr` makes `ptr` point to `arr[0]`.

When `ptr++` is used, the pointer does not simply move by 1 byte. Instead, it moves to the next integer location in memory. Since `ptr` is an `int*`, C++ automatically moves it by `sizeof(int)` bytes. That is why dereferencing it after increment gives the next array element.

## Pointer to Pointer

A pointer can store the address of another pointer. This is called a pointer to pointer or double pointer.

```cpp
#include <iostream>
using namespace std;

int main() {
    int number = 64;
    int* ptr = &number;
    int** dptr = &ptr;

    cout << *ptr << endl;
    cout << **dptr << endl;

    return 0;
}
```

### Output
64
64

### **Explanation**

Here is the chain of relationships:

- `number` stores `64`
- `ptr` stores the address of `number`
- `dptr` stores the address of `ptr`

So:

- `*ptr` gives the value of `number`
- `*dptr` gives `ptr`
- `dptr` gives the value stored in `number`

Double pointers are useful in advanced memory management, dynamic 2D arrays, and functions that need to modify pointers.

## Function Pointer

A function pointer stores the address of a function instead of the address of a normal variable.

```cpp
#include <iostream>
using namespace std;

int multiply(int a, int b) {
    return a * b;
}

int main() {
    int (*funcPtr)(int, int) = multiply;

    cout << funcPtr(3, 5) << endl;

    return 0;
}
```

### Output
15

### **Explanation**

The declaration `int (*funcPtr)(int, int)` means `funcPtr` is a pointer to a function that takes two integers and returns an integer. The function pointer is assigned the address of `multiply`.

When `funcPtr(3, 5)` is called, the function runs indirectly through the pointer. Function pointers are useful in callbacks, event handlers, and flexible program designs.

## Smart Pointers

Smart pointers are safer modern alternatives to raw pointers in many cases. They automatically manage memory and reduce problems like memory leaks.

Main smart pointer types:

- `unique_ptr` for single ownership
- `shared_ptr` for shared ownership
- `weak_ptr` for observing shared objects without owning them

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main() {
    unique_ptr<int> ptr = make_unique<int>(100);
    cout << *ptr << endl;

    return 0;
}
```

### Output
100

### **Explanation**

In this example, `ptr` owns an integer dynamically allocated in memory. Unlike raw pointers created with `new`, this memory does not need manual `delete`. When `ptr` goes out of scope, the memory is automatically released.

This makes smart pointers much safer and more suitable for modern C++ development.

## Pointer vs Reference

Pointers and references both allow access to another variable, but they are not the same.

| Feature | Pointer | Reference |
| --- | --- | --- |
| Can be null | Yes, using nullptr | No |
| Can be reassigned | Yes | No |
| Needs dereferencing | Yes, with * | No |
| Initialization required immediately | No | Yes |

Reference example:

```cpp
#include <iostream>
using namespace std;

int main() {
    int value = 30;
    int& ref = value;

    ref = 45;
    cout << value << endl;

    return 0;
}
```

### Output
45

### **Explanation**

A reference is another name for an existing variable. It does not store a separate address the way a pointer does. Once a reference is bound to a variable, it cannot be changed to refer to another variable.

Pointers are more flexible, but references are often easier and safer when nullability and reassignment are not needed.

## Practical Uses of Pointers

### 1. Dynamic Memory Allocation

Pointers are required when memory is allocated during runtime.

```cpp
#include <iostream>
using namespace std;

int main() {
    int* ptr = new int(75);

    cout << *ptr << endl;

    delete ptr;
    ptr = nullptr;

    return 0;
}
```

### Output
75

### **Explanation**

The `new` operator allocates memory while the program is running and returns its address. That address must be stored in a pointer. After the memory is no longer needed, `delete` is used to free it.

Setting the pointer to `nullptr` after deletion is a good habit because it avoids accidentally using an invalid address.

### 2. Building Data Structures

Pointers are essential for linked lists, trees, graphs, and other dynamic structures.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

int main() {
    Node first{1, nullptr};
    Node second{2, nullptr};

    first.next = &second;

    cout << first.data << " -> " << first.next->data << endl;

    return 0;
}
```

### Output
1 -> 2

### **Explanation**

Each node stores data and the address of the next node. This is how linked structures are formed. Instead of placing elements next to each other like arrays, data items are connected through addresses.

Pointers make these connections possible.

### 3. Passing Arguments for Modification

Pointers allow functions to modify original variables by receiving their addresses.

```cpp
#include <iostream>
using namespace std;

void increase(int* value) {
    *value = *value + 10;
}

int main() {
    int num = 5;
    increase(&num);

    cout << num << endl;

    return 0;
}
```

### Output
15

### **Explanation**

The function `increase()` receives the address of `num`. Inside the function, dereferencing that pointer gives direct access to the original variable. So the function changes the original value rather than a copy.

This is one of the classic uses of pointers in C++.

## Common Mistakes to Avoid

- Dereferencing an uninitialized pointer
- Dereferencing a null pointer
- Using a pointer after deleting memory
- Returning the address of a local variable
- Forgetting to free dynamically allocated memory
- Using the wrong pointer type

These mistakes can lead to segmentation faults, memory corruption, or hard-to-debug errors.

## Summary

Pointers are variables that store memory addresses. They are used to access and manipulate data indirectly, which makes them extremely useful in low-level programming, dynamic memory allocation, and data structures.

The most important ideas to remember are:

- `&` gives the address of a variable.
- A pointer stores that address.
- `*` dereferences the pointer and accesses the value at that address.
- Pointer types must match the data they point to.
- Safe pointer handling is essential to avoid bugs like dangling pointers and invalid memory access.

Once pointers are understood properly, many advanced C++ topics such as dynamic memory, linked lists, trees, function pointers, and smart pointers become much easier to learn.




