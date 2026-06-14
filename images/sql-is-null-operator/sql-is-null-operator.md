# SQL IS NULL Operator

## Introduction

The SQL `IS NULL` operator is used to check whether a column contains a NULL value. A NULL value represents missing, unknown, or unavailable data in a database.

Since NULL is not equal to zero, an empty string, or any other value, it cannot be compared using standard comparison operators such as `=` or `!=`. Instead, SQL provides the `IS NULL` operator specifically for checking NULL values.

## Why Use IS NULL?

The `IS NULL` operator helps you:

- Identify missing or incomplete data.
- Filter records containing NULL values.
- Count rows with missing values.
- Update NULL values with default values.
- Delete records containing NULL values.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name IS NULL;
```

### Syntax Components

| Component | Description |
| --- | --- |
| IS NULL | Checks whether a value is NULL |
| column_name | Column to be checked |
| table_name | Table containing the data |
| WHERE | Filters records based on the condition |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Sample Table

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Email VARCHAR(100),
    CodingScore INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 'akash@gmail.com', 95),
(2, 'Mohit', NULL, 88),
(3, 'Abhiram', 'abhiram@gmail.com', NULL),
(4, 'Hemesh', NULL, NULL),
(5, 'Sai', 'sai@gmail.com', 92);
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | CodingScore |
| --- | --- | --- | --- |
| 1 | Akash | [akash@gmail.com](mailto:akash@gmail.com) | 95 |
| 2 | Mohit | NULL | 88 |
| 3 | Abhiram | [abhiram@gmail.com](mailto:abhiram@gmail.com) | NULL |
| 4 | Hemesh | NULL | NULL |
| 5 | Sai | [sai@gmail.com](mailto:sai@gmail.com) | 92 |

---

## Example 1: IS NULL with WHERE Clause

Retrieve students whose email address is missing.

```sql
SELECT *
FROM Students
WHERE Email IS NULL;
```

### Output

| StudentID | StudentName | Email |
| --- | --- | --- |
| 2 | Mohit | NULL |
| 4 | Hemesh | NULL |

### Explanation

- The query checks whether the Email column contains NULL values.
- Only records with missing email addresses are returned.

---

## Example 2: IS NULL with Multiple Columns

Retrieve students whose email or coding score is NULL.

```sql
SELECT *
FROM Students
WHERE Email IS NULL
OR CodingScore IS NULL;
```

### Output

| StudentID | StudentName | Email | CodingScore |
| --- | --- | --- | --- |
| 2 | Mohit | NULL | 88 |
| 3 | Abhiram | [abhiram@gmail.com](mailto:abhiram@gmail.com) | NULL |
| 4 | Hemesh | NULL | NULL |

### Explanation

- The query checks two columns.
- Records are returned if either Email or CodingScore contains NULL.

---

## Example 3: IS NULL with COUNT()

Count how many students have a NULL coding score.

```sql
SELECT COUNT(*) AS StudentsWithoutScore
FROM Students
WHERE CodingScore IS NULL;
```

### Output

| StudentsWithoutScore |
| --- |
| 2 |

### Explanation

- COUNT(*) counts all filtered rows.
- Only rows with NULL CodingScore values are considered.

---

## Example 4: IS NULL with UPDATE Statement

Update all missing email addresses with a default value.

```sql
UPDATE Students
SET Email = 'default@gmail.com'
WHERE Email IS NULL;
```

Verify the changes:

```sql
SELECT *
FROM Students;
```

### Output

| StudentID | StudentName | Email |
| --- | --- | --- |
| 1 | Akash | [akash@gmail.com](mailto:akash@gmail.com) |
| 2 | Mohit | [default@gmail.com](mailto:default@gmail.com) |
| 3 | Abhiram | [abhiram@gmail.com](mailto:abhiram@gmail.com) |
| 4 | Hemesh | [default@gmail.com](mailto:default@gmail.com) |
| 5 | Sai | [sai@gmail.com](mailto:sai@gmail.com) |

### Explanation

- UPDATE modifies only rows where Email is NULL.
- Missing email addresses are replaced with a default value.

---

## Example 5: IS NULL with DELETE Statement

Delete students whose coding score is NULL.

```sql
DELETE FROM Students
WHERE CodingScore IS NULL;
```

Verify the remaining records:

```sql
SELECT *
FROM Students;
```

### Output

| StudentID | StudentName | CodingScore |
| --- | --- | --- |
| 1 | Akash | 95 |
| 2 | Mohit | 88 |
| 5 | Sai | 92 |

### Explanation

- Records with NULL coding scores are removed.
- Only rows containing valid scores remain.

---

## Example 6: IS NULL with AND Condition

Retrieve students whose email and coding score are both NULL.

```sql
SELECT *
FROM Students
WHERE Email IS NULL
AND CodingScore IS NULL;
```

### Output

| StudentID | StudentName |
| --- | --- |
| 4 | Hemesh |

### Explanation

- Both conditions must be TRUE.
- Only Hemesh has NULL values in both columns.

---

## Example 7: IS NULL with ORDER BY

Display students with missing email addresses sorted by name.

```sql
SELECT *
FROM Students
WHERE Email IS NULL
ORDER BY StudentName;
```

### Output

| StudentID | StudentName |
| --- | --- |
| Hemesh |  |
| Mohit |  |

### Explanation

- IS NULL filters records with missing emails.
- ORDER BY sorts the filtered records alphabetically.

---

## Difference Between NULL, Zero, and Empty String

| Value | Meaning |
| --- | --- |
| NULL | Missing or unknown value |
| 0 | Numeric value zero |
| '' | Empty string |
| Space (' ') | Blank character |

### Example

```sql
SELECT *
FROM Students
WHERE Email IS NULL;
```

This query returns only rows where Email is NULL, not rows containing empty strings.

---

## Common Use Cases

### Find Missing Email Addresses

```sql
SELECT *
FROM Users
WHERE Email IS NULL;
```

### Find Products Without Prices

```sql
SELECT *
FROM Products
WHERE Price IS NULL;
```

### Count Missing Phone Numbers

```sql
SELECT COUNT(*)
FROM Customers
WHERE PhoneNumber IS NULL;
```

### Delete Incomplete Records

```sql
DELETE FROM Orders
WHERE DeliveryDate IS NULL;
```

---

## Best Practices

- Always use IS NULL instead of = NULL.
- Use IS NOT NULL when checking for existing values.
- Handle NULL values carefully in calculations.
- Validate important fields during data entry.
- Replace unnecessary NULL values with meaningful defaults when appropriate.

---

## Important Points

- NULL represents missing or unknown data.
- NULL is not equal to zero or an empty string.
- Standard comparison operators cannot be used with NULL.
- IS NULL is used to identify NULL values.
- IS NULL can be used with SELECT, UPDATE, and DELETE statements.
- Aggregate functions such as COUNT(column) ignore NULL values.

---

## Conclusion

The SQL `IS NULL` operator is essential for working with missing or unknown data in a database. It allows developers to identify, count, update, and remove records containing NULL values. Understanding how NULL behaves and using IS NULL correctly helps maintain data quality and ensures accurate query results.



###
