# Matcher Class in Java

## Introduction

The **Matcher** class in Java belongs to the **java.util.regex** package and is used to perform matching operations on strings using Regular Expressions (Regex). It works together with the **Pattern** class, where Pattern defines the regex and Matcher applies that regex to input text.

The Matcher class provides functionality to:

- Check whether a pattern exists in a string
- Find occurrences of patterns
- Retrieve match positions
- Access matched groups
- Replace matched text
- Study the state of matching operations

# Creating a Matcher Object

A Matcher object is created using the `matcher()` method of the Pattern class.

## Example

```java
import java.util.regex.*;

public class AlphaKnowledge {

    public static void main(String[] args) {

        Pattern pattern =
                Pattern.compile("Java");

        Matcher matcher =
                pattern.matcher("Java is powerful");

        System.out.println(
                matcher.find()
        );
    }
}
```

### Output
true

### Explanation

- `Pattern.compile("Java")` creates a regex pattern.
- `matcher()` applies the pattern to the string.
- `find()` searches for the pattern inside the string.

# Methods of Matcher Class

The methods of Matcher class are grouped into:

1. Match Methods
2. Index Methods
3. Study Methods
4. Replacement Methods

# 1. Match Methods

Match methods are used to determine whether a pattern matches the input string.

| Method | Description |
| --- | --- |
| matches() | Matches entire string |
| find() | Finds next occurrence |
| lookingAt() | Matches beginning of string |

## Example: matches(), lookingAt() and find()

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("Java");

        Matcher m =
            p.matcher("Java is Java");

        System.out.println(
            m.matches()
        );

        System.out.println(
            m.lookingAt()
        );

        m.reset();

        while(m.find()) {
            System.out.println(
                "Match Found"
            );
        }
    }
}
```

### Output
false
true
Match Found
Match Found

### Explanation

- `matches()` checks the complete string.
- `lookingAt()` checks only from the beginning.
- `find()` searches occurrences one by one.

# Difference Between matches(), lookingAt() and find()

| Method | Checks |
| --- | --- |
| matches() | Entire string |
| lookingAt() | Beginning of string |
| find() | Anywhere in string |

# 2. Index Methods

Index methods provide position information about matched text.

| Method | Description |
| --- | --- |
| start() | Start index of match |
| end() | End index + 1 |
| start(group) | Start index of group |
| end(group) | End index of group |

## Example: Retrieving Match Positions

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("(Mohit)");

        Matcher m =
            p.matcher("Hello Mohit");

        if(m.find()) {

            System.out.println(
                m.start()
            );

            System.out.println(
                m.end()
            );

            System.out.println(
                m.start(1)
            );

            System.out.println(
                m.end(1)
            );
        }
    }
}
```

### Output
6
11
6
11

### Explanation

- Match starts at index 6.
- Match ends at index 11.
- Group positions are the same because only one group exists.

# 3. Study Methods

Study methods analyze matcher state and captured groups.

| Method | Description |
| --- | --- |
| group() | Returns matched text |
| groupCount() | Returns total groups |
| hitEnd() | Checks if end reached |
| requireEnd() | Checks if more input affects result |

## Example: Study Methods

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("(Java)(\\d)");

        Matcher m =
            p.matcher("Java8");

        if(m.find()) {

            System.out.println(
                m.group()
            );

            System.out.println(
                m.groupCount()
            );

            System.out.println(
                m.hitEnd()
            );

            System.out.println(
                m.requireEnd()
            );
        }
    }
}
```

### Output
Java8
2
false
false

### Explanation

- `group()` returns complete match.
- `groupCount()` returns number of captured groups.
- `hitEnd()` checks whether matching reached input end.
- `requireEnd()` checks whether additional input can change result.

# Capturing Groups

Parentheses create groups in Regex.

## Example

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("(Mohit)-(123)");

        Matcher m =
            p.matcher("Mohit-123");

        if(m.find()) {

            System.out.println(
                m.group(1)
            );

            System.out.println(
                m.group(2)
            );
        }
    }
}
```

### Output
Mohit
123

# 4. Replacement Methods

Replacement methods modify matched content.

| Method | Description |
| --- | --- |
| replaceFirst() | Replaces first occurrence |
| replaceAll() | Replaces all occurrences |
| appendReplacement() | Incremental replacement |
| appendTail() | Appends remaining text |

## Example: replaceFirst() and replaceAll()

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("Java");

        Matcher m =
            p.matcher("Java is Java");

        System.out.println(
            m.replaceFirst("JAVA")
        );

        System.out.println(
            m.replaceAll("JAVA")
        );
    }
}
```

### Output
JAVA is Java
JAVA is JAVA

## Example: appendReplacement()

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        Pattern p =
            Pattern.compile("Java");

        Matcher m =
            p.matcher("Java and Java");

        StringBuffer sb =
            new StringBuffer();

        while(m.find()) {

            m.appendReplacement(
                sb,
                "JAVA"
            );
        }

        m.appendTail(sb);

        System.out.println(sb);
    }
}
```

### Output
JAVA and JAVA

# Real-World Example: Email Extraction

```java
import java.util.regex.*;

public class Main {

    public static void main(String[] args) {

        String text =
        "Contact us at support@gmail.com or help@yahoo.com";

        Pattern p =
        Pattern.compile(
        "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}"
        );

        Matcher m =
            p.matcher(text);

        while(m.find()) {

            System.out.println(
                m.group()
            );
        }
    }
}
```

### Output
support@gmail.com
help@yahoo.com

# Advantages of Matcher Class

- Efficient pattern searching.
- Supports complex text processing.
- Provides detailed match information.
- Allows extraction of groups.
- Supports advanced replacement operations.
- Works seamlessly with Regex.

# Disadvantages of Matcher Class

- Complex regex patterns may reduce readability.
- Debugging large regex expressions can be difficult.
- Frequent recompilation of patterns affects performance.

# 

# Summary

The **Matcher** class in Java is part of the **java.util.regex** package and is responsible for applying regular expressions to input strings. It works with the **Pattern** class to perform matching, searching, grouping, indexing, and replacement operations. Methods like **find()**, **matches()**, **lookingAt()**, **group()**, **start()**, **end()**, **replaceFirst()**, and **replaceAll()** provide powerful tools for text processing. The Matcher class is widely used in applications involving input validation, data extraction, search engines, log analysis, and string manipulation, making it an essential component of Java's Regular Expression framework.




