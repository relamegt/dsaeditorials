# Java String Methods

## Introduction

Java provides a rich collection of built-in methods in the `String` class that help programmers manipulate, compare, search, and format text efficiently.

Since strings are immutable in Java, most string methods do not modify the original string. Instead, they return a new String object containing the result.

### Why String Methods are Important?

- Simplify text processing.
- Reduce coding effort.
- Improve readability.
- Provide efficient searching and comparison.
- Help in data validation and formatting.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println("Length = " + company.length());
        System.out.println("Uppercase = " + company.toUpperCase());
        System.out.println("Substring = " + company.substring(5));
    }
}
```

### Output
Length = 14
Uppercase = ALPHAKNOWLEDGE
Substring = Knowledge

# 1. length()

Returns the total number of characters present in a string.

### Syntax

```java
stringName.length();
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company.length());
    }
}
```

### Output
14

### Explanation

The string contains 14 characters.

# 2. charAt()

Returns the character present at a specified index.

### Syntax

```java
stringName.charAt(index);
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company.charAt(0));
        System.out.println(company.charAt(5));
    }
}
```

### Output
A
K

### Explanation

- Index starts from 0.
- Character at index 0 is A.
- Character at index 5 is K.

# 3. substring(int start)

Extracts characters from the specified index until the end.

### Syntax

```java
stringName.substring(startIndex);
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company.substring(5));
    }
}
```

### Output
Knowledge

### Explanation

Returns all characters from index 5 onwards.

# 4. substring(int start, int end)

Extracts characters from start index to end-1 index.

### Syntax

```java
stringName.substring(start,end);
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company.substring(0,5));
    }
}
```

### Output
Alpha

### Explanation

Characters from index 0 to 4 are extracted.

# 5. concat()

Joins one string to another string.

### Syntax

```java
string1.concat(string2);
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "Alpha";
        String s2 = "Knowledge";

        System.out.println(s1.concat(s2));
    }
}
```

### Output
AlphaKnowledge

### Explanation

Creates a new combined string.

# 6. indexOf()

Returns the first occurrence index of a character or substring.

### Syntax

```java
stringName.indexOf("text");
```

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(company.indexOf("Know"));
    }
}
```

### Output
5

### Explanation

"Know" starts at index 5.

# 7. indexOf(String, int)

Searches for a substring starting from a specified index.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text = "AlphaKnowledge Academy";

        System.out.println(text.indexOf("a",6));
    }
}
```

### Output
10

# 8. lastIndexOf()

Returns the last occurrence of a character or substring.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text = "AlphaKnowledge";

        System.out.println(text.lastIndexOf("a"));
    }
}
```

### Output
13

### Explanation

Returns the last occurrence of "a".

# 9. equals()

Checks whether two strings contain exactly the same content.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "AlphaKnowledge";
        String s2 = "AlphaKnowledge";

        System.out.println(s1.equals(s2));
    }
}
```

### Output
true

# 10. equalsIgnoreCase()

Compares strings while ignoring letter case.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "ALPHAKNOWLEDGE";
        String s2 = "alphaknowledge";

        System.out.println(
            s1.equalsIgnoreCase(s2)
        );
    }
}
```

### Output
true

# 11. compareTo()

Performs lexicographical comparison.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "Alpha";
        String s2 = "Knowledge";

        System.out.println(
            s1.compareTo(s2)
        );
    }
}
```

### Output
Negative Value

### Explanation

"Alpha" comes before "Knowledge" alphabetically.

# 12. compareToIgnoreCase()

Compares strings ignoring case differences.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "alpha";
        String s2 = "ALPHA";

        System.out.println(
            s1.compareToIgnoreCase(s2)
        );
    }
}
```

### Output
0

### Explanation

Both strings are considered equal.

# 13. toLowerCase()

Converts all letters into lowercase.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(
            company.toLowerCase()
        );
    }
}
```

### Output
alphaknowledge

# 14. toUpperCase()

Converts all letters into uppercase.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        System.out.println(
            company.toUpperCase()
        );
    }
}
```

### Output
ALPHAKNOWLEDGE

# 15. trim()

Removes leading and trailing spaces.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "   AlphaKnowledge   ";

        System.out.println(
            "'" + text.trim() + "'"
        );
    }
}
```

### Output
'AlphaKnowledge'

# 16. replace()

Replaces characters or substrings.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "AlphaKnowledge";

        System.out.println(
            text.replace('a','@')
        );
    }
}
```

### Output
Alph@Knowledge

# 17. contains()

Checks whether a substring exists.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "AlphaKnowledge";

        System.out.println(
            text.contains("Know")
        );
    }
}
```

### Output
true

# 18. toCharArray()

Converts the string into a character array.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "Alpha";

        char[] arr =
            text.toCharArray();

        for(char ch : arr)
        {
            System.out.print(ch + " ");
        }
    }
}
```

### Output
A l p h a

# 19. startsWith()

Checks whether a string begins with a specific prefix.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "AlphaKnowledge";

        System.out.println(
            text.startsWith("Alpha")
        );
    }
}
```

### Output
true

# 20. endsWith()

Checks whether a string ends with a specific suffix.

### Example

```java
public class Main {

    public static void main(String[] args) {

        String text =
            "AlphaKnowledge";

        System.out.println(
            text.endsWith("Knowledge")
        );
    }
}
```

### Output
true

# Summary Table

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-string-methods/1781781682971-5ce95dfd-d5eb-4583-853e-6cdad1cfee0f.png)

# Summary

Java provides a powerful String class with numerous built-in methods for manipulating, searching, comparing, and formatting text. Since strings are immutable, every modification operation creates a new String object rather than changing the existing one. Methods such as `length()`, `substring()`, `concat()`, `replace()`, `contains()`, and `equals()` simplify text processing and are widely used in real-world Java applications. A good understanding of these methods helps developers write cleaner, more efficient, and maintainable programs while handling textual data effectively.




