# Mutex in C++

## Introduction

Mutex stands for **Mutual Exclusion**. In C++, the `std::mutex` class is a synchronization primitive used to protect shared data (such as variables, files, or custom data structures) from being accessed or modified by multiple threads at the same exact time. By enforcing mutual exclusion, only one thread can access the protected resource at a time, preventing data corruption and race conditions.

The `std::mutex` class is declared in the `<mutex>` header and is part of the `std` namespace.

## The Need for a Mutex

When two or more threads attempt to write to the same shared memory location simultaneously, a **race condition** occurs. At the hardware level, an increment operation (like `counter++`) is not atomic; it consists of three separate steps:

1. Reading the value from memory into a CPU register.
2. Incrementing the value inside the register.
3. Writing the updated value back to memory.

If Thread A and Thread B perform this sequence concurrently, their instructions can interleave. Both might read the same initial value, increment it, and write it back, resulting in one of the increments being lost. A Mutex solves this by locking the execution block: while one thread holds the lock, all other threads attempting to acquire it are suspended (blocked) until the lock is released.

## Syntax

Using a mutex in C++ involves three basic steps:

1. **Instantiation:** Create a `std::mutex` object.

``````Cpp
mutex mtx;
```

1. **Acquiring the Lock:** Call `.lock()` before entering the critical section (the code modifying shared data).

``````Cpp
mtx.lock();
```

1. **Releasing the Lock:** Call `.unlock()` immediately after leaving the critical section.

``````Cpp
mtx.unlock();
```

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/mutex-in-c/1782653187392-WhatsApp_Image_2026-06-28_at_6.56.00_PM.jpeg)

## 

## Demonstration: Race Condition Without Mutex

The following program attempts to book tickets concurrently using two threads. Each thread increments a shared `ticketsBooked` counter `100,000` times.

```Cpp
#include <iostream>
#include <thread>
using namespace std;

// Shared global resource
int ticketsBooked = 0;

void bookTickets() {
    for (int i = 0; i < 100000; i++) {
        ticketsBooked++;
    }
}

int main() {
    // Launch two threads simulating concurrent bookings
    thread customer1(bookTickets);
    thread customer2(bookTickets);

    customer1.join();
    customer2.join();

    cout << "Total tickets booked: " << ticketsBooked << endl;
    return 0;
}
```

### Output
Total tickets booked: 147820

### Explanation of Unsynchronized Output

Because the threads run concurrently without synchronization, they constantly overwrite each other's increments. Running the code multiple times yields different, unpredictable totals, and it rarely reaches the expected target of `200,000`.

## Demonstration: Thread Synchronization Using Mutex

By introducing a `std::mutex` object, we ensure only one thread can modify `ticketsBooked` at any given moment.

```Cpp
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;

// Shared global resource and mutex lock
mutex mtx;
int ticketsBooked = 0;

void bookTickets() {
    // Lock the critical section
    mtx.lock();

    for (int i = 0; i < 100000; i++) {
        ticketsBooked++;
    }

    // Release the lock for other threads
    mtx.unlock();
}

int main() {
    thread customer1(bookTickets);
    thread customer2(bookTickets);

    customer1.join();
    customer2.join();

    cout << "Total tickets booked: " << ticketsBooked << endl;
    return 0;
}
```

### Output
Total tickets booked: 200000

### Explanation of Synchronized Output

When `customer1` calls `mtx.lock()`, it acquires the mutex lock. If `customer2` tries to call `mtx.lock()` while `customer1` holds it, `customer2` is blocked and goes to sleep. Once `customer1` finishes its loop and calls `mtx.unlock()`, `customer2` is woken up, acquires the lock, and safely executes its own loop. The final count is consistently and predictably `200,000`.

## Scoped Locking with std::lock_guard

Manually calling `.lock()` and `.unlock()` is discouraged in professional C++ programming. If a function exits early due to a `return` statement or an exception after calling `.lock()`, `.unlock()` is never called, resulting in a permanent deadlock.

To prevent this, use `std::lock_guard`. It uses the **Resource Acquisition Is Initialization (RAII)** pattern: it locks the mutex in its constructor when created, and automatically releases the lock in its destructor when it goes out of scope.

```Cpp
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;

mutex mtx;
int ticketsBooked = 0;

void bookTicketsSafe() {
    // Lock is acquired here automatically
    lock_guard<mutex> lock(mtx);

    for (int i = 0; i < 100000; i++) {
        ticketsBooked++;
    }
    // Lock is automatically released when 'lock' object is destroyed here
}

int main() {
    thread customer1(bookTicketsSafe);
    thread customer2(bookTicketsSafe);

    customer1.join();
    customer2.join();

    cout << "Total tickets booked (safe): " << ticketsBooked << endl;
    return 0;
}
```

### Output
Total tickets booked (safe): 200000

> **Note:** A mutex object is non-copyable and non-movable. Attempting to copy a `std::mutex` (e.g., passing it by value to a function) will cause a compilation error. When passing a mutex to helper functions or classes, it must always be passed by reference or pointer.

## Summary

A Mutex (Mutual Exclusion) is a C++ synchronization primitive used to prevent data race conditions by ensuring only one thread can access a shared resource at a time. The `.lock()` function acquires exclusive access, while `.unlock()` releases it. Because manual lock management is error-prone and vulnerable to exception-induced deadlocks, C++ provides RAII wrappers like `std::lock_guard` to handle locking and unlocking automatically within scoped blocks.




