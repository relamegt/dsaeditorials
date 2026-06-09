# Default Arguments in C++

Default arguments are values assigned to function parameters that are automatically used when no argument is provided during a function call. They make functions more flexible by allowing the same function to be called with different numbers of arguments.

Instead of creating multiple functions for similar tasks, default arguments allow a single function to handle different situations. This reduces code duplication and improves readability.

For example, if a function usually works with a common value, that value can be specified as a default argument. Whenever the user does not provide a value, the compiler automatically uses the default one.

## Example Code

```cpp
#include <iostream>
using namespace std;

void display(int num = 10)
{
    cout << num << endl;
}

int main()
{
    display();
    display(25);

    return 0;
}
```

### Output
10
25

### 

When `display()` is called without an argument, the compiler uses the default value `10`. When `display(25)` is called, the supplied value replaces the default value.

## Syntax of Default Arguments

A default value is assigned using the assignment operator (`=`) in the function declaration.

```cpp
return_type functionName(parameter = defaultValue);
```

For multiple parameters:

```cpp
return_type functionName(parameter1 = value1,
                         parameter2 = value2,
                         parameter3 = value3);
```

Here, each parameter is assigned a predefined value that will be used if no argument is supplied during the function call.

## Why Use Default Arguments?

Default arguments provide several benefits:

- Reduce code duplication.
- Make function calls simpler.
- Avoid unnecessary function overloading.
- Improve code readability.
- Allow optional parameters.
- Increase code flexibility.

Without default arguments, programmers often create multiple overloaded functions to handle different numbers of parameters. Default arguments provide a cleaner solution.

## Rules for Default Arguments

### 1. Specify Default Values in Function Declarations

Default values should generally be specified in the function declaration (prototype), not in the function definition.

```cpp
#include <iostream>
using namespace std;

void printValue(int x = 10);

void printValue(int x)
{
    cout << x << endl;
}

int main()
{
    printValue();
    return 0;
}
```

Providing default values in the declaration allows the compiler to correctly validate function calls before seeing the function definition.

### 2. Default Arguments Cannot Be Redefined

Once a default value has been assigned in the declaration, it must not be assigned again in the definition.

Incorrect Example:

```cpp
void show(int x = 10);

void show(int x = 20)
{
    cout << x;
}
```

The compiler generates an error because the default value is specified more than once.

### 3. Default Arguments Must Be Assigned from Right to Left

If one parameter has a default value, all parameters to its right must also have default values.

Valid Example:

```cpp
void display(int x, int y = 20);
```

Invalid Example:

```cpp
void display(int x = 10, int y);
```

The second example is invalid because `y` has no default value while the parameter before it does.

### 4. Avoid Ambiguity with Function Overloading

Default arguments can sometimes create ambiguity when combined with function overloading.

```cpp
void show(int x = 10);
void show(int x);
```

Calling:

```cpp
show();
```

causes ambiguity because the compiler cannot determine which version of the function should be called.

Therefore, default arguments and overloaded functions should be designed carefully.

## Example: Area of a Rectangle

Suppose we want to calculate the area of a rectangle. Most of the time, a default height may be sufficient, but users should also be able to provide a custom height.

```cpp
#include <iostream>
using namespace std;

double calculateArea(double length, double height = 10.0)
{
    return length * height;
}

int main()
{
    cout << "Area 1: " << calculateArea(5) << endl;
    cout << "Area 2: " << calculateArea(5, 8);

    return 0;
}
```

### Output
Area 1: 50
Area 2: 40

### 

In the first function call, only the length is provided, so the default height value `10.0` is used.

In the second function call, the supplied height `8` replaces the default value.

## Another Example

```cpp
#include <iostream>
using namespace std;

void greet(string name = "Guest")
{
    cout << "Welcome, " << name << "!" << endl;
}

int main()
{
    greet();
    greet("Mohit");

    return 0;
}
```

### Output
Welcome, Guest!
Welcome, Mohit!

### 

If no name is supplied, the function automatically uses `"Guest"` as the default value.

## Advantages of Default Arguments

- Simplify function calls.
- Reduce the need for overloaded functions.
- Improve readability.
- Allow optional parameters.
- Increase code reusability.
- Make programs easier to maintain.

## Limitations of Default Arguments

- Must follow the right-to-left rule.
- Can create ambiguity with overloaded functions.
- Cannot be redefined multiple times.
- Excessive use may reduce code clarity.

## Summary

Default arguments allow parameters to have predefined values that are automatically used when arguments are not supplied during a function call. They help reduce code duplication, simplify function calls, and improve program readability. When used correctly, default arguments make C++ programs more flexible, maintainable, and easier to understand.




