# File Allocation Methods in Operating Systems

File allocation methods define how the operating system stores file data across physical disk blocks. The primary goal of any allocation strategy is to provide efficient disk space utilization while enabling fast access to file data. The three main file allocation methods are Contiguous Allocation, Linked Allocation, and Indexed Allocation.

## Contiguous Allocation

In contiguous allocation, each file occupies a sequential, uninterrupted series of blocks on the disk. The directory entry for each file stores only two fields: the starting block address and the total number of blocks required.

- **Block Calculation:** If a file is stored starting at block `b` and requires `n` blocks, the occupied blocks are `b, b+1, b+2, ..., b+n-1`.
- **Sequential Access:** Since all blocks are physically adjacent, the disk head moves minimally during reads, making this the fastest allocation strategy for sequential workloads.
- **Direct Access:** The address of the `k`th block of a file starting at block `b` is directly computed as `b + k`, enabling instant random access.

### Disadvantages

- **External Fragmentation:** Over time, as files are created and deleted, free disk space becomes scattered into non-contiguous holes that are too small to hold new files.
- **Internal Fragmentation:** Allocating fixed-size regions wastes space when actual file sizes do not perfectly match block boundaries.
- **Fixed Size Limitation:** Expanding a file is difficult because contiguous free space following the file may not be available.

## Linked Allocation

In linked allocation, each file is stored as a linked list of disk blocks. The blocks do not need to be contiguous and can be scattered across the disk. Each block contains a pointer to the next block, and the directory entry stores only the address of the first and last block.

- **Flexibility:** Files can grow dynamically by attaching new blocks from anywhere on the disk without requiring contiguous free space.
- **No External Fragmentation:** Since individual blocks are allocated independently, free disk space is never wasted by fragmentation holes.

### Disadvantages

- **No Direct Access:** To access the `k`th block of a file, the system must traverse `k` blocks sequentially from the starting block, reading each pointer along the way.
- **Pointer Overhead:** Each block sacrifices a few bytes to store a pointer to the next block, reducing the effective data storage capacity per block.
- **High Seek Count:** Because blocks are scattered randomly on the disk, reaching multiple blocks requires many mechanical disk head seeks, making this method slow.

## Indexed Allocation

In indexed allocation, a dedicated block called the **Index Block** is created for each file. This index block stores an ordered array of pointers, where the `i`th entry holds the disk address of the `i`th data block of the file. The directory entry points only to this index block.

- **Direct Access:** The `k`th block of a file can be accessed directly by reading the `k`th pointer in the index block, without traversing other blocks.
- **No External Fragmentation:** Data blocks can be scattered anywhere on the disk.

### Disadvantages

- **Index Block Overhead:** For very small files (2–3 blocks), an entire index block is allocated just to hold a few pointers, wasting significant space. In linked allocation, only one pointer per block is used.
- **Limited Pointer Capacity:** A single index block has a fixed size. For very large files, its pointer array may not be sufficient to map all data blocks.

## Indexing Schemes for Large Files

When a file grows large enough that a single index block cannot hold all block pointers, the OS uses extended indexing strategies:

### 1. Linked Index Scheme

Multiple index blocks are chained together. Each index block stores disk block pointers and a pointer to the next index block, continuing until all blocks are mapped.

### 2. Multilevel Index

A hierarchy of index blocks is used. A first-level index block holds pointers to second-level index blocks, and those in turn hold pointers to actual data blocks. This can be extended to three or more levels as needed.

### 3. Combined Scheme (Inode Structure)

Used in Linux ext2/ext3/ext4 file systems, the **Inode (Index Node)** stores both file metadata (name, size, permissions, timestamps) and a mixed set of block pointers:

- **Direct Pointers:** Point directly to the first few data blocks (typically 10–12 blocks), enabling fast access for small files.
- **Single Indirect Pointer:** Points to an intermediate block that holds additional disk block pointers.
- **Double Indirect Pointer:** Points to a block of single-indirect pointers, each of which points to a block of data pointers.
- **Triple Indirect Pointer:** Adds a third layer of indirection for extremely large files.

This hybrid design provides fast direct access for small files while scaling transparently to very large file sizes.

## Comparison of Allocation Methods

| Feature | Contiguous | Linked | Indexed |
| --- | --- | --- | --- |
| **Sequential Access** | Excellent | Good | Good |
| **Direct Access** | Excellent | Not Supported | Excellent |
| **External Fragmentation** | High | None | None |
| **File Size Flexibility** | Rigid | Flexible | Flexible |
| **Pointer Overhead** | None | Per Block | Per Index Block |

> **Note:** No single allocation method is universally optimal. Contiguous allocation is fastest but fragmentation-prone. Linked allocation is flexible but does not support direct access. Indexed allocation supports direct access and scalability, making the combined inode scheme the preferred choice in modern file systems.

## Summary

File allocation methods control how the operating system distributes file data across disk blocks. Contiguous allocation is fast and supports direct access but suffers from external fragmentation and rigid file sizing. Linked allocation eliminates fragmentation and supports dynamic growth but lacks direct access and introduces pointer overhead per block. Indexed allocation resolves both issues by using a dedicated index block, though it is wasteful for very small files. Modern file systems like ext4 use the combined inode scheme, which integrates direct pointers with multiple levels of indirection to handle both small and very large files efficiently.




