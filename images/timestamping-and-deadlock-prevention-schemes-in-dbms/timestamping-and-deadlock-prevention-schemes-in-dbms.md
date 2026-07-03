# Timestamping and Deadlock Prevention Schemes in DBMS

In a database management system, a deadlock occurs when two or more transactions are blocked indefinitely, each waiting for resources held by the other. This circular wait halts system execution and threatens database consistency. Relational databases apply concurrency control protocols, including timestamp-based schemes, to prevent deadlocks and resolve transactional blocks.

## Principles of Deadlocks and Concurrency Control

To prevent database operations from freezing under concurrent schedules, database engines must regulate transaction execution sequences. Timestamp-based deadlock prevention resolves resource allocation conflicts by evaluating transaction ages, ensuring that execution dependencies remain cycle-free.

## Database Timestamps

A timestamp (TS) is a unique logical identifier assigned to a transaction by the database engine at its start. This value represents the transaction's age: older transactions receive smaller timestamps, while newer transactions receive larger timestamps.

### Timestamp Generation Methods

- **Logical Counter**: The database incrementer generates sequentially increasing numbers for each new transaction (e.g., **TS = TS + 1**).
- **System Clock**: The engine assigns timestamps based on the current date and time of the database server.

## Working of Timestamp-Based Scheduling

When a transaction requests read or write access to a data item, the engine compares the transaction's timestamp with the read and write timestamps of the last transaction that successfully accessed that item. If a rule violation is detected (e.g., a younger transaction has already updated the item), the requesting transaction is aborted and rolled back to maintain a serializable, consistent execution order.

## Timestamp-Based Deadlock Prevention Schemes

Database systems implement two primary timestamp-based protocols to dynamically prevent deadlocks:

### 1. Wait-Die Scheme

The Wait-Die scheme is a non-preemptive protocol. It allows older transactions to wait for younger transactions, but aborts and restarts younger transactions if they conflict with older ones.

- **Rule**: If **TS(Ti) &lt; TS(Tj)** (indicating **Ti** is older than **Tj**), **Ti** is allowed to wait. Otherwise, if **Ti** is younger, it aborts ("dies") and restarts later with its original timestamp.
- **Conceptual Case Study**:
- **Mohit (T1)** has a timestamp of **TS(T1) = 15** (older).
- **Akash (T2)** has a timestamp of **TS(T2) = 25** (younger).
- If **Mohit (T1)** requests a lock held by **Akash (T2)**: Since Mohit is older, the engine allows him to wait.
- If **Akash (T2)** requests a lock held by **Mohit (T1)**: Since Akash is younger, he is aborted and restarted later.
- **Result**: Deadlocks are prevented because wait dependencies are strictly one-directional (older waiting for younger), preventing circular cycles.

### 2. Wound-Wait Scheme

The Wound-Wait scheme is a preemptive protocol. It allows younger transactions to wait for older transactions, but older transactions preempt ("wound") younger ones to seize resources.

- **Rule**: If **TS(Ti) &lt; TS(Tj)** (indicating **Ti** is older than **Tj**), **Ti** preempts **Tj**, forcing it to abort and roll back ("wounds" it). Otherwise, if **Ti** is younger, it is allowed to wait.
- **Conceptual Case Study**:
- **Mohit (T1)** has a timestamp of **TS(T1) = 15** (older).
- **Akash (T2)** has a timestamp of **TS(T2) = 25** (younger).
- If **Mohit (T1)** requests a lock held by **Akash (T2)**: Since Mohit is older, he preempts and rolls back Akash.
- If **Akash (T2)** requests a lock held by **Mohit (T1)**: Since Akash is younger, he is allowed to wait.
- **Result**: Older transactions never wait for resources, reducing transaction delay and eliminating deadlocks.

## Deadlock Prevention Without Timestamps

When transaction timestamps are unavailable, databases apply alternative structural algorithms to prevent deadlocks:

### No-Wait Algorithm

If a transaction requests a lock held by another transaction, it is aborted and restarted immediately. Because transactions never enter a waiting queue, circular wait conditions cannot occur.

- **Drawback**: High abort-and-restart frequency increases CPU overhead and degrades throughput.

### Cautious Waiting

When transaction **Ti** requests a lock held by **Tj**:

- If **Tj** is actively executing (not waiting for any lock), **Ti** is allowed to wait.
- If **Tj** is currently blocked waiting for another lock, **Ti** is immediately aborted to prevent a circular wait.
- **Result**: Reduces transaction aborts compared to the No-Wait algorithm while ensuring a deadlock-free execution environment.

## Deadlock Detection Using Wait-For Graphs

When database engines do not apply active prevention, they monitor transactions using a Wait-For Graph (WFG).

- **Nodes**: Active transactions.
- **Directed Edges (Ti -&gt; Tj)**: Indicates **Ti** is waiting for a lock held by **Tj**.
- **Detection**: The database manager periodically scans the WFG. If it detects a cycle, it indicates a deadlock, and the engine selects a transaction to abort to break the cycle.
- **Example Cycle**: **Mohit (T1)** waits for **Akash (T2)**, who waits for **Hemesh (T3)**, who waits for **Mohit (T1)**. The resulting cycle (**T1 -&gt; T2 -&gt; T3 -&gt; T1**) triggers a deadlock rollback.

## Transaction Starvation and FCFS Scheduling

Starvation occurs when a transaction is continually bypassed or repeatedly aborted because the system prioritizes other operations. This is a common issue in deadlock prevention systems where younger transactions are repeatedly aborted.

- **Solution (FCFS Queue)**: Enforcing a First-Come, First-Serve (FCFS) queue ensures that transactions are processed in their arrival order, guaranteeing execution fairness.
- **Role of the Concurrency Control Manager**: The manager coordinates FCFS queues, lock assignments, and timestamp tracking to prevent starvation, eliminate deadlocks, and preserve transaction isolation.

## Comparison of Wait-Die and Wound-Wait Schemes

| Feature | Wait-Die Scheme | Wound-Wait Scheme |
| --- | --- | --- |
| **Waiting Rule** | Older transaction is allowed to wait for a younger transaction | Younger transaction is allowed to wait for an older transaction |
| **Preemption Behavior** | Non-preemptive (cannot seize resources) | Preemptive (older transaction wounds younger transaction) |
| **Abort / Rollback Target** | Younger transaction is aborted if it requests an older lock | Younger transaction is aborted if an older transaction requests its lock |
| **Restart Frequency** | Fewer restarts (older transactions wait instead of aborting) | Higher restarts (older transactions immediately abort younger ones) |
| **Starvation Risk** | High (older transactions can wait in queue indefinitely) | Low (older transactions never wait, ensuring progress) |

> **Key Insight**: Timestamps guarantee a total logical ordering of transactions based on their start times. Concurrency engines use this strict age hierarchy to enforce one-directional waits, making it mathematically impossible for circular wait chains to form, thereby inherently preventing deadlocks.

# Summary

Deadlocks occur when concurrent database transactions enter circular waiting states for shared resources. Database engines prevent these conflicts using timestamp-based prevention schemes like Wait-Die (where older transactions wait and younger ones abort) and Wound-Wait (where older transactions preempt younger ones). مرکزی database applications also implement non-timestamp alternatives like No-Wait or Cautious Waiting, or detect deadlocks dynamically using Wait-For Graphs. The Concurrency Control Manager must coordinate these mechanisms to maximize transaction throughput while preventing deadlock cycles and transaction starvation.




