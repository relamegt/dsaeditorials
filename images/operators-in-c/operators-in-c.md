# Operators in C

## Introduction

Operators are special symbols in C that perform operations on values, variables, or expressions. They are one of the fundamental building blocks of C programming and enable programmers to carry out mathematical calculations, comparisons, logical evaluations, bit-level manipulations, and many other operations.

The values or variables on which operators act are called **operands**. Depending on the number of operands involved, operators can be classified into unary, binary, and ternary operators.

### Key Features

- Perform operations on values and variables.
- Simplify arithmetic and logical calculations.
- Support comparison and decision-making.
- Provide bit-level manipulation capabilities.
- Allow assigning and modifying values efficiently.
- Include unary, binary, and ternary operators.

# Why Use Operators?

Operators help programmers perform computations and manipulate data easily. Without operators, writing expressions and processing data would be difficult and inefficient.

## Example

```c
#include <stdio.h>

int main()
{
    int totalMarks = 40 + 50;

    printf("%d", totalMarks);

    return 0;
}
```

### Output
90

### Explanation

The `+` operator adds two numbers and stores the result in `totalMarks`.

# Classification Based on Number of Operands

Operators can be classified according to the number of operands they require.

## Unary Operators

Unary operators work with a single operand.

### Examples

- Increment (`++`)
- Decrement (`--`)
- Unary Plus (`+`)
- Unary Minus (`-`)
- Logical NOT (`!`)
- Bitwise Complement (`~`)

### Example

```c
#include <stdio.h>

int main()
{
    int count = 10;

    count++;

    printf("%d", count);

    return 0;
}
```

### Output
11

## Binary Operators

Binary operators require two operands.

### Examples

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)
- Modulus (`%`)
- Relational operators
- Logical operators

### Example

```c
#include <stdio.h>

int main()
{
    int a = 15;
    int b = 5;

    printf("%d", a + b);

    return 0;
}
```

### Output
20

## Ternary Operators

Ternary operators work with three operands.

The conditional operator (`?:`) is the only ternary operator in C.

### Example

```c
#include <stdio.h>

int main()
{
    int age = 20;

    int result = (age >= 18) ? 1 : 0;

    printf("%d", result);

    return 0;
}
```

### Output
1

# Types of Operators in C

Based on functionality, operators are broadly classified into:

1. Arithmetic Operators
2. Relational Operators
3. Logical Operators
4. Bitwise Operators
5. Assignment Operators
6. Special Operators

# Arithmetic Operators

Arithmetic operators are used to perform mathematical calculations.

| Operator | Description |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| ++ | Increment |
| -- | Decrement |

## Addition Operator

```c
#include <stdio.h>

int main()
{
    int a = 25;
    int b = 15;

    printf("%d", a + b);

    return 0;
}
```

### Output
40

## Subtraction Operator

```c
#include <stdio.h>

int main()
{
    int a = 40;
    int b = 18;

    printf("%d", a - b);

    return 0;
}
```

### Output
22

## Multiplication Operator

```c
#include <stdio.h>

int main()
{
    int a = 12;
    int b = 5;

    printf("%d", a * b);

    return 0;
}
```

### Output
60

## Division Operator

```c
#include <stdio.h>

int main()
{
    int a = 20;
    int b = 4;

    printf("%d", a / b);

    return 0;
}
```

### Output
5

## Modulus Operator

The modulus operator returns the remainder after division.

```c
#include <stdio.h>

int main()
{
    int a = 17;
    int b = 5;

    printf("%d", a % b);

    return 0;
}
```

### Output
2

## Increment Operator

The increment operator increases the value of a variable by one.

```c
#include <stdio.h>

int main()
{
    int count = 10;

    count++;

    printf("%d", count);

    return 0;
}
```

### Output
11

## Decrement Operator

The decrement operator decreases the value of a variable by one.

```c
#include <stdio.h>

int main()
{
    int count = 10;

    count--;

    printf("%d", count);

    return 0;
}
```

### Output
9

# Relational Operators

Relational operators are used to compare two values. They return either `1` (true) or `0` (false).

| Operator | Meaning |
| --- | --- |
| &lt; | Less than |
| &gt; | Greater than |
| &lt;= | Less than or equal to |
| &gt;= | Greater than or equal to |
| == | Equal to |
| != | Not equal to |

## Example

```c
#include <stdio.h>

int main()
{
    int marks = 90;
    int passingMarks = 35;

    printf("%d\n", marks > passingMarks);
    printf("%d", marks == passingMarks);

    return 0;
}
```

### Output
1
0

### Explanation

- `marks > passingMarks` evaluates to true.
- `marks == passingMarks` evaluates to false.

# Logical Operators

Logical operators are used to combine multiple conditions or reverse the result of a condition. They are commonly used in decision-making statements such as `if`, `if-else`, and loops.

The result of a logical expression is either `1` (true) or `0` (false).

| Operator | Description |
| --- | --- |
| && | Logical AND |
| `__SAFE_PIPE_PLACEHOLDER____SAFE_PIPE_PLACEHOLDER__` | Logical OR |
| ! | Logical NOT |

## Logical AND Operator (&&)

The logical AND operator returns true only when both conditions are true.

### Example

```c
#include <stdio.h>

int main()
{
    int age = 20;
    int marks = 85;

    printf("%d", age >= 18 && marks >= 35);

    return 0;
}
```

### Output
1

### Explanation

Both conditions are true, so the result is `1`.

## Logical OR Operator (||)

The logical OR operator returns true if at least one condition is true.

### Example

```c
#include <stdio.h>

int main()
{
    int age = 16;
    int marks = 90;

    printf("%d", age >= 18 || marks >= 35);

    return 0;
}
```

### Output
1

### Explanation

Since one of the conditions is true, the entire expression evaluates to true.

## Logical NOT Operator (!)

The logical NOT operator reverses the result of a condition.

### Example

```c
#include <stdio.h>

int main()
{
    int value = 10;

    printf("%d", !value);

    return 0;
}
```

### Output
0

### Explanation

Since `value` is non-zero (true), applying `!` changes it to false (`0`).

# Bitwise Operators

Bitwise operators perform operations directly on individual bits of numbers.

| Operator | Description |
| --- | --- |
| & | Bitwise AND |
|  |  | Bitwise OR |
| ^ | Bitwise XOR |
| ~ | Bitwise Complement |
| &lt;&lt; | Left Shift |
| &gt;&gt; | Right Shift |

## Bitwise AND Operator (&)

The bitwise AND operator compares corresponding bits and returns 1 only when both bits are 1.

### Example

```c
#include <stdio.h>

int main()
{
    int a = 12;
    int b = 10;

    printf("%d", a & b);

    return 0;
}
```

### Output
8

## Bitwise OR Operator (|)

The bitwise OR operator returns 1 if at least one corresponding bit is 1.

### Example

```c
#include <stdio.h>

int main()
{
    int a = 12;
    int b = 10;

    printf("%d", a | b);

    return 0;
}
```

### Output
14

## Bitwise XOR Operator (^)

The XOR operator returns 1 only when corresponding bits are different.

### Example

```c
#include <stdio.h>

int main()
{
    int a = 12;
    int b = 10;

    printf("%d", a ^ b);

    return 0;
}
```

### Output
6

## Bitwise Complement Operator (~)

The complement operator reverses all bits.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 10;

    printf("%d", ~num);

    return 0;
}
```

### Output
-11

## Left Shift Operator (&lt;&lt;)

The left shift operator shifts bits to the left.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 5;

    printf("%d", num << 2);

    return 0;
}
```

### Output
20

### Explanation

Shifting left by 2 positions multiplies the number by 4.

## Right Shift Operator (&gt;&gt;)

The right shift operator shifts bits to the right.

### Example

```c
#include <stdio.h>

int main()
{
    int num = 20;

    printf("%d", num >> 2);

    return 0;
}
```

### Output
5

### Explanation

Shifting right by 2 positions divides the number by 4.

# Assignment Operators

Assignment operators are used to assign values to variables.

## Simple Assignment Operator (=)

### Example

```c
#include <stdio.h>

int main()
{
    int marks;

    marks = 95;

    printf("%d", marks);

    return 0;
}
```

### Output
95

# Compound Assignment Operators

Compound assignment operators combine arithmetic and assignment operations.

| Operator | Equivalent Expression |
| --- | --- |
| += | a = a + b |
| -= | a = a - b |
| *= | a = a * b |
| /= | a = a / b |
| %= | a = a % b |
| &= | a = a & b |
| `__SAFE_PIPE_PLACEHOLDER__=` | a = a | b |
| ^= | a = a ^ b |
| &lt;&lt;= | a = a &lt;&lt; b |
| &gt;&gt;= | a = a &gt;&gt; b |

## += Operator

### Example

```c
#include <stdio.h>

int main()
{
    int marks = 80;

    marks += 10;

    printf("%d", marks);

    return 0;
}
```

### Output
90

## -= Operator

### Example

```c
#include <stdio.h>

int main()
{
    int balance = 100;

    balance -= 20;

    printf("%d", balance);

    return 0;
}
```

### Output
80

## *= Operator

### Example

```c
#include <stdio.h>

int main()
{
    int value = 10;

    value *= 5;

    printf("%d", value);

    return 0;
}
```

### Output
50

## /= Operator

### Example

```c
#include <stdio.h>

int main()
{
    int value = 100;

    value /= 4;

    printf("%d", value);

    return 0;
}
```

### Output
25

## %= Operator

### Example

```c
#include <stdio.h>

int main()
{
    int value = 17;

    value %= 5;

    printf("%d", value);

    return 0;
}
```

### Output
2

# Special Operators in C

Apart from arithmetic, relational, logical, bitwise, and assignment operators, C provides several special operators that are used for specific purposes such as determining memory size, type conversion, pointer manipulation, and conditional evaluation.

# sizeof Operator

The `sizeof` operator returns the amount of memory occupied by a data type or variable in bytes. It is evaluated at compile time and returns a value of type `size_t`.

### Syntax

```c
sizeof(operand)
```

### Example

```c
#include <stdio.h>

int main()
{
    int age = 20;

    printf("Size of age = %zu bytes", sizeof(age));

    return 0;
}
```

### Output
Size of age = 4 bytes

### Explanation

The `sizeof` operator calculates the number of bytes required to store the variable `age`.

# Comma Operator (,)

The comma operator evaluates multiple expressions from left to right and returns the value of the last expression.

### Syntax

```c
expression1, expression2
```

### Example

```c
#include <stdio.h>

int main()
{
    int value;

    value = (10, 20, 30);

    printf("%d", value);

    return 0;
}
```

### Output
30

### Explanation

The expressions are evaluated sequentially, and the value of the final expression is assigned to `value`.

# Conditional Operator (? :)

The conditional operator is the only ternary operator in C. It works as a compact alternative to an `if-else` statement.

### Syntax

```c
condition ? expression1 : expression2;
```

### Example

```c
#include <stdio.h>

int main()
{
    int marks = 82;

    char result = (marks >= 35) ? 'P' : 'F';

    printf("%c", result);

    return 0;
}
```

### Output
P

### Explanation

Since the condition is true, the first expression is executed and `'P'` is assigned to `result`.

# Dot Operator (.)

The dot operator is used to access members of a structure or union object.

### Syntax

```c
structure_variable.member
```

### Example

```c
#include <stdio.h>

struct Student
{
    int rollNo;
};

int main()
{
    struct Student akash;

    akash.rollNo = 101;

    printf("%d", akash.rollNo);

    return 0;
}
```

### Output
101

### Explanation

The dot operator accesses the member `rollNo` of the structure variable `akash`.

# Arrow Operator (-&gt;)

The arrow operator is used to access structure members through a pointer.

### Syntax

```c
pointer -> member
```

### Example

```c
#include <stdio.h>

struct Student
{
    int rollNo;
};

int main()
{
    struct Student akash = {101};

    struct Student *ptr = &akash;

    printf("%d", ptr->rollNo);

    return 0;
}
```

### Output
101

### Explanation

The arrow operator accesses structure members through a pointer variable.

# Cast Operator

The cast operator converts one data type into another.

### Syntax

```c
(new_type) operand
```

### Example

```c
#include <stdio.h>

int main()
{
    float marks = 95.75;

    int result = (int) marks;

    printf("%d", result);

    return 0;
}
```

### Output
95

### Explanation

The cast operator converts the floating-point value into an integer by discarding the decimal part.

# Address-of Operator (&)

The address-of operator returns the memory address of a variable.

### Example

```c
#include <stdio.h>

int main()
{
    int age = 21;

    printf("%p", &age);

    return 0;
}
```

### Output
0x7ffd.... (Address may vary)

### Explanation

The memory address differs from one execution to another and across systems.

# Dereference Operator (*)

The dereference operator accesses the value stored at a memory address.

### Example

```c
#include <stdio.h>

int main()
{
    int age = 21;

    int *ptr = &age;

    printf("%d", *ptr);

    return 0;
}
```

### Output
21

### Explanation

`*ptr` retrieves the value stored at the address contained in `ptr`.

# Operator Precedence and Associativity

When multiple operators appear in an expression, precedence determines which operator is evaluated first. Associativity determines the order of evaluation when operators have the same precedence.

## Common Precedence Order

| Operator Category | Operators |
| --- | --- |
| Parentheses | () |
| Unary Operators | ++ -- ! ~ |
| Multiplication and Division | * / % |
| Addition and Subtraction | + - |
| Relational Operators | &lt; &lt;= &gt; &gt;= |
| Equality Operators | == != |
| Logical AND | && |
| Logical OR | `__SAFE_PIPE_PLACEHOLDER____SAFE_PIPE_PLACEHOLDER__` |
| Conditional Operator | ? : |
| Assignment Operators | = += -= *= /= |

### Example

```c
#include <stdio.h>

int main()
{
    int result = 10 + 5 * 2;

    printf("%d", result);

    return 0;
}
```

### Output
20

### Explanation

Multiplication has higher precedence than addition, so `5 * 2` is evaluated first.

# Advantages of Operators

1. Simplify mathematical and logical computations.
2. Reduce the amount of code required.
3. Improve program readability.
4. Support bit-level operations for efficient processing.
5. Provide concise ways to perform assignments and conditions.
6. Enable pointer and memory manipulation.

# Limitations of Operators

1. Incorrect precedence may produce unexpected results.
2. Complex expressions can reduce readability.
3. Misuse of bitwise operators may lead to logical errors.
4. Excessive use of nested conditional operators decreases maintainability.

# Summary

Operators are special symbols used to perform operations on values and variables in C. They are classified into arithmetic, relational, logical, bitwise, assignment, and special operators. Special operators such as `sizeof`, conditional, cast, address-of, dereference, dot, and arrow operators provide additional functionality for memory handling, type conversion, and structure access. Understanding operator precedence and associativity is essential for writing correct and efficient C programs.

