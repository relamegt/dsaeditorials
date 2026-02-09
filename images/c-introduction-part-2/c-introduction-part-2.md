# C++ Introduction Part-2

## Operators in C++

An  **operator**  is a symbol that tells the compiler to perform a specific operation on one or more operands.

 `a + b   // + is operator, a & b are operands`

<approaches>
## Arithmetic Operators

Used for mathematical operations.

| Operator | Meaning |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| ++ | Increment |
| -- | Decrement |

 `%`  works  **only with integers** , because remainder concept doesn’t exist for floating values at hardware level.

```cpp
int a = 10, b = 3;
cout << a + b;   // 13
cout << a % b;   // 1

```

### Output
13
1

## Assignment Operators

Used to assign or update values.

| Operator | Example |
| --- | --- |
| = | x = 10 |
| += | x += 2 |
| -= | x -= 2 |
| *= | x *= 2 |
| /= | x /= 2 |

```cpp
int x = 10;
x += 5;   // x = x + 5
x *= 2;   // x = x * 2

```

## Relational Operators

Used for comparisons → return  **true (1)**  or  **false (0)** .

| Operator | Example |
| --- | --- |
| > | x > 10 |
| <= | x <= 2 |
| == | x == 2 |
| != | x != 2 |


## Logical Operators

Used to combine multiple conditions.

| Operator | Meaning |
| --- | --- |
| && | AND |
| ! | NOT |

Logical operators use  **short-circuit evaluation**  → stops as soon as result is known.

```cpp
if (age > 18 && hasID)
```

## Bitwise Operators

Operate at  **bit level**  (0 & 1).

| Operator | Meaning |
| --- | --- |
| & | AND |
| ^ | XOR |
| << | Left Shift |
| >> | Right Shift |

```cpp
5 & 3   // 101 & 011 = 001 → 1

```

## Operator Precedence

Decides  **which operation happens first** .

 `() → *, / → +, - → relational → logical` 

 **Rule** : Use brackets to avoid confusion.


## Number System & Bitwise Basics

### Binary Number System

Base-2 system

Digits:  **0 and 1** 

Computers work internally in binary

---

### 🔹 Binary → Decimal

Example:  `101` 

 `1×2² + 0×2¹ + 1×2⁰
= 4 + 0 + 1
= 5` 

---

### 🔹 Decimal → Binary

Example:  `7` 

 `7 ÷ 2 = 3 remainder 1
3 ÷ 2 = 1 remainder 1
1 ÷ 2 = 0 remainder 1
Binary = 111` 

---

### 🔹 Two’s Complement

Used to represent  **negative numbers** .

Steps:

Take binary

Invert bits

Add 1

Two’s complement allows  **same hardware**  to handle addition & subtraction.

---

### 🔹 Left Shift & Right Shift

 `5 << 1   // 5 × 2 = 10
5 >> 1   // 5 ÷ 2 = 2` 

 Left shift = multiply by 2
 Right shift = divide by 2


## Conditional Statements

### if Statement

```cpp
int a, b;
char op;
cin >> a >> op >> b;

switch(op) {
    case '+': cout << a + b; break;
    case '-': cout << a - b; break;
    case '*': cout << a * b; break;
    case '/': cout << a / b; break;
    default: cout << "Invalid";
}
```

### 

### 

### if–else

### 

```cpp
result = (a > b) ? a : b;
```

### 

### 

### else if Ladder

```cpp
if (marks >= 40)
    cout << "Pass";
else
    cout << "Fail";
```

### 

### 

### 

### Ternary Operator

### 

### 

### 

```cpp
if (age >= 18) {
    cout << "Eligible";
}
```

### 

### 

### 

### switch Statement

    

    switch( choice ){

    case 1: cout << "Add"; break;

    case 2: cout << "Subtract"; break;

    default: cout << "Invalid";

    }


## Functions

A  **function**  is a reusable block of code.

### Function Syntax

```cpp
int add(int a, int b) {
    return a + b;
}

int result = add(3, 4); // calling
```

### 🔹 Declaration vs Definition

 **Declaration**  → function prototype

 **Definition**  → function body

---

### 🔹 Parameters & Arguments

Parameters → variables in function

Arguments → actual values passed

### Types of Functions

| Type |
| --- |
| No parameters, no return |
| Parameters, no return |
| No parameters, return |
| Parameters and return |

### Function Overloading

Same function name, different parameters.

 `int sum(int a, int b);`  `float sum(float a, float b);`  

### 🔹 Scope

 **Local**  → inside function

 **Global**  → outside all functions

 ***Prefer local → safer & cleaner.***


## Pointers & References

🔹 Memory Basics

Variables live in  **RAM** 

Each has an  **address** 

### **Address Operator  `&`**

```cpp
int a = 10;
cout << &a;
```

# 

### Pointer Declaration

 `int *ptr = &a;` 

 `ptr`  stores address

 `*ptr`  accesses value

### Dereference Operator  `*`

 `*ptr = 20;  // modifies a` 

### Types of Pointers

| Pointer | Meaning |
| --- | --- |
| Wild | Uninitialized |
| Null | Points to nothing |
| Dangling | Memory freed |
| Void | Generic pointer |

int *p = NULL;

### Reference Variables

 `int a = 10;`  `int &b = a;` 

Alias of same memory

No extra storage


## Parameter Passing

**Pass by Value** 

 `void f(int x)` 

No change in original.

 **Pass by Reference** 

 `void f(int &x)` 

Original changes.

 **Pass by Pointer** 

 `void f(int *x)` 

 ***Use reference → safer than pointer.***


</approaches>




