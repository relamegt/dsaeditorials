# Lock-Based Concurrency Control Protocols

In database management systems, a lock is a mechanism used to control concurrent access to shared data. By restricting access to one transaction at a time, lock-based protocols maintain database serializability, enforce transaction isolation, and prevent write conflicts such as lost updates or dirty reads.

## Principles of Database Locking

Lock-based protocols require that a transaction acquire a lock on a data item before performing read or write operations on it. The transaction must hold the lock until the operation finishes, releasing it based on the rules of the specific protocol in use.

## Classification of Lock Types

Database engines use two primary types of locks to regulate data access:

### Shared Lock (S)

A shared lock (or read lock) allows a transaction to read a data item but prevents it from modifying the value. Multiple transactions can hold shared locks on the same data item simultaneously, supporting concurrent read access.

- **Request Command**: `lock-S` instruction.

### Exclusive Lock (X)

An exclusive lock (or write lock) grants a transaction sole access to both read and update a data item. When an exclusive lock is held on an item, no other transaction can obtain any lock (shared or exclusive) on that same item.

- **Request Command**: `lock-X` instruction.

## The Lock Compatibility Matrix

To grant a lock, the DBMS checks if the requested lock mode is compatible with existing locks held by other transactions on the same data item:

| Requested \ Existing | Shared (S) | Exclusive (X) |
| --- | --- | --- |
| **Shared (S)** | **Compatible** (Granted) | Incompatible (Blocked) |
| **Exclusive (X)** | Incompatible (Blocked) | Incompatible (Blocked) |

If the requested lock is incompatible, the requesting transaction must wait in a queue until the holding transaction releases its lock.

## Lock-Based Concurrency Protocols

Database systems implement different locking protocols to dictate when locks are acquired and released:

### 1. Simplistic Lock Protocol

In this protocol, a transaction must lock a data item immediately before performing an insert, delete, or update, and unlock it as soon as that specific operation completes.

- *Conceptual Example*: A database has a data item `D101 = 10`. Transaction T1 (run by **Mohit**) wants to update `D101`, and Transaction T2 (run by **Akash**) wants to read `D101`. Mohit requests and gets an exclusive lock on `D101`, updating it to `20`. Akash requests a shared lock to read `D101` but is blocked until Mohit completes and releases the lock. While simple, this protocol does not prevent cascading rollbacks or deadlocks.

### 2. Pre-Claiming Lock Protocol

The pre-claiming protocol avoids deadlocks by requiring a transaction to declare and request all necessary locks before it begins execution. The transaction runs only if all requested locks are granted simultaneously; otherwise, it waits.

- *Conceptual Example*: Transaction T1 (run by **Mohit**) declares that it needs an exclusive lock on `D101` and a shared lock on `D102`. Since both are free, they are granted, and Mohit executes. Meanwhile, T2 (run by **Akash**) requests a shared lock on `D101`. Because Mohit holds the exclusive lock, Akash's request is denied, and T2 must wait until Mohit releases all locks upon completion.

### 3. Two-Phase Locking Protocol (2PL)

The Two-Phase Locking protocol guarantees transaction serializability by separating locking actions into two distinct phases:

- **Growing Phase**: The transaction can acquire new locks but is not allowed to release any existing locks.
- **Shrinking Phase**: The transaction can release locks but is not allowed to acquire any new locks.

### 4. Strict Two-Phase Locking Protocol (Strict 2PL)

Strict 2PL is a stricter version of 2PL. In addition to following the two-phase rule, it requires that all exclusive locks (write locks) held by a transaction must be retained until the transaction commits or aborts. This prevents dirty reads and guarantees a recoverable, cascadeless schedule.

### 5. Rigorous Two-Phase Locking Protocol (Rigorous 2PL)

Rigorous 2PL is the strictest locking protocol. It requires that all locks (both shared and exclusive) held by a transaction must be retained until the transaction commits or aborts, ensuring complete isolation.

## Inherent Problems with Simple Locking

If lock-based protocols are poorly configured, databases can suffer from two structural scheduling issues:

### Deadlock

A deadlock occurs when two or more transactions are in a circular wait state, each holding a lock that the other needs to proceed.

- *Conceptual Example*: T1 (run by **Mohit**) holds an exclusive lock on `D101`, while T2 (run by **Akash**) holds a shared lock on `D102`.

1. Akash (T2) requests a shared lock on `D101` and is blocked (waiting for Mohit).
2. Mohit (T1) requests an exclusive lock on `D102` and is blocked (waiting for Akash).
3. Both transactions are now blocked indefinitely, halting progress.

### Starvation

Starvation occurs when a transaction is delayed indefinitely because the concurrency control manager continually grants locks to other competing transactions.

- *Conceptual Example*: Transaction T1 (run by **Hemesh**) waits for an exclusive lock on `D101`. While Hemesh is waiting, a continuous stream of read transactions (run by **Abhiram** and others) request and are granted shared locks on `D101`. Because shared locks are compatible with each other, the read queue is never empty, and Hemesh is starved of write access.

## Comparison of Lock-Based Protocols

| Protocol | Lock Acquisition Rule | Lock Release Rule | Deadlock Risk | Cascading Rollback Risk |
| --- | --- | --- | --- | --- |
| **Simplistic** | Acquired right before the database operation | Released immediately after operation completes | Low | High |
| **Pre-Claiming** | All locks must be acquired before transaction starts | Released all at once when transaction completes | None | Low |
| **Basic 2PL** | Acquired during the Growing Phase | Released during the Shrinking Phase | High | High |
| **Strict 2PL** | Acquired during the Growing Phase | Exclusive locks held until transaction commits | High | None (Cascadeless) |
| **Rigorous 2PL** | Acquired during the Growing Phase | All locks held until transaction commits | High | None (Cascadeless) |

# Summary

Lock-based concurrency control protocols regulate concurrent access to relational databases by requiring transactions to obtain shared or exclusive locks on data items. The database engine evaluates lock compatibility to block conflicting write operations, enforcing serializability. While basic protocols like Two-Phase Locking (2PL) divide execution into growing and shrinking phases, stricter variants (Strict and Rigorous 2PL) hold locks until commit to prevent cascading rollbacks. When configuring these protocols, administrators must balance transaction throughput against the risks of deadlocks and transaction starvation.




