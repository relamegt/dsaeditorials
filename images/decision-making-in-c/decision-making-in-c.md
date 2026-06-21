# Decision Making in C

## Introduction

Decision making is an important concept in C programming that allows a program to choose different paths of execution based on certain conditions. These conditions are evaluated at runtime, and depending on whether they are true or false, specific blocks of code are executed.

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

```c
#include <stdio.h>

int main()
{
    int audience = 100;

    if (audience > 50)
    {
        printf("Start the show");
    }

    return 0;
}
```

### Output
Start the show

### Explanation

Since the number of people is greater than 50, the condition becomes true and the statement inside the `if` block gets executed.

# Types of Decision-Making Statements in C

C provides the following decision-making statements:

1. if Statement
2. if-else Statement
3. Nested if-else Statement
4. if-else-if Ladder
5. switch Statement
6. Conditional Operator

# if Statement

The `if` statement is the simplest decision-making statement in C. It executes a block of code only when a specified condition evaluates to true.

## Syntax

```c
if(condition)
{
    // statements
}
```

## Example

```c
#include <stdio.h>

int main()
{
    int age = 20;

    if (age >= 18)
    {
        printf("Akash is eligible to vote");
    }

    return 0;
}
```

### Output
Akash is eligible to vote

### Explanation

The condition `age >= 18` evaluates to true, so the statements inside the `if` block are executed.

## if Statement Without Braces

If only one statement exists inside the body, braces are optional.

### Example

```c
#include <stdio.h>

int main()
{
    int marks = 85;

    if (marks >= 35)
        printf("Pass");

    return 0;
}
```

### Output
Pass

# if-else Statement

The `if-else` statement provides an alternative block of code that executes when the condition becomes false.

## Syntax

```c
if(condition)
{
    // true block
}
else
{
    // false block
}
```

## Example

```c
#include <stdio.h>

int main()
{
    int age = 15;

    if (age >= 18)
    {
        printf("Eligible for voting");
    }
    else
    {
        printf("Not eligible for voting");
    }

    return 0;
}
```

### Output
Not eligible for voting

### Explanation

Since the condition is false, the statements inside the `else` block are executed.

# Multiple Statements Inside if-else

```c
#include <stdio.h>

int main()
{
    int percentage = 72;

    if (percentage >= 60)
    {
        printf("First Class\n");
        printf("Congratulations");
    }
    else
    {
        printf("Needs Improvement");
    }

    return 0;
}
```

### Output
First Class
Congratulations

### Explanation

Since the percentage is greater than 60, both statements inside the `if` block are executed.

# Nested if-else Statement

A nested `if-else` statement is an `if` statement placed inside another `if` or `else` block. It is useful when multiple conditions need to be checked sequentially.

## Syntax

```c
if(condition1)
{
    if(condition2)
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

```c
#include <stdio.h>

int main()
{
    int age = 65;

    if (age >= 18)
    {
        if (age >= 60)
        {
            printf("Senior Citizen Eligible for Voting");
        }
        else
        {
            printf("Eligible for Voting");
        }
    }
    else
    {
        printf("Not Eligible for Voting");
    }

    return 0;
}
```

### Output
Senior Citizen Eligible for Voting

### Explanation

The outer condition checks whether the person is eligible to vote. Since the age is greater than 18, the inner condition checks whether the person is a senior citizen.

## Example with Nested if-else Inside else Block

```c
#include <stdio.h>

int main()
{
    int age = 12;

    if (age >= 18)
    {
        printf("Eligible for Voting");
    }
    else
    {
        if (age >= 13)
        {
            printf("Teenager");
        }
        else
        {
            printf("Child");
        }
    }

    return 0;
}
```

### Output
Child

### Explanation

Since the age is less than 18 and also less than 13, the final else block gets executed.

# if-else-if Ladder

The `if-else-if` ladder is used when multiple conditions need to be checked. Conditions are evaluated from top to bottom. As soon as one condition becomes true, the corresponding block executes and the remaining conditions are skipped.

## Syntax

```c
if(condition1)
{
    // statements
}
else if(condition2)
{
    // statements
}
else if(condition3)
{
    // statements
}
else
{
    // statements
}
```

## Example

```c
#include <stdio.h>

int main()
{
    int marks = 82;

    if (marks >= 90)
    {
        printf("Grade A+");
    }
    else if (marks >= 75)
    {
        printf("Grade A");
    }
    else if (marks >= 60)
    {
        printf("Grade B");
    }
    else if (marks >= 35)
    {
        printf("Grade C");
    }
    else
    {
        printf("Fail");
    }

    return 0;
}
```

### Output
Grade A

### Explanation

The first condition is false, but the second condition is true, so the corresponding block is executed and the remaining conditions are ignored.

# Example: Finding Largest of Three Numbers

```c
#include <stdio.h>

int main()
{
    int a = 25, b = 40, c = 15;

    if (a > b && a > c)
    {
        printf("%d is largest", a);
    }
    else if (b > c)
    {
        printf("%d is largest", b);
    }
    else
    {
        printf("%d is largest", c);
    }

    return 0;
}
```

### Output
40 is largest

### Explanation

The program compares all three numbers and prints the largest value.

# Example: Checking Grade of a Student

```c
#include <stdio.h>

int main()
{
    int marks = 58;

    if (marks >= 90)
    {
        printf("Outstanding");
    }
    else if (marks >= 75)
    {
        printf("Excellent");
    }
    else if (marks >= 50)
    {
        printf("Good");
    }
    else
    {
        printf("Needs Improvement");
    }

    return 0;
}
```

### Output
Good

### Explanation

Since the marks are greater than or equal to 50 but less than 75, the third condition becomes true.

# switch Statement

The `switch` statement is a multi-way decision-making statement that allows a program to select one block of code from several alternatives based on the value of an expression.

It is often used as an alternative to long `if-else-if` ladders when comparing the same variable with multiple constant values.

## Syntax

```c
switch(expression)
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

```c
#include <stdio.h>

int main()
{
    int day = 3;

    switch (day)
    {
        case 1:
            printf("Monday");
            break;

        case 2:
            printf("Tuesday");
            break;

        case 3:
            printf("Wednesday");
            break;

        default:
            printf("Invalid Day");
    }

    return 0;
}
```

### Output
Wednesday

### Explanation

Since the value of `day` is 3, the third case is executed.

# Example Without break

```c
#include <stdio.h>

int main()
{
    int num = 1;

    switch (num)
    {
        case 1:
            printf("One\n");

        case 2:
            printf("Two\n");

        case 3:
            printf("Three");
    }

    return 0;
}
```

### Output
One
Two
Three

### Explanation

Since there is no `break` statement, execution continues into the subsequent cases. This behavior is known as **fall-through**.

# default Statement

The `default` block executes when none of the cases match.

## Example

```c
#include <stdio.h>

int main()
{
    int option = 10;

    switch (option)
    {
        case 1:
            printf("Add");
            break;

        case 2:
            printf("Delete");
            break;

        default:
            printf("Invalid Option");
    }

    return 0;
}
```

### Output
Invalid Option

### Explanation

No case matches the value 10, so the default block is executed.

# Conditional Operator (? :)

The conditional operator is also known as the **ternary operator** because it works with three operands.

It provides a compact alternative to an `if-else` statement.

## Syntax

```c
condition ? expression1 : expression2;
```

If the condition is true, `expression1` is executed; otherwise, `expression2` is executed.

## Example

```c
#include <stdio.h>

int main()
{
    int age = 20;

    char result = (age >= 18) ? 'Y' : 'N';

    printf("%c", result);

    return 0;
}
```

### Output
Y

### Explanation

Since the condition is true, `'Y'` is assigned to `result`.

# Example Using Ternary Operator

```c
#include <stdio.h>

int main()
{
    int marks = 75;

    printf("%s",
           (marks >= 35) ? "Pass" : "Fail");

    return 0;
}
```

### Output
Pass

### Explanation

The condition evaluates to true, so "Pass" is printed.

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

Decision-making statements allow C programs to execute different blocks of code based on conditions. The `if`, `if-else`, nested `if-else`, and `if-else-if` ladder are useful for evaluating one or more conditions. The `switch` statement provides an efficient alternative when multiple fixed values are involved, while the conditional operator offers a concise way to perform simple decisions. Understanding these constructs is essential for building interactive and logical C programs.

