# Python Strings

Below is an original, copyright-free **AlphaKnowledge** version. All examples and text are newly written and use only your specified names.

## Introduction

A string is a sequence of characters enclosed within quotes. Strings are used to store text such as names, messages, addresses, and sentences. In Python, there is no separate character data type, so even a single character is considered a string.

### Key Features

- Strings store textual data.
- A single character is also a string.
- Strings support indexing and slicing.
- Strings are immutable.
- Strings provide many built-in methods.
- Strings can be concatenated and repeated.

# Why Use Strings?

Strings are essential when working with names, messages, passwords, sentences, and other textual information.

### Example

```python
course = "AlphaKnowledge Python"

print(course)
```

### Output
AlphaKnowledge Python

### Explanation

The variable stores text inside quotation marks.

# Creating Strings

Strings can be created using single or double quotes.

## Using Single and Double Quotes

### Example

```python
a = 'AlphaKnowledge'

b = "Python Programming"

print(a)

print(b)
```

### Output
AlphaKnowledge
Python Programming

### Explanation

Both single and double quotes create strings.

# Multi-line Strings

Triple quotes are used to create strings spanning multiple lines.

### Example

```python
message = """
Welcome to AlphaKnowledge
Learn Python Step by Step
"""

print(message)
```

### Output
Welcome to AlphaKnowledge
Learn Python Step by Step

### Explanation

Triple quotes preserve line breaks.

# Accessing Characters

Strings use indexing. Indexing starts from 0.

## Positive Indexing

### Example

```python
text = "PYTHON"

print(text[0])

print(text[3])
```

### Output
P
H

### Explanation

Index 0 represents the first character.

## Negative Indexing

### Example

```python
text = "PYTHON"

print(text[-1])

print(text[-4])
```

### Output
N
T

### Explanation

Negative indexing starts from the end.

# String Slicing

Slicing extracts a part of a string.

### Example

```python
word = "PROGRAMMING"

print(word[0:4])

print(word[:7])

print(word[7:])

print(word[::-1])
```

### Output
PROG
PROGRAM
MING
GNIMMARGORP

### Explanation

Slicing creates a new string containing selected characters.

# Iterating Through Strings

Strings can be traversed using loops.

### Example

```python
language = "CODE"

for ch in language:
    print(ch)
```

### Output
C
O
D
E

### Explanation

The loop accesses one character at a time.

# String Immutability

Strings cannot be modified directly.

### Example

```python
title = "alphaknowledge"

title = "A" + title[1:]

print(title)
```

### Output
Alphaknowledge

### Explanation

A new string is created instead of modifying the original one.

# Deleting a String

The entire string variable can be removed using `del`.

### Example

```python
name = "Python"

del name
```

### Explanation

After deletion, the variable no longer exists.

# Updating Strings

Changes create new strings.

### Example

```python
message = "Learn Java"

updated = message.replace("Java", "Python")

print(updated)
```

### Output
Learn Python

### Explanation

The original string remains unchanged.

# Common String Methods

## len()

Returns the number of characters.

### Example

```python
platform = "AlphaKnowledge"

print(len(platform))
```

### Output
14

## upper() and lower()

Convert characters to uppercase or lowercase.

### Example

```python
text = "Python Course"

print(text.upper())

print(text.lower())
```

### Output
PYTHON COURSE
python course

## strip() and replace()

Remove spaces and replace text.

### Example

```python
text = "   Python   "

print(text.strip())

sentence = "Python is powerful"

print(sentence.replace("powerful", "awesome"))
```

### Output
Python
Python is awesome

# Concatenating Strings

Strings can be combined using `+`.

### Example

```python
first = "Alpha"

second = "Knowledge"

print(first + second)
```

### Output
AlphaKnowledge

### Explanation

The two strings are joined together.

# Repeating Strings

The `*` operator repeats strings.

### Example

```python
text = "Hi "

print(text * 3)
```

### Output
Hi Hi Hi

### Explanation

The string is repeated three times.

# Formatting Strings

## Using f-Strings

### Example

```python
student = "Akash Dangudubiyyapu"

score = 95

print(f"{student} scored {score}")
```

### Output
Akash Dangudubiyyapu scored 95

## Using format()

### Example

```python
text = "{} teaches Python at {}".format(
    "Mohit Chandaluri",
    "AlphaKnowledge"
)

print(text)
```

### Output
Mohit Chandaluri teaches Python at AlphaKnowledge

# Membership Testing

The `in` operator checks whether a substring exists.

### Example

```python
website = "AlphaKnowledge"

print("Alpha" in website)

print("Java" in website)
```

### Output
True
False

### Explanation

The operator returns `True` when the substring exists.

# Comparing Strings

### Example

```python
a = "Python"

b = "Python"

print(a == b)

print(a != "Java")
```

### Output
True
True

### Explanation

Comparison operators check string equality.

# Escape Characters

Escape sequences add special characters.

### Example

```python
quote = "Mohit Chandaluri said \"Keep Learning\""

print(quote)
```

### Output
Mohit Chandaluri said "Keep Learning"

# Advantages of Strings

1. Easy to store text.
2. Support indexing and slicing.
3. Provide many built-in methods.
4. Useful in data processing.
5. Support formatting and concatenation.
6. Immutable and safe from accidental changes.

# Limitations of Strings

1. Strings cannot be modified directly.
2. Large strings consume more memory.
3. Frequent modifications create new objects.

# Applications of Strings

- Storing names and addresses.
- Processing messages and documents.
- Password validation.
- Web development.
- File handling.
- Data analysis.

# Common String Methods

| Method | Description |
| --- | --- |
| `len()` | Returns length |
| `upper()` | Converts to uppercase |
| `lower()` | Converts to lowercase |
| `strip()` | Removes spaces |
| `replace()` | Replaces text |
| `split()` | Splits a string |
| `join()` | Joins strings |
| `find()` | Finds substring |
| `count()` | Counts occurrences |
| `startswith()` | Checks beginning |
| `endswith()` | Checks ending |

# Summary

Strings are sequences of characters used to store and manipulate text in Python. They support indexing, slicing, iteration, formatting, concatenation, and many built-in methods. Because strings are immutable, any modification creates a new string. Their simplicity and versatility make them one of the most frequently used data types in Python.

