# Multithreading in C++

## Introduction

Multithreading is a programming model that allows a single process to execute multiple threads concurrently. To understand this concept, think of a process as a kitchen: the kitchen contains a single set of ingredients, appliances, and recipes (shared memory space). A single-threaded program is like having a single chef executing one task at a time. A multithreaded program is like having multiple chefs (threads) working in the same kitchen simultaneously, sharing the tools and ingredients, but preparing different parts of the meal independently.

In C++, native support for multithreading was introduced in C++11 through the `<thread>` header file. Before this, developers had to rely on platform-specific libraries like POSIX threads (pthreads) on Linux or the Windows API, which made code less portable.

Key characteristics of threads:

- **Shared Memory:** Threads share the same address space, global variables, and heap memory of their parent process. This makes communication between threads very fast but requires careful coordination.
- **Private Stack:** Each thread has its own call stack and local variables, ensuring that their internal function call states do not interfere with each other.
- **Lightweight:** Creating and switching between threads is much faster than spawning new processes because threads do not need a separate memory allocation from the operating system.

## Creating a Thread

A thread is represented in C++ by the `std::thread` class. Creating an instance of this class launches a new execution thread that runs the callable task passed to its constructor.

**Syntax:**

```Cpp
thread thread_obj(callable_target);
```

### Basic Example

```Cpp
#include <iostream>
#include <thread>
using namespace std;

void printBanner() {
    cout << "Welcome to AlphaKnowledge Threading Demo!" << endl;
}

int main() {
    // Spawns thread 't' and immediately starts executing printBanner() in parallel
    thread t(printBanner);

    // Blocks the main thread until thread 't' finishes its task
    t.join();

    cout << "Main execution finished." << endl;
    return 0;
}
```

### Output
Welcome to AlphaKnowledge Threading Demo!
Main execution finished.

### Step-by-Step Execution Flow

1. **Creation:** In `main()`, `thread t(printBanner)` is executed. This requests the operating system scheduler to allocate a new thread of execution.
2. **Parallel Run:** The system starts executing the code inside `printBanner()` on a separate execution context. At the same time, the main thread continues its own execution.
3. **Synchronization:** The main thread calls `t.join()`. This is a blocking call, meaning `main()` stops and waits right here until `t` finishes running `printBanner()`.
4. **Termination:** Once `t` finishes printing, the main thread resumes and executes the final print statement.

### Managing Thread Lifecycles: Joining vs. Detaching

When you launch a thread, you must explicitly decide what to do with it before the `std::thread` object is destroyed (e.g., when it goes out of scope). If you do not join or detach a thread, the program will call `std::terminate()` and crash.

- **`join()`:** This is a synchronous approach. The calling thread waits for the spawned thread to finish. It acts as a barrier, ensuring that resources used by the child thread are safely cleaned up before the program proceeds.
- **`detach()`:** This is an asynchronous approach. It cuts the connection between the thread object and the actual execution thread. The thread runs independently in the background (as a daemon thread). The operating system automatically reclaims its resources when it finishes.
- **`joinable()`:** A safety check that returns `true` if the thread object is associated with an active thread of execution. You cannot join or detach a thread that is not joinable, and attempting to do so will throw a `std::system_error` exception.

```Cpp
#include <iostream>
#include <thread>
#include <chrono>
using namespace std;

void monitorSystem() {
    cout << "System Monitor Thread ID: " << this_thread::get_id() << endl;
}

void logActivity() {
    cout << "Activity Logger Thread ID: " << this_thread::get_id() << endl;
}

int main() {
    // Launch two concurrent worker threads
    thread t1(monitorSystem);
    thread t2(logActivity);

    cout << "t1 ID: " << t1.get_id() << endl;
    cout << "t2 ID: " << t2.get_id() << endl;

    // Safety check before joining
    if (t1.joinable()) {
        t1.join();
        cout << "t1 successfully joined." << endl;
    }

    // Safety check before detaching
    if (t2.joinable()) {
        t2.detach();
        cout << "t2 successfully detached." << endl;
    }

    // We sleep briefly to give the detached thread t2 a chance to print before main exits
    this_thread::sleep_for(chrono::milliseconds(50));
    cout << "Main program exiting." << endl;

    return 0;
}
```

### Output
t1 ID: 140737347512000
t2 ID: 140737213290176
System Monitor Thread ID: 140737347512000
t1 successfully joined.
t2 successfully detached.
Activity Logger Thread ID: 140737213290176
Main program exiting.

## Passing Callables to Threads

A thread can execute different kinds of executable entities (callables) in C++. Arguments are passed to these callables by listing them as extra parameters in the `std::thread` constructor.

### 1. Function Pointer with Arguments

When passing arguments, `std::thread` copies them into the thread's internal storage by default.

```Cpp
#include <iostream>
#include <thread>
using namespace std;

void processData(int id) {
    cout << "Processing package: " << id << endl;
}

int main() {
    // Passes the value 105 as an argument to processData()
    thread t(processData, 105);
    t.join();
    return 0;
}
```

### Output
Processing package: 105

### 2. Lambda Expression

Lambda expressions allow you to define inline, anonymous functions directly at the thread's launch site.

```Cpp
#include <iostream>
#include <thread>
using namespace std;

int main() {
    int taskNum = 7;

    // Define lambda directly in the constructor
    thread t([](int n) {
        cout << "Executing inline task #" << n << endl;
    }, taskNum);

    t.join();
    return 0;
}
```

### Output
Executing inline task #7

### 3. Function Objects (Functors)

A functor is an object of a class that overloads the parentheses operator `operator()`, allowing the object to be called like a function.

```Cpp
#include <iostream>
#include <thread>
using namespace std;

class Multiplier {
    int factor;
public:
    Multiplier(int f) : factor(f) {}
    
    // Parentheses operator overload makes the object callable
    void operator()(int val) const {
        cout << "Result: " << (val * factor) << endl;
    }
};

int main() {
    // The constructor copy-constructs the Multiplier functor inside the thread
    thread t(Multiplier(5), 10);
    t.join();
    return 0;
}
```

### Output
Result: 50

### 4. Member Functions (Static and Non-Static)

- **Non-static member functions:** Require a valid object pointer because they access instance-specific variables. The object address must be passed as the second argument.
- **Static member functions:** Do not belong to a specific instance and do not require an object reference. They are passed just like regular global functions.

```Cpp
#include <iostream>
#include <thread>
using namespace std;

class TaskRunner {
public:
    void runTask(int id) {
        cout << "Non-static runner: " << id << endl;
    }
    static void runGlobalTask(int id) {
        cout << "Static runner: " << id << endl;
    }
};

int main() {
    TaskRunner runner;

    // Requires reference to member function, object address, and arguments
    thread t1(&TaskRunner::runTask, &runner, 42);
    t1.join();

    // Static function called directly using class scope
    thread t2(&TaskRunner::runGlobalTask, 99);
    t2.join();

    return 0;
}
```

### Output
Non-static runner: 42
Static runner: 99

## C++ Thread Management Utilities

| Tool | Type | Description |
| --- | --- | --- |
| `join()` | Method | Suspends execution of the calling thread until this thread completes. |
| `detach()` | Method | Detaches the thread, allowing it to run independently in the background. |
| `std::mutex` | Class | Mutual exclusion primitive used to prevent data race conditions. |
| `std::lock_guard` | Class | Scoped RAII lock wrapper that locks a mutex and automatically releases it. |
| `std::condition_variable` | Class | Allows threads to sleep until notified by another thread of a state change. |
| `std::atomic<T>` | Template | Provides lock-free atomic operations for basic types. |
| `this_thread::sleep_for()` | Function | Blocks execution of the calling thread for a specified duration. |
| `this_thread::get_id()` | Function | Returns the unique thread ID of the currently executing thread. |
| `thread::hardware_concurrency()` | Static Method | Returns the number of concurrent hardware threads supported by the CPU. |

## Common Challenges in Multithreading

Concurrent execution introduces several classic problems that do not occur in single-threaded applications:

### 1. Race Conditions

A race condition occurs when two or more threads access a shared variable simultaneously, and at least one thread modifies it. The final value depends on the exact sequence in which the CPU schedules the threads, leading to unpredictable results.

- **Example:** Imagine a bank account with a balance of $100. If Thread A reads the balance to withdraw $50, and Thread B simultaneously reads the balance to withdraw $70, both see $100. Both approve the withdrawal, leaving the account overdrawn at -$20, which should have been blocked.

### 2. Deadlocks

A deadlock is a situation where two or more threads are unable to make progress because they are waiting for each other to release resources.

- **Example:** Thread A holds Mutex 1 and needs Mutex 2. Thread B holds Mutex 2 and needs Mutex 1. Both threads wait indefinitely for the other to release the required lock, freezing that part of the application.

### 3. Starvation

Starvation happens when a thread is perpetually denied access to shared resources or CPU time. This occurs when the OS thread scheduler repeatedly prioritizes other threads, leaving the starved thread waiting in the ready queue indefinitely.

### 4. Context Switching Overhead

A context switch is the process by which the CPU saves the state of an executing thread and loads the state of another. While this allows multiple threads to share CPU time, frequent context switching introduces computational overhead. Creating too many threads (thread thrashing) can slow down the system because the CPU spends more time switching states than executing actual tasks.

> **Important:** When passing arguments to a thread, C++ always creates a copy of the argument, even if the target function accepts parameters by reference (e.g., `void task(int& val)`). Attempting to pass a variable directly will result in a compilation error. To pass a real reference instead of a copy, you must wrap the argument in `std::ref()` (e.g., `thread t(task, ref(myVar))`).

## Summary

Multithreading in C++ allows concurrent execution of multiple tasks within a single process. Using the `std::thread` class introduced in C++11, developers can launch concurrent tasks by passing callables like function pointers, lambdas, functors, or member functions. Lifecycles must be closed cleanly using `join()` to wait for thread termination, or `detach()` to let it run independently in the background. While multithreading dramatically improves CPU utilization and interface responsiveness, it requires synchronization mechanisms (such as mutexes and locks) to protect shared data from race conditions, deadlocks, and scheduler starvation.




