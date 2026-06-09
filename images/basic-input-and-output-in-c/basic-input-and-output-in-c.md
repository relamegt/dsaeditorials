# Basic Input and Output in C++

Input and output operations enable a program to communicate with users and external devices. In C++, these operations are performed using **streams**, which represent the flow of data between a program and input/output devices.

A stream can be viewed as a sequence of characters or bytes transferred from one location to another.

- **Input Stream:** Transfers data from an input device (such as a keyboard) to the program's memory.
- **Output Stream:** Transfers data from the program's memory to an output device (such as a monitor).

The stream functionality in C++ is provided through the  header file, which contains several predefined stream objects for handling standard input, output, and error messages.

The most commonly used stream objects are:

- **cin** – Used for receiving input from the user.
- **cout** – Used for displaying output on the screen.
- **cerr** – Used for displaying error messages immediately.
- **clog** – Used for logging messages through a buffered stream.

---

## Standard Output Stream (`cout`)

The `cout` object is an instance of the `ostream` class and is used to display output on the screen. Data is sent to the output stream using the **insertion operator (`<<`)**.

The following example demonstrates how to display text using `cout`.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Welcome to C++ Programming";
    return 0;
}
```

### Output

```text
Welcome to C++ Programming
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## Standard Input Stream (`cin`)

The `cin` object is an instance of the `istream` class and is used to receive input from the keyboard. Data entered by the user is read using the **extraction operator (`>>`)** and stored in variables.

The following example demonstrates how to read input from the user and display it back on the screen.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int marks;

    cin >> marks;

    cout << "Marks: " << marks;

    return 0;
}
```

### Input

```text
95
```

### Output

```text
Marks: 95
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## Unbuffered Standard Error Stream (`cerr`)

The `cerr` object is used to display error and warning messages. It belongs to the `ostream` class and operates as an **unbuffered output stream**, meaning messages are displayed immediately without waiting for a buffer to fill.

This behavior makes `cerr` particularly useful for reporting runtime errors and debugging information that should appear instantly.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    cerr << "Invalid input detected!";
    return 0;
}
```

### Output

```text
Invalid input detected!
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## Buffered Standard Logging Stream (`clog`)

The `clog` object is used for logging and diagnostic messages. Like `cerr`, it belongs to the `ostream` class, but unlike `cerr`, it is a **buffered stream**.

Messages written to `clog` are stored temporarily in a buffer and displayed when the buffer is flushed or becomes full. This makes `clog` suitable for logging information that does not need to appear immediately.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    clog << "Program started successfully.";
    return 0;
}
```

### Output

```text
Program started successfully.
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## Difference Between `cout`, `cerr`, and `clog`

| Stream | Purpose | Buffered |
| --- | --- | --- |
| cout | Standard output | Yes |
| cerr | Error and warning messages | No |
| clog | Logging and diagnostic messages | Yes |

While `cout` is primarily used for normal program output, `cerr` and `clog` are intended for reporting errors and logging information. The key distinction is that `cerr` displays messages immediately, whereas `clog` may delay output due to buffering.

<approaches>
## Approach




</approaches>




