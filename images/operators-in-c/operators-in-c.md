# Operators in C++

### 

Operators are special symbols that instruct the compiler to perform specific operations on one or more operands. They are essential building blocks of C++ programs and are used to perform arithmetic calculations, comparisons, logical evaluations, assignments, and many other tasks.

For example, in the expression `10 + 20`, the symbol `+` is an operator that adds the two operands and produces the result `30`.

The following example demonstrates the use of an arithmetic operator in C++.

```cpp
#include <iostream>
using namespace std;

int main() {

    int total = 15 + 25;

    cout << total;

    return 0;
}
```

### Output
40

### **Types of Operators in C++**

Based on the operations they perform, C++ operators can be broadly classified into the following categories:

| Operator Category | Purpose |
| --- | --- |
| Arithmetic Operators | Perform mathematical calculations such as addition and subtraction |
| Relational Operators | Compare two values and produce a Boolean result |
| Logical Operators | Combine or negate logical expressions |
| Bitwise Operators | Perform operations at the binary bit level |
| Assignment Operators | Assign and update values of variables |
| Conditional (Ternary) Operator | Select a value based on a condition |
| Miscellaneous Operators | Provide special functionalities such as size calculation, type casting, and member access |

### **Arithmetic Operators**

Arithmetic operators are used to perform basic mathematical operations on numeric values. These operators can be applied to integers, floating-point numbers, and other compatible data types.

| Operator | Description |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus (remainder) |
| ++ | Increment |
| -- | Decrement |

The following example demonstrates the use of common arithmetic operators in C++.

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 12, b = 5;

    cout << "Addition: " << a + b << endl;
    cout << "Subtraction: " << a - b << endl;
    cout << "Multiplication: " << a * b << endl;
    cout << "Division: " << a / b << endl;
    cout << "Remainder: " << a % b;

    return 0;
}
```

### Output
Addition: 17
Subtraction: 7
Multiplication: 60
Division: 2
Remainder: 2

### **Important Notes on Arithmetic Operators**

When working with arithmetic operators in C++, it is important to understand a few key concepts:

- The modulus operator (`%`) is primarily used with integer operands and returns the remainder after division.
- Increment (`++`) and decrement (`--`) operators modify the value of a variable by one.
- Arithmetic operators can be used with variables, constants, and expressions.
- Division between two integers produces an integer result, discarding any fractional part.

Based on the number of operands they require, operators can also be categorized as:

- **Unary Operators:** Operate on a single operand (e.g., `++a`, `--b`, `!flag`).
- **Binary Operators:** Operate on two operands (e.g., `a + b`, `x * y`).
- **Ternary Operators:** Operate on three operands (e.g., `condition ? value1 : value2`).

### **Relational Operators**

Relational operators are used to compare two values or expressions. The result of a relational operation is a Boolean value, which is represented as `1` (true) or `0` (false) when displayed.

| Operator | Description |
| --- | --- |
| == | Equal to |
| != | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

The following example demonstrates the use of relational operators in C++.

```cpp
#include <iostream>
using namespace std;

int main() {

    int x = 15, y = 10;

    cout << (x > y) << endl;
    cout << (x == y) << endl;
    cout << (x != y);

    return 0;
}
```

### Output
1
0
1

### **Logical Operators**

Logical operators are used to combine multiple conditions or reverse the result of a condition. They are commonly used in decision-making statements such as `if`, `while`, and `for`.

| Operator | Description |
| --- | --- |
| && | Logical AND |
|  | Logical OR |
| ! | Logical NOT |

The result of a logical operation is either `true` or `false`.

```cpp
#include <iostream>
using namespace std;

int main() {

    bool a = true;
    bool b = false;

    cout << (a && b) << endl;
    cout << (a || b) << endl;
    cout << (!b);

    return 0;
}
```

### Output
0
1
1

### **Bitwise Operators**

Bitwise operators perform operations directly on the binary representation of integer values. They are commonly used in low-level programming, embedded systems, and performance-critical applications.

| Operator | Name |
| --- | --- |
| & | Bitwise AND |
|  | Bitwise OR |
| ^ | Bitwise XOR |
| ~ | Bitwise NOT |
| << | Left Shift |
| >> | Right Shift |

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 6, b = 3;

    cout << (a & b) << endl;
    cout << (a | b) << endl;
    cout << (a ^ b);

    return 0;
}
```

### Output
2
7
5

### **Assignment Operators**

Assignment operators are used to assign values to variables and update existing values. They provide a concise way to perform calculations and assignments in a single statement.

| Operator | Description |
| --- | --- |
| = | Assign |
| += | Add and assign |
| -= | Subtract and assign |
| *= | Multiply and assign |
| /= | Divide and assign |
| %= | Modulus and assign |

```cpp
#include <iostream>
using namespace std;

int main() {

    int value = 10;

    value += 5;

    cout << value;

    return 0;
}
```

### Output
15

### **Ternary (Conditional) Operator**

The conditional operator, also known as the **ternary operator**, is a shorthand alternative to the `if-else` statement. It evaluates a condition and returns one of two values depending on whether the condition is true or false.

**Syntax:**

`condition ? expression1 : expression2;`

- If the condition evaluates to `true`, `expression1` is executed.
- If the condition evaluates to `false`, `expression2` is executed.

The ternary operator requires three operands, which is why it is called a ternary operator.

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 15, b = 20;

    int largest = (a > b) ? a : b;

    cout << "Largest number: " << largest;

    return 0;
}
```

### Output
Largest number: 20

### **Miscellaneous Operators**

Apart from arithmetic, relational, logical, bitwise, assignment, and conditional operators, C++ provides several special-purpose operators that are used for memory management, type conversion, object manipulation, and other advanced operations.

Some commonly used miscellaneous operators are listed below:

| Operator | Purpose |
| --- | --- |
| sizeof | Determines the size of a variable or data type |
| , | Comma operator |
| & | Address-of operator |
| . | Member access operator |
| -> | Pointer member access operator |
| static_cast | Type conversion operator |
| dynamic_cast | Runtime type conversion |
| const_cast | Removes or adds const qualification |
| reinterpret_cast | Low-level type conversion |

These operators are used in specialized programming scenarios and provide additional control over memory, objects, and data types.

**1. `sizeof` Operator**

The `sizeof` operator is a unary operator used to determine the amount of memory occupied by a data type or variable in bytes. It is commonly used when working with memory management and data structures.

**Example:**

`sizeof(int);
sizeof(variable);`

```cpp
#include <iostream>
using namespace std;

int main() {

    cout << sizeof(double);

    return 0;
}
```

### Output
8

**2. Comma Operator (`,`)**

The comma operator evaluates multiple expressions from left to right and returns the value of the last expression. It can also be used to declare multiple variables in a single statement.

**Example:**

`int result = (5, 10, 15);`

Here, the value of `result` becomes `15`.

**3. Address-of Operator (`&`)**

The address-of operator returns the memory address of a variable. It is widely used with pointers and references.

**Example:**

`int num = 10;
cout << &num;`

The output will be the memory address where `num` is stored.

**4. Dot Operator (`.`)**

The dot operator is used to access members (variables or functions) of an object or structure.

**Example:**

`student.name;
car.startEngine();`

It allows direct access to the members of an object.

****5. Arrow Operator** (`->`)**

The arrow operator is used to access members of an object through a pointer. It combines dereferencing and member access into a single operation.

**Example:**

`studentPtr->name;`

This is equivalent to:

`(*studentPtr).name;`

**6. Casting Operators** 

Casting operators are used to convert a value from one data type to another. They are useful when performing operations involving different data types.

**Examples:**

`(float)x

static_cast<float>(x)`

Common C++ casting operators include:

- `static_cast` – General-purpose type conversion.
- `dynamic_cast` – Safe conversion in inheritance hierarchies.
- `const_cast` – Adds or removes `const` qualifiers.
- `reinterpret_cast` – Low-level type conversion between unrelated types.

These operators provide greater control and type safety compared to traditional C-style casting.




