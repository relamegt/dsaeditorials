# SQL DROP VIEW Statement

## Introduction

The SQL `DROP VIEW` statement is used to remove an existing view from a database. When a view is dropped, only the view definition is deleted; the underlying tables and their data remain unchanged.

The DROP VIEW command is commonly used to:

- Remove outdated views.
- Delete unused views.
- Improve database maintainability.
- Reduce unnecessary database objects.
- Prevent access to unwanted virtual tables.

---

## Why Use DROP VIEW?

The `DROP VIEW` statement helps you:

- Remove obsolete views.
- Keep the database organized.
- Simplify schema management.
- Eliminate unused virtual tables.
- Improve database readability.

---

## Syntax

```sql
DROP VIEW view_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| DROP VIEW | Deletes an existing view |
| view_name | Name of the view to remove |

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
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Position VARCHAR(50),
    Salary DECIMAL(10,2),
    Department VARCHAR(50)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Employees VALUES
(1, 'Akash', 'SQL Developer', 65000, 'IT'),
(2, 'Akhil', 'Java Developer', 55000, 'IT'),
(3, 'Hemanth', 'Database Administrator', 70000, 'Database'),
(4, 'Mohit', 'Analyst', 45000, 'Analytics'),
(5, 'Abhiram', 'Python Developer', 60000, 'IT');
```

Display the table:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Position | Salary | Department |
| --- | --- | --- | --- | --- |
| 1 | Akash | SQL Developer | 65000 | IT |
| 2 | Akhil | Java Developer | 55000 | IT |
| 3 | Hemanth | Database Administrator | 70000 | Database |
| 4 | Mohit | Analyst | 45000 | Analytics |
| 5 | Abhiram | Python Developer | 60000 | IT |

---

## Example 1: Creating a View

Create a view for employees earning more than 50,000.

```sql
CREATE VIEW HighSalaryEmployees AS
SELECT *
FROM Employees
WHERE Salary > 50000;
```

Display the view:

```sql
SELECT * FROM HighSalaryEmployees;
```

### Output

| EmployeeID | EmployeeName | Position | Salary | Department |
| --- | --- | --- | --- | --- |
| 1 | Akash | SQL Developer | 65000 |  |
| 2 | Akhil | Java Developer | 55000 |  |
| 3 | Hemanth | Database Administrator | 70000 |  |
| 5 | Abhiram | Python Developer | 60000 |  |

### Explanation

- The view displays employees with salaries above 50,000.
- The view acts as a virtual table.
- Data is fetched from the Employees table.

---

## Example 2: Creating a Department View

Create a view for IT employees.

```sql
CREATE VIEW ITEmployees AS
SELECT *
FROM Employees
WHERE Department = 'IT';
```

Display the view:

```sql
SELECT * FROM ITEmployees;
```

### Output

| EmployeeID | EmployeeName | Department |
| --- | --- | --- |
| 1 | Akash | IT |
| 2 | Akhil | IT |
| 5 | Abhiram | IT |

### Explanation

- The view filters employees belonging to the IT department.
- Only IT department records are displayed.

---

## Example 3: Display Available Views

View all created views.

```sql
SELECT TABLE_NAME
FROM INFORMATION_SCHEMA.VIEWS;
```

### Output

| TABLE_NAME |
| --- |
| HighSalaryEmployees |
| ITEmployees |

### Explanation

- INFORMATION_SCHEMA.VIEWS stores metadata about views.
- This query lists all available views in the database.

---

## Example 4: Dropping a View

Delete the HighSalaryEmployees view.

```sql
DROP VIEW HighSalaryEmployees;
```

### Explanation

- The view definition is removed.
- The Employees table remains unchanged.
- Only the virtual table is deleted.

---

## Example 5: Dropping Multiple Views

Delete multiple views.

```sql
DROP VIEW ITEmployees;
```

### Explanation

- The specified view is permanently removed.
- Underlying table data remains intact.

---

## Example 6: Verifying View Deletion

Attempt to access the deleted view.

```sql
SELECT * FROM HighSalaryEmployees;
```

### Output

```text
ERROR: View 'HighSalaryEmployees' does not exist.
```

### Explanation

- The view was successfully removed.
- SQL cannot locate the deleted view.
- The query generates an error.

---

## Best Practices

- Verify that a view is no longer required before deleting it.
- Check dependent applications before dropping views.
- Keep only necessary views in production databases.
- Document view removals for maintenance purposes.
- Use INFORMATION_SCHEMA.VIEWS to review existing views.

---

## Important Points

- DROP VIEW removes only the view definition.
- Base table data is never deleted.
- Deleted views cannot be queried.
- Multiple views can be removed individually.
- Views can be recreated later if needed.

---

## Conclusion

The SQL `DROP VIEW` statement is used to delete views that are no longer required in a database. Since views are virtual tables, removing them affects only their definitions and not the actual data stored in underlying tables. Proper use of DROP VIEW helps maintain a clean, organized, and efficient database structure.



###
