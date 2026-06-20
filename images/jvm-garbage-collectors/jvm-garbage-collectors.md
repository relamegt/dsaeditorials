# JVM Garbage Collectors

## Introduction

In the Java Virtual Machine (JVM), **Garbage Collectors** are background execution engines responsible for automatic heap memory management. They dynamically identify, track, and reclaim memory occupied by objects that are no longer reachable from any active execution path (GC Roots) in the application. By automating memory management, JVM Garbage Collectors prevent memory leaks, eliminate manual deallocation bugs, and optimize the overall performance of Java applications.

Whenever a Java program instantiates a new object, the JVM allocates a block of memory from the Heap. As objects are discarded or go out of scope, they accumulate as unreferenced data. If left unchecked, this unused memory would eventually fill the Heap, resulting in a system crash. The Garbage Collector solves this by periodically scanning the Heap, identifying unreferenced objects, reclaiming their memory, and compacting the remaining space.

## Basic Demo: Object Reachability and GC Eligibility

Below is a complete Java program demonstrating how objects transition from being active to eligible for garbage collection.

```java
class DataPayload {
    private String id;
    private byte[] buffer;

    public DataPayload(String id, int size) {
        this.id = id;
        this.buffer = new byte[size];
    }
}

public class GarbageCollectionDemo {
    public static void main(String[] args) {
        // 'payload' holds the reference to the newly instantiated DataPayload object in Heap Memory
        DataPayload payload = new DataPayload("TX-900", 1024 * 1024);

        // The reference is set to null. The DataPayload object is now unreachable 
        // from any GC Root on the Stack and becomes eligible for Garbage Collection.
        payload = null; 
    }
}
```

- When `payload` is assigned `null`, the reference path to the `DataPayload` object is severed.
- The next time the Garbage Collector runs, it detects this unreachable object, reclaims the 1MB buffer, and frees the memory for future object allocations.

# Threads in Garbage Collection

Garbage collection operations consume CPU cycles. Depending on the size of the heap and the latency requirements of the application, developers must configure how the JVM manages garbage collection threads and pause times.

## 1. Controlling Garbage Collection Threads

For multi-threaded collectors (such as Parallel GC and G1 GC), the JVM allows developers to explicitly set the number of threads allocated for parallel GC tasks. This is configured using the `-XX:ParallelGCThreads` JVM flag.

### Command Line Implementation

To limit the Parallel Garbage Collector to exactly 4 GC threads:

```bash
java -XX:+UseParallelGC -XX:ParallelGCThreads=4 -jar ApplicationJar.java
```

## 2. Limiting GC Pause Time

In latency-sensitive applications (like web servers or trading systems), long garbage collection pauses (Stop-The-World events) can degrade performance. Developers can suggest a maximum pause target in milliseconds using the `-XX:MaxGCPauseMillis` flag. The JVM will dynamically adjust heap region sizes and collection strategies to try to stay within this limit.

### Command Line Implementation

To suggest a maximum GC pause time target of 200 milliseconds:

```bash
java -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -jar ApplicationJar.java
```

# Types of JVM Garbage Collectors

The JVM provides several Garbage Collector algorithms, each optimized for different heap sizes, execution throughputs, and latency limits:

## 1. Serial Garbage Collector

The **Serial Garbage Collector** is the simplest GC algorithm in the JVM. It uses a single thread for all garbage collection tasks. When running, it pauses all application threads (Stop-The-World event) to perform its work.

- **Best Use Case**: Single-processor systems, small applications with heaps under 100MB, or background CLI utilities.
- **Command Line Configuration**:

`````bash
java -XX:+UseSerialGC -jar ApplicationJar.java
```

## 2. Parallel Garbage Collector

The **Parallel Garbage Collector** (the default collector in Java 8) uses multiple threads to perform garbage collection, focusing on maximizing application throughput. Although it pauses application threads during GC, it completes the collection much faster than the Serial collector on multi-core systems.

- **Best Use Case**: Batch processing, data analysis, and backend jobs where high throughput is required and brief pauses are acceptable.
- **Command Line Configuration**:

`````bash
java -XX:+UseParallelGC -jar ApplicationJar.java
```

## 3. Concurrent Mark-Sweep (CMS) Collector

The **CMS Collector** is designed to minimize pause times by performing most garbage collection phases concurrently with application threads. While it reduces latency, it consumes more CPU resources and can cause heap fragmentation because it does not perform memory compaction.

- **Status**: Deprecated in Java 9 and completely removed in Java 14.
- **Command Line Configuration**:

`````bash
java -XX:+UseConcMarkSweepGC -jar ApplicationJar.java
```

## 4. G1 (Garbage-First) Garbage Collector

The **G1 GC** (the default collector since Java 9) divides the Heap into multiple equal-sized regions. It tracks the amount of reclaimable garbage in each region and collects the regions with the most garbage first (hence "Garbage-First"). It supports large heaps (4GB+) and provides predictable, user-configured pause times.

- **Best Use Case**: Enterprise web applications, cloud microservices, and databases with large heaps where predictable pause times are required.
- **Command Line Configuration**:

`````bash
java -XX:+UseG1GC -jar ApplicationJar.java
```

## 5. Z Garbage Collector (ZGC)

The **ZGC** (introduced in Java 11) is a scalable, low-latency garbage collector. It executes all major GC phases concurrently with application threads, keeping Stop-The-World pauses under 1 millisecond regardless of the heap size (supporting heaps up to multiple terabytes).

- **Best Use Case**: Latency-critical enterprise services, real-time streaming, and high-frequency trading platforms.
- **Command Line Configuration**:

`````bash
java -XX:+UseZGC -jar ApplicationJar.java
```

## 6. Shenandoah Garbage Collector

The **Shenandoah GC** (introduced in Java 12) is an ultra-low-latency collector that performs object compaction concurrently with active application threads. This ensures that pause times remain independent of heap size.

- **Best Use Case**: High-performance, latency-sensitive services where low pause times are required.
- **Command Line Configuration**:

`````bash
java -XX:+UseShenandoahGC -jar ApplicationJar.java
```

# Garbage Collection JVM Options

## 1. General JVM Memory Options

These parameters configure Heap boundaries, Metaspace limits, and debugging details:

| Option | Description | Example Usage |
| --- | --- | --- |
| `-Xms<size>` | Sets the initial heap allocation size. | `-Xms512m` (512 Megabytes) |
| `-Xmx<size>` | Sets the maximum heap allocation limit. | `-Xmx4g` (4 Gigabytes) |
| `-XX:MaxMetaspaceSize=<size>` | Sets the maximum limit for class metadata native memory. | `-XX:MaxMetaspaceSize=256m` |
| `-XX:+HeapDumpOnOutOfMemoryError` | Automatically generates a physical heap dump file when an OOM occurs. | Enabled by default in debugging environments. |
| `-XX:HeapDumpPath=<path>` | Specifies the file path where the heap dump will be saved. | `-XX:HeapDumpPath=/var/logs/dumps` |
| `-XX:+PrintGCDetails` | Prints detailed logs of garbage collection cycles, showing regions and duration. | Used to profile memory performance. |
| `-XX:+UseContainerSupport` | Optimizes JVM memory allocations to align with container limits (Docker/K8s). | Enabled by default in modern JDKs. |

## 2. Garbage Collector Selection & Tuning Options

These parameters select the garbage collection algorithm and configure its threads:

| Option | Description | Collector Type |
| --- | --- | --- |
| `-XX:+UseSerialGC` | Enables the single-threaded Serial Garbage Collector. | Serial GC |
| `-XX:+UseParallelGC` | Enables the multi-threaded Parallel Garbage Collector. | Parallel GC |
| `-XX:+UseConcMarkSweepGC` | Enables the CMS Garbage Collector (Removed in Java 14). | CMS GC |
| `-XX:+UseG1GC` | Enables the region-based G1 Garbage Collector (Default). | G1 GC |
| `-XX:+UseZGC` | Enables the ultra-low latency Z Garbage Collector. | ZGC |
| `-XX:+UseShenandoahGC` | Enables the low-latency Shenandoah Garbage Collector. | Shenandoah GC |
| `-XX:ParallelGCThreads=<n>` | Sets the number of garbage collection threads. | Parallel and G1 Collectors |
| `-XX:ParallelCMSThreads=<n>` | Sets the thread count for the CMS Garbage Collector. | CMS GC |
| `-XX:G1HeapRegionSize=<size>` | Sets the size of individual regions (ranges from 1MB to 32MB). | G1 GC |

# Summary

JVM Garbage Collectors are responsible for automatic heap memory management, freeing unused objects to prevent memory leaks and improve performance. The JVM provides different collectors optimized for various workloads: the single-threaded **Serial GC** for small heaps, the high-throughput **Parallel GC**, the region-based **G1 GC** (default in Java 9+), and the ultra-low latency concurrent collectors **ZGC** and **Shenandoah GC**. By configuring JVM flags, developers can set Heap boundaries, select the collector algorithm, adjust garbage collection thread counts, and set pause time targets to match application requirements.




