# Queue in C++ STL

A **Queue** is a linear data structure that follows the **FIFO (First In First Out)** principle. This means that the element inserted first into the queue will be removed first, and the element inserted later will be removed after all the elements before it have been processed.

A queue works similarly to many real-world situations that we encounter every day. For example, customers waiting at a bank counter, passengers standing in line for a bus, print jobs waiting for a printer, and support tickets waiting to be handled all follow the FIFO principle. The person or task that arrives first gets processed first.

In C++, the Standard Template Library (STL) provides the **queue container adapter**, which allows programmers to efficiently implement queue behavior without manually creating the data structure from scratch.

A queue allows insertion of elements only at the rear (back) and deletion of elements only from the front. This restriction helps maintain the FIFO order and makes queue operations very efficient.

Queues are widely used in operating systems, scheduling algorithms, networking, simulation software, task management systems, and graph traversal algorithms.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/queue-in-c-stl/1781179061521-5468edbe-98e1-4372-8b81-a279ffaf3b64.png)

# Why Do We Need Queues?

In many applications, maintaining the order of processing is extremely important.

Consider an online shopping website. Thousands of customer orders may arrive every minute. These orders must be processed in the same sequence in which they were received. If a customer who placed an order later receives service before earlier customers, it can create inconsistency and unfairness.

Similarly, in a printer system, multiple users may send documents to print. The printer processes the documents one after another in the order they were submitted.

Queues provide an organized and efficient way to handle such situations by ensuring fairness and maintaining processing order.

Without queues:

- Tasks may be processed randomly.
- Scheduling becomes difficult.
- Resource allocation becomes inefficient.
- System performance may degrade.

Therefore, queues play an essential role in software development and system design.

# Real-World Examples of Queue

Queues can be observed in many real-world situations:

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/queue-in-c-stl/1781178997042-453ec6ae-adc8-4cfc-9333-2905767ac826.png)

# Queue Header File

The Queue container is available in the STL and is defined inside the following header file:

```cpp
#include <queue>
```

Most queue programs also require:

```cpp
#include <iostream>
using namespace std;
```

for input and output operations.

# Declaration of Queue

A queue can be declared similarly to other STL containers.

## Syntax

```cpp
queue<dataType> queueName;
```

## Example

```cpp
queue<string> supportTickets;
```

Here:

- `queue` represents the STL Queue container.
- `string` represents the type of elements stored.
- `supportTickets` is the queue name.

# Creating and Using a Queue

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> supportTickets;

    supportTickets.push("Login Issue");
    supportTickets.push("Payment Failed");
    supportTickets.push("Account Verification");

    cout << "First Ticket: "
         << supportTickets.front();

    return 0;
}
```

### Output
First Ticket: Login Issue

### Explanation

Three support tickets are inserted into the queue.

Since "Login Issue" was inserted first, it becomes the first ticket to be processed and appears at the front of the queue.

# Memory Representation of Queue

Consider the following queue:

```cpp
queue<int> q;

q.push(100);
q.push(200);
q.push(300);
q.push(400);
```

Internally it can be visualized as:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/queue-in-c-stl/1781179032026-7f12e00b-a496-4219-86a3-ee1ee06df90f.png)

Here:

- 100 entered first.
- 400 entered last.
- 100 will be removed first.
- 400 will be removed last.

This arrangement strictly follows the FIFO principle.

# Basic Operations on Queue

The most commonly used queue operations are:

1. push()
2. pop()
3. front()
4. back()
5. empty()
6. size()

# Inserting Elements using push()

The `push()` function inserts a new element at the rear of the queue.

The insertion operation in a queue is called **Enqueue**.

## Syntax

```cpp
queueName.push(value);
```

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> printJobs;

    printJobs.push("Resume.pdf");
    printJobs.push("ProjectReport.pdf");
    printJobs.push("Invoice.pdf");

    cout << printJobs.front();

    return 0;
}
```

### Output
Resume.pdf

### Explanation

Three print jobs are inserted.

Since Resume.pdf was submitted first, it appears at the front and will be printed before the other documents.

### Time Complexity

O(1)

# Accessing the Front Element

The `front()` function returns the first element of the queue.

It only accesses the element and does not remove it.

## Syntax

```cpp
queueName.front();
```

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> customers;

    customers.push("Customer A");
    customers.push("Customer B");
    customers.push("Customer C");

    cout << customers.front();

    return 0;
}
```

### Output
Customer A

### Explanation

Customer A entered the queue first.

Therefore, it remains at the front and is returned by the front() function.

### Time Complexity

O(1)

# Accessing the Rear Element

The `back()` function returns the most recently inserted element.

## Syntax

```cpp
queueName.back();
```

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> tasks;

    tasks.push("Design");
    tasks.push("Development");
    tasks.push("Testing");

    cout << tasks.back();

    return 0;
}
```

### Output
Testing

### Explanation

Testing was inserted last.

Therefore it becomes the rear element of the queue.

### Time Complexity

O(1)

# Removing Elements using pop()

The `pop()` function removes the front element from the queue.

The deletion operation in a queue is called **Dequeue**.

## Syntax

```cpp
queueName.pop();
```

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> orders;

    orders.push("Laptop");
    orders.push("Keyboard");
    orders.push("Mouse");

    orders.pop();

    cout << orders.front();

    return 0;
}
```

### Output
Keyboard

### Explanation

Initially:
Laptop → Keyboard → Mouse
After pop():
Keyboard → Mouse
The first order (Laptop) is removed because it entered the queue first.

### Time Complexity

O(1)

# Checking Whether Queue is Empty

The `empty()` function checks whether the queue contains any elements.

## Syntax

```cpp
queueName.empty();
```

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<int> q;

    if(q.empty())
    {
        cout << "Queue is Empty";
    }

    return 0;
}
```

### Output
Queue is Empty

### Explanation

No elements exist in the queue.

Therefore empty() returns true.

### Time Complexity

O(1)

# Finding Queue Size

The `size()` function returns the total number of elements currently present in the queue.

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> projects;

    projects.push("Website");
    projects.push("Mobile App");
    projects.push("AI Chatbot");

    cout << projects.size();

    return 0;
}
```

### Output
3

### Explanation

Three projects are currently stored inside the queue.

### Time Complexity

O(1)

# Queue Underflow

Queue Underflow occurs when an attempt is made to remove an element from an empty queue.

Example:

```cpp
queue<int> q;

q.pop();
```

Since no elements exist in the queue, the operation becomes invalid.

Before calling pop(), always check:

```cpp
if(!q.empty())
{
    q.pop();
}
```

# Pseudo Traversal of Queue

Queues do not provide iterators for direct traversal.

To view all elements, a copy of the queue is usually created.

## Example Code

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<string> orders;

    orders.push("Laptop");
    orders.push("Monitor");
    orders.push("Keyboard");

    queue<string> temp = orders;

    while(!temp.empty())
    {
        cout << temp.front() << " ";
        temp.pop();
    }

    return 0;
}
```

### Output
Laptop Monitor Keyboard

### Explanation

The copied queue is traversed while the original queue remains unchanged.

# Types of Queues

Different applications require different queue variations.

### Simple Queue

Follows FIFO order.

### Circular Queue

Last position connects back to the first position.

Used to efficiently reuse memory.

### Priority Queue

Elements are processed according to priority instead of insertion order.

Higher-priority elements are served first.

### Double Ended Queue (Deque)

Insertion and deletion are allowed at both ends.

Provides greater flexibility.

# Queue vs Stack

| Feature | Queue | Stack |
| --- | --- | --- |
| Principle | FIFO | LIFO |
| Insertion | Rear | Top |
| Deletion | Front | Top |
| First Element | Removed First | Removed Last |
| Last Element | Removed Last | Removed First |

# Advantages of Queue

### Maintains Order

Elements are processed exactly in the order they arrive.

### Fair Processing

Every task receives equal opportunity for execution.

### Efficient Operations

Insertion and deletion are performed in constant time.

### Useful in Scheduling

Ideal for managing tasks, requests, and resources.

### Supports BFS

Widely used in graph and tree traversal algorithms.

# Limitations of Queue

### No Random Access

Middle elements cannot be directly accessed.

### Restricted Operations

Elements can only be inserted and deleted from specific ends.

### Traversal Limitations

Direct traversal is not supported.

### Memory Consumption

Large queues may consume significant memory.

# Applications of Queue

Queues are used extensively in real-world software systems.

Examples include:

- CPU Scheduling
- Printer Management Systems
- Customer Service Systems
- Online Order Processing
- Ticket Booking Systems
- Call Centers
- Network Packet Routing
- Breadth First Search (BFS)
- Chat Message Processing
- Banking Systems
- Cloud Task Scheduling
- Web Server Request Handling

# Time Complexity of Queue Operations

| Operation | Complexity |
| --- | --- |
| push() | O(1) |
| pop() | O(1) |
| front() | O(1) |
| back() | O(1) |
| size() | O(1) |
| empty() | O(1) |

# Summary

A Queue is a linear data structure that follows the First In First Out (FIFO) principle. Elements are inserted at the rear and removed from the front, ensuring that tasks are processed in the same order in which they arrive. The C++ STL provides the queue container adapter to efficiently implement queue operations such as insertion, deletion, accessing front and rear elements, checking size, and testing whether the queue is empty. Queues play a vital role in scheduling systems, networking, operating systems, graph algorithms, and many real-world applications where maintaining processing order is essential.




