# Regular Expressions in SQL

## Introduction

Regular Expressions (Regex) are powerful pattern-matching tools used to search, validate, extract, and replace text based on specific patterns. In SQL, regex provides advanced text-processing capabilities that go beyond traditional string functions, making it easier to work with complex textual data.

Regular expressions are commonly used for:

- Validating data formats
- Extracting information from text
- Cleaning inconsistent data
- Searching for patterns
- Replacing unwanted characters

---

## What is a Regular Expression?

A Regular Expression (Regex) is a sequence of characters that defines a search pattern.

Regex can be used to:

- Match text patterns
- Validate input formats
- Extract specific portions of text
- Replace matching text
- Filter records based on text conditions

### Example

```sql
SELECT email
FROM users
WHERE REGEXP_LIKE(
    email,
    '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'
);
```

### Explanation

- Retrieves valid email addresses.
- Uses a regex pattern to verify the email structure.

---

# Types of Regular Expression Functions in SQL

Most SQL databases provide three primary regex functions:

1. REGEXP_LIKE()
2. REGEXP_REPLACE()
3. REGEXP_SUBSTR()

---

## REGEXP_LIKE()

The `REGEXP_LIKE()` function checks whether a string matches a specified regular expression pattern and returns TRUE or FALSE.

### Syntax

```sql
REGEXP_LIKE(column_name, 'pattern')
```

### Example

Find products whose names start with the letter A.

```sql
SELECT product_name
FROM products
WHERE REGEXP_LIKE(product_name, '^A');
```

### Output

| product_name |
| --- |
| Apple |
| Apricot |
| AirPods |

### Explanation

- `^` represents the beginning of a string.
- Only values beginning with `A` are returned.

---

## REGEXP_REPLACE()

The `REGEXP_REPLACE()` function searches for text matching a pattern and replaces it with another value.

### Syntax

```sql
REGEXP_REPLACE(
    string,
    'pattern',
    'replacement'
)
```

### Example

Remove all non-numeric characters from phone numbers.

```sql
SELECT REGEXP_REPLACE(
    phone_number,
    '[^0-9]',
    ''
) AS cleaned_number
FROM contacts;
```

### Output

| cleaned_number |
| --- |
| 9876543210 |
| 9123456780 |

### Explanation

- `[^0-9]` matches any non-digit character.
- Matching characters are replaced with an empty string.

---

## REGEXP_SUBSTR()

The `REGEXP_SUBSTR()` function extracts text that matches a regular expression pattern.

### Syntax

```sql
REGEXP_SUBSTR(
    string,
    'pattern',
    start_position,
    occurrence,
    match_parameter
)
```

### Example

Extract domains from email addresses.

```sql
SELECT REGEXP_SUBSTR(
    email,
    '@[^.]+'
) AS domain
FROM users;
```

### Output

| domain |
| --- |
| @gmail |
| @yahoo |
| @outlook |

### Explanation

- Extracts the domain portion starting with `@`.
- Stops before the first period.

---

# Basic Regular Expression Syntax

The following symbols form the foundation of regex pattern matching.

| Pattern | Description | Example | Matches |
| --- | --- | --- | --- |
| . | Any single character | h.t | hat, hit, hot |
| ^ | Start of string | ^A | Apple |
| $ | End of string | ing$ | sing, bring |
| `|` | Logical OR | cat\|dog | cat, dog |
| * | Zero or more occurrences | ab* | a, ab, abb |
| + | One or more occurrences | ab+ | ab, abb |
| ? | Zero or one occurrence | colou?r | color, colour |
| {n} | Exactly n times | a{3} | aaa |
| {n,} | n or more times | a{2,} | aa, aaa |
| {n,m} | Between n and m times | a{2,4} | aa, aaa, aaaa |
| [abc] | Any listed character | [aeiou] | vowels |
| [^abc] | Any character except listed | [^aeiou] | consonants |
| [a-z] | Character range | [0-9] | digits |
| \ | Escape character | . | . |
| \b | Word boundary | \bcat\b | cat |
| \B | Non-word boundary | \Bcat | scatter |
| (abc) | Grouping | (ha)+ | ha, haha |
| \1 | Back-reference | (ab)\1 | abab |

---

# Common Regex Patterns

These patterns are frequently used in SQL applications.

| Pattern | Purpose |
| --- | --- |
| `^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$` | Email validation |
| `^[0-9]+$` | Numeric strings only |
| `https?://[^ ]+` | URL matching |
| `^[A-Za-z0-9]+$` | Alphanumeric validation |

---

## Email Validation Pattern

```sql
SELECT email
FROM users
WHERE REGEXP_LIKE(
    email,
    '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'
);
```

### Matches

```text
john@gmail.com
alice@yahoo.in
admin@company.org
```

---

## Numeric String Validation

```sql
SELECT *
FROM records
WHERE REGEXP_LIKE(
    value,
    '^[0-9]+$'
);
```

### Matches

```text
123
456
7890
```

---

## URL Validation

```sql
SELECT *
FROM websites
WHERE REGEXP_LIKE(
    url,
    'https?://[^ ]+'
);
```

### Matches

```text
https://example.com
http://sample.org
```

---

## Alphanumeric Validation

```sql
SELECT *
FROM users
WHERE REGEXP_LIKE(
    username,
    '^[A-Za-z0-9]+$'
);
```

### Matches

```text
user123
admin99
abc789
```

---

# Real-World Examples

## Example 1: Extract URLs from Text

```sql
SELECT REGEXP_SUBSTR(
    message,
    'https?://[^ ]+'
) AS url
FROM messages;
```

### Explanation

- Extracts URLs from text messages.
- Supports both HTTP and HTTPS links.

---

## Example 2: Validate Email Addresses

```sql
SELECT email
FROM users
WHERE REGEXP_LIKE(
    email,
    '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'
);
```

### Explanation

Ensures:

- Username exists
- Contains @ symbol
- Domain exists
- Valid extension exists

---

## Example 3: Clean Phone Numbers

```sql
SELECT REGEXP_REPLACE(
    phone_number,
    '[^0-9]',
    ''
) AS cleaned_number
FROM contacts;
```

### Before

```text
+91-98765-43210
(040)12345678
```

### After

```text
919876543210
04012345678
```

### Explanation

- Removes spaces, brackets, dashes, and symbols.
- Leaves only numeric digits.

---

## Example 4: Find Product Names Containing Digits

```sql
SELECT product_name
FROM products
WHERE REGEXP_LIKE(
    product_name,
    '[0-9]'
);
```

### Matches

```text
iPhone16
Galaxy25
SQL101
```

---

## Example 5: Extract Subdomains

```sql
SELECT REGEXP_SUBSTR(
    url,
    '^[^.]+'
) AS subdomain
FROM web_logs;
```

### Output

| URL | Subdomain |
| --- | --- |
| blog.google.com | blog |
| shop.amazon.com | shop |

### Explanation

Extracts everything before the first dot.

---

## Example 6: Validate Numeric Strings

```sql
SELECT record_id
FROM data_table
WHERE REGEXP_LIKE(
    field_name,
    '^[0-9]+$'
);
```

### Explanation

Returns records containing only digits.

---

# Regular Expression Use Cases

## Data Validation

Validate:

- Email addresses
- Phone numbers
- ZIP codes
- Usernames

Example:

```sql
REGEXP_LIKE(email, pattern)
```

---

## Data Cleaning

Remove:

- Special characters
- Extra spaces
- Unwanted symbols

Example:

```sql
REGEXP_REPLACE(phone, '[^0-9]', '')
```

---

## Data Extraction

Extract:

- Domains
- URLs
- IDs
- Hashtags

Example:

```sql
REGEXP_SUBSTR(email, '@[^.]+')
```

---

## Pattern Searching

Search records containing specific patterns.

Example:

```sql
SELECT *
FROM products
WHERE REGEXP_LIKE(product_name, '[0-9]');
```

---

# Advantages of Regular Expressions

- Powerful pattern matching.
- Reduces complex string manipulation.
- Improves data validation.
- Useful for cleaning large datasets.
- Supports advanced searching capabilities.

---

# Limitations of Regular Expressions

- Regex operations can be slower on large datasets.
- Complex patterns may reduce readability.
- Syntax varies slightly across database systems.
- Excessive regex usage can impact performance.

---

# Best Practices

- Keep patterns simple whenever possible.
- Use regex only when string functions are insufficient.
- Test regex patterns thoroughly.
- Avoid running regex operations on unnecessarily large datasets.
- Document complex regex patterns for maintainability.

---

# Regular Expressions vs String Functions

| Feature | String Functions | Regular Expressions |
| --- | --- | --- |
| Exact Text Search | Yes | Yes |
| Pattern Matching | Limited | Advanced |
| Validation | Limited | Excellent |
| Data Extraction | Basic | Advanced |
| Flexibility | Moderate | Very High |

---

# Conclusion

Regular Expressions in SQL provide a powerful way to search, validate, extract, and transform text data. Functions such as `REGEXP_LIKE()`, `REGEXP_REPLACE()`, and `REGEXP_SUBSTR()` allow developers to perform advanced text processing directly within SQL queries. When used appropriately, regex can significantly simplify data validation, cleaning, and extraction tasks while improving overall database efficiency.



###
