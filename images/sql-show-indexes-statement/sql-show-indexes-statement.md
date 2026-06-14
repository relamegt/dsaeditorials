# SQL SHOW INDEXES Statement

## Introduction

Indexes are database objects that improve query performance by providing faster access paths to table data. The `SHOW INDEXES` statement is used to display information about all indexes associated with a table. It helps database administrators and developers analyze existing indexes and optimize query execution.

### Key Features of SHOW INDEXES

- Displays all indexes available on a table.
- Helps analyze index structure and usage.
- Shows uniqueness and index type information.
- Assists in database optimization.
- Useful for troubleshooting performance issues.

---

## Syntax

```sql
SHOW INDEXES FROM table_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| SHOW INDEXES | Displays index information |
| table_name | Name of the table whose indexes are displayed |

---

## Sample Table

We will create an `AlphaKnowledge_Students` table and define multiple indexes on it.

```sql
CREATE TABLE AlphaKnowledge_Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50),
    Course VARCHAR(50),
    City VARCHAR(50),
    Marks INT,
    
    INDEX idx_course (Course),
    UNIQUE INDEX idx_student_name (StudentName),
    INDEX idx_city_course (City, Course)
);
```

### Sample Data

```sql
INSERT INTO AlphaKnowledge_Students VALUES
(101,'Akash','SQL','Hyderabad',92),
(102,'Mohit','DBMS','Vijayawada',88),
(103,'Abhiram','Java','Guntur',85),
(104,'Hemesh','Python','Hyderabad',95),
(105,'Hemanth','SQL','Vijayawada',90),
(106,'Akhil','DBMS','Guntur',87);
```

---

## Understanding SHOW INDEXES Output

The output of the SHOW INDEXES command contains several useful columns.

| Column | Description |
| --- | --- |
| Table | Name of the table |
| Non_unique | Indicates whether duplicate values are allowed |
| Key_name | Name of the index |
| Seq_in_index | Position of a column inside the index |
| Column_name | Indexed column name |
| Collation | Sort order of indexed values |
| Cardinality | Estimated number of unique values |
| Sub_part | Indexed prefix length if partial indexing is used |
| Index_type | Type of index such as BTREE or HASH |
| Visible | Indicates whether optimizer can use the index |

---

## Example 1: Display All Indexes

### Query

```sql
SHOW INDEXES
FROM AlphaKnowledge_Students;
```

### Explanation

- Displays all indexes created on the table.
- Shows primary, unique, and regular indexes.
- Helps verify successful index creation.

---

## Example 2: Viewing Primary Key Index

### Query

```sql
SHOW INDEXES
FROM AlphaKnowledge_Students
WHERE Key_name = 'PRIMARY';
```

### Explanation

- Displays information about the primary key index.
- Created automatically when StudentID is defined as PRIMARY KEY.
- Ensures fast record retrieval.

---

## Example 3: Viewing Unique Index Information

### Query

```sql
SHOW INDEXES
FROM AlphaKnowledge_Students;
```

### Explanation

- Displays the unique index on StudentName.
- The Non_unique value will be 0.
- Prevents duplicate student names from being inserted.

---

## Example 4: Viewing Composite Index Details

### Query

```sql
SHOW INDEXES
FROM AlphaKnowledge_Students;
```

### Explanation

- Displays the composite index idx_city_course.
- Shows City as the first indexed column.
- Shows Course as the second indexed column.
- Useful for queries filtering on both columns.

---

## Example 5: Verify Indexes After Modification

### Query

```sql
DROP INDEX idx_course
ON AlphaKnowledge_Students;

SHOW INDEXES
FROM AlphaKnowledge_Students;
```

### Explanation

- Removes the idx_course index.
- Displays the updated list of indexes.
- Confirms successful index deletion.

---

## Types of Indexes Displayed

### Primary Index

Automatically created when a primary key is defined.

### Unique Index

Prevents duplicate values in indexed columns.

### Regular Index

Improves query performance without enforcing uniqueness.

### Composite Index

Indexes multiple columns together for optimized searching.

---

## Advantages of SHOW INDEXES

- Helps monitor database performance.
- Verifies existing indexes.
- Assists in query optimization.
- Simplifies database administration.
- Supports effective index management.

---

## Limitations

- Only displays index information.
- Cannot modify indexes directly.
- Output format varies across database systems.
- Does not indicate actual index usage frequency.

---

## Best Practices

- Regularly review indexes on large tables.
- Remove unused indexes.
- Avoid creating duplicate indexes.
- Monitor cardinality values for optimization.
- Use composite indexes only when necessary.

---

## Important Points

- SHOW INDEXES displays all indexes associated with a table.
- Primary keys automatically create indexes.
- Unique indexes prevent duplicate values.
- Composite indexes contain multiple columns.
- Reviewing indexes helps maintain database performance.

---

## Conclusion

The SQL `SHOW INDEXES` statement is an important administrative command that allows developers and database administrators to inspect and analyze existing indexes on a table. By understanding index details such as uniqueness, indexed columns, cardinality, and index types, database performance can be optimized more effectively.



###
