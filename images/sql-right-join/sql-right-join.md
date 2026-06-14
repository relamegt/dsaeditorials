# SQL RIGHT JOIN

## Introduction

The SQL `RIGHT JOIN` (also known as `RIGHT OUTER JOIN`) returns all records from the right table and the matching records from the left table. If no matching record exists in the left table, SQL returns `NULL` values for the left table columns.

RIGHT JOIN is useful when you want to keep all records from the right table regardless of whether matching data exists in the left table.

---

## Why Use RIGHT JOIN?

The `RIGHT JOIN` helps you:

- Retrieve all records from the right table.
- Include matching records from the left table.
- Identify records that have no related data in the left table.
- Analyze incomplete relationships between tables.
- Generate comprehensive reports.

## Syntax

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| RIGHT JOIN | Returns all rows from the right table |
| table1 | Left table providing matching records |
| table2 | Right table whose records are preserved |
| ON | Specifies the join condition |
| column_name | Related column used for matching |

---

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
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT
);

CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees VALUES
(1, 'Akash', 101),
(2, 'Mohit', 102),
(3, 'Abhiram', 101);

INSERT INTO Departments VALUES
(101, 'Technical'),
(102, 'Content'),
(103, 'Management'),
(104, 'Database');
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
| 3 | Abhiram | 101 |

```sql
SELECT * FROM Departments;
```

### Output

| DepartmentID | DepartmentName |
| --- | --- |
| 101 | Technical |
| 102 | Content |
| 103 | Management |
| 104 | Database |

---

## Example 1: Basic RIGHT JOIN

Retrieve all departments along with employee information.

```sql
SELECT Employees.EmployeeName,
       Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

### Output

| EmployeeName | DepartmentName |
| --- | --- |
| Akash | Technical |
| Abhiram | Technical |
| Mohit | Content |
| NULL | Management |
| NULL | Database |

### Explanation

- All departments are displayed.
- Matching employee records are retrieved.
- Departments without employees show NULL values.

---

## Example 2: Finding Departments Without Employees

```sql
SELECT Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID
WHERE Employees.EmployeeID IS NULL;
```

### Output

| DepartmentName |
| --- |
| Management |
| Database |

### Explanation

- RIGHT JOIN returns all departments.
- NULL employee values indicate departments with no employees.

## Example 3: RIGHT JOIN Using Aliases

```sql
SELECT e.EmployeeName,
       d.DepartmentName
FROM Employees e
RIGHT JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```

### Explanation

- e and d are aliases.
- Aliases improve readability and shorten queries.

---

## Applications of RIGHT JOIN

### Find Unassigned Departments

```sql
SELECT d.DepartmentName
FROM Employees e
RIGHT JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE e.EmployeeID IS NULL;
```

### Generate Department Reports

```sql
SELECT *
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

## ---

## RIGHT JOIN vs LEFT JOIN

| Feature | RIGHT JOIN | LEFT JOIN |
| --- | --- | --- |
| Returns all rows from right table | Yes | No |
| Returns all rows from left table | No | Yes |
| Returns matching rows | Yes | Yes |
| Displays NULL values | Yes | Yes |
| Used for preserving right table data | Yes | No |

---

## Best Practices

- Use RIGHT JOIN when all records from the right table are required.
- Use aliases for cleaner queries.
- Ensure join columns are properly indexed.
- Filter NULL values when identifying unmatched records.
- Use meaningful join conditions.

---

## Important Points

- RIGHT JOIN returns all rows from the right table.
- Matching rows are retrieved from the left table.
- Non-matching rows contain NULL values.
- RIGHT JOIN is also called RIGHT OUTER JOIN.
- It helps identify records without corresponding matches.

---

## Conclusion

The SQL `RIGHT JOIN` is used to retrieve all records from the right table and matching records from the left table. It is useful for identifying unmatched records, generating complete reports, and analyzing relationships while ensuring that no records from the right table are omitted.



###
