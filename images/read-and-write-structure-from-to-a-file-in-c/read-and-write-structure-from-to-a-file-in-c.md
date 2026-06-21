# Read and Write Structure From/To a File in C

## Introduction

Structures are used to store multiple related data members together. Sometimes, we need to permanently save structure data so that it can be used later. This can be achieved using file handling.

In C, structures are usually stored in binary format because binary files preserve the exact byte representation of structure data and provide faster input/output operations.

The `fwrite()` function is used to write structures to a file, while the `fread()` function is used to read structures from a file.

For binary file operations, the file should be opened in binary modes:

- `"wb"` : Write binary data.
- `"rb"` : Read binary data.
- `"ab"` : Append binary data.
- `"wb+"` : Read and write binary data.

## Writing Structures to a File Using fwrite()

The `fwrite()` function writes blocks of binary data into a file.

### Syntax

```c
size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
```

### Parameters

- `ptr` : Pointer to the data to be written.
- `size` : Size of each element in bytes.
- `count` : Number of elements to write.
- `stream` : File pointer.

### Return Value

It returns the number of objects successfully written to the file.

## Example: Writing a Structure to a File

```c
#include <stdio.h>
#include <stdlib.h>

struct Student {

    int rollNo;
    char firstName[20];
    char lastName[20];

};

int main() {

    FILE *fptr;

    struct Student student1 = {101, "Mohit", "Chandaluri"};

    fptr = fopen("student.bin", "wb");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    if (fwrite(&student1, sizeof(struct Student), 1, fptr)) {

        printf("Structure written successfully");
    }
    else {

        printf("Error writing to file");
    }

    fclose(fptr);

    return 0;
}
```

### Output
Structure written successfully

### Explanation

In this program:

- A structure named `Student` is created.
- The file `student.bin` is opened in binary write mode.
- `fwrite()` writes the structure contents into the file.
- Finally, the file is closed using `fclose()`.

---

## Reading Structures from a File Using fread()

The `fread()` function reads blocks of binary data from a file.

### Syntax

```c
size_t fread(void *ptr, size_t size, size_t count, FILE *stream);
```

### Parameters

- `ptr` : Address where data will be stored.
- `size` : Size of each object.
- `count` : Number of objects to read.
- `stream` : File pointer.

### Return Value

It returns the number of objects successfully read.

## Example: Reading a Structure from a File

```c
#include <stdio.h>
#include <stdlib.h>

struct Student {

    int rollNo;
    char firstName[20];
    char lastName[20];

};

int main() {

    FILE *fptr;

    struct Student student;

    fptr = fopen("student.bin", "rb");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    fread(&student, sizeof(struct Student), 1, fptr);

    printf("Roll Number : %d\n", student.rollNo);
    printf("First Name  : %s\n", student.firstName);
    printf("Last Name   : %s\n", student.lastName);

    fclose(fptr);

    return 0;
}
```

### Output
Roll Number : 101
First Name  : Mohit
Last Name   : Chandaluri

### Explanation

The `fread()` function reads the binary contents stored in the file and stores them into the structure variable. The values are then displayed on the screen.

---

## Writing Multiple Structures to a File

```c
#include <stdio.h>

struct Student {

    int rollNo;
    char name[20];

};

int main() {

    FILE *fptr;

    struct Student students[3] = {

        {101, "Mohit"},
        {102, "Abhiram"},
        {103, "Hemesh"}

    };

    fptr = fopen("students.bin", "wb");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    fwrite(students, sizeof(struct Student), 3, fptr);

    fclose(fptr);

    printf("Records saved successfully");

    return 0;
}
```

### Output
Records saved successfully

### Explanation

The entire array of structures is written into the binary file using a single `fwrite()` statement.

---

## Reading Multiple Structures from a File

```c
#include <stdio.h>

struct Student {

    int rollNo;
    char name[20];

};

int main() {

    FILE *fptr;

    struct Student student;

    fptr = fopen("students.bin", "rb");

    if (fptr == NULL) {

        printf("Unable to open file");

        return 0;
    }

    while (fread(&student, sizeof(struct Student), 1, fptr) == 1) {

        printf("Roll Number : %d\n", student.rollNo);
        printf("Name : %s\n\n", student.name);
    }

    fclose(fptr);

    return 0;
}
```

### Output
Roll Number : 101
Name : Mohit
Roll Number : 102
Name : Abhiram
Roll Number : 103
Name : Hemesh

### Explanation

The loop repeatedly calls `fread()` until no more records are available in the file.

---

## File Modes Used with Structures

| Mode | Purpose |
| --- | --- |
| `"rb"` | Read binary file |
| `"wb"` | Write binary file |
| `"ab"` | Append binary data |
| `"rb+"` | Read and write binary file |
| `"wb+"` | Create file and perform both reading and writing |

---

## Advantages of Using Binary Files with Structures

- Faster than text files.
- Stores complete structures directly.
- Preserves exact memory representation.
- Suitable for databases and record management.
- Efficient for handling large amounts of data.

## Limitations

- Binary files cannot be read easily by humans.
- Structure changes may make old files incompatible.
- Data portability may vary across systems.
- Corrupted binary files are difficult to recover.

## Real-Life Applications

- Student Management Systems.
- Employee Record Systems.
- Banking Applications.
- Library Management Systems.
- Inventory Management Systems.
- Hospital Management Systems.

## Summary

Structures can be stored and retrieved efficiently using binary files. The `fwrite()` function writes structures into a file, while `fread()` reads them back. Binary file operations are faster and preserve the original memory layout of structures, making them useful for applications that manage records such as students, employees, and inventory systems.

