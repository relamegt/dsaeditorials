# Lambda Expressions in C++

Lambda expressions are anonymous functions introduced in C++11 that allow developers to write small pieces of functionality directly where they are needed. Unlike regular functions, lambda expressions do not require a separate function name, making code shorter and easier to read.

They are particularly useful when a function is needed only once or for a specific operation. Lambda expressions are commonly used with STL algorithms such as `sort()`, `for_each()`, `find_if()`, and many others.

Some common applications of lambda expressions include:

- Custom sorting logic in STL containers.
- Searching and filtering data.
- Event handling and callbacks.
- Asynchronous programming.
- Functional-style programming.

## Basic Lambda Expression

```cpp
#include <iostream>
using namespace std;

int main()
{
    auto doubleValue = [](int x)
    {
        return x + x;
    };

    cout << doubleValue(5);

    return 0;
}
```

### Output
10

### 

In this example, the lambda expression takes an integer parameter and returns its double. The lambda is stored in the variable `doubleValue` using the `auto` keyword.

## Syntax of Lambda Expressions

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/lambda-expressions-in-c/1781016380228-ChatGPT_Image_Jun_9%2C_2026%2C_08_16_13_PM.png)

The general syntax of a lambda expression is:

```cpp
[capture_clause](parameters) -> return_type
{
    // Function body
};
```

Example:

```cpp
[](int x)
{
    return x * x;
};
```

A lambda expression consists of four parts:

### Capture Clause

The capture clause specifies which variables from the surrounding scope can be accessed inside the lambda.

```cpp
[]
```

### Parameters

Parameters work exactly like function parameters.

```cpp
[](int x, int y)
```

### Return Type

Usually, the compiler automatically determines the return type.

```cpp
[](int x, int y) -> int
{
    return x + y;
}
```

### Function Body

Contains the statements executed when the lambda is called.

```cpp
{
    return x + y;
}
```

## Capture Clause

One of the most powerful features of lambda expressions is the ability to access variables from the surrounding scope.

Normal functions cannot directly access local variables from another function, but lambda expressions can do this through the capture clause.

### Capture by Value `[=]`

All external variables are copied into the lambda.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int Mohit = 10;

    auto show = [=]()
    {
        cout << Mohit;
    };

    show();

    return 0;
}
```

### Output
10

### 

The variable `Mohit` is copied into the lambda. Any changes made inside the lambda will not affect the original variable.

### Capture by Reference `[&]`

All external variables are captured by reference.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a = 10;

    auto increase = [&]()
    {
        Mohit++;
    };

    increase();

    cout << a;

    return 0;
}
```

### Output
11

### 

Since the variable is captured by reference, modifications inside the lambda affect the original variable.

### Mixed Capture

Specific variables can be captured differently.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int Mohit = 10;
    int Akash = 20;

    auto display = [Mohit, &Akash]()
    {
        cout << Mohit << " " << Akash;
    };

    display();

    return 0;
}
```

### Output
10 20

### 

Here:

- `Mohit` is captured by value.
- `Akash` is captured by reference.

## Empty Capture Clause

A lambda with an empty capture clause cannot access local variables from the surrounding scope.

```cpp
#include <iostream>
using namespace std;

int main()
{
    auto greet = []()
    {
        cout << "Hello Mohit";
    };

    greet();

    return 0;
}
```

### Output
Hello Mohit

### 

Only parameters, global variables, and static variables can be accessed.

## Mutable Lambda

When variables are captured by value, they become read-only inside the lambda.

The `mutable` keyword allows modification of copied values.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x = 10;

    auto modify = [x]() mutable
    {
        x += 5;
        cout << x;
    };

    modify();

    return 0;
}
```

### Output
15

### 

The original variable remains unchanged because only the copy is modified.

## Lambda with STL Algorithms

Lambda expressions are heavily used with STL algorithms because they allow custom logic to be written directly at the point of use.

### Example 1: Sorting in Descending Order

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> marks = {75, 90, 60, 85, 95};

    sort(marks.begin(), marks.end(),
         [](int a, int b)
         {
             return a > b;
         });

    for (int mark : marks)
    {
        cout << mark << " ";
    }

    return 0;
}
```

### Output
95 90 85 75 60

# Time Complexity
O(n log n)

# Space Complexity
O(1)

### 

The lambda acts as a custom comparison function and instructs `sort()` to arrange elements in descending order.

## Example 2: Find First Even Number

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> numbers = {7, 11, 15, 18, 25};

    auto it = find_if(numbers.begin(),
                      numbers.end(),
                      [](int x)
                      {
                          return x % 2 == 0;
                      });

    if (it != numbers.end())
    {
        cout << *it;
    }

    return 0;
}
```

### Output
18

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

The lambda checks whether a number is even. `find_if()` stops as soon as the first matching element is found.

## Example 3: Using Lambda with for_each()

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<string> students =
    {
        "Mohit",
        "Akash",
        "Hemesh",
        "Abhiram"
    };

    for_each(students.begin(),
             students.end(),
             [](string name)
             {
                 cout << name << endl;
             });

    return 0;
}
```

### Output
Mohit
Akash
Hemesh
Abhiram

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

The lambda is executed for each element in the vector.

## Advantages of Lambda Expressions

- Reduce the need for separate helper functions.
- Improve code readability.
- Keep logic close to where it is used.
- Work seamlessly with STL algorithms.
- Support capturing local variables.
- Useful for callbacks and event handling.
- Encourage concise and expressive code.

## Limitations of Lambda Expressions

- Complex lambdas can reduce readability.
- Excessive nesting can make code difficult to maintain.
- Capturing large objects by value may increase memory usage.
- Debugging can sometimes be harder than debugging named functions.

## Lambda Expressions vs Regular Functions

| Feature | Lambda Expression | Regular Function |
| --- | --- | --- |
| Requires Name | No | Yes |
| Can Capture Local Variables | Yes | No |
| Suitable for Small Tasks | Yes | Less Suitable |
| Reusability | Limited | High |
| Readability for Small Logic | Better | More Verbose |
| STL Integration | Excellent | Good |

## Summary

Lambda expressions are anonymous functions that allow developers to write small pieces of logic directly where they are needed. They improve readability, reduce boilerplate code, and integrate naturally with STL algorithms. Their ability to capture local variables makes them more flexible than regular functions, making them one of the most useful features introduced in modern C++.




