# Concurrency Control in DBMS

Concurrency control is a database mechanism that allows multiple transactions to execute simultaneously while preserving ACID properties (Atomicity, Consistency, Isolation, and Durability). When multiple users or processes execute read and write transactions concurrently, the DBMS uses concurrency control to maintain data integrity, prevent data corruption, and ensure system reliability.

## Principles of Transaction Concurrency

In a multi-user database environment, overlapping transaction schedules can cause conflicts over shared data blocks. Concurrency control manages these conflicts, ensuring that the database remains in a consistent state and preventing transactions from overwriting or reading partial modifications.

## Relational Concurrency Problems

When database transactions run concurrently without proper concurrency controls, three primary problems occur:

### Dirty Read

A dirty read occurs when a transaction reads uncommitted data modified by another transaction. If the first transaction subsequently rolls back, the data read by the second transaction becomes invalid.

- *Conceptual Example*: Database operator **Hemesh** starts a transaction to update a device location from 'Chicago' to 'Boston'. Before **Hemesh** commits this update, **Abhiram** reads the location as 'Boston'. If **Hemesh's** transaction fails and rolls back to 'Chicago', the value **Abhiram** read is incorrect.

### Lost Update

A lost update occurs when two transactions update the same data item simultaneously, and the later transaction overwrites the changes made by the earlier transaction.

- *Conceptual Example*: Custodian **Mohit** and administrator **Akash** retrieve the allocation status of device `901` at the same time. Both attempt to update the allocation to different departments. Without concurrency control, **Akash's** commit overwrites **Mohit's** commit, causing **Mohit's** update to be permanently lost.

### Inconsistent Read

An inconsistent (or non-repeatable) read occurs when a transaction reads a data item multiple times and receives different values because another transaction modified and committed that data in between the reads.

- *Conceptual Example*: An inventory audit transaction reads the total device count. Before the audit completes, a separate transaction adds a new device and commits. If the audit transaction reads the device count again, it will see a different number, violating isolation.

## Concurrency Control Protocols

Database engines implement concurrency control protocols to dictate transaction schedules and guarantee serializability:

### Lock-Based Concurrency Control

This protocol restricts access to data items using locks during transaction execution.

- **Shared Lock (S-Lock)**: Allows multiple transactions to read a data item concurrently but prevents updates.
- **Exclusive Lock (X-Lock)**: Grants a single transaction exclusive write access, blocking all other read or write requests.
- **Two-Phase Locking (2PL)**: A protocol that guarantees serializability by dividing a transaction's locking behavior into two phases: a growing phase (obtaining locks) and a shrinking phase (releasing locks). Once a transaction releases a lock, it cannot acquire any new ones.

### Timestamp-Based Concurrency Control

This protocol orders transaction execution using logical start times instead of locks.

- **Timestamp Ordering**: Each transaction receives a unique timestamp when it begins. The database engine resolves conflicts by ensuring that older transactions (with earlier timestamps) always execute before newer transactions, rolling back and restarting any transactions that violate this order.

## Transaction Scheduling Properties

In addition to serializability, database protocols enforce scheduling rules to ensure safe database recovery:

### Recoverable Schedules

A schedule is recoverable if a transaction commits only after all other transactions it depends on have committed. This rule ensures that if a parent transaction rolls back, the dependent transaction can also be safely rolled back without leaving orphaned or corrupt records.

### Cascadeless Schedules

A schedule is cascadeless if a transaction is allowed to read a data item only after the previous transaction that modified it has committed. This structure completely avoids cascading rollbacks, where one failed transaction forces a chain reaction of rollbacks across other transactions.

## Performance Trade-Offs of Concurrency Control

Enforcing transaction safety involves balancing system speed against data isolation:

### System Advantages

- **Reduced Wait Times**: Allowing simultaneous reads and writes reduces database idle times.
- **Improved Throughput**: Hardware resources are utilized efficiently, letting the system process more queries per second.
- **Responsive Interactions**: Users experience faster response times when querying shared records.

### System Disadvantages

- **Protocol Overhead**: Tracking lock tables and managing transaction timestamps consumes memory and CPU resources.
- **Deadlock Risks**: Circular locking chains can cause deadlocks, where transactions wait indefinitely for each other to release locks, requiring the database engine to rollback one of the transactions.
- **Reduced Concurrency**: High levels of locking can force transactions to execute sequentially, limiting system scaling.

## Comparison of Concurrency Protocols

| Feature | Lock-Based Concurrency Control | Timestamp-Based Concurrency Control |
| --- | --- | --- |
| **Control Mechanism** | Restricts data access using Shared and Exclusive locks | Orders transactions using unique start-time stamps |
| **Deadlock Risk** | High (circular waiting can occur during lock requests) | None (transactions are rolled back and restarted instead of waiting) |
| **Conflict Resolution** | Blocks and delays conflicting transaction requests | Rolls back and restarts transactions that violate timestamp order |
| **Implementation Overhead** | High memory usage to maintain active lock tables | High CPU usage to execute rollbacks and transaction restarts |
| **Cascading Rollback Risk** | Possible (prevented by strict Two-Phase Locking) | Possible (prevented by delaying read operations) |

# Summary

Concurrency control protocols ensure that multiple transaction schedules execute safely without violating database ACID properties or creating dirty reads, lost updates, and inconsistent reads. Database systems enforce serializability using lock-based protocols like Two-Phase Locking (2PL) or logical ordering schemes like Timestamp Ordering. Additionally, systems enforce recoverable and cascadeless schedules to protect transaction recovery and prevent cascading rollbacks during failures. Selecting the appropriate protocol requires balancing transaction throughput against locking overhead and deadlock risks.




