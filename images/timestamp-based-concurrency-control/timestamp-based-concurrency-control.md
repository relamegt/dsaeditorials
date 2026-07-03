# Timestamp-Based Concurrency Control

In database management systems, timestamp-based concurrency control is a lock-free protocol used to ensure conflict serializability among concurrent transactions. Instead of restricting data access using locks, the database engine assigns unique chronological timestamps to transactions upon system entry, using these timestamps to determine the serializability order of execution.

## Principles of Timestamp Ordering

Every transaction **T** receives a unique timestamp **TS(T)** when it begins. The protocol dictates that older transactions (those with smaller timestamps) are given priority over newer transactions. The database engine resolves conflicting read and write operations by ensuring that they execute in strict timestamp order, preventing deadlocks by rolling back younger transactions when conflicts occur.

## Database Item Timestamps

To detect serializability violations, each data item **X** in the database maintains two metadata timestamps:

- **R_TS(X)**: Read Timestamp. Records the timestamp of the youngest transaction (largest timestamp) that has successfully read data item **X**.
- **W_TS(X)**: Write Timestamp. Records the timestamp of the youngest transaction (largest timestamp) that has successfully written to data item **X**.

## The Basic Timestamp Ordering Protocol

Under the Basic Timestamp Ordering (Basic TO) protocol, every read or write request compared against data item **X** is evaluated using specific logical checks:

### Read Operation Rule

When transaction **T** requests to read data item **X** (`R_item(X)`):

- If **W_TS(X) &gt; TS(T)**, the read is rejected. Transaction **T** is attempting to read an older version of data that has already been overwritten by a newer transaction. The database engine aborts and rolls back **T**.
- If **W_TS(X) &lt;= TS(T)**, the read is permitted. The database engine updates the read metadata to: **R_TS(X) = max(R_TS(X), TS(T))**.

### Write Operation Rule

When transaction **T** requests to write to data item **X** (`W_item(X)`):

- If **R_TS(X) &gt; TS(T)** or **W_TS(X) &gt; TS(T)**, the write is rejected. A newer transaction has already read or written to the data item, making **T**'s update outdated. The database engine aborts and rolls back **T**.
- Otherwise, the write is permitted. The database engine updates the write metadata to: **W_TS(X) = TS(T)**.

### Case Study Conflict Execution Scenario

Consider a data item `D101` initialized with timestamps **R_TS(D101) = 150** and **W_TS(D101) = 150**. We track three transactions:

- **T1** (run by **Mohit**) with timestamp **TS(T1) = 201**.
- **T2** (run by **Akash**) with timestamp **TS(T2) = 205**.
- **T3** (run by **Hemesh**) with timestamp **TS(T3) = 210**.

1. **Mohit (T1)** reads `D101`. Since **W_TS(D101) (150) &lt;= TS(T1) (201)**, the read is granted. The read timestamp is updated: **R_TS(D101) = max(150, 201) = 201**.
2. **Hemesh (T3)** writes to `D101`. The engine checks the conditions:

- **R_TS(D101) (201) &lt;= TS(T3) (210)** (True)
- **W_TS(D101) (150) &lt;= TS(T3) (210)** (True)

   The write is granted, and the write timestamp is updated: **W_TS(D101) = 210**.

1. **Akash (T2)** tries to read `D101`. The engine checks the read rule:

- **W_TS(D101) (210) &gt; TS(T2) (205)** (True)

   Because a younger transaction (**Hemesh**) has already written to `D101`, **Akash's** read request is rejected. The database engine aborts and rolls back **Akash (T2)**.

## The Strict Timestamp Ordering Protocol

While the Basic TO protocol ensures conflict serializability, it is susceptible to cascading rollbacks. If transaction **T1** writes an uncommitted value that is subsequently read by **T2**, and **T1** aborts, then **T2** must also be aborted. The Strict Timestamp Ordering protocol solves this problem by delaying conflicting operations.

### Avoiding Cascading Rollbacks

To prevent cascading rollbacks, strict timestamp ordering forces transactions to wait. An operation (read or write) on data item **X** is delayed until the transaction that holds the current write or read lock commits or aborts.

### Rules for Strict Read Operation

Transaction **T** can read data item **X** only if:

- **W_TS(X) &lt;= TS(T)**, and
- The transaction that performed the last write on **X** has successfully committed. If it is still active, **T**'s read is delayed.

### Rules for Strict Write Operation

Transaction **T** can write to data item **X** only if:

- **R_TS(X) &lt;= TS(T)** and **W_TS(X) &lt;= TS(T)**, and
- All previous transactions that have read or written to **X** have successfully committed. If any are still active, **T**'s write is delayed.

## Performance Trade-Offs of Timestamp Ordering

Implementing a lock-free protocol affects transaction speed and throughput:

### Advantages

- **Conflict-Serializable**: Guarantees serializable execution schedules.
- **Deadlock-Free**: Since transactions never wait on locks in Basic TO, circular wait conditions cannot occur.
- **No Lock Management Overhead**: Bypasses the memory overhead of maintaining lock tables.
- **Predictable Execution**: Operations follow a clear chronological sequence based on transaction arrival times.

### Disadvantages

- **Cascading Rollbacks**: Basic TO can trigger extensive rollbacks if uncommitted updates are read by newer transactions.
- **Starvation Risk**: If a transaction is repeatedly aborted and restarted with a new timestamp, it can suffer from write starvation.
- **Metadata Update Overhead**: Every read and write transaction requires updating the item's `R_TS` and `W_TS` values, increasing metadata write volume.

## Comparison of Basic and Strict Timestamp Ordering

| Feature | Basic Timestamp Ordering | Strict Timestamp Ordering |
| --- | --- | --- |
| **Conflict Resolution** | Aborts and rolls back the younger transaction immediately | Delays conflicting operations until the older transaction commits |
| **Cascading Rollback Risk** | High (aborted writes force dependent readers to abort) | None (guarantees cascadeless schedules) |
| **Transaction Latency** | Low (no delay queues) | High (operations wait for commits) |
| **Throughput Performance** | High under low contention, degrades under high conflicts | Stable but limited by serialization delay queues |
| **Transaction Starvation** | Possible (restarted transactions get new timestamps) | Low (older delayed transactions retain priority) |

# Summary

Timestamp-based concurrency control is a lock-free mechanism that enforces serializability by ordering transaction execution according to chronological timestamps. The database engine compares transaction timestamps against read and write timestamps on individual data items, aborting and restarting transactions that violate chronological order. While Basic Timestamp Ordering ensures conflict serializability without deadlock risks, it can lead to cascading rollbacks. Strict Timestamp Ordering delays conflicting operations until older transactions commit, eliminating cascading rollbacks at the cost of execution delays. Relational engines weigh these latency trade-offs against traditional lock-based protocols to maximize transactional throughput.




