# SQL INSERT INTO Statement

## Introduction

The SQL `INSERT INTO` statement is used to add new records to a database table. It allows users to insert a single row, multiple rows, or even copy data from another table.

Whenever new information needs to be stored in a database, the `INSERT INTO` statement is used to populate the table with records.

## Why Use INSERT INTO?

The `INSERT INTO` statement helps you:

- Add new records to a table.
- Insert data into all columns or selected columns.
- Insert multiple rows in a single query.
- Copy data from one table to another.
- Populate tables with initial or imported data.

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

## Inserting Data into All Columns

When values are provided for every column, column names can be omitted if the values follow the table's column order.

### Syntax

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

### Example

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 5);
```

View the inserted record:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |

## Inserting Data into Specific Columns

Sometimes only certain columns need values while the remaining columns can be left as `NULL` or use default values.

### Syntax

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

### Example

```sql
INSERT INTO TeamMembers (MemberID, MemberName, Department)
VALUES (2, 'Mohit Chandaluri', 'Content');
```

View the data:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 2 | Mohit Chandaluri | Content | NULL |

## Inserting Multiple Rows

Multiple records can be inserted in a single statement.

### Syntax

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES
(value1, value2, ...),
(value1, value2, ...),
(value1, value2, ...);
```

### Example

```sql
INSERT INTO TeamMembers
VALUES
(3, 'Abhiram Gopisetti', 'Technical', 4),
(4, 'Adapa Hemesh', 'Database', 2),
(5, 'Kiran Kumar', 'Technical', 3);
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 3 | Abhiram Gopisetti | Technical | 4 |
| 4 | Adapa Hemesh | Database | 2 |
| 5 | Kiran Kumar | Technical | 3 |

### Benefits

- Reduces database calls.
- Improves insertion performance.
- Makes bulk data entry easier.

## Inserting Data from Another Table

Data can be copied from one table to another using `INSERT INTO ... SELECT`.

### Creating a Backup Table

```sql
CREATE TABLE TeamMembersBackup (
    MemberID INT,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

## Copying All Records

### Syntax

```sql
INSERT INTO target_table
SELECT * FROM source_table;
```

### Example

```sql
INSERT INTO TeamMembersBackup
SELECT * FROM TeamMembers;
```

Verify the copied records:

```sql
SELECT * FROM TeamMembersBackup;
```

The backup table now contains all records from the original table.

## Copying Specific Columns

Only selected columns can be copied.

### Syntax

```sql
INSERT INTO target_table (column1, column2)
SELECT column1, column2
FROM source_table;
```

### Example

```sql
INSERT INTO TeamMembersBackup (MemberID, MemberName)
SELECT MemberID, MemberName
FROM TeamMembers;
```

## Copying Records Based on a Condition

Specific records can be inserted using a `WHERE` clause.

### Syntax

```sql
INSERT INTO target_table
SELECT *
FROM source_table
WHERE condition;
```

### Example

Copy only members from the Technical department.

```sql
INSERT INTO TeamMembersBackup
SELECT *
FROM TeamMembers
WHERE Department = 'Technical';
```

Only matching records are copied.

## Common INSERT INTO Variations

| Operation | Description |
| --- | --- |
| INSERT INTO VALUES | Inserts a single or multiple records |
| INSERT INTO (Columns) VALUES | Inserts data into selected columns |
| INSERT INTO SELECT | Copies data from another table |
| INSERT INTO SELECT WHERE | Copies filtered records |

## Important Points

- `INSERT INTO` is used to add new records to a table.
- Values must match the column data types.
- When column names are omitted, values must follow the exact column order.
- Multiple rows can be inserted in a single statement.
- Data can be copied directly from another table.
- Constraints such as primary keys and unique keys must be respected during insertion.

## INSERT INTO vs UPDATE

| Feature | INSERT INTO | UPDATE |
| --- | --- | --- |
| Adds New Records | Yes | No |
| Modifies Existing Records | No | Yes |
| Creates New Rows | Yes | No |
| Uses VALUES Clause | Yes | No |
| Uses SET Clause | No | Yes |

## SQL Query to Insert Multiple Rows

When working with databases, it is often necessary to insert multiple records into a table at once. SQL allows multiple rows to be inserted using a single `INSERT INTO` statement, making data entry faster and more efficient than executing separate insert statements for each record.

This approach is commonly used when importing datasets, adding bulk records, or transferring information between tables.

## Why Insert Multiple Rows?

Inserting multiple rows in a single query offers several advantages:

- Reduces the number of database operations.
- Improves query performance.
- Simplifies bulk data insertion.
- Makes scripts easier to maintain.
- Reduces network communication between applications and databases.

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

## Inserting a Single Row

Before inserting multiple rows, let's look at a standard single-row insertion.

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 5);
```

View the record:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |

## Inserting Multiple Rows Using VALUES

The most common method is to provide multiple sets of values within a single `INSERT INTO` statement.

### Syntax

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES
(value1, value2, value3),
(value4, value5, value6),
(value7, value8, value9);
```

### Example

```sql
INSERT INTO TeamMembers
VALUES
(2, 'Mohit Chandaluri', 'Content', 3),
(3, 'Abhiram Gopisetti', 'Technical', 4),
(4, 'Adapa Hemesh', 'Database', 2),
(5, 'Kiran Kumar', 'Technical', 4);
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
| 5 | Kiran Kumar | Technical | 4 |

## Inserting Multiple Rows into Specific Columns

You can also insert values into selected columns only.

### Example

```sql
INSERT INTO TeamMembers (MemberID, MemberName, Department)
VALUES
(6, 'Sai Kumar', 'Support'),
(7, 'Ravi Teja', 'Testing');
```

Columns that are not specified receive `NULL` values or their default values.

## Using INSERT INTO ... SELECT

Another common approach is copying records from one table to another.

### Creating a Source Table

```sql
CREATE TABLE NewTeamMembers (
    MemberID INT,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

### Adding Sample Records

```sql
INSERT INTO NewTeamMembers
VALUES
(8, 'Nikhil Reddy', 'Technical', 5),
(9, 'Vamsi Krishna', 'Content', 2),
(10, 'Rahul Kumar', 'Technical', 6);
```

## Copying All Records

```sql
INSERT INTO TeamMembers
SELECT *
FROM NewTeamMembers;
```

This copies every row from `NewTeamMembers` into `TeamMembers`.

## Copying Specific Columns

```sql
INSERT INTO TeamMembers (MemberID, MemberName)
SELECT MemberID, MemberName
FROM NewTeamMembers;
```

Only the selected columns are copied.

## Copying Records Based on Conditions

The `WHERE` clause can be used to insert only matching records.

### Example

Copy only members having more than 4 years of experience.

```sql
INSERT INTO TeamMembers
SELECT *
FROM NewTeamMembers
WHERE ExperienceYears > 4;
```

Only qualifying rows are inserted.

## Inserting Multiple Rows Using Transactions

Transactions help ensure that all inserts succeed together. If any statement fails, the changes can be rolled back.

### Example

```sql
BEGIN TRANSACTION;

INSERT INTO TeamMembers
VALUES
(11, 'Anil Kumar', 'Operations', 3);

INSERT INTO TeamMembers
VALUES
(12, 'Harsha Vardhan', 'Support', 2);

COMMIT;
```

### Transaction Commands

| Command | Purpose |
| --- | --- |
| BEGIN TRANSACTION | Starts a transaction |
| COMMIT | Saves changes permanently |
| ROLLBACK | Cancels all changes within the transaction |

## Common Methods for Inserting Multiple Rows

| Method | Use Case |
| --- | --- |
| INSERT INTO ... VALUES | Manually adding multiple records |
| INSERT INTO ... SELECT | Copying data from another table |
| INSERT INTO ... SELECT WHERE | Copying filtered records |
| Transactions | Ensuring safe bulk inserts |

## Best Practices

- Use a single INSERT statement whenever possible.
- Verify column order before inserting values.
- Use transactions for critical bulk operations.
- Ensure primary key values remain unique.
- Validate data before performing large inserts.

## Important Points

- Multiple rows can be inserted using a single SQL statement.
- Bulk inserts are generally faster than individual inserts.
- `INSERT INTO ... SELECT` is useful for copying data.
- Transactions help maintain data consistency.
- The number of values must match the number of specified columns.

##



###
