# Operating Systems Cheat Sheet — Final Interview Edition

## 1. OS Basics

| Term | Full Form / Meaning |
| --- | --- |
| OS | Operating System — software that manages hardware and provides services to programs |
| Kernel | Core of the OS; handles memory, processes, and hardware communication |
| PCB | Process Control Block — data structure storing a process's state, PC, registers, memory info |
| PC | Program Counter — register holding address of the next instruction to execute |

### Types of OS

- **Batch OS** — Jobs with similar needs are grouped and run one after another with no user interaction; CPU finishes one job before starting the next.
- **Multiprogramming OS** — Several jobs sit in memory together; when one job waits for I/O, the CPU switches to another so it's never idle.
- **Time-Sharing OS** — A form of multiprogramming where each process gets a small fixed time slice (quantum); rapid switching makes it feel like all users run simultaneously.
- **Multiprocessing OS** — Uses two or more CPUs at once, increasing throughput.
- **Distributed OS** — Manages many networked computers that cooperate but each has its own CPU and memory.
- **Network OS (NOS)** — Runs on a server, managing shared files, users, and security over a network.
- **Real-Time OS (RTOS)** — Guarantees task completion within strict deadlines; used in embedded and medical systems.

## 2. Process and Threads

- **Process** = a program in execution, with its own memory space and PCB.
- **Thread** = a lightweight sub-unit of a process; has its own PC, registers, and stack but shares code/data/files with sibling threads.
- **fork() rule**: a process making \(n\) fork() calls produces \(2^n - 1\) child processes.
- **Process states**: New → Ready → Running → Waiting → Terminated.
- New: process is being created.
- Ready: waiting in queue for CPU.
- Running: currently executing on CPU.
- Waiting: blocked on I/O or event.
- Terminated: execution finished.

## 3. Schedulers and Dispatcher

| Scheduler | What It Does |
| --- | --- |
| Long-term | Decides which jobs are admitted into main memory (New → Ready) |
| Medium-term | Suspends/resumes processes by swapping them out to and in from disk |
| Short-term | Picks which ready process runs next on the CPU (Ready → Running) |
| Dispatcher | Performs the actual context switch — saves the current process's state, loads the next one's |

## 4. Scheduling Timing Terms

- **Arrival Time (AT)** — when the process enters the ready queue.
- **Burst Time (BT)** — CPU time the process needs.
- **Completion Time (CT)** — when the process finishes.
- **Turnaround Time (TAT)**: \(TAT = CT - AT\)
- **Waiting Time (WT)**: \(WT = TAT - BT\)

## 5. CPU Scheduling Algorithms — How Each Works

**FCFS (First Come First Serve)**
How it works: Processes are queued in the exact order they arrive. The CPU executes the first process fully, then moves to the next in queue — no interruptions. If two processes arrive at the same time, the one with the lower process ID goes first.
Example: If P1 (AT=0, BT=5), P2 (AT=1, BT=3) arrive, P1 runs first (0–5), then P2 runs (5–8), even though P2 is shorter.
Trait: Simple to implement, but a long job at the front causes a "convoy effect" where short jobs behind it wait unnecessarily.

**SJF (Shortest Job First)**
How it works: Among all processes currently in the ready queue, the CPU always picks the one with the smallest burst time next. It is non-preemptive, so once a process starts, it runs to completion even if a shorter one arrives.
Trait: Gives the best possible average waiting time mathematically, but requires knowing burst times in advance (hard in practice) and can starve long processes if short ones keep arriving.

**SRTF (Shortest Remaining Time First)**
How it works: The preemptive version of SJF. At every new arrival, the scheduler compares the remaining burst time of the running process against the new arrival's burst time. If the new process has less remaining work, it preempts the current one immediately.
Trait: Minimizes average turnaround time but has high context-switch overhead and can starve long processes.

**Round Robin (RR)**
How it works: Each process in the ready queue gets a fixed time slice (quantum). The CPU runs a process for one quantum; if it isn't finished, it's paused and sent to the back of the queue, and the next process gets a turn. This cycles until all finish.
Trait: Fair and starvation-free. Small quantum → more context switches (overhead) but faster response; quantum larger than all burst times makes it behave exactly like FCFS.

**Priority Scheduling**
How it works: Each process is assigned a priority number; the CPU always picks the highest-priority process from the ready queue. Ties are broken by arrival time. It can be preemptive (a new higher-priority process interrupts the running one) or non-preemptive (current process finishes first).
Trait: Low-priority processes can starve indefinitely; fixed using "aging" (gradually raising the priority of waiting processes).

**HRRN (Highest Response Ratio Next)**
How it works: Non-preemptive; for every waiting process, the scheduler computes a response ratio \(=\dfrac{WT+BT}{BT}\). The process with the highest ratio runs next. Since WT grows the longer a process waits, this ratio automatically increases for jobs that have waited long, preventing starvation.
Trait: Balances SJF's efficiency with fairness for longer jobs.

## 6. Critical Section Problem

- **Critical Section (CS)**: the portion of code accessing shared resources.
- **Race Condition**: final result depends on the unpredictable order in which processes access shared data.
- A correct solution must guarantee:
- **Mutual Exclusion** — only one process in CS at a time.
- **Progress** — if no process is in CS, one of the waiting processes must be allowed in without indefinite delay.
- **Bounded Waiting** — a process can't be skipped forever; there's a limit on how many times others enter before it.

## 7. Synchronization Tools

**Semaphore**
How it works: An integer variable manipulated only through two atomic operations — wait()/P() (decrements; blocks if the value goes negative) and signal()/V() (increments; wakes a waiting process). Because these operations are atomic (uninterruptible), no race condition can occur while updating the semaphore.

- **Counting Semaphore**: value can be any integer; used when multiple identical resource instances exist.
- **Binary Semaphore/Mutex**: value restricted to 0 or 1; used purely for mutual exclusion. Note: a mutex is conceptually different from a binary semaphore even though implementations look similar — a mutex is a locking mechanism owned/released by the same thread, while a semaphore is a signaling mechanism that can be signaled by any thread.

## 8. Deadlock

**4 Necessary (Coffman) Conditions** — all four must hold simultaneously for deadlock:

1. **Mutual Exclusion** — resources are non-shareable.
2. **Hold and Wait** — a process holds one resource while waiting for another.
3. **No Preemption** — resources can't be forcibly taken away.
4. **Circular Wait** — a cycle of processes each waiting on the next.

**Handling Methods**

- **Prevention** — design the system so one of the four conditions can never occur (e.g., force processes to request all resources upfront to remove Hold-and-Wait; order resources numerically to remove Circular Wait).
- **Avoidance (Banker's Algorithm)** — How it works: before granting any resource request, the OS simulates the allocation and checks if the system would still be in a "safe state" (i.e., there exists some order in which all processes can finish). Uses four data structures: Available (free resources), Max (max demand per process), Allocation (currently held), Need = Max − Allocation. If the simulated allocation keeps the system safe, the request is granted; otherwise, it's deferred.
- **Detection & Recovery** — Let deadlocks happen, then detect them: for single-instance resources, a cycle in the resource allocation graph signals deadlock; for multi-instance resources, a safety algorithm is run periodically. Recovery is done by terminating a process or forcibly preempting a resource.
- **Ignorance (Ostrich Algorithm)** — Assume deadlock is rare enough to ignore; if it happens, simply reboot the system.

## 9. Memory Management

- **Logical (Virtual) Address**: generated by the CPU; can change.
- **Physical Address**: actual location in RAM.
- **Static Loading**: entire program is loaded into a fixed memory address before execution begins.
- **Dynamic Loading**: a routine is loaded only when it's actually called during execution, saving memory.
- **Fragmentation**:
- **Internal**: wasted space inside an allocated block (block bigger than the process needs).
- **External**: free memory is scattered in small non-contiguous chunks, too small individually to satisfy requests.

**Variable Partition Allocation Strategies**

- **First Fit**: allocate the first hole big enough for the process.
- **Best Fit**: allocate the smallest hole that still fits, minimizing leftover space.
- **Worst Fit**: allocate the largest hole, leaving the biggest leftover gap.
- Note: Best Fit isn't always truly "best" in practice — it can create many tiny unusable fragments over time.

## 10. Paging vs Segmentation

| Feature | Paging | Segmentation |
| --- | --- | --- |
| How it works | Physical memory split into fixed-size frames; logical memory split into equal-size pages; a page table maps each page to a frame | Logical memory split into variable-size segments (based on logical units like functions/arrays); a segment table maps segment number to base address and length |
| Fragmentation type | Internal (last page may not be full) | External (variable segments leave irregular gaps) |
| Purpose | Solves external fragmentation of contiguous allocation | Gives programs a logical view of memory |

**Page Fault**: occurs when a program accesses a page that's part of its virtual address space but not currently loaded in physical memory — the hardware raises an interrupt so the OS can fetch it from disk.

## 11. Page Replacement Algorithms — How Each Works

**FIFO (First In First Out)**
How it works: The OS maintains a queue of pages currently in memory, ordered by arrival. When a new page must be loaded and memory is full, the page that has been in memory the longest (front of queue) is evicted.
Example: Reference string 1,3,0,3,5,6 with 3 slots → 1,3,0 fill empty slots (3 faults); 3 already present (0 faults); 5 replaces 1 — the oldest (1 fault); 6 replaces 3 (1 fault). Total = 5 faults.
Quirk — **Belady's Anomaly**: increasing the number of frames can sometimes increase the number of page faults under FIFO — the opposite of what you'd expect.

**Optimal Page Replacement**
How it works: Whenever a page must be evicted, the algorithm looks ahead in the reference string and evicts the page that won't be needed for the longest time in the future.
Trait: Gives the theoretical minimum number of page faults, but is impossible in practice since the OS can't know future requests — used only as a benchmark to judge other algorithms.

**LRU (Least Recently Used)**
How it works: Tracks how recently each page in memory was accessed; when eviction is needed, it removes the page that hasn't been used for the longest time in the past (as an approximation of the Optimal algorithm using history instead of future knowledge).
Trait: Performs close to Optimal in most real workloads; does not suffer from Belady's Anomaly.

**MRU (Most Recently Used)**
How it works: The opposite of LRU — evicts the page that was used most recently, on the assumption it's less likely to be needed again soon.
Trait: Rarely used in practice; can suffer from Belady's Anomaly.

## 12. Virtual Memory, Demand Paging, and Thrashing

- **Virtual Memory**: uses disk space to simulate extra RAM, letting programs larger than physical memory run.
- **Demand Paging**: How it works — initially only essential pages are loaded; whenever the CPU references a page not currently in RAM, a page fault triggers the OS to fetch just that page from disk. This means memory holds only actively used pages, improving utilization and startup speed.
- **Thrashing**: How it happens — if too many processes compete for too little RAM, each process's needed pages keep getting evicted before they're used again, causing continuous page faults; the CPU spends more time swapping pages than executing instructions, and overall throughput collapses.
- Fixes: reduce the number of concurrently running processes, use the working-set model to allocate frames based on actual need, or add more physical RAM.

## 13. File Systems

**Directory Operations**: search, create, delete, list, rename, traverse.

**File Allocation Methods**

- **Contiguous Allocation**: How it works — the entire file is stored in one continuous block of disk sectors; the file table only needs to record the starting block and length. Fast to read sequentially, but suffers external fragmentation and requires knowing the file size in advance.
- **Linked Allocation**: How it works — each block holds data plus a pointer to the next block, forming a chain; the file table stores only the starting block. No external fragmentation since blocks can be scattered anywhere, but random access is slow since you must follow the chain from the start.
- **Indexed Allocation**: How it works — a separate index block stores pointers to all the data blocks of the file; the file table just records the index block's address. Supports fast direct access without the fragmentation issues of contiguous allocation.

## 14. Disk Scheduling Algorithms — How Each Works

**FCFS**: Requests are serviced strictly in the order they arrive in the queue, regardless of their position on the disk. Simple but can cause long seek times if requests are scattered.

**SSTF (Shortest Seek Time First)**: The disk head always moves to whichever pending request is physically closest to its current position, minimizing seek distance for each move. Can starve requests far from the head if closer ones keep arriving.

**SCAN (Elevator Algorithm)**: The head sweeps in one direction (e.g., outward), servicing every request it passes, until it reaches the end of the disk, then reverses direction and sweeps back — just like an elevator serving floors in order.

**C-SCAN (Circular SCAN)**: Like SCAN, but the head only services requests in one direction; upon reaching the end, it jumps immediately back to the starting end without servicing on the way back, then sweeps forward again. This gives more uniform wait times than SCAN.

**LOOK**: Same sweeping idea as SCAN, but the head reverses direction as soon as it passes the last request in that direction — it doesn't travel all the way to the physical end of the disk unnecessarily.

**C-LOOK**: The circular version of LOOK — head moves to the last request, then jumps back to the first pending request on the other side, instead of going all the way to disk's physical end.

## 15. I/O Management

- **Device Driver**: software that translates OS calls into specific hardware commands.
- **Buffering**: temporarily storing data in memory while it moves between two devices at different speeds.
- **Spooling** (Simultaneous Peripheral Operations On-Line): queues jobs (e.g., print jobs) on disk so a slow device can process them one at a time without blocking the requesting process.

## 16. System Calls

| Category | Examples |
| --- | --- |
| Process Control | fork(), exit(), wait() |
| File Management | open(), read(), write(), close() |
| Device Management | ioctl() |
| Information Maintenance | getpid(), alarm(), sleep() |
| Communication | pipe(), shmget(), mmap() |

## 17. Virtualization

- **Virtual Machine (VM)**: software emulation of a full physical computer.
- **Hypervisor Type 1**: runs directly on hardware, no host OS needed (e.g., VMware ESXi) — better performance.
- **Hypervisor Type 2**: runs as an application on top of a host OS (e.g., VirtualBox) — easier to set up, more overhead.
- **Containers (Docker)**: share the host OS kernel instead of virtualizing full hardware, making them much lighter and faster to start than VMs.

## Quick Interview Traps

- FCFS causes convoy effect if the first job is long.
- SJF/SRTF give minimum waiting/turnaround time but risk starvation of long jobs.
- Round Robin with a very large quantum behaves exactly like FCFS.
- Mutex and binary semaphore look similar but serve different purposes (ownership vs signaling).
- Belady's Anomaly happens only with FIFO, not with LRU or Optimal (which are "stack algorithms").
- Best Fit allocation isn't always optimal in practice — it can create many small unusable gaps.
- Paging removes external fragmentation but introduces internal fragmentation.

