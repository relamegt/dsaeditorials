# Conditional Statements in Python

## Introduction

Conditional statements are used to control the flow of a Python program by executing different blocks of code depending on whether a condition evaluates to `True` or `False`. They enable programs to make decisions and respond differently based on input values and logical conditions.

Python provides several conditional constructs, including `if`, `if-else`, `if-elif-else`, nested conditions, conditional expressions, and the `match-case` statement.

### Key Features

- Allow programs to make decisions.
- Execute code based on logical conditions.
- Support multiple conditions using `elif`.
- Enable nested decision-making.
- Provide concise one-line conditions using conditional expressions.
- Support pattern matching with `match-case`.

# Why Conditional Statements?

Without conditional statements, programs would always execute the same sequence of instructions regardless of circumstances.

### Example Without Conditions

```python
message = "Welcome to AlphaKnowledge"

print(message)
```

### Output
Welcome to AlphaKnowledge

### Limitation

The above program always produces the same output and cannot make decisions based on different situations.

# if Statement

The `if` statement executes a block of code only when the specified condition evaluates to `True`.

### Example

```python
age = 20

if age >= 18:
    print("Eligible to vote.")
```

### Output
Eligible to vote.

### Explanation

Since `age >= 18` is `True`, the statement inside the `if` block is executed.

# Short-Hand if Statement

When only one statement needs to be executed, Python allows writing the `if` statement in a single line.

### Example

```python
marks = 90

if marks >= 35: print("Pass")
```

### Output
Pass

### Explanation

Short-hand `if` improves readability when only one statement is required.

# if-else Statement

The `if-else` statement allows one block to execute when the condition is true and another block when the condition is false.

### Example

```python
temperature = 18

if temperature > 25:
    print("Use Fan")
else:
    print("Weather is Pleasant")
```

### Output
Weather is Pleasant

### Explanation

Since the temperature is not greater than 25, the `else` block executes.

# if-elif-else Statement

The `elif` statement is used to check multiple conditions one after another.

### Example

```python
score = 82

if score >= 90:
    print("Grade A")
elif score >= 75:
    print("Grade B")
elif score >= 50:
    print("Grade C")
else:
    print("Fail")
```

### Output
Grade B

### Explanation

Python checks each condition sequentially and executes the first matching block.

# Nested if Statement

An `if` statement inside another `if` statement is called a nested `if`.

### Example

```python
age = 65
member = True

if age >= 60:
    if member:
        print("30% Discount")
    else:
        print("20% Discount")
else:
    print("No Discount")
```

### Output
30% Discount

### Explanation

The inner condition is evaluated only if the outer condition becomes true.

# Conditional Expression (Ternary Operator)

Python provides a one-line alternative to the `if-else` statement.

### Syntax

```text
value_if_true if condition else value_if_false
```

### Example

```python
age = 17

status = "Adult" if age >= 18 else "Minor"

print(status)
```

### Output
Minor

### Explanation

Since the condition is false, `"Minor"` is assigned to `status`.

# Match-Case Statement

The `match-case` statement performs pattern matching and works similarly to switch statements found in other languages.

### Example

```python
day = 3

match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Invalid Day")
```

### Output
Wednesday

### Explanation

Since the value of `day` is 3, the corresponding case block executes.

# Comparison Operators in Conditions

Conditional statements frequently use comparison operators.

| Operator | Meaning |
| --- | --- |
| == | Equal to |
| != | Not equal to |
| &gt; | Greater than |
| &lt; | Less than |
| &gt;= | Greater than or equal to |
| &lt;= | Less than or equal to |

### Example

```python
a = 10
b = 20

if a < b:
    print("a is smaller")
```

### Output
a is smaller

# Logical Operators in Conditions

Logical operators combine multiple conditions.

| Operator | Meaning |
| --- | --- |
| and | Both conditions must be true |
| or | At least one condition must be true |
| not | Reverses the condition |

### Example

```python
age = 22
citizen = True

if age >= 18 and citizen:
    print("Eligible")
```

### Output
Eligible

# Pass Statement

The `pass` statement acts as a placeholder when no action is required.

### Example

```python
number = 5

if number > 0:
    pass

print("Program continues")
```

### Output
Program continues

### Explanation

The `pass` statement does nothing and prevents syntax errors.

# Advantages of Conditional Statements

1. Allow programs to make decisions dynamically.
2. Improve flexibility and control flow.
3. Support multiple conditions efficiently.
4. Simplify complex decision-making.
5. Make programs interactive and intelligent.
6. Enable concise code using conditional expressions.

# Limitations

1. Deeply nested conditions can reduce readability.
2. Improper conditions may cause logical errors.
3. Large decision structures become difficult to maintain.
4. Complex conditions may reduce code clarity.

# Summary

Conditional statements are essential building blocks of Python programming that enable decision-making and control the execution flow of programs. Python provides various constructs such as `if`, `if-else`, `if-elif-else`, nested conditions, conditional expressions, and `match-case` statements. Understanding these structures helps developers create dynamic, interactive, and efficient applications.

