# Dynamic SQL

## Introduction

Dynamic SQL is a technique in which SQL statements are created and executed at runtime rather than being written as fixed queries. Instead of hardcoding table names, column names, conditions, or sorting options, a query can be generated dynamically based on user input, application logic, or business requirements.

Dynamic SQL is widely used in database-driven applications where queries need to change according to different scenarios.

## Why Use Dynamic SQL?

Dynamic SQL is useful when:

- Table names are determined at runtime.
- Column names are selected dynamically.
- Search conditions vary based on user input.
- Reports require flexible filtering and sorting.
- Database objects are created or managed programmatically.

## Static SQL vs Dynamic SQL

| Feature | Static SQL | Dynamic SQL |
| --- | --- | --- |
| Query Definition | Written before execution | Generated during execution |
| Flexibility | Limited | Highly Flexible |
| Performance | Faster | Slightly Slower |
| Compilation | Precompiled | Compiled at Runtime |
| User-Driven Queries | Limited | Supported |
| Maintenance | Easier | More Complex |

## Basic Syntax

In SQL Server, Dynamic SQL is commonly executed using `sp_executesql`.

```sql
EXEC sp_executesql N'SELECT * FROM TeamMembers';
```

The `N` prefix indicates that the string is treated as Unicode.

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
(3, 'Abhiram Gopisetti', 'Technical'),
(4, 'Adapa Hemesh', 'Database');
```

## Steps to Create Dynamic SQL

### Step 1: Declare Variables

```sql
DECLARE @TableName NVARCHAR(100);
DECLARE @Query NVARCHAR(MAX);
```

### Step 2: Assign Values

```sql
SET @TableName = N'TeamMembers';
```

### Step 3: Build the Query

```sql
SET @Query =
N'SELECT * FROM ' + @TableName;
```

### Step 4: Execute the Query

```sql
EXEC sp_executesql @Query;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 3 | Abhiram Gopisetti | Technical |
| 4 | Adapa Hemesh | Database |

## Dynamic SQL with Table Names

Sometimes the table name is determined at runtime.

### Example

```sql
DECLARE @TableName NVARCHAR(100);
DECLARE @SQL NVARCHAR(MAX);

SET @TableName = N'TeamMembers';

SET @SQL =
N'SELECT * FROM ' + QUOTENAME(@TableName);

EXEC sp_executesql @SQL;
```

### Why Use QUOTENAME?

`QUOTENAME()` helps prevent errors and reduces the risk of SQL injection when working with object names.

## Dynamic SQL with WHERE Conditions

Conditions can also be generated dynamically.

### Example

```sql
DECLARE @Department NVARCHAR(50);
DECLARE @SQL NVARCHAR(MAX);

SET @Department = N'Technical';

SET @SQL =
N'SELECT * FROM TeamMembers
WHERE Department = @Dept';

EXEC sp_executesql
@SQL,
N'@Dept NVARCHAR(50)',
@Dept = @Department;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 3 | Abhiram Gopisetti | Technical |

## Dynamic SQL with ORDER BY

Sorting options can be selected dynamically.

### Example

```sql
DECLARE @SortColumn NVARCHAR(100);
DECLARE @SQL NVARCHAR(MAX);

SET @SortColumn = N'MemberName';

SET @SQL =
N'SELECT * FROM TeamMembers
ORDER BY ' + QUOTENAME(@SortColumn);

EXEC sp_executesql @SQL;
```

The results are sorted according to the selected column.

## Dynamic SQL for Multiple Filters

### Example

```sql
DECLARE @Department NVARCHAR(50);
DECLARE @SQL NVARCHAR(MAX);

SET @Department = N'Content';

SET @SQL =
N'SELECT *
FROM TeamMembers
WHERE Department = @Dept';

EXEC sp_executesql
@SQL,
N'@Dept NVARCHAR(50)',
@Dept = @Department;
```

This allows different filter values to be supplied at runtime.

## Dynamic SQL in Stored Procedures

Dynamic SQL is often used inside stored procedures.

### Example

```sql
CREATE PROCEDURE GetTeamData
    @TableName NVARCHAR(100)
AS
BEGIN
    DECLARE @SQL NVARCHAR(MAX);

    SET @SQL =
    N'SELECT * FROM '
    + QUOTENAME(@TableName);

    EXEC sp_executesql @SQL;
END;
```

Execute the procedure:

```sql
EXEC GetTeamData 'TeamMembers';
```

## Advantages of Dynamic SQL

### Flexibility

Queries can change based on runtime requirements.

### Reusability

The same logic can work with multiple tables and conditions.

### Dynamic Filtering

Supports user-defined searches and reports.

### Reduced Code Duplication

A single query template can handle multiple scenarios.

## Disadvantages of Dynamic SQL

### Performance Overhead

Queries must be parsed and compiled during execution.

### Increased Complexity

Debugging dynamically generated queries can be difficult.

### Security Risks

Improper handling of user input can lead to SQL injection attacks.

### Maintenance Challenges

Large dynamic queries may become difficult to manage.

## Preventing SQL Injection

Unsafe Example:

```sql
SET @SQL =
N'SELECT * FROM TeamMembers
WHERE Department = '''
+ @Department + '''';
```

Safer Example:

```sql
SET @SQL =
N'SELECT * FROM TeamMembers
WHERE Department = @Dept';

EXEC sp_executesql
@SQL,
N'@Dept NVARCHAR(50)',
@Dept = @Department;
```

Using parameters is the recommended approach.

## Best Practices

- Use `sp_executesql` instead of `EXEC` whenever possible.
- Use parameterized queries.
- Validate all user input.
- Use `QUOTENAME()` for object names.
- Prefer Static SQL when query requirements are fixed.
- Test generated queries before deployment.

## Common Use Cases

| Scenario | Dynamic SQL Usage |
| --- | --- |
| Dynamic Reports | User-selected filters |
| Search Applications | Variable conditions |
| Administrative Scripts | Dynamic object management |
| Data Migration | Flexible table selection |
| Stored Procedures | Runtime query generation |

## Important Points

- Dynamic SQL generates queries during execution.
- It provides flexibility when query structures vary.
- `sp_executesql` is the preferred execution method in SQL Server.
- Parameterized queries help prevent SQL injection.
- Dynamic SQL should be used only when static SQL cannot meet the requirement.

## Conclusion

Dynamic SQL allows SQL statements to be generated and executed at runtime, making database applications more flexible and adaptable. It is particularly useful when table names, columns, filters, or sorting conditions are not known beforehand. While Dynamic SQL offers powerful capabilities, it should be implemented carefully using parameterized queries and proper validation techniques to ensure security, maintainability, and performance.



###
