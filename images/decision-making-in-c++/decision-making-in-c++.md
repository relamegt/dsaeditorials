# Decision Making in C++

## Introduction

Decision making is an important concept in C++ programming that allows a program to choose different paths of execution based on certain conditions. These conditions are evaluated at runtime, and depending on whether they are true or false, specific blocks of code are executed.

Decision-making statements make programs interactive and intelligent by enabling them to perform different actions under different situations.

### Key Features

- Executes code based on conditions.
- Supports single and multiple conditions.
- Helps implement real-world logic.
- Improves flexibility and control flow.
- Provides different conditional statements for various scenarios.

# Why Use Decision-Making Statements?

Decision-making statements help programs decide which block of code should be executed depending on the result of a condition.

## Example

```cpp
#include <iostream>

int main()
{
    int audience = 100;

    if (audience > 50)
    {
        std::cout << "Start the show" << std::endl;
    }

    return 0;
}
```

### Output
Start the show

### Explanation

- Since the number of people is greater than 50, the condition becomes true and the statement inside the `if` block gets executed.

# Types of Decision-Making Statements in C++

C++ provides the following decision-making statements:

1. if Statement
2. if-else Statement
3. Nested if-else Statement
4. if-else-if Ladder
5. switch Statement
6. Conditional Operator
7. if with Initializer (C++17)

# if Statement

The `if` statement is the simplest decision-making statement in C++. It executes a block of code only when a specified condition evaluates to true.

## Syntax

```cpp
if (condition)
{
    // statements
}
```

## Example

```cpp
#include <iostream>

int main()
{
    int age = 20;

    if (age >= 18)
    {
        std::cout << "Abhiram is eligible to vote" << std::endl;
    }

    return 0;
}
```

### Output
Abhiram is eligible to vote

### Explanation

- The condition `age >= 18` evaluates to true, so the statements inside the `if` block are executed.

## if Statement Without Braces

If only one statement exists inside the body, braces are optional.

### Example

```cpp
#include <iostream>

int main()
{
    int marks = 85;

    if (marks >= 35)
        std::cout << "Pass" << std::endl;

    return 0;
}
```

### Output
Pass

# if-else Statement

The `if-else` statement provides an alternative block of code that executes when the condition becomes false.

## Syntax

```cpp
if (condition)
{
    // true block
}
else
{
    // false block
}
```

## Example

```cpp
#include <iostream>

int main()
{
    int age = 15;

    if (age >= 18)
    {
        std::cout << "Eligible for voting" << std::endl;
    }
    else
    {
        std::cout << "Not eligible for voting" << std::endl;
    }

    return 0;
}
```

### Output
Not eligible for voting

### Explanation

- Since the condition is false, the statements inside the `else` block are executed.

# Multiple Statements Inside if-else

```cpp
#include <iostream>

int main()
{
    int percentage = 72;

    if (percentage >= 60)
    {
        std::cout << "First Class" << std::endl;
        std::cout << "Congratulations" << std::endl;
    }
    else
    {
        std::cout << "Needs Improvement" << std::endl;
    }

    return 0;
}
```

### Output
First Class
Congratulations

### Explanation

- Since the percentage is greater than 60, both statements inside the `if` block are executed.

# Nested if-else Statement

A nested `if-else` statement is an `if` statement placed inside another `if` or `else` block. It is useful when multiple conditions need to be checked sequentially.

## Syntax

```cpp
if (condition1)
{
    if (condition2)
    {
        // statements
    }
    else
    {
        // statements
    }
}
else
{
    // statements
}
```

## Example

```cpp
#include <iostream>

int main()
{
    int age = 65;

    if (age >= 18)
    {
        if (age >= 60)
        {
            std::cout << "Senior Citizen Eligible for Voting" << std::endl;
        }
        else
        {
            std::cout << "Eligible for Voting" << std::endl;
        }
    }
    else
    {
        std::cout << "Not Eligible for Voting" << std::endl;
    }

    return 0;
}
```

### Output
Senior Citizen Eligible for Voting

### Explanation

- The outer condition checks whether the person is eligible to vote. Since the age is greater than 18, the inner condition checks whether the person is a senior citizen.

## Example with Nested if-else Inside else Block

```cpp
#include <iostream>

int main()
{
    int age = 12;

    if (age >= 18)
    {
        std::cout << "Eligible for Voting" << std::endl;
    }
    else
    {
        if (age >= 13)
        {
            std::cout << "Teenager" << std::endl;
        }
        else
        {
            std::cout << "Child" << std::endl;
        }
    }

    return 0;
}
```

### Output
Child

### Explanation

- Since the age is less than 18 and also less than 13, the final else block gets executed.

# if-else-if Ladder

The `if-else-if` ladder is used when multiple conditions need to be checked. Conditions are evaluated from top to bottom. As soon as one condition becomes true, the corresponding block executes and the remaining conditions are skipped.

## Syntax

```cpp
if (condition1)
{
    // statements
}
else if (condition2)
{
    // statements
}
else if (condition3)
{
    // statements
}
else
{
    // statements
}
```

## Example

```cpp
#include <iostream>

int main()
{
    int marks = 82;

    if (marks >= 90)
    {
        std::cout << "Grade A+" << std::endl;
    }
    else if (marks >= 75)
    {
        std::cout << "Grade A" << std::endl;
    }
    else if (marks >= 60)
    {
        std::cout << "Grade B" << std::endl;
    }
    else if (marks >= 35)
    {
        std::cout << "Grade C" << std::endl;
    }
    else
    {
        std::cout << "Fail" << std::endl;
    }

    return 0;
}
```

### Output
Grade A

### Explanation

- The first condition is false, but the second condition is true, so the corresponding block is executed and the remaining conditions are ignored.

## Example: Finding Largest of Three Numbers

```cpp
#include <iostream>

int main()
{
    int a = 25, b = 40, c = 15;

    if (a > b && a > c)
    {
        std::cout << a << " is largest" << std::endl;
    }
    else if (b > c)
    {
        std::cout << b << " is largest" << std::endl;
    }
    else
    {
        std::cout << c << " is largest" << std::endl;
    }

    return 0;
}
```

### Output
40 is largest

### Explanation

- The program compares all three numbers and prints the largest value.

## Example: Checking Grade of a Student

```cpp
#include <iostream>

int main()
{
    int marks = 58;

    if (marks >= 90)
    {
        std::cout << "Outstanding" << std::endl;
    }
    else if (marks >= 75)
    {
        std::cout << "Excellent" << std::endl;
    }
    else if (marks >= 50)
    {
        std::cout << "Good" << std::endl;
    }
    else
    {
        std::cout << "Needs Improvement" << std::endl;
    }

    return 0;
}
```

### Output
Good

### Explanation

- Since the marks are greater than or equal to 50 but less than 75, the third condition becomes true.

# switch Statement

The `switch` statement is a multi-way decision-making statement that allows a program to select one block of code from several alternatives based on the value of an expression.

It is often used as an alternative to long `if-else-if` ladders when comparing the same variable with multiple constant values.

## Syntax

```cpp
switch (expression)
{
    case constant1:
        // statements
        break;

    case constant2:
        // statements
        break;

    ...

    default:
        // statements
}
```

### Components of switch Statement

- **Expression**: The value that is evaluated.
- **case**: Represents possible values of the expression.
- **break**: Terminates the current case and exits the switch block.
- **default**: Executes when none of the cases match.

## Example

```cpp
#include <iostream>

int main()
{
    int day = 3;

    switch (day)
    {
        case 1:
            std::cout << "Monday" << std::endl;
            break;

        case 2:
            std::cout << "Tuesday" << std::endl;
            break;

        case 3:
            std::cout << "Wednesday" << std::endl;
            break;

        default:
            std::cout << "Invalid Day" << std::endl;
    }

    return 0;
}
```

### Output
Wednesday

### Explanation

- Since the value of `day` is 3, the third case is executed.

## Example Without break

```cpp
#include <iostream>

int main()
{
    int num = 1;

    switch (num)
    {
        case 1:
            std::cout << "One" << std::endl;

        case 2:
            std::cout << "Two" << std::endl;

        case 3:
            std::cout << "Three" << std::endl;
    }

    return 0;
}
```

### Output
One
Two
Three

### Explanation

- Since there is no `break` statement, execution continues into the subsequent cases. This behavior is known as **fall-through**.

## default Statement

The `default` block executes when none of the cases match.

### Example

```cpp
#include <iostream>

int main()
{
    int option = 10;

    switch (option)
    {
        case 1:
            std::cout << "Add" << std::endl;
            break;

        case 2:
            std::cout << "Delete" << std::endl;
            break;

        default:
            std::cout << "Invalid Option" << std::endl;
    }

    return 0;
}
```

### Output
Invalid Option

### Explanation

- No case matches the value 10, so the default block is executed.

# Conditional Operator (? :)

The conditional operator is also known as the **ternary operator** because it works with three operands.

It provides a compact alternative to an `if-else` statement.

## Syntax

```cpp
condition ? expression1 : expression2;
```

If the condition is true, `expression1` is executed; otherwise, `expression2` is executed.

## Example

```cpp
#include <iostream>

int main()
{
    int age = 20;

    char result = (age >= 18) ? 'Y' : 'N';

    std::cout << result << std::endl;

    return 0;
}
```

### Output
Y

### Explanation

- Since the condition is true, `'Y'` is assigned to `result`.

## Example Using Ternary Operator

```cpp
#include <iostream>

int main()
{
    int marks = 75;

    std::cout << ((marks >= 35) ? "Pass" : "Fail") << std::endl;

    return 0;
}
```

### Output
Pass

### Explanation

- The condition evaluates to true, so "Pass" is printed.

# C++17 if with Initializer

C++17 introduced the ability to initialize variables directly inside the condition block of `if` and `switch` statements. The initialized variable is scoped only within that statement block, avoiding namespace pollution.

## Syntax

```cpp
if (init-statement; condition)
{
    // statements
}
```

## Example

```cpp
#include <iostream>

int main()
{
    if (int age = 22; age >= 18)
    {
        std::cout << "Eligible to vote with age: " << age << std::endl;
    }

    return 0;
}
```

### Output
Eligible to vote with age: 22

### Explanation

- The variable `age` is initialized to `22` and evaluated. Since it is greater than or equal to `18`, the statement executes.
- The variable `age` is not accessible outside of the `if-else` block.

# Difference Between if-else and switch

| Feature | if-else | switch |
| --- | --- | --- |
| Conditions | Supports relational and logical expressions | Supports equality checks |
| Data Types | Any valid expression | Integer, character, enum |
| Readability | Better for complex conditions | Better for multiple fixed values |
| Execution Speed | Slightly slower | Usually faster |
| Range Checking | Supported | Not supported |

# Advantages of Decision-Making Statements

1. Enable programs to make logical decisions.
2. Improve flexibility and control flow.
3. Support execution of different blocks based on conditions.
4. Reduce unnecessary code execution.
5. Help solve real-world problems effectively.
6. Improve readability and maintainability.

# Limitations

1. Deep nesting can reduce readability.
2. Complex conditions may become difficult to maintain.
3. Excessive use of nested `if-else` statements can increase program complexity.
4. The `switch` statement supports only specific data types.

# Summary

Decision-making statements allow C++ programs to execute different blocks of code based on conditions. The `if`, `if-else`, nested `if-else`, and `if-else-if` ladder are useful for evaluating one or more conditions, and C++17 expands this via `if` statements with local initializers. The `switch` statement provides an efficient alternative when multiple fixed values are involved, while the conditional operator offers a concise way to perform simple decisions. Understanding these constructs is essential for building interactive and logical C++ programs.




