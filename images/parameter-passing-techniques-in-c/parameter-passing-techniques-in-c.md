# Parameter Passing Techniques in C++

When a function is called, data is often passed to it so that it can perform operations using that data. The process of transferring data from the calling function to the called function is known as **parameter passing**.

Parameter passing is an important concept because it determines whether changes made inside a function affect the original variables or only temporary copies of them.

Before learning the different parameter-passing techniques, it is important to understand two commonly used terms.

## Formal Parameters and Actual Parameters

**Formal Parameters** are the variables declared in the function definition. They act as placeholders that receive values when the function is called.

```cpp
void display(int num)
```

In the above example, `num` is a formal parameter.

**Actual Parameters (Arguments)** are the values or variables passed during the function call.

```cpp
display(10);
```

Here, `10` is an actual parameter or argument.

When a function is invoked, the actual parameters are transferred to the formal parameters using one of the parameter-passing techniques provided by C++.

## Parameter Passing Methods in C++

C++ supports three main techniques for passing data to functions:

1. Pass by Value
2. Pass by Reference
3. Pass by Pointer

Each method behaves differently and has its own advantages and use cases.

| Method | Original Variable Modified? | Additional Copy Created? |
| --- | --- | --- |
| Pass by Value | No | Yes |
| Pass by Reference | Yes | No |
| Pass by Pointer | Yes | No |

## 1. Pass by Value

In pass-by-value, a copy of the original variable is created and passed to the function. The function works with this copy rather than the original variable.

Since the function receives a separate copy, any modifications made inside the function affect only the copied value and not the original variable.

This technique is easy to understand and prevents accidental modification of the caller's data.

### Example Code

```cpp
#include <iostream>
using namespace std;

void changeValue(int num)
{
    num = 50;
}

int main()
{
    int value = 10;

    changeValue(value);

    cout << value;

    return 0;
}
```

### Output
10

### 

The output remains `10` because the function modifies only the copied value. The original variable `value` remains unchanged.

When the function is called:

```cpp
changeValue(value);
```

the compiler internally creates a copy of `value` and assigns it to `num`. Therefore, any changes made to `num` do not affect `value`.

### Advantages

- Easy to implement.
- Original data remains safe.
- Suitable for primitive data types such as integers and characters.

### Disadvantages

- Extra memory is required for copying.
- Less efficient for large objects, arrays, and structures.

## 2. Pass by Reference

In pass-by-reference, the function receives a reference to the original variable instead of a copy.

A reference acts as another name for the same memory location. Therefore, modifications made inside the function directly affect the original variable.

This approach avoids unnecessary copying and is widely used in modern C++ programming.

### Example Code

```cpp
#include <iostream>
using namespace std;

void changeValue(int &num)
{
    num = 50;
}

int main()
{
    int value = 10;

    changeValue(value);

    cout << value;

    return 0;
}
```

### Output
50

### 

The output becomes `50` because `num` is a reference to `value`. Both names refer to the same memory location.

When the function executes:

```cpp
num = 50;
```

it directly modifies the original variable `value`.

The ampersand (`&`) in the parameter declaration indicates that the parameter is being passed by reference.

```cpp
void changeValue(int &num)
```

### Advantages

- No copying overhead.
- Efficient for large data structures.
- Allows direct modification of original data.

### Disadvantages

- Original data can be changed unintentionally.
- Requires careful handling.

## 3. Pass by Pointer

Pass-by-pointer is similar to pass-by-reference because it allows the function to modify the original variable.

However, instead of passing the variable itself, the memory address of the variable is passed to the function.

The function then uses the address to access and modify the original value.

### Example Code

```cpp
#include <iostream>
using namespace std;

void changeValue(int *num)
{
    *num = 50;
}

int main()
{
    int value = 10;

    changeValue(&value);

    cout << value;

    return 0;
}
```

### Output
50

### 

The output becomes `50` because the function receives the memory address of `value`.

The statement:

```cpp
&value
```

returns the address of the variable and passes it to the function.

Inside the function:

```cpp
*num = 50;
```

the dereference operator (`*`) accesses the actual value stored at that address and modifies it.

### Understanding the Symbols

| Symbol | Purpose |
| --- | --- |
| & | Returns the memory address of a variable |
| * | Accesses the value stored at an address |

### Advantages

- No unnecessary copying.
- Allows modification of original data.
- Useful in dynamic memory management and low-level programming.

### Disadvantages

- Syntax is more complex.
- Higher risk of programming errors.
- Invalid pointers can cause runtime issues.

## Pass by Reference vs Pass by Pointer

Both methods allow modification of the original variable, but they differ in syntax and usability.

| Feature | Pass by Reference | Pass by Pointer |
| --- | --- | --- |
| Syntax | Simple | More Complex |
| Uses Addresses Explicitly | No | Yes |
| Requires Dereferencing | No | Yes |
| Can Be Null | No | Yes |
| Readability | High | Moderate |
| Preferred in Modern C++ | Yes | Only When Necessary |

Pass-by-reference is generally preferred because it offers the efficiency of pointers while keeping the code simpler and easier to read.

## When to Use Each Technique?

- Use **Pass by Value** when the function should not modify the original data.
- Use **Pass by Reference** when the function needs to modify the original variable or when large objects must be passed efficiently.
- Use **Pass by Pointer** when working with dynamic memory, arrays, or situations where null values need to be handled.

Choosing the right technique improves both performance and code clarity.

## Summary

Parameter passing defines how data is transferred from a calling function to a called function. C++ provides three parameter-passing techniques: pass by value, pass by reference, and pass by pointer.

In pass-by-value, a copy of the original variable is created, so modifications do not affect the caller. In pass-by-reference, the function receives an alias to the original variable, allowing direct modification without copying. In pass-by-pointer, the memory address of the variable is passed, enabling the function to access and modify the original data through dereferencing.

Understanding these techniques is essential for writing efficient, reusable, and maintainable C++ programs.




