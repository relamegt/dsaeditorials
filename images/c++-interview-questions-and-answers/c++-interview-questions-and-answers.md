# C++ Interview Questions and Answers

**Last Updated:** 6 May, 2026

C++ is a powerful, high-performance, general-purpose, and object-oriented programming language designed by Bjarne Stroustrup at Bell Labs. It extends C by adding features like classes, inheritance, polymorphism, templates, and exception handling. It is widely used in systems programming, game development, embedded systems, high-frequency trading, and large-scale applications where hardware control and performance are critical.

This guide provides a comprehensive list of C++ interview questions and answers, categorized into Freshers, Intermediate, and Expert levels, to help you prepare thoroughly.

# C++ Interview Questions for Freshers

## 1. What is C++? What are the advantages of C++?

C++ is an extension of the C programming language that incorporates Object-Oriented Programming (OOP) principles while retaining low-level capabilities. It is a multi-paradigm language that supports procedural, object-oriented, and generic programming.

### Advantages of C++:

- **High Performance & Speed:** C++ is a compiled language that executes close to the hardware. It allows manual optimization and has minimal runtime overhead.
- **Object-Oriented Programming (OOP):** Supports concepts like Encapsulation, Abstraction, Inheritance, and Polymorphism, promoting code reusability and structured design.
- **Direct Memory Management:** Provides developers control over memory allocation and deallocation using pointers and operators like `new` and `delete`.
- **Standard Template Library (STL):** Offers a rich collection of built-in containers (like vector, set, map) and algorithms, saving development time and effort.
- **Portability:** C++ code can be compiled and run across different operating systems with minimal changes.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Welcome to C++ Programming!" << endl;
    return 0;
}
```

### Output
Welcome to C++ Programming!

## 2. What are the different data types present in C++?

Data types define the type and size of data a variable can store. The C++ compiler allocates memory based on the specified data type.

### Classification of Data Types

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-interview-questions-and-answers/1781189172537-72a7bed4-7a6e-4a43-9066-14430f33ddc6.png)

1. **Primitive Data Types:** Built-in types that are directly supported by the compiler (e.g., `int`, `char`, `float`, `double`, `bool`, `void`, `wchar_t`).
2. **Derived Data Types:** Types derived from primitive data types (e.g., Arrays, Pointers, References, Functions).
3. **User-Defined Data Types:** Defined by the programmer (e.g., `struct`, `union`, `class`, `enum`).

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 21;
    char grade = 'A';
    float distance = 4.5f;
    double exact_pi = 3.14159265358979;
    bool isCPlusPlusFun = true;

    cout << "Age: " << age << " (Size: " << sizeof(age) << " bytes)" << endl;
    cout << "Grade: " << grade << " (Size: " << sizeof(grade) << " byte)" << endl;
    cout << "Distance: " << distance << " (Size: " << sizeof(distance) << " bytes)" << endl;
    cout << "Pi: " << exact_pi << " (Size: " << sizeof(exact_pi) << " bytes)" << endl;
    cout << "Boolean: " << isCPlusPlusFun << " (Size: " << sizeof(isCPlusPlusFun) << " byte)" << endl;

    return 0;
}
```

### Output
Age: 21 (Size: 4 bytes)
Grade: 'A' (Size: 1 byte)
Distance: 4.5 (Size: 4 bytes)
Pi: 3.14159 (Size: 8 bytes)
Boolean: 1 (Size: 1 byte)

## 3. Define 'std'?

In C++, `std` stands for "standard". It is the default namespace that encapsulates all the standard library components, such as `cout`, `cin`, `vector`, `string`, and `map`. Using a namespace helps avoid name collisions between standard library functions and custom user-defined names.

The statement `using namespace std;` imports the entire `std` namespace into the global scope. While convenient for simple programs, importing namespaces globally is generally discouraged in large production projects to prevent naming conflicts.

### Code Example

```cpp
#include <iostream>

int main() {
    // Explicit namespace resolution using ::
    std::cout << "Using explicit std:: namespace resolution." << std::endl;
    return 0;
}
```

### Output
Using explicit std:: namespace resolution.

## 4. What are references in C++?

A reference is an alias (another name) for an existing variable. Once initialized, the reference becomes bound to that variable and cannot be changed to refer to any other variable.

### Key Characteristics:

- Must be initialized at the time of declaration.
- Cannot be `NULL`.
- Operates on the same memory location as the original variable.
- Shares the same address as the variable it references.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int original = 100;
    int& ref = original; // ref is an alias for original

    cout << "Original: " << original << endl;
    cout << "Reference: " << ref << endl;

    ref = 200; // Modifying ref updates original
    cout << "After modifying reference:" << endl;
    cout << "Original: " << original << endl;
    cout << "Reference: " << ref << endl;
    cout << "Addresses match: " << (&original == &ref ? "Yes" : "No") << endl;

    return 0;
}
```

### Output
Original: 100
Reference: 100
After modifying reference:
Original: 200
Reference: 200
Addresses match: Yes

## 5. What do you mean by Call by Value and Call by Reference?

These are two methods of passing arguments to functions:

| Feature | Call by Value | Call by Reference |
| --- | --- | --- |
| **Passing Mechanism** | A copy of the actual variable is passed. | The memory address (alias) of the variable is passed. |
| **Modification** | Changes made inside the function do not affect the original variable. | Changes made inside the function affect the original variable. |
| **Memory Allocation** | Parameters are stored in different memory locations. | Parameters share the same memory locations. |
| **Performance** | Slower and memory inefficient for large objects due to copying. | Faster and memory efficient since no copy is created. |

### Code Example

```cpp
#include <iostream>
using namespace std;

void callByValue(int x) {
    x = 100;
}

void callByReference(int& x) {
    x = 200;
}

int main() {
    int a = 10;
    int b = 10;

    callByValue(a);
    cout << "After callByValue, a = " << a << endl;

    callByReference(b);
    cout << "After callByReference, b = " << b << endl;

    return 0;
}
```

### Output
After callByValue, a = 10
After callByReference, b = 200

## 6. Define token in C++

A token is the smallest individual block/unit of a program that the compiler recognizes.

- **Keywords:** Predefined words that have special meanings (e.g., `int`, `for`, `class`, `return`).
- **Identifiers:** User-defined names for variables, functions, and classes (e.g., `myVar`, `calculateSum`).
- **Constants:** Fixed values that do not change during runtime (e.g., `10`, `3.14`).
- **Strings:** Sequential sequences of characters (e.g., `"Hello, World!"`).
- **Special Symbols:** Characters with syntax-specific meanings (e.g., `[ ]`, `( )`, `{ }`, `;`, `,`).
- **Operators:** Symbols used to perform operations on variables and values (e.g., `+`, `-`, `*`, `/`, `=`, `==`).

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    // int is a Keyword
    // value is an Identifier
    // = is an Operator
    // 50 is a Constant
    // ; is a Special Symbol
    int value = 50; 
    cout << "Value: " << value << endl;
    return 0;
}
```

### Output
Value: 50

## 7. What is the difference between C and C++?

| Feature | C | C++ |
| --- | --- | --- |
| **Programming Paradigm** | Procedural/Structured programming. | Multi-paradigm (Procedural & Object-Oriented). |
| **Classes & Objects** | Not supported. | Supported. |
| **Overloading** | Does not support Function or Operator Overloading. | Supports Function and Operator Overloading. |
| **Focus** | Focuses on step-by-step instructions (procedure-driven). | Focuses on data security and real-world representations (object-driven). |
| **Memory Management** | Uses `malloc()` and `free()`. | Uses `new` and `delete` operators. |
| **Data Hiding** | Not supported (no access modifiers). | Supported via access specifiers (`private`, `protected`). |

### Code Example

```cpp
#include <iostream>
using namespace std;

// C++ allows object-oriented structure
class Greeting {
public:
    void printMessage() {
        cout << "Hello from C++ Object-Oriented world!" << endl;
    }
};

int main() {
    Greeting greet;
    greet.printMessage();
    return 0;
}
```

### Output
Hello from C++ Object-Oriented world!

## 8. What is the difference between struct and class?

In C++, `struct` and `class` are functionally identical except for default behaviors:

| Aspect | struct | class |
| --- | --- | --- |
| **Default Access Modifier** | Members and inheritance are `public` by default. | Members and inheritance are `private` by default. |
| **Typical Use Case** | Used for grouping simple data elements (Plain Old Data / POD). | Used for building complex objects containing behavior, methods, and encapsulation. |
| **Access Control** | Allows access modifiers, but rarely used with them. | Frequently uses `public`, `private`, and `protected` modifiers. |

### Code Example

```cpp
#include <iostream>
using namespace std;

struct Point {
    int x; // public by default
    int y;
};

class Rectangle {
    int width, height; // private by default
public:
    void setDimensions(int w, int h) {
        width = w;
        height = h;
    }
    int getArea() { return width * height; }
};

int main() {
    Point p = {10, 20}; // Can access directly
    cout << "Point: (" << p.x << ", " << p.y << ")" << endl;

    Rectangle rect;
    rect.setDimensions(5, 10);
    cout << "Rectangle Area: " << rect.getArea() << endl;

    return 0;
}
```

### Output
Point: (10, 20)
Rectangle Area: 50

## 9. What is the difference between reference and pointer?

| Aspect | Reference | Pointer |
| --- | --- | --- |
| **Definition** | An alias for an existing variable. | A variable that stores the memory address of another variable. |
| **Reassignment** | Cannot be reassigned to refer to another variable. | Can be reassigned to point to different memory locations. |
| **Null Values** | Cannot be `NULL`. Must bind to a valid object. | Can be `NULL` (`nullptr`). |
| **Syntax** | Uses the `.` operator to access members directly. | Uses the `->` operator or dereferences (`*`) to access members. |
| **Memory Allocation** | Does not occupy separate storage space in memory. | Occupies its own memory space (e.g., 4 or 8 bytes). |

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int val = 10;
    int other = 20;

    int& ref = val;
    int* ptr = &val;

    cout << "val through reference: " << ref << endl;
    cout << "val through pointer: " << *ptr << endl;

    // Pointer can be reassigned
    ptr = &other;
    cout << "ptr now points to: " << *ptr << endl;

    return 0;
}
```

### Output
val through reference: 10
val through pointer: 10
ptr now points to: 20

## 10. What is the difference between function overloading and operator overloading?

| Aspect | Function Overloading | Operator Overloading |
| --- | --- | --- |
| **Definition** | Having multiple functions with the same name but different signatures. | Redefining the behavior of built-in operators (like `+`, `-`, `<<`) to work on user-defined objects. |
| **Purpose** | To perform similar tasks with different types or numbers of arguments. | To write clean, intuitive syntax for custom types/classes. |
| **Complexity** | Simple type matching checks during compile-time. | Involves implementing special operator methods or helper functions. |

### Code Example

```cpp
#include <iostream>
using namespace std;

// Function Overloading
void display(int i) {
    cout << "Int: " << i << endl;
}
void display(double f) {
    cout << "Double: " << f << endl;
}

// Operator Overloading
class Complex {
public:
    int real, imag;
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    Complex operator + (const Complex& obj) {
        return Complex(real + obj.real, imag + obj.imag);
    }
};

int main() {
    display(10);
    display(3.14);

    Complex c1(3, 4), c2(1, 2);
    Complex c3 = c1 + c2; // Calls custom + operator
    cout << "Complex Result: " << c3.real << " + " << c3.imag << "i" << endl;

    return 0;
}
```

### Output
Int: 10
Double: 3.14
Complex Result: 4 + 6i

## 11. What is the difference between an array and a list?

| Feature | Array | List (`std::list`) |
| --- | --- | --- |
| **Memory Layout** | Contiguous memory allocation. | Non-contiguous memory allocation (nodes linked via pointers). |
| **Size** | Fixed size (for raw arrays) or dynamic capacity (for vectors). | Fully dynamic sizing; elements can be inserted/removed easily. |
| **Access Speed** | $O(1)$ constant time random access via index. | $O(N)$ sequential access (must traverse links). |
| **Insertion/Deletion** | Slow ($O(N)$) as elements must shift. | Fast ($O(1)$) once the position is located. |
| **Memory Overhead** | Lower memory requirement (only holds data). | Higher memory requirement (holds data and forward/backward pointers). |

### Code Example

```cpp
#include <iostream>
#include <vector>
#include <list>
using namespace std;

int main() {
    // Array / Vector representation
    vector<int> arr = {10, 20, 30};
    cout << "Array index 1: " << arr[1] << endl;

    // List representation
    list<int> lst = {100, 200, 300};
    // Need an iterator to access list element
    auto it = lst.begin();
    advance(it, 1);
    cout << "List position 1: " << *it << endl;

    return 0;
}
```

### Output
Array index 1: 20
List position 1: 200

## 12. What is the difference between const and #define?

- **`const`:** Enforced by the compiler, respects scoping rules, has a defined data type, and allows type-checking, preventing hard-to-debug replacement errors.
- **`#define`:** A preprocessor directive that performs literal string replacement throughout the source file before compilation. It lacks scope and type-checking.

### Code Example

```cpp
#include <iostream>
using namespace std;

#define MACRO_PI 3.1415
const double CONST_PI = 3.1415;

int main() {
    cout << "Macro PI: " << MACRO_PI << endl;
    cout << "Const PI: " << CONST_PI << endl;
    return 0;
}
```

### Output
Macro PI: 3.1415
Const PI: 3.1415

## 13. What is the difference between a while loop and a do-while loop?

| Feature | while loop | do-while loop |
| --- | --- | --- |
| **Condition Check** | Evaluated at the start of the loop (Pre-test loop). | Evaluated at the end of the loop (Post-test loop). |
| **Minimum Runs** | May execute $0$ times if the condition starts as false. | Always executes at least $1$ time. |
| **Syntax** | `while(cond) { ... }` | `do { ... } while(cond);` |
| **Semicolon** | No semicolon after condition wrapper. | Semicolon is mandatory after `while(cond);`. |

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int i = 5;

    // while loop checking condition first
    while (i < 5) {
        cout << "Inside while" << endl;
    }

    // do-while loop executes block then checks condition
    do {
        cout << "Inside do-while" << endl;
    } while (i < 5);

    return 0;
}
```

### Output
Inside do-while

## 14. What is the difference between a reference and a pointer?

*(This question provides a hands-on code comparison showing reference bounds and pointer mechanics to expand on structural concepts.)*

A reference acts as a permanent alias for a variable, sharing its address directly. A pointer is an independent variable storing the target's address, which can be modified or set to null at any time.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10;

    int& ref = a;    // reference
    int* ptr = &a;   // pointer

    cout << "ref value: " << ref << endl;
    cout << "ptr pointed value: " << *ptr << endl;

    *ptr = 20;
    cout << "After modifying via pointer, a = " << a << endl;

    ref = 30;
    cout << "After modifying via reference, a = " << a << endl;

    return 0;
}
```

### Output
ref value: 10
ptr pointed value: 10
After modifying via pointer, a = 20
After modifying via reference, a = 30

## 15. Define storage class in C++ and name some

Storage classes dictate the lifetime, visibility (scope), and linkage of variables and functions.

```text
┌─────────────────┬────────────────────────────────────────────────────────┐
│ Storage Class   │ Lifetime / Scope Details                               │
├─────────────────┼────────────────────────────────────────────────────────┤
│ auto            │ Automatic local variables (default inside blocks).     │
│ register        │ Suggests storing in CPU register (deprecated in C++17).│
│ static          │ Retains value throughout program execution.            │
│ extern          │ Global scope variable defined in another file.         │
│ mutable         │ Allows editing class members within const methods.     │
│ thread_local    │ Separate instance of variable for each execution thread│
└─────────────────┴────────────────────────────────────────────────────────┘
```

### Code Example

```cpp
#include <iostream>
using namespace std;

void counterFunc() {
    static int count = 0; // Value is retained across function calls
    count++;
    cout << "Static Count: " << count << endl;
}

int main() {
    counterFunc();
    counterFunc();
    counterFunc();
    return 0;
}
```

### Output
Static Count: 1
Static Count: 2
Static Count: 3

## 16. Discuss the difference between prefix and postfix?

Prefix (`++x`, `--x`) modifies the variable's value first, and then returns the modified value.
Postfix (`x++`, `x--`) returns the current value of the variable, and then performs the modification.

### Key differences:

- **Prefix:** Operates directly, returning a reference to the updated variable.
- **Postfix:** Creates a copy of the temporary variable, modifies the original, and returns the copy, making postfix slightly slower.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;
    int b = 5;

    int prefixResult = ++a;  // a is now 6, prefixResult gets 6
    int postfixResult = b++; // postfixResult gets 5, b is now 6

    cout << "Prefix Result: " << prefixResult << ", a = " << a << endl;
    cout << "Postfix Result: " << postfixResult << ", b = " << b << endl;

    return 0;
}
```

### Output
Prefix Result: 6, a = 6
Postfix Result: 5, b = 6

## 17. What is the difference between new and malloc()?

| Feature | `new` Operator | `malloc()` Function |
| --- | --- | --- |
| **Type** | C++ operator. | Standard C library function. |
| **Constructor Call** | Calls constructor of the class automatically. | Does not call constructors. |
| **Type Safety** | Typesafe; returns exact type pointer. | Returns `void*` which must be explicitly cast. |
| **Failure Behavior** | Throws `std::bad_alloc` exception on failure. | Returns `NULL` pointer on failure. |
| **Syntax** | `int* p = new int;` | `int* p = (int*)malloc(sizeof(int));` |
| **Memory Deallocation** | Freed via `delete`. | Freed via `free()`. |

### Code Example

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

class Entity {
public:
    Entity() { cout << "Constructor Invoked!" << endl; }
    ~Entity() { cout << "Destructor Invoked!" << endl; }
};

int main() {
    cout << "--- Allocating using new ---" << endl;
    Entity* obj1 = new Entity();
    delete obj1;

    cout << "--- Allocating using malloc ---" << endl;
    Entity* obj2 = (Entity*)malloc(sizeof(Entity)); // No constructor called
    free(obj2);                                    // No destructor called

    return 0;
}
```

### Output
--- Allocating using new ---
Constructor Invoked!
Destructor Invoked!
--- Allocating using malloc ---

## 18. What is the difference between virtual functions and pure virtual functions?

- **Virtual Function:** A function declared in a base class using the `virtual` keyword that *can* be overridden by derived classes. It contains a default implementation.
- **Pure Virtual Function:** A function declared in a base class with no implementation, initialized to `= 0`. Any class containing a pure virtual function is abstract and cannot be instantiated.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { // Virtual Function
        cout << "Base Default Show" << endl;
    }
    virtual void run() = 0; // Pure Virtual Function
};

class Derived : public Base {
public:
    void run() override {
        cout << "Derived Class running" << endl;
    }
};

int main() {
    // Base b; // Error: Cannot instantiate abstract class
    Base* ptr = new Derived();
    ptr->show(); // Calls base default since not overridden
    ptr->run();  // Calls derived implementation
    delete ptr;
    return 0;
}
```

### Output
Base Default Show
Derived Class running

## 19. What are classes and objects in C++?

- **Class:** A user-defined template or blueprint that defines the member variables (attributes) and member functions (behaviors) that represent a type.
- **Object:** An instance of a class. When a class is declared, no memory is allocated. Memory is allocated only when objects of the class are instantiated.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;

    void display() {
        cout << "Student Name: " << name << endl;
    }
};

int main() {
    Student s;       // Instantiating an object
    s.name = "Rahul"; // Setting property
    s.display();     // Calling method
    return 0;
}
```

### Output
Student Name: Rahul

## 20. What is Function Overriding?

Function Overriding occurs when a derived class redefines a member function that is already declared in its base class. It is the basis for Runtime Polymorphism. To execute function overriding correctly, the signature, arguments, and return types must be identical, and the base function should be declared `virtual`.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void makeSound() {
        cout << "Some generic animal sound" << endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override { // Overridden function
        cout << "Woof! Woof!" << endl;
    }
};

int main() {
    Animal* myAnimal = new Dog();
    myAnimal->makeSound(); // Calls Dog::makeSound() at runtime
    delete myAnimal;
    return 0;
}
```

### Output
Woof! Woof!

## 21. What are the various OOPs concepts in C++?

Object-Oriented Programming (OOP) is a programming paradigm that uses classes and objects to model real-world entities. C++ fully supports the following core OOP concepts:

- **Class:** A user-defined blueprint containing data members and member functions.
- **Object:** An instance of a class that is allocated memory at runtime.
- **Encapsulation:** Binding data and methods into a single unit (class) while controlling access via access specifiers.
- **Abstraction:** Hiding complex implementation details and showing only the essential features to the outside world.
- **Inheritance:** Deriving new classes (derived) from existing ones (base), enabling code reuse.
- **Polymorphism:** The ability of an entity (function, operator, or object) to take multiple forms.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Abstraction: User interacts with class interface without knowing details
class BankAccount {
private:
    double balance; // Encapsulation: Private member data

public:
    BankAccount(double initial_balance) : balance(initial_balance) {}

    void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    double getBalance() { // Public getter to access encapsulated data safely
        return balance;
    }
};

int main() {
    BankAccount myAccount(1000.0);
    myAccount.deposit(500.0);
    cout << "Account Balance: $" << myAccount.getBalance() << endl;
    return 0;
}
```

### Output
Account Balance: $1500

## 22. What is inheritance in C++?

Inheritance is the mechanism by which a new class (derived class) inherits properties, behaviors, and attributes from an existing class (base class). It establishes an "IS-A" relationship and fosters code reusability.

### Types of Inheritance:

1. **Single Inheritance:** One derived class inherits from one base class.
2. **Multiple Inheritance:** One derived class inherits from two or more base classes.
3. **Multilevel Inheritance:** A class is derived from another derived class (A $\rightarrow$ B $\rightarrow$ C).
4. **Hierarchical Inheritance:** Multiple derived classes inherit from a single base class.
5. **Hybrid Inheritance:** A combination of two or more types of inheritance.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Base class
class Animal {
public:
    void eat() {
        cout << "This animal is eating." << endl;
    }
};

// Derived class (Single Inheritance)
class Dog : public Animal {
public:
    void bark() {
        cout << "The dog is barking." << endl;
    }
};

int main() {
    Dog myDog;
    myDog.eat();  // Inherited method
    myDog.bark(); // Class-specific method
    return 0;
}
```

### Output
This animal is eating.
The dog is barking.

## 23. What is encapsulation in C++?

Encapsulation is the process of binding data members (variables) and member functions (methods) together into a single cohesive unit, known as a Class. Along with wrapping data, it enforces access restrictions using modifiers (`private`, `protected`, `public`) to protect the internal state of the object.

### Benefits:

- **Data Protection / Hiding:** Prevents external functions from directly modifying internal variables.
- **Control:** Setter methods can validate data before updating variables.
- **Flexibility:** Implementation details of the class can change without breaking client code.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Employee {
private:
    int salary; // Restricted access

public:
    // Setter method with validation
    void setSalary(int s) {
        if (s > 0) {
            salary = s;
        } else {
            salary = 0;
        }
    }

    // Getter method
    int getSalary() {
        return salary;
    }
};

int main() {
    Employee emp;
    emp.setSalary(50000);
    cout << "Employee Salary: $" << emp.getSalary() << endl;

    emp.setSalary(-1000); // Invalid salary check
    cout << "Invalid Salary Result: $" << emp.getSalary() << endl;
    return 0;
}
```

### Output
Employee Salary: $50000
Invalid Salary Result: $0

## 24. What is virtual inheritance?

Virtual inheritance is an inheritance technique used in C++ to resolve the **Diamond Problem**. The Diamond Problem occurs when a grandchild class inherits from two parent classes that both share a common base class, resulting in duplicate copies of the base class members.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/c-interview-questions-and-answers/1781190134243-c03360b1-d325-4a0f-9d9a-bb36237250fd.png)

By inheriting the base class virtually, the compiler ensures that only one instance of the grandparent base class is instantiated and shared.

### Code Example

```cpp
#include <iostream>
using namespace std;

class A {
public:
    int value;
};

// Virtual inheritance prevents duplication of A
class B : virtual public A {};
class C : virtual public A {};

class D : public B, public C {};

int main() {
    D obj;
    obj.value = 42; // unambiguous because of virtual inheritance
    cout << "Shared value: " << obj.value << endl;
    return 0;
}
```

### Output
Shared value: 42

## 25. What is polymorphism in C++?

Polymorphism means "many forms". It is the ability of a function, operator, or object to behave differently depending on the context in which it is used.

### Categories:

1. **Compile-time Polymorphism (Static Binding):** Resolved during compilation. Examples include function overloading and operator overloading.
2. **Run-time Polymorphism (Dynamic Binding):** Resolved during execution. It is achieved through function overriding and virtual functions.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Print {
public:
    // Compile-time polymorphism (Function Overloading)
    void show(int i) {
        cout << "Integer: " << i << endl;
    }
    void show(string s) {
        cout << "String: " << s << endl;
    }
};

int main() {
    Print p;
    p.show(100);
    p.show("Polymorphism");
    return 0;
}
```

### Output
Integer: 100
String: Polymorphism

## 26. What are the different types of polymorphism in C++?

C++ supports two main types of polymorphism:

### 1. Compile-Time Polymorphism

- **Function Overloading:** Declaring multiple functions with the same name but different parameter list signatures.
- **Operator Overloading:** Redefining built-in operators (`+`, `-`, `<<`, etc.) to operate on user-defined objects.

### 2. Run-Time Polymorphism

- **Function Overriding:** Redefining a base class `virtual` function inside a derived class to customize behavior.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Base class for Run-time polymorphism
class Base {
public:
    virtual void print() {
        cout << "Base class print function" << endl;
    }
};

class Derived : public Base {
public:
    void print() override {
        cout << "Derived class print function" << endl;
    }
};

int main() {
    Base* ptr = new Derived();
    ptr->print(); // Runtime polymorphism determines call to Derived::print()
    delete ptr;
    return 0;
}
```

### Output
Derived class print function

## 27. Compare compile-time polymorphism and Runtime polymorphism

| Feature | Compile-Time Polymorphism | Run-Time Polymorphism |
| --- | --- | --- |
| **Alternative Names** | Static Binding, Early Binding. | Dynamic Binding, Late Binding. |
| **Resolution Time** | Resolved at compile time. | Resolved at run time. |
| **Mechanism** | Function and Operator overloading. | Virtual functions and inheritance overriding. |
| **Execution Speed** | Faster, since addresses are mapped at compile time. | Slower, as it requires dynamic lookup via vtables. |
| **Flexibility** | Less flexible. | Highly flexible (facilitates plugin architectures). |

### Code Example

```cpp
#include <iostream>
using namespace std;

class Math {
public:
    // Compile-time overloading
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};

int main() {
    Math m;
    cout << "Int Add: " << m.add(5, 10) << endl;
    cout << "Double Add: " << m.add(5.5, 4.5) << endl;
    return 0;
}
```

### Output
Int Add: 15
Double Add: 10

## 28. Explain the constructor in C++.

A constructor is a special member function of a class that is automatically called when an object of that class is created. It is used to initialize the object's data members.

### Properties:

- Same name as the class.
- No return type (not even `void`).
- Can be overloaded.
- Can have default arguments.

### Types of Constructors:

1. **Default Constructor:** Accepts no arguments.
2. **Parameterized Constructor:** Accepts arguments to initialize fields with specific values.
3. **Copy Constructor:** Initializes an object using another existing object of the same class (`ClassName(const ClassName& obj)`).

### Code Example

```cpp
#include <iostream>
using namespace std;

class Box {
private:
    int width;

public:
    // Default Constructor
    Box() {
        width = 0;
        cout << "Default Constructor called." << endl;
    }

    // Parameterized Constructor
    Box(int w) {
        width = w;
        cout << "Parameterized Constructor called. Width = " << width << endl;
    }

    // Copy Constructor
    Box(const Box& other) {
        width = other.width;
        cout << "Copy Constructor called." << endl;
    }
};

int main() {
    Box b1;        // Default
    Box b2(15);    // Parameterized
    Box b3 = b2;   // Copy constructor
    return 0;
}
```

### Output
Default Constructor called.
Parameterized Constructor called. Width = 15
Copy Constructor called.

## 29. What are destructors in C++?

A destructor is a special member function that is automatically called when an object goes out of scope or is explicitly deleted via `delete`. It is responsible for releasing system resources, closing files, and freeing dynamically allocated heap memory.

### Properties:

- Same name as the class, prefixed with a tilde (`~`).
- No parameters and no return type.
- Only one destructor can exist per class (cannot be overloaded).
- Follows a reverse order of destruction compared to constructors (bottom-up).

### Code Example

```cpp
#include <iostream>
using namespace std;

class Resource {
public:
    Resource() {
        cout << "Resource Acquired!" << endl;
    }
    ~Resource() {
        cout << "Resource Released!" << endl;
    }
};

int main() {
    cout << "Entering block..." << endl;
    {
        Resource res; // Constructor called
    } // Out of scope here, Destructor called
    cout << "Exited block." << endl;
    return 0;
}
```

### Output
Entering block...
Resource Acquired!
Resource Released!
Exited block.

## 30. What is a virtual destructor?

A virtual destructor is used in base classes to ensure that the destructors of derived classes are executed correctly when deleting a derived object through a base class pointer.

If the base class destructor is **not** virtual, only the base class destructor will run, which leads to memory leaks and resource leaks of elements owned by the derived class.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    Base() { cout << "Base Constructor" << endl; }
    virtual ~Base() { cout << "Base Destructor (Virtual)" << endl; } // Virtual destructor
};

class Derived : public Base {
private:
    int* data;
public:
    Derived() {
        data = new int[5];
        cout << "Derived Constructor" << endl;
    }
    ~Derived() override {
        delete[] data;
        cout << "Derived Destructor" << endl;
    }
};

int main() {
    Base* ptr = new Derived();
    delete ptr; // Deleting via base class pointer
    return 0;
}
```

### Output
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor (Virtual)

## 31. Is destructor overloading possible? If yes then explain and if no then why?

No, destructor overloading is **not** possible in C++. 

### Reasons:

- Destructors do not take any arguments or parameters.
- Overloading requires function signatures to differ by parameter lists.
- Since destructors accept no arguments, they cannot be differentiated.
- Each class can only have a single destructor (`~ClassName()`).

### Code Example

```cpp
#include <iostream>
using namespace std;

class Demo {
public:
    Demo() {}
    ~Demo() {
        cout << "Standard Destructor running." << endl;
    }

    // ~Demo(int x) { } // Error: Destructors cannot have parameters
};

int main() {
    Demo d;
    return 0;
}
```

### Output
Standard Destructor running.

## 32. When should we use multiple inheritance?

Multiple inheritance is used when a class logically needs to combine features or behaviors from more than one independent base class.

### Use Cases:

- To implement classes that combine multiple distinct interfaces (e.g., a class that is both `Printable` and `Serializable`).
- Real-world modeling where an object fits multiple taxonomy groups (e.g., `TeacherResearcher` inheriting from both `Teacher` and `Researcher`).

### Caution:

Multiple inheritance can lead to ambiguity and compiler errors (e.g., name clashes, diamond problem). It should be replaced with interface classes (classes containing only pure virtual functions) where possible.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Painter {
public:
    void paint() {
        cout << "Painting canvas..." << endl;
    }
};

class Writer {
public:
    void write() {
        cout << "Writing manuscript..." << endl;
    }
};

// Artist inherits features from Painter and Writer
class Artist : public Painter, public Writer {};

int main() {
    Artist art;
    art.paint();
    art.write();
    return 0;
}
```

### Output
Painting canvas...
Writing manuscript...

# C++ Interview Questions - Intermediate Level

## 33. Which operations are permitted on pointers?

Pointers are variables that store the memory addresses of other variables. The following operations are permitted on pointers in C++:

1. **Arithmetic Operations:**

- **Increment (`ptr++`) / Decrement (`ptr--`):** Moves the pointer forward or backward by the size of the data type it points to.
- **Addition / Subtraction of an integer (`ptr + n`, `ptr - n`):** Offsets the pointer by $n$ elements.
- **Subtraction of two pointers (`ptr1 - ptr2`):** Allowed only when both pointers point to elements of the same array; it returns the number of elements between them.

1. **Comparison Operations:**

- Pointers of the same type can be compared using relational operators (`==`, `!=`, `<`, `>`, `<=`, `>=`) to check their relative positions or if they point to the same memory location.

1. **Dereferencing (`*ptr`):** Accessing the value stored at the address pointed to by the pointer.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40};
    int* ptr1 = &arr[0];
    int* ptr2 = &arr[2];

    cout << "Value at ptr1: " << *ptr1 << endl;
    cout << "Value at ptr2: " << *ptr2 << endl;

    // Pointer subtraction
    cout << "Distance between ptr2 and ptr1: " << (ptr2 - ptr1) << " elements" << endl;

    // Pointer arithmetic (Increment)
    ptr1++;
    cout << "Value at ptr1 after increment: " << *ptr1 << endl;

    // Pointer comparison
    if (ptr1 < ptr2) {
        cout << "ptr1 points to an earlier memory address than ptr2." << endl;
    }

    return 0;
}
```

### Output
Value at ptr1: 10
Value at ptr2: 30
Distance between ptr2 and ptr1: 2 elements
Value at ptr1 after increment: 20
ptr1 points to an earlier memory address than ptr2.

## 34. What is the purpose of the "delete" operator?

The `delete` operator is used to manually deallocate memory that was previously allocated on the heap (dynamic memory) using the `new` operator. If dynamically allocated memory is not freed using `delete`, it remains allocated until the program exits, causing a **memory leak**.

### Key features of the `delete` operator:

- It invokes the destructor of the object being deleted before releasing the memory.
- Deleting a pointer that is null (`nullptr`) is safe and does nothing.
- After deletion, the pointer becomes a **dangling pointer** and should be reset to `nullptr` to avoid undefined behavior.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Tracker {
public:
    Tracker() { cout << "Tracker Created." << endl; }
    ~Tracker() { cout << "Tracker Destroyed." << endl; }
};

int main() {
    // Dynamic allocation
    Tracker* myTracker = new Tracker();

    // Manually freeing memory
    delete myTracker;
    myTracker = nullptr; // Prevent dangling pointer

    return 0;
}
```

### Output
Tracker Created.
Tracker Destroyed.

## 35. How delete [] is different from delete?

In C++, `delete` and `delete[]` are used to release dynamic memory, but they target different allocation structures:

| Aspect | `delete` | `delete[]` |
| --- | --- | --- |
| **Target** | Used to deallocate a single object allocated with `new`. | Used to deallocate an array of objects allocated with `new[]`. |
| **Destructors called** | Invokes the destructor only once for the targeted object. | Invokes the destructor for every single element in the array. |
| **Mismatched Usage** | Using `delete` on an array leads to undefined behavior and leaks. | Using `delete[]` on a single object leads to undefined behavior. |

### Code Example

```cpp
#include <iostream>
using namespace std;

class Item {
public:
    ~Item() { cout << "Item Destructor called." << endl; }
};

int main() {
    cout << "--- Deleting single object ---" << endl;
    Item* singleItem = new Item();
    delete singleItem;

    cout << "--- Deleting array of objects ---" << endl;
    Item* itemArray = new Item[3];
    delete[] itemArray; // Correctly calls destructor 3 times

    return 0;
}
```

### Output
--- Deleting single object ---
Item Destructor called.
--- Deleting array of objects ---
Item Destructor called.
Item Destructor called.
Item Destructor called.

## 36. What do you know about friend class and friend function?

Under standard encapsulation rules, non-member functions and outside classes cannot access `private` or `protected` members of a class. However, C++ provides the `friend` keyword to bypass this restriction for specific functions or classes.

### 1. Friend Function

A friend function is a non-member function that is granted access to the private and protected members of a class. It is declared inside the class using the `friend` keyword.

### 2. Friend Class

A friend class is an entire class whose member functions can all access the private and protected members of the class that declares it as a friend.

### Caution:

Friendship is **not mutual** (if Class A is a friend of Class B, Class B is not automatically a friend of Class A) and **not transitive** (if A is a friend of B and B is a friend of C, A is not a friend of C).

### Code Example

```cpp
#include <iostream>
using namespace std;

class ValueContainer {
private:
    int secretValue;

public:
    ValueContainer(int val) : secretValue(val) {}

    // Declaring friend function
    friend void revealSecret(const ValueContainer& obj);

    // Declaring friend class
    friend class ValueInspector;
};

// Friend function definition
void revealSecret(const ValueContainer& obj) {
    cout << "Secret accessed via Friend Function: " << obj.secretValue << endl;
}

// Friend class definition
class ValueInspector {
public:
    void inspect(const ValueContainer& obj) {
        cout << "Secret accessed via Friend Class: " << obj.secretValue << endl;
    }
};

int main() {
    ValueContainer container(999);
    revealSecret(container);

    ValueInspector inspector;
    inspector.inspect(container);

    return 0;
}
```

### Output
Secret accessed via Friend Function: 999
Secret accessed via Friend Class: 999

## 37. What is an Overflow Error?

An **Overflow Error** occurs during an arithmetic operation when the resulting value exceeds the maximum value capacity that the assigned data type is designed to represent.

### Key Points:

- **Signed Integer Overflow:** In C++, signed overflow results in **undefined behavior**. Many compilers default to wrap-around behavior using two's complement, but this should not be relied upon.
- **Unsigned Integer Overflow:** Well-defined in C++; it wraps around modulo $2^{n}$ (where $n$ is the number of bits).

### Code Example

```cpp
#include <iostream>
#include <climits>
using namespace std;

int main() {
    // Demonstrating unsigned wrap-around overflow
    unsigned int maxUnsigned = UINT_MAX;
    cout << "Max Unsigned Value: " << maxUnsigned << endl;

    maxUnsigned = maxUnsigned + 1; // Overflows and wraps to 0
    cout << "After Overflow (Unsigned): " << maxUnsigned << endl;

    return 0;
}
```

### Output
Max Unsigned Value: 4294967295
After Overflow (Unsigned): 0

## 38. What does the Scope Resolution operator do?

The scope resolution operator (`::`) in C++ is used to identify and specify the scope of an identifier (variables, functions, or classes).

### Common Uses of the Scope Resolution Operator:

1. **Accessing Global Variables:** Accesses a global variable when a local variable shares the same name.
2. **Defining Class Methods Externally:** Allows defining a class's member functions outside the class declaration.
3. **Resolving Ambiguity in Multiple Inheritance:** Explicitly calls a method from a specific parent class.
4. **Accessing Namespaces or Static Members:** Refers to static data members or elements within a specific namespace.

### Code Example

```cpp
#include <iostream>
using namespace std;

int number = 100; // Global variable

class Demo {
public:
    static int staticValue;
    void printMessage(); // Declaration only
};

// Defining class method outside the class
void Demo::printMessage() {
    cout << "Method defined outside the class." << endl;
}

// Initializing static variable
int Demo::staticValue = 50;

int main() {
    int number = 10; // Local variable
    cout << "Local Number: " << number << endl;
    cout << "Global Number via :: : " << ::number << endl;

    cout << "Static member of Demo: " << Demo::staticValue << endl;

    Demo d;
    d.printMessage();

    return 0;
}
```

### Output
Local Number: 10
Global Number via :: : 100
Static member of Demo: 50
Method defined outside the class.

## 39. What are the C++ access modifiers?

Access modifiers (or access specifiers) define how class members (attributes and methods) can be accessed outside the class. C++ provides three types:

1. **`public`:** Members are accessible from anywhere in the program.
2. **`private`:** Members are accessible *only* within the class where they are defined. They cannot be accessed or modified directly by external code or derived classes.
3. **`protected`:** Members are accessible within the class itself and by derived classes, but remain inaccessible to the rest of the application.

| Access Modifier | Inside Class | Derived Class | External Code |
| --- | --- | --- | --- |
| public | Yes | Yes | Yes |
| protected | Yes | Yes | No |
| private | Yes | No | No |

**Code Example**

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
    int pubVar = 1;
protected:
    int protVar = 2;
private:
    int privVar = 3;
};

class Child : public Parent {
public:
    void display() {
        cout << "Public: " << pubVar << endl;
        cout << "Protected: " << protVar << endl;
        // cout << "Private: " << privVar << endl; // Error: private is inaccessible
    }
};

int main() {
    Child obj;
    obj.display();
    cout << "Accessing public directly: " << obj.pubVar << endl;
    // cout << "Accessing protected directly: " << obj.protVar << endl; // Error
    return 0;
}
```

### Output
Public: 1
Protected: 2
Accessing public directly: 1

## 40. Can you compile a program without the main function?

Yes, a C++ program can compile successfully without a `main()` function under certain configurations:

1. **Shared/Static Libraries:** Dynamic Link Libraries (DLLs in Windows, `.so` in Linux) and static libraries (`.lib`/`.a`) compile without a `main()` function because they are designed to be loaded by other executable programs.
2. **Custom Entry Points:** The default linker setting can be overridden to point to a custom entry point function using linker flags.
3. **Preprocessor Macros:** By using macros to rename a function name dynamically during compilation.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Using macros to rename the entry point function
#define fun main

int fun() {
    cout << "Compiled and run without writing the word 'main' explicitly!" << endl;
    return 0;
}
```

### Output
Compiled and run without writing the word 'main' explicitly!

## 41. What is STL?

**STL** stands for the **Standard Template Library**. It is a powerful, generic library in C++ that provides pre-written, highly optimized data structures and algorithms. 

### Core Components of STL:

1. **Containers:** Data structures used to store collections of data (e.g., `vector`, `list`, `set`, `map`).
2. **Algorithms:** High-level, template-based functions to perform operations on containers (e.g., `sort`, `binary_search`, `reverse`).
3. **Iterators:** Pointer-like objects used to traverse elements in a container.
4. **Functors:** Objects that act like functions (function objects) by overloading the `()` operator.

### Code Example

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> numbers = {30, 10, 20, 50, 40};

    // STL Algorithm: sort
    sort(numbers.begin(), numbers.end());

    cout << "Sorted elements: ";
    // STL Iterators used implicitly in range-based loop
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

### Output
Sorted elements: 10 20 30 40 50

## 42. What are STL containers? Explain different types with examples.

STL containers are object collections that organize and store data in memory. They are categorized into four types:

### 1. Sequence Containers

Store elements sequentially in linear arrangements.

- `vector`: Dynamic array with fast random access ($O(1)$) and back insertion.
- `list`: Doubly linked list allowing fast insertions and deletions ($O(1)$) anywhere.
- `deque`: Double-ended queue allowing insertion/deletion at both front and back.

### 2. Associative Containers

Store sorted, keyed data. Implemented typically as binary search trees (Self-balancing BST like Red-Black Trees).

- `set`: Collection of unique sorted elements.
- `map`: Collection of unique key-value pairs sorted by key.

### 3. Unordered Associative Containers

Implement hash tables for fast access. Elements are unsorted.

- `unordered_set` / `unordered_map`: Average constant-time operations ($O(1)$).

### 4. Container Adaptors

Provide restricted interfaces over sequence containers.

- `stack` (LIFO), `queue` (FIFO), `priority_queue` (heap-based sorted queue).

### Code Example

```cpp
#include <iostream>
#include <vector>
#include <map>
using namespace std;

int main() {
    // Sequence Container
    vector<string> cities = {"Delhi", "Mumbai"};
    cities.push_back("Bangalore");

    // Associative Container
    map<string, int> ageMap;
    ageMap["Alice"] = 25;
    ageMap["Bob"] = 30;

    cout << "First City: " << cities[0] << endl;
    cout << "Alice's Age: " << ageMap["Alice"] << endl;

    return 0;
}
```

### Output
First City: Delhi
Alice's Age: 25

## 43. What are iterators in STL? Describe types of iterators with examples.

An iterator is a pointer-like object used to navigate and traverse through elements of STL containers. They decouple algorithms from containers, allowing generic algorithms to process different container types uniformly.

### Types of Iterators:

1. **Input Iterator:** Read-only, single-pass, forward direction.
2. **Output Iterator:** Write-only, single-pass, forward direction.
3. **Forward Iterator:** Read-write, multi-pass, forward direction.
4. **Bidirectional Iterator:** Read-write, multi-pass, forward and backward (e.g., `list`, `set`, `map`). Supports `++` and `--`.
5. **Random Access Iterator:** Read-write, direct index jump, multi-pass (e.g., `vector`, `deque`, raw array). Supports `++`, `--`, `+`, `-`, `+=`, `-=`, `<`.

### Code Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> nums = {10, 20, 30, 40};

    // Random Access Iterator
    vector<int>::iterator it = nums.begin();

    cout << "First element: " << *it << endl;
    it += 2; // Direct offset jump
    cout << "Third element: " << *it << endl;

    return 0;
}
```

### Output
First element: 10
Third element: 30

## 44. What are lambda expressions in C++? How do they relate to STL?

A lambda expression is an anonymous (nameless), in-line function that can capture variables from its enclosing scope. Introduced in C++11, they simplify coding by removing the need to declare separate class functors or stand-alone helper functions.

### Syntax:

```text
[capture](parameters) -> return_type { body }
```

- **Capture Clause (`[]`):** Specifies which variables from the surrounding scope are accessible inside the lambda (by value `[=]` or by reference `[&]`).

### Relationship to STL:

Lambdas are highly integrated with STL algorithms to define custom predicates, sorting keys, or operations dynamically.

### Code Example

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> nums = {1, 2, 3, 4, 5, 6};

    // Counting even numbers using an inline lambda predicate
    int evens = count_if(nums.begin(), nums.end(), [](int x) {
        return x % 2 == 0;
    });

    cout << "Count of even numbers: " << evens << endl;
    return 0;
}
```

### Output
Count of even numbers: 3

## 45. What happens if you insert a duplicate key in std::set or std::map? How do you detect insertion success?

Both `std::set` and `std::map` store only unique keys. If you attempt to insert a duplicate key:

- The insertion is ignored; the existing element is not modified.
- The `insert()` method returns a `std::pair<iterator, bool>`, where the `bool` value is `true` if the insertion succeeded, and `false` if the key already existed.

*(Note: To allow duplicate keys, use `std::multiset` or `std::multimap`.)*

### Code Example

```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> uniqueNumbers;

    // First insertion
    auto result1 = uniqueNumbers.insert(10);
    cout << "First insert of 10 success: " << (result1.second ? "True" : "False") << endl;

    // Second insertion (Duplicate)
    auto result2 = uniqueNumbers.insert(10);
    cout << "Second insert of 10 success: " << (result2.second ? "True" : "False") << endl;

    return 0;
}
```

### Output
First insert of 10 success: True
Second insert of 10 success: False

## 46. Define inline function. Can we have a recursive inline function in C++?

An **inline function** is a compiler optimization technique. When a function is declared inline, the compiler replaces calls to that function with its actual body code, eliminating the performance overhead of function calls (such as pushing arguments onto the stack and saving states).

### Can an inline function be recursive?

No, a recursive function cannot be inlined at compilation time because the depth of recursion depends on runtime conditions and is unknown at compile time. 
While you can add the `inline` keyword to a recursive function, the compiler treats `inline` as a suggestion and will ignore it, compiling it as a regular function call instead.

### Code Example

```cpp
#include <iostream>
using namespace std;

inline int square(int x) {
    return x * x;
}

int main() {
    cout << "Square of 5: " << square(5) << endl;
    return 0;
}
```

### Output
Square of 5: 25

## 47. What is an abstract class and when do you use it?

An **Abstract Class** is a class designed to act as a base interface and cannot be instantiated. It must contain at least one **pure virtual function** (declared with `= 0`). Derived classes must override all pure virtual functions to become instantiable.

### When to Use:

- To define a generic API interface that must be implemented by subclasses.
- To achieve runtime polymorphism by managing subclasses via base pointers.
- To share implementation code while leaving specific methods abstract.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Abstract Class
class Device {
public:
    virtual void turnOn() = 0; // Pure Virtual Function
    void status() { cout << "Device ready." << endl; } // Common method
};

class Laptop : public Device {
public:
    void turnOn() override {
        cout << "Laptop booting up..." << endl;
    }
};

int main() {
    // Device dev; // Error: Cannot instantiate abstract class
    Device* devPtr = new Laptop();
    devPtr->turnOn();
    devPtr->status();
    delete devPtr;
    return 0;
}
```

### Output
Laptop booting up...
Device ready.

## 48. What are the static data members and static member functions?

### Static Data Members:

- A static data member belongs to the class itself, not to individual objects.
- Only one copy of the static member exists, shared among all instances.
- Must be defined and initialized outside the class declaration.

### Static Member Functions:

- Can be invoked using the class name directly without instantiating an object (`ClassName::Function()`).
- Can only access static variables or other static functions within the class.
- Do not have access to the `this` pointer (since they are not tied to an object).

### Code Example

```cpp
#include <iostream>
using namespace std;

class ScoreTracker {
private:
    static int totalGames; // Static data member declaration

public:
    ScoreTracker() { totalGames++; }

    // Static member function
    static int getTotalGames() {
        return totalGames;
    }
};

// Initializing the static data member outside the class
int ScoreTracker::totalGames = 0;

int main() {
    ScoreTracker match1;
    ScoreTracker match2;
    ScoreTracker match3;

    // Call static method using class name
    cout << "Total matches played: " << ScoreTracker::getTotalGames() << endl;
    return 0;
}
```

### Output
Total matches played: 3

## 49. How can standard I/O performance be optimized in C++ (Fast I/O)?

By default, C++ standard streams (`std::cin` and `std::cout`) are synchronized with the standard C library streams (`stdin` and `stdout`) after each input/output operation. While this synchronization allows mixing C and C++ style I/O functions (like `printf` and `std::cout`), it introduces substantial runtime overhead. In competitive programming or applications processing huge datasets, this delay can be problematic.

### Optimization Techniques:

1. **Disable Synchronization (`std::ios_base::sync_with_stdio(false);`):** This de-synchronizes C++ streams from C streams, allowing C++ streams to buffer operations much faster.
2. **Untie input/output (`std::cin.tie(nullptr);`):** By default, `cin` is "tied" to `cout`. This means `cout` is automatically flushed (written to screen) before any input is requested from `cin`. Untieing them prevents this automatic flushing, allowing continuous block reads and writes.
3. **Use `\n` instead of `std::endl`:** `std::endl` inserts a newline character *and* forces a flush of the stream buffer, which is slow. Using `\n` writes the newline without flushing the buffer.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    // Enable Fast I/O
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    // Prompting and printing values quickly
    int age = 25;
    cout << "User age: " << age << "\n";

    return 0;
}
```

### Output
User age: 25

## 50. What is RAII (Resource Acquisition Is Initialization)?

RAII is a central programming paradigm in C++ that binds the lifecycle of a resource (e.g., heap memory, file pointers, database handles, sockets, mutex locks) to the lifetime of a local stack object.

### Key Principles:

- **Acquisition in Constructor:** The resource is acquired when the stack object is created (constructed).
- **Release in Destructor:** The resource is automatically released when the stack object goes out of scope (destroyed), even if exceptions are thrown.
- **Automatic Lifetime Management:** Since C++ guarantees that the destructors of local stack variables are executed upon leaving their scope (including during stack unwinding due to exceptions), memory leaks and resource leaks are avoided.

### Code Example

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class FileHandler {
private:
    ofstream fileStream;

public:
    // Resource acquired in constructor
    FileHandler(const string& filename) {
        fileStream.open(filename);
        if (fileStream.is_open()) {
            cout << "File opened successfully." << endl;
        }
    }

    // Resource automatically released in destructor
    ~FileHandler() {
        if (fileStream.is_open()) {
            fileStream.close();
            cout << "File closed automatically by RAII." << endl;
        }
    }

    void writeData(const string& data) {
        if (fileStream.is_open()) {
            fileStream << data << "\n";
        }
    }
};

int main() {
    {
        FileHandler handler("example_log.txt");
        handler.writeData("Hello, RAII!");
    } // handler goes out of scope here; destructor runs and closes the file

    return 0;
}
```

### Output
File opened successfully.
File closed automatically by RAII.

# C++ Interview Questions - Expert Level

## 51. What is the main use of the keyword “Volatile”?

The `volatile` keyword is a type qualifier that tells the compiler that a variable's value can be changed by actions outside the control of the program at any moment (for example, by the operating system, a hardware interrupt signal, or another concurrent thread).

### Main Use Cases:

- **Interfacing with Hardware:** Used for memory-mapped I/O registers where hardware updates status values.
- **Signal Handlers:** Modifying flags inside signal handlers that are checked in the main execution loop.
- **Preventing Compiler Optimizations:** Prevents the compiler from optimizing out reads or writes to variables, forcing the compiler to load the value from memory every time it is referenced rather than keeping it cached in CPU registers.

*Note: `volatile` does not guarantee thread-safety or atomic operations in C++. For concurrency, `std::atomic` should be used instead.*

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    volatile int sensorValue = 100; // Informs compiler value can change unexpectedly

    cout << "Sensor Initial Value: " << sensorValue << endl;

    sensorValue = 200; // Accessing volatile variable
    cout << "Sensor Updated Value: " << sensorValue << endl;

    return 0;
}
```

### Output
Sensor Initial Value: 100
Sensor Updated Value: 200

## 52. Define storage class in C++ and name some

*(This question provides an advanced deep-dive into linkage, scope, and lifetime details, expanding on the concepts introduced in Q15.)*

A storage class specifier defines the storage duration, visibility (scope), and linkage (how it is seen by the linker across files) of a variable or function.

### Advanced Storage Classes:

- **`thread_local`:** Specifies that a variable has thread storage duration. Each thread has its own distinct copy of the variable, which is created when the thread starts and destroyed when the thread joins/exits.
- **`extern`:** Declares that a variable has external linkage and is defined in another source file. This allows global variables to be shared across multiple translation units.
- **`static`:**
- In a local scope, it retains the variable's value between function calls.
- In a global/namespace scope, it limits visibility to the current translation unit (internal linkage).

### Code Example

```cpp
#include <iostream>
#include <thread>
using namespace std;

// Each thread will have its own private instance of this variable
thread_local int threadScore = 0;

void incrementScore(int id) {
    threadScore += id;
    cout << "Thread " << id << " Score: " << threadScore << endl;
}

int main() {
    thread t1(incrementScore, 10);
    thread t2(incrementScore, 20);

    t1.join();
    t2.join();

    return 0;
}
```

### Output
Thread 10 Score: 10
Thread 20 Score: 20

## 53. What is a mutable storage class specifier? How can they be used?

The `mutable` specifier is used exclusively on non-static class data members. It allows that member to be modified even if the containing object is declared as `const`, or if the modification is made inside a `const` member function.

### When to Use:

- For caching or memoization (e.g., storing a computed hash or search result).
- For locking mutexes or updating access counters inside read-only getter methods.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Database {
private:
    string data;
    mutable int accessCount; // Can be modified in const methods

public:
    Database(string d) : data(d), accessCount(0) {}

    string getData() const { // Const member function
        accessCount++; // Permitted because accessCount is mutable
        return data;
    }

    int getAccessCount() const {
        return accessCount;
    }
};

int main() {
    const Database db("Secure Records"); // Const object
    cout << "Read: " << db.getData() << endl;
    cout << "Read: " << db.getData() << endl;
    cout << "Database Access Count: " << db.getAccessCount() << endl;
    return 0;
}
```

### Output
Read: Secure Records
Read: Secure Records
Database Access Count: 2

## 54. Define the Block scope variable.

A block scope variable (or local variable) is declared inside a block of code, delimited by curly braces `{ }`. It is visible and accessible only from its point of declaration to the end of that block.

### Properties:

- **Lifetime:** Automatically allocated on the stack when the block is entered, and deallocated when execution leaves the block.
- **Shadowing:** A block scope variable can shadow (hide) variables with the same name in an outer scope.

### Code Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10; // Function scope
    cout << "Outer x: " << x << endl;

    {
        int x = 20; // Block scope variable shadowing outer x
        int y = 30; // Visible only in this block
        cout << "Inner block x: " << x << endl;
        cout << "Inner block y: " << y << endl;
    } // y is destroyed here; outer x becomes accessible again

    cout << "Outer x after block: " << x << endl;
    // cout << y; // Compiler Error: y is not declared in this scope

    return 0;
}
```

### Output
Outer x: 10
Inner block x: 20
Inner block y: 30
Outer x after block: 10

## 55. What is the function of the keyword "Auto"?

Introduced in C++11, the `auto` keyword instructs the compiler to automatically deduce the data type of a declared variable from its initialization expression.

### Benefits:

- **Reduces Verbosity:** Eliminates long, complex type names, such as STL iterators or templates.
- **Compile-Time Type Deduction:** Deduces types during compilation, ensuring zero runtime overhead.
- **Function Return Type Deduction:** Allows functions to deduce their return types automatically.

### Code Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    auto number = 42;          // Deduces int
    auto message = "C++ auto"; // Deduces const char*
    auto pi = 3.14159;         // Deduces double

    vector<int> numbers = {10, 20, 30};

    // Auto simplifies iterator declarations
    cout << "Vector Elements: ";
    for (auto it = numbers.begin(); it != numbers.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```

### Output
Vector Elements: 10 20 30

## 56. Define namespace in C++.

A namespace is a declarative region that provides a scope for identifiers (names of variables, functions, classes, etc.) to prevent naming collisions.

### Key points:

- Prevents collisions when combining multiple third-party libraries.
- Accessed using the scope resolution operator (`::`) or importing via `using namespace`.
- Can be nested inside other namespaces.
- Standard C++ library components are defined inside the `std` namespace.

### Code Example

```cpp
#include <iostream>
using namespace std;

namespace LibraryA {
    void display() {
        cout << "Display function from LibraryA" << endl;
    }
}

namespace LibraryB {
    void display() {
        cout << "Display function from LibraryB" << endl;
    }
}

int main() {
    LibraryA::display();
    LibraryB::display();
    return 0;
}
```

### Output
Display function from LibraryA
Display function from LibraryB

## 57. When is void return type used?

The `void` keyword is used as a function return type to indicate that the function does not return any value to the caller. 

### Characteristics:

- The function executes its statements and exits when it reaches the end of the block or a parameterless `return;` statement.
- Cannot be used to assign values to variables (e.g., `int x = myVoidFunc();` is a compiler error).
- Also used as a parameter list specifier `int func(void)` in C (and C++) to denote that a function accepts zero arguments.

### Code Example

```cpp
#include <iostream>
using namespace std;

// Function returns no value
void printLog(string message) {
    if (message.empty()) {
        return; // Exit early without returning a value
    }
    cout << "LOG: " << message << endl;
}

int main() {
    printLog("Process started successfully.");
    printLog(""); // Exits early silently
    return 0;
}
```

### Output
LOG: Process started successfully.

## 58. What is the difference between shallow copy and deep copy?

When copying objects that manage dynamic resource pointers:

| Aspect | Shallow Copy | Deep Copy |
| --- | --- | --- |
| **Mechanism** | Copies member values, including raw pointer addresses directly. | Copies values, allocates separate memory for pointers, and copies the actual contents. |
| **Data Sharing** | The original and copied objects share the same memory location/resource. | The original and copied objects have independent resources in memory. |
| **Destruction Hazard** | Leads to **double-free errors** when both objects go out of scope and delete the same pointer. | Safe to destroy; objects manage their own lifetimes. |
| **Default behavior** | Default compiler copy constructor performs a shallow copy. | Must be custom-implemented by overriding the copy constructor and copy assignment operator. |

### Code Example

```cpp
#include <iostream>
using namespace std;

class Deep {
public:
    int* ptr;
    Deep(int val) {
        ptr = new int(val);
    }

    // Deep copy constructor implementation
    Deep(const Deep& source) {
        ptr = new int(*source.ptr); // Allocates new memory
    }

    ~Deep() {
        delete ptr;
    }
};

int main() {
    Deep obj1(10);
    Deep obj2 = obj1; // Deep copy called

    cout << "Original ptr value: " << *obj1.ptr << " at address: " << obj1.ptr << endl;
    cout << "Copied ptr value: " << *obj2.ptr << " at address: " << obj2.ptr << endl;

    return 0;
}
```

### Output
Original ptr value: 10 at address: 0x
Copied ptr value: 10 at address: 0x

## 59. Can we call a virtual function from a constructor?

Yes, a virtual function can be called from a constructor, but it will **not** behave polymorphically as expected. 

### Why:

- During base class constructor execution, the derived class portion of the object has not yet been built.
- The virtual table (`vptr`) points to the class currently being constructed (the base class).
- Therefore, the compiler resolves the virtual function call to the static class constructor being run (the base class version), rather than the derived class's overridden method.

### Code Example

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    Base() {
        cout << "Base Constructor calling virtual function:" << endl;
        display(); // Resolves to Base::display(), not Derived::display()
    }

    virtual void display() {
        cout << " -> Base::display() called" << endl;
    }
};

class Derived : public Base {
public:
    Derived() {}
    void display() override {
        cout << " -> Derived::display() called" << endl;
    }
};

int main() {
    Derived d;
    return 0;
}
```

### Output
Base Constructor calling virtual function:
 -> Base::display() called

## 60. What are void pointers?

A **void pointer** (`void*`) is a generic pointer that has no associated data type. It can point to an address of any data type in memory.

### Constraints:

- Cannot be dereferenced directly because the compiler does not know the size of the underlying type.
- Must be explicitly typecast to another pointer type before dereferencing.
- Pointer arithmetic cannot be performed on a `void*` directly.

### Code Example

```cpp
#include <iostream>
using namespace std;

void printValue(void* ptr, char type) {
    if (type == 'i') {
        // Cast void* to int* before dereferencing
        cout << "Integer value: " << *(static_cast<int*>(ptr)) << endl;
    } else if (type == 'c') {
        // Cast void* to char* before dereferencing
        cout << "Character value: " << *(static_cast<char*>(ptr)) << endl;
    }
}

int main() {
    int num = 42;
    char letter = 'Z';

    printValue(&num, 'i');
    printValue(&letter, 'c');

    return 0;
}
```

### Output
Integer value: 42
Character value: Z

## 61. What is the difference between std::unique_ptr, std::shared_ptr, and std::weak_ptr?

C++11 introduced smart pointers in the `<memory>` header to automate memory management, adhering to RAII principles. They wrap raw pointers and guarantee automatic resource cleanup, preventing memory leaks.

| Smart Pointer | Ownership Model | Reference Counter | Key Use Case |
| --- | --- | --- | --- |
| `std::unique_ptr` | **Exclusive ownership**: Only one pointer can own the resource. Cannot be copied, only moved. | None | Default choice for single-owner object lifecycles. |
| `std::shared_ptr` | **Shared ownership**: Multiple pointers can point to the same resource. Uses reference counting. | Yes (managed in control block) | Used when resource lifetime is co-owned by multiple entities. |
| `std::weak_ptr` | **Non-owning observer**: Holds a weak reference to a resource managed by `std::shared_ptr`. | No (does not increment ref count) | Used to break cyclic dependencies (circular references) that cause memory leaks. |

### Code Example

```cpp
#include <iostream>
#include <memory>
using namespace std;

class Widget {
public:
    Widget() { cout << "Widget Constructor" << endl; }
    ~Widget() { cout << "Widget Destructor" << endl; }
    void greet() { cout << "Hello from Widget!" << endl; }
};

int main() {
    cout << "--- unique_ptr Example ---" << endl;
    {
        unique_ptr<Widget> uptr = make_unique<Widget>();
        uptr->greet();
        // unique_ptr<Widget> uptrCopy = uptr; // Error: Copy not allowed
        unique_ptr<Widget> uptrMoved = move(uptr); // Move is allowed
    } // Widget automatically destroyed here

    cout << "--- shared_ptr & weak_ptr Example ---" << endl;
    shared_ptr<Widget> sptr1 = make_shared<Widget>();
    cout << "Use count: " << sptr1.use_count() << endl;
    {
        shared_ptr<Widget> sptr2 = sptr1; // Shared ownership
        cout << "Use count (after copy): " << sptr1.use_count() << endl;

        weak_ptr<Widget> wptr = sptr1; // Weak reference
        if (auto locked = wptr.lock()) { // Safely convert to shared_ptr to use
            locked->greet();
        }
    }
    cout << "Use count (after scope exit): " << sptr1.use_count() << endl;

    return 0;
} // Widget automatically destroyed when sptr1 goes out of scope
```

### Output
--- unique_ptr Example ---
Widget Constructor
Hello from Widget!
Widget Destructor
--- shared_ptr & weak_ptr Example ---
Widget Constructor
Use count: 1
Use count (after copy): 2
Hello from Widget!
Use count (after scope exit): 1
Widget Destructor

## 62. Compare std::move and std::forward in modern C++.

Both `std::move` and `std::forward` are utility functions in the C++ Standard Library (`<utility>`) that perform compile-time type casts. However, they serve very different purposes in move semantics:

- **`std::move`:**
- Unconditionally casts its argument to an rvalue reference (`T&&`).
- Used to signal that an object's resources can be "moved" (stolen) to avoid expensive copy operations.
- **`std::forward`:**
- Conditionally casts its argument to an rvalue reference *only* if the original parameter was initialized with an rvalue.
- Used in templates for **Perfect Forwarding**, ensuring that arguments retain their original value category (lvalue vs rvalue) when passed to another function.

### Code Example

```cpp
#include <iostream>
#include <utility>
using namespace std;

class Resource {
public:
    Resource() {}
    Resource(const Resource&) { cout << "Copy Constructor" << endl; }
    Resource(Resource&&) noexcept { cout << "Move Constructor" << endl; }
};

// Target overloaded functions
void process(const Resource& r) { cout << "Processing Lvalue" << endl; }
void process(Resource&& r) { cout << "Processing Rvalue" << endl; }

// Perfect forwarding wrapper
template <typename T>
void relay(T&& arg) {
    process(forward<T>(arg)); // Preserves value category of arg
}

int main() {
    Resource res;

    cout << "--- Using std::move ---" << endl;
    Resource movedRes = move(res); // Force move constructor

    cout << "--- Perfect Forwarding ---" << endl;
    relay(res);        // Lvalue passed -> invokes process(const Resource&)
    relay(move(res));  // Rvalue passed -> invokes process(Resource&&)

    return 0;
}
```

### Output
--- Using std::move ---
Move Constructor
--- Perfect Forwarding ---
Processing Lvalue
Processing Rvalue

# Summary

This comprehensive C++ interview guide covers critical topics ranging from freshers' core syntax and object-oriented programming fundamentals to expert-level memory management, pointers, and runtime behavior. Key takeaways emphasize the importance of distinguishing references from pointers, understanding compile-time versus runtime polymorphism via virtual tables, and mastering advanced memory features like virtual destructors, mutable accessors, and shallow versus deep copies. By analyzing the provided code examples and exact program execution outputs, candidates can gain a thorough technical command of low-level resource management and object design patterns, building the practical confidence required to pass rigorous engineering interviews at top-tier software companies.




