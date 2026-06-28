# File Systems in Operating Systems

A file system is a subsystem in an operating system that manages how data is stored, organized, and retrieved on secondary storage devices (such as Hard Disk Drives, Solid State Drives, and flash storage). By translating user-level file operations into physical disk address requests, the file system enables users and applications to perform Create, Read, Update, and Delete (CRUD) operations on files in an organized and secure manner.

## Architectural Layers of a File System

Operating systems structure file management systems into four hierarchical layers:

- **User Application Layer:** User-space software and programs that initiate read, write, or delete calls.
- **Logical File System:** Manages metadata, maps file names to directory paths, and enforces access permissions and security policies.
- **Virtual File System (VFS):** An abstraction layer that provides a uniform API for user applications, allowing different physical file systems to run concurrently under a single interface.
- **Physical File System:** Handles the low-level translation of logical files into physical hardware sectors and data blocks on the storage media.

## Popular File System Implementations

Operating systems utilize different file system formats based on performance and platform requirements:

- **NTFS (New Technology File System):** The standard journaling file system for modern Windows operating systems, supporting file permissions, encryption, compression, and transactions.
- **ext4 (Fourth Extended File System):** A high-performance journaling file system commonly used in Linux distributions.
- **APFS (Apple File System):** A modern file system designed for macOS and iOS, optimized for Solid State Drives (SSDs) and supporting snapshotting, cloning, and strong encryption.
- **FAT32 / exFAT (File Allocation Table):** Legacy cross-platform file allocation formats, widely used in USB drives and memory cards due to their simple design and universal compatibility.

## Directory Structures

A directory is a specialized file maintained by the operating system that stores metadata (names, sizes, attributes, and starting address pointers) of other files. Operating systems organize directories using three main structures:

- **Single-Level Directory:** A single directory contains all files for all users. It is simple but causes naming conflicts because two files cannot share the same name.
- **Two-Level Directory:** Creates a separate User File Directory (UFD) for each user under a Master File Directory (MFD). This resolves naming conflicts but prevents users from sharing files easily.
- **Tree-Structured Directory:** A hierarchical tree structure where directories can contain files and subdirectories. This is the standard model in modern OS platforms, supporting efficient searching and logical grouping using absolute and relative paths.

## File Allocation Methods

When a file is created or grows, the operating system allocates disk blocks using one of three techniques:

- **Contiguous Allocation:** Each file occupies a single, continuous sequence of blocks on the disk. This method offers fast sequential read speeds but suffers from severe external fragmentation.
- **Linked Allocation:** Files are stored in non-contiguous blocks, and each block contains a pointer to the next block in the chain. This eliminates external fragmentation but suffers from slow random access and pointer overhead.
- **Indexed Allocation:** An index block is created for each file to store pointers to all its non-contiguous data blocks. This combines the benefits of fast random access with the elimination of external fragmentation.

## Disk Free Space Management

To allocate blocks to incoming files, the operating system must track unallocated disk space. Consider a small disk partition containing **16 blocks** (numbered 0 to 15), where blocks 0, 1, 2, 5, 6, 9, 13, and 14 are currently allocated, and the rest are free.

The OS manages this free space using two primary methods:

### 1. Bit Vector (Bit Map)

The system maintains an array of bits, where each bit corresponds to a physical disk block:

- `1` indicates the block is allocated/occupied.
- `0` indicates the block is free/available.

For our 16-block partition, the bit vector is:

```text
Bit Vector = [1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 0, 0, 0, 1, 1, 0]
```

*(Bit index 3, 4, 7, 8, 10, 11, 12, and 15 are set to 0, indicating they are free).*

### 2. Free Block List

The system maintains a list (often using linked pointers) tracking only the addresses of free blocks:

```text
Free List = [3, 4, 7, 8, 10, 11, 12, 15]
```

> **Note:** A file system abstracts raw physical disk sectors into logical files and directories. To manage storage space efficiently, the operating system utilizes bit maps or linked free-block lists to track unallocated disk sectors for dynamic file allocations.

## Summary

A file system is a core operating system component that organizes, allocates, and secures data stored on secondary storage. Through layers like the Virtual File System (VFS), directory structures (single-level, two-level, or hierarchical trees), and allocation methods (contiguous, linked, or indexed), the OS balances access speed with storage capacity. By maintaining bit vectors or free block lists to track unallocated disk sectors, file systems ensure efficient resource usage and data recovery on modern drives.




