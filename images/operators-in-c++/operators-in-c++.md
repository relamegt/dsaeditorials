# Operators in C++

## Introduction

Operators are special symbols in C++ that perform operations on values, variables, or expressions. They are one of the fundamental building blocks of C++ programming and enable programmers to carry out mathematical calculations, comparisons, logical evaluations, bit-level manipulations, and many other operations.

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

```cpp
#include <iostream>

int main()
{
    int totalMarks = 40 + 50;

    std::cout << totalMarks << std::endl;

    return 0;
}
```

### Output
90

### Explanation

- The `+` operator adds two numbers and stores the result in `totalMarks`.
- Standard output stream `std::cout` displays the value of `totalMarks`.

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

```cpp
#include <iostream>

int main()
{
    int count = 10;

    count++;

    std::cout << count << std::endl;

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

```cpp
#include <iostream>

int main()
{
    int a = 15;
    int b = 5;

    std::cout << (a + b) << std::endl;

    return 0;
}
```

### Output
20

## Ternary Operators

Ternary operators work with three operands.

The conditional operator (`?:`) is the most common ternary operator in C++.

### Example

```cpp
#include <iostream>

int main()
{
    int age = 20;

    int result = (age >= 18) ? 1 : 0;

    std::cout << result << std::endl;

    return 0;
}
```

### Output
1

# Types of Operators in C++

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

```cpp
#include <iostream>

int main()
{
    int a = 25;
    int b = 15;

    std::cout << (a + b) << std::endl;

    return 0;
}
```

### Output
40

## Subtraction Operator

```cpp
#include <iostream>

int main()
{
    int a = 40;
    int b = 18;

    std::cout << (a - b) << std::endl;

    return 0;
}
```

### Output
22

## Multiplication Operator

```cpp
#include <iostream>

int main()
{
    int a = 12;
    int b = 5;

    std::cout << (a * b) << std::endl;

    return 0;
}
```

### Output
60

## Division Operator

```cpp
#include <iostream>

int main()
{
    int a = 20;
    int b = 4;

    std::cout << (a / b) << std::endl;

    return 0;
}
```

### Output
5

## Modulus Operator

The modulus operator returns the remainder after division.

```cpp
#include <iostream>

int main()
{
    int a = 17;
    int b = 5;

    std::cout << (a % b) << std::endl;

    return 0;
}
```

### Output
2

## Increment Operator

The increment operator increases the value of a variable by one.

```cpp
#include <iostream>

int main()
{
    int count = 10;

    count++;

    std::cout << count << std::endl;

    return 0;
}
```

### Output
11

## Decrement Operator

The decrement operator decreases the value of a variable by one.

```cpp
#include <iostream>

int main()
{
    int count = 10;

    count--;

    std::cout << count << std::endl;

    return 0;
}
```

### Output
9

# Relational Operators

Relational operators are used to compare two values. They return either `true` or `false` in C++.

| Operator | Meaning |
| --- | --- |
| &lt; | Less than |
| &gt; | Greater than |
| &lt;= | Less than or equal to |
| &gt;= | Greater than or equal to |
| == | Equal to |
| != | Not equal to |

## Example

```cpp
#include <iostream>

int main()
{
    int marks = 90;
    int passingMarks = 35;

    std::cout << std::boolalpha;
    std::cout << (marks > passingMarks) << std::endl;
    std::cout << (marks == passingMarks) << std::endl;

    return 0;
}
```

### Output
true
false

### Explanation

- `marks > passingMarks` evaluates to true.
- `marks == passingMarks` evaluates to false.

# Logical Operators

Logical operators are used to combine multiple conditions or reverse the result of a condition. They are commonly used in decision-making statements such as `if`, `if-else`, and loops.

The result of a logical expression in C++ is a `bool` value of either `true` or `false`.

| Operator | Description |
| --- | --- |
| && | Logical AND |
|  |  |  | Logical OR |
| ! | Logical NOT |

## Logical AND Operator (&&)

The logical AND operator returns true only when both conditions are true.

### Example

```cpp
#include <iostream>

int main()
{
    int age = 20;
    int marks = 85;

    std::cout << std::boolalpha << (age >= 18 && marks >= 35) << std::endl;

    return 0;
}
```

### Output
true

### Explanation

- Both conditions are true, so the result is `true`.

## Logical OR Operator (||)

The logical OR operator returns true if at least one condition is true.

### Example

```cpp
#include <iostream>

int main()
{
    int age = 16;
    int marks = 90;

    std::cout << std::boolalpha << (age >= 18 || marks >= 35) << std::endl;

    return 0;
}
```

### Output
true

### Explanation

- Since one of the conditions (`marks >= 35`) is true, the entire expression evaluates to `true`.

## Logical NOT Operator (!)

The logical NOT operator reverses the result of a condition.

### Example

```cpp
#include <iostream>

int main()
{
    bool value = true;

    std::cout << std::boolalpha << (!value) << std::endl;

    return 0;
}
```

### Output
false

### Explanation

- Since `value` is `true`, applying `!` reverses it to `false`.

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

```cpp
#include <iostream>

int main()
{
    int a = 12;
    int b = 10;

    std::cout << (a & b) << std::endl;

    return 0;
}
```

### Output
8

## Bitwise OR Operator (|)

The bitwise OR operator returns 1 if at least one corresponding bit is 1.

### Example

```cpp
#include <iostream>

int main()
{
    int a = 12;
    int b = 10;

    std::cout << (a | b) << std::endl;

    return 0;
}
```

### Output
14

## Bitwise XOR Operator (^)

The XOR operator returns 1 only when corresponding bits are different.

### Example

```cpp
#include <iostream>

int main()
{
    int a = 12;
    int b = 10;

    std::cout << (a ^ b) << std::endl;

    return 0;
}
```

### Output
6

## Bitwise Complement Operator (~)

The complement operator reverses all bits.

### Example

```cpp
#include <iostream>

int main()
{
    int num = 10;

    std::cout << (~num) << std::endl;

    return 0;
}
```

### Output
-11

## Left Shift Operator (&lt;&lt;)

The left shift operator shifts bits to the left.

### Example

```cpp
#include <iostream>

int main()
{
    int num = 5;

    std::cout << (num << 2) << std::endl;

    return 0;
}
```

### Output
20

### Explanation

- Shifting left by 2 positions multiplies the number by 4.

## Right Shift Operator (&gt;&gt;)

The right shift operator shifts bits to the right.

### Example

```cpp
#include <iostream>

int main()
{
    int num = 20;

    std::cout << (num >> 2) << std::endl;

    return 0;
}
```

### Output
5

### Explanation

- Shifting right by 2 positions divides the number by 4.

# Assignment Operators

Assignment operators are used to assign values to variables.

## Simple Assignment Operator (=)

### Example

```cpp
#include <iostream>

int main()
{
    int marks;

    marks = 95;

    std::cout << marks << std::endl;

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
|  | = | a = a __SAFE_PIPE_PLACEHOLDER__ b |
| ^= | a = a ^ b |
| &lt;&lt;= | a = a &lt;&lt; b |
| &gt;&gt;= | a = a &gt;&gt; b |

## += Operator

### Example

```cpp
#include <iostream>

int main()
{
    int marks = 80;

    marks += 10;

    std::cout << marks << std::endl;

    return 0;
}
```

### Output
90

## -= Operator

### Example

```cpp
#include <iostream>

int main()
{
    int balance = 100;

    balance -= 20;

    std::cout << balance << std::endl;

    return 0;
}
```

### Output
80

## *= Operator

### Example

```cpp
#include <iostream>

int main()
{
    int value = 10;

    value *= 5;

    std::cout << value << std::endl;

    return 0;
}
```

### Output
50

## /= Operator

### Example

```cpp
#include <iostream>

int main()
{
    int value = 100;

    value /= 4;

    std::cout << value << std::endl;

    return 0;
}
```

### Output
25

## %= Operator

### Example

```cpp
#include <iostream>

int main()
{
    int value = 17;

    value %= 5;

    std::cout << value << std::endl;

    return 0;
}
```

### Output
2

# Special Operators in C++

Apart from arithmetic, relational, logical, bitwise, and assignment operators, C++ provides several special operators that are used for specific purposes such as determining memory size, type conversion, pointer manipulation, and conditional evaluation.

# sizeof Operator

The `sizeof` operator returns the amount of memory occupied by a data type or variable in bytes. It is evaluated at compile time and returns a value of type `size_t`.

### Syntax

```cpp
sizeof(operand)
```

### Example

```cpp
#include <iostream>

int main()
{
    int age = 20;

    std::cout << "Size of age = " << sizeof(age) << " bytes" << std::endl;

    return 0;
}
```

### Output
Size of age = 4 bytes

### Explanation

- The `sizeof` operator calculates the number of bytes required to store the variable `age`.

# Comma Operator (,)

The comma operator evaluates multiple expressions from left to right and returns the value of the last expression.

### Syntax

```cpp
expression1, expression2
```

### Example

```cpp
#include <iostream>

int main()
{
    int value;

    value = (10, 20, 30);

    std::cout << value << std::endl;

    return 0;
}
```

### Output
30

### Explanation

- The expressions are evaluated sequentially, and the value of the final expression is assigned to `value`.

# Conditional Operator (? :)

The conditional operator is a compact alternative to an `if-else` statement.

### Syntax

```cpp
condition ? expression1 : expression2;
```

### Example

```cpp
#include <iostream>

int main()
{
    int marks = 82;

    char result = (marks >= 35) ? 'P' : 'F';

    std::cout << result << std::endl;

    return 0;
}
```

### Output
P

### Explanation

- Since the condition is true, the first expression is executed and `'P'` is assigned to `result`.

# Scope Resolution Operator (::)

The scope resolution operator (`::`) is specific to C++ and is used to access global variables, call static class functions, or specify names within namespaces.

### Example

```cpp
#include <iostream>

int value = 100; // Global variable

int main()
{
    int value = 10; // Local variable

    std::cout << "Local = " << value << std::endl;
    std::cout << "Global = " << ::value << std::endl;

    return 0;
}
```

### Output
Local = 10
Global = 100

# Memory Management Operators (new and delete)

C++ provides `new` and `delete` operators for dynamic memory allocation and deallocation respectively.

### Example

```cpp
#include <iostream>

int main()
{
    // Dynamically allocate memory
    int *ptr = new int(42);

    std::cout << "Value = " << *ptr << std::endl;

    // Deallocate memory
    delete ptr;

    return 0;
}
```

### Output
Value = 42

# Dot Operator (.)

The dot operator is used to access members of a structure or class object.

### Syntax

```cpp
object.member
```

### Example

```cpp
#include <iostream>

struct Student
{
    int rollNo;
};

int main()
{
    Student akash;

    akash.rollNo = 101;

    std::cout << akash.rollNo << std::endl;

    return 0;
}
```

### Output
101

### Explanation

- In C++, declaring a structure variable does not require the `struct` keyword prefix.
- The dot operator accesses the member `rollNo` of the structure variable `akash`.

# Arrow Operator (-&gt;)

The arrow operator is used to access structure or class members through a pointer.

### Syntax

```cpp
pointer -> member
```

### Example

```cpp
#include <iostream>

struct Student
{
    int rollNo;
};

int main()
{
    Student akash = {101};

    Student *ptr = &akash;

    std::cout << ptr->rollNo << std::endl;

    return 0;
}
```

### Output
101

### Explanation

- The arrow operator accesses structure members through a pointer variable.

# Cast Operator (static_cast)

C++ supports standard cast operations. While C-style casting `(type)value` is supported, C++ introduces explicit cast operators such as `static_cast` for safer, clearer conversions.

### Syntax

```cpp
static_cast<new_type>(operand)
```

### Example

```cpp
#include <iostream>

int main()
{
    float marks = 95.75f;

    int result = static_cast<int>(marks);

    std::cout << result << std::endl;

    return 0;
}
```

### Output
95

### Explanation

- The cast operator converts the floating-point value into an integer by discarding the decimal part.

# Address-of Operator (&)

The address-of operator returns the memory address of a variable.

### Example

```cpp
#include <iostream>

int main()
{
    int age = 21;

    std::cout << &age << std::endl;

    return 0;
}
```

### Output
0x7ffd.... (Address may vary)

### Explanation

- The memory address differs from one execution to another and across systems.

# Dereference Operator (*)

The dereference operator accesses the value stored at a memory address.

### Example

```cpp
#include <iostream>

int main()
{
    int age = 21;

    int *ptr = &age;

    std::cout << *ptr << std::endl;

    return 0;
}
```

### Output
21

### Explanation

- `*ptr` retrieves the value stored at the address contained in `ptr`.

# Operator Precedence and Associativity

When multiple operators appear in an expression, precedence determines which operator is evaluated first. Associativity determines the order of evaluation when operators have the same precedence.

## Common Precedence Order

| Operator Category | Operators |
| --- | --- |
| Scope Resolution | `::` |
| Parentheses | () |
| Unary Operators | ++ -- ! ~ |
| Multiplication and Division | * / % |
| Addition and Subtraction | + - |
| Relational Operators | &lt; &lt;= &gt; &gt;= |
| Equality Operators | == != |
| Logical AND | && |
| Logical OR |  |  |  |
| Conditional Operator | ? : |
| Assignment Operators | = += -= *= /= |

### Example

```cpp
#include <iostream>

int main()
{
    int result = 10 + 5 * 2;

    std::cout << result << std::endl;

    return 0;
}
```

### Output
20

### Explanation

- Multiplication has higher precedence than addition, so `5 * 2` is evaluated first.

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

Operators are special symbols used to perform operations on values and variables in C++. They are classified into arithmetic, relational, logical, bitwise, assignment, and special operators. Special operators such as `sizeof`, conditional, cast, address-of, dereference, dot, arrow, scope resolution (`::`), and dynamic memory allocation (`new` and `delete`) operators provide additional functionality for memory handling, type conversion, scope management, and class member access. Understanding operator precedence and associativity is essential for writing correct and efficient C++ programs.




