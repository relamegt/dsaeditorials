# Python Strings

## Introduction

Strings are sequences of characters enclosed within single quotes, double quotes, or triple quotes. They are used to represent text data and can contain letters, numbers, symbols, and spaces. In Python, there is no separate character data type, so even a single character is considered a string of length one.

Strings are one of the most commonly used data types for storing and manipulating textual information.

### Key Features

- Strings store text data.
- Characters are arranged in a sequence.
- Support positive and negative indexing.
- Strings are immutable.
- Support slicing and iteration.
- Provide many built-in methods for text manipulation.
- Can be concatenated and repeated.

# Why Use Strings?

Strings allow programs to store and process textual information such as names, messages, addresses, and user input.

### Example

```python
name = "Python"

print(name)
```

### Output
Python

### Explanation

The variable `name` stores a string and the `print()` function displays it.

# Creating Strings

Strings can be created using single quotes or double quotes.

### Example

```python
a = 'Hello'

b = "Python"

print(a)

print(b)
```

### Output
Hello
Python

### Explanation

Both single and double quotes create string objects.

# Multi-line Strings

Triple quotes are used for strings spanning multiple lines.

### Example

```python
s = """Welcome
to
Python"""

print(s)
```

### Output
Welcome
to
Python

### Explanation

Triple quotes preserve line breaks exactly as written.

# Accessing Characters

Strings are indexed sequences.

### Positive Indexing

```python
s = "PYTHON"

print(s[0])

print(s[3])
```

### Output
P
H

### Explanation

Indexing starts from 0.

### Negative Indexing

```python
s = "PYTHON"

print(s[-1])

print(s[-4])
```

### Output
N
T

### Explanation

Negative indexing starts from the end of the string.

# String Slicing

Slicing extracts a portion of a string.

### Example

```python
s = "PYTHON"

print(s[1:4])

print(s[:3])

print(s[2:])

print(s[::-1])
```

### Output
YTH
PYT
THON
NOHTYP

### Explanation

- `s[1:4]` extracts characters from index 1 to 3.
- `s[:3]` starts from index 0.
- `s[2:]` extracts from index 2 onward.
- `s[::-1]` reverses the string.

# Looping Through Strings

Strings are iterable.

### Example

```python
s = "ABC"

for ch in s:

    print(ch)
```

### Output
A
B
C

### Explanation

Each iteration accesses one character from the string.

# String Immutability

Strings cannot be modified after creation.

### Example

```python
s = "python"

s = "P" + s[1:]

print(s)
```

### Output
Python

### Explanation

A new string is created instead of modifying the original string.

# Deleting Strings

Entire strings can be deleted using `del`.

### Example

```python
s = "Hello"

del s
```

### Explanation

The variable is removed from memory.

# Updating Strings

Strings are updated by creating new strings.

### Example

```python
s = "Python"

s = s.replace("Py", "py")

print(s)
```

### Output
python

### Explanation

`replace()` returns a new string.

# Common String Methods

## len()

Returns the total number of characters.

### Example

```python
s = "Python"

print(len(s))
```

### Output
6

## upper() and lower()

Convert characters to uppercase and lowercase.

### Example

```python
s = "Hello World"

print(s.upper())

print(s.lower())
```

### Output
HELLO WORLD
hello world

## strip()

Removes leading and trailing spaces.

### Example

```python
s = "   Python   "

print(s.strip())
```

### Output
Python

## replace()

Replaces one substring with another.

### Example

```python
s = "Python is easy"

print(s.replace("easy", "awesome"))
```

### Output
Python is awesome

# Concatenating Strings

Strings can be combined using the `+` operator.

### Example

```python
s1 = "Hello"

s2 = "World"

print(s1 + " " + s2)
```

### Output
Hello World

### Explanation

The strings are joined together.

# Repeating Strings

The `*` operator repeats a string.

### Example

```python
s = "Hi "

print(s * 3)
```

### Output
Hi Hi Hi

### Explanation

The string is repeated three times.

# String Formatting

## Using f-Strings

### Example

```python
name = "Emma"

age = 21

print(f"Name: {name}, Age: {age}")
```

### Output
Name: Emma, Age: 21

### Explanation

Variables are inserted directly inside curly braces.

## Using format()

### Example

```python
s = "My name is {} and I am {} years old"

print(s.format("Emily", 22))
```

### Output
My name is Emily and I am 22 years old

### Explanation

Values replace the placeholders `{}`.

# Membership Testing

The `in` operator checks whether a substring exists.

### Example

```python
s = "Python Programming"

print("Python" in s)

print("Java" in s)
```

### Output
True
False

### Explanation

The operator returns `True` if the substring exists and `False` otherwise.

# Escape Characters

Escape sequences represent special characters.

### Example

```python
print("Hello\nWorld")

print("Python\tProgramming")
```

### Output
Hello
World

Python    Programming

### Explanation

- `\n` creates a new line.
- `\t` inserts a tab space.

# String Comparison

Strings can be compared using comparison operators.

### Example

```python
a = "Apple"

b = "Banana"

print(a == b)

print(a < b)
```

### Output
False
True

### Explanation

Strings are compared lexicographically.

# Advantages of Strings

1. Easy to create and use.
2. Support indexing and slicing.
3. Provide numerous built-in methods.
4. Useful for text processing.
5. Support formatting and concatenation.
6. Work efficiently with loops.

# Limitations of Strings

1. Strings are immutable.
2. Large string operations consume memory.
3. Frequent modifications create new objects.
4. Character deletion is not possible directly.

# Applications of Strings

- Storing names and messages.
- User input processing.
- Text formatting.
- File handling.
- Data validation.
- Pattern matching.
- Natural language processing.
- Web development.

# Common String Methods

| Method | Description |
| --- | --- |
| `len()` | Returns string length |
| `upper()` | Converts to uppercase |
| `lower()` | Converts to lowercase |
| `strip()` | Removes spaces |
| `replace()` | Replaces substrings |
| `split()` | Splits a string |
| `join()` | Joins elements |
| `find()` | Finds substring position |
| `count()` | Counts occurrences |
| `startswith()` | Checks starting substring |
| `endswith()` | Checks ending substring |

# Summary

Strings are sequences of characters used to represent text in Python. They support indexing, slicing, iteration, concatenation, formatting, and many built-in methods for manipulation. Since strings are immutable, modifications create new string objects rather than altering existing ones. Strings are fundamental to text processing and are widely used in applications such as input handling, web development, file processing, and data analysis.

