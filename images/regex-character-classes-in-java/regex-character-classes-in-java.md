# Regex Character Classes in Java

## Introduction

**Regex Character Classes** in Java allow us to match a single character from a specified set of characters. They simplify pattern matching and help write shorter, more readable regular expressions.

### Uses of Character Classes

- Match multiple characters using one pattern.
- Validate usernames, phone numbers, and passwords.
- Search and extract specific text patterns.
- Reduce complex conditional checks.

# Basic Example

```java
public class AlphaKnowledge {
    public static void main(String[] args) {

        String input = "abc123";

        System.out.println(
            input.matches(".*[a-z]+.*")
        );
    }
}
```

### Output
true

### Explanation

- `[a-z]` matches any lowercase letter.
- `+` means one or more occurrences.
- `.*` allows any characters before and after.
- Since `"abc123"` contains lowercase letters, it matches.

# Syntax

```java
[characters]
```

Example:

```java
[a-z]
```

Matches any lowercase letter.

# Types of Character Classes

## 1. Simple Character Class

A simple character class matches exactly one character from the specified set.

### Example

```java
public class Main {
    public static void main(String[] args) {

        String regex = "[xyz]";

        System.out.println("x".matches(regex));
        System.out.println("y".matches(regex));
        System.out.println("a".matches(regex));
    }
}
```

### Output
true
true
false

### Explanation

- `[xyz]` accepts only x, y, or z.
- `"a"` is not part of the set.

## 2. Range Character Class

A range class matches one character within a specified range.

### Example

```java
public class Main {
    public static void main(String[] args) {

        String regex = "[0-9]";

        System.out.println("8".matches(regex));
        System.out.println("A".matches(regex));
    }
}
```

### Output
true
false

### Explanation

- `[0-9]` matches any digit.
- `"A"` is outside the range.

## 3. Multiple Ranges

Multiple ranges can be combined into one character class.

### Example

```java
public class Main {
    public static void main(String[] args) {

        String regex = "[a-zA-Z0-9]";

        System.out.println("M".matches(regex));
        System.out.println("7".matches(regex));
        System.out.println("#".matches(regex));
    }
}
```

### Output
true
true
false

### Explanation

The pattern accepts:

- Lowercase letters
- Uppercase letters
- Digits

Special characters like `#` are rejected.

## 4. Negated Character Class

A negated class matches everything except the specified characters.

### Example

```java
public class Main {
    public static void main(String[] args) {

        String regex = "[^0-9]";

        System.out.println("A".matches(regex));
        System.out.println("5".matches(regex));
    }
}
```

### Output
true
false

### Explanation

- `^` means NOT.
- `[ ^0-9 ]` matches any non-digit character.

# Predefined Character Classes

Java provides several commonly used character classes.

| Regex | Description |
| --- | --- |
| \d | Digit [0-9] |
| \D | Non-digit |
| \w | Word Character [a-zA-Z0-9_] |
| \W | Non-word Character |
| \s | Whitespace |
| \S | Non-whitespace |

## Example: Predefined Character Classes

```java
public class Main {
    public static void main(String[] args) {

        System.out.println("5".matches("\\\\d"));
        System.out.println("A".matches("\\\\D"));

        System.out.println("Mohit_123".matches("\\\\w+"));

        System.out.println(" ".matches("\\\\s"));
    }
}
```

### Output
true
true
true
true

# Quantifiers with Character Classes

Quantifiers specify how many times a character class can occur.

| Quantifier | Meaning | Example |
| --- | --- | --- |
| * | 0 or more times | [0-9]* |
| + | 1 or more times | [0-9]+ |
| ? | 0 or 1 time | [A-Z]? |
| {n} | Exactly n times | [0-9]{4} |
| {n,} | At least n times | [0-9]{2,} |
| {n,m} | Between n and m times | [0-9]{2,4} |

## Example: Using Quantifiers

```java
public class Main {
    public static void main(String[] args) {

        System.out.println(
            "1234".matches("[0-9]{4}")
        );

        System.out.println(
            "123".matches("[0-9]{4}")
        );

        System.out.println(
            "hello".matches("[a-z]+")
        );

        System.out.println(
            "aaaa".matches("a*")
        );
    }
}
```

### Output
true
false
true
true

### Explanation

- `{4}` requires exactly 4 digits.
- `+` requires one or more letters.
- `*` allows zero or more occurrences.

# Real-World Examples

## 1. Validate Mobile Number

```java
public class Main {
    public static void main(String[] args) {

        String phone = "9876543210";

        System.out.println(
            phone.matches("[0-9]{10}")
        );
    }
}
```

### Output
true

## 2. Validate Username

```java
public class Main {
    public static void main(String[] args) {

        String username = "Mohit123";

        System.out.println(
            username.matches("[a-zA-Z0-9]+")
        );
    }
}
```

### Output
true

## 3. Validate Roll Number

```java
public class Main {
    public static void main(String[] args) {

        String roll = "23CSE101";

        System.out.println(
            roll.matches("[0-9]{2}[A-Z]{3}[0-9]{3}")
        );
    }
}
```

### Output
true

# **Advantages of Character Classes**

- Makes regex shorter.
- Improves readability.
- Simplifies validations.
- Supports powerful text searching.
- Reduces coding effort.

# Disadvantages of Character Classes

- Complex regex patterns may become difficult to understand.
- Incorrect ranges can lead to unexpected matches.
- Debugging large regex expressions can be challenging.

# Summary

Regex Character Classes in Java are used to match a single character from a defined set of characters. They can be simple classes (`[abc]`), ranges (`[a-z]`), multiple ranges (`[a-zA-Z0-9]`), negated classes (`[^0-9]`), or predefined classes (`\\d`, `\\w`, `\\s`). Character classes become even more powerful when combined with quantifiers such as `*`, `+`, `?`, and `{n}`. They are widely used for validating user input, searching text, extracting data, and building efficient regular expressions in Java applications.




