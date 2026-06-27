# Dispatcher vs Scheduler in Operating System

In a multitasking operating system, multiple processes compete for CPU time. To manage these processes efficiently, the operating system uses two important components: the **Scheduler** and the **Dispatcher**.

The **Scheduler** decides **which process should execute next**, while the **Dispatcher** gives **CPU control to the selected process**. Both work together to ensure efficient CPU utilization, smooth multitasking, and proper process management.

## Scheduler

A **Scheduler** is an operating system component responsible for selecting the next process that should use the CPU. It manages process execution by maintaining different process queues and deciding the order in which processes are executed.

The scheduler improves overall system performance by ensuring that CPU time is shared fairly among processes.

### Functions of Scheduler

- Selects the next process for execution.
- Manages process queues.
- Allocates CPU time efficiently.
- Improves CPU utilization.
- Reduces waiting and response time.
- Maintains fairness among processes.

## Types of Scheduler

### 1. Long-Term Scheduler (Job Scheduler)

The Long-Term Scheduler controls the admission of new processes into the system.

- Moves processes from secondary storage to main memory.
- Controls the degree of multiprogramming.
- Maintains a balanced mix of CPU-bound and I/O-bound processes.
- Executes less frequently than other schedulers.

### 2. Medium-Term Scheduler

The Medium-Term Scheduler manages process swapping.

- Temporarily removes processes from main memory.
- Frees memory when the system is overloaded.
- Brings suspended processes back into memory when required.
- Helps improve memory utilization.

### 3. Short-Term Scheduler (CPU Scheduler)

The Short-Term Scheduler selects one process from the ready queue for CPU execution.

- Chooses the next process to run.
- Executes very frequently.
- Uses CPU scheduling algorithms.
- Invokes the Dispatcher after selecting a process.

### Scheduling Algorithms Used

The scheduler may use different CPU scheduling algorithms, such as:

- First Come First Serve (FCFS)
- Shortest Job First (SJF)
- Shortest Remaining Time First (SRTF)
- Round Robin (RR)
- Priority Scheduling
- Multilevel Queue Scheduling
- Multilevel Feedback Queue Scheduling

## Dispatcher

The **Dispatcher** is a small operating system module that transfers CPU control to the process selected by the **Short-Term Scheduler**.

Unlike the scheduler, the dispatcher does not decide which process should execute. Its responsibility is to start execution of the selected process as quickly as possible.

### Functions of Dispatcher

- Performs context switching.
- Switches CPU from kernel mode to user mode.
- Loads CPU registers of the selected process.
- Transfers CPU control to the selected process.
- Starts execution from the correct instruction.

### Dispatcher Latency

**Dispatcher Latency** is the time required by the dispatcher to stop one process and start another process.

A lower dispatcher latency results in better overall system performance.

## Working of Scheduler and Dispatcher

The scheduler and dispatcher work together in the following sequence:

1. Multiple processes enter the Ready Queue.
2. The Short-Term Scheduler selects the most suitable process.
3. The Dispatcher performs context switching.
4. CPU registers are loaded for the selected process.
5. Control is transferred to the selected process.
6. The process begins execution on the CPU.

## Difference Between Scheduler and Dispatcher

| Scheduler | Dispatcher |
| --- | --- |
| Decides which process should execute next. | Gives CPU control to the selected process. |
| Responsible for process selection. | Responsible for process execution. |
| Uses scheduling algorithms. | Does not use scheduling algorithms. |
| Types: Long-Term, Medium-Term, and Short-Term. | No types; it is a single operating system module. |
| Works independently to select processes. | Depends on the scheduler's decision. |
| Manages process queues. | Performs context switching. |
| Determines execution order. | Starts execution of the selected process. |
| Works with Ready Queue and scheduling policies. | Works directly with the CPU and selected process. |
| Decision-making takes relatively more time. | Executes very quickly. |
| Focuses on efficient CPU allocation. | Focuses on fast CPU transfer between processes. |

## Scheduler vs Dispatcher at a Glance

| Feature | Scheduler | Dispatcher |
| --- | --- | --- |
| Main Purpose | Selects the next process | Executes the selected process |
| Uses Algorithms | Yes | No |
| Performs Context Switching | No | Yes |
| CPU Allocation | Indirect | Direct |
| Decision Making | Yes | No |
| Frequency | Depends on scheduling events | Every process switch |
| Speed | Comparatively slower | Very fast |

## Summary

The **Scheduler** and **Dispatcher** are two essential components of process management in an operating system. The scheduler decides **which process should execute next** by using various scheduling algorithms and managing process queues, while the dispatcher **transfers CPU control** to the selected process by performing context switching, mode switching, and register loading. In simple terms, the scheduler makes the decision, and the dispatcher executes that decision. Together, they ensure efficient CPU utilization, smooth multitasking, and effective process execution.




