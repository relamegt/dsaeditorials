# Parameter Passing Techniques in C

## Introduction

Parameter passing is the process of transferring data from a calling function to a called function. Parameters enable functions to receive input values, perform operations, and optionally return results.

In C, data is transferred to functions through arguments. Understanding parameter passing techniques is essential because they determine whether modifications inside a function affect the original variables.

### Key Features

- Enables communication between functions.
- Allows functions to receive input values.
- Improves code reusability and modularity.
- Supports efficient handling of large data structures.
- Provides control over whether original data should be modified.

# Actual Parameters and Formal Parameters

## Actual Parameters

Actual parameters, also called arguments, are the values passed during the function call.

### Example

```c
add(10, 20);
```

Here, `10` and `20` are actual parameters.

## Formal Parameters

Formal parameters are variables declared in the function definition that receive values from the calling function.

### Example

```c
int add(int a, int b)
{
    return a + b;
}
```

Here, `a` and `b` are formal parameters.

# Parameter Passing Techniques

C mainly uses two techniques:

1. Pass By Value
2. Pass By Pointer

# Pass By Value

In pass by value, a copy of the actual argument is passed to the function. Changes made inside the function affect only the copy and do not modify the original variable.

## How Pass By Value Works

1. The value of the variable is copied.
2. The copied value is assigned to the formal parameter.
3. Any modification affects only the local copy.
4. The original variable remains unchanged.

## Example

```c
#include <stdio.h>

void updateValue(int number)
{
    number = 100;
}

int main()
{
    int marks = 50;

    updateValue(marks);

    printf("Marks = %d", marks);

    return 0;
}
```

### Output
Marks = 50

### Explanation

The value of `marks` is copied into `number`. Changing `number` does not affect the original variable.

# Memory Representation of Pass By Value

```Code
Main Function

marks = 50
      |
      | Copy
      ↓

updateValue()

number = 50

number = 100
```

The original variable remains unchanged.

# Example: Swapping Numbers Using Pass By Value

```c
#include <stdio.h>

void swap(int a, int b)
{
    int temp;

    temp = a;
    a = b;
    b = temp;
}

int main()
{
    int num1 = 10, num2 = 20;

    swap(num1, num2);

    printf("%d %d", num1, num2);

    return 0;
}
```

### Output
10 20

### Explanation

Only copies of the variables are swapped. The original variables remain unchanged.

# Advantages of Pass By Value

1. Original data remains safe.
2. Easy to understand and implement.
3. Avoids unintended side effects.
4. Suitable for primitive data types.

# Limitations of Pass By Value

1. Additional memory is required for copies.
2. Inefficient for large arrays and structures.
3. Cannot modify original variables.

# Pass By Pointer

Pass by pointer allows a function to access and modify the original data by passing its memory address.

Pointers are used to simulate call by reference in C.

## How Pass By Pointer Works

1. Address of the variable is passed.
2. The pointer receives that address.
3. Dereferencing accesses the original variable.
4. Changes are reflected in the calling function.

## Example

```c
#include <stdio.h>

void updateValue(int *number)
{
    *number = 100;
}

int main()
{
    int marks = 50;

    updateValue(&marks);

    printf("Marks = %d", marks);

    return 0;
}
```

### Output
Marks = 100

### Explanation

The address of `marks` is passed. The pointer accesses the original memory location and changes its value.

# Memory Representation of Pass By Pointer

```Code
Main Function

marks = 50
Address = 2000
      ↑
      |
number points here

*number = 100

marks becomes 100
```

Since both refer to the same memory location, changes are reflected in the original variable.

# Example: Swapping Numbers Using Pass By Pointer

```c
#include <stdio.h>

void swap(int *a, int *b)
{
    int temp;

    temp = *a;
    *a = *b;
    *b = temp;
}

int main()
{
    int num1 = 10, num2 = 20;

    swap(&num1, &num2);

    printf("%d %d", num1, num2);

    return 0;
}
```

### Output
20 10

### Explanation

Addresses are passed to the function. Therefore, the original variables are modified.

# Pass By Value vs Pass By Pointer

| Feature | Pass By Value | Pass By Pointer |
| --- | --- | --- |
| What is Passed | Copy of data | Address of data |
| Original Variable Modified | No | Yes |
| Memory Usage | Higher for large data | Lower |
| Performance | Slower for large structures | Faster |
| Side Effects | None | Possible |
| Suitable For | Primitive values | Arrays, structures, and large data |

# Arrays and Parameter Passing

Arrays are effectively passed using pointers because the array name represents the address of the first element.

## Example

```c
#include <stdio.h>

void modifyArray(int arr[])
{
    arr[0] = 99;
}

int main()
{
    int marks[] = {10, 20, 30};

    modifyArray(marks);

    printf("%d", marks[0]);

    return 0;
}
```

### Output
99

### Explanation

Arrays are passed by address, so modifications affect the original array.

# Important Points

- C fundamentally supports only pass by value.
- Pass by pointer is achieved by passing addresses.
- Pointers themselves are also passed by value.
- Arrays naturally behave like pointer parameters.
- Pass by pointer improves efficiency for large data structures.

# Advantages of Parameter Passing

1. Enables communication between functions.
2. Improves code modularity.
3. Supports data sharing.
4. Reduces code duplication.
5. Increases flexibility.

# Limitations

1. Pointer-based programming is more complex.
2. Incorrect pointer usage may cause errors.
3. Pass by value consumes extra memory for large data.
4. Side effects may occur when using pointers improperly.

# Summary

Parameter passing techniques determine how data is transferred between functions. In pass by value, copies of variables are passed, so modifications do not affect the original variables. In pass by pointer, memory addresses are passed, allowing functions to modify the original data. Although C officially supports only pass by value, pointers provide behavior similar to call by reference and are widely used for efficient manipulation of arrays, structures, and large data objects.

