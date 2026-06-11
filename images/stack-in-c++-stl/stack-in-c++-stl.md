# Stack in C++ STL

A **Stack** is a linear data structure that follows the **LIFO (Last In First Out)** principle. This means that the element inserted last is the first element to be removed, while the element inserted first is removed last.

You can think of a stack like a pile of books placed one on top of another. When you want to remove a book, you always remove the book from the top. Similarly, when adding a new book, it is placed on the top of the pile.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stack-in-c-stl/1781177964705-4d8e9646-a4c5-47d0-b642-90bd36718446.png)

Only the top element is directly accessible.

The C++ Standard Template Library (STL) provides a ready-made implementation of the stack data structure through the `std::stack` container adapter.

# Why Do We Need a Stack?

Stacks are useful whenever data needs to be processed in reverse order of insertion.

Common applications include:

- Function Call Management
- Undo and Redo Operations
- Browser History
- Expression Evaluation
- Parentheses Matching
- Backtracking Algorithms
- Depth First Search (DFS)
- Compiler Design

For example, when using the Undo feature in a text editor, the most recent action is undone first, which perfectly follows the LIFO principle.

# Real-World Example

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stack-in-c-stl/1781178140092-202b2bb8-c2fe-4505-a1f7-621ea9796505.png)

The most recently added plate leaves first.

This is exactly how a stack works.

# Stack Header File

The stack container is defined inside the `<stack>` header file.

Before using a stack, include:

```cpp
#include <stack>
```

Most programs also include:

```cpp
#include <iostream>
using namespace std;
```

for input and output operations.

# Declaration of Stack

A stack can be declared using the following syntax:

## Syntax

```cpp
stack<dataType> stackName;
```

### Example

```cpp
stack<int> marks;
```

Here:

- `stack` → STL Stack Container
- `int` → Type of elements stored
- `marks` → Stack name

The stack can store integer values.

# Example Program

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> marks;

    marks.push(85);
    marks.push(90);
    marks.push(95);

    cout << marks.top();

    return 0;
}
```

### Output
95
The most recently inserted element appears at the top.

# Memory Representation of Stack

Consider:

```cpp
stack<int> st;

st.push(10);
st.push(20);
st.push(30);
st.push(40);
```

Internal representation:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stack-in-c-stl/1781178208972-4d8e9646-a4c5-47d0-b642-90bd36718446.png)

The element 40 is at the top and will be removed first.

# Basic Operations on Stack

The most common operations performed on a stack are:

1. push()
2. top()
3. pop()
4. empty()
5. size()

# Inserting Elements using push()

The `push()` function inserts a new element at the top of the stack.

Whenever a new element is pushed, it becomes the new top element.

## Syntax

```cpp
stackName.push(value);
```

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> scores;

    scores.push(50);
    scores.push(75);
    scores.push(100);

    cout << scores.top();

    return 0;
}
```

### Output
100

# Time Complexity
O(1)

### Explanation

The values are inserted in the order:
50 → 75 → 100
Since 100 was inserted last, it becomes the top element.

### 

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stack-in-c-stl/1781178274555-4d8e9646-a4c5-47d0-b642-90bd36718446.png)

# Accessing Elements using top()

The `top()` function returns the element present at the top of the stack.

It does not remove the element.

## Syntax

```cpp
stackName.top();
```

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<string> students;

    students.push("Mohit");
    students.push("Akash");
    students.push("Hemesh");

    cout << students.top();

    return 0;
}
```

### Output
Hemesh

# Time Complexity
O(1)

### Explanation

The stack stores:
Mohit
Akash
Hemesh
Since Hemesh was inserted last, it becomes the top element.
The `top()` function only returns the value and does not remove it.

### 

# Removing Elements using pop()

The `pop()` function removes the topmost element from the stack.

Unlike `top()`, it does not return the removed value.

## Syntax

```cpp
stackName.pop();
```

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> st;

    st.push(10);
    st.push(20);
    st.push(30);

    st.pop();

    cout << st.top();

    return 0;
}
```

### Output
20

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/stack-in-c-stl/1781178335206-6387bc76-c3eb-409d-b6a6-7547e0e995a8.png)

### 

# Checking Whether Stack is Empty

The `empty()` function checks whether the stack contains any elements.

It returns:

- `true` → Stack is empty
- `false` → Stack contains elements

## Syntax

```cpp
stackName.empty();
```

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> st;

    if(st.empty())
    {
        cout << "Stack is Empty";
    }

    return 0;
}
```

### Output
Stack is Empty

# Time Complexity
O(1)

### Explanation

Since no elements are inserted into the stack, `empty()` returns true.

### 

# Finding Size of Stack

The `size()` function returns the total number of elements currently stored in the stack.

## Syntax

```cpp
stackName.size();
```

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> st;

    st.push(10);
    st.push(20);
    st.push(30);

    cout << st.size();

    return 0;
}
```

### Output
3

# Time Complexity
O(1)

### Explanation

Three elements are stored inside the stack.
Therefore, the size becomes 3.

### 

# Pseudo Traversal of Stack

Unlike vectors and arrays, stacks do not provide iterators.

Therefore, direct traversal is not possible.

To view all elements, a copy of the stack is usually created.

## Example Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> st;

    st.push(10);
    st.push(20);
    st.push(30);
    st.push(40);

    stack<int> temp(st);

    while(!temp.empty())
    {
        cout << temp.top() << " ";

        temp.pop();
    }

    return 0;
}
```

### Output
40 30 20 10

### Explanation

A copy of the original stack is created.
The copied stack is traversed using:

- top()
- pop()

The original stack remains unchanged.

# Common Stack Functions

The STL stack provides several useful functions.

### push()

Adds an element at the top.

### pop()

Removes the top element.

### top()

Returns the top element.

### empty()

Checks whether stack is empty.

### size()

Returns the number of elements.

### swap()

Exchanges contents of two stacks.

# Time Complexity of Stack Operations

| Operation | Complexity |
| --- | --- |
|  | - |
| push() | O(1) |
| pop() | O(1) |
| top() | O(1) |
| empty() | O(1) |
| size() | O(1) |

Most stack operations are extremely efficient.

# Advantages of Stack

### Simple Implementation

Stacks are easy to understand and implement.

### Fast Operations

Insertion and deletion occur in constant time.

### Useful in Recursion

Function calls internally use stacks.

### Memory Efficient

Operations occur only at one end.

### Supports Backtracking

Widely used in undo operations and DFS algorithms.

# Limitations of Stack

### Limited Access

Only the top element can be accessed.

### No Random Access

Elements in the middle cannot be directly accessed.

### Fixed Order

Only LIFO processing is supported.

### Traversal Restrictions

Direct iteration is not available.

# Real-World Applications of Stack

Stacks are used extensively in software development.

Examples include:

- Browser Back Button
- Undo and Redo Operations
- Function Call Stack
- Expression Evaluation
- Syntax Parsing
- Compiler Design
- Parentheses Matching
- Depth First Search (DFS)
- Backtracking Problems
- Navigation Systems

# Summary

A Stack is a linear data structure that follows the Last In First Out (LIFO) principle. The last element inserted into the stack is the first element removed. C++ STL provides the `stack` container adapter to efficiently implement stack operations. The most important functions are `push()`, `pop()`, `top()`, `empty()`, and `size()`. Stacks are widely used in recursion, expression evaluation, undo operations, browser history management, and various algorithmic problems.




