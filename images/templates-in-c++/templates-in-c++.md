# Templates in C++

Templates are one of the most powerful features of C++. They allow programmers to write generic and reusable code that works with different data types without rewriting the same logic multiple times.

Normally, if a function or class needs to work with multiple data types such as `int`, `float`, `double`, or `string`, separate versions must be created for each type. Templates eliminate this duplication by allowing a single implementation to work with multiple data types.

Templates are heavily used throughout the C++ Standard Template Library (STL), including containers such as `vector`, `list`, `map`, `set`, and algorithms such as `sort()`, `find()`, and `max()`.

Templates improve:

- Code Reusability
- Maintainability
- Flexibility
- Type Safety
- Performance

They allow developers to write generic programs while still maintaining compile-time type checking.

# Why Do We Need Templates?

Consider a situation where we need a function to find the larger of two values.

Without templates, we might write:

```cpp
int maximum(int a, int b);

double maximum(double a, double b);

char maximum(char a, char b);
```

Although the logic is identical, we are forced to repeat the code for every data type.

As programs become larger, this leads to:

- Code duplication
- Increased maintenance effort
- Higher chance of errors
- Reduced readability

Templates solve this problem by allowing us to write the logic once and use it with multiple data types.

# What is Generic Programming?

Templates are the foundation of Generic Programming in C++.

Generic Programming refers to writing algorithms and data structures in a way that they work independently of any specific data type.

Instead of writing:

```text
Integer Stack
Double Stack
String Stack
```

We can simply write:

```text
Stack<T>
```

and use it with any type.

This approach makes programs more flexible and reusable.

# Features of Templates

Templates provide several important features.

## Code Reusability

A single template can work with multiple data types.

## Type Safety

Templates are checked by the compiler, reducing runtime errors.

## Better Maintainability

Changes need to be made in only one place.

## Compile-Time Efficiency

Templates are expanded during compilation, resulting in highly optimized code.

## Foundation of STL

Almost every major STL container and algorithm is implemented using templates.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/templates-in-c/1781095490777-c1a7dee6-3099-4fe2-83c1-8981222351dc.png)

# Syntax of Templates

Templates are declared using the `template` keyword.

## General Syntax

```cpp
template <typename T>
```

or

```cpp
template <class T>
```

Both `typename` and `class` are equivalent in template declarations.

### Explanation

- `template` tells the compiler that a template is being defined.
- `T` is called a template parameter.
- `T` acts as a placeholder for a data type.

The compiler replaces `T` with the actual type during compilation.

# Function Templates

Function templates allow functions to work with different data types.

Instead of writing separate functions for integers, floating-point values, and characters, a single generic function can handle all of them.

## Example: Finding Maximum of Two Values

### Example Code

```cpp
#include <iostream>
using namespace std;

template <typename T>
T findMaximum(T a, T b)
{
    return (a > b) ? a : b;
}

int main()
{
    cout << findMaximum(15, 25) << endl;

    cout << findMaximum(7.5, 9.8) << endl;

    cout << findMaximum('A', 'Z') << endl;

    return 0;
}
```

### Output
25
9.8
Z

### 

### Explanation

The function `findMaximum()` is written only once.

When the compiler encounters:

```cpp
findMaximum(15, 25);
```

it generates:

```cpp
int findMaximum(int, int);
```

Similarly:

```cpp
findMaximum(7.5, 9.8);
```

generates:

```cpp
double findMaximum(double, double);
```

This process is known as **Template Instantiation**.

# Template Instantiation

Template Instantiation is the process by which the compiler generates actual functions or classes from a template.

For example:

```cpp
findMaximum<int>(10, 20);
```

creates:

```cpp
int findMaximum(int, int);
```

while:

```cpp
findMaximum<double>(5.5, 7.7);
```

creates:

```cpp
double findMaximum(double, double);
```

The compiler automatically generates these versions when needed.

# Class Templates

Just as functions can be made generic, classes can also be made generic.

Class templates allow the creation of reusable data structures and classes that work with different data types.

Examples include:

- Stack
- Queue
- Linked List
- Binary Tree
- Vector

## Example: Generic Student Data Container

### Example Code

```cpp
#include <iostream>
using namespace std;

template <typename T>
class DataHolder
{
private:

    T data;

public:

    DataHolder(T value)
    {
        data = value;
    }

    void display()
    {
        cout << data << endl;
    }
};

int main()
{
    DataHolder<int> marks(95);

    DataHolder<string> name("Mohit");

    marks.display();

    name.display();

    return 0;
}
```

### Output
95
Mohit

### 

### Explanation

The class `DataHolder` is written once.

Different objects can be created using different data types.

```cpp
DataHolder<int>
```

stores integers.

```cpp
DataHolder<string>
```

stores strings.

The compiler generates separate versions internally.

# Multiple Template Parameters

Templates can accept more than one type parameter.

## Syntax

```cpp
template <typename T1, typename T2>
```

---

## Example Code

```cpp
#include <iostream>
using namespace std;

template <typename T1,
          typename T2>

class Student
{
public:

    T1 rollNumber;

    T2 cgpa;

    Student(T1 r, T2 c)
    {
        rollNumber = r;
        cgpa = c;
    }

    void display()
    {
        cout << rollNumber
             << " "
             << cgpa;
    }
};

int main()
{
    Student<int, double>
    s1(101, 9.25);

    s1.display();

    return 0;
}
```

### Output
101 9.25

### 

# Default Template Arguments

Templates can provide default types similar to default function parameters.

## Example

```cpp
template <typename T = int>
class Example
{
};
```

If no type is specified, `int` will be used automatically.

# Non-Type Template Parameters

Templates can also accept constant values instead of data types.

These are called Non-Type Template Parameters.

## Example Code

```cpp
#include <iostream>
using namespace std;

template <int size>
class Marks
{
public:

    int arr[size];
};

int main()
{
    Marks<5> studentMarks;

    cout << sizeof(studentMarks.arr)
         / sizeof(int);

    return 0;
}
```

### Output
5

### 

### Explanation

The value `5` becomes part of the template definition.

The compiler creates a version specifically for size 5.

# Template Argument Deduction

Template Argument Deduction allows the compiler to determine the template type automatically.

Instead of:

```cpp
findMaximum<int>(10, 20);
```

we can simply write:

```cpp
findMaximum(10, 20);
```

The compiler automatically deduces that `T` is `int`.

This feature makes templates easier to use.

# Class Template Argument Deduction (CTAD)

Introduced in C++17.

Allows creation of class template objects without explicitly specifying template types.

## Example

```cpp
Pair p(10, 20);
```

instead of:

```cpp
Pair<int> p(10, 20);
```

The compiler automatically determines the type.

# Template Specialization

Sometimes a generic template implementation is not suitable for every data type.

Template Specialization allows custom behavior for specific types.

## Example Code

```cpp
#include <iostream>
using namespace std;

template <typename T>
class Printer
{
public:

    void print()
    {
        cout << "Generic Type";
    }
};

template <>
class Printer<string>
{
public:

    void print()
    {
        cout << "String Type";
    }
};

int main()
{
    Printer<int> p1;

    Printer<string> p2;

    p1.print();

    cout << endl;

    p2.print();

    return 0;
}
```

### Output
Generic Type
String Type

### 

# Template Metaprogramming

Template Metaprogramming is an advanced technique where computations are performed during compilation rather than runtime.

Benefits:

- Faster execution
- Better optimization
- Reduced runtime calculations

The compiler performs calculations before the program runs.

## Example: Compile-Time Factorial

### Example Code

```cpp
#include <iostream>
using namespace std;

template <int N>
struct Factorial
{
    static const int value =
        N * Factorial<N - 1>::value;
};

template <>
struct Factorial<0>
{
    static const int value = 1;
};

int main()
{
    cout << Factorial<5>::value;

    return 0;
}
```

### Output
120

### 

### Explanation

The factorial is calculated during compilation.

No factorial calculation occurs during runtime.

This demonstrates the power of template metaprogramming.

# Real-World Applications of Templates

Templates are widely used in modern software development.

Examples include:

- Standard Template Library (STL)
- Generic Data Structures
- Database Libraries
- Game Engines
- Scientific Computing
- Machine Learning Frameworks
- Operating Systems
- Network Programming
- Financial Applications

Templates make software more flexible and reusable.

# Advantages of Templates

| Advantage | Explanation |
| --- | --- |
| **Code Reusability** | Write once and use with multiple data types. |
| **Type Safety** | Errors are detected during compilation. |
| **Better Maintainability** | Changes are made in one place only. |
| **Improved Performance** | No runtime overhead because templates are expanded at compile time. |
| **Supports Generic Programming** | Enables reusable algorithms and data structures. |
| **Foundation of STL** | Used extensively throughout the Standard Template Library. |

# Limitations of Templates

| Limitation | Explanation |
| --- | --- |
| **Complex Error Messages** | Compiler errors involving templates can be difficult to understand. |
| **Longer Compilation Time** | The compiler must generate multiple versions of templates. |
| **Code Bloat** | Many template instantiations can increase executable size. |
| **Difficult for Beginners** | Advanced template syntax can be challenging to learn. |
| **Debugging Complexity** | Template-generated code can be harder to debug. |

# Summary

Templates are a powerful feature of C++ that enable generic programming by allowing functions and classes to work with multiple data types. They reduce code duplication, improve maintainability, and provide compile-time type safety. Templates form the backbone of the Standard Template Library and are widely used in modern software development.

By using templates, programmers can write flexible, reusable, and efficient code while maintaining strong type checking and high performance. Understanding templates is essential for mastering advanced C++ programming and effectively utilizing STL containers and algorithms.




