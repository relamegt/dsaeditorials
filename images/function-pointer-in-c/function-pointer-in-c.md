# Function Pointer in C

## Introduction

A function pointer in C is a special type of pointer that stores the address of a function instead of the address of a variable. Using a function pointer, a program can invoke functions dynamically during runtime. This provides flexibility and makes programs more modular and reusable.

Function pointers are widely used in callback functions, menu-driven applications, event handling systems, state machines, and implementing polymorphic behavior in C.

Unlike ordinary pointers that point to data, function pointers point to executable code.

## Why Use Function Pointers?

Function pointers provide several advantages:

- Allow dynamic selection of functions.
- Enable callback mechanisms.
- Improve code reusability.
- Support modular program design.
- Help implement polymorphism in C.
- Used extensively in operating systems and embedded systems.

# Declaring a Function Pointer

The declaration of a function pointer must match the return type and parameter list of the function it points to.

### Syntax

```c
return_type (*pointer_name)(parameter_types);
```

Where:

- `return_type` specifies the type returned by the function.
- `pointer_name` is the name of the function pointer.
- `parameter_types` represent the parameters accepted by the function.

The parentheses around `*pointer_name` are necessary. Without them, the compiler interprets the statement differently.

# Creating a Function Pointer

Suppose we have a function that adds two numbers.

## Example

```c
#include <stdio.h>

int add(int a, int b) {

    return a + b;
}

int main() {

    int (*ptr)(int, int);

    ptr = add;

    printf("%d", ptr(15, 5));

    return 0;
}
```

### Output
20

### Explanation

The pointer `ptr` stores the address of the `add()` function. Calling `ptr(15, 5)` executes the function and returns the sum.

# Assigning Functions to Function Pointers

A function can be assigned using either the address operator or the function name itself.

## Example

```c
#include <stdio.h>

int square(int n) {

    return n * n;
}

int main() {

    int (*ptr)(int);

    ptr = &square;

    printf("%d\n", ptr(8));

    ptr = square;

    printf("%d", ptr(10));

    return 0;
}
```

### Output
64
100

### Explanation

The function name itself acts as the address of the function, so both assignments are valid.

# Calling a Function Through Pointer

Functions can be invoked using the pointer variable.

## Example

```c
#include <stdio.h>

int multiply(int a, int b) {

    return a * b;
}

int main() {

    int (*ptr)(int, int) = multiply;

    printf("%d", (*ptr)(4, 6));

    return 0;
}
```

### Output
24

### Explanation

The expression `(*ptr)(4, 6)` calls the function whose address is stored inside `ptr`.

# Properties of Function Pointers

Function pointers have the following characteristics:

- They point to executable code instead of data.
- The declaration must match the function signature.
- They can point to different functions having the same signature.
- Pointer arithmetic is not allowed.
- They are useful in callback mechanisms.
- Arrays of function pointers are supported.

# Function Pointer as Function Argument

Passing a function pointer to another function is called a callback mechanism.

## Example

```c
#include <stdio.h>

int addition(int a, int b) {

    return a + b;
}

int subtraction(int a, int b) {

    return a - b;
}

void calculate(int x, int y,
               int (*operation)(int, int)) {

    printf("%d\n", operation(x, y));
}

int main() {

    calculate(20, 10, addition);

    calculate(20, 10, subtraction);

    return 0;
}
```

### Output
30
10

### Explanation

The `calculate()` function receives another function as an argument and executes it dynamically.

# Function Pointer with Student Result Processing

Suppose Akash Dangudubiyyapu wants to perform different operations on marks of Mohit Chandaluri and Abhiram Gopisetti.

## Example

```c
#include <stdio.h>

int maximum(int a, int b) {

    if (a > b)
        return a;

    return b;
}

int minimum(int a, int b) {

    if (a < b)
        return a;

    return b;
}

void process(int x, int y,
             int (*ptr)(int, int)) {

    printf("%d\n", ptr(x, y));
}

int main() {

    process(92, 85, maximum);

    process(92, 85, minimum);

    return 0;
}
```

### Output
92
85

# Array of Function Pointers

Multiple functions can be stored inside an array of function pointers.

## Example

```c
#include <stdio.h>

int add(int a, int b) {

    return a + b;
}

int subtract(int a, int b) {

    return a - b;
}

int multiply(int a, int b) {

    return a * b;
}

int divide(int a, int b) {

    return a / b;
}

int main() {

    int (*operations[])(int, int) = {

        add,
        subtract,
        multiply,
        divide
    };

    int a = 20;
    int b = 5;

    printf("%d\n", operations[0](a, b));

    printf("%d\n", operations[1](a, b));

    printf("%d\n", operations[2](a, b));

    printf("%d", operations[3](a, b));

    return 0;
}
```

### Output
25
15
100
4

### Explanation

Each element in the array stores the address of a different function. Functions are called dynamically through indexing.

# Function Pointer Inside Structure

Function pointers can be stored as members inside structures to simulate object-oriented behavior.

## Example

```c
#include <stdio.h>

typedef struct Student {

    int marks;

    void (*display)(struct Student *);

} Student;

void show(Student *s) {

    printf("Marks = %d", s->marks);
}

int main() {

    Student st;

    st.marks = 95;

    st.display = show;

    st.display(&st);

    return 0;
}
```

### Output
Marks = 95

### Explanation

The structure contains a function pointer that behaves similarly to a member function.

# Callback Functions

A callback function is a function passed as an argument to another function and executed later.

## Example

```c
#include <stdio.h>

void message() {

    printf("Welcome to AlphaKnowledge");
}

void execute(void (*ptr)()) {

    ptr();
}

int main() {

    execute(message);

    return 0;
}
```

### Output
Welcome to AlphaKnowledge

### Explanation

The function `message()` is passed to `execute()` and called indirectly.

# Difference Between Normal Pointer and Function Pointer

| Feature | Normal Pointer | Function Pointer |
| --- | --- | --- |
| Points To | Data | Function |
| Stores | Address of variable | Address of function |
| Arithmetic Allowed | Yes | No |
| Dereferencing | Retrieves data | Executes function |
| Usage | Memory access | Dynamic function execution |

# Applications of Function Pointers

Function pointers are used in:

1. Callback functions.
2. Menu-driven applications.
3. Event-driven programming.
4. State machines.
5. Device drivers.
6. Interrupt handling.
7. Sorting and searching libraries.
8. Dynamic dispatch mechanisms.
9. Operating systems.
10. Embedded systems.

# Advantages of Function Pointers

1. Increase flexibility.
2. Enable callback mechanisms.
3. Improve code modularity.
4. Reduce repetitive code.
5. Support runtime function selection.
6. Help simulate polymorphism in C.
7. Useful in large software systems.

# Limitations of Function Pointers

1. Syntax is difficult for beginners.
2. Incorrect signatures cause compilation errors.
3. Debugging becomes more complex.
4. Excessive use reduces readability.
5. Pointer misuse may lead to undefined behavior.

# Real-Life Example

Suppose Akash Dangudubiyyapu develops a calculator application for Mohit Chandaluri, Abhiram Gopisetti, Adapa Hemesh, Hemanth, and Akhil. Instead of writing separate programs for addition, subtraction, multiplication, and division, he stores all operation functions inside function pointers. Depending on the user's choice, the appropriate function is executed dynamically.

# Summary

A function pointer in C stores the address of a function and enables dynamic function execution. It plays an important role in callback mechanisms, event handling, and modular programming. Function pointers increase flexibility and code reusability, making them essential for system programming, embedded applications, and large-scale software development. Understanding function pointers allows programmers to design efficient and extensible C programs.

