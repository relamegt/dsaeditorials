# SQL WHERE Clause

## Introduction

The SQL `WHERE` clause is used to filter records based on specified conditions. It allows you to retrieve, update, or delete only the rows that satisfy a particular criterion instead of affecting the entire table.

The `WHERE` clause is one of the most frequently used components in SQL because it helps users work with specific data efficiently.

## Why Use the WHERE Clause?

The `WHERE` clause helps you:

- Retrieve only the required records.
- Update specific rows in a table.
- Delete selected records safely.
- Apply filtering conditions to queries.
- Improve query accuracy and performance.

## Basic Syntax

### Using WHERE with SELECT

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Using WHERE with UPDATE

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

### Using WHERE with DELETE

```sql
DELETE FROM table_name
WHERE condition;
```

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    Age INT,
    ExperienceYears INT
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 24, 5),
(2, 'Mohit Chandaluri', 'Content', 23, 3),
(3, 'Abhiram Gopisetti', 'Technical', 24, 4),
(4, 'Adapa Hemesh', 'Database', 22, 2),
(5, 'Kiran Kumar', 'Technical', 21, 1);
```

View the table:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | Age | ExperienceYears |
| --- | --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 24 | 5 |
| 2 | Mohit Chandaluri | Content | 23 | 3 |
| 3 | Abhiram Gopisetti | Technical | 24 | 4 |
| 4 | Adapa Hemesh | Database | 22 | 2 |
| 5 | Kiran Kumar | Technical | 21 | 1 |

## Using WHERE with Equality Operator

Retrieve members whose age is 24.

```sql
SELECT *
FROM TeamMembers
WHERE Age = 24;
```

### Output

| MemberID | MemberName | Age |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | 24 |
| 3 | Abhiram Gopisetti | 24 |

## Using Comparison Operators

Retrieve members older than 22 years.

```sql
SELECT MemberID,
       MemberName,
       Age
FROM TeamMembers
WHERE Age > 22;
```

### Output

| MemberID | MemberName | Age |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | 24 |
| 2 | Mohit Chandaluri | 23 |
| 3 | Abhiram Gopisetti | 24 |

## WHERE with AND Operator

Retrieve Technical team members who are older than 22.

```sql
SELECT *
FROM TeamMembers
WHERE Department = 'Technical'
AND Age > 22;
```

### Output

| MemberID | MemberName | Department | Age |
| --- | --- | --- | --- |
| 3 | Abhiram Gopisetti | Technical | 24 |

## WHERE with OR Operator

Retrieve members who belong to Management or Database departments.

```sql
SELECT *
FROM TeamMembers
WHERE Department = 'Management'
OR Department = 'Database';
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 4 | Adapa Hemesh | Database |

## WHERE with NOT Operator

Retrieve members who are not in the Technical department.

```sql
SELECT *
FROM TeamMembers
WHERE NOT Department = 'Technical';
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 4 | Adapa Hemesh | Database |

## WHERE with BETWEEN

The `BETWEEN` operator filters records within a specified range, including both boundary values.

### Example

Retrieve members whose age is between 22 and 24.

```sql
SELECT *
FROM TeamMembers
WHERE Age BETWEEN 22 AND 24;
```

### Output

| MemberID | MemberName | Age |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | 24 |
| 2 | Mohit Chandaluri | 23 |
| 3 | Abhiram Gopisetti | 24 |
| 4 | Adapa Hemesh | 22 |

## WHERE with IN

The `IN` operator allows multiple values to be specified in a single condition.

### Example

Retrieve members whose age is either 21 or 24.

```sql
SELECT MemberName
FROM TeamMembers
WHERE Age IN (21, 24);
```

### Output

| MemberName |
| --- |
| Akash Dangudubiyyapu |
| Abhiram Gopisetti |
| Kiran Kumar |

## WHERE with LIKE

The `LIKE` operator searches for patterns within text values.

### Example 1: Names Starting with A

```sql
SELECT *
FROM TeamMembers
WHERE MemberName LIKE 'A%';
```

### Output

| MemberName |
| --- |
| Akash Dangudubiyyapu |
| Abhiram Gopisetti |
| Adapa Hemesh |

### Example 2: Names Ending with i

```sql
SELECT *
FROM TeamMembers
WHERE MemberName LIKE '%i';
```

### Example 3: Single Character Wildcard

```sql
SELECT *
FROM TeamMembers
WHERE MemberName LIKE '_o%';
```

### Wildcards

| Symbol | Description |
| --- | --- |
| % | Any number of characters |
| _ | Exactly one character |

## WHERE with NULL Values

To find NULL values, use `IS NULL`.

```sql
SELECT *
FROM TeamMembers
WHERE Department IS NULL;
```

To find non-NULL values:

```sql
SELECT *
FROM TeamMembers
WHERE Department IS NOT NULL;
```

## Using WHERE with UPDATE

Update Mohit Chandaluri's experience.

```sql
UPDATE TeamMembers
SET ExperienceYears = 4
WHERE MemberID = 2;
```

Only the specified record is updated.

## Using WHERE with DELETE

Delete a specific record.

```sql
DELETE FROM TeamMembers
WHERE MemberID = 5;
```

Only the matching row is removed.

## Comparison Operators Used with WHERE

| Operator | Description |
| --- | --- |
| = | Equal To |
| &gt; | Greater Than |
| &gt;= | Greater Than or Equal To |
| &lt; | Less Than |
| &lt;= | Less Than or Equal To |
| &lt;&gt; | Not Equal To |
| != | Not Equal To (supported by many databases) |
| BETWEEN | Within a range |
| IN | Matches multiple values |
| LIKE | Pattern matching |
| IS NULL | Checks for NULL values |

## Best Practices

- Always verify conditions before running UPDATE or DELETE queries.
- Use indexes on frequently filtered columns.
- Avoid unnecessary wildcard searches on large tables.
- Use meaningful filtering conditions for better performance.
- Test complex conditions using SELECT before modifying data.

## Important Points

- The `WHERE` clause filters rows based on conditions.
- It can be used with `SELECT`, `UPDATE`, and `DELETE`.
- Multiple conditions can be combined using `AND`, `OR`, and `NOT`.
- Operators such as `BETWEEN`, `IN`, and `LIKE` provide advanced filtering options.
- Omitting the `WHERE` clause in UPDATE or DELETE affects all rows.

## Conclusion

The SQL `WHERE` clause is an essential filtering mechanism that allows users to work with specific records instead of entire tables. By combining comparison operators, logical operators, and pattern-matching techniques, developers can retrieve, update, and delete data accurately and efficiently.



###
