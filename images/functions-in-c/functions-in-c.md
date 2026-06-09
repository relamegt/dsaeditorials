# Functions in C++

A function is a named block of code that performs a specific task. Functions help divide a program into smaller and manageable parts, making the code easier to understand, maintain, and reuse. Instead of writing the same logic multiple times, a function allows us to write it once and call it whenever needed.

Consider a program that needs to calculate the square of several numbers. Writing the same calculation repeatedly would increase code duplication. By creating a function, the logic can be reused throughout the program with different inputs.

Functions are one of the fundamental concepts in C++ because they support modular programming, where a large problem is divided into smaller tasks. This makes programs more organized and easier to debug.

### Example Code

```cpp
#include <iostream>
using namespace std;

// Function definition
int square(int x)
{
    return x * x;
}

int main()
{
    int result = square(5);

    cout << "Square of 5 is: " << result;

    return 0;
}
```

### Output
Square of 5 is: 25

In the above program, the function `square()` receives a number, calculates its square, and returns the result. When `square(5)` is called, the value `5` is passed to the function, which computes `5 × 5` and returns `25`.

![Function Usage](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/functions-in-c/1781013968973-15.png)

## Why Use Functions?

Functions provide several advantages in programming:

- Reduce repetition of code.
- Improve readability.
- Simplify debugging and testing.
- Make programs easier to maintain.
- Promote code reusability.
- Divide large programs into smaller logical units.

Without functions, large programs can become difficult to understand because all code would exist inside a single block.

---

## Function Syntax

Every function in C++ follows a general structure:

```cpp
return_type function_name(parameter_list)
{
    // statements
    return value;
}
```

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/functions-in-c/1781014024736-16.png)

The different parts of a function are:

- **Return Type:** Specifies the type of value returned by the function.
- **Function Name:** The identifier used to call the function.
- **Parameters:** Input values accepted by the function.
- **Function Body:** Contains the statements executed when the function is called.

For example:

```cpp
int add(int a, int b)
{
    return a + b;
}
```

Here:

- `int` is the return type.
- `add` is the function name.
- `a` and `b` are parameters.
- `return a + b;` sends the result back to the caller.

## Function Declaration and Definition

Before a function can be used, the compiler must know about it. This can be achieved through a function declaration.

A function declaration tells the compiler the function's name, return type, and parameters.

```cpp
int add(int, int);
```

The actual implementation of the function is called the function definition.

```cpp
int add(int a, int b)
{
    return a + b;
}
```

The declaration acts like a promise that the function exists somewhere in the program. This is especially useful when the function definition appears after the `main()` function or is located in another file.

## Calling a Function

A function executes only when it is called. Calling a function means transferring control from the current part of the program to the function.

### Example Code

```cpp
#include <iostream>
using namespace std;

void greet()
{
    cout << "Welcome to C++ Programming!" << endl;
}

int multiply(int a, int b)
{
    return a * b;
}

int main()
{
    greet();

    int result = multiply(4, 5);

    cout << "Multiplication Result: " << result;

    return 0;
}
```

### Output
Welcome to C++ Programming!
Multiplication Result: 20

### 

The function `greet()` simply displays a message and does not return any value. The function `multiply()` accepts two integers and returns their product. Functions can be called multiple times whenever their functionality is needed.

## Parameters and Arguments

Functions often require input values to perform their tasks. These inputs are handled through parameters and arguments.

A **parameter** is a variable defined in the function header.

```cpp
void printNumber(int n)
```

Here, `n` is a parameter.

An **argument** is the actual value supplied during the function call.

```cpp
printNumber(10);
```

Here, `10` is an argument.

### Example Code

```cpp
#include <iostream>
using namespace std;

void printNumber(int n)
{
    cout << n << endl;
}

int main()
{
    int num1 = 10;
    int num2 = 99;

    printNumber(num1);
    printNumber(num2);

    return 0;
}
```

### Output
10
99

### 

The same function is called twice with different arguments. Inside the function, the parameter `n` receives the passed value and is used for processing. This demonstrates how functions can perform the same task with different inputs.

## Types of Functions

Functions can be classified based on their origin and behavior.

### Based on Origin

| Type | Description |
| --- | --- |
| Library Functions | Predefined functions provided by C++ libraries |
| User-Defined Functions | Functions created by the programmer |

Examples of library functions include:

```cpp
sqrt()
abs()
pow()
getline()
```

These functions are already implemented in standard libraries and can be used by including the appropriate header files.

User-defined functions are created to solve specific problems.

### Based on Parameters and Return Values

#### 1. No Parameters, No Return Value

Such functions neither accept input nor return output.

```cpp
#include <iostream>
using namespace std;

void welcome()
{
    cout << "Welcome!";
}

int main()
{
    welcome();
    return 0;
}
```

### Output
Welcome!

### 

The function performs a task but does not interact with external data.

#### 2. Parameters, No Return Value

These functions accept input but do not return anything.

```cpp
#include <iostream>
using namespace std;

void displaySquare(int num)
{
    cout << num * num;
}

int main()
{
    displaySquare(6);

    return 0;
}
```

### Output
36

### 

The function receives data through parameters and directly displays the result.

#### 3. No Parameters, Return Value

These functions do not require input but return a result.

```cpp
#include <iostream>
using namespace std;

int getValue()
{
    return 50;
}

int main()
{
    cout << getValue();

    return 0;
}
```

### Output
50

### 

The function independently generates a value and sends it back to the caller.

#### 4. Parameters and Return Value

These are the most commonly used functions in programming.

```cpp
#include <iostream>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

int main()
{
    cout << add(10, 20);

    return 0;
}
```

### Output
30

### 

The function accepts input, processes it, and returns a result. This design makes functions flexible and reusable.

## Important Notes About Functions

- A function can be called multiple times.
- Function names should be meaningful and descriptive.
- The number and type of arguments should match the parameters.
- Functions can return only one value directly using the `return` statement.
- A function declared with `void` cannot return a value.
- Every C++ program starts execution from the `main()` function.

## Summary

Functions are reusable blocks of code that perform specific tasks. They help reduce redundancy, improve readability, and make programs modular. A function may accept inputs through parameters, process the data, and optionally return a value. Understanding function declaration, definition, function calls, parameters, arguments, and the different types of functions is essential for writing efficient and maintainable C++ programs.




