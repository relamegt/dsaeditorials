# Enumeration (enum) in C

## Introduction

An enumeration, commonly known as an `enum`, is a user-defined data type in C that consists of a collection of named integer constants. Enumerations provide meaningful names to integer values, improving code readability and maintainability.

By default, the constants inside an enumeration are assigned integer values starting from 0, and each subsequent constant receives a value incremented by 1. However, programmers can also assign custom values to enumeration constants.

Enums are commonly used to represent states, menu options, days of the week, error codes, directions, permissions, and many other predefined sets of values.

## Why Use Enums?

Enums provide several advantages:

- Improve code readability.
- Replace meaningless integer values with descriptive names.
- Reduce programming errors.
- Simplify maintenance.
- Increase program clarity.
- Represent fixed sets of values efficiently.

# Declaring an Enumeration

An enumeration is declared using the `enum` keyword.

### Syntax

```c
enum enum_name {

    constant1,

    constant2,

    constant3

};
```

By default:

- The first constant gets value 0.
- The second constant gets value 1.
- The third constant gets value 2.

## Example

```c
#include <stdio.h>

enum Direction {

    EAST,

    WEST,

    NORTH,

    SOUTH

};

int main() {

    enum Direction dir = NORTH;

    printf("%d", dir);

    return 0;
}
```

### Output
2

### Explanation

Since numbering starts from 0:

- EAST = 0
- WEST = 1
- NORTH = 2
- SOUTH = 3

Therefore, `NORTH` produces 2.

# Creating Enum Variables

After defining an enum, variables of that type can be created.

## Example

```c
#include <stdio.h>

enum Grade {

    PASS,

    FAIL

};

int main() {

    enum Grade result = PASS;

    printf("%d", result);

    return 0;
}
```

### Output
0

### Explanation

`PASS` is the first constant, so it receives the value 0.

# Assigning Custom Values

Enum constants can be assigned specific integer values.

## Example

```c
#include <stdio.h>

enum Marks {

    LOW = 40,

    AVERAGE = 60,

    HIGH = 90

};

int main() {

    printf("%d\n", LOW);

    printf("%d\n", AVERAGE);

    printf("%d", HIGH);

    return 0;
}
```

### Output
40
60
90

### Explanation

The values are assigned manually instead of using default numbering.

# Automatic Value Increment

When some values are assigned manually, the remaining constants continue from the previous value.

## Example

```c
#include <stdio.h>

enum Level {

    BEGINNER = 1,

    INTERMEDIATE,

    ADVANCED

};

int main() {

    printf("%d\n", BEGINNER);

    printf("%d\n", INTERMEDIATE);

    printf("%d", ADVANCED);

    return 0;
}
```

### Output
1
2
3

### Explanation

After assigning 1 to `BEGINNER`, the compiler automatically assigns 2 and 3 to the next constants.

# Multiple Constants with Same Value

Different enum constants may have the same integer value.

## Example

```c
#include <stdio.h>

enum Status {

    SUCCESS = 1,

    COMPLETED = 1,

    FAILED = 0

};

int main() {

    printf("%d\n", SUCCESS);

    printf("%d", COMPLETED);

    return 0;
}
```

### Output
1
1

### Explanation

Although the names are different, both constants have the same value.

# Size of Enum

Generally, enum variables occupy memory equal to an integer.

## Example

```c
#include <stdio.h>

enum Day {

    MONDAY,

    TUESDAY,

    WEDNESDAY

};

int main() {

    enum Day d = MONDAY;

    printf("%zu", sizeof(d));

    return 0;
}
```

### Output
4

### Explanation

On most systems, enums are implemented using integers, which occupy 4 bytes.

# Enum with typedef

Using `typedef`, we can avoid repeatedly writing the `enum` keyword.

## Example

```c
#include <stdio.h>

typedef enum {

    RED,

    GREEN,

    BLUE

} Color;

int main() {

    Color c = GREEN;

    printf("%d", c);

    return 0;
}
```

### Output
1

### Explanation

`Color` acts as an alias for the enumeration type.

# Enum in Switch Statement

Enums are commonly used with switch statements.

## Example

```c
#include <stdio.h>

enum Operation {

    ADD,

    SUBTRACT,

    MULTIPLY

};

int main() {

    enum Operation choice = MULTIPLY;

    switch (choice) {

        case ADD:

            printf("Addition");

            break;

        case SUBTRACT:

            printf("Subtraction");

            break;

        case MULTIPLY:

            printf("Multiplication");

            break;

    }

    return 0;
}
```

### Output
Multiplication

# Enum for Days of Week

## Example

```c
#include <stdio.h>

enum Day {

    MONDAY,

    TUESDAY,

    WEDNESDAY,

    THURSDAY,

    FRIDAY,

    SATURDAY,

    SUNDAY

};

int main() {

    enum Day today = FRIDAY;

    printf("%d", today);

    return 0;
}
```

### Output
4

# Enum for Student Sections

## Example

```c
#include <stdio.h>

enum Section {

    SECTION_A,

    SECTION_B,

    SECTION_C

};

int main() {

    enum Section sec = SECTION_B;

    printf("%d", sec);

    return 0;
}
```

### Output
1

# Enum with Student Names

Suppose Akash Dangudubiyyapu wants to assign IDs to students Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

## Example

```c
#include <stdio.h>

enum StudentID {

    MOHIT = 101,

    ABHIRAM = 102,

    HEMESH = 103,

    HEMANTH = 104,

    AKHIL = 105

};

int main() {

    printf("%d\n", MOHIT);

    printf("%d", AKHIL);

    return 0;
}
```

### Output
101
105

# Enum vs Macro

| Feature | Enum | Macro |
| --- | --- | --- |
| Type Safety | Available | Not Available |
| Debugging | Easy | Difficult |
| Scope | Limited Scope | Global |
| Readability | Better | Moderate |
| Compiler Checking | Supported | Not Supported |

# Enum vs Constants

| Feature | Enum | Constant Variables |
| --- | --- | --- |
| Grouping | Possible | Not Possible |
| Memory Usage | Minimal | Occupies Memory |
| Readability | High | High |
| Type Checking | Available | Available |
| Use Case | Related Values | Individual Values |

# Applications of Enums

Enums are used in:

1. State machines.
2. Error codes.
3. Menu-driven programs.
4. Days and months representation.
5. Traffic light systems.
6. User permissions.
7. File handling modes.
8. Operating systems.
9. Game development.
10. Network protocols.

# Advantages of Enums

1. Improve readability.
2. Replace magic numbers.
3. Reduce coding errors.
4. Make programs easier to maintain.
5. Increase code clarity.
6. Provide meaningful names to values.
7. Support switch-case statements effectively.

# Limitations of Enums

1. Enum constants are integer values only.
2. String values cannot be stored directly.
3. Constants must have unique names within the same scope.
4. Complex relationships cannot be represented.
5. Not suitable for dynamic values.

# Real-Life Example

Suppose Akash Dangudubiyyapu is developing a college management system for students Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil. Instead of assigning arbitrary numbers throughout the program, he uses enums to represent departments, sections, grades, and attendance statuses. This makes the program easier to understand and maintain.

# Summary

An enumeration (`enum`) in C is a user-defined data type consisting of named integer constants. It improves code readability by replacing numeric values with meaningful names. Enums support automatic and manual value assignment, work efficiently with switch statements, and are widely used in state representation, menu systems, error handling, and many real-world applications. They help create programs that are easier to understand, maintain, and debug.

