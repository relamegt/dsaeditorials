# Using goto for Exception Handling in C

## Introduction

C does not provide built-in exception handling mechanisms such as `try-catch` blocks found in languages like Java or C++. However, error handling can be implemented using conditional statements, error codes, and the `goto` statement.

The `goto` statement allows control to jump to a labeled section within the same function. Although excessive use of `goto` is discouraged, it is commonly used for resource cleanup and centralized error handling.

## Syntax

```c
goto label;

/* statements */

label:
/* code to execute after goto */
```

## Why Use goto for Exception Handling?

The `goto` statement is useful in situations such as:

- Cleaning up allocated memory.
- Closing files before exiting.
- Avoiding duplicate cleanup code.
- Providing a single exit point for error handling.
- Breaking out of deeply nested conditions.

# Simulating try-catch Using goto

## Example

```c
#include <stdio.h>

int main() {

    int numerator = 20;
    int denominator = 0;
    int result;

    if (denominator == 0) {

        goto exception;
    }

    result = numerator / denominator;

    printf("Result = %d", result);

    return 0;

exception:

    printf("Exception: Division by zero is not allowed");

    return 0;
}
```

### Output
Exception: Division by zero is not allowed

### Explanation

Before performing division, the program checks whether the denominator is zero. If it is zero, control jumps directly to the exception label and prints an error message.

# File Processing Error Handling Using goto

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("student.txt", "r");

    if (fp == NULL) {

        printf("Error opening file\n");
        goto error;
    }

    printf("File opened successfully\n");

error:

    if (fp != NULL) {

        fclose(fp);
    }

    return 0;
}
```

### Output
Error opening file

### Explanation

If the file cannot be opened, execution jumps to the `error` label where cleanup operations are performed.

# Memory Allocation Cleanup Using goto

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    int *ptr = (int *)malloc(sizeof(int) * 5);

    if (ptr == NULL) {

        printf("Memory allocation failed\n");
        goto cleanup;
    }

    printf("Memory allocated successfully\n");

cleanup:

    free(ptr);

    return 0;
}
```

### Output
Memory allocated successfully

### Explanation

The cleanup section ensures that allocated memory is released before the program terminates.

# Multiple Resource Cleanup Using goto

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    FILE *fp = fopen("data.txt", "r");

    if (fp == NULL) {

        goto error;
    }

    int *arr = (int *)malloc(sizeof(int) * 10);

    if (arr == NULL) {

        goto error;
    }

    printf("Resources allocated successfully\n");

    free(arr);
    fclose(fp);

    return 0;

error:

    if (fp != NULL)
        fclose(fp);

    printf("Error occurred");

    return 0;
}
```

### Output
Error occurred

### Explanation

When an error occurs, control transfers to a single cleanup section instead of writing cleanup code multiple times.

# Single Exit Point Technique

## Example

```c
#include <stdio.h>

int main() {

    int marks = -5;

    if (marks < 0) {

        goto invalid;
    }

    printf("Marks = %d", marks);

    return 0;

invalid:

    printf("Invalid marks");

    return 0;
}
```

### Output
Invalid marks

### Explanation

The program transfers control to one common section responsible for handling invalid input.

# Advantages of Using goto for Error Handling

1. Reduces duplicate cleanup code.
2. Provides a single exit point.
3. Useful for resource management.
4. Simplifies nested error conditions.
5. Commonly used in system-level programming.

# Limitations of goto

1. Makes code harder to understand when overused.
2. Can create spaghetti code.
3. Reduces maintainability in large programs.
4. Cannot jump between functions.
5. Structured programming alternatives are usually preferred.

# Best Practices

- Use `goto` only for error handling and cleanup.
- Keep labels near the end of the function.
- Avoid multiple unnecessary labels.
- Prefer functions and structured control statements when possible.
- Always release allocated resources before jumping to exit sections.

# Practical Example

Suppose Akash Dangudubiyyapu is developing a student database application. The program allocates memory, opens files, and processes records of Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

If memory allocation or file opening fails, a `goto cleanup` statement transfers control to a common cleanup section where all opened files are closed and allocated memory is freed. This avoids resource leaks and duplicate cleanup code.

# Summary

The `goto` statement in C is often used to implement exception-like behavior by transferring control to a centralized error-handling section. Although it should not be overused, it is particularly useful for resource cleanup, file handling, and managing multiple error conditions efficiently.

