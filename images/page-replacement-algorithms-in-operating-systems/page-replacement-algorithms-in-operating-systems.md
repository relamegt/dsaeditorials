# Page Replacement Algorithms in Operating Systems

In a paged virtual memory system, the operating system triggers a page fault when a process references a page that does not reside in physical RAM. If physical memory is completely occupied, the memory manager must execute a page replacement algorithm to select a resident "victim page" for eviction to make space for the incoming page.

## The Replacement Lifecycle

The operating system executes page replacement using the following steps:

1. **Victim Selection:** The memory manager applies a specific page replacement algorithm to select an active page frame in RAM for eviction.
2. **Page Table De-registration:** The OS marks the victim page's entry in the page table as invalid (not present).
3. **Dirty Page Check:** If the page was modified (marked dirty) during its residency in RAM, the OS schedules a write operation to sync it back to secondary storage. If it was unmodified, the frame is cleared immediately.
4. **Ingestion and Update:** The OS reads the incoming page into the cleared frame, updates the process's page table, and restarts the faulting instruction.

The efficiency of a page replacement algorithm directly affects the page fault rate, which determines system performance.

## Standard Page Replacement Algorithms

Operating systems utilize several replacement strategies to manage page lifetimes:

### 1. First-In, First-Out (FIFO)

The simplest replacement policy, where the OS maintains all resident pages in a queue.

- **Logic:** The page at the front of the queue (the oldest page in memory) is evicted first when a page fault occurs.
- **Limitations:** Can lead to suboptimal performance and is susceptible to **Belady's Anomaly**, where increasing the number of physical frames can paradoxically increase the page fault rate.

### 2. Optimal Page Replacement (OPT)

A theoretical benchmark algorithm that yields the lowest possible page fault rate for a given reference string.

- **Logic:** Evicts the page that will not be referenced for the longest duration of time in the future.
- **Implementation Constraint:** Impossible to implement in practice because the operating system cannot foresee future memory reference sequences. It serves solely as a baseline to evaluate the performance of other algorithms.

### 3. Least Recently Used (LRU)

An algorithm that approximates the Optimal strategy by using past access history as a predictor of future activity.

- **Logic:** Evicts the page that has not been accessed for the longest duration of time.
- **Implementation:** Requires hardware register support or stack structures to track page access timestamps dynamically, introducing runtime overhead.

### 4. Most Recently Used (MRU)

The opposite of the LRU algorithm.

- **Logic:** Evicts the page that has been referenced most recently.
- **Use Case:** Useful in scanning situations where a program is sequentially reading large datasets and is unlikely to access recently read data again soon.

## Step-by-Step Execution Walkthrough

Consider a system configured with **3 physical memory frames** (initially empty) and the following logical page reference sequence:

```text
Reference String: 4, 7, 3, 0, 1, 7, 3, 8, 4, 7
```

We trace and compare the page fault behavior for all four algorithms below:

### 1. FIFO Trace

- **Page 4:** Frame load `[4, _, _]` (Fault 1)
- **Page 7:** Frame load `[4, 7, _]` (Fault 2)
- **Page 3:** Frame load `[4, 7, 3]` (Fault 3)
- **Page 0:** Evicts oldest page (4). Frames: `[0, 7, 3]` (Fault 4)
- **Page 1:** Evicts oldest page (7). Frames: `[0, 1, 3]` (Fault 5)
- **Page 7:** Evicts oldest page (3). Frames: `[0, 1, 7]` (Fault 6)
- **Page 3:** Evicts oldest page (0). Frames: `[3, 1, 7]` (Fault 7)
- **Page 8:** Evicts oldest page (1). Frames: `[3, 8, 7]` (Fault 8)
- **Page 4:** Evicts oldest page (7). Frames: `[3, 8, 4]` (Fault 9)
- **Page 7:** Evicts oldest page (3). Frames: `[7, 8, 4]` (Fault 10)
- **Total Page Faults (FIFO):** 10

### 2. Optimal Trace

- **Page 4:** Frame load `[4, _, _]` (Fault 1)
- **Page 7:** Frame load `[4, 7, _]` (Fault 2)
- **Page 3:** Frame load `[4, 7, 3]` (Fault 3)
- **Page 0:** Look ahead: `1, 7, 3, 8, 4, 7`. Page 7 is accessed next, then 3, then 4. Page 4 is accessed furthest in the future. Evicts 4. Frames: `[0, 7, 3]` (Fault 4)
- **Page 1:** Look ahead: `7, 3, 8, 4, 7`. Pages 7 and 3 are referenced next, but 0 is never accessed again. Evicts 0. Frames: `[1, 7, 3]` (Fault 5)
- **Page 7:** Already resident. Hit! Frames: `[1, 7, 3]`
- **Page 3:** Already resident. Hit! Frames: `[1, 7, 3]`
- **Page 8:** Look ahead: `4, 7`. Page 7 and 4 are referenced next, but 1 and 3 are not. Evict 1. Frames: `[8, 7, 3]` (Fault 6)
- **Page 4:** Look ahead: `7`. Page 7 is accessed next, but 8 and 3 are not. Evict 3. Frames: `[8, 7, 4]` (Fault 7)
- **Page 7:** Already resident. Hit! Frames: `[8, 7, 4]`
- **Total Page Faults (Optimal):** 7

### 3. LRU Trace

- **Page 4:** Frame load `[4, _, _]` (Fault 1)
- **Page 7:** Frame load `[4, 7, _]` (Fault 2)
- **Page 3:** Frame load `[4, 7, 3]` (Fault 3)
- **Page 0:** Page 4 is the least recently accessed (at t=0). Evicts 4. Frames: `[0, 7, 3]` (Fault 4)
- **Page 1:** Page 7 is the least recently accessed (at t=1). Evicts 7. Frames: `[0, 1, 3]` (Fault 5)
- **Page 7:** Page 3 is the least recently accessed (at t=2). Evicts 3. Frames: `[0, 1, 7]` (Fault 6)
- **Page 3:** Page 0 is the least recently accessed (at t=3). Evicts 0. Frames: `[3, 1, 7]` (Fault 7)
- **Page 8:** Page 1 is the least recently accessed (at t=4). Evicts 1. Frames: `[3, 8, 7]` (Fault 8)
- **Page 4:** Page 7 is the least recently accessed (at t=5). Evicts 7. Frames: `[3, 8, 4]` (Fault 9)
- **Page 7:** Page 3 is the least recently accessed (at t=6). Evicts 3. Frames: `[7, 8, 4]` (Fault 10)
- **Total Page Faults (LRU):** 10

### 4. MRU Trace

- **Page 4:** Frame load `[4, _, _]` (Fault 1)
- **Page 7:** Frame load `[4, 7, _]` (Fault 2)
- **Page 3:** Frame load `[4, 7, 3]` (Fault 3)
- **Page 0:** Page 3 is the most recently accessed (at t=2). Evicts 3. Frames: `[4, 7, 0]` (Fault 4)
- **Page 1:** Page 0 is the most recently accessed (at t=3). Evicts 0. Frames: `[4, 7, 1]` (Fault 5)
- **Page 7:** Already resident. Hit! (t=5: access 7). Frames: `[4, 7, 1]`
- **Page 3:** Page 7 is the most recently accessed (at t=5). Evicts 7. Frames: `[4, 3, 1]` (Fault 6)
- **Page 8:** Page 3 is the most recently accessed (at t=6). Evicts 3. Frames: `[4, 8, 1]` (Fault 7)
- **Page 4:** Already resident. Hit! (t=8: access 4). Frames: `[4, 8, 1]`
- **Page 7:** Page 4 is the most recently accessed (at t=8). Evicts 4. Frames: `[7, 8, 1]` (Fault 8)
- **Total Page Faults (MRU):** 8

## Comparison Matrix of Algorithms

| Algorithm | Fault Rate | Implementability | Hardware Support | Belady's Anomaly |
| --- | --- | --- | --- | --- |
| **Optimal** | Lowest (Benchmark) | Impossible (Theoretical) | None | No |
| **FIFO** | Higher | Very Simple | None | Yes |
| **LRU** | Low (Approximates OPT) | Complex | High (Timestamps/Registers) | No |
| **MRU** | Variable | Moderate | Moderate (Access tracking) | Yes |

> **Note:** Page replacement algorithms represent trade-offs between hardware overhead and execution efficiency. While the Optimal algorithm serves as a theoretical performance benchmark, operating systems use LRU and its approximations to achieve low page fault rates.

## Summary

Page replacement algorithms are crucial components of virtual memory management systems, deciding which active RAM page to evict when new pages must be loaded into full memory. While FIFO is simple but susceptible to anomalies, Optimal replacement remains a theoretical standard. Practical systems implement LRU or MRU based on access histories to minimize page fault interrupts. Selecting and optimizing these replacement routines directly affects virtual memory access speeds and overall system stability.




