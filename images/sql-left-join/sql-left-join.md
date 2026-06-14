# SQL LEFT JOIN

## Introduction

The SQL `LEFT JOIN` (also known as `LEFT OUTER JOIN`) returns all records from the left table and the matching records from the right table. If no matching record exists in the right table, SQL returns `NULL` values for the right table columns.

LEFT JOIN is commonly used when you want to preserve all records from the primary table while retrieving related information from another table.

## Why Use LEFT JOIN?

A LEFT JOIN helps you:

- Retrieve all records from the left table.
- Include matching records from the right table.
- Identify records that have no matching values.
- Analyze incomplete relationships between tables.
- Generate comprehensive reports.

## Syntax

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| LEFT JOIN | Returns all rows from the left table |
| table1 | Left table whose records are preserved |
| table2 | Right table providing matching records |
| ON | Specifies the join condition |
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
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Departments VALUES
(101, 'Technical'),
(102, 'Content'),
(103, 'Management');

INSERT INTO Employees VALUES
(1, 'Akash', 101),
(2, 'Mohit', 102),
(3, 'Abhiram', NULL),
(4, 'Hemesh', 104);
```

Display table data:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID |
| --- | --- | --- |
| 1 | Akash | 101 |
| 2 | Mohit | 102 |
| 3 | Abhiram | NULL |
| 4 | Hemesh | 104 |

```sql
SELECT * FROM Departments;
```

### Output

| DepartmentID | DepartmentName |
| --- | --- |
| 101 | Technical |
| 102 | Content |
| 103 | Management |

---

## Example 1: Basic LEFT JOIN

Retrieve all employees along with their department names.

```sql
SELECT Employees.EmployeeName,
       Departments.DepartmentName
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

### Output

| EmployeeName | DepartmentName |
| --- | --- |
| Akash | Technical |
| Mohit | Content |
| Abhiram | NULL |
| Hemesh | NULL |

### Explanation

- All employee records are displayed.
- Matching department names are retrieved.
- Employees without valid departments show NULL values.

---

## Example 2: LEFT JOIN with WHERE Clause

Retrieve employees belonging to the Technical department.

```sql
SELECT Employees.EmployeeName,
       Departments.DepartmentName
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID
WHERE Departments.DepartmentName = 'Technical';
```

### Output

| EmployeeName | DepartmentName |
| --- | --- |
| Akash | Technical |

### Explanation

- LEFT JOIN combines the tables.
- WHERE filters the result to Technical department employees.

---

## Example 3: LEFT JOIN Using Aliases

```sql
SELECT e.EmployeeName,
       d.DepartmentName
FROM Employees e
LEFT JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```

### Explanation

- e and d are aliases.
- Aliases make queries shorter and easier to read.

---

## Example 4: Finding Employees Without Departments

```sql
SELECT EmployeeName
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID
WHERE Departments.DepartmentID IS NULL;
```

### Output

| EmployeeName |
| --- |
| Abhiram |
| Hemesh |

### Explanation

- LEFT JOIN returns all employees.
- Records without matching departments are identified using NULL values.

---

## LEFT JOIN vs INNER JOIN

| Feature | LEFT JOIN | INNER JOIN |
| --- | --- | --- |
| Returns all rows from left table | Yes | No |
| Returns matching rows | Yes | Yes |
| Returns non-matching rows | Yes | No |
| Displays NULL values | Yes | No |
| Used for incomplete relationships | Yes | No |

---

## Common Use Cases

### Employee and Department Management

```sql
SELECT *
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

### Customer and Orders

```sql
SELECT *
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Students and Courses

```sql
SELECT *
FROM Students
LEFT JOIN Courses
ON Students.StudentID = Courses.StudentID;
```

---

## Best Practices

- Use LEFT JOIN when all records from the left table are required.
- Ensure join columns are properly indexed.
- Use aliases for better readability.
- Filter NULL values when finding unmatched records.
- Use meaningful join conditions.

---

## Important Points

- LEFT JOIN returns all rows from the left table.
- Matching rows are retrieved from the right table.
- Non-matching rows contain NULL values.
- LEFT JOIN is also called LEFT OUTER JOIN.
- It is useful for finding missing relationships between tables.

---

## Conclusion

The SQL `LEFT JOIN` is used to retrieve all records from the left table and matching records from the right table. It is particularly useful when analyzing incomplete relationships, identifying unmatched records, and generating comprehensive reports while ensuring that no records from the primary table are lost.



###
