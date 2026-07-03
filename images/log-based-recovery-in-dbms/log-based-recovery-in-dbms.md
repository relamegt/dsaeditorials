# Log-Based Recovery in DBMS

In a database management system, log-based recovery is a collection of techniques used to restore a database to a consistent state following a system crash or hardware failure. By recording all transaction operations sequentially on stable storage before modifying the database, the DBMS creates a reliable execution trail that can be replayed or reverted during recovery.

## Principles of Database Recovery and Logs

To prevent database corruption and preserve transactional ACID properties, the database engine must ensure that committed updates are never lost and that incomplete transactions are completely rolled back. The database log serves as this execution log, documenting every read, write, commit, and abort action.

## Structure of Log Records

A transaction log is a sequence of records. Each record documents a specific transaction milestone or data update:

### Start Log

Indicates that a specific transaction has begun execution.

- **Format**: `<Tn, Start>` (where `Tn` is the transaction ID).
- **Example**: `<T1, Start>` indicates that Transaction 1 has started.

### Operation Log

Records a data modification, capturing the state of the data item before and after the write operation.

- **Format**: `<Tn, Attribute, Old_Value, New_Value>`
- **Example**: `<T1, DepotLocation, 'Chicago', 'Dallas'>` shows that Transaction 1 updated the `DepotLocation` attribute from `'Chicago'` to `'Dallas'`.

### Commit Log

Indicates that a transaction has successfully finished and all its updates are permanently applied.

- **Format**: `<Tn, Commit>`
- **Example**: `<T1, Commit>` signifies that Transaction 1 has completed successfully.

## Primary Log-Based Recovery Operations

When the system restarts after a crash, the recovery manager evaluates the log file to perform two key operations:

### Undo Operation

The undo operation reverses the changes made by an uncommitted transaction to remove partial or dirty updates from disk.

- **Trigger**: Applied to transactions that started but were not committed or aborted before the crash.
- **Action**: Restores the data items to their original values using the `Old_Value` field in the log.
- **Conceptual Case Study**:
- **Initial State**: A device count is `12`.
- Transaction T1 (run by **Mohit**) updates the count to `15`, generating the log `<T1, DeviceCount, 12, 15>`.
- If the database crashes before T1 commits, the recovery manager executes `undo(T1)`, reverting the count to `12` and appending `<T1, Abort>` to the log.

### Redo Operation

The redo operation reapplies the changes made by a committed transaction to ensure they are written to disk.

- **Trigger**: Applied to transactions that committed before the crash but whose modified buffer pages were not yet flushed to physical storage.
- **Action**: Overwrites the data items on disk using the `New_Value` field in the log.
- **Conceptual Case Study**:
- **Initial State**: A device count is `8`.
- Transaction T2 (run by **Akash**) updates the count to `10`, generating the logs: `<T2, Start>`, `<T2, DeviceCount, 8, 10>`, and `<T2, Commit>`.
- If the system crashes, the recovery manager executes `redo(T2)`, reapplying the write to set the count on disk to `10`.

### Undo-Redo Combined Scenario

Suppose a database log contains the following sequence:

- `<T1, Start>`, `<T1, DeviceCount, 12, 15>`, `<T2, Start>`, `<T2, DeviceCount, 8, 10>`, `<T2, Commit>`
- **Analysis**: At the time of the crash, **Akash (T2)** has committed, while **Mohit (T1)** has not.
- **Action**: The recovery manager performs `undo(T1)` to revert the device count to `12`, and performs `redo(T2)` to ensure the device count is set to `10`.

## Approaches to Modifying the Database

Relational database engines use two primary methods to apply transaction updates:

### 1. Immediate Modification Approach

In this approach, updates to the database are written directly to disk while the transaction is still executing, even before it commits.

- **Execution Step**:

1. Transaction T0 starts: `<T0, Start>` is logged.
2. T0 updates device count `A` from 200 to 180: `<T0, A, 200, 180>` is logged and written to memory/disk.
3. T0 updates device count `B` from 300 to 350: `<T0, B, 300, 350>` is logged and written to memory/disk.
4. T0 commits: `<T0, Commit>` is logged.
5. Transaction T1 starts: `<T1, Start>` is logged.
6. T1 updates device count `C` from 100 to 90: `<T1, C, 100, 90>` is logged and written.
7. Crash occurs before T1 commits.

- **Recovery Requirement**: Because changes are written immediately, recovery requires **both** undo operations (to revert the uncommitted T1) and redo operations (to reapply the committed T0).

### 2. Deferred Modification Approach

In this approach, database updates are postponed until the transaction successfully commits. While the transaction is running, updates are recorded only in the log file, leaving the physical database unchanged.

- **Execution Step**:

1. Transaction T0 starts: `<T0, Start>` is logged.
2. T0 intends to update device count `A` from 500 to 450: `<T0, A, 500, 450>` is logged, but the database value remains 500.
3. T0 intends to update device count `B` from 300 to 350: `<T0, B, 300, 350>` is logged, but the database value remains 300.
4. T0 commits: The changes are written to the database (`A = 450`, `B = 350`) and `<T0, Commit>` is logged.

- **Recovery Requirement**: Since no uncommitted changes are ever written to disk, the database never contains dirty data. Recovery is simpler, requiring **only** redo operations for committed transactions.

## Recovery Execution and Checkpointing

Scanning the entire log file from the beginning of time during a recovery is highly inefficient. Database engines use checkpoints to streamline this process.

### The Checkpoint Mechanism

A checkpoint is a periodic operation where the DBMS flushes all modified buffer blocks and log records from memory to disk. The engine then writes a checkpoint record to the log: `<checkpoint L>` (where `L` is a list of all active transactions at the time of the checkpoint).

### Recovery Algorithm Steps

When a crash occurs, the recovery manager restores the database using these steps:

1. **Find Checkpoint**: Scans the log backward to locate the most recent `<checkpoint L>` record.
2. **Identify Active Transactions**: Continues scanning backward to the start log record of the oldest active transaction in list `L`. Any transactions that completed before this point are safely ignored.
3. **Execute Recovery**:

- For transactions with a commit log: Reapply updates using **Redo**.
- For transactions without a commit log: Revert changes using **Undo** (in immediate modification environments).
- *Example Scenario*: A checkpoint occurs while transactions `T45` and `T47` are active. Transactions `T1` through `T44` completed before the checkpoint and are ignored. Transactions `T45` through `T60` (which were active during or started after the checkpoint) are scanned. If a transaction committed, the engine executes a redo; if it remained incomplete, the engine executes an undo.

## Performance Trade-Offs of Log-Based Recovery

Enforcing recovery safety introduces system overhead and design challenges:

### Advantages of Log Recovery

- **Guaranteed Durability**: Committed transactions are never lost, ensuring durability even during severe power crashes.
- **Fast Replay Speed**: Sequential log replay is faster than alternative table-scanning recovery methods.
- **Incremental Backups**: Backups only need to save the log modifications written since the last checkpoint rather than the entire database.

### Disadvantages of Log Recovery

- **Disk I/O Overhead**: Logging every operation increases write latency, which can degrade database performance.
- **Storage Consumption**: Log files can grow rapidly in transaction-heavy databases, requiring automated archiving.
- **System Complexity**: Designing and managing checkpoint intervals and log-flushing schemes is complex.

## Comparison of Immediate and Deferred Modifications

| Feature | Immediate Modification | Deferred Modification |
| --- | --- | --- |
| **Database Update Timing** | Applied to disk during transaction execution | Postponed and applied to disk only after commit |
| **Undo Operation Needed** | Yes (required to roll back uncommitted changes) | No (uncommitted changes are never written to disk) |
| **Redo Operation Needed** | Yes (required to flush committed buffer updates) | Yes (required to apply committed log entries to disk) |
| **Recovery Process** | Complex (requires both undo and redo passes) | Simpler (requires only a single redo pass) |
| **Log Writing Priority** | Logs must be written to disk before database blocks | Logs must be written to disk before database blocks |

# Summary

Log-based recovery protects database integrity by documenting all transaction steps on stable storage before modifying database blocks. Relational engines execute undo operations to remove incomplete changes and redo operations to reapply committed updates. While immediate modification writes transaction changes to disk immediately (requiring both undo and redo recovery), deferred modification postpones database updates until commit, simplifying recovery to redo-only operations. Database systems use periodic checkpoints to limit log scanning distances, optimizing crash recovery speeds while preserving data durability.




