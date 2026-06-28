# Thread Synchronization in C++

## Introduction

In multithreaded applications, thread synchronization is the process of coordinating the execution of concurrent threads to ensure consistent and predictable behavior. When multiple threads access and modify shared resources (such as global variables, shared files, or data structures) without proper coordination, it can lead to data corruption, inconsistent program states, and unpredictable application behavior.

### Why Thread Synchronization is Critical

Consider a warehouse inventory management system:

- **Initial Stock:** 50 units.
- **Restock Process (Thread A):** Adds 100 units (Expected total = 150).
- **Order Process (Thread B):** Shocks/Ships 80 units (Requires at least 80 units in stock).

If these operations run concurrently without synchronization, Thread B might execute its check and attempt to ship 80 units *before* the Restock Process has completed its update. Since the initial stock is only 50, the order fails with an "insufficient stock" error, even though a shipment of 100 units was already arriving. By synchronizing the two tasks, we ensure that the restock operation completes and updates the inventory before the shipping process runs, allowing both tasks to resolve successfully.

Unsynchronized operations give rise to three classic concurrency issues:

1. **Race Conditions:** Occur when multiple threads modify a resource simultaneously, resulting in lost updates.
2. **Deadlocks:** Occur when threads block indefinitely, waiting for locks held by one another.
3. **Starvation:** Occurs when low-priority threads are perpetually bypassed by the system scheduler.

C++ provides three primary mechanisms for thread synchronization:

1. Mutexes (Mutual Exclusion)
2. Condition Variables
3. Promises and Futures

## 1. Mutex (Mutual Exclusion)

A Mutex is a synchronization primitive that acts as a lock. When a thread wants to modify shared data, it acquires the mutex lock. While the lock is held, any other thread attempting to access the resource is blocked and put to sleep by the operating system.

### Unsynchronized Execution (Race Condition)

```Cpp
#include <iostream>
#include <thread>
using namespace std;

double totalSales = 0.0;
int transactionCount = 0;

void addSales(double amount) {
    totalSales += amount;
    transactionCount++;
    cout << "Transaction " << transactionCount << ": Added $" << amount 
         << ". Total sales: $" << totalSales << endl;
}

int main() {
    thread t1(addSales, 150.50);
    thread t2(addSales, 250.75);

    t1.join();
    t2.join();

    cout << "Final sales total: $" << totalSales << endl;
    return 0;
}
```

### Output
Transaction Transaction 2: Added $2: Added $150.5. Total sales: $250.75. Total sales: $401.25
401.25

Final sales total: $401.25

Without synchronization, both threads attempt to modify `totalSales` and write to the console simultaneously, garbling the output text.

### Synchronized Execution using Mutex

```Cpp
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;

double totalSales = 0.0;
mutex salesMutex;
int transactionCount = 0;

void addSales(double amount) {
    // Acquire the lock before entering the critical section
    salesMutex.lock();

    totalSales += amount;
    transactionCount++;
    cout << "Transaction " << transactionCount << ": Added $" << amount 
         << ". Total sales: $" << totalSales << endl;

    // Release the lock for other threads
    salesMutex.unlock();
}

int main() {
    thread t1(addSales, 150.50);
    thread t2(addSales, 250.75);

    t1.join();
    t2.join();

    cout << "Final sales total (synchronized): $" << totalSales << endl;
    return 0;
}
```

### Output
Transaction 1: Added $150.5. Total sales: $150.5
Transaction 2: Added $250.75. Total sales: $401.25
Final sales total (synchronized): $401.25

By locking `salesMutex`, we guarantee that only one thread can modify `totalSales` and print to the console at a time. The other thread waits in a blocked state until the lock is released.

## 2. Condition Variables

A condition variable is a synchronization primitive used to block one or more threads until another thread modifies a shared state and sends a notification. It is always used in conjunction with a mutex.

### Example: Warehouse Stock and Shipping

```Cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
using namespace std;

mutex mtx;
condition_variable cv;
int itemsInWarehouse = 0;

void produceItems(int count) {
    // Lock the mutex using lock_guard
    lock_guard<mutex> lock(mtx);
    itemsInWarehouse += count;
    cout << "Producer: Supplied " << count << " items. Stock: " << itemsInWarehouse << endl;

    // Notify the waiting consumer thread
    cv.notify_one();
}

void shipItems(int count) {
    unique_lock<mutex> ulock(mtx);

    // Wait until there is stock in the warehouse
    cv.wait(ulock, [] { return itemsInWarehouse > 0; });

    if (itemsInWarehouse >= count) {
        itemsInWarehouse -= count;
        cout << "Consumer: Shipped " << count << " items. Stock remaining: " << itemsInWarehouse << endl;
    } else {
        cout << "Consumer: Insufficient stock to ship!" << endl;
    }
}

int main() {
    // Launch the consumer first
    thread consumer(shipItems, 80);
    
    // Simulate delay before producing items
    this_thread::sleep_for(chrono::milliseconds(50));
    
    // Launch the producer
    thread producer(produceItems, 100);

    consumer.join();
    producer.join();

    return 0;
}
```

### Output
Producer: Supplied 100 items. Stock: 100
Consumer: Shipped 80 items. Stock remaining: 20

### How It Works

1. The consumer thread (`consumer`) starts and locks the mutex. It then evaluates the lambda condition `itemsInWarehouse > 0`.
2. Since the initial stock is `0` (false), `cv.wait()` releases the lock and puts the consumer thread to sleep.
3. The producer thread (`producer`) starts, locks the mutex, increments `itemsInWarehouse` to 100, and calls `cv.notify_one()`.
4. The consumer thread is woken up, re-acquires the lock, verifies the condition is now true, and proceeds to ship the items.

## 3. Promise and Future

`std::promise` and `std::future` are synchronization mechanisms used to transfer a value from a worker thread to the thread that spawned it. The `std::promise` object is the sending end, and the `std::future` object is the receiving end.

This mechanism is preferred over condition variables when a thread needs to return a single result exactly once.

### Example: Counting Primes in a Range

```Cpp
#include <iostream>
#include <thread>
#include <future>
using namespace std;

bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

void countPrimes(promise<int>&& primePromise, int begin, int end) {
    int count = 0;
    for (int i = begin; i <= end; i++) {
        if (isPrime(i)) {
            count++;
        }
    }
    // Set the result in the promise
    primePromise.set_value(count);
}

int main() {
    int start = 1, finish = 100;
    
    promise<int> primeNumPromise;
    future<int> primeNumFuture = primeNumPromise.get_future();

    cout << "Spawning prime calculation thread..." << endl;
    thread t(countPrimes, move(primeNumPromise), start, finish);

    cout << "Waiting for calculation results..." << endl;

    // get() blocks the main thread until the value is set in the promise
    int result = primeNumFuture.get();

    cout << "Total prime numbers between 1 and 100: " << result << endl;

    t.join();
    return 0;
}
```

### Output
Spawning prime calculation thread...
Waiting for calculation results...
Total prime numbers between 1 and 100: 25

### How It Works

The `main()` thread retrieves a `std::future` object from the `std::promise` before launching the worker thread. Inside `main()`, calling `primeNumFuture.get()` blocks execution until the worker thread calls `primePromise.set_value(count)`. Once set, the value is returned, and `main()` continues.

> **Note:** The `get()` method of `std::future` can only be called once. Calling `get()` a second time on the same future object results in undefined behavior or throws a `std::future_error`. If multiple threads need to retrieve the same result, use `std::shared_future` instead.

## Summary

Thread synchronization in C++ prevents data corruption and concurrency errors in multithreaded environments. C++ provides three main synchronization tools: Mutexes to enforce mutual exclusion on critical sections; Condition Variables to allow threads to sleep and notify each other of resource status changes; and Promise/Future structures to cleanly return a single value from a worker thread to the calling thread. Selecting the appropriate synchronization model ensures thread safety and reliable execution flow.




