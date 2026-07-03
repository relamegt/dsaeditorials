# Multiple Granularity Locking in DBMS

In a database management system, lock granularity refers to the physical size of the data item upon which a lock is applied. Locking at a very fine granularity (e.g., individual records) maximizes concurrency but increases lock maintenance overhead. Conversely, locking at a coarse granularity (e.g., entire databases) minimizes lock overhead but restricts concurrent access. Multiple Granularity Locking (MGL) balances these trade-offs by organizing database items hierarchically, allowing locks to be applied at multiple levels.

## Principles of Hierarchical Locking

Under Multiple Granularity Locking, database resources are structured as a tree. When a transaction acquires a lock on a parent node, it implicitly holds a lock of the same type on all descendant nodes. This implicit locking eliminates the need to explicitly lock hundreds of child records, significantly reducing overhead for queries that access large portions of a database.

## The Multiple Granularity Hierarchy Tree

A typical database granularity hierarchy can be visualized as a tree:

```Text
Database
 └── Area
      └── File
           └── Record
```

- **Database**: The entire database system (coarsest level).
- **Area**: Logical database segments.
- **File**: Groups of records.
- **Record**: Individual data entries (finest level).

### Custom System Directory Tree Structure

For this guide, we map this standard database hierarchy to a custom Project System Directory:

- **Root Level (SystemDirectory)**: Represents the entire database system.
- **Level 1 (ProjectDivision)**: Logical database segments (e.g., `DivAlpha`, `DivBeta`).
- **Level 2 (DataRegistry)**: Groups of records stored in files (e.g., `RegOne`, `RegTwo`).
- **Level 3 (CustodianRecord)**: Individual records containing specific custodian details (e.g., `RecMohit`, `RecAkash`, `RecHemesh`, `RecAbhiram`, `RecSiddu`).

## Intention Lock Modes

To support implicit locking without requiring child scans, MGL introduces intention locks. A transaction places an intention lock on a parent node to declare its plan to lock descendant nodes explicitly:

- **Intention-Shared (IS)**: Indicates that the transaction plans to acquire shared (S) locks at a lower level of the tree.
- **Intention-Exclusive (IX)**: Indicates that the transaction plans to acquire shared (S) or exclusive (X) locks at a lower level of the tree.
- **Shared & Intention-Exclusive (SIX)**: Locks the entire subtree rooted at that node in shared (S) mode, while indicating that explicit exclusive (X) locks will be acquired on child nodes at a lower level.

## Locking Protocol Rules

To ensure serializability, transactions must follow these six MGL rules:

1. **Root Lock Requirement**: Transactions must lock the root node of the hierarchy first, in any lock mode.
2. **Shared Lock Parent Rule**: A transaction can acquire a Shared (S) or Intention-Shared (IS) lock on a node only if the node's parent is currently locked in either IS or IX mode.
3. **Exclusive Lock Parent Rule**: A transaction can acquire an Exclusive (X), Intention-Exclusive (IX), or Shared & Intention-Exclusive (SIX) lock on a node only if the node's parent is currently locked in either IX or SIX mode.
4. **Top-Down Lock Acquisition**: Transactions must request locks starting from the root and proceeding down to the leaf nodes.
5. **Bottom-Up Lock Release**: Transactions must release locks starting from the leaf nodes and proceeding up to the root.
6. **Child Lock Constraint**: A node can only be unlocked if all of its children have been successfully unlocked first.

Additionally, transactions must follow the Two-Phase Locking (2PL) protocol, separating lock acquisition (growing phase) from lock release (shrinking phase).

## Case Study Transaction Schedules

We analyze four concurrent transactions operating on the `SystemDirectory -> DivAlpha -> RegOne` subtree:

### Transaction T1 (Read Operation)

Mohit (T1) wants to read the record `RecAkash` located in data registry `RegOne`.

- **Lock Path**: T1 locks `SystemDirectory` in **IS** mode, locks `DivAlpha` in **IS** mode, locks `RegOne` in **IS** mode, and finally locks `RecAkash` in **S** mode.

### Transaction T2 (Update Operation)

Akash (T2) wants to modify record `RecHemesh` located in data registry `RegOne`.

- **Lock Path**: T2 locks `SystemDirectory` in **IX** mode, locks `DivAlpha` in **IX** mode, locks `RegOne` in **IX** mode, and finally locks `RecHemesh` in **X** mode.

### Transaction T3 (Subtree Read)

Hemesh (T3) wants to read all records inside data registry `RegOne`.

- **Lock Path**: T3 locks `SystemDirectory` in **IS** mode, locks `DivAlpha` in **IS** mode, and finally locks `RegOne` in **S** mode. This implicitly locks all records under `RegOne` (including `RecAkash`, `RecHemesh`, etc.) in shared mode.

### Transaction T4 (Root Read)

Abhiram (T4) wants to read the entire database.

- **Lock Path**: T4 locks the root `SystemDirectory` in **S** mode, implicitly locking the entire database in shared mode.

### Concurrency Compatibility Analysis

Based on MGL rules, we evaluate which transactions can run in parallel:

- **T1, T3, and T4**: Can execute concurrently because their lock modes (**IS** and **S**) are fully compatible on all shared parent nodes.
- **T1 and T2**: Can execute concurrently. Their lock modes on the parent nodes are compatible (**IS** and **IX**). On the leaf level, T1 holds an **S** lock on `RecAkash` and T2 holds an **X** lock on `RecHemesh`. Since they operate on different record nodes, their locks do not conflict.
- **T2 and T3**: Cannot execute concurrently. T3 requests an **S** lock on file `RegOne`, but T2 holds an **IX** lock on `RegOne`. Since **S** and **IX** are incompatible, T3 must wait until T2 completes and releases its locks.
- **T2 and T4**: Cannot execute concurrently. T4 requests an **S** lock on the root `SystemDirectory`, which conflicts with the **IX** lock held by T2.

## Multiple Granularity Lock Compatibility Matrix

Before granting a lock request, the database engine checks if it is compatible with existing locks held by other transactions:

| Existing \ Requested | Intention-Shared (IS) | Intention-Exclusive (IX) | Shared (S) | Shared & Intention-Exclusive (SIX) | Exclusive (X) |
| --- | --- | --- | --- | --- | --- |
| **IS** | **Compatible** | **Compatible** | **Compatible** | **Compatible** | Incompatible |
| **IX** | **Compatible** | **Compatible** | Incompatible | Incompatible | Incompatible |
| **S** | **Compatible** | Incompatible | **Compatible** | Incompatible | Incompatible |
| **SIX** | **Compatible** | Incompatible | Incompatible | Incompatible | Incompatible |
| **X** | Incompatible | Incompatible | Incompatible | Incompatible | Incompatible |

# Summary

Multiple Granularity Locking (MGL) balances database locking overhead against transaction concurrency by organizing data items into a tree hierarchy. Coarser locks at the database or area level implicitly secure descendant records, while intention locks like IS, IX, and SIX alert concurrent transactions to lower-level lock requests without requiring extensive scans. Transactions must acquire locks top-down and release them bottom-up while adhering to Two-Phase Locking rules. Selecting MGL allows databases to optimize lock footprints dynamically, maximizing performance for both high-concurrency record writes and large-scale analytical scans.




