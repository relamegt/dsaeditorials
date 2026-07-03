# Indexing in Databases

Indexing is a physical database design technique used to optimize data retrieval speeds. By creating auxiliary data structures that map search keys to their physical disk addresses, indexes minimize the number of disk block accesses required to satisfy query predicates, bypassing slow, full-table scans.

## Principles of Relational Indexing

An index functions similarly to a catalog card system. It stores copies of values from specific database columns (the search key) alongside pointers (logical or physical disk block addresses) that reference the corresponding data rows in the primary table.

## Performance Attributes of Database Indexes

When implementing an indexing strategy, database designers evaluate five operational characteristics:

- **Access Types**: The query patterns supported by the index, such as exact key lookups or range scans.
- **Access Time**: The time required to navigate the index and retrieve the target data blocks.
- **Insertion Time**: The processing overhead needed to locate the correct insertion slot and update the index structure.
- **Deletion Time**: The overhead required to remove a data entry and restructure the index tree.
- **Space Overhead**: The additional disk storage consumed by the index file itself.

## Index File Organizations

Ordered indexes are classified based on how closely their entries correspond to the records in the physical data file:

### Ordered (Sequential) Indexing

In this organization, index records are stored in a sorted order based on the search key values. Sequential indexes can be dense or sparse:

#### Dense Indexing
A dense index maintains exactly one index record for every single search key value present in the primary data file.

- **Conceptual Case Study**: Consider a device deployment file with five custodians:

1. Mohit (Block 1)
2. Akash (Block 1)
3. Hemesh (Block 2)
4. Abhiram (Block 2)
5. Siddu (Block 3)

- **Dense Index Table**: The dense index maps each custodian to their precise row position:
- Mohit -&gt; Pointer to Block 1, Row 1
- Akash -&gt; Pointer to Block 1, Row 2
- Hemesh -&gt; Pointer to Block 2, Row 1
- Abhiram -&gt; Pointer to Block 2, Row 2
- Siddu -&gt; Pointer to Block 3, Row 1

#### Sparse Indexing
A sparse index contains index records for only a subset of the search key values. Typically, it stores one index entry for each physical disk block (referencing the first record of the block, known as the anchor record).

- **Access Method**: To locate a record, the engine finds the index entry with the largest search key value that is less than or equal to the target key, and then performs a sequential scan within that specific block.
- **Access Cost**: **log_2(n) + 1** (where `n` is the number of blocks involved in the index file).
- **Sparse Index Table**:
- Mohit (Block 1 Anchor) -&gt; Pointer to Block 1
- Hemesh (Block 2 Anchor) -&gt; Pointer to Block 2
- Siddu (Block 3 Anchor) -&gt; Pointer to Block 3
- To locate **Akash**, the database identifies that `Akash > Mohit` and `Akash < Hemesh`, and scans Block 1 sequentially.

### Hash File Indexing

Hash indexing uses a mathematical hash function to map search keys to specific bucket addresses on disk.

- **Attributes**: Provides extremely fast access (constant time complexity) for exact-match queries (e.g., `WHERE CustodianName = 'Mohit'`).
- **Disadvantage**: Does not support range queries because hashing scatters sequential keys across different physical buckets.

## Types of Indexing Methods

Database engines deploy several indexing algorithms depending on the table schema and query requirements:

### Clustered Indexing

Clustered indexing groups related records physically together in the same storage file. The primary data file is physically sorted based on the clustered index key (which does not need to be a primary key).

- **Conceptual Case Study**: Grouping device records by department. All records for the `Security` department (associated with **Hemesh**) are stored contiguously on disk, allowing range scans to fetch them with minimal disk head movements.

### Primary Indexing

Primary indexing is built on the table's primary key, and the primary data file is physically sorted based on this key. Each entry in the primary index corresponds to a data block, containing the primary key of the anchor record and a pointer to the block.

### Secondary (Non-Clustered) Indexing

A secondary index provides a separate, sorted pointer structure without altering the physical order of the primary data file. The data rows are scattered on disk, and the index leaf nodes store pointers (virtual references) to these locations.

- **Warehouse Catalog Analogy**: Similar to a warehouse inventory registry. The hardware items themselves are scattered across different warehouse shelves based on size and arrival date, but the catalog registry lists item names alphabetically with shelf locations.
- **Attributes**: Because the physical data is not sorted by the secondary key, secondary indexes must be dense. They require more I/O than clustered indexes because the engine must follow pointers to fetch non-contiguous data rows.

### Multilevel Indexing

As database files grow, single-level indexes become too large to fit in memory, leading to high disk search times. Multilevel indexing resolves this by creating a static hierarchy of index blocks:

- **Structure**: An outer index (coarse pointers) references inner index pages (finer pointers), which point to the actual data blocks. This tree-based hierarchy ensures that index searches can execute with minimal memory overhead and a fixed number of block reads.

## Performance Trade-Offs of Indexing

While indexes improve database read speeds, they introduce write and storage costs:

### Advantages of Database Indexes

- **Accelerated Queries**: Dramatically reduces search times for selective predicates.
- **Disk I/O Reduction**: Minimizes memory usage by loading only matching block records.
- **Ordered Sorting**: Speeds up `ORDER BY` operations because data can be accessed in index order.
- **Unique Validation**: Enforces column uniqueness, preventing duplicate record insertions.

### Disadvantages of Database Indexes

- **Increased Disk Consumption**: Creating indexes on multiple columns increases overall database size.
- **Write Transaction Latency**: Inserting, updating, or deleting a record requires updating the data file and all associated indexes, slowing down write transactions.
- **Index Maintenance Overhead**: Requires database administrators to periodically rebuild fragmented indexes.

## Comparison of Database Indexing Methods

| Indexing Type | Physical Data Ordering | Key Constraint | Index Density | Search Cost | Update Overhead |
| --- | --- | --- | --- | --- | --- |
| **Primary Indexing** | Physically sorted by index key | Must be Primary Key | Can be Sparse or Dense | Moderate | High (requires data shift on insert) |
| **Clustered Indexing** | Physically sorted by index key | Can be Non-Primary Key | Typically Sparse | Low | High (requires data regrouping) |
| **Secondary Indexing** | Unsorted (independent of index key) | Can be Non-Primary Key | Must be Dense | Moderate to High (requires pointer hops) | Low (only updates index pointers) |
| **Multilevel Indexing** | Sorted hierarchical index blocks | Can be Primary/Non-Primary Key | Sparse outer, dense inner | Low (fixed tree-search paths) | High (requires tree balancing) |

> **Key Insight**: The primary difference between clustered and non-clustered (secondary) indexing lies in the physical storage layout. A clustered index physically dictates the sort order of the records on disk, restricting each table to a single clustered index. A secondary index maintains an independent, sorted file of pointer references to unsorted records, allowing tables to support multiple secondary indexes.

# Summary

Indexing optimizes database query performance by creating auxiliary search keys that point to physical data blocks, bypassing slow, sequential table scans. Database engines implement primary and clustered indexes that physically organize data records on disk, or secondary indexes that maintain separate, dense files of logical pointers to unsorted records. For large databases, multilevel indexes structure pointers into trees, minimizing memory footprint and access costs. Determining the appropriate indexing strategy requires balancing accelerated read queries against the storage overhead and write transaction latency of index updates.




