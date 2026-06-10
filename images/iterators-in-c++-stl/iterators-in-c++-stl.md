# Iterators in C++ STL

## Introduction to Iterators

Iterators are one of the most important components of the Standard Template Library (STL). They act as a bridge between STL containers and STL algorithms.

An iterator is an object that behaves similarly to a pointer and is used to access, traverse, and manipulate elements stored inside a container.

In simple words, an iterator points to an element inside a container and allows us to move through the container one element at a time.

Almost every STL algorithm such as:

- sort()
- find()
- count()
- reverse()
- binary_search()

works using iterators rather than directly working on containers.

Because of this design, the same algorithm can work with multiple container types without needing separate implementations.

For example, the `count()` algorithm can work with:

- vector
- list
- deque
- set
- multiset

using exactly the same syntax.

This flexibility is one of the major reasons why STL is powerful and widely used.

## Why Do We Need Iterators?

Before STL was introduced, different data structures required different traversal methods.

For example:

- Arrays use indexes.
- Linked Lists use node pointers.
- Trees require traversal algorithms.
- Hash tables require bucket traversal.

This created inconsistency because algorithms had to be implemented separately for each data structure.

Consider the following examples.

Student marks stored in an array:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100407867-Screenshot_2026-06-10_193628.png)

Employee IDs stored in a linked list:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100110951-bfa1b6b2-0ef0-4288-9df1-96a8517e9c6a.png)

Product IDs stored in a set:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100044044-3c3f5466-c861-434f-a194-59fb4fc1f6b9.png)

Without iterators, different traversal logic would be required for each structure.

Iterators solve this problem by providing a common interface for accessing elements regardless of the underlying container.

As a result:

- Algorithms become reusable.
- Code becomes cleaner.
- Containers become independent of algorithms.
- Development becomes faster.

This concept is known as Generic Programming and forms the foundation of STL.

## Iterator as a Generalized Pointer

An iterator behaves similarly to a pointer.

Both pointers and iterators can:

- Point to an element
- Access values using *
- Move to the next element
- Compare positions

For example:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781099566006-ec2ee828-b891-4037-9f2e-2eccebdde1c4.png)

The iterator continues moving until it reaches the position returned by `end()`.

Although iterators resemble pointers, they are more flexible because they work with different container types without exposing internal implementation details.

## Relationship Between Containers, Iterators and Algorithms

The STL is built on three major components:

- Containers
- Iterators
- Algorithms

Their relationship can be represented as:

```text
Container  ←→  Iterator  ←→  Algorithm
```

Explanation:

- Containers store data.
- Iterators access data.
- Algorithms process data.

For example:

```text
Vector stores student marks.

Iterator accesses the marks.

sort() arranges the marks in ascending order.
```

Without iterators, algorithms would not know how to access elements stored inside containers.

## Declaring Iterators

Iterators can be declared using the container type.

### Syntax

```cpp
container_type::iterator iteratorName;
```

### Example

```cpp
vector<int>::iterator it;
```

Modern C++ provides a simpler approach using `auto`.

### Example

```cpp
auto it = marks.begin();
```

Using `auto` is generally preferred because it automatically determines the iterator type.

## Basic Iterator Traversal

The most common use of iterators is traversing containers.

An iterator usually starts at the beginning of the container and keeps moving forward until it reaches the end.

Example traversal:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100637850-Screenshot_2026-06-10_193933.png)

After multiple increments:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100708560-Screenshot_2026-06-10_194133.png)

This process allows every element in the container to be visited exactly once.

## Container Iterator Functions

Most STL containers provide predefined member functions that return iterators.

These functions provide different ways to access container elements.

### begin()

Returns an iterator pointing to the first element.

Example:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100778699-Screenshot_2026-06-10_193933.png)

### end()

Returns an iterator pointing to the position immediately after the last element.

Example:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/iterators-in-c-stl/1781100811100-Screenshot_2026-06-10_194303.png)

### cbegin()

Returns a constant iterator to the first element.

A constant iterator allows reading but not modifying elements.

### cend()

Returns a constant iterator to the position after the last element.

### rbegin()

Returns a reverse iterator pointing to the last element.

Example:

```text
10 20 30 40
          ^
          |
       rbegin()
```

### rend()

Returns a reverse iterator pointing before the first element.

### crbegin()

Returns a constant reverse iterator.

Elements can be read but not modified.

### crend()

Returns a constant reverse end iterator.

These iterator functions provide multiple traversal options for containers.

## Iterator Operations

Several operations can be performed on iterators.

These operations make iterators powerful tools for container traversal and manipulation.

### Dereferencing Iterators

Dereferencing means accessing the value pointed to by the iterator.

The dereference operator (*) is used.

Example:

```text
Iterator → 50

*Iterator = 50
```

This operation is similar to pointer dereferencing.

### Incrementing Iterators

Incrementing moves the iterator to the next element.

Example:

```text
10 20 30 40

Before:
^

After ++:
   ^
```

### Decrementing Iterators

Decrementing moves the iterator to the previous element.

Example:

```text
10 20 30 40

Before:
      ^

After --:
   ^
```

Not all iterator types support decrement operations.

### Adding or Subtracting Integers

Random access iterators allow arithmetic operations.

Example:

```text
10 20 30 40 50

Iterator at 10

it + 2

Iterator moves to 30
```

Supported by:

- vector
- deque
- array

Not supported by:

- list
- set
- map

### Subtracting Two Iterators

Two iterators can be subtracted to determine the distance between them.

Example:

```text
10 20 30 40 50

it1 → 10
it2 → 40

Distance = 3
```

### Comparing Iterators

Iterators can be compared using:

- ==
- !=
- &lt;
- &gt;
- &lt;=
- &gt; =

Comparison helps determine traversal completion and relative positions.

## Types of Iterators

STL iterators are classified according to the operations they support.

### Input Iterator

Input iterators can only read elements.

Characteristics:

- Single-pass traversal
- Read-only access
- Supports increment operation

Applications:

- Reading data streams
- File input processing

### Output Iterator

Output iterators can only write elements.

Characteristics:

- Single-pass traversal
- Write-only access

Applications:

- Writing data to streams
- Output generation

### Forward Iterator

Forward iterators support multiple passes through a container.

Characteristics:

- Read and write operations
- Forward movement only

Containers:

- forward_list
- unordered_set
- unordered_map

### Bidirectional Iterator

Bidirectional iterators support movement in both directions.

Characteristics:

- Forward traversal
- Backward traversal

Containers:

- list
- set
- map
- multiset
- multimap

### Random Access Iterator

Random access iterators provide the highest level of functionality.

Characteristics:

- Direct element access
- Arithmetic operations
- Fast movement

Containers:

- vector
- deque
- array

These iterators behave almost exactly like pointers.

## Iterator Adaptors

Iterator adaptors are specialized iterators that provide additional functionality.

They are built on top of existing iterators.

### Reverse Iterator

Allows traversal from the end towards the beginning.

Applications:

- Reverse printing
- Reverse searching

### Stream Iterators

Treat input and output streams as containers.

Applications:

- Reading file data
- Writing data to files

### Move Iterators

Enable move semantics.

Benefits:

- Faster execution
- Reduced memory usage
- Efficient resource transfer

### Inserter Iterators

Used for inserting elements into containers.

Types include:

- back_insert_iterator
- front_insert_iterator
- insert_iterator

Applications:

- Dynamic insertion
- Data merging
- Container expansion

## Iterator Utility Functions

STL provides several utility functions that simplify iterator operations.

### advance()

Moves an iterator by a specified number of positions.

Applications:

- Skipping elements
- Navigation

### next()

Returns a new iterator positioned ahead of the current iterator.

### prev()

Returns a new iterator positioned behind the current iterator.

### distance()

Calculates the number of elements between two iterators.

Applications:

- Range calculations
- Position determination

### begin() and end()

Provide universal access to container boundaries.

### rbegin() and rend()

Provide reverse traversal support.

### inserter()

Creates an insertion iterator at a specific position.

### back_inserter()

Creates an insertion iterator at the end of a container.

### front_inserter()

Creates an insertion iterator at the front of a container.

## Applications of Iterators

Iterators are used extensively throughout STL.

### Traversing Containers

The most common use of iterators.

Applications:

- Printing elements
- Processing records
- Data analysis

### Reverse Traversal

Reverse iterators simplify backward traversal.

Applications:

- Reverse printing
- Undo operations

### Container-Independent Algorithms

Algorithms work on iterators instead of containers.

Examples:

- sort()
- find()
- count()
- reverse()

This allows the same algorithm to work with multiple containers.

### Data Processing

Iterators simplify data manipulation and transformation.

Applications:

- Student record analysis
- Sales reporting
- Log processing

### Searching Operations

Iterators are heavily used with searching algorithms.

Examples:

- find()
- binary_search()
- lower_bound()
- upper_bound()

## Advantages of Iterators

| Advantage | Description |
| --- | --- |
| Container Independence | Same traversal mechanism for all containers |
| Algorithm Compatibility | Works seamlessly with STL algorithms |
| Reusability | Same code works with multiple containers |
| Generic Programming | Supports template-based programming |
| Flexibility | Supports different traversal directions |
| Efficiency | Provides optimized access mechanisms |

## Limitations of Iterators

| Limitation | Description |
| --- | --- |
| Complexity | Different iterator categories can confuse beginners |
| Container Restrictions | Some operations are only supported by specific iterators |
| Invalid Iterators | Insertions and deletions may invalidate iterators |
| Debugging Difficulty | Iterator-related errors can be difficult to identify |

## Summary

Iterators are objects that provide a uniform way to access and traverse elements stored inside STL containers. They act as a bridge between containers and algorithms, enabling generic programming and code reusability.

Different iterator categories provide different capabilities, ranging from simple input/output access to full random access. STL also provides iterator adaptors and utility functions that extend iterator functionality.

Understanding iterators is essential because they form the foundation of STL algorithms, container traversal, and modern C++ programming.




