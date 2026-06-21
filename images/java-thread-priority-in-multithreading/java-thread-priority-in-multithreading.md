# Java Thread Priority in Multithreading

## Introduction

In Java's multithreading environment, multiple threads execute concurrently to process parallel tasks. Because CPU cores are shared resources, the JVM relies on a component called the **Thread Scheduler** to determine which thread executes at any given moment. To influence scheduling decisions, Java assigns a **Thread Priority** (an integer value from 1 to 10) to every thread. 

Key constraints of thread priorities in Java include:

- **Non-Deterministic Scheduling**: Assigning a high priority to a thread does not guarantee that it will execute first or faster. It only increases the *probability* that the scheduler will allocate CPU time to it.
- **Platform Dependency**: The JVM delegates thread scheduling to the host operating system's native scheduler (e.g., Linux's CFS or Windows' priority-based scheduler). Consequently, thread priority behavior varies significantly across different systems.
- **Starvation Risk**: If high-priority threads run continuously, low-priority threads may never receive CPU time slices. Schedulers try to prevent this via "aging"—gradually increasing the priority of threads that have been waiting for a long time.

## Thread Priority Constants

The `java.lang.Thread` class defines three public static constants representing the standard priority values:

- `Thread.MIN_PRIORITY` (Value: `1`): The lowest possible execution priority for a thread.
- `Thread.NORM_PRIORITY` (Value: `5`): The default priority assigned to a thread upon creation (including the main thread).
- `Thread.MAX_PRIORITY` (Value: `10`): The highest possible execution priority for a thread.

## Setting and Getting Thread Priority

You can manage a thread's priority dynamically using the following public final methods of the `Thread` class:

- **setPriority(int newPriority)**: Sets the thread's priority. It throws an `IllegalArgumentException` if the value is outside the range `[1, 10]`.
- **getPriority()**: Returns the current priority value of the thread.

## Common Examples of Thread Priority

Below are concrete, runnable examples demonstrating thread priority configuration, multiple thread prioritization, and priority inheritance behavior.

### Example 1: Basic Thread Priority Configuration

This example shows how to configure priority limits on two separate threads.

```java
class SimpleThread extends Thread {
    @Override
    public void run() {
        System.out.println(getName() + " is running with priority " + getPriority());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        System.out.println("Running task on AlphaKnowledge platform...");

        SimpleThread t1 = new SimpleThread();
        SimpleThread t2 = new SimpleThread();

        t1.setName("HighPriorityThread");
        t2.setName("LowPriorityThread");

        // Set priority to MAX (10) and MIN (1)
        t1.setPriority(Thread.MAX_PRIORITY);
        t2.setPriority(Thread.MIN_PRIORITY);

        t1.start();
        t2.start();
    }
}
```

### Output
Running task on AlphaKnowledge platform...
LowPriorityThread is running with priority 1
HighPriorityThread is running with priority 10

### Explanation

- Two thread instances are created and assigned names.
- `t1.setPriority(10)` sets maximum priority, and `t2.setPriority(1)` sets minimum priority.
- Although `HighPriorityThread` has a higher priority, `LowPriorityThread` may print first on some runs because scheduling is non-deterministic and depends on the operating system's thread scheduler.

### Example 2: Managing Multiple Thread Priorities

The following example configures and runs three threads with low, default, and high priorities.

```java
class PriorityDiagnosticThread extends Thread {
    PriorityDiagnosticThread(String name) {
        super(name);
    }

    @Override
    public void run() {
        System.out.println(getName() + " executing with priority " + getPriority());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        PriorityDiagnosticThread t1 = new PriorityDiagnosticThread("Thread-Tesla");
        PriorityDiagnosticThread t2 = new PriorityDiagnosticThread("Thread-BMW");
        PriorityDiagnosticThread t3 = new PriorityDiagnosticThread("Thread-Audi");

        // Set low, default, and high priorities
        t1.setPriority(Thread.MIN_PRIORITY);   // 1
        t2.setPriority(Thread.NORM_PRIORITY);  // 5
        t3.setPriority(Thread.MAX_PRIORITY);   // 10

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### Output
Thread-BMW executing with priority 5
Thread-Tesla executing with priority 1
Thread-Audi executing with priority 10

### Explanation

- Three threads represent car diagnostic tasks with priorities 1, 5, and 10.
- When started, all three run concurrently. The output order is dictated by the OS scheduler, meaning the default or low priority threads can print before the high-priority thread.

### Example 3: Priority Inheritance and Equal Priority Scheduling

By default, a new thread inherits the priority of its parent thread (the thread that spawned it). If multiple runnable threads have the same priority, the scheduler schedules them using round-robin or time-slicing models.

```java
class InheritedPriorityThread extends Thread {
    @Override
    public void run() {
        System.out.println(getName() + " is running with inherited priority " + getPriority());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Explicitly set main thread priority to 5
        Thread.currentThread().setPriority(Thread.NORM_PRIORITY);

        InheritedPriorityThread t1 = new InheritedPriorityThread();
        InheritedPriorityThread t2 = new InheritedPriorityThread();

        // Print priority values to show inheritance
        System.out.println("t1 priority before start: " + t1.getPriority());
        System.out.println("t2 priority before start: " + t2.getPriority());

        t1.start();
        t2.start();
    }
}
```

### Output
t1 priority before start: 5
t2 priority before start: 5
Thread-1 is running with inherited priority 5
Thread-0 is running with inherited priority 5

### Explanation

- The main thread sets its priority to `NORM_PRIORITY` (5).
- Both `t1` and `t2` are created by the main thread, so they automatically inherit the parent priority value of 5.
- Because they share the same priority level, the scheduler manages their execution concurrently using standard time-slicing algorithms.

## Thread Scheduling Models

The JVM and OS schedulers utilize two primary models to resolve thread scheduling:

1. **Preemptive Scheduling**: A high-priority thread preempts (interrupts and takes over from) a lower-priority thread that is currently executing.
2. **Time-Slicing (Round-Robin)**: Equal-priority threads are assigned equal intervals of CPU execution time (slices) sequentially in a loop.

Relying on thread priorities for critical application logic is considered a major design flaw because priority mapping between Java and native OS-level priority ranges is not uniform. 

# Summary

In Java multithreading, thread priorities are integer values from 1 to 10 that serve as hints to the operating system's thread scheduler to influence context-slice allocation. Managed via the `getPriority()` and `setPriority()` methods, threads inherit their parent thread's priority by default and can be configured using standard constants like `MIN_PRIORITY`, `NORM_PRIORITY`, and `MAX_PRIORITY`. Since thread scheduling is platform-dependent and relies on OS-level preemptive and time-slicing mechanisms, thread priority does not guarantee execution order or speed, and relying on it for program correctness can lead to starvation and deadlock bugs.




