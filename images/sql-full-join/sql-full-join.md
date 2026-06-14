# SQL FULL JOIN

## Introduction

The SQL `FULL JOIN` (also called `FULL OUTER JOIN`) returns all records from both tables. If matching records exist, they are combined into a single row. If no match exists, NULL values are returned for the missing side.

A FULL JOIN combines the results of both `LEFT JOIN` and `RIGHT JOIN`.

## Why Use FULL JOIN?

The `FULL JOIN` helps you:

- Retrieve all records from both tables.
- Display matching and non-matching data together.
- Identify missing relationships between tables.
- Analyze complete datasets.
- Combine results from LEFT JOIN and RIGHT JOIN.

## Syntax

```sql
SELECT column_name(s)
FROM table1
FULL JOIN table2
ON table1.column_name = table2.column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| FULL JOIN | Returns all rows from both tables |
| table1 | First table |
| table2 | Second table |
| ON | Specifies the matching condition |
| column_name | Related column used for matching |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating Sample Tables

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    StudentID INT,
    CourseName VARCHAR(100)
);
```

## Inserting Sample Records

```sql
INSERT INTO Students VALUES
(1, 'Akash'),
(2, 'Mohit'),
(3, 'Abhiram');

INSERT INTO Courses VALUES
(101, 1, 'SQL'),
(102, 2, 'Java'),
(103, 4, 'Python');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName |
| --- | --- |
| 1 | Akash |
| 2 | Mohit |
| 3 | Abhiram |

```sql
SELECT * FROM Courses;
```

### Output

| CourseID | StudentID | CourseName |
| --- | --- | --- |
| 101 | 1 | SQL |
| 102 | 2 | Java |
| 103 | 4 | Python |

---

## Example 1: Basic FULL JOIN

Retrieve all students and courses.

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
FULL JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Output

| StudentName | CourseName |
| --- | --- |
| Akash | SQL |
| Mohit | Java |
| Abhiram | NULL |
| NULL | Python |

### Explanation

- Matching records are combined.
- Unmatched students appear with NULL course values.
- Unmatched courses appear with NULL student values.

---

## Example 2: FULL JOIN with WHERE Clause

Display only unmatched records.

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
FULL JOIN Courses
ON Students.StudentID = Courses.StudentID
WHERE Students.StudentID IS NULL
   OR Courses.StudentID IS NULL;
```

### Output

| StudentName | CourseName |
| --- | --- |
| Abhiram | NULL |
| NULL | Python |

### Explanation

- Shows records without matches.
- Useful for identifying missing relationships.

---

## FULL JOIN vs INNER JOIN

| Feature | FULL JOIN | INNER JOIN |
| --- | --- | --- |
| Returns matching rows | Yes | Yes |
| Returns non-matching rows | Yes | No |
| Shows NULL values | Yes | No |
| Includes all records | Yes | No |

---

## Best Practices

- Use FULL JOIN when all records from both tables are required.
- Filter NULL values to identify unmatched records.
- Use meaningful join conditions.
- Prefer INNER JOIN when only matching records are needed.

---

## Important Points

- FULL JOIN returns all rows from both tables.
- Matching rows are combined into a single result.
- Non-matching rows contain NULL values.
- FULL JOIN combines LEFT JOIN and RIGHT JOIN results.
- Useful for complete data analysis.

---

## Conclusion

The SQL `FULL JOIN` retrieves all records from both tables while combining matching rows and displaying NULL values for unmatched records. It is useful for identifying missing relationships and performing complete data analysis across multiple tables.



###
