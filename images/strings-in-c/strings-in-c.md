# Strings in C++

Strings are one of the most commonly used data types in programming. They are used to store and manipulate textual information such as names, addresses, messages, passwords, email IDs, and sentences.

In C++, a string is represented using the `std::string` class, which is part of the Standard Template Library (STL). The string class provides a convenient way to work with text data without worrying about low-level memory management.

Before the introduction of the string class, programmers used character arrays (`char[]`) to store text. Although character arrays are still supported, they require manual handling of memory and are more error-prone. The `std::string` class simplifies string operations by providing automatic memory management and numerous built-in functions.

A string can contain:

- Alphabets
- Digits
- Special symbols
- Spaces
- Combination of all character types

Examples:

```text
"Abhiram"
"Hemesh"
"Mohit"
"Akash"
```

All the above examples are strings because they represent a sequence of characters enclosed within double quotation marks.

# Why Do We Need Strings?

Imagine storing a student's name using individual characters:

```cpp
char c1 = 'M';
char c2 = 'o';
char c3 = 'h';
char c4 = 'i';
char c5 = 't';
```

Managing text in this way becomes difficult and impractical.

Instead, we can use a string:

```cpp
string name = "Mohit";
```

Now the complete text is stored in a single object.

Strings make programs:

- Easier to write.
- Easier to understand.
- Easier to maintain.
- More efficient.

They provide built-in support for many common operations such as searching, inserting, deleting, comparing, and concatenating text.

# Features of std::string

The C++ string class provides several advantages over traditional character arrays.

### Dynamic Size

A string can automatically grow or shrink as needed.

```cpp
string name = "Mohit";

name += " Kumar";
```

The string automatically adjusts its size.

### Automatic Memory Management

The string class automatically allocates and deallocates memory.

Programmers do not need to manually manage memory as they do with character arrays.

### Rich Set of Functions

Many useful operations are already available.

Examples:

```cpp
length()
size()
find()
substr()
append()
erase()
replace()
```

These functions reduce programming effort.

### Easy Character Access

Individual characters can be accessed using indexes.

```cpp
string name = "Mohit";

cout << name[0];
```

### Output
M

### Easy String Manipulation

Strings can be modified easily.

```cpp
string name = "Mohit";

name.push_back('!');
```

### Output
Mohit!

# String Header File

The string class is defined in the  header file.

Before using strings, this header must be included.

```cpp
#include <string>
```

Most programs also include:

```cpp
#include <iostream>
```

for input and output operations.

# Declaration of Strings

A string variable can be declared just like any other variable.

## Syntax

```cpp
string stringName;
```

### Example

```cpp
string studentName;
```

At this stage, the string exists but contains no characters.

# Initialization of Strings

Initialization means assigning a value to a string at the time of creation.

A string can be initialized in multiple ways.

## Direct Initialization

```cpp
string college = "PVPSIT";
```

## Constructor Initialization

```cpp
string college("PVPSIT");
```

Both approaches produce the same result.

## Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string studentName = "Akash";

    cout << studentName;

    return 0;
}
```

### Output
Akash

### 

# Memory Representation of Strings

Consider:

```cpp
string name = "Mohit";
```

Internally, characters are stored sequentially.

```text
Index : 0 1 2 3 4

Value : M o h i t
```

Each character occupies one byte of memory.

Unlike character arrays, the string class automatically keeps track of:

- Length
- Capacity
- Memory allocation

This makes strings easier to manage.

# Traversing a String

Traversing means visiting every character one by one.

Since strings store characters sequentially, traversal is straightforward.

There are several methods to traverse strings.

## Traversing Using Index

Every character has a unique index.

```text
String : Mohit

Index  : 0 1 2 3 4
```

The first character is stored at index 0.

The last character is stored at index `length - 1`.

## Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name = "Hemanth";

    for(int i = 0; i < name.size(); i++)
    {
        cout << name[i] << " ";
    }

    return 0;
}
```

### Output
H e m a n t h

### 

This is the most commonly used traversal method.

## Traversing Using Range-Based For Loop

Modern C++ provides a cleaner way to traverse strings.

Instead of managing indexes manually, the loop automatically accesses each character.

## Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name = "Akash";

    for(char ch : name)
    {
        cout << ch << " ";
    }

    return 0;
}
```

### Output
A k a s h

### 

This method is easier to read and write.

## Traversing Using Iterators

Strings support iterators because they are STL containers.

Iterators behave like pointers and allow sequential access to elements.

## Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name = "Hemesh";

    for(auto it = name.begin();
        it != name.end();
        it++)
    {
        cout << *it << " ";
    }

    return 0;
}
```

### Output
H e m e s h

### 

Iterators are commonly used with STL algorithms.

# String vs Character Array

Many beginners get confused between strings and character arrays.

Both store text, but they differ significantly.

| Feature | Character Array | String |
| --- | --- | --- |
| Size | Fixed | Dynamic |
| Memory Management | Manual | Automatic |
| Built-in Functions | Very Few | Many |
| Ease of Use | Difficult | Easy |
| Safety | Less Safe | Safer |
| Concatenation | Complex | Simple |

### Character Array Example

```cpp
char name[] = "Mohit";
```

### String Example

```cpp
string name = "Mohit";
```

For modern C++ development, strings are preferred in most situations.

# 

# Real-World Applications of Strings

Strings are used almost everywhere in software development.

Examples include:

- User names
- Passwords
- Email addresses
- Search engines
- Chat applications
- Social media posts
- Programming languages
- File names
- URLs
- Database records

Without strings, handling textual information would be extremely difficult.

### Common C++ String Functions

The `std::string` class provides many built-in functions that simplify string manipulation. These functions allow programmers to perform operations such as finding string length, accessing characters, searching text, extracting substrings, modifying content, and comparing strings efficiently.

| Function | Description |
| --- | --- |
| length() | Returns the number of characters present in the string. |
| size() | Returns the size (length) of the string. It performs the same task as length(). |
| empty() | Checks whether the string is empty. Returns true if the string contains no characters. |
| clear() | Removes all characters from the string, making it empty. |
| push_back() | Adds a character at the end of the string. |
| pop_back() | Removes the last character from the string. |
| append() | Appends another string to the end of the current string. |
| insert() | Inserts characters or a substring at a specified position. |
| erase() | Removes characters from a specified position in the string. |
| replace() | Replaces a portion of the string with another string. |
| substr() | Extracts a substring from the string. |
| find() | Finds the first occurrence of a character or substring and returns its position. |
| rfind() | Finds the last occurrence of a character or substring and returns its position. |
| compare() | Compares two strings lexicographically and returns an integer value indicating the result. |
| swap() | Swaps the contents of two strings. |
| resize() | Changes the length of the string by increasing or decreasing its size. |
| at() | Accesses a character at a specific index with bounds checking. |
| front() | Returns the first character of the string. |
| back() | Returns the last character of the string. |
| c_str() | Returns a C-style null-terminated character array representation of the string. |
| capacity() | Returns the amount of storage currently allocated for the string. |
| reserve() | Requests memory allocation for a specified number of characters. |
| begin() | Returns an iterator pointing to the first character of the string. |
| end() | Returns an iterator pointing just after the last character of the string. |

# Time Complexity of Common String Operations

| Operation | Complexity |
| --- | --- |
| Access Character | O(1) |
| size() | O(1) |
| length() | O(1) |
| push_back() | O(1) |
| pop_back() | O(1) |
| Concatenation | O(n + m) |
| find() | O(n × m) |
| substr() | O(k) |
| insert() | O(n) |
| erase() | O(n) |

Understanding these complexities helps in writing efficient programs.

# Taking Input in Strings

Input is one of the most frequently performed operations on strings. In C++, string data can be read from the keyboard using either `cin` or `getline()`. Both methods are used to accept input from the user, but they behave differently when spaces are involved. Understanding the difference between them helps in choosing the correct method for different situations.

## Using `cin`

The `cin` object reads input until it encounters a whitespace character such as a space, tab, or newline. Therefore, it is suitable when the input consists of only a single word.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string studentName;

    cout << "Enter Name: ";
    cin >> studentName;

    cout << "Name: " << studentName;

    return 0;
}
```

### Input

Mohit Kumar

### Output

Name: Mohit

Although the user enters two words, only "Mohit" is stored in the string. This happens because `cin` stops reading as soon as it encounters the first whitespace character. For this reason, `cin` is generally used for reading single-word inputs such as usernames, passwords, IDs, or short names without spaces.

### When to Use `cin`

Use `cin` when:

- Input consists of a single word.
- Spaces are not required.
- Reading usernames, passwords, IDs, or short names.
- Reading numerical values along with simple text.

## Using `getline()`

The `getline()` function reads an entire line of text from the input stream. Unlike `cin`, it does not stop at spaces and continues reading until the Enter key is pressed.

This makes `getline()` ideal for reading complete names, addresses, messages, and other text that may contain spaces.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string studentName;

    cout << "Enter Name: ";
    getline(cin, studentName);

    cout << "Name: " << studentName;

    return 0;
}
```

### Input

Mohit Kumar

### Output

Name: Mohit Kumar

In this case, the complete line entered by the user is stored in the string. Since `getline()` reads all characters until a newline character is encountered, spaces become part of the string instead of terminating the input operation.

### When to Use `getline()`

Use `getline()` when:

- Reading full names.
- Reading addresses.
- Reading messages.
- Reading paragraphs or sentences.
- Reading any input that may contain spaces.

## Difference Between `cin` and `getline()`

| Feature | cin | getline() |
| --- | --- | --- |
| Reads until first space | Yes | No |
| Reads complete line | No | Yes |
| Supports spaces | No | Yes |
| Suitable for sentences | No | Yes |
| Suitable for single words | Yes | Yes |

## Common Issue When Mixing `cin` and `getline()`

A common mistake occurs when `getline()` is used immediately after `cin`.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int age;
    cin >> age;

    string name;

    getline(cin, name);

    cout << name;

    return 0;
}
```

The program may appear to skip the input for the string variable.

This happens because `cin` leaves a newline character (`\n`) in the input buffer after reading the integer. The subsequent `getline()` reads that newline character immediately and considers the input complete.

### Solution

The problem can be solved using `cin.ignore()`.

```cpp
cin.ignore();
getline(cin, name);
```

The `ignore()` function removes the leftover newline character from the input buffer, allowing `getline()` to work correctly.

# String Concatenation

Concatenation means joining two or more strings together to form a single string. It is one of the most commonly performed operations in string manipulation.

For example:

```text
"Hello" + " Mohit"
```

becomes:

```text
Hello Mohit
```

String concatenation is frequently used while generating messages, creating usernames, formatting output, constructing file paths, and processing text data.

## Concatenation Using `+` Operator

The simplest way to join strings is by using the `+` operator.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string firstName = "Mohit";
    string lastName = " Kumar";

    string fullName = firstName + lastName;

    cout << fullName;

    return 0;
}
```

### Output
Mohit Kumar

### 

The `+` operator creates a new string that contains all characters from both strings. The original strings remain unchanged.

Time Complexity: O(n + m)

where:

- n = length of first string
- m = length of second string

## Concatenation Using `append()`

The `append()` function is another way to join strings. Instead of creating a new string, it directly modifies the existing string.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name= "Akash";

    college.append(" Abhiram");

    cout << name;

    return 0;
}
```

### Output
Akash Abhiram

### 

The `append()` function adds the specified text at the end of the current string. It is often preferred when repeatedly adding text because it avoids creating unnecessary temporary strings.

# Modifying Strings

One of the major advantages of `std::string` is that its contents can be modified easily after creation. Characters and substrings can be added, removed, inserted, or replaced without manually handling memory.

Common modification operations include:

- Adding characters
- Removing characters
- Inserting text
- Erasing text
- Replacing text

## Adding Characters Using `push_back()`

The `push_back()` function adds a single character at the end of the string.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name = "Mohit";

    name.push_back('!');

    cout << name;

    return 0;
}
```

### Output
Mohit!

# Time Complexity
O(1)

### 

The character `'!'` is appended to the end of the string. This operation is very efficient and is commonly used when constructing strings character by character.

## Removing Characters Using `pop_back()`

The `pop_back()` function removes the last character from the string.

### Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string name = "Mohit!";

    name.pop_back();

    cout << name;

    return 0;
}
```

### Output
Mohit

### 

The last character of the string is removed. This operation is useful when unwanted characters need to be discarded from the end of a string.

# Summary

A string is a sequence of characters used to store textual information. In C++, strings are represented using the `std::string` class, which provides dynamic memory management and numerous built-in functions for easy string manipulation.

Key points to remember:

- Strings store sequences of characters.
- `std::string` is defined in the  header file.
- Strings can grow and shrink dynamically.
- Characters are stored sequentially and can be accessed using indexes.
- Strings provide many built-in functions such as `size()`, `length()`, `find()`, `append()`, and `substr()`.
- Traversal can be performed using indexes, range-based loops, or iterators.
- Strings are safer and easier to use than character arrays.
- String operations are heavily used in real-world applications involving text processing.

Strings form the foundation for many advanced topics such as pattern matching, text processing, parsing, competitive programming, and STL algorithms.




