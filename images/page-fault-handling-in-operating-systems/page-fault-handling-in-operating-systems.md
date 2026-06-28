# Page Fault Handling in Operating Systems

A page fault is a hardware interrupt triggered by the Memory Management Unit (MMU) when an executing program references a virtual memory page that is not currently mapped into the system's physical RAM. When this occurs, the operating system must intercept the fault, locate the required page in secondary storage, load it into physical RAM, update the address mapping tables, and resume program execution.

## Detailed Step-by-Step Page Fault Handling Lifecycle

Resolving a page fault involves a coordinated sequence of hardware and software routines:

1. **Hardware Trap to Kernel:** The MMU detects that the valid-invalid bit for the requested virtual page is set to invalid. The CPU immediately halts execution and generates a trap (exception) to the operating system kernel. The program counter (PC) and instruction state are saved on the system stack.
2. **State Conservation:** A low-level assembly routine saves the current state of volatile CPU registers and address descriptors to prevent the OS from overwriting them.
3. **Fault Diagnosis:** The operating system kernel services the trap, determines that a page fault has occurred, and retrieves the specific virtual address that caused the fault from hardware registers.
4. **Validation Check:** The OS checks the validity of the virtual address to ensure the program is not attempting to access unallocated memory space or violate memory protection rules (such as writing to a read-only page).
5. **Frame Allocation:** The OS searches the free frame list for an empty block in RAM. If all frames are occupied, a page replacement algorithm (such as Least Recently Used) is executed to select a resident page for eviction.
6. **Dirty Page Synchronization:** If the page selected for eviction is marked as "dirty" (modified), it must be written back to disk. The faulting process is suspended, a context switch occurs, and another process runs until the disk write operation completes.
7. **Page Ingestion:** Once a clean physical frame is secured, the OS schedules a disk read operation to load the target page from secondary storage into the empty frame.
8. **Page Table Update:** After the disk controller signals that the transfer is complete via a hardware interrupt, the OS updates the process's page table, mapping the virtual page to the new physical frame number and marking its status bit as valid.
9. **State Restoration and Execution Restart:** The saved register states are reloaded. The program counter is reset to the instruction that originally triggered the fault, and the CPU re-executes the instruction in user space.

## Primary Causes of Page Faults

Page faults are triggered by three primary execution behaviors:

- **Demand Paging:** Accessing a valid virtual page that has not yet been loaded into RAM from secondary storage.
- **Out-of-Bounds Access:** A program trying to reference virtual memory addresses that lie outside its allocated address space.
- **Permission Violations:** A process attempting to perform unauthorized operations, such as executing data blocks or modifying read-only memory segments.

## Classification of Page Faults

Operating systems categorize page faults based on how they are resolved:

### 1. Minor Page Fault (Soft Fault)

A minor page fault occurs when the requested page resides in physical RAM but is not currently mapped in the calling process's page table.

- *Example:* A shared library block (such as `libc`) is already loaded in RAM because another active program is executing it. The OS resolves the fault simply by mapping the existing physical frame to the new process's page table, bypassing disk I/O entirely.

### 2. Major Page Fault (Hard Fault)

A major page fault occurs when the requested page is not present in physical RAM and must be fetched from secondary disk storage.

- *Example:* A process accesses a section of compiled user code that has not been read from the binary executable file on disk yet, requiring disk read latency.

### 3. Invalid Page Fault

An invalid page fault occurs when a process attempts to reference an invalid address. The OS cannot resolve this fault and terminates the process, generating a **Segmentation Fault** or **Access Violation** error.

## System Performance Impact

Frequent page faults impact operating system throughput in several ways:

- **Swap Latency:** Accessing secondary storage is significantly slower than reading RAM, causing program execution to pause during disk read cycles.
- **CPU Starvation:** Excessive major page faults force the processor to remain idle while waiting for disk transfer operations to complete, reducing overall CPU utilization.
- **Thrashing:** If page faults occur too frequently, the system spends more time executing replacement algorithms and swapping pages than running application logic, causing the system to freeze.

> **Note:** Page faults are a standard mechanism for implementing virtual memory. While minor page faults are resolved quickly in RAM with zero disk overhead, major page faults involve disk reads that interrupt execution and can degrade performance if they occur frequently.

## Summary

A page fault is an MMU-generated exception that halts process execution when a referenced virtual page is not mapped in physical RAM. By executing a sequence of kernel steps—saving states, checking validation, allocating frames, performing page replacement, updating page tables, and restarting the faulting instruction—the operating system manages memory transparently. While minor page faults are resolved instantly inside RAM, major page faults require disk access. Operating systems must control page fault rates to prevent thrashing, latency, and CPU starvation.




