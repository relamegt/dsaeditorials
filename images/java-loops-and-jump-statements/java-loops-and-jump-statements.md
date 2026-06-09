# Java Loops and Jump Statements

In Java, loops and jump statements are used to control how a program executes. Loops help repeat a block of code, while jump statements help skip iterations, stop loops, or return from methods.

Loops are useful when a task needs to run multiple times, and jump statements are useful when the normal flow needs to change based on a condition.

## Java Loops

Java provides four main looping options:

- `for` loop
- `while` loop
- `do-while` loop
- enhanced `for` loop (for-each)

## 1. for Loop

![for loop](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-loops-and-jump-statements/1781014983907-for_loop.png)

A `for` loop is used when the number of iterations is known in advance. It keeps initialization, condition, and update in a single line.

### Syntax

```java
for (initialization; condition; update) {
    // code to be executed
}
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i <= 5; i++) {
            System.out.print(i + " ");
        }
    }
}
```

### Output
0 1 2 3 4 5

## 2. while Loop

![while loop](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-loops-and-jump-statements/1781015046388-while_loop.png)

A `while` loop checks the condition before running the loop body, so it is an entry-controlled loop. It is useful when the number of iterations is not fixed beforehand.

### Syntax

```java
while (condition) {
    // code to be executed
}
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        int i = 0;
        while (i <= 5) {
            System.out.print(i + " ");
            i++;
        }
    }
}
```

### Output
0 1 2 3 4 5

## 3. do-while Loop

![do-while](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-loops-and-jump-statements/1781015136184-do-while_loop.png)

A `do-while` loop executes the loop body first and checks the condition afterward, so it always runs at least once. This makes it an exit-controlled loop.

### Syntax

```java
do {
    // code to be executed
} while (condition);
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        int i = 0;
        do {
            System.out.print(i + " ");
            i++;
        } while (i <= 5);
    }
}
```

### Output
0 1 2 3 4 5

## 4. Enhanced for Loop (for-each)

![for-each](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-loops-and-jump-statements/1781015163756-for_each_loop.png)

The enhanced `for` loop, also called the for-each loop, is used to iterate through arrays or collections one item at a time.

### Syntax

```java
for (dataType variable : arrayOrCollection) {
    // code to be executed
}
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"Akash", "Mohit", "Abhiram", "AlphaKnowledge"};

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

### Output
Akash
Mohit
Abhiram
AlphaKnowledge

## Loop Summary

| Loop Type | When to Use | Condition Check | Runs At Least Once |
| --- | --- | --- | --- |
| `for` | When iterations are known | Before loop body | No |
| `while` | When condition is checked first | Before loop body | No |
| `do-while` | When code must run at least once | After loop body | Yes |
| `for-each` | When iterating arrays or collections | Internally handled | No |

## Common Loop Mistakes

Some common loop mistakes include infinite loops, off-by-one errors, changing the loop variable unexpectedly inside the loop, and writing an empty loop body with no useful work. These problems can affect readability, correctness, and performance.

### Infinite Loop Example

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i--) {
            System.out.println("This loop will run forever");
        }
    }
}
```

### Off-by-One Example

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i <= 5; i++) {
            System.out.print(i + " ");
        }
    }
}
```

### Output
0 1 2 3 4 5

The loop above runs 6 times because it includes both 0 and 5.

## Java Jump Statements

Jump statements are used to change the normal flow of execution. In Java, the common jump statements are `break`, `continue`, and `return`.

![jump statements](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-loops-and-jump-statements/1781015211072-jump_stmts.png)

## 1. continue Statement

The `continue` statement skips the current iteration of a loop and moves directly to the next iteration. In a `for` loop, control jumps to the update statement; in `while` and `do-while`, control jumps to the condition check.

### Example

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            if (i == 2) {
                continue;
            }
            System.out.println(i);
        }
    }
}
```

### Output
0
1
3
4

## 2. break Statement

The `break` statement immediately terminates a loop or switch statement and transfers control to the next statement after it. It is commonly used when a specific condition is met and the remaining iterations are not needed.

### Example

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 4) {
                break;
            }
            System.out.println(i);
        }
    }
}
```

### Output
0
1
2
3

## 3. return Statement

The `return` statement exits a method and can optionally send a value back to the calling code. Any statement written after `return` in the same execution path becomes unreachable.

### Example

```java
public class Main {
    public static int calculateSum(int num1, int num2) {
        int sum = num1 + num2;
        return sum;
    }

    public static void main(String[] args) {
        int result = calculateSum(10, 20);
        System.out.println("Result: " + result);
    }
}
```

### Output
Result: 30

## break vs continue vs return

| Statement | Purpose | Used In |
| --- | --- | --- |
| `break` | Stops the loop or switch completely | Loops, `switch` |
| `continue` | Skips the current iteration and continues | Loops |
| `return` | Exits from a method, with or without a value | Methods |

## Combined Example

```java
public class Main {
    public static int findFirstEven(int[] numbers) {
        for (int number : numbers) {
            if (number < 0) {
                continue;
            }

            if (number % 2 == 0) {
                return number;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] values = {-3, -1, 5, 7, 8, 10};

        for (int value : values) {
            if (value == 10) {
                break;
            }
            System.out.println("Checking: " + value);
        }

        int result = findFirstEven(values);
        System.out.println("First even number: " + result);
    }
}
```

### Output
Checking: -3
Checking: -1
Checking: 5
Checking: 7
Checking: 8
First even number: 8

## Quick Notes

- Use `for` when the number of iterations is known.
- Use `while` when the loop should continue only while a condition remains true.
- Use `do-while` when the loop body must execute at least once.
- Use `continue` to skip a specific round of the loop.
- Use `break` to stop the loop early.
- Use `return` to exit from a method and pass back a result.

## Final Note

Loops repeat work, and jump statements adjust control flow when needed. Together, they form an important part of Java program structure and are widely used in conditions, arrays, collections, and method logic.



###
