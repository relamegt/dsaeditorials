# Belady's Anomaly in Page Replacement Algorithms

Belady's Anomaly is a counter-intuitive phenomenon in operating systems where increasing the number of physical memory frames allocated to a process results in an unexpected increase in the number of page faults. Under normal conditions, allocating more physical RAM to a program should reduce page faults and improve performance. However, page replacement algorithms that do not satisfy the stack property can experience the opposite effect, degrading system efficiency.

## Stack-Based Algorithms vs. FIFO

Operating systems categorize page replacement algorithms based on how they allocate and track page residency:

### Stack-Based Algorithms

Algorithms such as Optimal (OPT) and Least Recently Used (LRU) are classified as stack-based algorithms.

- **The Stack Property:** A replacement algorithm is stack-based if the set of pages resident in memory with `N` frames is always a strict subset of the pages resident in memory if `N + 1` frames were allocated.
- **Inclusion Guarantee:** Because stack-based algorithms ensure that any page that would be resident in a smaller memory space is also resident in a larger memory space, they **never** suffer from Belady's Anomaly.
- *Example (LRU):* LRU priorities are based solely on the order of page references. The top `N` entries of the access stack represent the most recently used pages. Increasing the frame count to `N + 1` simply adds the next page in history to the pool, ensuring the original `N` pages remain in memory.

### FIFO Algorithm

The First-In, First-Out (FIFO) algorithm is not stack-based.

- **Lack of Subset Inclusion:** FIFO tracks pages using a simple queue based on their entry times, independent of their access frequency or recency.
- **Anomaly Vulnerability:** When physical frames increase, the queue dynamics shift. A page that is highly active can be evicted simply because it was loaded earlier, breaking the subset inclusion property and triggering Belady's Anomaly on specific reference patterns.

## Walkthrough: FIFO Anomaly Trace

Consider a system executing the FIFO page replacement algorithm on the following page reference sequence:

```text
Reference String: 2, 3, 4, 5, 2, 3, 1, 2, 3, 4, 5, 1
```

We evaluate the page fault behavior across two frame allocations:

### Case 1: FIFO with 3 Physical Frames

The system allocates three RAM frames (slots 1, 2, and 3):

1. **Page 2:** Frame load `[2, _, _]` (Fault 1)
2. **Page 3:** Frame load `[2, 3, _]` (Fault 2)
3. **Page 4:** Frame load `[2, 3, 4]` (Fault 3)
4. **Page 5:** Evicts oldest page (2). Frames: `[5, 3, 4]` (Fault 4)
5. **Page 2:** Evicts oldest page (3). Frames: `[5, 2, 4]` (Fault 5)
6. **Page 3:** Evicts oldest page (4). Frames: `[5, 2, 3]` (Fault 6)
7. **Page 1:** Evicts oldest page (5). Frames: `[1, 2, 3]` (Fault 7)
8. **Page 2:** Already resident. Hit! Frames: `[1, 2, 3]`
9. **Page 3:** Already resident. Hit! Frames: `[1, 2, 3]`

10. **Page 4:** Evicts oldest page (2). Frames: `[1, 4, 3]` (Fault 8)
11. **Page 5:** Evicts oldest page (3). Frames: `[1, 4, 5]` (Fault 9)
12. **Page 1:** Already resident. Hit! Frames: `[1, 4, 5]`

- **Total Page Faults (3 Frames):** **9**

### Case 2: FIFO with 4 Physical Frames

The system allocates four RAM frames (slots 1, 2, 3, and 4):

1. **Page 2:** Frame load `[2, _, _, _]` (Fault 1)
2. **Page 3:** Frame load `[2, 3, _, _]` (Fault 2)
3. **Page 4:** Frame load `[2, 3, 4, _]` (Fault 3)
4. **Page 5:** Frame load `[2, 3, 4, 5]` (Fault 4)
5. **Page 2:** Already resident. Hit! Frames: `[2, 3, 4, 5]`
6. **Page 3:** Already resident. Hit! Frames: `[2, 3, 4, 5]`
7. **Page 1:** Evicts oldest page (2). Frames: `[1, 3, 4, 5]` (Fault 5)
8. **Page 2:** Evicts oldest page (3). Frames: `[1, 2, 4, 5]` (Fault 6)
9. **Page 3:** Evicts oldest page (4). Frames: `[1, 2, 3, 5]` (Fault 7)

10. **Page 4:** Evicts oldest page (5). Frames: `[1, 2, 3, 4]` (Fault 8)
11. **Page 5:** Evicts oldest page (1). Frames: `[5, 2, 3, 4]` (Fault 9)
12. **Page 1:** Evicts oldest page (2). Frames: `[5, 1, 3, 4]` (Fault 10)

- **Total Page Faults (4 Frames):** **10**

### Conclusion

By increasing the physical frame allocation from **3 to 4**, the page faults increased from **9 to 10**. This confirms the presence of Belady's Anomaly under the FIFO replacement scheme.

## Walkthrough: LRU Consistency Trace

To verify that stack-based algorithms are immune to the anomaly, we trace the same reference string under the Least Recently Used (LRU) algorithm:

### Case 1: LRU with 3 Physical Frames

1. **Page 2:** Frame load `[2, _, _]` (Fault 1)
2. **Page 3:** Frame load `[2, 3, _]` (Fault 2)
3. **Page 4:** Frame load `[2, 3, 4]` (Fault 3)
4. **Page 5:** Evicts LRU page (2). Frames: `[5, 3, 4]` (Fault 4)
5. **Page 2:** Evicts LRU page (3). Frames: `[5, 2, 4]` (Fault 5)
6. **Page 3:** Evicts LRU page (4). Frames: `[5, 2, 3]` (Fault 6)
7. **Page 1:** Evicts LRU page (5). Frames: `[1, 2, 3]` (Fault 7)
8. **Page 2:** Hit! Frames: `[1, 2, 3]` (LRU order: 2, 1, 3)
9. **Page 3:** Hit! Frames: `[1, 2, 3]` (LRU order: 3, 2, 1)

10. **Page 4:** Evicts LRU page (1). Frames: `[4, 2, 3]` (Fault 8)
11. **Page 5:** Evicts LRU page (2). Frames: `[4, 5, 3]` (Fault 9)
12. **Page 1:** Evicts LRU page (3). Frames: `[4, 5, 1]` (Fault 10)

- **Total Page Faults (3 Frames):** **10**

### Case 2: LRU with 4 Physical Frames

1. **Page 2:** Frame load `[2, _, _, _]` (Fault 1)
2. **Page 3:** Frame load `[2, 3, _, _]` (Fault 2)
3. **Page 4:** Frame load `[2, 3, 4, _]` (Fault 3)
4. **Page 5:** Frame load `[2, 3, 4, 5]` (Fault 4)
5. **Page 2:** Hit! Frames: `[2, 3, 4, 5]` (LRU order: 2, 5, 4, 3)
6. **Page 3:** Hit! Frames: `[2, 3, 4, 5]` (LRU order: 3, 2, 5, 4)
7. **Page 1:** Evicts LRU page (4). Frames: `[2, 3, 1, 5]` (Fault 5)
8. **Page 2:** Hit! Frames: `[2, 3, 1, 5]` (LRU order: 2, 1, 3, 5)
9. **Page 3:** Hit! Frames: `[2, 3, 1, 5]` (LRU order: 3, 2, 1, 5)

10. **Page 4:** Evicts LRU page (5). Frames: `[2, 3, 1, 4]` (Fault 6)
11. **Page 5:** Evicts LRU page (1). Frames: `[2, 3, 5, 4]` (Fault 7)
12. **Page 1:** Evicts LRU page (4). Frames: `[2, 3, 5, 1]` (Fault 8)

- **Total Page Faults (4 Frames):** **8**

As physical memory frames increased, page faults under the LRU algorithm decreased from **10 to 8**, demonstrating expected performance scaling.

## Summary

Belady's Anomaly is a counter-intuitive memory management scenario where increasing physical memory frames results in a higher number of page faults. While queue-based policies like FIFO are vulnerable to the anomaly because they fail to satisfy the stack subset property, stack-based replacement algorithms like Optimal and LRU are immune to this issue. Operating systems mitigate this anomaly by prioritizing stack-based page eviction heuristics in virtual memory managers to ensure that increased RAM allocation translates to predictable performance gains.




