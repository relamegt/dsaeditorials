# Strings in C++

## Introduction

In C++, a string is an object of the `std::string` class, which is part of the Standard Template Library (STL). It represents and manages dynamic sequences of characters. 

Unlike traditional C-style character arrays (`char[]`), `std::string` manages its memory buffers automatically. This removes the risk of buffer overflow bugs and null-termination mistakes, making text manipulation safer and more convenient.

Key features:

- **Dynamic Sizing:** Automatically expands and contracts in memory as characters are added or removed.
- **Rich Member Functions:** Built-in support for concatenation, searching, replacements, substring extraction, and comparison.
- **Safe Traversal:** Supports index-based loops, range-based loops, and iterator-based traversal.

## Basic Syntax

The string container is defined as `std::string` class inside the `<string>` header file.

```Cpp
#include <string>
using namespace std;

string str;
```

Here, `string` represents the `std::string` container class and `str` is the initialized object name.

## Traversing a String

You can traverse the characters of a string using three primary techniques: index-based iteration, range-based `for` loop, and iterators.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    // 1. Traversing using index
    cout << "Index traversal : ";
    for (int i = 0; i < str.size(); i++) {
        cout << str[i];
    }
    cout << endl;

    // 2. Traversing using range-based for loop
    cout << "Range-based loop: ";
    for (char ch : str) {
        cout << ch;
    }
    cout << endl;

    // 3. Traversing using iterators
    cout << "Iterator loop   : ";
    for (auto it = str.begin(); it != str.end(); ++it) {
        cout << *it;
    }
    cout << endl;

    return 0;
}
```

### Output
Index traversal : AlphaKnowledge
Range-based loop: AlphaKnowledge
Iterator loop   : AlphaKnowledge

## Basic Operations on Strings

### 1. Initialization

Strings can be initialized directly with a string literal or using copy constructors.

```Cpp
#include <iostream>
using namespace std;

int main() {
    string str = "AlphaKnowledge";
    cout << str << endl;
    return 0;
}
```

### Output
AlphaKnowledge

### 2. Accessing Characters

Individual characters can be accessed in constant time `O(1)` using the array subscript operator `[]` or the `.at()` member function.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    // Access using subscript operator
    cout << "First character : " << str[0] << endl;
    cout << "Sixth character : " << str[5] << endl;

    // Access using at()
    cout << "Char at index 6 : " << str.at(6) << endl;

    return 0;
}
```

### Output
First character : A
Sixth character : K
Char at index 6 : n

Using `.at()` performs bounds checking at runtime, throwing an exception if the index is invalid. The subscript operator `[]` is slightly faster but does not perform bounds checking.

### 3. Determining String Length

You can retrieve the character count of a string in `O(1)` time using either `.size()` or `.length()`.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    cout << "Length via size()   : " << str.size() << endl;
    cout << "Length via length() : " << str.length() << endl;

    return 0;
}
```

### Output
Length via size()   : 14
Length via length() : 14

### 4. Concatenation

Strings can be concatenated using the `+` operator (which creates a new string) or the `.append()` function (which modifies the calling string in-place).

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "Alpha";
    string str2 = "Knowledge";

    // Using + operator
    string result1 = str1 + str2;
    cout << "Using + operator : " << result1 << endl;

    // Using append()
    string result2 = str1;
    result2.append(str2);
    cout << "Using append()   : " << result2 << endl;

    return 0;
}
```

### Output
Using + operator : AlphaKnowledge
Using append()   : AlphaKnowledge

### 5. Modifying a String

Characters can be appended to the end using `.push_back()`, removed using `.pop_back()`, or inserted/erased at specific locations using `.insert()` and `.erase()`.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    // Add character at the end
    str.push_back('!');
    cout << "After push_back : " << str << endl;

    // Remove last character
    str.pop_back();
    cout << "After pop_back  : " << str << endl;

    // Insert a substring
    str.insert(5, " Platform ");
    cout << "After insert    : " << str << endl;

    // Erase a portion
    str.erase(5, 10); 
    cout << "After erase     : " << str << endl;

    return 0;
}
```

### Output
After push_back : AlphaKnowledge!
After pop_back  : AlphaKnowledge
After insert    : Alpha Platform Knowledge
After erase     : AlphaKnowledge

### 6. Substring Extraction

The `.substr(pos, len)` function extracts a segment of a string starting at index `pos` and spanning `len` characters.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    // Extract "Alpha"
    string sub1 = str.substr(0, 5);   
    cout << "Substring 1 : " << sub1 << endl;

    // Extract "Knowledge"
    string sub2 = str.substr(5, 9);  
    cout << "Substring 2 : " << sub2 << endl;

    return 0;
}
```

### Output
Substring 1 : Alpha
Substring 2 : Knowledge

### 7. Searching

The `.find()` function searches for a character or substring. If found, it returns the starting index of the first match. If no match is found, it returns `std::string::npos`.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    size_t pos = str.find("Knowledge");  

    if (pos != string::npos) {
        cout << "\"Knowledge\" found at index: " << pos << endl;
    } else {
        cout << "Substring not found" << endl;
    }

    return 0;
}
```

### Output
"Knowledge" found at index: 5

## Common C++ String Functions

| Function | Description |
| --- | --- |
| `length()` / `size()` | Returns the number of characters in the string |
| `swap()` | Swaps the contents of two string variables in constant time |
| `resize()` | Resizes the string to a specified character count |
| `push_back()` | Appends a single character to the end of the string |
| `pop_back()` | Deletes the last character of the string |
| `clear()` | Removes all characters from the string |
| `find()` | Locates the first occurrence of a substring |
| `rfind()` | Locates the last occurrence of a substring |
| `replace()` | Replaces a segment of the string with another string |
| `substr()` | Extracts a portion of the string as a new object |
| `compare()` | Performs lexicographical comparison returning an integer |
| `erase()` | Deletes a portion of the string |

> **Note:** Traditional C-style string manipulation functions like `strcpy()` and `strcat()` operate directly on raw character pointers (`char*`) and are prone to buffer overflows if boundaries are not manually verified. In modern C++, it is strongly recommended to use `std::string` and its associated member functions to handle text data safely and efficiently.

## Summary

Strings in C++ are managed via the standard `std::string` class, which handles dynamic resizing and buffer management automatically. Characters within a string can be traversed using indices, range-based `for` loops, or iterators. C++ strings support a wide variety of operations, including element-wise access via `[]` and `at()`, concatenation via `+` and `append()`, search via `find()`, substring extraction via `substr()`, and dynamic modification via `push_back()`, `pop_back()`, `insert()`, and `erase()`. Using the `std::string` class is the standard and safest approach to working with text in modern C++ applications.




