# Deadlock in Java Multithreading

Deadlock is a situation in multithreading where two or more threads are permanently blocked because each one is waiting for the other to release a required lock. In simple terms, threads get stuck forever, and the program never continues.

- Each thread holds a lock and waits for another lock held by a different thread.
- This creates a circular wait, causing the application to freeze indefinitely.

## Understanding Deadlocks

A deadlock occurs when threads develop a circular dependency on a set of locks. For example, if Thread 1 holds Lock A and requests Lock B, while Thread 2 holds Lock B and requests Lock A, neither thread can proceed. Since both threads wait indefinitely for the other to release their locks, the application hangs.

### Java Implementation (Deadlock Condition)

Below is an example demonstrating a deadlock condition in Java where two threads attempt to acquire locks on two shared resources in opposite orders.

```java
// Utility class to pause thread execution safely
class Util {
    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}

// Shared class with synchronized methods representing locked resources
class Shared {
    // First synchronized method
    synchronized void test1(Shared s2) {
        System.out.println(Thread.currentThread().getName() + " enters test1 of " + this);
        Util.sleep(1000);

        // Trying to call test2 on another object (requires s2's monitor lock)
        s2.test2();
        System.out.println(Thread.currentThread().getName() + " exits test1 of " + this);
    }

    // Second synchronized method
    synchronized void test2() {
        System.out.println(Thread.currentThread().getName() + " enters test2 of " + this);
        Util.sleep(1000);
        System.out.println(Thread.currentThread().getName() + " exits test2 of " + this);
    }
}

class Thread1 extends Thread {
    private final Shared s1;
    private final Shared s2;

    public Thread1(Shared s1, Shared s2) {
        this.s1 = s1;
        this.s2 = s2;
    }

    @Override
    public void run() {
        s1.test1(s2);
    }
}

class Thread2 extends Thread {
    private final Shared s1;
    private final Shared s2;

    public Thread2(Shared s1, Shared s2) {
        this.s1 = s1;
        this.s2 = s2;
    }

    @Override
    public void run() {
        s2.test1(s1);
    }
}

public class AK {
    public static void main(String[] args) {
        System.out.println("Starting AlphaKnowledge Deadlock Demonstration...");

        Shared s1 = new Shared();
        Shared s2 = new Shared();

        Thread1 t1 = new Thread1(s1, s2);
        t1.setName("Thread-Tesla");
        t1.start();

        Thread2 t2 = new Thread2(s1, s2);
        t2.setName("Thread-BMW");
        t2.start();

        // Keep main thread alive to monitor execution
        Util.sleep(2000);
    }
}
```

### Output
Starting AlphaKnowledge Deadlock Demonstration...
Thread-Tesla enters test1 of Shared@...
Thread-BMW enters test1 of Shared@...

### Explanation

- The program execution gets permanently stuck at this point. It does not complete because:
- `Thread-Tesla` starts by acquiring a lock on the `s1` object and enters the `test1()` method.
- Concurrently, `Thread-BMW` starts by acquiring a lock on the `s2` object and enters its own `test1()` method.
- Inside `test1()`, `Thread-Tesla` attempts to call `s2.test2()`, which requires acquiring the lock on `s2` (currently held by `Thread-BMW`).
- Meanwhile, `Thread-BMW` attempts to call `s1.test2()`, which requires acquiring the lock on `s1` (currently held by `Thread-Tesla`).
- Both threads enter a blocked state waiting for each other to release their respective locks, creating a circular wait and freezing execution.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/deadlock-in-java-multithreading/1782030817827-fc169173-304e-4fdc-ad4a-17ea68dd623e.png)

## Detecting Deadlocks

We can detect deadlocks in a running Java application using JVM diagnostic utilities:

### 1. List Active Java Processes

Use the Java Virtual Machine Process Status Tool (`jps`) to list all active Java processes with their fully qualified main class names:

```bash
jps -l
```

### 2. Generate and Analyze Thread Dumps

Identify the Process ID (PID) of the target application and trigger a thread print operation using `jcmd`:

```bash
jcmd <PID> Thread.print
```

Alternatively, you can generate a thread dump using:

```bash
jstack -l <PID>
```

When analyzing the thread dump output, the JVM will explicitly declare if it found a deadlock:

```Code
Found one Java-level deadlock:
=============================
"Thread-Tesla":
  waiting to lock monitor 0x000000001e4a3c18 (object 0x000000076b9dfa38, a Shared),
  which is held by "Thread-BMW"
"Thread-BMW":
  waiting to lock monitor 0x000000001e4a3b10 (object 0x000000076b9dfa28, a Shared),
  which is held by "Thread-Tesla"
```

## Preventing Deadlocks

Avoiding deadlocks requires careful design of lock acquisition strategies. Below are key methods used to mitigate and prevent deadlock situations:

- **Avoid Nested Locks**: This is the primary cause of deadlocks. Try to avoid acquiring multiple locks simultaneously. If nested locking is unavoidable, always acquire locks in a globally consistent order across all threads.
- **Avoid Unnecessary Locks**: Only synchronize the critical sections of code that directly modify shared state. Unnecessary or coarse-grained locking increases contention and the probability of deadlocks.
- **Use Timed Lock Acquisition**: Instead of blocking indefinitely using the implicit `synchronized` keyword, utilize the Lock API's `tryLock(long timeout, TimeUnit unit)` method. This allows a thread to back off and release its own locks if it fails to acquire the target lock within a specified duration.
- **Using Thread Join**: If one thread must wait for another thread to finish, use `join()` with a maximum timeout rather than waiting indefinitely.

# Summary

A deadlock in Java multithreading is a state in which two or more threads are permanently blocked, each waiting to acquire a lock held by another thread in a circular dependency chain. Traditional implicit synchronization methods using the synchronized keyword are highly vulnerable to deadlocks because blocked threads wait indefinitely and cannot be interrupted. Developers can detect active deadlocks in production environments by generating and analyzing thread dumps using JVM diagnostic tools like jps, jcmd, and jstack. To prevent deadlocks, applications should implement strict design strategies such as establishing consistent lock acquisition ordering, minimizing the scope of synchronized blocks, avoiding nested locks, and utilizing the explicit Lock API's tryLock method to attempt non-blocking, timed lock acquisitions.




