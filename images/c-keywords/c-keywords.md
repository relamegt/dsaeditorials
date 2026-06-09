# C++ Keywords

### 

Keywords are predefined words in C++ that carry special meanings and serve specific purposes within the language. These words are reserved by the compiler and cannot be used as identifiers for variables, functions, classes, or any other user-defined entities.

Because keywords already have a defined role in the language syntax, attempting to redefine or repurpose them will result in a compilation error.

The following example demonstrates the use of several C++ keywords such as `int`, `if`, and `return` in a simple program.

```cpp
#include <iostream>
using namespace std;

// 'int' is a keyword
int main() {
    
    // 'int' is a keyword
    int marks = 85;
    
    // 'if' is a keyword
    if (marks >= 50) {
        cout << "Pass";
    }
    
    // 'return' is a keyword
    return 0;
}
```

### Output
Pass

# Time Complexity
O(1)

# Space Complexity
O(1)

### How to Identify C++ Keywords

There are several ways to recognize keywords in a C++ program:

1. **Syntax Highlighting:** Modern code editors and IDEs typically display keywords in distinct colors, making them easy to distinguish from user-defined names.
2. **Compiler Validation:** If a reserved keyword is used as an identifier, the compiler generates an error because keywords cannot be assigned a different meaning.

**Example:**

`int return = 10; // Error: 'return' is a reserved keyword`

Understanding keywords is essential because they form the foundation of C++ syntax and control the behavior of programs.

| Category | Representative Keywords |
| --- | --- |
| Fundamental Data Types | bool, char, char8_t, char16_t, char32_t, wchar_t, int, short, long, signed, unsigned, float, double, void |
| Program Flow Control | if, else, switch, case, default, for, while, do, break, continue, goto |
| Boolean and Null Values | true, false, nullptr |
| Memory Management | new, delete, sizeof, alignas, alignof |
| Class and Object-Oriented Features | class, struct, union, enum, friend, this, mutable |
| Access Control | public, private, protected |
| Function-Related Keywords | inline, virtual, override, final, explicit, operator |
| Type Deduction and Aliases | auto, decltype, typedef, using, typename |
| Compile-Time Programming | constexpr, consteval, constinit, static_assert |
| Templates and Generic Programming | template, concept, requires |
| Exception Handling | try, catch, throw, noexcept |
| Type Casting and Runtime Type Information | static_cast, dynamic_cast, const_cast, reinterpret_cast, typeid |
| Storage Duration and Qualifiers | const, static, extern, register, thread_local, volatile |
| Namespaces and Modules | namespace, export |
| Coroutine Support (C++20) | co_await, co_return, co_yield |
| Alternative Operator Keywords | and, or, not, bitand, bitor, xor, and_eq, or_eq, xor_eq, not_eq, compl |
| Miscellaneous Keywords | asm, return |

---

**Note:** The set of keywords available in C++ has expanded with each major language revision. As new features and programming paradigms were introduced, additional keywords were added to support them. For instance, C++98 included 63 keywords, while C++11 increased this number significantly by introducing keywords related to modern language features such as type deduction, multithreading, and compile-time programming.

---

### **Keywords vs Identifiers**

Although keywords and identifiers may appear similar in source code, they serve entirely different purposes. Keywords are reserved words defined by the C++ language and have predefined meanings, whereas identifiers are user-defined names used to represent variables, functions, classes, and other program elements.

The following table highlights the key differences between keywords and identifiers.

| Keywords | Identifiers |
| --- | --- |
| Reserved words that have predefined meanings in the C++ language. | User-defined names assigned to variables, functions, classes, arrays, structures, and other program elements. |
| Their purpose and behavior are fixed by the compiler and cannot be changed. | Their names and purposes are determined by the programmer. |
| Used to define the syntax and structure of a C++ program. | Used to uniquely identify and reference entities within a program. |
| Cannot be used as names for variables, functions, or other user-defined entities. | Must follow identifier naming rules and cannot match reserved keywords. |
| Most keywords consist of lowercase letters, although newer standards include some with underscores and digits. | Can contain letters, digits, and underscores, but cannot begin with a digit. |
| Have predefined meanings recognized by the compiler. | Have meanings based on how they are declared and used in the program. |
| Examples: int, char, if, while, return, class | Examples: studentAge, calculateSum, employeeRecord, count1 |




