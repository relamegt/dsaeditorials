# Java Runnable Interface

## Introduction

The `Runnable` interface is a functional interface in the `java.lang` package used to define a task that can be executed by a thread. It serves as a foundational component in Java's multithreading architecture, separating the core logic of a task (the "what") from the actual thread execution mechanism (the "how"). 

Key design aspects of the `Runnable` interface include:

- **Single Abstract Method**: It defines a single abstract method, `run()`, which holds the code to be executed when the thread starts.
- **Single Inheritance Preservation**: In Java, a class can extend only one superclass. By implementing `Runnable` instead of extending the `Thread` class, a class remains free to extend another class, promoting a cleaner class hierarchy and better design flexibility.
- **Separation of Concerns**: Implementing `Runnable` promotes loose coupling. The task definition can be reused across different thread execution architectures (e.g., manual threads, thread pools, and executors).

## Declaration

The `Runnable` interface is decorated with the `@FunctionalInterface` annotation and is declared as follows:

```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```

## Steps to Implement Runnable Interface

Using the `Runnable` interface involves three basic steps:

1. **Implement the Interface**: Create a class that implements `Runnable` and override the `run()` method with the task execution logic.
2. **Pass instance to Thread**: Instantiate the `Runnable` task and pass its reference to the constructor of a `java.lang.Thread` object.
3. **Start the Thread**: Call the `start()` method on the `Thread` instance, which signals the JVM to allocate a new stack and execute the `run()` method concurrently.

## Common Execution Models of Runnable

Below are detailed implementations demonstrating different ways to define and execute `Runnable` tasks.

### 1. Classic Class-Based Implementation

This is the standard approach where a dedicated class implements `Runnable` and is passed to a Thread object.

```java
class CarDiagnosticsJob implements Runnable {
    private String carModel;

    CarDiagnosticsJob(String carModel) {
        this.carModel = carModel;
    }

    @Override
    public void run() {
        System.out.println("Thread is running diagnostics on AlphaKnowledge for " + carModel);
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        CarDiagnosticsJob job = new CarDiagnosticsJob("Tesla");
        Thread t = new Thread(job);

        // Starts a new thread of execution
        t.start();
    }
}
```

### Output
Thread is running diagnostics on AlphaKnowledge for Tesla

### Explanation

- `CarDiagnosticsJob` implements `Runnable` and overrides `run()`.
- An instance of the task is passed to `new Thread(job)`.
- Invoking `t.start()` allocates a new call stack and executes `run()` concurrently on `Thread-0`.

### 2. Runnable with Lambda Expressions

Since `Runnable` is a functional interface, it can be written concisely using Java 8 lambda expressions without declaring a separate implementation class.

```java
public class AlphaKnowledge {
    public static void main(String[] args) {
        // Defining task using a lambda expression
        Runnable task = () -> {
            System.out.println("Thread is running using a lambda expression");
        };

        Thread t = new Thread(task);
        t.start();
    }
}
```

### Output
Thread is running using a lambda expression

### Explanation

- The lambda expression `() -> { ... }` matches the signature of the `run()` method.
- The JVM internally creates an anonymous implementation of `Runnable` containing this logic, which is executed concurrently when `t.start()` is called.

### 3. Runnable with the Executor Framework

For production-grade applications, manually spawning threads is discouraged due to resource overhead. The Java Concurrent API provides the Executor Framework to manage thread pools efficiently.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class AlphaKnowledge {
    public static void main(String[] args) {
        // Create a thread pool with 2 worker threads
        ExecutorService executor = Executors.newFixedThreadPool(2);

        // Submit tasks to the pool
        executor.execute(() -> {
            System.out.println("Task executed by Executor on thread: " + Thread.currentThread().getName());
        });

        // Gracefully shut down the executor service
        executor.shutdown();
    }
}
```

### Output
Task executed by Executor on thread: pool-1-thread-1

### Explanation

- `Executors.newFixedThreadPool(2)` initializes a pool of 2 reusable worker threads.
- `executor.execute()` submits the `Runnable` task. The framework assigns the task to an idle thread in the pool (`pool-1-thread-1`), avoiding the overhead of creating new threads.
- `executor.shutdown()` releases the resources and halts the executor service once tasks complete.

## Exception Handling inside Runnable

An important design detail of the `Runnable` interface is that the `run()` method signature does not declare a `throws` clause.

### Exception Constraints

- **Checked Exceptions**: Because the interface signature is `void run()`, you cannot throw checked exceptions (e.g., `IOException`, `SQLException`) out of the method. Any checked exception must be caught and handled inside the `run()` method using a `try-catch` block.
- **Unchecked Exceptions**: Runtime exceptions (e.g., `ArithmeticException`, `NullPointerException`) can be thrown, but if they are uncaught, they will bubble up to the JVM's thread group exception handler, print a stack trace, and immediately terminate that specific thread.

```java
class DivisionJob implements Runnable {
    @Override
    public void run() {
        try {
            // ArithmeticException: division by zero
            int result = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException caught and handled inside Runnable");
        }
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        Thread t = new Thread(new DivisionJob());
        t.start();
    }
}
```

### Output
ArithmeticException caught and handled inside Runnable

### Explanation

- The potential division-by-zero error is wrapped inside a `try-catch` block inside `run()`.
- The exception is handled gracefully, preventing the JVM from terminating the thread abruptly.

## Runnable Interface vs Thread Class

The following table highlights the differences between using `Runnable` and extending `Thread`:

| Feature | Runnable Interface | Thread Class |
| --- | --- | --- |
| **Type** | An interface representing a task. | A class representing an execution thread. |
| **Inheritance** | Class can implement multiple interfaces and extend one class. | Class cannot extend any other class. |
| **Separation of Concerns** | Excellent. Task logic and thread execution are decoupled. | Poor. Task logic and thread lifecycle are tightly coupled. |
| **Resource Reuse** | High. The same task instance can be submitted to different pools. | Low. A Thread instance represents a one-off execution. |
| **Memory Overhead** | Low. Avoids overhead associated with inheriting class fields. | High. Each task instantiation carries full thread object overhead. |
| **Thread Pooling** | Native support. Designed for use with Executor services. | Not supported. Thread pools require `Runnable` or `Callable`. |

# Summary

The Java `Runnable` interface is a functional interface used to define a concurrent task's execution logic separately from the thread lifecycle mechanism. Because it is an interface, it preserves single inheritance boundaries, promotes modular separation of concerns, and integrates with the Executor framework and thread pools. While checked exceptions must be handled locally within the `run()` method due to its signature constraints, implementing `Runnable` (or utilizing equivalent lambda expressions) remains the standard best practice for building flexible, robust, and memory-efficient multithreaded applications in Java.




