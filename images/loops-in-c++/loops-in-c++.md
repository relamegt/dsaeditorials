# Loops in C++

## Introduction

Loops are control flow structures that execute a block of instructions repeatedly as long as a specified condition remains true. They eliminate redundant code, reduce errors, and make applications more concise and maintainable. 

Instead of manually duplicating code statements, a loop allows developers to run the same block of code hundreds or thousands of times using just a few lines.

### Key Features

- Repeats execution of a statement block based on a boolean condition.
- Minimizes code redundancy and file size.
- Simplifies operations on collections like arrays, vectors, and lists.
- Controls execution flow dynamically using initialization, condition, and update expressions.

## Why Use Loops?

Imagine a scenario where we need to print a message three times.

### Duplicating Code Manually

```Cpp
#include <iostream>
using namespace std;

int main() {
    cout << "AlphaKnowledge C++ Tutorial" << endl;
    cout << "AlphaKnowledge C++ Tutorial" << endl;
    cout << "AlphaKnowledge C++ Tutorial" << endl;

    return 0;
}
```

### Output
AlphaKnowledge C++ Tutorial
AlphaKnowledge C++ Tutorial
AlphaKnowledge C++ Tutorial

If the requirement changes to print the message a hundred times, duplicating the lines becomes completely impractical.

### Implementing a Loop

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 0; i < 3; i++) {
        cout << "AlphaKnowledge C++ Tutorial" << endl;
    }

    return 0;
}
```

### Output
AlphaKnowledge C++ Tutorial
AlphaKnowledge C++ Tutorial
AlphaKnowledge C++ Tutorial

The loop manages the repetition automatically, executing the output block exactly three times.

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1782644335718-1781013309940-12.png)

## Types of Loops in C++

C++ supports four primary looping structures:

1. `for` Loop
2. `while` Loop
3. `do-while` Loop
4. Range-based `for` Loop (introduced in C++11)

## 1. The for Loop

The standard `for` loop is an entry-controlled loop, meaning the condition is checked before entering the loop body. It is typically used when the exact number of iterations is known beforehand.

**Syntax:**

```Cpp
for (initialization; condition; update) {
    // loop body
}
```

- **Initialization:** Declares and sets the loop counter variable. Runs only once at the start.
- **Condition:** Evaluated before each iteration. If true, the body executes. If false, the loop terminates.
- **Update:** Modifies the loop counter after the body executes, then checks the condition again.

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 3; i <= 15; i += 3) {
        cout << i << " ";
    }
    cout << endl;
    return 0;
}
```

### Output
3 6 9 12 15

### Example: Tracking User IDs

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int userID = 1001; userID <= 1005; userID++) {
        cout << "User ID: " << userID << endl;
    }
    return 0;
}
```

### Output
User ID: 1001
User ID: 1002
User ID: 1003
User ID: 1004
User ID: 1005

## 2. The while Loop

The `while` loop is also an entry-controlled loop. It executes a statement block repeatedly as long as its condition remains true. It is preferred when the number of iterations is not known in advance and depends on dynamic conditions.

**Syntax:**

```Cpp
while (condition) {
    // loop body
    // update statement
}
```

The loop variable must be initialized before the loop starts, and the update statement must be included inside the loop body.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int count = 5;

    while (count >= 1) {
        cout << count << " ";
        count--;
    }
    cout << endl;
    return 0;
}
```

### Output
5 4 3 2 1

### Example: Displaying Multiples of 5

```Cpp
#include <iostream>
using namespace std;

int main() {
    int num = 5;

    while (num <= 25) {
        cout << num << " ";
        num += 5;
    }
    cout << endl;
    return 0;
}
```

### Output
5 10 15 20 25

## While Loop work flow:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1782644462906-1781013514736-13.png)

## **3. The do-while Loop**

The `do-while` loop is an exit-controlled loop. The loop body is executed first, and the condition is evaluated afterward. This guarantees that the loop body will run **at least once**, even if the condition is false from the start.

**Syntax:**

```Cpp
do {
    // loop body
    // update statement
} while (condition);
```

Note the semicolon at the end of the `while (condition);` line.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int count = 10;

    do {
        cout << count << " ";
        count += 10;
    } while (count <= 50);
    cout << endl;
    return 0;
}
```

### Output
10 20 30 40 50

### Example: Running at Least Once with a False Condition

```Cpp
#include <iostream>
using namespace std;

int main() {
    int speed = 120;

    do {
        cout << "Current speed: " << speed << " km/h" << endl;
    } while (speed < 60);

    return 0;
}
```

### Output
Current speed: 120 km/h

Even though `speed < 60` is false, the loop body executes once before checking the condition.

## 

## do-while Loop work flow:

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1782644414115-1781013553643-14.png)

## 4. Range-Based for Loop (C++11)

The range-based `for` loop provides a simpler way to iterate through all elements of a collection, such as arrays or vectors. It eliminates the need for manual indexing and loop counters, reducing the chance of out-of-bounds errors.

**Syntax:**

```Cpp
for (declaration : collection) {
    // loop body
}
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    int prices[] = {15, 25, 35, 45};

    cout << "Item Prices: ";
    for (int price : prices) {
        cout << price << " ";
    }
    cout << endl;
    return 0;
}
```

### Output
Item Prices: 15 25 35 45

## Infinite Loops

An infinite loop is a loop whose exit condition is never met. It runs indefinitely until the program is manually terminated or crashes due to memory exhaustion.

### Infinite for Loop

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (;;) {
        cout << "Server active..." << endl;
    }
    return 0;
}
```

### Output
Server active...
Server active...
Server active...

### Infinite while Loop

```Cpp
#include <iostream>
using namespace std;

int main() {
    while (true) {
        cout << "Listening for connections..." << endl;
    }
    return 0;
}
```

### Output
Listening for connections...
Listening for connections...
Listening for connections...

## Nested Loops

A nested loop is a loop declared inside the body of another loop. The inner loop executes its full set of iterations for every single iteration of the outer loop.

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int row = 1; row <= 3; row++) {
        for (int col = 1; col <= 2; col++) {
            cout << "Row: " << row << ", Col: " << col << endl;
        }
    }
    return 0;
}
```

### Output
Row: 1, Col: 1
Row: 1, Col: 2
Row: 2, Col: 1
Row: 2, Col: 2
Row: 3, Col: 1
Row: 3, Col: 2

## Loop Control Statements

Loop control statements interrupt or modify the default sequential execution flow of a loop.

| Statement | Action |
| --- | --- |
| `break` | Immediately terminates the loop and transfers execution to the statement following the loop |
| `continue` | Skips the remaining statements in the current iteration and jumps to the next iteration / update phase |
| `goto` | Jumps directly to a defined label elsewhere in the same function |

### The break Statement

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int count = 1; count <= 5; count++) {
        if (count == 4) {
            break;  // Exit the loop immediately
        }
        cout << count << " ";
    }
    cout << endl;
    return 0;
}
```

### Output
1 2 3

### The continue Statement

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int count = 1; count <= 5; count++) {
        if (count == 3) {
            continue;  // Skip printing 3 and jump to next iteration
        }
        cout << count << " ";
    }
    cout << endl;
    return 0;
}
```

### Output
1 2 4 5

### The goto Statement

```Cpp
#include <iostream>
using namespace std;

int main() {
    for (int count = 1; count <= 5; count++) {
        if (count == 4) {
            goto cleanup;  // Jump directly to the cleanup label
        }
        cout << count << " ";
    }
cleanup:
    cout << "\nTerminated early and jumped to cleanup." << endl;
    return 0;
}
```

### Output
1 2 3 
Terminated early and jumped to cleanup.

## Comparison of C++ Loop Structures

| Feature | `for` Loop | `while` Loop | `do-while` Loop | Range-based `for` Loop |
| --- | --- | --- | --- | --- |
| **Control Type** | Entry-controlled | Entry-controlled | Exit-controlled | Entry-controlled |
| **Condition Check** | Before execution | Before execution | After execution | Implicitly per element |
| **Minimum Iterations** | 0 | 0 | 1 | 0 (if collection is empty) |
| **Best Use Case** | Known iteration count | Dynamic condition | At least one run needed | Traversing arrays/STL containers |
| **Variables Scoped To** | Loop block (if declared inside) | External scope | External scope | Loop block |

## Advantages of Loops

- **Code Reusability:** Writes logic once and executes it multiple times.
- **Reduces Complexity:** Keeps code readable and short.
- **Dynamic Control:** Adjusts iteration counts dynamically based on runtime variables or input.
- **Collection Traversal:** Essential for working with array elements and standard library containers.

## Limitations

- **Infinite Execution:** Missing or incorrect loop conditions cause programs to hang indefinitely.
- **Readability Overhead:** Heavily nested loops make code difficult to follow and maintain.
- **Performance Impact:** Excessive iterations in nested loops can significantly increase execution time (high time complexity).

> **Note:** In C++, when writing standard `for` loops, prefer using the prefix increment operator (`++i`) over the postfix increment operator (`i++`) in the update expression. While they perform identically for built-in integer types, using `++i` is a better habit because it does not create a temporary copy of the iterator or loop variable, which saves memory overhead when iterating over complex C++ Standard Template Library (STL) classes.

## Summary

Loops in C++ are control flow mechanisms that execute a statement block repeatedly based on a boolean condition. C++ supports entry-controlled loops (`for` and `while`), where the condition is evaluated before execution, and the exit-controlled loop (`do-while`), which guarantees the body executes at least once. C++11 also introduced range-based `for` loops to simplify array and container traversal without manual indexing. Loop execution can be altered using control statements like `break` (to exit immediately), `continue` (to skip the current iteration), or `goto` (to jump to a label). Proper selection and management of loop conditions are critical to avoid infinite loops and maintain optimal performance.




