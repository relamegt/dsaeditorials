# C++ Identifiers

In C++, identifiers are user-defined names used to uniquely identify various program elements such as variables, functions, classes, structures, arrays, and other entities. These names help programmers reference and manipulate these elements throughout the program.

For example:

`// Creating a variable` 

`int age = 20;`

`// Creating a function`

`void displayMessage() {}`

In the above code, **`age`** and **`displayMessage`** are identifiers. In general, any name created by the programmer to represent a program component is considered an identifier.

Identifiers play a crucial role in making code readable, organized, and easy to maintain, as they provide meaningful names for different entities within a program.

**Rules for Naming an Identifier**

An identifier in C++ must follow certain naming conventions to be considered valid. The following rules should be observed when creating identifiers:

1. An identifier can contain letters (`A–Z`, `a–z`), digits (`0–9`), and the underscore (`_`) character.
2. The first character of an identifier must be a letter or an underscore; it cannot begin with a digit.
3. Identifiers are case-sensitive, meaning `count`, `Count`, and `COUNT` are treated as different names.
4. Reserved keywords such as `int`, `while`, `return`, and `class` cannot be used as identifiers.
5. Special characters such as `@`, `#`, `%`, `&`, and `!` are not allowed.
6. Spaces are not permitted within an identifier name.
7. Identifiers should be meaningful and descriptive to improve code readability.

**Valid Identifiers:**

- `studentName`
- `_count`
- `totalMarks`
- `num1`

**Invalid Identifiers:**

- `2value` (starts with a digit)
- `total marks` (contains a space)
- `class` (reserved keyword)
- `price@item` (contains a special character)

It is important to note that C++ is a **case-sensitive** programming language. As a result, identifiers that differ only in letter casing are considered distinct. For example, `Num`, `num`, and `NUM` are treated as three separate identifiers by the compiler.

The following illustrations present examples of both **valid** and **invalid** identifiers in C++, helping to clarify the naming rules and conventions that programmers must follow.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-identifiers/1780989239959-ChatGPT_Image_Jun_9%2C_2026%2C_12_43_39_PM.png)

The following example demonstrates the use of identifiers in different parts of a C++ program. Identifiers are used to name a class (`Car`), a function (`getSum`), variables (`studentAge`, `accountBalance`, `student_Name`), and other program elements. All identifiers follow the standard naming rules of C++ and help make the code more readable and meaningful.

```cpp
#include <iostream>
using namespace std;

// Here Car identifier is used to refer to below class
class Car {
    string Brand;
    string model;
    int year;
};

// getSum identifier is used to call the below function
void getSum(int a, int b) {
    int _sum = a + b;
    cout << "The sum is: " << _sum;
}

int main() {
  
    // Identifiers used as variable names
    int studentAge = 20;
    double accountBalance = 1000.50;
    string student_Name = "Karan";

    getSum(2, 10);

    return 0;
}
```

### Output
The sum is: 12

# Time Complexity
O(1)

# Space Complexity
O(1)

### Identifier Naming Conventions

Identifier naming conventions are recommended practices followed by programmers to make code more readable, consistent, and easier to maintain. Unlike the rules for valid identifiers, these conventions are not enforced by the C++ compiler. Instead, they serve as guidelines that help improve code quality and collaboration among developers.

Naming Variables

- Prefer **camelCase** style for variable names.
- Begin the name with a lowercase letter.
- Choose descriptive names that clearly indicate the purpose of the variable.
- Constants are often written using **UPPER_SNAKE_CASE**.

**Examples:**

- `studentAge`
- `frequencyCount`
- `personName`
- `MAX_SIZE` (constant)

Naming Functions

- Use **camelCase** style.
- Function names should generally be verbs or verb phrases because they represent actions.
- Choose names that clearly describe the task performed by the function.

**Examples:**

- `getName()`
- `calculateTotal()`
- `countFrequency()`
- `displayResult()`

Naming Classes

- Use **PascalCase** style, where the first letter of each word is capitalized.
- Class names are usually nouns or noun phrases because they represent objects or entities.

**Examples:**

- `Car`
- `Student`
- `BankAccount`
- `EmployeeRecord`

These conventions are widely used in the programming community, but specific projects or organizations may adopt their own coding standards. Therefore, it is important to follow the guidelines established for the project you are working on while maintaining meaningful and consistent naming practices.

The following example illustrates commonly used naming conventions in C++. It demonstrates the use of **camelCase** for variables and functions, **UPPER_SNAKE_CASE** for constants, and **PascalCase** for class names, helping to make the code more readable and maintainable.

```cpp
#include <iostream>
using namespace std;

// Class name using PascalCase
class StudentRecord {
public:
    string studentName;
};

// Constant using UPPER_SNAKE_CASE
const int MAX_STUDENTS = 100;

// Function name using camelCase
void displayMessage() {
    cout << "Identifier Naming Conventions";
}

int main() {
    
    // Variable names using camelCase
    int studentAge = 20;
    double accountBalance = 1500.75;

    displayMessage();

    return 0;
}
```

### Output
Identifier Naming Conventions

# Time Complexity
O(1)

# Space Complexity
O(1)




