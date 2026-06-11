# Set in C++ STL

A **Set** is an associative container provided by the C++ Standard Template Library (STL) that stores **unique elements** in a **sorted order**. Unlike vectors or arrays, sets automatically maintain the order of elements and prevent duplicate values from being stored.

Internally, a set is usually implemented using a **Self-Balancing Binary Search Tree (Red-Black Tree)**. This allows insertion, deletion, and searching operations to be performed efficiently.

A set has the following characteristics:

- Stores only unique elements.
- Automatically sorts elements in ascending order by default.
- Duplicate values are ignored.
- Supports efficient searching, insertion, and deletion.
- Provides ordered traversal.
- Supports useful functions such as `find()`, `count()`, `lower_bound()`, and `upper_bound()`.

Because of these features, sets are widely used when uniqueness and sorted data are required.

# Why Do We Need Sets?

Consider a college event registration system.
Many students may accidentally register multiple times.
Student IDs Entered:

101
102
101
103
102
104
If we store these values in a vector, duplicates will remain.

However, when stored in a set:
101
102
103
104
Duplicate values are automatically removed.

This makes sets extremely useful when:

- Duplicate values should not exist.
- Data must remain sorted.
- Fast searching is required.
- Unique records need to be maintained.

# Real-World Applications of Sets

Sets are used in many real-world software applications.

### Unique Student IDs

Student ID Collection
Each student ID must appear only once.

### Website Usernames

Username Collection
Two users cannot have the same username.

### Unique Product Codes

Product IDs
Each product should have a unique identifier.

### Search Engine Keywords

Keyword Database
Duplicate keywords are unnecessary.

### Library Book IDs

Book Identification System
Every book receives a unique ID.

### Voting Systems

Voter IDs
A voter should only vote once.

# Set Header File

The set container is defined inside:

```cpp
#include <set>
```

Most programs also include:

```cpp
#include <iostream>
using namespace std;
```

for input and output operations.

# Declaration of Set

A set can be declared by specifying the data type of elements.

## Syntax

```cpp
set<dataType> setName;
```

## Example

```cpp
set<int> studentIDs;
```

Here:

- `int` represents the data type.
- `studentIDs` is the name of the set.

# Creating and Initializing a Set

Sets can be initialized during declaration.

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> marks =
    {
        85,
        90,
        75,
        85,
        95,
        90
    };

    for(int value : marks)
    {
        cout << value << " ";
    }

    return 0;
}
```

### Output
75 85 90 95

### Explanation

Although duplicate values were inserted, the set stores only unique values and automatically sorts them.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/set-in-c-stl/1781180255955-0cc5b000-612c-4cb0-93e8-c6c1f86a302b.png)

# Memory Representation of Set

Consider:

```cpp
set<int> numbers;

numbers.insert(50);
numbers.insert(20);
numbers.insert(70);
numbers.insert(10);
```

Internally, elements are arranged in sorted order.
10
20
50
70
Even though elements are inserted randomly, the set automatically maintains sorting.

# Basic Operations on Set

The most commonly used operations are:

1. Insertion
2. Searching
3. Traversal
4. Deletion
5. Size Check
6. Empty Check

# Inserting Elements

Insertion means adding elements into the set.

Duplicate elements are ignored.

## Syntax

```cpp
setName.insert(value);
```

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<string> courses;

    courses.insert("C++");
    courses.insert("Python");
    courses.insert("Java");
    courses.insert("Python");

    for(auto course : courses)
    {
        cout << course << endl;
    }

    return 0;
}
```

### Output
C++
Java
Python

### Explanation

Although "Python" was inserted twice, it appears only once because sets do not allow duplicates.

### Time Complexity

O(log n)

# Searching Elements

Searching is performed using `find()` or `count()`.

## Using find()

The `find()` function searches for an element and returns an iterator.

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> rollNumbers =
    {
        101,
        102,
        103,
        104
    };

    auto result = rollNumbers.find(103);

    if(result != rollNumbers.end())
    {
        cout << "Roll Number Found";
    }
    else
    {
        cout << "Roll Number Not Found";
    }

    return 0;
}
```

### Output
Roll Number Found

# Time Complexity
O(log n)

# Using count()

The `count()` function checks whether an element exists.

Since duplicate elements are not allowed, the result is either:
0 → Not Present
1 → Present

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> ids =
    {
        10,
        20,
        30
    };

    cout << ids.count(20);

    return 0;
}
```

### Output
1

# Traversing a Set

Traversal means visiting every element in the set.

Elements are always visited in sorted order.

## Using Range-Based Loop

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> numbers =
    {
        40,
        10,
        30,
        20
    };

    for(int value : numbers)
    {
        cout << value << " ";
    }

    return 0;
}
```

### Output
10 20 30 40

### Explanation

The values are displayed in ascending order even though they were inserted randomly.

# Traversing Using Iterators

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<string> technologies =
    {
        "Python",
        "Java",
        "C++"
    };

    for(auto it = technologies.begin();
        it != technologies.end();
        it++)
    {
        cout << *it << endl;
    }

    return 0;
}
```

### Output
C++
Java
Python

# Time Complexity
O(n)

# Deleting Elements

Elements can be removed using `erase()`.

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> values =
    {
        10,
        20,
        30,
        40
    };

    values.erase(20);

    for(int value : values)
    {
        cout << value << " ";
    }

    return 0;
}
```

### Output
10 30 40

### Explanation

The value 20 is removed from the set.

### Time Complexity

O(log n)

# Size of Set

The `size()` function returns the number of elements present in the set.

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> numbers =
    {
        10,
        20,
        30
    };

    cout << numbers.size();

    return 0;
}
```

### Output
3

# Checking Whether Set is Empty

The `empty()` function checks whether the set contains elements.

## Example Code

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> data;

    if(data.empty())
    {
        cout << "Set is Empty";
    }

    return 0;
}
```

### Output
Set is Empty

# lower_bound() and upper_bound()

These are powerful functions available in ordered sets.

## lower_bound()

Returns the first element greater than or equal to the given value.

### Example

```cpp
set<int> s = {10, 20, 30, 40};

auto it = s.lower_bound(25);
```

Result:
30

## upper_bound()

Returns the first element strictly greater than the given value.

### Example

```cpp
set<int> s = {10, 20, 30, 40};

auto it = s.upper_bound(30);
```

Result:
40

These functions are extremely useful in competitive programming and searching applications.

# Useful Set Functions

| Function | Description |
| --- | --- |
| insert() | Inserts a new element |
| erase() | Removes an element |
| find() | Searches for an element |
| count() | Checks element existence |
| size() | Returns number of elements |
| empty() | Checks whether set is empty |
| clear() | Removes all elements |
| lower_bound() | First element ≥ value |
| upper_bound() | First element &gt; value |
| begin() | Iterator to first element |
| end() | Iterator after last element |

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/set-in-c-stl/1781180303147-0cc5b000-612c-4cb0-93e8-c6c1f86a302b.png)

# Set vs Vector

| Feature | Set | Vector |
| --- | --- | --- |
| Duplicates | Not Allowed | Allowed |
| Ordering | Automatically Sorted | Insertion Order |
| Search | O(log n) | O(n) |
| Random Access | Not Supported | Supported |
| Insert/Delete | O(log n) | O(n) in middle |

# Set vs Unordered Set

| Feature | Set | Unordered Set |
| --- | --- | --- |
| Internal Structure | Red-Black Tree | Hash Table |
| Ordering | Sorted | Unsorted |
| Search | O(log n) | O(1) Average |
| lower_bound() | Supported | Not Supported |
| upper_bound() | Supported | Not Supported |

# Advantages of Set

### Automatic Sorting

Elements always remain sorted.

### No Duplicate Values

Uniqueness is guaranteed.

### Efficient Searching

Searching operations are fast.

### Useful Range Functions

Supports lower_bound() and upper_bound().

### Ideal for Unique Data

Perfect when duplicates are not allowed.

# Limitations of Set

### Slower Than Unordered Set

Because tree balancing is required.

### No Random Access

Cannot access elements using indexes.

### Extra Memory Usage

Tree nodes require additional memory.

### Duplicate Elements Not Allowed

Not suitable when duplicate values are required.

# Time Complexity of Common Operations

| Operation | Complexity |
| --- | --- |
| Insert | O(log n) |
| Search | O(log n) |
| Delete | O(log n) |
| Count | O(log n) |
| lower_bound() | O(log n) |
| upper_bound() | O(log n) |
| Traversal | O(n) |

# Summary

A Set is an associative container in C++ STL that stores unique elements in sorted order. It is implemented using a Red-Black Tree, allowing efficient insertion, deletion, and searching operations. Sets automatically remove duplicates and maintain sorting, making them ideal for applications involving unique records, IDs, usernames, keywords, and other distinct values. They provide powerful searching capabilities along with ordered traversal, making them one of the most important containers in the STL.




