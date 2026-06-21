# C Preprocessors

## Introduction

A preprocessor is a program that processes C source code before compilation. It performs tasks such as macro expansion, file inclusion, and conditional compilation to prepare the source code for the compiler.

The preprocessor is the first stage of the C compilation process.

It supports:

- Macros
- Header file inclusion
- Conditional compilation
- `#undef`
- `#pragma`
- `#error`
- `#line`

For example, if we define:

```c
#define PI 3.14
```

then every occurrence of `PI` in the program is replaced with `3.14` before compilation.

## Features of C Preprocessors

- Executes before compilation.
- Performs text substitution.
- Makes code reusable and modular.
- Supports conditional compilation.
- Allows compiler-specific instructions.
- Improves code readability and maintainability.

# Types of Preprocessor Directives

C preprocessor directives are commonly divided into four categories:

1. Macros
2. File Inclusion
3. Conditional Compilation
4. Other Directives

---

# Macros

## Introduction

Macros are symbolic names that replace values or expressions before compilation.

The `#define` directive creates a macro and `#undef` removes it.

## Syntax

```c
#define token replacement_text

#undef token
```

## Example: Defining a Macro

```c
#include <stdio.h>

#define LIMIT 5

int main() {

    for (int i = 0; i < LIMIT; i++) {

        printf("%d\n", i);
    }

    return 0;
}
```

### Output
0
1
2
3
4

### Explanation

Before compilation, every occurrence of `LIMIT` is replaced with `5`.

---

## Removing a Macro using #undef

```c
#include <stdio.h>

#define LIMIT 5

#undef LIMIT

int main() {

    printf("%d", LIMIT);

    return 0;
}
```

### Output
error: 'LIMIT' undeclared

### Explanation

Since `LIMIT` has been undefined, the preprocessor no longer replaces it, causing a compilation error.

---

# Predefined Macros

C provides some predefined macros:

| Macro | Description |
| --- | --- |
| `__FILE__` | Current filename |
| `__LINE__` | Current line number |
| `__DATE__` | Compilation date |
| `__TIME__` | Compilation time |

## Example

```c
#include <stdio.h>

int main() {

    printf("File : %s\n", __FILE__);
    printf("Line : %d\n", __LINE__);
    printf("Date : %s\n", __DATE__);
    printf("Time : %s\n", __TIME__);

    return 0;
}
```

### Output
File : main.c
Line : 7
Date : Jun 21 2026
Time : 12:15:32

### Explanation

These predefined macros provide useful information about the compilation environment.

---

# Macros with Arguments

## Introduction

Function-like macros accept parameters and expand them during preprocessing.

## Syntax

```c
#define macro_name(parameter) replacement
```

## Example

```c
#include <stdio.h>

#define AREA(length, breadth) ((length) * (breadth))

int main() {

    int length = 10;
    int breadth = 6;

    printf("Area = %d", AREA(length, breadth));

    return 0;
}
```

### Output
Area = 60

### Explanation

The preprocessor replaces:

```c
AREA(length, breadth)
```

with:

```c
((length) * (breadth))
```

---

# File Inclusion

## Introduction

The `#include` directive includes declarations and definitions from external files.

It promotes modular programming and code reuse.

## Syntax

```c
#include <filename>

#include "filename"
```

### `< >`

Searches standard system directories.

### `" "`

Searches the current directory first and then system directories.

## Example

```c
#include <stdio.h>

int main() {

    printf("Hello World");

    return 0;
}
```

### Output
Hello World

### Explanation

The statement:

```c
#include <stdio.h>
```

includes standard input-output functions such as `printf()`.

---

# Conditional Compilation

## Introduction

Conditional compilation allows specific sections of code to be compiled only when certain conditions are satisfied.

It is useful for:

- Debugging
- Platform-specific code
- Optional features

## Directives Used

- `#if`
- `#ifdef`
- `#ifndef`
- `#elif`
- `#else`
- `#endif`

## Example

```c
#include <stdio.h>

#define PI 3.14159

int main() {

#ifdef PI

    printf("PI is defined\n");

#elif defined(SQUARE)

    printf("Square is defined\n");

#else

#error "Neither PI nor SQUARE is defined"

#endif

#ifndef SQUARE

    printf("Square is not defined");

#else

    printf("Square is defined");

#endif

    return 0;
}
```

### Output
PI is defined
Square is not defined

### Explanation

Since `PI` is defined, the first block executes. Because `SQUARE` is undefined, the second condition prints "Square is not defined".

---

# Other Preprocessor Directives

## #pragma

### Introduction

The `#pragma` directive provides compiler-specific instructions.

Common uses include:

- Warning control
- Memory alignment
- Optimization

## Example

```c
#pragma once
```

### Explanation

It prevents multiple inclusions of the same header file.

---

## #error

### Introduction

The `#error` directive generates a compilation error with a custom message.

## Syntax

```c
#error "Error message"
```

## Example

```c
#if !defined(MAX)

#error "MAX is not defined"

#endif
```

### Output
error: MAX is not defined

### Explanation

Compilation stops when the condition becomes true.

---

## #line

### Introduction

The `#line` directive changes the line number and optionally the filename reported by the compiler.

## Syntax

```c
#line line_number "filename"
```

## Example

```c
#include <stdio.h>

#line 100 "sample.c"

int main() {

    printf("%d", __LINE__);

    return 0;
}
```

### Output
100

### Explanation

The compiler treats the next line as line number 100.

---

# Advantages of Preprocessors

- Improve code readability.
- Reduce code duplication.
- Enable modular programming.
- Support conditional compilation.
- Increase portability.
- Provide compiler-specific controls.

# Limitations

- Errors after macro expansion can be difficult to debug.
- Excessive macro usage reduces readability.
- Macros do not perform type checking.
- Compiler-specific directives may reduce portability.

# Summary

C preprocessors process source code before compilation. They perform tasks such as macro expansion, header file inclusion, conditional compilation, and compiler-specific operations. The most common directives are `#define`, `#include`, `#ifdef`, `#ifndef`, `#pragma`, `#error`, and `#line`. Preprocessors improve code reusability and maintainability and form the first stage of the C compilation process.

