# SQL CREATE INDEX Statement

## Introduction

The `CREATE INDEX` statement in SQL is used to create indexes on one or more table columns. Indexes improve query performance by allowing the database to locate records quickly instead of scanning the entire table.

### Benefits of CREATE INDEX

- Improves data retrieval speed.
- Enhances query performance.
- Optimizes WHERE, JOIN, and ORDER BY operations.
- Works without changing table structure.

---

## Syntax

### Create a Standard Index

```sql id="11e7sq"
CREATE INDEX index_name
ON table_name(column1, column2, ...);
```

### Create a Unique Index

```sql id="lgw9ra"
CREATE UNIQUE INDEX index_name
ON table_name(column1, column2, ...);
```

### Syntax Components

| Component | Description |
| --- | --- |
| index_name | Name of the index |
| table_name | Table on which index is created |
| column_name | Column(s) used for indexing |

---

## Sample Table

We will use the following AlphaKnowledge_Students table.

```sql id="h6kl9p"
CREATE TABLE AlphaKnowledge_Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50),
    Course VARCHAR(50),
    City VARCHAR(50),
    Marks INT
);

INSERT INTO AlphaKnowledge_Students VALUES
(101,'Akash','DSA','Hyderabad',92),
(102,'Mohit','DBMS','Vijayawada',88),
(103,'Abhiram','Java','Guntur',85),
(104,'Hemesh','Python','Hyderabad',95),
(105,'Hemanth','DSA','Vijayawada',90),
(106,'Akhil','DBMS','Guntur',87);
```

---

## Example 1: Creating a Standard Index

Create an index on the StudentName column.

### Query

```sql id="xuvmws"
CREATE INDEX idx_student_name
ON AlphaKnowledge_Students(StudentName);
```

### Explanation

- Creates a non-unique index on StudentName.
- Speeds up searches based on student names.
- Useful when the column is frequently used in WHERE conditions.

---

## Example 2: Creating a Unique Index

Create a unique index on StudentID.

### Query

```sql id="h2bwjr"
CREATE UNIQUE INDEX idx_student_id
ON AlphaKnowledge_Students(StudentID);
```

### Explanation

- Prevents duplicate StudentID values.
- Maintains data integrity.
- Improves lookup performance.

---

## Example 3: Using Indexed Data

Retrieve records using the indexed StudentName column.

### Query

```sql id="i0jfb0"
SELECT *
FROM AlphaKnowledge_Students
WHERE StudentName = 'Akash';
```

### Explanation

- Database uses the index to locate records faster.
- Avoids full table scanning.
- Improves query performance.

---

## Example 4: Viewing Existing Indexes

Display all indexes created on the table.

### Query

```sql id="k8ldho"
SHOW INDEXES
FROM AlphaKnowledge_Students;
```

### Explanation

- Shows available indexes.
- Displays index names and indexed columns.
- Helps verify successful index creation.

---

## Example 5: Creating a Multi-Column Index

Create an index on Course and City.

### Query

```sql id="n9xw4z"
CREATE INDEX idx_course_city
ON AlphaKnowledge_Students(Course, City);
```

### Explanation

- Creates an index on multiple columns.
- Improves searches using both Course and City.
- Useful for filtering and sorting operations.

---

## Advantages of CREATE INDEX

- Faster data retrieval.
- Better query execution.
- Improved JOIN performance.
- Faster sorting and filtering.
- Reduces table scan operations.

---

## Disadvantages of Indexes

- Requires additional storage space.
- Slows INSERT operations.
- Slows UPDATE operations.
- Slows DELETE operations.
- Requires maintenance for large databases.

---

## Best Practices

- Create indexes on frequently searched columns.
- Avoid excessive indexing.
- Use unique indexes when uniqueness is required.
- Monitor unused indexes regularly.
- Use multi-column indexes only when needed.

---

## Important Points

- CREATE INDEX improves query performance.
- Indexes do not change table data.
- PRIMARY KEY automatically creates an index.
- UNIQUE constraints create unique indexes automatically.
- Too many indexes can negatively affect write performance.

---

## Conclusion

The SQL CREATE INDEX statement is a powerful performance optimization feature that helps databases retrieve records faster. By creating indexes on frequently searched columns, developers can significantly improve query execution speed and overall database efficiency.



###
