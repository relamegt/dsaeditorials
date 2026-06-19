# Python Operators

## Introduction

Operators are special symbols used to perform operations on values, variables, and expressions in Python. They provide a convenient way to manipulate data and evaluate conditions. Every operation involves one or more values called operands and an operator that specifies the action to perform.

Python provides different categories of operators to support arithmetic calculations, comparisons, logical decisions, bit-level manipulations, assignment operations, identity checks, and membership testing.

### Key Features

- Perform operations on variables and values.
- Simplify mathematical and logical computations.
- Support decision-making through conditions.
- Enable bit-level operations for low-level programming.
- Improve code readability and reduce complexity.

## Components of an Expression

### Operators

Operators are symbols that perform specific actions.

Examples:

- `+`
- `-`
- `*`
- `/`
- `==`
- `and`
- `in`

### Operands

Operands are the values on which operators act.

Example

```Code
result = 20 + 10
```

Here:

- `+` is the operator.
- `20` and `10` are operands.

# Types of Operators

Python provides several categories of operators:

1. Arithmetic Operators
2. Comparison Operators
3. Logical Operators
4. Bitwise Operators
5. Assignment Operators
6. Identity Operators
7. Membership Operators
8. Conditional (Ternary) Operator

# Arithmetic Operators

Arithmetic operators are used for mathematical calculations.

| Operator | Meaning |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| // | Floor Division |
| % | Modulus |
| ** | Exponentiation |

### Example

```python
a = 18
b = 5

print("Addition:", a + b)
print("Subtraction:", a - b)
print("Multiplication:", a * b)
print("Division:", a / b)
print("Floor Division:", a // b)
print("Remainder:", a % b)
print("Power:", a ** b)
```

### Output
Addition: 23
Subtraction: 13
Multiplication: 90
Division: 3.6
Floor Division: 3
Remainder: 3
Power: 1889568

### Explanation

The division operator (`/`) produces a floating-point result, whereas floor division (`//`) returns only the integer quotient.

## Addition Operator

### Example

```python
course = "Alpha"
name = "Knowledge"

print(course + name)
```

### Output
AlphaKnowledge

### Explanation

The `+` operator can concatenate strings in addition to adding numbers.

## Modulus Operator

The modulus operator returns the remainder after division.

### Example

```python
print(17 % 4)
```

### Output
1

## Exponentiation Operator

Raises a number to a specified power.

### Example

```python
print(3 ** 4)
```

### Output
81

# Comparison Operators

Comparison operators compare two values and return either `True` or `False`.

| Operator | Meaning |
| --- | --- |
| == | Equal To |
| != | Not Equal To |
| &gt; | Greater Than |
| &lt; | Less Than |
| &gt;= | Greater Than or Equal To |
| &lt;= | Less Than or Equal To |

### Example

```python
marks = 85
cutoff = 90

print(marks > cutoff)
print(marks < cutoff)
print(marks == cutoff)
print(marks != cutoff)
print(marks >= cutoff)
print(marks <= cutoff)
```

### Output
False
True
False
True
False
True

### Explanation

Comparison operators are frequently used in decision-making statements such as `if`, `while`, and loops.

# Logical Operators

Logical operators combine multiple conditions.

| Operator | Meaning |
| --- | --- |
| and | Logical AND |
| or | Logical OR |
| not | Logical NOT |

### Example

```python
python_completed = True
dsa_completed = False

print(python_completed and dsa_completed)
print(python_completed or dsa_completed)
print(not python_completed)
```

### Output
False
True
False

### Explanation

- `and` returns True only when both conditions are True.
- `or` returns True if at least one condition is True.
- `not` reverses the Boolean value.

## Operator Precedence in Logical Expressions

Priority order:

1. `not`
2. `and`
3. `or`

### Example

```python
print(True or False and False)
```

### Output
True

### Explanation

The `and` operation executes before the `or` operation.

# Bitwise Operators

Bitwise operators work directly on binary representations of numbers.

| Operator | Meaning |
| --- | --- |
| & | AND |
|  |  | OR |
| ^ | XOR |
| ~ | NOT |
| &lt;&lt; | Left Shift |
| &gt;&gt; | Right Shift |

### Example

```python
a = 12
b = 10

print(a & b)
print(a | b)
print(a ^ b)
print(~a)
print(a << 2)
print(a >> 2)
```

### Output
8
14
6
-13
48
3

### Explanation

Bitwise operators manipulate individual bits and are useful in system programming and optimization.

# Assignment Operators

Assignment operators store values and modify variables efficiently.

| Operator | Meaning |
| --- | --- |
| = | Assignment |
| += | Add and Assign |
| -= | Subtract and Assign |
| *= | Multiply and Assign |
| /= | Divide and Assign |
| %= | Modulus and Assign |

### Example

```python
score = 10

score += 5
print(score)

score *= 2
print(score)

score -= 8
print(score)
```

### Output
15
30
22

### Explanation

Compound assignment operators perform calculations and assignments simultaneously.

# Identity Operators

Identity operators determine whether two variables refer to the same object in memory.

| Operator | Meaning |
| --- | --- |
| is | Objects are identical |
| is not | Objects are different |

### Example

```python
a = [10, 20]
b = a
c = [10, 20]

print(a is b)
print(a is c)
print(a is not c)
```

### Output
True
False
True

### Explanation

Variables `a` and `b` reference the same object, whereas `c` refers to a different object even though it contains the same values.

# Membership Operators

Membership operators determine whether a value exists inside a sequence.

| Operator | Meaning |
| --- | --- |
| in | Present in sequence |
| not in | Not present in sequence |

### Example

```python
courses = [
    "Python",
    "Java",
    "C++"
]

print("Python" in courses)
print("SQL" not in courses)
```

### Output
True
True

### Explanation

Membership operators are commonly used with lists, tuples, sets, strings, and dictionaries.

# Conditional (Ternary) Operator

The conditional operator provides a compact way to write simple if-else expressions.

### Syntax

```text
value_if_true if condition else value_if_false
```

### Example

```python
marks = 92

result = (
    "Pass"
    if marks >= 35
    else "Fail"
)

print(result)
```

### Output
Pass

### Explanation

The expression before `if` executes when the condition is true. Otherwise, the expression after `else` executes.

# Operator Precedence

When an expression contains multiple operators, Python evaluates them according to precedence rules.

### Example

```python
value = 10 + 5 * 2

print(value)
```

### Output
20

### Explanation

Multiplication has higher precedence than addition, so `5 * 2` is evaluated first.

### Common Precedence Order

| Priority | Operators |
| --- | --- |
| Highest | `()` |
|  | `**` |
|  | `*`, `/`, `//`, `%` |
|  | `+`, `-` |
|  | Comparison Operators |
|  | `not` |
|  | `and` |
| Lowest | `or` |

# Associativity of Operators

Associativity determines the order of evaluation when multiple operators have the same precedence.

Most operators follow left-to-right associativity.

### Example

```python
print(100 / 10 * 5)
print(20 - 8 + 3)
```

### Output
50.0
15

### Explanation

The expressions are evaluated from left to right because both operators have equal precedence.

## Right-to-Left Associativity

Exponentiation follows right-to-left associativity.

### Example

```python
print(2 ** 3 ** 2)
```

### Output
512

### Explanation

Python evaluates:

```text
2 ** (3 ** 2)
```

which becomes:

```text
2 ** 9 = 512
```

# Combining Operators

Operators can be combined to create complex expressions.

### Example

```python
age = 22
cgpa = 9.1

eligible = (
    age >= 18 and
    cgpa > 8
)

print(eligible)
```

### Output
True

### Explanation

The comparison operators evaluate conditions, while the logical operator combines them into a single Boolean expression.

# Advantages of Operators

1. Simplify mathematical and logical calculations.
2. Improve code readability.
3. Reduce the amount of code required.
4. Enable efficient bit-level manipulations.
5. Support concise decision-making.
6. Increase program maintainability.

# Common Mistakes

## 1. Confusing `=` with `==`

### Incorrect

```python
# if x = 10:
#     print("Hello")
```

### Correct

```python
x = 10

if x == 10:
    print("Hello")
```

### Output
Hello

## 2. Confusing `is` with `==`

### Example

```python
a = [1, 2]
b = [1, 2]

print(a == b)
print(a is b)
```

### Output
True
False

### Explanation

`==` compares values, whereas `is` compares object identities.

## 3. Ignoring Operator Precedence

### Example

```python
print(5 + 2 * 3)
print((5 + 2) * 3)
```

### Output
11
21

### Explanation

Parentheses alter the evaluation order and improve readability.

# Summary

Operators are fundamental building blocks in Python that enable programs to perform calculations, comparisons, and logical decisions. Python provides arithmetic, comparison, logical, bitwise, assignment, identity, membership, and conditional operators, each serving a specific purpose. Understanding operator precedence and associativity helps developers write accurate and efficient expressions. Proper use of operators improves readability, simplifies complex computations, and forms the basis for decision-making and data manipulation in Python programs.

