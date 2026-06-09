# Loops in C++

Loops are control structures that allow a set of statements to be executed repeatedly until a specified condition becomes false. They help reduce code duplication, improve readability, and make programs more efficient.

For example, if we want to print **"Hello World"** five times, writing the same statement repeatedly is unnecessary. A loop can perform the same task using only a few lines of code.

## Why Use Loops?

Loops are useful when:

- A task needs to be repeated multiple times.
- The number of repetitions is known or can be determined at runtime.
- We want to reduce repetitive code.
- We need to process arrays, vectors, strings, or other collections of data.

### Example Without a Loop

```cpp
#include <iostream>
using namespace std;

int main() {

    cout << "Hello World" << endl;
    cout << "Hello World" << endl;
    cout << "Hello World" << endl;
    cout << "Hello World" << endl;
    cout << "Hello World" << endl;

    return 0;
}
```

### Output
Hello World
Hello World
Hello World
Hello World
Hello World

### Example Using a Loop

```cpp
#include <iostream>
using namespace std;

int main() {

    for(int i = 0; i < 5; i++) {
        cout << "Hello World" << endl;
    }

    return 0;
}
```

### Output
Hello World
Hello World
Hello World
Hello World
Hello World

### 

The loop version is shorter, cleaner, and easier to modify.

# Types of Loops in C++

C++ provides the following looping constructs:

1. `for` Loop
2. `while` Loop
3. `do-while` Loop
4. Range-Based `for` Loop (For Each Loop)

Each loop performs repetitive execution but is used in different situations.

# 1. for Loop

The `for` loop is an **entry-controlled loop**, meaning the condition is checked before entering the loop body.

It is most suitable when the number of iterations is known in advance.

## Syntax

```cpp
for(initialization; condition; update)
{
    // loop body
}
```

### Components

- **Initialization**: Executes once at the beginning.
- **Condition**: Checked before each iteration.
- **Update**: Executes after every iteration.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1781013309940-12.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    for(int i = 1; i <= 5; i++) {
        cout << i << " ";
    }

    return 0;
}
```

### Output
1 2 3 4 5

# Time Complexity
O(n)

# Space Complexity
O(1)

### **Explanation**

- The loop starts with `i = 1`.
- It continues while `i <= 5`.
- After each iteration, `i` is incremented by 1.
- The loop stops when `i` becomes 6.

# 2. while Loop

The `while` loop is also an **entry-controlled loop**. It is generally used when the number of iterations is not known beforehand.

The loop continues as long as the condition remains true.

## Syntax

```cpp
while(condition)
{
    // loop body
}
```

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1781013514736-13.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int count = 1;

    while(count <= 5) {
        cout << count << " ";
        count++;
    }

    return 0;
}
```

### Output
1 2 3 4 5

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

- `count` starts from 1.
- The condition is checked before each iteration.
- The value is printed and incremented.
- The loop terminates when `count` becomes 6.

# 3. do-while Loop

The `do-while` loop is an **exit-controlled loop**. The condition is checked after the loop body executes.

As a result, the loop body executes at least once.

## Syntax

```cpp
do
{
    // loop body
}
while(condition);
```

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/loops-in-c/1781013553643-14.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int num = 1;

    do {
        cout << num << " ";
        num++;
    }
    while(num <= 5);

    return 0;
}
```

### Output
1 2 3 4 5

### 

- The loop body executes first.
- The condition is checked afterward.
- Even if the condition is initially false, the body executes once.

### Important Note

A semicolon (`;`) is required after the `while(condition)` statement.

# 4. Range-Based for Loop (For Each Loop)

The range-based `for` loop was introduced in C++11. It simplifies traversing arrays and containers.

It automatically accesses each element one by one without requiring an index variable.

## Syntax

```cpp
for(dataType variable : container)
{
    // loop body
}
```

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int marks[] = {75, 80, 90, 85, 95};

    for(auto score : marks) {
        cout << score << " ";
    }

    return 0;
}
```

### Output
75 80 90 85 95

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

- The loop automatically visits each element.
- No indexing is required.
- The variable `score` stores one element at a time.

# Infinite Loops

An infinite loop is a loop that never terminates because its condition never becomes false.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    while(true) {
        cout << "Loop Running" << endl;
    }

    return 0;
}
```

### 

Since the condition `true` is always true, the loop continues forever unless terminated externally.

### Common Reasons

- Missing update statement.
- Incorrect loop condition.
- Intentional endless processing.

# Nested Loops

A nested loop is a loop placed inside another loop.

The inner loop executes completely for every iteration of the outer loop.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    for(int i = 1; i <= 3; i++) {

        for(int j = 1; j <= 2; j++) {
            cout << "(" << i << "," << j << ") ";
        }

        cout << endl;
    }

    return 0;
}
```

### Output
(1,1) (1,2)
(2,1) (2,2)
(3,1) (3,2)

# Time Complexity
O(n × m)

# Space Complexity
O(1)

### Output

### Explanation

- Outer loop runs 3 times.
- Inner loop runs 2 times for each outer iteration.
- Total executions = 3 × 2 = 6.

# Loop Control Statements

Loop control statements modify the normal execution flow of loops.

## break Statement

The `break` statement immediately terminates the loop.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    for(int i = 1; i <= 5; i++) {

        if(i == 4)
            break;

        cout << i << " ";
    }

    return 0;
}
```

### Output
1 2 3

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

When `i` becomes 4, the `break` statement stops the loop immediately.

## continue Statement

The `continue` statement skips the remaining statements in the current iteration and proceeds to the next iteration.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    for(int i = 1; i <= 5; i++) {

        if(i == 3)
            continue;

        cout << i << " ";
    }

    return 0;
}
```

### Output
1 2 4 5

# Time Complexity
O(n)

# Space Complexity
O(1)

### 

When `i` becomes 3, the `continue` statement skips printing and moves directly to the next iteration.

# Summary

Loops allow repeated execution of a block of code, making programs shorter, cleaner, and more efficient.

The major looping constructs in C++ are:

- `for` Loop
- `while` Loop
- `do-while` Loop
- Range-Based `for` Loop

Additional concepts such as infinite loops, nested loops, `break`, and `continue` provide greater control over loop execution and are widely used in real-world programming applications.




