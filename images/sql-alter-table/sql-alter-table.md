# SQL ALTER TABLE 

## Introduction

The SQL `ALTER TABLE` statement is used to modify the structure of an existing table without deleting the table or its data. It allows developers and database administrators to adapt database schemas as application requirements evolve.

Using `ALTER TABLE`, you can add new columns, modify existing columns, remove unwanted columns, rename columns, and even rename entire tables.

## Why Use ALTER TABLE?

The `ALTER TABLE` command is useful when:

- New information needs to be stored in a table.
- Existing column definitions need to be updated.
- Unnecessary columns must be removed.
- Column names need to be made more descriptive.
- Table names need to be changed to better reflect their purpose.

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating the Employees Table

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

## Inserting Sample Data

```sql
INSERT INTO Employees
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 85000),
(2, 'Mohit Chandaluri', 'Content', 65000),
(3, 'Abhiram Gopisetti', 'Technical', 72000),
(4, 'Adapa Hemesh', 'Database', 70000);
```

View the data:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Salary |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 85000 |
| 2 | Mohit Chandaluri | Content | 65000 |
| 3 | Abhiram Gopisetti | Technical | 72000 |
| 4 | Adapa Hemesh | Database | 70000 |

## Basic Syntax

### Adding a Column

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### Modifying a Column

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name new_datatype;
```

### Dropping a Column

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Renaming a Column

```sql
ALTER TABLE table_name
RENAME COLUMN old_column_name TO new_column_name;
```

### Renaming a Table

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

## Example 1: Adding a New Column

Suppose we want to store employee email addresses.

```sql
ALTER TABLE Employees
ADD Email VARCHAR(100);
```

The table now contains an additional column named `Email`.

## Example 2: Modifying a Column

Assume the department names may become longer in the future.

```sql
ALTER TABLE Employees
MODIFY COLUMN Department VARCHAR(100);
```

The maximum size of the `Department` column is increased.

## Example 3: Dropping a Column

If the `Email` column is no longer required, it can be removed.

```sql
ALTER TABLE Employees
DROP COLUMN Email;
```

The column and all data stored within it are permanently deleted.

## Example 4: Renaming a Column

To make the column name more descriptive:

```sql
ALTER TABLE Employees
RENAME COLUMN EmployeeName TO FullName;
```

The column name changes while the data remains unchanged.

## Example 5: Renaming a Table

If the organization decides to rename the table:

```sql
ALTER TABLE Employees
RENAME TO StaffMembers;
```

The table is renamed without affecting its records.

## Common ALTER TABLE Operations

| Operation | Purpose |
| --- | --- |
| ADD | Adds a new column |
| MODIFY COLUMN | Changes a column's data type or size |
| DROP COLUMN | Removes a column |
| RENAME COLUMN | Changes a column name |
| RENAME TO | Changes the table name |

## Practical Example

The following statement performs multiple structural updates over time:

```sql
ALTER TABLE Employees
ADD JoiningDate DATE;
```

```sql
ALTER TABLE Employees
MODIFY COLUMN Salary DECIMAL(12,2);
```

```sql
ALTER TABLE Employees
RENAME COLUMN Department TO Team;
```

These modifications allow the table structure to evolve without recreating the table.

## Important Points

- `ALTER TABLE` modifies an existing table structure.
- Existing data is usually preserved during most alterations.
- Dropping a column permanently removes its data.
- Different database systems may have slight syntax variations.
- Always test structural changes before applying them to production databases.
- Creating a backup before major schema changes is recommended.

## ALTER TABLE vs DROP TABLE

| Feature | ALTER TABLE | DROP TABLE |
| --- | --- | --- |
| Modifies Structure | Yes | No |
| Deletes Table | No | Yes |
| Preserves Data | Usually Yes | No |
| Adds Columns | Yes | No |
| Renames Tables | Yes | No |

## Conclusion

The SQL `ALTER TABLE` statement is one of the most important database management commands. It allows developers to update table structures by adding, modifying, renaming, or removing columns without recreating the table. Proper use of `ALTER TABLE` helps maintain flexible and scalable database designs as application requirements change.



###
