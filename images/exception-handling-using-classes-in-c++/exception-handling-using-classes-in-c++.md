# Exception Handling using Classes in C++

Exception handling is one of the most important features of C++ that helps programs deal with unexpected situations during execution. Instead of abruptly terminating the program whenever an error occurs, C++ allows developers to detect, throw, catch, and handle errors in a controlled manner.

In real-world applications, errors are unavoidable. A student may enter an invalid roll number, a user may attempt to log in with incorrect credentials, a file may not exist, or a program may run out of memory. If such situations are not handled properly, the application may crash or produce incorrect results.

Exception handling provides a structured mechanism to manage these abnormal conditions and allows the program to continue executing safely.

When working with exception handling, developers often use classes to represent different categories of errors. These classes can store additional information about the error and provide meaningful messages to the user.

## Why Use Classes for Exception Handling?

Although C++ allows throwing simple values such as integers, characters, or strings, this approach is not recommended for large applications.

For example:

```cpp
throw 101;
```

The number `101` itself does not explain what actually went wrong.

Instead, we can create a dedicated exception class:

```cpp
throw InvalidCourseException();
```

This immediately tells the programmer that the error is related to course validation.

Using classes for exception handling provides:

- Better readability.
- Better maintainability.
- Detailed error information.
- Support for inheritance.
- Easy integration with large projects.

## Real-World Example

Consider an online learning platform called **AlphaKnowledge**.

A student attempts to enroll in a course.

Possible problems include:

- Course does not exist.
- Course is already full.
- Student has not completed prerequisites.
- Payment failed.

Instead of using numeric error codes, we can represent each error using separate exception classes.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/exception-handling-using-classes-in-c/1781182534565-4f459b0f-a099-4b25-a25a-1e6e9a3fbd86.png)

Each error can be represented by a separate exception class.

# Built-In Exception Classes

The C++ Standard Library already provides several predefined exception classes.

These classes are useful for handling common runtime errors.

Most of these exception classes are derived from the base class:

```cpp
std::exception
```

The base class provides the virtual function:

```cpp
what()
```

which returns a descriptive message about the exception.

## Common Built-In Exception Classes

| Exception Class | Purpose |
| --- | --- |
| exception | Base class for standard exceptions |
| runtime_error | Runtime related errors |
| logic_error | Logical errors in program |
| invalid_argument | Invalid function arguments |
| out_of_range | Access outside valid range |
| overflow_error | Arithmetic overflow |
| underflow_error | Arithmetic underflow |
| bad_alloc | Memory allocation failure |
| ios_base::failure | File/Input-Output failures |
| bad_cast | Invalid type casting |

These exceptions save development time because many common errors are already represented.

### Standard Exception Class Hierarchy Diagram

The relationships between standard exception classes can be structured hierarchically:

```cpp
std::exception (Base Class)
       ├── std::logic_error
       │         ├── std::invalid_argument
       │         ├── std::domain_error
       │         ├── std::length_error
       │         └── std::out_of_range
       └── std::runtime_error
                 ├── std::range_error
                 ├── std::overflow_error
                 ├── std::underflow_error
                 └── std::system_error
```

In C++, `std::logic_error` represents errors that could have been prevented through correct program logic (such as passing invalid arguments), while `std::runtime_error` represents errors that are caused by events outside the control of the program (such as mathematical overflow or system failures).

## Example: Using a Standard Exception

Suppose an AlphaKnowledge student enters an invalid course fee.

### Example Code

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

int main()
{
    int courseFee = -1000;

    try
    {
        if(courseFee < 0)
        {
            throw invalid_argument(
                "Course fee cannot be negative"
            );
        }

        cout << "Course Registered";
    }

    catch(const invalid_argument& e)
    {
        cout << "Error: "
             << e.what();
    }

    return 0;
}
```

### Output
Error: Course fee cannot be negative

### Explanation

The program checks whether the entered course fee is valid.

Since the fee is negative, an `invalid_argument` exception is thrown.

The catch block catches the exception and displays a meaningful message using the `what()` function.

The program handles the error gracefully instead of crashing.

# Creating Custom Exception Classes

Although standard exceptions cover many situations, real-world applications often require specialized exceptions.

For example:

- StudentNotFoundException
- InvalidCourseException
- EnrollmentFailedException
- PaymentFailedException
- LibraryBookUnavailableException

These exceptions are specific to business logic and therefore must be created by developers.

## Method 1: Inheriting from std::exception

This is the most commonly used approach.

The custom exception class inherits from `std::exception` and overrides the `what()` function.

### Example Code

```cpp
#include <iostream>
#include <exception>
using namespace std;

class InvalidCourseException
    : public exception
{
public:

    const char* what()
    const noexcept override
    {
        return "Selected course does not exist.";
    }
};

int main()
{
    try
    {
        throw InvalidCourseException();
    }

    catch(const InvalidCourseException& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Selected course does not exist.

### Explanation

The custom exception class inherits from `std::exception`.

The `what()` method is overridden to return a custom error message.

When the exception is thrown, the catch block displays the message returned by `what()`.

This approach integrates perfectly with the standard exception hierarchy.

## Method 2: Inheriting from runtime_error

Sometimes we want to provide custom messages dynamically.

In such situations, inheriting from `runtime_error` is a better choice.

### Example Code

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class EnrollmentException
    : public runtime_error
{
public:

    EnrollmentException(
        const string& msg
    )
    : runtime_error(msg)
    {
    }
};

int main()
{
    try
    {
        throw EnrollmentException(
            "Enrollment limit exceeded"
        );
    }

    catch(const EnrollmentException& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Enrollment limit exceeded

### Explanation

The custom class inherits from `runtime_error`.

The constructor receives a custom message.

The message is passed to the parent class and later returned by `what()`.

This method is useful when different situations require different messages.

## Method 3: Creating an Independent Exception Class

A custom exception can also be created without inheriting from any standard exception.

### Example Code

```cpp
#include <iostream>
using namespace std;

class PaymentException
{
private:

    string message;

public:

    PaymentException(
        string msg
    )
    {
        message = msg;
    }

    const char* what() const
    {
        return message.c_str();
    }
};

int main()
{
    try
    {
        throw PaymentException(
            "Payment gateway unavailable"
        );
    }

    catch(const PaymentException& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Payment gateway unavailable

### Explanation

The exception class is completely independent.

It stores a custom message and provides a `what()` function.

Although this method offers flexibility, it does not integrate with the standard exception hierarchy.

Therefore, inheriting from `std::exception` is generally preferred.

# Comparison of Different Exception Class Approaches

| Method | Advantages | Disadvantages |
| --- | --- | --- |
| Inheriting from std::exception | Standard compliant and widely used | Fixed message unless customized |
| Inheriting from runtime_error | Supports custom messages easily | Slightly more complex |
| Independent Class | Complete flexibility | Does not integrate with standard exception hierarchy |

# Benefits of Using Exception Classes

Using exception classes offers several advantages:

- Provides meaningful error messages.
- Makes debugging easier.
- Supports inheritance and polymorphism.
- Improves readability.
- Allows grouping related exceptions.
- Integrates with standard library exception handling.
- Makes large applications easier to maintain.

# Real-World Applications

Exception classes are heavily used in modern software systems such as:

- Banking Applications
- Hospital Management Systems
- E-Commerce Platforms
- Online Learning Portals
- Library Management Systems
- Flight Reservation Systems
- Cloud Computing Services
- Database Management Systems

Whenever a business rule is violated, a dedicated exception class can be thrown to clearly describe the problem.

### Example Scenarios

| Application | Possible Exception |
| --- | --- |
| Banking System | InsufficientBalanceException |
| E-Commerce Website | ProductOutOfStockException |
| Online Learning Platform | CourseNotFoundException |
| Hospital System | PatientRecordNotFoundException |
| Library Management System | BookUnavailableException |

# Polymorphic Exceptions and Object Slicing

When throwing and catching exception classes, it is critical to catch exceptions by reference (preferably `const` reference) rather than by value.

If you catch a derived exception class object by value using a base class handler, C++ will perform **Object Slicing**. This means the derived portion of the object is discarded, and only the base class portion is copied into the catch block.

As a result:

- The virtual method `what()` will call the base class implementation instead of the derived class override.
- Any custom member variables or functions added in the derived exception class will be lost.

### Object Slicing Example (Catching by Value)

```cpp
try
{
    throw InvalidCourseException(); // Derived from std::exception
}
catch(exception e) // Caught by value (Slicing occurs)
{
    cout << e.what(); // Outputs base message instead of "Selected course does not exist."
}
```

### Polymorphic Catch Example (Catching by Reference)

```cpp
try
{
    throw InvalidCourseException();
}
catch(const exception& e) // Caught by reference (Polymorphism preserved)
{
    cout << e.what(); // Outputs "Selected course does not exist."
}
```

# Best Practices for Custom Exceptions

When creating custom exceptions, follow these guidelines:

- Prefer inheriting from `std::exception`.
- Override the `what()` method.
- Use meaningful exception names.
- Catch exceptions by constant reference.
- Avoid throwing primitive data types such as integers.
- Create different exception classes for different error categories.
- Use exception messages that clearly describe the problem.

# Summary

Exception handling using classes provides a powerful and organized way to manage runtime errors in C++. Instead of throwing simple values such as integers or strings, developers can create dedicated exception classes that clearly represent different error conditions.

Key points to remember:

- Exception classes represent specific error types.
- Standard exceptions are derived from `std::exception`.
- The `what()` function returns information about the error.
- Custom exception classes can inherit from `std::exception` or other standard exceptions.
- Exception classes improve readability and maintainability.
- Real-world applications heavily rely on custom exception classes for robust error handling.
- Using meaningful exception classes makes debugging and software maintenance significantly easier.

Exception handling through classes is considered a professional and scalable approach for building reliable C++ applications and is widely used in modern software development.




