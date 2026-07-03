# Thomas Write Rule in DBMS

The Thomas Write Rule (TWR) is a timestamp-based concurrency control protocol used in database management systems (DBMS). Developed as an extension of the Basic Timestamp Ordering (Basic TO) protocol, TWR increases concurrency levels and reduces transaction rollbacks by ignoring obsolete write operations instead of immediately aborting the transaction.

## Principles of Obsolete Writes

In traditional Basic TO protocols, if an older transaction attempts to write to a data item that has already been updated by a newer transaction, the write is considered outdated, and the older transaction is aborted. The Thomas Write Rule recognizes that if a newer transaction has already written a value, the older transaction's write is obsolete because it would have been immediately overwritten anyway. Thus, TWR ignores the write operation, allowing the older transaction to continue executing.

## Write Operation Rules in Thomas Write Rule

When transaction **T** requests to write to data item **X** (`W_item(X)`), the database engine evaluates three conditions based on transaction timestamps:

### 1. Transaction Abort and Rollback

- **Condition**: **R_TS(X) &gt; TS(T)**
- **Explanation**: A newer transaction has already read **X**. If **T** writes to **X** now, it would invalidate the newer transaction's read, violating serializability.
- **Action**: Abort and roll back transaction **T**.

### 2. Obsolete Write Ignored

- **Condition**: **W_TS(X) &gt; TS(T)**
- **Explanation**: A newer transaction has already written a value to **X**. Writing **T**'s value now is obsolete because the newer write has already taken effect.
- **Action**: Ignore the write operation and allow transaction **T** to continue executing without updating the database.

### 3. Normal Write Execution

- **Condition**: **R_TS(X) &lt;= TS(T)** and **W_TS(X) &lt;= TS(T)**
- **Explanation**: No newer transaction has read or written to **X**. The write operation is valid and does not violate serializability.
- **Action**: Execute **W_item(X)** and update the metadata write timestamp: **W_TS(X) = TS(T)**.

## Case Study: Ignoring an Outdated Write

We trace two transactions operating on a data item `D101` initialized with **R_TS(D101) = 10** and **W_TS(D101) = 10**:

- **T1** (run by **Mohit**): Older transaction with timestamp **TS(T1) = 20**.
- **T2** (run by **Akash**): Newer transaction with timestamp **TS(T2) = 30**.

The execution schedule unfolds as follows:

| Step | Transaction Operation | Execution Mechanics under Thomas Write Rule |
| --- | --- | --- |
| **1** | **Akash (T2)**: `W_item(D101)` | The engine checks rules: **R_TS(D101) (10) &lt;= 30** and **W_TS(D101) (10) &lt;= 30**. The write is executed. **W_TS(D101)** is updated to **30**. |
| **2** | **Mohit (T1)**: `W_item(D101)` | The engine checks rules: **R_TS(D101) (10) &lt;= 20** (True), but **W_TS(D101) (30) &gt; TS(T1) (20)** (True). The write is obsolete. |
| **3** | **T1**'s write is ignored | Under TWR, **Mohit (T1)**'s write operation is ignored, and the transaction continues running. (Under Basic TO, **Mohit** would have aborted). |

## View Serializability vs. Conflict Serializability

The Thomas Write Rule allows database engines to execute schedules that are view-serializable but not conflict-serializable. Conflicting write-write operations are permitted to execute in non-timestamp order as long as the read values remain consistent.

### Schedule Example

Consider the concurrent schedule between **Mohit (T1, TS=20)** and **Akash (T2, TS=30)**:

| Mohit (T1) | Akash (T2) |
| --- | --- |
| Read(A) |  |
| Write(A) |  |
| Commit |  |
|  | Write(A) |
|  | Commit |

This schedule contains a write-write conflict on `A`. In Basic TO, this conflict violates serializability. By ignoring the write ordering conflict, the Thomas Write Rule allows the execution because it is logically equivalent to the serial schedule **T1 -&gt; T2**, ensuring view serializability.

## Comparison of Basic Timestamp Ordering and Thomas Write Rule

| Feature | Basic Timestamp Ordering (Basic TO) | Thomas Write Rule (TWR) |
| --- | --- | --- |
| **Outdated Write Action** | Aborts and rolls back the older transaction | Ignores the write operation and continues execution |
| **Serializability Type** | Guarantees Conflict Serializability | Guarantees View Serializability (not always conflict serializable) |
| **Transaction Abort Rate** | High (frequent rollbacks on write conflicts) | Low (ignores obsolete write conflicts) |
| **Concurrency Level** | Low | Higher |
| **System Throughput** | Low (degraded by repeated transaction restarts) | High (avoided restarts optimize CPU usage) |

# Summary

The Thomas Write Rule is a modified timestamp-based concurrency control protocol that reduces transaction rollbacks by ignoring obsolete write operations. By bypassing write requests from older transactions when a newer write has already updated the data, TWR avoids unnecessary aborts and increases system throughput. While Basic Timestamp Ordering strictly enforces conflict-serializable schedules, the Thomas Write Rule permits non-conflicting write-write execution paths, guaranteeing view serializability. Relational databases apply this rule to minimize the performance penalty of transaction restarts on write-heavy database tables.




