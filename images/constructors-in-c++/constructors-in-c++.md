# Constructors in C++

A constructor is a special member function of a class that is automatically executed whenever an object of that class is created. The primary purpose of a constructor is to initialize the data members of an object and prepare the object for use.

Constructors are one of the most important features of Object-Oriented Programming because they ensure that objects start their life in a valid and usable state.

For example, when a student record is created, we may want to automatically assign values such as the student's name, roll number, and marks. Instead of assigning these values manually every time, a constructor can perform the initialization automatically.

# Why Do We Need Constructors?

Consider a Student class without a constructor.

```cpp
Student s1;

s1.name = "Mohit";
s1.rollNo = 101;
s1.marks = 95;
```

For a single object this may seem fine, but if a program creates hundreds or thousands of student records, repeatedly assigning values becomes tedious and increases the chances of errors.

Constructors solve this problem by automatically initializing objects at the time of creation.

Benefits of constructors include:

- Automatic object initialization.
- Improved code readability.
- Reduced repetitive code.
- Prevention of uninitialized variables.
- Better object management.
- Easier maintenance of large programs.

# Characteristics of Constructors

Constructors have several unique characteristics that differentiate them from normal member functions.

- The constructor name must be exactly the same as the class name.
- Constructors do not have a return type.
- Constructors are called automatically when an object is created.
- Constructors can be overloaded.
- A class can have multiple constructors.
- Constructors are generally declared in the public section of a class.
- Constructors help ensure that every object starts with valid data.

# Syntax of a Constructor

```cpp
class ClassName
{
public:

    ClassName()
    {
        // Initialization code
    }
};
```

The constructor name must always match the class name.

# Basic Constructor Example

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    Student()
    {
        cout << "Student Object Created";
    }
};

int main()
{
    Student s1;

    return 0;
}
```

### Output
Student Object Created

### 

The constructor is called automatically when the object `s1` is created.

Notice that we never explicitly call the constructor.

# How Constructors Work Internally

When the following statement executes:

```cpp
Student s1;
```

The compiler performs the following steps:

```text
1. Memory is allocated for s1.
2. Constructor is called automatically.
3. Data members are initialized.
4. Object becomes ready to use.
```

This process happens automatically whenever an object is created.

# Types of Constructors in C++

Constructors are commonly classified into four types:

1. Default Constructor
2. Parameterized Constructor
3. Copy Constructor
4. Move Constructor

Each type serves a different purpose.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/constructors-in-c/1781089401890-71ae6c04-b780-4b69-a0d9-1cf345cebbc5.png)

# 1. Default Constructor

A Default Constructor is a constructor that does not take any parameters.

It is used to initialize objects with default values.

If no constructor is defined by the programmer, the compiler automatically generates a default constructor.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    Student()
    {
        cout << "Default Constructor Called";
    }
};

int main()
{
    Student s1;

    return 0;
}
```

### Output
Default Constructor Called

### 

The constructor executes automatically during object creation.

## Default Constructor with Initialization

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    string name;
    int marks;

    Student()
    {
        name = "Mohit";
        marks = 90;
    }

    void display()
    {
        cout << "Name: " << name << endl;
        cout << "Marks: " << marks;
    }
};

int main()
{
    Student s1;

    s1.display();

    return 0;
}
```

### Output
Name: Mohit
Marks: 90

### 

The constructor automatically assigns default values when the object is created.

# Compiler Generated Default Constructor

If no constructor is written by the programmer, the compiler automatically generates one.

```cpp
class Student
{
public:
    string name;
};
```

Object creation remains valid.

```cpp
Student s1;
```

Behind the scenes, the compiler creates a simple default constructor.

# 2. Parameterized Constructor

A Parameterized Constructor accepts arguments and uses them to initialize object data members.

It allows different objects to store different values during creation.

# Why Use Parameterized Constructors?

Without a parameterized constructor:

```cpp
Student s1;

s1.name = "Mohit";
s1.marks = 95;
```

We must manually assign values after creating the object.

Parameterized constructors allow values to be supplied directly.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    string name;

    Student(string studentName)
    {
        name = studentName;
    }
};

int main()
{
    Student s1("AlphaKnowledge");

    cout << s1.name;

    return 0;
}
```

### Output
AlphaKnowledge

### 

The value is passed directly when the object is created.

## Parameterized Constructor with Multiple Parameters

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    string name;
    int rollNo;
    int marks;

    Student(string n,
            int r,
            int m)
    {
        name = n;
        rollNo = r;
        marks = m;
    }

    void display()
    {
        cout << "Name: " << name << endl;
        cout << "Roll No: " << rollNo << endl;
        cout << "Marks: " << marks;
    }
};

int main()
{
    Student s1(
        "Mohit",
        101,
        95
    );

    s1.display();

    return 0;
}
```

### Output
Name: Mohit
Roll No: 101
Marks: 95

### 

This allows each object to have its own unique data.

# Constructor Overloading

A class can contain multiple constructors with different parameter lists.

This concept is called Constructor Overloading.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    Student()
    {
        cout << "Default Constructor" << endl;
    }

    Student(string name)
    {
        cout << "Student Name: "
             << name << endl;
    }
};

int main()
{
    Student s1;

    Student s2("Hemesh");

    return 0;
}
```

### Output
Default Constructor
Student Name: Hemesh

### 

The compiler selects the constructor whose parameters match the provided arguments.

# 3. Copy Constructor

A Copy Constructor creates a new object as a copy of an existing object.

Instead of manually copying individual values, the entire object state can be copied at once.

# Why Do We Need Copy Constructors?

Suppose we already have a student object.

```cpp
Student s1(
    "Mohit",
    101,
    95
);
```

If we need another object with identical information, manually assigning every value becomes repetitive.

Copy constructors solve this problem.

## Syntax

```cpp
ClassName(const ClassName& obj)
{
}
```

The object is passed by reference to avoid unnecessary copying.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    string name;

    Student(string n)
    {
        name = n;
    }

    Student(const Student& s)
    {
        name = s.name;
    }
};

int main()
{
    Student s1("Akash");

    Student s2(s1);

    cout << s2.name;

    return 0;
}
```

### Output
Akash

### 

The object `s2` becomes an exact copy of `s1`.

# When is a Copy Constructor Called?

A copy constructor is automatically called in several situations.

### Copy Initialization

```cpp
Student s2 = s1;
```

### Passing Object by Value

```cpp
displayStudent(s1);
```

### Returning Object by Value

```cpp
return s1;
```

# Compiler Generated Copy Constructor

If no copy constructor is defined, the compiler automatically creates one.

The compiler-generated copy constructor performs a member-by-member copy.

This is known as a shallow copy.

# 4. Move Constructor

Move Constructors were introduced in C++11 to improve performance.

Instead of copying resources, a move constructor transfers ownership of resources from one object to another.

This reduces unnecessary copying and improves efficiency.

# Why Move Constructors?

Imagine an object storing:

- Large strings
- Large arrays
- Large vectors
- Dynamic memory blocks

Copying these resources can be expensive.

Move constructors transfer ownership instead of duplicating resources.

# Move Semantics

Traditional Copying:

```text
Object A
     ↓ Copy
Object B
```

Move Semantics:

```text
Object A
     ↓ Transfer Ownership
Object B
```

The resource is moved rather than copied.

## Example Code

```cpp
#include <iostream>
#include <utility>
using namespace std;

class Student
{
public:

    string name;

    Student(string&& n)
    {
        name = move(n);

        cout << "Move Constructor Called"
             << endl;
    }
};

int main()
{
    string studentName = "Mohit";

    Student s1(move(studentName));

    cout << s1.name;

    return 0;
}
```

### Output
Move Constructor Called
Mohit

### 

Ownership of the string is transferred instead of copied.

# Constructor Initialization List

C++ provides a cleaner and more efficient way to initialize data members using an initialization list.

## Example Code

```cpp
#include <iostream>
using namespace std;

class Student
{
public:

    string name;
    int marks;

    Student(string n,
            int m)
        : name(n),
          marks(m)
    {
    }
};

int main()
{
    Student s1(
        "Mohit",
        95
    );

    cout << s1.name << endl;
    cout << s1.marks;

    return 0;
}
```

### Output
Mohit
95

### 

Initialization lists are generally preferred because they initialize members directly.

# Constructor vs Normal Function

| Constructor | Normal Function |
| --- | --- |
| Same name as class. | Any valid name. |
| No return type. | Can have a return type. |
| Called automatically. | Called manually. |
| Used for initialization. | Used to perform operations. |
| Executes during object creation. | Executes when invoked. |

# Common Mistakes While Using Constructors

### Forgetting to Define a Default Constructor

If only a parameterized constructor exists:

```cpp
Student(string name)
{
}
```

Then:

```cpp
Student s1;
```

will generate an error.

### Giving a Return Type

Incorrect:

```cpp
int Student()
{
}
```

Constructors cannot have return types.

### Using a Different Name

Constructor name must exactly match the class name.

# Real-World Applications of Constructors

Constructors are used in almost every Object-Oriented application.

Examples include:

- Student Management Systems
- Library Management Systems
- Banking Applications
- Hospital Management Systems
- Employee Management Systems
- Inventory Systems
- E-Commerce Applications

Whenever an object needs automatic initialization, constructors are used.

# Summary

A constructor is a special member function that automatically executes whenever an object is created. Its primary purpose is to initialize object data members and prepare the object for use. Constructors improve code readability, reduce repetitive initialization code, and help ensure that objects always start in a valid state. C++ provides several types of constructors including Default Constructors, Parameterized Constructors, Copy Constructors, and Move Constructors. Understanding constructors is essential because they form the foundation of object creation and initialization in Object-Oriented Programming.




