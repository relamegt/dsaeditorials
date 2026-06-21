# Inline Function in C

## Introduction

An inline function is a function whose code may be substituted directly at the point where the function is called. Instead of performing a normal function call, the compiler may replace the call with the actual body of the function, thereby reducing function call overhead.

Inline functions are declared using the `inline` keyword and are generally used for small and frequently used functions. However, the compiler ultimately decides whether the function should actually be inlined.

### Key Features

- Declared using the `inline` keyword.
- Reduces function call overhead.
- Suitable for small and frequently called functions.
- Improves performance in time-critical applications.
- Compiler may ignore the inline request if the function is complex.

# Basic Example

```c
#include <stdio.h>

inline int add(int a, int b)
{
    return a + b;
}

int main()
{
    int result = add(5, 3);

    printf("Sum = %d", result);

    return 0;
}
```

### Output
Sum = 8

### Explanation

The compiler may replace the function call `add(5, 3)` with:

```c
int result = 5 + 3;
```

thus eliminating the overhead of a normal function call.

# Why Use Inline Functions?

Normal function calls involve:

- Passing arguments.
- Saving the return address.
- Creating stack frames.
- Returning control to the caller.

Inline functions eliminate most of this overhead, making execution faster.

# Syntax of Inline Function

```c
inline return_type function_name(parameters)
{
    // function body
}
```

## Example

```c
inline int square(int num)
{
    return num * num;
}
```

# Behavior of Inline Functions

The `inline` keyword is only a request to the compiler. The compiler may or may not inline the function depending on optimization settings.

## Example

```c
#include <stdio.h>

inline int multiply(int a, int b)
{
    return a * b;
}

int main()
{
    printf("%d", multiply(4, 5));

    return 0;
}
```

### Output
20

### Explanation

If optimization is enabled, the compiler may substitute the function body directly into the calling code.

# Static Inline Function

Using `static inline` gives the function internal linkage and prevents linker errors.

## Example

```c
#include <stdio.h>

static inline int cube(int x)
{
    return x * x * x;
}

int main()
{
    printf("%d", cube(3));

    return 0;
}
```

### Output
27

### Explanation

The compiler treats the function as local to the source file and may inline it during compilation.

# Inline Function with Forward Declaration

A function can first be declared and then defined as inline.

## Example

```c
#include <stdio.h>

int square(int);

inline int square(int n)
{
    return n * n;
}

int main()
{
    printf("%d", square(6));

    return 0;
}
```

### Output
36

### Explanation

The declaration allows the linker to recognize the function even if inlining does not occur.

# Inline Function vs Normal Function

| Feature | Inline Function | Normal Function |
| --- | --- | --- |
| Keyword Required | Yes | No |
| Function Call Overhead | Very Low | Present |
| Execution Speed | Faster | Slightly Slower |
| Stack Frame Creation | Usually Avoided | Required |
| Code Size | May Increase | Smaller |
| Suitable For | Small Functions | Large Functions |

# Inline Function vs Macro

| Feature | Inline Function | Macro |
| --- | --- | --- |
| Type Checking | Yes | No |
| Debugging | Easy | Difficult |
| Parameter Evaluation | Once | Multiple Times |
| Scope Rules | Followed | Not Followed |
| Recursive Calls | Allowed | Not Allowed |
| Safety | High | Lower |

## Example of Macro

```c
#define SQUARE(x) x*x
```

Calling:

```c
SQUARE(2 + 3)
```

Expands to:

```c
2 + 3 * 2 + 3
```

which produces an incorrect result.

### Inline Function Alternative

```c
inline int square(int x)
{
    return x * x;
}
```

Calling:

```c
square(2 + 3)
```

correctly returns 25.

# Inline Function with GCC Optimization

Inlining usually occurs when optimization flags are enabled.

```text
gcc program.c -O1
gcc program.c -O2
gcc program.c -O3
```

Optimization levels greater than `O0` enable inline optimization.

# Inline Function with extern

```c
extern inline int add(int a, int b)
{
    return a + b;
}
```

This allows the definition to be available across translation units while still permitting inlining.

# When to Use Inline Functions?

Inline functions are recommended when:

- Functions are very small.
- Functions are called frequently.
- Execution speed is important.
- Type safety is required.
- Replacing macros with safer alternatives.

## Example

```c
inline int max(int a, int b)
{
    return (a > b) ? a : b;
}
```

# When Not to Use Inline Functions?

Inline functions should be avoided when:

- The function is very large.
- The function contains loops or recursion.
- Excessive inlining may increase executable size.
- Performance gain is insignificant.

# Advantages of Inline Functions

1. Reduces function call overhead.
2. Improves execution speed.
3. Provides type checking.
4. Easier to debug than macros.
5. Parameters are evaluated only once.
6. Suitable for embedded systems and performance-critical programs.

# Limitations

1. Compiler may ignore the inline request.
2. Excessive use increases binary size.
3. Large functions are not suitable for inlining.
4. Optimization settings affect inlining behavior.
5. Recursive functions are rarely inlined.

# Summary

An inline function is a small function declared using the `inline` keyword. The compiler may replace the function call with the actual function body, thereby eliminating function call overhead and improving performance. Inline functions are safer and easier to debug than macros because they support type checking and evaluate arguments only once. They are best suited for small, frequently used functions, while large and complex functions are generally better implemented as normal functions.

