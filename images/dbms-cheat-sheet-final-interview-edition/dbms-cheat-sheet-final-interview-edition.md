# DBMS Cheat Sheet — Final Interview Edition

## 1. Basic Terminology

| Term | Full Form / Meaning |
| --- | --- |
| DBMS | Database Management System — software that manages data, providing an interface between the database and users |
| RDBMS | Relational Database Management System — DBMS based on the relational model (tables) |
| OODBMS | Object-Oriented Database Management System — stores data as objects with attributes/behaviors |
| SQL | Structured Query Language — language used to interact with relational databases |
| DDL | Data Definition Language — CREATE, ALTER, DROP |
| DML | Data Manipulation Language — INSERT, UPDATE, DELETE |
| DCL | Data Control Language — GRANT, REVOKE |
| TCL | Transaction Control Language — COMMIT, ROLLBACK, SAVEPOINT |

## 2. DBMS vs File System — Why DBMS Exists

**How it works**: Traditional file systems store data in flat files managed separately by each application, causing data redundancy (same data duplicated across files) and inconsistency (updates in one file not reflected elsewhere). DBMS centralizes storage — all applications go through a single system that enforces consistency rules, controls concurrent access, and provides a query language, eliminating these problems.

## 3. Three-Schema Architecture

**How it works**: Data is described at three separate levels so that changes at one level don't force changes at others (data independence).

- **External (View) Level** — how individual users see the data (customized views).
- **Conceptual (Logical) Level** — the overall structure of the whole database (entities, relationships, constraints), independent of physical storage.
- **Internal (Physical) Level** — how data is actually stored on disk (file structures, indexes).
- **Logical Data Independence**: ability to change the conceptual schema without altering external views/applications.
- **Physical Data Independence**: ability to change the internal (storage) schema without altering the conceptual schema.

## 4. ER Model (Entity-Relationship Model)

**How it works**: Represents real-world things as **entities** (e.g., Student), their properties as **attributes** (e.g., Name, ID), and connections between entities as **relationships** (e.g., Student *enrolls in* Course). This is translated into tables during database design.

- **Entity**: an object with independent existence (e.g., "Employee").
- **Attribute**: a property describing an entity (e.g., "Salary").
- Simple vs Composite (can be split, e.g., Name → First+Last).
- Single-valued vs Multi-valued (e.g., Phone numbers).
- Derived (calculated, e.g., Age from DOB).
- **Relationship**: association between two or more entities.
- **Degree**: unary, binary, ternary (number of entities involved).
- **Cardinality**: One-to-One, One-to-Many, Many-to-One, Many-to-Many.
- **Weak Entity**: cannot be uniquely identified by its own attributes alone; depends on a "strong entity" via a foreign key.

## 5. Keys — How Each Works

| Key | Definition |
| --- | --- |
| Candidate Key | A minimal set of attributes that can uniquely identify a row; a table can have multiple |
| Primary Key | The candidate key chosen to uniquely identify rows; cannot be NULL |
| Alternate Key | Candidate keys not chosen as the primary key |
| Composite Key | A primary key made of two or more attributes combined |
| Foreign Key | An attribute in one table that references the primary key of another table, enforcing referential integrity |
| Super Key | Any set of attributes (possibly with extra redundant ones) that uniquely identifies a row |

## 6. Relational Model & Constraints

- **Relation** = table; **Tuple** = row; **Attribute** = column; **Domain** = set of allowed values for an attribute.
- **Integrity Constraints**:
- **Entity Integrity**: primary key can't be NULL.
- **Referential Integrity**: foreign key must either match an existing primary key value in the referenced table or be NULL.
- **Domain Constraint**: value in a column must belong to the attribute's defined domain.

## 7. Normalization — How Each Form Works

**Why normalize**: Removes data redundancy and prevents update/insert/delete anomalies by systematically splitting tables based on dependency rules.

- **1NF (First Normal Form)**: Every column must hold atomic (indivisible) values — no repeating groups or multi-valued attributes in a single cell.
- **2NF (Second Normal Form)**: Table must be in 1NF, and every non-key attribute must depend on the *whole* primary key (removes partial dependency — relevant when the key is composite).
- **3NF (Third Normal Form)**: Table must be in 2NF, and no non-key attribute depends on another non-key attribute (removes transitive dependency).
- **BCNF (Boyce-Codd Normal Form)**: A stricter version of 3NF — for every functional dependency X→Y, X must be a super key (fixes edge cases 3NF misses).

**Functional Dependency**: an attribute Y is functionally dependent on X if each value of X corresponds to exactly one value of Y (written X→Y).

## 8. Keys to Anomalies (Without Normalization)

- **Insertion Anomaly**: can't insert data about one entity without also having data about another (e.g., can't add a course without a student enrolled).
- **Deletion Anomaly**: deleting one piece of data unintentionally removes other needed data.
- **Update Anomaly**: same data duplicated in multiple rows means updating it requires changing every occurrence, risking inconsistency.

## 9. SQL Joins — How Each Works

| Join | How It Works |
| --- | --- |
| Inner Join | Returns only rows that have matching values in both tables |
| Left (Outer) Join | Returns all rows from the left table, plus matched rows from right; unmatched right columns are NULL |
| Right (Outer) Join | Returns all rows from the right table, plus matched rows from left; unmatched left columns are NULL |
| Full (Outer) Join | Returns all rows from both tables; unmatched columns from either side filled with NULL |
| Self Join | A table is joined with itself, treated as two separate copies via aliases |
| Cross Join | Returns the Cartesian product — every row of one table paired with every row of the other |

## 10. Transactions and ACID Properties

**Transaction**: a sequence of operations treated as a single logical unit of work, either fully completed or fully rolled back.

- **Atomicity**: all operations in a transaction happen, or none do — no partial execution.
- **Consistency**: a transaction takes the database from one valid state to another, preserving all rules/constraints.
- **Isolation**: concurrently running transactions don't interfere with each other — each behaves as if it ran alone.
- **Durability**: once a transaction commits, its changes persist permanently, even after a system crash.

**Transaction States**: Active → Partially Committed → Committed (or Failed → Aborted).

## 11. Concurrency Control

**Why needed**: When multiple transactions run simultaneously, uncontrolled interleaving can cause problems:

- **Dirty Read**: reading data written by an uncommitted transaction that might later roll back.
- **Lost Update**: two transactions overwrite each other's changes because neither sees the other's update.
- **Unrepeatable Read**: reading the same row twice within a transaction gives different results because another transaction modified it in between.

**How Locking Works**: Before accessing data, a transaction acquires a lock; other transactions must wait until it's released.

- **Shared Lock (S)**: allows multiple transactions to read the same data simultaneously, but blocks writes.
- **Exclusive Lock (X)**: allows only one transaction to read/write; blocks all other access.
- **Two-Phase Locking (2PL)**: a transaction acquires all needed locks first (growing phase), then releases them only after it's done making changes (shrinking phase) — guarantees serializability.

**Timestamp Ordering**: assigns each transaction a unique timestamp at start; the system executes/orders conflicting operations based on timestamp order instead of locks, avoiding deadlocks.

## 12. Deadlock in DBMS

**How it happens**: Transaction T1 holds a lock T2 needs, while T2 holds a lock T1 needs — both wait forever.

- **Prevention**: order transactions by timestamp, abort/restart the "younger" one if a conflict arises.
- **Detection**: build a wait-for graph; a cycle indicates deadlock, resolved by aborting one transaction.

## 13. Indexing — How It Works

**How it works**: An index is a separate data structure (often a B+ Tree) that stores a sorted mapping of key column values to their row locations, letting the database jump directly to relevant rows instead of scanning the whole table.

- **Primary Index**: built on the primary key; data file is physically ordered by this key.
- **Clustered Index**: table's actual rows are stored in the same order as the index (only one per table).
- **Non-Clustered (Secondary) Index**: a separate structure pointing to row locations; table order is unrelated (multiple allowed per table).
- **B+ Tree**: a balanced tree structure where all actual data pointers are at leaf nodes and internal nodes only guide the search — enables fast range queries and equality lookups in \(O(\log n)\).

## 14. Database Schemas

- **Star Schema**: a central fact table connected directly to multiple dimension tables (used in data warehousing) — simple, fast for read-heavy analytics.
- **Snowflake Schema**: like star schema, but dimension tables are further normalized into sub-dimensions — saves storage but adds join complexity.

## 15. Types of DBMS

| Type | How It Works |
| --- | --- |
| Hierarchical | Data organized in a tree structure with parent-child relationships |
| Network | Data organized as a graph, allowing many-to-many relationships between records |
| Relational (RDBMS) | Data stored in tables with rows/columns, linked via keys |
| Object-Oriented (OODBMS) | Data stored as objects, integrating OOP concepts |
| NoSQL | Non-relational, flexible schema — Key-Value, Document, Column, or Graph based; built for scale and unstructured data |

## 16. Views

**How it works**: A view is a virtual table defined by a stored SQL query; it doesn't store data itself but dynamically pulls from underlying tables whenever queried — useful for simplifying complex queries and restricting user access to specific columns/rows.

## 17. Stored Procedures & Triggers

- **Stored Procedure**: precompiled block of SQL code saved in the database, executed by calling its name — reduces repeated query-writing and network overhead.
- **Trigger**: a block of code automatically executed by the database when a specified event (INSERT/UPDATE/DELETE) occurs on a table.

## 18. Quick Interview Traps

- 1NF removes multi-valued attributes; 2NF removes partial dependency; 3NF removes transitive dependency; BCNF fixes edge cases 3NF misses.
- Primary key can't be NULL; foreign key can be NULL.
- Clustered index physically reorders table data (only one allowed); non-clustered index is a separate lookup structure (many allowed).
- A candidate key becomes the primary key; the rest become alternate keys.
- Dirty read happens only when reading uncommitted data — this is what Isolation levels aim to prevent.
- 2PL guarantees serializability but doesn't prevent deadlocks — timestamp ordering does.
- Star schema is denormalized (fast reads); snowflake schema is normalized (less redundancy, more joins).

