# SQL CREATE TABLE

## Introduction

The CREATE TABLE statement in SQL is used to create a new table within a database. Tables are the foundation of relational databases, allowing data to be stored in rows and columns for efficient management and retrieval.

Before data can be inserted into a database, a table must be created to define its structure, column names, and data types.

## Why Use CREATE TABLE?

The CREATE TABLE command helps developers:

- Create a new table in a database.
- Define column names and data types.
- Enforce data integrity using constraints.
- Organize information systematically.
- Prepare a database for storing records.

## Basic Syntax

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

### Explanation

| Component | Description |
| --- | --- |
| table_name | Name of the table being created |
| column1, column2 | Column names |
| datatype | Type of data stored in the column |

## Example: Creating a Students Table

Suppose AlphaKnowledge wants to maintain student information.

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT,
    City VARCHAR(50)
);
```

### Table Structure Output

| Field | Type | Key |
| --- | --- | --- |
| StudentID | INT | PRIMARY KEY |
| FirstName | VARCHAR(50) | - |
| LastName | VARCHAR(50) | - |
| Age | INT | - |
| City | VARCHAR(50) | - |

**Output:** Table created successfully.

## Inserting Sample Records

```sql
INSERT INTO Students
(StudentID, FirstName, LastName, Age, City)
VALUES
(1, 'Akash', 'Dangudubiyyapu', 21, 'Hyderabad'),
(2, 'Mohit', 'Chandaluri', 22, 'Vijayawada'),
(3, 'Abhiram', 'Gopisetti', 20, 'Guntur'),
(4, 'Adapa', 'Hemesh', 21, 'Visakhapatnam');
```

### Output Table

| StudentID | FirstName | LastName | Age | City |
| --- | --- | --- | --- | --- |
| 1 | Akash | Dangudubiyyapu | 21 | Hyderabad |
| 2 | Mohit | Chandaluri | 22 | Vijayawada |
| 3 | Abhiram | Gopisetti | 20 | Guntur |
| 4 | Adapa | Hemesh | 21 | Visakhapatnam |

## Using Constraints

Constraints are rules applied to columns to ensure data accuracy and consistency.

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Age INT CHECK (Age >= 18),
    City VARCHAR(50)
);
```

### Common Constraints

| Constraint | Purpose |
| --- | --- |
| PRIMARY KEY | Uniquely identifies each row |
| NOT NULL | Prevents empty values |
| UNIQUE | Prevents duplicate values |
| CHECK | Ensures data meets a condition |
| DEFAULT | Assigns a default value |

### Example

```sql
INSERT INTO Students
VALUES (5, 'Rahul', 'Kumar', 17, 'Delhi');
```

### Output

```text
ERROR: CHECK constraint violated
```

Because the Age value must be 18 or greater.

## Creating a Table from an Existing Table

SQL allows creating a new table based on an existing table.

```sql
CREATE TABLE StudentBackup AS
SELECT *
FROM Students;
```

### Output

#### StudentBackup Table

| StudentID | FirstName | LastName | Age | City |
| --- | --- | --- | --- | --- |
| 1 | Akash | Dangudubiyyapu | 21 | Hyderabad |
| 2 | Mohit | Chandaluri | 22 | Vijayawada |
| 3 | Abhiram | Gopisetti | 20 | Guntur |
| 4 | Adapa | Hemesh | 21 | Visakhapatnam |

**Note:** Constraints and indexes are generally not copied when using CREATE TABLE AS SELECT.

## Viewing Table Structure

To view the structure of a table:

```sql
DESC Students;
```

### Output

| Field | Type | Null | Key |
| --- | --- | --- | --- |
| StudentID | INT | NO | PRI |
| FirstName | VARCHAR(50) | YES |  |
| LastName | VARCHAR(50) | YES |  |
| Age | INT | YES |  |
| City | VARCHAR(50) | YES |  |

## Using IF NOT EXISTS

To avoid errors when creating a table that already exists:

```sql
CREATE TABLE IF NOT EXISTS Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);
```

### Benefit

The database creates the table only if it does not already exist.

## Best Practices

- Use meaningful table names.
- Define a primary key whenever possible.
- Choose appropriate data types.
- Apply constraints to maintain data quality.
- Avoid unnecessary columns.
- Keep table structures simple and scalable.

## Advantages of CREATE TABLE

- Establishes database structure.
- Improves data organization.
- Supports data validation through constraints.
- Enables efficient querying and management.
- Forms the foundation of relational database systems.

## Conclusion

The CREATE TABLE statement is one of the most important SQL commands because it defines how data will be stored within a database. By carefully selecting column names, data types, and constraints, developers can build reliable, efficient, and scalable database systems.

Understanding CREATE TABLE is the first step toward mastering SQL database design and management.

##



###
