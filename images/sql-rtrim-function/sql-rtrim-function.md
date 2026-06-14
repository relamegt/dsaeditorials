# SQL RTRIM() Function

## Introduction

The SQL `RTRIM()` function is a string function used to remove unwanted characters or spaces from the right side (trailing end) of a string. It is commonly used in data cleaning and formatting operations to ensure consistency in stored and displayed text values.

The function removes only trailing characters and does not affect leading spaces or characters at the beginning of the string.

---

## Why Use RTRIM()?

The `RTRIM()` function helps you:

- Remove unwanted trailing spaces.
- Clean imported or user-entered data.
- Standardize text values.
- Improve string comparisons.
- Prepare data for reporting and display.

---

## Syntax

### Basic Syntax

```sql
RTRIM(input_text)
```

### Removing Specific Characters

```sql
RTRIM(input_text, trim_characters)
```

### Using a Column

```sql
SELECT RTRIM(column_name)
FROM table_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| RTRIM() | Removes trailing characters from the right side |
| input_text | Text value to trim |
| trim_characters | Optional characters to remove |
| column_name | Column containing text data |

---

## Basic Example

Remove trailing spaces from a string.

```sql
SELECT RTRIM('Hello World     ') AS TrimmedText;
```

### Output

| TrimmedText |
| --- |
| Hello World |

### Explanation

- Removes extra spaces from the end of the string.
- Preserves the original text content.

---

## Creating a Sample Table

```sql
CREATE TABLE Users (
    Name VARCHAR(50)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Users (Name)
VALUES
('Akash     '),
('Mohit      '),
('Abhiram       '),
('Sai      '),
('Hemesh      ');
```

Display the table:

```sql
SELECT * FROM Users;
```

### Output

| Name |
| --- |
| Akash |
| Mohit |
| Abhiram |
| Sai |
| Hemesh |

---

## Example 1: Remove Trailing Spaces from a String

```sql
SELECT
'          Geeks for Geeks          ' AS BeforeRTRIM,
RTRIM('          Geeks for Geeks          ') AS AfterRTRIM;
```

### Output

| BeforeRTRIM | AfterRTRIM |
| --- | --- |
| Geeks for Geeks | Geeks for Geeks |

### Explanation

- Original string contains spaces on both sides.
- RTRIM() removes only the right-side spaces.
- Leading spaces remain unchanged.

---

## Example 2: Remove Specific Characters

```sql
SELECT RTRIM('SQL*****', '*') AS TrimmedText;
```

### Output

| TrimmedText |
| --- |
| SQL |

### Explanation

- Removes all `*` characters from the end.
- Stops trimming when a different character is encountered.

---

## Example 3: Remove Multiple Trailing Characters

```sql
SELECT RTRIM('Database###', '#') AS TrimmedText;
```

### Output

| TrimmedText |
| --- |
| Database |

### Explanation

- Removes all trailing hash (`#`) characters.
- Returns the cleaned string.

---

## Example 4: Apply RTRIM() on a Table Column

```sql
SELECT
Name AS OriginalName,
RTRIM(Name) AS TrimmedName
FROM Users;
```

### Output

| OriginalName | TrimmedName |
| --- | --- |
| Akash | Akash |
| Mohit | Mohit |
| Abhiram | Abhiram |
| Sai | Sai |
| Hemesh | Hemesh |

### Explanation

- Removes trailing spaces from every row.
- Keeps the original values unchanged in the table.

---

## Example 5: Store Cleaned Data

```sql
UPDATE Users
SET Name = RTRIM(Name);
```

### Explanation

- Permanently removes trailing spaces.
- Updates the values stored in the table.

---

## Example 6: Using RTRIM() with CONCAT()

```sql
SELECT CONCAT(RTRIM('Hello     '), ' World') AS Result;
```

### Output

| Result |
| --- |
| Hello World |

### Explanation

- Removes trailing spaces first.
- Then concatenates another string.

---

## Example 7: Using RTRIM() with Variables

```sql
DELIMITER //

CREATE PROCEDURE RTRIM_Example()
BEGIN

    DECLARE input_string VARCHAR(20);

    SET input_string = 'Hello          ';

    SELECT CONCAT(
        RTRIM(input_string),
        ' World'
    ) AS Result;

END //

DELIMITER ;

CALL RTRIM_Example();
```

### Output

| Result |
| --- |
| Hello World |

### Explanation

- Creates a variable containing trailing spaces.
- Removes the spaces using RTRIM().
- Combines the result with another string.

---

## Example 8: Compare Values After Trimming

```sql
SELECT *
FROM Users
WHERE RTRIM(Name) = 'Akash';
```

### Explanation

- Ignores trailing spaces during comparison.
- Helps find matching values accurately.

---

## RTRIM() vs LTRIM() vs TRIM()

| Function | Removes |
| --- | --- |
| RTRIM() | Trailing spaces/characters |
| LTRIM() | Leading spaces/characters |
| TRIM() | Both leading and trailing spaces/characters |

### Example

```sql
SELECT
LTRIM('     SQL') AS LeftTrim,
RTRIM('SQL     ') AS RightTrim,
TRIM('     SQL     ') AS BothTrim;
```

### Output

| LeftTrim | RightTrim | BothTrim |
| --- | --- | --- |
| SQL | SQL | SQL |

---

## Common Use Cases

### Clean Imported Data

```sql
SELECT RTRIM(CustomerName)
FROM Customers;
```

### Remove Trailing Spaces Before Comparison

```sql
SELECT *
FROM Customers
WHERE RTRIM(CustomerName) = 'John';
```

### Standardize Report Output

```sql
SELECT RTRIM(ProductName)
FROM Products;
```

### Clean Data Before Export

```sql
UPDATE Products
SET ProductName = RTRIM(ProductName);
```

---

## Best Practices

- Use RTRIM() when data contains unnecessary trailing spaces.
- Combine RTRIM() with LTRIM() or TRIM() for complete cleanup.
- Clean imported files before processing.
- Apply trimming before string comparisons when data quality is uncertain.
- Store cleaned values whenever possible to avoid repeated processing.

---

## Important Points

- RTRIM() removes characters only from the right side.
- Leading spaces remain unchanged.
- It works with strings, variables, and table columns.
- Commonly used in data cleaning and reporting.
- Supported by major databases such as SQL Server, MySQL, Oracle, PostgreSQL, and Azure SQL.

---

## Conclusion

The SQL `RTRIM()` function is a useful string function for removing unwanted trailing spaces or characters from text values. It helps maintain clean and standardized data, improves comparison accuracy, and ensures consistent formatting across reports and applications. When dealing with imported or user-entered text data, `RTRIM()` is an essential tool for efficient data cleaning.



###
