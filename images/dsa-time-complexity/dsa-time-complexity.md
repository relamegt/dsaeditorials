# DSA Time Complexity

In computer science and data structures, evaluating an algorithm's performance requires understanding its runtime—the computational time needed to execute its logic. Analyzing this performance ensures that software remains scalable and responsive as the volume of input data grows.

## Principles of Algorithm Runtime

Exploring runtime is essential for designing robust software. Implementing an inefficient sorting or search algorithm can cause system freezes, performance bottlenecks, or even application crashes when processing production-scale datasets.

## Actual Runtime vs. Time Complexity

To measure how fast an algorithm executes, we must distinguish between its physical run duration and its abstract operational complexity:

### Limits of Actual Runtime

Relying on a stopwatch to measure the exact seconds a program takes to execute is unreliable because it depends on several transient factors:

- The programming language chosen for implementation.
- The specific style and optimization techniques applied by the coder.
- The compiler flags or interpreter version running the execution.
- The hardware capabilities (CPU speed, cache size, memory bandwidth).
- Concurrent operating system background processes.
- The size of the input data block.

### Abstracting Time Complexity

To compare algorithms independently of hardware and language, computer science uses time complexity. Time complexity abstracts runtime by counting the number of basic operations (such as comparisons, swaps, or arithmetic calculations) required to process a dataset of size **n**. Since CPUs execute operations in constant cycles, the operation count correlates directly with physical execution time.

- *Linear Example*: Finding the lowest value in an unsorted list of **n** elements requires scanning and comparing each element exactly once. This creates a linear relationship: searching 100 items requires 100 operations, while 5,000 items requires 5,000 operations.

## The "One Operation" Abstraction

An "operation" represents a basic step in an algorithm that takes constant time. An action takes constant time if its execution speed is independent of the size of the input dataset **n**.

- *Example*: Comparing two array elements or swapping their memory slots takes the same amount of time whether the array contains 10 elements or 1,000,000 elements.
- *Constant-Time Operations*: Assigning a variable, checking a boolean condition, or looking up an array index (e.g., accessing `DeviceRegistry[42]`) are all treated as single, constant-time operations.

## Big O Notation

In mathematics, Big O notation defines the asymptotic upper bound of a function. In computer science, it describes the worst-case time complexity of an algorithm, representing the maximum execution time required for an input of size **n**.

### Time Complexity Classes with Examples

- **Constant Time - O(1)**: Execution speed is independent of data size. An example is looking up a record directly by index:

`````Sql
-- Accessing a value directly by array index
  print(DeviceRegistry[97]);
```

- **Linear Time - O(n)**: Execution speed grows in direct proportion to data size. An example is finding the minimum value in an unsorted array, which requires scanning all **n** elements.
- **Quadratic Time - O(n^2)**: Execution speed grows quadratically. Algorithms containing nested loops (such as Bubble Sort, Selection Sort, or Insertion Sort) exhibit this complexity. Doubling the dataset size from 100 to 200 elements can increase operations by up to 30,000.
- **Linearithmic Time - O(n log n)**: Typical average-case complexity for efficient divide-and-conquer sorting algorithms (such as Quicksort or Mergesort).

The following chart illustrates how execution times scale relative to the size of the dataset **n** for these different complexity classes:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/dsa-time-complexity/1784485416273-time_complexity_comparison.png)

## Execution Scenarios: Best, Average, and Worst Cases

An algorithm's runtime can vary depending on the initial state of the input data, even when the dataset size **n** remains constant:

- **Uniform Case Algorithms**: Some algorithms perform the same number of steps regardless of data order. For instance, finding the lowest value in an unsorted list always requires scanning all **n** elements.
- **Value-Dependent Case Algorithms**: For sorting algorithms, input order dramatically impacts speed. We can analyze this using two custom scenarios:
- **Mohit** sorts a highly scrambled array of device IDs: `[12, 5, 19, 2, 8, 17]`. The sorting algorithm must perform multiple comparisons and swaps to order the list.
- **Akash** sorts a nearly sorted array: `[2, 5, 8, 12, 17, 19]`. The algorithm detects the existing order quickly, completing with minimal swaps.

To ensure performance guarantees, computer scientists evaluate time complexity using the worst-case scenario.

## Mathematical Definition of Big O

Mathematically, Big O establishes that one function dominates another as the input variable grows toward infinity.

### The Bounded Growth Inequality

Let **f(n)** and **g(n)** be two functions. We say that **f(n)** is **O(g(n))** if and only if there exist positive constants **C** and **n_0** such that:

**C * g(n) &gt; f(n)** for all **n &gt; n_0**.

This means that for all data sizes larger than threshold **n_0**, the function **C * g(n)** acts as an upper ceiling for **f(n)**.

### Custom Mathematical Walkthrough

Consider the runtime function:

**f(n) = 0.6n^2 + 3n + 5**

The graph for this runtime function **f** looks like this:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/dsa-time-complexity/1784485478754-runtime_function_plot.png)

Consider another function:

**g(n) = n^2**

Which we can draw like this:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/dsa-time-complexity/1784485537533-bounding_function_plot.png)

We select this bounding function **g(n) = n^2** to test if **f(n)** is **O(n^2)**:

1. We choose constant **C = 2**, giving the bounding equation:

   **2n^2 &gt; 0.6n^2 + 3n + 5**

1. Subtracting **0.6n^2** from both sides yields:

   **1.4n^2 &gt; 3n + 5**

1. We solve for the threshold value **n_0** where this inequality holds:

- For **n = 3**: **1.4(9) = 12.6**, and **3(3) + 5 = 14**. Since **12.6 &lt; 14**, the inequality does not hold.
- For **n = 4**: **1.4(16) = 22.4**, and **3(4) + 5 = 17**. Since **22.4 &gt; 17**, the inequality holds.

1. For all values **n &gt;= 4**, **2n^2** remains strictly greater than **0.6n^2 + 3n + 5**. Therefore, choosing **C = 2** and **n_0 = 4** proves that **f(n)** is **O(n^2)**.

The following graph visually demonstrates this bounding proof. For all inputs to the right of **n_0 = 4**, the bounding function **C * g(n) = 2n^2** lies strictly above **f(n) = 0.6n^2 + 3n + 5** (indicated by the shaded upper bound zone):

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/dsa-time-complexity/1784485565836-mathematical_bounding_proof.png)

## Comparison of Time Complexity Classes

| Complexity Class | Operations Growth Rate | System Scalability | Typical Algorithm | Operations for n=1,000 |
| --- | --- | --- | --- | --- |
| **O(1)** | Constant (flat line) | Excellent (unaffected by scale) | Index-based lookup | 1 |
| **O(log n)** | Logarithmic (highly tapered growth) | Excellent (scales to billions easily) | Binary Search | ~10 |
| **O(n)** | Linear (straight proportional line) | Good (scales well for single scans) | Linear Search | 1,000 |
| **O(n log n)** | Linearithmic (slight upward curve) | Good (standard for sorting scales) | Mergesort / Quicksort | ~10,000 |
| **O(n^2)** | Quadratic (steep exponential curve) | Poor (unusable for large datasets) | Bubble Sort / Selection Sort | 1,000,000 |

> **Key Insight**: Time complexity focuses on asymptotic behavior as input size **n** approaches infinity. While low-order terms and coefficients (like the `3n + 5` in `0.6n^2 + 3n + 5`) dominate runtime for small datasets, they become mathematically insignificant as **n** grows very large, leaving the highest-order term (`n^2`) to define the algorithm's scalability.

# Summary

Time complexity provides an abstract, hardware-independent framework to evaluate and compare algorithm execution speeds. By counting basic operations rather than measuring physical runtime seconds, Big O notation establishes worst-case boundaries for data growth. Algorithms fall into classes ranging from highly efficient constant-time index lookups to poor quadratic-time sorting loops. Applying Big O mathematics ensures that database engines and software systems select algorithms that can scale efficiently without causing resource starvation or system latency.




