# SQL UPDATE with JOIN

## Introduction

The SQL `UPDATE with JOIN` statement is used to update records in one table using data from another related table. It is useful when changes need to be made based on matching rows between tables.

This feature helps synchronize data, apply updates efficiently, and avoid multiple queries.

## Why Use UPDATE with JOIN?

The `UPDATE with JOIN` helps you:

- Update data using values from another table.
- Synchronize related tables.
- Modify multiple records efficiently.
- Avoid writing complex subqueries.
- Maintain data consistency.

## Syntax

### UPDATE with INNER JOIN

```sql
UPDATE table1
JOIN table2
ON table1.column_name = table2.column_name
SET table1.column_name = table2.column_name;
```

### UPDATE with LEFT JOIN

```sql
UPDATE table1
LEFT JOIN table2
ON table1.column_name = table2.column_name
SET table1.column_name = table2.column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| UPDATE | Modifies existing records |
| JOIN | Connects related tables |
| ON | Specifies the matching condition |
| SET | Defines the columns to update |
| LEFT JOIN | Updates rows even without matches |

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
    DepartmentName VARCHAR(100),
    Bonus DECIMAL(10,2)
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    Salary DECIMAL(10,2)
);
```

## Inserting Sample Records

```sql
INSERT INTO Departments VALUES
(101, 'Technical', 5000),
(102, 'Content', 3000),
(103, 'Management', 7000);

INSERT INTO Employees VALUES
(1, 'Akash', 101, 50000),
(2, 'Mohit', 102, 45000),
(3, 'Abhiram', 103, 60000);
```

Display employee data:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID | Salary |
| --- | --- | --- | --- |
| 1 | Akash | 101 | 50000 |
| 2 | Mohit | 102 | 45000 |
| 3 | Abhiram | 103 | 60000 |

---

## Example 1: UPDATE with INNER JOIN

Increase employee salaries using department bonuses.

```sql
UPDATE Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
SET e.Salary = e.Salary + d.Bonus;
```

Display updated data:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID | Salary |
| --- | --- | --- | --- |
| 1 | Akash | 101 | 55000 |
| 2 | Mohit | 102 | 48000 |
| 3 | Abhiram | 103 | 67000 |

### Explanation

- Employees are matched with departments.
- Bonus values are added to salaries.
- Only matching records are updated.

---

## Example 2: UPDATE Specific Records

Increase salary only for employees in the Technical department.

```sql
UPDATE Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
SET e.Salary = e.Salary + 2000
WHERE d.DepartmentName = 'Technical';
```

### Explanation

- Only Technical department employees are updated.
- Other employee records remain unchanged.

---

## Example 3: UPDATE with LEFT JOIN

```sql
UPDATE Employees e
LEFT JOIN Departments d
ON e.DepartmentID = d.DepartmentID
SET e.Salary = e.Salary + IFNULL(d.Bonus, 0);
```

### Explanation

- All employee records are considered.
- Employees without matching departments receive 0 bonus.
- Useful when some relationships may be missing.

---

## Applications of UPDATE with JOIN

### Synchronize Related Tables

```sql
UPDATE Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
SET e.DepartmentName = d.DepartmentName;
```

### Apply Bonus Updates

```sql
UPDATE Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
SET e.Salary = e.Salary + d.Bonus;
```

### Correct Existing Data

```sql
UPDATE table1
JOIN table2
ON table1.ID = table2.ID
SET table1.Column = table2.Column;
```

---

## INNER JOIN vs LEFT JOIN in UPDATE

| Feature | INNER JOIN | LEFT JOIN |
| --- | --- | --- |
| Updates matching rows only | Yes | No |
| Includes non-matching rows | No | Yes |
| Returns unmatched rows | No | Yes |
| Commonly used | Yes | Less Often |

---

## Best Practices

- Always verify records using SELECT before UPDATE.
- Use WHERE conditions to avoid accidental updates.
- Create backups before bulk updates.
- Ensure join columns are indexed.
- Test updates on sample data first.

---

## Important Points

- UPDATE with JOIN modifies one table using another table's data.
- INNER JOIN updates only matching rows.
- LEFT JOIN can include non-matching rows.
- JOIN conditions must be carefully defined.
- Always preview affected records before updating.

---

## Conclusion

The SQL `UPDATE with JOIN` statement allows data in one table to be updated using related data from another table. It simplifies bulk updates, improves consistency, and helps maintain synchronized information across multiple tables.



###
