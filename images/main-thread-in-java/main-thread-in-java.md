# Main Thread in Java

## Introduction

When a Java program starts up, the Java Virtual Machine (JVM) automatically creates a special thread of execution known as the **Main Thread**. This thread is responsible for executing the application's entry point—the `main()` method—and controlling the initial execution flow of the program.

Key characteristics of the Main Thread include:

- **Parent Thread**: It is the default parent thread from which all subsequent user-defined (child) threads are spawned.
- **Default Name**: The JVM assigns the default name `"main"` to this thread.
- **Default Priority**: By default, the main thread runs with a priority of `5` (represented by `Thread.NORM_PRIORITY`).
- **Shutdown Control**: The main thread typically finishes last because it performs cleanup operations, manages user-defined threads, and coordinates the graceful shutdown of the JVM.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/main-thread-in-java/1782030226661-82c78b0f-2080-4406-8182-b9af5374c576.png)

## JVM Startup and Lifecycle of the Main Thread

The lifecycle of the main thread is closely bound to the JVM's initialization process:

1. **JVM Booting**: The operating system launches the Java launcher (e.g., `java.exe`), which starts the JVM, allocates the heap, and loads core system classes.
2. **Main Thread Spawning**: The JVM spawns a native thread designated as the main execution thread.
3. **Class Resolution**: The main thread loads the class specified in the command line argument, verifies its bytecode, and searches for the mandatory entry-point method signature: `public static void main(String[] args)`. If this method is missing, the JVM halts execution.
4. **Execution Flow**: The main thread runs the statements inside the `main()` method. When the `main()` method ends, the main thread terminates. However, if the main thread has spawned non-daemon child threads, the JVM continues to run until all non-daemon threads complete.

## Controlling the Main Thread

Although the main thread is created automatically, developers can inspect and modify its properties programmatically. To control it, you must first get a reference to it using `Thread.currentThread()`, which returns the currently executing thread instance.

### Thread Properties Manipulation

- **getName() / setName()**: Allows reading and changing the thread name for debugging and logging purposes.
- **getPriority() / setPriority()**: Allows reading and changing the thread priority (ranging from `Thread.MIN_PRIORITY` of 1 to `Thread.MAX_PRIORITY` of 10).
- **Priority Inheritance**: Any child thread created by the main thread inherits the main thread's priority value at the moment of creation.

```java
import java.io.*;

public class AlphaKnowledge extends Thread {
    public static void main(String[] args) {
        // Getting reference to the Main thread
        Thread t = Thread.currentThread();

        // Getting name of the Main thread
        System.out.println("Current thread: " + t.getName());

        // Changing the name of the Main thread
        t.setName("AlphaKnowledge");
        System.out.println("After name change: " + t.getName());

        // Getting priority of the Main thread
        System.out.println("Main thread priority: " + t.getPriority());

        // Setting priority of the Main thread to MAX (10)
        t.setPriority(MAX_PRIORITY);
        System.out.println("Main thread new priority: " + t.getPriority());

        for (int i = 0; i < 2; i++) {
            System.out.println("Main thread processing diagnostics...");
        }

        // Main thread creating a child thread
        Thread ct = new Thread() {
            @Override
            public void run() {
                for (int i = 0; i < 2; i++) {
                    System.out.println("Child thread running car diagnostic check...");
                }
            }
        };

        // Child thread inherits the priority of its parent (10)
        System.out.println("Child thread inherited priority: " + ct.getPriority());

        // Setting priority of the child thread to MIN (1)
        ct.setPriority(MIN_PRIORITY);
        System.out.println("Child thread new priority: " + ct.getPriority());

        // Starting child thread execution
        ct.start();
    }
}
```

### Output
Current thread: main
After name change: AlphaKnowledge
Main thread priority: 5
Main thread new priority: 10
Main thread processing diagnostics...
Main thread processing diagnostics...
Child thread inherited priority: 10
Child thread new priority: 1
Child thread running car diagnostic check...
Child thread running car diagnostic check...

### Explanation

- `Thread.currentThread()` fetches the thread instance executing the static `main()` method.
- The name of the main thread is changed dynamically to `"AlphaKnowledge"`.
- The parent thread's priority is set to `10`. Consequently, when the child thread `ct` is instantiated, it automatically inherits this priority (`10`).
- The child thread's priority is later lowered to `1` using `ct.setPriority(MIN_PRIORITY)` before starting.

## Deadlock Using the Main Thread

A deadlock is a situation where two or more threads are blocked forever, waiting for each other. Interestingly, a single-threaded program can experience a deadlock if the main thread waits for itself to finish.

### Self-Deadlock Mechanics

Calling `Thread.currentThread().join()` instructs the currently running thread (the main thread) to wait until the target thread terminates. Since the target thread is the main thread itself, it enters an infinite waiting state, blocking execution permanently.

```java
public class AlphaKnowledge {
    public static void main(String[] args) {
        try {
            System.out.println("Entering into Deadlock...");

            // Main thread joins itself, waiting indefinitely
            Thread.currentThread().join();

            // This statement will never execute
            System.out.println("This statement will never execute");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### Output
Entering into Deadlock...

### Explanation

- The call to `Thread.currentThread().join()` blocks the main thread.
- Because the main thread is waiting for itself to die, and it cannot die until it finishes executing the method, it remains suspended indefinitely.
- The subsequent print statement is never reached, resulting in a silent application hang (deadlock).

## Architectural Comparison: Main Thread vs Child Threads

The differences between the main thread and user-defined child threads are outlined below:

| Feature | Main Thread | Child Threads |
| --- | --- | --- |
| **Creation Mechanism** | Spawned automatically by the JVM launcher on startup. | Created manually by developers or executors in code. |
| **Default Name** | `"main"` | `"Thread-0"`, `"Thread-1"`, etc. (or pool-based names). |
| **Default Priority** | `5` (`Thread.NORM_PRIORITY`). | Inherits parent thread priority at instantiation. |
| **Execution Entry Point** | Executes the static `main(String[] args)` method. | Executes the overridden `run()` method of a Runnable/Thread. |
| **Lifecycle Impact** | Spawns initial child threads, but JVM can run after it terminates. | If declared as daemon, JVM terminates them automatically when non-daemon threads die. |

# Summary

The main thread in Java is the initial execution thread created automatically by the JVM to execute the application's `main()` entry method. It serves as the default parent thread from which all child threads are spawned and inherits basic properties such as a priority of 5 and the name `"main"`, which can be inspected and modified dynamically using `Thread.currentThread()`. By calling methods like `join()` on itself, the main thread can trigger a self-deadlock, suspending execution indefinitely. Understanding the main thread's lifecycle, priority inheritance mechanisms, and relationship with child threads is fundamental for developing robust concurrent Java applications.




