# Recursion in C

## Introduction

Recursion is a programming technique in which a function calls itself to solve a problem. A function that calls itself is known as a **recursive function**. Recursive calls continue until a specific condition, called the **base case**, is reached.

Recursion is commonly used to solve problems that can be broken down into smaller subproblems, such as factorial calculation, tree traversal, searching, and divide-and-conquer algorithms.

### Key Features

- A recursive function calls itself.
- Every recursive function must contain a base case.
- Problems are solved by dividing them into smaller subproblems.
- Recursive calls are stored in the function call stack.
- Control returns back after reaching the base case.

## Basic Example

```c
#include <stdio.h>

void printNumbers(int n)
{
    if (n == 6)
        return;

    printf("Number %d\n", n);

    printNumbers(n + 1);
}

int main()
{
    printNumbers(1);

    return 0;
}
```

### Output
Number 1
Number 2
Number 3
Number 4
Number 5

### Explanation

The function prints the current number and calls itself with the next number. When `n` becomes 6, the base case is reached and recursion stops.

# How Recursion Works

Every recursive call creates a new stack frame in memory. These stack frames are stored in the function call stack. Once the base case is reached, the stack frames are removed one by one and control returns to previous calls.

## Example

```c
#include <stdio.h>

void display(int n)
{
    printf("Entering %d\n", n);

    if (n > 1)
    {
        display(n - 1);
    }

    printf("Leaving %d\n", n);
}

int main()
{
    display(3);

    return 0;
}
```

### Output
Entering 3
Entering 2
Entering 1
Leaving 1
Leaving 2
Leaving 3

### Explanation

Function calls go deeper until `n` becomes 1. After that, execution returns back in reverse order.

# Components of Recursion

## Base Case

The base case stops recursive calls and prevents infinite recursion.

```c
if (n == 0)
    return;
```

## Recursive Case

The recursive case contains the function call itself.

```c
factorial(n - 1);
```

# Example: Factorial Using Recursion

```c
#include <stdio.h>

int factorial(int n)
{
    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}

int main()
{
    int result = factorial(5);

    printf("Factorial = %d", result);

    return 0;
}
```

### Output
Factorial = 120

### Explanation

The recursive calls are:

```text
factorial(5)
5 × factorial(4)
5 × 4 × factorial(3)
5 × 4 × 3 × factorial(2)
5 × 4 × 3 × 2 × factorial(1)
5 × 4 × 3 × 2 × 1
= 120
```

# Memory Management in Recursion

Each recursive call creates a separate stack frame containing:

- Parameters
- Local variables
- Return address

When the function finishes execution, its stack frame is removed from memory.

## Example

```c
#include <stdio.h>

void demo(int n)
{
    if (n == 0)
        return;

    printf("%d\n", n);

    demo(n - 1);
}

int main()
{
    demo(3);

    return 0;
}
```

### Output
3
2
1

### Explanation

Three stack frames are created and removed one by one after reaching the base case.

# Stack Overflow

If recursion continues indefinitely or becomes too deep, the call stack becomes full. This condition is called **stack overflow**, causing abnormal program termination.

## Example

```c
#include <stdio.h>

void infinite()
{
    infinite();
}

int main()
{
    infinite();

    return 0;
}
```

### Output
Program terminated due to stack overflow

### Explanation

Since there is no base case, recursive calls continue forever and exhaust stack memory.

# Applications of Recursion

- Factorial and Fibonacci series
- Binary search
- Tower of Hanoi
- Tree traversals
- Graph algorithms
- Merge sort
- Quick sort
- Dynamic programming
- Divide and conquer algorithms

# Recursion vs Iteration

| Feature | Recursion | Iteration |
| --- | --- | --- |
| Uses | Function calls | Loops |
| Memory Usage | Higher | Lower |
| Speed | Slightly slower | Faster |
| Stack Usage | Yes | No |
| Suitable For | Trees and divide-and-conquer | Repetitive tasks |

# Advantages of Recursion

1. Makes code shorter and cleaner.
2. Simplifies complex problems.
3. Useful for trees and graphs.
4. Natural fit for divide-and-conquer algorithms.
5. Easier implementation of recursive data structures.

# Limitations

1. Function call overhead makes execution slower.
2. Uses additional stack memory.
3. Excessive recursion can cause stack overflow.
4. Sometimes iterative solutions are more efficient.
5. Recursive logic can be difficult to understand for beginners.

# Summary

Recursion is a technique in which a function calls itself repeatedly until a base condition is satisfied. Each recursive call creates a separate stack frame and execution returns in reverse order after reaching the base case. Recursion is widely used in mathematical problems, searching, sorting, trees, and divide-and-conquer algorithms. Although it provides elegant solutions, it consumes additional memory and may cause stack overflow if not implemented carefully.

