# CPU Scheduling in Operating System

**CPU Scheduling** is the process by which the operating system decides which process should be allocated the CPU for execution at a particular time. Since a CPU can execute only one process at a time (in a single-core system), scheduling ensures that all ready processes get CPU time in an efficient and fair manner.

The operating system continuously selects processes from the **Ready Queue** and assigns them to the CPU based on a scheduling algorithm.

## Objectives of CPU Scheduling

The primary objectives of CPU scheduling are:

- Maximize CPU utilization.
- Minimize process waiting time.
- Minimize response time.
- Improve overall system performance.
- Ensure fair allocation of CPU time among processes.

## Importance of CPU Scheduling

In a multiprogramming operating system, multiple processes may be ready for execution at the same time. CPU scheduling ensures that whenever the CPU becomes idle, another process from the ready queue is immediately selected for execution.

Proper CPU scheduling helps to:

- Keep the CPU busy as much as possible.
- Improve system throughput.
- Reduce unnecessary waiting.
- Provide better user experience in interactive systems.

## Terminologies Used in CPU Scheduling

Understanding the following terms is essential before learning scheduling algorithms.

### 1. Arrival Time (AT)

The **Arrival Time** is the time at which a process enters the Ready Queue.

### 2. Completion Time (CT)

The **Completion Time** is the time at which a process finishes its execution completely.

### 3. Burst Time (BT)

The **Burst Time** is the total amount of CPU time required by a process for execution.

### 4. Turnaround Time (TAT)

**Turnaround Time** is the total time taken by a process from its arrival until its completion.

**Formula**

```text
Turnaround Time = Completion Time − Arrival Time
```

It includes:

- Waiting time
- CPU execution time
- I/O waiting time (if applicable)

### 5. Waiting Time (WT)

**Waiting Time** is the total time a process spends waiting in the Ready Queue before getting CPU time.

**Formula**

```text
Waiting Time = Turnaround Time − Burst Time
```

### 6. Response Time (RT)

**Response Time** is the time between the submission of a process and the moment it receives the CPU for the first time.

This metric is especially important in interactive systems where users expect quick responses.

## Important Performance Factors in CPU Scheduling

Different scheduling algorithms are designed with different goals. The choice of an algorithm depends on several performance factors.

### CPU Utilization

CPU utilization indicates how efficiently the processor is being used.

- Ideal utilization is close to **100%**.
- In real systems, it usually ranges between **40% and 90%**, depending on workload.

A good scheduling algorithm keeps the CPU busy most of the time.

### Throughput

**Throughput** is the number of processes completed per unit time.

Higher throughput means more processes are completed within a given period.

### Turnaround Time

This measures the total time required for a process to complete after entering the system.

Lower turnaround time improves overall system efficiency.

### Waiting Time

This is the amount of time a process spends waiting in the Ready Queue.

An efficient scheduling algorithm aims to minimize waiting time.

### Response Time

Response time measures how quickly the system responds after a process is submitted.

It is particularly important in:

- Interactive systems
- Online applications
- Real-time environments

## Types of CPU Scheduling

CPU scheduling methods are broadly classified into two categories.

### 1. Preemptive Scheduling

In **Preemptive Scheduling**, the operating system can interrupt a running process and allocate the CPU to another process.

This usually happens when:

- A higher-priority process arrives.
- The allocated time quantum expires.
- A scheduling event occurs.

**Advantages**

- Better response time.
- Suitable for multitasking systems.
- Prevents a single process from monopolizing the CPU.

**Disadvantages**

- More context switching.
- Higher scheduling overhead.

### 2. Non-Preemptive Scheduling

In **Non-Preemptive Scheduling**, once a process gets the CPU, it continues execution until it either:

- Completes execution, or
- Moves to the Waiting state.

The operating system cannot forcibly interrupt the running process.

**Advantages**

- Simple to implement.
- Fewer context switches.
- Lower overhead.

**Disadvantages**

- Longer waiting time for other processes.
- Poor response for interactive applications.

## CPU Scheduling Algorithms

Several scheduling algorithms are used by operating systems depending on system requirements.

### 1. FCFS (First Come First Serve)

- Executes processes in the order they arrive.
- Simple and easy to implement.
- Suitable for batch systems.
- May suffer from the **Convoy Effect**, where short processes wait behind long ones.

### 2. SJF (Shortest Job First)

- Selects the process with the smallest CPU Burst Time.
- Produces the minimum average waiting time.
- Requires prediction of Burst Time.
- Long processes may suffer from starvation.

### 3. SRTF (Shortest Remaining Time First)

- Preemptive version of SJF.
- Always executes the process with the smallest remaining Burst Time.
- Newly arrived shorter processes can preempt the currently running process.
- Improves response time but may cause starvation.

### 4. Round Robin (RR)

- Each process receives a fixed **Time Quantum**.
- After the quantum expires, the process moves to the end of the Ready Queue if it has not finished.
- Ensures fairness among processes.
- Widely used in time-sharing operating systems.

### 5. Priority Scheduling

- CPU is allocated based on process priority.
- Higher-priority processes execute before lower-priority ones.
- Can be either preemptive or non-preemptive.
- May lead to starvation of low-priority processes.

### 6. HRRN (Highest Response Ratio Next)

- Selects the process with the highest response ratio.
- Balances waiting time and Burst Time.
- Helps reduce starvation compared to SJF.

### 7. Multilevel Queue Scheduling (MLQ)

- Ready Queue is divided into multiple queues.
- Each queue has its own scheduling algorithm.
- Processes remain permanently in their assigned queue.
- Suitable for systems with different categories of processes.

### 8. Multilevel Feedback Queue Scheduling (MLFQ)

- Extension of Multilevel Queue Scheduling.
- Processes can move between different queues.
- Higher priority is given to interactive and short processes.
- One of the most flexible and efficient scheduling algorithms used in modern operating systems.

## Comparison of CPU Scheduling Algorithms

| Algorithm | CPU Allocation | Complexity | Average Waiting Time | Preemptive | Starvation | Performance |
| --- | --- | --- | --- | --- | --- | --- |
| **FCFS** | Arrival order | Simple | High | No | No | Slow |
| **SJF** | Shortest Burst Time | Moderate | Very Low | No | Yes | Minimum average waiting time |
| **SRTF** | Shortest Remaining Time | Moderate | Low | Yes | Yes | Good for short jobs |
| **Round Robin** | Fixed Time Quantum | Moderate | Moderate | Yes | No | Fair CPU sharing |
| **Priority (Preemptive)** | Highest Priority | Moderate | Low | Yes | Yes | Good but may cause starvation |
| **Priority (Non-Preemptive)** | Highest Priority | Simple | Low | No | Yes | Suitable for batch systems |
| **Multilevel Queue (MLQ)** | Queue Priority | High | Low | Usually No | Yes | Good for specialized systems |
| **Multilevel Feedback Queue (MLFQ)** | Dynamic Queue Priority | Very High | Very Low | Yes | No (in most cases) | Excellent overall performance |

## Summary

CPU Scheduling is one of the most important responsibilities of an operating system because it determines which process gets CPU time whenever multiple processes are ready to execute. It improves CPU utilization, reduces waiting and response times, and ensures efficient multitasking. Scheduling algorithms such as **FCFS, SJF, SRTF, Round Robin, Priority Scheduling, HRRN, Multilevel Queue, and Multilevel Feedback Queue** are designed for different system requirements, each having its own advantages and limitations. Selecting the appropriate scheduling algorithm helps achieve better system performance, fairness, and efficient resource utilization.




