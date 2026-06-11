# Map in C++ STL

A **Map** is an associative container provided by the C++ Standard Template Library (STL) that stores data in the form of **key-value pairs**. Each key is associated with exactly one value, allowing efficient storage, retrieval, and management of data.

Unlike arrays or vectors where elements are accessed using numerical indexes, maps use meaningful keys to access corresponding values. This makes maps extremely useful when data needs to be organized using identifiers such as student IDs, employee IDs, product codes, usernames, or account numbers.

Internally, a map is generally implemented using a **Self-Balancing Red-Black Tree**, which keeps the elements automatically sorted according to their keys. Because of this property, insertion, deletion, and searching operations can be performed efficiently.

A map has the following characteristics:

- Stores data as key-value pairs.
- Keys are unique.
- Elements are automatically sorted by key.
- Supports efficient searching and retrieval.
- Allows traversal in sorted order.
- Provides several useful functions for searching and range queries.

Maps are one of the most widely used STL containers because they combine efficient searching with automatic ordering.

# Why Do We Need Maps?

In real-world applications, data is often associated with identifiers.

Consider a college management system:
Student ID → Student Name

101 → Mohit
102 → Akash
103 → Hemesh
Searching for a student using an ID becomes easier when the data is stored as key-value pairs.

Similarly, in an e-commerce website:
Product Code → Product Name

P101 → Laptop
P102 → Keyboard
P103 → Mouse
Instead of searching through an entire array, maps allow direct access to data using keys.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/map-in-c-stl/1781179310976-d4f1cf04-3b3d-4e4e-b87a-344ca8e284fb.png)

Without maps:

- Searching becomes slower.
- Data organization becomes difficult.
- Managing large datasets becomes inefficient.

Maps solve these problems by providing structured and efficient storage.

# Real-World Applications of Maps

Maps are heavily used in software systems.

Examples include:

### Student Database

Student ID → Student Name

### Employee Management System

Employee ID → Employee Details

### Banking System

Account Number → Account Information

### Online Shopping Platform

Product ID → Product Details

### Library Management System

Book ID → Book Information

### DNS System

Domain Name → IP Address

Every time data is associated with a unique identifier, maps become an excellent choice.

# Map Header File

The map container is defined inside the following header file:

```cpp
#include <map>
```

Most programs also include:

```cpp
#include <iostream>
using namespace std;
```

for input and output operations.

# Declaration of Map

A map is declared by specifying the data type of the key and value.

## Syntax

```cpp
map<keyType, valueType> mapName;
```

## Example

```cpp
map<int, string> students;
```

Here:

- `int` represents the key type.
- `string` represents the value type.
- `students` is the map name.

# Creating and Initializing a Map

Maps can be initialized during declaration.

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> students =
    {
        {101, "Mohit"},
        {102, "Akash"},
        {103, "Hemesh"}
    };

    for(auto student : students)
    {
        cout << student.first
             << " -> "
             << student.second
             << endl;
    }

    return 0;
}
```

### Output
101 -> Mohit
102 -> Akash
103 -> Hemesh

### Explanation

Each element consists of:
Key → Value
The map automatically stores entries in sorted order according to keys.

# Memory Representation of Map

Consider:

```cpp
map<int, string> products;

products[103] = "Mouse";
products[101] = "Laptop";
products[102] = "Keyboard";
```

Even though elements are inserted randomly, the map stores them in sorted order.
101 → Laptop
102 → Keyboard
103 → Mouse
This automatic sorting is one of the major advantages of maps.

# Basic Operations on Map

The most commonly used operations are:

1. Insertion
2. Accessing Elements
3. Updating Elements
4. Finding Elements
5. Traversing
6. Deleting Elements

# Inserting Elements

Insertion means adding a new key-value pair into the map.

If the key already exists, insert() does not replace the existing value.

## Syntax

```cpp
mapName.insert({key, value});
```

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> courses;

    courses.insert({101, "C++"});
    courses.insert({102, "Python"});
    courses.insert({103, "Java"});

    for(auto course : courses)
    {
        cout << course.first
             << " "
             << course.second
             << endl;
    }

    return 0;
}
```

### Output
101 C++
102 Python
103 Java

### Explanation

Three course records are inserted into the map.

Each course code acts as a key and each course name acts as a value.

### Time Complexity

O(log n)

# Accessing Elements

Elements can be accessed using:

- [] operator
- at() function

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> employees =
    {
        {201, "Ravi"},
        {202, "Priya"},
        {203, "Kiran"}
    };

    cout << employees[201] << endl;

    cout << employees.at(202);

    return 0;
}
```

### Output
Ravi
Priya

### Explanation

The map uses keys to retrieve values.

Instead of accessing by position, we access by identifier.

### Time Complexity

O(log n)

# Difference Between [] and at()

Both functions access elements using keys.

### [] Operator

```cpp
employees[500];
```

If key 500 does not exist:
A new entry is automatically created.

### at() Function

```cpp
employees.at(500);
```

If key 500 does not exist:
Throws an exception.

Therefore, at() is generally safer when accidental insertion is not desired.

# Updating Elements

Existing values can be modified by assigning a new value to an existing key.

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> products =
    {
        {101, "Laptop"},
        {102, "Keyboard"}
    };

    products[102] = "Mechanical Keyboard";

    cout << products[102];

    return 0;
}
```

### Output
Mechanical Keyboard

### Explanation

The key already exists.

Only the value associated with that key is updated.

### Time Complexity

O(log n)

# Finding Elements

Searching is one of the strongest features of maps.

The find() function searches for a key.

## Syntax

```cpp
mapName.find(key);
```

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> books =
    {
        {1, "C++"},
        {2, "Python"},
        {3, "Java"}
    };

    auto result = books.find(2);

    if(result != books.end())
    {
        cout << "Book Found: "
             << result->second;
    }
    else
    {
        cout << "Book Not Found";
    }

    return 0;
}
```

### Output
Book Found: Python

### Explanation

The map searches for key 2.

Since the key exists, the corresponding value is returned.

### Time Complexity

O(log n)

# Traversing a Map

Traversal means visiting every key-value pair.

Maps always traverse in sorted order of keys.

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> products =
    {
        {103, "Mouse"},
        {101, "Laptop"},
        {102, "Keyboard"}
    };

    for(auto it = products.begin();
        it != products.end();
        it++)
    {
        cout << it->first
             << " -> "
             << it->second
             << endl;
    }

    return 0;
}
```

### Output
101 -> Laptop
102 -> Keyboard
103 -> Mouse

### Explanation

Although inserted in random order, traversal occurs in sorted order.

### Time Complexity

O(n)

# Deleting Elements

Elements can be removed using erase().

## Example Code

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int, string> inventory =
    {
        {101, "Laptop"},
        {102, "Monitor"},
        {103, "Mouse"}
    };

    inventory.erase(102);

    for(auto item : inventory)
    {
        cout << item.first
             << " "
             << item.second
             << endl;
    }

    return 0;
}
```

### Output
101 Laptop
103 Mouse

### Explanation

The key 102 and its associated value are removed from the map.

### Time Complexity

O(log n)

# Useful Map Functions

### size()

Returns total number of key-value pairs.

### empty()

Checks whether the map is empty.

### clear()

Removes all elements from the map.

### count()

Checks whether a key exists.

Returns:
1 → Key Exists
0 → Key Does Not Exist

### lower_bound()

Returns iterator pointing to the first element whose key is greater than or equal to the given key.

### upper_bound()

Returns iterator pointing to the first element whose key is strictly greater than the given key.

### swap()

Swaps contents of two maps.

# Difference Between Map and Unordered Map

| Feature | Map | Unordered Map |
| --- | --- | --- |
| Internal Structure | Red-Black Tree | Hash Table |
| Ordering | Sorted | Unsorted |
| Search Complexity | O(log n) | O(1) Average |
| Traversal | Sorted Order | Random Order |
| lower_bound() | Available | Not Available |
| upper_bound() | Available | Not Available |

# Advantages of Map

### Automatic Sorting

Elements remain sorted according to keys.

### Fast Searching

Searching is highly efficient.

### Unique Keys

Duplicate keys are not allowed.

### Easy Data Organization

Data can be organized naturally using identifiers.

### Useful STL Functions

Provides powerful searching and range operations.

# Limitations of Map

### Slower Than Unordered Map

Because of tree balancing operations.

### Additional Memory Usage

Tree nodes require extra memory.

### No Duplicate Keys

Only unique keys are allowed.

### Not Suitable for Index-Based Access

Elements must be accessed using keys.

# Time Complexity of Common Operations

| Operation | Complexity |
| --- | --- |
| Insert | O(log n) |
| Search | O(log n) |
| Update | O(log n) |
| Delete | O(log n) |
| Traversal | O(n) |
| Access by Key | O(log n) |

# Summary

A Map is an associative container in C++ STL that stores data as key-value pairs while maintaining keys in sorted order. It is implemented using a self-balancing Red-Black Tree, providing efficient insertion, deletion, searching, and traversal operations. Maps are widely used in databases, management systems, banking software, inventory systems, and applications where data must be associated with unique identifiers. Their automatic sorting, fast searching, and powerful STL functions make them one of the most important containers in modern C++ programming.




