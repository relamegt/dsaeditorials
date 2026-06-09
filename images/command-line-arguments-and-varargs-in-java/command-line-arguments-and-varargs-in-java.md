# Command Line Arguments and Varargs in Java

In Java, you can pass input to a program at runtime using command-line arguments. You can also write methods that accept a variable number of parameters using varargs.

This article covers:

- command-line arguments in Java
- variable arguments (varargs) in Java

## Command Line Arguments in Java

Command-line arguments are values passed to a program when it is executed from the command prompt. These arguments are stored as String values in the `main(String[] args)` parameter.

### Why Command-Line Arguments Are Useful

Command-line arguments help in several ways:

- provide input without hardcoding values
- make programs flexible and reusable
- pass file names, configuration values, or user data at runtime

### Syntax

```bash
java ClassName arg1 arg2 arg3
```

For example:

```bash
java Main Hello World
```

The JVM collects these values and passes them to `main(String[] args)`:

- `Hello` → stored in `args[0]`
- `World` → stored in `args[1]`

### Example

```java
public class Main {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println(args);
        } else {
            System.out.println("No arguments provided");
        }
    }
}
```

### Running the Program

```bash
javac Main.java
java Main AlphaKnowledge
```

### Output
AlphaKnowledge

If no arguments are given, the program prints "No arguments provided". Trying to access `args[0]` when the array is empty would throw `ArrayIndexOutOfBoundsException`.

### Display All Command-Line Arguments

```java
public class Main {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println("The command line arguments are:");

            for (String val : args) {
                System.out.println(val);
            }
        } else {
            System.out.println("No command line arguments found.");
        }
    }
}
```

### Running the Program

```bash
java Main Akash Mohit Abhiram
```

### Output
The command line arguments are:
Akash
Mohit
Abhiram

### How Command-Line Arguments Work

- command-line arguments are space-separated values passed to `main(String[] args)`
- the JVM wraps them into the `args[]` array
- each value is stored as a String (`args[0]`, `args[1]`, etc.)
- the number of arguments can be checked using `args.length`

## Variable Arguments (Varargs) in Java

Varargs allow methods to accept a variable number of parameters using a simplified syntax. Varargs were introduced in Java 5.

### Key Rules for Varargs

- declared using `...` (ellipsis)
- must be the last parameter in the method
- only one varargs parameter is allowed per method
- internally handled as arrays

### Syntax

```java
public static void methodName(type... parameterName) {
    // method body
}
```

### Example with Strings

```java
public class Main {
    public static void printNames(String... names) {
        for (String name : names) {
            System.out.print(name + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        printNames("Akash", "Mohit");
        printNames("Akash", "Mohit", "Abhiram");
    }
}
```

### Output
Akash Mohit 
Akash Mohit Abhiram

### Example with Integers

```java
public class Main {
    public static void printNumbers(int... numbers) {
        System.out.println("Number of arguments: " + numbers.length);

        for (int n : numbers) {
            System.out.print(n + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        printNumbers(100);
        printNumbers(1, 2, 3, 4);
        printNumbers();
    }
}
```

### Output
Number of arguments: 1
100 
Number of arguments: 4
1 2 3 4 
Number of arguments: 0

### Varargs with Other Parameters

Varargs can be combined with other parameters, but the varargs parameter must always be the last one.

```java
public class Main {
    public static void printInfo(String message, int... numbers) {
        System.out.println("Message: " + message);
        System.out.println("Number of arguments: " + numbers.length);

        for (int n : numbers) {
            System.out.print(n + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        printInfo("Values", 10, 20);
        printInfo("Numbers", 1, 2, 3, 4, 5);
        printInfo("Empty");
    }
}
```

### Output
Message: Values
Number of arguments: 2
10 20 
Message: Numbers
Number of arguments: 5
1 2 3 4 5 
Message: Empty
Number of arguments: 0

## Important Rules and Limitations for Varargs

### 1. Only One Varargs Parameter

You cannot have two varargs parameters in the same method.

```java
// This will cause a compile-time error
void method(String... a, int... b) { }
```

### 2. Varargs Must Be Last

Varargs must appear as the last parameter in the method declaration.

```java
// This will cause a compile-time error
void method(int... a, String b) { }
```

Valid example:

```java
// This is correct
void method(String b, int... a) { }
```

## Comparing Command-Line Arguments and Varargs

| Feature | Command-Line Arguments | Varargs |
| --- | --- | --- |
| Where passed | At runtime from command prompt | When calling a method |
| Type | Always `String[]` | Any type as array |
| Declared in | `main(String[] args)` | Method parameter with `...` |
| Use Case | External input, file names, config | Flexible method parameters |

## Complete Example Using Both

```java
public class Main {
    // Varargs method
    public static void printAll(String... values) {
        for (String v : values) {
            System.out.println(v);
        }
    }

    public static void main(String[] args) {
        System.out.println("Command-line arguments:");
        if (args.length > 0) {
            for (String arg : args) {
                System.out.println(arg);
            }
        } else {
            System.out.println("No command-line arguments");
        }

        System.out.println("\nVarargs call:");
        printAll("Akash", "Mohit", "Abhiram", "AlphaKnowledge");
    }
}
```

### Running the Program

```bash
java Main Hello World
```

### Output
Command-line arguments:
Hello
World

Varargs call:
Akash
Mohit
Abhiram
AlphaKnowledge

## Final Note

Command-line arguments help you pass external input to a Java program at runtime, while varargs make methods more flexible by allowing them to accept any number of parameters. Both features improve code reuse and make programs easier to adapt to different situations.



###
