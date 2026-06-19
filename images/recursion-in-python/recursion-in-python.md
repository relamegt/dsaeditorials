# Recursion in Python

## Introduction

Recursion is a programming technique in which a function calls itself directly or indirectly to solve a problem. Instead of solving a problem all at once, recursion breaks it into smaller subproblems until a simple stopping condition is reached.

Recursive solutions are widely used in mathematical calculations, tree and graph traversals, divide-and-conquer algorithms, and many other problems where a repetitive pattern exists.

### Key Features

- A function calls itself repeatedly.
- Problems are divided into smaller subproblems.
- Requires a base case to stop recursion.
- Uses the call stack to store function calls.
- Produces elegant solutions for complex problems.
- Commonly used in trees, graphs, and mathematical computations.

# Why Use Recursion?

Some problems naturally follow a self-similar pattern. Recursion allows such problems to be expressed in a simple and readable manner.

### Example

To calculate factorial of 5:

```Code
5! = 5 × 4!
4! = 4 × 3!
3! = 3 × 2!
2! = 2 × 1!
1! = 1
```

Instead of writing multiple multiplication statements, recursion solves the problem by repeatedly calling the same function with smaller values.

# Structure of a Recursive Function

Every recursive function contains two essential parts:

1. Base Case
2. Recursive Case

### Syntax

```python
def recursive_function(parameters):

    if base_condition:
        return result

    return recursive_function(modified_parameters)
```

### Explanation

- The base case stops recursion.
- The recursive case calls the function again with modified values.

# Working of Recursion

Consider calculating factorial of 4.

```Code
factorial(4)
↓
4 × factorial(3)
↓
3 × factorial(2)
↓
2 × factorial(1)
↓
1 × factorial(0)
↓
1
```

After reaching the base case, the function returns back through each previous call.

# Factorial Using Recursion

### Example

```python
def factorial(n):

    if n == 0:
        return 1

    return n * factorial(n - 1)

print(factorial(5))
```

### Output
120

### Explanation

The function repeatedly multiplies `n` by factorial of `n-1` until `n` becomes 0.

# Fibonacci Series Using Recursion

### Example

```python
def fibonacci(n):

    if n == 0:
        return 0

    if n == 1:
        return 1

    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))
```

### Output
55

### Explanation

Each Fibonacci number is obtained by adding the previous two Fibonacci numbers.

# Sum of Natural Numbers

### Example

```python
def sum_numbers(n):

    if n == 1:
        return 1

    return n + sum_numbers(n - 1)

print(sum_numbers(5))
```

### Output
15

### Explanation

The function adds numbers from 5 down to 1.

# Printing Numbers Using Recursion

### Example

```python
def display(n):

    if n == 0:
        return

    display(n - 1)

    print(n)

display(5)
```

### Output
1
2
3
4
5

### Explanation

Recursive calls reach the base case first, and then numbers are printed while returning.

# Types of Recursion

Recursion can be categorized into different types.

## 1. Direct Recursion

A function directly calls itself.

### Example

```python
def count_down(n):

    if n == 0:
        return

    print(n)

    count_down(n - 1)

count_down(3)
```

### Output
3
2
1

## 2. Indirect Recursion

Functions call one another.

### Example

```python
def even(n):

    if n == 0:
        return True

    return odd(n - 1)

def odd(n):

    if n == 0:
        return False

    return even(n - 1)

print(even(4))
```

### Output
True

## 3. Tail Recursion

The recursive call is the last statement executed.

### Example

```python
def tail_factorial(n, result=1):

    if n == 0:
        return result

    return tail_factorial(
        n - 1,
        result * n
    )

print(tail_factorial(5))
```

### Output
120

### Explanation

No additional work remains after the recursive call.

## 4. Non-Tail Recursion

Some operation occurs after the recursive call.

### Example

```python
def factorial(n):

    if n == 0:
        return 1

    return n * factorial(n - 1)

print(factorial(5))
```

### Output
120

### Explanation

Multiplication occurs after the recursive call returns.

# Recursive Binary Search

### Example

```python
def binary_search(arr, low, high, key):

    if low > high:
        return -1

    mid = (low + high) // 2

    if arr[mid] == key:
        return mid

    if key < arr[mid]:
        return binary_search(
            arr,
            low,
            mid - 1,
            key
        )

    return binary_search(
        arr,
        mid + 1,
        high,
        key
    )

arr = [10, 20, 30, 40, 50]

print(binary_search(arr, 0, 4, 40))
```

### Output
3

# Advantages of Recursion

1. Produces clean and elegant code.
2. Simplifies complex problems.
3. Useful for tree and graph traversals.
4. Naturally fits divide-and-conquer algorithms.
5. Reduces the need for explicit loops.

# Limitations of Recursion

1. Uses extra memory because of function calls.
2. Slower than iterative solutions in many cases.
3. Deep recursion may cause stack overflow.
4. Excessive recursive calls can increase execution time.

# Recursion vs Iteration

| Feature | Recursion | Iteration |
| --- | --- | --- |
| Repetition | Function calls itself | Uses loops |
| Memory Usage | Higher | Lower |
| Speed | Slower | Faster |
| Stack Usage | Uses call stack | No stack overhead |
| Risk | Stack overflow possible | No stack overflow |
| Best For | Trees, graphs, divide-and-conquer | Sequential repetition |

# When to Avoid Recursion?

Avoid recursion when:

- The problem can be solved easily using loops.
- Recursion depth becomes very large.
- Memory usage is critical.
- Performance is extremely important.

# Recursion Limit in Python

Python restricts the number of recursive calls to avoid stack overflow.

### Example

```python
import sys

print(sys.getrecursionlimit())
```

### Output
1000

### Explanation

Python allows approximately 1000 recursive calls by default.

# Applications of Recursion

- Factorial calculation
- Fibonacci sequence
- Tower of Hanoi
- Binary Search
- Tree Traversals
- Graph Traversals
- Merge Sort
- Quick Sort
- Dynamic Programming
- Backtracking algorithms etc..

# Summary

Recursion is a technique in which a function calls itself to solve smaller instances of the same problem. Every recursive function requires a base case to stop execution and a recursive case to continue processing. Recursion provides elegant solutions for problems involving trees, graphs, divide-and-conquer strategies, and mathematical computations. Although recursive solutions are often easier to understand, they consume more memory and may lead to stack overflow if used improperly. Understanding recursion is essential for mastering advanced algorithms and data structures.

