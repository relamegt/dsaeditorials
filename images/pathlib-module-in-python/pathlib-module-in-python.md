# Pathlib Module in Python

## Introduction

The `pathlib` module provides an object-oriented approach to working with file and directory paths. Introduced in Python 3.4, it simplifies path manipulation and file operations compared to traditional string-based methods. The `Path` class is the primary class used to represent and interact with filesystem paths.

Unlike `os.path`, `pathlib` treats paths as objects, making code cleaner, easier to read, and platform-independent.

### Key Features

- Object-oriented representation of paths.
- Cross-platform compatibility.
- Easy path joining using the `/` operator.
- Built-in support for file reading and writing.
- Methods to check path properties.
- Recursive file searching.
- Supports file and directory creation.

## Why Use Pathlib?

Working with paths using string concatenation is error-prone and difficult to maintain. The `pathlib` module provides a simpler and safer way to manage files and directories.

### Example Without Pathlib

```python
path = "Documents" + "/" + "notes.txt"

print(path)
```

### Output
Documents/notes.txt

### Limitation

The path separator differs across operating systems. Manual concatenation makes code less readable and less portable.

# Importing Path Class

The `Path` class is imported from the `pathlib` module.

### Example

```python
from pathlib import Path

print(
    "Path Imported"
)
```

### Output
Path Imported

### Explanation

The `Path` class provides methods for interacting with files and directories.

# Creating a Path Object

Path objects represent file or directory paths.

### Example

```python
from pathlib import Path

file_path = Path(
    "Projects"
) / "program.py"

print(file_path)
```

### Output
Projects/program.py

### Explanation

The `/` operator joins paths in a platform-independent manner.

# Getting the Current Working Directory

The `cwd()` method returns the current working directory.

### Example

```python
from pathlib import Path

current = Path.cwd()

print(current)
```

### Output
C:\PythonProjects

### Explanation

`cwd()` returns the directory from which the script is running.

# Listing Files and Directories

The `iterdir()` method lists all files and folders inside a directory.

### Example

```python
from pathlib import Path

folder = Path(".")

for item in folder.iterdir():
    print(item)
```

### Output
Documents
main.py
notes.txt

### Explanation

The `iterdir()` method returns immediate contents of a directory.

# Listing Only Directories

The `is_dir()` method identifies folders.

### Example

```python
from pathlib import Path

folder = Path(".")

for item in folder.iterdir():
    if item.is_dir():
        print(item)
```

### Output
Projects
Images
Documents

### Explanation

The method filters only directory entries.

# Searching Python Files Recursively

The `rglob()` method searches files inside all subdirectories.

### Example

```python
from pathlib import Path

folder = Path(".")

for file in folder.rglob(
        "*.py"
):
    print(file)
```

### Output
main.py
Projects\demo.py
Projects\sample.py

### Explanation

`rglob()` recursively searches matching files.

# Checking Path Properties

Several methods provide information about paths.

### Example

```python
from pathlib import Path

path = Path(
    "notes.txt"
)

print(
    path.name
)

print(
    path.suffix
)

print(
    path.parent
)
```

### Output
notes.txt
.txt
.

### Explanation

- `name` returns the file name.
- `suffix` returns the extension.
- `parent` returns the parent directory.

# Checking File Existence

The `exists()` method determines whether a path exists.

### Example

```python
from pathlib import Path

file = Path(
    "notes.txt"
)

print(
    file.exists()
)
```

### Output
True

### Explanation

It returns `True` if the file exists, otherwise `False`.

# Checking Whether a Path Is a Directory

The `is_dir()` method checks whether a path points to a directory.

### Example

```python
from pathlib import Path

folder = Path(
    "Projects"
)

print(
    folder.is_dir()
)
```

### Output
True

### Explanation

It returns `True` only for directories.

# Reading a File

Files can be opened through a `Path` object.

### Example

```python
from pathlib import Path

with Path(
        "notes.txt"
).open(
        "r"
) as file:
    print(
        file.read()
    )
```

### Output
Python makes file handling simple.

### Explanation

The `open()` method works similarly to Python's built-in `open()` function.

# Writing to a File

The `write_text()` method writes text to a file.

### Example

```python
from pathlib import Path

Path(
    "message.txt"
).write_text(
    "Welcome to AlphaKnowledge"
)
```

### Output
File Created Successfully

### Explanation

If the file does not exist, it is created automatically.

# Reading Text Directly

The `read_text()` method reads file contents directly.

### Example

```python
from pathlib import Path

content = Path(
    "message.txt"
).read_text()

print(content)
```

### Output
Welcome to AlphaKnowledge

### Explanation

The entire file content is returned as a string.

# Creating an Empty File

The `touch()` method creates a new file.

### Example

```python
from pathlib import Path

file = Path(
    "sample.txt"
)

file.touch()

print(
    "File Created"
)
```

### Output
File Created

### Explanation

If the file already exists, its modification time is updated.

# Pure Paths

Pure paths perform path manipulation without accessing the filesystem.

## PurePath

### Example

```python
from pathlib import PurePath

path = PurePath(
    "Course/Python"
)

print(path)
```

### Output
Course/Python

## PurePosixPath

### Example

```python
from pathlib import PurePosixPath

path = PurePosixPath(
    "Data/Files"
)

print(path)
```

### Output
Data/Files

## PureWindowsPath

### Example

```python
from pathlib import PureWindowsPath

path = PureWindowsPath(
    "Data/Files"
)

print(path)
```

### Output
Data\Files

# Important Methods of Path Class

## 1. cwd()

Returns the current working directory.

### Example

```python
from pathlib import Path

print(
    Path.cwd()
)
```

## 2. exists()

Checks whether a path exists.

### Example

```python
from pathlib import Path

print(
    Path(
        "notes.txt"
    ).exists()
)
```

## 3. is_dir()

Checks whether the path is a directory.

### Example

```python
from pathlib import Path

print(
    Path(
        "Projects"
    ).is_dir()
)
```

## 4. iterdir()

Lists directory contents.

### Example

```python
from pathlib import Path

for item in Path(
        "."
).iterdir():
    print(item)
```

## 5. rglob()

Searches files recursively.

### Example

```python
from pathlib import Path

for file in Path(
        "."
).rglob(
        "*.txt"
):
    print(file)
```

## 6. touch()

Creates an empty file.

### Example

```python
from pathlib import Path

Path(
    "demo.txt"
).touch()
```

# Advantages of Pathlib

1. Provides an object-oriented interface.
2. Supports cross-platform path handling.
3. Eliminates manual path concatenation.
4. Simplifies file operations.
5. Improves code readability and maintainability.

# Limitations

1. Available only in Python 3.4 and above.
2. Some advanced operations still require the `os` module.
3. Beginners may need time to understand path objects.

# Summary

The `pathlib` module offers a modern and object-oriented approach to handling files and directories. Through the `Path` class, developers can create, read, write, search, and manage paths easily. Features such as `cwd()`, `exists()`, `iterdir()`, `rglob()`, and `touch()` make filesystem operations cleaner and more readable compared to traditional string-based approaches.

