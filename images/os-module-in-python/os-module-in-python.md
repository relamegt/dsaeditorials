# OS Module in Python

## Introduction

The `os` module in Python provides functions that allow programs to interact with the operating system. It helps perform tasks such as working with directories, creating and deleting files, retrieving file information, checking file existence, and managing paths.

Since the `os` module is part of Python's standard library, no additional installation is required.

### Key Features

- Access the current working directory.
- Create and remove files and directories.
- List files and folders.
- Rename files and directories.
- Check file existence and size.
- Retrieve file metadata and permissions.
- Perform platform-independent path operations.

## Why Use the OS Module?

Many applications need to interact with the file system and operating system. The `os` module provides a convenient way to perform these operations.

### Example Without OS Module

```python
path = "notes.txt"

print(path)
```

### Output
notes.txt

### Limitation

The above example only stores a path as a string. It cannot create, delete, or manipulate files and directories.

# Importing the OS Module

Before using its functions, the module must be imported.

### Example

```python
import os

print(
    "OS Module Imported"
)
```

### Output
OS Module Imported

# Getting the Current Working Directory

The current working directory is the folder where Python is currently operating.

### Example

```python
import os

cwd = os.getcwd()

print(cwd)
```

### Output

```text
C:\Projects\Python
```

### Explanation

The `getcwd()` function returns the current directory path.

# Changing the Current Working Directory

The `chdir()` function changes the current directory.

### Example

```python
import os

print(
    os.getcwd()
)

os.chdir(
    ".."
)

print(
    os.getcwd()
)
```

### Output

```text
C:\Projects\Python
C:\Projects
```

### Explanation

The `chdir()` method moves one level upward.

# Creating a Directory

The `mkdir()` function creates a single directory.

### Example

```python
import os

os.mkdir(
    "PythonNotes"
)

print(
    "Directory Created"
)
```

### Output
Directory Created

### Explanation

A new folder named `PythonNotes` is created.

# Creating Multiple Directories

The `makedirs()` function creates nested directories.

### Example

```python
import os

os.makedirs(
    "Projects/Python/Examples"
)

print(
    "Folders Created"
)
```

### Output
Folders Created

### Explanation

Missing parent directories are automatically created.

# Listing Files and Directories

The `listdir()` function returns all files and folders inside a path.

### Example

```python
import os

items = os.listdir()

print(items)
```

### Output

```python
['Documents', 'notes.txt', 'Projects']
```

### Explanation

The function returns a list containing files and directories.

# Removing a File

The `remove()` function deletes a file.

### Example

```python
import os

os.remove(
    "old_notes.txt"
)

print(
    "File Deleted"
)
```

### Output
File Deleted

### Explanation

The specified file is permanently removed.

# Removing an Empty Directory

The `rmdir()` function removes an empty directory.

### Example

```python
import os

os.rmdir(
    "TempFolder"
)

print(
    "Directory Removed"
)
```

### Output
Directory Removed

### Explanation

Only empty directories can be deleted using `rmdir()`.

# Renaming a File

The `rename()` function changes the name of a file or folder.

### Example

```python
import os

os.rename(
    "old_report.txt",
    "new_report.txt"
)

print(
    "File Renamed"
)
```

### Output
File Renamed

### Explanation

The file name changes from `old_report.txt` to `new_report.txt`.

# Checking File Existence

The `exists()` function determines whether a file or directory exists.

### Example

```python
import os

result = os.path.exists(
    "data.txt"
)

print(result)
```

### Output

```python
True
```

### Explanation

If the file exists, the function returns `True`; otherwise, it returns `False`.

# Getting File Size

The `getsize()` function returns the size of a file in bytes.

### Example

```python
import os

size = os.path.getsize(
    "report.txt"
)

print(size)
```

### Output

```python
256
```

### Explanation

The output represents the size of the file in bytes.

# Joining Paths

The `join()` function creates platform-independent paths.

### Example

```python
import os

path = os.path.join(
    "Projects",
    "Python",
    "demo.py"
)

print(path)
```

### Output

```text
Projects\Python\demo.py
```

### Explanation

The separator is automatically adjusted according to the operating system.

# Getting File Information

The `stat()` function returns metadata about a file.

### Example

```python
import os

info = os.stat(
    "report.txt"
)

print(
    info.st_size
)
```

### Output

```python
256
```

### Explanation

The `st_size` attribute returns the file size.

# Changing File Permissions

The `chmod()` function changes file permissions.

### Example

```python
import os

os.chmod(
    "report.txt",
    0o600
)

print(
    "Permission Changed"
)
```

### Output
Permission Changed

### Explanation

The owner receives read and write permissions.

# Getting the Operating System Name

The `name` attribute identifies the operating system.

### Example

```python
import os

print(
    os.name
)
```

### Output

```python
nt
```

### Explanation

- `nt` → Windows
- `posix` → Linux or macOS

# Using os.popen()

The `popen()` function executes operating system commands.

### Example

```python
import os

command = os.popen(
    "echo Hello Python"
)

print(
    command.read()
)
```

### Output
Hello Python

### Explanation

The command output is returned as a string.

# Important Functions in the OS Module

## 1. getcwd()

Returns the current working directory.

### Example

```python
import os

print(
    os.getcwd()
)
```

## 2. listdir()

Lists files and directories.

### Example

```python
import os

print(
    os.listdir()
)
```

## 3. mkdir()

Creates a directory.

### Example

```python
import os

os.mkdir(
    "Examples"
)
```

## 4. remove()

Deletes a file.

### Example

```python
import os

os.remove(
    "temp.txt"
)
```

## 5. rename()

Renames a file.

### Example

```python
import os

os.rename(
    "a.txt",
    "b.txt"
)
```

## 6. exists()

Checks file existence.

### Example

```python
import os

print(
    os.path.exists(
        "sample.txt"
    )
)
```

# Advantages of the OS Module

1. Provides access to operating system features.
2. Supports file and directory management.
3. Works across multiple platforms.
4. Simplifies path handling.
5. Helps automate system tasks.

# Limitations

1. Some functions are platform dependent.
2. Incorrect operations may delete important files.
3. Permission restrictions may prevent execution.
4. Certain functions require administrator privileges.

# Summary

The `os` module provides a collection of functions for interacting with the operating system. It allows programs to manage files, directories, permissions, and paths efficiently. Functions such as `getcwd()`, `mkdir()`, `listdir()`, `rename()`, and `exists()` simplify system-related tasks and are widely used in file handling, automation, and scripting applications.

