# Header Files in C

## Introduction

A header file in C is a file with the `.h` extension that contains declarations of functions, macros, constants, data types, and other definitions that can be reused across multiple programs using the `#include` preprocessor directive.

Header files help in modular programming and code reusability by providing standard libraries and user-defined functionalities.

## Example

```c
#include <stdio.h>

int main() {

    printf("Hello");

    return 0;
}
```

### Output
Hello

### Explanation

The `stdio.h` header file contains declarations for standard input and output functions such as `printf()` and `scanf()`.

## Why Use Header Files?

- Promote code reuse.
- Reduce code duplication.
- Improve readability.
- Support modular programming.
- Simplify maintenance.
- Provide access to standard library functions.

# Including Header Files

There are two ways to include header files.

## System Header Files

```c
#include <filename.h>
```

These files are searched in the compiler's standard directory.

### Example

```c
#include <stdio.h>
#include <math.h>
```

---

## User-Defined Header Files

```c
#include "filename.h"
```

These files are searched first in the current source file directory.

### Example

```c
#include "myheader.h"
```

## Explanation

The `#include` directive instructs the preprocessor to insert the contents of the specified header file before compilation.

# Types of Header Files in C

There are two types of header files:

1. Standard Header Files
2. User-Defined Header Files

# Standard Header Files

## Introduction

Standard header files are predefined libraries supplied with the C compiler. They follow the ISO C standard and are available on all compilers.

## Common Standard Header Files

| Header File | Purpose |
| --- | --- |
| `<stdio.h>` | Input and output functions |
| `<stdlib.h>` | Memory allocation and utility functions |
| `<string.h>` | String manipulation functions |
| `<math.h>` | Mathematical functions |
| `<ctype.h>` | Character handling functions |
| `<errno.h>` | Error handling |
| `<limits.h>` | Integer limits |
| `<float.h>` | Floating-point limits |
| `<time.h>` | Date and time functions |
| `<signal.h>` | Signal handling |
| `<stdarg.h>` | Variable arguments |
| `<setjmp.h>` | Non-local jumps |
| `<locale.h>` | Localization support |
| `<stddef.h>` | Common type definitions |
| `<assert.h>` | Debugging support |

## Example

```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {

    char str1[20] = "12345";
    char str2[20] = "Hello";
    char str3[20] = "World";

    long result;

    result = pow(9, 3);

    printf("Power = %ld\n", result);

    long num = atol(str1);

    printf("String to Integer = %ld\n", num);

    strcpy(str2, str3);

    printf("%s %s", str2, str3);

    return 0;
}
```

### Output
Power = 729
String to Integer = 12345
World World

### Explanation

- `pow()` comes from `math.h`.
- `atol()` comes from `stdlib.h`.
- `strcpy()` comes from `string.h`.

# User-Defined Header Files

## Introduction

User-defined header files are created by programmers to store custom functions, constants, structures, and macros that can be shared among multiple programs.

These files are generally placed in the same directory as the source file.

## Example

### myheader.h

```c
void displayMessage();
```

### main.c

```c
#include <stdio.h>
#include "myheader.h"

void displayMessage() {

    printf("Welcome to C Programming");
}

int main() {

    displayMessage();

    return 0;
}
```

### Output
Welcome to C Programming

### Explanation

The header file contains the function declaration, while the function definition is implemented in the source file.

---

# Some Non-Standard Header Files

Non-standard header files are compiler-specific and are not part of the ISO C standard.

| Header File | Purpose |
| --- | --- |
| `<conio.h>` | Console functions |
| `<gtk/gtk.h>` | GUI programming |
| `<graphics.h>` | Graphics programming |

## Example

```c
#include <stdio.h>
#include <conio.h>

void displayMessage() {

    printf("Hello C Programming\n");
}

int main() {

    printf("Press any key\n");

    getch();

    displayMessage();

    return 0;
}
```

### Output
Press any key
Hello C Programming

### Explanation

The `getch()` function from `conio.h` waits for a key press before displaying the message.

# Creating Your Own Header File

Suppose we have a function that calculates the square of a number.

### square.h

```c
int square(int num);
```

### square.c

```c
int square(int num) {

    return num * num;
}
```

### main.c

```c
#include <stdio.h>
#include "square.h"

int square(int num);

int main() {

    printf("%d", square(6));

    return 0;
}

int square(int num) {

    return num * num;
}
```

### Output
36

### Explanation

The declaration is stored in `square.h`, making the function reusable across multiple programs.

# Advantages of Header Files

- Promote modular programming.
- Improve readability.
- Reduce code duplication.
- Simplify maintenance.
- Enable code reuse.
- Provide access to standard libraries.

# Limitations

- Excessive inclusion may increase compilation time.
- Circular dependencies can cause errors.
- Non-standard header files are compiler-dependent.
- Incorrect declarations may lead to bugs.

# Summary

Header files in C are `.h` files containing declarations of functions, macros, constants, and data types. They are included using the `#include` directive. Header files are classified into standard and user-defined header files. Standard header files provide built-in library functions, whereas user-defined header files help organize and reuse custom code, making programs modular, readable, and easier to maintain.

