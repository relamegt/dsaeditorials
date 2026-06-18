# Java String concat() Method

## Introduction

The `concat()` method in Java is used to join (concatenate) one string to another string. It returns a new String containing the combined text.

Since Strings in Java are immutable, the original String is never modified. Instead, a new String object is created and returned.

### Key Features

- Used to combine two or more strings.
- Returns a new String object.
- Does not modify the original String.
- Throws `NullPointerException` if the argument is `null`.
- Belongs to the `String` class.

# Syntax

```java
public String concat(String str)
```

## Parameters

| Parameter | Description |
| --- | --- |
| str | The string to be appended to the current string |

## Return Value

Returns a new String containing the combined result.

## Exception

| Exception | Reason |
| --- | --- |
| NullPointerException | If the argument passed is null |

# Basic Example

```java
public class Main {

    public static void main(String[] args) {

        String company = "Alpha";

        company = company.concat("Knowledge");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

## Explanation

- `"Knowledge"` is appended to `"Alpha"`.
- A new String `"AlphaKnowledge"` is created.
- The result is assigned back to `company`.

![](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/java-string-concat-method/1781780779017-8d5095c5-68ee-4b67-af20-3fe355719c49.png)

# Example 1: Combining Two Strings

Suppose we want to create a platform name.

```java
public class Main {

    public static void main(String[] args) {

        String word1 = "Alpha";
        String word2 = "Knowledge";

        String result = word1.concat(word2);

        System.out.println(result);
    }
}
```

### Output
AlphaKnowledge

## Explanation

- `concat()` joins both strings.
- The combined string is stored in `result`.

# Example 2: Sequential Concatenation

Multiple strings can be joined one after another.

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "Alpha";
        String s2 = "Knowledge";
        String s3 = " Platform";

        String result = s1.concat(s2);
        result = result.concat(s3);

        System.out.println(result);
    }
}
```

### Output
AlphaKnowledge Platform

## Explanation

- First concatenation creates `"AlphaKnowledge"`.
- Second concatenation creates `"AlphaKnowledge Platform"`.

# Example 3: String Immutability

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        company.concat(" Academy");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

## Explanation

- `concat()` creates a new String.
- Original String remains unchanged.
- Since the new String is not assigned, it is discarded.

### Memory Representation

```text
company ─► "AlphaKnowledge"

company.concat(" Academy")

New Object:
"AlphaKnowledge Academy"

company still points to:
"AlphaKnowledge"
```

# Example 4: Updating the Reference

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";

        company = company.concat(" Academy");

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge Academy

## Explanation

- New String is created.
- Reference variable is updated.
- Output shows the modified value.

# Example 5: Concatenating with Spaces

```java
public class Main {

    public static void main(String[] args) {

        String firstName = "Mohit";
        String lastName = " Kumar";

        String fullName =
            firstName.concat(lastName);

        System.out.println(fullName);
    }
}
```

### Output
Mohit Kumar

## Explanation

- Space is included in the second string.
- Both strings are combined into one.

# Example 6: Building an Email Address

```java
public class Main {

    public static void main(String[] args) {

        String user = "support";
        String domain = "@alphaknowledge.com";

        String email =
            user.concat(domain);

        System.out.println(email);
    }
}
```

### Output
support@alphaknowledge.com

## Explanation

- Useful for dynamically generating email IDs.
- Both strings are joined into one complete email address.

# Example 7: Handling NullPointerException

```java
public class Main {

    public static void main(String[] args) {

        String s1 = "AlphaKnowledge";
        String s2 = null;

        String result = s1.concat(s2);

        System.out.println(result);
    }
}
```

### Output
Exception in thread "main"
java.lang.NullPointerException

## Explanation

- `concat()` does not accept null values.
- Passing `null` causes a `NullPointerException`.

# Example 8: Safe Concatenation

```java
public class Main {

    public static void main(String[] args) {

        String company = "AlphaKnowledge";
        String branch = null;

        if(branch != null) {
            company = company.concat(branch);
        }

        System.out.println(company);
    }
}
```

### Output
AlphaKnowledge

## Explanation

- Null check prevents exceptions.
- Safe approach for real-world applications.

# Example 9: Reversing a String Using concat()

```java
public class Main {

    public static void main(String[] args) {

        String original = "Alpha";
        String reversed = "";

        for(int i = original.length() - 1;
            i >= 0; i--) {

            reversed =
                reversed.concat(
                    Character.toString(
                        original.charAt(i)
                    )
                );
        }

        System.out.println(original);
        System.out.println(reversed);
    }
}
```

### Output
Alpha
ahplA

## Explanation

- Characters are taken from right to left.
- Each character is added using `concat()`.
- Final string becomes reversed.

# concat() vs + Operator

Both methods can join strings.

## Using concat()

```java
String s =
"Alpha".concat("Knowledge");
```

### Output
AlphaKnowledge

## Using + Operator

```java
String s =
"Alpha" + "Knowledge";
```

### Output
AlphaKnowledge

### Difference

| concat() | + Operator |
| --- | --- |
| Method of String class | Operator |
| Accepts only Strings | Can combine numbers and Strings |
| Throws exception for null | Converts null to "null" |
| Explicit string joining | Simpler syntax |

# concat() vs StringBuilder

| Feature | concat() | StringBuilder |
| --- | --- | --- |
| Mutable | No | Yes |
| Creates New Object | Yes | No |
| Performance | Slower for repeated concatenation | Faster |
| Memory Usage | Higher | Lower |
| Best For | Small operations | Large repeated operations |

# Performance Example

### Using concat()

```java
String result = "";

for(int i = 1; i <= 5; i++) {
    result = result.concat("Java ");
}
```

Every iteration creates a new String object.

### Using StringBuilder

```java
StringBuilder sb =
    new StringBuilder();

for(int i = 1; i <= 5; i++) {
    sb.append("Java ");
}
```

More efficient because the same object is modified.

# Real-World Applications of concat()

- Creating usernames
- Building email addresses
- Generating URLs
- Creating reports
- Formatting messages
- Building file paths
- Creating dynamic text content

### Example

```java
String website =
    "https://".concat(
        "alphaknowledge.com"
    );

System.out.println(website);
```

### Output
https://alphaknowledge.com
# Advantages of concat()

- Easy to use.
- Simple syntax.
- Returns a new String.
- Useful for joining small strings.
- Maintains String immutability.

# Limitations of concat()

- Creates a new object every time.
- Slower for repeated concatenations.
- Throws NullPointerException for null values.
- Not suitable for large-scale string building.

# Interview Questions

| Question | Answer |
| --- | --- |
| What does concat() do? | Combines two strings |
| Does concat() modify the original String? | No |
| What does concat() return? | A new String object |
| Can concat() accept null? | No |
| Which exception is thrown for null? | NullPointerException |
| Is concat() faster than StringBuilder? | No |
| Why is a new object created? | Because Strings are immutable |

# Summary

The `concat()` method is used to join strings in Java and belongs to the `String` class. Because Strings are immutable, the original String is never modified, and a new String object is always created as a result of the concatenation. Note that passing `null` as an argument to `concat()` will cause a `NullPointerException`. For frequent or large-scale string modifications, using `StringBuilder` is preferred to improve performance and reduce memory usage, while `concat()` is best suited for simple, readable string joining operations.




