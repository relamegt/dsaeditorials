# Graph-Based Concurrency Control Protocols

In database management systems (DBMS), graph-based concurrency control protocols manage conflicts between concurrent transactions using a directed graph. By representing transactions as nodes and conflict dependencies as directed edges, these protocols ensure conflict serializability and database consistency by keeping the serialization graph acyclic.

## Principles of Graph-Based Serialization

When multiple transactions overlap in time, the database engine builds a serialization graph to monitor dependencies. If adding a new lock request creates a cycle in the graph, a deadlock is detected. To resolve the conflict, the DBMS rolls back one of the transactions to break the cycle, ensuring that the serialization order remains directed and acyclic.

## Partial Ordering and the Database Graph

Before applying a graph-based protocol, the system defines a partial ordering on the database items. Let the set of database items be **D = {d1, d2, ..., dn}**. If **di -&gt; dj**, then any transaction that accesses both items must access **di** before it can access **dj**. This ordering forms a Directed Acyclic Graph (DAG) known as the Database Graph.

## The Tree-Based Locking Protocol

The Tree Protocol is a specific graph-based concurrency control method that organizes database items in a hierarchical tree structure. It guarantees conflict serializability and prevents deadlocks without following the strict growing and shrinking phases of Two-Phase Locking (2PL).

### Core Rules of the Tree Protocol

1. **Exclusive Locks Only**: Transactions can only request exclusive (X) locks; shared (S) locks are not used.
2. **Arbitrary Initial Lock**: A transaction can lock any data item as its first lock.
3. **Parent-Lock Requirement**: After the first lock, a transaction can lock a data item only if it currently holds a lock on that item's parent in the database graph.
4. **Flexible Unlocking**: Data items can be unlocked at any time during execution.
5. **No Relocking**: Once a transaction unlocks a data item, it cannot lock that same item again.

### Analytical Case Study Schedule

Consider a database graph structured as a tree with three distinct branches:

- **Root**: `M`
- **Left Branch**: `M -> N -> X`
- **Middle Branch**: `M -> O -> Y`
- **Right Branch**: `M -> P -> Z`

We track three concurrent transactions: T1 (run by **Mohit**), T2 (run by **Akash**), and T3 (run by **Hemesh**). The schedule executes as follows:

| Mohit (T1) | Akash (T2) | Hemesh (T3) |
| --- | --- | --- |
| Lock-X(M) |  |  |
| Lock-X(O) |  |  |
| Lock-X(Y) |  |  |
| Unlock-X(M) |  |  |
|  |  | Lock-X(M) |
|  |  | Lock-X(N) |
| Unlock-X(O) |  |  |
|  | Lock-X(O) |  |
|  | Lock-X(Y) |  |
| Unlock-X(Y) |  |  |
|  | Unlock-X(O) |  |
|  | Unlock-X(Y) |  |
|  |  | Lock-X(X) |
|  |  | Unlock-X(M) |
|  |  | Unlock-X(N) |
|  |  | Unlock-X(X) |

#### Serializability Analysis
This schedule is conflict serializable. By tracking conflicts on individual data items:

- On `M`: **Mohit** (T1) locks it first, then **Hemesh** (T3). This creates the dependency **T1 -&gt; T3**.
- On `O`: **Mohit** (T1) locks it first, then **Akash** (T2). This creates the dependency **T1 -&gt; T2**.
- On `Y`: **Mohit** (T1) locks it first, then **Akash** (T2). This matches the dependency **T1 -&gt; T2**.

Since there are no cycles in the dependency graph, the schedule is conflict serializable, yielding the execution paths **T1 -&gt; T2** and **T1 -&gt; T3**. All transactions strictly follow the tree protocol rules, locking parent nodes before child nodes and never relocking nodes once unlocked.

## Performance Evaluation of the Tree Protocol

The Tree Protocol introduces several design trade-offs:

### Advantages of Tree Locking

- **Deadlock-Free Execution**: Because the hierarchical database graph prevents circular wait chains, transactions cannot deadlock, eliminating rollback overhead.
- **Increased Concurrency**: Unlocking data items early reduces lock hold times and transaction wait times.
- **Schedules Outside 2PL**: Allows certain conflict-serializable schedules that are blocked under standard 2PL protocols.

### Drawbacks of Tree Locking

- **No Recoverability Guarantee**: Unlocking items early can cause cascading rollbacks if a parent transaction aborts, unless strict commit delays are applied.
- **Lock Overhead**: Transactions may need to lock parent nodes they do not need simply to reach a target child node.
- **Restricted Access Paths**: Some valid parallel schedules allowed in 2PL are blocked by the strict tree-hierarchy path.

## Comparison of Tree Protocol and Two-Phase Locking (2PL)

| Feature | Tree Protocol | Two-Phase Locking (2PL) |
| --- | --- | --- |
| **Lock Types Allowed** | Only Exclusive (X) write locks | Both Shared (S) and Exclusive (X) locks |
| **Lock Release Timing** | Locks can be released at any time during execution | No locks can be released until the shrinking phase starts |
| **Deadlock Risk** | None (guaranteed deadlock-free by tree hierarchy) | High (requires deadlock detection and resolution) |
| **Recoverability** | Not guaranteed (subject to cascading rollbacks) | Guaranteed under Strict and Rigorous 2PL variants |
| **Lock Overhead** | High (must lock parent nodes to access child nodes) | Low (only locks the specific target data items) |

# Summary

Graph-based concurrency control protocols utilize database graphs to manage transaction conflicts and ensure conflict serializability. The Tree Protocol implements a hierarchical locking structure where transactions can only acquire exclusive locks and must lock a node's parent before accessing the child node. While the Tree Protocol provides deadlock-free execution and reduces transaction wait times by allowing early unlocking, it does not guarantee recoverability, which can lead to cascading rollbacks. Relational databases evaluate tree protocols against traditional 2PL to balance deadlock prevention against the lock overhead of hierarchical database graphs.




