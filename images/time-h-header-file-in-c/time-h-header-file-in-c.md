# time.h Header File in C

## Introduction

The `time.h` header file provides functions, macros, and data types for working with date and time in C. It allows programs to obtain the current date and time, measure execution time, convert time formats, and format date and time strings.

The `time.h` library contains:

- `time_t` for calendar time.
- `clock_t` for processor time.
- `struct tm` for storing date and time components.
- Functions such as `time()`, `clock()`, `localtime()`, `gmtime()`, `difftime()`, `asctime()`, `ctime()`, and `strftime()`.
- Macro `CLOCKS_PER_SEC` to represent clock ticks per second.

## Time Data Types

### 1. time_t

Stores calendar time as the number of seconds elapsed since January 1, 1970 (Unix Epoch).

### 2. clock_t

Stores processor time consumed by a program.

### 3. struct tm

Stores individual components of date and time.

```c
struct tm {
    int tm_sec;
    int tm_min;
    int tm_hour;
    int tm_mday;
    int tm_mon;
    int tm_year;
    int tm_wday;
    int tm_yday;
    int tm_isdst;
};
```

## Common Functions in time.h

| Function | Description |
| --- | --- |
| time() | Gets current calendar time |
| localtime() | Converts time into local time |
| gmtime() | Converts time into UTC |
| asctime() | Converts struct tm into string |
| ctime() | Converts time_t into string |
| clock() | Returns processor time |
| difftime() | Calculates difference between two times |
| mktime() | Converts struct tm to time_t |
| strftime() | Formats date and time |

# Get Current Date and Time

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    time_t currentTime;
    struct tm *ptr;

    currentTime = time(NULL);

    ptr = localtime(&currentTime);

    printf("%s", asctime(ptr));

    return 0;
}
```

### Output
Tue Apr 15 07:22:42 2025

### Explanation

- `time()` obtains the current time.
- `localtime()` converts it into local date and time components.
- `asctime()` converts it into a human-readable string.

---

# Print UTC Time

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    time_t currentTime;
    struct tm *ptr;

    currentTime = time(NULL);

    ptr = gmtime(&currentTime);

    printf("%s", asctime(ptr));

    return 0;
}
```

### Output
Tue Apr 15 12:44:17 2025

### Explanation

`gmtime()` converts the current time into Coordinated Universal Time (UTC).

---

# Find Time Difference

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    time_t startTime, endTime;

    startTime = time(NULL);

    int num1 = 15;
    int num2 = 25;

    printf("Sum = %d\n", num1 + num2);

    endTime = time(NULL);

    printf("Execution Time = %.2f seconds",
           difftime(endTime, startTime));

    return 0;
}
```

### Output
Sum = 40
Execution Time = 0.00 seconds

### Explanation

`difftime()` calculates the difference between two `time_t` values in seconds.

---

# Measure CPU Time

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    clock_t start, end;

    start = clock();

    long sum = 0;

    for (int i = 1; i <= 1000000; i++) {
        sum += i;
    }

    end = clock();

    printf("Sum = %ld\n", sum);

    printf("CPU Time = %f seconds",
           (double)(end - start) / CLOCKS_PER_SEC);

    return 0;
}
```

### Output
Sum = 500000500000
CPU Time = 0.002000 seconds

### Explanation

- `clock()` records CPU clock ticks.
- The difference between end and start gives processor time consumed.
- Dividing by `CLOCKS_PER_SEC` converts ticks into seconds.

---

# Format Time Using strftime()

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    time_t currentTime;
    struct tm *ptr;
    char buffer[80];

    time(&currentTime);

    ptr = localtime(&currentTime);

    strftime(buffer, 80,
             "Time is %I:%M %p",
             ptr);

    puts(buffer);

    return 0;
}
```

### Output
Time is 09:00 AM

### Explanation

`strftime()` formats date and time according to format specifiers.

| Specifier | Meaning |
| --- | --- |
| %I | Hour (12-hour format) |
| %H | Hour (24-hour format) |
| %M | Minutes |
| %S | Seconds |
| %p | AM or PM |
| %d | Day |
| %m | Month |
| %Y | Year |

---

# Using ctime()

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    time_t currentTime;

    currentTime = time(NULL);

    printf("%s", ctime(&currentTime));

    return 0;
}
```

### Output
Tue Apr 15 07:22:42 2025

### Explanation

`ctime()` converts a `time_t` value directly into a formatted string.

---

# Using mktime()

## Example

```c
#include <stdio.h>
#include <time.h>

int main() {

    struct tm date = {0};

    date.tm_year = 2025 - 1900;
    date.tm_mon = 3;
    date.tm_mday = 15;

    time_t t = mktime(&date);

    printf("%ld", t);

    return 0;
}
```

### Output
1744675200

### Explanation

`mktime()` converts a `struct tm` object into calendar time (`time_t`).

---

# Advantages of time.h

- Provides date and time operations.
- Measures execution time.
- Supports time formatting.
- Converts between various time representations.
- Portable and part of the standard C library.

# Limitations

- Accuracy depends on system clock resolution.
- Time zones vary across systems.
- `clock()` measures CPU time rather than actual elapsed time.
- Some functions return static memory and are not thread-safe.

# Summary

The `time.h` header file in C provides facilities for obtaining and manipulating date and time information. It defines the data types `time_t`, `clock_t`, and `struct tm`, and provides functions such as `time()`, `clock()`, `localtime()`, `gmtime()`, `ctime()`, `asctime()`, `difftime()`, `mktime()`, and `strftime()` for working with calendar time, processor time, and formatted date and time strings.

