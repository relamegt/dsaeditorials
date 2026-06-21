# C Program to Read Content of a File

## Introduction

Reading data from a file is one of the most important operations in file handling. It allows a program to retrieve previously stored information and process it whenever required. In C, reading a file involves three basic steps:

1. Opening the file.
2. Reading the data.
3. Closing the file.

The C Standard Library provides several functions to read file contents. Depending on the type of data and the application requirements, programmers can choose different methods.

All file-reading functions are declared in the `<stdio.h>` header file.

## Steps to Read a File

Reading a file generally consists of three stages:

### 1. Open the File

The file is opened using `fopen()` in read mode (`"r"`).

### 2. Read the Data

Data can be read using various functions such as:

- `fgetc()`
- `fgets()`
- `fscanf()`
- `fread()`

### 3. Close the File

After completing all operations, the file should be closed using `fclose()`.

# Reading a File Using fgetc()

The `fgetc()` function reads one character at a time from the file. It returns the next character and automatically moves the file pointer forward.

When the end of the file is reached, `fgetc()` returns `EOF`.

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;
    char ch;

    fptr = fopen("course.txt", "r");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    while ((ch = fgetc(fptr)) != EOF) {

        printf("%c", ch);
    }

    fclose(fptr);

    return 0;
}
```

Suppose `course.txt` contains:

```text
Welcome to AlphaKnowledge
```

### Output
Welcome to AlphaKnowledge

### Explanation

The `fgetc()` function reads one character at a time until it encounters `EOF`.

## When to Use fgetc()?

Use `fgetc()` when:

- Character-by-character processing is required.
- Counting characters.
- Searching specific symbols.
- Performing encryption or decryption.

# Reading a File Using fgets()

The `fgets()` function reads one line or a specified number of characters from a file and stores them in a character array.

### Syntax

```c
fgets(buffer, size, file_pointer);
```

## Example

```c
#include <stdio.h>

int main() {

    FILE *fptr;
    char line[100];

    fptr = fopen("students.txt", "r");

    if (fptr == NULL) {

        printf("File not found");

        return 0;
    }

    while (fgets(line, 100, fptr) != NULL) {

        printf("%s", line);
    }

    fclose(fptr);

    return 0;
}
```

Suppose `students.txt` contains:

```text
Akash Dangudubiyyapu
Mohit Chandaluri
Abhiram Gopisetti
```

### Output
Akash Dangudubiyyapu
Mohit Chandaluri
Abhiram Gopisetti

### Explanation

The `fgets()` function reads one line at a time until no more lines remain.

## When to Use fgets()?

Use `fgets()` when:

- Reading text files line by line.
- Reading log files.
- Processing configuration files.
- Handling long strings.

# Reading a File Using fscanf()

The `fscanf()` function works similarly to `scanf()`. It reads formatted input from a file.

### Syntax

```c
fscanf(file_pointer, format_specifier, variables);
```

## Example

Suppose `marks.txt` contains:

```text
Mohit 90
Abhiram 85
Hemesh 95
```

```c
#include <stdio.h>

int main() {

    FILE *fptr;

    char name[30];
    int marks;

    fptr = fopen("marks.txt", "r");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    while (fscanf(fptr, "%s %d", name, &marks) == 2) {

        printf("%s %d\n", name, marks);
    }

    fclose(fptr);

    return 0;
}
```

### Output
Mohit 90
Abhiram 85
Hemesh 95

### Explanation

The `fscanf()` function reads formatted data consisting of a string followed by an integer.

## When to Use fscanf()?

Use `fscanf()` when:

- Reading structured data.
- Processing records.
- Reading CSV-like data.
- Handling formatted text files.

# Reading a Binary File Using fread()

The `fread()` function reads blocks of binary data from a file.

### Syntax

```c
fread(pointer, size, count, file_pointer);
```

### Parameters

- `pointer` : Address where data will be stored.
- `size` : Size of each object.
- `count` : Number of objects.
- `file_pointer` : Pointer to the binary file.

## Example

```c
#include <stdio.h>

struct Student {

    int rollNo;
    int marks;

};

int main() {

    FILE *fptr;
    struct Student s;

    fptr = fopen("student.bin", "rb");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    while (fread(&s, sizeof(struct Student), 1, fptr)) {

        printf("Roll Number = %d\n", s.rollNo);

        printf("Marks = %d\n", s.marks);
    }

    fclose(fptr);

    return 0;
}
```

Suppose the binary file contains:

- Roll Number = 101
- Marks = 95

### Output

Roll Number = 101
Marks = 95

### Explanation

The `fread()` function reads binary data block by block and stores it in the structure variable.

## When to Use fread()?

Use `fread()` when:

- Reading binary files.
- Reading images.
- Reading structures.
- Handling databases.
- Processing large files.

# Comparison of File Reading Functions

| Function | Reads | Suitable For |
| --- | --- | --- |
| fgetc() | One character | Character processing |
| fgets() | One line | Text files |
| fscanf() | Formatted data | Structured records |
| fread() | Binary blocks | Binary files |

# Checking End of File

The constant `EOF` indicates the end of a file.

## Example

```c
while ((ch = fgetc(fptr)) != EOF) {

    printf("%c", ch);
}
```

### Explanation

The loop continues until the end of the file is reached.

# Real-Life Example

Suppose Akash Dangudubiyyapu develops a student management system. Student details of Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil are stored inside files.

- `fgets()` is used to read names line by line.
- `fscanf()` is used to read marks and roll numbers.
- `fread()` is used to retrieve complete student records from binary files.

This approach enables efficient storage and retrieval of information.

# Advantages of Reading Files

1. Provides permanent storage access.
2. Supports large amounts of data.
3. Enables record management.
4. Useful for databases and logs.
5. Supports text and binary files.
6. Makes data reusable.

# Limitations

1. File operations are slower than memory operations.
2. Improper file handling can lead to errors.
3. Files must be opened before reading.
4. Reading binary files requires proper data structures.
5. End-of-file conditions must be handled carefully.

# Summary

Reading a file in C involves opening the file, retrieving data, and closing it properly. C provides several functions such as `fgetc()`, `fgets()`, `fscanf()`, and `fread()` to read data in different ways. Character-based reading is suitable for simple processing, line-based reading works well for text files, formatted reading is useful for records, and binary reading is ideal for structures and raw data. Understanding these methods helps programmers efficiently manage and process stored information.

