# C String Functions

## Introduction

C provides several built-in string functions to perform operations such as finding length, copying, concatenation, comparison, searching, formatting, and tokenization. These functions are declared in the `<string.h>` header file and help simplify string manipulation.

### Key Features

- Available through the `<string.h>` header file.
- Simplify common string operations.
- Work with character arrays terminated by `'\0'`.
- Improve code readability and reduce programming effort.
- Support copying, comparison, searching, and tokenization.

# Header File

Before using string functions, include the header file:

```c
#include <string.h>
```

# strlen()

The `strlen()` function returns the number of characters in a string excluding the null character.

## Syntax

```c
strlen(str);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "Programming";

    printf("%lu", strlen(str));

    return 0;
}
```

### Output
11

### Explanation

`strlen()` counts only the characters and ignores `'\0'`.

# strcpy()

The `strcpy()` function copies one string into another.

## Syntax

```c
strcpy(destination, source);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char source[] = "AlphaKnowledge";
    char destination[30];

    strcpy(destination, source);

    printf("%s", destination);

    return 0;
}
```

### Output
AlphaKnowledge

### Explanation

The complete source string, including the null character, is copied.

# strncpy()

The `strncpy()` function copies only the first n characters.

## Syntax

```c
strncpy(destination, source, n);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char source[] = "Computer";
    char destination[20];

    strncpy(destination, source, 4);
    destination[4] = '\0';

    printf("%s", destination);

    return 0;
}
```

### Output
Comp

### Explanation

Only the first four characters are copied.

# strcat()

The `strcat()` function appends one string to another.

## Syntax

```c
strcat(destination, source);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[30] = "Hello ";
    char str2[] = "World";

    strcat(str1, str2);

    printf("%s", str1);

    return 0;
}
```

### Output
Hello World

### Explanation

The source string is added to the end of the destination string.

# strncat()

The `strncat()` function appends only the first n characters.

## Syntax

```c
strncat(destination, source, n);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[30] = "Data";
    char str2[] = "Structure";

    strncat(str1, str2, 5);

    printf("%s", str1);

    return 0;
}
```

### Output
DataStruc

### Explanation

Only five characters are appended.

# strcmp()

The `strcmp()` function compares two strings lexicographically.

## Syntax

```c
strcmp(str1, str2);
```

### Return Values

| Value | Meaning |
| --- | --- |
| 0 | Strings are equal |
| Negative | First string is smaller |
| Positive | First string is larger |

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[] = "Apple";
    char str2[] = "Banana";

    int result = strcmp(str1, str2);

    printf("%d", result);

    return 0;
}
```

### Output
Negative value

### Explanation

"Apple" comes before "Banana" alphabetically.

# strncmp()

The `strncmp()` function compares only the first n characters.

## Syntax

```c
strncmp(str1, str2, n);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[] = "Program";
    char str2[] = "Progress";

    if (strncmp(str1, str2, 3) == 0)
    {
        printf("Equal");
    }

    return 0;
}
```

### Output
Equal

### Explanation

The first three characters are the same.

# strchr()

The `strchr()` function finds the first occurrence of a character.

## Syntax

```c
strchr(string, character);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "Computer";

    char *ptr = strchr(str, 'p');

    printf("%ld", ptr - str);

    return 0;
}
```

### Output
3

### Explanation

The first occurrence of `'p'` is at index 3.

# strrchr()

The `strrchr()` function finds the last occurrence of a character.

## Syntax

```c
strrchr(string, character);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "Programming";

    char *ptr = strrchr(str, 'm');

    printf("%ld", ptr - str);

    return 0;
}
```

### Output
7

### Explanation

The last occurrence of `'m'` is at index 7.

# strstr()

The `strstr()` function searches for a substring.

## Syntax

```c
strstr(mainString, subString);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "Learn C Programming";

    if (strstr(str, "Programming"))
    {
        printf("Found");
    }

    return 0;
}
```

### Output
Found

### Explanation

The substring exists inside the string.

# sprintf()

The `sprintf()` function stores formatted data into a string.

## Syntax

```c
sprintf(string, format, values);
```

## Example

```c
#include <stdio.h>

int main()
{
    char str[50];
    int age = 21;

    sprintf(str, "Age = %d", age);

    printf("%s", str);

    return 0;
}
```

### Output
Age = 21

### Explanation

The formatted text is stored inside the character array.

# strtok()

The `strtok()` function breaks a string into tokens using delimiters.

## Syntax

```c
strtok(string, delimiter);
```

## Example

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[] = "C,Java,Python";

    char *token = strtok(str, ",");

    while (token != NULL)
    {
        printf("%s\n", token);
        token = strtok(NULL, ",");
    }

    return 0;
}
```

### Output
C
Java
Python

### Explanation

Each token is separated using the comma delimiter.

# Common String Functions Table

| Function | Purpose |
| --- | --- |
| strlen() | Find string length |
| strcpy() | Copy string |
| strncpy() | Copy first n characters |
| strcat() | Concatenate strings |
| strncat() | Concatenate first n characters |
| strcmp() | Compare strings |
| strncmp() | Compare first n characters |
| strchr() | Find first occurrence of character |
| strrchr() | Find last occurrence of character |
| strstr() | Find substring |
| sprintf() | Store formatted output in string |
| strtok() | Split string into tokens |

# Advantages

1. Simplifies string manipulation.
2. Reduces coding effort.
3. Improves readability.
4. Provides efficient string operations.
5. Widely supported in all C compilers.

# Limitations

1. Functions do not automatically prevent buffer overflow.
2. Incorrect usage may lead to memory issues.
3. Some functions modify the original string.
4. Extra care is required with pointers and arrays.

# Summary

C provides a rich set of built-in string functions through the `<string.h>` header file. Functions such as `strlen()`, `strcpy()`, `strcat()`, `strcmp()`, `strchr()`, `strstr()`, `sprintf()`, and `strtok()` help perform common string operations efficiently. Understanding these functions is essential for working with text and character arrays in C programs.

