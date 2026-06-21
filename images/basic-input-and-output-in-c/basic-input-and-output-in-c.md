# Basic Input and Output in C

## Introduction

Input and Output (I/O) operations enable a C program to communicate with users and external devices. Input operations allow programs to receive data during execution, whereas output operations display information on the screen or send data to files and other devices.

The Standard Input/Output library (`stdio.h`) provides several functions for handling input and output. Some functions support formatted data, while others are designed for simple text or character processing.

### Key Features

- Enables interaction between users and programs.
- Supported through the Standard Input/Output library (`stdio.h`).
- Provides formatted and unformatted input/output functions.
- Supports integers, characters, strings, and other data types.
- Allows reading data from keyboards and writing data to screens or files.

# Output Operations in C

Output operations are used to display information on the console or write data to files. The most commonly used output function is `printf()`.

### Features of Output Functions

- Display text and messages.
- Print values stored in variables.
- Support format specifiers for different data types.
- Print expressions and strings.

# Printing Text Using printf()

The following program prints a simple message on the screen.

```c
#include <stdio.h>

int main()
{
    printf("Welcome to AlphaKnowledge");

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The text enclosed within double quotes is called a string. The `printf()` function displays the string exactly as written.

# Printing Variables

Variables can also be displayed using format specifiers.

```c
#include <stdio.h>

int main()
{
    int age = 22;

    printf("%d", age);

    return 0;
}
```

### Output
22

### Explanation

`%d` is a format specifier used for integer values. The value stored inside `age` replaces `%d`.

# Printing Variables Along with Text

Formatted output allows variables and strings to be combined.

```c
#include <stdio.h>

int main()
{
    int age = 22;

    printf("Akash is %d years old", age);

    return 0;
}
```

### Output
Akash is 22 years old

### Explanation

The `printf()` function inserts the value of `age` in place of `%d`.

# Using fputs()

The `fputs()` function writes strings to files, but it can also display text on the console.

```c
#include <stdio.h>

int main()
{
    fputs("Learning C Programming with AlphaKnowledge", stdout);

    return 0;
}
```

### Output
Learning C Programming with AlphaKnowledge

### Explanation

`stdout` represents the standard output device, which is usually the console screen.

# Input Operations in C

Input functions are used to receive data from users during program execution.

### Features of Input Functions

- Read integers, characters, and strings.
- Support formatted input through `scanf()`.
- Provide safer string handling with `fgets()`.
- Allow character-by-character input using `getchar()`.

# Using scanf()

### Syntax

```c
scanf("format_specifier", &variable);
```

The address operator (`&`) is used because `scanf()` stores the entered value in memory.

# Reading an Integer

```c
#include <stdio.h>

int main()
{
    int marks;

    printf("Enter marks: ");

    scanf("%d", &marks);

    printf("Marks = %d", marks);

    return 0;
}
```

### Output
Enter marks: 95
Marks = 95

### Explanation

The `%d` format specifier reads an integer value and stores it in `marks`.

# Reading a Character

```c
#include <stdio.h>

int main()
{
    char grade;

    printf("Enter grade: ");

    scanf("%c", &grade);

    printf("Grade = %c", grade);

    return 0;
}
```

### Output
Enter grade: A
Grade = A

### Explanation

The `%c` format specifier reads a single character.

# Reading a String Using scanf()

```c
#include <stdio.h>

int main()
{
    char name[20];

    printf("Enter your name: ");

    scanf("%s", name);

    printf("Hello %s", name);

    return 0;
}
```

### Output
Enter your name: Mohit
Hello Mohit

### Explanation

`%s` reads characters until a space or newline is encountered. Therefore, it is suitable only for single-word strings.

# Using fgets()

The `fgets()` function reads an entire line, including spaces, and limits the number of characters to prevent buffer overflow.

```c
#include <stdio.h>

int main()
{
    char name[30];

    printf("Enter your full name: ");

    fgets(name, sizeof(name), stdin);

    printf("Welcome %s", name);

    return 0;
}
```

### Output
Enter your full name: Abhiram Gopisetti
Welcome Abhiram Gopisetti

### Explanation

Unlike `scanf("%s")`, `fgets()` can read multiple words and provides better safety.

# Using getchar()

The `getchar()` function reads a single character from the keyboard.

```c
#include <stdio.h>

int main()
{
    char ch;

    printf("Enter a character: ");

    ch = getchar();

    printf("You entered %c", ch);

    return 0;
}
```

### Output
Enter a character: K
You entered K

### Explanation

`getchar()` reads one character and returns it.

# Common Format Specifiers

| Format Specifier | Data Type |
| --- | --- |
| `%d` | Integer |
| `%f` | Float |
| `%lf` | Double |
| `%c` | Character |
| `%s` | String |
| `%u` | Unsigned Integer |
| `%x` | Hexadecimal Integer |
| `%o` | Octal Integer |

# Difference Between printf() and scanf()

| Feature | printf() | scanf() |
| --- | --- | --- |
| Purpose | Displays output | Reads input |
| Direction | Program to user | User to program |
| Return Type | Number of characters printed | Number of values successfully read |
| Format Specifiers | Required | Required |
| Uses Address Operator | No | Yes |

# Difference Between scanf() and fgets()

| Feature | scanf("%s") | fgets() |
| --- | --- | --- |
| Reads Single Word | Yes | Yes |
| Reads Spaces | No | Yes |
| Safer Input | No | Yes |
| Prevents Buffer Overflow | Limited | Better |
| Suitable for Sentences | No | Yes |

# Advantages of Input and Output Functions

1. Enable communication between programs and users.
2. Support various data types.
3. Allow formatted display of information.
4. Simplify data entry and output operations.
5. Provide functions for both character-based and string-based input.

# Limitations

1. Incorrect format specifiers may lead to unexpected results.
2. `scanf("%s")` cannot read strings containing spaces.
3. Buffer overflow can occur if input size is not controlled.
4. Some functions require careful handling of memory addresses.

# Summary

Input and Output operations are essential components of C programming. The Standard Input/Output library provides functions such as `printf()`, `scanf()`, `fputs()`, `fgets()`, and `getchar()` for displaying and reading data. Formatted functions allow handling multiple data types efficiently, while safer functions like `fgets()` help prevent buffer overflow. Understanding these functions is fundamental for building interactive C programs.

