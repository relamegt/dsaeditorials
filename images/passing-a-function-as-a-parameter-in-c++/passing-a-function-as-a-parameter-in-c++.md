# Passing a Function as a Parameter in C++

Passing a function as a parameter allows one function to use another function to perform a specific task. This technique makes programs more flexible because behavior can be changed dynamically without modifying existing code.

A function that is passed to another function is commonly called a **callback function**.

## Why Pass Functions as Parameters?

Normally, a function performs a fixed task.

For example:

- A calculator function may always perform addition.
- A sorting function may always sort in ascending order.

By passing functions as parameters, we can change the behavior of a function at runtime.

### Benefits

- Improves code reusability.
- Reduces code duplication.
- Makes programs more flexible.
- Supports callback mechanisms.
- Widely used in event handling and STL algorithms.
- Allows dynamic behavior selection.

## Real-World Example

Consider **AlphaKnowledge**, an online learning platform.

Suppose there is a report generation system.

The same report can display:

- Total Students
- Total Courses
- Total Revenue

Instead of creating separate report functions, we can pass different calculation functions to a common report generator.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/passing-a-function-as-a-parameter-in-c/1782653718731-WhatsApp_Image_2026-06-28_at_7.05.02_PM.jpeg)

# Callback Function

A callback is a function passed as an argument to another function and executed inside it.

## Example

```cpp
#include <iostream>
using namespace std;

// Callback function
int square(int x)
{
    return x * x;
}

// Function accepting another function
void process(int value, int (*func)(int))
{
    cout << "Result: " << func(value);
}

int main()
{
    process(5, square);

    return 0;
}
```

### Output
Result: 25

### Explanation

- `square()` calculates the square of a number.
- `process()` receives a function as a parameter.
- `square` is passed to `process()`.
- `process()` calls `square(5)` and prints the result.

# Function Pointer

A function pointer stores the address of a function.

Just as normal pointers store memory addresses of variables, function pointers store addresses of functions.

## Syntax

```cpp
return_type (*pointer_name)(parameters);
```

### Example

```cpp
int (*operation)(int, int);
```

This pointer can store the address of any function that:

- Returns an integer.
- Accepts two integer parameters.

### Optional Note

A function pointer can only point to functions having the exact same return type and parameter list as specified in the pointer declaration.

For example, the pointer declaration:

```cpp
int (*operation)(int, int);
```

can only store addresses of functions that:

- Return `int`
- Accept two `int` parameters

# Passing Function Pointers

## Example

```cpp
#include <iostream>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

int multiply(int a, int b)
{
    return a * b;
}

int calculate(int a, int b,
              int (*operation)(int, int))
{
    return operation(a, b);
}

int main()
{
    cout << calculate(20, 10, add) << endl;
    cout << calculate(20, 10, multiply);

    return 0;
}
```

### Output
30
200

### Explanation

- `calculate()` accepts a function pointer.
- The function pointer can point to either `add()` or `multiply()`.
- The same function performs different operations based on the callback passed.

# Passing a Function Name vs Function Address

When passing a function as an argument, both the function name and its address can be used.

Key concepts:

- A function pointer stores the address of a function.
- The address of a function can be obtained using the address-of operator (`&`).
- In most situations, the function name automatically converts (decays) into a function pointer.
- Therefore, both approaches are equivalent.

## Example

```cpp
#include <iostream>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

int calculate(
    int a,
    int b,
    int (*operation)(int, int))
{
    return operation(a, b);
}

int main()
{
    cout << calculate(10, 20, add) << endl;

    cout << calculate(10, 20, &add);

    return 0;
}
```

### Output
30
30

### Explanation

Both calls work identically.

`add` automatically converts to `&add` when passed to a function expecting a function pointer.

Therefore, the following statements are equivalent:

```cpp
calculate(10, 20, add);
```

```cpp
calculate(10, 20, &add);
```

Most modern C++ code uses the function name directly because it is shorter and easier to read.

# Function Pointer Visualization

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/passing-a-function-as-a-parameter-in-c/1782653746126-WhatsApp_Image_2026-06-28_at_7.03.47_PM.jpeg)

# Using typedef with Function Pointers

Function pointer syntax can be difficult to read.

Using `typedef` makes code simpler.

## Example

```cpp
#include <iostream>
using namespace std;

typedef int (*Operation)(int, int);

int add(int a, int b)
{
    return a + b;
}

int calculate(int a, int b,
              Operation op)
{
    return op(a, b);
}

int main()
{
    cout << calculate(10, 20, add);

    return 0;
}
```

### Output
30

# std::function (Modern C++)

C++11 introduced `std::function`, a flexible wrapper capable of storing:

- Normal functions
- Function pointers
- Lambda expressions
- Functors
- Member functions

It is defined in the `<functional>` header.

## Syntax

```cpp
function<return_type(parameters)>
```

### Example

```cpp
#include <iostream>
#include <functional>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

int calculate(
    int a,
    int b,
    function<int(int, int)> op)
{
    return op(a, b);
}

int main()
{
    cout << calculate(10, 20, add);

    return 0;
}
```

### Output
30

### Explanation

`std::function` can store any callable object having the same signature.

# Why Use std::function?

### Advantages

- Easier syntax.
- Supports lambdas.
- Supports functors.
- Supports member functions.
- Type-safe.
- More flexible than function pointers.

# Lambda Expressions

A lambda is an anonymous function created directly where it is needed.

They are commonly used with `std::function`.

## Syntax

```cpp
[capture](parameters)
{
    // body
};
```

## Example

```cpp
#include <iostream>
#include <functional>
using namespace std;

int calculate(
    int a,
    int b,
    function<int(int, int)> operation)
{
    return operation(a, b);
}

int main()
{
    int result =
        calculate(
            10,
            20,
            [](int x, int y)
            {
                return x + y;
            });

    cout << result;

    return 0;
}
```

### Output
30

### Explanation

The lambda function performs addition and is passed directly to `calculate()` without creating a separate function.

# Real-World Example using Lambda

Suppose AlphaKnowledge wants to calculate student performance.

```cpp
#include <iostream>
#include <functional>
using namespace std;

void evaluate(
    int marks,
    function<void(int)> checker)
{
    checker(marks);
}

int main()
{
    evaluate(85,
             [](int marks)
             {
                 if(marks >= 50)
                     cout << "Pass";
                 else
                     cout << "Fail";
             });

    return 0;
}
```

### Output
Pass

# Functors (Function Objects)

A functor is a class object that behaves like a function.

This is achieved by overloading the `()` operator.

## Example

```cpp
#include <iostream>
using namespace std;

class Square
{
public:
    int operator()(int x)
    {
        return x * x;
    }
};

int main()
{
    Square sq;

    cout << sq(5);

    return 0;
}
```

### Output
25

### Explanation

The object `sq` behaves like a function.

# Passing Member Functions

Member functions belong to objects.

Therefore, they require an object before invocation.

## Example

```cpp
#include <iostream>
#include <functional>
using namespace std;

class Course
{
public:
    int calculateFee(int months,
                     int feePerMonth)
    {
        return months * feePerMonth;
    }
};

void display(
    function<int(int, int)> func)
{
    cout << func(6, 2000);
}

int main()
{
    Course c;

    auto feeCalculator =
        bind(
            &Course::calculateFee,
            &c,
            placeholders::_1,
            placeholders::_2);

    display(feeCalculator);

    return 0;
}
```

### Output
12000

### Explanation

- `calculateFee()` belongs to `Course`.
- `bind()` connects the function with the object.
- The bound function is passed like a normal callback.

# std::bind()

`std::bind()` converts member functions into callable objects.

## Syntax

```cpp
bind(
    &Class::Function,
    &object,
    placeholders::_1,
    placeholders::_2
);
```

### Uses

- Passing member functions.
- Reordering parameters.
- Creating partial functions.

# Passing Functions to STL Algorithms

Many STL algorithms accept functions as parameters.

## Example

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool ascending(int a, int b)
{
    return a < b;
}

int main()
{
    vector<int> marks =
    {70, 90, 50, 80};

    sort(
        marks.begin(),
        marks.end(),
        ascending);

    for(int x : marks)
        cout << x << " ";

    return 0;
}
```

### Output
50 70 80 90

### Explanation

The sorting behavior is determined by the callback function.

# Function Pointer vs Lambda vs std::function

| Feature | Function Pointer | Lambda | std::function |
| --- | --- | --- | --- |
| Supports Normal Functions | Yes | No | Yes |
| Supports Lambdas | No | Yes | Yes |
| Supports Functors | No | No | Yes |
| Supports Member Functions | No | No | Yes |
| Stores State | No | Yes | Yes |
| Easy Syntax | Moderate | Easy | Easy |
| Performance | Fastest | Fast | Slight Overhead |
| Flexibility | Low | Medium | High |

# Function Pointer vs std::function

| Feature | Function Pointer | std::function |
| --- | --- | --- |
| Type Safety | Limited | Strong |
| Flexibility | Low | High |
| Supports Lambdas | No | Yes |
| Supports Functors | No | Yes |
| Supports Member Functions | No | Yes |
| Memory Management | Manual | Automatic |
| Ease of Use | Moderate | Easy |

# When to Use Which?

| Situation | Recommended Choice |
| --- | --- |
| Simple callback | Function Pointer |
| High performance | Function Pointer |
| Anonymous function needed | Lambda |
| Flexible callback system | std::function |
| Event handling | std::function |
| GUI programming | std::function |
| Modern C++ development | std::function + Lambda |

# Advantages of Passing Functions as Parameters

- Makes functions reusable.
- Enables callback mechanisms.
- Reduces code duplication.
- Improves flexibility.
- Supports event-driven programming.
- Works well with STL algorithms.
- Encourages modular design.

# Common Applications

- Sorting algorithms.
- Searching algorithms.
- Event handling systems.
- GUI programming.
- Game engines.
- Task scheduling.
- Signal processing.
- Plugin architectures.

# Key Takeaways

- Functions can be passed as arguments to other functions.
- Callback functions allow dynamic behavior selection.
- Function pointers were the traditional method.
- `std::function` is the modern and preferred approach.
- Lambdas provide inline anonymous functions.
- `std::bind()` helps pass member functions.
- STL algorithms heavily rely on callbacks.
- Using functions as parameters improves flexibility, modularity, and code reuse.

# Summary

Passing a function as a parameter in C++ enables callback mechanisms where behavior is dynamically selected and executed at runtime, significantly enhancing code reusability and modularity. While traditional C++ relied on function pointers (which store function addresses and require strict signature matching) or typedefs for readability, modern C++ introduces `std::function` as a flexible, type-safe wrapper that supports normal functions, functors, member functions (using `std::bind()`), and inline anonymous lambda expressions. This callback technique is highly standard in modern development and is heavily utilized in event-driven systems, GUI architectures, and Standard Template Library (STL) algorithms like `std::sort` to customize behavior without altering core algorithm logic.




