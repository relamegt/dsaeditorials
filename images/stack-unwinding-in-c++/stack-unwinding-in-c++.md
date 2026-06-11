# Stack Unwinding in C++

Stack unwinding is the process through which the C++ runtime system removes function call frames from the call stack when an exception is thrown and not handled in the current function.

Whenever a function is called, a new stack frame is created. This frame stores:

- Local variables
- Function parameters
- Return address
- Temporary objects

When an exception occurs, C++ begins searching for a matching `catch` block.

If the current function does not contain a suitable catch block, the runtime:

1. Terminates the current function.
2. Destroys all local objects inside that function.
3. Removes its stack frame.
4. Moves to the calling function.
5. Continues searching for a matching catch block.

This process continues until:

- A matching catch block is found.
- The program terminates because no handler is available.

The automatic cleanup of local objects during exception propagation is known as **Stack Unwinding**.

# Why is Stack Unwinding Important?

Without stack unwinding, resources allocated inside functions would remain occupied whenever an exception occurs.

This could lead to:

- Memory leaks
- Open files remaining open
- Database connections not being released
- Locked resources remaining locked
- Program instability

Stack unwinding ensures that local objects are properly destroyed, making programs safer and more reliable.

# Function Call Stack Visualization

Consider the following sequence of function calls:
main()
  |
  v
processCourse()
  |
  v
loadStudentData()
  |
  v
validateRecord()
Suppose `validateRecord()` throws an exception.

The runtime begins unwinding the stack:
validateRecord()   ← Exception Thrown
        ↑
loadStudentData()  ← Removed
        ↑
processCourse()    ← Removed
        ↑
main()             ← Catch Block Found
Each function frame is removed one by one until a matching exception handler is found.

# Example: Basic Stack Unwinding

## Example Code

```cpp
#include <iostream>
using namespace std;

void validateRecord()
{
    cout << "Validating Record" << endl;

    throw 101;
}

void loadStudentData()
{
    cout << "Loading Student Data" << endl;

    validateRecord();

    cout << "Load Completed" << endl;
}

void processCourse()
{
    cout << "Processing Course" << endl;

    loadStudentData();

    cout << "Process Completed" << endl;
}

int main()
{
    try
    {
        processCourse();
    }
    catch(int errorCode)
    {
        cout << "Exception Caught: "
             << errorCode << endl;
    }

    return 0;
}
```

### Output
Processing Course
Loading Student Data
Validating Record
Exception Caught: 101

### Explanation

The exception is thrown from `validateRecord()`.

Since `validateRecord()` does not contain a matching catch block, the function terminates immediately.

The exception propagates to `loadStudentData()`, which also does not handle it.

The stack frame of `loadStudentData()` is removed.

Finally, the exception reaches `main()`, where it is caught and handled.

The statements after the exception in both functions are never executed.

# Destructors During Stack Unwinding

One of the most important features of stack unwinding is the automatic execution of destructors.

Whenever a local object goes out of scope due to exception propagation, its destructor is called automatically.

This ensures that resources are cleaned up correctly.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Course
{
public:

    Course()
    {
        cout << "Course Created" << endl;
    }

    ~Course()
    {
        cout << "Course Destroyed" << endl;
    }
};

void startLearning()
{
    Course cppCourse;

    throw runtime_error("Learning Error");
}

int main()
{
    try
    {
        startLearning();
    }
    catch(...)
    {
        cout << "Exception Handled" << endl;
    }

    return 0;
}
```

### Output
Course Created
Course Destroyed
Exception Handled

### Explanation

The local object `cppCourse` is created inside the function.

When the exception is thrown, stack unwinding begins.

Before leaving the function, the destructor of `cppCourse` is automatically executed.

This cleanup occurs even though the function terminates abnormally.

# Order of Destructor Calls

During stack unwinding, destructors are called in the reverse order of object creation.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Resource
{
    string name;

public:

    Resource(string n)
    {
        name = n;
        cout << name << " Created" << endl;
    }

    ~Resource()
    {
        cout << name << " Destroyed" << endl;
    }
};

void process()
{
    Resource r1("Database");

    Resource r2("File");

    Resource r3("Network");

    throw runtime_error("Error");
}

int main()
{
    try
    {
        process();
    }
    catch(...)
    {
        cout << "Exception Handled";
    }
}
```

### Output
Database Created
File Created
Network Created
Network Destroyed
File Destroyed
Database Destroyed
Exception Handled

### Explanation

Objects are destroyed in reverse order of their construction.

This ensures that dependent resources are released safely and correctly.

# Destructors Throwing During Unwinding (Double Exception)

A critical rule in C++ is that **destructors must never throw exceptions**, especially during stack unwinding.

If a destructor throws an exception while another exception is already active (propagating up the stack), the runtime environment has no way to handle both simultaneously. In this scenario, the program calls `std::terminate()` immediately.

Since C++11, destructors are implicitly `noexcept(true)`. If a destructor throws an exception and does not handle it internally, `std::terminate()` is called.

## Example Code

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class DatabaseConnection
{
public:

    ~DatabaseConnection() noexcept(false)
    {
        cout << "Closing Database Connection..." << endl;

        // Throwing an exception from a destructor
        throw runtime_error("Failed to close connection cleanly");
    }
};

void runQuery()
{
    DatabaseConnection conn;

    cout << "Executing query..." << endl;

    throw runtime_error("Query syntax error");
}

int main()
{
    try
    {
        runQuery();
    }
    catch(const exception& e)
    {
        cout << "Caught exception: " << e.what() << endl;
    }

    return 0;
}
```

### Output
Executing query...
Closing Database Connection...
terminate called after throwing an instance of 'std::runtime_error'
  what():  Failed to close connection cleanly

### Explanation

The function `runQuery()` throws a "Query syntax error" exception.

During stack unwinding, the destructor of `DatabaseConnection` is invoked.

Inside the destructor, a second exception "Failed to close connection cleanly" is thrown.

Since the first exception is still active and propagation is in progress, the throw of the second exception leads to an immediate call to `std::terminate()`. The catch block in `main()` is never reached.

# Uncaught Exceptions and std::terminate

If an exception propagates all the way up the call stack to `main()` (or the thread entry function) and no matching catch block is found, it is called an **uncaught exception**.

When an uncaught exception occurs:

1. The runtime calls `std::terminate()`.
2. By default, `std::terminate()` calls `std::abort()`, causing the program to crash.

## The Unwinding Guarantee

Whether the stack is unwound for uncaught exceptions is **implementation-defined** by the C++ compiler.

- Some compilers/platforms will unwind the stack and call destructors of local objects before calling `std::terminate()`.
- Other compilers/platforms will terminate the program immediately without executing any destructors.

Therefore, you should never rely on stack unwinding or destructors to release critical external resources if there is a chance the exception will go uncaught.

## Example Code

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class FileHandler
{
public:

    FileHandler()
    {
        cout << "File opened" << endl;
    }

    ~FileHandler()
    {
        cout << "File closed safely" << endl;
    }
};

void readFile()
{
    FileHandler fh;

    cout << "Reading file contents..." << endl;

    throw runtime_error("Disk read failure");
}

int main()
{
    // No try-catch block here to catch the exception
    readFile();

    return 0;
}
```

### Output
File opened
Reading file contents...
terminate called after throwing an instance of 'std::runtime_error'
  what():  Disk read failure

### Explanation

The exception is thrown inside `readFile()`.

Because there is no active `try-catch` block in `readFile()` or `main()`, the exception remains uncaught.

The runtime immediately calls `std::terminate()`. Note that depending on the compiler and operating system, the destructor of `FileHandler` (`File closed safely`) may or may not be called before termination.

# Stack Unwinding and RAII

RAII stands for:
Resource Acquisition Is Initialization

RAII is one of the most important programming techniques in modern C++.

The idea is simple:

- Acquire resources inside constructors.
- Release resources inside destructors.

When stack unwinding occurs, destructors automatically release resources.

Examples of resources include:

- Memory
- Files
- Database connections
- Network sockets
- Mutex locks

Because destructors are guaranteed to execute, resources are released safely even when exceptions occur.

# Stack Unwinding with Smart Pointers

Modern C++ recommends using smart pointers instead of raw pointers.

Smart pointers automatically release heap memory during stack unwinding.

## Example Code

```cpp
#include <iostream>
#include <memory>
using namespace std;

void processEnrollment()
{
    unique_ptr<int> students(
        new int(250));

    cout << "Students Enrolled: "
         << *students << endl;

    throw runtime_error(
        "Unexpected Error");
}

int main()
{
    try
    {
        processEnrollment();
    }
    catch(exception& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Students Enrolled: 250
Unexpected Error

### Explanation

The memory allocated using `new` is owned by `unique_ptr`.

When the exception is thrown, stack unwinding destroys the smart pointer.

The destructor of `unique_ptr` automatically releases the allocated memory.

No memory leak occurs.

# What Stack Unwinding Does Not Clean Automatically

Stack unwinding only destroys local stack-based objects.

It does not automatically free:

- Raw pointers allocated using `new`
- Resources not managed by objects
- Global variables
- Static variables

Example:

```cpp
int* ptr = new int(100);

throw runtime_error("Error");
```

In this example, the memory remains allocated because no destructor manages it.

This causes a memory leak.

# Common Uses of Stack Unwinding

Stack unwinding is heavily used in:

- File handling systems
- Database applications
- Network programming
- Banking applications
- Online learning platforms
- Operating systems
- Multithreaded applications

Any application that uses exceptions relies on stack unwinding for safe resource cleanup.

# Advantages of Stack Unwinding

- Automatic cleanup of local objects.
- Prevents many resource leaks.
- Supports exception-safe programming.
- Reduces manual cleanup code.
- Works naturally with RAII.
- Improves program reliability.

# Limitations of Stack Unwinding

- Does not automatically free raw heap memory.
- Improper resource management can still cause memory leaks.
- Excessive exception propagation may reduce readability.
- Uncaught exceptions terminate the program.

# Best Practices

- Use RAII-based design.
- Prefer smart pointers over raw pointers.
- Use STL containers such as vector, map, and string.
- Catch exceptions by reference.
- Avoid manual memory management whenever possible.
- Never throw exceptions from destructors.
- Keep destructors lightweight and safe.

# Summary

Stack unwinding is the process of removing function call frames when an exception propagates through the call stack. During this process, local objects are automatically destroyed and their destructors are executed in reverse order of creation. This mechanism guarantees proper cleanup of resources and forms the foundation of RAII and exception-safe programming in C++. By using smart pointers and standard library containers, developers can take full advantage of stack unwinding to write safer, cleaner, and more reliable applications.




