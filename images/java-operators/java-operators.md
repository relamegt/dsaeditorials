# Java Operators

In Java, **operators** are symbols used to perform operations on variables and values. They help us do calculations, compare values, test conditions, and update data.

For example:

- `+` adds values
- `-` subtracts values
- `>` compares values
- `&&` checks two conditions together
- `=` assigns a value

## Why Operators Are Important

Operators are used in many Java programs. They help us:

- perform math
- compare values
- make decisions
- update variables
- write shorter and cleaner code

## Types of Operators in Java

Java operators can be grouped into these main types:

1. Arithmetic operators
2. Unary operators
3. Assignment operators
4. Relational operators
5. Logical operators
6. Ternary operator
7. Bitwise and shift operators
8. `instanceof` operator

## 1. Arithmetic Operators

Arithmetic operators are used for mathematical calculations on numeric data types like `int`, `float`, and `double`.

| Operator | Meaning | Example |
| --- | --- | --- |
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Division | `a / b` |
| `%` | Modulus (remainder) | `a % b` |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 10, b = 3;
        
        int sum = a + b;
        int diff = a - b;
        int mul = a * b;
        int div = a / b;
        int mod = a % b;
        
        System.out.println("Sum: " + sum);
        System.out.println("Difference: " + diff);
        System.out.println("Multiplication: " + mul);
        System.out.println("Division: " + div);
        System.out.println("Modulus: " + mod);
    }
}
```

### Output
Sum: 13
Difference: 7
Multiplication: 30
Division: 3
Modulus: 1

When two integers are divided, Java returns only the quotient and ignores decimals.

## 2. Unary Operators

Unary operators work on a single operand. They increment, decrement, or negate a value.

| Operator | Meaning |
| --- | --- |
| `+` | Positive sign |
| `-` | Negative sign |
| `++` | Increment by 1 |
| `--` | Decrement by 1 |
| `!` | Logical NOT |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 10;
        
        System.out.println("Postincrement : " + (a++));
        System.out.println("Preincrement : " + (++a));
        
        System.out.println("Postdecrement : " + (b--));
        System.out.println("Predecrement : " + (--b));
    }
}
```

### Output
Postincrement : 10
Preincrement : 12
Postdecrement : 10
Predecrement : 8

Post-increment (`a++`) returns the value first, then increments it.
Pre-increment (`++a`) increments first, then returns the updated value.

## 3. Assignment Operators

The assignment operator assigns a value from the right side to a variable on the left. Compound operators perform an operation and assignment together.

| Operator | Meaning | Example |
| --- | --- | --- |
| `=` | Assign | `num = 10` |
| `+=` | Add and assign | `num += 5` |
| `-=` | Subtract and assign | `num -= 5` |
| `*=` | Multiply and assign | `num *= 2` |
| `/=` | Divide and assign | `num /= 2` |
| `%=` | Modulus and assign | `num %= 3` |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int num = 10;
        System.out.println("Initial: " + num);
        
        num += 5;
        System.out.println("After +5: " + num);
        
        num *= 2;
        System.out.println("After *2: " + num);
        
        num -= 5;
        System.out.println("After -5: " + num);
        
        num /= 2;
        System.out.println("After /2: " + num);
        
        num %= 3;
        System.out.println("After %3: " + num);
    }
}
```

### Output
Initial: 10
After +5: 15
After *2: 30
After -5: 25
After /2: 12
After %3: 0

Compound assignments like `+=`, `-=`, `*=` make code cleaner.

## 4. Relational Operators

Relational operators check relationships like equality, greater than, and less than. They return `true` or `false` and are used in `if-else` statements and loops.

| Operator | Meaning |
| --- | --- |
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 3;
        int c = 5;
        
        System.out.println("a > b: " + (a > b));
        System.out.println("a < b: " + (a < b));
        System.out.println("a >= b: " + (a >= b));
        System.out.println("a <= b: " + (a <= b));
        System.out.println("a == c: " + (a == c));
        System.out.println("a != c: " + (a != c));
    }
}
```

### Output
a > b: true
a < b: false
a >= b: true
a <= b: false
a == c: false
a != c: true

## 5. Logical Operators

Logical operators perform logical AND and OR operations. They have a short-circuiting effect: the second condition is not evaluated if the first determines the result.

| Operator | Meaning |
| --- | --- |
| `&&` | Logical AND |
| `||` | Logical OR |
| `!` | Logical NOT |

### Example

```java
public class Main {
    public static void main(String[] args) {
        boolean x = true;
        boolean y = false;
        
        System.out.println("x && y: " + (x && y));
        System.out.println("x || y: " + (x || y));
        System.out.println("!x: " + (!x));
    }
}
```

### Output
x && y: false
x || y: true
!x: false

- `&&` returns `true` only if both conditions are true
- `||` returns `true` if at least one condition is true
- `!` reverses the boolean value

## 6. Ternary Operator

The ternary operator is a shorthand version of `if-else`. It has three operands.

**Syntax:** `(condition) ? value1 : value2`

### Example

```java
public class Main {
    public static void main(String[] args) {
        int a = 20, b = 10, c = 30, result;
        
        result = ((a > b) ? (a > c) ? a : c : (b > c) ? b : c);
        System.out.println("Max of three numbers = "+ result);
    }
}
```

### Output
Max of three numbers = 30

The ternary operator evaluates multiple conditions to find the maximum among three numbers.

## 7. Bitwise Operators

Bitwise operators manipulate individual bits using AND, OR, XOR, and NOT.

| Operator | Meaning |
| --- | --- |
| `&` | Bitwise AND |
| `|` | Bitwise OR |
| `^` | Bitwise XOR |
| `~` | Bitwise NOT |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int d = 0b1010;
        int e = 0b1100;
        
        System.out.println("d & e : " + (d & e));
        System.out.println("d | e : " + (d | e));
        System.out.println("d ^ e : " + (d ^ e));
        System.out.println("~d : " + (~d));
    }
}
```

### Output
d & e : 8
d | e : 14
d ^ e : 6
~d : -11

## Shift Operators

Shift operators move bits left or right, effectively multiplying or dividing by powers of two.

| Operator | Meaning |
| --- | --- |
| `<<` | Left shift |
| `>>` | Right shift |
| `>>>` | Unsigned right shift |

### Example

```java
public class Main {
    public static void main(String[] args) {
        int d = 0b1010;
        int e = 0b1100;
        
        System.out.println("d << 2 : " + (d << 2));
        System.out.println("e >> 1 : " + (e >> 1));
        System.out.println("e >>> 1 : " + (e >>> 1));
    }
}
```

### Output
d << 2 : 40
e >> 1 : 6
e >>> 1 : 6

## 8. instanceof Operator

The `instanceof` operator checks if an object is an instance of a class, subclass, or interface. It returns `true` if the object belongs to that type.

### Example

```java
public class Main {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println(str instanceof String);
        
        Object obj = 10;
        System.out.println(obj instanceof Integer);
        System.out.println(obj instanceof String);
    }
}
```

### Output
true
true
false

The `instanceof` operator helps ensure type safety and avoid runtime errors.

## Common Mistakes to Avoid

### Confusing `==` with `=`

Using `==` for assignment instead of `=` for equality check leads to logical errors.

### Integer Division Confusion

Dividing two integers results in integer division (truncating the decimal part).

```java
System.out.println(10 / 3);
```

### Output
3

Not `3.33`

### Floating Point Comparison

Comparing floating point numbers using `==` can lead to unexpected results due to precision issues.

### String Concatenation in Loops

Using `+` for concatenating strings in loops creates new string objects on each iteration, causing performance issues.

## Operator Precedence

Operators follow a defined precedence and associativity to determine execution order.

### Example

```java
int result = 10 + 5 * 2;
System.out.println(result);
```

### Output
20

Multiplication happens before addition.

### With Parentheses

```java
int result = (10 + 5) * 2;
System.out.println(result);
```

### Output
30

Use parentheses when you want to control the execution order.

## Quick Summary

| Operator Type | Main Use |
| --- | --- |
| Arithmetic | Math operations |
| Unary | Increment, decrement, or negate |
| Assignment | Store and update values |
| Relational | Compare values |
| Logical | Combine conditions |
| Ternary | Short if-else |
| Bitwise | Bit-level operations |
| Shift | Move bits left or right |
| `instanceof` | Type checking |

##



###
