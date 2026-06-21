# ReentrantLock in Java

In Java, a **Reentrant Lock** is a part of the `java.util.concurrent.locks` package and provides a more flexible mechanism for thread synchronization compared to the intrinsic locks managed by the `synchronized` keyword. It allows threads to enter a lock multiple times (reentrant behavior) without causing a deadlock on itself.

- **Reentrancy**: The same thread can acquire the lock multiple times. Each lock acquisition must be paired with a corresponding unlock.
- **Explicit Locking**: Unlike the synchronized keyword, ReentrantLock requires manual locking and unlocking using `lock()` and `unlock()`.
- **Interruptible Waits**: Threads waiting to acquire a lock can be interrupted, allowing them to stop waiting.
- **Non-blocking tryLock()**: Threads can attempt to acquire a lock immediately without waiting indefinitely.
- **Fairness Policy**: Locks can be configured to grant access in a first-come-first-serve order (FIFO queue).

## Declaration and Usage

Reentrant locks are created using the `ReentrantLock` class. The programmer must explicitly acquire the lock before entering a critical section and release it in a `finally` block to guarantee release under all execution paths.

### Java Implementation (Basic Usage)

The following example demonstrates how to declare, acquire, and release a `ReentrantLock` when performing a shared task.

```java
import java.util.concurrent.locks.ReentrantLock;

class SharedResource {
    private final ReentrantLock lock = new ReentrantLock();

    public void performTask() {
        // Acquire lock explicitly
        lock.lock();
        try {
            // Critical section code
            System.out.println(Thread.currentThread().getName() + " is performing task on AlphaKnowledge");
        } finally {
            // Release lock in the finally block
            lock.unlock();
        }
    }
}

public class AlphaKnowledgeDemo {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread t1 = new Thread(resource::performTask, "TeslaWorker");
        Thread t2 = new Thread(resource::performTask, "BMWWorker");

        t1.start();
        t2.start();
    }
}
```

### Output
TeslaWorker is performing task on AlphaKnowledge
BMWWorker is performing task on AlphaKnowledge

### Explanation

- `lock.lock()` acquires the lock. If another thread already holds it, the current thread is suspended and waits.
- The critical section contains printing statements that can only be executed by one thread at a time.
- `lock.unlock()` releases the lock inside the `finally` block to ensure it is freed even if runtime exceptions occur.

## Reentrant Behavior Example

The reentrant capability of a lock means that if a thread holds the lock, it can reacquire it without blocking itself. This is highly useful when a synchronized method calls another synchronized method within the same lock context.

### Java Implementation (Reentrant Behavior)

The following code demonstrates a single thread acquiring the same `ReentrantLock` recursively across two different methods without causing a self-deadlock.

```java
import java.util.concurrent.locks.ReentrantLock;

public class ReentrantExample {
    private final ReentrantLock lock = new ReentrantLock();

    public void methodA() {
        lock.lock();
        try {
            System.out.println("Inside Method A");
            // Reentrant behavior allows the same thread to acquire the lock again in methodB
            methodB();
        } finally {
            lock.unlock();
        }
    }

    public void methodB() {
        lock.lock();
        try {
            System.out.println("Inside Method B");
        } finally {
            lock.unlock();
        }
    }

    public static void main(String[] args) {
        System.out.println("Starting ReentrantLock Behavior Demo on AlphaKnowledge...");
        ReentrantExample example = new ReentrantExample();
        example.methodA();
    }
}
```

### Output
Starting ReentrantLock Behavior Demo on AlphaKnowledge...
Inside Method A
Inside Method B

### Explanation

- The main thread enters `methodA()`, acquiring the lock for the first time.
- While holding the lock, it invokes `methodB()`, which attempts to acquire the same lock.
- Because the lock is reentrant and the calling thread is already the owner, it successfully acquires the lock a second time (incrementing the hold count).
- Both lock acquisitions are released sequentially via their respective `finally` blocks, decrementing the hold count back to zero.

## Fairness Policy

Reentrant locks can be configured with an optional fairness policy using the boolean constructor:

```java
ReentrantLock fairLock = new ReentrantLock(true); // Fair lock
```

- **Fair Lock**: Threads acquire the lock in the exact order they requested it (First-In-First-Out). This guarantees thread allocation and reduces starvation, but introduces a minor throughput overhead.
- **Non-Fair Lock (Default)**: Threads can acquire the lock in arbitrary order. This can improve overall throughput but may cause thread starvation for long-waiting threads.

## ReentrantLock Methods

The `ReentrantLock` class provides several built-in methods for fine-grained monitoring and control:

| Method | Description |
| --- | --- |
| **lock()** | Acquires the lock, incrementing the hold count. If the resource is free, the calling thread gets it immediately. |
| **unlock()** | Releases the lock, decrementing the hold count. When the count reaches zero, the resource is released. |
| **tryLock()** | Attempts to acquire the lock without blocking. Returns `true` if successful, and `false` if the lock is held by another thread. |
| **tryLock(long timeout, TimeUnit unit)** | Waits up to the specified time to acquire the lock, exiting with `false` if unsuccessful. |
| **lockInterruptibly()** | Acquires the lock unless the thread is interrupted while waiting in a blocked state. |
| **getHoldCount()** | Returns the number of times the current thread holds the lock. |
| **isHeldByCurrentThread()** | Returns `true` if the current thread holds the lock. |
| **hasQueuedThreads()** | Checks if there are any threads waiting to acquire the lock. |
| **isLocked()** | Returns `true` if any thread holds the lock. |
| **newCondition()** | Returns a `Condition` instance associated with this lock for advanced thread coordination. |

## Advantages over synchronized

| Feature | synchronized | ReentrantLock |
| --- | --- | --- |
| **Lock acquisition** | Implicitly handled by JVM scope | Explicitly handled using `lock()` and `unlock()` |
| **Interruptible** | No; waiting threads block indefinitely | Yes; via `lockInterruptibly()` |
| **Try-lock** | No | Yes; via `tryLock()` |
| **Fairness** | No; managed implicitly by OS thread scheduler | Optional; configurable via constructor |
| **Reentrant** | Yes; built-in JVM feature | Yes; built-in API feature |

# Summary

ReentrantLock is an explicit synchronization construct in Java that offers developers highly flexible alternatives to traditional synchronized blocks. It supports reentrant locking, allowing the same thread to acquire a lock multiple times recursively without self-blocking. Beyond mutual exclusion, ReentrantLock provides advanced scheduling features such as configurable fairness policies to prevent thread starvation, non-blocking lock attempts via `tryLock()`, and interruptible lock waiting states. Although it requires careful manual management to ensure that `unlock()` is always invoked within a `finally` block, ReentrantLock remains the preferred tool for constructing robust, high-performance, and complex concurrent systems in modern Java applications.




