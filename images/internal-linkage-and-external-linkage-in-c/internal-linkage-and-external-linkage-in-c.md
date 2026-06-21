# Internal Linkage and External Linkage in C

## Introduction

Linkage in C determines how identifiers such as variables and functions are connected across different parts of a program. It specifies whether an identifier can be accessed from other source files or remains restricted to the file in which it is declared.

Linkage is different from scope:

- Scope determines where an identifier is visible.
- Linkage determines whether an identifier can be shared between translation units.

A translation unit is a source file together with all the header files included in it.

There are three types of linkage in C:

- Internal Linkage
- External Linkage
- No Linkage

## Internal Linkage

Identifiers with internal linkage are accessible only within the same translation unit (source file). They cannot be accessed from other source files.

Internal linkage is achieved using the `static` keyword.

### Example

Suppose we have two source files.

### animals.c

```c
#include <stdio.h>

// Variable with internal linkage
static int animals = 8;

void displayAnimals() {
    printf("Animals = %d\n", animals);
}
```

### feed.c

```c
#include <stdio.h>

extern void displayAnimals();

int main() {

    displayAnimals();

    return 0;
}
```

### Output
Animals = 8

### Explanation

- `animals` is declared using `static`, so it has internal linkage.
- It cannot be directly accessed outside `animals.c`.
- The function `displayAnimals()` has external linkage and can access `animals` because both belong to the same translation unit.

## Characteristics of Internal Linkage

- Implemented using `static`.
- Accessible only within the current source file.
- Helps prevent naming conflicts.
- Used for private variables and helper functions.

# External Linkage

Identifiers with external linkage are visible throughout the program and can be accessed from multiple source files.

Global variables and functions have external linkage by default.

The `extern` keyword tells the compiler that the definition exists in another file.

## Example

### animals.c

```c
#include <stdio.h>

// Variable with external linkage
int animals = 8;
```

### feed.c

```c
#include <stdio.h>

// Declaration of external variable
extern int animals;

int main() {

    printf("Animals = %d", animals);

    return 0;
}
```

### Output
Animals = 8

### Explanation

- The variable `animals` is defined in `animals.c`.
- `extern int animals;` informs the compiler that the variable exists elsewhere.
- During linking, both source files are combined and the variable becomes accessible.

## Characteristics of External Linkage

- Default for global variables and functions.
- Shared across translation units.
- Implemented using `extern`.
- Useful in multi-file programs.

# Internal Linkage with Functions

Functions can also have internal linkage by using the `static` keyword.

## Example

```c
#include <stdio.h>

static void greet() {
    printf("Welcome\n");
}

int main() {

    greet();

    return 0;
}
```

### Output
Welcome

### Explanation

The function `greet()` can only be used within this source file because it has internal linkage.

# External Linkage with Functions

Functions defined globally automatically have external linkage.

## Example

### math_operations.c

```c
#include <stdio.h>

void showMessage() {
    printf("Learning C Programming\n");
}
```

### main.c

```c
#include <stdio.h>

extern void showMessage();

int main() {

    showMessage();

    return 0;
}
```

### Output
Learning C Programming

### Explanation

`showMessage()` is available to all translation units because it has external linkage.

# Internal vs External Linkage

| Feature | Internal Linkage | External Linkage |
| --- | --- | --- |
| Keyword | static | extern |
| Accessibility | Same source file only | Entire program |
| Visibility | Restricted | Global |
| Used For | Private variables/functions | Shared variables/functions |
| Naming Conflicts | Avoided | Possible |
| Default for Global Variables | No | Yes |

# No Linkage

Local variables inside functions have no linkage. They are accessible only within their block.

## Example

```c
#include <stdio.h>

int main() {

    int marks = 90;

    printf("%d", marks);

    return 0;
}
```

### Output
90

### Explanation

The variable `marks` exists only inside `main()` and cannot be accessed elsewhere.

# Memory Segments

| Linkage Type | Storage Segment |
| --- | --- |
| Internal linkage variables | Initialized or uninitialized data segment |
| External linkage variables | Initialized or uninitialized data segment |
| Functions | Text segment |
| Local variables | Stack |

# Advantages of Internal Linkage

- Provides data hiding.
- Prevents name collisions.
- Improves program organization.
- Makes modules independent.

# Advantages of External Linkage

- Enables communication between source files.
- Supports modular programming.
- Allows code reuse.
- Simplifies large projects.

# Limitations

- Excessive external linkage can cause naming conflicts.
- Internal linkage variables cannot be shared across files.
- Incorrect use of `extern` may lead to linker errors.

# Summary

Linkage in C determines how variables and functions are shared across source files. Internal linkage, implemented using `static`, restricts access to the same translation unit, whereas external linkage, implemented using `extern`, allows identifiers to be shared throughout the program. Local variables have no linkage and are confined to their own blocks. Understanding linkage is essential for designing modular and maintainable C programs.

