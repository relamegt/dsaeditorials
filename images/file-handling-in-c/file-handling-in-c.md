# File Handling in C

## Introduction

File handling in C is the process of creating, opening, reading, writing, updating, and closing files stored on secondary storage devices. Files provide permanent storage, allowing data to persist even after the program terminates.

Instead of storing data only in variables during execution, file handling enables programs to save and retrieve information whenever required. C provides a set of standard library functions to perform various file operations efficiently.

All file handling functions are declared in the `<stdio.h>` header file.

## Why Use File Handling?

File handling provides several advantages:

- Enables permanent data storage.
- Allows reading and writing large amounts of data.
- Supports text and binary files.
- Makes data available even after program termination.
- Useful for databases, logs, reports, and records.
- Eliminates the need to re-enter data repeatedly.

# What is a File?

A file is a collection of related data stored on secondary storage devices such as hard disks, SSDs, or flash drives.

There are two types of files in C:

1. Text Files
2. Binary Files

# FILE Pointer

C uses a special pointer called `FILE` pointer to perform file operations.

### Syntax

```c
FILE *fptr;
```

The file pointer stores information about the opened file and acts as a connection between the program and the file.

# Opening a File

The `fopen()` function is used to open an existing file or create a new file.

### Syntax

```c
FILE *fopen(const char *filename,
            const char *mode);
```

### Parameters

- `filename` : Name or path of the file.
- `mode` : Specifies how the file should be accessed.

### Return Value

- Returns a valid file pointer if successful.
- Returns `NULL` if opening fails.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("student.txt", "r");

    if (fptr == NULL) {

        printf("File could not be opened");
    }

    return 0;
}
```

### Output
File could not be opened

### Explanation

Since the file does not exist, `fopen()` returns `NULL`.

# File Opening Modes

Different modes determine the operations allowed on a file.

| Mode | Description |
| --- | --- |
| r | Opens file for reading |
| w | Opens file for writing |
| a | Opens file for appending |
| r+ | Reading and writing |
| w+ | Reading and writing with overwrite |
| a+ | Reading and appending |
| rb | Binary read mode |
| wb | Binary write mode |
| ab | Binary append mode |
| rb+ | Binary read/write mode |
| wb+ | Binary read/write with overwrite |
| ab+ | Binary append/read mode |

# Creating a File

If a file does not exist, modes such as `w`, `w+`, `a`, and `a+` create a new file automatically.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("students.txt", "w");

    if (fptr == NULL) {

        printf("File creation failed");
    }
    else {

        printf("File created successfully");
    }

    fclose(fptr);

    return 0;
}
```

### Output
File created successfully

### Explanation

The file `students.txt` is created in write mode.

# Writing to a File

Several functions are available for writing data:

- `fprintf()`
- `fputs()`
- `fputc()`
- `fwrite()`

# Using fprintf()

The `fprintf()` function works like `printf()` but writes data into a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("students.txt", "w");

    fprintf(fptr, "Akash Dangudubiyyapu\n");
    fprintf(fptr, "Mohit Chandaluri\n");
    fprintf(fptr, "Abhiram Gopisetti");

    fclose(fptr);

    return 0;
}
```

### Output
Data written successfully into students.txt

### Explanation

The student names are written into the file.

# Using fputs()

The `fputs()` function writes an entire string into a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("course.txt", "w");

    fputs("Welcome to AlphaKnowledge", fptr);

    fclose(fptr);

    return 0;
}
```

### Output
Data written successfully

# Using fputc()

The `fputc()` function writes a single character into a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("letter.txt", "w");

    fputc('A', fptr);

    fclose(fptr);

    return 0;
}
```

### Output
Character written successfully

# Reading From a File

Common functions used for reading are:

- `fscanf()`
- `fgets()`
- `fgetc()`
- `fread()`

# Using fscanf()

The `fscanf()` function works similarly to `scanf()` and reads formatted input from a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    char name[50];

    fptr = fopen("students.txt", "r");

    fscanf(fptr, "%s", name);

    printf("%s", name);

    fclose(fptr);

    return 0;
}
```

### Output
Akash

### Explanation

The first word from the file is read into the variable.

# Using fgets()

The `fgets()` function reads an entire line from a file.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    char data[100];

    fptr = fopen("course.txt", "r");

    fgets(data, 100, fptr);

    printf("%s", data);

    fclose(fptr);

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The complete line stored inside the file is read.

# Using fgetc()

The `fgetc()` function reads one character at a time.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    char ch;

    fptr = fopen("letter.txt", "r");

    ch = fgetc(fptr);

    printf("%c", ch);

    fclose(fptr);

    return 0;
}
```

### Output
A

# End of File (EOF)

When reading reaches the end of the file, the special value `EOF` is returned.

## Example

```c
while ((ch = fgetc(fptr)) != EOF) {

    printf("%c", ch);
}
```

### Explanation

The loop continues until the end of the file is reached.

# Closing a File

After completing file operations, files should always be closed using `fclose()`.

### Syntax

```c
fclose(fptr);
```

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    fptr = fopen("sample.txt", "w");

    fclose(fptr);

    printf("File closed successfully");

    return 0;
}
```

### Output
File closed successfully

### Explanation

Closing releases resources associated with the file.

# Applications of File Handling

File handling is used in:

1. Student management systems.
2. Banking applications.
3. Hospital databases.
4. Inventory management systems.
5. Payroll systems.
6. Log files.
7. Configuration files.
8. Report generation.
9. Data analysis.
10. Operating systems.

# Advantages of File Handling

1. Provides permanent storage.
2. Supports large amounts of data.
3. Reduces memory consumption.
4. Makes data reusable.
5. Enables record management.
6. Supports text and binary data.

# Limitations of File Handling

1. File operations are slower than memory operations.
2. Improper handling can corrupt data.
3. Requires proper error checking.
4. Files occupy storage space.
5. Simultaneous access may create conflicts.

# Summary

File handling in C allows programs to create, open, read, write, and close files. Using functions such as `fopen()`, `fprintf()`, `fscanf()`, `fgets()`, `fgetc()`, and `fclose()`, programmers can store information permanently and retrieve it whenever required. File handling plays an important role in developing databases, record systems, and real-world applications where data persistence is essential.

