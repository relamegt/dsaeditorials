# Exception Handling in C++

Exception Handling is a mechanism in C++ that allows a program to detect and handle runtime errors gracefully without abruptly terminating execution.

In real-world software applications, unexpected situations may occur while a program is running. For example:

- A user may enter invalid input.
- A file may not exist.
- A database connection may fail.
- A division operation may attempt to divide by zero.
- An array index may go beyond its valid range.

Without exception handling, such situations can cause the program to crash unexpectedly. Exception handling provides a structured way to detect these errors and respond appropriately.

Instead of terminating the program immediately, C++ allows developers to throw an exception when an error occurs and catch that exception elsewhere in the program.

This makes applications more robust, reliable, and easier to maintain.

# Why Do We Need Exception Handling?

Consider an online learning platform such as AlphaKnowledge.
A student attempts to access a course using a course ID that does not exist.
Without exception handling:
Program crashes
With exception handling:
Course Not Found
Please Enter a Valid Course ID
The application continues running normally.

Exception handling helps in:

- Preventing program crashes.
- Separating error-handling code from normal logic.
- Improving program reliability.
- Making debugging easier.
- Handling unexpected runtime situations.

# What is an Exception?

An exception is an event that occurs during program execution and disrupts the normal flow of instructions.

Examples include:

- Division by zero.
- File opening failure.
- Invalid user input.
- Memory allocation failure.
- Accessing an invalid index.
- Network connection errors.

When such situations occur, an exception can be generated and handled appropriately.

# Components of Exception Handling

C++ exception handling mainly uses three keywords:

| Keyword | Purpose |
| --- | --- |
| try | Contains code that may generate an exception |
| throw | Used to generate an exception |
| catch | Handles the exception |

The flow is:
try → throw → catch

# Understanding try, throw and catch

The code that may produce an error is placed inside a try block.

If an error occurs, an exception is generated using throw.

The corresponding catch block receives and handles the exception.

## Syntax

```cpp
try
{
    // Risky code
}
catch(ExceptionType e)
{
    // Exception handling code
}
```

# First Exception Handling Program

## Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    try
    {
        int totalStudents = 100;
        int availableSections = 0;

        if(availableSections == 0)
        {
            throw "Cannot divide by zero sections";
        }

        cout << totalStudents / availableSections;
    }
    catch(const char* message)
    {
        cout << "Exception: " << message;
    }

    return 0;
}
```

### Output
Exception: Cannot divide by zero sections

### Explanation

The program attempts to divide students among sections.

Since the number of sections is zero, the program throws an exception.

The catch block receives the exception and displays an appropriate message instead of crashing.

# How Exception Handling Works

The execution follows these steps:
Step 1:
Enter try block

Step 2:
Error occurs

Step 3:
throw statement executes

Step 4:
Program leaves try block immediately

Step 5:
Matching catch block executes

Step 6:
Program continues normally

# Throwing Exceptions

The throw keyword is used to generate exceptions.

## Syntax

```cpp
throw value;
```

The value can be:

- Integer
- Character
- String
- Object
- Standard exception object

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/exception-handling-in-c/1781181800764-1101650b-306b-4ac7-8d79-92a194e550e6.png)

# Throwing Integer Exceptions

## Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int courseSeats = -5;

    try
    {
        if(courseSeats < 0)
        {
            throw -1;
        }
    }
    catch(int errorCode)
    {
        cout << "Invalid Seat Count. Error Code: "
             << errorCode;
    }

    return 0;
}
```

### Output
Invalid Seat Count. Error Code: -1

### Explanation

The program detects an invalid seat count.

Instead of continuing with incorrect data, it throws an integer exception.

# Types of Exceptions in C++

Exceptions can be categorized into three main types.

## 1. Built-in Exceptions

These use primitive data types.

Examples:

```cpp
throw 10;
throw 'A';
throw 5.5;
```

Although simple, they provide very little information about the actual problem.

# 2. Standard Exceptions

The C++ Standard Library provides predefined exception classes.

These are defined inside:

```cpp
#include <stdexcept>
```

Common standard exceptions include:

| Exception | Description |
| --- | --- |
| invalid_argument | Invalid argument passed |
| out_of_range | Index exceeds valid range |
| runtime_error | Runtime-related errors |
| overflow_error | Arithmetic overflow |
| underflow_error | Arithmetic underflow |
| bad_alloc | Memory allocation failure |

These exceptions provide detailed information through the `what()` function.

# Handling Standard Exceptions

## Example Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> marks = {80, 85, 90};

    try
    {
        cout << marks.at(10);
    }
    catch(out_of_range& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
vector::_M_range_check ...

### Explanation

The vector contains only three elements.

Trying to access index 10 generates an out_of_range exception which is handled using catch.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/exception-handling-in-c/1781181833880-c61a7289-55f1-408a-8f76-664781232d94.png)

# Understanding what()

The `what()` function provides a description of the exception.

## Example

```cpp
catch(exception& e)
{
    cout << e.what();
}
```

This helps programmers understand the reason behind the error.

# Custom Exceptions

Sometimes built-in exceptions are not sufficient.

In such cases, we can create our own exception classes.

Custom exceptions make programs more meaningful and easier to debug.

# Creating a Custom Exception

## Example Code

```cpp
#include <iostream>
#include <exception>
using namespace std;

class InvalidCourseException : public exception
{
public:

    const char* what() const noexcept override
    {
        return "Invalid Course Selected";
    }
};

int main()
{
    try
    {
        throw InvalidCourseException();
    }
    catch(InvalidCourseException& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Invalid Course Selected

### Explanation

A custom exception named InvalidCourseException is created.

Whenever an invalid course is selected, the exception can be thrown and handled.

# Catching Multiple Exceptions

A single try block can have multiple catch blocks.

This allows different errors to be handled differently.

## Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    try
    {
        int choice = 2;

        if(choice == 1)
        {
            throw 100;
        }
        else
        {
            throw "Invalid Selection";
        }
    }
    catch(int x)
    {
        cout << "Integer Exception";
    }
    catch(const char* msg)
    {
        cout << msg;
    }

    return 0;
}
```

### Output
Invalid Selection

## Catch Matching and Inheritance Rules

When catching exceptions of classes related by inheritance (e.g., base and derived exception classes), C++ matches catch blocks in the order they are written.

If a catch block for a base class exception appears before a catch block for a derived class exception, the base class block will intercept the exception. The derived class block will never be executed.

For this reason, always order catch blocks from the most specific (derived) to the most general (base).

### Incorrect Order Example

```cpp
try
{
    throw out_of_range("Index out of bounds");
}
catch(exception& e) // Base class caught first
{
    cout << "Caught base exception: " << e.what();
}
catch(out_of_range& e) // Unreachable block
{
    cout << "Caught out_of_range";
}
```

### Correct Order Example

```cpp
try
{
    throw out_of_range("Index out of bounds");
}
catch(out_of_range& e) // Specific caught first
{
    cout << "Caught out_of_range: " << e.what();
}
catch(exception& e) // General caught as backup
{
    cout << "Caught base exception: " << e.what();
}
```

# Catch-All Handler

Sometimes we do not know what type of exception may occur.

For such situations, C++ provides a catch-all block.

## Syntax

```cpp
catch(...)
{
    // Handle any exception
}
```

## Example

```cpp
try
{
    throw 3.14;
}
catch(...)
{
    cout << "Unknown Exception";
}
```

### Output
Unknown Exception

# Catching Exceptions by Value

An exception object can be copied into the catch block.

## Example

```cpp
catch(runtime_error e)
{
    cout << e.what();
}
```

This creates a copy of the exception object.

# Catching Exceptions by Reference

This is the preferred method.

## Example

```cpp
catch(runtime_error& e)
{
    cout << e.what();
}
```

### Advantages

- No object copying.
- Better performance.
- Supports polymorphism.
- Preserves original exception information.

# Exception Propagation

When an exception is thrown inside a function and not handled there, it travels upward through the function call stack.

This process is known as Exception Propagation.

## Example Flow

main()
  ↓
functionA()
  ↓
functionB()
  ↓
throw exception

The exception travels upward until a matching catch block is found.

# Stack Unwinding

When an exception occurs:

- Current function terminates.
- Local objects are destroyed.
- Control moves upward through the call stack.

This process is called Stack Unwinding.

It ensures proper cleanup of local resources.

# RAII and Exception Safety

Resource Acquisition Is Initialization (RAII) is a key design pattern in C++ that ties resource management (like memory, file handles, or network sockets) to object lifetime.

When an exception is thrown, stack unwinding automatically calls the destructors of all local objects on the stack.

By managing resources inside classes (such as `std::unique_ptr`, `std::vector`, or file streams), you guarantee that resources are automatically released when an exception is thrown, preventing resource leaks.

Because C++ relies on RAII, it does not need a `finally` block (unlike languages such as Java or C#).

# Exceptions in Constructors and Destructors

Handling exceptions in constructors and destructors requires special care:

### Constructors

If a constructor throws an exception, the object construction is considered incomplete.

The destructor of the throwing object will NOT be called. However, destructors of all fully constructed member variables and base classes WILL be called.

To prevent memory leaks when a constructor throws, use RAII or smart pointers to manage dynamically allocated memory.

### Destructors

Never throw exceptions from a destructor.

If a destructor throws an exception while another exception is already active (during stack unwinding), C++ will immediately call `std::terminate()` and abort the program.

Always catch all potential exceptions inside a destructor and prevent them from escaping.

# Nested Try-Catch Blocks

C++ allows try-catch blocks inside other try-catch blocks.

## Example Structure

```cpp
try
{
    try
    {
        throw 10;
    }
    catch(int e)
    {
        cout << "Inner Catch";
    }
}
catch(...)
{
    cout << "Outer Catch";
}
```

Nested exception handling is useful in large applications.

# Rethrowing Exceptions

Sometimes a function catches an exception but wants another function to handle it.

In such cases, the exception can be rethrown.

## Example

```cpp
catch(...)
{
    throw;
}
```

The same exception is passed to an outer catch block.

# Exception Specifications

Exception specifications indicate whether a function may throw exceptions.

## noexcept

Used when a function guarantees that it will not throw exceptions.

```cpp
void display() noexcept
{
}
```

## noexcept(false)

Indicates that exceptions may occur.

```cpp
void process() noexcept(false)
{
}
```

# Common Runtime Errors Handled Using Exceptions

### Division by Zero

Arithmetic Error

### File Not Found

File Handling Error

### Invalid Input

Input Validation Error

### Array Index Out of Range

Boundary Error

### Memory Allocation Failure

Memory Error

# Best Practices for Exception Handling

### Use Exceptions Only for Exceptional Situations

Do not use exceptions for normal program logic.

### Catch Exceptions by Reference

```cpp
catch(exception& e)
```

is preferred over

```cpp
catch(exception e)
```

### Use Standard Exceptions Whenever Possible

They provide meaningful error information.

### Avoid Empty Catch Blocks

Bad Practice:

```cpp
catch(...)
{
}
```

Exceptions should be handled properly.

### Release Resources Properly

Use smart pointers and RAII to prevent memory leaks.

### Provide Meaningful Messages

Helpful messages make debugging easier.

# Advantages of Exception Handling

### Improves Program Stability

Programs do not crash unexpectedly.

### Better Code Organization

Error handling remains separate from normal logic.

### Easier Maintenance

Errors can be located and fixed quickly.

### Supports Large Applications

Exception propagation enables layered error handling.

### Cleaner Code

Reduces excessive if-else error checking.

# Limitations of Exception Handling

### Slight Runtime Overhead

Exception handling introduces additional processing.

### Can Increase Complexity

Poorly designed exception hierarchies become difficult to manage.

### Improper Handling May Hide Bugs

Ignoring exceptions can make debugging harder.

### Not Suitable for Regular Flow Control

Exceptions should represent exceptional situations only.

# Summary

Exception Handling in C++ is a mechanism used to manage runtime errors gracefully without terminating the program abruptly. It uses the try, throw, and catch keywords to detect and handle abnormal situations such as invalid input, division by zero, memory allocation failures, and file handling errors. C++ supports built-in exceptions, standard exceptions, and custom exceptions, allowing developers to build reliable and fault-tolerant applications. Proper exception handling improves program stability, maintainability, readability, and overall software quality.




