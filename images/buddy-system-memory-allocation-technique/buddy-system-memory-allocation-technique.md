# Buddy System Memory Allocation Technique

The Buddy Allocation System is a memory management technique that partitions memory blocks in powers of two. When a process requests memory, the system dynamically divides the available memory space into equal halves (buddies) recursively until it locates the smallest suitable power-of-two partition. Upon deallocation, the system checks if the process's buddy block is also free; if so, they merge back to reconstruct a larger block, reducing external fragmentation and enabling fast memory recycling.

## Algorithm of the Buddy System

The allocation and deallocation lifecycle in a Buddy System follows these operational steps:

1. **Define Block Boundaries:** Divide physical memory into blocks sized in powers of two (e.g., 2 KB, 4 KB, 8 KB, 16 KB, 32 KB, 64 KB, etc.).
2. **Track Free Lists:** Maintain a binary tree or an array of free lists tracking unallocated blocks of each power-of-two size.
3. **Handle Allocation Request:** When a process requests memory of size S:

- Calculate the smallest power-of-two block that can hold S (i.e., find K such that 2^(K-1) &lt; S &lt;= 2^K).
- Search the free list for a block of size 2^K.
- If a block of size 2^K is available, allocate it to the process.
- If no block of size 2^K exists, locate the smallest available larger block (size 2^U, where U &gt; K) and split it in half, creating two equal-sized "buddy" blocks of size 2^(U-1).
- Continue splitting the left (lower address) buddy recursively until a block of size 2^K is created.
- Allocate the final left buddy to the process, keeping the remaining split buddies on their respective free lists.

1. **Handle Deallocation Request:** When a process releases an allocated block:

- Mark the block as free.
- Check the state of its buddy block (the adjacent block of the same size created during the original split).
- If the buddy block is also free, merge (coalesce) them to form a single block of size 2^(K+1).
- Recursively repeat this buddy-merge check for the newly formed block until a buddy is found that is currently allocated or the maximum system memory boundary is reached.

## Illustrative Splitting Example

Suppose a system has a total of 256 KB of memory and receives a process request of 35 KB.

- The system calculates the smallest power of two that can hold 35 KB: 2^K &gt;= 35 KB, which is 64 KB (since 32 KB is too small).
- Since only a 256 KB block is initially available, the system splits it:

1. 256 KB splits into two 128 KB buddies.
2. The left 128 KB block splits into two 64 KB buddies.
3. The left 64 KB block is allocated to the process.

- The remaining 29 KB (64 KB - 35 KB) inside the allocated partition goes unused, representing **internal fragmentation**.

## Trace Walkthrough Example

Consider a system initialized with 512 KB of total memory. We trace the following sequence of process allocations and terminations:

1. **Initial State:** One free block of 512 KB.

``````text
[ Free: 512 KB ]
```

1. **Process X requests 45 KB:** (Target size is 64 KB).

- 512 KB splits to Left 256 KB + Right 256 KB.
- Left 256 KB splits to Left 128 KB + Right 128 KB.
- Left 128 KB splits to Left 64 KB + Right 64 KB.
- Allocate Left 64 KB to Process X.

``````text
[ Process X: 64 KB ] [ Free: 64 KB ] [ Free: 128 KB ] [ Free: 256 KB ]
```

1. **Process Y requests 25 KB:** (Target size is 32 KB).

- The free Right 64 KB block splits to Left 32 KB + Right 32 KB.
- Allocate Left 32 KB to Process Y.

``````text
[ Process X: 64 KB ] [ Process Y: 32 KB ] [ Free: 32 KB ] [ Free: 128 KB ] [ Free: 256 KB ]
```

1. **Process Z requests 110 KB:** (Target size is 128 KB).

- Allocate the free Right 128 KB block to Process Z.

``````text
[ Process X: 64 KB ] [ Process Y: 32 KB ] [ Free: 32 KB ] [ Process Z: 128 KB ] [ Free: 256 KB ]
```

1. **Process X terminates:** (Frees its 64 KB block).

- Buddy check: The buddy of Process X's block is the Right 64 KB block. However, this buddy is currently split (partially allocated to Process Y), so they cannot merge.

``````text
[ Free: 64 KB ] [ Process Y: 32 KB ] [ Free: 32 KB ] [ Process Z: 128 KB ] [ Free: 256 KB ]
```

1. **Process Y terminates:** (Frees its 32 KB block).

- Buddy check: The buddy is the free Right 32 KB block.
- Merging: Left 32 KB and Right 32 KB merge to reform the Right 64 KB block.
- Buddy check: The buddy of this newly formed block is the free Left 64 KB block.
- Merging: Left 64 KB and Right 64 KB merge to reform the Left 128 KB block.

``````text
[ Free: 128 KB ] [ Process Z: 128 KB ] [ Free: 256 KB ]
```

## Types of Buddy Systems

Operating systems implement different variants of the buddy system to optimize memory layouts:

### 1. Binary Buddy System

The standard implementation where memory is split into powers of two (e.g., 2, 4, 8, 16, 32, ...). It simplifies address calculations using bitwise operators, making allocation and coalescing fast.

### 2. Fibonacci Buddy System

Memory is divided into block sizes based on the Fibonacci sequence (e.g., 1, 2, 3, 5, 8, 13, 21, 34, ...), following the relation:

```text
Zi = Z(i-1) + Z(i-2)
```

This model reduces internal fragmentation compared to the binary buddy system by providing finer partition steps.

### 3. Weighted Buddy System

Associates each block with a size weight relative to others. The allocation algorithm selects blocks by analyzing both the requested size and the relative weights of the free slots.

### 4. Tertiary Buddy System

Introduces a third partition division structure, offering greater flexibility and sizing steps during memory division.

## Advantages and Disadvantages

### Advantages

- **Fast Execution:** Address mapping, splitting, and merging are handled quickly using bitwise calculations.
- **Reduced External Fragmentation:** Automatic buddy merging (coalescing) prevents memory from dissolving into scattered, unusable gaps.
- **Simple Addressing:** The physical starting address of a block's buddy can be calculated directly by XORing the block address with its block size.

### Disadvantages

- **Internal Fragmentation:** If a process requires memory slightly larger than a power of two (e.g., requesting 33 KB), it is allocated the next power of two (64 KB), wasting almost half the allocated space.
- **Management Overhead:** Maintaining tree structures or free lists for multiple block sizes requires continuous kernel bookkeeping.

## Summary

The Buddy System is an efficient memory management technique that allocates memory in blocks sized in powers of two. By recursively splitting blocks to satisfy process requests and merging them back upon deallocation, the system balances allocation speed with external fragmentation control. While variants like the Fibonacci Buddy System attempt to minimize internal fragmentation, the binary buddy system remains widely used in kernel memory allocators due to its fast bitwise calculations.




