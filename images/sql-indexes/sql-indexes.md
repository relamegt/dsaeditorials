# SQL Indexes

## Introduction

Indexes in SQL are special database objects that improve query performance by allowing the database to locate records quickly without scanning the entire table.

They work like an index in a book, helping the database find information faster.

### Benefits of Indexes

- Speed up SELECT queries.
- Improve JOIN performance.
- Optimize WHERE clause filtering.
- Enhance ORDER BY operations.
- Help enforce uniqueness using unique indexes.

> **Note:** PRIMARY KEY and UNIQUE constraints automatically create indexes.

---

## Sample Table

We will use the AlphaKnowledge_Students table throughout this article.

```sql
CREATE TABLE AlphaKnowledge_Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50),
    Course VARCHAR(50),
    City VARCHAR(50),
    Marks INT
);

INSERT INTO AlphaKnowledge_Students VALUES
(101, 'Akash', 'DSA', 'Hyderabad', 92),
(102, 'Mohit', 'DBMS', 'Vijayawada', 88),
(103, 'Abhiram', 'Java', 'Guntur', 85),
(104, 'Hemesh', 'Python', 'Hyderabad', 95),
(105, 'Hemanth', 'DSA', 'Vijayawada', 90),
(106, 'Akhil', 'DBMS', 'Guntur', 87);
```

---

## Creating Indexes

### 1. Single Column Index

A Single Column Index is created on one column and improves searches performed on that column.

### Syntax

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

### Example: Create Index on Course Column

```sql
CREATE INDEX idx_course
ON AlphaKnowledge_Students(Course);
```

### Explanation

- Creates an index named `idx_course`.
- Improves queries that search using the Course column.
- Useful when Course is frequently used in WHERE conditions.

---

### 2. Multi-Column Index

A Multi-Column Index is created on multiple columns and improves queries that filter using those columns together.

### Syntax

```sql
CREATE INDEX index_name
ON table_name(column1, column2);
```

### Example: Create Index on Course and City

```sql
CREATE INDEX idx_course_city
ON AlphaKnowledge_Students(Course, City);
```

### Explanation

- Creates an index on both Course and City.
- Improves filtering and sorting using these columns together.
- Useful for complex searches.

---

### 3. Unique Index

A Unique Index prevents duplicate values from being inserted into a column.

### Syntax

```sql
CREATE UNIQUE INDEX index_name
ON table_name(column_name);
```

### Example: Create Unique Index on Student Name

```sql
CREATE UNIQUE INDEX idx_unique_student
ON AlphaKnowledge_Students(StudentName);
```

### Explanation

- Ensures each student name is unique.
- Prevents duplicate records.
- Helps maintain data integrity.

### Example: Duplicate Entry

```sql
INSERT INTO AlphaKnowledge_Students
VALUES (107, 'Akash', 'SQL', 'Hyderabad', 89);
```

### Result

The query fails because a student named **Akash** already exists.

---

## Viewing Indexes

Indexes can be viewed to verify their existence and properties.

### Syntax

```sql
SHOW INDEXES FROM table_name;
```

### Example

```sql
SHOW INDEXES FROM AlphaKnowledge_Students;
```

### Explanation

- Displays all indexes available on the table.
- Shows index names, columns, and uniqueness information.

---

## Removing an Index

Unused indexes can be removed to reduce storage and maintenance overhead.

### Syntax

```sql
DROP INDEX index_name
ON table_name;
```

### Example

```sql
DROP INDEX idx_course_city
ON AlphaKnowledge_Students;
```

### Explanation

- Removes the specified index.
- Does not affect table data.
- Can improve INSERT and UPDATE performance.

---

## Rebuilding an Index

Indexes may become fragmented over time. Rebuilding reorganizes them for better performance.

### Syntax

```sql
ALTER INDEX index_name
ON table_name
REBUILD;
```

### Example

```sql
ALTER INDEX idx_course
ON AlphaKnowledge_Students
REBUILD;
```

### Explanation

- Reorganizes index structure.
- Improves index efficiency.
- Useful for large databases.

---

## Renaming an Index

Sometimes index names need to be updated for better readability.

### Syntax (SQL Server)

```sql
EXEC sp_rename
'old_index_name',
'new_index_name',
'INDEX';
```

### Example

```sql
EXEC sp_rename
'idx_course',
'idx_student_course',
'INDEX';
```

### Explanation

- Renames an existing index.
- Makes schema management easier.
- Does not affect data or table structure.

---

## Advantages of Indexes

- Faster data retrieval.
- Better query performance.
- Improved JOIN operations.
- Faster sorting and filtering.
- Supports uniqueness constraints.

---

## Disadvantages of Indexes

- Require additional storage.
- Slow down INSERT operations.
- Slow down UPDATE operations.
- Slow down DELETE operations.
- Need periodic maintenance.

---

## Best Practices

- Create indexes only on frequently searched columns.
- Avoid excessive indexing.
- Use multi-column indexes when necessary.
- Monitor unused indexes.
- Rebuild fragmented indexes regularly.

---

## Important Points

- Indexes improve read performance.
- PRIMARY KEY automatically creates an index.
- UNIQUE constraints create unique indexes.
- Too many indexes can reduce write performance.
- Indexes are especially useful for large tables.

---

## Conclusion

SQL Indexes help databases retrieve data efficiently by reducing the amount of scanning required during query execution. Proper indexing improves performance, enhances user experience, and makes database operations more efficient while balancing storage and maintenance costs.



###
