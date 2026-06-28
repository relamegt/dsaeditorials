# Disk Scheduling Algorithms in Operating Systems

Disk scheduling algorithms (also called I/O scheduling algorithms) manage the order in which pending read and write requests to a hard disk are processed. Since the disk controller can serve only one request at a time, all remaining requests queue up and wait. Efficient scheduling minimizes the total seek distance, reduces response time, and improves overall disk throughput.

Hard drives are among the slowest components in a computer system, so poorly ordered disk access can cause significant performance bottlenecks. When multiple processes issue I/O requests simultaneously, the disk arm may jump unpredictably across tracks, wasting time.

## Key Performance Metrics

- **Seek Time:** Time taken by the disk arm to move to the correct track.
- **Rotational Latency:** Time taken for the desired sector to rotate under the R/W head.
- **Transfer Time:** Time taken to actually read or write data once the head is positioned.
- **Disk Access Time = Seek Time + Rotational Latency + Transfer Time**
- **Total Seek Time = Total Head Movement × Seek Time per Track**
- **Response Time:** The total wait time a request spends in the queue before service begins. Algorithms aim to minimize average response time and its variance.

## Goals of Disk Scheduling

- Minimize total seek time and head movement.
- Maximize disk throughput (requests serviced per unit time).
- Ensure fairness — no request waits indefinitely (starvation prevention).
- Maintain low and consistent response time variance.

## Disk Scheduling Algorithms

### 1. First-Come, First-Served (FCFS)

The simplest algorithm. Requests are processed strictly in arrival order without any reordering.

- **Example:** Request queue `(50, 82, 170, 43, 140, 24, 16, 190)`, head starts at 50.

```text
Total Head Movement = (82-50)+(170-82)+(170-43)+(140-43)+(140-24)+(24-16)+(190-16) = 642
```

- **Advantages:** Fair — every request is guaranteed to be served. No starvation.
- **Disadvantages:** Does not optimize seek distance. Can result in excessive head movement when requests are spread across the disk.

### 2. Shortest Seek Time First (SSTF)

Selects the pending request closest to the current head position, minimizing immediate seek time.

- **Example:** Queue `(82, 170, 43, 140, 24, 16, 190)`, head at 50.

```text
Total Head Movement = (50-43)+(43-24)+(24-16)+(82-16)+(140-82)+(170-140)+(190-170) = 208
```

- **Advantages:** Significantly reduces average seek time compared to FCFS. Higher throughput.
- **Disadvantages:** Causes starvation for requests far from the current head position. High variance in response time.

### 3. SCAN (Elevator Algorithm)

The disk arm moves in one direction, servicing all requests along the way, and reverses at the physical end of the disk, then sweeps back.

- **Example:** Queue `(82, 170, 43, 140, 24, 16, 190)`, head at 50, moving toward larger values.

```text
Total Head Movement = (199-50) + (199-16) = 332
```

- **Advantages:** Low variance in response time. High throughput. Better than FCFS and SSTF for uniform loads.
- **Disadvantages:** Head moves to the disk end even if no pending request exists there. Requests just behind the head direction may experience long waits.

### 4. C-SCAN (Circular SCAN)

An improvement over SCAN. The arm moves only in one direction. After reaching the end, it immediately jumps back to the start of the disk and continues sweeping forward, serving requests in a circular loop.

- **Example:** Queue `(82, 170, 43, 140, 24, 16, 190)`, head at 50, moving toward larger values.

```text
Total Head Movement = (199-50) + (199-0) + (43-0) = 391
```

- **Advantages:** More uniform waiting time than SCAN. Eliminates the long wait imposed on requests at one end of the disk.
- **Disadvantages:** Higher total head movement than SCAN. The return sweep to the start adds extra seek overhead.

### 5. LOOK

Similar to SCAN, but the arm reverses direction at the last pending request in that direction rather than traveling all the way to the physical end of the disk.

- **Example:** Queue `(82, 170, 43, 140, 24, 16, 190)`, head at 50, moving toward larger values.

```text
Total Head Movement = (190-50) + (190-16) = 314
```

- **Advantages:** Eliminates unnecessary head movement beyond the outermost request. Faster than SCAN.
- **Disadvantages:** Waiting time for some requests can still be high depending on request distribution.

### 6. C-LOOK

Combines the circular behavior of C-SCAN with the efficiency of LOOK. The arm moves only up to the last request in the current direction, then jumps to the request at the opposite extreme and continues sweeping.

- **Example:** Queue `(82, 170, 43, 140, 24, 16, 190)`, head at 50, moving toward larger values.

```text
Total Head Movement = (190-50) + (190-16) + (43-16) = 341
```

- **Advantages:** More uniform wait time than LOOK. Avoids traveling to physical disk ends.
- **Disadvantages:** Jump from last to first request still adds circular overhead. Newly added requests may need to wait a full cycle.

### 7. Random Scheduling (RSS)

Selects requests in a random order, irrespective of their position or arrival time. Used primarily for benchmarking, simulation studies, and performance modeling rather than real production systems.

### 8. LIFO (Last-In, First-Out)

Services the most recently arrived request first. Maximizes locality of reference but can cause starvation of older requests. If new requests keep arriving near the current head position, earlier requests may wait indefinitely.

### 9. N-Step SCAN

Requests are divided into fixed-size groups of N. The arm processes all N requests in the current group before picking up new requests. New arrivals during a sweep are held in a separate buffer until the current group is fully serviced. This eliminates arm stickiness and guarantees all requests are served in bounded time.

### 10. F-SCAN

Uses two sub-queues. During a scan pass, all requests in the first queue are serviced. Any new requests arriving during the scan are placed in the second queue. When the first queue is exhausted, the queues are swapped. This design prevents the disk arm from getting stuck near a cluster of frequently arriving requests (arm stickiness), improving fairness.

## Comparison of Disk Scheduling Algorithms

| Algorithm | Seek Optimization | Starvation Risk | Fairness | Best Use Case |
| --- | --- | --- | --- | --- |
| **FCFS** | None | No | High | Low-load systems |
| **SSTF** | High | Yes | Low | Throughput-focused |
| **SCAN** | Moderate | No | Moderate | General purpose |
| **C-SCAN** | Moderate | No | High | Heavy/uniform load |
| **LOOK** | High | No | Moderate | Improved SCAN |
| **C-LOOK** | High | No | High | Improved C-SCAN |
| **N-Step SCAN** | Moderate | No | Very High | Fair, bounded delay |
| **F-SCAN** | Moderate | No | Very High | Prevents arm stickiness |

> **Note:** No single disk scheduling algorithm is universally optimal. SSTF minimizes seek time but risks starvation. SCAN and LOOK balance throughput and fairness. C-LOOK is generally preferred in modern operating systems for combining low head movement with uniform response times.

## Summary

Disk scheduling algorithms determine the order in which pending I/O requests are served by the disk arm. FCFS is simple but inefficient. SSTF minimizes immediate seek time but can starve distant requests. SCAN and C-SCAN sweep the disk like an elevator, while LOOK and C-LOOK optimize further by stopping at the last request rather than the physical disk end. N-Step SCAN and F-SCAN add buffering strategies to prevent arm stickiness and guarantee bounded service. Modern operating systems typically use LOOK or C-LOOK variants to balance throughput, fairness, and seek efficiency.




