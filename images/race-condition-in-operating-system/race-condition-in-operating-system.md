# Race Condition in Operating System

A **Race Condition** is a situation in which two or more processes or threads access and modify the same shared resource simultaneously, causing the final result to depend on the order in which they execute. Since the execution order is unpredictable, the output may become incorrect or inconsistent.

Race conditions are one of the most common synchronization problems in operating systems and occur when shared resources are accessed without proper synchronization.

## Real-Life Example

Consider a **bank account** with a balance of **₹100**.

- Mohit wants to **deposit ₹10**.
- Akash wants to **withdraw ₹10** at the same time.

If both transactions occur simultaneously without proper synchronization, the final account balance may become incorrect because both operations use the same balance value before either update is completed.

## Important Terms

### Shared Resource

A **Shared Resource** is any resource that can be accessed by multiple processes or threads.

Examples include:

- Shared variables
- Memory locations
- Files
- Printers
- I/O devices

### Concurrency

**Concurrency** refers to multiple processes or threads executing simultaneously or overlapping during execution.

Modern operating systems support concurrency to improve CPU utilization and system performance.

### Non-Atomic Operations

A **Non-Atomic Operation** is an operation that can be interrupted before it completes.

A common example is the **Read → Modify → Write** sequence.

Since another process may interrupt this sequence, inconsistent data can be produced.

## Causes of Race Condition

### 1. Simultaneous Access

Two or more processes access the same shared resource at the same time.

### 2. Non-Atomic Updates

Operations such as increment (`++`) or decrement (`--`) are performed in multiple steps rather than as a single indivisible operation.

### 3. Lack of Synchronization

Synchronization mechanisms such as mutexes, semaphores, or monitors are not used to protect shared resources.

### 4. Improper Scheduling

The operating system interrupts a process while it is updating shared data, allowing another process to modify the same resource.

## Example of Race Condition

Assume a shared variable:

```Code
balance = 100
```

Two processes execute simultaneously:

- **Process P1** adds **10** to the balance.
- **Process P2** subtracts **10** from the balance.

### Execution Without Synchronization

1. P1 reads the balance as **100**.
2. P1 calculates **100 + 10 = 110**.
3. Before P1 writes the new value, it is interrupted.
4. P2 reads the balance, which is still **100**.
5. P2 calculates **100 − 10 = 90**.
6. P2 writes **90** into memory.
7. P1 resumes execution.
8. P1 writes **110** into memory.

Final balance becomes:

```Code
110
```

or, depending on execution order,

```Code
90
```

The correct balance should actually be:

```Code
100
```

This incorrect result is called a **Race Condition**.

## Effects of Race Condition

### Data Corruption

Shared data may become incorrect or inconsistent.

### Unpredictable Results

The same program may produce different outputs every time it executes.

### Security Problems

Race conditions can be exploited in banking systems, authentication systems, and file management, leading to security vulnerabilities.

### System Failures

Critical data corruption caused by race conditions may result in application crashes or system instability.

## Prevention Techniques

### 1. Mutex (Mutual Exclusion)

A mutex allows only one process or thread to enter the critical section at a time.

This prevents simultaneous access to shared resources.

### 2. Semaphores

Semaphores control access to shared resources by allowing a limited number of processes to access them simultaneously.

Both binary and counting semaphores are commonly used.

### 3. Monitors

Monitors are high-level synchronization mechanisms that automatically ensure mutual exclusion while accessing shared resources.

### 4. Atomic Operations

Atomic operations execute completely without interruption, preventing other processes from accessing the shared resource during execution.

### 5. Disable Interrupts

In kernel-level programming, interrupts may be temporarily disabled while executing a critical section to prevent context switching.

### 6. Proper Scheduling

The operating system scheduler should avoid interrupting processes while they are executing critical sections, reducing the possibility of race conditions.

## Race Condition vs Critical Section

| Race Condition | Critical Section |
| --- | --- |
| A synchronization problem caused by simultaneous access to shared data. | A section of code where shared resources are accessed. |
| Produces incorrect or inconsistent results. | Must be protected to prevent race conditions. |
| Occurs when synchronization is absent. | Uses synchronization mechanisms like mutexes or semaphores. |
| Undesirable situation. | Normal part of a program that requires controlled access. |

## Summary

A **Race Condition** occurs when multiple processes or threads simultaneously access and modify the same shared resource without proper synchronization, causing unpredictable or incorrect results. It commonly arises due to simultaneous access, non-atomic operations, lack of synchronization, or improper scheduling. Race conditions can lead to data corruption, inconsistent outputs, security vulnerabilities, and system failures. Operating systems prevent race conditions using synchronization techniques such as **Mutexes, Semaphores, Monitors, Atomic Operations, Proper Scheduling,** and **Interrupt Control**, ensuring that shared resources are accessed safely and correctly.




