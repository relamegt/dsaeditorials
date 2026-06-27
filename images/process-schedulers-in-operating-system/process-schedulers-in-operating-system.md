# Process Schedulers in Operating System

**Process Scheduling** is the activity performed by the operating system to decide which process should use the CPU at a particular time. When the currently running process finishes, waits for an event, or is interrupted, the scheduler selects another process for execution based on a scheduling algorithm.

Throughout its lifetime, a process moves through different scheduling queues such as the **Job Queue**, **Ready Queue**, and **Waiting (Device) Queue**. Process schedulers manage these queues to ensure efficient CPU utilization and smooth execution of multiple processes.

## Why Process Scheduling is Important

Process scheduling is essential in **multiprogramming** and **multitasking** operating systems because multiple processes may be ready to execute simultaneously.

Some important reasons for process scheduling are:

- Ensures efficient CPU utilization.
- Decides which process should execute next.
- Allows multiple processes to share the CPU fairly.
- Improves overall system performance.
- Reduces CPU idle time and increases throughput.

## Process Schedulers

A **Process Scheduler** is an operating system component responsible for selecting processes for execution and allocating CPU time efficiently.

There are three main types of process schedulers:

- Long-Term Scheduler (Job Scheduler)
- Short-Term Scheduler (CPU Scheduler)
- Medium-Term Scheduler

## 1. Long-Term Scheduler (Job Scheduler)

The **Long-Term Scheduler** is responsible for selecting processes from secondary storage (disk) and loading them into the main memory so they can begin execution.

### Functions of Long-Term Scheduler

- Transfers processes from the **Job Queue** to the **Ready Queue**.
- Controls the **degree of multiprogramming**, which is the number of processes present in memory.
- Selects a balanced combination of **CPU-bound** and **I/O-bound** processes.
- Prevents situations where either the CPU or I/O devices remain idle.
- Helps maintain efficient system performance.

### Characteristics

- Operates less frequently than other schedulers.
- It is the **slowest scheduler** because new process admission does not happen very often.
- In many modern operating systems (such as Windows), the long-term scheduler is either minimal or absent, as processes are admitted directly into memory.

## 2. Short-Term Scheduler (CPU Scheduler)

The **Short-Term Scheduler** is responsible for selecting one process from the **Ready Queue** and assigning the CPU to it.

Since CPU allocation happens continuously, this scheduler works very frequently.

### Functions of Short-Term Scheduler

- Selects the next ready process for execution.
- Allocates CPU time fairly among processes.
- Uses CPU scheduling algorithms to determine execution order.
- Maximizes CPU utilization by minimizing idle time.
- Invokes the **Dispatcher** to perform the actual CPU allocation.

### Characteristics

- Executes very frequently, often every few milliseconds.
- It is the **fastest scheduler** in the operating system.
- Directly affects system responsiveness and performance.

## Dispatcher

The **Dispatcher** is a special operating system component that transfers CPU control to the process selected by the Short-Term Scheduler.

It performs the actual switching between processes.

### Functions of Dispatcher

### Context Switching

Saves the execution state of the currently running process and restores the saved state of the selected process.

### Mode Switching

Changes the CPU from **Kernel Mode** to **User Mode** before the selected process begins execution.

### Program Control Transfer

Transfers CPU control to the correct instruction of the selected process so execution resumes from the appropriate point.

### Dispatcher Example

Suppose four processes are waiting:

**P1 → P2 → P3 → P4**

The execution sequence is:

1. The scheduler selects **P1**.
2. The dispatcher loads **P1** onto the CPU.
3. After P1 finishes or is interrupted, the scheduler selects **P2**.
4. The dispatcher assigns the CPU to **P2**.
5. The same process continues for **P3** and **P4**.

### Dispatch Latency

**Dispatch Latency** is the time required by the dispatcher to stop one process and start another.

Lower dispatch latency results in better system performance.

## 3. Medium-Term Scheduler

The **Medium-Term Scheduler** manages **swapping**, where processes are temporarily moved between main memory and secondary storage.

Its primary objective is to improve memory utilization.

### Functions of Medium-Term Scheduler

- Swaps blocked or inactive processes from memory to disk.
- Frees memory for other active processes.
- Swaps suspended processes back into memory when they are ready for execution.
- Maintains an efficient balance between CPU-bound and I/O-bound processes.
- Helps control the degree of multiprogramming during execution.

### Characteristics

- Faster than the Long-Term Scheduler.
- Slower than the Short-Term Scheduler.
- Mainly responsible for memory management through swapping.

## Other Types of Schedulers

Besides CPU schedulers, operating systems also use specialized schedulers for handling specific tasks.

### I/O Scheduler

The **I/O Scheduler** manages the order in which input/output requests are executed.

### Functions

- Organizes disk read and write requests.
- Reduces I/O waiting time.
- Improves storage device performance.

### Common Algorithms

- FCFS (First Come First Serve)
- Round Robin (RR)
- SCAN
- C-SCAN

### Real-Time Scheduler

A **Real-Time Scheduler** is used in systems where tasks must complete within strict deadlines.

### Functions

- Schedules time-critical tasks.
- Ensures deadline-based execution.
- Provides predictable system behavior.

### Common Algorithms

- EDF (Earliest Deadline First)
- RM (Rate Monotonic Scheduling)

## Comparison of Process Schedulers

| Feature | Long-Term Scheduler | Short-Term Scheduler | Medium-Term Scheduler |
| --- | --- | --- | --- |
| **Also Called** | Job Scheduler | CPU Scheduler | Process Swapping Scheduler |
| **Speed** | Slowest | Fastest | Medium |
| **Main Function** | Loads processes from disk into memory | Selects a ready process for CPU execution | Swaps processes between memory and disk |
| **Degree of Multiprogramming** | Controls the degree of multiprogramming | Has little control over multiprogramming | Reduces the degree of multiprogramming through swapping |
| **Frequency of Execution** | Rare | Very Frequent | Occasional |
| **Availability in Time-Sharing Systems** | Rarely used or may be absent | Essential | Usually available |

## Summary

Process schedulers are essential components of an operating system that manage CPU allocation among multiple processes. The **Long-Term Scheduler** admits new processes into memory, the **Short-Term Scheduler** selects processes for CPU execution, and the **Medium-Term Scheduler** manages swapping to optimize memory usage. The **Dispatcher** performs context switching and transfers CPU control to the selected process. In addition, operating systems use specialized schedulers such as **I/O Schedulers** and **Real-Time Schedulers** to efficiently manage storage operations and time-critical tasks. Together, these schedulers ensure fair CPU allocation, efficient resource utilization, improved multitasking, and better overall system performance.




