# Macros in C

## Introduction

A macro in C is a symbolic name or constant that represents a value, expression, or block of code. Macros are defined using the `#define` preprocessor directive, and before compilation, the preprocessor replaces the macro name with its corresponding definition.

Macros are processed during the preprocessing stage and do not consume memory like variables.

## Syntax

```c
#define MACRO_NAME value
```

where:

- `MACRO_NAME` is the symbolic name.
- `value` is the expression or code that replaces the macro.

## Example

```c
#include <stdio.h>

#define LIMIT 5

int main() {

    printf("LIMIT = %d", LIMIT);

    return 0;
}
```

### Output
LIMIT = 5

### Explanation

The preprocessor replaces every occurrence of `LIMIT` with `5` before compilation.

## Features of Macros

- Processed before compilation.
- Improve code readability.
- Avoid repeated constants.
- Do not consume memory.
- Execute faster because no function call overhead exists.
- Can represent values, expressions, or code fragments.

# Types of Macros in C

There are four common types of macros:

1. Object-Like Macros
2. Chain Macros
3. Multi-Line Macros
4. Function-Like Macros

---

# 1. Object-Like Macros

## Introduction

Object-like macros replace a macro name with a constant value or expression. They are mainly used for defining constants.

## Example

```c
#include <stdio.h>

#define DATE 31

int main() {

    printf("Last Date = %d", DATE);

    return 0;
}
```

### Output
Last Date = 31

### Explanation

Whenever the compiler encounters `DATE`, the preprocessor substitutes it with `31`.

## Advantages

- Easy to define constants.
- Improves readability.
- Eliminates magic numbers.

---

# 2. Chain Macros

## Introduction

Chain macros involve multiple macros referring to one another. The parent macro is expanded first, followed by the child macro.

## Example

```c
#include <stdio.h>

#define TOTAL STUDENTS
#define STUDENTS 120

int main() {

    printf("Students = %d", TOTAL);

    return 0;
}
```

### Output
Students = 120

### Explanation

First:

```c
TOTAL
```

becomes:

```c
STUDENTS
```

Then:

```c
STUDENTS
```

is replaced with:

```c
120
```

Hence, the output becomes 120.

## Advantages

- Makes macro definitions reusable.
- Simplifies maintenance.
- Helps organize related constants.

---

# 3. Multi-Line Macros

## Introduction

Multi-line macros span multiple lines and are created using the backslash (`\`) character.

They are useful when several statements need to be grouped together.

## Example

```c
#include <stdio.h>

#define ELEMENTS 10, \
                 20, \
                 30

int main() {

    int arr[] = { ELEMENTS };

    for (int i = 0; i < 3; i++) {

        printf("%d ", arr[i]);
    }

    return 0;
}
```

### Output
10 20 30

### Explanation

The preprocessor expands:

```c
ELEMENTS
```

into:

```c
10, 20, 30
```

which initializes the array.

## Advantages

- Improves readability.
- Useful for long definitions.
- Helps group multiple statements.

---

# 4. Function-Like Macros

## Introduction

Function-like macros accept parameters and behave similarly to functions. They are expanded during preprocessing and avoid function call overhead.

## Syntax

```c
#define MACRO_NAME(parameter) expression
```

## Example

```c
#include <stdio.h>

#define MIN(a, b) (((a) < (b)) ? (a) : (b))

int main() {

    int num1 = 18;
    int num2 = 76;

    printf("Minimum = %d", MIN(num1, num2));

    return 0;
}
```

### Output
Minimum = 18

### Explanation

The expression:

```c
MIN(num1, num2)
```

expands to:

```c
(((num1) < (num2)) ? (num1) : (num2))
```

which returns the smaller value.

## Advantages

- Faster than functions.
- Eliminates function call overhead.
- Reusable expressions.
- Makes code concise.

---

# Comparison of Macro Types

| Macro Type | Purpose | Example |
| --- | --- | --- |
| Object-Like Macro | Constants or values | `#define PI 3.14` |
| Chain Macro | Macro expansion through another macro | `#define A B` |
| Multi-Line Macro | Multiple-line definitions | `#define DATA 1,\ 2,\ 3` |
| Function-Like Macro | Parameterized expressions | `#define MAX(a,b)` |

# Advantages of Macros

- Improve code readability.
- Increase reusability.
- Reduce code duplication.
- Faster execution due to no function calls.
- Useful for symbolic constants.
- Simplify maintenance.

# Limitations of Macros

- No type checking.
- Difficult to debug after expansion.
- Complex macros reduce readability.
- May produce unexpected results if parentheses are omitted.

# Summary

Macros are preprocessor directives defined using `#define` that replace values or expressions before compilation. They improve readability and eliminate repetitive code. The four common types of macros are object-like macros, chain macros, multi-line macros, and function-like macros. Although macros provide speed and flexibility, improper usage can make debugging difficult and may lead to unexpected results.

