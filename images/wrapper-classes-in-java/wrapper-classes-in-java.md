# Wrapper Classes in Java

In Java, **wrapper classes** are object versions of primitive data types. They let you use simple values like `int`, `double`, and `char` as objects.

This is useful because some parts of Java work only with objects, not with primitive values.

## What Is a Wrapper Class?

A wrapper class "wraps" a primitive value inside an object.

For example:

- `int` becomes `Integer`
- `double` becomes `Double`
- `char` becomes `Character`
- `boolean` becomes `Boolean`

## Why Wrapper Classes Are Needed

Wrapper classes are useful because:

- Java collections like `ArrayList` store objects, not primitives
- Some methods and APIs need objects
- Wrapper objects can hold `null`, but primitives cannot
- Wrapper classes provide useful methods like parsing, comparing, and converting values

## Primitive Types and Their Wrapper Classes

| Primitive Type | Wrapper Class |
| --- | --- |
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

## Simple Example

```java
public class Main {
    public static void main(String[] args) {
        int mohitMarks = 357;
        Integer mohitWrapper = mohitMarks;

        System.out.println("Primitive value: " + mohitMarks);
        System.out.println("Wrapper object: " + mohitWrapper);
    }
}
```

### Output
Primitive value: 357
Wrapper object: 357

## In this example:

- `mohitMarks` is a primitive `int`
- `mohitWrapper` is an `Integer` object

## Autoboxing

**Autoboxing** means Java automatically converts a primitive value into its wrapper object.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int akashAge = 21;

        Integer ageObject = akashAge;

        System.out.println("Primitive: " + akashAge);
        System.out.println("Wrapper: " + ageObject);
    }
}
```

Here, Java automatically converts `int` to `Integer`.

## Unboxing

**Unboxing** means Java automatically converts a wrapper object back into a primitive value.

### Example

```java
public class Main {
    public static void main(String[] args) {
        Integer abhiramScore = 95;

        int score = abhiramScore;

        System.out.println("Wrapper: " + abhiramScore);
        System.out.println("Primitive: " + score);
    }
}
```

Here, Java automatically converts `Integer` to `int`.

## Why Autoboxing and Unboxing Matter

These features make Java easier to use because you do not always need to convert values manually.

Without them, you would need more code like this:

```java
Integer num = Integer.valueOf(10);
int value = num.intValue();
```

With autoboxing and unboxing, Java can do this automatically in many cases.

## Wrapper Class Example with ArrayList

Collections like `ArrayList` cannot store primitive values directly.

### Correct Example

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> marksList = new ArrayList<>();

        marksList.add(85);
        marksList.add(90);
        marksList.add(95);

        System.out.println("First Marks: " + marksList.get(0));
        System.out.println("Second Marks: " + marksList.get(1));
    }
}
```

### Output
First Marks: 85
Second Marks: 90

## Here:

- `85`, `90`, and `95` are primitive `int` values
- Java automatically changes them into `Integer` objects

This is autoboxing.

## Example of Unboxing from ArrayList

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> scores = new ArrayList<>();
        scores.add(88);

        int mohitScore = scores.get(0);

        System.out.println("Mohit Score: " + mohitScore);
    }
}
```

Here, `scores.get(0)` returns an `Integer`, and Java automatically changes it into `int`.

This is unboxing.

## Common Wrapper Class Methods

Wrapper classes have useful built-in methods.

| Method | Meaning | Example |
| --- | --- | --- |
| parseInt() | Converts text to primitive int | Integer.parseInt("100") |
| valueOf() | Converts value or text to wrapper object | Integer.valueOf("100") |
| intValue() | Converts wrapper to primitive int | num.intValue() |
| doubleValue() | Converts wrapper to primitive double | price.doubleValue() |
| toString() | Converts value to string | Integer.toString(10) |
| equals() | Compares values | a.equals(b) |
| compareTo() | Compares two wrapper objects | a.compareTo(b) |

## parseInt() Example

`parseInt()` converts a `String` into a primitive `int`.

```java
public class Main {
    public static void main(String[] args) {
        String marksText = "120";

        int marks = Integer.parseInt(marksText);

        System.out.println("Marks: " + marks);
    }
}
```

## valueOf() Example

`valueOf()` converts a value or string into a wrapper object.

```java
public class Main {
    public static void main(String[] args) {
        String scoreText = "250";

        Integer scoreObject = Integer.valueOf(scoreText);

        System.out.println("Score Object: " + scoreObject);
    }
}
```

## parseInt() vs valueOf()

This is a common beginner confusion.

| Method | Returns |
| --- | --- |
| Integer.parseInt("10") | primitive int |
| Integer.valueOf("10") | Integer object |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int num1 = Integer.parseInt("50");
        Integer num2 = Integer.valueOf("50");

        System.out.println("Primitive int: " + num1);
        System.out.println("Wrapper Integer: " + num2);
    }
}
```

## Wrapper Objects Can Store null

Primitive types cannot store `null`, but wrapper classes can.

### Example

```java
public class Main {
    public static void main(String[] args) {
        Integer alphaKnowledgeRank = null;

        System.out.println(alphaKnowledgeRank);
    }
}
```

This is possible because `Integer` is an object type.

But this is not possible:

```java
int alphaKnowledgeRank = null;
```

## Full Example with Multiple Wrapper Classes

```java
public class Main {
    public static void main(String[] args) {
        int akashAge = 22;
        double mohitSalary = 45000.75;
        char abhiramGrade = 'A';
        boolean isAlphaKnowledgeLive = true;

        Integer ageObj = akashAge;
        Double salaryObj = mohitSalary;
        Character gradeObj = abhiramGrade;
        Boolean liveObj = isAlphaKnowledgeLive;

        System.out.println("Age Object: " + ageObj);
        System.out.println("Salary Object: " + salaryObj);
        System.out.println("Grade Object: " + gradeObj);
        System.out.println("Live Object: " + liveObj);

        int age = ageObj;
        double salary = salaryObj;
        char grade = gradeObj;
        boolean live = liveObj;

        System.out.println("Age Primitive: " + age);
        System.out.println("Salary Primitive: " + salary);
        System.out.println("Grade Primitive: " + grade);
        System.out.println("Live Primitive: " + live);
    }
}
```

### Output
Age Object: 22
Salary Object: 45000.75
Grade Object: A
Live Object: true
Age Primitive: 22
Salary Primitive: 45000.75
Grade Primitive: A
Live Primitive: true

## **When to Use Primitive Types**

Use primitive types when:

- you only need simple values
- you do not need object methods
- performance matters
- you are doing calculations

### Example

```java
int total = 100;
double price = 99.99;
```

## When to Use Wrapper Classes

Use wrapper classes when:

- working with collections like `ArrayList`
- using generics
- you need `null`
- you need methods like `parseInt()`, `valueOf()`, `compareTo()`, or `equals()`

### Example

```java
ArrayList<Integer> marks = new ArrayList<>();
```

## Important Note

Autoboxing and unboxing are helpful, but they should not be overused in performance-sensitive code. Oracle specifically recommends using them mainly when there is a mismatch between primitives and reference types, such as putting numbers into collections, rather than for heavy numerical work. [web:94]

## Summary Table

| Term | Meaning |
| --- | --- |
| Primitive type | Simple value like int, double, char |
| Wrapper class | Object form of a primitive type |
| Autoboxing | Primitive to wrapper automatically |
| Unboxing | Wrapper to primitive automatically |

## Final Note

Wrapper classes in Java help primitive values behave like objects. They are very useful when working with collections, methods, and object-based features. If you understand wrappers, autoboxing, and unboxing, many Java topics become much easier.



###
