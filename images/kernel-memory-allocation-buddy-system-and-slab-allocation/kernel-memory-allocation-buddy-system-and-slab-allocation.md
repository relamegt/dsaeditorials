# Kernel Memory Allocation: Buddy System and Slab Allocation

Kernel memory allocation is the process of managing physical memory blocks used by the operating system kernel to perform critical kernel tasks. Unlike user-space programs, which are allocated virtual memory pages that can be loaded non-contiguously, the kernel frequently requires contiguous physical memory blocks for direct hardware access (such as DMA buffers) and needs fast, low-overhead allocation routines to handle small kernel data structures with minimal fragmentation.

To satisfy these requirements, operating systems utilize two primary memory allocation techniques: the Buddy System and Slab Allocation.

## The Buddy Allocation System

The Buddy Allocation System manages physical memory by dividing large contiguous blocks into smaller partitions sized in powers of two. 

### Splitting and Allocation

- **Power-of-Two Sizing:** Memory requests are satisfied by allocating a block size equal to the smallest power of two that is greater than or equal to the requested size.
- **Recursive Splitting:** If no block of the requested size is available, a larger block is located and split in half. This split creates two equal-sized "buddy" blocks. The division continues recursively until the exact power-of-two size is produced.

#### Custom Sizing Example
Suppose a system starts with a **512 KB** contiguous memory block and receives a kernel request of **55 KB**:

1. The allocator determines the nearest power of two greater than or equal to 55 KB, which is **64 KB** (since 32 KB is too small).
2. The 512 KB block is split into two 256 KB buddies.
3. The left 256 KB block is split into two 128 KB buddies.
4. The left 128 KB block is split into two 64 KB buddies.
5. One of the 64 KB blocks is allocated to satisfy the request.
6. The remaining 9 KB (64 KB - 55 KB) goes unused, resulting in **internal fragmentation**.

### Coalescing (Merging)

When a block is released, the allocator checks if its adjacent buddy is also free.

- If the buddy is free, they are combined (coalesced) to reform the original larger block.
- *Example:* If block X1 (64 KB) is freed, and its buddy X2 (64 KB) is already free, the system merges them into a 128 KB block. If that block's buddy is also free, they merge into a 256 KB block, recursively restoring the memory state.

### Variations of the Buddy System

Operating systems utilize different buddy structures to optimize allocation layouts:

- **Binary Buddy System:** Splits memory strictly in powers of two.
- **Fibonacci Buddy System:** Divides blocks based on the Fibonacci sequence (e.g., 1, 2, 3, 5, 8, 13, 21, 34, ...) to reduce internal fragmentation.
- **Weighted Buddy System:** Assigns size weights to blocks, choosing allocations based on matching request weights.
- **Tertiary Buddy System:** Adds an extra division structure to provide more flexible partition steps.

## The Slab Allocation Scheme

Slab Allocation is a memory management technique designed to eliminate internal fragmentation and improve allocation speed for frequently used kernel objects. Instead of allocating pages in powers of two, the slab allocator keeps caches of pre-allocated, initialized data structures (such as process descriptors, file locks, or semaphores) ready for instant reuse.

### Core Concepts of Slab Allocation

- **Slab:** One or more physically contiguous memory pages. The slab serves as the container for pre-allocated objects.
- **Cache:** A software structure that stores pre-allocated objects of a specific type (e.g., a "process descriptor cache" or a "semaphore cache").

#### Custom Sizing Example
A **16 KB slab** (made of four contiguous 4 KB pages) can be configured to store **eight 2 KB semaphore objects**. Initially, all eight objects are marked as free. When the kernel needs a new semaphore, the allocator assigns one of the free objects from the cache and marks it as used, avoiding page-splitting overhead.

### Slab States in the Linux Kernel

In Linux, slabs are classified into three possible states:

- **Full:** All pre-allocated objects in the slab are marked as used.
- **Empty:** All objects in the slab are marked as free.
- **Partial:** The slab contains both free and used objects. When an object request arrives, the allocator satisfies it from a partial slab first.

## Advantages and Disadvantages of Allocators

| Feature | Buddy Allocation System | Slab Allocation Scheme |
| --- | --- | --- |
| **Primary Use Case** | Large, physically contiguous memory blocks. | Small, repetitive, object-specific kernel allocations. |
| **Fragmentation Control** | Prone to internal fragmentation due to power-of-two rounding. | Eliminates internal fragmentation by matching object sizes exactly. |
| **Allocation Speed** | Moderate; requires traversing page lists and splitting blocks. | High; returns pre-allocated, constructed objects from cache. |
| **Unit of Management** | Pages (powers of two). | Contiguous page structures (slabs) divided into objects. |

> **Note:** Kernel memory management uses two complementary allocators: the Buddy System, which manages large page-sized blocks in powers of two, and the Slab Allocator, which slices these pages into caches of specific objects to eliminate internal fragmentation.

## Summary

Kernel memory allocation requires fast speeds and contiguous memory support for OS tasks. While the Buddy System allocates page frames in powers of two and merges free buddies through coalescing, it is prone to internal fragmentation. The Slab Allocator solves this by using contiguous pages (slabs) to store caches of pre-allocated, uniform kernel objects. Operating systems combine these techniques, using the Buddy System for large page allocations and the Slab Allocator for managing fine-grained kernel data structures.




