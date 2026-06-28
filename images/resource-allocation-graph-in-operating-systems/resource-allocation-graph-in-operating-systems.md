# Resource Allocation Graph in Operating Systems

A Resource Allocation Graph (RAG) is a directed graph used to model and analyze the state of resource allocations and pending requests in an operating system. Rather than relying solely on matrix tables, a RAG represents the relationships between active processes and system resources visually. This graphical model simplifies the process of identifying deadlocks and checking whether the system is in a safe or unsafe configuration.

## Vertices in a Resource Allocation Graph

The RAG contains two primary classes of nodes (vertices):

### Process Vertices

Every active process or thread in the system is represented as a process vertex, visually depicted as a circle.

### Resource Vertices

Every system resource (such as a database lock, memory block, or I/O device) is represented as a resource vertex, depicted as a rectangle. Resource vertices are divided into two types:

- **Single-Instance Resources:** Resources that contain only a single copy (instance). Represented as a rectangle containing a single internal dot. Only one process can utilize this resource at any given time.
- **Multi-Instance Resources:** Resources that contain multiple identical copies (instances) of the same type. Represented as a rectangle containing multiple internal dots. Several processes can hold separate instances of this resource concurrently.

## Edges in a Resource Allocation Graph

Edges in a RAG are directed and represent the state of access between processes and resources:

### Request Edges

A request edge indicates that a process is currently waiting to acquire a resource. It is represented as a directed arrow pointing from a process circle to a resource rectangle (Process -&gt; Resource). The process remains blocked in a waiting state as long as this edge exists.

### Assignment Edges

An assignment edge indicates that a resource instance has been allocated to a process. It is represented as a directed arrow pointing from a resource instance dot inside the rectangle to a process circle (Resource -&gt; Process).

## Cycle Analysis and Deadlock Detection

By examining the cycles in a Resource Allocation Graph, the operating system can detect deadlock conditions based on resource instance counts:

### Deadlock in Single-Instance Resource Graphs

In systems where every resource type has only a single instance, the presence of a cycle in the RAG is a necessary and sufficient condition for a deadlock.

- **Deadlocked Scenario:** If Thread A holds Lock X and requests Lock Y, while Thread B holds Lock Y and requests Lock X, a cycle forms: `Lock X -> Thread A -> Lock Y -> Thread B -> Lock X`. Because both resources are single-instance, both threads are permanently deadlocked.
- **Safe Scenario:** If Thread A and Thread B hold Lock X and Lock Y, and Thread C is waiting to acquire both locks, no circular dependency exists. Since there is no cycle, the system is safe and free of deadlocks.

### Deadlock in Multi-Instance Resource Graphs

In systems containing multi-instance resource types, the presence of a cycle in the graph is a necessary condition for a deadlock, but it is **not** a sufficient condition. A cycle may exist in the graph without the system being deadlocked.

#### 1. Multi-Instance Cycle Without Deadlock
Consider three threads (Thread A, Thread B, Thread C) and two resources: Lock X (1 instance) and Lock Y (2 instances).

- **Allocations:** Lock X is allocated to Thread A. Lock Y has one instance allocated to Thread B and another allocated to Thread C.
- **Outstanding Requests:** Thread A requests an instance of Lock Y. Thread B requests Lock X.
- **Available Resources:** {0, 0}

We construct the allocation and request tables:

| Process | Allocation (Lock X, Lock Y) | Request (Lock X, Lock Y) |
| --- | --- | --- |
| **Thread A** | {1, 0} | {0, 1} |
| **Thread B** | {0, 1} | {1, 0} |
| **Thread C** | {0, 1} | {0, 0} |

Analysis: A cycle exists in the graph: `Lock X -> Thread B -> Lock Y -> Thread A -> Lock X`. However, the system is not deadlocked. Thread C holds an instance of Lock Y but has no pending requests. Thread C can run to completion and release its instance of Lock Y. Once released, the available resource vector becomes {0, 1}, allowing Thread A's request to be satisfied. Thread A can then complete, release Lock X, and resolve Thread B's block, clearing the cycle.

#### 2. Multi-Instance Cycle With Deadlock
Using the same system setup, suppose Thread C now submits a request for Lock X:

| Process | Allocation (Lock X, Lock Y) | Request (Lock X, Lock Y) |
| --- | --- | --- |
| **Thread A** | {1, 0} | {0, 1} |
| **Thread B** | {0, 1} | {1, 0} |
| **Thread C** | {0, 1} | {1, 0} |

- **Available Resources:** {0, 0}

Analysis: The available resources are {0, 0}. Thread A requires Lock Y, while Thread B and Thread C both require Lock X. Because the free resources cannot satisfy the request of any thread, no thread can progress or release its allocated locks. In this case, the cycle in the multi-instance graph leads to a deadlock.

## Summary

A Resource Allocation Graph is a visual modeling tool that illustrates process-resource dependencies using circles, rectangles, request edges, and assignment edges. In single-instance systems, cycle detection is a sufficient check for deadlocks. In multi-instance systems, a cycle is necessary but not sufficient, requiring the system to evaluate allocation and request matrices dynamically to confirm deadlock conditions. RAGs provide operating system designers with a clean visual abstraction to trace and resolve circular blocking states.




