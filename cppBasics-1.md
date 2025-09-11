<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# C++ Basics - 1

[Introduction]()
[Data Types]()
[Operators]()
[Conditional Statements]()
Introduction
What is C++?
C++ is a powerful, high-performance programming language widely used across various domains, including game development, system programming, embedded systems, and more. It is an extension of the C programming language with added features like object-oriented programming (OOP), making it versatile for both low-level and high-level programming tasks.
C++ is a popular choice in technical interviews due to its efficiency and control over system resources, making it a valuable skill for software developers.
C++ Basic Syntax
CPP
Breakdown of the Syntax:

\#include <iostream>
: This is a standard library header file that provides input and output functionalities, such as printing to the console (
cout
) and reading from the console (
cin
).

int main() { ... }
: The
main()
function is the entry point of every C++ program. Execution begins here.

return 0;
: This indicates that the program has executed successfully. A non-zero value typically signifies an error.

Key Points to Remember:
Semicolon (
;
): Every statement in C++ must end with a semicolon.

Curly Braces
{}
: Always ensure that the
main()
function (and other blocks of code) are properly closed with a closing curly brace
}
.

endl
: This is used to insert a newline character, moving the cursor to the next line.

using namespace std;
: This directive allows you to use standard library functions (like
cout
and
cin
) without prefixing them with
std::
.

\#include <bits/stdc++.h>
: This is a convenience header that includes almost all standard C++ libraries. It’s commonly used in competitive programming to save time.

Comments in C++
Single-line Comment:
CPP
Multi-line Comment:
CPP
Hello World Program
CPP

cout
: This is used to print output to the console.

<<
: The insertion operator is used to send data to the output stream.

endl
: Inserts a newline after the output.

Input and Output in C++
Basic Input and Output
CPP

cin
: Used to take input from the user.

>>
: The extraction operator is used to read data from the input stream.

String Input
CPP
Sentence Input
Using
cin
:

cin
reads only the first word from the input.

CPP
Using
getline()
:

To read an entire sentence (including spaces), use
getline()
.

CPP
Example: Addition of Two Numbers
CPP
 
Data Types in C++
C++ supports various data types to store different kinds of data. Here are some commonly used ones:
Data TypeSyntax ExampleDescription
int
int myVariable = 42;
Stores integer values.
float
float myFloat = 3.14;
Stores single-precision floating-point numbers.
double
double myDouble = 3.14159265359;
Stores double-precision floating-point numbers.
char
char myChar = 'A';
Stores a single character.
std::string
std::string myString = "Hello";
Stores a sequence of characters (strings).
long
long al = 1234567890L;
Stores larger integer values.
long long
long long all = 123456789012345LL;
Stores very large integer values.
bool
bool booleanValue = true;
Stores 
true
 or 
false
 values.
Example: Data Types and Sizes
CPP
 
 
Expand
Operators in C++
Operators are symbols that perform operations on variables and values.
C++ supports various types of operators, including logical, arithmetic, relational, and assignment operators.
Logical Operators
Logical operators are used to combine multiple conditions or to negate a condition. They return a boolean value (
true
or
false
).

AND (
\&\&
): Returns
true
if both conditions are true.

OR (
||
): Returns
true
if at least one condition is true.

NOT (
!
): Reverses the logical state of the condition (true becomes false, and vice versa).

Example:
CPP
 
 
Expand
Arithmetic Operators
Arithmetic operators are used to perform mathematical operations like addition, subtraction, multiplication, division, and modulus.
Addition (
+
): Adds two operands.

Subtraction (
-
): Subtracts the second operand from the first.

Multiplication (
*
): Multiplies two operands.

Division (
/
): Divides the first operand by the second.

Modulus (
%
): Returns the remainder of division.

Example:
CPP
 
 
Expand
Relational Operators
Relational operators are used to compare two values or expressions. They return a boolean value (
true
or
false
).

Greater than (
>
): Returns
true
if the left operand is greater than the right.

Less than (
<
): Returns
true
if the left operand is less than the right.

Equal to (
==
): Returns
true
if both operands are equal.

Not equal to (
!=
): Returns
true
if the operands are not equal.

Greater than or equal (
>=
): Returns
true
if the left operand is greater than or equal to the right.

Less than or equal (
<=
): Returns
true
if the left operand is less than or equal to the right.

Example:
CPP
 
 
Expand
Assignment Operators
Assignment operators are used to assign values to variables. They can also perform operations while assigning values.
Assignment (
=
): Assigns the value of the right operand to the left operand.

Add and assign (
+=
): Adds the right operand to the left operand and assigns the result to the left operand.

Subtract and assign (
-=
): Subtracts the right operand from the left operand and assigns the result to the left operand.

Multiply and assign (
*=
): Multiplies the left operand by the right operand and assigns the result to the left operand.

Divide and assign (
/=
): Divides the left operand by the right operand and assigns the result to the left operand.

Modulus and assign (
%=
): Takes the modulus of the left operand by the right operand and assigns the result to the left operand.

Example:
CPP
 
 
Expand
Conditional Statements
Control statements in programming are instructions that tell the computer what to do based on certain conditions.
They allow the program to make decisions. If a condition is true, the program executes one block of code; if it’s false, it executes another block.
Following are some of the decision-making statements in C++:
if Statement
The
if
statement is used to execute a block of code only if a specified condition is true. If the condition is false, the block of code is skipped.

Syntax:
CPP
 
The
if
statement checks a condition, which evaluates to a boolean value (
true
or
false
).

If the condition is
true
, the code inside the
if
block is executed.

If the condition is
false
, the code inside the
if
block is skipped.

Example:
CPP
 
Expand
if-else Statement
The
if-else
statement is used to execute one block of code if the condition is true and another block if the condition is false.

Syntax:
CPP
 
If the condition is
true
, the code inside the
if
block is executed.

If the condition is
false
, the code inside the
else
block is executed.

Example:
CPP
 
 
Expand
Nested if-else Statements
A nested
if-else
statement is an
if-else
statement inside another
if-else
statement. It is used when you need to check multiple conditions in a hierarchical manner.

Syntax:
CPP
 
Expand
The outer
if-else
statement is evaluated first.

If the outer condition is
true
, the inner
if-else
statement is evaluated.

This allows for more complex decision-making.
Example:
CPP
 
 
Expand
Explanation:
The outer
if
checks if the age is 18 or older.

If the age is 18 or older, the inner
if
checks if the user has a driving license.

If the user has a license, they are eligible to drive.
If the user does not have a license, they are prompted to get one.
If the age is less than 18, the program outputs that the user is not old enough to drive.
if-else-if Ladder
The
if-else-if
ladder is used when there are multiple conditions to check.

The program evaluates each condition sequentially, and when a true condition is found, the corresponding block of code is executed. If none of the conditions are true, the
else
block (if present) is executed.

Syntax:
CPP
 
 
Expand
Example:
CPP
 
 
Expand
Switch Statement
The
switch
statement is used to select one of many code blocks to execute based on the value of a variable.

It provides a cleaner alternative to a series of
if-else-if
statements.

Syntax:
CPP
 
 
Expand
The
expression
is evaluated once, and its value is compared with the values of each
case
.

If a match is found, the corresponding block of code is executed.
The
break
statement is used to exit the
switch
block after a match is found.

The
default
case is optional and is executed if no match is found.

Example:
CPP
 
 
Expand

create editorial for this matter as per the below format the code examples should be in cpp,java,python give simple and full codes
<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Linear Search Algorithm

Linear search is one of the simplest searching algorithms that sequentially checks each element in a collection until the target element is found or the entire collection has been searched.

## Brute Force Approach

The most straightforward approach to implement linear search is to traverse the entire array from beginning to end, comparing each element with the target value.

### Algorithm Explanation

1. Start from the first element of the array
2. Compare the current element with the target value
3. If they match, return the index
4. If they don't match, move to the next element
5. Repeat until found or end of array is reached
6. Return -1 if element is not found

### Implementation

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == target) {
                return i;
            }
        }
        return -1;
    }
};
```

```java
class Solution {
    public int search(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                return i;
            }
        }
        return -1;
    }
}
```

```javascript
function search(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === target) {
            return i;
        }
    }
    return -1;
}
```

```python
def search(nums, target):
    for i in range(len(nums)):
        if nums[i] == target:
            return i
    return -1
```


### Time Complexity

O(n) where n is the number of elements in the array. In worst case, we might have to check all elements.

### Space Complexity

O(1) as we only use a constant amount of extra space for the loop variable.

## Optimized Approach

For linear search, there isn't much room for optimization in terms of time complexity, but we can make small improvements.

### Early Termination with Sentinel

We can add the target element at the end of the array to avoid boundary checking in every iteration.

```cpp
class Solution {
public:
    int searchWithSentinel(vector<int>& nums, int target) {
        int n = nums.size();
        if (n == 0) return -1;
        
        // Store the last element
        int last = nums[n-1];
        
        // Put target at the end
        nums[n-1] = target;
        
        int i = 0;
        while (nums[i] != target) {
            i++;
        }
        
        // Restore the last element
        nums[n-1] = last;
        
        // Check if target was found before the last element
        // or if the last element was the target
        if (i < n-1 || nums[n-1] == target) {
            return i;
        }
        
        return -1;
    }
};
```

```java
class Solution {
    public int searchWithSentinel(int[] nums, int target) {
        int n = nums.length;
        if (n == 0) return -1;
        
        // Store the last element
        int last = nums[n-1];
        
        // Put target at the end
        nums[n-1] = target;
        
        int i = 0;
        while (nums[i] != target) {
            i++;
        }
        
        // Restore the last element
        nums[n-1] = last;
        
        // Check if target was found before the last element
        // or if the last element was the target
        if (i < n-1 || nums[n-1] == target) {
            return i;
        }
        
        return -1;
    }
}
```

```javascript
function searchWithSentinel(nums, target) {
    const n = nums.length;
    if (n === 0) return -1;
    
    // Store the last element
    const last = nums[n-1];
    
    // Put target at the end
    nums[n-1] = target;
    
    let i = 0;
    while (nums[i] !== target) {
        i++;
    }
    
    // Restore the last element
    nums[n-1] = last;
    
    // Check if target was found before the last element
    // or if the last element was the target
    if (i < n-1 || nums[n-1] === target) {
        return i;
    }
    
    return -1;
}
```

```python
def search_with_sentinel(nums, target):
    n = len(nums)
    if n == 0:
        return -1
    
    # Store the last element
    last = nums[n-1]
    
    # Put target at the end
    nums[n-1] = target
    
    i = 0
    while nums[i] != target:
        i += 1
    
    # Restore the last element
    nums[n-1] = last
    
    # Check if target was found before the last element
    # or if the last element was the target
    if i < n-1 or nums[n-1] == target:
        return i
    
    return -1
```


### Time Complexity

O(n) - Same as brute force but with slightly better constants due to reduced boundary checking.

### Space Complexity

O(1) - Still constant space complexity.

## Better Approach

For unsorted arrays, linear search is optimal. However, if we can sort the array first, we can use binary search for better performance.

### Pre-sorting + Binary Search

```cpp
class Solution {
public:
    int searchInSorted(vector<int>& nums, int target) {
        // This assumes array is already sorted
        int left = 0, right = nums.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
};
```

```java
class Solution {
    public int searchInSorted(int[] nums, int target) {
        // This assumes array is already sorted
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
}
```

```javascript
function searchInSorted(nums, target) {
    // This assumes array is already sorted
    let left = 0, right = nums.length - 1;
    
    while (left <= right) {
        const mid = Math.floor(left + (right - left) / 2);
        
        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;
}
```

```python
def search_in_sorted(nums, target):
    # This assumes array is already sorted
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```


### Time Complexity

O(log n) for searching in sorted array, but O(n log n) if we need to sort first.

### Space Complexity

O(1) for iterative binary search, O(log n) for recursive approach due to call stack.
Special thanks to [Neerav Sethi](https://takeUforward.org) for contributing to this article on takeUforward.

```

<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# C++ Basics - Complete Programming Guide

C++ is a powerful, high-performance programming language that serves as an extension of C with object-oriented programming capabilities, making it essential for system programming, game development, and competitive programming.

## Basic Syntax and Structure

The fundamental structure of a C++ program consists of header inclusions, namespace declarations, and the main function as the entry point.

### Essential Components

1. **Header Files**: Include necessary libraries using `#include`
2. **Namespace**: Use `using namespace std;` for standard library access
3. **Main Function**: Program execution begins with `int main()`
4. **Return Statement**: `return 0;` indicates successful execution

### Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

```python
print("Hello, World!")
```


## Data Types and Variables

C++ provides various built-in data types to handle different kinds of information efficiently.

### Fundamental Data Types

C++ supports integers, floating-point numbers, characters, booleans, and strings with specific memory allocations and value ranges.

### Implementation

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // Integer types
    int age = 25;
    long population = 1234567890L;
    long long bigNumber = 123456789012345LL;
    
    // Floating point types
    float price = 19.99f;
    double pi = 3.14159265359;
    
    // Character and string types
    char grade = 'A';
    string name = "John Doe";
    
    // Boolean type
    bool isActive = true;
    
    cout << "Age: " << age << endl;
    cout << "Name: " << name << endl;
    cout << "Grade: " << grade << endl;
    cout << "Active: " << isActive << endl;
    
    return 0;
}
```

```java
public class DataTypes {
    public static void main(String[] args) {
        // Integer types
        int age = 25;
        long population = 1234567890L;
        
        // Floating point types
        float price = 19.99f;
        double pi = 3.14159265359;
        
        // Character and string types
        char grade = 'A';
        String name = "John Doe";
        
        // Boolean type
        boolean isActive = true;
        
        System.out.println("Age: " + age);
        System.out.println("Name: " + name);
        System.out.println("Grade: " + grade);
        System.out.println("Active: " + isActive);
    }
}
```

```python
# Python is dynamically typed
age = 25
population = 1234567890
price = 19.99
pi = 3.14159265359
grade = 'A'
name = "John Doe"
is_active = True

print(f"Age: {age}")
print(f"Name: {name}")
print(f"Grade: {grade}")
print(f"Active: {is_active}")
```


## Input and Output Operations

Input and output operations form the backbone of interactive programming, allowing programs to communicate with users.

### Basic I/O Operations

C++ uses `cin` for input and `cout` for output, with special handling required for string inputs containing spaces.

### Implementation

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string firstName, lastName, fullName;
    int age;
    
    cout << "Enter your first name: ";
    cin >> firstName;
    
    cout << "Enter your age: ";
    cin >> age;
    
    // Clear the input buffer
    cin.ignore();
    
    cout << "Enter your full name: ";
    getline(cin, fullName);
    
    cout << "\nHello " << firstName << "!" << endl;
    cout << "You are " << age << " years old." << endl;
    cout << "Full name: " << fullName << endl;
    
    return 0;
}
```

```java
import java.util.Scanner;

public class InputOutput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your first name: ");
        String firstName = scanner.next();
        
        System.out.print("Enter your age: ");
        int age = scanner.nextInt();
        
        // Clear the buffer
        scanner.nextLine();
        
        System.out.print("Enter your full name: ");
        String fullName = scanner.nextLine();
        
        System.out.println("\nHello " + firstName + "!");
        System.out.println("You are " + age + " years old.");
        System.out.println("Full name: " + fullName);
        
        scanner.close();
    }
}
```

```python
first_name = input("Enter your first name: ")
age = int(input("Enter your age: "))
full_name = input("Enter your full name: ")

print(f"\nHello {first_name}!")
print(f"You are {age} years old.")
print(f"Full name: {full_name}")
```


## Operators in C++

Operators are symbols that perform specific operations on variables and values, essential for mathematical calculations and logical decisions.

### Arithmetic Operations

Basic mathematical operations including addition, subtraction, multiplication, division, and modulus for remainder calculation.

### Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 15, b = 4;
    
    cout << "Arithmetic Operations:" << endl;
    cout << "a + b = " << (a + b) << endl;
    cout << "a - b = " << (a - b) << endl;
    cout << "a * b = " << (a * b) << endl;
    cout << "a / b = " << (a / b) << endl;
    cout << "a % b = " << (a % b) << endl;
    
    // Relational operations
    cout << "\nRelational Operations:" << endl;
    cout << "a > b: " << (a > b) << endl;
    cout << "a < b: " << (a < b) << endl;
    cout << "a == b: " << (a == b) << endl;
    cout << "a != b: " << (a != b) << endl;
    
    // Logical operations
    bool x = true, y = false;
    cout << "\nLogical Operations:" << endl;
    cout << "x && y: " << (x && y) << endl;
    cout << "x || y: " << (x || y) << endl;
    cout << "!x: " << (!x) << endl;
    
    return 0;
}
```

```java
public class Operators {
    public static void main(String[] args) {
        int a = 15, b = 4;
        
        System.out.println("Arithmetic Operations:");
        System.out.println("a + b = " + (a + b));
        System.out.println("a - b = " + (a - b));
        System.out.println("a * b = " + (a * b));
        System.out.println("a / b = " + (a / b));
        System.out.println("a % b = " + (a % b));
        
        // Relational operations
        System.out.println("\nRelational Operations:");
        System.out.println("a > b: " + (a > b));
        System.out.println("a < b: " + (a < b));
        System.out.println("a == b: " + (a == b));
        System.out.println("a != b: " + (a != b));
        
        // Logical operations
        boolean x = true, y = false;
        System.out.println("\nLogical Operations:");
        System.out.println("x && y: " + (x && y));
        System.out.println("x || y: " + (x || y));
        System.out.println("!x: " + (!x));
    }
}
```

```python
a, b = 15, 4

print("Arithmetic Operations:")
print(f"a + b = {a + b}")
print(f"a - b = {a - b}")
print(f"a * b = {a * b}")
print(f"a / b = {a / b}")
print(f"a % b = {a % b}")

# Relational operations
print("\nRelational Operations:")
print(f"a > b: {a > b}")
print(f"a < b: {a < b}")
print(f"a == b: {a == b}")
print(f"a != b: {a != b}")

# Logical operations
x, y = True, False
print("\nLogical Operations:")
print(f"x and y: {x and y}")
print(f"x or y: {x or y}")
print(f"not x: {not x}")
```


## Conditional Statements

Conditional statements enable programs to make decisions and execute different code blocks based on specific conditions.

### Decision Making Structures

C++ provides various conditional constructs including if, if-else, nested conditions, if-else-if ladders, and switch statements for comprehensive decision making.

### Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    cout << "Enter your score (0-100): ";
    cin >> score;
    
    // if-else-if ladder
    if (score >= 90) {
        cout << "Grade: A+" << endl;
    } else if (score >= 80) {
        cout << "Grade: A" << endl;
    } else if (score >= 70) {
        cout << "Grade: B" << endl;
    } else if (score >= 60) {
        cout << "Grade: C" << endl;
    } else if (score >= 50) {
        cout << "Grade: D" << endl;
    } else {
        cout << "Grade: F" << endl;
    }
    
    // Switch statement example
    int choice;
    cout << "\nSelect operation (1-4): ";
    cin >> choice;
    
    switch (choice) {
        case 1:
            cout << "Addition selected" << endl;
            break;
        case 2:
            cout << "Subtraction selected" << endl;
            break;
        case 3:
            cout << "Multiplication selected" << endl;
            break;
        case 4:
            cout << "Division selected" << endl;
            break;
        default:
            cout << "Invalid choice" << endl;
    }
    
    return 0;
}
```

```java
import java.util.Scanner;

public class ConditionalStatements {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your score (0-100): ");
        int score = scanner.nextInt();
        
        // if-else-if ladder
        if (score >= 90) {
            System.out.println("Grade: A+");
        } else if (score >= 80) {
            System.out.println("Grade: A");
        } else if (score >= 70) {
            System.out.println("Grade: B");
        } else if (score >= 60) {
            System.out.println("Grade: C");
        } else if (score >= 50) {
            System.out.println("Grade: D");
        } else {
            System.out.println("Grade: F");
        }
        
        // Switch statement example
        System.out.print("\nSelect operation (1-4): ");
        int choice = scanner.nextInt();
        
        switch (choice) {
            case 1:
                System.out.println("Addition selected");
                break;
            case 2:
                System.out.println("Subtraction selected");
                break;
            case 3:
                System.out.println("Multiplication selected");
                break;
            case 4:
                System.out.println("Division selected");
                break;
            default:
                System.out.println("Invalid choice");
        }
        
        scanner.close();
    }
}
```

```python
score = int(input("Enter your score (0-100): "))

# if-elif-else ladder
if score >= 90:
    print("Grade: A+")
elif score >= 80:
    print("Grade: A")
elif score >= 70:
    print("Grade: B")
elif score >= 60:
    print("Grade: C")
elif score >= 50:
    print("Grade: D")
else:
    print("Grade: F")

# Switch-like statement using dictionary
choice = int(input("\nSelect operation (1-4): "))

operations = {
    1: "Addition selected",
    2: "Subtraction selected", 
    3: "Multiplication selected",
    4: "Division selected"
}

print(operations.get(choice, "Invalid choice"))
```


## Complete Example Program

A comprehensive program demonstrating all the covered concepts working together in a practical application.

### Calculator Application

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string userName;
    int num1, num2, choice;
    char continueChoice;
    
    cout << "=== Welcome to C++ Calculator ===" << endl;
    cout << "Enter your name: ";
    getline(cin, userName);
    
    do {
        cout << "\nHello " << userName << "!" << endl;
        cout << "Enter first number: ";
        cin >> num1;
        cout << "Enter second number: ";
        cin >> num2;
        
        cout << "\nSelect operation:" << endl;
        cout << "1. Addition (+)" << endl;
        cout << "2. Subtraction (-)" << endl;
        cout << "3. Multiplication (*)" << endl;
        cout << "4. Division (/)" << endl;
        cout << "5. Modulus (%)" << endl;
        cout << "Enter your choice (1-5): ";
        cin >> choice;
        
        int result;
        bool validOperation = true;
        
        switch (choice) {
            case 1:
                result = num1 + num2;
                cout << num1 << " + " << num2 << " = " << result << endl;
                break;
            case 2:
                result = num1 - num2;
                cout << num1 << " - " << num2 << " = " << result << endl;
                break;
            case 3:
                result = num1 * num2;
                cout << num1 << " * " << num2 << " = " << result << endl;
                break;
            case 4:
                if (num2 != 0) {
                    result = num1 / num2;
                    cout << num1 << " / " << num2 << " = " << result << endl;
                } else {
                    cout << "Error: Division by zero!" << endl;
                    validOperation = false;
                }
                break;
            case 5:
                if (num2 != 0) {
                    result = num1 % num2;
                    cout << num1 << " % " << num2 << " = " << result << endl;
                } else {
                    cout << "Error: Modulus by zero!" << endl;
                    validOperation = false;
                }
                break;
            default:
                cout << "Invalid choice!" << endl;
                validOperation = false;
        }
        
        if (validOperation && choice >= 1 && choice <= 5) {
            if (result > 0) {
                cout << "Result is positive." << endl;
            } else if (result < 0) {
                cout << "Result is negative." << endl;
            } else {
                cout << "Result is zero." << endl;
            }
        }
        
        cout << "\nDo you want to perform another calculation? (y/n): ";
        cin >> continueChoice;
        
    } while (continueChoice == 'y' || continueChoice == 'Y');
    
    cout << "Thank you for using the calculator, " << userName << "!" << endl;
    return 0;
}
```

```java
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String userName;
        int num1, num2, choice;
        char continueChoice;
        
        System.out.println("=== Welcome to Java Calculator ===");
        System.out.print("Enter your name: ");
        userName = scanner.nextLine();
        
        do {
            System.out.println("\nHello " + userName + "!");
            System.out.print("Enter first number: ");
            num1 = scanner.nextInt();
            System.out.print("Enter second number: ");
            num2 = scanner.nextInt();
            
            System.out.println("\nSelect operation:");
            System.out.println("1. Addition (+)");
            System.out.println("2. Subtraction (-)");
            System.out.println("3. Multiplication (*)");
            System.out.println("4. Division (/)");
            System.out.println("5. Modulus (%)");
            System.out.print("Enter your choice (1-5): ");
            choice = scanner.nextInt();
            
            int result = 0;
            boolean validOperation = true;
            
            switch (choice) {
                case 1:
                    result = num1 + num2;
                    System.out.println(num1 + " + " + num2 + " = " + result);
                    break;
                case 2:
                    result = num1 - num2;
                    System.out.println(num1 + " - " + num2 + " = " + result);
                    break;
                case 3:
                    result = num1 * num2;
                    System.out.println(num1 + " * " + num2 + " = " + result);
                    break;
                case 4:
                    if (num2 != 0) {
                        result = num1 / num2;
                        System.out.println(num1 + " / " + num2 + " = " + result);
                    } else {
                        System.out.println("Error: Division by zero!");
                        validOperation = false;
                    }
                    break;
                case 5:
                    if (num2 != 0) {
                        result = num1 % num2;
                        System.out.println(num1 + " % " + num2 + " = " + result);
                    } else {
                        System.out.println("Error: Modulus by zero!");
                        validOperation = false;
                    }
                    break;
                default:
                    System.out.println("Invalid choice!");
                    validOperation = false;
            }
            
            if (validOperation && choice >= 1 && choice <= 5) {
                if (result > 0) {
                    System.out.println("Result is positive.");
                } else if (result < 0) {
                    System.out.println("Result is negative.");
                } else {
                    System.out.println("Result is zero.");
                }
            }
            
            System.out.print("\nDo you want to perform another calculation? (y/n): ");
            continueChoice = scanner.next().charAt(0);
            
        } while (continueChoice == 'y' || continueChoice == 'Y');
        
        System.out.println("Thank you for using the calculator, " + userName + "!");
        scanner.close();
    }
}
```

```python
def main():
    print("=== Welcome to Python Calculator ===")
    user_name = input("Enter your name: ")
    
    while True:
        print(f"\nHello {user_name}!")
        num1 = int(input("Enter first number: "))
        num2 = int(input("Enter second number: "))
        
        print("\nSelect operation:")
        print("1. Addition (+)")
        print("2. Subtraction (-)")
        print("3. Multiplication (*)")
        print("4. Division (/)")
        print("5. Modulus (%)")
        
        choice = int(input("Enter your choice (1-5): "))
        
        valid_operation = True
        result = 0
        
        if choice == 1:
            result = num1 + num2
            print(f"{num1} + {num2} = {result}")
        elif choice == 2:
            result = num1 - num2
            print(f"{num1} - {num2} = {result}")
        elif choice == 3:
            result = num1 * num2
            print(f"{num1} * {num2} = {result}")
        elif choice == 4:
            if num2 != 0:
                result = num1 // num2  # Integer division
                print(f"{num1} / {num2} = {result}")
            else:
                print("Error: Division by zero!")
                valid_operation = False
        elif choice == 5:
            if num2 != 0:
                result = num1 % num2
                print(f"{num1} % {num2} = {result}")
            else:
                print("Error: Modulus by zero!")
                valid_operation = False
        else:
            print("Invalid choice!")
            valid_operation = False
        
        if valid_operation and 1 <= choice <= 5:
            if result > 0:
                print("Result is positive.")
            elif result < 0:
                print("Result is negative.")
            else:
                print("Result is zero.")
        
        continue_choice = input("\nDo you want to perform another calculation? (y/n): ")
        if continue_choice.lower() != 'y':
            break
    
    print(f"Thank you for using the calculator, {user_name}!")

if __name__ == "__main__":
    main()
```

Special thanks to the C++ community for contributing to programming education and making these concepts accessible to learners worldwide.

