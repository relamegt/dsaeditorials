# SQL Unique Index

## Introduction

A SQL `UNIQUE INDEX` is used to ensure that no duplicate values exist in one or more columns of a table. It helps maintain data integrity while also improving query performance by creating an index on the specified column(s).

A unique index can be created on a single column or multiple columns. When applied to multiple columns, the combination of values must remain unique.

## Why Use a Unique Index?

The `UNIQUE INDEX` helps you:

- Prevent duplicate values in a column.
- Maintain data consistency and integrity.
- Improve data retrieval performance.
- Enforce uniqueness across multiple columns.
- Reduce the chances of invalid data entries.

## Syntax

### Create a Unique Index on a Single Column

```sql
CREATE UNIQUE INDEX index_name
ON table_name(column_name);
```

### Create a Unique Index on Multiple Columns

```sql
CREATE UNIQUE INDEX index_name
ON table_name(column1, column2);
```

### Syntax Components

| Component | Description |
| --- | --- |
| CREATE UNIQUE INDEX | Creates a unique index |
| index_name | Name of the unique index |
| table_name | Table where the index is created |
| column_name | Column on which uniqueness is enforced |

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Sample Table

```sql
CREATE TABLE Students (
    StudentID INT,
    StudentName VARCHAR(100),
    Email VARCHAR(100),
    City VARCHAR(50)
);
```

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 'akash@alphaknowledge.in', 'Vijayawada'),
(102, 'Mohit', 'mohit@alphaknowledge.in', 'Hyderabad'),
(103, 'Abhiram', 'abhiram@alphaknowledge.in', 'Guntur'),
(104, 'Hemesh', 'hemesh@alphaknowledge.in', 'Visakhapatnam'),
(105, 'Hemanth', 'hemanth@alphaknowledge.in', 'Hyderabad'),
(106, 'Akhil', 'akhil@alphaknowledge.in', 'Vijayawada');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | City |
| --- | --- | --- | --- |
| 101 | Akash | [akash@alphaknowledge.in](mailto:akash@alphaknowledge.in) | Vijayawada |
| 102 | Mohit | [mohit@alphaknowledge.in](mailto:mohit@alphaknowledge.in) | Hyderabad |
| 103 | Abhiram | [abhiram@alphaknowledge.in](mailto:abhiram@alphaknowledge.in) | Guntur |
| 104 | Hemesh | [hemesh@alphaknowledge.in](mailto:hemesh@alphaknowledge.in) | Visakhapatnam |
| 105 | Hemanth | [hemanth@alphaknowledge.in](mailto:hemanth@alphaknowledge.in) | Hyderabad |
| 106 | Akhil | [akhil@alphaknowledge.in](mailto:akhil@alphaknowledge.in) | Vijayawada |

---

## Example 1: Creating a Unique Index on a Single Column

Create a unique index on the Email column.

### Query

```sql
CREATE UNIQUE INDEX idx_unique_email
ON Students(Email);
```

### Explanation

- Creates a unique index on the Email column.
- Ensures no two students can have the same email address.
- Improves search performance on the Email column.

---

## Example 2: Inserting a Duplicate Value

Attempt to insert a student with an existing email address.

### Query

```sql
INSERT INTO Students
VALUES
(107, 'Akash Kumar', 'akash@alphaknowledge.in', 'Chennai');
```

### Output

```text
ERROR: Duplicate entry 'akash@alphaknowledge.in'
for key 'idx_unique_email'
```

### Explanation

- The email already exists in the table.
- The unique index prevents duplicate values.
- The insert operation fails.

---

## Example 3: Creating a Unique Index on Multiple Columns

Create a unique index on StudentName and City.

### Query

```sql
CREATE UNIQUE INDEX idx_name_city
ON Students(StudentName, City);
```

### Explanation

- Enforces uniqueness on the combination of StudentName and City.
- Duplicate combinations are not allowed.
- Individual column values may still repeat.

---

## Example 4: Attempting Duplicate Combination Entry

Try inserting a duplicate StudentName and City combination.

### Query

```sql
INSERT INTO Students
VALUES
(108, 'Mohit', 'mohit_new@alphaknowledge.in', 'Hyderabad');
```

### Output

```text
ERROR: Duplicate entry for unique index 'idx_name_city'
```

### Explanation

- The combination Mohit and Hyderabad already exists.
- The unique index blocks the duplicate combination.

---

## Example 5: Viewing Unique Indexes

Display all indexes available on the Students table.

### Query

```sql
SHOW INDEXES FROM Students;
```

### Sample Output

| Key_name | Column_name | Non_unique |
| --- | --- | --- |
| idx_unique_email | Email | 0 |
| idx_name_city | StudentName | 0 |
| idx_name_city | City | 0 |

### Explanation

- Shows all indexes associated with the table.
- Non_unique value of 0 indicates a unique index.
- Helps verify index creation.

## Example 6: Updating a Record with a Duplicate Value

Attempt to update a student's email to an existing email address.

### Query

```sql
UPDATE Students
SET Email = 'mohit@alphaknowledge.in'
WHERE StudentID = 103;
```

### Output

```text
ERROR: Duplicate entry 'mohit@alphaknowledge.in'
for key 'idx_unique_email'
```

### Explanation

- The unique index checks updates as well as inserts.
- Duplicate values are not allowed.
- The update operation is rejected.

---

## Benefits of Unique Indexes

- Prevent duplicate records.
- Improve data quality.
- Speed up searches.
- Enforce business rules.
- Maintain database consistency.

## Limitations of Unique Indexes

- Cannot be created if duplicates already exist.
- Require additional storage space.
- Slightly slower INSERT and UPDATE operations.
- Must be managed carefully in large databases.

---

## Best Practices

- Use unique indexes on emails, usernames, and IDs.
- Remove duplicate data before creating a unique index.
- Avoid unnecessary unique indexes.
- Use meaningful index names.
- Regularly review index usage.

---

## Important Points

- Unique indexes enforce uniqueness.
- They improve query performance.
- Multiple-column unique indexes validate combinations.
- Duplicate inserts and updates are blocked.
- Existing duplicate values prevent index creation.

---

## Conclusion

The SQL `UNIQUE INDEX` is an essential database feature for maintaining data integrity and preventing duplicate records. It ensures that critical columns contain unique values while also providing faster data retrieval. Proper use of unique indexes helps create reliable, consistent, and efficient database systems.



###
