# Contiguous Memory Allocation Techniques

Contiguous memory allocation is a memory management strategy where the operating system assigns a single, continuous block of physical memory addresses to each executing process. Under this strategy, all instructions and variables of a process reside in adjacent memory locations. If a process requests access to RAM, the operating system must locate a single, unbroken region of free memory that is large enough to hold the process.

Contiguous memory management is implemented using two primary models: Fixed (Static) Partitioning and Variable (Dynamic) Partitioning.

## Fixed Partitioning Scheme

In the Fixed Partitioning scheme, the computer's main memory is divided into a set number of pre-defined partitions during system boot. Once defined, the boundaries and number of partitions remain unchanged.

### Execution Boundaries

Each partition is assigned to at most one process at a time. The operating system tracks partition boundaries using two hardware registers:

- **Base Register (Lower Limit):** Stores the physical starting address of the partition.
- **Limit Register (Upper Limit):** Stores the size or ending address of the partition.

### Characteristics of Fixed Partitioning

- **Constrained Multiprogramming:** The maximum number of concurrent processes (the degree of multiprogramming) is strictly limited by the number of partitions.
- **Process Size Limits:** A process cannot execute if its size exceeds the size of the largest available partition.
- **Internal Fragmentation:** If a process is smaller than its assigned partition, the unused memory within that partition is wasted. Other processes cannot access this idle space.

### Advantages and Disadvantages of Fixed Partitioning

#### Advantages

- **Low Management Overhead:** Because partition sizes are static and defined in advance, the operating system does not perform complex placement calculations.
- **Simple Implementation:** The OS only needs to maintain a simple status table (Allocated or Free) for each partition.

#### Disadvantages

- **Inflexible Architecture:** Process sizes are bounded by partition limits, and the degree of multiprogramming is fixed.
- **Wasted Space:** Wasted memory due to internal fragmentation can be significant if process sizes vary widely.

## Variable Partitioning Scheme

In the Variable Partitioning scheme, memory begins as a single, continuous free block. Partitions are created dynamically during runtime to match the exact size of incoming processes.

### Characteristics of Variable Partitioning

- **On-Demand Sizing:** When a process is loaded, the OS carves out a partition that matches the process size exactly.
- **Dynamic Multiprogramming:** The number of concurrent processes is not fixed; it scales dynamically based on process sizes and memory availability.
- **No Internal Fragmentation:** Because partitions match process sizes exactly, no memory is wasted inside an allocated partition.

### Advantages and Disadvantages of Variable Partitioning

#### Advantages

- **Efficient Memory Usage:** Eliminates internal fragmentation, maximizing the active space used by programs.
- **Dynamic Scaling:** Processes of varying sizes are accommodated without fixed boundaries.

#### Disadvantages

- **External Fragmentation:** As processes complete and terminate, they leave behind small, scattered free spaces in memory. Over time, these gaps become too small to hold new processes, even if the total free memory in the system is large enough.
- *Example:* A process requiring 45 KB of memory trying to run when the total free memory is 60 KB but split into separate non-contiguous blocks of 20 KB and 40 KB.
- **Increased Bookkeeping:** The OS must maintain complex data structures to track variable-sized free holes and allocated blocks.

## Solutions for External Fragmentation

To resolve external fragmentation, operating systems utilize two primary techniques:

### 1. Memory Compaction

Compaction is the process of moving all active processes toward one end of the physical memory (top or bottom). This consolidates all scattered free memory blocks into a single, contiguous free region.

- **Overhead:** Compaction requires significant CPU cycles to copy memory blocks and update relocation registers. It also requires halting running processes during the transfer, making it undesirable for real-time systems.

### 2. Non-Contiguous Memory Allocation

Rather than requiring a process to reside in a single continuous memory block, the operating system can split the process into smaller components and distribute them across non-adjacent locations in RAM.

- **Frames:** Physical RAM is divided into fixed-size blocks called frames.
- **Pages:** The process's logical address space is divided into blocks of the same size called pages.
- **Address Translation:** The Memory Management Unit (MMU) uses page tables to map logical pages to non-contiguous physical frames transparently during execution.

## Summary

Contiguous memory allocation distributes physical RAM to processes in unbroken address blocks. Fixed partitioning divides memory into pre-defined sections at boot time, offering low overhead but suffering from internal fragmentation. Variable partitioning creates partitions dynamically, eliminating internal fragmentation but causing external fragmentation over time as processes exit. To mitigate external fragmentation, operating systems must perform expensive memory compaction or transition to non-contiguous allocation methods like paging.




