### Introduction

C++ is a powerful, high-performance programming language widely used across various domains, including game development, system programming, embedded systems, and more. It is an extension of the C programming language with added features like object-oriented programming (OOP), making it versatile for both low-level and high-level programming tasks.

C++ is a popular choice in technical interviews due to its efficiency and control over system resources, making it a valuable skill for software developers.

### C++ Basic Syntax

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

**Breakdown of the Syntax:**

- `#include <iostream>`: This is a standard library header file that provides input and output functionalities, such as printing to the console (`cout`) and reading from the console (`cin`).
- `int main() { ... }`: The `main()` function is the entry point of every C++ program. Execution begins here.
- `return 0;`: This indicates that the program has executed successfully. A non-zero value typically signifies an error.

**Key Points to Remember:**

- **Semicolon (`;`)**: Every statement in C++ must end with a semicolon.
- **Curly Braces `{}`**: Always ensure that the `main()` function (and other blocks of code) are properly closed with a closing curly brace `}`.
- **endl**: This is used to insert a newline character, moving the cursor to the next line.
- **using namespace std;**: This directive allows you to use standard library functions (like `cout` and `cin`) without prefixing them with `std::`.
- \#include <bits/stdc++.h>: This is a convenience header that includes almost all standard C++ libraries. It's commonly used in competitive programming to save time.


### Comments in C++

**Single-line Comment:**

```cpp
// This is a single-line comment
```

**Multi-line Comment:**

```cpp
/* 
   This is a multi-line comment
   It can span multiple lines
*/
```


### Hello World Program

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

- `cout`: This is used to print output to the console.
- `<<`: The insertion operator is used to send data to the output stream.
- `endl`: Inserts a newline after the output.


### Input and Output in C++

**Basic Input and Output**

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Enter your age: ";
    cin >> age;
    cout << "You are " << age << " years old." << endl;
    return 0;
}
```

- `cin`: Used to take input from the user.
- `>>`: The extraction operator is used to read data from the input stream.

**String Input**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello, " << name << "!" << endl;
    return 0;
}
```

**Sentence Input**

Using `cin`:
`cin` reads only the first word from the input.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your full name: ";
    cin >> name;  // Only reads first word
    cout << "Hello, " << name << "!" << endl;
    return 0;
}
```

Using `getline()`:
To read an entire sentence (including spaces), use `getline()`.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string fullName;
    cout << "Enter your full name: ";
    getline(cin, fullName);
    cout << "Hello, " << fullName << "!" << endl;
    return 0;
}
```

**Example: Addition of Two Numbers**

```cpp
#include <iostream>
using namespace std;

int main() {
    int num1, num2, sum;
    
    cout << "Enter first number: ";
    cin >> num1;
    
    cout << "Enter second number: ";
    cin >> num2;
    
    sum = num1 + num2;
    
    cout << "Sum = " << sum << endl;
    
    return 0;
}
```


## Data Types in C++

C++ supports various data types to store different kinds of data. Here are some commonly used ones:


| Data Type | Syntax Example | Description |
| :-- | :-- | :-- |
| int | `int myVariable = 42;` | Stores integer values. |
| float | `float myFloat = 3.14;` | Stores single-precision floating-point numbers. |
| double | `double myDouble = 3.14159265359;` | Stores double-precision floating-point numbers. |
| char | `char myChar = 'A';` | Stores a single character. |
| std::string | `std::string myString = "Hello";` | Stores a sequence of characters (strings). |
| long | `long al = 1234567890L;` | Stores larger integer values. |
| long long | `long long all = 123456789012345LL;` | Stores very large integer values. |
| bool | `bool booleanValue = true;` | Stores `true` or `false` values. |

**Example: Data Types and Sizes**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // Integer types
    int age = 25;
    long population = 1234567890L;
    long long bigNumber = 123456789012345LL;
    
    // Floating point types
    float price = 19.99f;
    double pi = 3.14159265359;
    
    // Character and string types
    char grade = 'A';
    string name = "John Doe";
    
    // Boolean type
    bool isActive = true;
    
    cout << "Data Types and their sizes:" << endl;
    cout << "int: " << sizeof(int) << " bytes" << endl;
    cout << "float: " << sizeof(float) << " bytes" << endl;
    cout << "double: " << sizeof(double) << " bytes" << endl;
    cout << "char: " << sizeof(char) << " bytes" << endl;
    cout << "bool: " << sizeof(bool) << " bytes" << endl;
    
    return 0;
}
```


## Operators in C++

Operators are symbols that perform operations on variables and values. C++ supports various types of operators, including logical, arithmetic, relational, and assignment operators.

### Logical Operators

Logical operators are used to combine multiple conditions or to negate a condition. They return a boolean value (`true` or `false`).

- **AND (`&&`)**: Returns `true` if both conditions are true.
- **OR (`||`)**: Returns `true` if at least one condition is true.
- **NOT (`!`)**: Reverses the logical state of the condition (true becomes false, and vice versa).

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    bool a = true, b = false;
    
    cout << "Logical Operations:" << endl;
    cout << "a && b: " << (a && b) << endl;  // false
    cout << "a || b: " << (a || b) << endl;  // true
    cout << "!a: " << (!a) << endl;          // false
    cout << "!b: " << (!b) << endl;          // true
    
    return 0;
}
```


### Arithmetic Operators

Arithmetic operators are used to perform mathematical operations like addition, subtraction, multiplication, division, and modulus.

- **Addition (`+`)**: Adds two operands.
- **Subtraction (`-`)**: Subtracts the second operand from the first.
- **Multiplication (`*`)**: Multiplies two operands.
- **Division (`/`)**: Divides the first operand by the second.
- **Modulus (`%`)**: Returns the remainder of division.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 15, b = 4;
    
    cout << "Arithmetic Operations:" << endl;
    cout << "a + b = " << (a + b) << endl;  // 19
    cout << "a - b = " << (a - b) << endl;  // 11
    cout << "a * b = " << (a * b) << endl;  // 60
    cout << "a / b = " << (a / b) << endl;  // 3
    cout << "a % b = " << (a % b) << endl;  // 3
    
    return 0;
}
```


### Relational Operators

Relational operators are used to compare two values or expressions. They return a boolean value (`true` or `false`).

- **Greater than (`>`)**: Returns `true` if the left operand is greater than the right.
- **Less than (`<`)**: Returns `true` if the left operand is less than the right.
- **Equal to (`==`)**: Returns `true` if both operands are equal.
- **Not equal to (`!=`)**: Returns `true` if the operands are not equal.
- **Greater than or equal (`>=`)**: Returns `true` if the left operand is greater than or equal to the right.
- **Less than or equal (`<=`)**: Returns `true` if the left operand is less than or equal to the right.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 20;
    
    cout << "Relational Operations:" << endl;
    cout << "a > b: " << (a > b) << endl;   // false
    cout << "a < b: " << (a < b) << endl;   // true
    cout << "a == b: " << (a == b) << endl; // false
    cout << "a != b: " << (a != b) << endl; // true
    cout << "a >= b: " << (a >= b) << endl; // false
    cout << "a <= b: " << (a <= b) << endl; // true
    
    return 0;
}
```


### Assignment Operators

Assignment operators are used to assign values to variables. They can also perform operations while assigning values.

- **Assignment (`=`)**: Assigns the value of the right operand to the left operand.
- **Add and assign (`+=`)**: Adds the right operand to the left operand and assigns the result to the left operand.
- **Subtract and assign (`-=`)**: Subtracts the right operand from the left operand and assigns the result to the left operand.
- **Multiply and assign (`*=`)**: Multiplies the left operand by the right operand and assigns the result to the left operand.
- **Divide and assign (`/=`)**: Divides the left operand by the right operand and assigns the result to the left operand.
- **Modulus and assign (`%=`)**: Takes the modulus of the left operand by the right operand and assigns the result to the left operand.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10;
    
    cout << "Initial value of a: " << a << endl;
    
    a += 5;  // a = a + 5
    cout << "After a += 5: " << a << endl;  // 15
    
    a -= 3;  // a = a - 3
    cout << "After a -= 3: " << a << endl;  // 12
    
    a *= 2;  // a = a * 2
    cout << "After a *= 2: " << a << endl;  // 24
    
    a /= 4;  // a = a / 4
    cout << "After a /= 4: " << a << endl;  // 6
    
    a %= 4;  // a = a % 4
    cout << "After a %= 4: " << a << endl;  // 2
    
    return 0;
}
```


## Conditional Statements

Control statements in programming are instructions that tell the computer what to do based on certain conditions. They allow the program to make decisions. If a condition is true, the program executes one block of code; if it's false, it executes another block.

Following are some of the decision-making statements in C++:

### if Statement

The `if` statement is used to execute a block of code only if a specified condition is true. If the condition is false, the block of code is skipped.

**Syntax:**

```cpp
if (condition) {
    // code to execute if condition is true
}
```

- The `if` statement checks a condition, which evaluates to a boolean value (`true` or `false`).
- If the condition is `true`, the code inside the `if` block is executed.
- If the condition is `false`, the code inside the `if` block is skipped.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int number = 10;
    
    if (number > 0) {
        cout << "The number is positive." << endl;
    }
    
    if (number % 2 == 0) {
        cout << "The number is even." << endl;
    }
    
    return 0;
}
```


### if-else Statement

The `if-else` statement is used to execute one block of code if the condition is true and another block if the condition is false.

**Syntax:**

```cpp
if (condition) {
    // code to execute if condition is true
} else {
    // code to execute if condition is false
}
```

- If the condition is `true`, the code inside the `if` block is executed.
- If the condition is `false`, the code inside the `else` block is executed.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    cout << "Enter a number: ";
    cin >> number;
    
    if (number % 2 == 0) {
        cout << number << " is even." << endl;
    } else {
        cout << number << " is odd." << endl;
    }
    
    return 0;
}
```


### Nested if-else Statements

A nested `if-else` statement is an `if-else` statement inside another `if-else` statement. It is used when you need to check multiple conditions in a hierarchical manner.

**Syntax:**

```cpp
if (outer_condition) {
    if (inner_condition) {
        // code if both conditions are true
    } else {
        // code if outer is true but inner is false
    }
} else {
    // code if outer condition is false
}
```

- The outer `if-else` statement is evaluated first.
- If the outer condition is `true`, the inner `if-else` statement is evaluated.
- This allows for more complex decision-making.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    bool hasLicense;
    
    cout << "Enter your age: ";
    cin >> age;
    
    if (age >= 18) {
        cout << "Do you have a driving license? (1 for yes, 0 for no): ";
        cin >> hasLicense;
        
        if (hasLicense) {
            cout << "You are eligible to drive!" << endl;
        } else {
            cout << "You need to get a driving license first." << endl;
        }
    } else {
        cout << "You are not old enough to drive." << endl;
    }
    
    return 0;
}
```

**Explanation:**

- The outer `if` checks if the age is 18 or older.
- If the age is 18 or older, the inner `if` checks if the user has a driving license.
- If the user has a license, they are eligible to drive.
- If the user does not have a license, they are prompted to get one.
- If the age is less than 18, the program outputs that the user is not old enough to drive.


### if-else-if Ladder

The `if-else-if` ladder is used when there are multiple conditions to check. The program evaluates each condition sequentially, and when a true condition is found, the corresponding block of code is executed. If none of the conditions are true, the `else` block (if present) is executed.

**Syntax:**

```cpp
if (condition1) {
    // code for condition1
} else if (condition2) {
    // code for condition2
} else if (condition3) {
    // code for condition3
} else {
    // code if none of the conditions are true
}
```

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    cout << "Enter your score: ";
    cin >> score;
    
    if (score >= 90) {
        cout << "Grade: A" << endl;
    } else if (score >= 80) {
        cout << "Grade: B" << endl;
    } else if (score >= 70) {
        cout << "Grade: C" << endl;
    } else if (score >= 60) {
        cout << "Grade: D" << endl;
    } else {
        cout << "Grade: F" << endl;
    }
    
    return 0;
}
```


### Switch Statement

The `switch` statement is used to select one of many code blocks to execute based on the value of a variable. It provides a cleaner alternative to a series of `if-else-if` statements.

**Syntax:**

```cpp
switch (expression) {
    case value1:
        // code for value1
        break;
    case value2:
        // code for value2
        break;
    case value3:
        // code for value3
        break;
    default:
        // code if no case matches
        break;
}
```

- The `expression` is evaluated once, and its value is compared with the values of each `case`.
- If a match is found, the corresponding block of code is executed.
- The `break` statement is used to exit the `switch` block after a match is found.
- The `default` case is optional and is executed if no match is found.

**Example:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    cout << "Select an option (1-4):" << endl;
    cout << "1. Coffee" << endl;
    cout << "2. Tea" << endl;
    cout << "3. Juice" << endl;
    cout << "4. Water" << endl;
    cout << "Enter your choice: ";
    cin >> choice;
    
    switch (choice) {
        case 1:
            cout << "You selected Coffee." << endl;
            break;
        case 2:
            cout << "You selected Tea." << endl;
            break;
        case 3:
            cout << "You selected Juice." << endl;
            break;
        case 4:
            cout << "You selected Water." << endl;
            break;
        default:
            cout << "Invalid choice!" << endl;
            break;
    }
    
    return 0;
}
```

