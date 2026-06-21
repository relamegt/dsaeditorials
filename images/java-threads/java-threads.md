# Java Threads

## Introduction

A Java thread is the smallest unit of execution within a program. It is a lightweight subprocess that runs independently but shares the same memory space as the process, allowing multiple tasks to execute concurrently.

## Create Threads in Java

We can create threads in java using two ways:

- Extending Thread Class
- Implementing a Runnable interface

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-threads/1782029805294-44fa1e0b-b3cf-4131-95cd-8d387ee7166c.png)

### 1. By Extending Thread Class

Create a class that extends Thread. Override the run() method, this is where you put the code that the thread should execute. Then create an object of your class and call the start() method. This will internally call run() in a new thread.

```java
import java.io.*;
import java.util.*;

class MyThread extends Thread {
    public void run() {
        String str = "Thread Started Running on AlphaKnowledge...";
        System.out.println(str);
    }
}

public class AlphaKnowledge {
    public static void main(String args[]) {
        MyThread t1 = new MyThread();
        t1.start();
    }
}
```

### Output
Thread Started Running on AlphaKnowledge...

### 2. Using Runnable Interface

Create a class that implements Runnable. Override the run() method, this contains the code for the thread. Then create a Thread object, pass your Runnable object to it and call start().

```java
import java.io.*;
import java.util.*;

class MyRunnable implements Runnable {
    public void run() {
        String str = "Thread is Running Successfully";
        System.out.println(str);
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        MyRunnable g1 = new MyRunnable();
        Thread t1 = new Thread(g1);
        t1.start();
    }
}
```

### Output
Thread is Running Successfully

Note: Extend Thread when you don’t need to extend any other class. Implement Runnable when your class already extends another class (preferred in most cases).

## Life Cycle of a Thread

During its thread life cycle, a Java thread transitions through several states from creation to termination.

- **New State**: Thread is created but start() has not been called.
- **Runnable State**: Thread is ready to run and waiting for CPU allocation.
- **Blocked State**: Thread is waiting for a monitor lock.
- **Waiting State**: Thread is waiting indefinitely for another thread to perform a specific action.
- **Timed Waiting State**: Thread is waiting for a specified waiting time.
- **Terminated State**: Thread has completed execution or aborted.

## Running Threads in Java

There are two methods used for running Threads in Java:

- **run() Method**: Contains the code for the thread. Calling it directly behaves like a normal method call.
- **start() Method**: Launches a new thread and internally calls run() concurrently.

### Example: Using Thread Class and Runnable Interface

```java
class ThreadImpl extends Thread {
    @Override
    public void run() {
        System.out.println("Thread Class Running");
    }
}

class RunnableThread implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable Thread Running");
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        ThreadImpl t1 = new ThreadImpl();
        t1.start();

        RunnableThread r = new RunnableThread();
        Thread t2 = new Thread(r);
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### Output
Thread Class Running
Runnable Thread Running

Note: We use start() to launch a new thread, which then calls the run() method in parallel. If we call run() directly, it works like a normal method call and no new thread is created.

## Java Thread Class

The Thread class is used to create and control threads in Java. Each object of this class represents a single thread of execution.

### Syntax

```java
public class Thread extends Object implements Runnable
```

## Advantages of Threads

- **Improved performance**: Multiple threads can execute tasks concurrently.
- **Better resource utilization**: Threads share the same memory and resources.
- **Responsive applications**: UI applications remain responsive while performing background tasks.

# Summary

A Java thread is the smallest execution unit within a program, representing a lightweight subprocess that runs concurrently with other threads while sharing the process memory space. Threads can be created by either extending the Thread class or implementing the Runnable interface, and they are managed by calling the start() method which spawns a separate stack and triggers the run() method. Over its life cycle, a thread moves through New, Runnable, Blocked, Waiting, Timed Waiting, and Terminated states. Using threads improves application performance, enhances resource utilization, and keeps user interfaces responsive by processing intensive operations in the background.




