# untitled

Operators in C++ are special symbols that tell the compiler to perform specific operations on values, such as arithmetic, comparison, or logical checks. They form the core of how expressions are written and evaluated in a C++ program.

## Basic idea of operators

An operator works on one or more values (called operands) and produces a result.
For example:

```
#include <iostream>
using namespace std;

int main() {
    int a = 10 + 20;   // + is an operator, 10 and 20 are operands
    cout << a;
    return 0;
}
```

**Output:**

```
30
```

Here `+` adds `10` and `20` and the result `30` is stored in `a`, so the program prints `30`.

Operators can be:

- **Unary**: work on one operand (e.g., `++a`, `!x`)
- **Binary**: work on two operands (e.g., `a + b`, `x == y`)
- **Ternary**: work on three operands (only `?:` in C++)

## Arithmetic operators

Arithmetic operators perform basic mathematical operations.

- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division
- `%` remainder (modulo, only for integers)
- `++` increment (adds 1)
- `--` decrement (subtracts 1)

Example:

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

    cout << "++a = " << ++a << endl;  // a becomes 9, then printed
    cout << "b-- = " << b-- << endl;  // prints 3, then b becomes 2
    return 0;
}
```

**Output:**

```
a + b = 11
a - b = 5
a * b = 24
a / b = 2
a % b = 2
++a = 9
b-- = 3
```

Key points:

- Use `%` only with integer types.
- `++a` (pre‑increment) changes the value first, then uses it.
- `a++` (post‑increment) uses the value first, then changes it.

## Relational operators

Relational operators compare two values and return `true` (non‑zero) or `false` (0).

- `==` equal to
- `>` greater than
- `>=` greater than or equal to
- `<` less than
- `<=` less than or equal to
- `!=` not equal to

Example:

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    cout << "a == b is " << (a == b) << endl;
    cout << "a > b is "  << (a > b)  << endl;
    cout << "a >= b is " << (a >= b) << endl;
    cout << "a < b is "  << (a < b)  << endl;
    cout << "a <= b is " << (a <= b) << endl;
    cout << "a != b is " << (a != b) << endl;

    return 0;
}
```

**Output:**

```
a == b is 0
a > b is 1
a >= b is 1
a < b is 0
a <= b is 0
a != b is 1
```

On most systems this prints `0` for false and `1` for true.

## Logical operators

Logical operators work with boolean expressions and combine or invert conditions.

- `&&` logical AND – true only if both conditions are true
- `||` logical OR – true if at least one condition is true
- `!` logical NOT – flips true to false and false to true

Example:

```
#include <iostream>
using namespace std;

int main() {
    bool x = true;
    bool y = false;

    cout << "x && y = " << (x && y) << endl;  // false
    cout << "x || y = " << (x || y) << endl;  // true
    cout << "!y = "    << (!y)     << endl;   // true

    return 0;
}
```

**Output:**

```
x && y = 0
x || y = 1
!y = 1
```

These are heavily used in `if`, `while`, and other control statements.

## Bitwise operators

Bitwise operators work at the level of individual bits of integer values.

- `&` bitwise AND
- `|` bitwise OR
- `^` bitwise XOR (exclusive OR)
- `<<` left shift
- `>>` right shift
- `~` bitwise NOT (one's complement)

Example:

```
#include <iostream>
using namespace std;

int main() {
    int a = 6; // 6  = 0110 (binary)
    int b = 4; // 4  = 0100 (binary)

    cout << "a & b = "  << (a & b)  << endl;  // 0100 = 4
    cout << "a | b = "  << (a | b)  << endl;  // 0110 = 6
    cout << "a ^ b = "  << (a ^ b)  << endl;  // 0010 = 2
    cout << "a << 1 = " << (a << 1) << endl;  // 1100 = 12
    cout << "a >> 1 = " << (a >> 1) << endl;  // 0011 = 3
    cout << "~a = "     << (~a)     << endl;

    return 0;
}
```

**Output:**

```
a & b = 4
a | b = 6
a ^ b = 2
a << 1 = 12
a >> 1 = 3
~a = -7
```

Bitwise operators are mainly used in low‑level programming, flags, and performance‑sensitive code.

## Assignment operators

Assignment operators store values into variables, sometimes combining assignment with an operation.

- `=` simple assignment
- `+=` add then assign
- `-=` subtract then assign
- `*=` multiply then assign
- `/=` divide then assign
- `%=` modulo then assign

Example:

```
#include <iostream>
using namespace std;

int main() {
    int a = 6, b = 4;

    cout << "a = " << a << endl;

    a += b;  // a = a + b  →  10
    cout << "a += b -> " << a << endl;

    a -= b;  // a = a - b  →  6
    cout << "a -= b -> " << a << endl;

    a *= b;  // a = a * b  →  24
    cout << "a *= b -> " << a << endl;

    a /= b;  // a = a / b  →  6
    cout << "a /= b -> " << a << endl;

    return 0;
}
```

**Output:**

```
a = 6
a += b -> 10
a -= b -> 6
a *= b -> 24
a /= b -> 6
```

These operators make expressions shorter and often clearer.

## Ternary (conditional) operator

The ternary operator chooses one of two values based on a condition.

Syntax:

```
condition ? expression_if_true : expression_if_false;
```

Example:

```
#include <iostream>
using namespace std;

int main() {
    int a = 3, b = 4;

    int result = (a < b) ? b : a;
    cout << "Larger value is " << result << endl;

    return 0;
}
```

**Output:**

```
Larger value is 4
```

If `a < b` is true, `result` becomes `b`; otherwise it becomes `a`.

## Other useful operators

- **`sizeof`** – gives the size of a type or variable in bytes

```
sizeof(int);      // size of int type
sizeof(myVar);    // size of variable myVar
```
- **Comma operator `,`** – evaluates multiple expressions, result is the last one

```
int n = (1 + 2, 5); // 1+2 is evaluated then discarded, n becomes 5
```
- **Address‑of `&`** – gives the memory address of a variable, also used to declare references

```
int x = 10;
int* p = &x;   // p stores address of x
```
- **Dot `.`** – accesses members of an object or struct

```
obj.member;
```
- **Arrow `->`** – accesses members through a pointer to an object

```
ptr->member;
```
- **Casting operators** – convert one type to another

```
int x = 5;
float f1 = (float)x;              // C-style cast
float f2 = static_cast<float>(x); // C++-style cast
```

These operators help with memory access, object handling, and type conversions.

## Precedence and associativity

When an expression contains multiple operators, C++ follows rules to decide which parts run first.

- **Precedence**: which operator is applied first.
For example, in `3 * 2 + 8`, multiplication happens before addition, so it becomes `(3 * 2) + 8 = 14`.
- **Associativity**: direction of evaluation when operators have the same precedence.
Most binary operators (like `+`, `-`, `*`, `/`) associate **left to right**:
`50 / 25 * 2` is evaluated as `(50 / 25) * 2 = 4`.
Some operators (like assignment `=`) associate **right to left**.

Understanding precedence and associativity helps write expressions that behave as intended. When in doubt, use parentheses to make the order of evaluation explicit and your code easier to read.
