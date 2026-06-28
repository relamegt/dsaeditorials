# Segmentation in Operating Systems

Segmentation is a memory management technique that models physical RAM allocations according to the logical structure of a program. Instead of breaking process code into arbitrary, fixed-size pages, segmentation divides a process into variable-sized logical units called segments. Each segment represents a distinct program module, such as a function, global data section, class object, or execution stack, aligning memory layout with the developer's structural view of the application.

## Key Features of Segmentation

- **Variable-Sized Blocks:** Segments have varying lengths that match the exact memory requirements of the logical modules they represent.
- **Two-Dimensional Addressing:** The CPU references memory locations using a dual-value coordinate: the Segment Number (s) and the Offset (d).

`````text
Logical Address = ⟨Segment Number, Offset⟩
```

- **Memory Protection and Sharing:** Security attributes (read, write, and execute permissions) are set on a per-segment basis. For example, a code segment can be marked read-only and shared among multiple processes, while the stack segment remains private and writeable.
- **No Internal Fragmentation:** Because segments are sized exactly to process needs, there is no wasted memory within a segment boundary.
- **External Fragmentation:** Over time, loading and unloading variable-sized segments can split physical memory into scattered, unusable free slots.

## Classification of Segmentation Systems

Operating systems implement segmentation using two primary models:

- **Simple Segmentation:** All segments of a process are loaded into physical RAM during startup (not necessarily contiguously) using a segment table.
- **Virtual Memory Segmentation (Demand Segmentation):** Segments are stored on secondary disk storage and loaded into main memory dynamically only when they are referenced during program execution, reducing RAM usage.

## Segment Table and Address Translation

To map logical addresses to physical RAM, the operating system maintains a **Segment Table** for each active process. Every segment has a dedicated entry in the table containing:

- **Base Address:** The starting physical RAM address where the segment resides.
- **Segment Limit:** The maximum valid size (length) of the segment.

### Translation Logic

When the CPU generates a logical address `⟨s, d⟩`:

1. The hardware uses the segment index `s` to look up the segment's base and limit in the Segment Table.
2. The Memory Management Unit (MMU) checks if the offset `d` is valid:

``````text
Is d < Limit?
```

1. If `d` is greater than or equal to the limit, the CPU triggers a **Segmentation Fault** trap, halting the program to prevent out-of-bounds memory access.
2. If `d` is within the limit, the MMU calculates the physical address:

``````text
Physical Address = Base + d
```

## Address Translation Walkthrough Example

Consider a process configured with four active segments:

| Segment ID (s) | Segment Type | Base Physical Address | Segment Limit (Size) |
| --- | --- | --- | --- |
| **0** | Code Segment | 1400 | 800 Bytes |
| **1** | Data Segment | 6300 | 400 Bytes |
| **2** | Stack Segment | 3900 | 1000 Bytes |
| **3** | Shared Library | 8200 | 300 Bytes |

Let us trace three different logical memory requests:

### Request 1: Logical Address ⟨0, 450⟩

- Segment `s = 0`, Offset `d = 450`.
- Check Limit: Offset (450) &lt; Limit (800) is **True** (Valid).
- Calculate Address: Base (1400) + Offset (450) = **1850**.

### Request 2: Logical Address ⟨1, 410⟩

- Segment `s = 1`, Offset `d = 410`.
- Check Limit: Offset (410) &lt; Limit (400) is **False** (Invalid).
- Outcome: The MMU triggers a **Segmentation Fault** and halts execution.

### Request 3: Logical Address ⟨2, 900⟩

- Segment `s = 2`, Offset `d = 900`.
- Check Limit: Offset (900) &lt; Limit (1000) is **True** (Valid).
- Calculate Address: Base (3900) + Offset (900) = **4800**.

## Advantages and Disadvantages of Segmentation

### Advantages

- **Eliminates Internal Fragmentation:** Memory blocks match process sizes exactly, preventing wasted memory space inside partitions.
- **Reduced Table Overhead:** The segment table only needs entries for the logical components of a program, making it smaller than flat page tables.
- **Logical Security Isolation:** Facilitates access permissions per segment (e.g., read-only code segments), preventing malicious code injection.
- **Modular Code Sharing:** Entire functions, classes, or libraries can be shared easily among multiple programs by mapping their base addresses to the same physical RAM frame.

### Disadvantages

- **Severe External Fragmentation:** Variable segment sizes leave scattered gaps in memory, which may require expensive memory compaction.
- **Complex Allocation Algorithms:** Tracking dynamic, variable-sized free partitions increases operating system bookkeeping overhead.
- **Memory Access Overhead:** Finding physical addresses requires looking up the segment table first, requiring two memory accesses unless cached.

> **Note:** Segmentation maps physical memory to match the user's logical program modules. Unlike paging, it requires checking both the segment base and the segment limit for every memory reference to prevent out-of-bounds segmentation fault errors.

## Summary

Segmentation is a memory management technique that allocates memory in variable-sized blocks based on the logical structure of a program. By using a segment table containing physical base addresses and segment limits, the operating system translates logical coordinates into physical RAM addresses. While segmentation eliminates internal fragmentation and enforces granular memory protection, it suffers from external fragmentation and lookup latency. Modern operating systems often combine segmentation with paging to benefit from both architectures.




