# Java Thread.start() vs Thread.run() Method

## Introduction

In Java's multithreading model, `start()` and `run()` are the two key methods defined in the `java.lang.Thread` class that control how thread execution begins. While they might seem similar because they both execute the thread's core logic, they behave very differently from an architectural and runtime perspective. This article explains the internal JVM behaviors, native operating system interactions, thread state transitions, multiple invocation rules, and best practices for using both methods.

## 1. Deep Dive: The Thread.start() Method

The `start()` method is used to launch a new, concurrent execution thread. When you call `t1.start()`, it does not immediately execute the logic inside `run()`. Instead, it signals the JVM to perform the underlying system setup needed to execute a parallel task.

### JVM Internals & OS Mapping

When `start()` is invoked, the JVM performs the following low-level tasks:

- **State Validation**: Checks that the thread is in a state where it is allowed to start.
- **Native OS Thread Creation**: The JVM calls a native helper method (typically `private native void start0()`). This method communicates with the host operating system's native thread APIs (e.g., `pthread_create` on Linux/POSIX systems or `CreateThread` on Windows). On modern JVMs, a 1-to-1 mapping model is used, meaning every Java thread corresponds to one native operating system thread.
- **Memory Allocation**: The OS allocates a new runtime call stack for the thread (configured via the `-Xss` JVM option) to hold its local variables and method call stack frames.
- **Thread Scheduler Insertion**: The thread moves from the `NEW` state to the `RUNNABLE` state. It is handed over to the OS thread scheduler, which determines when to context-switch it onto an active CPU core.
- **Asynchronous run() Invocation**: Once scheduled, the new thread runs independently, creating its own execution call stack, and internally invokes the overridden `run()` method.

```java
class CarDiagnosticsTask extends Thread {
    private String carModel;

    CarDiagnosticsTask(String carModel) {
        this.carModel = carModel;
    }

    @Override
    public void run() {
        System.out.println("Processing car diagnostics for: " + carModel + " on AlphaKnowledge");
        System.out.println("Execution thread: " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsTask t1 = new CarDiagnosticsTask("Tesla");

        // Triggers JVM to spawn a new native execution thread
        t1.start();
    }
}
```

### Output
Processing car diagnostics for: Tesla on AlphaKnowledge
Execution thread: Thread-0

### Explanation

- The call to `t1.start()` returns immediately to the main thread, allowing the main method to continue executing concurrently.
- The JVM allocates a separate call stack for `Thread-0`.
- The operating system scheduler allocates CPU slices to `Thread-0`, which executes the `run()` method in the background, printing `"Tesla on AlphaKnowledge"` and identifying the thread name as `"Thread-0"`.

## 2. Deep Dive: The Thread.run() Method

The `run()` method contains the code that is executed by the thread. However, calling `run()` directly on a Thread object does not spawn a new thread. Instead, it behaves exactly like calling any normal method on a standard Java object.

### Synchronous Call Stack Behavior

When `t1.run()` is called directly:

- **No Native OS Calls**: The native method `start0()` is never executed. No request is sent to the operating system to create a new thread or allocate a separate stack.
- **Caller Thread Stack Execution**: The instructions within the `run()` method are executed inside the call stack of the calling thread (the thread that invoked the method, such as `main`).
- **Synchronous Execution**: The caller thread is blocked and cannot proceed to subsequent lines of code until the execution of the `run()` method finishes.
- **No Concurrency**: The application runs sequentially, meaning no parallel execution takes place.

```java
class CarDiagnosticsTask extends Thread {
    private String carModel;

    CarDiagnosticsTask(String carModel) {
        this.carModel = carModel;
    }

    @Override
    public void run() {
        System.out.println("Processing car diagnostics for: " + carModel);
        System.out.println("Execution thread: " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsTask t1 = new CarDiagnosticsTask("BMW");

        // Direct method call - behaves like a normal Java method
        t1.run();
    }
}
```

### Output
Processing car diagnostics for: BMW
Execution thread: main

### Explanation

- The call to `t1.run()` blocks the `main` method execution.
- No separate thread is created. The thread executing the `run()` method is reported as `"main"`, demonstrating that the code ran synchronously on the primary application thread.

## 3. Multiple Invocations: State Validation & Exceptions

A critical difference between `start()` and `run()` is how they handle multiple invocations on the same Thread instance.

### The start() Constraint

A Java Thread object represents a state machine with a lifecycle managed by the JVM. Once `start()` is called and the thread is launched, its internal state transitions from `NEW` to `RUNNABLE`. 

- **Internal Check**: The JVM checks the thread's status at the beginning of the `start()` method. If the thread is not in the `NEW` state, it immediately throws an `IllegalThreadStateException`.
- **No Restarts**: Even if a thread has completed its task and has transitioned to the `TERMINATED` state, calling `start()` again on the same Thread object is illegal. You must create a new Thread instance to rerun a task.

### The run() Flexibility

Because `run()` is just a standard virtual method call, it is not bound by any state machine constraints. You can invoke `run()` on a Thread object as many times as you like, just like calling methods on a list or string object.

### Example 1: Multiple invocation of start() method

```java
class CarDiagnosticsTask extends Thread {
    @Override
    public void run() {
        System.out.println("Running task inside thread: " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsTask t = new CarDiagnosticsTask();
        t.start();
        t.start(); // Throws exception on second call
    }
}
```

### Output
Running task inside thread: Thread-0
Exception in thread "main" java.lang.IllegalThreadStateException

### Example 2: Multiple invocation of run() method

```java
class CarDiagnosticsTask extends Thread {
    @Override
    public void run() {
        System.out.println("Running task inside thread: " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsTask t = new CarDiagnosticsTask();
        t.run();
        t.run(); // Executes normally twice on main thread
    }
}
```

### Output
Running task inside thread: main
Running task inside thread: main

### Explanation

- In Example 1, the second `t.start()` invocation fails because the thread state is no longer `NEW`, resulting in an `IllegalThreadStateException`.
- In Example 2, calling `t.run()` twice runs the execution logic sequentially twice on the `main` thread, returning the current thread name as `"main"`.

## 4. Architectural Comparison: Thread.start() vs Thread.run()

The following table summarizes the structural and behavioral differences between the two methods:

| Feature | start() Method | run() Method |
| --- | --- | --- |
| **Thread Spawning** | Creates and initializes a new execution thread. | Does not spawn a new thread. |
| **Calling Stack** | Runs the code in a new, independent call stack. | Runs the code in the current caller's call stack. |
| **Concurrency Model** | Executes asynchronously (does not block caller). | Executes synchronously (blocks the calling thread). |
| **Native System Integration** | Calls native OS methods (`start0()`) to create threads. | No native system interactions are initiated. |
| **Multiple Invocations** | Allowed only once. Second call throws `IllegalThreadStateException`. | Allowed multiple times, behaving like any standard method call. |
| **State Transitions** | Transitions thread from `NEW` to `RUNNABLE`. | Does not impact the thread's lifecycle state machine. |
| **Syntax Usage** | `threadInstance.start();` | `threadInstance.run();` |

# Summary

In Java multithreading, the `start()` method is used to allocate thread resources and invoke the `run()` method concurrently within a new execution thread, whereas calling the `run()` method directly executes its code synchronously as a regular method call on the calling thread. Furthermore, a thread's `start()` method cannot be invoked more than once on the same object without throwing an `IllegalThreadStateException`, while the `run()` method can be executed multiple times without any issues.




