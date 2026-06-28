# Decision Making in C++

## Introduction

Decision making is a core concept in C++ that allows a program to select different paths of execution based on evaluated conditions. At runtime, the program tests whether a condition is true or false and then executes the corresponding block of code. This mechanism makes programs intelligent — capable of responding differently to different inputs or states rather than following a fixed, unchanging sequence.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1782643730065-ChatGPT_Image_Jun_9%2C_2026%2C_07_09_11_PM.png)

### Key Features

- Executes code selectively based on conditions evaluated at runtime.
- Handles both single conditions and complex multi-branch logic.
- Supports real-world scenarios such as grade classification, eligibility checks, and menu-driven programs.
- Improves program flexibility and control flow significantly.

## Why Decision-Making Statements Are Needed

Without decision-making, every program would execute all statements unconditionally, top to bottom. Conditional statements allow specific blocks to run only when defined conditions are satisfied.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int audience = 100;

    if (audience > 50) {
        cout << "Start the show" << endl;
    }

    return 0;
}
```

### Output
Start the show

Since `audience > 50` is true, the block inside the `if` statement executes. If the value were less than 50, nothing would be printed.

## Types of Decision-Making Statements in C++

1. `if` Statement
2. `if-else` Statement
3. Nested `if-else` Statement
4. `if-else-if` Ladder
5. `switch` Statement
6. Conditional (Ternary) Operator
7. `if` with Initializer (C++17)

## 1. if Statement

The `if` statement evaluates a condition and executes its body only when that condition is true. If the condition is false, the body is skipped entirely.

```Cpp
if (condition) {
    // executes only if condition is true
}
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 20;

    if (age >= 18) {
        cout << "Eligible to vote" << endl;
    }

    return 0;
}
```

### Output
Eligible to vote

The condition `age >= 18` evaluates to true, so the message is printed.

### Single-Statement if (Without Braces)

When the `if` body contains only one statement, the curly braces are optional.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int marks = 85;

    if (marks >= 35)
        cout << "Pass" << endl;

    return 0;
}
```

### Output
Pass

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1782643904866-1781012481470-53f5e2d4-8047-438a-a66b-063bb88d3708.png)

## 

## 2. if-else Statement

The `if-else` statement adds an alternative path. When the condition is true the `if` block runs; when it is false, the `else` block runs. Exactly one of the two blocks always executes.

```Cpp
if (condition) {
    // executes when true
}
else {
    // executes when false
}
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 15;

    if (age >= 18) {
        cout << "Eligible for voting" << endl;
    }
    else {
        cout << "Not eligible for voting" << endl;
    }

    return 0;
}
```

### Output
Not eligible for voting

Since `age < 18`, the condition is false and the `else` block executes.

### Multiple Statements Inside if-else

```Cpp
#include <iostream>
using namespace std;

int main() {
    int percentage = 72;

    if (percentage >= 60) {
        cout << "First Class" << endl;
        cout << "Congratulations" << endl;
    }
    else {
        cout << "Needs Improvement" << endl;
    }

    return 0;
}
```

### Output
First Class
Congratulations

All statements inside a block execute when that block's condition is satisfied.

## 3. Nested if-else Statement

A nested `if-else` places one `if-else` structure inside another. This is useful when a secondary condition only makes sense after a primary condition is already confirmed to be true.

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 65;

    if (age >= 18) {
        if (age >= 60) {
            cout << "Senior Citizen — Eligible for Voting" << endl;
        }
        else {
            cout << "Eligible for Voting" << endl;
        }
    }
    else {
        cout << "Not Eligible for Voting" << endl;
    }

    return 0;
}
```

### Output
Senior Citizen — Eligible for Voting

The outer `if` confirms voting eligibility. Only then does the inner `if` check whether the person qualifies as a senior citizen.

### Nested if-else Inside the else Block

```Cpp
#include <iostream>
using namespace std;

int main() {
    int age = 12;

    if (age >= 18) {
        cout << "Eligible for Voting" << endl;
    }
    else {
        if (age >= 13) {
            cout << "Teenager" << endl;
        }
        else {
            cout << "Child" << endl;
        }
    }

    return 0;
}
```

### Output
Child

Since `age` is below both 18 and 13, the innermost `else` block executes.

## 

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1782643973541-1781012736897-f702f5c8-11bd-455d-9125-4f2b89ba0c0e.png)

## 

## 4. if-else-if Ladder

The `if-else-if` ladder evaluates conditions sequentially from top to bottom. The moment one condition becomes true, its block executes and all remaining conditions are bypassed without being checked.

```Cpp
if (condition1) {
    // block 1
}
else if (condition2) {
    // block 2
}
else if (condition3) {
    // block 3
}
else {
    // default block
}
```

### Grade Classification Example

```Cpp
#include <iostream>
using namespace std;

int main() {
    int marks = 82;

    if (marks >= 90)
        cout << "Grade A+" << endl;
    else if (marks >= 75)
        cout << "Grade A" << endl;
    else if (marks >= 60)
        cout << "Grade B" << endl;
    else if (marks >= 35)
        cout << "Grade C" << endl;
    else
        cout << "Fail" << endl;

    return 0;
}
```

### Output
Grade A

The first condition fails (82 < 90), but the second succeeds (82 >= 75), so "Grade A" is printed and the rest are skipped.

### Finding the Largest of Three Numbers

```Cpp
#include <iostream>
using namespace std;

int main() {
    int a = 25, b = 40, c = 15;

    if (a > b && a > c)
        cout << a << " is largest" << endl;
    else if (b > c)
        cout << b << " is largest" << endl;
    else
        cout << c << " is largest" << endl;

    return 0;
}
```

### Output
40 is largest

## 

## ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1782643973541-1781012736897-f702f5c8-11bd-455d-9125-4f2b89ba0c0e.png)

## 

## 5. switch Statement

The `switch` statement compares a single expression against a series of constant values (cases). When a match is found, the corresponding block executes. It is a cleaner alternative to long `if-else-if` chains when testing the same variable against multiple fixed values.

```Cpp
switch (expression) {
    case constant1:
        // statements
        break;
    case constant2:
        // statements
        break;
    default:
        // statements
}
```

- **`break`** — exits the switch block after a case executes. Without it, execution continues into the next case (fall-through).
- **`default`** — executes when no case matches the expression.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1782644056361-1781012805271-5e2b5985-9164-44e9-b778-e3d17bcc171c.png)

### Day of the Week Example

```Cpp
#include <iostream>
using namespace std;

int main() {
    int day = 3;

    switch (day) {
        case 1: cout << "Monday"    << endl; break;
        case 2: cout << "Tuesday"   << endl; break;
        case 3: cout << "Wednesday" << endl; break;
        case 4: cout << "Thursday"  << endl; break;
        case 5: cout << "Friday"    << endl; break;
        default: cout << "Weekend"  << endl;
    }

    return 0;
}
```

### Output
Wednesday

### Fall-Through Behavior (Without break)

```Cpp
#include <iostream>
using namespace std;

int main() {
    int num = 1;

    switch (num) {
        case 1: cout << "One"   << endl;
        case 2: cout << "Two"   << endl;
        case 3: cout << "Three" << endl;
    }

    return 0;
}
```

### Output
One
Two
Three

When `break` is absent, execution flows through all subsequent cases regardless of whether they match.

### default Block Example

```Cpp
#include <iostream>
using namespace std;

int main() {
    int option = 10;

    switch (option) {
        case 1: cout << "Add"    << endl; break;
        case 2: cout << "Delete" << endl; break;
        default: cout << "Invalid Option" << endl;
    }

    return 0;
}
```

### Output
Invalid Option

## 6. Conditional (Ternary) Operator

The ternary operator `? :` provides a compact single-line alternative to a simple `if-else` statement. It works with three operands: a condition, a value for true, and a value for false.

```Cpp
condition ? expression_if_true : expression_if_false;
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    int marks = 75;

    cout << ((marks >= 35) ? "Pass" : "Fail") << endl;

    int age = 20;
    char eligible = (age >= 18) ? 'Y' : 'N';
    cout << "Eligible: " << eligible << endl;

    return 0;
}
```

### Output
Pass
Eligible: Y

The ternary operator is best suited for simple, single-value decisions. For multi-statement logic, `if-else` is more readable.

## 7. if with Initializer — C++17

Introduced in C++17, the `if` statement can include a variable initialization directly inside its condition. The variable's scope is limited to the `if-else` block, which prevents it from leaking into the surrounding scope.

```Cpp
if (init-statement; condition) {
    // statements
}
```

```Cpp
#include <iostream>
using namespace std;

int main() {
    if (int age = 22; age >= 18) {
        cout << "Eligible to vote. Age: " << age << endl;
    }
    // 'age' is not accessible here

    return 0;
}
```

### Output
Eligible to vote. Age: 22

The variable `age` is initialized to 22 inside the `if` clause. It is evaluated against the condition and is no longer accessible outside the block.

## Difference Between if-else and switch

| Feature | `if-else` | `switch` |
| --- | --- | --- |
| **Condition Type** | Any relational or logical expression | Equality against constant values only |
| **Data Types** | Any valid expression | Integer, character, enum, or string (C++17) |
| **Range Checking** | Supported | Not supported |
| **Fall-through** | Not applicable | Occurs without `break` |
| **Readability** | Better for complex conditions | Better for multiple fixed value checks |

## Advantages

- Enables programs to react intelligently to different inputs and states.
- Reduces unnecessary code execution by running only relevant blocks.
- Simplifies the implementation of real-world logic such as menus, eligibility checks, and classification.
- The ternary operator and C++17 initializer `if` reduce verbosity for simple decisions.

## Limitations

- Deeply nested `if-else` structures reduce code readability (known as "arrow anti-pattern").
- The `switch` statement cannot handle ranges or non-constant expressions.
- Complex ladders are harder to debug and maintain.

> **Note:** Prefer `switch` over `if-else-if` ladders when testing a single variable against many known constant values — it is easier to read and the compiler can optimize it using jump tables. For range-based or logical expression checks, `if-else` is the only applicable option. Always include a `default` case in every `switch` block to handle unexpected values gracefully.

## Summary

Decision-making statements in C++ give programs the ability to choose execution paths at runtime based on evaluated conditions. The `if` statement handles single conditions; `if-else` provides an alternative path when the condition is false; nested `if-else` handles layered conditions; and the `if-else-if` ladder evaluates multiple distinct conditions in order. The `switch` statement offers a structured way to compare a variable against multiple constant values, while the ternary operator compresses simple decisions into a single expression. C++17 further extended `if` to support inline variable initialization with block-scoped lifetime. Mastering these constructs is essential for building interactive, logic-driven C++ programs.




