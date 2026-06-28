# Non-Contiguous Memory Allocation in Operating Systems

Non-contiguous memory allocation is a dynamic memory management strategy where a process's memory footprint does not need to occupy a single, continuous block of physical addresses. Instead, the process is divided into smaller units and distributed across scattered, non-adjacent free spaces in physical RAM. Address translation hardware and the operating system maintain mapping tables to link these separated segments transparently during program execution.

## Core Approaches to Non-Contiguous Allocation

Operating systems implement non-contiguous memory management using three primary models:

### 1. Paging

Paging divides a process's logical address space into fixed-size blocks called pages, and physical RAM into blocks of the same size called frames.

- **Eliminating External Fragmentation:** Because any page can fit into any free frame, the system eliminates external fragmentation. It can, however, suffer from minor **internal fragmentation** in the final page of a process.

### 2. Segmentation

Segmentation divides a program into logical, variable-sized blocks called segments (such as the code segment, stack segment, heap, and shared libraries) based on the developer's logical view of the program.

- **Protection and Sharing:** This model facilitates memory sharing and access protection, but variable segment sizes can lead to external fragmentation over time.

### 3. Paged Segmentation (Hybrid Model)

A hybrid technique that first divides a process into logical segments and then splits each segment into fixed-size pages. This combines the modular protection benefits of segmentation with the external fragmentation solutions of paging.

## Working Mechanism of Non-Contiguous Allocation

To illustrate the operational advantages of non-contiguous allocation over contiguous schemes, consider the following scenarios:

### Contiguous versus Non-Contiguous Spanning

- **Setup:** A process requires a total of 6 MB of memory to run. The system has three scattered, free memory slots of 2 MB each at non-adjacent physical addresses (Total free memory = 6 MB).
- **Contiguous Allocation:** The allocation fails. Because contiguous allocation requires the process to occupy an unbroken 6 MB block, the scattered 2 MB slots cannot be utilized.
- **Non-Contiguous Allocation:** The process is split into three 2 MB segments. The OS allocates each segment to one of the free 2 MB slots. The process loads and executes successfully, optimizing memory utilization.

### Page and Frame Mapping

To avoid the overhead of dynamically dividing processes to match arbitrary free spaces, modern systems divide programs in advance into uniform pages. The operating system ensures that:

```text
Rule: Page Size = Frame Size
```

Suppose physical memory has a frame size of 4 KB, and two processes, Job A and Job B (each requiring 8 KB, or 2 pages), are loaded into memory:

1. **Job A Pages:** Page 0 and Page 1
2. **Job B Pages:** Page 0 and Page 1

Because memory is non-contiguous, these pages can be stored alternately or in any available sequence across the physical memory frames:

- **Frame 1:** Holds Page 0 of Job A
- **Frame 2:** Holds Page 0 of Job B
- **Frame 3:** Holds Page 1 of Job A
- **Frame 4:** Holds Page 1 of Job B

The OS maintains a **Page Table** for each process to map logical pages to physical frames, allowing the CPU to resolve addresses transparently during execution.

## Advantages and Disadvantages

### Advantages

- **Reduced Internal Fragmentation:** Memory is allocated in small, uniform pages (e.g., 4 KB), minimizing wasted space within allocated blocks.
- **Execution Flexibility:** Processes can be loaded into memory as long as the total number of free frames matches the process page requirement, without requiring a large contiguous space.
- **Efficient Memory Utilization:** Small, scattered memory gaps are utilized to fit pages of different processes, preventing memory wastage.
- **Dynamic Heap and Stack Growth:** Processes can request additional memory pages dynamically, which can be allocated from any scattered free frames.
- **Foundation for Virtual Memory:** Non-contiguous allocation forms the basis of virtual memory, allowing processes to execute even if only a fraction of their pages are currently resident in physical RAM.

### Disadvantages

- **Address Translation Overhead:** Every memory access requires translating a logical address to a physical address using page or segment tables, which can introduce latency.
- **Hardware Requirement:** This technique requires dedicated hardware support (the CPU's Memory Management Unit and Translation Lookaside Buffer) to speed up address mapping.
- **Memory Overhead for Tables:** The operating system must store page tables and segment tables in physical memory, consuming RAM.
- **Deallocation Complexity:** Releasing scattered pages and maintaining free-frame lists requires more complex kernel bookkeeping than contiguous schemes.

## Summary

Non-contiguous memory allocation allows processes to be split into smaller pages or segments and distributed across scattered, non-adjacent locations in physical RAM. While this technique introduces address translation latency and requires page table storage in memory, it eliminates external fragmentation and maximizes RAM utilization. By using page tables and the Memory Management Unit (MMU) to map logical pages to physical frames, non-contiguous allocation serves as the foundation for virtual memory systems in modern operating systems.




