# std::string Class in C++

The `std::string` class is the standard C++ library class used to represent and manipulate sequences of characters. It automatically manages memory, making string handling significantly safer and more convenient than using raw character arrays (`char[]`). It is declared in the `<string>` header and is part of the `std` namespace.

Key characteristics:

- Dynamically resizes its internal buffer without requiring manual memory allocation or null-termination.
- Provides a rich set of built-in member functions for creating, accessing, modifying, comparing, and searching strings.
- Behaves as a regular C++ object — supports copy, assignment, and comparison operators natively.

## Syntax

```Cpp
#include <string>
std::string str;
```

`std::string` is the class name and `str` is the string object variable.

## Creating and Initializing Strings

```Cpp
string str1 = "AlphaKnowledge";   // Initialized with a string literal
string str2("ak");                 // Constructor initialization
string str3(5, 'x');              // Repeated character: "xxxxx"
string str4 = str1;               // Copy from another string
string str5;                       // Empty string
```

`str1` and `str2` are initialized with values. `str3` demonstrates character repetition initialization. `str5` is an empty string with zero length.

## String vs Character Array

| Feature | `std::string` | Character Array (`char[]`) |
| --- | --- | --- |
| **Memory** | Dynamically resizes as needed | Fixed size set at declaration |
| **Built-in Functions** | Rich set of member functions | Requires `<cstring>` library functions |
| **Array Decay** | Does not decay when passed to functions | Decays to a pointer when passed |
| **Memory Management** | Automatic | Manual — risk of buffer overflow |
| **Performance** | Slight overhead due to abstraction | Faster — direct memory access |
| **Safety** | Bounds-safe with `.at()` | No automatic bounds checking |

## Common String Operations

### Input Functions

These functions are used to read or modify the contents of a string.

| Function | Description |
| --- | --- |
| `getline()` | Reads an entire line (including spaces) from input into the string object. |
| `push_back(c)` | Appends a single character `c` to the end of the string. |
| `pop_back()` | Removes the last character from the string (C++11 and later). |

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    cout << "Initial string : " << str << endl;

    // Appending a character
    str.push_back('!');
    cout << "After push_back : " << str << endl;

    // Removing the last character
    str.pop_back();
    cout << "After pop_back  : " << str << endl;

    return 0;
}
```

### Output
Initial string : AlphaKnowledge
After push_back : AlphaKnowledge!
After pop_back  : AlphaKnowledge

`push_back()` appends a character at the end. `pop_back()` removes it. Both operate in O(1) amortized time.

**Time Complexity:** O(1) | **Space Complexity:** O(n) where n is the string length

### Capacity Functions

These functions provide information about the size and memory allocated to a string.

| Function | Description |
| --- | --- |
| `length()` / `size()` | Returns the number of characters currently in the string. |
| `capacity()` | Returns the total memory (in characters) currently allocated. |
| `resize(n)` | Changes the string length to n characters (truncates or pads with null). |
| `shrink_to_fit()` | Reduces allocated capacity to match the current string length. |
| `empty()` | Returns `true` if the string contains zero characters. |

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge is for learners";

    cout << "Initial string   : " << str << endl;
    cout << "Length           : " << str.length() << endl;
    cout << "Capacity         : " << str.capacity() << endl;

    // Resize to 14 characters
    str.resize(14);
    cout << "After resize(14) : " << str << endl;
    cout << "Length after resize : " << str.length() << endl;

    // Reduce capacity to match current length
    str.shrink_to_fit();
    cout << "Capacity after shrink_to_fit : " << str.capacity() << endl;

    return 0;
}
```

### Output
Initial string   : AlphaKnowledge is for learners
Length           : 30
Capacity         : 30
After resize(14) : AlphaKnowledge
Length after resize : 14
Capacity after shrink_to_fit : 14

`resize()` truncates the string to 14 characters. `shrink_to_fit()` releases the unused memory buffer.

**Time Complexity:** O(1) | **Space Complexity:** O(n)

### Iterator Functions

Iterators allow traversal of a string in both forward and reverse directions.

| Function | Description |
| --- | --- |
| `begin()` | Returns an iterator pointing to the first character. |
| `end()` | Returns an iterator pointing past the last character. |
| `rbegin()` | Returns a reverse iterator to the last character. |
| `rend()` | Returns a reverse iterator to the position before the first character. |
| `cbegin()` / `cend()` | Constant (read-only) forward iterators. |
| `crbegin()` / `crend()` | Constant (read-only) reverse iterators. |

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "alphaknowledge";

    // Forward traversal (modifying first character to uppercase)
    string::iterator it = str.begin();
    *it = 'A';

    cout << "Forward (modified) : ";
    for (it = str.begin(); it != str.end(); ++it)
        cout << *it;
    cout << endl;

    // Reverse traversal
    cout << "Reverse            : ";
    for (string::reverse_iterator rit = str.rbegin(); rit != str.rend(); ++rit)
        cout << *rit;
    cout << endl;

    // Constant forward iterator (read-only)
    cout << "Const forward      : ";
    for (string::const_iterator cit = str.cbegin(); cit != str.cend(); ++cit)
        cout << *cit;
    cout << endl;

    return 0;
}
```

### Output
Forward (modified) : Alphaknowledge
Reverse            : egdelwonkahplA
Const forward      : Alphaknowledge

Normal iterators allow character modification. Constant iterators (`cbegin`, `cend`) provide read-only access and prevent accidental modification.

**Time Complexity:** O(n) | **Space Complexity:** O(n)

### String Manipulating Functions

These functions modify or exchange string contents.

| Function | Description |
| --- | --- |
| `copy(arr, len, pos)` | Copies `len` characters starting from position `pos` into a character array `arr`. |
| `swap(str2)` | Exchanges the entire contents of two strings in O(1) without element-wise copying. |

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "AlphaKnowledge is for learners";
    string str2 = "ak platform rocks";

    // Copy first 14 characters of str1 into a char array
    char ch[80];
    str1.copy(ch, 14, 0);
    ch[14] = '\0';  // Null-terminate the array
    cout << "Copied char array : " << ch << endl;

    cout << "Before swap:" << endl;
    cout << "  str1 = " << str1 << endl;
    cout << "  str2 = " << str2 << endl;

    // Swap contents
    str1.swap(str2);

    cout << "After swap:" << endl;
    cout << "  str1 = " << str1 << endl;
    cout << "  str2 = " << str2 << endl;

    return 0;
}
```

### Output
Copied char array : AlphaKnowledge
Before swap:
  str1 = AlphaKnowledge is for learners
  str2 = ak platform rocks
After swap:
  str1 = ak platform rocks
  str2 = AlphaKnowledge is for learners

`copy()` copies characters into a raw character array; the null terminator must be added manually. `swap()` exchanges the contents of both strings internally in constant time.

## Advantages of `std::string`

- Automatic memory management — no manual `malloc`/`free` required.
- Dynamic resizing — the string grows or shrinks as content changes.
- Rich member function library for searching, comparing, splitting, and modifying.
- Supports native comparison operators (`==`, `<`, `>`) without external functions.
- Safer than character arrays — no risk of missing null terminators or buffer overflows.

> **Note:** While `std::string` provides safety and convenience, it carries a slight performance overhead compared to raw `char` arrays due to heap allocation and internal bookkeeping. For performance-critical, fixed-length string scenarios (such as network protocols or embedded systems), `std::string_view` (C++17) offers a lightweight, non-owning alternative that avoids unnecessary copies.

## Summary

The `std::string` class in C++ is the standard, preferred way to handle text data. It automatically manages memory, provides forward and reverse iterators for traversal, and includes member functions for capacity management (resize, shrink_to_fit), content modification (push_back, pop_back, swap), and direct character array interop (copy). Compared to `char[]` arrays, `std::string` is safer, more flexible, and far easier to work with for everyday string operations, making it the default choice for string handling in modern C++ applications.




