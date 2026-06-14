# SQL String Functions

## Introduction

SQL String Functions are built-in functions used to manipulate, analyze, and format text data stored in a database. These functions help perform operations such as combining strings, extracting substrings, converting case, finding character positions, and cleaning text values.

String functions are commonly used in applications that store names, addresses, email IDs, product descriptions, and other text-based information.

### Why Use String Functions?

SQL String Functions help you:

- Manipulate and format text data efficiently.
- Combine multiple strings into a single value.
- Extract specific portions of text.
- Convert text into uppercase or lowercase.
- Clean unwanted spaces or characters.
- Improve data consistency and readability.

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

## Creating a Sample Table

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Email VARCHAR(100),
    City VARCHAR(50)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 'akash@alphaknowledge.in', 'Vijayawada'),
(2, 'Mohit', 'mohit@alphaknowledge.in', 'Hyderabad'),
(3, 'Abhiram', 'abhiram@alphaknowledge.in', 'Guntur'),
(4, 'Hemesh', 'hemesh@alphaknowledge.in', 'Chennai'),
(5, 'Hemanth', 'hemanth@alphaknowledge.in', 'Bangalore'),
(6, 'Akhil', 'akhil@alphaknowledge.in', 'Visakhapatnam');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | City |
| --- | --- | --- | --- |
| 1 | Akash | [akash@alphaknowledge.in](mailto:akash@alphaknowledge.in) | Vijayawada |
| 2 | Mohit | [mohit@alphaknowledge.in](mailto:mohit@alphaknowledge.in) | Hyderabad |
| 3 | Abhiram | [abhiram@alphaknowledge.in](mailto:abhiram@alphaknowledge.in) | Guntur |
| 4 | Hemesh | [hemesh@alphaknowledge.in](mailto:hemesh@alphaknowledge.in) | Chennai |
| 5 | Hemanth | [hemanth@alphaknowledge.in](mailto:hemanth@alphaknowledge.in) | Bangalore |
| 6 | Akhil | [akhil@alphaknowledge.in](mailto:akhil@alphaknowledge.in) | Visakhapatnam |

---

## Example 1: CONCAT()

Combine first and last name values.

```sql
SELECT CONCAT('Akash', ' ', 'Kumar') AS FullName;
```

### Output

| FullName |
| --- |
| Akash Kumar |

### Explanation

- CONCAT() combines multiple strings into a single string.
- Useful for generating full names and formatted text.

---

## Example 2: CHAR_LENGTH()

Find the number of characters in a string.

```sql
SELECT CHAR_LENGTH('AlphaKnowledge') AS LengthOfText;
```

### Output

| LengthOfText |
| --- |
| 14 |

### Explanation

- Returns the number of characters in the string.
- Useful for validating text length.

---

## Example 3: UPPER()

Convert text to uppercase.

```sql
SELECT UPPER('akash') AS UpperText;
```

### Output

| UpperText |
| --- |
| AKASH |

### Explanation

- Converts all characters to uppercase.
- Useful for standardizing text comparisons.

---

## Example 4: LOWER()

Convert text to lowercase.

```sql
SELECT LOWER('MOHIT') AS LowerText;
```

### Output

| LowerText |
| --- |
| mohit |

### Explanation

- Converts all characters to lowercase.
- Helps maintain consistent data formatting.

---

## Example 5: LENGTH()

Find string length in bytes.

```sql
SELECT LENGTH('Abhiram') AS LengthInBytes;
```

### Output

| LengthInBytes |
| --- |
| 7 |

### Explanation

- Returns the size of the string in bytes.
- Useful when working with multi-byte character sets.

---

## Example 6: REPLACE()

Replace a word inside a string.

```sql
SELECT REPLACE('Alpha Knowledge', 'Knowledge', 'Learning') AS UpdatedText;
```

### Output

| UpdatedText |
| --- |
| Alpha Learning |

### Explanation

- Replaces one substring with another.
- Useful for correcting or formatting text data.

---

## Example 7: SUBSTRING()

Extract a portion of a string.

```sql
SELECT SUBSTRING('alphaknowledge.in', 1, 5) AS ExtractedText;
```

### Output

| ExtractedText |
| --- |
| alpha |

### Explanation

- Extracts characters from a specified position.
- Useful for parsing email addresses and codes.

---

## Example 8: LEFT()

Retrieve characters from the left side.

```sql
SELECT LEFT('AlphaKnowledge', 5) AS LeftText;
```

### Output

| LeftText |
| --- |
| Alpha |

### Explanation

- Returns the specified number of characters from the left.

---

## Example 9: RIGHT()

Retrieve characters from the right side.

```sql
SELECT RIGHT('AlphaKnowledge', 9) AS RightText;
```

### Output

| RightText |
| --- |
| Knowledge |

### Explanation

- Returns characters from the end of the string.

---

## Example 10: INSTR()

Find the position of a substring.

```sql
SELECT INSTR('AlphaKnowledge', 'Know') AS PositionValue;
```

### Output

| PositionValue |
| --- |
| 6 |

### Explanation

- Returns the starting position of a substring.
- Returns 0 if not found.

---

## Example 11: TRIM()

Remove leading and trailing spaces.

```sql
SELECT TRIM('   Akash   ') AS CleanText;
```

### Output

| CleanText |
| --- |
| Akash |

### Explanation

- Removes extra spaces around text values.
- Commonly used for data cleaning.

---

## Example 12: REVERSE()

Reverse a string.

```sql
SELECT REVERSE('Akhil') AS ReversedText;
```

### Output

| ReversedText |
| --- |
| lihkA |

### Explanation

- Reverses all characters in the string.

---

## Example 13: ASCII()

Return the ASCII value of a character.

```sql
SELECT ASCII('A') AS ASCIIValue;
```

### Output

| ASCIIValue |
| --- |
| 65 |

### Explanation

- Returns the numeric ASCII code of a character.

---

## Example 14: CONCAT_WS()

Concatenate strings using a separator.

```sql
SELECT CONCAT_WS('-', 'Akash', 'Mohit', 'Abhiram') AS CombinedNames;
```

### Output

| CombinedNames |
| --- |
| Akash-Mohit-Abhiram |

### Explanation

- Adds a separator between multiple strings automatically.

---

## Example 15: FIND_IN_SET()

Find a value inside a comma-separated list.

```sql
SELECT FIND_IN_SET('Mohit', 'Akash,Mohit,Abhiram,Hemesh');
```

### Output

| FIND_IN_SET |
| --- |
| 2 |

### Explanation

- Returns the position of the searched value.

---

## Example 16: LPAD()

Pad text from the left.

```sql
SELECT LPAD('123', 6, '0') AS PaddedText;
```

### Output

| PaddedText |
| --- |
| 000123 |

### Explanation

- Adds characters to the left until the required length is reached.

---

## Example 17: RPAD()

Pad text from the right.

```sql
SELECT RPAD('ABC', 6, '0') AS PaddedText;
```

### Output

| PaddedText |
| --- |
| ABC000 |

### Explanation

- Adds characters to the right side of a string.

---

## Example 18: REPEAT()

Repeat a string multiple times.

```sql
SELECT REPEAT('SQL ', 3) AS RepeatedText;
```

### Output

| RepeatedText |
| --- |
| SQL SQL SQL |

### Explanation

- Repeats the specified string a given number of times.

---

## Example 19: POSITION()

Find character position in a string.

```sql
SELECT POSITION('K' IN 'AlphaKnowledge') AS CharacterPosition;
```

### Output

| CharacterPosition |
| --- |
| 6 |

### Explanation

- Returns the position of the specified character.

---

## Example 20: RTRIM()

Remove trailing spaces.

```sql
SELECT RTRIM('Hemesh     ') AS TrimmedText;
```

### Output

| TrimmedText |
| --- |
| Hemesh |

### Explanation

- Removes spaces from the right side only.

---

## Common Use Cases

### Generate Full Names

```sql
SELECT CONCAT(StudentName, ' - Student')
FROM Students;
```

### Extract Email Usernames

```sql
SELECT SUBSTRING(Email, 1, INSTR(Email, '@') - 1)
FROM Students;
```

### Convert Names to Uppercase

```sql
SELECT UPPER(StudentName)
FROM Students;
```

### Remove Extra Spaces

```sql
SELECT TRIM(StudentName)
FROM Students;
```

---

## Best Practices

- Use string functions only when required.
- Avoid excessive string operations on large datasets.
- Use indexes where possible for better performance.
- Clean user input using TRIM() and REPLACE().
- Standardize text using UPPER() or LOWER().

---

## Important Points

- String functions manipulate and format text values.
- CONCAT() combines strings.
- SUBSTRING() extracts text portions.
- UPPER() and LOWER() modify letter case.
- TRIM() removes unwanted spaces.
- REPLACE() substitutes text values.
- POSITION() and INSTR() locate characters or substrings.

---

## Conclusion

SQL String Functions provide powerful tools for handling textual data within a database. They simplify tasks such as combining strings, extracting information, formatting values, cleaning data, and performing text analysis. Mastering these functions helps create cleaner databases, more efficient queries, and better reporting solutions.



###
