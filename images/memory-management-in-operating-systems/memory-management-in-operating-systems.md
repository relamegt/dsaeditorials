# Memory Management in Operating Systems

Memory management is the process of coordinating and controlling a computer's primary memory. It involves dynamically allocating memory blocks (RAM) to executing programs, mapping logical addresses to physical hardware addresses, protecting processes from unauthorized cross-boundary access, and reclaiming memory when programs terminate.

## Key Functions of Memory Management

A robust memory management subsystem is responsible for several critical tasks:

- **Multi-Process Support:** Allowing multiple active processes to reside in primary memory concurrently.
- **Memory Protection:** Ensuring that executing processes cannot read or write to memory spaces allocated to other processes without authorization.
- **Virtual Memory and Swapping:** Utilizing secondary storage to extend the apparent size of physical RAM, swapping idle processes out to disk to free up memory.
- **Resource Maximization:** Maximizing CPU utilization and throughput by maintaining a steady pipeline of memory-resident tasks.

## Memory Allocation Techniques

Operating systems distribute memory to processes using contiguous or non-contiguous allocation strategies:

### Swapping

Swapping is a technique where the operating system temporarily moves entire processes between main memory (RAM) and secondary storage (swap space) to free up memory for active tasks.

- **Priority-Based Swapping:** Lower-priority processes are swapped out to disk when higher-priority processes require memory space.
- **Reclamation:** Once the swapped-out process is rescheduled, it is loaded back into main memory and resumes execution from its saved state.

### Contiguous Memory Allocation

Contiguous allocation requires that each process be allocated a single, unbroken block of adjacent physical memory addresses.

#### 1. Single Contiguous Memory Allocation
The simplest allocation model. Main memory is divided into two distinct regions:

- One region is reserved exclusively for the Operating System kernel.
- The remaining memory is allocated to a single active user process.
- **Limitations:** No multiprogramming is supported, and memory utilization is poor because only one program can run at a time.

#### 2. Partitioned Contiguous Memory Allocation
To support multiprogramming, main memory is divided into multiple contiguous partitions, with each partition holding a single process.

- **Fixed Partitioning:** Memory is divided into partitions of fixed sizes at boot time. Each partition holds exactly one process. While simple to implement, it leads to **internal fragmentation** (wasted space within a partition if a process is smaller than the partition size).
- **Variable (Dynamic) Partitioning:** Partitions are created dynamically during runtime to match the exact size of the executing processes. This eliminates internal fragmentation but leads to **external fragmentation** (free memory gets broken into small, scattered blocks that cannot satisfy larger incoming allocation requests).

##### Example Partition Table
The operating system maintains partition allocation status using a dedicated table:

| Starting Address | Size of Partition | Allocation Status |
| --- | --- | --- |
| **0 MB** | 4 MB | Allocated |
| **4 MB** | 2 MB | Free |
| **6 MB** | 3 MB | Free |
| **9 MB** | 7 MB | Allocated |

### Non-Contiguous Memory Allocation

Non-contiguous allocation divides a process's logical address space into smaller chunks that can be distributed across different, non-adjacent physical frames in RAM. This model requires address translation support from the CPU's Memory Management Unit (MMU).

Non-contiguous allocation techniques include:

- **Paging:** Divides a process's logical memory into fixed-size units (pages) and physical RAM into frames of the same size. The MMU maps pages to frames using a Page Table.
- **Segmentation:** Divides a process into logical segments of variable sizes based on compiler structures (such as code, data, and stack segments).
- **Paged Segmentation:** Combines both techniques, page-mapping individual logical segments to reduce external fragmentation.

## Memory Management Mechanisms

- **Virtual Memory:** A mechanism that simulates more main memory than is physically present by using secondary storage (disk swap space) as a transparent extension of RAM.
- **Demand Paging:** An optimization of virtual memory where pages are loaded into physical RAM frames only when they are referenced (demanded) during execution, reducing startup overhead.
- **Page Replacement Algorithms:** When physical memory is full and a new page must be loaded, the OS evicts an existing page using specific algorithms:
- *FIFO (First-In, First-Out):* Evicts the page that has been in memory the longest.
- *LRU (Least Recently Used):* Evicts the page that has not been accessed for the longest duration.
- *Optimal:* Evicts the page that will not be needed for the longest duration in the future (theoretical baseline).
- *LFU (Least Frequently Used):* Evicts the page with the lowest execution reference counter.

## Common Memory Management Problems

- **Internal Fragmentation:** Wasted memory space inside a pre-allocated partition when a process does not use the entire allocated block.
- **External Fragmentation:** Wasted memory space scattered across small, non-contiguous blocks that cannot satisfy larger contiguous allocation requests.
- **Thrashing:** A state where the OS spends more time context-switching and swapping pages between disk and RAM than executing actual program instructions, leading to a system freeze.

## Placement Algorithms for Dynamic Memory

When a process requests memory, the OS uses placement algorithms to decide which free block to allocate:

- **First Fit:** Allocates the first free memory block from the starting address that is large enough.
- **Best Fit:** Scans the entire memory space to allocate the smallest available block that fits, minimizing wasted space.
- **Worst Fit:** Allocates the largest available memory block, leaving a large remaining fragment.
- **Next Fit:** Works like First Fit, but starts searching from the location of the last allocation rather than the beginning of memory.

## Summary

Memory management is a core operating system function that optimizes RAM allocation among competing processes. Through contiguous methods (such as fixed and dynamic partitioning) and non-contiguous methods (such as paging and segmentation), the OS balances access latency, address translation costs, and fragmentation. By incorporating virtual memory, demand paging, and page replacement algorithms, operating systems enable the execution of large programs while maintaining system stability and performance.




