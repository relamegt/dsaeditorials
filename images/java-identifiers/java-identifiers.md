# Java Identifiers

In Java, an **identifier** is the name given to things like variables, methods, classes, and packages. These names help us identify and use different parts of a program.

## What Is an Identifier?

An identifier is simply a name used in Java code.

Examples:

- Variable name
- Method name
- Class name
- Package name
- Interface name

### Example

![Identifier](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-identifiers/1781008689047-identifiers.png)

```java
public class Alpha{
    public static void main(String[] args) {
        int x= 9;
    }
}
```

In this example:

- `Alpha` is a class name
- `main` is a method name
- `args` is a parameter name
- `age` is a variable name

All of these are identifiers.

## Rules for Java Identifiers

Java identifiers must follow some rules. If a name breaks these rules, the program will give an error.

### Rule 1: Allowed Characters

An identifier can contain:

- Letters (`A-Z`, `a-z`)
- Digits (`0-9`)
- Underscore (`_`)
- Dollar sign (`$`)

### Rule 2: Cannot Start with a Number

A Java identifier cannot begin with a digit.

### Rule 3: No Spaces

Identifiers cannot contain spaces.

### Rule 4: No Special Symbols

Characters like `@`, `#`, `%`, `&`, `-`, and `+` are not allowed in identifiers.

### Rule 5: Case-Sensitive

Java is case-sensitive, so these names are different:

- `age`
- `Age`
- `AGE`

### Rule 6: Keywords Cannot Be Used

You cannot use Java reserved words like `int`, `class`, `public`, or `while` as identifiers.

## Valid Identifiers

These are correct Java identifiers:

```java
name
studentAge
totalMarks
_myValue
$count
number1
HelloWorld
```

## Invalid Identifiers

These are not valid:

```java
1name
student age
total-marks
class
my@value
```

### Why They Are Invalid

- `1name` starts with a number
- `student age` contains a space
- `total-marks` contains `-`
- `class` is a Java keyword
- `my@value` contains `@`

## Simple Example

```java
public class StudentInfo {
    public static void main(String[] args) {
        String studentName = "Rahul";
        int studentAge = 18;

        System.out.println(studentName);
        System.out.println(studentAge);
    }
}
```

Here:

- `StudentInfo` is a class identifier
- `studentName` is a variable identifier
- `studentAge` is a variable identifier

## Naming Tips for Beginners

These are not strict rules, but they are good coding style.

- Use meaningful names
- Keep names easy to read
- Use `camelCase` for variables and methods
- Use `PascalCase` for class names
- Avoid strange names like `a1`, `x2`, or `_tempValue` unless truly needed

## Common Naming Style in Java

### Variable Names

Start with a lowercase letter:

```java
firstName
totalAmount
studentMarks
```

### Method Names

Also start with a lowercase letter:

```java
getName()
calculateTotal()
printMessage()
```

### Class Names

Start with an uppercase letter:

```java
Student
BankAccount
EmployeeDetails
```

## Best Practice

Even though `_` and `$` are allowed, beginners should usually avoid using them at the start of names. Clear names like `totalMarks` or `userName` are easier to understand.

## Final Note

Identifiers are the names you give to parts of your Java program. If you follow the basic naming rules and use clear names, your code becomes easier to write, read, and understand.



###
