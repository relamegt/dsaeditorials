# Strings in C

## Introduction

A string in C is a sequence of characters terminated by a special null character `'\0'`. Unlike some programming languages, C does not provide a built-in string data type. Instead, strings are represented using character arrays.

The null character marks the end of the string and allows string functions to determine where the string ends.

### Key Features

- Strings are arrays of characters.
- Every string ends with the null character `'\0'`.
- C does not have a separate string data type.
- Strings are stored in contiguous memory locations.
- Standard library functions are available for manipulating strings.

# Declaring and Initializing Strings

A string can be declared and initialized using double quotes.

## Example

```c
#include <stdio.h>

int main()
{
    char str[] = "AlphaKnowledge";

    printf("%s", str);

    return 0;
}
```

### Output
AlphaKnowledge

### Explanation

The string `"AlphaKnowledge"` is stored internally as:

```text
{'A','l','p','h','a','K','n','o','w','l','e','d','g','e','\0'}
```

The null character `'\0'` is automatically added at the end.

# Accessing Characters

Individual characters can be accessed using indexes.

## Example

```c
#include <stdio.h>

int main()
{
    char str[] = "Programming";

    printf("%c\n", str[0]);
    printf("%c", str[4]);

    return 0;
}
```

### Output
P
r

### Explanation

Strings behave like arrays, so indexing starts from 0.

# Modifying Characters

Characters inside a character array can be modified.

## Example

```c
#include <stdio.h>

int main()
{
    char str[] = "Cat";

    str[0] = 'B';

    printf("%s", str);

    return 0;
}
```

### Output
Bat

### Explanation

The first character was changed from `C` to `B`.

# Finding String Length

The `strlen()` function returns the number of characters excluding the null character.

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "Computer";

    printf("%d", strlen(str));

    return 0;
}
```

### Output
8

### Explanation

The string contains eight characters. The null character is not counted.

# Input Strings Using scanf()

The `%s` format specifier reads a single word.

## Example

```c
#include <stdio.h>

int main()
{
    char name[20];

    printf("Enter name: ");
    scanf("%s", name);

    printf("Name = %s", name);

    return 0;
}
```

### Output
Enter name: Akash
Name = Akash

### Explanation

`scanf()` stops reading when it encounters whitespace.

# Reading Strings with Spaces Using Scanset

## Example

```c
#include <stdio.h>

int main()
{
    char str[30];

    printf("Enter text: ");
    scanf("%29[^\n]", str);

    printf("%s", str);

    return 0;
}
```

### Output
Enter text: Alpha Knowledge Platform
Alpha Knowledge Platform

### Explanation

The scanset reads characters until a newline character is encountered.

# Input Strings Using fgets()

`fgets()` reads complete lines including spaces.

## Example

```c
#include <stdio.h>

int main()
{
    char str[50];

    printf("Enter text: ");
    fgets(str, sizeof(str), stdin);

    printf("%s", str);

    return 0;
}
```

### Output
Enter text: Learning C Language
Learning C Language

### Explanation

`fgets()` is safer than `scanf()` because it prevents buffer overflow.

# Passing Strings to Functions

Strings are passed to functions just like arrays.

## Example

```c
#include <stdio.h>

void display(char str[])
{
    printf("%s", str);
}

int main()
{
    char name[] = "AlphaKnowledge";

    display(name);

    return 0;
}
```

### Output
AlphaKnowledge

### Explanation

The address of the first character is passed to the function.

# Strings and Pointers

A pointer can point to the first character of a string.

## Example

```c
#include <stdio.h>

int main()
{
    char str[] = "Hello";
    char *ptr = str;

    while (*ptr != '\0')
    {
        printf("%c", *ptr);
        ptr++;
    }

    return 0;
}
```

### Output
Hello

### Explanation

The pointer moves one character at a time until it reaches the null character.

# String Literals

String literals are sequences of characters enclosed in double quotes.

## Example

```c
#include <stdio.h>

int main()
{
    const char *str = "Welcome to C";

    printf("%s", str);

    return 0;
}
```

### Output
Welcome to C

### Explanation

String literals are generally stored in read-only memory, so they should not be modified.

# Common String Functions

| Function | Description |
| --- | --- |
| strlen() | Finds string length |
| strcpy() | Copies one string to another |
| strcat() | Concatenates two strings |
| strcmp() | Compares two strings |
| strchr() | Finds a character in a string |
| strstr() | Finds a substring |

# Example of String Functions

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[30] = "Alpha";
    char str2[] = "Knowledge";

    strcat(str1, str2);

    printf("%s\n", str1);
    printf("%d", strlen(str1));

    return 0;
}
```

### Output
AlphaKnowledge
14

### Explanation

`strcat()` joins the strings and `strlen()` returns the total number of characters.

# Memory Representation of Strings

```text
String = "Hello"

Index   Character
0          H
1          e
2          l
3          l
4          o
5         '\0'
```

The null character marks the end of the string.

# Advantages

1. Efficient memory usage.
2. Easy to store text data.
3. Supported by many library functions.
4. Simple character manipulation.
5. Can be accessed using arrays and pointers.

# Limitations

1. No built-in string type.
2. Buffer overflow can occur if input size is not controlled.
3. Manual memory management is required.
4. String operations may be slower for very large strings.
5. String literals should not be modified.

# Summary

A string in C is a character array terminated by the null character `'\0'`. Strings can be declared using character arrays or string literals and accessed using indexes or pointers. Functions such as `strlen()`, `strcpy()`, `strcat()`, and `strcmp()` simplify string operations. Input can be taken using `scanf()` or `fgets()`, with `fgets()` being the safer option. Strings are one of the most important data structures used in C programming for handling textual information.

