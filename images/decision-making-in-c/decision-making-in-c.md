# Decision Making in C++

Decision-making is a fundamental concept in programming that allows a program to choose different actions based on specific conditions. In C++, decision-making statements control the flow of execution by evaluating conditions and executing particular blocks of code depending on whether those conditions are true or false.

The primary decision-making constructs available in C++ are:

1. `if` Statement
2. `if-else` Statement
3. `if-else-if` Ladder
4. Nested `if-else`
5. `switch` Statement
6. Ternary Operator (`?:`)

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012399460-ChatGPT_Image_Jun_9%2C_2026%2C_07_09_11_PM.png)

## 1. if Statement

The `if` statement is the simplest decision-making construct in C++. It executes a block of code only when the specified condition evaluates to `true`.

**Flowchart:**

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012481470-53f5e2d4-8047-438a-a66b-063bb88d3708.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int marks = 85;

    if (marks >= 50) {
        cout << "Pass";
    }

    return 0;
}
```

### Output
Pass

### 

### Note

If the `if` block contains only one statement, curly braces `{}` can be omitted.

```cpp
if (marks >= 50)
    cout << "Pass";
```

---

## 2. if-else Statement

The `if-else` statement allows a program to choose between two alternative blocks of code. If the condition is true, the `if` block executes; otherwise, the `else` block executes.

**Flowchart:**

### ![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012555309-cd7a7c21-7741-4f2d-8267-07938b455ad1.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int number = -5;

    if (number >= 0) {
        cout << "Non-negative number";
    }
    else {
        cout << "Negative number";
    }

    return 0;
}
```

### Output

```text
Negative number
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## 3. if-else-if Ladder

The `if-else-if` ladder is used when multiple conditions need to be evaluated. Conditions are checked sequentially, and the first condition that evaluates to true has its corresponding block executed.

**Flowchart:**

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012711148-f702f5c8-11bd-455d-9125-4f2b89ba0c0e.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int score = 78;

    if (score >= 90) {
        cout << "Grade A";
    }
    else if (score >= 75) {
        cout << "Grade B";
    }
    else if (score >= 50) {
        cout << "Grade C";
    }
    else {
        cout << "Grade F";
    }

    return 0;
}
```

### Output

```text
Grade B
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## 4. Nested if-else

A nested `if-else` statement contains one `if` statement inside another. It is useful when multiple levels of conditions need to be checked.

**Flowchart:**

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012736897-f702f5c8-11bd-455d-9125-4f2b89ba0c0e.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int num = 24;

    if (num > 0) {

        if (num % 2 == 0) {
            cout << "Positive Even Number";
        }
        else {
            cout << "Positive Odd Number";
        }
    }
    else {
        cout << "Non-positive Number";
    }

    return 0;
}
```

### Output

```text
Positive Even Number
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## 5. switch Statement

The `switch` statement is used to select one block of code from multiple alternatives based on the value of a variable or expression. It often provides a cleaner alternative to lengthy `if-else-if` ladders.

**Flowchart:**

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-c/1781012805271-5e2b5985-9164-44e9-b778-e3d17bcc171c.png)

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int day = 3;

    switch (day) {

    case 1:
        cout << "Monday";
        break;

    case 2:
        cout << "Tuesday";
        break;

    case 3:
        cout << "Wednesday";
        break;

    default:
        cout << "Invalid Day";
    }

    return 0;
}
```

### Output

```text
Wednesday
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

### Important Notes

- The `break` statement prevents execution from continuing into the next case.
- The `default` block executes when no case matches the expression value.
- Case labels must contain constant values.

---

## 6. Ternary Operator (`?:`)

The ternary operator is a compact alternative to a simple `if-else` statement. It evaluates a condition and returns one of two expressions depending on the result.

### Syntax

```cpp
condition ? expression1 : expression2;
```

- If the condition is true, `expression1` is evaluated.
- If the condition is false, `expression2` is evaluated.

### Example Code

```cpp
#include <iostream>
using namespace std;

int main() {

    int a = 15, b = 25;

    int larger = (a > b) ? a : b;

    cout << larger;

    return 0;
}
```

### Output

```text
25
```

**Time Complexity:** O(1)

**Space Complexity:** O(1)

---

## Summary

Decision-making statements allow a C++ program to execute different blocks of code based on conditions. These constructs help create dynamic and intelligent programs that can respond to varying inputs and situations.

The major decision-making constructs in C++ are:

- `if` Statement
- `if-else` Statement
- `if-else-if` Ladder
- Nested `if-else`
- `switch` Statement
- Ternary Operator (`?:`)

Mastering these statements is essential for controlling program flow and implementing real-world logic in C++ applications.

<approaches>
## Approach




</approaches>




