# Structures in C++

Structures are user-defined data types that allow multiple related variables to be grouped together under a single name. These variables can belong to the same data type or different data types. Structures help organize data logically and make programs easier to design, understand, and maintain.

For example, a student has multiple attributes such as name, roll number, age, and CGPA. Instead of creating separate variables for each attribute, a structure can group all these related values together.

Structures are widely used in software development to represent real-world entities such as students, employees, products, bank accounts, and more. They also form the foundation of many important data structures such as linked lists, stacks, queues, trees, and graphs.

## Why Do We Need Structures?

Consider storing information about a student using separate variables.

### Example Code

```cpp
string name = "Mohit";
int rollNumber = 101;
float cgpa = 8.7;
```

This approach works well for a single student. However, if we need to store information for hundreds or thousands of students, managing separate variables becomes difficult and confusing.

A structure allows all related information to be grouped together under a single entity.

### Example Code

```cpp
struct Student
{
    string name;
    int rollNumber;
    float cgpa;
};
```

Now all student-related information is organized inside a single user-defined data type called `Student`.

Structures provide:

- Better organization of data.
- Improved readability.
- Easier maintenance.
- Reusability.
- Real-world data representation.

## Structure Definition

A structure is defined using the `struct` keyword followed by the structure name and its members enclosed within curly braces.

### Syntax

```cpp
struct StructureName
{
    dataType member1;
    dataType member2;
    dataType member3;
};
```

### Example Code

```cpp
struct Student
{
    string name;
    int rollNumber;
    float cgpa;
};
```

In this structure:

- `Student` is the structure name.
- `name`, `rollNumber`, and `cgpa` are structure members.
- The structure acts as a blueprint for creating objects.

Defining a structure does not allocate memory. Memory is allocated only when structure variables are created.

## Creating Structure Variables

After defining a structure, variables of that structure type can be created just like built-in data type variables.

### Syntax

```cpp
StructureName variableName;
```

### Example Code

```cpp
Student student1;
Student student2;
```

Here:

- `student1` and `student2` are structure variables.
- Each variable has its own copy of all members.
- Memory is allocated separately for every structure variable.

## Structure Variable with Definition

Structure variables can also be declared at the time of structure definition.

### Example Code

```cpp
struct Student
{
    string name;
    int rollNumber;
} student1, student2;
```

Here, the variables `student1` and `student2` are created immediately after the structure definition.

## Initializing Structure Members

Initialization means assigning values to structure members. Structures can be initialized in multiple ways.

### Initialization Using Curly Braces

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int rollNumber;
};

int main()
{
    Student student = {"Mohit", 101};

    cout << student.name << " ";
    cout << student.rollNumber;

    return 0;
}
```

### Output
Mohit 101

### 

The values inside the curly braces are assigned sequentially to the members of the structure. The first value is assigned to `name` and the second value is assigned to `rollNumber`.

### Default Member Initialization

Since C++11, structure members can be initialized directly within the structure definition.

### Example Code

```cpp
struct Student
{
    string name = "Unknown";
    int rollNumber = 0;
};
```

Whenever a structure variable is created without explicit initialization, these default values are automatically assigned.

## Accessing Structure Members

Structure members are accessed using the dot (`.`) operator.

### Syntax

```cpp
variable.memberName;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int rollNumber;
};

int main()
{
    Student student = {"Akash", 102};

    cout << student.name << endl;
    cout << student.rollNumber;

    return 0;
}
```

### Output
Akash
102

### 

The dot operator accesses individual members stored inside the structure variable.

## Modifying Structure Members

Structure members can be modified using the assignment operator.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int rollNumber;
};

int main()
{
    Student student = {"Akash", 102};

    student.name = "Hemesh";
    student.rollNumber = 105;

    cout << student.name << endl;
    cout << student.rollNumber;

    return 0;
}
```

### Output
Hemesh
105

### 

The original values stored inside the structure are replaced with the new values.

## Member Functions in Structures

Unlike C structures, C++ structures can contain functions. These functions are called member functions because they belong to the structure itself.

Member functions can directly access structure data members without requiring additional parameters.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Marks
{
    int subject1;
    int subject2;

    int total()
    {
        return subject1 + subject2;
    }
};

int main()
{
    Marks student = {45, 50};

    cout << student.total();

    return 0;
}
```

### Output
95

### 

The member function `total()` accesses both data members and returns their sum.

## Constructors in Structures

Structures can contain constructors just like classes. Constructors are special member functions that automatically initialize objects when they are created.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int rollNumber;

    Student(string n, int r)
    {
        name = n;
        rollNumber = r;
    }

    void display()
    {
        cout << name << " " << rollNumber;
    }
};

int main()
{
    Student student("Abhiram", 120);

    student.display();

    return 0;
}
```

### Output
Abhiram 120

### 

The constructor automatically assigns values to the structure members when the object is created.

## Access Specifiers in Structures

Like classes, structures support access specifiers.

The three access specifiers are:

- public
- private
- protected

### Difference Between Structure and Class

| Feature | Structure | Class |
| --- | --- | --- |
| Default Access Specifier | Public | Private |

By default, all members of a structure are public.

## Size of Structure

The size of a structure depends on:

- Size of individual data members.
- Memory alignment requirements.
- Structure padding added by the compiler.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    char section;
    int rollNumber;
};

int main()
{
    cout << sizeof(Student);

    return 0;
}
```

### Output
8

### 

Although the actual size of the members is 5 bytes (1 byte for `char` and 4 bytes for `int`), the compiler adds extra bytes called padding to improve memory access efficiency.

This process is known as **Structure Padding**.

## Typedef with Structures

The `typedef` keyword creates an alias for an existing data type.

### Example Code

```cpp
#include <iostream>
using namespace std;

typedef struct
{
    int id;
    string name;
} Student;

int main()
{
    Student student = {101, "Mohit"};

    cout << student.id << " ";
    cout << student.name;

    return 0;
}
```

### Output
101 Mohit

### 

The alias `Student` can now be used directly without repeatedly writing the complete structure definition.

## Nested Structures

A structure can contain another structure as one of its members. This concept is known as nested structures.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Address
{
    string city;
    string state;
};

struct Student
{
    string name;
    Address address;
};

int main()
{
    Student student = {"Mohit", {"Vijayawada", "Andhra Pradesh"}};

    cout << student.name << endl;
    cout << student.address.city;

    return 0;
}
```

### Output
Mohit
Vijayawada

### 

Nested structures help represent complex real-world objects more naturally.

## Pointer to Structure

A pointer can store the address of a structure variable. Structure members can then be accessed using the arrow (`->`) operator.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
};

int main()
{
    Student student = {"Akash"};

    Student* ptr = &student;

    cout << ptr->name;

    return 0;
}
```

### Output
Akash

### 

The arrow operator is a shortcut for dereferencing the pointer and then accessing the member.

## Self-Referential Structures

A self-referential structure contains a pointer to another variable of the same structure type.

### Example Code

```cpp
struct Node
{
    int data;
    Node* next;
};
```

Such structures are commonly used in:

- Linked Lists
- Trees
- Graphs
- Dynamic Data Structures

A structure cannot contain a direct variable of its own type because it would result in an infinite size definition. Therefore, only pointers to the same type are allowed.

## Structures with Functions

Structures can be passed to functions and returned from functions.

Passing structures by reference is preferred because it avoids copying the entire structure and improves performance.

### Example Code

```cpp
void display(Student& student)
{
    cout << student.name;
}
```

The reference symbol (`&`) allows the original structure object to be accessed directly.

## Bit Fields

Bit fields allow structure members to occupy a specific number of bits instead of using the entire size of their data type.

### Example Code

```cpp
struct Flags
{
    unsigned int isActive : 1;
    unsigned int isAdmin : 1;
    unsigned int isVerified : 1;
};
```

Bit fields are useful in:

- Embedded Systems
- Hardware Programming
- Network Protocols
- Memory-Constrained Applications

They help reduce memory consumption when only a few bits are needed to store information.

# Summary

Structures are user-defined data types that allow related data to be grouped together under a single name. They improve data organization, readability, and maintainability. Structures support member variables, member functions, constructors, pointers, nested structures, and many object-oriented features. They are widely used in software development and serve as the foundation for advanced data structures such as linked lists, trees, graphs, and various real-world data models.




