# String Functions in C++

In C++, a string is an ordered sequence of characters managed through the `std::string` class provided by the Standard Library. Unlike plain character arrays, `std::string` handles memory internally and comes packed with a comprehensive collection of member functions that make text operations straightforward and safe.

The `<string>` header must be included to use these features. Key benefits include:

- Strings resize automatically as their content grows or shrinks.
- A broad set of built-in functions covers searching, modifying, comparing, and extracting text.
- Operations are significantly easier to write and maintain compared to raw `char[]` manipulation.

### Quick Demo

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    cout << "String       : " << str << endl;
    cout << "Length       : " << str.length() << endl;

    str.append(" Platform");
    cout << "After Append : " << str << endl;

    cout << "First Char   : " << str[0] << endl;
    cout << "Find 'Platform' at index : " << str.find("Platform") << endl;

    return 0;
}
```

### Output
String       : AlphaKnowledge
Length       : 14
After Append : AlphaKnowledge Platform
First Char   : A
Find 'Platform' at index : 15

## Standard String Class (std::string)

Introduced in C++98 and defined in the `<string>` header, `std::string` is the go-to class for handling dynamic character sequences. It serves as a safer, more capable replacement for C-style character arrays, offering native support for operations like searching, replacing, comparing, and splitting text without needing external libraries.

## Commonly Used String Functions

### 1. String Length — `length()` and `size()`

Both `length()` and `size()` return the number of characters currently stored in the string. They are functionally identical; `size()` exists for consistency with other STL containers.

**Syntax:**

```Cpp
str.length();
str.size();
```

Neither function takes any parameter. Both return the character count as an unsigned integer (`size_t`).

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string text = "AlphaKnowledge";

    cout << "String              : " << text << endl;
    cout << "Length using length(): " << text.length() << endl;
    cout << "Length using size()  : " << text.size() << endl;

    return 0;
}
```

### Output
String              : AlphaKnowledge
Length using length(): 14
Length using size()  : 14

### 2. Accessing Characters — `at()`

Characters within a string can be accessed using either the `[]` subscript operator or the `at()` member function. The key difference is that `at()` performs bounds checking and throws an `std::out_of_range` exception when the supplied index falls outside the valid range, while `[]` silently causes undefined behavior for invalid indices.

**Syntax:**

```Cpp
str.at(index);
```

`index` is zero-based — the first character is at position 0.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string text = "AlphaKnowledge";

    cout << "String                 : " << text << endl;
    cout << "Character at index 0   : " << text.at(0) << endl;
    cout << "Character at index 5   : " << text.at(5) << endl;

    return 0;
}
```

### Output
String                 : AlphaKnowledge
Character at index 0   : A
Character at index 5   : K

### 3. Concatenating Strings — `+` Operator and `append()`

Two approaches exist for joining strings together.

#### 3a. `+` Operator
The `+` operator is overloaded in `std::string` to produce a new string by joining two existing strings. The original strings remain unchanged.

```Cpp
str1 + str2;
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "AlphaKnowledge";
    string str2 = " — Learn Smarter";

    string result = str1 + str2;
    cout << "Concatenated: " << result << endl;

    return 0;
}
```

### Output
Concatenated: AlphaKnowledge — Learn Smarter

#### 3b. `append()` Function
Unlike `+`, `append()` modifies the calling string directly by attaching another string to its end. It returns a reference to the modified string, so calls can be chained.

```Cpp
str1.append(str2);
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "AlphaKnowledge";
    string str2 = " ak";

    str1.append(str2);
    cout << "After append: " << str1 << endl;

    return 0;
}
```

### Output
After append: AlphaKnowledge ak

### 4. Comparing Strings — `==` Operator and `compare()`

#### 4a. `==` Operator
The simplest way to check whether two strings contain identical content. Returns a boolean `true` or `false`.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "ak";
    string str2 = "ak";

    if (str1 == str2)
        cout << "Strings are equal" << endl;
    else
        cout << "Strings are not equal" << endl;

    return 0;
}
```

### Output
Strings are equal

#### 4b. `compare()` Function
Returns a numeric result for lexicographic comparison — useful when sorting or ordering strings.

- Returns `0` when both strings are identical.
- Returns a value `> 0` when the calling string is lexicographically greater.
- Returns a value `< 0` when the calling string is lexicographically smaller.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "Apple";
    string str2 = "Banana";

    int result = str1.compare(str2);
    cout << "Compare result: " << result << endl;

    if (result < 0)
        cout << str1 << " comes before " << str2 << endl;
    else if (result > 0)
        cout << str1 << " comes after " << str2 << endl;
    else
        cout << "Both strings are equal" << endl;

    return 0;
}
```

### Output
Compare result: -1
Apple comes before Banana

### 5. Searching — `find()`

`find()` scans the string from left to right and returns the zero-based index of the first occurrence of a character or substring. If the target is not found, it returns the special constant `std::string::npos`.

**Syntax:**

```Cpp
str.find(var);
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string text = "Learn with AlphaKnowledge Platform";

    size_t pos = text.find("AlphaKnowledge");

    if (pos != string::npos)
        cout << "'AlphaKnowledge' found at index: " << pos << endl;
    else
        cout << "Substring not found" << endl;

    return 0;
}
```

### Output
'AlphaKnowledge' found at index: 11

### 6. Extracting a Substring — `substr()`

`substr()` cuts out a portion of the string and returns it as a brand-new `std::string` object. The original string is not modified.

**Syntax:**

```Cpp
str.substr(start, length);
```

`start` is the beginning index and `length` is the number of characters to extract.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string text = "AlphaKnowledge Platform";

    string sub = text.substr(0, 14);
    cout << "Extracted substring: " << sub << endl;

    return 0;
}
```

### Output
Extracted substring: AlphaKnowledge

### 7. Modifying Strings — `insert()`, `replace()`, `erase()`

#### 7a. `insert()`
Inserts a string at a given position without removing existing characters. Everything after the insertion point shifts to the right.

```Cpp
str1.insert(index, str2);
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "Alpha Platform";
    string str2 = "Knowledge ";

    str1.insert(6, str2);
    cout << "After insert: " << str1 << endl;

    return 0;
}
```

### Output
After insert: AlphaKnowledge  Platform

#### 7b. `replace()`
Replaces a section of the string — the specified characters are removed and substituted with the new string.

```Cpp
str1.replace(index, size, str2);
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "I prefer Java";
    string str2 = "C++";

    str1.replace(9, 4, str2);
    cout << "After replace: " << str1 << endl;

    return 0;
}
```

### Output
After replace: I prefer C++

#### 7c. `erase()`
Removes a range of characters from the string starting at a given position.

```Cpp
str.erase(start, count);
```

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge Platform";

    str.erase(14, 9);  // Remove " Platform"
    cout << "After erase: " << str << endl;

    return 0;
}
```

### Output
After erase: AlphaKnowledge

### 8. Converting to C-Style String — `c_str()`

`c_str()` converts a `std::string` object into a null-terminated `const char*` pointer, which is required when interfacing with legacy C APIs or system functions that expect a raw character array.

```Cpp
str.c_str();
```

The returned pointer remains valid only as long as the string is not modified. It takes no parameters and does not alter the original string.

```Cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "AlphaKnowledge";

    const char* cstr = str.c_str();
    cout << "C-style string: " << cstr << endl;

    return 0;
}
```

### Output
C-style string: AlphaKnowledge

## Summary of String Functions

| Category | Function / Operator | Description |
| --- | --- | --- |
| **Length** | `length()`, `size()` | Returns the number of characters in the string |
| **Access** | `[]`, `at(index)` | Accesses a character by index; `at()` is bounds-safe |
| **Concatenation** | `+`, `append()` | Joins two strings; `+` creates a new string, `append()` modifies in place |
| **Comparison** | `==`, `compare()` | Checks equality or lexicographic order |
| **Search** | `find()` | Returns the index of the first occurrence; `npos` if not found |
| **Substring** | `substr(start, len)` | Extracts and returns a portion of the string |
| **Insert** | `insert(index, str)` | Inserts a string at a given position |
| **Replace** | `replace(index, n, str)` | Replaces n characters starting at index with a new string |
| **Erase** | `erase(start, count)` | Removes count characters starting at start |
| **Conversion** | `c_str()` | Returns a null-terminated `const char*` for C API compatibility |

> **Note:** When using `find()`, always compare the result against `std::string::npos` before using it as an index. Using a `npos` result as an array index directly leads to out-of-bounds access. Similarly, prefer `at()` over `[]` whenever bounds safety is a concern, especially in functions receiving unknown input lengths.

## Summary

C++ `std::string` provides a comprehensive set of built-in functions that cover every common text operation. `length()` and `size()` report the character count; `at()` safely retrieves a character by index; `append()` and `+` join strings; `compare()` and `==` evaluate string ordering and equality; `find()` locates substrings; `substr()` extracts portions; `insert()`, `replace()`, and `erase()` modify content in place; and `c_str()` bridges `std::string` with C-style APIs. Together these functions make string processing in C++ both expressive and safe without manual memory management.




