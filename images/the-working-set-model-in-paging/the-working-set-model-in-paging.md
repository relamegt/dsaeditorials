# The Working Set Model in Paging

The Working Set Model is a memory management technique designed to prevent thrashing in virtual memory systems. It is built on the Locality of Reference model, which observes that a running process dynamically transitions through execution phases where it repeatedly accesses a relatively small, concentrated set of pages over a short period. This active subset of pages is called the process's working set.

## Principles of the Working Set Model

The working set model aims to keep a process's active pages resident in physical RAM by implementing the following strategies:

- **Defining the Working Set:** The model uses a sliding parameter called the working set window (`Delta`), representing a fixed number of recent page references (e.g., the last 1,000 memory references). The working set for a process at any instant is the set of all unique pages referenced within this window. The number of unique pages is called the Working Set Size (WSS).
- **Dynamic Frame Allocation:** The operating system dynamically allocates physical memory frames to each process to match its current Working Set Size. This ensures that the pages actively required by the process are kept in RAM, minimizing page faults.
- **Locality Adaptation:** As the process execution transitions (e.g., exiting one function and entering another), its memory access pattern shifts. The OS dynamically grows or shrinks the process's frame allocation to match the changing WSS.
- **Managing Memory Shortages:** If the sum of all processes' working set sizes exceeds the available physical memory frames, the OS suspends one or more processes to free up frames, preventing the entire system from thrashing.

## Walkthrough: Working Set Trace Example

Consider a system using a sliding working set window size of **Delta = 8** page references. We sample the working set at three different execution intervals:

### 1. Sampling at Time Instance t0

- **Recent Page References:** 2, 5, 2, 8, 2, 5, 5, 8
- **Unique Page Set:** {2, 5, 8}
- **Working Set Size (WSS):** 3
- **Allocated RAM Frames:** 3

### 2. Sampling at Time Instance t1

- **Recent Page References:** 6, 1, 9, 3, 6, 9, 1, 6
- **Unique Page Set:** {1, 3, 6, 9}
- **Working Set Size (WSS):** 4
- **Allocated RAM Frames:** 4

### 3. Sampling at Time Instance t2

- **Recent Page References:** 0, 0, 4, 0, 4, 4, 0, 4
- **Unique Page Set:** {0, 4}
- **Working Set Size (WSS):** 2
- **Allocated RAM Frames:** 2

## Impact of Window Size (Delta) Selection

Choosing the correct working set window size is critical to system performance:

- **If Delta is too small:** The window may not cover the process's active locality. Pages will be repeatedly loaded and evicted, leading to high page fault rates and thrashing.
- **If Delta is too large:** The window will overlap multiple execution localities, over-allocating physical frames to idle pages and reducing the number of concurrent processes the system can run.
- **If Delta is infinite:** The working set becomes the set of all pages accessed since the program started, reducing the model to simple paging without dynamic locality tracking.

> **Note:** The Working Set Model prevents thrashing by dynamically tracking a process's active page locality within a sliding window. It ensures that the operating system only schedules processes whose working set sizes can fit collectively within physical memory.

## Summary

The Working Set Model prevents system thrashing by dynamically allocating frames to processes based on their active page references within a sliding window. By matching physical frame allocations to the changing working set size of each process, the operating system ensures that active page localities remain resident in RAM. While selecting the optimal window size is critical to prevent over-allocation or page starvation, this model serves as a standard mechanism for balancing multiprogramming capacity and memory stability.




