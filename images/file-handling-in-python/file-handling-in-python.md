# File Handling in Python

## Introduction

File handling allows programs to store and retrieve data from files. It provides a way to create, open, read, write, append and close files. File handling is useful when data needs to be stored permanently instead of being lost when the program ends.

Python provides built-in functions that make file operations simple and efficient.

### Key Features

- Supports reading and writing files.
- Stores data permanently.
- Works with text, CSV, JSON and other file types.
- Automatically handles file resources using the `with` statement.
- Supports exception handling during file operations.

## Why File Handling?

Variables store data temporarily in memory. Once the program terminates, the data is lost. Files help preserve information for future use.

### Example Without File Handling

```python
student_name = "Akash"

print(student_name)
```

### Output
Akash

### Limitation

The data exists only while the program runs. After termination, the value is lost.

# Opening a File

The `open()` function is used to open a file.

### Syntax

```python
file = open(
    "filename.txt",
    "mode"
)
```

### Parameters

- `filename.txt`: Name or path of the file.
- `mode`: Specifies how the file should be accessed.

If no mode is specified, Python uses read mode (`r`) by default.

## Example

```python
file = open(
    "students.txt",
    "r"
)

print(file)

file.close()
```

### Output
<_io.TextIOWrapper name='students.txt' mode='r' encoding='UTF-8'>

### Explanation

The file is opened in read mode and a file object is returned.

# File Modes

| Mode | Description |
| --- | --- |
| `r` | Read file |
| `w` | Write file (overwrites existing data) |
| `a` | Append data |
| `x` | Create a new file |
| `r+` | Read and write |
| `rb` | Read binary file |
| `wb` | Write binary file |

# Closing a File

The `close()` method releases resources associated with the file.

### Example

```python
file = open(
    "students.txt",
    "r"
)

file.close()
```

### Explanation

Closing files prevents resource leakage and ensures data is saved properly.

# Checking File Properties

File objects contain useful properties.

### Example

```python
file = open(
    "students.txt",
    "r"
)

print(
    "Name:",
    file.name
)

print(
    "Mode:",
    file.mode
)

print(
    "Closed:",
    file.closed
)

file.close()

print(
    "Closed:",
    file.closed
)
```

### Output
Name: students.txt

Mode: r

Closed: False

Closed: True

### Explanation

- `name` returns the file name.
- `mode` returns the file mode.
- `closed` indicates whether the file is closed.

# Reading a File

The `read()` method reads the entire content of a file.

### Example

Suppose `courses.txt` contains:

Python

Java

SQL

```python
file = open(
    "courses.txt",
    "r"
)

content = file.read()

print(content)

file.close()
```

### Output
Python

Java

SQL

### Explanation

`read()` retrieves the complete contents of the file.

# Reading One Line

The `readline()` method reads one line at a time.

### Example

```python
file = open(
    "courses.txt",
    "r"
)

print(
    file.readline()
)

file.close()
```

### Output
Python

### Explanation

Only the first line is read.

# Reading All Lines

The `readlines()` method returns a list containing all lines.

### Example

```python
file = open(
    "courses.txt",
    "r"
)

print(
    file.readlines()
)

file.close()
```

### Output
['Python\n', 'Java\n', 'SQL']

### Explanation

Each line becomes an element of the list.

# Writing to a File

The `write()` method adds content to a file.

### Example

```python
file = open(
    "notes.txt",
    "w"
)

file.write(
    "Welcome to AlphaKnowledge."
)

file.close()

print(
    "File written successfully."
)
```

### Output
File written successfully.

### Explanation

The file is opened in write mode. Existing content is overwritten.

# Appending to a File

Append mode adds new content without deleting existing data.

### Example

```python
file = open(
    "notes.txt",
    "a"
)

file.write(
    "\nPython is easy to learn."
)

file.close()

print(
    "Content appended."
)
```

### Output
Content appended.

### Explanation

New data is added at the end of the file.

# Using with Statement

The `with` statement automatically closes files.

### Example

Suppose `message.txt` contains:

Welcome to Python

```python
with open(
    "message.txt",
    "r"
) as file:

    data = file.read()

    print(data)
```

### Output
Welcome to Python

### Explanation

The file closes automatically when the block ends.

# Handling Exceptions in File Operations

Exception handling prevents program crashes when files are missing.

### Example

```python
try:

    file = open(
        "data.txt",
        "r"
    )

    print(
        file.read()
    )

except FileNotFoundError:

    print(
        "File not found."
    )

finally:

    print(
        "Operation completed."
    )
```

### Output
File not found.

Operation completed.

### Explanation

The exception is handled gracefully and the program continues execution.

# Creating a File

Using `x` mode creates a new file.

### Example

```python
try:

    file = open(
        "report.txt",
        "x"
    )

    print(
        "File created."
    )

    file.close()

except FileExistsError:

    print(
        "File already exists."
    )
```

### Output
File created.

### Explanation

A new file is created if it does not already exist.

# Advantages of File Handling

1. Stores data permanently.
2. Supports large amounts of data.
3. Reduces memory usage.
4. Enables data sharing between programs.
5. Supports various file formats.

# Limitations

1. File operations are slower than memory operations.
2. Missing files may raise exceptions.
3. Improper closing may cause data loss.
4. Large files may require efficient processing techniques.

# Summary

File handling in Python allows programs to interact with files for storing and retrieving information. Python provides functions such as `open()`, `read()`, `write()`, and `close()` to perform file operations. The `with` statement simplifies resource management by automatically closing files. Proper exception handling further improves reliability, making file handling an essential feature for building real-world applications.

