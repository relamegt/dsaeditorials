# Process Control Block (PCB) in Operating System

A **Process Control Block (PCB)** is a special data structure maintained by the operating system to store all the information related to a process. It enables the operating system to manage, monitor, and control the execution of processes efficiently.

Every process created in the system has its own PCB. Whenever the operating system needs information about a process, it accesses the corresponding PCB.

## Key Features of Process Control Block

- Every process is assigned a unique **Process ID (PID)** for identification.
- Stores important information such as process state, program counter, CPU registers, stack pointer, scheduling details, and open files.
- Updated automatically whenever the process changes its state (Ready, Running, Waiting, etc.).
- Contains scheduling information like **process priority** and **CPU time quantum**.
- All PCBs are maintained in a **Process Table**, which stores information about every active process in the system.

## PCB Structure

The Process Control Block contains several fields that help the operating system manage a process efficiently.

### PCB Storage

The PCB is stored in the **kernel space** of the operating system, making it inaccessible to normal users. Since it contains critical process information, only the operating system can access and modify it.

In many operating systems, the PCB is placed near the process's **kernel stack**, providing a secure and efficient location for storing process-related information.

## Components of a Process Control Block

### 1. Process State

This field indicates the current status of a process.

Common process states include:

- New
- Ready
- Running
- Waiting (Blocked)
- Terminated

The operating system updates this field whenever the process changes its execution state.

### 2. Process ID (PID)

Each process is assigned a unique identification number called the **Process ID (PID)**.

The PID helps the operating system distinguish one process from another and perform operations such as scheduling, monitoring, and termination.

### 3. Program Counter

The **Program Counter (PC)** stores the address of the next instruction that the CPU will execute when the process resumes execution.

This information is essential during context switching because it allows the process to continue from the exact point where it was interrupted.

### 4. CPU Registers

The PCB stores the values of all CPU registers associated with the process.

When a process is interrupted or its time slice expires:

- The current register values are saved in the PCB.
- Another process is loaded into the CPU.
- When the original process gets CPU time again, the saved register values are restored from the PCB.

This mechanism makes **context switching** possible.

### 5. Memory Management Information

This field contains details about the memory allocated to the process.

Depending on the memory management technique used by the operating system, it may include:

- Page Tables
- Segment Tables
- Base and Limit Registers
- Memory allocation details

These details help the operating system manage the process memory efficiently.

### 6. List of Open Files

The PCB keeps track of all files currently opened by the process.

This information may include:

- File descriptors
- Input and output files
- Network sockets
- Other I/O resources

The operating system uses this information to manage file operations and release resources when the process terminates.

## Process Table

The operating system maintains a **Process Table**, which is a collection (or array) of Process Control Blocks.

Each entry in the Process Table corresponds to one active process in the system.

The operating system searches this table whenever it needs information about a particular process.

## Applications of Process Control Block

The Process Control Block plays a vital role in process management. Its major applications include:

- Enables the operating system to schedule processes efficiently.
- Helps allocate CPU time according to scheduling policies.
- Improves resource utilization by maintaining resource usage information.
- Supports **context switching** by saving and restoring CPU registers and execution details.
- Assists in process synchronization by tracking waiting processes and required resources.
- Monitors process states and resource usage to determine which process should execute next.

## Summary

A **Process Control Block (PCB)** is one of the most important data structures in an operating system because it stores all the information required to manage a process. It contains details such as the process state, PID, program counter, CPU registers, memory management information, scheduling details, and open files. During context switching, the operating system saves and restores process information using the PCB, ensuring smooth execution of multiple processes. Together with the Process Table, the PCB allows the operating system to efficiently schedule processes, manage resources, and maintain overall system performance.




