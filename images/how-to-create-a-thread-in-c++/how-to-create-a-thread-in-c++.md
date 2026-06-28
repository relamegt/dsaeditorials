# How to Create a Thread in C++

## Introduction

A thread represents the smallest, independent sequence of execution steps that the operating system's scheduler can manage. In a multithreaded application, different threads execute concurrently, sharing the process's global state and resources while maintaining their own private registers and call stacks. In C++, thread creation and management are native since C++11, implemented through the `std::thread` class template in the `<thread>` header.

When creating a thread in C++, you must provide the entry-point instructions the thread will execute. These instructions are supplied in the form of a **callable** target. C++ supports three primary ways to pass these instructions:

1. Function Pointers
2. Lambda Expressions
3. Functors (Function Objects)

## 1. Creating a Thread Using a Function Pointer

The most direct way to create a thread is by passing a standard global or static function pointer to the `std::thread` constructor.

### Example: Running a Background Logger

```Cpp
#include <iostream>
#include <thread>
using namespace std;

// Function to run inside the background thread
void runBackgroundWorker() {
    cout << "Background worker: Initializing update cycle..." << endl;
}

int main() {
    // Spawn the thread and pass the function pointer
    thread workerThread(runBackgroundWorker);

    // Block the main thread until the worker completes
    workerThread.join();

    cout << "Main thread: Background worker finished." << endl;
    return 0;
}
```

### Output
Background worker: Initializing update cycle...
Main thread: Background worker finished.

When `workerThread` is instantiated, the constructor launches a new thread that runs the `runBackgroundWorker()` function. The `.join()` call blocks the `main()` function, preventing it from executing the next statement until `workerThread` has completed.

## 2. Creating a Thread Using a Lambda Expression

Lambda expressions let you define the code block directly inline inside the `std::thread` constructor, which is convenient for short-lived tasks that do not need a named function definition.

### Example: Dynamic Inline Task

```Cpp
#include <iostream>
#include <thread>
using namespace std;

int main() {
    // Spawn the thread and pass an inline lambda expression
    thread tempThread([]() {
        cout << "Lambda thread: Executing inline calculation..." << endl;
    });

    // Wait for the thread to complete
    tempThread.join();

    cout << "Main thread: Lambda execution resolved." << endl;
    return 0;
}
```

### Output
Lambda thread: Executing inline calculation...
Main thread: Lambda execution resolved.

The lambda `[]() { ... }` acts as the entry-point task. It runs in parallel and is joined to `main()` in the same manner.

## 3. Creating a Thread Using a Functor

A functor is an instance of a class that overloads the call operator `operator()`. When you pass a functor to the `std::thread` constructor, C++ copies or moves the object into the thread's internal storage and invokes its call operator.

### Example: Task Execution via Functor

```Cpp
#include <iostream>
#include <thread>
using namespace std;

class SensorMonitor {
    int sensorID;
public:
    SensorMonitor(int id) : sensorID(id) {}

    // Overloading operator() makes instances of this class callable
    void operator()() const {
        cout << "Functor thread: Monitoring sensor #" << sensorID << endl;
    }
};

int main() {
    // Pass a temporary SensorMonitor functor instance to the thread
    thread monitorThread(SensorMonitor(301));

    // Wait for the monitoring task to finish
    monitorThread.join();

    cout << "Main thread: Monitoring cycle completed." << endl;
    return 0;
}
```

### Output
Functor thread: Monitoring sensor #301
Main thread: Monitoring cycle completed.

The class constructor initializes the object state (`sensorID = 301`), and the thread executes the behavior defined inside `operator()()`.

## Summary of Thread Creation Methods

| Method | Syntax | Best Use Case |
| --- | --- | --- |
| **Function Pointer** | `thread t(funcName)` | Standard reusable procedures defined globally or statically |
| **Lambda Expression** | `thread t([](){ ... })` | Short-lived, inline tasks that do not need to be reused elsewhere |
| **Functor** | `thread t(FunctorClass(args))` | Tasks that need to carry state variables and execute custom object logic |

> **Important:** Always verify that a thread has been either joined (`.join()`) or detached (`.detach()`) before the `std::thread` object reaches the end of its scope. If a `std::thread` object is destroyed while still associated with an active thread of execution (i.e., when `.joinable()` returns `true`), the C++ runtime will immediately invoke `std::terminate()`, causing the application to crash.

## Summary

In C++, threads are created and managed using the `std::thread` class template from the `<thread>` header. To spawn a thread, developers must supply a callable target containing the execution instructions. The three main methods of passing these instructions are using function pointers for reusable functions, lambda expressions for simple inline tasks, and functors (function objects) for tasks requiring internal state. Regardless of the method chosen, every active thread must be joined or detached before its `std::thread` object is destroyed to prevent abnormal program termination.




