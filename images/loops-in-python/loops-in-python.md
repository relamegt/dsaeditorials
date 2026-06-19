# Loops in Python

## Introduction

Loops are control structures that allow a block of code to execute repeatedly until a condition becomes false or all elements of a sequence are processed. They eliminate the need to write the same code multiple times and make programs more efficient and compact.

Python mainly provides two types of loops:

- `for` loop
- `while` loop

Loops can also be nested and combined with control statements like `break`, `continue`, and `pass`.

### Key Features

- Execute code repeatedly.
- Reduce code duplication.
- Support iteration over sequences.
- Allow condition-based repetition.
- Can be nested for complex patterns.
- Work with control statements for better flow management.

# Why Use Loops?

Without loops, repetitive tasks would require writing the same statements multiple times.

### Example Without Loops

```python
print("Welcome to AlphaKnowledge")
print("Welcome to AlphaKnowledge")
print("Welcome to AlphaKnowledge")
```

### Output
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge

### Limitation

Writing repetitive statements manually increases code size and reduces maintainability.

# for Loop

The `for` loop is used to iterate over sequences such as lists, tuples, strings, and ranges.

### Example

```python
n = 5

for i in range(n):
    print(i)
```

### Output
0
1
2
3
4

### Explanation

- `range(5)` generates numbers from 0 to 4.
- The loop executes once for each value.
- Variable `i` stores the current iteration value.

# Iterating Through Lists

A `for` loop can directly access list elements.

### Example

```python
courses = [
    "Python",
    "Java",
    "C++"
]

for course in courses:
    print(course)
```

### Output
Python
Java
C++

### Explanation

Each element of the list is assigned to `course` during every iteration.

# Iterating Using Index Values

The combination of `range()` and `len()` allows iteration using indexes.

### Example

```python
students = [
    "Akash",
    "Abhiram",
    "Hemesh"
]

for i in range(len(students)):
    print(students[i])
```

### Output
Akash
Abhiram
Hemesh

### Explanation

- `len(students)` returns 3.
- `range(3)` generates index values 0, 1, and 2.
- Each index accesses a list element.

# while Loop

The `while` loop repeatedly executes a block as long as its condition remains true.

### Example

```python
count = 1

while count <= 3:
    print("Hello AlphaKnowledge")
    count += 1
```

### Output
Hello AlphaKnowledge
Hello AlphaKnowledge
Hello AlphaKnowledge

### Explanation

The loop runs until the condition `count <= 3` becomes false.

# Infinite while Loop

A loop whose condition always remains true is called an infinite loop.

### Example

```python
while True:
    print("Running...")
```

### Explanation

Since the condition is always true, the loop never stops automatically.

### Note

Infinite loops should be used carefully because they require manual termination.

# Nested Loops

A loop inside another loop is called a nested loop.

### Example

```python
for i in range(1, 5):
    for j in range(i):
        print(i, end=" ")
    print()
```

### Output
1
2 2
3 3 3
4 4 4 4

### Explanation

The inner loop executes completely for every iteration of the outer loop.

# Looping Through Strings

Strings can also be iterated character by character.

### Example

```python
word = "Python"

for ch in word:
    print(ch)
```

### Output
P
y
t
h
o
n

### Explanation

Each character is processed individually.

# break Statement

The `break` statement immediately terminates a loop.

### Example

```python
for i in range(1, 10):
    if i == 5:
        break

    print(i)
```

### Output
1
2
3
4

### Explanation

When `i` becomes 5, the loop stops.

# continue Statement

The `continue` statement skips the current iteration and moves to the next one.

### Example

```python
for i in range(1, 6):
    if i == 3:
        continue

    print(i)
```

### Output
1
2
4
5

### Explanation

The value 3 is skipped.

# pass Statement

The `pass` statement does nothing and acts as a placeholder.

### Example

```python
for i in range(3):
    pass

print("Loop Finished")
```

### Output
Loop Finished

### Explanation

`pass` allows empty blocks without causing syntax errors.

# else with Loops

Python allows an `else` block with loops. It executes when the loop completes normally.

### Example

```python
for i in range(3):
    print(i)
else:
    print("Loop Completed")
```

### Output
0
1
2
Loop Completed

### Explanation

Since the loop finishes without encountering a `break`, the `else` block executes.

# Important Functions Used with Loops

## 1. range()

Generates a sequence of numbers.

### Example

```python
for i in range(2, 7):
    print(i)
```

### Output
2
3
4
5
6

## 2. len()

Returns the number of elements.

### Example

```python
languages = [
    "Python",
    "Java",
    "C"
]

print(len(languages))
```

### Output
3

## 3. enumerate()

Returns both index and value.

### Example

```python
subjects = [
    "Math",
    "Science",
    "English"
]

for index, value in enumerate(subjects):
    print(index, value)
```

### Output
0 Math
1 Science
2 English

# for Loop vs while Loop

| Feature | for Loop | while Loop |
| --- | --- | --- |
| Iteration Type | Sequence based | Condition based |
| Initialization | Automatic | Manual |
| Counter Update | Automatic | Manual |
| Infinite Loop Risk | Low | High |
| Best Use Case | Known iterations | Unknown iterations |

# Advantages of Loops

1. Reduce code duplication.
2. Simplify repetitive tasks.
3. Improve readability.
4. Support sequence traversal.
5. Allow pattern generation.
6. Make programs efficient and scalable.

# Limitations

1. Infinite loops may consume resources.
2. Deeply nested loops reduce readability.
3. Improper conditions may cause logical errors.
4. Excessive loops can decrease performance.

# Summary

Loops are essential control structures that execute blocks of code repeatedly. Python provides `for` loops for sequence traversal and `while` loops for condition-based repetition. Additional statements like `break`, `continue`, and `pass` offer more control over loop execution. Understanding loops is fundamental for solving repetitive tasks, processing collections, and building efficient Python programs.

