# Preemptive and Non-Preemptive Scheduling

CPU Scheduling is the process by which the operating system selects a process from the **Ready Queue** and allocates the CPU for execution. Since multiple processes may be waiting for CPU time, scheduling ensures efficient processor utilization, reduced waiting time, improved response time, and smooth multitasking.

CPU scheduling is mainly classified into **Preemptive Scheduling** and **Non-Preemptive Scheduling**.

## Preemptive Scheduling

**Preemptive Scheduling** is a CPU scheduling method in which the operating system can interrupt a running process and allocate the CPU to another process before the current process completes its execution.

This interruption usually occurs when:

- A higher-priority process arrives.
- The allocated time quantum expires.
- The scheduler decides another process should execute.

The interrupted process is moved from the **Running** state back to the **Ready** state, where it waits for another chance to execute.

### Key Characteristics

- The operating system controls CPU allocation.
- Running processes can be interrupted at any time.
- Provides better responsiveness for interactive systems.
- Supports multitasking efficiently.
- Requires frequent context switching.

### Common Preemptive Scheduling Algorithms

- Round Robin (RR)
- Shortest Remaining Time First (SRTF)
- Preemptive Priority Scheduling
- Multilevel Feedback Queue (MLFQ)

### Advantages

- Prevents a single process from occupying the CPU for a long time.
- Provides faster response time for users.
- Improves CPU utilization.
- Suitable for multitasking and time-sharing operating systems.
- Used by modern operating systems such as Windows, Linux, and macOS.

### Disadvantages

- More complex to implement.
- Frequent context switching increases overhead.
- Low-priority processes may experience starvation.
- Requires careful synchronization when processes share resources.

## Non-Preemptive Scheduling

**Non-Preemptive Scheduling** is a CPU scheduling method in which, once a process gets the CPU, it continues execution until it:

- Completes its execution, or
- Moves to the Waiting state (for example, waiting for I/O).

The operating system cannot forcibly interrupt the running process.

### Key Characteristics

- CPU remains with the running process until completion or waiting.
- Very simple scheduling mechanism.
- Fewer context switches.
- Lower scheduling overhead.

### Common Non-Preemptive Scheduling Algorithms

- First Come First Serve (FCFS)
- Shortest Job First (SJF)
- Non-Preemptive Priority Scheduling

### Advantages

- Easy to design and implement.
- Minimal scheduling overhead.
- Fewer context switches improve efficiency.
- Suitable for simple batch processing systems.

### Disadvantages

- Long processes can delay shorter processes.
- Higher average response time.
- Interactive applications may become less responsive.
- CPU may remain idle while waiting for a blocked process in certain scheduling scenarios.

## Difference Between Preemptive and Non-Preemptive Scheduling

| Feature | Preemptive Scheduling | Non-Preemptive Scheduling |
| --- | --- | --- |
| CPU Allocation | CPU is allocated for a limited time or until interruption | CPU remains with the process until completion or waiting state |
| Process Interruption | Running process can be interrupted | Running process cannot be interrupted |
| CPU Control | Operating System controls CPU allocation | Process keeps CPU until it voluntarily releases it |
| Context Switching | Frequent | Very less |
| Scheduling Overhead | High | Low |
| Response Time | Lower (better) | Higher |
| CPU Utilization | Better for multitasking systems | Good for simple systems |
| Starvation | Low-priority processes may starve | Long jobs may delay short jobs |
| Complexity | More complex | Simple |
| Suitable For | Interactive, real-time and time-sharing systems | Batch processing systems |
| Examples | Round Robin, SRTF, Preemptive Priority | FCFS, SJF, Non-Preemptive Priority |

## When to Use Preemptive Scheduling

Preemptive Scheduling is preferred when:

- Fast response is required.
- Multiple users share the system.
- Interactive applications are running.
- Real-time performance is important.
- Fair CPU sharing is needed.

## When to Use Non-Preemptive Scheduling

Non-Preemptive Scheduling is preferred when:

- Simplicity is important.
- Batch jobs are executed.
- Context switching should be minimized.
- The workload is predictable.
- System resources are limited.

## Summary

CPU scheduling is broadly divided into **Preemptive Scheduling** and **Non-Preemptive Scheduling**. In **Preemptive Scheduling**, the operating system can interrupt a running process and assign the CPU to another process, making it suitable for multitasking, interactive, and modern operating systems due to its faster response time. In **Non-Preemptive Scheduling**, once a process starts executing, it keeps the CPU until it completes or enters the waiting state, making it simple to implement with minimal scheduling overhead but generally resulting in higher response times. Choosing the appropriate scheduling method depends on system requirements, workload characteristics, and performance objectives.




