# Input and Output in Python

## Introduction

Input and output operations form the foundation of interaction between a Python program and the user. Input operations allow a program to receive information during execution, while output operations enable it to display information on the screen. Python provides built-in functions such as `input()` and `print()` to perform these tasks efficiently.

The `input()` function reads data entered by the user and returns it as a string by default. The `print()` function is used to display text, variables, expressions, and formatted messages on the console.

### Key Features

- **User Interaction**: Programs can receive data from users during execution.
- **Simple Syntax**: Input and output operations require only built-in functions.
- **Default String Input**: `input()` returns values as strings unless explicitly converted.
- **Flexible Output**: `print()` can display strings, variables, expressions, and multiple values simultaneously.
- **Type Conversion Support**: Input values can easily be converted into integers, floating-point numbers, and other data types.

## Why Input and Output?

Most programs need to communicate with users. Input operations allow users to provide information, while output operations present results in a readable form.

### Example Without User Input

```python
course = "AlphaKnowledge Python Course"

print(course)
```

### Output
AlphaKnowledge Python Course

### Limitation

In the above example, the value is fixed. Every time the program runs, it produces the same output. There is no way for users to provide their own data.

## Taking Input Using input()

The `input()` function allows programs to accept data from users during execution. By default, the value entered by the user is returned as a string.

### Example

```python
name = input("Enter your name: ")

print("Welcome,", name)
```

### *Sample Input*

*`Akash Dangudubiyyapu`* 

### *Output*

*`Welcome, Akash Dangudubiyyapu`* 

### Explanation

1. The program displays a prompt message.
2. The user enters a value.
3. The entered value is stored in the variable `name`.
4. The `print()` function displays the greeting message.

# Printing Output Using print()

The `print()` function displays information on the console. It can print strings, variables, expressions, and multiple values.

## Printing Text

### Example

```python
print("Hello, AlphaKnowledge!")
```

### Output
Hello, AlphaKnowledge!

### Explanation

The text enclosed inside quotation marks is a string literal. The `print()` function sends the string to the console.

# Printing Variables

Variables can be displayed directly using the `print()` function.

### Example

```python
mentor = "Mohit Chandaluri"

print(mentor)
```

### Output
Mohit Chandaluri

## Printing Multiple Variables

Multiple variables can be printed together by separating them with commas.

### Example

```python
name = "Abhiram Gopisetti"
age = 22
city = "Vijayawada"

print(name, age, city)
```

### Output
Abhiram Gopisetti 22 Vijayawada

### Explanation

The `print()` function automatically inserts spaces between the values separated by commas.

# Taking Multiple Inputs

Python allows multiple values to be accepted in a single line using the `split()` method.

### Example

```python
first_name, last_name = input(
        "Enter first and last name: "
).split()

print(first_name)
print(last_name)
```

### *Sample Input*

*`Akash Dangudubiyyapu`*
 

### *Output*

*`Akash
Dangudubiyyapu`* 

### *Explanation*

The `split()` method divides the input into separate strings based on spaces and assigns them to individual variables.

# Taking Integer Input

Since `input()` returns strings, numerical input must be converted using `int()`.

### Example

```python
age = int(input("Enter your age: "))

print(age)
```

### *Sample Input*

*`23`* 

### *Output*

*`23`* 

### Explanation

The `int()` function converts the string returned by `input()` into an integer.

# Taking Floating-Point Input

Decimal values can be accepted using the `float()` function.

### Example

```python
cgpa = float(input(
        "Enter your CGPA: "
))

print(cgpa)
```

### *Sample Input*

*`9.24`* 

### *Output*

*`9.24`* 

### Explanation

The `float()` function converts the string input into a floating-point number.

# Important Functions Used in Input and Output

Python provides several functions for handling user interaction.

## 1. input()

Accepts data from the keyboard and returns a string.

### Example

```python
name = input("Enter name: ")

print(name)
```

### *Sample Input*

*`Hemanth Akhil`*
 

### *Output*

`Hemanth Akhil`
 

## 2. print()

Displays values on the console.

### Example

```python
message = "Welcome to AlphaKnowledge"

print(message)
```

### Output
Welcome to AlphaKnowledge

## 3. int()

Converts a string into an integer.

### Example

```python
number = int("100")

print(number)
```

### Output
100

## 4. float()

Converts a string into a decimal number.

### Example

```python
value = float("3.14")

print(value)
```

### Output
3.14

## 5. split()

Splits a string into multiple parts.

### Example

```python
data = "Adapa Hemesh Python"

print(data.split())
```

### Output
['Adapa', 'Hemesh', 'Python']

# Advantages of Input and Output Operations

1. Enable interaction between users and programs.
2. Support dynamic execution instead of fixed values.
3. Allow processing of different types of data.
4. Simplify displaying results and messages.
5. Make programs more flexible and user-friendly.

# Limitations

1. `input()` returns values as strings by default, requiring explicit conversion.
2. Invalid input may cause runtime errors.
3. User interaction slows automated execution.
4. Additional validation is needed for robust programs.

# Summary

Input and output operations are fundamental components of Python programming. The `input()` function enables programs to receive information from users, while the `print()` function allows results to be displayed on the console. Through type conversion functions such as `int()` and `float()`, Python supports handling different kinds of data efficiently. Understanding these operations is essential for building interactive and dynamic applications.

