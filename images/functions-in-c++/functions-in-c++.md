# Functions in C++

## Introduction

A function is a self-contained, named block of code designed to carry out a specific, well-defined task. By splitting a large program into smaller, isolated logical units, functions make code modular, readable, and significantly easier to debug and maintain. A function can take inputs (parameters), run its internal statements, and return a result back to the caller.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/functions-in-c/1782644956246-1781013968973-15.png)

Key advantages:

- **Modularity:** Divides a complex application into manageable, isolated segments.
- **Code Reusability:** Writes a specific logic once and executes it anywhere in the program, reducing code size.
- **Ease of Maintenance:** Isolates bugs within individual functions, making updates safer and cleaner.
- **Enhanced Readability:** Replaces inline code blocks with descriptive function names.

```Cpp
#include <iostream>
using namespace std;

// Function definition to convert Celsius to Fahrenheit
double celsiusToFahrenheit(double celsius) {
    return (celsius * 9.0 / 5.0) + 32.0;
}

int main() {
    double tempC = 25.0;
    
    // Call the function and store the result
    double tempF = celsiusToFahrenheit(tempC);
    
    cout << tempC << " C is equal to " << tempF << " F" << endl;
    
    return 0;
}
```

### Output
25 C is equal to 77 F

## Function Syntax in C++

A standard C++ function definition consists of the following structure:

```Cpp
return_type function_name(parameter_list) {
    // Function body (code to execute)
    return value; // Optional depending on return_type
}
```

- **Return Type:** The data type of the value the function returns to the caller (e.g., `int`, `double`, `string`). If the function does not return a value, the `void` keyword is used.
- **Function Name:** A unique identifier used to call the function, following C++ identifier naming conventions (typically camelCase).
- **Parameter List:** The input variables the function accepts, defined by their types and names inside parentheses. If the function takes no inputs, the parentheses are left empty.
- **Function Body:** The enclosed block of statements that execute when the function is invoked.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/functions-in-c/1782644916685-1781014024736-16.png)

## Function Declaration vs. Definition

In C++, the compiler parses code from top to bottom. Therefore, a function must be known to the compiler before it can be called. This can be handled in two ways:

### 1. Function Declaration (Prototype)

A declaration introduces the function to the compiler by specifying its name, return type, and expected parameters, but does not include the function body. It acts as a signature or blueprint.

```Cpp
// Declaration (Prototype)
double calculateVolume(double side);
```

### 2. Function Definition

A definition provides the actual code block that executes when the function is invoked.

```Cpp
// Definition
double calculateVolume(double side) {
    return side * side * side;
}
```

If you define a function *after* the `main()` function, you must declare its prototype *before* `main()`. Alternatively, you can define the entire function before `main()`, which serves as both declaration and definition simultaneously.

## Invoking a Function

To run a function, you call it by its name and supply the required arguments (actual values) within parentheses.

```Cpp
#include <iostream>
using namespace std;

// Declaration (Prototype)
void displayBanner();
int calculateArea(int length, int width);

int main() {
    // Invoking the parameterless void function
    displayBanner();

    // Invoking a function that returns a value
    int area = calculateArea(6, 8);
    cout << "Calculated Area : " << area << " sq units" << endl;

    return 0;
}

// Function definitions
void displayBanner() {
    cout << "=== Area calculation utility ===" << endl;
}

int calculateArea(int length, int width) {
    return length * width;
}
```

### Output
=== Area calculation utility ===
Calculated Area : 48 sq units

## Parameters and Arguments

- **Parameters:** Variables defined in the function signature (e.g., `length` and `width` in `calculateArea`).
- **Arguments:** The actual values passed to the function during a call (e.g., `6` and `8` in `calculateArea(6, 8)`).

```Cpp
#include <iostream>
using namespace std;

void displaySensorWarning(double reading) {
    cout << "Warning! Sensor reading is abnormally high: " << reading << " units" << endl;
}

int main() {
    double primarySensor = 92.4;
    double backupSensor = 98.7;

    displaySensorWarning(primarySensor);
    displaySensorWarning(backupSensor);

    return 0;
}
```

### Output
Warning! Sensor reading is abnormally high: 92.4 units
Warning! Sensor reading is abnormally high: 98.7 units

When calling a function, the arguments must match the parameter list in quantity, type, and order.

## Types of Functions in C++

Functions are classified by their origin or their signature structure.

### Classification by Origin

- **Library Functions:** Predefined functions built into standard libraries (e.g., `sqrt()` from `<cmath>`, `std::getline()` from `<string>`).
- **User-Defined Functions:** Functions created from scratch by the programmer to address custom requirements.

### Classification by Signature Structure

| Structure | Description | Example Signature |
| --- | --- | --- |
| **No Parameters, No Return** | Performs an isolated action with no input or output | `void showMenu();` |
| **Parameters, No Return** | Processes input arguments but does not send a result back | `void printScore(int s);` |
| **No Parameters, Returns Value** | Retrieves or generates a value without external input | `double getPiValue();` |
| **Parameters, Returns Value** | Transforms inputs into a resulting value and returns it | `int getMax(int a, int b);` |

> **Note:** Unlike C, C++ supports passing arguments by reference (using the `&` symbol in the parameter list), which allows a function to modify the original variable at the call site directly. Additionally, C++ allows you to specify **default parameters** (e.g., `void config(int speed = 50)`) so the function can be called with fewer arguments, making C++ function management significantly more flexible.

## Summary

A function in C++ is a reusable block of code that performs a specific task, promoting modularity, reusability, and easier maintenance. A function's signature requires a return type, name, and parameter list, followed by its body. In C++, a function must be declared (via prototype) or defined before it is used. Functions can be built-in library functions or user-defined, and they are categorized based on their parameter and return configurations. Advanced features like pass-by-reference and default arguments make C++ functions highly versatile.




