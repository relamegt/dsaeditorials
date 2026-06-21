# Error Handling During File Operations in C

## Introduction

File operations are essential in many C programs. While working with files, various errors can occur such as missing files, insufficient permissions, invalid file pointers, or reaching the end of a file unexpectedly. Proper error handling helps prevent crashes and ensures reliable program execution.

Common file-related errors include:

- File not found
- Permission denied
- Disk full
- File already exists
- Invalid file pointer
- End of file reached
- File open failure
- File closing errors

## Common File Errors

| Error | Cause |
| --- | --- |
| File Not Found | Trying to open a file that does not exist |
| Permission Denied | Insufficient access rights |
| Disk Full | No space available for writing |
| File Already Exists | Attempting to create an existing file |
| Invalid File Pointer | Using NULL file pointer |
| End of File | Reading beyond available data |
| File Not Open | Operations performed on unopened file |
| File Closing Error | Failure while closing a file |

# File Not Found Error

## Introduction

When a file is opened in read mode and the file does not exist, `fopen()` returns `NULL`.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("student.txt", "r");

    if (fp == NULL) {

        perror("Error");
        return 1;
    }

    fclose(fp);

    return 0;
}
```

### Output
Error: No such file or directory

### Explanation

Since the file is unavailable, `fopen()` returns `NULL`. The `perror()` function displays the corresponding error message.

# Permission Denied Error

## Introduction

If the program does not have permission to access a file, `fopen()` fails and returns `NULL`.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("/restricted/data.txt", "w");

    if (fp == NULL) {

        perror("Permission denied");
    }

    return 0;
}
```

### Output
Permission denied: Permission denied

### Explanation

The operating system prevents access to the file due to insufficient privileges.

# Handling Disk Full Error

## Introduction

When the disk becomes full during writing operations, file functions may fail. `ferror()` can detect such errors.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("records.txt", "w");

    if (fp == NULL) {

        perror("File opening error");
        return 1;
    }

    fprintf(fp, "Hello World");

    if (ferror(fp)) {

        perror("Writing error");
    }

    fclose(fp);

    return 0;
}
```

### Output
Writing error: No space left on device

### Explanation

If writing fails because storage space is exhausted, `ferror()` detects the error.

# File Already Exists Error

## Introduction

Opening a file using `"wx"` mode creates a file only if it does not already exist.

## Example

```c
#include <stdio.h>
#include <errno.h>

int main() {

    FILE *fp = fopen("marks.txt", "wx");

    if (fp == NULL) {

        if (errno == EEXIST) {

            printf("File already exists");
        }
    }

    return 0;
}
```

### Output
File already exists

### Explanation

The file already exists, so creation fails and `errno` is set to `EEXIST`.

# Invalid File Pointer Error

## Introduction

A file pointer should always be checked before performing operations.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = NULL;

    if (fp == NULL) {

        printf("Invalid file pointer");
    }

    return 0;
}
```

### Output
Invalid file pointer

### Explanation

Using a NULL pointer for file operations results in undefined behavior, so validation is necessary.

# End of File Handling

## Introduction

While reading data, the end of the file can be detected using `feof()`.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("data.txt", "r");

    char ch;

    while ((ch = fgetc(fp)) != EOF) {

        putchar(ch);
    }

    if (feof(fp)) {

        printf("\nEnd of file reached");
    }

    fclose(fp);

    return 0;
}
```

### Output
End of file reached

### Explanation

When all characters have been read, `feof()` confirms that the end of the file has been reached.

# File Open Failure

## Introduction

Always verify whether `fopen()` successfully opens a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("report.txt", "r");

    if (fp == NULL) {

        printf("File could not be opened");
    }
    else {

        printf("File opened successfully");
        fclose(fp);
    }

    return 0;
}
```

### Output
File could not be opened

### Explanation

If the file cannot be opened, `fopen()` returns `NULL`.

# File Closing Error

## Introduction

`fclose()` returns `0` when successful and `EOF` (typically -1) if an error occurs while closing the file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fp = fopen("info.txt", "w");

    fprintf(fp, "Programming");

    if (fclose(fp) == EOF) {

        printf("File closing error");
    }
    else {

        printf("File closed successfully");
    }

    return 0;
}
```

### Output
File closed successfully

### Explanation

The return value of `fclose()` indicates whether the file was closed correctly.

# Practical Example

Suppose Akash Dangudubiyyapu develops a student database system that stores records of Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil in files.

While opening and updating student records, the program should:

- Verify whether files exist.
- Check file pointers before reading.
- Detect disk write failures.
- Handle end-of-file conditions.
- Ensure files are closed properly.

This prevents data corruption and unexpected program termination.

# Best Practices

1. Always check whether `fopen()` returns `NULL`.
2. Use `perror()` to display descriptive error messages.
3. Verify write operations using `ferror()`.
4. Use `feof()` to detect end-of-file conditions.
5. Always close files using `fclose()`.
6. Check the return value of `fclose()`.
7. Avoid using invalid file pointers.

# Advantages

- Prevents program crashes.
- Improves reliability.
- Provides meaningful error messages.
- Detects file operation failures.
- Ensures proper resource management.

# Limitations

- Requires manual checking.
- Some errors depend on the operating system.
- Error handling increases code complexity.
- Failure to check return values can cause bugs.

# Summary

Error handling during file operations in C is achieved by checking the return values of functions such as `fopen()`, `fclose()`, `ferror()`, and `feof()`. Proper validation and handling of conditions like missing files, permission issues, disk errors, and end-of-file situations help create robust and reliable applications.

