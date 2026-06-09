# Data Types in C++

Data types specify the category of values that a variable can hold within a program.

- In C++, the data type assigned to a variable determines how the compiler stores and interprets its value in memory.
- Different data types occupy different amounts of memory, depending on the nature and size of the data they are designed to represent.

![Data Types in C++](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/data-types-in-c/1780987108089-9.png)

The example below illustrates how the **integer data type (`int`)** is declared and used in C++. The `int` type is commonly employed to store numerical values that do not contain fractional components.

```cpp
#include <iostream>
using namespace std;

int main() {

    // Declaring and initializing an integer variable
    int age = 20;

    cout << "Age: " << age;

    return 0;
}
```

### Output
Age: 20

# Time Complexity
O(1)

# Space Complexity
O(1)

Let us now examine the primitive data types available in C++ and understand how they are used in programs.

### **Character Data Type (`char`)**

The `char` data type is designed to store a single character, such as a letter, digit, or symbol. It is declared using the keyword `char` and typically occupies **1 byte** of memory. Character values are written inside **single quotation marks** (`' '`).

Internally, a character is stored as a numeric code based on a character encoding scheme such as ASCII. Because a `char` usually uses 1 byte, it can represent up to 256 unique character values, depending on the implementation.

**Examples:**

- `'A'`
- `'b'`
- `'7'`
- `'@'`

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Character variable
    char grade = 'B';

    cout << "Grade: " << grade;

    return 0;
}
```

### Output
Grade: B

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Integer Data Type (`int`)**

The `int` data type is used to store whole numbers that do not contain any fractional or decimal part. In C++, integers are declared using the `int` keyword. On most modern systems, an `int` typically occupies **4 bytes** of memory, although the exact size may vary depending on the compiler and platform.

Integer values can be represented in different number systems, including **decimal (base 10)**, **binary (base 2)**, **octal (base 8)**, and **hexadecimal (base 16)**. A standard 4-byte integer generally supports values ranging from **−2,147,483,648** to **2,147,483,647**.

**Examples of integer values:**

- `25`
- `-100`
- `0`
- `0b1010` (binary)
- `012` (octal)
- `0xA` (hexadecimal)

The example below illustrates the declaration and usage of an **integer variable (`int`)** in C++. The program stores an integer value and prints it to the console.

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Creating an integer variable
    int num = 100;
    cout << num << endl;

    // Using binary base value
    num = 0b1100100;
    cout << num;

    return 0;
}
```

### Output
100
100

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Boolean Data Type (`bool`)**

The `bool` data type is used to represent logical values in C++. A boolean variable can store only one of two possible states: **`true`** or **`false`**. It is declared using the `bool` keyword and typically occupies **1 byte** of memory on most systems.

Boolean values are commonly used in decision-making statements, comparisons, loops, and conditional expressions where a result must evaluate to either true or false.

**Examples of boolean values:**

- `true`
- `false`

In C++, `true` is generally represented by the value **1**, while `false` is represented by **0** when displayed as numeric output.

The following example demonstrates the use of the **boolean (**`**bool**`**) data type** in C++. A boolean variable named `isStudent` is declared and assigned the value `false`. The program then displays the stored value using the `cout` statement.

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Creating a boolean variable
    bool isStudent = false;

    cout << isStudent;

    return 0;
}
```

### Output
0

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Floating Point Data Type (`float`)**

The `float` data type is used to store real numbers that contain fractional or decimal values. It is declared using the `float` keyword and typically occupies **4 bytes** of memory on most modern systems. A floating-point variable can represent a wide range of values, approximately from **1.2 × 10⁻³⁸** to **3.4 × 10³⁸**.

The `float` type is commonly used in applications that require decimal precision, such as scientific calculations, measurements, and financial computations where extremely high precision is not required.

**Examples of floating-point values:**

- `3.14`
- `25.75`
- `-0.5`
- `100.0`

The following example demonstrates how the **`float` data type** can be used to store and display decimal values in C++.

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Floating point variable
    float price = 49.99f;

    cout << price;

    return 0;
}
```

### Output
49.99

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Double Data Type (`double`)**

The `double` data type is used to store decimal numbers that require greater precision than the `float` data type. It is declared using the `double` keyword and typically occupies **8 bytes** of memory on most modern 64-bit systems.

Because of its larger size, a `double` can represent a much wider range of values, approximately from **1.7 × 10⁻³⁰⁸** to **1.7 × 10³⁰⁸**. It is commonly used in scientific computations, engineering applications, and financial calculations where higher accuracy is important.

**Examples of double values:**

- `3.1415926535`
- `12345.6789`
- `-0.000125`
- `2.5e10`

The following example demonstrates how the **`double` data type** can be used to store and display high-precision decimal values in C++.

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Double precision floating-point variable
    double pi = 3.14159265358979;

    cout << pi;

    return 0;
}
```

### Output
3.14159

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Void Data Type (`void`)**

The `void` data type is used to indicate the absence of a value or data. Unlike other primitive data types, variables of type `void` cannot be created because `void` does not represent any storage type. It is commonly used with functions that do not return a value and with generic pointers (`void*`) that can reference objects of different data types.

The `void` keyword helps programmers clearly specify when a function is intended to perform an action without producing a return value.

### **Type Safety in C++**

C++ is a strongly typed programming language, which means every variable must be declared with a specific data type before it can be used. Once a variable is declared, its data type remains fixed throughout its lifetime, although the value stored in it can change.

C++ supports both implicit and explicit type conversions, allowing values of one type to be converted to another when necessary. However, such conversions may sometimes result in loss of precision or information if the destination type cannot fully represent the original value.

For example, when an integer value is assigned to a boolean variable, C++ automatically performs an implicit conversion: a value of `0` becomes `false`, while any non-zero value is converted to `true`.

The following example demonstrates **implicit type conversion** in C++. A floating-point value is assigned to a boolean variable. Since the value is non-zero, C++ automatically converts it to `true`, which is displayed as `1` when printed.

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Assigning a floating-point value to a boolean variable
    bool isActive = 5.75f;

    cout << isActive;

    return 0;
}
```

### Output
1

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Data Type Conversion**

Data type conversion is the process of transforming a value from one data type to another compatible data type. This feature enables different types of data to interact within the same program and helps improve flexibility when performing calculations, comparisons, or data processing tasks.

In C++, conversions can occur automatically through **implicit conversion** or be performed manually using **explicit conversion (casting)**. Proper use of data type conversion ensures that values are interpreted correctly while minimizing the risk of data loss or unexpected results.

The following example demonstrates **explicit type conversion (type casting)** in C++. A character value is converted into its corresponding ASCII integer value and then displayed.

```cpp
#include <iostream>
using namespace std;

int main()
{
    char ch = 'A';

    // Converting character to integer
    int asciiValue = (int)ch;

    cout << asciiValue;

    return 0;
}
```

### Output
65

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Size of Data Types in C++**

The amount of memory occupied by a data type in C++ is not fixed across all systems. The actual size may vary depending on factors such as the computer architecture (32-bit or 64-bit), the compiler being used, and the underlying system implementation.

As a result, the same data type may consume different amounts of memory on different platforms. These differences can affect the range of values that a variable can store.

C++ provides the **`sizeof`** operator, which can be used to determine the memory size of a data type or variable during program execution. Understanding data type sizes is important for efficient memory usage and for selecting appropriate data types in applications.

The following example uses the **`sizeof`** operator to determine and display the memory occupied by various data types in C++.

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Size of int: " << sizeof(int) << " bytes" << endl;
    cout << "Size of char: " << sizeof(char) << " byte" << endl;
    cout << "Size of float: " << sizeof(float) << " bytes" << endl;
    cout << "Size of double: " << sizeof(double) << " bytes";

    return 0;
}
```

### Output
Size of int: 4 bytes
Size of char: 1 byte
Size of float: 4 bytes
Size of double: 8 bytes

# Time Complexity
O(1)

# Space Complexity
O(1)

### **Data Type Modifiers**

Data type modifiers are special keywords in C++ that alter the size, range, or behavior of fundamental data types. They are placed before a primitive data type to extend its storage capacity or modify the range of values it can represent.

The four commonly used data type modifiers in C++ are:

- `short`
- `long`
- `signed`
- `unsigned`

These modifiers allow programmers to choose data types that best suit the requirements of a program. For example, applying the `long` modifier to an integer type generally increases its storage capacity, enabling it to store larger values than a regular `int`.

Some commonly used modified data types include:

- `long int`
- `long long int`
- `unsigned int`
- `short int`
- `long double`

Using appropriate modifiers can improve memory efficiency and ensure that variables can accommodate the required range of values.

The following example demonstrates how data type modifiers can be used to change the size and range of primitive data types in C++.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num1 = 100;
    long int num2 = 1000000;

    cout << "Size of int: " << sizeof(num1) << " bytes" << endl;
    cout << "Size of long int: " << sizeof(num2) << " bytes";

    return 0;
}
```

### Output
Size of int: 4 bytes
Size of long int: 8 bytes

# Time Complexity
O(1)

# Space Complexity
O(1)




