# Recursion in C++

Recursion is a programming technique in which a function calls itself to solve a problem. Instead of solving a large problem directly, recursion breaks it into smaller versions of the same problem and continues solving them until a stopping condition is reached.

A function that calls itself is known as a **recursive function**, and each self-call is called a **recursive call**.

Recursion is widely used in programming because many problems can naturally be divided into smaller subproblems. Examples include calculating factorials, generating Fibonacci numbers, traversing trees, and solving problems such as Tower of Hanoi.

## Example Code

```cpp
#include <iostream>
using namespace std;

void printMessage(int n)
{
    if(n == 0)
        return;

    cout << "Hello Mohit" << endl;

    printMessage(n - 1);
}

int main()
{
    printMessage(5);

    return 0;
}
```

### Output
Hello Mohit
Hello Mohit
Hello Mohit
Hello Mohit
Hello Mohit

# Time Complexity
O(n)

# Space Complexity
O(n)

### 

The function starts with `n = 5`. Each time it prints the message and calls itself with a smaller value of `n`. When `n` becomes `0`, the function stops making further calls and returns.

## Understanding a Recursive Function

Every recursive function must contain two important parts:

### 1. Base Case

The base case is the stopping condition that terminates recursion.

Without a base case, the function would continue calling itself forever, eventually causing a stack overflow.

Example:

```cpp
if(n == 0)
    return;
```

### 2. Recursive Case

The recursive case is the part where the function calls itself with a modified input.

Example:

```cpp
printMessage(n - 1);
```

This recursive call reduces the problem size and moves the function closer to the base case.

### General Structure of Recursion

```cpp
returnType functionName(parameters)
{
    if(baseCondition)
        return baseValue;

    return functionName(modifiedParameters);
}
```

A recursive function repeatedly reduces the problem until the base condition is satisfied.

## How Recursion Works

To understand recursion, it is important to understand the **call stack**.

Whenever a function is called, the system stores information about that function in memory. This stored information is called a **stack frame**.

In recursion:

1. A function calls itself.
2. A new stack frame is created.
3. Another recursive call creates another stack frame.
4. This continues until the base case is reached.
5. Functions then return one by one.

This process consists of two phases:

### Descending Phase

The function keeps calling itself and moving deeper into recursion.

### Ascending Phase

After reaching the base case, functions start returning one by one and the call stack begins to shrink.

## Example: Understanding the Call Stack

```cpp
#include <iostream>
using namespace std;

void show(int n)
{
    cout << "Entering Function " << n << endl;

    if(n > 1)
    {
        show(n - 1);
    }

    cout << "Leaving Function " << n << endl;
}

int main()
{
    show(3);

    return 0;
}
```

### Output
Entering Function 3
Entering Function 2
Entering Function 1
Leaving Function 1
Leaving Function 2
Leaving Function 3

# Time Complexity
O(n)

# Space Complexity
O(n)

### 

The output clearly shows how recursive calls move deeper first and then return back one by one.

## Memory Management in Recursion

Like any other function, a recursive function uses memory.

Each recursive call creates a separate stack frame containing:

- Function parameters
- Local variables
- Return address
- Execution state

As recursion goes deeper, more stack frames are added to memory.

When the base case is reached:

1. The topmost function completes.
2. Its stack frame is removed.
3. Control returns to the previous function.
4. This process continues until all stack frames are removed.

Unlike loops, recursion relies heavily on the call stack, which increases memory usage.

## Stack Overflow

A stack overflow occurs when the program uses more stack memory than the system allows.

This usually happens when:

- A base case is missing.
- The base case is incorrect.
- Too many recursive calls are made.

Example of Infinite Recursion:

```cpp
#include <iostream>
using namespace std;

void recurse()
{
    cout << "Running..." << endl;

    recurse();
}

int main()
{
    recurse();

    return 0;
}
```

Since there is no base condition, the function keeps calling itself indefinitely until the program crashes with a stack overflow error.

## Applications of Recursion

Recursion is used in many important algorithms and data structures.

### Problem Solving

Many problems are naturally recursive, including:

- Factorial
- Fibonacci Series
- Tower of Hanoi

### Divide and Conquer Algorithms

Recursion forms the foundation of:

- Merge Sort
- Quick Sort
- Binary Search

### Backtracking Algorithms

Used in problems such as:

- N-Queens Problem
- Sudoku Solver
- Maze Solving

### Tree and Graph Traversal

Recursion is commonly used for:

- Depth First Search (DFS)
- Binary Tree Traversals
- Graph Traversals

## Advantages of Recursion

- Produces shorter and cleaner code.
- Simplifies complex problems.
- Useful for tree and graph structures.
- Naturally fits divide-and-conquer algorithms.
- Makes certain mathematical problems easier to implement.

## Limitations of Recursion

Although recursion is powerful, it also has some drawbacks.

### Performance Overhead

Each recursive call creates a new stack frame, which increases execution overhead.

### Higher Memory Usage

Recursion consumes additional memory because every function call is stored on the call stack.

### Difficult Debugging

Tracking multiple recursive calls can be challenging, especially in deeply nested recursion.

### Stack Overflow Risk

Deep or infinite recursion can exhaust stack memory and terminate the program.

## Recursion vs Iteration

| Feature | Recursion | Iteration |
| --- | --- | --- |
| Uses Function Calls | Yes | No |
| Uses Call Stack | Yes | No |
| Memory Usage | Higher | Lower |
| Code Length | Usually Shorter | Usually Longer |
| Performance | Slightly Slower | Usually Faster |
| Risk of Stack Overflow | Yes | No |

In practice, iteration is often preferred when performance and memory efficiency are important, while recursion is preferred when it leads to a simpler and more natural solution.

## Summary

Recursion is a technique in which a function solves a problem by calling itself. Every recursive function must contain a base case to stop recursion and a recursive case to reduce the problem size. Internally, recursion relies on the call stack to manage function calls. It is widely used in algorithms involving divide-and-conquer, backtracking, trees, and graphs. Although recursion can produce elegant solutions, it consumes additional memory and may lead to stack overflow if not implemented carefully.




