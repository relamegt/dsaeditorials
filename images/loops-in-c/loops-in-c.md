# Loops in C

## Introduction

Loops are control structures that allow a block of code to execute repeatedly as long as a specified condition remains true. They help eliminate repetitive code and make programs shorter, more readable, and easier to maintain.

Without loops, programmers would have to write the same statements many times. Using loops, the same task can be performed efficiently with only a few lines of code.

### Key Features

- Repeats a block of code multiple times.
- Reduces code duplication.
- Improves readability and maintainability.
- Supports condition-based execution.
- Useful for processing arrays, patterns, and repetitive calculations.

# Why Use Loops?

Suppose we want to print a message three times.

## Without Using Loops

```c
#include <stdio.h>

int main()
{
    printf("Welcome to AlphaKnowledge\n");
    printf("Welcome to AlphaKnowledge\n");
    printf("Welcome to AlphaKnowledge");

    return 0;
}
```

### Output
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge

Writing the same statement many times becomes difficult when the repetition count increases.

## Using Loops

```c
#include <stdio.h>

int main()
{
    for (int i = 0; i < 3; i++)
    {
        printf("Welcome to AlphaKnowledge\n");
    }

    return 0;
}
```

### Output
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge
Welcome to AlphaKnowledge

### Explanation

The loop executes three times and prints the message during each iteration.

# Types of Loops in C

C provides three looping statements:

1. for Loop
2. while Loop
3. do-while Loop

# for Loop

The `for` loop is an entry-controlled loop. The condition is checked before the execution of the loop body.

## Syntax

```c
for(initialization; condition; update)
{
    // statements
}
```

### Components of for Loop

- **Initialization**: Executes only once.
- **Condition**: Determines whether the loop should continue.
- **Update**: Changes the loop variable after each iteration.
- **Body**: Statements that are repeatedly executed.

## Example

```c
#include <stdio.h>

int main()
{
    for (int i = 1; i <= 5; i++)
    {
        printf("%d ", i);
    }

    return 0;
}
```

### Output
1 2 3 4 5

### Explanation

The loop starts from 1 and continues until the value becomes 5.

# Example: Printing Student Roll Numbers

```c
#include <stdio.h>

int main()
{
    for (int rollNo = 101; rollNo <= 105; rollNo++)
    {
        printf("%d\n", rollNo);
    }

    return 0;
}
```

### Output
101
102
103
104
105

# while Loop

The `while` loop is also an entry-controlled loop. It checks the condition before executing the body.

## Syntax

```c
while(condition)
{
    // statements
}
```

Unlike the `for` loop, initialization and updating are done separately.

## Example

```c
#include <stdio.h>

int main()
{
    int number = 1;

    while (number <= 5)
    {
        printf("%d ", number);

        number++;
    }

    return 0;
}
```

### Output
1 2 3 4 5

### Explanation

The condition is checked before every iteration. As long as it remains true, the loop continues.

# Example: Printing Even Numbers

```c
#include <stdio.h>

int main()
{
    int num = 2;

    while (num <= 10)
    {
        printf("%d ", num);

        num += 2;
    }

    return 0;
}
```

### Output
2 4 6 8 10

# do-while Loop

The `do-while` loop is an exit-controlled loop. Unlike `for` and `while` loops, the condition is checked after executing the loop body. Therefore, the body of a `do-while` loop executes at least once, regardless of whether the condition is true or false.

## Syntax

```c
do
{
    // statements
} while(condition);
```

## Example

```c
#include <stdio.h>

int main()
{
    int number = 1;

    do
    {
        printf("%d ", number);

        number++;
    }
    while (number <= 5);

    return 0;
}
```

### Output
1 2 3 4 5

### Explanation

The loop body executes first and then checks the condition. It continues until the condition becomes false.

# Example: Executing at Least Once

```c
#include <stdio.h>

int main()
{
    int value = 10;

    do
    {
        printf("Hello AlphaKnowledge");
    }
    while (value < 5);

    return 0;
}
```

### Output
Hello AlphaKnowledge

### Explanation

Even though the condition is false, the loop body executes once because the condition is checked after execution.

# Infinite Loops

An infinite loop occurs when the loop condition never becomes false. Such loops continue indefinitely unless they are terminated manually or by using loop control statements.

## Infinite for Loop

```c
#include <stdio.h>

int main()
{
    for (;;)
    {
        printf("Running Forever\n");
    }

    return 0;
}
```

### Output
Running Forever
Running Forever
Running Forever
...

## Infinite while Loop

```c
#include <stdio.h>

int main()
{
    while (1)
    {
        printf("Infinite Loop\n");
    }

    return 0;
}
```

### Output
Infinite Loop
Infinite Loop
Infinite Loop
...

### Explanation

Since the condition always remains true, the loop never terminates.

# Nested Loops

A loop placed inside another loop is called a nested loop. The inner loop executes completely for every iteration of the outer loop.

## Example

```c
#include <stdio.h>

int main()
{
    for (int i = 1; i <= 3; i++)
    {
        for (int j = 1; j <= 2; j++)
        {
            printf("i = %d, j = %d\n", i, j);
        }
    }

    return 0;
}
```

### Output
i = 1, j = 1
i = 1, j = 2
i = 2, j = 1
i = 2, j = 2
i = 3, j = 1
i = 3, j = 2

### Explanation

For each iteration of the outer loop, the inner loop runs completely.

# Loop Control Statements

Loop control statements modify the normal execution flow of loops.

| Statement | Description |
| --- | --- |
| break | Terminates the loop immediately |
| continue | Skips the current iteration |
| goto | Transfers control to a labeled statement |

# break Statement

The `break` statement terminates the loop when a certain condition is met.

## Example

```c
#include <stdio.h>

int main()
{
    for (int i = 1; i <= 5; i++)
    {
        if (i == 4)
        {
            break;
        }

        printf("%d ", i);
    }

    return 0;
}
```

### Output
1 2 3

### Explanation

When `i` becomes 4, the loop terminates immediately.

# continue Statement

The `continue` statement skips the current iteration and moves to the next iteration.

## Example

```c
#include <stdio.h>

int main()
{
    for (int i = 1; i <= 5; i++)
    {
        if (i == 3)
        {
            continue;
        }

        printf("%d ", i);
    }

    return 0;
}
```

### Output
1 2 4 5

### Explanation

When `i` becomes 3, that iteration is skipped.

# goto Statement

The `goto` statement transfers control to a labeled statement.

## Example

```c
#include <stdio.h>

int main()
{
    int i;

    for (i = 1; i <= 5; i++)
    {
        if (i == 4)
        {
            goto end;
        }

        printf("%d ", i);
    }

end:
    printf("\nLoop Terminated");

    return 0;
}
```

### Output
1 2 3
Loop Terminated

### Explanation

When `i` becomes 4, control jumps to the label `end`.

# Difference Between for, while, and do-while Loops

| Feature | for Loop | while Loop | do-while Loop |
| --- | --- | --- | --- |
| Type | Entry-controlled | Entry-controlled | Exit-controlled |
| Condition Check | Before execution | Before execution | After execution |
| Executes At Least Once | No | No | Yes |
| Initialization and Update | Included in syntax | Done separately | Done separately |
| Best Used When | Number of iterations is known | Condition-based repetition | Body must execute at least once |

# Advantages of Loops

1. Reduce code duplication.
2. Improve readability and maintainability.
3. Automate repetitive tasks.
4. Simplify pattern generation and array processing.
5. Reduce program size.
6. Increase development efficiency.

# Limitations of Loops

1. Incorrect conditions may cause infinite loops.
2. Deeply nested loops reduce readability.
3. Excessive iterations can increase execution time.
4. Improper loop control may lead to logical errors.

# Summary

Loops are control structures that execute a block of code repeatedly while a condition remains true. C provides three looping statements: `for`, `while`, and `do-while`. The `for` and `while` loops are entry-controlled, whereas the `do-while` loop is exit-controlled and guarantees at least one execution. Loop control statements such as `break`, `continue`, and `goto` modify the normal flow of loops. Understanding loops is essential for solving repetitive tasks efficiently and writing concise C programs.

