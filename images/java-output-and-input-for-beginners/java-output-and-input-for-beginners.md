# Java Output and Input for Beginners

In Java, one of the first things you learn is how to show output on the screen and how to take input from the user. For output, Java uses `System.out.println()`. For input, beginners often use the `Scanner` class.

## 1. Display Output in Java

`System.out.println()` is used to print something on the screen. After printing, it moves to the next line.

### Example

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.out.println("Welcome to Java.");
    }
}
```

### Output
Hello, World!
Welcome to Java.

### **2. What** `System.out.println()` **Means**

This statement has three parts:

- `System` is a built-in Java class
- `out` is the standard output stream
- `println()` prints the value and then goes to a new line

### Syntax

```java
System.out.println(value);
```

You can print:

- Text
- Numbers
- Variables
- Results of expressions

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;

        System.out.println("A = " + a);
        System.out.println("B = " + b);
        System.out.println("Sum = " + (a + b));
    }
}
```

### Output
A = 10
B = 20
Sum = 30

### **3.** `print()` **vs** `println()`

- `print()` prints on the same line
- `println()` prints on a new line

### Example

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("Java ");
        System.out.print("is ");
        System.out.println("easy.");
        System.out.println("This is the next line.");
    }
}
```

### Output
Java is easy.
This is the next line.

### **4. Take Input in Java Using Scanner**

To take input from the keyboard, Java commonly uses the `Scanner` class.

### Import Scanner

```java
import java.util.Scanner;
```

### Create Scanner Object

```java
Scanner sc = new Scanner(System.in);
```

`System.in` means the program will read input from the keyboard.

## 5. Steps to Use Scanner

1. Import `Scanner`
2. Create a Scanner object
3. Read input using Scanner methods
4. Close the Scanner

## 6. Example: Read One Number

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int num = sc.nextInt();

        System.out.println("You entered: " + num);

        sc.close();
    }
}
```

## 7. Example: Read Two Numbers and Add Them

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter first number: ");
        int a = sc.nextInt();

        System.out.print("Enter second number: ");
        int b = sc.nextInt();

        System.out.println("Sum = " + (a + b));

        sc.close();
    }
}
```

## 8. Example: Read Text Input

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.println("Hello, " + name);

        sc.close();
    }
}
```

## 9. Common Scanner Methods

- `nextInt()` for integer values
- `nextDouble()` for decimal values
- `next()` for one word
- `nextLine()` for a full line of text
- `nextFloat()` for float values
- `nextLong()` for long values

## 10. `next()` vs `nextLine()`

- `next()` reads only one word
- `nextLine()` reads the full line

### Example

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter full name: ");
        String fullName = sc.nextLine();

        System.out.println("Your name is: " + fullName);

        sc.close();
    }
}
```

## 11. Common Beginner Issue

Sometimes `nextInt()` and `nextLine()` do not work together as expected because of leftover newline characters. A simple way for beginners is to use `nextLine()` and convert the value when needed.

### Example

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter age: ");
        int age = Integer.parseInt(sc.nextLine());

        System.out.println("Your age is: " + age);

        sc.close();
    }
}
```

## 12. Final Note

In simple words:

- Use `System.out.println()` to show output
- Use `Scanner` to take input from the user

These are two of the most important basics in Java, and almost every beginner program starts with them.



###
