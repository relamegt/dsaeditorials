# Vector in C++ STL

## Introduction to Vector

A vector is one of the most commonly used containers provided by the Standard Template Library (STL). It is a dynamic array that can automatically change its size during program execution.

Unlike traditional arrays, vectors do not require a fixed size at the time of declaration. As elements are added or removed, the vector automatically manages memory and adjusts its size accordingly.

Vectors store elements in contiguous memory locations, similar to arrays. Because of this, they provide fast access to elements using indexes while also offering the flexibility of dynamic resizing.

The vector container is implemented as a template class in STL, which means it can store any data type such as:

- int
- float
- double
- char
- string
- structures
- classes
- user-defined data types

Because of their simplicity, flexibility, and efficiency, vectors are widely used in competitive programming, software development, data analysis, game development, and machine learning applications.

### Practice Problem

**Problem Statement:** Create a vector of integers, add elements 10, 20, and 30 using `push_back`, and print them and the vector's size.

### Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec;
    vec.push_back(10);
    vec.push_back(20);
    vec.push_back(30);
    cout << "Vector elements: ";
    for (int x : vec) {
        cout << x << " ";
    }
    cout << "\nVector size: " << vec.size() << endl;
    return 0;
}
```

### Output
Vector elements: 10 20 30 
Vector size: 3

## Why Do We Need Vectors?

Before vectors were introduced, programmers primarily used arrays to store collections of data.

Example:

```cpp
int marks[5];
```

The above array can store exactly five elements.

Although arrays are fast and easy to use, they have several limitations.

### Practice Problem

**Problem Statement:** Demonstrate how a vector dynamically resizes as elements are added, showing the size and capacity at each stage, compared to a static array.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers;
    for (int i = 1; i <= 5; ++i) {
        numbers.push_back(i * 10);
        cout << "Added " << i * 10 << " -> Size: " << numbers.size() << ", Capacity: " << numbers.capacity() << "\n";
    }
    return 0;
}
```

### Output
Added 10 -> Size: 1, Capacity: 1
Added 20 -> Size: 2, Capacity: 2
Added 30 -> Size: 3, Capacity: 4
Added 40 -> Size: 4, Capacity: 4
Added 50 -> Size: 5, Capacity: 8

### Fixed Size

The size of an array cannot be changed after creation.

For example:

```cpp
int marks[5];
```

If later we need to store ten elements instead of five, the existing array cannot be expanded.

A new larger array must be created and all elements must be copied manually.

### Memory Wastage

Sometimes programmers allocate more memory than required.

Example:

```cpp
int marks[100];
```

If only 20 elements are used, the remaining 80 locations remain unused.

This results in memory wastage.

### Difficult Memory Management

Dynamic arrays require manual memory allocation using:

```cpp
new
```

and memory deallocation using:

```cpp
delete
```

Improper handling can lead to:

- Memory leaks
- Dangling pointers
- Program crashes

### Complex Resizing

Whenever the array becomes full, programmers must:

1. Create a larger array.
2. Copy existing elements.
3. Delete the old array.

This process increases complexity.

Vectors solve all these problems by automatically managing memory and resizing themselves whenever required.

## Features of Vector

Vectors provide several useful features that make them superior to traditional arrays in many situations.

### Practice Problem

**Problem Statement:** Showcase three key features of vectors: random access, dynamic resizing, and standard sorting algorithm compatibility.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> vec = {40, 10, 30, 20};
    cout << "Random Access (index 2): " << vec[2] << "\n";
    vec.push_back(50);
    cout << "Size after push_back: " << vec.size() << "\n";
    sort(vec.begin(), vec.end());
    cout << "Sorted elements: ";
    for(int x : vec) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Random Access (index 2): 30
Size after push_back: 5
Sorted elements: 10 20 30 40 50

### Dynamic Resizing

Vectors automatically increase or decrease their size as elements are inserted or removed.

The programmer does not need to worry about memory allocation.

### Fast Random Access

Elements can be accessed using indexes just like arrays.

Example:

```cpp
marks[3]
```

This operation is extremely fast because vector elements are stored in contiguous memory locations.

### Automatic Memory Management

Vectors automatically allocate and deallocate memory.

This reduces the chances of memory-related errors.

### STL Compatibility

Vectors work seamlessly with STL algorithms such as:

- sort()
- find()
- count()
- reverse()
- binary_search()

### Iterator Support

Vectors provide iterator support, making traversal easier and allowing compatibility with STL algorithms.

### Type Safety

Vectors store elements of a specific data type and provide better type checking than traditional C-style arrays.

## Array vs Vector

Both arrays and vectors are used to store collections of elements, but they differ in several important aspects.

| Feature | Array | Vector |
| --- | --- | --- |
| Size | Fixed | Dynamic |
| Memory Management | Manual | Automatic |
| Resizing | Not Possible | Automatic |
| STL Support | Limited | Full Support |
| Safety | Less Safe | Safer |
| Ease of Use | Moderate | Easy |
| Iterator Support | No | Yes |

### Practice Problem

**Problem Statement:** Write a program that declares a C-style array of size 3 and a std::vector. Append a 4th element to the vector and print the contents of both.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int arr[3] = {1, 2, 3};
    vector<int> vec = {1, 2, 3};
    vec.push_back(4);
    cout << "Array elements: ";
    for(int i = 0; i < 3; ++i) cout << arr[i] << " ";
    cout << "\nVector elements: ";
    for(int x : vec) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Array elements: 1 2 3 
Vector elements: 1 2 3 4

## Example Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> marks = {85, 90, 78, 95};

    for(auto it = marks.begin();
        it != marks.end();
        it++)
    {
        cout << *it << " ";
    }

    return 0;
}
```

### Output
85 90 78 95

### Explanation

The begin() function returns an iterator pointing to the first element of the vector, while end() returns an iterator pointing just after the last element.

By incrementing the iterator using `++it`, we can traverse all elements of the vector sequentially.

In modern C++ programming, vectors are generally preferred unless a fixed-size collection is required.

## Vector Header File

The vector container is defined inside the `<vector>` header file.

Before using vectors, this header must be included.Practice Problem**Problem Statement:**  Write a simple C++ program that uses the `<vector>` header to declare a character vector and output a confirmation message.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<char> v = {'X', 'Y', 'Z'};
    std::cout << "Header <vector> included successfully. Size: " << v.size() << "\n";
    return 0;
}
```

### Output
3Header <vector> included successfully. Size: 3

Most programs also include:

```cpp
#include <iostream>
using namespace std;
```

for input and output operations.

## Declaration of Vector

A vector can be declared similarly to other variables.

### Practice Problem

**Problem Statement:** Declare three empty vectors: one of int, one of float, and one of std::string. Print the size of each vector to confirm they are empty.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<int> intVec;
    vector<float> floatVec;
    vector<string> stringVec;
    cout << "Int vector size: " << intVec.size() << "\n";
    cout << "Float vector size: " << floatVec.size() << "\n";
    cout << "String vector size: " << stringVec.size() << "\n";
    return 0;
}
```

### Output
Int vector size: 0
Float vector size: 0
String vector size: 0

### Syntax

```cpp
vector<dataType> vectorName;
```

### Example

```cpp
vector<int> marks;
```

The above statement creates an empty vector capable of storing integer values.

### More Examples

```cpp
vector<float> prices;
```

```cpp
vector<string> studentNames;
```

```cpp
vector<char> grades;
```

Each vector stores elements of only one specific data type.

## Initialization of Vector

Vectors can be initialized in multiple ways depending on requirements.

### Practice Problem

**Problem Statement:** Demonstrate five different methods to initialize vectors (empty, fixed size, fixed size with value, initializer list, and copy constructor) and print their elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v1;
    vector<int> v2(3);
    vector<int> v3(3, 7);
    vector<int> v4 = {10, 20, 30};
    vector<int> v5(v4);
    
    cout << "v3: ";
    for(int x : v3) cout << x << " ";
    cout << "\nv5: ";
    for(int x : v5) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
v3: 7 7 7 
v5: 10 20 30

### Empty Vector

```cpp
vector<int> numbers;
```

Creates an empty vector.

### Vector with Fixed Size

```cpp
vector<int> numbers(5);
```

Creates a vector containing five elements initialized with default values.

Memory representation:

```text
0 0 0 0 0
```

### Vector with Fixed Size and Value

```cpp
vector<int> marks(4, 100);
```

Memory representation:

```text
100 100 100 100
```

All elements are initialized with the value 100.

### Initializer List

```cpp
vector<int> marks = {85, 90, 78, 92};
```

Memory representation:

```text
85 90 78 92
```

This is one of the most commonly used initialization methods.

### Copy Initialization

```cpp
vector<int> original = {10, 20, 30};

vector<int> copy(original);
```

The copy vector contains the same elements as the original vector.

## Internal Working of Vector

Many beginners assume that vectors simply keep adding elements indefinitely.

Internally, vectors manage memory using two important concepts:

### Practice Problem

**Problem Statement:** Verify how capacity changes as elements are added, demonstrating that capacity increases exponentially when the size exceeds the current limit.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    for(int i = 0; i < 6; ++i) {
        v.push_back(i);
        cout << "Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    }
    return 0;
}
```

### Output
Size: 1, Capacity: 1
Size: 2, Capacity: 2
Size: 3, Capacity: 4
Size: 4, Capacity: 4
Size: 5, Capacity: 8
Size: 6, Capacity: 8

### Size

Size represents the number of elements currently stored in the vector.

Example:

```text
10 20 30 40
```

Size = 4

### Capacity

Capacity represents the total number of elements that can be stored before the vector needs additional memory.

Example:

```text
Size = 4
Capacity = 8
```

The vector can still store four additional elements without allocating new memory.

### Memory Reallocation

Suppose a vector has:

```text
Size = 4
Capacity = 4
```

Memory:

```text
10 20 30 40
```

When another element is inserted:

```text
10 20 30 40 50
```

The capacity becomes insufficient.

The vector then:

1. Allocates a larger memory block.
2. Copies all existing elements.
3. Releases old memory.
4. Stores the new element.

This process is called **reallocation**.

Because reallocation involves copying elements, excessive resizing may affect performance.

This is why functions such as `reserve()` are useful when the approximate size is known beforehand.

## Inserting Elements into a Vector

One of the biggest advantages of vectors is their ability to add elements dynamically during program execution.

Unlike arrays, vectors do not have a fixed size. New elements can be inserted whenever required, and the vector automatically expands its storage if necessary.

STL provides multiple functions for inserting elements into a vector.

### push_back()

The `push_back()` function inserts an element at the end of the vector.

Example:

```text
Before:

10 20 30

After push_back(40):

10 20 30 40
```

This is the most commonly used insertion function because adding elements at the end is highly efficient.

**Time Complexity:** O(1) Average

#### Practice Problem
**Problem Statement:** Create an empty vector and push numbers 5, 10, 15, and 20 into it using `push_back()`. Print all elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.push_back(5);
    v.push_back(10);
    v.push_back(15);
    v.push_back(20);
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
5 10 15 20

### emplace_back()

The `emplace_back()` function constructs an object directly at the end of the vector.

Unlike `push_back()`, which first creates an object and then copies it into the vector, `emplace_back()` creates the object directly inside the vector memory.

Benefits:

- Better performance
- Avoids unnecessary copying
- Useful for complex objects

#### Practice Problem
**Problem Statement:** Define a custom struct `Product` with two attributes: `id` (int) and `price` (double). Create a vector of `Product` and use `emplace_back` to add elements in-place.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Product {
    int id;
    double price;
    Product(int i, double p) : id(i), price(p) {}
};

int main() {
    vector<Product> products;
    products.emplace_back(101, 49.99);
    products.emplace_back(102, 9.99);
    for(const auto& p : products) {
        cout << "Product ID: " << p.id << ", Price: $" << p.price << "\n";
    }
    return 0;
}
```

### Output
Product ID: 101, Price: $49.99
Product ID: 102, Price: $9.99

### insert()

The `insert()` function allows insertion at any position inside the vector.

Example:

```text
Before:

10 30 40

Insert 20 at index 1

After:

10 20 30 40
```

When inserting in the middle, all elements after that position must shift one position to the right.

**Time Complexity:** O(n)

#### Practice Problem
**Problem Statement:** Create a vector with elements {1, 2, 4, 5}. Insert the number 3 at index 2 using the `insert()` function and print the final vector.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 4, 5};
    v.insert(v.begin() + 2, 3);
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
1 2 3 4 5

## Accessing Elements in a Vector

Accessing elements means retrieving values stored inside the vector.

Since vectors store elements in contiguous memory locations, accessing elements is extremely fast.

### Using Index Operator []

The simplest method for accessing elements.

Example:

```text
Index : 0  1  2  3

Value : 10 20 30 40
```

Accessing:

```cpp
marks[2]
```

Returns:

```text
30
```

**Time Complexity:** O(1)

#### Practice Problem
**Problem Statement:** Create a vector of floats, access and print elements using the index operator `[]`, and modify the element at index 1.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<float> prices = {1.99f, 2.99f, 3.99f};
    cout << "Before update: " << prices[1] << "\n";
    prices[1] = 5.99f;
    cout << "After update: " << prices[1] << "\n";
    return 0;
}
```

### Output
Before update: 2.99
After update: 5.99

### Using at()

The `at()` function provides bounds checking.

Example:

```cpp
marks.at(2)
```

Returns:

```text
30
```

Difference between `[]` and `at()`:

| Feature | [] | at() |
| --- | --- | --- |
| Speed | Faster | Slightly Slower |
| Bounds Checking | No | Yes |
| Safety | Lower | Higher |

If an invalid index is used with `at()`, an exception is generated.

This makes it safer than the index operator.

#### Practice Problem
**Problem Statement:** Show bounds checking with `at()` by safely accessing an invalid index (e.g. index 5 in a vector of size 3) inside a try-catch block.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30};
    try {
        cout << "Accessing index 1: " << v.at(1) << "\n";
        cout << "Accessing index 5: " << v.at(5) << "\n";
    } catch(const out_of_range& e) {
        cout << "Caught out of range exception safely.\n";
    }
    return 0;
}
```

### Output
Accessing index 1: 20
Caught out of range exception safely.

### front()

Returns the first element of the vector.

Example:

```text
10 20 30 40
```

Returns:

```text
10
```

#### Practice Problem
**Problem Statement:** Print the first element of a vector containing names using `front()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> names = {"Alice", "Bob", "Charlie"};
    cout << "First name: " << names.front() << "\n";
    return 0;
}
```

### Output
First name: Alice

### back()

Returns the last element of the vector.

Example:

```text
10 20 30 40
```

Returns:

```text
40
```

#### Practice Problem
**Problem Statement:** Print the last element of a vector containing names using `back()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> names = {"Alice", "Bob", "Charlie"};
    cout << "Last name: " << names.back() << "\n";
    return 0;
}
```

### Output
Last name: Charlie

## Updating Elements

Updating means replacing an existing value with a new value.

Since vectors support direct indexing, updating elements is straightforward.

Example:

```text
Before:

10 20 30 40
```

Updating index 1:

```text
10 50 30 40
```

The old value 20 is replaced by 50.

Applications:

- Updating student marks
- Modifying employee salaries
- Changing product quantities
- Editing user information

**Time Complexity:** O(1)

### Practice Problem

**Problem Statement:** Write a program that takes a vector of student test scores and updates the score at index 2 from 85 to 98.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> scores = {90, 75, 85, 92};
    cout << "Before update: " << scores[2] << "\n";
    scores[2] = 98;
    cout << "After update: " << scores[2] << "\n";
    return 0;
}
```

### Output
Before update: 85
After update: 98

## Finding Vector Size

The size of a vector represents the total number of elements currently stored.

Consider:

```text
10 20 30 40 50
```

Size:

```text
5
```

The `size()` function is commonly used:

- Loop control
- Validations
- Searching
- Traversal operations

Unlike arrays, vector size can change during execution.

This makes `size()` extremely useful.

**Time Complexity:** O(1)

### Practice Problem

**Problem Statement:** Declare a vector and print its size before and after inserting elements using `push_back()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    cout << "Initial size: " << v.size() << "\n";
    v.push_back(10);
    v.push_back(20);
    cout << "Size after push: " << v.size() << "\n";
    return 0;
}
```

### Output
Initial size: 0
Size after push: 2

## Capacity of a Vector

Many students confuse size and capacity.

### Practice Problem

**Problem Statement:** Create a vector, reserve space for 20 elements, and print the size and capacity before and after reserving.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3};
    cout << "Initial Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    v.reserve(20);
    cout << "After reserve(20) - Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Initial Size: 3, Capacity: 3
After reserve(20) - Size: 3, Capacity: 20

### Size

Number of elements currently stored.

Example:

```text
10 20 30
```

Size = 3

### Capacity

Maximum number of elements that can currently be stored without allocating new memory.

Example:

```text
Size = 3
Capacity = 8
```

The vector can still accommodate five more elements before resizing.

### Why Capacity Exists

Frequent memory allocation is expensive.

To improve performance, vectors allocate extra memory in advance.

This reduces the number of reallocations required.

### capacity()

Returns the current capacity.

#### Practice Problem
**Problem Statement:** Create an empty vector, reserve memory for 50 elements, and check the capacity using `capacity()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(50);
    cout << "Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Capacity: 50

### reserve()

Reserves memory beforehand.

Example scenario:

Suppose we know that 10,000 student records will be inserted.

Instead of allowing repeated reallocations, we can reserve memory initially.

Benefits:

- Better performance
- Fewer reallocations
- Faster insertion operations

#### Practice Problem
**Problem Statement:** Demonstrate how `reserve()` prevents multiple capacity growth events when pushing 10 elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(10);
    cout << "Initial Capacity: " << v.capacity() << "\n";
    for(int i = 0; i < 10; ++i) v.push_back(i);
    cout << "Final Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Initial Capacity: 10
Final Capacity: 10

## Traversing a Vector

Traversing means visiting each element one by one.

This is one of the most common operations performed on vectors.

### Traversing Using Index

Every element has a unique index.

Example:

```text
Index : 0 1 2 3

Value : 10 20 30 40
```

The loop starts from index 0 and continues until the last element.

Advantages:

- Easy to understand
- Direct access to indexes

#### Practice Problem
**Problem Statement:** Traverse a vector of doubles using index-based loop and print the elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> weights = {5.4, 6.2, 7.8};
    for(size_t i = 0; i < weights.size(); ++i) {
        cout << weights[i] << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
5.4 6.2 7.8

### Traversing Using Range-Based Loop

Modern C++ introduced range-based loops to simplify traversal.

Instead of manually handling indexes, each element is accessed automatically.

Advantages:

- Cleaner syntax
- Less code
- Better readability

#### Practice Problem
**Problem Statement:** Traverse a vector of integers using range-based loop and print the elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers = {100, 200, 300};
    for(int val : numbers) {
        cout << val << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
100 200 300

### Traversing Using Iterators

Vectors fully support iterators.

Iterators provide a container-independent way of traversal.

Benefits:

- Works with STL algorithms
- Flexible and reusable
- Essential for advanced STL programming

Applications:

- Sorting
- Searching
- Counting
- Reversing

**Time Complexity:** O(n)

#### Practice Problem
**Problem Statement:** Traverse a vector of strings using a standard iterator and print each string.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> fruits = {"Apple", "Banana", "Cherry"};
    for(auto it = fruits.begin(); it != fruits.end(); ++it) {
        cout << *it << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Apple Banana Cherry

## Deleting Elements from a Vector

Vectors provide multiple functions for removing elements.

### pop_back()

Removes the last element.

Example:

```text
Before:

10 20 30 40
```

After:

```text
10 20 30
```

This operation is highly efficient because no shifting is required.

**Time Complexity:** O(1)

#### Practice Problem
**Problem Statement:** Write a program that pushes 3 values into a vector, removes the last element using `pop_back()`, and prints the remaining elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30};
    v.pop_back();
    cout << "Elements after pop_back: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Elements after pop_back: 10 20

### erase()

Removes elements from any position.

Example:

```text
Before:

10 20 30 40
```

Remove 20:

```text
10 30 40
```

Since elements must shift left to fill the gap, this operation is slower.

**Time Complexity:** O(n)

#### Practice Problem
**Problem Statement:** Create a vector with values {10, 20, 30, 40, 50}. Erase the element at index 2 (value 30) and print the remaining elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};
    v.erase(v.begin() + 2);
    cout << "Elements after erase: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Elements after erase: 10 20 40 50

### clear()

Removes all elements from the vector.

Example:

```text
Before:

10 20 30 40
```

After:

```text
Empty Vector
```

The vector size becomes zero.

**Time Complexity:** O(n)

#### Practice Problem
**Problem Statement:** Create a vector of floats with 3 elements, clear it using `clear()`, and verify its size and whether it is empty.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<float> v = {1.5f, 2.5f, 3.5f};
    v.clear();
    cout << "After clear - Size: " << v.size() << ", Is Empty: " << (v.empty() ? "Yes" : "No") << "\n";
    return 0;
}
```

### Output
After clear - Size: 0, Is Empty: Yes

## Checking Whether a Vector is Empty

Before accessing elements, it is often useful to verify whether the vector contains any data.

The `empty()` function performs this check.

Example:

```text
[]
```

Result:

```text
True
```

Example:

```text
10 20 30
```

Result:

```text
False
```

Applications:

- Preventing runtime errors
- Input validation
- Safe element access

**Time Complexity:** O(1)

### Practice Problem

**Problem Statement:** Write a program that uses `empty()` to check if a vector is empty, adds an element, and checks again.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    cout << "Empty before push? " << (v.empty() ? "Yes" : "No") << "\n";
    v.push_back(9);
    cout << "Empty after push? " << (v.empty() ? "Yes" : "No") << "\n";
    return 0;
}
```

### Output
Empty before push? Yes
Empty after push? No

## Multidimensional Vectors

A vector can store another vector as its element.

This allows the creation of multidimensional structures.

### Two-Dimensional Vector

A two-dimensional vector behaves like a table or matrix.

Example:

```text
1 2 3

4 5 6

7 8 9
```

Applications:

- Matrix operations
- Student mark sheets
- Image processing
- Spreadsheet software
- Game boards

#### Practice Problem
**Problem Statement:** Initialize a 2D vector matrix of size 3x3 with sequential numbers from 1 to 9. Print the elements row by row.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    for(size_t r = 0; r < matrix.size(); ++r) {
        for(size_t c = 0; c < matrix[r].size(); ++c) {
            cout << matrix[r][c] << " ";
        }
        cout << "\n";
    }
    return 0;
}
```

### Output
1 2 3 
4 5 6 
7 8 9

### Three-Dimensional Vector

A vector can also store multiple two-dimensional vectors.

Applications:

- Scientific simulations
- 3D graphics
- Medical imaging
- Machine learning datasets

One of the major advantages of multidimensional vectors is flexibility.

Rows and columns can grow dynamically during execution.

Unlike traditional multidimensional arrays, dimensions do not need to be fixed beforehand.

#### Practice Problem
**Problem Statement:** Create a 3D vector representing a 2x2x2 space grid, fill all cells with 0 except a single cell at [1][0][1] with the value 99, and print that cell.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<vector<int>>> grid(2, vector<vector<int>>(2, vector<int>(2, 0)));
    grid[1][0][1] = 99;
    cout << "grid[1][0][1] value: " << grid[1][0][1] << "\n";
    return 0;
}
```

### Output
grid[1][0][1] value: 99

## Commonly Used Vector Functions

The vector container provides many built-in member functions that simplify data storage, retrieval, insertion, deletion, and memory management.

These functions eliminate the need to manually implement common operations and make vectors easy to use in real-world applications.

| Function | Description |
| --- | --- |
| push_back() | Inserts an element at the end of the vector |
| emplace_back() | Constructs and inserts an element at the end |
| pop_back() | Removes the last element |
| insert() | Inserts element at a specified position |
| erase() | Removes element from a specified position |
| clear() | Removes all elements from the vector |
| size() | Returns the current number of elements |
| capacity() | Returns the current storage capacity |
| empty() | Checks whether the vector is empty |
| resize() | Changes the size of the vector |
| reserve() | Reserves memory for future elements |
| front() | Returns the first element |
| back() | Returns the last element |
| at() | Accesses element with bounds checking |
| begin() | Returns iterator to the first element |
| end() | Returns iterator to the position after the last element |
| rbegin() | Returns reverse iterator to the last element |
| rend() | Returns reverse iterator before the first element |
| swap() | Exchanges contents of two vectors |

Understanding these functions is essential because they are frequently used in competitive programming, interviews, and real-world software development.

### Practice Problem

**Problem Statement:** Implement a single C++ program that utilizes at least five member functions of `std::vector` (such as `push_back()`, `size()`, `front()`, `back()`, and `empty()`) and prints the intermediate results.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    cout << "Empty? " << (v.empty() ? "Yes" : "No") << "\n";
    v.push_back(12);
    v.push_back(34);
    cout << "Size: " << v.size() << "\n";
    cout << "Front: " << v.front() << ", Back: " << v.back() << "\n";
    v.pop_back();
    cout << "New Back: " << v.back() << "\n";
    return 0;
}
```

### Output
Empty? Yes
Size: 2
Front: 12, Back: 34
New Back: 12

## Real World Applications of Vectors

Vectors are used extensively in modern software systems because data sizes are rarely fixed in real applications.

### Student Management Systems

A college application may need to store student records.

Since the number of students can change every year, vectors provide a flexible storage solution.

Example:

```text
Student Records

Mohit
Akash
Hemesh
Abhiram
```

New students can be added without modifying existing code.

#### Practice Problem
**Problem Statement:** Create a system to store student records (Name and Roll Number) using a vector of structs, and print them out.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Student {
    string name;
    int roll;
};

int main() {
    vector<Student> classList;
    classList.push_back({"Mohit", 101});
    classList.push_back({"Akash", 102});
    for(const auto& s : classList) {
        cout << "Name: " << s.name << ", Roll: " << s.roll << "\n";
    }
    return 0;
}
```

### Output
Name: Mohit, Roll: 101
Name: Akash, Roll: 102

### Online Shopping Applications

Shopping carts continuously change as users add or remove products.

Example:

```text
Shopping Cart

Laptop
Mouse
Keyboard
Headphones
```

Vectors make dynamic modifications simple.

#### Practice Problem
**Problem Statement:** Simulate an online shopping cart where user can push new item names to a vector, then print all items in the cart.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> cart = {"Laptop", "Mouse"};
    cart.push_back("Keyboard");
    cout << "Shopping Cart Items:\n";
    for(const auto& item : cart) {
        cout << "- " << item << "\n";
    }
    return 0;
}
```

### Output
Shopping Cart Items:

- Laptop
- Mouse
- Keyboard

### Social Media Platforms

Posts, comments, likes, and messages are often stored using vector-like structures because the amount of data constantly changes.

Example:

```text
Post 1
Post 2
Post 3
Post 4
```

#### Practice Problem
**Problem Statement:** Simulate storing a list of post IDs in a vector as a user publishes new posts, and print the IDs.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> postIds = {2001, 2002, 2003};
    postIds.push_back(2004);
    cout << "Feed Posts:\n";
    for(int id : postIds) {
        cout << "Post ID: " << id << "\n";
    }
    return 0;
}
```

### Output
Feed Posts:
Post ID: 2001
Post ID: 2002
Post ID: 2003
Post ID: 2004

### Gaming Applications

Game developers frequently use vectors to store:

- Player information
- Inventory items
- Scores
- Levels
- Enemy positions

Example:

```text
Player Scores

250
420
510
700
```

#### Practice Problem
**Problem Statement:** Create a vector storing scores of players in a game. Print the scores and find the highest score.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> scores = {250, 420, 510, 700};
    cout << "Player Scores: ";
    for(int s : scores) cout << s << " ";
    cout << "\nHighest Score: " << *max_element(scores.begin(), scores.end()) << "\n";
    return 0;
}
```

### Output
Player Scores: 250 420 510 700 
Highest Score: 700

### Data Analysis and Machine Learning

Machine learning models often process large datasets.

Vectors provide efficient storage for:

- Training data
- Feature values
- Predictions
- Statistical information

#### Practice Problem
**Problem Statement:** Write a C++ program that stores numerical features in a vector and calculates the mean value of these features.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

int main() {
    vector<double> features = {1.5, 2.5, 3.5, 4.5};
    double sum = accumulate(features.begin(), features.end(), 0.0);
    cout << "Mean of features: " << sum / features.size() << "\n";
    return 0;
}
```

### Output
Mean of features: 3

### AlphaKnowledge Learning Platform

Suppose AlphaKnowledge stores programming course ratings.

Example:

```text
Course Ratings

4.5
4.8
4.2
4.9
```

As new students submit ratings, the vector automatically grows.

This flexibility makes vectors ideal for educational platforms.

#### Practice Problem
**Problem Statement:** Track ratings of a course on AlphaKnowledge. Create a vector of ratings and print the average rating.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

int main() {
    vector<double> ratings = {4.5, 4.8, 4.2, 4.9};
    double sum = accumulate(ratings.begin(), ratings.end(), 0.0);
    cout << "AlphaKnowledge Average Rating: " << sum / ratings.size() << "\n";
    return 0;
}
```

### Output
AlphaKnowledge Average Rating: 4.6

## Advantages of Vectors

Vectors provide several benefits that make them one of the most popular STL containers.

| Advantage | Description |
| --- | --- |
| Dynamic Size | Automatically grows and shrinks during execution |
| Fast Random Access | Elements can be accessed directly using indexes |
| Automatic Memory Management | No need for manual allocation and deallocation |
| STL Compatibility | Works seamlessly with STL algorithms |
| Iterator Support | Supports all major iterator operations |
| Easy to Use | Simple syntax and rich set of built-in functions |
| Reusable | Can store different data types using templates |
| Contiguous Memory | Provides cache-friendly performance |

### Practice Problem

**Problem Statement:** Demonstrate the safety and automatic memory management of vectors by showing that we do not need to manually delete resources.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

void makeVector() {
    vector<int> temp = {1, 2, 3};
    cout << "Temporary vector size: " << temp.size() << "\n";
} // memory deallocated automatically here

int main() {
    makeVector();
    cout << "Memory automatically managed without manual delete.\n";
    return 0;
}
```

### Output
Temporary vector size: 3
Memory automatically managed without manual delete.

### Dynamic Resizing

One of the biggest advantages of vectors is automatic resizing.

Programmers do not need to predict future storage requirements.

### Efficient Access

Since vector elements are stored continuously in memory, element access is extremely fast.

### Simplified Programming

Many complex operations such as insertion, deletion, and resizing are handled internally.

This reduces code complexity significantly.

### Better Integration with STL

Vectors work naturally with algorithms such as:

- sort()
- reverse()
- find()
- count()
- binary_search()

making them highly versatile.

## Limitations of Vectors

Although vectors are extremely useful, they are not ideal in every situation.

| Limitation | Description |
| --- | --- |
| Costly Middle Insertions | Elements must be shifted |
| Costly Middle Deletions | Elements must be shifted |
| Reallocation Overhead | Resizing may require memory copying |
| Extra Memory Usage | Capacity may exceed actual size |
| Not Suitable for Frequent Middle Updates | Linked lists may perform better |

### Practice Problem

**Problem Statement:** Write a C++ program that demonstrates that inserting elements in the middle of a vector shifts all subsequent elements to the right, showing size change.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 40, 50};
    v.insert(v.begin() + 2, 30);
    cout << "Vector after middle insert: ";
    for(int x : v) cout << x << " ";
    cout << "\nSize: " << v.size() << "\n";
    return 0;
}
```

### Output
Vector after middle insert: 10 20 30 40 50 
Size: 5

### Costly Insertions in the Middle

Consider:

```text
10 20 40 50
```

If we insert 30:

```text
10 20 30 40 50
```

The elements 40 and 50 must be shifted.

This increases execution time.

### Costly Deletions

Removing an element from the middle requires shifting remaining elements.

Example:

```text
Before:

10 20 30 40 50
```

Remove 30:

```text
After:

10 20 40 50
```

Again, elements must be shifted.

### Memory Reallocation

When capacity becomes full, the vector allocates new memory and copies existing elements.

Frequent reallocations may affect performance in large applications.

## Vector vs Array

Vectors and arrays both store collections of elements, but they differ in several important aspects.

| Feature | Array | Vector |
| --- | --- | --- |
| Size | Fixed | Dynamic |
| Memory Allocation | Static or Manual | Automatic |
| Resizing | Not Possible | Automatic |
| STL Support | Limited | Full Support |
| Iterator Support | No | Yes |
| Safety | Less Safe | Safer |
| Built-in Functions | Very Few | Many |
| Memory Management | Programmer Managed | STL Managed |
| Ease of Use | Moderate | Easy |

### When to Use Arrays

Arrays are suitable when:

- Size is fixed.
- Memory overhead must be minimal.
- Maximum performance is required.

### When to Use Vectors

Vectors are suitable when:

- Size is unknown beforehand.
- Frequent insertions are required.
- STL algorithms will be used.
- Code simplicity is important.

In modern C++ programming, vectors are generally preferred over arrays.

## Best Practices While Using Vectors

To write efficient programs, follow these recommendations:

### Practice Problem

**Problem Statement:** Use const references in a range-based loop to read and print elements of a string vector without copying them.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> words = {"Const", "Reference", "Saves", "Memory"};
    for(const auto& w : words) {
        cout << w << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Const Reference Saves Memory

### Use reserve() When Possible

If the approximate size is known beforehand, reserve memory in advance.

Benefits:

- Fewer reallocations
- Better performance
- Reduced memory copying

### Use at() for Safer Access

During development, `at()` helps detect invalid index access.

### Use Range-Based Loops

Range-based loops improve readability and reduce errors.

### Use const References During Traversal

For read-only traversal:

```cpp
for(const auto& value : vectorName)
```

This avoids unnecessary copying.

### Avoid Frequent Middle Insertions

If frequent middle insertions are required, consider using:

- list
- deque

instead of vectors.

## Internal Working of a Vector

Understanding how vectors work internally helps explain why they are one of the most efficient and widely used containers in C++.

Unlike linked lists, vectors store elements in **contiguous memory locations**, similar to normal arrays.

For example:

```text
Index : 0   1   2   3

Value : 10  20  30  40
```

Memory Representation:

```text
Address

1000 → 10
1004 → 20
1008 → 30
1012 → 40
```

Since elements are stored continuously in memory, vectors provide very fast random access.

This means accessing:

```cpp
v[2]
```

directly retrieves the third element without traversing previous elements.

Because of this property, vectors are highly efficient for applications where frequent element access is required.

### Practice Problem

**Problem Statement:** Verify the contiguous memory location feature of vectors by printing the memory addresses of consecutive elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30};
    cout << "Address 0: " << &v[0] << "\n";
    cout << "Address 1: " << &v[1] << "\n";
    cout << "Address 2: " << &v[2] << "\n";
    return 0;
}
```

### Output
Address 0: 0x1071d68
Address 1: 0x1071d6c
Address 2: 0x1071d70

## Size vs Capacity

Many beginners assume that size and capacity are the same, but they represent different concepts.

### Practice Problem

**Problem Statement:** Write a C++ program that prints size and capacity changes of a vector as we add five elements one by one.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    for(int i = 0; i < 5; ++i) {
        v.push_back(i);
        cout << "Added " << i << " -> Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    }
    return 0;
}
```

### Output
Added 0 -&gt; Size: 1, Capacity: 1
Added 1 -&gt; Size: 2, Capacity: 2
Added 2 -&gt; Size: 3, Capacity: 4
Added 3 -&gt; Size: 4, Capacity: 4
Added 4 -&gt; Size: 5, Capacity: 8

### Size

The **size** of a vector represents the number of elements currently stored inside it.

Example:

```cpp
vector<int> marks = {85, 90, 78};
```

Here:

```text
Size = 3
```

because three elements are present.

### Capacity

The **capacity** of a vector represents the total number of elements that can be stored before additional memory allocation becomes necessary.

Example:

```text
Size = 3
Capacity = 4
```

The vector still has room for one additional element without allocating new memory.

### Why Capacity Exists

Suppose a vector increased its memory every time a new element was inserted.

For each insertion, the vector would need to:

1. Allocate new memory.
2. Copy existing elements.
3. Release old memory.

This process would be extremely slow.

To improve performance, vectors allocate extra memory in advance.

Example:

```text
Size = 4
Capacity = 8
```

Although only four elements currently exist, memory has already been reserved for eight elements.

This significantly reduces future memory allocations.

## Vector Growth Strategy

When a vector becomes full, it automatically allocates a larger memory block.

Consider the following situation:

### Practice Problem

**Problem Statement:** Demonstrate the growth strategy of a vector by pushing elements and detecting when reallocation occurs.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    size_t cap = 0;
    for(int i = 0; i < 15; ++i) {
        v.push_back(i);
        if(v.capacity() != cap) {
            cout << "Reallocation detected! Size: " << v.size() << ", New Capacity: " << v.capacity() << "\n";
            cap = v.capacity();
        }
    }
    return 0;
}
```

### Output
Reallocation detected! Size: 1, New Capacity: 1
Reallocation detected! Size: 2, New Capacity: 2
Reallocation detected! Size: 3, New Capacity: 4
Reallocation detected! Size: 5, New Capacity: 8
Reallocation detected! Size: 9, New Capacity: 16

### Initial State

```text
Size = 4
Capacity = 4

10 20 30 40
```

Now insert a new element:

```cpp
v.push_back(50);
```

### New State

```text
Size = 5
Capacity = 8

10 20 30 40 50
```

Internally, the vector performs the following steps:

1. Allocates a larger memory block.
2. Copies existing elements to the new memory.
3. Inserts the new element.
4. Releases the old memory block.

This process is called **reallocation**.

Although reallocation is expensive, it happens infrequently. Therefore, the average insertion time remains very efficient.

## Capacity Related Functions

Vectors provide several useful functions for managing memory and storage.

### Practice Problem

**Problem Statement:** Implement a program that showcases the difference between `reserve()` and `resize()` and outputs the results.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(10);
    cout << "After reserve(10) -> Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    v.resize(5, 42);
    cout << "After resize(5, 42) -> Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    cout << "Elements: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
After reserve(10) -> Size: 0, Capacity: 10
After resize(5, 42) -> Size: 5, Capacity: 10
Elements: 42 42 42 42 42

### size()

Returns the number of elements currently stored in the vector.

Example:

```text
Vector

10 20 30 40

Size = 4
```

#### Practice Problem
**Problem Statement:** Create a vector of floats, insert 3 items, pop 1, and print its size using `size()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<float> v = {1.1f, 2.2f, 3.3f};
    v.pop_back();
    cout << "Vector Size: " << v.size() << "\n";
    return 0;
}
```

### Output
Vector Size: 2

### capacity()

Returns the amount of memory currently allocated for the vector.

Example:

```text
Size = 4
Capacity = 8
```

### reserve()

The `reserve()` function allocates memory in advance.

This is useful when the approximate number of elements is already known.

Benefits:

- Reduces reallocations.
- Improves performance.
- Minimizes memory copying.

Example:

```text
Expected Students = 1000

Reserve Capacity = 1000
```

The vector can now store 1000 elements before needing additional memory.

### resize()

The `resize()` function changes the number of elements stored in the vector.

If the size is increased:

```text
Original

1 2 3

resize(5)

1 2 3 0 0
```

New elements are automatically added.

If the size is decreased:

```text
Original

1 2 3 4 5

resize(3)

1 2 3
```

Extra elements are removed.

#### Practice Problem
**Problem Statement:** Demonstrate `resize()` by resizing a vector of size 3 to 6 with a default value of 100, and print its elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3};
    v.resize(6, 100);
    cout << "Resized Elements: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Resized Elements: 1 2 3 100 100 100

## Traversing a Vector

Traversing means visiting every element of the vector one by one.

Vectors support multiple traversal methods.

### Practice Problem

**Problem Statement:** Traverse a vector of names in reverse using reverse iterators.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> names = {"Alice", "Bob", "Charlie"};
    cout << "Reverse traversal: ";
    for(auto it = names.rbegin(); it != names.rend(); ++it) {
        cout << *it << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Reverse traversal: Charlie Bob Alice

### Traversal Using Index

Every element inside a vector has a unique index.

Example:

```text
Index : 0 1 2 3

Value : 5 10 15 20
```

Elements can be accessed using their index values.

This is the simplest and most commonly used traversal technique.

#### Practice Problem
**Problem Statement:** Write a C++ program that accesses and prints every second element of a vector using an index-based loop.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50, 60};
    cout << "Every second element: ";
    for(size_t i = 0; i < v.size(); i += 2) {
        cout << v[i] << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Every second element: 10 30 50

### Advantages

- Easy to understand.
- Direct access to elements.
- Useful when index positions are required.

### Traversal Using Range-Based Loop

Modern C++ provides a cleaner and more readable way to traverse vectors.

Instead of manually managing indexes, the loop automatically accesses each element.

#### Practice Problem
**Problem Statement:** Calculate the sum of all elements in an integer vector using a range-based loop.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    int sum = 0;
    for(int x : v) sum += x;
    cout << "Sum: " << sum << "\n";
    return 0;
}
```

### Output
Sum: 15

### Advantages

- Shorter syntax.
- Better readability.
- Reduced chance of indexing errors.

This approach is preferred when only element values are needed.

### Traversal Using Iterators

Vectors are STL containers, so they support iterators.

Iterators behave similarly to pointers and allow sequential access to elements.

#### Practice Problem
**Problem Statement:** Perform traversal of a float vector using standard iterators and double the value of each element.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> v = {1.5, 2.5, 3.5};
    for(auto it = v.begin(); it != v.end(); ++it) {
        *it *= 2.0;
    }
    cout << "Doubled elements: ";
    for(double x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Doubled elements: 3 5 7

### Advantages

- Works with all STL containers.
- Compatible with STL algorithms.
- More flexible than indexes.

Iterators are widely used with algorithms such as:

- sort()
- find()
- count()
- reverse()
- binary_search()

making them an essential part of STL programming.

## Performance Characteristics of Vectors

Understanding vector performance helps in selecting the right data structure.

| Operation | Complexity |
| --- | --- |
| Access Element | O(1) |
| Update Element | O(1) |
| push_back() | O(1) Average |
| pop_back() | O(1) |
| insert() at End | O(1) Average |
| insert() in Middle | O(n) |
| erase() from Middle | O(n) |
| Traversal | O(n) |
| size() | O(1) |
| empty() | O(1) |

Vectors are extremely fast for:

- Random access.
- End insertions.
- End deletions.

However, they are less efficient for:

- Frequent middle insertions.
- Frequent middle deletions.

In such situations, containers like `list` or `deque` may be better choices.

### Practice Problem

**Problem Statement:** Write a program that measures the average execution behavior of random access in a vector (showing it is O(1)).

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};
    int val = v[3]; // O(1) access
    cout << "Value at index 3: " << val << "\n";
    return 0;
}
```

### Output
Value at index 3: 40

# Advanced Concepts of Vectors

After learning the basic operations of vectors, it is important to understand some advanced concepts that make vectors powerful and efficient for real-world applications.

These concepts are frequently used in competitive programming, software development, system design, and technical interviews.

## Practice Problem

**Problem Statement:** Show a C++ program that utilizes constant reverse iterators to inspect elements in reverse without modification.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {5, 10, 15};
    cout << "Const reverse traversal: ";
    for(auto it = v.crbegin(); it != v.crend(); ++it) {
        cout << *it << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Const reverse traversal: 15 10 5

## Capacity Management in Vectors

One of the major advantages of vectors is their ability to manage memory automatically.

Internally, a vector keeps track of two important values:

- Size
- Capacity

While size represents the number of elements currently stored, capacity represents the total amount of memory allocated.

Sometimes a vector may contain:

```text
Elements : 5

Capacity : 8
```

This means memory for eight elements has already been allocated even though only five elements currently exist.

This strategy helps reduce the number of reallocations and improves performance.

### Practice Problem

**Problem Statement:** Write a program that reserves capacity, pushes elements, and prints the ratio of size to capacity.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(10);
    v.push_back(10);
    v.push_back(20);
    cout << "Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Size: 2, Capacity: 10

## Shrinking a Vector

When elements are removed, the size decreases but the capacity usually remains unchanged.

Example:

```text
Before Deletion

Size = 10
Capacity = 16
```

After removing elements:

```text
Size = 3
Capacity = 16
```

The unused memory remains allocated.

This is intentional because the vector assumes more elements may be inserted later.

### Practice Problem

**Problem Statement:** Demonstrate the `shrink_to_fit()` method by reducing a vector's capacity to its size after erasing elements.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    v.reserve(50);
    cout << "Initial capacity: " << v.capacity() << "\n";
    v.erase(v.begin() + 3, v.end());
    cout << "Size after erase: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    v.shrink_to_fit();
    cout << "Capacity after shrink_to_fit: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Initial capacity: 50
Size after erase: 3, Capacity: 50
Capacity after shrink_to_fit: 3

### shrink_to_fit()

If memory optimization is important, unused memory can be released.

Example:

```text
Before

Size = 3
Capacity = 16
```

After shrinking:

```text
Size = 3
Capacity = 3
```

This reduces memory consumption.

#### Practice Problem
**Problem Statement:** Show capacity reduction using `shrink_to_fit()` on a vector that has extra allocated memory.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30};
    v.reserve(100);
    cout << "Capacity before shrink: " << v.capacity() << "\n";
    v.shrink_to_fit();
    cout << "Capacity after shrink: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Capacity before shrink: 100
Capacity after shrink: 3

## Swapping Vectors

Sometimes two vectors need to exchange their contents.

Example:

```text
Vector A

10 20 30
```

```text
Vector B

100 200 300
```

After swapping:

```text
Vector A

100 200 300
```

```text
Vector B

10 20 30
```

Swapping is extremely efficient because only internal pointers are exchanged rather than copying all elements.

### Practice Problem

**Problem Statement:** Declare two vectors of different sizes and swap their contents using the `swap()` member function.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v1 = {1, 2, 3};
    vector<int> v2 = {10, 20};
    v1.swap(v2);
    cout << "v1 size: " << v1.size() << ", v2 size: " << v2.size() << "\n";
    return 0;
}
```

### Output
v1 size: 2, v2 size: 3

## Front and Back Elements

Vectors provide direct access to both ends.

### Practice Problem

**Problem Statement:** Access the front and back elements of a vector, modify them, and print the results.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {5, 15, 25};
    cout << "Original front: " << v.front() << ", back: " << v.back() << "\n";
    v.front() = 100;
    v.back() = 200;
    cout << "New front: " << v.front() << ", back: " << v.back() << "\n";
    return 0;
}
```

### Output
Original front: 5, back: 25
New front: 100, back: 200

### Front Element

Returns the first element.

Example:

```text
10 20 30 40

Front = 10
```

#### Practice Problem
**Problem Statement:** Access the first element of a vector containing floating point values using `front()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> v = {3.14, 2.71, 1.41};
    cout << "First: " << v.front() << "\n";
    return 0;
}
```

### Output
First: 3.14

### Back Element

Returns the last element.

Example:

```text
10 20 30 40

Back = 40
```

These operations are very useful when processing sequences.

#### Practice Problem
**Problem Statement:** Access the last element of a vector containing floating point values using `back()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> v = {3.14, 2.71, 1.41};
    cout << "Last: " << v.back() << "\n";
    return 0;
}
```

### Output
Last: 1.41

## Checking Whether a Vector is Empty

Before accessing elements, it is often important to verify whether the vector contains any data.

Example:

```text
[]
```

The vector contains no elements.

Checking emptiness helps avoid runtime errors and invalid accesses.

Common use cases include:

- Stack implementations
- Queue implementations
- Menu-driven applications
- Data processing systems

### Practice Problem

**Problem Statement:** Create a vector of strings, use `empty()` to check if it has content, and print the size.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    vector<string> v = {"C++"};
    cout << "Is empty? " << (v.empty() ? "Yes" : "No") << ", Size: " << v.size() << "\n";
    return 0;
}
```

### Output
Is empty? No, Size: 1

## Copying Vectors

A vector can be copied into another vector.

Example:

```text
Original Vector

10 20 30
```

Copied Vector:

```text
10 20 30
```

After copying, both vectors become independent.

Changing one vector does not affect the other.

Example:

```text
Original

10 20 30
```

```text
Copy

10 20 30
```

Modify Original:

```text
Original

100 20 30
```

```text
Copy

10 20 30
```

The copied vector remains unchanged.

### Practice Problem

**Problem Statement:** Create an original vector, copy it to another, modify the original vector, and verify the copied vector is unaffected.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> original = {10, 20, 30};
    vector<int> duplicate = original;
    original[0] = 999;
    cout << "Original: " << original[0] << ", Duplicate: " << duplicate[0] << "\n";
    return 0;
}
```

### Output
Original: 999, Duplicate: 10

## Assigning Values to a Vector

Sometimes all elements need to be initialized with the same value.

Example:

```text
Size = 5

Value = 100
```

Result:

```text
100 100 100 100 100
```

This is useful when initializing:

- Scores
- Marks
- Distances
- Frequencies
- DP tables

### Practice Problem

**Problem Statement:** Clear a vector and assign 5 elements of value 100 using the `assign()` function.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3};
    v.assign(5, 100);
    cout << "Assigned elements: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Assigned elements: 100 100 100 100 100

## Comparing Two Vectors

Vectors can be compared directly.

Two vectors are equal only if:

- Sizes are equal.
- Corresponding elements are equal.

Example:

```text
Vector A

10 20 30
```

```text
Vector B

10 20 30
```

Result:

```text
Equal
```

Example:

```text
Vector A

10 20 30
```

```text
Vector B

10 20 40
```

Result:

```text
Not Equal
```

### Practice Problem

**Problem Statement:** Write a C++ program that compares two vectors using `==` and relational operator `<`, printing the comparison results.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v1 = {1, 2, 3};
    vector<int> v2 = {1, 2, 3};
    vector<int> v3 = {1, 2, 4};
    cout << "v1 == v2: " << (v1 == v2 ? "Equal" : "Not Equal") << "\n";
    cout << "v1 < v3: " << (v1 < v3 ? "True" : "False") << "\n";
    return 0;
}
```

### Output
v1 == v2: Equal
v1 < v3: True

## Sorting a Vector

Sorting is one of the most common operations performed on vectors.

Unsorted Data:

```text
40 10 50 20 30
```

Sorted Data:

```text
10 20 30 40 50
```

Sorting is useful for:

- Searching
- Ranking
- Statistical analysis
- Competitive programming

After sorting, many advanced algorithms become applicable.

### Practice Problem

**Problem Statement:** Create a vector of integers, sort it in descending order using `std::sort()` and `std::greater<int>()`.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {15, 3, 22, 8, 11};
    sort(v.begin(), v.end(), greater<int>());
    cout << "Sorted descending: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Sorted descending: 22 15 11 8 3

## Searching in a Vector

Searching means locating a specific element.

Example:

```text
10 20 30 40 50
```

Searching for:

```text
30
```

Result:

```text
Found
```

Searching is heavily used in:

- Databases
- Student management systems
- Inventory systems
- Search engines

### Practice Problem

**Problem Statement:** Search for the string "C++" in a vector of programming languages using `std::find()` and print its index if found.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    vector<string> langs = {"Java", "Python", "C++", "Rust"};
    auto it = find(langs.begin(), langs.end(), "C++");
    if(it != langs.end()) {
        cout << "Found C++ at index: " << distance(langs.begin(), it) << "\n";
    } else {
        cout << "Not Found\n";
    }
    return 0;
}
```

### Output
Found C++ at index: 2

## Reversing a Vector

Sometimes data must be processed in reverse order.

Original:

```text
10 20 30 40 50
```

After Reversing:

```text
50 40 30 20 10
```

Applications include:

- Undo operations
- Stack processing
- Reverse traversal

### Practice Problem

**Problem Statement:** Reverse the elements of an integer vector using `std::reverse()` and print them.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    reverse(v.begin(), v.end());
    cout << "Reversed: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Reversed: 5 4 3 2 1

## Two-Dimensional Vectors

A two-dimensional vector stores data in rows and columns.

It behaves like a dynamic matrix.

Example:

```text
1 2 3

4 5 6

7 8 9
```

Rows and columns can grow dynamically.

Applications include:

- Matrices
- Game boards
- Seating arrangements
- Spreadsheet data
- Image processing

### Practice Problem

**Problem Statement:** Create a 2D vector where each row represents scores of a student in 3 subjects. Traverse and print scores.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<int>> studentScores = {
        {80, 85, 90},
        {70, 75, 80}
    };
    for(size_t i = 0; i < studentScores.size(); ++i) {
        cout << "Student " << i << " scores: ";
        for(int s : studentScores[i]) cout << s << " ";
        cout << "\n";
    }
    return 0;
}
```

### Output
Student 0 scores: 80 85 90 
Student 1 scores: 70 75 80

### Advantages of 2D Vectors

- Dynamic row size
- Dynamic column size
- Easy traversal
- Flexible memory management

## Three-Dimensional Vectors

A three-dimensional vector can store data across three dimensions.

Example:

```text
Classroom

Floor 1
 ├─ Room 1
 └─ Room 2

Floor 2
 ├─ Room 1
 └─ Room 2
```

Applications include:

- 3D graphics
- Scientific simulations
- Gaming environments
- Volumetric data processing

### Practice Problem

**Problem Statement:** Declare a 3D vector of size 2x2x2 and print the sum of all its elements initialized with value 5.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<vector<int>>> v3d(2, vector<vector<int>>(2, vector<int>(2, 5)));
    int sum = 0;
    for(const auto& r2d : v3d) {
        for(const auto& row : r2d) {
            for(int val : row) {
                sum += val;
            }
        }
    }
    cout << "Total Sum of 3D Vector elements: " << sum << "\n";
    return 0;
}
```

### Output
Total Sum of 3D Vector elements: 40

## When Should You Use Vectors?

Vectors are the best choice when:

- Data size is unknown.
- Frequent end insertions are required.
- Random access is important.
- STL algorithms will be used.
- Code simplicity is preferred.

Examples:

- Student records
- AlphaKnowledge course enrollments
- Online shopping carts
- Social media feeds
- Competitive programming problems

### Practice Problem

**Problem Statement:** Write a C++ program that reads inputs dynamically until 0 is entered, stores them in a vector, and then prints the sum.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // Simulated input loop
    vector<int> inputs;
    int testInputs[] = {12, 18, 5, 0};
    int i = 0;
    while(testInputs[i] != 0) {
        inputs.push_back(testInputs[i]);
        i++;
    }
    int sum = 0;
    for(int x : inputs) sum += x;
    cout << "Sum of inputs: " << sum << "\n";
    return 0;
}
```

### Output
Sum of inputs: 35

## When Should You Avoid Vectors?

Vectors may not be ideal when:

- Frequent middle insertions are required.
- Frequent middle deletions are required.
- Memory usage must be extremely optimized.
- Constant-time insertion in the middle is necessary.

Alternative containers:

| Requirement | Better Choice |
| --- | --- |
| Frequent Middle Insertions | List |
| Frequent Front Insertions | Deque |
| Unique Sorted Data | Set |
| Key-Value Storage | Map |
| Fast FIFO Operations | Queue |
| Fast LIFO Operations | Stack |

### Practice Problem

**Problem Statement:** Demonstrate why deque is preferred over vector for frequent front insertions by showing both options pushing elements at front.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

int main() {
    deque<int> d = {2, 3};
    d.push_front(1);
    vector<int> v = {2, 3};
    v.insert(v.begin(), 1);
    cout << "Deque front: " << d.front() << ", Vector front: " << v.front() << "\n";
    return 0;
}
```

### Output
Deque front: 1, Vector front: 1

## Interview Questions on Vectors

### Practice Problem

**Problem Statement:** Implement Kadane's algorithm to find the maximum sum of a contiguous subarray using std::vector.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    int maxSoFar = nums[0], maxEndingHere = nums[0];
    for (size_t i = 1; i < nums.size(); ++i) {
        maxEndingHere = max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = max(maxSoFar, maxEndingHere);
    }
    cout << "Maximum Subarray Sum: " << maxSoFar << "\n";
    return 0;
}
```

### Output
Maximum Subarray Sum: 6

### Why are vectors preferred over arrays?

Because vectors:

- Grow dynamically.
- Manage memory automatically.
- Provide STL support.
- Offer many built-in functions.

### What is the difference between size and capacity?

| Size | Capacity |
| --- | --- |
| Number of stored elements | Allocated storage space |

### Why is push_back() efficient?

Because vectors allocate extra memory in advance, reducing frequent reallocations.

### Why is insertion in the middle expensive?

Because all subsequent elements must be shifted to create space.

### Why is random access fast?

Because vector elements are stored in contiguous memory locations.

# Practical Applications of Vectors

Vectors are one of the most widely used data structures in modern software development because they provide dynamic storage, fast access, and easy integration with STL algorithms.

Understanding where vectors are used in real-world applications helps in appreciating their importance beyond academic examples.

## Student Management Systems

Educational institutions often need to store information about students.

Since the number of students changes every year, using fixed-size arrays becomes impractical.

Example:

```text
Students

Mohit
Akash
Hemesh
Abhiram
```

Whenever a new student joins:

```text
Students

Mohit
Akash
Hemesh
Abhiram
Rohit
```

The vector automatically grows to accommodate the new record.

### Practice Problem

**Problem Statement:** Search for a student in a vector database by name and print their record.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Student {
    string name;
    int roll;
};

int main() {
    vector<Student> database = {{"Mohit", 101}, {"Akash", 102}};
    string searchName = "Akash";
    for(const auto& s : database) {
        if(s.name == searchName) {
            cout << "Student Found! Name: " << s.name << ", Roll: " << s.roll << "\n";
            return 0;
        }
    }
    cout << "Student not found.\n";
    return 0;
}
```

### Output
Student Found! Name: Akash, Roll: 102

### Benefits

- Dynamic size
- Easy insertion
- Easy traversal
- Efficient storage

## AlphaKnowledge Learning Platform

Consider a learning platform such as AlphaKnowledge.

The platform may need to store:

- Student enrollments
- Course ratings
- Quiz scores
- Learning progress

Example:

```text
Course Ratings

4.5
4.8
4.6
4.9
```

Whenever a new student submits a rating:

```text
Course Ratings

4.5
4.8
4.6
4.9
4.7
```

The vector expands automatically.

### Practice Problem

**Problem Statement:** Filter and print ratings in a course that are higher than 4.5.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> ratings = {4.5, 4.8, 4.2, 4.9};
    cout << "Ratings above 4.5: ";
    for(double r : ratings) {
        if(r > 4.5) cout << r << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Ratings above 4.5: 4.8 4.9

### Benefits

- Handles growing user data
- Supports fast retrieval
- Easy statistical analysis

## Online Shopping Systems

E-commerce websites continuously manage products added to shopping carts.

Example:

```text
Cart

Laptop
Mouse
Keyboard
```

After adding headphones:

```text
Cart

Laptop
Mouse
Keyboard
Headphones
```

The vector automatically stores the additional item.

### Practice Problem

**Problem Statement:** Remove a specific product by name from an online shopping cart vector and print remaining items.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    vector<string> cart = {"Laptop", "Mouse", "Keyboard"};
    auto it = find(cart.begin(), cart.end(), "Mouse");
    if(it != cart.end()) cart.erase(it);
    cout << "Remaining Cart Items: ";
    for(const auto& item : cart) cout << item << " ";
    cout << "\n";
    return 0;
}
```

### Output
Remaining Cart Items: Laptop Keyboard

### Benefits

- Dynamic cart management
- Fast product access
- Easy item removal

## Social Media Platforms

Social media applications constantly process:

- Posts
- Comments
- Likes
- Followers

Example:

```text
Posts

Post 1
Post 2
Post 3
Post 4
```

As users create new posts:

```text
Posts

Post 1
Post 2
Post 3
Post 4
Post 5
```

The vector grows dynamically.

### Practice Problem

**Problem Statement:** Find the post with the maximum number of likes stored in a vector of post scores.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> likes = {120, 450, 310, 89};
    auto maxIt = max_element(likes.begin(), likes.end());
    cout << "Max Likes: " << *maxIt << " at index " << distance(likes.begin(), maxIt) << "\n";
    return 0;
}
```

### Output
Max Likes: 450 at index 1

### Benefits

- Efficient feed generation
- Dynamic content management
- Quick traversal

## Gaming Applications

Game developers frequently use vectors to store dynamic game objects.

Examples include:

- Player inventory
- Enemy positions
- Weapons
- Scores
- Levels

Example:

```text
Inventory

Sword
Shield
Potion
```

After collecting a new item:

```text
Inventory

Sword
Shield
Potion
Helmet
```

### Practice Problem

**Problem Statement:** Sort a list of player high scores in descending order and print them.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> scores = {9500, 8200, 7500, 11000};
    sort(scores.begin(), scores.end(), greater<int>());
    cout << "Ranked High Scores: ";
    for(int s : scores) cout << s << " ";
    cout << "\n";
    return 0;
}
```

### Output
Ranked High Scores: 11000 9500 8200 7500

### Benefits

- Dynamic storage
- Fast access
- Flexible updates

## Competitive Programming

Vectors are the most frequently used STL container in competitive programming.

Applications include:

- Graph representation
- Dynamic arrays
- Prefix sums
- Dynamic programming
- Sliding window problems

Example:

```text
Input Data

10 20 30 40 50
```

The vector efficiently stores and processes the values.

### Benefits

- Easy implementation
- STL compatibility
- High performance

## Data Analysis Applications

Data analysts frequently process large datasets.

Vectors are used to store:

- Sales records
- Customer information
- Statistical data
- Survey responses

Example:

```text
Monthly Sales

12000
15000
18000
20000
```

The vector allows efficient processing of large datasets.

### Practice Problem

**Problem Statement:** Compute the minimum and maximum value from a vector of temperature measurements in a single pass.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<double> temps = {36.5, 37.2, 35.8, 38.0, 36.9};
    auto result = minmax_element(temps.begin(), temps.end());
    cout << "Min Temp: " << *result.first << ", Max Temp: " << *result.second << "\n";
    return 0;
}
```

### Output
Min Temp: 35.8, Max Temp: 38

### Benefits

- Dynamic data handling
- Efficient traversal
- Easy integration with algorithms

## Machine Learning Applications

Machine learning models often process numerical features stored in vectors.

Example:

```text
Feature Vector

Height
Weight
Age
Experience
```

Each training sample can be represented using a vector.

### Practice Problem

**Problem Statement:** Compute the Euclidean distance between two feature vectors.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

int main() {
    vector<double> v1 = {1.0, 2.0, 3.0};
    vector<double> v2 = {4.0, 5.0, 6.0};
    double sum = 0.0;
    for(size_t i = 0; i < v1.size(); ++i) {
        sum += pow(v1[i] - v2[i], 2);
    }
    cout << "Euclidean Distance: " << sqrt(sum) << "\n";
    return 0;
}
```

### Output
Euclidean Distance: 5.19615

### Benefits

- Fast access
- Efficient memory usage
- Mathematical processing support

## Graph Representation Using Vectors

Vectors are heavily used in graph algorithms.

Example:

```text
1 → 2
1 → 3
2 → 4
3 → 5
```

Adjacency lists are commonly implemented using vectors.

### Practice Problem

**Problem Statement:** Represent a directed graph with 4 nodes using an adjacency list of vectors, and print adjacent nodes.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<int>> adj(4);
    adj[0].push_back(1);
    adj[0].push_back(2);
    adj[1].push_back(3);
    cout << "Nodes adjacent to Node 0: ";
    for(int node : adj[0]) cout << node << " ";
    cout << "\n";
    return 0;
}
```

### Output
Nodes adjacent to Node 0: 1 2

### Benefits

- Memory efficient
- Fast traversal
- Easy edge insertion

## Why Vectors Are So Popular

Vectors are preferred because they combine the strengths of arrays and dynamic memory allocation.

### Practice Problem

**Problem Statement:** Demonstrate the efficiency and compactness of vectors by performing filter and sort on a dynamic structure.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {10, -5, 20, 0, 15};
    sort(v.begin(), v.end());
    cout << "Sorted dynamic vector: ";
    for(int x : v) cout << x << " ";
    cout << "\n";
    return 0;
}
```

### Output
Sorted dynamic vector: -5 0 10 15 20

### Major Reasons

- Dynamic resizing
- Automatic memory management
- Fast random access
- STL algorithm compatibility
- Easy syntax
- Reusability
- Excellent performance

Because of these advantages, vectors are often the first STL container programmers learn and the one they use most frequently.

# Common Mistakes While Using Vectors

Beginners often make mistakes when working with vectors.

Understanding these mistakes helps avoid bugs and runtime errors.

## Accessing Invalid Indexes

Example:

```text
Vector Size = 5

Valid Indexes

0 1 2 3 4
```

Accessing:

```text
Index 10
```

is invalid.

Always ensure the index exists before accessing it.

### Practice Problem

**Problem Statement:** Create a safety wrapper function `safe_get` using `at()` that catches index out of bounds exceptions.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>
using namespace std;

int safe_get(const vector<int>& v, size_t index) {
    try {
        return v.at(index);
    } catch(const out_of_range& e) {
        cerr << "Index " << index << " out of bounds! ";
        return -1;
    }
}

int main() {
    vector<int> v = {10, 20};
    cout << "safe_get(v, 1): " << safe_get(v, 1) << "\n";
    cout << "safe_get(v, 5): " << safe_get(v, 5) << "\n";
    return 0;
}
```

### Output
safe_get(v, 1): 20
safe_get(v, 5): -1

## Confusing Size and Capacity

Many beginners assume:

```text
Size = Capacity
```

which is incorrect.

Example:

```text
Size = 5
Capacity = 8
```

Only five elements exist even though memory for eight elements is allocated.

### Practice Problem

**Problem Statement:** Create a vector of capacity 10 and print both size and capacity to show they are different.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(10);
    cout << "Size: " << v.size() << ", Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Size: 0, Capacity: 10

## Forgetting Empty Checks

Accessing:

```text
front()
```

or

```text
back()
```

on an empty vector leads to undefined behavior.

Always verify that the vector contains elements first.

### Practice Problem

**Problem Statement:** Write a program that safely retrieves `front()` and `back()` only after confirming `empty()` is false.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

void printEnds(const vector<int>& v) {
    if(v.empty()) {
        cout << "Vector is empty! Cannot access front/back.\n";
    } else {
        cout << "Front: " << v.front() << ", Back: " << v.back() << "\n";
    }
}

int main() {
    vector<int> emptyVec;
    vector<int> filledVec = {1, 2, 3};
    printEnds(emptyVec);
    printEnds(filledVec);
    return 0;
}
```

### Output
Vector is empty! Cannot access front/back.
Front: 1, Back: 3

## Excessive Reallocation

Repeated insertions may trigger multiple reallocations.

When the approximate size is known:

```text
Use reserve()
```

to improve performance.

### Practice Problem

**Problem Statement:** Show size and capacity checks demonstrating reallocation happens multiple times when we do not use `reserve()` vs once when we do.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(5);
    cout << "Reserved Capacity: " << v.capacity() << "\n";
    for(int i = 0; i < 5; ++i) v.push_back(i);
    cout << "Final Capacity: " << v.capacity() << "\n";
    return 0;
}
```

### Output
Reserved Capacity: 5
Final Capacity: 5

# Iterator Support in Vectors

Vectors fully support STL iterators, making them compatible with almost all STL algorithms.

Iterators allow traversal without using indexes.

Benefits:

- Cleaner code
- STL compatibility
- Better flexibility
- Container-independent programming

Common iterator types supported by vectors:

- Iterator
- Constant Iterator
- Reverse Iterator
- Constant Reverse Iterator

Because vectors provide Random Access Iterators, they support operations such as:

- Increment
- Decrement
- Iterator arithmetic
- Distance calculation
- Comparison operations

This makes vectors one of the most powerful STL containers.

## Practice Problem

**Problem Statement:** Traverse a vector of floats using const reverse iterators.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<double> v = {10.5, 20.5, 30.5};
    cout << "Reverse traversal: ";
    for(auto it = v.crbegin(); it != v.crend(); ++it) {
        cout << *it << " ";
    }
    cout << "\n";
    return 0;
}
```

### Output
Reverse traversal: 30.5 20.5 10.5

# Using STL Algorithms with Vectors

One major advantage of vectors is their seamless integration with STL algorithms.

Commonly used algorithms include:

| Algorithm | Purpose |
| --- | --- |
| sort() | Sort elements |
| reverse() | Reverse elements |
| find() | Search element |
| count() | Count occurrences |
| binary_search() | Search in sorted vector |
| max_element() | Find largest element |
| min_element() | Find smallest element |
| accumulate() | Find sum of elements |
| unique() | Remove consecutive duplicates |

These algorithms reduce development time and improve code readability.

## Practice Problem

**Problem Statement:** Demonstrate the use of `std::accumulate()` and `std::max_element()` on a vector.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <numeric>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {4, 1, 9, 2, 7};
    int sum = accumulate(v.begin(), v.end(), 0);
    int maxVal = *max_element(v.begin(), v.end());
    cout << "Sum: " << sum << ", Max Element: " << maxVal << "\n";
    return 0;
}
```

### Output
Sum: 23, Max Element: 9

# Memory Efficiency in Vectors

Vectors attempt to balance performance and memory usage.

When elements are added:

- Memory may grow automatically.
- Capacity often increases exponentially.
- Reallocation happens only occasionally.

Advantages:

- Faster insertions.
- Reduced allocation overhead.
- Better runtime performance.

Disadvantages:

- Slightly more memory than currently required may be reserved.

This trade-off helps vectors achieve excellent practical performance.

## Practice Problem

**Problem Statement:** Write a program that measures capacity before and after `shrink_to_fit()` following dynamic sizing.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.reserve(100);
    v.push_back(1);
    cout << "Before shrink: Capacity = " << v.capacity() << "\n";
    v.shrink_to_fit();
    cout << "After shrink: Capacity = " << v.capacity() << "\n";
    return 0;
}
```

### Output
Before shrink: Capacity = 100
After shrink: Capacity = 1

# Vector vs Other STL Containers

Choosing the correct container is important.

| Requirement | Recommended Container |
| --- | --- |
| Fast Random Access | Vector |
| Frequent Front Insertions | Deque |
| Frequent Middle Insertions | List |
| Unique Sorted Elements | Set |
| Key-Value Storage | Map |
| Fast Lookup | Unordered Map |
| Priority Processing | Priority Queue |

Vectors are generally the default choice unless a specific requirement suggests otherwise.

## Practice Problem

**Problem Statement:** Compare vector and deque by displaying element access of vector vs front insertion of deque.

**Code:**

```cpp
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

int main() {
    deque<int> d = {2, 3};
    d.push_front(1);
    vector<int> v = {1, 2, 3};
    cout << "Deque Front: " << d.front() << ", Vector Index 0: " << v[0] << "\n";
    return 0;
}
```

### Output
Deque Front: 1, Vector Index 0: 1

# Key Takeaways

- Vector is a dynamic array provided by STL.
- Elements are stored in contiguous memory locations.
- Supports automatic resizing.
- Provides fast random access.
- Integrates seamlessly with STL algorithms.
- Supports iterators for traversal.
- Ideal for most real-world applications involving dynamic data.
- Frequently used in interviews, competitive programming, and software development.

A strong understanding of vectors forms the foundation for learning advanced STL containers such as **Deque, List, Stack, Queue, Set, Map, Unordered Map, Priority Queue, and Graph Representations**.

## Practice Problem

**Problem Statement:** Summarize vector usage by printing size, front element, back element, and custom validation.

**Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {100, 200, 300};
    cout << "Key Takeaways Demo - Size: " << v.size() << ", Front: " << v.front() << ", Back: " << v.back() << "\n";
    return 0;
}
```

### Output
Key Takeaways Demo - Size: 3, Front: 100, Back: 300




