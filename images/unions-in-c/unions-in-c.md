# Unions in C

## Introduction

A union in C is a user-defined data type that allows multiple members of different data types to share the same memory location. Similar to structures, unions can contain variables of various types, but unlike structures, all members occupy the same memory space.

Since all members share a common memory area, storing a value in one member overwrites the value previously stored in another member. This property makes unions highly memory-efficient when only one piece of data needs to be stored at a time.

Unions are defined using the `union` keyword and are commonly used in embedded systems, hardware programming, memory optimization, and situations where data can have multiple interpretations.

## Why Use Unions?

Unions offer several advantages:

- Reduce memory consumption.
- Allow different data types to share the same memory.
- Useful in hardware register mapping.
- Suitable when only one member is required at a time.
- Improve memory efficiency in embedded applications.
- Support flexible data representation.

# Defining a Union

A union is declared using the `union` keyword.

### Syntax

```c
union union_name {

    data_type member1;

    data_type member2;

    data_type member3;

};
```

Memory for all members is shared, and the size of the union depends on the largest member.

## Example

```c
#include <stdio.h>

union Student {

    int rollNo;

    float marks;

};

int main() {

    union Student s;

    s.rollNo = 101;

    printf("%d", s.rollNo);

    return 0;
}
```

### Output
101

### Explanation

The union `Student` contains two members. Both members occupy the same memory location, but only one value should be used at a time.

# Accessing Union Members

Union members are accessed using the dot (`.`) operator.

## Example

```c
#include <stdio.h>

union Data {

    int number;

    char grade;

};

int main() {

    union Data d;

    d.grade = 'A';

    printf("%c", d.grade);

    return 0;
}
```

### Output
A

# Shared Memory Concept

All members of a union share the same memory location.

## Example

```c
#include <stdio.h>

union Value {

    int x;

    float y;

};

int main() {

    union Value v;

    v.x = 25;

    printf("%d\n", v.x);

    v.y = 15.5;

    printf("%.1f", v.y);

    return 0;
}
```

### Output
25
15.5

### Explanation

Assigning a value to `y` overwrites the value previously stored in `x` because both members share the same memory.

# Size of a Union

The size of a union is equal to the size of its largest member.

## Example

```c
#include <stdio.h>

union A {

    int number;

    char ch;

};

int main() {

    printf("%zu", sizeof(union A));

    return 0;
}
```

### Output
4

### Explanation

The integer occupies 4 bytes, while the character occupies 1 byte. Therefore, the size of the union becomes 4 bytes.

# Another Example of Union Size

```c
#include <stdio.h>

union Data {

    int marks[10];

    char grade;

};

int main() {

    printf("%zu", sizeof(union Data));

    return 0;
}
```

### Output
40

### Explanation

The array of integers occupies 40 bytes, which is larger than a single character. Hence, the union size becomes 40 bytes.

# Initializing Union Members

Only one member should be initialized at a time.

## Example

```c
#include <stdio.h>

union Employee {

    int id;

    float salary;

};

int main() {

    union Employee emp = {105};

    printf("%d", emp.id);

    return 0;
}
```

### Output
105

# Nested Union

A union can contain another union as one of its members.

## Example

```c
#include <stdio.h>

union Academic {

    int marks;

};

union Student {

    int rollNo;

    union Academic performance;

};

int main() {

    union Student s;

    s.performance.marks = 95;

    printf("%d", s.performance.marks);

    return 0;
}
```

### Output
95

### Explanation

The union `Student` contains another union named `Academic`.

# Anonymous Union

An anonymous union does not have a name and its members can be accessed directly.

## Example

```c
#include <stdio.h>

struct Student {

    int rollNo;

    union {

        int marks;

    };

};

int main() {

    struct Student s;

    s.rollNo = 101;

    s.marks = 90;

    printf("%d\n", s.rollNo);

    printf("%d", s.marks);

    return 0;
}
```

### Output
101
90

### Explanation

The member `marks` can be accessed directly without referring to the union name.

# Union Inside Structure

Structures and unions are often used together.

## Example

```c
#include <stdio.h>

struct Student {

    char name[30];

    union {

        int rollNo;

        float cgpa;

    } details;

};

int main() {

    struct Student s;

    s.details.cgpa = 9.3;

    printf("%.1f", s.details.cgpa);

    return 0;
}
```

### Output
9.3

# Array of Unions

Multiple union variables can be stored in an array.

## Example

```c
#include <stdio.h>

union Number {

    int value;

};

int main() {

    union Number numbers[3];

    numbers[0].value = 10;

    numbers[1].value = 20;

    numbers[2].value = 30;

    for (int i = 0; i < 3; i++) {

        printf("%d\n", numbers[i].value);

    }

    return 0;
}
```

### Output
10
20
30

# Structure vs Union

| Feature | Structure | Union |
| --- | --- | --- |
| Memory Allocation | Separate memory for each member | Shared memory |
| Size | Sum of member sizes | Size of largest member |
| Simultaneous Values | Possible | Not possible |
| Memory Usage | More | Less |
| Data Storage | Independent | Shared |
| Efficiency | Lower | Higher |

# Real-Life Example

Suppose Akash Dangudubiyyapu is developing a student management system for Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

A student record may contain either:

- Roll number
- CGPA
- Attendance percentage

At a particular time, only one of these values needs to be stored. Using a union allows all these values to share the same memory location, reducing overall memory usage.

# Applications of Unions

Unions are used in:

1. Embedded systems.
2. Hardware register mapping.
3. Device drivers.
4. Compiler design.
5. Communication protocols.
6. Memory optimization.
7. Variant data representation.
8. Operating systems.
9. Sensor data processing.
10. Network packet interpretation.

# Advantages of Unions

1. Efficient memory utilization.
2. Support multiple interpretations of the same memory.
3. Reduce storage requirements.
4. Useful in low-level programming.
5. Suitable for embedded applications.
6. Improve performance when memory is limited.

# Limitations of Unions

1. Only one member should contain valid data at a time.
2. Assigning a value to one member overwrites others.
3. Difficult to debug.
4. Can cause unexpected behavior if used improperly.
5. Less intuitive compared to structures.

# Summary

A union in C is a user-defined data type in which all members share the same memory location. Unlike structures, where each member has separate memory, unions use a common memory area, making them highly memory-efficient. They are widely used in embedded systems, hardware interfaces, device drivers, and situations where different types of data need to occupy the same memory space. Proper understanding of unions helps programmers optimize memory usage and design efficient low-level applications.

