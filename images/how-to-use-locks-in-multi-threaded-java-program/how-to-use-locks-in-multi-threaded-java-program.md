# How to Use Locks in Multi-Threaded Java Program

## Introduction

In Java, a **Lock** is a synchronization mechanism defined in the `java.util.concurrent.locks` package (introduced in Java 5). It provides more flexible, structured, and extensible locking operations than traditional implicit synchronization blocks and methods. While `synchronized` locks are tied to the execution scope of methods or blocks, the explicit Lock API allows developers to acquire and release locks in different scopes, implement timeout policies, allow interruptible waiting, and configure thread allocation fairness.

The two most common lock models in Java are:

- **Exclusive Lock (ReentrantLock)**: Ensures strict mutual exclusion, allowing only one thread to hold the lock and access the critical section at any given time.
- **Shared Lock (ReadWriteLock)**: Allows multiple reader threads to access a resource concurrently while restricting writes to a single exclusive thread, ensuring high performance for read-heavy resources.

### Basic Lock Usage

Unlike implicit synchronization, explicit locks require manual acquisition and release. It is critical to release locks inside a `finally` block to prevent resource leaks (deadlocks) in the event of runtime exceptions:

```java
Lock lock = new ReentrantLock();
lock.lock(); // Acquire the lock
try {
    // Critical section (shared data modification)
} finally {
    lock.unlock(); // Guaranteed lock release
}
```

## Types of Locks in Java

Java provides several built-in Lock implementations to solve different concurrency patterns:

### 1. ReentrantLock

A `ReentrantLock` is an exclusive lock that allows a thread to reacquire the lock it already holds without causing a self-deadlock. It supports a **Fairness Parameter** (`new ReentrantLock(true)`), which ensures that the thread scheduler allocates the lock to the longest-waiting thread, reducing starvation.

```java
import java.util.concurrent.locks.ReentrantLock;

class DiagnosticWorker implements Runnable {
    private final ReentrantLock lock;
    private final String threadName;

    DiagnosticWorker(ReentrantLock lock, String threadName) {
        this.lock = lock;
        this.threadName = threadName;
    }

    @Override
    public void run() {
        lock.lock(); // Acquire exclusive lock
        try {
            System.out.println(threadName + " acquired lock");
            Thread.sleep(1000); // Simulate diagnostics task
            System.out.println(threadName + " finished work");
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock(); // Release lock in finally block
        }
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        System.out.println("Executing lock demonstration on AlphaKnowledge...");
        ReentrantLock lock = new ReentrantLock();

        Thread t1 = new Thread(new DiagnosticWorker(lock, "Thread-Tesla"));
        Thread t2 = new Thread(new DiagnosticWorker(lock, "Thread-BMW"));

        t1.start();
        t2.start();
    }
}
```

### Output
Executing lock demonstration on AlphaKnowledge...
Thread-Tesla acquired lock
Thread-Tesla finished work
Thread-BMW acquired lock
Thread-BMW finished work

### Explanation

- Two worker threads (`Thread-Tesla` and `Thread-BMW`) attempt to enter their run methods concurrently.
- `Thread-Tesla` acquires the exclusive lock first, causing `Thread-BMW` to block and wait.
- Only after `Thread-Tesla` invokes `unlock()` in the `finally` block can `Thread-BMW` acquire the lock and execute.

### 2. ReadWriteLock

A `ReadWriteLock` separates locking for read-only operations from write-only operations. Multiple threads can hold the read lock simultaneously as long as there are no writers. Only a single thread can hold the write lock, blocking all readers and other writers.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

class CarDiagnosticsLog {
    private final List<String> logList = new ArrayList<>();
    private final ReadWriteLock rwLock = new ReentrantReadWriteLock();
    private final Lock readLock = rwLock.readLock();
    private final Lock writeLock = rwLock.writeLock();

    // Writer requires exclusive lock
    public void appendLog(String entry) {
        writeLock.lock();
        try {
            logList.add(entry);
            System.out.println(Thread.currentThread().getName() + " logged: " + entry);
        } finally {
            writeLock.unlock();
        }
    }

    // Reader requires shared lock
    public void printLog(int index) {
        readLock.lock();
        try {
            if (index < logList.size()) {
                System.out.println(Thread.currentThread().getName() + " read: " + logList.get(index));
            }
        } finally {
            readLock.unlock();
        }
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsLog log = new CarDiagnosticsLog();

        // Writers (Exclusive)
        Thread writer1 = new Thread(() -> log.appendLog("Tesla Diagnostics Completed"), "Writer-1");
        Thread writer2 = new Thread(() -> log.appendLog("BMW Diagnostics Completed"), "Writer-2");

        // Readers (Shared)
        Thread reader1 = new Thread(() -> log.printLog(0), "Reader-1");
        Thread reader2 = new Thread(() -> log.printLog(1), "Reader-2");

        writer1.start();
        writer2.start();
        reader1.start();
        reader2.start();
    }
}
```

### Output
Writer-1 logged: Tesla Diagnostics Completed
Writer-2 logged: BMW Diagnostics Completed
Reader-1 read: Tesla Diagnostics Completed
Reader-2 read: BMW Diagnostics Completed

### Explanation

- The writers acquire the exclusive `writeLock` sequentially to safely mutate the shared `logList` instance.
- The readers acquire the shared `readLock` concurrently. Multiple readers are allowed to read the data at the same time, optimizing throughput compared to standard full synchronization.

## Methods in the Lock Interface

The `java.util.concurrent.locks.Lock` interface defines several methods for fine-grained synchronization control:

| Method | Description |
| --- | --- |
| **void lock()** | Acquires the lock if it is available. If the lock is held by another thread, the calling thread blocks and is suspended until the lock is released. |
| **void lockInterruptibly()** | Acquires the lock unless the current thread is interrupted. Allows the thread to break out of its blocked waiting state if another thread calls `interrupt()`. |
| **void unlock()** | Releases the lock. Must be placed in a `finally` block to prevent resource leaks. |
| **Condition newCondition()** | Returns a new `Condition` instance bound to this lock. Serves as a more flexible alternative to `Object.wait()` and `notify()`. |
| **boolean tryLock()** | Attempts to acquire the lock immediately. Returns `true` if successful, and `false` if the lock is held by another thread, avoiding thread blocking. |
| **boolean tryLock(long time, TimeUnit unit)** | Tries to acquire the lock within the specified timeout duration. Returns `true` if successful, or `false` if the timeout expires before acquisition. |

# Summary

Explicit locks in Java provide a robust, flexible alternative to implicit synchronization, offering developers fine-grained control over resource locking. Through implementations like `ReentrantLock` (exclusive mutual exclusion with optional fairness parameters) and `ReadWriteLock` (shared concurrent reads and exclusive writes), the Lock API supports advanced features such as non-blocking lock attempts (`tryLock()`), timeout-based waits, and interruptible locks. Because explicit locks must be manually acquired and released, enclosing the `unlock()` invocation within a `finally` block is mandatory to guarantee lock release and avoid application deadlocks.




