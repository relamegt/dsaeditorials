# Introduction to C++

C++ is a versatile general-purpose programming language developed by Bjarne Stroustrup as an extension of the C programming language, introducing object-oriented programming concepts. It combines the efficiency of C with advanced programming features, making it suitable for a wide range of applications.

### The key features of C++ include:

- ****Low- **Level** Access** :** C++ allows direct interaction with system resources and memory, making it ideal for            developing embedded systems, compilers, operating systems, and web browsers.
- **High Performance:**  Known for its fast execution speed, C++ is widely used in performance-critical applications such as game engines, real-time systems, and high-performance software.
- **Object-Oriented Programming:**  C++ supports object-oriented principles such as encapsulation, inheritance, and polymorphism, enabling developers to create scalable, maintainable, and reusable software for large-scale applications.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/introduction-to-c/1780298545744-1.png)

### First C++ Program

The following C++ program demonstrates the fundamental structure of a C++ application. It provides an introduction to the essential components of a program and helps you understand how each part functions. Learn more about its working in the following article.

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

### Output
Hello, World!

### **Structure of a C++ Program**

The structure of a C++ program represents the standard format that every C++ program should follow. Adhering to this format helps the compiler understand the code correctly and ensures successful compilation. The basic structure consists of the following components:

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/introduction-to-c/1780298730130-2.png)

1. Header File: The  `#include <iostream>`  directive includes the input and output stream library, enabling the use of objects such as  `cin`  and  `cout` . Other commonly used header files include  `fstream`  for file handling,  `string`  for string manipulation,  `vector`  for dynamic arrays, and  `bits/stdc++.h`  for accessing most standard libraries at once.
2. Namespace Declaration: The statement  `using namespace std;`  allows programmers to use standard library components like  `cout`  and  `cin`  without prefixing them with  `std::` .
3. Main Function: The  `int main()`  function serves as the starting point of every C++ program. Program execution begins here, and  `return 0;`  indicates that the program has finished successfully.
4. Comments: Comments are used to improve code readability and documentation. Single-line comments are written using  `//` , while multi-line comments are enclosed within  `/* ... */` . The compiler ignores comments during execution.
5. Statements: Statements contain the instructions that the program executes. For example,  `cout << "Hello World!";`  displays the text  *Hello World!*  on the screen using the insertion operator ( `<<` ).
6. Return Statement: The  `return 0;`  statement ends the execution of the  `main()`  function and signals successful program completion to the operating system.

### History of C++

C++ is a powerful object-oriented, middle-level programming language created by Bjarne Stroustrup at Bell Labs in 1979. Initially known as  **“C with Classes,”**  it was renamed  **C++**  in 1983. The language was designed as an extension of C, introducing features such as classes, inheritance, encapsulation, and stronger type checking to support object-oriented programming.

Over the years, C++ has evolved through several standardized versions, including  **C++98, C++11, C++17, C++20, and C++23** , each bringing new features, performance improvements, and enhanced safety. Today, C++ is extensively used in operating systems, game development, embedded systems, competitive programming, high-performance computing, and large-scale software applications due to its efficiency, flexibility, and powerful programming capabilities.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/introduction-to-c/1780299041953-3.png)

Next Read : C++ vs Other Languages



Article Tags:C++,CPP-Basics
