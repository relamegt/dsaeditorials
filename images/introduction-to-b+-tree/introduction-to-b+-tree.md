# Introduction to B+ Tree

A B+ Tree is an advanced self-balancing search tree data structure designed to maintain sorted data for high-speed retrieval, especially in database indexing and file system storage. It extends the design of the standard B-Tree by storing all actual data records (or data pointers) solely in the leaf nodes, while the internal nodes contain only keys used to guide the search path.

## Principles of Leaf-Focused Indexing

Because the internal nodes of a B+ Tree do not store actual data records, they can hold a significantly larger number of search keys and child pointers in a single disk block. This high fan-out reduces the height of the tree, ensuring that query engines can locate records with very few disk lookups.

## Core Components of a B+ Tree

A B+ Tree consists of two distinct types of nodes:

### Internal Nodes

Internal nodes are used strictly for navigation, guiding search queries to the appropriate leaf nodes.

- **Structure Format**: `<P1, K1, P2, K2, ..., Pc-1, Kc-1, Pc>` (where `c <= a`, `a` is the order of the internal node, `Pi` are tree pointers to child nodes, and `Ki` are search key values).
- **Sort Ordering**: Keys within an internal node are stored in sorted ascending order (**K1 &lt; K2 &lt; ... &lt; Kc-1**).
- **Range Partitioning**: For any value `X` in the child subtree pointed to by `Pi`, the condition holds: **Ki-1 &lt; X &lt;= Ki** (for `1 < i < c`), and **Ki-1 &lt; X** (for `i = c`).
- **Minimum Pointers**: Except for the root, every internal node must contain at least **ceil(a / 2)** tree pointers.

### Leaf Nodes

Leaf nodes store the actual data records (or pointers referencing their disk block locations) and are linked together sequentially.

- **Structure Format**: `<<K1, D1>, <K2, D2>, ..., <Kc-1, Dc-1>, Pnext>` (where `c <= b`, `b` is the leaf order, `Di` are data pointers to disk records, `Ki` are keys, and `Pnext` is a pointer referencing the next leaf node).
- **Linked Leaf List**: The `Pnext` pointer links all leaf nodes together as a singly linked list, allowing database engines to perform sequential and range queries without returning to the root or internal nodes.
- **Minimum Entries**: Every leaf node must contain at least **ceil(b / 2)** values.
- **Uniform Depth**: All leaf nodes are aligned at the exact same depth level.

## Core Operations in B+ Trees

B+ Trees support efficient searching, insertion, and deletion:

### Search Operation

To locate a specific key, the engine starts at the root and traverses down the internal nodes by comparing the search key with node keys until it reaches the appropriate leaf node. If the key exists in that leaf node, the engine retrieves its data pointer; otherwise, it reports that the record is not found.

### Case Study: Searching and Range Scanning

Consider a database graph structured as a B+ Tree of order 4:

- **Root Node**: Contains key `[100]`.
- **Internal Nodes**: Left child contains `[50]`; Right child contains `[150]`.
- **Leaf Nodes**:
- Leaf 1: `<30, D30>`, `<50, D50>`
- Leaf 2: `<60, D60>`, `<90, D90>`
- Leaf 3: `<110, D110>`, `<140, D140>`
- Leaf 4: `<150, D150>`, `<155, D155>`, `<180, D180>`

We execute two analytical queries:

- **Point Lookup (Search for 155)**:

1. Compare `155 > 100` at the root and follow the right pointer.
2. Compare `155 > 150` at the internal node `[150]` and follow the right pointer.
3. Reach Leaf 4, locate `155`, and retrieve the record pointer `D155`.

- **Range Query (Scan values between 90 and 150)**:

1. Traverse the tree to locate the start key `90` in Leaf 2.
2. Instead of returning to the root, follow the `Pnext` pointer sequentially from Leaf 2 to Leaf 3 (reading `110` and `140`) and then to Leaf 4 (reading `150`), scanning the contiguous leaf blocks directly.

### Insertion Operation

1. Traverse the tree to locate the target leaf node in sorted order.
2. If the leaf node has space, insert the new key-value pair.
3. If an overflow occurs (keys exceed `b - 1`), split the leaf node into two. Retain the lower half in the left leaf and copy the middle key to the parent node. If the parent overflows, propagate the split upward to the root.

### Deletion Operation

1. Locate and remove the key from the target leaf node.
2. If the node contains fewer than the minimum allowed entries (**ceil(b/2)**), rebalance the tree by borrowing a key from a neighboring sibling node.
3. If the sibling lacks spare keys, merge the node with its sibling, updating or removing the reference key in the parent node.

## Performance Trade-Offs of B+ Trees

Enforcing leaf-only data storage introduces several design trade-offs:

### Advantages of B+ Trees

- **High Fan-Out and Capacity**: Internal nodes can store more keys since they omit data records, keeping the tree shorter and reducing disk accesses.
- **Fast Range Queries**: The linked leaf list allows range scans to retrieve sequential blocks directly without traversing internal nodes.
- **Predictable Access Latency**: Every point lookup query must traverse the same number of levels to reach a leaf, guaranteeing a consistent search path.

### Disadvantages of B+ Trees

- **Slower Point Lookups**: Unlike standard B-Trees where keys can be found in internal nodes, a B+ Tree query must always traverse to the leaf level.
- **Complex Update Operations**: Split and merge operations require updating parent links and maintaining the linked leaf pointer chain.
- **Extra Pointer Storage Space**: Maintaining the `Pnext` pointer list across all leaves consumes additional disk space.

## Comparison of B+ Trees and B Trees

| Feature | B+ Tree | B Tree |
| --- | --- | --- |
| **Data Storage Location** | Only in the leaf nodes | In both internal and leaf nodes |
| **Leaf Node Pointers** | Linked together as a list (`Pnext`) | Not linked together |
| **Internal Node Keys** | Contains only navigation keys | Contains both keys and data records |
| **Key Duplication** | Allows key duplication (keys in internal nodes also exist in leaves) | No duplicate keys allowed |
| **Range Query Speed** | Fast and efficient (uses the linked leaf list) | Slower (requires traversing up and down the tree branches) |
| **Disk I/O Latency** | Low (fewer tree levels maximize block reads) | Higher (more tree levels due to bulky internal nodes) |
| **Memory Footprint** | Requires extra space to store navigation keys and list pointers | Lower memory footprint (no duplicate keys stored) |

> **Key Insight**: The primary difference between B+ Trees and B-Trees lies in leaf node chaining and key distribution. A B-Tree stores data records in both internal and leaf nodes, which can increase the tree's height. A B+ Tree stores data records only in leaf nodes and links them sequentially via pointers, reducing the tree's height for point lookups and enabling fast, direct sequential range scans.

# Summary

A B+ Tree is an advanced self-balancing search tree designed to optimize data access and range scans in relational database file systems. By storing all actual data records in leaf nodes and linking them sequentially, B+ Trees enable engines to run direct point lookups and sequential range queries efficiently. Internal nodes store only navigation keys, maximizing key capacity per disk block and keeping the tree structure short. Relational database engines rely on B+ Trees to implement primary and clustered table indexes, balancing transaction rebalancing overhead against predictable read latency.




