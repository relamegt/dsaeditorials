# Synchronization in Java

## Introduction

In multithreaded applications, multiple threads run concurrently and share access to common objects, files, and system resources. If multiple threads attempt to read and write to the same shared mutable state simultaneously, it can lead to data inconsistency, corrupt records, and non-deterministic results known as **Race Conditions**. To prevent these anomalies, Java provides the concept of **Synchronization**, which coordinates and controls thread access to critical sections, ensuring mutual exclusion.

Key benefits of synchronization include:

- **Resource Control**: Regulates access to shared variables and objects, allowing only one thread to interact with them at a time.
- **Data Consistency**: Ensures updates made by one thread are fully completed and written to memory before another thread reads them.
- **Orderly Execution**: Coordinates the execution sequence of threads to avoid race conditions.

## Ways to Achieve Synchronization

Java provides three primary mechanisms to synchronize concurrent execution:

### 1. Synchronized Methods

A synchronized method locks the entire method scope using the target object's intrinsic lock (also known as a monitor lock). When a thread calls a synchronized instance method, it automatically acquires the lock for that instance. Other threads attempting to execute any synchronized method on that same instance are blocked until the lock is released.

```java
class Counter {
    private int count = 0; 

    // Synchronized method locks 'this' object instance
    public synchronized void increment() {
        count++; 
    }

    public synchronized int getCount() {
        return count; 
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        System.out.println("Processing counter increments on AlphaKnowledge...");
        Counter cnt = new Counter(); 

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                cnt.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                cnt.increment();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Counter final value: " + cnt.getCount());
    }
}
```

### Output
Processing counter increments on AlphaKnowledge...
Counter final value: 2000

### Explanation

- Two concurrent threads (`t1` and `t2`) attempt to increment the same `Counter` instance.
- Because `increment()` is synchronized, only one thread can acquire the lock for `cnt` and execute the body at a time. This guarantees that `count++` (which is a read-modify-write operation) is atomic, resulting in a correct final count of `2000`.

### 2. Synchronized Blocks

Synchronized blocks allow you to lock only a specific critical section of code within a method rather than the entire method scope. This improves performance by reducing the lock's scope, allowing other threads to execute non-critical code concurrently.

```java
class BlockCounter {
    private int count = 0;

    public void increment() {
        // Only lock the critical section using the 'this' instance
        synchronized (this) {
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) throws InterruptedException {
        BlockCounter cnt = new BlockCounter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                cnt.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                cnt.increment();
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Block Counter final value: " + cnt.getCount());
    }
}
```

### Output
Block Counter final value: 2000

### Explanation

- The block `synchronized (this) { count++; }` restricts mutual exclusion strictly to the increment statement.
- Threads can enter the `increment()` method simultaneously, but must wait sequentially to enter the synchronized block, minimizing locking overhead.

### 3. Static Synchronization

If a static method is synchronized, the lock is acquired on the class's `java.lang.Class` object (e.g., `Table.class`) rather than on an object instance. This prevents multiple threads from accessing static synchronized methods concurrently across all class instances.

```java
class Table {
    // Lock is applied to Table.class object
    public synchronized static void printTable(int factor) {
        for (int i = 1; i <= 3; i++) {
            System.out.println(factor * i);
        }
    }
}

class DiagnosticThread1 extends Thread {
    @Override
    public void run() {
        Table.printTable(1);
    }
}

class DiagnosticThread2 extends Thread {
    @Override
    public void run() {
        Table.printTable(10);
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        DiagnosticThread1 t1 = new DiagnosticThread1();
        DiagnosticThread2 t2 = new DiagnosticThread2();
        t1.start();
        t2.start();
    }
}
```

### Output
1
2
3
10
20
30

### Explanation

- Both `t1` and `t2` execute static methods on `Table`.
- Static synchronization acquires the lock at the class-level (`Table.class`).
- Even if they were calling `printTable()` on different instances, the class-level lock ensures they execute sequentially.

## Types of Synchronization

Synchronization is split into two primary paradigms:

### 1. Process Synchronization

Coordinating execution across separate execution contexts or threads that share resources to ensure data integrity and avoid race conditions.

```java
class BankAccount {
    private int balance = 1000;

    public synchronized void deposit(int amount) {
        balance += amount;
        System.out.println("Deposited: " + amount + ", Balance: " + balance);
    }

    public synchronized void withdraw(int amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount + ", Balance: " + balance);
        } else {
            System.out.println("Insufficient balance for withdrawal: " + amount);
        }
    }

    public int getBalance() {
        return balance;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 3; i++) {
                account.deposit(200);
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 3; i++) {
                account.withdraw(100);
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final Balance: " + account.getBalance());
    }
}
```

### Output
Deposited: 200, Balance: 1200
Withdrawn: 100, Balance: 1100
Deposited: 200, Balance: 1300
Deposited: 200, Balance: 1500
Withdrawn: 100, Balance: 1400
Withdrawn: 100, Balance: 1300
Final Balance: 1300

### 2. Thread Synchronization

Coordinating the execution order of threads in a multithreaded program.

- **Mutual Exclusion**: Solved using `synchronized` methods, blocks, and static locks.
- **Cooperation (Inter-thread communication)**: Threads communicate state changes using `wait()`, `notify()`, and `notifyAll()`.

```java
class TicketBooking {
    private int availableTickets = 10; 

    public synchronized void bookTicket(int tickets) {
        if (availableTickets >= tickets) {
            availableTickets -= tickets;
            System.out.println("Booked " + tickets + " tickets, Remaining: " + availableTickets);
        } else {
            System.out.println("Not enough tickets available to book " + tickets);
        }
    }

    public int getAvailableTickets() {
        return availableTickets;
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) {
        TicketBooking booking = new TicketBooking(); 

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 2; i++) {
                booking.bookTicket(2); 
                try {
                    Thread.sleep(50); 
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 2; i++) {
                booking.bookTicket(3); 
                try {
                    Thread.sleep(40);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final Available Tickets: " + booking.getAvailableTickets());
    }
}
```

### Output
Booked 2 tickets, Remaining: 8
Booked 3 tickets, Remaining: 5
Booked 3 tickets, Remaining: 2
Booked 2 tickets, Remaining: 0
Final Available Tickets: 0

## The Volatile Keyword

The `volatile` keyword in Java ensures that updates to a variable are immediately visible across all threads. It prevents threads from caching the variable in local registers, forcing all reads and writes directly to main memory.

### Working of Volatile

- **Visibility Guarantee**: Write operations to a volatile variable are immediately synchronized to main memory and made visible to all threads.
- **No Atomicity**: `volatile` does **not** provide mutual exclusion or lock protection. Read-modify-write operations (like `count++`) are still not atomic and can cause race conditions if executed concurrently.

```java
class StatusMonitor {
    private volatile boolean running = true;

    public void stop() {
        running = false;
    }

    public void start() {
        new Thread(() -> {
            while (running) {
                System.out.println("Service running...");
                try {
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
            System.out.println("Service stopped.");
        }).start();
    }
}

public class AlphaKnowledge {
    public static void main(String[] args) throws InterruptedException {
        StatusMonitor monitor = new StatusMonitor();
        monitor.start();

        Thread.sleep(600); 
        monitor.stop();    
    }
}
```

### Output
Service running...
Service running...
Service running...
Service stopped.

## Volatile vs Synchronized Comparison

| Feature | volatile | synchronized |
| --- | --- | --- |
| **Visibility** | Guarantees immediate visibility across threads. | Guarantees visibility along with mutual exclusion. |
| **Locking** | Lock-free. Does not block execution. | Uses intrinsic monitor locking. Block threads. |
| **Atomicity** | Does not guarantee atomic compound actions. | Guarantees atomic operations in critical sections. |
| **Overhead** | Lightweight and very fast. | Heavyweight due to thread suspension and context switches. |
| **Usage Scope** | Applies only to variables. | Applies to methods, static methods, and code blocks. |
| **Use Cases** | Simple boolean flags, visibility switches. | Counters, transactions, shared database resources. |

# Summary

Java synchronization coordinates the execution of multiple threads accessing shared mutable resources to prevent race conditions and ensure data consistency. Achieved via instance-level synchronized methods and blocks (locking the `this` instance) or class-level static synchronization (locking the `Class` object), it forces mutual exclusion in critical code paths. Additionally, the `volatile` keyword guarantees immediate variable visibility across threads by bypassing local CPU register caching but does not ensure atomic operations, making it a lightweight option suited for simple status flags rather than complex counters.




