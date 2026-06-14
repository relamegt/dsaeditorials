# SQL Query to Delete Duplicate Rows

## Introduction

Duplicate rows occur when multiple records contain the same data in one or more columns. These duplicates can lead to inaccurate reports, increased storage usage, and slower query performance.

Removing duplicate records helps maintain data quality and ensures that database operations produce accurate results.

## Why Do Duplicate Rows Occur?

Duplicate records can be introduced due to:

- Data import errors.
- Missing unique constraints.
- Multiple user submissions.
- Application bugs.
- Data migration issues.

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50)
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management'),
(2, 'Mohit Chandaluri', 'Content'),
(3, 'Mohit Chandaluri', 'Content'),
(4, 'Abhiram Gopisetti', 'Technical'),
(5, 'Adapa Hemesh', 'Database'),
(6, 'Abhiram Gopisetti', 'Technical');
```

View the records:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 3 | Mohit Chandaluri | Content |
| 4 | Abhiram Gopisetti | Technical |
| 5 | Adapa Hemesh | Database |
| 6 | Abhiram Gopisetti | Technical |

Notice that Mohit Chandaluri and Abhiram Gopisetti appear more than once with identical department information.

## Identifying Duplicate Rows

Before deleting duplicates, it is recommended to identify them.

### Example

```sql
SELECT MemberName,
       Department,
       COUNT(*) AS DuplicateCount
FROM TeamMembers
GROUP BY MemberName, Department
HAVING COUNT(*) > 1;
```

### Output

| MemberName | Department | DuplicateCount |
| --- | --- | --- |
| Mohit Chandaluri | Content | 2 |
| Abhiram Gopisetti | Technical | 2 |

## Method 1: Using GROUP BY and MIN()

This method keeps the record with the smallest ID and removes the remaining duplicates.

### Example

```sql
DELETE FROM TeamMembers
WHERE MemberID NOT IN (
    SELECT MIN(MemberID)
    FROM TeamMembers
    GROUP BY MemberName, Department
);
```

### Result

Only one record remains for each duplicate group.

## Method 2: Using ROW_NUMBER()

The `ROW_NUMBER()` function assigns a unique number to each row within a duplicate group.

### Example

```sql
WITH DuplicateRecords AS (
    SELECT MemberID,
           ROW_NUMBER() OVER (
               PARTITION BY MemberName, Department
               ORDER BY MemberID
           ) AS RowNum
    FROM TeamMembers
)
DELETE FROM TeamMembers
WHERE MemberID IN (
    SELECT MemberID
    FROM DuplicateRecords
    WHERE RowNum > 1
);
```

### How It Works

- Records are grouped by MemberName and Department.
- The first record receives RowNum = 1.
- Duplicate records receive RowNum values greater than 1.
- All duplicate records are deleted.

## Method 3: Using Common Table Expressions (CTEs)

A Common Table Expression can simplify duplicate removal queries.

### Example

```sql
WITH DuplicateRows AS (
    SELECT MemberID,
           ROW_NUMBER() OVER (
               PARTITION BY MemberName, Department
               ORDER BY MemberID
           ) AS RowNumber
    FROM TeamMembers
)
DELETE FROM TeamMembers
WHERE MemberID IN (
    SELECT MemberID
    FROM DuplicateRows
    WHERE RowNumber > 1
);
```

### Benefits

- Easier to read.
- Easier to maintain.
- Suitable for complex duplicate detection logic.

## Method 4: Using a Temporary Table

A temporary table can store only unique records before replacing the original data.

### Step 1: Create a Temporary Table

```sql
CREATE TEMPORARY TABLE UniqueMembers AS
SELECT *
FROM TeamMembers
WHERE MemberID IN (
    SELECT MIN(MemberID)
    FROM TeamMembers
    GROUP BY MemberName, Department
);
```

### Step 2: Remove Existing Records

```sql
DELETE FROM TeamMembers;
```

### Step 3: Insert Unique Records Back

```sql
INSERT INTO TeamMembers
SELECT *
FROM UniqueMembers;
```

### Step 4: Remove the Temporary Table

```sql
DROP TEMPORARY TABLE UniqueMembers;
```

## Method 5: Using DISTINCT

The `DISTINCT` keyword can retrieve unique records.

### Example

```sql
CREATE TABLE CleanTeamMembers AS
SELECT DISTINCT MemberName, Department
FROM TeamMembers;
```

This creates a new table containing only unique values.

## Verifying Duplicate Removal

After removing duplicates, verify the results.

```sql
SELECT *
FROM TeamMembers;
```

### Expected Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 4 | Abhiram Gopisetti | Technical |
| 5 | Adapa Hemesh | Database |

## Preventing Duplicate Rows

Instead of removing duplicates later, it is better to prevent them.

### Using UNIQUE Constraints

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    UNIQUE (MemberName, Department)
);
```

This prevents duplicate combinations from being inserted.

## Common Techniques Comparison

| Method | Suitable For | Complexity |
| --- | --- | --- |
| GROUP BY + MIN() | Simple duplicate removal | Easy |
| ROW_NUMBER() | Advanced duplicate handling | Medium |
| CTE | Readable and maintainable queries | Medium |
| Temporary Table | Large data cleanup operations | Medium |
| DISTINCT | Creating unique copies of data | Easy |

## Benefits of Removing Duplicates

- Improves data accuracy.
- Reduces storage usage.
- Improves query performance.
- Prevents reporting errors.
- Maintains database consistency.

## Important Points

- Duplicate records can affect business decisions and reports.
- Always identify duplicates before deleting them.
- Keep at least one valid record from each duplicate group.
- Use transactions when removing large numbers of records.
- Consider adding unique constraints to prevent future duplicates.

## Conclusion

Duplicate records can negatively impact database performance and data quality. SQL provides multiple techniques such as `GROUP BY`, `ROW_NUMBER()`, `CTE`, temporary tables, and `DISTINCT` to identify and remove duplicate rows effectively. Choosing the appropriate method depends on the database system, table size, and complexity of the duplicate records.



###
