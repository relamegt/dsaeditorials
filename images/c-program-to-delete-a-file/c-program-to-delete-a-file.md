# C Program to Delete a File

## Introduction

File handling in C allows programmers to create, read, write, modify, and delete files stored on secondary storage devices. Sometimes, files are no longer needed and should be removed to free storage space or prevent unnecessary data accumulation.

The C Standard Library provides the `remove()` function to delete files from the file system. This function is declared in the `<stdio.h>` header file.

When a file is deleted successfully, it is permanently removed from its storage location.

## remove() Function

The `remove()` function is used to delete a specified file from the system.

### Syntax

```c
remove(file_name);
```

### Parameters

- `file_name` : Name or path of the file to be deleted.

### Return Value

- Returns `0` if the file is deleted successfully.
- Returns a non-zero value if the deletion fails.

# Deleting a File

## Example

```c
#include <stdio.h>

int main() {

    const char *fileName = "records.txt";

    if (remove(fileName) == 0) {

        printf("File deleted successfully");
    }
    else {

        printf("Unable to delete the file");
    }

    return 0;
}
```

### Output
File deleted successfully

### Explanation

In this program:

1. The filename `"records.txt"` is stored in a character pointer.
2. The `remove()` function attempts to delete the file.
3. If the file is deleted successfully, `remove()` returns `0`.
4. Otherwise, an error message is displayed.

# Deleting a File Using User Input

Instead of hardcoding the filename, we can ask the user to enter the file name.

## Example

```c
#include <stdio.h>

int main() {

    char fileName[100];

    printf("Enter file name: ");
    scanf("%s", fileName);

    if (remove(fileName) == 0) {

        printf("File deleted successfully");
    }
    else {

        printf("File does not exist or cannot be deleted");
    }

    return 0;
}
```

### Input

students.txt

### Output

File deleted successfully

### Explanation

The user enters the filename, and the program passes it to the `remove()` function for deletion.

# Deleting a File Using an Absolute Path

The `remove()` function can also delete files using complete paths.

## Example

```c
#include <stdio.h>

int main() {

    if (remove("C:\\Documents\\course.txt") == 0) {

        printf("File deleted successfully");
    }
    else {

        printf("Deletion failed");
    }

    return 0;
}
```

### Output
File deleted successfully

### Explanation

The complete path is supplied to `remove()`, allowing files stored in other directories to be deleted.

# Handling Errors During Deletion

Deletion may fail due to several reasons:

- The file does not exist.
- The file is already open in another program.
- The program lacks permission to delete the file.
- The specified path is incorrect.

## Example

```c
#include <stdio.h>

int main() {

    if (remove("report.txt") != 0) {

        printf("Error deleting file");
    }
    else {

        printf("File deleted successfully");
    }

    return 0;
}
```

### Output
Error deleting file

### Explanation

If the file is unavailable or inaccessible, the `remove()` function returns a non-zero value.

# Practical Example

Suppose Akash Dangudubiyyapu develops a student management system. Temporary reports are created for Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

After processing the reports, these temporary files are no longer needed. Using the `remove()` function, the program can automatically delete those files to save storage space and maintain system cleanliness.

# Important Points About remove()

- The file must be closed before deletion.
- The program should have proper permissions.
- Deleted files are permanently removed from storage.
- `remove()` works for both text and binary files.
- Always check the return value to verify successful deletion.

# Comparison Between File Operations

| Operation | Function Used |
| --- | --- |
| Create/Open File | `fopen()` |
| Read Data | `fscanf()`, `fgets()`, `fgetc()`, `fread()` |
| Write Data | `fprintf()`, `fputs()`, `fputc()`, `fwrite()` |
| Move File Pointer | `fseek()` |
| Close File | `fclose()` |
| Delete File | `remove()` |

# Advantages of File Deletion

1. Frees storage space.
2. Removes unnecessary files.
3. Helps maintain organized directories.
4. Supports automatic cleanup in applications.
5. Works with both text and binary files.

# Limitations

1. Deleted files cannot be recovered easily.
2. File permissions may prevent deletion.
3. Files currently in use cannot be removed.
4. Incorrect file names cause deletion failure.

# Summary

The `remove()` function in C is used to delete files from the file system. It accepts the filename or file path as an argument and returns `0` when deletion succeeds. Proper error handling and permission checking are important when deleting files. The function is useful in applications that generate temporary files, reports, logs, and backup files that need to be removed after use.

