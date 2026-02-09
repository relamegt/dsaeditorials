# Linear Search-2

## 

### `code`

```cpp
cpp
```

```cpp
cpp2
```

Uses insertion operator  
Uses insertion opera `code`  tor  " `*<<"*` 
Sends data to output stream

Sends data to output stream

```cpp
cpp
```

## 1. Arithmetic Operators

These are used to perform basic mathematical operations.

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| + | Addition | Adds two operands | a + b |
| - | Subtraction | Subtracts second from first | a - b |
| * | Multiplication | Multiplies two operands | a * b |
| / | Division | Divides numerator by denominator | b / a |
| % | Modulo | Returns the remainder | b % a |

 **Code Example:** 

C++ `int a = 10, b = 3;
cout << "Addition: " << (a + b) << endl;    // 13
cout << "Remainder: " << (a % b) << endl;   // 1` 

---

## 2. Relational (Comparison) Operators

These operators compare two values and return a boolean result:  `true`  (1) or  `false`  (0).

 **`==`** : Equal to

 **`!=`** : Not equal to

 **`>`**  /  **`<`** : Greater than / Less than

 **`>=`**  /  **`<=`** : Greater/Less than or equal to

 **Code Example:** 

C++ `int x = 5, y = 10;
if (x < y) {
    cout << "x is smaller than y";
}` 

---

## 3. Logical Operators

Used to combine two or more conditions or complement the evaluation of the original condition.

![Editorial Image](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcRjsnI5uYV05bTzZeZ-J2ay5T0ABMSHcUg3jYii_AbJAgJq3lM0UDWIwpQ0yYFRcUUXg-o0pBMsjmO265sl8HWxZriPLscvwfA4_uGDSyjx25ZMlso)

Shutterstock

 **`&&`  (Logical AND):**  Returns true if both statements are true.

 **`||`  (Logical OR):**  Returns true if one of the statements is true.

 **`!`  (Logical NOT):**  Reverses the result (true becomes false).

 **Code Example:** 

C++ `bool isSunny = true;
bool isWarm = false;

if (isSunny && !isWarm) {
    cout << "It's a crisp, clear day!";
}` 

---

## 4. Increment and Decrement Operators

These are shorthand for increasing or decreasing a value by 1.

 **Prefix ( `++x` ):**  Increments the value, then returns it.

 **Postfix ( `x++` ):**  Returns the current value, then increments it.

 **Code Example:** 

C++ `int count = 5;
cout << ++count; // Outputs 6
cout << count++; // Outputs 6, but 'count' is now 7` 

---

## 5. Assignment Operators

Used to assign values to variables. You'll often see "Compound Assignments" which combine math and assignment.

 **`=`** : Simple assignment ( `a = b` )

 **`+=`** : Add and assign ( `a = a + b` )

 **`*=`** : Multiply and assign ( `a = a * b` )

---

## 6. Bitwise Operators (Advanced)

These perform operations on the binary representations of numbers (at the bit level).

 **`&`** : Bitwise AND

 **`|`** : Bitwise OR

 **`^`** : Bitwise XOR

 **`<<`  /  `>>`** : Left shift / Right shift

### 

### ![Editorial Image](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search-2/1770628857357-Screenshot_2026-01-18_152703.png)

Uses extraction operator  " **>> *"  `code`*** 

Reads from keyboard → memory

📌  **Stream concept** 

Data flows like water:

Keyboard → Memory ( `cin` )

Memory → Screen ( `cout` )

 `code`  

 `code testing don`  

```cpp
cpp
```

### Naming Conventions

| Entity | Style |
| --- | --- |
| Variables | camelCase |
| Functions | camelCase |
| Classes | PascalCase |

### Keywords vs Identifiers

| Keywords | Identifiers |
| --- | --- |
| Reserved | User-defined |
| Define behavior | Name entities |
| int, while | count, sum |

---

```cpp
cpp
```

### Output
no uptu

# Time Complexity
1

# Space Complexity
1

<carousel>
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search-2/1770628934689-4.jpeg" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search-2/1770628936651-3.jpeg" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search-2/1770628937893-2.jpeg" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search-2/1770628939391-1.jpeg" />
</carousel>

## 1. What is Linear Search?

 **Linear Search**  (also called  **Sequential Search** ) is a simple searching algorithm that checks  **each element one by one**  in a list until:

the target element is found, or

the list ends.

It works on  **both sorted and unsorted arrays** .

## 2. Structure of a C++ Program

A basic C++ program has the following structure:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```
```python
pythong
```

### Output
hello world

Explanation of Parts

| Part | Purpose |
| --- | --- |
| #include <iostream> | Includes input-output library |
| using namespace std; | Allows use of standard names |
| int main() | Starting point of program |
| { } | Body of the program |
| return 0; | Ends the program |

### 

---

## 2. How Linear Search Works

Start from the first element.

Compare the current element with the key.

If it matches → return the index.

If not → move to the next element.

If the end is reached → element not found

---

## 3. Algorithm (Steps)

 **Input:**  Array  `A` , size  `n` , search key  `x` 

 *for i = 0 to n-1
    if A[i] == x
        return i
return -1* 

---

## 4. Time & Space Complexity

| Case | Time Complexity |
| --- | --- |
| Best Case | O(1) |
| Average Case | O(n) |
| Worst Case | O(n) |

### **Space Complexity:**  O(1)

---

## 5. Advantages & Disadvantages

### Advantages

Very simple to implement

Works on unsorted data

No extra memory required

### Disadvantages

Slow for large datasets

Inefficient compared to binary search

---

## Below is Slide Play

<carousel>
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483224034-Slide1.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483225252-Slide2.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483226569-Slide3.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483228002-Slide4.JPG" />
<img src="https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/linear-search/1768483229015-Slide5.JPG" />
</carousel>

<approaches>
## Hash Map

Explanation of Parts

| Part | Purpose |
| --- | --- |
| #include <iostream> | Includes input-output library |
| using namespace std; | Allows use of standard names |
| int main() | Starting point of program |
| { } | Body of the program |
| return 0; | Ends the program |

```cpp
cpp inline
```

```cpp
hey there cpp
```
```python
Pythong
```

### Output
no outputs

# Time Complexity
no tc

# Space Complexity
no sc

testing this blocl

```cpp
just cpp
```

### Output
cpp output

# Time Complexity
no tc

# Space Complexity
no sc

## Brute Force



## Two_Pointer



</approaches>



### *Special Thanks to  [Mohit](https://www.linkedin.com/authwall?trk=bf&trkInfo=AQGCnCKArgzSgAAAAZxBQR_orGjE4L1ubsxoZW092aNFU6LPUiIysFN76DE2hBpfAPfGO8-4i9Txj_U1RuBhukmbiVEoXOY9GANnfoEHCZ7CVId6r2T8EBUSOIkA5uuJsFtpOe4=&original_referer=&sessionRedirect=https%3A%2F%2Fwww.linkedin.com%2Fin%2Fmohit-ch%2F)*
