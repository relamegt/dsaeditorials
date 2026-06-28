# Starvation and Livelock in Process Synchronization

Starvation and livelock are scheduling and coordination anomalies that occur in multi-threaded and distributed systems when processes compete for shared resources. Unlike a deadlock where processes are completely blocked and static, processes in starvation or livelock can remain in ready or active execution states, yet still fail to complete their work due to resource allocation bugs or lock-step synchronization loops.

## Starvation

Starvation (also referred to as indefinite postponement) is a scheduling problem where a process is ready to execute but is repeatedly denied access to CPU time or shared resources because other tasks are continuously prioritized ahead of it.

### Causes of Starvation

- **Unfair Priority Scheduling:** If a system's scheduler dynamically schedules tasks based strictly on priority, a continuous stream of higher-priority processes will monopolize the CPU, leaving lower-priority tasks waiting indefinitely.
- **Asymmetric Resource Allocation:** Processes requiring exclusive locks on critical resources may find those resources continually allocated to tasks with higher operational priority.

### Concrete Scenario: Diagnostics Bandwidth Deprivation

Consider a spacecraft data router coordinating network packet transmissions:

1. **Critical Telemetry Packet (High Priority):** Continuously transmits sensor data to ensure flight stability.
2. **System Diagnostics Logger (Low Priority):** Queues packets to log minor environmental metrics.
3. **Outcome:** Under a heavy telemetry load, the router continually prioritizes telemetry packets. As long as telemetry is active, the diagnostics log packets are bypassed, causing the logging thread to starve.

### Mitigating Starvation

The primary solution to starvation is **Aging**. Aging is a technique where the operating system gradually increases the priority of a process the longer it waits in the ready queue. Eventually, the starved process obtains a high enough priority to preempt other tasks and execute. Other solutions include using first-come-first-serve (FCFS) or round-robin scheduling algorithms.

## Livelock

Livelock is a coordination anomaly where two or more processes continuously change their execution states in response to each other, yet fail to make any forward progress. In a livelock, the processes are not blocked or sleeping; they are actively running, consuming CPU cycles, and modifying variables, but their mutual reactions keep them stuck in an infinite cycle of conflict avoidance.

### Causes of Livelock

- **Over-Politeness (Cooperation Loops):** Algorithms designed to avoid conflicts by yielding resources can fail if multiple processes yield to each other in lockstep.
- **Endless Rollback and Retry:** Automatic recovery mechanisms that abort and retry operations immediately upon conflict can cause processes to collide, abort, and retry in identical intervals.
- **Busy-Waiting Loops:** Threads consuming CPU time to check state variables that fluctuate cyclically without ever resolving.

### Concrete Scenario: Lock-Step Network Collision

Consider two network routers attempting to transmit data packets over a shared physical link:

1. Both routers detect that the link is idle and attempt to transmit a packet simultaneously, causing a collision.
2. Both routers detect the collision, immediately abort their transmission, back off, and wait exactly 1 millisecond.
3. At the end of the 1-millisecond delay, both routers attempt to transmit again at the exact same microsecond, causing another collision.
4. This collision-abort-retry cycle repeats indefinitely. The routers are actively executing code and transmitting, but no data is successfully sent.

### Mitigating Livelock

To resolve livelock, systems introduce **Randomized Back-Off Algorithms** (such as the exponential back-off used in Ethernet CSMA/CD). By introducing randomness into the wait times before retrying a failed operation, processes break their lock-step synchronization, allowing one process to acquire the resource first and proceed.

## Comparison of Starvation and Livelock

| Feature | Starvation | Livelock |
| --- | --- | --- |
| **Definition** | A process is indefinitely delayed because it is constantly bypassed in favor of other tasks. | Processes continuously change states in response to each other without making progress. |
| **Primary Cause** | Unfair scheduling algorithms or resource allocation preferences. | Inter-process coordination loops, excessive yielding, or synchronization lock-step. |
| **Process State** | Ready and waiting to be scheduled (typically blocked or idle). | Actively executing and running (consuming CPU cycles). |
| **System Progress** | The system makes progress; high-priority tasks complete, but the starved task is stuck. | The system is busy executing instructions, but no real work is accomplished by the affected tasks. |
| **Common Example** | A low-priority print job is bypassed by higher-priority print requests. | Two routers continuously backing off and colliding at identical time intervals. |
| **Primary Resolution** | Priority aging or round-robin scheduling. | Randomized back-off delays or randomized retry intervals. |

## Summary

Starvation and livelock represent major concurrency challenges where processes fail to complete execution despite the absence of a standard deadlock. Starvation occurs when a task is ready but denied CPU time due to high-priority resource monopoly, and is resolved using priority aging. Livelock occurs when active processes change states in lockstep to avoid conflict but fail to progress, and is resolved using randomized back-off algorithms. Designing fair scheduling and randomized recovery protocols is essential to ensure progress in multi-threaded operating systems.




