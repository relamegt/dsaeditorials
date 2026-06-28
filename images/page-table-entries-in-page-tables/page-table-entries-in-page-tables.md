# Page Table Entries in Page Tables

A Page Table is a hardware-supported data structure used by operating systems to map the virtual addresses of executing processes to physical addresses in RAM. Every individual mapping record in this table is stored in a Page Table Entry (PTE). While the exact bit width and layout of a PTE are determined by the processor architecture and operating system, the entry always stores the target address location along with critical metadata flags to enforce memory protection and hardware efficiency.

## Core Structure of a Page Table Entry

To manage memory pages safely, each Page Table Entry stores specific hardware control bits and location metadata:

### 1. Physical Frame Number

This field stores the physical memory address (frame index) where the virtual page resides in RAM. The number of bits required to represent the frame number is calculated as:

```text
Frame Number Bits = log2(Physical Memory Size / Frame Size)
```

### 2. Present/Absent Bit (Valid/Invalid Bit)

A 1-bit flag indicating whether the logical page currently resides in physical RAM or is stored on secondary storage.

- **State 1 (Present):** The page is resident in RAM, and the CPU can access it directly.
- **State 0 (Absent):** The page is not in RAM. Accessing it triggers a **page fault**, forcing the OS to fetch the page from disk.

### 3. Protection Bits

A set of permission flags that define the allowed hardware operations on the page:

- **Read (R):** Permits reading the page contents.
- **Write (W):** Permits modifying the page contents.
- **Execute (X):** Permits executing instructions stored on the page.

These bits prevent processes from executing data pages (preventing buffer overflow exploits) or modifying read-only code segments.

### 4. Referenced Bit

A flag set automatically by the CPU hardware whenever the page is accessed (read or written). Page replacement algorithms (such as Least Recently Used) check this bit to identify which pages are active and which can be safely evicted when memory is full.

### 5. Caching Control (Enabled/Disabled)

Determines whether the CPU should cache the page in its high-speed L1/L2/L3 caches. 

- **Disable Caching:** Essential for memory-mapped I/O registers (such as a keyboard buffer or network controller interface) to ensure that the CPU always reads the live hardware state directly rather than a cached value.

### 6. Modified Bit (Dirty Bit)

Set automatically by the hardware when a process writes to the page. 

- **State 1 (Dirty):** The page has been modified. During page eviction, the OS must write the modified page back to disk.
- **State 0 (Clean):** The page has not been modified. The OS can discard the page frame immediately during eviction, avoiding disk writing overhead.

## Page Table Size Calculation Example

Consider a computer configured with a 36-bit virtual address space and a page size of 8 KB:

1. **Represent Page Size in Bytes:**

``````text
8 KB = 8 * 1024 Bytes = 2^3 * 2^10 = 2^13 Bytes
```

This requires 13 offset bits in the logical address.

1. **Calculate Total Number of Pages:**

``````text
Number of Pages = Total Virtual Space / Page Size
   Number of Pages = 2^36 / 2^13 = 2^23 pages (approximately 8.38 million pages)
```

1. **Calculate Flat Page Table Size:**

   If each Page Table Entry requires 8 bytes (64 bits) to store frame addresses and metadata:

``````text
Total Table Size = Number of Pages * PTE Size
   Total Table Size = 2^23 * 8 Bytes = 2^26 Bytes = 64 MB
```

Because a flat 64 MB page table for every single process consumes too much physical RAM, modern 64-bit systems utilize **multi-level (hierarchical) page tables** to allocate table pages dynamically on demand, saving memory.

## Advantages of Page Tables in Virtual Memory

- **Dynamic Resource Allocation:** Physical RAM frames are allocated only when pages are actively referenced, maximizing memory efficiency.
- **Granular Access Security:** Embedded protection bits prevent unauthorized memory writes and protect critical kernel data structures.
- **Process Address Isolation:** Each process receives a private page table, preventing tasks from accessing or corrupting the memory spaces of other processes.
- **Large Address Space Scaling:** Hierarchical page table structures allow operating systems to support immense virtual memory spaces without requiring huge flat tables in physical RAM.

> **Note:** A Page Table Entry (PTE) acts as the fundamental bridge between virtual memory and physical hardware. It stores not only the address mapping details but also essential metadata flags to enforce memory security, caching configurations, and page eviction heuristics.

## Summary

A Page Table Entry (PTE) is a compact hardware-mapped data structure that records the relationship between a logical page and a physical RAM frame. By storing frame indices alongside present-absent bits, protection flags, referenced bits, and dirty bits, the PTE provides the operating system and MMU with the metadata required to translate addresses, enforce memory security, regulate caching, and manage page replacement algorithms. Multi-level page tables ensure that these entries can scale efficiently in modern large-memory architectures.




