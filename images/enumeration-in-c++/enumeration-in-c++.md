# Enumeration in C++

An Enumeration (or Enum) is a user-defined data type in C++ that consists of a set of named integer constants. Instead of using raw integer values throughout a program, enums allow programmers to assign meaningful names to those values, making code easier to read, understand, and maintain.
For example, instead of using numbers like 0, 1, 2, and 3 to represent directions, we can use meaningful names such as EAST, WEST, NORTH, and SOUTH.

Enumerations are commonly used when a variable can take only a limited set of predefined values, such as:

- Days of the week
- Months of the year
- Directions
- Colors
- Status codes
- Menu options

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/enumeration-in-c/1781077350311-ChatGPT_Image_Jun_10%2C_2026%2C_11_55_09_AM.png)

## Why Do We Need Enumerations?

Consider a program that stores the current traffic signal.

### Example Code

```cpp
int signal = 2;
```

Although this works, it is difficult to understand what value 2 represents.

A better approach is:

### Example Code

```cpp
enum TrafficSignal
{
    RED,
    YELLOW,
    GREEN
};
```

Now the code becomes much more readable.

```cpp
TrafficSignal signal = GREEN;
```

Anyone reading the code can immediately understand the meaning of the value.

Enumerations improve:

- Code readability
- Maintainability
- Debugging
- Program organization

## Creating an Enumeration

An enumeration is created using the `enum` keyword.

### Syntax

```cpp
enum EnumName
{
    Constant1,
    Constant2,
    Constant3
};
```

### Example Code

```cpp
enum Direction
{
    EAST,
    WEST,
    NORTH,
    SOUTH
};
```

Here:

- `Direction` is the enum name.
- `EAST`, `WEST`, `NORTH`, and `SOUTH` are named constants.
- Each constant is automatically assigned an integer value.

## Default Values in Enum

By default, enum values start from 0 and increase by 1 for each subsequent member.

### Example Code

```cpp
enum Direction
{
    EAST,
    WEST,
    NORTH,
    SOUTH
};
```

Internally, the compiler assigns:

```text
EAST  = 0
WEST  = 1
NORTH = 2
SOUTH = 3
```

These values are assigned automatically.

## Creating Enum Variables

After defining an enumeration, variables of that enum type can be created.

### Syntax

```cpp
EnumName variableName;
```

### Example Code

```cpp
#include <iostream>
using namespace std;

enum Direction
{
    EAST,
    WEST,
    NORTH,
    SOUTH
};

int main()
{
    Direction dir = NORTH;

    cout << dir;

    return 0;
}
```

### Output
2

### 

The output is 2 because the compiler assigned the value 2 to `NORTH`.

## Understanding Enum Values

Although enum members have meaningful names, they are internally stored as integers.

### Example Code

```cpp
#include <iostream>
using namespace std;

enum Day
{
    MONDAY,
    TUESDAY,
    WEDNESDAY
};

int main()
{
    cout << MONDAY << endl;
    cout << TUESDAY << endl;
    cout << WEDNESDAY;

    return 0;
}
```

### Output
0
1
2

### 

The compiler automatically assigns consecutive integer values.

## Assigning Custom Values

Enum members can also be assigned custom integer values.

### Example Code

```cpp
enum Grade
{
    A = 90,
    B = 80,
    C = 70
};
```

Here:

```text
A = 90
B = 80
C = 70
```

The compiler uses the specified values instead of default values.

### Example Code

```cpp
#include <iostream>
using namespace std;

enum Grade
{
    A = 90,
    B = 80,
    C = 70
};

int main()
{
    cout << A << endl;
    cout << B << endl;
    cout << C;

    return 0;
}
```

### Output
90
80
70

### 

## Partial Custom Initialization

It is not necessary to assign values to all enum members.

### Example Code

```cpp
enum Marks
{
    PASS = 35,
    GOOD = 60,
    VERYGOOD,
    EXCELLENT
};
```

Internally:

```text
PASS      = 35
GOOD      = 60
VERYGOOD  = 61
EXCELLENT = 62
```

After a manually assigned value, the compiler continues incrementing automatically.

## Changing Enum Variables

Enum variables can be reassigned to another valid enum constant.

### Example Code

```cpp
#include <iostream>
using namespace std;

enum Status
{
    PENDING,
    PROCESSING,
    COMPLETED
};

int main()
{
    Status current = PENDING;

    cout << current << endl;

    current = COMPLETED;

    cout << current;

    return 0;
}
```

### Output
0
2

### 

The variable changes from one enum constant to another.

## Memory Representation of Enum

An enum variable stores an integer value internally.

Consider:

### Example Code

```cpp
enum Direction
{
    EAST,
    WEST,
    NORTH,
    SOUTH
};

Direction dir = WEST;
```

Internally:

```text
dir = 1
```

Although the program uses meaningful names, the compiler stores the corresponding integer value.

## Enum and Switch Statements

Enums are frequently used with switch statements because they represent a limited set of choices.

### Example Code

```cpp
#include <iostream>
using namespace std;

enum Day
{
    MONDAY,
    TUESDAY,
    WEDNESDAY
};

int main()
{
    Day today = TUESDAY;

    switch(today)
    {
        case MONDAY:
            cout << "Monday";
            break;

        case TUESDAY:
            cout << "Tuesday";
            break;

        case WEDNESDAY:
            cout << "Wednesday";
            break;
    }

    return 0;
}
```

### Output
Tuesday

### 

Enums make switch statements cleaner and easier to read.

## Enum Classes (Scoped Enumerations)

Traditional enums have a drawback: their names are placed in the global scope, which can cause naming conflicts.

To solve this problem, C++11 introduced **enum classes**.

Enum classes provide:

- Better type safety.
- Scoped names.
- Reduced naming conflicts.
- Stronger compile-time checking.

## Creating an Enum Class

### Syntax

```cpp
enum class EnumName
{
    Value1,
    Value2,
    Value3
};
```

### Example Code

```cpp
enum class Day
{
    MONDAY,
    TUESDAY,
    WEDNESDAY
};
```

Unlike traditional enums, members must be accessed using the scope resolution operator (`::`).

### Example Code

```cpp
Day today = Day::TUESDAY;
```

## Enum Class Example

### Example Code

```cpp
#include <iostream>
using namespace std;

enum class Day
{
    MONDAY,
    TUESDAY,
    WEDNESDAY
};

int main()
{
    Day today = Day::WEDNESDAY;

    cout << static_cast<int>(today);

    return 0;
}
```

### Output
2

### 

The `static_cast<int>()` converts the enum value to an integer before printing.

## Why Enum Class is Safer

Consider two traditional enums:

### Example Code

```cpp
enum Color
{
    RED
};

enum Signal
{
    RED
};
```

This causes a naming conflict because both enums contain `RED`.

With enum classes:

### Example Code

```cpp
enum class Color
{
    RED
};

enum class Signal
{
    RED
};
```

Now there is no conflict because they are accessed as:

```cpp
Color::RED
Signal::RED
```

This makes the code safer and more organized.

## Applications of Enumerations

Enumerations are commonly used in:

- Days of the week
- Months of the year
- Directions
- Game states
- Traffic signals
- User roles
- Menu systems
- Status codes
- Device states
- Finite State Machines (FSM)

## Advantages of Enumerations

- Improves code readability.
- Makes programs easier to understand.
- Eliminates the use of magic numbers.
- Provides type safety.
- Simplifies switch-case implementations.
- Reduces programming errors.

## Limitations of Enumerations

- Enum values are limited to integers.
- Traditional enums may cause naming conflicts.
- Cannot directly store strings or floating-point values.
- Less flexible compared to classes.

## Enum vs Enum Class

| Feature | Enum | Enum Class |
| --- | --- | --- |
| Scope | Global | Scoped |
| Type Safety | Less | More |
| Naming Conflicts | Possible | Avoided |
| Requires Explicit Casting | No | Yes |
| Introduced In | C++98 | C++11 |

# Summary

Enumeration is a user-defined data type that allows a set of named integer constants to be grouped together. Enums improve readability and maintainability by replacing numeric values with meaningful names. Traditional enums automatically assign integer values and are widely used in switch statements and state-based programming. C++11 introduced enum classes, which provide stronger type safety, scoped names, and better protection against naming conflicts. Enumerations are commonly used to represent a fixed set of related values such as days, directions, statuses, and system states.




