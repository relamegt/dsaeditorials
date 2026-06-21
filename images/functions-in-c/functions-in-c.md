# Functions in C

## Introduction

A function is a named block of code that performs a specific task. Functions help divide large programs into smaller, manageable modules, making programs easier to understand, maintain, and reuse.

A function may accept input values called parameters, execute a set of statements, and optionally return a value to the calling function. By using functions, programmers can avoid writing the same code repeatedly.

### Key Features

- Promote code reusability.
- Improve readability and maintainability.
- Reduce code duplication.
- Support modular programming.
- Can accept parameters and return values.
- Help organize programs into logical units.

# Why Use Functions?

Suppose we need to calculate the square of several numbers. Without functions, the same logic would need to be written multiple times.

## Example

```c
#include <stdio.h>

int square(int number)
{
    return number * number;
}

int main()
{
    int result = square(5);

    printf("Square of 5 = %d", result);

    return 0;
}
```

### Output
Square of 5 = 25

### Explanation

The `square()` function calculates the square of a number and returns the result to the `main()` function.

# How Functions Work in C

When a function is called:

1. Control transfers to the called function.
2. Input values are passed through parameters.
3. The statements inside the function are executed.
4. A value may be returned to the calling function.
5. Control returns to the point where the function was called.

# Function Syntax

```c
return_type function_name(parameter_list)
{
    // statements

    return value;
}
```

### Components of a Function

- **Return Type**: Specifies the type of value returned by the function. If no value is returned, `void` is used.
- **Function Name**: A unique identifier for the function.
- **Parameters**: Inputs supplied to the function.
- **Function Body**: Statements enclosed inside braces.
- **Return Statement**: Sends a value back to the calling function.

# Function Declaration

A function declaration informs the compiler about the function's name, return type, and parameters before it is used.

## Syntax

```c
return_type function_name(parameter_list);
```

## Example

```c
int add(int num1, int num2);
```

### Explanation

This declaration tells the compiler that a function named `add()` exists and accepts two integer arguments.

# Function Definition

The function definition contains the actual implementation.

## Example

```c
int add(int num1, int num2)
{
    return num1 + num2;
}
```

### Explanation

The function adds two numbers and returns the result.

# Function Declaration vs Definition

| Feature | Declaration | Definition |
| --- | --- | --- |
| Purpose | Introduces the function | Implements the function |
| Contains Body | No | Yes |
| Ends With | Semicolon | Curly braces |
| Memory Allocation | No | Yes |
| Number of Times | Multiple declarations allowed | Only one definition allowed |

# Calling a Function

A function is executed by calling its name followed by parentheses.

## Example

```c
#include <stdio.h>

int add(int a, int b)
{
    return a + b;
}

int main()
{
    int sum = add(10, 20);

    printf("Sum = %d", sum);

    return 0;
}
```

### Output
Sum = 30

### Explanation

The values 10 and 20 are passed to the `add()` function, which returns their sum.

# Library Functions

Library functions are predefined functions provided by C.

Some commonly used library functions are:

| Function | Header File | Purpose |
| --- | --- | --- |
| printf() | stdio.h | Displays output |
| scanf() | stdio.h | Reads input |
| strlen() | string.h | Finds string length |
| sqrt() | math.h | Calculates square root |
| pow() | math.h | Calculates powers |

## Example

```c
#include <stdio.h>
#include <math.h>

int main()
{
    printf("%.2f", sqrt(64));

    return 0;
}
```

### Output
8.00

# User-Defined Functions

User-defined functions are created by programmers to perform specific tasks.

## Example

```c
#include <stdio.h>

void greet()
{
    printf("Welcome to AlphaKnowledge");
}

int main()
{
    greet();

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The user-defined function `greet()` prints a welcome message.

# Types of User-Defined Functions

User-defined functions can be classified into four types depending on whether they accept arguments and return values.

1. No Arguments and No Return Value
2. Arguments and No Return Value
3. No Arguments and Return Value
4. Arguments and Return Value

# 1. No Arguments and No Return Value

These functions neither accept input values nor return a value. They perform a specific task internally.

## Example

```c
#include <stdio.h>

void displayMessage()
{
    printf("Welcome to AlphaKnowledge");
}

int main()
{
    displayMessage();

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The function `displayMessage()` does not take any parameters and does not return a value.

# 2. Arguments and No Return Value

These functions accept values from the calling function but do not return any value.

## Example

```c
#include <stdio.h>

void printSum(int num1, int num2)
{
    printf("Sum = %d", num1 + num2);
}

int main()
{
    printSum(10, 20);

    return 0;
}
```

### Output
Sum = 30

### Explanation

The function receives two numbers and prints their sum directly.

# 3. No Arguments and Return Value

These functions do not take input values but return a value to the calling function.

## Example

```c
#include <stdio.h>

int getNumber()
{
    return 100;
}

int main()
{
    int value = getNumber();

    printf("%d", value);

    return 0;
}
```

### Output
100

### Explanation

The function returns a value which is stored in the variable `value`.

# 4. Arguments and Return Value

These functions accept input values and return a result.

## Example

```c
#include <stdio.h>

int multiply(int a, int b)
{
    return a * b;
}

int main()
{
    int result = multiply(5, 4);

    printf("Result = %d", result);

    return 0;
}
```

### Output
Result = 20

### Explanation

The values 5 and 4 are passed to the function, and their product is returned.

# Parameter Passing

Arguments passed to functions are called parameters.

## Actual Parameters

These are values supplied during the function call.

```c
add(10, 20);
```

Here, `10` and `20` are actual parameters.

## Formal Parameters

These are variables declared inside the function definition.

```c
int add(int a, int b)
{
    return a + b;
}
```

Here, `a` and `b` are formal parameters.

# Call by Value

By default, C uses call by value. A copy of the actual argument is passed to the function.

## Example

```c
#include <stdio.h>

void modify(int num)
{
    num = 50;
}

int main()
{
    int value = 10;

    modify(value);

    printf("%d", value);

    return 0;
}
```

### Output
10

### Explanation

Only a copy of `value` is modified. The original variable remains unchanged.

# Memory Management of Functions

Whenever a function is called, memory is allocated in the function call stack.

The stack frame stores:

- Parameters
- Local variables
- Return address
- Temporary data

When the function finishes execution, its stack frame is automatically removed and memory is released.

# Recursion

A function calling itself is known as recursion.

## Example

```c
#include <stdio.h>

void countdown(int num)
{
    if (num == 0)
        return;

    printf("%d\n", num);

    countdown(num - 1);
}

int main()
{
    countdown(5);

    return 0;
}
```

### Output
5
4
3
2
1

### Explanation

The function repeatedly calls itself until the value becomes 0.

# Advantages of Functions

1. Promote code reusability.
2. Improve program readability.
3. Simplify debugging and maintenance.
4. Support modular programming.
5. Reduce code duplication.
6. Enable teamwork by dividing tasks into modules.
7. Make large programs easier to manage.

# Limitations of Functions

1. Function calls introduce a small execution overhead.
2. Excessive use of tiny functions can reduce readability.
3. Tracking program flow across many functions can become difficult.
4. Local variables cannot be accessed outside their function.
5. Recursive functions consume additional stack memory.

# Summary

Functions are reusable blocks of code that perform specific tasks in a program. They improve readability, modularity, and maintainability by dividing large programs into smaller units. Functions can be predefined library functions or programmer-defined functions and may or may not accept arguments and return values. C uses call by value for parameter passing, and memory for functions is managed using the function call stack. Proper use of functions helps build efficient, organized, and scalable programs.

