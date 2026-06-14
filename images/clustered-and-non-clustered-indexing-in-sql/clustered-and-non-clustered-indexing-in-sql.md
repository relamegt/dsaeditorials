# Clustered and Non-Clustered Indexing in SQL

## Introduction

Indexing is a database optimization technique used to improve the speed of data retrieval operations. SQL databases commonly use two types of indexes:

- Clustered Index
- Non-Clustered Index

Both indexes improve query performance, but they organize and store data differently. Understanding their differences helps in selecting the appropriate indexing strategy for a database.

---

## What is a Clustered Index?

A Clustered Index determines the physical order in which rows are stored in a table. When a clustered index is created, the actual data rows are arranged according to the indexed column.

Since the data itself is stored in sorted order, a table can have only one clustered index.

### Key Characteristics

- Defines the physical order of table data.
- Data rows are stored according to the index key.
- Only one clustered index can exist per table.
- Provides excellent performance for range-based queries.
- Primary keys are often implemented as clustered indexes.

---

## What is a Non-Clustered Index?

A Non-Clustered Index creates a separate structure from the table data. It stores indexed values along with pointers to the actual data rows.

Unlike clustered indexes, multiple non-clustered indexes can be created on a table.

### Key Characteristics

- Stored separately from the table data.
- Contains index values and row pointers.
- Does not change the physical order of records.
- Multiple non-clustered indexes can exist.
- Ideal for search and lookup operations.

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
    RollNo INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50),
    Course VARCHAR(50)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 'Vijayawada', 'SQL'),
(102, 'Mohit', 'Hyderabad', 'Python'),
(103, 'Abhiram', 'Guntur', 'Java'),
(104, 'Hemesh', 'Visakhapatnam', 'SQL'),
(105, 'Hemanth', 'Hyderabad', 'Python'),
(106, 'Akhil', 'Vijayawada', 'Java');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| RollNo | StudentName | City | Course |
| --- | --- | --- | --- |
| 101 | Akash | Vijayawada | SQL |
| 102 | Mohit | Hyderabad | Python |
| 103 | Abhiram | Guntur | Java |
| 104 | Hemesh | Visakhapatnam | SQL |
| 105 | Hemanth | Hyderabad | Python |
| 106 | Akhil | Vijayawada | Java |

---

## Example 1: Clustered Index Using Primary Key

When a primary key is created, most database systems automatically create a clustered index on that column.

### Query

```sql
CREATE TABLE Students (
    RollNo INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50)
);
```

### Explanation

- RollNo becomes the clustered index.
- Records are physically stored in RollNo order.
- Queries using RollNo become faster.

---

## Example 2: Creating a Clustered Index Explicitly

Create a clustered index on the StudentName column.

### Query

```sql
CREATE CLUSTERED INDEX idx_student_name
ON Students(StudentName);
```

### Explanation

- Data rows are physically rearranged by StudentName.
- Records are stored alphabetically.
- Only one clustered index can exist on the table.

---

## Example 3: Creating a Non-Clustered Index

Create a non-clustered index on the City column.

### Query

```sql
CREATE NONCLUSTERED INDEX idx_city
ON Students(City);
```

### Explanation

- Creates a separate index structure.
- Does not change the table's physical order.
- Improves searches based on City.

---

## Example 4: Using a Non-Clustered Index in Searches

Retrieve students from Hyderabad.

### Query

```sql
SELECT *
FROM Students
WHERE City = 'Hyderabad';
```

### Output

| RollNo | StudentName | City | Course |
| --- | --- | --- | --- |
| 102 | Mohit | Hyderabad | Python |
| 105 | Hemanth | Hyderabad | Python |

### Explanation

- The non-clustered index helps locate matching rows quickly.
- SQL uses pointers stored in the index to access records.

---

## Example 5: Creating a Composite Non-Clustered Index

Create a non-clustered index using multiple columns.

### Query

```sql
CREATE NONCLUSTERED INDEX idx_city_course
ON Students(City, Course);
```

### Explanation

- Creates an index using both City and Course.
- Improves filtering based on both columns.
- Useful for multi-column search conditions.

---

## Example 6: Viewing Existing Indexes

Display all indexes available on the Students table.

### Query

```sql
SHOW INDEXES FROM Students;
```

### Sample Output

| Key_name | Column_name |
| --- | --- |
| PRIMARY | RollNo |
| idx_city | City |
| idx_city_course | City |
| idx_city_course | Course |

### Explanation

- Lists all indexes associated with the table.
- Helps verify index creation.
- Displays indexed columns and index names.

---

## Clustered vs Non-Clustered Index

| Feature | Clustered Index | Non-Clustered Index |
| --- | --- | --- |
| Data Storage | Stored with table data | Stored separately |
| Physical Order | Changes physical order | Does not change physical order |
| Number Allowed | One per table | Multiple per table |
| Query Performance | Faster for range queries | Faster for lookups |
| Storage Requirement | Lower | Higher |
| Leaf Nodes | Contain actual data | Contain pointers to data |

---

## Advantages of Clustered Indexes

- Faster range-based queries.
- Efficient sorting operations.
- Better performance for primary key searches.
- Reduced disk I/O for sequential access.

---

## Advantages of Non-Clustered Indexes

- Multiple indexes can be created.
- Faster lookup operations.
- Ideal for frequently searched columns.
- Improves filtering and join performance.

---

## Best Practices

- Use clustered indexes on primary key columns.
- Create non-clustered indexes on frequently searched columns.
- Avoid excessive indexing.
- Regularly monitor index performance.
- Remove unused indexes to reduce maintenance overhead.

---

## Important Points

- A table can have only one clustered index.
- Multiple non-clustered indexes can exist.
- Clustered indexes define physical row order.
- Non-clustered indexes store pointers to data.
- Proper indexing significantly improves query performance.

---

## Conclusion

Clustered and Non-Clustered indexes are fundamental database optimization tools. A clustered index organizes the actual table data, while a non-clustered index creates a separate lookup structure. Choosing the right index type based on query patterns and data access requirements can greatly improve database performance and efficiency.



###
