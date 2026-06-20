# Garbage Collection in Java

## Introduction

In programming languages like C and C++, memory allocation and deallocation are manual tasks. Developers allocate memory on the heap using functions like `malloc()` or operators like `new`, and must explicitly release that memory using `free()` or `delete`. Failing to deallocate memory leads to memory leaks, while double deallocation causes program crashes and security vulnerabilities (dangling pointers).

Java addresses these risks through **Garbage Collection (GC)**. Garbage Collection is an automatic memory management process performed by the Java Virtual Machine (JVM). The JVM automatically detects and removes objects from Heap Memory that are no longer reachable by any active thread in the application. This ensures efficient utilization of memory resources and allows developers to focus entirely on application logic without the burden of manual pointer tracking.

# Features of Java Garbage Collection

- **Automatic Resource Reclamation**: The JVM runs GC as a low-priority background daemon thread, cleaning up unreferenced heap objects automatically.
- **Leak Prevention**: Reclaiming unreferenced objects prevents memory limits from being reached.
- **Compaction**: Most garbage collectors compact memory, moving active objects into adjacent slots to eliminate fragmentation and preserve large contiguous memory blocks.
- **Generational Classification**: Organizes objects by age (Young vs. Old Generation) to run collections quickly.

# Working of Garbage Collection

The lifecycle of an object in Java's memory follows a structured sequence:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/garbage-collection-in-java/1781965044494-dbf2a2bf-a06a-422b-a030-8d9ac403479d.png)

1. **Object Creation**: Objects are instantiated on the Heap (typically in the Eden space of the Young Generation) using the `new` keyword.
2. **Reference Tracking**: The JVM monitors references to each object. As long as an object is reachable via a chain of references starting from a **GC Root** (active local stack variables, static fields, active thread descriptors), it remains in memory.
3. **Unreachability Identification**: When all references to an object are severed or go out of scope, the object becomes **unreachable**.
4. **Memory Reclamation**: During a GC cycle, the JVM identifies these unreachable objects, clears their occupied space, and returns the memory to the free memory pool.
5. **Memory Compaction**: The JVM rearranges surviving objects to ensure that free space remains contiguous, facilitating future allocations.

# Types of Garbage Collection in Java

To minimize pause times, the JVM Heap is divided into regions. Garbage Collection is classified based on which region is being collected:

## 1. Minor Garbage Collection

Minor GC collects the **Young Generation** (Eden Space and Survivor Spaces S0/S1).

- **Target**: Reclaims short-lived, temporary objects.
- **Frequency**: Runs frequently since most objects die young.
- **Performance**: Extremely fast (usually a few milliseconds) because the space is relatively small.
- **Stop-The-World (STW)**: Briefly pauses application threads, but the pause is barely noticeable.

## 2. Major or Full Garbage Collection

Major GC collects the **Old (Tenured) Generation**.

- **Target**: Reclaims long-lived objects that have been promoted from the Young Generation survivor spaces.
- **Frequency**: Runs much less frequently.
- **Performance**: Slower than Minor GC because the Old Generation is significantly larger.
- **Stop-The-World (STW)**: Causes longer application pauses as the GC traces a larger object graph.

# Key Concepts of Garbage Collection

## Unreachable Objects

An object is considered unreachable if it cannot be accessed through any reference path originating from active GC Roots.

### Example

```java
class Customer {
    String id;
    Customer(String id) { this.id = id; }
}

public class ReachabilityDemo {
    public static void main(String[] args) {
        Customer c1 = new Customer("CUST-101"); // Reachable via stack variable 'c1'
        c1 = null;                              // Unreachable, eligible for Garbage Collection
    }
}
```

## Making Objects Eligible for GC

There are four primary ways to make an object eligible for garbage collection:

### 1. Nullifying the Reference Variable

Disconnecting the reference variable from the object by setting it to `null`.

```java
Account acc = new Account("Acc-5005");
acc = null; // Object at original memory is now eligible for GC
```

### 2. Re-assigning the Reference Variable

Re-assigning the reference variable to point to another object, leaving the first object unreferenced.

```java
Product p1 = new Product("Laptop"); // Object 1
p1 = new Product("Desktop");        // Object 1 is now eligible; p1 points to Object 2
```

### 3. Out-Of-Scope Allocations

Objects created inside a method become eligible for GC once the method finishes execution and its stack frame is popped.

```java
public class ScopeDemo {
    static void loadTempConfig() {
        Config temp = new Config(); // Created inside method stack frame
        temp.readValues();
    } // 'temp' goes out of scope; Config object is eligible for GC here
}
```

### 4. Island of Isolation

This occurs when two or more objects reference each other, but none of them are referenced by any active, reachable references from GC Roots.

```java
class Node {
    Node next;
}

public class IslandDemo {
    public static void main(String[] args) {
        Node first = new Node();  // Node 1
        Node second = new Node(); // Node 2

        // Create references between them
        first.next = second; 
        second.next = first;

        // Disconnect the stack references
        first = null;
        second = null;

        // Node 1 and Node 2 reference each other (forming an island), 
        // but are unreachable from the stack, making both eligible for GC.
    }
}
```

# Requesting Garbage Collection

Because Java's GC is automated, the daemon thread runs at the JVM's discretion. Developers cannot force the GC to execute immediately; they can only **suggest** or request it.

Java provides two APIs to request garbage collection:

1. **`System.gc()`**: A static utility method.
2. **`Runtime.getRuntime().gc()`**: Invokes the GC through the runtime environment descriptor.

```java
System.gc();
// Or
Runtime.getRuntime().gc();
```

> !*WARNING:* Calling `System.gc()` in production is an anti-pattern. It suggests a Full GC, which can freeze application threads (Stop-The-World pause), leading to latency spikes.

# The `finalize()` Method (Deprecated since Java 9)

Historically, the `Object` class provided the `finalize()` method. Before reclaiming an object's memory, the GC would invoke this method to allow the object to release system resources (like file descriptors or database connections).

```java
class Resource {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Cleaning up resource pointers...");
    }
}
```

### Why was `finalize()` Deprecated?

- **Unpredictable Execution**: There is no guarantee when (or if) `finalize()` will run, as the GC runs at its own discretion.
- **Performance Overhead**: Objects with finalizers delay garbage collection because they must be placed on a finalization queue, requiring at least two GC cycles to be cleared.
- **Security Vulnerabilities**: Malicious code can exploit finalizers by keeping objects alive during creation failures (finalizer attacks).
- **Exceptions Ignored**: If `finalize()` throws an exception, the JVM halts the finalization process silently, leaving resources unreleased.

# Modern Alternatives to `finalize()`

## 1. Try-With-Resources (`AutoCloseable`)

For explicit resource management, classes should implement `java.lang.AutoCloseable` and be used inside a try-with-resources block.

```java
class DatabaseConnection implements AutoCloseable {
    public void query() { System.out.println("Querying data..."); }

    @Override
    public void close() {
        System.out.println("Connection closed safely.");
    }
}

public class ResourceDemo {
    public static void main(String[] args) {
        try (DatabaseConnection db = new DatabaseConnection()) {
            db.query();
        } // JVM automatically invokes db.close() here
    }
}
```

## 2. Cleaner API (Introduced in Java 9)

The `java.lang.ref.Cleaner` API provides a safer, thread-separated cleanup mechanism. It runs a cleanup action when an object becomes unreachable, without the performance overhead of finalizers.

# Real-World Scenario: Client Session Tracker

Suppose you are writing a server application that tracks the number of active client sessions. To optimize resources, guest sessions should be closed automatically when they are no longer in use.

### 1. Beginner Approach (Without Garbage Collection Control)

A beginner might write a class with a static counter that increments upon creation, but does not decrement when guest sessions go out of scope.

```java
class ClientSession {
    private int sessionId;
    private String username;
    private static int activeSessions = 0;

    public ClientSession(String username) {
        this.username = username;
        this.sessionId = ++activeSessions;
    }

    public void showSession() {
        System.out.println("Session ID: " + sessionId + " | User: " + username);
    }

    public void showActiveCount() {
        System.out.println("Active Session Count: " + activeSessions);
    }
}

public class UseSession {
    public static void main(String[] args) {
        ClientSession s1 = new ClientSession("User-A");
        ClientSession s2 = new ClientSession("User-B");
        s1.showSession();
        s2.showSession();
        s1.showActiveCount(); // Prints 2

        {
            // Block representing guest session
            ClientSession guest = new ClientSession("Guest-User");
            guest.showSession();
            guest.showActiveCount(); // Prints 3
        }

        // Guest went out of scope, but activeSessions still shows 3
        s1.showActiveCount(); // Output is 3, which is incorrect
    }
}
```

### Output
Session ID: 1 | User: User-A
Session ID: 2 | User: User-B
Active Session Count: 2
Session ID: 3 | User: Guest-User
Active Session Count: 3
Active Session Count: 3

### 2. Modern Approach using Cleaner API

By using Java's `Cleaner` API, we can automatically decrement the active session count when the guest session object becomes unreachable and is garbage collected.

```java
import java.lang.ref.Cleaner;

class ClientSession {
    private int sessionId;
    private String username;
    private static int activeSessions = 0;

    // Create a static cleaner instance
    private static final Cleaner cleaner = Cleaner.create();
    private final Cleaner.Cleanable cleanable;

    // Runnable task must not reference the outer object to avoid memory leaks
    private static class CleanupAction implements Runnable {
        @Override
        public void run() {
            synchronized (ClientSession.class) {
                activeSessions--;
            }
        }
    }

    public ClientSession(String username) {
        this.username = username;
        synchronized (ClientSession.class) {
            this.sessionId = ++activeSessions;
        }
        // Register object and cleanup action with the cleaner
        this.cleanable = cleaner.register(this, new CleanupAction());
    }

    public void showSession() {
        System.out.println("Session ID: " + sessionId + " | User: " + username);
    }

    public void showActiveCount() {
        System.out.println("Active Session Count: " + activeSessions);
    }
}

public class UseSession {
    public static void main(String[] args) {
        ClientSession s1 = new ClientSession("User-A");
        ClientSession s2 = new ClientSession("User-B");
        s1.showSession();
        s2.showSession();
        s1.showActiveCount(); // Prints 2

        {
            // Block representing guest session
            ClientSession guest = new ClientSession("Guest-User");
            guest.showSession();
            guest.showActiveCount(); // Prints 3

            // Dereference guest session to make it eligible for GC
            guest = null;
            System.gc(); // Suggest Garbage Collection
        }

        // Give the Cleaner thread a moment to execute the cleanup action
        try {
            Thread.sleep(50);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }

        // The guest session was garbage collected, and the count is updated
        s1.showActiveCount(); // Prints 2
    }
}
```

### Output
Session ID: 1 | User: User-A
Session ID: 2 | User: User-B
Active Session Count: 2
Session ID: 3 | User: Guest-User
Active Session Count: 3
Active Session Count: 2

# Advantages of Garbage Collection

- **Automated Memory Cleanup**: Eliminates the need to manually free memory, preventing memory leaks, dangling pointers, and double-free errors.
- **Simplified Development**: Developers do not need to write verbose memory management code.
- **Improved Performance**: Generational collection models prioritize young objects, keeping collection pause times short.
- **Compaction**: Reclaims fragmented memory blocks automatically, ensuring contiguous memory allocation for future objects.

# Disadvantages of Garbage Collection

- **Latency Spikes**: Garbage collection cycles (especially Full GC) introduce pauses (Stop-The-World events) that can affect real-time or low-latency systems.
- **CPU & Memory Overhead**: Tracing the reference graph and moving objects in memory requires additional CPU cycles.
- **No Direct Control**: Developers cannot force garbage collection immediately; calling `System.gc()` is only a suggestion to the JVM.

# Summary

Garbage Collection (GC) in Java is an automatic memory management process performed by the JVM. It identifies and reclaims unreachable objects in Heap Memory, ensuring optimal memory utilization and preventing memory leaks. JVM divides the Heap into Young and Old generations to prioritize short-lived objects via Minor GC and long-lived objects via Major GC. While Java historically relied on the now-deprecated `finalize()` method for resource cleanup, modern applications use try-with-resources or the `Cleaner` API. Automatic Garbage Collection simplifies development, ensures memory safety, and enhances Java application reliability.




