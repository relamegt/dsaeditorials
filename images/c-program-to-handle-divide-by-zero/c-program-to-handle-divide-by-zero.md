# C Program to Handle Divide by Zero

## Introduction

Division by zero is one of the most common runtime errors in programming. In C, there is no built-in exception handling mechanism like `try-catch` found in Java or C++. Therefore, programmers must explicitly handle divide-by-zero situations to prevent undefined behavior and program crashes.

There are two common methods to handle divide-by-zero errors:

- Manually checking the divisor before division.
- Using signal handling with `SIGFPE`.

## Why Handle Divide by Zero?

Handling division by zero helps to:

- Prevent unexpected program crashes.
- Avoid undefined behavior.
- Improve program reliability.
- Display meaningful error messages.
- Allow recovery from runtime exceptions.

# Method 1: Manually Checking Before Division

## Introduction

The simplest and most commonly used approach is to check whether the divisor is zero before performing division.

## Example

```c
#include <stdio.h>

int main() {

    float num = 20;
    float den = 0;
    float result;

    if (den == 0) {

        printf("Error: Division by zero is not allowed");
    }
    else {

        result = num / den;

        printf("Result = %.2f", result);
    }

    return 0;
}
```

### Output
Error: Division by zero is not allowed

### Explanation

Before performing division, the program checks whether the denominator is zero. If it is zero, an error message is displayed instead of executing the division.

## Example with Integer Division

```c
#include <stdio.h>

int main() {

    int a = 40;
    int b = 5;

    if (b == 0) {

        printf("Division by zero is not possible");
    }
    else {

        printf("Quotient = %d", a / b);
    }

    return 0;
}
```

### Output
Quotient = 8

### Explanation

Since the divisor is not zero, the division operation is performed normally.

# Method 2: Using Signal Handling

## Introduction

C provides signal handling facilities through the `<signal.h>` header file. Floating-point exceptions are represented by the signal `SIGFPE`.

When a divide-by-zero error occurs, a signal handler function can catch the exception and prevent the program from terminating abruptly.

## Example

```c
#include <stdio.h>
#include <signal.h>
#include <stdlib.h>

void divideByZeroHandler(int sig) {

    printf("Error: Division by zero detected\n");

    exit(1);
}

int main() {

    signal(SIGFPE, divideByZeroHandler);

    int a = 10;
    int b = 0;

    int result = a / b;

    printf("%d", result);

    return 0;
}
```

### Output
Error: Division by zero detected

### Explanation

The signal handler is associated with `SIGFPE`. When division by zero occurs, the handler function executes and displays an error message before terminating the program.

# Using setjmp() and longjmp()

## Introduction

`setjmp()` and `longjmp()` allow the program to jump back to a previously saved execution state after an exception occurs.

## Example

```c
#include <stdio.h>
#include <setjmp.h>

jmp_buf recovery;

int main() {

    if (setjmp(recovery) != 0) {

        printf("Recovered from division by zero");

        return 0;
    }

    int x = 20;
    int y = 0;

    if (y == 0) {

        longjmp(recovery, 1);
    }

    printf("%d", x / y);

    return 0;
}
```

### Output
Recovered from division by zero

### Explanation

`setjmp()` saves the execution state. When division by zero is detected, `longjmp()` transfers control back to the saved location.

# Using Functions for Safe Division

## Example

```c
#include <stdio.h>

float divide(float a, float b) {

    if (b == 0) {

        printf("Error: Division by zero\n");

        return 0;
    }

    return a / b;
}

int main() {

    float answer = divide(50, 0);

    printf("Result = %.2f", answer);

    return 0;
}
```

### Output
Error: Division by zero
Result = 0.00

### Explanation

The division logic is separated into a function. This improves code reusability and keeps error handling centralized.

# Practical Example

Suppose Akash Dangudubiyyapu develops a student grading system. The percentage calculation formula is:

```Code
Percentage = Obtained Marks / Total Marks × 100
```

If total marks accidentally become zero, the program should first verify the denominator before division. This prevents runtime errors and ensures reliable calculations for students such as Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil.

# Advantages

1. Prevents undefined behavior.
2. Avoids program crashes.
3. Provides meaningful error messages.
4. Improves program reliability.
5. Allows recovery from exceptions using signals.

# Limitations

1. C does not provide built-in exception handling.
2. Signal handling is platform-dependent.
3. Improper signal handling may increase complexity.
4. Recovery mechanisms require additional code.
5. Manual checking is necessary before every division.

# Best Practice

The recommended and simplest approach is to check the divisor using an `if` statement before performing division:

```c
if (divisor == 0) {

    printf("Division by zero is not allowed");
}
else {

    result = dividend / divisor;
}
```

# Summary

Divide-by-zero errors are common runtime exceptions in C. Since C lacks built-in exception handling, these errors are usually handled by manually checking the divisor before division. Advanced techniques such as signal handling using `SIGFPE` and recovery mechanisms using `setjmp()` and `longjmp()` can also be used. Manual checking remains the safest and most widely recommended method.

