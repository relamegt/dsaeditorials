# Inline Functions in C++

An inline function is a function whose code is expanded directly at the point where it is called, rather than performing a normal function call. The `inline` keyword is used to suggest to the compiler that the function should be expanded inline.

The primary purpose of inline functions is to reduce the overhead associated with function calls. For small and frequently used functions, replacing the function call with the actual function code can improve performance.

However, it is important to understand that the `inline` keyword is only a request to the compiler. The compiler may choose to ignore this request if it determines that inlining is not beneficial.

## Example Code

```cpp
#include <iostream>
using namespace std;

inline int getSum(int a, int b)
{
    return a + b;
}

int main()
{
    int Mohit = 5;
    int Akash = 10;

    int result = getSum(Mohit, Akash);

    cout << "Sum: " << result;

    return 0;
}
```

### Output
Sum: 15

### 

In this example, the compiler may replace:

```cpp
getSum(Mohit, Akash);
```

with:

```cpp
Mohit + Akash;
```

directly at the call location, eliminating the need for a normal function call.

## Why Do We Need Inline Functions?

Whenever a normal function is called, several operations take place:

1. Control is transferred to the function.
2. Function parameters are passed.
3. The return address is stored.
4. The function executes.
5. Control returns to the calling location.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/inline-functions-in-c/1781015953969-d81ec9fb-6951-4a40-acc9-36829e8c5df0.png)

These steps introduce a small amount of overhead.

For large functions, this overhead is negligible. However, for very small functions that are called thousands of times, the overhead may become significant.

Inline functions help eliminate this overhead by replacing the function call with the function body during compilation.

### Normal Function Call

```cpp
result = getSum(5, 10);
```

Internally:

```text
Call Function
Pass Arguments
Execute Function
Return Result
```

### Inline Function

```cpp
result = 5 + 10;
```

No separate function call is required.

This can improve execution speed for small functions.

## How Inline Functions Work

The compiler processes inline functions during compilation.

Consider the following code:

```cpp
inline int square(int n)
{
    return n * n;
}

int result = square(5);
```

The compiler may transform it into:

```cpp
int result = 5 * 5;
```

This process is called **function expansion** or **inline substitution**.

Because the function body is inserted directly into the code, the overhead of calling the function is removed.

## Another Example

```cpp
#include <iostream>
using namespace std;

inline void greet()
{
    cout << "Welcome Akash!" << endl;
}

int main()
{
    greet();
    greet();

    return 0;
}
```

### Output
Welcome Akash!
Welcome Akash!

# Time Complexity
O(1)

# Space Complexity
O(1)

### 

Since the function is very small, it is a good candidate for inlining.

## When Does the Compiler Ignore Inline?

Using the `inline` keyword does not guarantee that the function will actually be inlined.

Modern compilers may ignore inline requests for:

- Large functions.
- Recursive functions.
- Functions containing loops.
- Functions containing switch statements.
- Functions using static variables.
- Functions that are too complex.

### Example

```cpp
inline void displayNumbers()
{
    for(int i = 1; i <= 100; i++)
    {
        cout << i << " ";
    }
}
```

Although the function is marked as inline, the compiler may decide not to inline it because the function body is relatively large.

The program will still work correctly; only the optimization decision changes.

## Behavior of Inline Functions

Inline functions behave differently from normal functions in several ways:

- The compiler may replace the function call with the function body.
- Multiple identical inline function definitions across different files are allowed.
- Inline functions are commonly placed in header files.
- Templates and class member functions often use inline functions.

Unlike normal functions, inline functions do not usually create multiple-definition errors when included in multiple source files.

## Inline Functions and Header Files

Inline functions are frequently defined in header files.

Example:

```cpp
inline int multiply(int a, int b)
{
    return a * b;
}
```

Because the function is marked inline, it can safely appear in multiple files without violating the One Definition Rule (ODR).

This makes inline functions especially useful in library development.

## Virtual Functions and Inlining

Virtual functions are resolved at runtime through dynamic dispatch.

Inline functions are expanded during compile time.

Since the compiler cannot always determine which virtual function will be called during execution, virtual functions generally cannot be inlined.

### Example

```cpp
class Person
{
public:
    virtual void show()
    {
        cout << "Person";
    }
};
```

The actual function to execute is determined during runtime, making compile-time inlining difficult.

Therefore, virtual functions and inlining usually do not work together.

## Inline Functions vs Macros

Both inline functions and macros aim to reduce function-call overhead, but they differ significantly.

| Aspect | Inline Functions | Macros |
| --- | --- | --- |
| Definition | Defined using inline keyword | Defined using #define |
| Type Checking | Supported | Not Supported |
| Scope | Follows normal C++ scope rules | No scope |
| Argument Evaluation | Evaluated once | May be evaluated multiple times |
| Processing | Handled by compiler | Handled by preprocessor |
| Safety | Safer | Less safe |
| Debugging | Easier | More difficult |
| Recursion | Supported | Not supported |

### Macro Example

```cpp
#define SQUARE(x) x*x
```

Problem:

```cpp
SQUARE(2 + 3)
```

Expands to:

```cpp
2 + 3 * 2 + 3
```

which produces an incorrect result.

### Inline Function Example

```cpp
inline int square(int x)
{
    return x * x;
}
```

Calling:

```cpp
square(2 + 3);
```

correctly returns:

```text
25
```

This is one reason why inline functions are generally preferred over macros in modern C++.

## Advantages of Inline Functions

- Reduce function-call overhead.
- Improve execution speed for small functions.
- Provide type checking.
- Safer than macros.
- Allow compiler optimizations.
- Useful in header files and templates.
- Improve readability while maintaining performance.

## Disadvantages of Inline Functions

- Excessive inlining may increase executable size.
- Larger binaries may reduce cache efficiency.
- Complex functions are poor candidates for inlining.
- Recursive functions are usually not inlined.
- Changes require recompilation of dependent files.

## When Should Inline Functions Be Used?

Inline functions are most effective when:

- The function is small.
- The function is called frequently.
- The function contains only a few statements.
- Performance is more important than code size.

Examples include:

- Getter functions.
- Setter functions.
- Mathematical utility functions.
- Small helper functions.

## Summary

Inline functions allow the compiler to replace a function call with the actual function body during compilation. This reduces function-call overhead and can improve performance for small, frequently called functions. However, the compiler is not required to inline a function and may ignore the request for complex functions. Inline functions provide type safety, better debugging support, and improved maintainability compared to macros, making them a preferred optimization technique in modern C++.




