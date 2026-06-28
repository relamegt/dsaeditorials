# Parameter Passing Techniques in C++

## Introduction

Parameter passing refers to the mechanism by which values are transmitted from the calling environment to the function being invoked. When designing functions, choosing the correct passing method is critical for program correctness, efficiency, and memory conservation.

Before exploring the methods, it is helpful to distinguish between two key concepts:

- **Formal Parameters:** The variable declarations inside the function's parentheses. They act as placeholders that receive data when the function runs.
- **Actual Parameters (Arguments):** The real values, variables, or expressions passed to the function when it is called from the main body or another function.

C++ supports three primary parameter-passing techniques:

1. Pass by Value
2. Pass by Reference
3. Pass by Pointer

## 1. Pass by Value

In the pass-by-value method, the compiler creates a separate copy of the actual parameter's value in memory and assigns it to the function's formal parameter. Any changes made to the parameter inside the function body only modify this local copy, leaving the original variable in the calling scope completely unaffected.

### Scenario: Applying a Store Discount

```Cpp
#include <iostream>
using namespace std;

void applyDiscount(double price) {
    price = price * 0.90; // Apply 10% discount to local copy
    cout << "Inside function (discounted) : $" << price << endl;
}

int main() {
    double originalPrice = 100.0;

    applyDiscount(originalPrice);

    cout << "In main (original price)     : $" << originalPrice << endl;
    return 0;
}
```

### Output
Inside function (discounted) : $90
In main (original price)     : $100

Because `originalPrice` was passed by value, the local modifications inside `applyDiscount()` did not leak back to affect `originalPrice` in `main()`.

### Advantages

- **Safety:** The caller's variables are protected from accidental modifications.
- **Simplicity:** No need to manage memory addresses or pointers.

### Disadvantages

- **Memory Overhead:** Copying large data structures (such as heavy classes or large vectors) can be slow and consume unnecessary memory.

## 2. Pass by Reference

In the pass-by-reference method, the function receives an alias (a reference) to the actual variable in the calling scope. No copy is created in memory. Instead, both the formal parameter inside the function and the actual parameter in the calling scope refer to the exact same memory location. Any modifications performed inside the function immediately affect the original variable.

### Scenario: Updating a Player's Game Score

```Cpp
#include <iostream>
using namespace std;

void updatePlayerScore(int& score) {
    score += 500; // Modify original score directly
}

int main() {
    int currentScore = 1500;

    cout << "Score before update : " << currentScore << endl;

    updatePlayerScore(currentScore);

    cout << "Score after update  : " << currentScore << endl;
    return 0;
}
```

### Output
Score before update : 1500
Score after update  : 2000

Declaring the parameter as `int& score` allows the function to write directly to `currentScore` in the calling function, avoiding copying overhead.

### Advantages

- **Performance:** Extremely fast for large objects since no copy is created.
- **Direct Modification:** Allows functions to return updates directly back to the caller's variables.

### Disadvantages

- **Accidental Modification:** If the function makes a mistake, it can corrupt the caller's data. (This can be mitigated by passing as a constant reference).

## 3. Pass by Pointer

The pass-by-pointer method passes the memory address of the actual variable to the function. Inside the function, the address is stored in a pointer parameter. To read or write the value at that address, the pointer must be dereferenced using the dereference operator (`*`). Like pass-by-reference, this allows direct modification of the original variable.

### Scenario: Adjusting Audio Volume Level

```Cpp
#include <iostream>
using namespace std;

void adjustVolume(int* volume) {
    if (volume != nullptr) {
        *volume = 80; // Dereference pointer to modify original value
    }
}

int main() {
    int currentVolume = 50;

    cout << "Volume before adjustment : " << currentVolume << endl;

    adjustVolume(&currentVolume); // Pass memory address of variable

    cout << "Volume after adjustment  : " << currentVolume << endl;
    return 0;
}
```

### Output
Volume before adjustment : 50
Volume after adjustment  : 80

### Advantages

- **Optional Parameters:** Can pass `nullptr` to indicate that no variable is being provided.
- **Dynamic Structures:** Essential when passing dynamically allocated arrays or interfacing with C APIs.

### Disadvantages

- **Syntax Complexity:** Requires explicit address-of (`&`) and dereferencing (`*`) operators.
- **Safety Risks:** Risk of dereferencing a null or wild pointer, which leads to program crashes (segmentation faults).

## Comparison of Parameter Passing Techniques

| Feature | Pass by Value | Pass by Reference | Pass by Pointer |
| --- | --- | --- | --- |
| **Object Copied?** | Yes | No | No (only the address is copied) |
| **Changes Original?** | No | Yes | Yes |
| **Syntax Complexity** | Low | Low | High (requires `*` and `&`) |
| **Can Be Null?** | No | No | Yes (`nullptr`) |
| **Safety** | High (isolated) | Medium (safe references) | Low (pointer math, null pointers) |
| **Best For** | Small primitive types (`int`, `char`, `double`) | Large structures, objects, class instances | Optional arguments, C API integration, raw arrays |

> **Note:** In modern C++, pass-by-reference is generally preferred over pass-by-pointer because it offers clean, direct syntax without pointer arithmetic risks. To protect large objects from accidental modifications while retaining pass-by-reference efficiency, use a **constant reference** (`const Type&`), which allows compiler-enforced read-only access without the cost of copying.

## Summary

C++ supports three parameter-passing techniques: pass by value, pass by reference, and pass by pointer. Pass by value copies the argument's data, ensuring the caller's variable remains unchanged, but incurs copying overhead. Pass by reference passes an alias to the original variable, enabling direct modifications and avoiding copy overhead. Pass by pointer passes the memory address of the argument, offering similar direct modification capabilities with the additional flexibility of supporting null parameters, though at the expense of syntax complexity and safety risks. Choosing the right method depends on data size, optionality requirements, and safety concerns.




