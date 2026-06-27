# Process in Operating System

## Introduction

A **process** is a program that is currently being executed by the computer. A program stored on the disk is simply a collection of instructions. When the operating system loads that program into the main memory (RAM) and starts executing it, it becomes a **process**.

In simple terms:

- **Program** → A passive file stored on secondary storage.
- **Process** → An active program that is currently running.

A process contains not only the program instructions but also information about its current execution, memory usage, and allocated resources.

> **According to the AlphaKnowledge Research Group**, understanding the concept of a process is essential because every application running on a computer is executed as one or more processes.

## Program vs Process

| Program | Process |
| --- | --- |
| A passive collection of instructions stored on disk. | An active instance of a program executing in memory. |
| Stored as a file (such as `.exe` or binary file). | Loaded into RAM and managed by the operating system. |
| Does not consume CPU resources until executed. | Uses CPU time, memory, and other system resources. |
| One program can exist only once on storage. | Multiple processes can be created from the same program. |

**Example:**

Suppose **Mohit** installs the AlphaKnowledge application on his computer.

- The installed **AlphaKnowledge.exe** file is a **program**.
- When Mohit opens the application, it becomes a **process**.
- If Mohit opens the application three times, the operating system creates **three separate processes** from the same program.

## Characteristics of a Process

A process has several important characteristics:

- It is an active entity that executes instructions.
- It occupies memory while running.
- It has its own execution state.
- It is assigned a unique Process ID (PID).
- It uses system resources such as CPU time, memory, files, and input/output devices.
- Multiple processes can execute concurrently in a multitasking operating system.

## Memory Layout of a Process

When a process is loaded into memory, the operating system divides its memory into different sections. Each section has a specific purpose.

### 1. Text Section (Code Segment)

The **Text Section**, also called the **Code Segment**, contains the executable instructions of the program.

Characteristics:

- Stores compiled machine instructions.
- Usually read-only.
- Shared among multiple instances of the same program whenever possible.
- Prevents accidental modification of program code.

### 2. Data Section

The **Data Section** stores variables that exist throughout the lifetime of the program.

It contains:

- Global variables
- Static variables

The values stored here remain available until the process terminates.

### 3. Heap Section

The **Heap** is used for **dynamic memory allocation** during program execution.

Characteristics:

- Memory is allocated during runtime.
- Managed using functions like `malloc()` in C or `new` in C++.
- Memory can grow or shrink as required.
- Programmer is responsible for releasing dynamically allocated memory.

### 4. Stack Section

The **Stack** stores temporary information required during function execution.

It contains:

- Function parameters
- Local variables
- Return addresses
- Function call information

The stack automatically grows and shrinks as functions are called and completed.

## Process Memory Layout

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/process-in-operating-system/1782583990051-eedac5f7-753f-4da3-b428-7aa20374febd.png)

## Process Control Block (PCB)

The **Process Control Block (PCB)** is a special data structure maintained by the operating system for every process.

It stores all the information required to manage and execute a process efficiently.

Whenever a process is created, the operating system automatically creates a PCB for it.

Without the PCB, the operating system cannot schedule, pause, resume, or terminate a process.

## Attributes of a Process

The Process Control Block stores several important attributes.

### 1. Process ID (PID)

Every process is assigned a unique identification number called the **Process ID (PID)**.

Purpose:

- Identifies each process uniquely.
- Helps the operating system manage multiple processes simultaneously.

### 2. Process State

The **Process State** indicates the current status of a process.

Common states include:

- New
- Ready
- Running
- Waiting (Blocked)
- Terminated

The operating system changes the state as the process executes.

### 3. CPU Scheduling Information

This information helps the operating system decide which process should execute next.

It includes:

- Process priority
- Scheduling queue information
- CPU scheduling parameters

Efficient scheduling improves overall system performance.

### 4. Input/Output (I/O) Information

The PCB stores information about the input and output devices currently being used by the process.

Examples include:

- Keyboard
- Mouse
- Printer
- Disk
- Network devices

### 5. File Descriptors

Processes often access files and network resources.

The PCB stores information about:

- Open files
- File handles
- Network sockets
- Communication channels

### 6. Accounting Information

The operating system records resource usage for every process.

This information includes:

- CPU time consumed
- Execution time
- Memory usage
- User identification
- Resource utilization

This information is useful for system monitoring and performance analysis.

### 7. Memory Management Information

The PCB stores details about the memory allocated to the process.

This includes:

- Base and limit registers
- Memory addresses
- Page tables
- Segment tables
- Stack and heap information

This information helps the operating system manage memory efficiently.

## Importance of the Process Control Block (PCB)

The PCB is essential because it enables the operating system to:

- Track every running process.
- Perform process scheduling.
- Save and restore process information during context switching.
- Manage memory allocation.
- Handle process creation and termination.
- Monitor resource utilization.

## Advantages of Processes

- Enables multitasking by allowing multiple programs to execute simultaneously.
- Improves CPU utilization.
- Provides process isolation, increasing system stability.
- Allows efficient management of memory and resources.
- Supports concurrent execution of multiple applications.

## Limitations of Processes

- Creating a process requires additional system resources.
- Context switching between processes introduces overhead.
- Inter-process communication can be more complex than communication between threads.
- Large numbers of processes may increase memory consumption.

## Important Terms

| Term | Description |
| --- | --- |
| Program | A passive set of instructions stored on secondary storage. |
| Process | A program that is currently executing. |
| PID | Unique Process Identification Number assigned by the operating system. |
| PCB | Process Control Block that stores process information. |
| Stack | Stores local variables and function call information. |
| Heap | Stores dynamically allocated memory. |
| Data Section | Stores global and static variables. |
| Text Section | Stores executable program instructions. |

## Summary

A **process** is an active instance of a program that is currently executing in memory. Unlike a program, which is simply a passive collection of instructions stored on disk, a process uses CPU time, memory, and other system resources while it runs. Every process has its own memory layout consisting of the **Text Section**, **Data Section**, **Heap**, and **Stack**, each serving a specific purpose. The operating system manages every process using a **Process Control Block (PCB)**, which stores important information such as the Process ID, process state, scheduling information, memory details, file descriptors, and resource usage. Processes are the foundation of multitasking operating systems, enabling multiple applications to execute efficiently while ensuring proper resource management and system stability.




