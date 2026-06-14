# SQL CREATE INDEX Statement

## Introduction

The SQL `CREATE INDEX` statement is used to create indexes on database tables. Indexes improve query performance by allowing the database engine to locate rows more efficiently without scanning the entire table.

Indexes are commonly created on columns that are frequently used in `WHERE`, `JOIN`, `ORDER BY`, and `GROUP BY` clauses.

## Why Use CREATE INDEX?

The `CREATE INDEX` statement helps you:

- Improve query execution speed.
- Reduce table scan operations.
- Enhance performance of large tables.
- Optimize filtering and sorting operations.
- Speed up JOIN operations.

## Syntax

### Create a Regular Index

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

### Create a Multi-Column Index

```sql
CREATE INDEX index_name
ON table_name(column1, column2);
```

### Create a Unique Index

```sql
CREATE UNIQUE INDEX index_name
ON table_name(column_name);
```

### Syntax Components

| Component | Description |
| --- | --- |
| CREATE INDEX | Creates a new index |
| index_name | Name of the index |
| table_name | Table on which the index is created |
| column_name | Column to be indexed |

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

## Creating a Sample Table

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Course VARCHAR(50),
    City VARCHAR(50)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 'SQL', 'Vijayawada'),
(102, 'Mohit', 'Python', 'Hyderabad'),
(103, 'Abhiram', 'SQL', 'Guntur'),
(104, 'Hemesh', 'Java', 'Visakhapatnam'),
(105, 'Hemanth', 'SQL', 'Hyderabad'),
(106, 'Akhil', 'Python', 'Vijayawada');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Course | City |
| --- | --- | --- | --- |
| 101 | Akash | SQL | Vijayawada |
| 102 | Mohit | Python | Hyderabad |
| 103 | Abhiram | SQL | Guntur |
| 104 | Hemesh | Java | Visakhapatnam |
| 105 | Hemanth | SQL | Hyderabad |
| 106 | Akhil | Python | Vijayawada |

---

## Example 1: Creating an Index on a Single Column

Create an index on the Course column.

### Query

```sql
CREATE INDEX idx_course
ON Students(Course);
```

### Explanation

- Creates an index named `idx_course`.
- The index is built on the Course column.
- Queries filtering by Course can execute faster.

---

## Example 2: Using the Indexed Column in a Query

Retrieve all students enrolled in SQL.

### Query

```sql
SELECT StudentName, Course
FROM Students
WHERE Course = 'SQL';
```

### Output

| StudentName | Course |
| --- | --- |
| Akash | SQL |
| Abhiram | SQL |
| Hemanth | SQL |

### Explanation

- The database can use the `idx_course` index.
- Fewer rows need to be scanned.
- Query execution becomes more efficient.

---

## Example 3: Creating a Multi-Column Index

Create an index on Course and City.

### Query

```sql
CREATE INDEX idx_course_city
ON Students(Course, City);
```

### Explanation

- Creates a composite index.
- Useful when queries frequently filter by both Course and City.
- Improves multi-column search performance.

---

## Example 4: Creating a Unique Index

Create a unique index on StudentID.

### Query

```sql
CREATE UNIQUE INDEX idx_student_id
ON Students(StudentID);
```

### Explanation

- Prevents duplicate StudentID values.
- Ensures data integrity.
- Improves lookup speed for StudentID searches.

---

## Example 5: Attempting to Insert Duplicate Values

Suppose a unique index exists on StudentID.

### Query

```sql
INSERT INTO Students
VALUES
(101, 'Akash Kumar', 'Java', 'Chennai');
```

### Output

```text
ERROR: Duplicate entry '101' for key 'idx_student_id'
```

### Explanation

- StudentID 101 already exists.
- The unique index blocks duplicate entries.
- Data consistency is maintained.

---

## Example 6: Viewing Existing Indexes

Display all indexes created on the Students table.

### Query

```sql
SHOW INDEXES FROM Students;
```

### Sample Output

| Key_name | Column_name |
| --- | --- |
| PRIMARY | StudentID |
| idx_course | Course |
| idx_course_city | Course |
| idx_course_city | City |
| idx_student_id | StudentID |

### Explanation

- Displays all indexes associated with the table.
- Shows indexed columns and index names.
- Helps verify successful index creation.

---

## Benefits of CREATE INDEX

- Faster data retrieval.
- Better JOIN performance.
- Improved sorting and grouping.
- Reduced table scans.
- Enhanced user experience for large databases.

---

## Limitations of Indexes

- Require additional storage space.
- Slow down INSERT operations.
- Slow down UPDATE operations.
- Slow down DELETE operations.
- Too many indexes can reduce overall performance.

---

## Best Practices

- Create indexes on frequently searched columns.
- Avoid indexing every column.
- Use composite indexes carefully.
- Remove unused indexes periodically.
- Monitor query performance before adding indexes.

---

## Important Points

- Indexes improve query performance.
- They do not change table structure.
- Unique indexes prevent duplicate values.
- Composite indexes can include multiple columns.
- Excessive indexing may affect write operations.

---

## Conclusion

The SQL `CREATE INDEX` statement is a powerful performance optimization feature that helps databases retrieve data faster. By creating indexes on frequently searched columns, developers can significantly improve query execution speed and overall database efficiency. Proper index management ensures the right balance between fast retrieval and storage overhead.



###
