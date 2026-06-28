# Memory Interleaving in Computer Architecture

Memory interleaving is a hardware design technique used to increase memory access speed by dividing physical memory into multiple independent modules (banks) and accessing them in parallel. By distributing contiguous memory addresses across different banks in a round-robin fashion, the CPU can overlap access cycles, retrieving data from one module while another is completing a previous read or write cycle.

## Why Memory Interleaving is Required

A major bottleneck in modern computer architecture is the speed gap between the CPU and main memory (RAM):

- **Memory Bottleneck:** CPUs execute instructions orders of magnitude faster than physical RAM can supply data, causing the CPU to stall (remain idle) during memory accesses.
- **Overlapped Access:** Memory interleaving resolves this latency. While one memory bank is busy retrieving data, the CPU can immediately issue a request to another bank, keeping the data pipeline full.

## High-Order Interleaving (Consecutive Words in a Module)

In High-Order Interleaving, memory addresses are structured so that consecutive logical words are stored in the same physical memory module.

- **Address Bit Structure:** The Most Significant Bits (MSB) of the address bus designate the memory module (bank), while the Least Significant Bits (LSB) designate the internal word offset within that bank.
- **Access Characteristics:** Because consecutive memory locations reside in the same bank, sequential read operations keep one module busy while other modules remain idle, offering no parallel speedup for sequential access.

### Custom High-Order Trace Example

Suppose 16 data values (100 to 1600) are distributed across 4 memory modules (Bank 00, Bank 01, Bank 10, and Bank 11) using a 4-bit address bus:

- **Bank 00 (Bank 0):** Holds data `100` (0000), `200` (0001), `300` (0010), and `400` (0011)
- **Bank 01 (Bank 1):** Holds data `500` (0100), `600` (0101), `700` (0110), and `800` (0111)
- **Bank 10 (Bank 2):** Holds data `900` (1000), `1000` (1001), `1100` (1010), and `1200` (1011)
- **Bank 11 (Bank 3):** Holds data `1300` (1100), `1400` (1101), `1500` (1110), and `1600` (1111)

#### Address Translation Walkthrough
To retrieve the data `1100` (located at binary address `1010`):

1. The CPU puts address `1010` on the address bus.
2. The 2 MSBs (`10`) select the target module: **Bank 2 (Bank 10)**.
3. The 2 LSBs (`10`) select the internal offset: **Offset 2 (binary 10)** within Bank 2.

## Low-Order Interleaving (Consecutive Words in Consecutive Modules)

In Low-Order Interleaving, consecutive memory addresses are distributed across consecutive physical memory modules in a round-robin fashion.

- **Address Bit Structure:** The Least Significant Bits (LSB) of the address designate the memory module (bank), while the Most Significant Bits (MSB) designate the internal word offset.
- **Access Characteristics:** Since consecutive locations reside in different banks, sequential read operations (such as instruction streams or array traversals) access different modules in a round-robin cycle, allowing the system to overlap access latencies and achieve true parallel data transfers.

### Custom Low-Order Trace Example

Using the same 16 data values (100 to 1600) and 4 memory modules, low-order interleaving distributes the values round-robin:

- **Bank 00 (Bank 0):** Holds data `100` (0000), `500` (0100), `900` (1000), and `1300` (1100)
- **Bank 01 (Bank 1):** Holds data `200` (0001), `600` (0101), `1000` (1001), and `1400` (1101)
- **Bank 10 (Bank 2):** Holds data `300` (0010), `700` (0110), `1100` (1010), and `1500` (1110)
- **Bank 11 (Bank 3):** Holds data `400` (0011), `800` (0111), `1200` (1011), and `1600` (1111)

#### Address Translation Walkthrough
To retrieve the data `900` (located at binary address `1000`):

1. The CPU puts address `1000` on the address bus.
2. The 2 LSBs (`00`) select the target module: **Bank 0 (Bank 00)**.
3. The 2 MSBs (`10`) select the internal offset: **Offset 2 (binary 10)** within Bank 0.

## Benefits of Memory Interleaving

- **Higher Memory Bandwidth:** By accessing multiple memory banks in parallel, the system increases the total amount of data that can be transferred to the CPU per second.
- **Lower Effective Latency:** While one bank is completing a refresh or access cycle, other banks are ready to receive requests, reducing CPU wait times.
- **Improved System Throughput:** Together, higher bandwidth and lower latency improve performance, especially for memory-intensive tasks like video rendering, database queries, and parallel processing.

> **Note:** Memory interleaving increases throughput by distributing contiguous addresses across separate hardware memory banks. While high-order interleaving places consecutive words within the same module, low-order interleaving places consecutive words across different modules, allowing for parallel access during sequential data reads.

## Summary

Memory interleaving is a hardware technique designed to resolve the CPU-memory speed gap by partitioning RAM into multiple independent memory banks. High-order interleaving uses the MSB to select modules, keeping contiguous data in the same bank, which is simple but does not optimize sequential access speeds. Low-order interleaving uses the LSB to select modules, distributing consecutive words round-robin across different banks, which enables parallel access during sequential operations. This technique increases system bandwidth and reduces latency in modern multi-core computing architectures.




