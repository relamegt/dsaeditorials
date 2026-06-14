# SQL ALTER TABLE

## Introduction

The SQL `ALTER TABLE` statement is used to modify the structure of an existing table without affecting the stored data. It allows database administrators and developers to adapt tables as application requirements evolve.

Using `ALTER TABLE`, you can rename tables, rename columns, add new columns, modify column definitions, and remove existing columns.

## Why Use ALTER TABLE?

The `ALTER TABLE` statement is useful when:

- A table name needs to be updated.
- Column names need to be made more meaningful.
- Additional fields are required to store new information.
- Existing column data types need to be changed.
- Unnecessary columns need to be removed.

## Syntax

### Rename a Table

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

### Rename a Column

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name TO new_column_name;
```

### Add a New Column

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### Modify a Column

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name new_datatype;
```

### Remove a Column

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

## Creating a Sample Database

Create a database for the examples:

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating the Team Table

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

View the data:

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

## Example 1: Renaming a Table

Suppose the table name `TeamMembers` no longer accurately represents the data. We can rename it to `AlphaTeam`.

```sql
ALTER TABLE TeamMembers
RENAME TO AlphaTeam;
```

The table name is changed while preserving all existing records.

## Example 2: Renaming a Column

Assume we want the column name `Department` to be more descriptive.

```sql
ALTER TABLE AlphaTeam
RENAME COLUMN Department TO TeamDepartment;
```

The column is renamed without affecting the stored values.

## Example 3: Adding a New Column

To store each member's experience level, add a new column:

```sql
ALTER TABLE AlphaTeam
ADD ExperienceYears INT;
```

The new column is added to the table structure.

## Example 4: Modifying a Column Data Type

Suppose we want to allow longer department names.

```sql
ALTER TABLE AlphaTeam
MODIFY COLUMN TeamDepartment VARCHAR(200);
```

The column's maximum character limit is increased.

## Example 5: Removing a Column

If a column is no longer required, it can be deleted.

```sql
ALTER TABLE AlphaTeam
DROP COLUMN ExperienceYears;
```

The selected column and its data are removed from the table.

## Common ALTER TABLE Operations

| Operation | Purpose |
| --- | --- |
| RENAME TO | Changes the table name |
| RENAME COLUMN | Changes a column name |
| ADD | Adds a new column |
| MODIFY COLUMN | Changes a column's data type or size |
| DROP COLUMN | Removes an existing column |

## Important Points

- `ALTER TABLE` changes the structure of an existing table.
- Existing data is generally preserved during most ALTER operations.
- Some database systems may use slightly different syntax.
- Structural changes should be tested before applying them in production environments.
- Always back up important data before making major schema modifications.

## Conclusion

The SQL `ALTER TABLE` statement provides a flexible way to modify database tables as requirements change. Whether you need to rename tables, update column names, add new fields, modify data types, or remove unnecessary columns, `ALTER TABLE` helps maintain and evolve your database structure without recreating tables from scratch.



###
