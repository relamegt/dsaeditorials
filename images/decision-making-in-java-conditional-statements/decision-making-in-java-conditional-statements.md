# Decision Making in Java - Conditional Statements

Decision-making in programming is similar to real-life decision-making. We often want certain blocks of code to execute only when specific conditions are met. In Java, decision-making statements control the flow of execution.

Java provides these decision-making statements:

- `if` statement
- `if-else` statement
- nested `if` statement
- `if-else-if` ladder
- `switch` statement
- Ternary operator (`? :`)

![Decision Making](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/decision-making-in-java-conditional-statements/1781013716355-decision_making_in_java.png)

## 1. if Statement

The `if` statement is the simplest decision-making statement. It executes a block of code only if a given condition is true.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int akashAge = 10;
        
        if (akashAge < 15) {
            System.out.println("Condition is True");
        }
    }
}
```

### Output
Condition is True

Note: If curly braces `{}` are omitted, only the next line after `if` is considered part of the block.

## 2. if-else Statement

The `if-else` statement allows you to execute one block if the condition is true and another block if it is false.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int mohitAge = 10;
        
        if (mohitAge < 15)
            System.out.println("mohitAge is smaller than 15");
        else
            System.out.println("mohitAge is greater than 15");
    }
}
```

### Output
mohitAge is smaller than 15

## 3. nested-if Statement

A nested-if is an `if` statement inside another `if` statement. It is useful when a second condition depends on the first.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int abhiramAge = 10;
        
        if (abhiramAge < 15) {
            System.out.println("abhiramAge is smaller than 15");
            
            if (abhiramAge == 10) {
                System.out.println("abhiramAge is exactly 10");
            }
        }
    }
}
```

### Output
abhiramAge is smaller than 15
abhiramAge is exactly 10

## 4. if-else-if Ladder

The `if-else-if` ladder allows multiple independent conditions to be checked in order. As soon as one condition is true, its block executes, and the rest are skipped.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int score = 20;
        
        if (score == 10)
            System.out.println("score is 10");
        else if (score == 15)
            System.out.println("score is 15");
        else if (score == 20)
            System.out.println("score is 20");
        else
            System.out.println("score is not present");
    }
}
```

### Output
score is 20

## 5. Switch Case

The `switch` statement is a multiway branch statement. It provides an easy way to dispatch execution to different parts of code based on the value of the expression.

### Example

```java
public class Main {
    public static void main(String[] args) {
        int num = 20;
        switch (num) {
            case 5:
                System.out.println("It is 5");
                break;
            case 10:
                System.out.println("It is 10");
                break;
            case 15:
                System.out.println("It is 15");
                break;
            case 20:
                System.out.println("It is 20");
                break;
            default:
                System.out.println("Not present");
        }
    }
}
```

### Output
It is 20

Important notes:

- The expression can be of type `byte`, `short`, `int`, `char`, or an enumeration
- Starting from JDK 7, the expression can also be of type `String`
- Duplicate case values are not allowed
- The `default` statement is optional
- The `break` statement terminates a statement sequence
- Without `break`, statements in switch blocks fall through

## 6. Ternary Operator (`? :`)

The ternary operator is a conditional operator that provides a shorthand way to write simple `if-else` statements.

**Syntax:**

```java
condition ? expression_if_true : expression_if_false;
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 10, b = 20;
        int max = (a > b) ? a : b;
        
        System.out.println("Maximum is " + max);
    }
}
```

### Output
Maximum is 20

This program uses the ternary operator to find the maximum of two numbers. It checks the condition `a > b`; if true, it assigns `a` to `max`, otherwise it assigns `b`.

## if-else vs switch-case

| Features | if-else | switch-case |
| --- | --- | --- |
| Use Case | Suitable for condition-based checks | Best for exact value matching |
| Readability | More readable for a few conditions | More readable and efficient for many cases |
| Performance | Slower for many checks | Faster and optimized for many cases |
| Flexibility | Supports ranges and complex conditions | Only supports exact matches of values |

## Common Mistakes to Avoid

### 1. Missing Curly Braces

When omitting curly braces, only the next line is part of the `if` block.

```java
if (condition)
    System.out.println("This is in the block");
System.out.println("This is NOT in the block");
```

### 2. Using `=` instead of `==`

```java
if (x = 5)  // Wrong - assignment
if (x == 5) // Right - comparison
```

### 3. Missing break in switch

Without `break`, switch cases fall through to the next case.

```java
case 10:
    System.out.println("It is 10");
    // Missing break - will execute next case too
case 15:
    System.out.println("It is 15");
```

### 4. Nested if-else Confusion

In nested `if-else`, the `else` belongs to the nearest `if`.

```java
if (x > 2)
    if (x > 4)
        System.out.println("A");
    else
        System.out.println("B");
```

When `x = 5`, output is `A`.
When `x = 3`, output is `B`.

## Full Example with All Decision Making Statements

### Example

```java
public class Main {
    public static void main(String[] args) {
        int akashMarks = 85;
        
        if (akashMarks >= 90) {
            System.out.println("Grade A");
        } else if (akashMarks >= 80) {
            System.out.println("Grade B");
        } else if (akashMarks >= 70) {
            System.out.println("Grade C");
        } else {
            System.out.println("Grade D");
        }
        
        int mohitGrade = 2;
        switch (mohitGrade) {
            case 1:
                System.out.println("Excellent");
                break;
            case 2:
                System.out.println("Good");
                break;
            case 3:
                System.out.println("Average");
                break;
            default:
                System.out.println("Invalid Grade");
        }
        
        int abhiramAge = 20;
        String status = (abhiramAge >= 18) ? "Adult" : "Minor";
        System.out.println("Status: " + status);
    }
}
```

### Output
Grade B
Good
Status: Adult

## Quick Summary

| Statement | When to Use |
| --- | --- |
| `if` | Single condition check |
| `if-else` | Two alternative blocks |
| nested `if` | Multiple dependent conditions |
| `if-else-if` | Multiple independent conditions |
| `switch` | Exact value matching for many cases |
| Ternary | Simple if-else as expression |

## Final Note

Decision-making statements control which blocks of code execute based on conditions. They are essential for implementing logic, handling different scenarios, and making programs respond dynamically to different inputs. Understanding when to use each statement helps write cleaner and more efficient code.



###
