# User-Defined Custom Exceptions with Classes in C++

In C++, exceptions are not limited to built-in data types such as integers, characters, or strings. Programmers can create their own exception classes and throw objects of those classes whenever a specific error condition occurs.

User-defined exceptions allow developers to represent application-specific errors in a meaningful and organized manner. Instead of throwing generic values such as `-1` or `"Error"`, custom exception classes provide detailed information about what actually went wrong.

This makes programs:

- Easier to understand
- Easier to debug
- More maintainable
- More scalable for large applications

Custom exceptions are widely used in:

- Banking systems
- Student management systems
- Online learning platforms
- Hospital management software
- E-commerce applications
- File processing systems

## Why Use Custom Exceptions?

Consider an online learning platform such as **AlphaKnowledge**.

Possible errors include:

- Course not found
- Student not enrolled
- Invalid course ID
- Assignment submission deadline exceeded
- Insufficient course credits

Using integer values for these errors becomes difficult to manage.

Example:

```cpp
throw -1;
```

Looking at this statement, it is impossible to understand what error actually occurred.

Instead:

```cpp
throw CourseNotFoundException();
```

The error becomes self-explanatory.

This is the primary reason custom exceptions are preferred in professional software development.

# Creating a User-Defined Exception

A custom exception is simply a class.

Objects of this class can be thrown using the `throw` keyword and caught using a matching `catch` block.

## Syntax

```cpp
class ExceptionClass
{
};

throw ExceptionClass();
```

The type of the thrown object determines which catch block will handle the exception.

# Example 1: Basic User-Defined Exception

## Example Code

```cpp
#include <iostream>
using namespace std;

class EnrollmentException
{
};

int main()
{
    try
    {
        throw EnrollmentException();
    }
    catch(EnrollmentException e)
    {
        cout << "Enrollment Exception Caught";
    }

    return 0;
}
```

### Output
Enrollment Exception Caught

### Explanation

A custom exception class named `EnrollmentException` is created.

Inside the try block, an object of this class is thrown.

The catch block receives the same exception type and handles it successfully.

This demonstrates the simplest form of user-defined exception handling.

# Real-World Example: Course Registration System

Suppose a student tries to register for a course that does not exist.

## Example Code

```cpp
#include <iostream>
using namespace std;

class CourseNotFoundException
{
};

void registerCourse(int courseId)
{
    if(courseId != 101)
    {
        throw CourseNotFoundException();
    }

    cout << "Course Registered Successfully";
}

int main()
{
    try
    {
        registerCourse(999);
    }
    catch(CourseNotFoundException)
    {
        cout << "Course Not Found";
    }

    return 0;
}
```

### Output
Course Not Found

### Explanation

The function checks whether the course exists.

If the course ID is invalid, a custom exception object is thrown.

The exception is caught and an appropriate message is displayed.

# Multiple User-Defined Exceptions

Large applications often require multiple exception types.

Each exception can represent a different error condition.

## Example Code

```cpp
#include <iostream>
using namespace std;

class CourseNotFoundException
{
};

class StudentNotFoundException
{
};

int main()
{
    for(int i = 1; i <= 2; i++)
    {
        try
        {
            if(i == 1)
                throw CourseNotFoundException();
            else
                throw StudentNotFoundException();
        }
        catch(CourseNotFoundException)
        {
            cout << "Course Not Found" << endl;
        }
        catch(StudentNotFoundException)
        {
            cout << "Student Not Found" << endl;
        }
    }

    return 0;
}
```

### Output
Course Not Found
Student Not Found

### Explanation

Different exception types are thrown.

Each exception is handled by its corresponding catch block.

This provides precise error handling and improves code readability.

# Exception Handling with Inheritance

Exception classes can also participate in inheritance.

This allows multiple related exceptions to share a common base class.

## Example Code

```cpp
#include <iostream>
using namespace std;

class LearningException
{
};

class CourseNotFoundException
    : public LearningException
{
};

int main()
{
    try
    {
        throw CourseNotFoundException();
    }
    catch(CourseNotFoundException)
    {
        cout << "Course Exception Handled";
    }
    catch(LearningException)
    {
        cout << "Learning Exception Handled";
    }

    return 0;
}
```

### Output
Course Exception Handled

### Explanation

`CourseNotFoundException` inherits from `LearningException`.

The derived class catch block appears first.

Therefore the exact exception type is matched and handled.

# Importance of Catch Order

When inheritance exists among exception classes, catch block order becomes important.

Always place derived exception handlers before base exception handlers.

## Incorrect Example

```cpp
catch(LearningException)
{
}

catch(CourseNotFoundException)
{
}
```

In this case, the base class handler catches all derived exceptions first.

The derived handler never executes.

## Correct Example

```cpp
catch(CourseNotFoundException)
{
}

catch(LearningException)
{
}
```

The specific exception is handled first, followed by generic exceptions.

# Custom Exception with Error Message

Most real-world exception classes contain additional information.

For example, an error message.

## Example Code

```cpp
#include <iostream>
using namespace std;

class CourseException
{
private:

    string message;

public:

    CourseException(string msg)
    {
        message = msg;
    }

    string getMessage()
    {
        return message;
    }
};

int main()
{
    try
    {
        throw CourseException(
            "Course Capacity Full"
        );
    }
    catch(CourseException e)
    {
        cout << e.getMessage();
    }

    return 0;
}
```

### Output
Course Capacity Full

### Explanation

The exception object stores additional information.

The catch block retrieves and displays the message.

This makes exceptions more informative.

# Custom Exception Using std::exception

Modern C++ recommends deriving custom exceptions from `std::exception`.

This allows integration with the standard exception hierarchy.

## Example Code

```cpp
#include <iostream>
#include <exception>
using namespace std;

class AlphaKnowledgeException
    : public exception
{
public:

    const char* what() const noexcept override
    {
        return "Invalid Course Registration";
    }
};

int main()
{
    try
    {
        throw AlphaKnowledgeException();
    }
    catch(const exception& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Invalid Course Registration

### Explanation

The custom exception inherits from `std::exception`.

The `what()` function is overridden to provide a custom error message.

This is the most commonly used approach in professional C++ applications.

# Exceptions Inside Constructors

Constructors can also throw exceptions when invalid data is provided.

This prevents creation of invalid objects.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Course
{
private:

    int courseId;

public:

    Course(int id)
    {
        if(id <= 0)
        {
            throw "Invalid Course ID";
        }

        courseId = id;

        cout << "Course Created";
    }
};

int main()
{
    try
    {
        Course c(-1);
    }
    catch(const char* msg)
    {
        cout << msg;
    }

    return 0;
}
```

### Output
Invalid Course ID

### Explanation

The constructor validates the input.

If invalid data is provided, an exception is thrown.

Object creation stops immediately.

# Deriving from Specific Standard Exception Classes

Instead of inheriting directly from the base `std::exception` and overriding the `what()` function manually, you can inherit from more specific standard exception classes such as:

- `std::runtime_error` (for errors that can only be detected at runtime)
- `std::logic_error` (for logical errors in the program, like out of bounds or invalid arguments)

These classes already provide constructors that accept a string and automatically override the `what()` function.

## Example Code

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class InsufficientCreditsException : public runtime_error
{
public:

    // Forward the message to the base std::runtime_error constructor
    InsufficientCreditsException(const string& msg)
        : runtime_error(msg)
    {
    }
};

void checkCredits(int credits)
{
    if (credits < 12)
    {
        throw InsufficientCreditsException("Error: Credit hours must be at least 12");
    }

    cout << "Registration successful" << endl;
}

int main()
{
    try
    {
        checkCredits(8);
    }
    catch (const InsufficientCreditsException& e)
    {
        cout << e.what();
    }

    return 0;
}
```

### Output
Error: Credit hours must be at least 12

### Explanation

`InsufficientCreditsException` inherits from `std::runtime_error`.

The custom constructor uses constructor delegation to pass the error string to the base `runtime_error` constructor.

In `main()`, catching by reference retrieves the correct message using `e.what()` without needing to manually write an override.

# Catching Exceptions by Reference vs. Value (Object Slicing)

In C++, you should **always throw exceptions by value and catch them by reference** (specifically `const` reference).

If you catch exceptions by value using a base class exception type:

- The derived part of the thrown exception object is discarded.
- This is known as **object slicing**.
- Any overridden virtual functions (such as `what()`) will call the base class version instead of the derived version.

Catching by reference avoids copying overhead and preserves polymorphic behavior.

## Example Code

```cpp
#include <iostream>
#include <exception>
using namespace std;

class DatabaseException : public exception
{
public:

    const char* what() const noexcept override
    {
        return "Database Connection Failed";
    }
};

void connectDatabase()
{
    throw DatabaseException();
}

int main()
{
    try
    {
        connectDatabase();
    }
    // CAUTION: Catching by value (Slicing occurs)
    catch (exception e)
    {
        cout << "Caught by value: " << e.what() << endl;
    }

    try
    {
        connectDatabase();
    }
    // CORRECT: Catching by const reference
    catch (const exception& e)
    {
        cout << "Caught by reference: " << e.what() << endl;
    }

    return 0;
}
```

### Output
Caught by value: std::exception
Caught by reference: Database Connection Failed

### Explanation

When catching by value (`catch (exception e)`), the `DatabaseException` is sliced into a base `std::exception` object. As a result, calling `e.what()` displays the generic compiler-dependent base output (e.g., `std::exception`).

When catching by reference (`catch (const exception& e)`), polymorphism is preserved, and the derived class's overridden `what()` function is correctly executed, outputting `"Database Connection Failed"`.

# Advantages of User-Defined Exceptions

- Improves code readability.
- Makes errors easier to understand.
- Supports application-specific error handling.
- Works well with inheritance.
- Enables structured exception hierarchies.
- Simplifies debugging and maintenance.

# Best Practices

- Use meaningful exception class names.
- Derive custom exceptions from `std::exception` whenever possible.
- Catch exceptions by reference.
- Keep exception classes lightweight.
- Provide meaningful error messages.
- Use exception hierarchies for large applications.

# Summary

User-defined exceptions allow programmers to create custom error types that represent application-specific problems. Instead of throwing generic values such as integers or strings, custom exception objects provide meaningful and structured error information. Exception classes can support inheritance, store custom messages, integrate with the standard exception hierarchy, and improve program maintainability. Modern C++ applications commonly create custom exceptions by inheriting from `std::exception` and overriding the `what()` function to provide detailed error descriptions.




