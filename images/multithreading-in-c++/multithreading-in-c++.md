# Multithreading in C++

## Introduction

Multithreading is a programming technique where a program is divided into multiple independent execution units called **threads**. These threads run concurrently within the same process and share the same memory space.

Instead of executing one task at a time, multithreading allows multiple tasks to progress simultaneously, improving performance, responsiveness, and resource utilization.

### Real-World Example

Consider **AlphaKnowledge**, an online learning platform.

While a student is:

- Watching a video lecture
- Downloading course materials
- Receiving notifications
- Tracking course progress

all these activities can execute simultaneously using multiple threads.

Without multithreading, each task would wait for the previous task to finish, making the application slow and unresponsive.

## Benefits of Multithreading

- Improves CPU utilization.
- Increases application responsiveness.
- Enables parallel execution of tasks.
- Reduces waiting time for users.
- Makes efficient use of multicore processors.
- Allows background processing while the main application continues running.

## Process vs Thread

| Process | Thread |
| --- | --- |
| Independent program execution unit | Smallest execution unit within a process |
| Has its own memory space | Shares memory with other threads |
| Creation is expensive | Creation is lightweight |
| Communication is slower | Communication is faster |
| Failure of one process rarely affects others | One faulty thread may affect the process |

## Thread Lifecycle

A thread generally moves through the following stages:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multithreading-in-c/1781187997564-a189d907-010a-401b-b275-603afd4f5db4.png)

## Creating a Thread

C++11 introduced multithreading support through the `<thread>` header.

### Syntax

```cpp
thread thread_name(callable);
```

where:

- `thread_name` → object of `std::thread`
- `callable` → function, lambda, functor, or member function

### Example: Course Notification Thread

```cpp
#include <iostream>
#include <thread>
using namespace std;

void sendNotification()
{
    cout << "Course notification sent." << endl;
}

int main()
{
    thread t(sendNotification);

    t.join();

    cout << "Main application running.";

    return 0;
}
```

### Output
Course notification sent.
Main application running.

### Explanation

- A new thread is created to send notifications.
- The main thread waits using `join()`.
- After completion, execution returns to the main thread.

# Thread Creation Behavior

Creating a `std::thread` object immediately starts a new thread of execution.

```cpp
thread t(myFunction);
```

### Explanation

- The thread begins execution as soon as the thread object is created.
- The operating system schedules the new thread independently of the calling thread.
- `join()` and `detach()` do not start the thread; they only control how the thread is managed after creation.
- The new thread and the main thread may run concurrently.

### Visualization

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multithreading-in-c/1781188036176-7c222e3b-cb4e-484c-bd14-a512c08055d0.png)

# Passing Arguments to Threads

Arguments can be supplied directly when creating a thread.

## Syntax

```cpp
thread thread_name(function_name, arg1, arg2, ...);
```

## Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

void displayCourse(int courseId)
{
    cout << "Course ID: "
         << courseId;
}

int main()
{
    thread t(displayCourse, 101);

    t.join();

    return 0;
}
```

### Output
Course ID: 101

### Explanation

- `displayCourse()` requires one parameter.
- The value `101` is passed when the thread is created.
- The thread executes `displayCourse(101)` concurrently.

You can also pass multiple parameters by listing them sequentially as arguments after the function name:

```cpp
thread t(func, arg1, arg2, arg3);
```

---

# Joining a Thread

The `join()` function blocks the current thread until the target thread finishes execution.

### Syntax

```cpp
thread_name.join();
```

### Why Use join()?

Without joining:

- Main thread may finish early.
- Child thread may terminate abruptly.
- Program behavior becomes unpredictable.

### Example

```cpp
thread reportThread(generateReport);

reportThread.join();
```

The main application waits until the report generation completes.

# Important Note About join()

Calling join() on a non-joinable thread throws a std::system_error exception.

Examples of non-joinable threads:

- Threads that have already been joined.
- Threads that have been detached.
- Default-constructed thread objects that do not represent an active thread.

### Safe Practice

Always check if a thread is joinable before calling `join()` on it:

```cpp
if(threadObj.joinable())
{
    threadObj.join();
}
```

### Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

int main()
{
    thread t;

    if(t.joinable())
    {
        t.join();
    }

    return 0;
}
```

### Explanation

The thread object `t` is not associated with any running thread. Calling `join()` directly would cause an exception. Using `joinable()` prevents this problem.

# Checking Whether a Thread is Joinable

Before joining, it is recommended to verify that the thread is valid.

### Syntax

```cpp
thread_name.joinable();
```

### Returns

- `true` → thread can be joined
- `false` → thread already joined, detached, or invalid

### Example

```cpp
if(reportThread.joinable())
{
    reportThread.join();
}
```

---

# Detaching a Thread

A detached thread runs independently in the background.

### Syntax

```cpp
thread_name.detach();
```

### Example

```cpp
thread notificationThread(sendNotification);

notificationThread.detach();
```

### Use Cases

- Background logging
- Notification services
- Analytics collection
- Monitoring services

### Important

Once detached:

- Cannot be joined later.
- Main thread does not wait for it.

# Getting Thread ID

Every thread has a unique identifier.

### Syntax

```cpp
thread_name.get_id();
```

or

```cpp
this_thread::get_id();
```

### Example

```cpp
cout << this_thread::get_id();
```

### Uses

- Debugging
- Logging
- Monitoring
- Performance analysis

# Complete Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

void generateCertificate()
{
    cout << "Certificate Generation Thread ID: "
         << this_thread::get_id() << endl;
}

void sendMail()
{
    cout << "Email Thread ID: "
         << this_thread::get_id() << endl;
}

int main()
{
    thread t1(generateCertificate);
    thread t2(sendMail);

    cout << "t1 ID: "
         << t1.get_id() << endl;

    cout << "t2 ID: "
         << t2.get_id() << endl;

    t1.join();

    t2.join();

    cout << "All tasks completed.";

    return 0;
}
```

---

# Callables in Multithreading

A thread executes any object that can be called.

C++ supports four major callable types:

1. Function Pointer
2. Lambda Expression
3. Function Object (Functor)
4. Member Function

# 1. Function Pointer

```cpp
#include <iostream>
#include <thread>
using namespace std;

void processCourse(int id)
{
    cout << "Processing Course "
         << id;
}

int main()
{
    thread t(processCourse, 101);

    t.join();

    return 0;
}
```

### Output
Processing Course 101

---

# 2. Lambda Expression

Lambda functions are anonymous functions.

### Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

int main()
{
    thread t([]()
    {
        cout << "Downloading course material";
    });

    t.join();

    return 0;
}
```

### Output
Downloading course material

### Advantages

- No separate function needed.
- Cleaner syntax.
- Ideal for one-time tasks.

# 3. Function Object (Functor)

A functor is a class with overloaded `()` operator.

### Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

class ProgressTracker
{
public:
    void operator()()
    {
        cout << "Tracking course progress";
    }
};

int main()
{
    thread t(ProgressTracker());

    t.join();

    return 0;
}
```

### Output
Tracking course progress

---

# 4. Member Functions

### Non-Static Member Function

```cpp
#include <iostream>
#include <thread>
using namespace std;

class Course
{
public:
    void display(int id)
    {
        cout << "Course ID: "
             << id;
    }
};

int main()
{
    Course c;

    thread t(&Course::display,
             &c,
             101);

    t.join();

    return 0;
}
```

### Output
Course ID: 101

---

# Static Member Functions

Static functions do not require objects.

```cpp
class Course
{
public:

    static void show()
    {
        cout << "Static Course Function";
    }
};

thread t(&Course::show);
```

---

# Thread Synchronization

When multiple threads access the same resource simultaneously, incorrect results may occur.

Synchronization ensures controlled access to shared resources.

### Example

Suppose:

- Thread A updates student marks.
- Thread B generates a report.

Without synchronization, the report may use incomplete data.

# Race Condition

A race condition occurs when multiple threads modify shared data simultaneously.

### Example

```cpp
counter++;
```

If two threads execute this statement together:

- Expected value = 2
- Actual value may become 1

### Problems

- Incorrect calculations
- Corrupted data
- Unpredictable behavior

# Mutex

A mutex (Mutual Exclusion) allows only one thread to access a critical section at a time.

### Example

```cpp
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;

mutex mtx;

void print()
{
    mtx.lock();

    cout << "Thread Working\n";

    mtx.unlock();
}
```

### Benefits

- Prevents race conditions.
- Ensures data consistency.

# lock_guard

Manually calling lock() and unlock() can be risky.

`lock_guard` automatically manages locking.

### Example

```cpp
lock_guard<mutex> lock(mtx);

cout << "Protected Code";
```

### Advantages

- Safer.
- Automatically unlocks.
- Exception-safe.

# Atomic Variables

Atomic variables allow thread-safe operations without mutexes.

### Example

```cpp
#include <atomic>

atomic<int> counter(0);

counter++;
```

### Benefits

- Faster than mutex.
- No locking overhead.
- Thread-safe increment/decrement.

# Condition Variable

Condition variables allow threads to wait until a specific condition becomes true.

### Example Use Cases

- Task scheduling
- Producer-Consumer problem
- Notification systems
- Job queues

# Sleeping a Thread

### sleep_for()

Pauses execution for a specified duration.

```cpp
this_thread::sleep_for(
    chrono::seconds(2));
```

### Example

```cpp
cout << "Downloading...";

this_thread::sleep_for(
chrono::seconds(2));

cout << "Completed";
```

# Hardware Concurrency

Returns the number of available CPU threads.

### Syntax

```cpp
thread::hardware_concurrency();
```

### Example

```cpp
cout << thread::
hardware_concurrency();
```

### Uses

- Performance optimization
- Deciding thread count

# Context Switching

A context switch occurs when the CPU pauses one thread and starts another.

### Process

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multithreading-in-c/1781188125088-767d7905-8c1a-483c-a15e-df7f0d946990.png)

### Advantages

- Better CPU utilization

### Disadvantages

- Additional overhead
- Excessive switching reduces performance

# Common Multithreading Problems

## Race Condition

Multiple threads access shared data simultaneously.

### Solution

- Mutex
- Atomic Variables

## Deadlock

Occurs when threads wait forever for each other's resources.

### Example

```text
Thread A waiting for Resource B
Thread B waiting for Resource A
```

Neither proceeds.

### Prevention

- Lock resources in consistent order.
- Use lock_guard.
- Minimize lock duration.

---

## Starvation

A thread never gets CPU time because other threads continuously receive priority.

### Solution

- Fair scheduling.
- Balanced resource allocation.

---

## Livelock

Threads keep responding to each other but make no progress.

### Example

Two workers continuously stepping aside for each other but never moving forward.

---

# Best Practices

- Prefer `lock_guard` over manual lock/unlock.
- Use atomic variables for simple counters.
- Avoid excessive thread creation.
- Join or detach every thread.
- Keep critical sections small.
- Minimize shared data.
- Use RAII for synchronization objects.
- Avoid deadlocks through proper locking order.

---

# Thread Management Functions Summary

| Function | Purpose |
| --- | --- |
| join() | Wait for thread completion |
| detach() | Run thread independently |
| joinable() | Check if thread can be joined |
| get_id() | Retrieve thread ID |
| sleep_for() | Pause thread for duration |
| sleep_until() | Pause thread until specific time |
| hardware_concurrency() | Get available hardware threads |

---

# Synchronization Tools Summary

| Tool | Purpose |
| --- | --- |
| mutex | Protect shared resources |
| lock_guard | Automatic mutex management |
| atomic | Lock-free thread-safe operations |
| condition_variable | Thread communication and waiting |
| unique_lock | Flexible mutex management |

---

# Multithreading vs Multiprocessing

| Multithreading | Multiprocessing |
| --- | --- |
| Threads share memory | Processes have separate memory |
| Faster communication | Slower communication |
| Lightweight | Heavyweight |
| Lower creation cost | Higher creation cost |
| Better responsiveness | Better isolation |

---

# Advantages of Multithreading

- Faster execution.
- Better CPU utilization.
- Improved responsiveness.
- Efficient multitasking.
- Suitable for real-time systems.
- Better user experience.

# Disadvantages of Multithreading

- Complex debugging.
- Synchronization overhead.
- Deadlock possibility.
- Race conditions.
- Context switching overhead.

# Key Takeaways

- Multithreading allows multiple tasks to execute concurrently.
- C++11 introduced multithreading through the `<thread>` library.
- Threads can execute functions, lambdas, functors, and member functions.
- `join()` waits for thread completion.
- `detach()` allows independent execution.
- Synchronization is required when sharing resources.
- Mutexes, lock_guard, atomics, and condition variables help manage thread safety.
- Proper thread management improves performance, responsiveness, and scalability.

# Summary

Multithreading in C++ allows a process to be divided into multiple concurrent execution units called threads, sharing the same memory space to optimize CPU utilization, application responsiveness, and task execution speed. When a `std::thread` is created, it begins execution immediately under the scheduling of the operating system, allowing arguments to be passed directly upon initialization. Thread lifecycles are managed through `join()`, which waits for a thread to complete, and `detach()`, which runs the thread independently in the background; however, calling `join()` on a non-joinable thread (such as detached or already-joined threads) throws a `std::system_error` exception, making it best practice to verify state with `joinable()` first. To prevent multi-threaded data corruption issues like race conditions and deadlocks, C++ provides key synchronization tools including mutexes, automatic `lock_guard` RAII locks, condition variables, and lock-free `std::atomic` variables.




