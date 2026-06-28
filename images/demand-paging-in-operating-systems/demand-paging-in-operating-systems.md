# Demand Paging in Operating Systems

Demand paging is a virtual memory management technique where pages are loaded from secondary storage (disk) into physical memory (RAM) only when they are actively requested or needed by the CPU. Instead of pre-loading a program's entire address space into RAM during process initiation, the operating system brings in pages dynamically, minimizing RAM consumption and speed up initial process startup.

## Pure Demand Paging

Pure demand paging is an execution model where the operating system starts a program with **zero** pages pre-loaded in physical memory:

- **Disk-Only Initialization:** When the program is launched, the OS creates its process control structures and page tables, but marks every single page table entry as invalid (indicating the page resides on disk).
- **Immediate Page Faulting:** The very first execution of the program's initial instruction immediately triggers a page fault because the first code page is not in RAM.
- **Incremental Loading:** The OS loads the first page, resumes execution, and continues fetching pages one by one only as they are dynamically referenced.
- **Benefits:** Extremely useful for launching massive programs immediately on memory-constrained systems.
- **Drawbacks:** Can cause a high frequency of initial page faults, slowing down the program during its initial startup phase.

## Workflow of Demand Paging

When a process executes, the demand paging system coordinates memory access through the following phases:

1. **Process Reference:** The CPU attempts to access a memory address on a virtual page.
2. **Page Table Inspection:** The MMU inspects the page table entry (PTE) corresponding to the requested page.
3. **Trap Generation (Page Fault):**

- If the PTE valid/invalid bit is set to **valid**, the address translation completes, and the CPU reads or writes the memory location.
- If the PTE bit is set to **invalid**, the MMU halts execution and triggers a **Page Fault** trap to the operating system kernel.

1. **Disk Search:** The OS kernel processes the interrupt, verifies that the memory request is valid, and locates the requested page in secondary storage.
2. **Frame Allocation:** The OS identifies a free physical RAM frame. If physical memory is full, the OS runs a page replacement algorithm to evict an existing page, writing it back to disk if it was modified.
3. **Fetch and Map:** The OS reads the page from disk into the allocated frame, updates the page table entry to **valid**, and records the physical frame number.
4. **Instruction Restart:** The OS signals the CPU to resume the interrupted program, restarting the exact instruction that triggered the page fault.

## Page Table Allocation Scenario

Suppose we want to execute a program called **Task-A** which consists of six pages: Page 0, Page 1, Page 2, Page 3, Page 4, and Page 5. 

- **Current State:** During startup, the demand paging manager only loads Page 0 and Page 2 into RAM frames.
- **Page Table Map:**
- Page 0 -&gt; Valid (Resident in RAM)
- Page 1 -&gt; Invalid (On Disk)
- Page 2 -&gt; Valid (Resident in RAM)
- Page 3 -&gt; Invalid (On Disk)
- Page 4 -&gt; Invalid (On Disk)
- Page 5 -&gt; Invalid (On Disk)
- **Access Scenario:** When the CPU attempts to read data located on Page 3, the MMU checks the Page Table and detects the "Invalid" status. This immediately triggers a page fault, prompting the OS to retrieve Page 3 from disk and update the mapping to Valid.

## Page Replacement Algorithms

When all physical RAM frames are occupied and a page fault occurs, the OS must select a resident page to evict using a page replacement algorithm:

- **FIFO (First-In, First-Out):** Evicts the page that has been in physical memory the longest. While simple to implement, it can cause suboptimal performance and is vulnerable to **Belady's Anomaly** (where allocating more physical frames can paradoxically increase page faults).
- **LRU (Least Recently Used):** Evicts the page that has not been accessed for the longest time. It is highly effective at reducing thrashing but requires hardware support or list tracking.
- **LFU (Least Frequently Used):** Evicts the page with the lowest execution reference counter, assuming pages accessed rarely are no longer needed.
- **MRU (Most Recently Used):** Evicts the page that was accessed most recently, which is useful in sequential database scanning.
- **Random Selection:** Randomly chooses an active frame to evict, requiring no metadata tracking but offering unpredictable performance.

## Comparison: Demand Paging vs. Pre-Paging

| Feature | Demand Paging | Pre-Paging |
| --- | --- | --- |
| **Allocation Principle** | Loads pages into RAM only when the CPU references them. | Loads multiple pages into memory predictively in advance. |
| **Startup Latency** | Low initial startup delay; processes begin execution immediately. | Higher initial startup delay due to pre-fetching. |
| **Memory Efficiency** | High; RAM is only allocated for pages that are actually executed. | Low; memory is wasted if predicted pages are never accessed. |
| **Execution Interrupts** | High initial page faults can interrupt execution and cause delays. | Minimizes page faults during execution, ensuring smoother runtimes. |
| **Locality Assumption** | Relies on temporal and spatial locality during run-time. | Predicts spatial locality beforehand (loading adjacent blocks). |

> **Note:** Demand paging optimizes physical memory utilization by loading pages only when referenced. However, if a process accesses too many non-resident pages too quickly, it can cause a cascade of page faults, leading to system thrashing.

## Summary

Demand paging is a virtual memory management technique that loads memory pages into RAM frames only when they are referenced by the CPU. By utilizing page table valid/invalid bits and triggering page fault traps, the operating system dynamically swaps pages between RAM and disk storage. While demand paging reduces process startup overhead and maximizes RAM efficiency, it introduces swapping delays. Operating systems use page replacement algorithms (such as LRU or FIFO) and pre-paging strategies to optimize address translation speeds.




