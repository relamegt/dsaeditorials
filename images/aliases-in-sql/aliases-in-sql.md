# Aliases in SQL

## Introduction

In SQL, an alias is a temporary name assigned to a column or a table during query execution. Aliases improve query readability and make complex SQL statements easier to write and understand.

Aliases do not permanently change the names of tables or columns in the database. They exist only for the duration of the query execution.

## Why Use Aliases?

Aliases are commonly used to:

- Improve query readability.
- Provide meaningful column names in reports.
- Simplify long table names.
- Make JOIN queries easier to write.
- Improve the presentation of calculated values.

## Types of Aliases

SQL supports two types of aliases:

1. Column Aliases
2. Table Aliases

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
    Salary DECIMAL(10,2),
    City VARCHAR(50)
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(1, 'Akash', 'Management', 85000, 'Vijayawada'),
(2, 'Mohit', 'Content', 55000, 'Hyderabad'),
(3, 'Abhiram', 'Technical', 72000, 'Vijayawada'),
(4, 'Hemesh', 'Database', 68000, 'Guntur'),
(5, 'Sai', 'Technical', 92000, 'Hyderabad');
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Salary | City |
| --- | --- | --- | --- | --- |
| 1 | Akash | Management | 85000 | Vijayawada |
| 2 | Mohit | Content | 55000 | Hyderabad |
| 3 | Abhiram | Technical | 72000 | Vijayawada |
| 4 | Hemesh | Database | 68000 | Guntur |
| 5 | Sai | Technical | 92000 | Hyderabad |

---

## Column Aliases

Column aliases provide temporary names for columns in the result set.

They are useful when:

- Column names are lengthy.
- Aggregate functions are used.
- Calculated values need meaningful headings.
- Reports require user-friendly column names.

### Syntax

```sql
SELECT column_name AS alias_name
FROM table_name;
```

The `AS` keyword is optional.

---

## Example 1: Basic Column Alias

```sql
SELECT EmployeeID AS ID
FROM Employees;
```

### Output

| ID |
| --- |
| -- |
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |

### Explanation

- EmployeeID is displayed as ID.
- The original column name remains unchanged in the database.

---

## Example 2: Alias Without AS

```sql
SELECT EmployeeName Employee
FROM Employees;
```

### Output

| Employee |
| --- |
| Akash |
| Mohit |
| Abhiram |
| Hemesh |
| Sai |

### Explanation

- SQL allows aliases without the AS keyword.
- The result is identical.

---

## Example 3: Alias for Calculated Columns

```sql
SELECT EmployeeName,
       Salary * 12 AS AnnualSalary
FROM Employees;
```

### Output

| EmployeeName | AnnualSalary |
| --- | --- |
| Akash | 1020000 |
| Mohit | 660000 |
| Abhiram | 864000 |
| Hemesh | 816000 |
| Sai | 1104000 |

### Explanation

- The calculated value receives a meaningful name.
- This makes reports easier to understand.

---

## Example 4: Alias for Aggregate Functions

```sql
SELECT COUNT(*) AS TotalEmployees
FROM Employees;
```

### Output

| TotalEmployees |
| --- |
| 5 |

### Explanation

- Aggregate functions often produce unclear column headings.
- Aliases improve readability.

---

## Table Aliases

Table aliases assign temporary names to tables.

They are particularly useful when:

- Working with JOIN operations.
- Referencing multiple tables.
- Writing self-joins.
- Simplifying long table names.

### Syntax

```sql
SELECT column_name
FROM table_name AS alias_name;
```

---

## Example 5: Basic Table Alias

```sql
SELECT e.EmployeeName,
       e.Department
FROM Employees AS e;
```

### Explanation

- Employees is temporarily renamed to e.
- The query becomes shorter and easier to read.

---

## Example 6: Table Alias Without AS

```sql
SELECT e.EmployeeName,
       e.Salary
FROM Employees e;
```

### Explanation

- AS is optional for table aliases.
- The query behaves exactly the same.

---

## Example 7: Combining Column and Table Aliases

```sql
SELECT e.EmployeeName AS Name,
       e.Department AS Team,
       e.Salary AS MonthlySalary
FROM Employees AS e;
```

### Output

| Name | Team | MonthlySalary |
| --- | --- | --- |
| Akash | Management | 85000 |
| Mohit | Content | 55000 |
| Abhiram | Technical | 72000 |
| Hemesh | Database | 68000 |
| Sai | Technical | 92000 |

### Explanation

- e is the table alias.
- Name, Team, and MonthlySalary are column aliases.
- Both types of aliases can be used together.

---

## Aliases in JOIN Queries

Aliases become extremely useful when multiple tables are involved.

### Creating Another Table

```sql
CREATE TABLE Projects (
    ProjectID INT PRIMARY KEY,
    EmployeeID INT,
    ProjectName VARCHAR(100)
);
```

Insert sample records:

```sql
INSERT INTO Projects
VALUES
(101, 1, 'ERP System'),
(102, 3, 'Inventory Portal'),
(103, 5, 'Cloud Migration');
```

---

## Example 8: JOIN with Aliases

```sql
SELECT e.EmployeeName AS Employee,
       p.ProjectName AS Project
FROM Employees e
INNER JOIN Projects p
ON e.EmployeeID = p.EmployeeID;
```

### Output

| Employee | Project |
| --- | --- |
| Akash | ERP System |
| Abhiram | Inventory Portal |
| Sai | Cloud Migration |

### Explanation

- e refers to the Employees table.
- p refers to the Projects table.
- Aliases simplify JOIN queries significantly.

---

## Example 9: Aliases with Aggregate Functions

```sql
SELECT Department,
       AVG(Salary) AS AverageSalary
FROM Employees
GROUP BY Department;
```

### Output

| Department | AverageSalary |
| --- | --- |
| Management | 85000 |
| Content | 55000 |
| Technical | 82000 |
| Database | 68000 |

### Explanation

- AVG(Salary) calculates the average salary of each department.
- The alias AverageSalary provides a meaningful column heading.

---

## Rules for Aliases

- Aliases exist only during query execution.
- They do not permanently rename columns or tables.
- AS is optional in most database systems.
- Aliases containing spaces should be enclosed in quotes.

Example:

```sql
SELECT EmployeeName AS "Employee Name"
FROM Employees;
```

---

## Common Use Cases

### Rename Columns in Reports

```sql
SELECT EmployeeName AS Name
FROM Employees;
```

### Simplify Long Table Names

```sql
SELECT e.EmployeeName
FROM Employees e;
```

### Display Calculated Values

```sql
SELECT Salary * 12 AS AnnualSalary
FROM Employees;
```

### Improve Aggregate Results

```sql
SELECT COUNT(*) AS TotalRecords
FROM Employees;
```

---

## Best Practices

- Use meaningful alias names.
- Use table aliases in JOIN queries.
- Use aliases for calculated columns.
- Avoid overly short aliases in complex queries.
- Maintain consistent alias naming conventions.

---

## Important Points

- Aliases are temporary names for columns or tables.
- They improve readability and maintainability.
- AS is optional in most SQL databases.
- Column aliases affect only the output.
- Table aliases simplify complex queries.
- Aliases are heavily used in JOIN operations and reporting.

---

## Conclusion

Aliases in SQL provide temporary and meaningful names for columns and tables, making queries easier to read, write, and maintain. They are especially valuable in reporting, aggregate functions, calculated columns, and JOIN operations. Proper use of aliases results in cleaner, more professional, and maintainable SQL code.



###
