# Operators

Operators in C++

**By Alpha Knowledge**
**Last Updated: 16 Sep, 2025**

In C++, **operators** are special symbols that help us perform operations on data.
They are used to do **calculations**, **comparisons**, **logical checks**, and **data manipulation**.

Every C++ program uses operators in some form, making them one of the most important concepts to learn.

## Simple Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 10 + 20;
    cout << a;
    return 0;
}
```

### Output

```
30
```

### Explanation

The `+` symbol is an **addition operator**.
It adds `10` and `20`, and the result `30` is stored in variable `a`.

## Types of Operators in C++

C++ operators are mainly divided into **6 categories** based on what they do:

1. Arithmetic Operators
2. Relational Operators
3. Logical Operators
4. Bitwise Operators
5. Assignment Operators
6. Conditional (Ternary) Operator

## 1. Arithmetic Operators

Arithmetic operators are used to perform **mathematical calculations**.

| Operator | Meaning |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Remainder (Modulo) |
| ++ | Increment |
| -- | Decrement |

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 8, b = 3;

    cout << "a + b = " << (a + b) << endl;
    cout << "a - b = " << (a - b) << endl;
    cout << "a * b = " << (a * b) << endl;
    cout << "a / b = " << (a / b) << endl;
    cout << "a % b = " << (a % b) << endl;
    cout << "++a = " << ++a << endl;
    cout << "b-- = " << b-- << endl;

    return 0;
}
```

### Output

```
a + b = 11
a - b = 5
a * b = 24
a / b = 2
a % b = 2
++a = 9
b-- = 3
```

### Important Notes

- % works only with integers
- ++a → increase first, then use
- a++ → use first, then increase

## Operator Based on Operands

- Unary → works on one value (++a)
- Binary → works on two values (a + b)
- Ternary → works on three values (?:)

## 2. Relational Operators

These operators are used to **compare two values**.
The result is either **true (1)** or **false (0)**.

| Operator | Meaning |
| --- | --- |
| == | Equal to |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    cout << (a == b) << endl;
    cout << (a > b) << endl;
    cout << (a >= b) << endl;
    cout << (a < b) << endl;
    cout << (a <= b) << endl;
    cout << (a != b) << endl;

    return 0;
}
```

### Output

```
0
1
1
0
0
1
```

## 3. Logical Operators

Logical operators are used to **combine conditions**.

| Operator | Meaning |
| --- | --- |
| && | Logical AND |
| ` |  |
| ! | Logical NOT |

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    cout << (a && b) << endl;
    cout << (a || b) << endl;
    cout << (!b) << endl;

    return 0;
}
```

### Output

```
1
1
0
```

## 4. Bitwise Operators

Bitwise operators work on **binary bits**.

| Operator | Meaning |
| --- | --- |
| & | AND |
| ` | ` |
| ^ | XOR |
| << | Left shift |
| >> | Right shift |
| ~ | One’s complement |

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    cout << (a & b) << endl;
    cout << (a | b) << endl;
    cout << (a ^ b) << endl;
    cout << (a << 1) << endl;
    cout << (a >> 1) << endl;
    cout << (~a) << endl;

    return 0;
}
```

## 5. Assignment Operators

These operators **assign values** to variables.

| Operator | Meaning |
| --- | --- |
| = | Assign |
| += | Add and assign |
| -= | Subtract and assign |
| *= | Multiply and assign |
| /= | Divide and assign |

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    a += b;
    a -= b;
    a *= b;
    a /= b;

    cout << a;
    return 0;
}
```

## 6. Conditional (Ternary) Operator

The **ternary operator** chooses a value based on a condition.

### Syntax

```
condition ? value_if_true : value_if_false
```

### Example

```
#include <iostream>
using namespace std;

int main() {
    int a = 3, b = 4;

    int result = (a > b) ? a : b;
    cout << result;

    return 0;
}
```

## Other Important Operators

### sizeof

Finds memory size of a variable

```
sizeof(int);
```

### Comma ,

Executes multiple expressions

### Address-of &

Gets memory address of a variable

### Dot .

Access class or structure members

### Arrow ->

Access members using pointer

### Type Casting

```
float(x);
static_cast<float>(x);
```

## Operator Precedence

Precedence decides **which operator runs first**.

Example:

```
3 * 2 + 8
```

Result:

```
(3 * 2) + 8 = 14
```

## Operator Associativity

Associativity decides **direction of evaluation** when precedence is same.

Example:

```
50 / 25 * 2
```

Evaluation:

```
(50 / 25) * 2 = 4
```
