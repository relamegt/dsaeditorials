# SQL Joins (INNER, LEFT, RIGHT and FULL JOIN)

## Introduction

SQL Joins are used to combine data from two or more tables based on a related column. They help retrieve connected information stored across different tables and create meaningful result sets.

## Why Use SQL Joins?

SQL Joins help you:

- Combine related data from multiple tables.
- Retrieve information using common columns.
- Reduce data redundancy.
- Analyze relationships between tables.
- Generate meaningful reports.

## Types of SQL Joins

SQL provides several types of joins for combining data.

### 1. INNER JOIN

Returns only the rows that have matching values in both tables.

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN

Returns all rows from the left table and matching rows from the right table.

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

### 3. RIGHT JOIN

Returns all rows from the right table and matching rows from the left table.

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

### 4. FULL JOIN

Returns all rows from both tables, including matched and unmatched rows.

```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;
```

### 5. NATURAL JOIN

Automatically joins tables using columns with the same name and compatible data types.

```sql
SELECT *
FROM table1
NATURAL JOIN table2;
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

Insert records:

```sql
INSERT INTO Students VALUES
(1, 'Akash'),
(2, 'Mohit'),
(3, 'Abhiram'),
(4, 'Hemesh');

INSERT INTO Courses VALUES
(101, 1, 'SQL'),
(102, 2, 'Java'),
(103, 3, 'Python');
```

---

## Example 1: INNER JOIN

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
INNER JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Explanation

- Returns only students who have matching course records.
- Unmatched rows are excluded.

---

## Example 2: LEFT JOIN

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
LEFT JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Explanation

- Returns all students.
- Students without courses display NULL values.

---

## Example 3: RIGHT JOIN

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
RIGHT JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Explanation

- Returns all course records.
- Matching student information is displayed.

---

## Example 4: FULL JOIN

```sql
SELECT Students.StudentName,
       Courses.CourseName
FROM Students
FULL JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Explanation

- Returns all records from both tables.
- Non-matching rows contain NULL values.

---

## Example 5: NATURAL JOIN

```sql
SELECT StudentID,
       StudentName,
       CourseName
FROM Students
NATURAL JOIN Courses;
```

### Explanation

- Automatically joins using StudentID.
- Common columns appear only once in the result.

---

## Join Comparison

| Join Type | Returns |
| --- | --- |
| INNER JOIN | Matching rows only |
| LEFT JOIN | All left table rows + matching right rows |
| RIGHT JOIN | All right table rows + matching left rows |
| FULL JOIN | All rows from both tables |
| NATURAL JOIN | Matching rows using common columns automatically |

---

## Common Use Cases

### Student and Course Management

```sql
SELECT *
FROM Students
INNER JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

### Employee and Department Information

```sql
SELECT *
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

### Customer and Order Records

```sql
SELECT *
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

## Best Practices

- Join tables using related columns.
- Use INNER JOIN when only matching data is needed.
- Use LEFT JOIN when all records from the primary table are required.
- Avoid unnecessary joins to improve performance.
- Use aliases to simplify complex queries.

---

## Important Points

- SQL Joins combine data from multiple tables.
- INNER JOIN returns matching rows only.
- LEFT JOIN returns all rows from the left table.
- RIGHT JOIN returns all rows from the right table.
- FULL JOIN returns all rows from both tables.
- NATURAL JOIN automatically matches common columns.

---

## Conclusion

SQL Joins are essential for working with relational databases because they allow data from multiple tables to be combined into a single result set. Understanding INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN, and NATURAL JOIN helps retrieve related information efficiently and build powerful database queries.



###
