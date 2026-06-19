# Reading a File in Python

## Introduction

Reading a file in Python means accessing data stored in external files and using it inside a program. Files may contain text, binary data, CSV records, or JSON objects. Reading files is useful for processing datasets, configuration files, reports, logs, and user-generated content.

Python provides several methods such as `read()`, `readline()`, and `readlines()` to retrieve data from files efficiently.

### Key Features

- Supports reading text and binary files.
- Allows reading complete files or partial content.
- Supports line-by-line processing.
- Handles CSV and JSON files easily.
- Provides automatic resource management using the `with` statement.

## Why Read Files?

Many applications need information stored outside the program. File reading allows programs to access saved data whenever required.

### Example Without File Reading

```python
message = "Welcome to AlphaKnowledge"

print(message)
```

### Output
Welcome to AlphaKnowledge

### Limitation

The data is hardcoded. To work with external data, files must be read.

# Basic File Reading

Reading a file involves three steps:

1. Open the file.
2. Read its contents.
3. Close the file.

### Example

Suppose `message.txt` contains:

```Code
Python Programming
Data Science
Machine Learning
```

```python
file = open(
    "message.txt",
    "r"
)

content = file.read()

print(content)

file.close()
```

### Output

```Code
Python Programming
Data Science
Machine Learning
```

### Explanation

The file is opened in read mode, all contents are read into a string, and the file is closed after reading.

# Using the with Statement

The `with` statement automatically closes the file after use.

### Example

Suppose `notes.txt` contains:

```Code
Artificial Intelligence
Deep Learning
```

```python
with open(
    "notes.txt",
    "r"
) as file:

    data = file.read()

    print(data)
```

### Output

```Code
Artificial Intelligence
Deep Learning
```

### Explanation

The file is automatically closed when the block finishes execution.

# Reading a File Line by Line

Reading line by line is useful when working with large files.

## Using a for Loop

### Example

Suppose `courses.txt` contains:

```Code
Python
Java
SQL
```

```python
file = open(
    "courses.txt",
    "r"
)

for line in file:

    print(
        line.strip()
    )

file.close()
```

### Output

```Code
Python
Java
SQL
```

### Explanation

Each line is read individually. The `strip()` method removes newline characters.

# Reading One Line at a Time Using readline()

The `readline()` method returns one line during each call.

### Example

```python
file = open(
    "courses.txt",
    "r"
)

line = file.readline()

while line:

    print(
        line.strip()
    )

    line = file.readline()

file.close()
```

### Output

```Code
Python
Java
SQL
```

### Explanation

The loop continues until no more lines remain.

# Reading All Lines Using readlines()

The `readlines()` method returns a list containing all lines.

### Example

```python
file = open(
    "courses.txt",
    "r"
)

lines = file.readlines()

print(lines)

file.close()
```

### Output

```python
['Python\n', 'Java\n', 'SQL']
```

### Explanation

Each line becomes an element in the list.

# Reading Specific Characters

The `read()` method can accept a number indicating how many characters should be read.

### Example

Suppose `welcome.txt` contains:

```Code
Welcome to Python Programming
```

```python
file = open(
    "welcome.txt",
    "r"
)

text = file.read(12)

print(text)

file.close()
```

### Output

```Code
Welcome to P
```

### Explanation

Only the first twelve characters are read from the file.

# Reading Binary Files

Binary files contain non-text data such as images, videos, and executable files.

### Example

```python
file = open(
    "sample.bin",
    "rb"
)

content = file.read()

print(content)

file.close()
```

### Output

```python
b'Python File Data'
```

### Explanation

The file is opened in binary mode (`rb`), and the data is returned as bytes.

# Reading CSV Files

CSV files store tabular data separated by commas.

### Example

Suppose `students.csv` contains:

```Code
Name,Marks
Akash,95
Rahul,88
```

```python
import csv

with open(
    "students.csv",
    "r"
) as file:

    reader = csv.reader(file)

    for row in reader:

        print(row)
```

### Output

```python
['Name', 'Marks']
['Akash', '95']
['Rahul', '88']
```

### Explanation

The `csv.reader()` function reads each row and converts it into a list.

# Reading JSON Files

JSON files are commonly used for storing structured data.

Suppose `employee.json` contains:

```json
{
    "name": "Akash",
    "role": "Developer"
}
```

### Example

```python
import json

with open(
    "employee.json",
    "r"
) as file:

    data = json.load(file)

    print(data)
```

### Output

```python
{'name': 'Akash', 'role': 'Developer'}
```

### Explanation

The `json.load()` function converts JSON data into a Python dictionary.

# Handling Exceptions While Reading Files

Exceptions prevent programs from crashing when files are missing.

### Example

```python
try:

    file = open(
        "data.txt",
        "r"
    )

    content = file.read()

    print(content)

except FileNotFoundError:

    print(
        "File does not exist."
    )

finally:

    print(
        "Reading operation completed."
    )
```

### Output

```Code
File does not exist.
Reading operation completed.
```

### Explanation

The exception is caught safely, and the `finally` block always executes.

# Important Methods Used for Reading Files

## 1. read()

Reads the complete file or a specified number of characters.

### Example

```python
file = open(
    "sample.txt",
    "r"
)

print(
    file.read()
)

file.close()
```

## 2. readline()

Reads one line at a time.

### Example

```python
file = open(
    "sample.txt",
    "r"
)

print(
    file.readline()
)

file.close()
```

## 3. readlines()

Returns all lines as a list.

### Example

```python
file = open(
    "sample.txt",
    "r"
)

print(
    file.readlines()
)

file.close()
```

# Advantages of Reading Files

1. Accesses external data easily.
2. Supports large datasets.
3. Enables data persistence.
4. Works with text, binary, CSV, and JSON files.
5. Useful for configuration files and reports.

# Limitations

1. Reading large files may consume memory.
2. Missing files raise exceptions.
3. Improper handling may cause resource leaks.
4. Binary data is not human-readable.

# Summary

Reading files in Python allows programs to access information stored externally. Python provides methods such as `read()`, `readline()`, and `readlines()` for retrieving data. The `with` statement automatically manages resources, while modules like `csv` and `json` simplify handling structured data. Understanding file reading is essential for developing real-world applications that process external information.

