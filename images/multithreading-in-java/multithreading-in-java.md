# Multithreading in Java

## Introduction

**Multithreading** in Java is a feature that enables a program to run multiple threads simultaneously, allowing tasks to execute in parallel and utilize the CPU more efficiently. A thread is a lightweight, independent unit of execution inside a program (process).

Key concepts of multithreading include:

- **Parallel Task Execution**: Spawns multiple concurrent threads to process operations simultaneously.
- **Process vs Thread**: A process can contain multiple threads.
- **Shared Memory Space**: Threads share the same process memory space and resources, but execute independently with their own call stack.

## Real-World Analogy

Imagine a car manufacturing assembly line. Multiple robotic arms (threads) are assembling different car parts (preparing different items) at the same time. This speeds up assembly and utilizes all available workshop resources (CPU cores) efficiently compared to a single arm working sequentially.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/multithreading-in-java/1782029330961-a5292c5a-a897-47a8-b90f-35b3b93fc4fb.png)

## Different Ways to Create Threads

In Java, threads can be created using two primary mechanisms:

### 1. Extending the Thread Class

We create a custom class that extends `java.lang.Thread` and override its `run()` method to define the task. Then, we instantiate this class and call `start()`, which automatically triggers the `run()` method and begins concurrent execution.

```java
class AssemblyTask extends Thread {
    private String task;

    AssemblyTask(String task) {
        this.task = task;
    }

    public void run() {
        System.out.println(task + " is being prepared by " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        Thread t1 = new AssemblyTask("Tesla");
        Thread t2 = new AssemblyTask("BMW");
        Thread t3 = new AssemblyTask("mohit");
        Thread t4 = new AssemblyTask("AlphaKnowledge");

        t1.start();
        t2.start();
        t3.start();
        t4.start();
    }
}
```

### Output
AlphaKnowledge is being prepared by Thread-3
Tesla is being prepared by Thread-0
mohit is being prepared by Thread-2
BMW is being prepared by Thread-1

### Explanation

- The `AssemblyTask` class extends `Thread` and defines a custom task inside `run()`.
- Four threads (`t1` to `t4`) are created and initiated using `start()`.
- Calling `start()` creates a new thread with its own call stack and invokes `run()` concurrently. The execution order is non-deterministic because thread scheduling is managed by the OS.

### 2. Implementing the Runnable Interface

We create a class that implements the `java.lang.Runnable` interface, defining the execution logic inside `run()`. We then instantiate a `Thread` object, passing the `Runnable` instance to the thread constructor, and call `start()`.

```java
class AssemblyJob implements Runnable {
    private String task;

    AssemblyJob(String task) {
        this.task = task;
    }

    public void run() {
        System.out.println(task + " is being processed by " + Thread.currentThread().getName());
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        Thread t1 = new Thread(new AssemblyJob("Tesla"));
        Thread t2 = new Thread(new AssemblyJob("BMW"));
        Thread t3 = new Thread(new AssemblyJob("AlphaKnowledge"));

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### Output
AlphaKnowledge is being processed by Thread-2
BMW is being processed by Thread-1
Tesla is being processed by Thread-0

### Explanation

- `AssemblyJob` implements `Runnable` and overrides `run()`.
- The `Runnable` objects are passed to `Thread` constructors, separating task definition from execution structure.
- Calling `start()` schedules the threads for execution, which run concurrently with the main thread.

## Best Use Cases for Thread and Runnable

- **Extending Thread**: Use this approach if your class does not need to extend any other class.
- **Implementing Runnable**: Preferred because Java does not support multiple inheritance. Implementing `Runnable` leaves the class free to extend another class, promotes loose coupling, and separates the task definition from the thread-running mechanism.

## Advantages of Multithreading in Java

- **Improved Performance**: Concurrently executes tasks to reduce the overall program execution time.
- **Efficient CPU Utilization**: Keeps cores busy by executing operations in parallel.
- **Responsiveness**: Ensures background tasks (e.g., file downloads or calculations) do not freeze the main application thread.
- **Resource Sharing**: Threads share the same process memory and resources, avoiding the overhead of creating separate processes.
- **Better User Experience**: Enables smooth animations, calculations, and real-time UI updates.

# Summary

Java Multithreading enables concurrent execution of multiple lightweight threads within a single process to maximize CPU utilization and improve application responsiveness. By utilizing either Thread class extension or Runnable interface implementation to define run methods, developers can spawn threads that share memory space while executing independently. While thread scheduling remains non-deterministic and requires synchronization handling under shared mutable states, multithreading remains essential for building high-performance, responsive, and resource-efficient Java programs.




