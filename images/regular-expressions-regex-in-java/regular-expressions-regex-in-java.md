# Regular Expressions (Regex) in Java

## Introduction

Regular Expressions (Regex) in Java are special patterns used to search, validate, extract, and manipulate text. Regex provides a powerful and flexible way to work with strings by defining search rules instead of checking characters one by one.

Regular expressions are widely used in form validation, data extraction, search operations, text replacement, log analysis, and data cleaning applications.

### Applications of Regex

- Email validation
- Password validation
- Mobile number validation
- Searching specific words in text
- Extracting data from files
- Data filtering and processing
- Input validation in web applications

# Java Regex Package

Java provides regex support through the:

```java
java.util.regex
```

package.

The main classes are:

| Class | Purpose |
| --- | --- |
| Pattern | Represents compiled regex pattern |
| Matcher | Performs matching operations |
| PatternSyntaxException | Handles invalid regex patterns |

# Regex Workflow

The regex process generally follows three steps:

Regex Pattern
      ↓
Pattern Object
      ↓
Matcher Object
      ↓
Search / Match Result

# Pattern Class

The Pattern class is used to compile regular expressions into reusable pattern objects.

### Common Methods

| Method | Description |
| --- | --- |
| compile() | Compiles regex pattern |
| matcher() | Creates matcher object |
| matches() | Checks full string match |
| split() | Splits string using regex |

## Example: Pattern Class

```java
import java.util.regex.Pattern;

public class AlphaKnowledge {

    public static void main(String[] args) {

        System.out.println(
            Pattern.matches("Mohit.*", "MohitKumar")
        );

        System.out.println(
            Pattern.matches("Akash[0-9]+", "Akash123")
        );
    }
}
```

### Output
true
true

### Explanation

- `Mohit.*` means string starts with Mohit.
- `[0-9]+` means one or more digits.

# Matcher Class

The Matcher class performs actual matching operations on strings.

### Important Methods

| Method | Description |
| --- | --- |
| find() | Finds next occurrence |
| matches() | Checks entire string |
| start() | Starting index |
| end() | Ending index |
| group() | Returns matched text |
| groupCount() | Returns group count |

## Example: Matcher Class

```java
import java.util.regex.*;

public class AlphaKnowledge {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("Java");

        Matcher m =
            p.matcher("Java is powerful. Java is popular.");

        while(m.find()) {

            System.out.println(
                "Found at: "
                + m.start()
                + " to "
                + (m.end()-1)
            );
        }
    }
}
```

### Output
Found at: 0 to 3
Found at: 18 to 21

# Character Classes

Character classes define a set of characters to match.

## Common Character Classes

| Pattern | Meaning |
| --- | --- |
| [abc] | a or b or c |
| [^abc] | except a,b,c |
| [a-z] | lowercase letters |
| [A-Z] | uppercase letters |
| [a-zA-Z] | all alphabets |
| [0-9] | digits |

## Example

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        System.out.println(
            Pattern.matches("[a-z]", "m")
        );

        System.out.println(
            Pattern.matches("[A-Z]", "M")
        );
    }
}
```

### Output
true
true

# Quantifiers

Quantifiers specify how many times a character or group can occur.

| Quantifier | Meaning |
| --- | --- |
| X? | 0 or 1 time |
| X+ | 1 or more times |
| X* | 0 or more times |
| X{n} | Exactly n times |
| X{n,} | At least n times |
| X{n,m} | Between n and m times |

## Example

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        System.out.println(
            Pattern.matches("\\d{4}", "2026")
        );

        System.out.println(
            Pattern.matches("a+", "aaaa")
        );

        System.out.println(
            Pattern.matches("a*", "")
        );
    }
}
```

### Output
true
true
true

# Common Regex Symbols

## Dot (.)

Matches any single character.

```java
Pattern.matches("A.", "Ak");
```

Output:

true

## Digit (\d)

Matches digits.

```java
Pattern.matches("\\d+", "12345");
```

Output:

true

## Non-Digit (\D)

Matches non-numeric characters.

```java
Pattern.matches("\\D+", "Mohit");
```

Output:

true

## Whitespace (\s)

Matches spaces and tabs.

```java
Pattern.matches("\\s", " ");
```

Output:

true

## Non-Whitespace (\S)

```java
Pattern.matches("\\S+", "Java");
```

Output:

true

## Word Character (\w)

Matches:

a-z
A-Z
0-9
_
Example:

```java
Pattern.matches("\\w+", "AlphaKnowledge_2026");
```

Output:

true

## Non-Word Character (\W)

Matches symbols.

```java
Pattern.matches("\\W", "@");
```

Output:

true

# Word Boundaries

## \b

Matches word boundary.

```java
Pattern p =
Pattern.compile("\\bJava\\b");
```

Matches:

Java Programming
Does not match:

JavaScript

# Email Validation Example

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        String email =
            "mohit@gmail.com";

        boolean result =
        Pattern.matches(
            "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}",
            email
        );

        System.out.println(result);
    }
}
```

### Output
true

# Mobile Number Validation

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        String mobile =
            "9876543210";

        boolean result =
            Pattern.matches(
                "[6-9][0-9]{9}",
                mobile
            );

        System.out.println(result);
    }
}
```

### Output
true

# Password Validation Example

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        String password =
            "Mohit@123";

        boolean result =
        Pattern.matches(
            "^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d).{8,}$",
            password
        );

        System.out.println(result);
    }
}
```

### Output
true

# Splitting Strings Using Regex

```java
import java.util.regex.Pattern;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile(",");

        String[] names =
            p.split(
                "Mohit,Akash,Hemesh,Abhiram"
            );

        for(String s : names)
            System.out.println(s);
    }
}
```

### Output
Mohit
Akash
Hemesh
Abhiram

# Replacing Text Using Regex

```java
public class Main {

    public static void main(String[] args) {

        String data =
            "Java is awesome";

        System.out.println(
            data.replaceAll(
                "Java",
                "AlphaKnowledge"
            )
        );
    }
}
```

### Output
AlphaKnowledge is awesome

# Advantages of Regex

- Reduces complex string-processing code.
- Fast pattern matching.
- Powerful validation mechanism.
- Useful for data extraction.
- Widely used in web and enterprise applications.
- Supports text replacement and filtering.

# Disadvantages of Regex

- Complex patterns may be difficult to understand.
- Hard to debug for beginners.
- Large regex expressions reduce readability.
- Performance may decrease for extremely complex patterns.

# 

# Summary

Regular Expressions (Regex) in Java provide a powerful mechanism for searching, validating, extracting, splitting, and replacing text using predefined patterns. Java implements regex functionality through the `java.util.regex` package using the Pattern and Matcher classes. Character classes, quantifiers, and special symbols make it possible to define flexible matching rules for real-world tasks such as email validation, password checking, phone number verification, text processing, and data extraction. Regex significantly reduces the amount of code required for complex string operations and is widely used in modern Java applications.




