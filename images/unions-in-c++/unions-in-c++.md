# Unions in C++

A union is a user-defined data type in C++ that allows multiple members of different data types to share the same memory location. Unlike structures, where every member gets its own separate memory space, all members of a union occupy the same memory block.

Because all members share the same memory location, only one member can store a meaningful value at a time. When a new value is assigned to one member, it overwrites the data previously stored by another member.

Unions are mainly used when memory optimization is important and only one of several possible values needs to be stored at a given time.

## Why Do We Need Unions?

Consider a situation where a system needs to store either:

- A student's roll number
- A student's CGPA
- A student's grade

but never all of them at the same time.

Using a structure would allocate separate memory for every member.

### Example Code

```cpp
struct Student
{
    int rollNumber;
    float cgpa;
    char grade;
};
```

In this case, memory is allocated for all three members.

A union allows all members to share the same memory location.

### Example Code

```cpp
union StudentData
{
    int rollNumber;
    float cgpa;
    char grade;
};
```

Now only one memory block is allocated and all members use it.

This significantly reduces memory usage.

## Structure vs Union

The major difference between structures and unions is memory allocation.

| Feature | Structure | Union |
| --- | --- | --- |
| Memory Allocation | Separate memory for each member | Shared memory for all members |
| Memory Usage | Higher | Lower |
| Member Access | All members can store values simultaneously | Only one member should hold a valid value at a time |
| Size | Sum of member sizes (plus padding) | Size of largest member |
| Use Case | Store multiple related values | Memory optimization |

## Union Declaration

A union is declared using the `union` keyword.

### Syntax

```cpp
union UnionName
{
    dataType member1;
    dataType member2;
    dataType member3;
};
```

### Example Code

```cpp
union StudentData
{
    int rollNumber;
    float cgpa;
    char grade;
};
```

Here:

- `StudentData` is the union name.
- `rollNumber`, `cgpa`, and `grade` are union members.
- All members share the same memory location.

Defining a union does not allocate memory. Memory is allocated only when a union variable is created.

<carousel autoplay="true" loop="true" arrows="true" dots="true" direction="horizontal" interval="4000">
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/unions-in-c/1781076955124-a80c491f-6e1a-42fd-bec6-d0d1ae79d5f2.png" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/unions-in-c/1781077011465-39c8a5b5-279f-4c7b-b97f-093c2ef6dbb8.png" />
</carousel>

## 

## Creating Union Variables

After defining a union, variables can be created in the same way as other data types.

### Syntax

```cpp
UnionName variableName;
```

### Example Code

```cpp
StudentData student;
```

Here, `student` is a union variable.

## Declaring Variables Along with Union Definition

Variables can also be created at the time of union definition.

### Example Code

```cpp
union StudentData
{
    int rollNumber;
    float cgpa;
} student1, student2;
```

Here, `student1` and `student2` are created immediately after the union definition.

## Accessing Union Members

Union members are accessed using the dot (`.`) operator, similar to structures.

### Example Code

```cpp
#include <iostream>
using namespace std;

union StudentData
{
    int rollNumber;
    float cgpa;
};

int main()
{
    StudentData student;

    student.rollNumber = 105;

    cout << student.rollNumber;

    return 0;
}
```

### Output
105

### 

The dot operator accesses members stored inside the union variable.

## Understanding Shared Memory

The most important concept in unions is shared memory.

All members use the same memory location.

### Example Code

```cpp
#include <iostream>
using namespace std;

union StudentData
{
    int rollNumber;
    float cgpa;
};

int main()
{
    StudentData student;

    student.rollNumber = 120;
    cout << "Roll Number: " << student.rollNumber << endl;

    student.cgpa = 8.9;
    cout << "CGPA: " << student.cgpa << endl;

    return 0;
}
```

### Output
Roll Number: 120
CGPA: 8.9

### 

When `cgpa` is assigned a value, it overwrites the memory previously used by `rollNumber`.

Therefore, only the most recently assigned member contains valid data.

## Memory Representation of a Union

Consider the following union:

### Example Code

```cpp
union StudentData
{
    int rollNumber;
    char grade;
};
```

Internally, both members share the same memory block.

```text
+----------------+
| Shared Memory  |
+----------------+
| rollNumber     |
| grade          |
+----------------+
```

Unlike structures, separate memory locations are not allocated for each member.

## Size of a Union

The size of a union is equal to the size of its largest member.

### Example Code

```cpp
#include <iostream>
using namespace std;

union Data
{
    int rollNumber;
    double cgpa;
    char grade;
};

int main()
{
    cout << sizeof(Data);

    return 0;
}
```

### Output
8

### 

The largest member is `double`, which occupies 8 bytes.

Therefore, the size of the entire union becomes 8 bytes.

## Comparing Structure Size and Union Size

### Example Code

```cpp
#include <iostream>
using namespace std;

struct StudentStruct
{
    int rollNumber;
    float cgpa;
    char grade;
};

union StudentUnion
{
    int rollNumber;
    float cgpa;
    char grade;
};

int main()
{
    cout << "Structure Size: "
         << sizeof(StudentStruct)
         << endl;

    cout << "Union Size: "
         << sizeof(StudentUnion);

    return 0;
}
```

### Output
Structure Size: 12
Union Size: 4

### 

The structure requires memory for all members, while the union only requires memory for its largest member.

## Nested Unions

A union can be declared inside another structure, class, or union. This is called a nested union.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Employee
{
    int employeeId;

    union Payment
    {
        float salary;
        float hourlyRate;
    } pay;
};

int main()
{
    Employee emp;

    emp.employeeId = 101;
    emp.pay.salary = 45000;

    cout << emp.employeeId << endl;
    cout << emp.pay.salary;

    return 0;
}
```

### Output
101
45000

### 

Nested unions help organize related data while still providing memory efficiency.

## Anonymous Unions

An anonymous union is a union without a name.

Its members can be accessed directly without specifying the union name.

### Example Code

```cpp
#include <iostream>
using namespace std;

struct Employee
{
    int employeeId;

    union
    {
        float salary;
        float hourlyRate;
    };
};

int main()
{
    Employee emp;

    emp.employeeId = 102;
    emp.salary = 50000;

    cout << emp.employeeId << endl;
    cout << emp.salary;

    return 0;
}
```

### Output
102
50000

### 

Notice that `salary` is accessed directly without writing a union name.

## Union Inside Another Union

A union can also contain another union.

### Example Code

```cpp
#include <iostream>
using namespace std;

union Outer
{
    int value;

    union
    {
        char grade;
        bool status;
    };
};

int main()
{
    Outer data;

    data.grade = 'A';

    cout << data.grade;

    return 0;
}
```

### Output
A

### 

This creates multiple levels of shared memory.

## Applications of Unions

Unions are mainly used when memory efficiency is more important than storing multiple values simultaneously.

Common applications include:

- Embedded systems.
- Microcontroller programming.
- Hardware register mapping.
- Network packet processing.
- Device drivers.
- Memory-constrained applications.

## Advantages of Unions

- Memory efficient.
- Reduces storage requirements.
- Useful in low-level programming.
- Allows multiple interpretations of the same memory location.
- Helpful in embedded and hardware-related applications.

## Limitations of Unions

- Only one member can hold valid data at a time.
- Incorrect usage may lead to unexpected results.
- More difficult to debug than structures.
- Less intuitive for beginners.
- Data can be overwritten accidentally.

## When Should You Use a Union?

Use a union when:

- Only one value is needed at a time.
- Memory optimization is critical.
- Working with hardware or embedded systems.
- Different representations of the same data are required.

Avoid unions when multiple values must exist simultaneously. In such cases, structures are a better choice.

# Summary

A union is a user-defined data type that allows multiple members to share the same memory location. Unlike structures, unions allocate memory only for their largest member, making them highly memory efficient. Since all members share the same memory block, only one member should contain valid data at a time. Unions are commonly used in embedded systems, hardware programming, network protocols, and memory-constrained applications where efficient memory utilization is essential.




