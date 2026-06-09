# Java Variables

In Java, a **variable** is a name used to store data. You can think of a variable like a labeled box that keeps a value inside it.

For example, a variable can store:

- a number
- a word
- a decimal value
- a single character
- `true` or `false`

## What Is a Variable?

A variable is used to store information that can be used later in a program.

### Example

```java
int age = 25;
```

In this line:

- `int` is the data type
- `age` is the variable name
- `25` is the value stored in the variable

## Why Variables Are Important

Variables help us:

- store data
- reuse data
- update values
- perform calculations
- show output

Without variables, programs would not be able to work with changing data.

## Parts of a Variable

A Java variable usually has 3 parts.

| Part | Meaning |
| --- | --- |
| Data type | Tells Java what kind of value will be stored |
| Variable name | The name of the variable |
| Value | The actual data stored in the variable |

### Example

```java
double salary = 50000.50;
```

| Part | Value |
| --- | --- |
| Data type | double |
| Variable name | salary |
| Stored value | 50000.50 |

## Variable Syntax

The basic syntax is:

```java
dataType variableName = value;
```

### Example

```java
String name = "Rahul";
```

## Declaring a Variable

Declaration means creating a variable by giving it a type and a name.

### Example

```java
int marks;
```

This creates a variable named `marks`, but no value is stored yet.

## Initializing a Variable

Initialization means giving a value to the variable.

### Example

```java
marks = 90;
```

## Declaration and Initialization Together

![variable declaration](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-variables/1781009590131-variable_1.png)

This is the most common style.

```java
int marks = 90;
```

## Simple Example Program

```java
public class Main {
    public static void main(String[] args) {
        int age = 25;
        String name = "Amit";
        double salary = 50000.50;

        System.out.println("Age: " + age);
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}
```

### Output
Age: 25
Name: Amit
Salary: 50000.5

## ![Memory allocation](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-variables/1781009712233-variable_2.png)

## Common Data Types Used with Variables

Here are some popular Java data types used with variables.

| Data Type | What It Stores | Example |
| --- | --- | --- |
| int | Whole numbers | int age = 20; |
| double | Decimal numbers | double price = 99.99; |
| float | Decimal numbers | float pi = 3.14f; |
| char | Single character | char grade = 'A'; |
| boolean | true or false | boolean isPassed = true; |
| String | Text | String name = "Ravi"; |

## More Examples

```java
int number = 10;
float temp = 5.5f;
char letter = 'H';
boolean isJavaEasy = true;
String city = "Hyderabad";
```

## Changing Variable Value

The value of a variable can be changed later.

### Example

```java
int score = 10;
score = 20;
```

Now the value of `score` is `20`.

## Example Program

```java
public class Main {
    public static void main(String[] args) {
        int score = 10;
        System.out.println("Old Score: " + score);

        score = 25;
        System.out.println("New Score: " + score);
    }
}
```

### Output
Old Score: 10
New Score: 25

## **Types of Variables in Java**

Java mainly uses these common variable types.

| Type | Meaning |
| --- | --- |
| Local variable | Declared inside a method or block |
| Parameter | Variable given to a method |
| Instance variable | Declared inside a class but outside methods, belongs to an object |
| Static variable | Shared variable that belongs to the class |

## 1. Local Variable

A local variable is created inside a method.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int age = 20;
        System.out.println(age);
    }
}
```

Here, `age` is a local variable because it is inside the `main()` method.

## 2. Parameter

A parameter is a variable used in a method definition.

### Example

```java
public class Main {
    static void showAge(int age) {
        System.out.println(age);
    }

    public static void main(String[] args) {
        showAge(20);
    }
}
```

Here, `age` inside `showAge(int age)` is a parameter.

## 3. Instance Variable

An instance variable is declared inside a class but outside methods. Each object gets its own copy.

### Example

```java
public class Student {
    String name;
}
```

Here, `name` is an instance variable.

## 4. Static Variable

A static variable belongs to the class, not to each object.

### Example

```java
public class Student {
    static String schoolName = "ABC School";
}
```

Here, `schoolName` is a static variable.

## Variable Naming Rules

Java variables must follow some rules.

| Rule | Explanation |
| --- | --- |
| Must start with a letter, _, or $ | Cannot start with a number |
| Cannot use spaces | student name is wrong |
| Cannot use Java keywords | int class = 5; is wrong |
| Can contain letters and digits | Example: mark1 |
| Case-sensitive | age and Age are different |

## Valid Variable Names

```java
age
studentName
totalMarks
_myValue
$price
number1
```

## Invalid Variable Names

```java
1age
student name
class
my-value
total@marks
```

## Why These Are Invalid

| Invalid Name | Reason |
| --- | --- |
| 1age | Starts with a number |
| student name | Contains space |
| class | Java keyword |
| my-value | Contains - |
| total@marks | Contains @ |

## Naming Best Practices

Even if Java allows `_` and `$`, beginners should use simple and meaningful names.

### Good Variable Names

```java
studentName
totalMarks
price
isPassed
```

### Poor Variable Names

```java
a
x1
temp123
_data
```

## Java Naming Style

For variable names, Java usually uses **camelCase**.

That means:

- first word starts with a small letter
- next words start with capital letters

### Example

```java
firstName
totalAmount
studentMarks
isActive
```

## Example with Different Variables

```java
public class Main {
    public static void main(String[] args) {
        String studentName = "Anjali";
        int studentAge = 19;
        double marks = 88.5;
        boolean isPassed = true;

        System.out.println("Name: " + studentName);
        System.out.println("Age: " + studentAge);
        System.out.println("Marks: " + marks);
        System.out.println("Passed: " + isPassed);
    }
}
```

### Output
Name: Anjali
Age: 19
Marks: 88.5
Passed: true

## 

## Final Note

Variables are one of the most important basics in Java. They store data, make programs flexible, and help you work with values easily. Once you understand variables well, learning Java becomes much easier.



###
