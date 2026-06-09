# Java Keywords

In Java, **keywords** are special reserved words that already have a fixed meaning in the language. These words are understood by the compiler and are used to write Java programs correctly.

You cannot use a keyword as your own name for a variable, method, class, or object.

## What Is a Keyword?

A keyword is a word that Java keeps reserved for its own use.

These words help Java understand things like:

- data types
- conditions
- loops
- classes
- methods
- inheritance
- exception handling

### Simple Example

```java
public class Main {
    public static void main(String[] args) {
        int x = 10;

        if (x > 5) {
            System.out.println("x is greater than 5");
        } else {
            System.out.println("x is 5 or smaller");
        }
    }
}
```

In this example:

- `public`
- `class`
- `static`
- `void`
- `int`
- `if`
- `else`

are Java keywords.

## Why Keywords Are Important

Keywords are the basic building blocks of Java syntax. They tell Java what action to perform and how the program should behave.

For example:

- `int` means a whole number
- `if` checks a condition
- `class` creates a class
- `return` sends a value back from a method

## Rule: Keywords Cannot Be Used as Identifiers

You cannot use a keyword as a:

- variable name
- method name
- class name
- object name

### Wrong Example

```java
public class Main {
    public static void main(String[] args) {
        int class = 5;
    }
}
```

This is invalid because `class` is a keyword.

### Correct Example

```java
public class Main {
    public static void main(String[] args) {
        int marks = 5;
    }
}
```

## Java Keywords by Category

## Data Type Keywords

These keywords define the type of data a variable can store.

| Keyword | Meaning |
| --- | --- |
| byte | Stores a small whole number |
| short | Stores a short integer value |
| int | Stores a whole number |
| long | Stores a very large whole number |
| float | Stores a decimal number with less precision |
| double | Stores a decimal number with more precision |
| char | Stores a single character |
| boolean | Stores true or false |
| void | Shows that a method returns no value |

### Example

```java
int age = 20;
double price = 99.99;
char grade = 'A';
boolean isJavaFun = true;
```

## Control Flow Keywords

These keywords control the order in which code runs.

| Keyword | Meaning |
| --- | --- |
| if | Runs code if a condition is true |
| else | Runs code if the if condition is false |
| switch | Chooses one option from many |
| case | Defines one choice in a switch |
| default | Runs if no case matches |
| for | Repeats code a fixed number of times |
| while | Repeats code while a condition is true |
| do | Runs code once, then repeats if condition is true |
| break | Stops a loop or switch |
| continue | Skips the current loop step |
| return | Ends a method and may return a value |

### Example

```java
int age = 18;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

## Exception Handling Keywords

These keywords are used to manage errors in a program.

| Keyword | Meaning |
| --- | --- |
| try | Tests code that may cause an error |
| catch | Handles the error |
| finally | Runs whether an error happens or not |
| throw | Manually creates an exception |
| throws | Declares that a method may throw an exception |
| assert | Checks whether a condition is true during debugging |

### Example

```java
try {
    int result = 10 / 0;
} catch (Exception e) {
    System.out.println("Error happened");
}
```

## Object-Oriented Keywords

These keywords are used in classes, objects, inheritance, and interfaces.

| Keyword | Meaning |
| --- | --- |
| class | Creates a class |
| interface | Creates an interface |
| extends | Inherits from another class |
| implements | Uses an interface in a class |
| new | Creates an object |
| this | Refers to the current object |
| super | Refers to the parent class |
| abstract | Declares incomplete class or method |
| final | Prevents change, overriding, or inheritance |
| static | Belongs to the class, not object |
| enum | Creates a fixed set of constants |
| instanceof | Checks object type |
| record | Creates a simple data class |
| sealed | Restricts which classes can inherit |
| permits | Lists allowed subclasses of a sealed class |

### Example

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
}
```

Here, `class` and `extends` are keywords.

## Access Control Keywords

These keywords control where a class member can be used.

| Keyword | Meaning |
| --- | --- |
| public | Can be accessed from anywhere |
| private | Can be accessed only inside the same class |
| protected | Can be accessed in the same package and subclasses |

## Package Keywords

These are used to organize Java code.

| Keyword | Meaning |
| --- | --- |
| package | Groups related classes |
| import | Brings classes from another package |

### Example

```java
import java.util.Scanner;
```

## Multithreading Keywords

These are used when multiple tasks run at the same time.

| Keyword | Meaning |
| --- | --- |
| synchronized | Allows only one thread at a time to access code |
| volatile | Tells Java a variable may change unexpectedly |

## Memory and Native Code Keywords

These keywords handle serialization and native methods.

| Keyword | Meaning |
| --- | --- |
| transient | Skips a variable during serialization |
| native | Shows method is written in non-Java code |

## Utility Keyword

| Keyword | Meaning |
| --- | --- |
| strictfp | Makes floating-point calculations consistent across systems |

## Reserved but Not Commonly Used

These words are reserved in Java, but they are not used in normal Java programming.

| Keyword | Meaning |
| --- | --- |
| const | Reserved for future use |
| goto | Reserved for future use |

You still cannot use them as identifiers.

## Special Literals

These are not normal keywords, but they also cannot be used as names.

| Literal | Meaning |
| --- | --- |
| true | Boolean true value |
| false | Boolean false value |
| null | No object reference |

## Keywords vs Identifiers

| Feature | Keywords | Identifiers |
| --- | --- | --- |
| Meaning | Reserved words in Java | Names given by the programmer |
| Purpose | Define Java syntax | Identify variables, methods, classes, etc. |
| Can be used as variable names | No | Yes |
| Meaning decided by | Java language | Programmer |
| Examples | int, class, if | age, studentName, totalMarks |

## Commonly Used Java Keywords with Easy Meaning

| Keyword | Easy Meaning |
| --- | --- |
| int | whole number |
| double | decimal number |
| boolean | true or false |
| class | blueprint of object |
| public | open to all |
| private | only inside same class |
| static | belongs to class |
| void | no return value |
| if | check condition |
| else | otherwise |
| for | loop with count |
| while | loop while condition is true |
| return | send value back |
| new | create object |
| this | current object |
| super | parent class |
| final | cannot change |
| try | test risky code |
| catch | handle error |

## Example Program Using Multiple Keywords

```java
public class Main {
    public static void main(String[] args) {
        final int age = 20;

        if (age >= 18) {
            System.out.println("Eligible");
        } else {
            System.out.println("Not Eligible");
        }
    }
}
```

### Keywords Used Here

| Keyword | Use in Program |
| --- | --- |
| public | makes class and method accessible |
| class | creates a class |
| static | main belongs to class |
| void | main returns nothing |
| final | age value cannot change |
| int | age is a whole number |
| if | checks condition |
| else | runs other block if condition is false |

## Beginner Tips

- Do not try to memorize every keyword in one day
- Learn keywords while writing programs
- Focus first on common keywords like `int`, `if`, `else`, `for`, `while`, `class`, `public`, `static`, and `void`
- Practice small examples to understand each keyword better

## Final Note

Java keywords are special reserved words that give structure and meaning to Java programs. If you understand the common keywords and what they do, learning Java becomes much easier.



###
