# SQL DELETE Statement

## Introduction

The SQL `DELETE` statement is used to remove existing records from a table. Unlike the `DROP TABLE` statement, which removes the entire table and its structure, `DELETE` removes only the selected rows while preserving the table structure, indexes, constraints, and relationships.

The `DELETE` statement is commonly used when outdated, incorrect, or unnecessary records need to be removed from a database.

## Why Use DELETE?

The `DELETE` statement helps you:

- Remove unwanted records from a table.
- Delete specific rows using conditions.
- Clean up outdated information.
- Maintain accurate database records.
- Preserve the table structure while removing data.

## Basic Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| DELETE FROM | Specifies the table from which records will be removed |
| WHERE | Determines which rows should be deleted |

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 5),
(2, 'Mohit Chandaluri', 'Content', 3),
(3, 'Abhiram Gopisetti', 'Technical', 4),
(4, 'Adapa Hemesh', 'Database', 2),
(5, 'Kiran Kumar', 'Technical', 3);
```

View the records:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |
| 2 | Mohit Chandaluri | Content | 3 |
| 3 | Abhiram Gopisetti | Technical | 4 |
| 4 | Adapa Hemesh | Database | 2 |
| 5 | Kiran Kumar | Technical | 3 |

## Deleting a Single Record

To remove a specific row, use the `WHERE` clause.

### Example

Delete the record belonging to Adapa Hemesh.

```sql
DELETE FROM TeamMembers
WHERE MemberID = 4;
```

Verify the result:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |
| 2 | Mohit Chandaluri | Content | 3 |
| 3 | Abhiram Gopisetti | Technical | 4 |
| 5 | Kiran Kumar | Technical | 3 |

## Deleting Multiple Records

The `WHERE` clause can match multiple rows.

### Example

Delete all members from the Technical department.

```sql
DELETE FROM TeamMembers
WHERE Department = 'Technical';
```

### Result

All records belonging to the Technical department are removed.

## Deleting Records Using Multiple Conditions

### Example

Delete members with less than 3 years of experience.

```sql
DELETE FROM TeamMembers
WHERE ExperienceYears < 3;
```

Only matching rows are deleted.

## Deleting All Records

To remove every row from a table, omit the `WHERE` clause.

```sql
DELETE FROM TeamMembers;
```

### Result

The table remains available, but all records are removed.

```sql
SELECT * FROM TeamMembers;
```

### Output

Empty result set.

## Important Warning

Always verify the `WHERE` clause before executing a DELETE statement.

```sql
DELETE FROM TeamMembers;
```

The above query removes every record in the table.

## Using DELETE with Transactions

Transactions allow deleted records to be restored if necessary.

### Example

```sql
BEGIN TRANSACTION;

DELETE FROM TeamMembers
WHERE Department = 'Content';

ROLLBACK;
```

### Explanation

- `BEGIN TRANSACTION` starts a transaction.
- `DELETE` removes matching records.
- `ROLLBACK` cancels the deletion and restores the data.

If the changes are correct, use:

```sql
COMMIT;
```

This permanently saves the deletion.

## Common DELETE Operations

### Delete by ID

```sql
DELETE FROM TeamMembers
WHERE MemberID = 2;
```

### Delete by Name

```sql
DELETE FROM TeamMembers
WHERE MemberName = 'Mohit Chandaluri';
```

### Delete by Department

```sql
DELETE FROM TeamMembers
WHERE Department = 'Database';
```

### Delete Records Matching Multiple Conditions

```sql
DELETE FROM TeamMembers
WHERE Department = 'Technical'
AND ExperienceYears < 5;
```

## DELETE vs TRUNCATE vs DROP

| Feature | DELETE | TRUNCATE | DROP |
| --- | --- | --- | --- |
| Removes Data | Yes | Yes | Yes |
| Removes Specific Rows | Yes | No | No |
| Uses WHERE Clause | Yes | No | No |
| Removes Table Structure | No | No | Yes |
| Can Be Rolled Back* | Usually Yes | Database Dependent | No |
| Table Remains Available | Yes | Yes | No |

*Rollback support depends on the database system and transaction settings.

## Best Practices

- Always test the condition using a `SELECT` statement first.
- Use transactions for critical deletions.
- Create backups before removing important data.
- Avoid running DELETE statements without a `WHERE` clause unless intentionally clearing the table.
- Verify affected rows before committing changes.

## Important Points

- `DELETE` removes records from a table.
- The table structure remains intact.
- The `WHERE` clause determines which rows are removed.
- Omitting `WHERE` deletes all rows.
- Transactions can help recover accidentally deleted data.
- DELETE is a Data Manipulation Language (DML) command.

## Conclusion

The SQL `DELETE` statement is an essential command for removing records from a database table while preserving the table structure. By combining `DELETE` with appropriate `WHERE` conditions and transactions, developers can safely manage and maintain database records without affecting the underlying schema.



###
