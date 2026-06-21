# Error Handling in C

## Introduction

Error handling in C is the process of detecting and managing runtime errors that may occur during program execution. Unlike languages such as Java or Python, C does not provide built-in exception handling mechanisms like `try-catch`. Instead, error handling is mainly performed using return values, error codes, predefined library functions, and conditional statements.

Many C library functions indicate failure by returning special values such as `NULL`, `EOF`, or `-1`. The global variable `errno` is used to identify the reason for the error.

## Why Error Handling is Important?

Error handling helps to:

- Prevent unexpected program crashes.
- Detect invalid operations.
- Display meaningful error messages.
- Improve reliability and maintainability.
- Handle system and file-related failures gracefully.

# errno in C

## Introduction

`errno` is a global variable defined in the `<errno.h>` header file. When certain library functions fail, they automatically set `errno` to an appropriate error code.

## Example

```c
#include <stdio.h>
#include <errno.h>

int main() {

    FILE *fp = fopen("data.txt", "r");

    if (fp == NULL) {

        printf("Error Number: %d", errno);
    }

    return 0;
}
```

### Output
Error Number: 2

### Explanation

Since the file does not exist, `fopen()` fails and sets `errno` to an error code corresponding to "No such file or directory".

# Common errno Values

| errno Value | Meaning |
| --- | --- |
| 1 | Operation not permitted |
| 2 | No such file or directory |
| 5 | Input/Output error |
| 12 | Out of memory |
| 13 | Permission denied |

# Using if-else for Error Handling

The simplest way to handle errors in C is by checking return values using conditional statements.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("sample.txt", "r");

    if (fp == NULL) {

        printf("File opening failed");
    }
    else {

        printf("File opened successfully");
        fclose(fp);
    }

    return 0;
}
```

### Output
File opening failed

### Explanation

If the file cannot be opened, `fopen()` returns `NULL`. The program checks this condition using an `if-else` statement.

# perror() Function

## Introduction

The `perror()` function prints a user-defined message followed by the corresponding error description based on `errno`.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("sample.txt", "r");

    if (fp == NULL) {

        perror("Error");
    }

    return 0;
}
```

### Output
Error: No such file or directory

### Explanation

`perror()` automatically displays the message associated with the current value of `errno`.

# strerror() Function

## Introduction

The `strerror()` function returns a pointer to a string containing the description of the current error.

## Example

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main() {

    FILE *fp = fopen("sample.txt", "r");

    if (fp == NULL) {

        printf("%s", strerror(errno));
    }

    return 0;
}
```

### Output
No such file or directory

### Explanation

`strerror()` converts the numeric error code stored in `errno` into a human-readable message.

# ferror() Function

## Introduction

`ferror()` checks whether an error occurred during a file operation.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("info.txt", "w");

    fprintf(fp, "Hello");

    if (ferror(fp) == 0) {

        printf("Data written successfully");
    }

    fclose(fp);

    return 0;
}
```

### Output
Data written successfully

### Explanation

`ferror()` returns zero if no error occurs during file operations.

# feof() Function

## Introduction

`feof()` checks whether the end of a file has been reached.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("message.txt", "r");

    if (fp == NULL)
        return 0;

    while (!feof(fp)) {

        char ch = fgetc(fp);

        if (!feof(fp))
            printf("%c", ch);
    }

    fclose(fp);

    return 0;
}
```

### Output
Hello World

### Explanation

The loop continues until the end of the file is reached.

# clearerr() Function

## Introduction

The `clearerr()` function clears error and EOF indicators associated with a stream.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("sample.txt", "w+");

    fprintf(fp, "Programming");

    while (fgetc(fp) != EOF);

    if (feof(fp)) {

        printf("End of file reached\n");
    }

    clearerr(fp);

    if (!feof(fp)) {

        printf("EOF flag cleared");
    }

    fclose(fp);

    return 0;
}
```

### Output
End of file reached
EOF flag cleared

### Explanation

`clearerr()` resets the EOF and error flags, allowing the stream to be reused.

# exit() Function

## Introduction

The `exit()` function terminates the program immediately and returns a status value to the operating system.

Two predefined constants are available:

- `EXIT_SUCCESS`
- `EXIT_FAILURE`

## Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    FILE *fp = fopen("file.txt", "r");

    if (fp == NULL) {

        printf("Unable to open file");
        exit(EXIT_FAILURE);
    }

    fclose(fp);

    exit(EXIT_SUCCESS);
}
```

### Output
Unable to open file

### Explanation

Since the file does not exist, the program terminates with `EXIT_FAILURE`.

# Handling Division by Zero

## Example

```c
#include <stdio.h>

int main() {

    int num1 = 20;
    int num2 = 0;

    if (num2 == 0) {

        printf("Division by zero is not allowed");
    }
    else {

        printf("%d", num1 / num2);
    }

    return 0;
}
```

### Output
Division by zero is not allowed

### Explanation

The program checks the divisor before performing division, preventing undefined behavior.

# Practical Example

Suppose Akash Dangudubiyyapu develops a student management system. The program reads data from files containing information about Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

If a file is missing, the program uses:

- `if-else` to detect failure.
- `errno` to identify the error.
- `perror()` to display a meaningful message.
- `exit(EXIT_FAILURE)` to terminate safely.

This prevents the program from crashing unexpectedly.

# Advantages of Error Handling

1. Prevents abnormal program termination.
2. Provides meaningful error messages.
3. Improves program reliability.
4. Helps in debugging.
5. Allows graceful recovery from failures.

# Limitations

1. C does not support exception handling.
2. Error checking must be done manually.
3. Forgetting to check return values may cause bugs.
4. Complex programs require extensive error management.

# Summary

Error handling in C is primarily performed using conditional statements, `errno`, `perror()`, `strerror()`, `ferror()`, `feof()`, `clearerr()`, and `exit()`. Since C lacks built-in exception handling mechanisms, programmers must manually check return values and error codes to ensure reliable and robust applications.

