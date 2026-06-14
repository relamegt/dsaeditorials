# Temporary Tables in SQL

## Introduction

A temporary table is a special type of table that stores data for a limited period of time. Unlike regular tables, temporary tables are created to hold intermediate results during query execution, data processing, reporting, or complex calculations.

Temporary tables help developers work with temporary datasets without modifying permanent database tables.

## Why Use Temporary Tables?

Temporary tables are useful when:

- Storing intermediate query results.
- Simplifying complex SQL operations.
- Processing large amounts of data in multiple steps.
- Generating reports from temporary datasets.
- Avoiding changes to permanent tables.

## Creating a Temporary Table

The syntax for creating a temporary table varies slightly between database systems.

### MySQL

```sql
CREATE TEMPORARY TABLE TempTeam (
    MemberID INT,
    MemberName VARCHAR(100)
);
```

### SQL Server

```sql
CREATE TABLE #TempTeam (
    MemberID INT,
    MemberName VARCHAR(100)
);
```

## Inserting Data into a Temporary Table

```sql
INSERT INTO TempTeam
VALUES
(1, 'Akash Dangudubiyyapu'),
(2, 'Mohit Chandaluri'),
(3, 'Abhiram Gopisetti'),
(4, 'Adapa Hemesh');
```

## Viewing Data

```sql
SELECT * FROM TempTeam;
```

### Output

| MemberID | MemberName |
| --- | --- |
| 1 | Akash Dangudubiyyapu |
| 2 | Mohit Chandaluri |
| 3 | Abhiram Gopisetti |
| 4 | Adapa Hemesh |

## Types of Temporary Tables

Temporary tables are generally categorized into two types.

### 1. Local Temporary Tables

A local temporary table is accessible only within the session that created it.

In SQL Server, local temporary tables are created using a single hash (`#`) symbol.

```sql
CREATE TABLE #ProjectMembers (
    MemberID INT,
    MemberName VARCHAR(100)
);
```

### Characteristics

- Visible only to the current session.
- Automatically removed when the session ends.
- Cannot be accessed by other users or sessions.
- Suitable for session-specific operations.

## Example of a Local Temporary Table

```sql
CREATE TABLE #ProjectMembers (
    MemberID INT,
    MemberName VARCHAR(100)
);

INSERT INTO #ProjectMembers
VALUES
(1, 'Akash Dangudubiyyapu'),
(2, 'Mohit Chandaluri');

SELECT * FROM #ProjectMembers;
```

## 2. Global Temporary Tables

A global temporary table can be accessed by multiple sessions.

In SQL Server, global temporary tables are created using a double hash (`##`) symbol.

```sql
CREATE TABLE ##ProjectMembers (
    MemberID INT,
    MemberName VARCHAR(100)
);
```

### Characteristics

- Accessible to all active sessions.
- Remains available until the last session using it is closed.
- Useful when temporary data must be shared.
- Suitable for collaborative or multi-session processes.

## Example of a Global Temporary Table

```sql
CREATE TABLE ##ProjectMembers (
    MemberID INT,
    MemberName VARCHAR(100)
);

INSERT INTO ##ProjectMembers
VALUES
(1, 'Abhiram Gopisetti'),
(2, 'Adapa Hemesh');

SELECT * FROM ##ProjectMembers;
```

## Local vs Global Temporary Tables

| Feature | Local Temporary Table | Global Temporary Table |
| --- | --- | --- |
| Prefix | # | ## |
| Visibility | Current Session Only | All Sessions |
| Lifetime | Until Session Ends | Until Last Active Session Ends |
| Data Sharing | Not Allowed | Allowed |
| Common Use Case | Individual Processing | Shared Processing |

## Dropping a Temporary Table

A temporary table can be removed manually if it is no longer needed.

### MySQL

```sql
DROP TEMPORARY TABLE TempTeam;
```

### SQL Server

```sql
DROP TABLE #ProjectMembers;
```

## Advantages of Temporary Tables

- Improve query readability.
- Store intermediate processing results.
- Reduce complexity in large SQL scripts.
- Prevent accidental modification of permanent tables.
- Simplify report generation and data transformation tasks.

## Important Points

- Temporary tables are intended for short-term data storage.
- They are automatically removed after their lifetime expires.
- Different database systems implement temporary tables differently.
- Local temporary tables are session-specific.
- Global temporary tables can be shared across sessions.
- Temporary tables do not replace permanent database tables.

## Conclusion

Temporary tables provide an efficient way to store and process temporary data within SQL queries and database operations. Whether used for reporting, data transformation, or intermediate calculations, they help organize complex workflows while keeping permanent tables unchanged.



###
