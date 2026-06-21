# Structures in C

## Introduction

A structure in C is a user-defined data type that allows multiple variables of different data types to be grouped together under a single name. The variables inside a structure are called members or fields. Structures make programs more organized and are useful for representing real-world entities such as students, employees, books, bank accounts, and more.

Structures are defined using the `struct` keyword. Each member inside a structure can have its own data type, making structures more flexible than arrays, which store elements of the same type.

Structures are extensively used in implementing data structures such as linked lists, stacks, queues, trees, and graphs.

## Why Use Structures?

Structures provide several benefits:

- Group related data together.
- Represent real-world entities efficiently.
- Improve code readability and maintainability.
- Support complex data structures.
- Allow functions to work with multiple values using a single variable.
- Enable efficient memory organization.

# Defining a Structure

A structure is defined using the `struct` keyword.

### Syntax

```c
struct structure_name {

    data_type member1;
    data_type member2;
    data_type member3;

};
```

The structure definition only creates a template. Memory is allocated when structure variables are declared.

## Example

```c
#include <stdio.h>

struct Student {

    int rollNumber;
    float marks;

};

int main() {

    struct Student s1;

    s1.rollNumber = 101;
    s1.marks = 92.5;

    printf("%d\n", s1.rollNumber);
    printf("%.1f", s1.marks);

    return 0;
}
```

### Output
101
92.5

### Explanation

The structure `Student` contains two members. A variable `s1` is created and its members are accessed using the dot operator.

# Structure Members

The variables inside a structure are called members.

## Example

```c
struct Employee {

    int id;

    char grade;

    float salary;

};
```

Here:

- `id`
- `grade`
- `salary`

are members of the structure.

# Accessing Structure Members

The dot operator (`.`) is used to access structure members.

## Example

```c
#include <stdio.h>

struct Book {

    int pages;

};

int main() {

    struct Book b1;

    b1.pages = 450;

    printf("%d", b1.pages);

    return 0;
}
```

### Output
450

# Structure Initialization

Members can be initialized when the structure variable is declared.

## Example

```c
#include <stdio.h>

struct Student {

    char name[30];

    int age;

};

int main() {

    struct Student s = {

        "Akash Dangudubiyyapu",

        22

    };

    printf("%s\n", s.name);

    printf("%d", s.age);

    return 0;
}
```

### Output
Akash Dangudubiyyapu
22

# Designated Initialization

Members can also be initialized in any order using designated initializers.

## Example

```c
#include <stdio.h>

struct Student {

    char name[30];

    int age;

    float cgpa;

};

int main() {

    struct Student s = {

        .cgpa = 9.2,

        .name = "Mohit Chandaluri",

        .age = 21

    };

    printf("%s\n", s.name);

    printf("%d\n", s.age);

    printf("%.1f", s.cgpa);

    return 0;
}
```

### Output
Mohit Chandaluri
21
9.2

# Copying Structures

Structure variables can be copied using the assignment operator.

## Example

```c
#include <stdio.h>

struct Student {

    int id;

    char section;

};

int main() {

    struct Student s1 = {

        101,

        'A'

    };

    struct Student s2;

    s2 = s1;

    printf("%d\n", s2.id);

    printf("%c", s2.section);

    return 0;
}
```

### Output
101
A

### Explanation

The values stored in `s1` are copied into `s2`.

# Passing Structures to Functions

Structures can be passed to functions just like ordinary variables.

## Example

```c
#include <stdio.h>

struct Number {

    int value;

};

void display(struct Number n) {

    printf("%d", n.value);

}

int main() {

    struct Number n = {50};

    display(n);

    return 0;
}
```

### Output
50

# Passing Structure by Pointer

Passing structures using pointers avoids copying large amounts of data.

## Example

```c
#include <stdio.h>

struct Marks {

    int value;

};

void update(struct Marks *m) {

    m->value = 95;

}

int main() {

    struct Marks m = {80};

    update(&m);

    printf("%d", m.value);

    return 0;
}
```

### Output
95

### Explanation

The arrow operator is used when accessing members through structure pointers.

# typedef with Structures

The `typedef` keyword provides an alternative name for a structure.

## Example

```c
#include <stdio.h>

typedef struct {

    int age;

} Student;

int main() {

    Student s = {22};

    printf("%d", s.age);

    return 0;
}
```

### Output
22

### Explanation

Using `typedef`, we no longer need to write the `struct` keyword while creating variables.

# Size of Structure

The size of a structure may not be equal to the sum of the sizes of its members because of padding.

## Example

```c
#include <stdio.h>

struct Data {

    char ch;

    int num;

};

int main() {

    printf("%zu", sizeof(struct Data));

    return 0;
}
```

### Output
8

### Explanation

Extra bytes may be inserted by the compiler to improve memory alignment.

# Nested Structures

A structure can contain another structure as its member.

## Example

```c
#include <stdio.h>

struct Address {

    int pincode;

};

struct Student {

    int roll;

    struct Address addr;

};

int main() {

    struct Student s = {

        101,

        521456

    };

    printf("%d\n", s.roll);

    printf("%d", s.addr.pincode);

    return 0;
}
```

### Output
101
521456

# Structure Pointer

A pointer can point to a structure variable.

The arrow operator (`->`) is used to access members.

## Example

```c
#include <stdio.h>

struct Point {

    int x;

    int y;

};

int main() {

    struct Point p = {

        10,

        20

    };

    struct Point *ptr = &p;

    printf("%d\n", ptr->x);

    printf("%d", ptr->y);

    return 0;
}
```

### Output
10
20

# Self-Referential Structures

A structure can contain a pointer to its own type.

## Example

```c
struct Node {

    int data;

    struct Node *next;

};
```

Self-referential structures are used in linked lists, trees, and graphs.

# Bit Fields

Bit fields allow specifying the number of bits used by a member.

## Example

```c
struct Status {

    unsigned int active : 1;

    unsigned int role : 2;

};
```

Bit fields help reduce memory consumption.

# Array of Structures

Structures can be stored inside arrays.

## Example

```c
#include <stdio.h>

struct Student {

    char name[30];

};

int main() {

    struct Student students[3] = {

        {"Akash Dangudubiyyapu"},

        {"Abhiram Gopisetti"},

        {"Adapa Hemesh"}

    };

    for (int i = 0; i < 3; i++) {

        printf("%s\n", students[i].name);

    }

    return 0;
}
```

### Output
Akash Dangudubiyyapu
Abhiram Gopisetti
Adapa Hemesh

# Structure vs Array

| Feature | Structure | Array |
| --- | --- | --- |
| Data Types | Different | Same |
| Access | Dot operator | Index |
| Flexibility | High | Limited |
| Real-world Objects | Yes | No |
| Memory Allocation | Members separately | Continuous |

# Applications of Structures

Structures are used in:

1. Student management systems.
2. Employee databases.
3. Banking applications.
4. Linked lists.
5. Trees and graphs.
6. File systems.
7. Operating systems.
8. Compilers.
9. Database management systems.
10. Network programming.

# Real-Life Example

Suppose Akash Dangudubiyyapu is developing a college management system. Information about students such as Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil can be grouped together using structures.

Each student record may contain:

- Roll number
- Name
- CGPA
- Phone number

Instead of maintaining separate variables for every piece of information, a structure keeps everything organized under one entity.

# Advantages of Structures

1. Organize related data together.
2. Improve readability.
3. Support different data types.
4. Enable implementation of complex data structures.
5. Reduce code complexity.
6. Facilitate modular programming.

# Limitations of Structures

1. Structure members cannot be initialized inside the definition.
2. Operations like addition and subtraction are not allowed between structures.
3. Structures consume extra memory because of padding.
4. Deep copying dynamic memory must be handled manually.
5. Large structures may increase memory usage.

# Summary

Structures in C are user-defined data types that group variables of different types into a single unit. They are widely used for representing real-world objects and implementing advanced data structures. Structures support initialization, copying, nesting, pointers, and arrays, making them one of the most powerful features of the C language. Understanding structures is essential for mastering linked lists, trees, file systems, and many real-world applications.

