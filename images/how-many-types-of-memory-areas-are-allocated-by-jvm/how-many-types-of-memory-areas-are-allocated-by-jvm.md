# How Many Types of Memory Areas are Allocated by JVM?

## Introduction

The **Java Virtual Machine (JVM)** is the runtime engine responsible for executing Java applications. One of its most critical responsibilities is managing system memory. When a Java program starts, the operating system allocates a block of memory to the JVM. The JVM then organizes this block into distinct runtime data areas to store class metadata, active objects, local execution frames, thread instructions, and native system resources.

To support concurrent thread execution, garbage collection, and dynamic class loading, the JVM divides its memory into **five major runtime areas**:

1. **Method Area (Class Area)** (Thread-Shared)
2. **Heap Memory** (Thread-Shared)
3. **Stack Memory** (Thread-Isolated / Private)
4. **Program Counter (PC) Register** (Thread-Isolated / Private)
5. **Native Method Stack** (Thread-Isolated / Private)

Understanding these memory divisions is essential for Java developers to optimize application throughput, prevent memory leaks, tune Garbage Collection settings, and debug memory errors like stack overflows and heap out-of-memory errors.

# Example Program

Below is a complete, runnable Java program that illustrates the role of each JVM memory area during application execution.

```java
public class Main {
    // Stored in the Method Area (static field)
    static int staticVar = 100;

    public static void main(String[] args) {
        // Stored in Stack Memory (local primitive)
        int localVar = 10;

        // Student reference (student) on Stack; Object created in Heap Memory
        Student student = new Student("Mohit", 20);

        display(student);

        // Native method call tracked by the Native Method Stack
        System.gc();
    }

    static void display(Student s) { // Parameter reference (s) on Stack
        System.out.println(s.name + " - " + s.age);
    }
}

class Student {
    String name; // Instance field, stored in Heap Memory as part of the object
    int age;     // Instance field, stored in Heap Memory as part of the object

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### Output
Mohit - 20

### Step-by-Step Memory Tracing

1. **JVM Startup**: The JVM loads class files (`Main`, `Student`, etc.) and stores their definitions, schemas, and the static variable `staticVar` (value `100`) inside the **Method Area**.
2. **Thread Launch**: The JVM starts the main execution thread, allocating its private **Stack Memory** and **PC Register**.
3. **Frame Allocation**: The JVM pushes the stack frame for `main(String[] args)` onto the stack. The local primitive `localVar` (value `10`) is stored directly within this frame's local variable array.
4. **Heap Allocation**: The `new Student("Mohit", 20)` expression instantiates the `Student` object. The JVM allocates space for the object and its fields (`name`, `age`) inside **Heap Memory**.
5. **Reference Storage**: The reference variable `student` (which holds the memory address of the newly allocated Heap object) is saved inside the `main` stack frame.
6. **Method Invocation**: Calling `display(student)` pushes a new frame onto the Stack. The parameter reference `s` is stored in this new frame, pointing to the same `Student` object in the Heap.
7. **Native Code Tracing**: Invoking `System.gc()` triggers a native system call, allocating resources on the **Native Method Stack** for execution.

# JVM Memory Structure

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/how-many-types-of-memory-areas-are-allocated-by-jvm/1781963501198-f453167a-b7b5-48d6-9608-d31104e8f154.png)

# 1. Method Area (Class Area)

The **Method Area** is a shared runtime memory region created when the JVM starts up. It serves as the primary repository for class definitions and global application structures.

### Detailed Storage Types

- **Class Metadata**: Details about class definitions, interface extensions, modifier flags, and hierarchical bindings.
- **Method Information**: Bytecode instructions, method signatures, return types, parameter configurations, and access flags.
- **Static Fields**: Variables declared with the `static` modifier. They persist for the entire lifetime of the class loader.
- **Runtime Constant Pool**: Stores constant values (strings, numerical literals) and symbolic references resolved during class loading.

### Key Characteristics

- **Shared Access**: All threads in the JVM share access to this region, allowing threads to look up class metadata concurrently.
- **Garbage Collection**: The Method Area is subject to collection (mostly class unloading and constant pool collection), though it occurs much less frequently than in the Heap.
- **Metaspace Evolution**: In modern JVMs (Java 8+), the class metadata is stored in **Metaspace**, which is allocated directly in the operating system's native memory, preventing limits associated with the old PermGen implementation.

## Code Example: Static vs Instance Storage

```java
class College {
    static String name = "PVP Siddhartha"; // Saved in Method Area
    int studentCount = 1200;                // Saved in Heap Memory
}
```

# 2. Heap Memory

**Heap Memory** is the dynamic memory region allocated for storing object instances and arrays. Whenever your Java program uses the `new` keyword, the JVM allocates memory for the new object from the Heap.

### Generations within Heap Memory

To optimize Garbage Collection efficiency, Heap Memory is structured into regions based on object lifetimes:

1. **Young Generation**:

- **Eden Space**: The initial allocation space for new objects.
- **Survivor Spaces (S0 / S1)**: Objects that survive a minor GC in Eden are moved here. S0 and S1 alternate roles to prevent memory gaps (fragmentation).

1. **Old (Tenured) Generation**:

- Stores long-lived objects. Objects that survive a specified age threshold (typically surviving 15 GC cycles) are promoted from the Survivor space to the Old Generation.

1. **Metaspace / Native Memory**:

- In modern Java, class metadata resides in Metaspace, which is separate from the standard JVM heap and utilizes the host operating system's virtual memory.

## Code Example: Object Allocation

```java
Student s = new Student("Mohit", 20);
```

### Allocation Flow

- The JVM allocates space on the Heap to store the `Student` object, including its properties `name` (reference to String) and `age` (primitive integer).
- The address of this Heap block is returned and saved in the reference variable `s`, which resides on the Stack.

# 3. Stack Memory

**Stack Memory** is thread-local and manages the execution flow of method invocations and local variables. Each JVM thread has its own private Stack.

### The Stack Frame Structure

Every time a thread invokes a method, the JVM pushes a new **Stack Frame** onto the thread's Stack. When the method returns, this frame is popped. Each frame contains:

- **Local Variable Array**: Stores method parameters and local variables of primitive types (like `int`, `char`, `double`, `boolean`) and reference addresses pointing to Heap objects.
- **Operand Stack**: A workspace for executing intermediate calculations and pushing method return values.
- **Frame Data**: Contains references to the constant pool to support dynamic resolution, along with the method's exception table.

### Key Characteristics

- **Fast Execution**: Accessing stack memory requires only pointer increments/decrements, making it much faster than heap allocation.
- **Isolated Thread Safety**: Because stacks are thread-local, local variables cannot be accessed or modified by other threads.

## Code Example: Stack Frame Lifecycle

```java
public class Calculator {
    static void compute() {
        int x = 10; // Stored in the compute() stack frame
        int y = 20; // Stored in the compute() stack frame
        System.out.println(x + y);
    }

    public static void main(String[] args) {
        compute();
    }
}
```

### Execution Trace

- Running `main` pushes the `main()` frame onto the Stack.
- Invoking `compute()` pushes the `compute()` frame on top of `main()`.
- The local variables `x` and `y` are initialized inside the `compute()` frame.
- When `compute()` finishes, its frame is popped from the Stack, freeing its local variables.

# 4. Program Counter (PC) Register

The **Program Counter (PC) Register** is a thread-local memory region that tracks the thread's instruction execution path.

### Purpose and Execution Flow

The PC Register stores the address of the JVM instruction currently being executed by the thread.

- If the thread is executing a standard Java method, the PC Register points to its bytecode instruction address.
- If the thread is executing a native method (e.g., C/C++ libraries), the PC Register is undefined.

### Importance in Multithreading

In a multi-threaded JVM, the CPU switches execution slices among threads (context switching). When the CPU returns execution to a thread, the JVM checks the thread's PC Register to determine the exact instruction where execution should resume.

Thread 1 execution (Instruction #12)  ---&gt;  PC Register 1 = 12
Thread 2 execution (Instruction #45)  ---&gt;  PC Register 2 = 45
Thread 3 execution (Instruction #08)  ---&gt;  PC Register 3 = 8

# 5. Native Method Stack

The **Native Method Stack** supports the execution of native methods (usually written in C or C++) invoked via the Java Native Interface (JNI).

### Key Characteristics

- **Separate Execution Paths**: It is isolated from the standard Java stack, preventing native operations from corrupting Java stack frames.
- **Platform Dependent**: Unlike the Java Stack, which is defined by the JVM specifications, the Native Method Stack is implemented based on the host operating system's standards (such as DLL configurations on Windows or SO binaries on Linux).

## Code Example: Calling Native Methods

```java
public class SystemCall {
    public static void main(String[] args) {
        // Triggers native garbage collection logic, managed by the Native Method Stack
        System.gc();
    }
}
```

# Complete Memory Flow Example

Below is a detailed trace mapping a custom object and its fields to their respective memory allocations inside the JVM runtime.

```java
class Student {
    static String college = "PVP Siddhartha"; // Saved in Method Area
    String name;                              // Instance variable, saved in Heap

    Student(String name) {
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student("Mohit"); // Reference 's' on Stack; Object on Heap
    }
}
```

### Visual Representation of Memory Allocation

   

# Comparison of JVM Memory Areas

| Memory Area | Shared Across Threads? | Stores | Lifecycle | Access Speed |
| --- | --- | --- | --- | --- |
| **Method Area** | **Yes** | Class metadata, method bytecodes, static fields, constant pools. | Created on JVM startup; destroyed on JVM shutdown. | Medium (cached lookup). |
| **Heap Memory** | **Yes** | Object instances, instance fields, and array data. | Exists for JVM runtime; objects cleaned by GC. | Slower (dynamic pointers). |
| **Stack Memory** | **No** (Thread-Local) | Method frames, parameters, local primitives, and references. | Frame pushed on method call; popped on return. | Fastest (LIFO stack). |
| **PC Register** | **No** (Thread-Local) | Current JVM bytecode instruction address. | Created when thread starts; destroyed when thread dies. | Extremely Fast (native registers). |
| **Native Method Stack** | **No** (Thread-Local) | Native code execution logs (C/C++ method arguments). | Exists for thread execution lifetime. | High (direct system memory). |

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/how-many-types-of-memory-areas-are-allocated-by-jvm/1781963542547-b009d561-dda2-493f-bee8-24894155a888.png)

# Advantages of JVM Memory Division

- **Concise Execution Boundaries**: Separating class schemas (Method Area) from object instances (Heap) and execution paths (Stack) keeps JVM compilation stable.
- **Enhanced Multithreading Support**: Thread-local stacks, PC registers, and native stacks allow threads to run concurrently without block contention or synchronization overhead.
- **Efficient Automatic Garbage Collection**: The generational division of Heap memory allows collectors to focus on short-lived objects (Eden space), keeping pause times short.
- **Optimized Performance**: Small thread stacks and hardware-bound PC registers make execution fast, using JIT compiled paths for hot code.
- **Memory Safety**: Direct pointer access is restricted, protecting the host system from buffer overflow vulnerabilities.

# Limitations & Best Practices

- **Performance Overhead**: Generational collection and reference tracking require CPU cycles and memory resources.
- **GC Pauses**: Most collectors introduce brief pauses (Stop-The-World events) to inspect references, which can affect real-time systems.
- **Tuning Complexity**: Tuning parameters like `-Xms` (min heap), `-Xmx` (max heap), and `-Xss` (thread stack) requires profiling to prevent out-of-memory or stack overflow errors.

# 

# Summary

The JVM divides memory into five major runtime areas: **Method Area, Heap Memory, Stack Memory, Program Counter (PC) Register, and Native Method Stack**. The Method Area stores class-level information and static variables, Heap Memory stores objects and instance data, Stack Memory manages local variables and method execution, the Program Counter Register tracks the currently executing instruction, and the Native Method Stack supports the execution of native code. Together, these memory areas enable efficient execution, automatic memory management, multithreading support, and improved application performance in Java.




