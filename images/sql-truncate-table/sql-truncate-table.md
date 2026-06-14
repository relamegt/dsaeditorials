# SQL TRUNCATE TABLE

## Introduction

The SQL `TRUNCATE TABLE` statement is used to remove all records from a table while keeping the table structure intact. It is commonly used when you need to quickly clear large amounts of data without deleting the table itself.

Unlike the `DELETE` statement, `TRUNCATE TABLE` removes all rows at once, making it a faster option for emptying tables.

## What Does TRUNCATE TABLE Do?

When a table is truncated:

- All rows in the table are removed.
- The table structure remains unchanged.
- Existing columns, indexes, and constraints are preserved.
- The table can immediately be reused for new data.
- The operation is generally faster than deleting rows individually.

## Syntax

```sql
TRUNCATE TABLE table_name;
```

### Parameters

| Parameter | Description |
| --- | --- |
| table_name | Name of the table whose records should be removed |

## Creating a Sample Database

Create a database for the demonstration:

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating the TeamMembers Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(100)
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management'),
(2, 'Mohit Chandaluri', 'Content'),
(3, 'Abhiram Gopisetti', 'Technical'),
(4, 'Adapa Hemesh', 'Database');
```

Display the records:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 3 | Abhiram Gopisetti | Technical |
| 4 | Adapa Hemesh | Database |

## Truncating the Table

To remove all records from the table:

```sql
TRUNCATE TABLE TeamMembers;
```

After execution, all rows are deleted, but the table itself remains available.

## Checking the Table Contents

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| No Records Found |  |  |

The table exists, but all stored data has been removed.

## Verifying the Table Structure

You can inspect the table structure using:

```sql
DESC TeamMembers;
```

### Output

| Field | Type |
| --- | --- |
| MemberID | INT |
| MemberName | VARCHAR(100) |
| Department | VARCHAR(100) |

The structure remains unchanged even after truncation.

## TRUNCATE vs DELETE

| Feature | TRUNCATE | DELETE |
| --- | --- | --- |
| Removes All Rows | Yes | Yes |
| Supports WHERE Clause | No | Yes |
| Removes Rows Individually | No | Yes |
| Faster for Large Tables | Yes | No |
| Preserves Table Structure | Yes | Yes |

## Important Points

- `TRUNCATE TABLE` removes all records from a table.
- The table structure, indexes, and constraints remain intact.
- A `WHERE` clause cannot be used with `TRUNCATE`.
- It is generally faster than `DELETE` for removing large volumes of data.
- The table can immediately be used again for inserting new records.
- Use this command carefully because all existing data in the table will be removed.

## Conclusion

The SQL `TRUNCATE TABLE` statement is an efficient way to clear all records from a table while preserving its structure. It is particularly useful for large tables where removing data quickly is important. Since the table definition remains unchanged, new data can be inserted immediately after truncation.



###
