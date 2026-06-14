# SQL DELETE JOIN

## Introduction

The SQL `DELETE JOIN` statement is used to delete records from one table based on matching data in another table. It combines the functionality of a JOIN and DELETE operation, allowing precise removal of related records.

DELETE JOIN is commonly used when records in one table depend on information stored in another table.

## Why Use DELETE JOIN?

The `DELETE JOIN` statement helps you:

- Delete records using conditions from another table.
- Remove unwanted related data efficiently.
- Maintain database consistency.
- Avoid complex subqueries.
- Delete specific records based on relationships.

## Syntax

### DELETE with INNER JOIN

```sql
DELETE table1
FROM table1
JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| DELETE | Removes records from a table |
| JOIN | Connects related tables |
| ON | Defines the join condition |
| WHERE | Filters rows to delete |
| table1 | Table from which rows are deleted |

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
    DepartmentName VARCHAR(50)
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
(102, 'HR'),
(103, 'Finance');

INSERT INTO Employees VALUES
(1, 'Akash', 101),
(2, 'Mohit', 102),
(3, 'Abhiram', 102),
(4, 'Hemanth', 103),
(5, 'Akhil', 101);
```

Display employee records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID |
| --- | --- | --- |
| 1 | Akash | 101 |
| 2 | Mohit | 102 |
| 3 | Abhiram | 102 |
| 4 | Hemanth | 103 |
| 5 | Akhil | 101 |

---

## Example 1: DELETE Records Using JOIN

Delete employees belonging to the HR department.

```sql
DELETE e
FROM Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName = 'HR';
```

Display records after deletion:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID |
| --- | --- | --- |
| 1 | Akash | 101 |
| 4 | Hemanth | 103 |
| 5 | Akhil | 101 |

### Explanation

- Employees and Departments tables are joined.
- Employees belonging to the HR department are identified.
- Matching employee records are deleted.

---

## Example 2: DELETE Specific Employee Records

Delete employees from the Finance department.

```sql
DELETE e
FROM Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName = 'Finance';
```

### Explanation

- Finance department employees are selected through the join.
- Matching rows are removed from the Employees table.

---

## Example 3: DELETE Customer Orders Using JOIN

Create sample tables:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    Status VARCHAR(20)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    ProductName VARCHAR(100)
);
```

Insert records:

```sql
INSERT INTO Customers VALUES
(1, 'Akash', 'Active'),
(2, 'Mohit', 'Inactive'),
(3, 'Abhiram', 'Active');

INSERT INTO Orders VALUES
(101, 1, 'Laptop'),
(102, 2, 'Keyboard'),
(103, 3, 'Mouse');
```

Delete orders of inactive customers:

```sql
DELETE o
FROM Orders o
JOIN Customers c
ON o.CustomerID = c.CustomerID
WHERE c.Status = 'Inactive';
```

Display orders:

```sql
SELECT * FROM Orders;
```

### Output

| OrderID | CustomerID | ProductName |
| --- | --- | --- |
| 101 | 1 | Laptop |
| 103 | 3 | Mouse |

### Explanation

- Orders are matched with customers.
- Orders belonging to inactive customers are deleted.
- Remaining orders stay unchanged.

---

## Applications of DELETE JOIN

### Remove Inactive Customer Orders

```sql
DELETE o
FROM Orders o
JOIN Customers c
ON o.CustomerID = c.CustomerID
WHERE c.Status = 'Inactive';
```

### Remove Employees from a Specific Department

```sql
DELETE e
FROM Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName = 'HR';
```

### Delete Related Records Efficiently

```sql
DELETE t1
FROM Table1 t1
JOIN Table2 t2
ON t1.ID = t2.ID
WHERE t2.Status = 'Inactive';
```

## DELETE vs DELETE JOIN

| Feature | DELETE | DELETE JOIN |
| --- | --- | --- |
| Uses single table | Yes | No |
| Uses multiple tables | No | Yes |
| Supports relationship-based deletion | No | Yes |
| Useful for linked data | Limited | Yes |

---

## Best Practices

- Always test the JOIN with SELECT before deleting.
- Use WHERE conditions carefully.
- Take backups before bulk deletions.
- Verify affected rows before execution.
- Use transactions when deleting critical data.

---

## Important Points

- DELETE JOIN removes rows from only one table.
- JOIN helps identify records using related tables.
- WHERE controls which rows are deleted.
- INNER JOIN is the most commonly used DELETE JOIN.
- Always verify data before running DELETE statements.

---

## Conclusion

The SQL `DELETE JOIN` statement allows records to be removed based on conditions in related tables. It provides a powerful way to manage linked data, maintain consistency, and perform targeted deletions efficiently in relational databases.



###
