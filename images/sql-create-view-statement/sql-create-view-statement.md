# SQL CREATE VIEW Statement

## Introduction

The SQL `CREATE VIEW` statement is used to create a virtual table based on the result of a SQL query. A view does not store data physically; instead, it displays data from one or more underlying tables whenever it is accessed.

Views help simplify complex queries, improve security, and provide a customized way of viewing data.

## Why Use CREATE VIEW?

The `CREATE VIEW` statement helps you:

- Simplify complex SQL queries.
- Improve database security.
- Hide unnecessary columns from users.
- Reuse frequently executed queries.
- Make reporting easier and more organized.

## Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| CREATE VIEW | Creates a new view |
| view_name | Name of the view |
| AS | Defines the query for the view |
| SELECT | Retrieves data for the view |
| WHERE | Optional filter condition |

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Sample Table

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees VALUES
(101, 'Akash', 'Technical', 75000),
(102, 'Mohit', 'Content', 55000),
(103, 'Abhiram', 'Technical', 72000),
(104, 'Hemanth', 'Management', 85000),
(105, 'Akhil', 'Content', 50000);
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Salary |
| --- | --- | --- | --- |
| 101 | Akash | Technical | 75000 |
| 102 | Mohit | Content | 55000 |
| 103 | Abhiram | Technical | 72000 |
| 104 | Hemanth | Management | 85000 |
| 105 | Akhil | Content | 50000 |

---

## Example 1: Creating a Simple View

Create a view containing employees from the Technical department.

```sql
CREATE VIEW TechnicalEmployees AS
SELECT EmployeeID, EmployeeName, Salary
FROM Employees
WHERE Department = 'Technical';
```

Display the view:

```sql
SELECT * FROM TechnicalEmployees;
```

### Output

| EmployeeID | EmployeeName | Salary |
| --- | --- | --- |
| 101 | Akash | 75000 |
| 103 | Abhiram | 72000 |

### Explanation

- A view named TechnicalEmployees is created.
- Only Technical department employees are displayed.
- The original table remains unchanged.

---

## Example 2: Creating a View with Selected Columns

Create a view showing employee names and departments.

```sql
CREATE VIEW EmployeeDetails AS
SELECT EmployeeName, Department
FROM Employees;
```

Display the view:

```sql
SELECT * FROM EmployeeDetails;
```

### Output

| EmployeeName | Department |
| --- | --- |
| Akash | Technical |
| Mohit | Content |
| Abhiram | Technical |
| Hemanth | Management |
| Akhil | Content |

### Explanation

- Only selected columns are displayed.
- Other columns remain hidden from users.

---

## Example 3: Creating a View Using Multiple Tables

Create a Departments table:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);
```

Insert records:

```sql
INSERT INTO Departments VALUES
(1, 'Technical'),
(2, 'Content'),
(3, 'Management');
```

Create a new Employees table:

```sql
CREATE TABLE EmployeeDepartment (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT
);
```

Insert records:

```sql
INSERT INTO EmployeeDepartment VALUES
(101, 'Akash', 1),
(102, 'Mohit', 2),
(103, 'Abhiram', 1),
(104, 'Hemanth', 3),
(105, 'Akhil', 2);
```

Create a joined view:

```sql
CREATE VIEW EmployeeDepartmentView AS
SELECT
e.EmployeeName,
d.DepartmentName
FROM EmployeeDepartment e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```

Display the view:

```sql
SELECT * FROM EmployeeDepartmentView;
```

### Output

| EmployeeName | DepartmentName |
| --- | --- |
| Akash | Technical |
| Mohit | Content |
| Abhiram | Technical |
| Hemanth | Management |
| Akhil | Content |

### Explanation

- Data from two tables is combined.
- The view behaves like a virtual joined table.

---

## Example 4: Updating Data Through a View

Update salary using a view.

```sql
UPDATE TechnicalEmployees
SET Salary = 80000
WHERE EmployeeID = 101;
```

Display Employees table:

```sql
SELECT * FROM Employees;
```

### Explanation

- Changes made through the view affect the underlying table.
- Not all views are updatable, depending on their complexity.

---

## Example 5: Deleting a View

Remove an existing view.

```sql
DROP VIEW TechnicalEmployees;
```

### Explanation

- Only the view is deleted.
- Original table data remains unchanged.

---

## Common Use Cases

### Department-Specific Reports

```sql
CREATE VIEW TechnicalEmployees AS
SELECT *
FROM Employees
WHERE Department = 'Technical';
```

### Hide Sensitive Data

```sql
CREATE VIEW EmployeePublicInfo AS
SELECT EmployeeID, EmployeeName
FROM Employees;
```

### Simplify Complex Queries

```sql
CREATE VIEW EmployeeDepartmentView AS
SELECT ...
```

## Benefits of Views

### Simplifies Queries

Complex queries can be stored and reused.

### Improves Security

Users can access limited data through views.

### Provides Data Abstraction

Underlying table structure remains hidden.

### Enhances Reusability

Frequently used queries can be accessed easily.

---

## Best Practices

- Use meaningful view names.
- Avoid overly complex views.
- Restrict access through views when possible.
- Update views when underlying table structures change.
- Use views for reporting and data presentation.

---

## Important Points

- A view is a virtual table.
- Views do not store data physically.
- Data is retrieved from underlying tables.
- Views can simplify complex queries.
- Views can improve security by limiting visible columns.
- Changes in base tables are reflected in views.

---

## Conclusion

The SQL `CREATE VIEW` statement allows you to create virtual tables that simplify data access and improve security. Views help organize complex queries, provide customized data access, and make database applications easier to manage. They are widely used in reporting, data abstraction, and access control within relational databases.



###
