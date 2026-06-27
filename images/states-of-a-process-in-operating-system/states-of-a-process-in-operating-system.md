# States of a Process in Operating System

A **process** moves through several states during its lifetime, from the moment it is created until it finishes execution. These states describe the current condition of the process and help the operating system manage CPU time, memory, and other system resources efficiently.

As a process executes, it may wait for resources, get scheduled by the CPU, perform computations, or terminate after completing its task. This complete journey is known as the **Process Life Cycle**.

## Types of Process State Models

Operating systems use different models to represent process states. The most common models are:

- Two-State Model
- Five-State Model
- Seven-State Model

## 1. Two-State Model

The **Two-State Model** is the simplest representation of process execution. It divides the entire process lifecycle into only two states based on whether the process is currently using the CPU.

### States in the Two-State Model

### Running

The process is currently executing instructions on the CPU.

### Not Running

The process is not using the CPU. It may be waiting for CPU time, waiting for resources, or temporarily paused.

### Working of the Two-State Model

- A newly created process first enters the **Not Running** state.
- The **Dispatcher** checks whether the CPU is available.
- If the CPU is free, the dispatcher loads the process onto the CPU.
- The process then moves to the **Running** state.
- The **CPU Scheduler** decides which process should execute next according to the scheduling algorithm used by the operating system.

## 2. Five-State Model

The **Five-State Model** provides a more realistic representation of process execution by separating processes that are waiting for CPU time from those waiting for external events such as I/O operations.

### Process States

### New

The process has just been created.

- The operating system creates its **Process Control Block (PCB)**.
- Required resources are allocated.
- The process has not yet started execution.

### Ready

The process is loaded into main memory and is ready to execute.

It waits in the **Ready Queue** until the CPU becomes available.

### Running

The CPU is currently executing the process.

In a single-processor system, only **one process** can remain in the Running state at a time.

### Blocked (Waiting)

The process cannot continue execution because it is waiting for an external event.

Examples include:

- Completion of an I/O operation
- User input
- Availability of a required resource

After the event completes, the process moves back to the Ready state.

### Exit (Terminated)

The process has completed its execution or has been terminated.

The operating system releases all allocated resources and removes its PCB from the process table.

## 3. Seven-State Model

The **Seven-State Model** extends the Five-State Model by introducing suspended states for better memory management. It is commonly used in systems that support swapping.

### Process States

### New

The process is being created.

Its program exists in secondary storage, and the operating system prepares its PCB before loading it into main memory.

### Ready

The process is loaded into main memory and waits for CPU allocation.

### Running

The CPU executes the instructions of the process.

### Blocked (Waiting)

The process waits for an external event such as:

- I/O completion
- User input
- Availability of shared resources

Once the event is completed, it returns to the Ready state.

### Terminated

The process has completed execution or has been stopped.

The operating system releases all resources associated with it.

### Suspend Ready

A ready process is temporarily moved from main memory to secondary storage due to insufficient memory.

When memory becomes available, it is brought back to the Ready state.

### CPU-Bound / I/O-Bound

Some operating systems also classify processes based on resource usage.

- **CPU-Bound Process:** Performs more computations and spends most of its time using the CPU.
- **I/O-Bound Process:** Performs frequent input/output operations and spends most of its time waiting for I/O completion.

## Process State Transitions

A process changes its state depending on system events and resource availability.

### New → Ready

The operating system creates the process, allocates required resources, and places it into the Ready Queue.

### Ready → Running

The CPU scheduler selects the process and assigns the CPU for execution.

### Running → Blocked (Waiting)

The process requests an I/O operation or waits for a resource, causing it to enter the Waiting state.

### Blocked → Ready

The required event finishes or the needed resource becomes available.

The process is then moved back to the Ready Queue.

### Running → Ready

The operating system temporarily removes the process from the CPU.

This usually happens because:

- The time slice expires.
- A higher-priority process becomes ready.
- The scheduler decides to preempt the running process.

### Running → Terminated

The process successfully completes execution or is terminated by the operating system.

### Blocked → Terminated

A waiting process may also be terminated before completing execution due to user intervention or system requirements.

### General Rule

A process may repeatedly move between the **Ready**, **Running**, and **Blocked** states during execution.

However:

- **New** occurs only once.
- **Terminated** occurs only once.

## Schedulers

Schedulers are operating system components responsible for deciding which process should execute and when.

### Long-Term Scheduler

The **Long-Term Scheduler** decides which newly created processes should enter the Ready Queue.

It also controls the **degree of multiprogramming** by limiting the number of processes in memory.

### Short-Term Scheduler

The **Short-Term Scheduler** selects the next process from the Ready Queue and assigns it to the CPU.

It runs very frequently because CPU scheduling occurs continuously.

### Medium-Term Scheduler

The **Medium-Term Scheduler** manages swapping.

It temporarily moves processes between main memory and secondary storage to improve memory utilization.

## Preemption

When multiple processes are ready for execution, the operating system uses one of two scheduling approaches.

### Preemptive Scheduling

In **Preemptive Scheduling**, the operating system can interrupt a running process and allocate the CPU to another process.

This approach is commonly used in modern multitasking operating systems.

### Non-Preemptive Scheduling

In **Non-Preemptive Scheduling**, once a process receives the CPU, it continues executing until it finishes or voluntarily releases the CPU.

The operating system cannot forcibly remove it during execution.

### Degree of Multiprogramming

The **degree of multiprogramming** refers to the maximum number of processes that can remain in the Ready state at a given time.

For example, if the degree of multiprogramming is **100**, then at most **100 processes** can stay in the Ready Queue simultaneously.

## Operations on a Process

During its lifetime, a process undergoes several important operations.

### Process Creation

A new process is created, assigned resources, and placed in the Ready Queue.

### Scheduling

The operating system selects one process from the Ready Queue for execution.

### Execution

The selected process begins executing on the CPU.

If it requires an external resource, it enters the Waiting state.

### Blocking

Whenever a process waits for I/O or another event, it moves into the Blocked state until the required event is completed.

### Context Switching

When the operating system changes the CPU from one process to another, it saves the current process's state and restores the state of the next process.

This operation is called **Context Switching**.

### Inter-Process Communication (IPC)

Processes often need to exchange data or coordinate with each other.

The operating system supports communication using mechanisms such as:

- Shared Memory
- Message Passing
- Synchronization techniques

### Termination

Once the process completes its work, the operating system terminates it, releases all allocated resources, and removes its PCB from the Process Table.

## Summary

A process passes through several states during its lifetime, including **New, Ready, Running, Blocked, Suspended, and Terminated** depending on the process model used by the operating system. State transitions are controlled by schedulers, the dispatcher, and system events such as I/O completion or CPU allocation. Concepts such as context switching, preemption, process scheduling, synchronization, and inter-process communication work together to ensure efficient CPU utilization, smooth multitasking, proper resource sharing, and reliable execution of multiple processes within the operating system.




