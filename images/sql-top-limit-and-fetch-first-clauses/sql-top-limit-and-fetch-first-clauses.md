# SQL TOP, LIMIT, and FETCH FIRST Clauses

## Introduction

When working with large databases, it is often unnecessary to retrieve every row from a table. SQL provides several clauses to limit the number of rows returned by a query.

Different database systems use different clauses:

- **TOP** is used in SQL Server and MS Access.
- **LIMIT** is used in MySQL, PostgreSQL, and SQLite.
- **FETCH FIRST** is used in Oracle, PostgreSQL, DB2, and modern SQL standards.

These clauses improve performance and help retrieve only the required records.

## Why Use Row Limiting Clauses?

Row limiting clauses help:

- Retrieve only a specific number of records.
- Improve query performance.
- Support pagination.
- Display top-performing records.
- Reduce unnecessary data transfer.

---

# Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

# Creating a Sample Table

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

---

# Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(1, 'Akash', 'Management', 85000),
(2, 'Mohit', 'Content', 55000),
(3, 'Abhiram', 'Technical', 72000),
(4, 'Hemesh', 'Database', 68000),
(5, 'Sai', 'Technical', 92000),
(6, 'Rahul', 'Content', 50000),
(7, 'Kiran', 'Database', 61000),
(8, 'Nikhil', 'Management', 97000);
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Salary |
| --- | --- | --- | --- |
| 1 | Akash | Management | 85000 |
| 2 | Mohit | Content | 55000 |
| 3 | Abhiram | Technical | 72000 |
| 4 | Hemesh | Database | 68000 |
| 5 | Sai | Technical | 92000 |
| 6 | Rahul | Content | 50000 |
| 7 | Kiran | Database | 61000 |
| 8 | Nikhil | Management | 97000 |

---

# SQL TOP Clause

The `TOP` clause is used in SQL Server and MS Access to limit the number of rows returned.

## Syntax

```sql
SELECT TOP number column_list
FROM table_name;
```

---

## Example 1: Retrieve Top 3 Records

```sql
SELECT TOP 3 *
FROM Employees;
```

### Output

| EmployeeID | EmployeeName |
| --- | --- |
| 1 | Akash |
| 2 | Mohit |
| 3 | Abhiram |

### Explanation

- Returns the first three rows from the table.
- Without ORDER BY, the returned rows depend on table storage order.

---

## Example 2: Top Highest Salaries

```sql
SELECT TOP 3 *
FROM Employees
ORDER BY Salary DESC;
```

### Output

| EmployeeName | Salary |
| --- | --- |
| Nikhil | 97000 |
| Sai | 92000 |
| Akash | 85000 |

### Explanation

- Sorts employees by salary.
- Returns the highest-paid three employees.

---

## Example 3: TOP with WHERE Clause

```sql
SELECT TOP 2 *
FROM Employees
WHERE Salary > 60000
ORDER BY Salary ASC;
```

### Explanation

- Filters employees earning more than 60000.
- Returns the first two records after sorting.

---

## Example 4: TOP PERCENT

```sql
SELECT TOP 50 PERCENT *
FROM Employees;
```

### Explanation

- Returns half of the records from the table.
- Useful when working with percentage-based sampling.

---

# SQL LIMIT Clause

The `LIMIT` clause is commonly used in MySQL, PostgreSQL, and SQLite.

## Syntax

```sql
SELECT column_list
FROM table_name
LIMIT number;
```

---

## Example 1: Retrieve First 3 Rows

```sql
SELECT *
FROM Employees
LIMIT 3;
```

### Output

| EmployeeID | EmployeeName |
| --- | --- |
| 1 | Akash |
| 2 | Mohit |
| 3 | Abhiram |

### Explanation

- Restricts the result set to three rows.

---

## Example 2: Top 3 Highest Salaries

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC
LIMIT 3;
```

### Output

| EmployeeName | Salary |
| --- | --- |
| Nikhil | 97000 |
| Sai | 92000 |
| Akash | 85000 |

---

## Example 3: LIMIT with WHERE Clause

```sql
SELECT *
FROM Employees
WHERE Department = 'Technical'
LIMIT 2;
```

### Explanation

- Retrieves only two employees from the Technical department.

---

# LIMIT with OFFSET

The `OFFSET` clause skips a specified number of rows before returning results.

## Syntax

```sql
SELECT *
FROM table_name
LIMIT row_count OFFSET skip_count;
```

---

## Example 4: Skip First 2 Rows

```sql
SELECT *
FROM Employees
LIMIT 3 OFFSET 2;
```

### Explanation

- Skips the first two records.
- Returns the next three records.

---

## Example 5: Pagination Example

### Page 1

```sql
SELECT *
FROM Employees
LIMIT 3 OFFSET 0;
```

### Page 2

```sql
SELECT *
FROM Employees
LIMIT 3 OFFSET 3;
```

### Page 3

```sql
SELECT *
FROM Employees
LIMIT 3 OFFSET 6;
```

### Explanation

- Frequently used in web applications.
- Displays records page by page.

---

# Finding nth Highest Salary Using LIMIT

## Example: Third Highest Salary

```sql
SELECT Salary
FROM Employees
ORDER BY Salary DESC
LIMIT 1 OFFSET 2;
```

### Output

| Salary |
| --- |
| 85000 |

### Explanation

- Sorts salaries in descending order.
- Skips the first two highest salaries.
- Returns the third highest salary.

---

# SQL FETCH FIRST Clause

The `FETCH FIRST` clause follows the SQL standard and is supported by Oracle, PostgreSQL, and DB2.

## Syntax

```sql
SELECT column_list
FROM table_name
FETCH FIRST n ROWS ONLY;
```

---

## Example 1: Retrieve First 3 Rows

```sql
SELECT *
FROM Employees
FETCH FIRST 3 ROWS ONLY;
```

### Explanation

- Returns the first three rows from the table.

---

## Example 2: Top 3 Highest Salaries

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC
FETCH FIRST 3 ROWS ONLY;
```

### Output

| EmployeeName | Salary |
| --- | --- |
| Nikhil | 97000 |
| Sai | 92000 |
| Akash | 85000 |

---

## Example 3: FETCH FIRST with WHERE Clause

```sql
SELECT *
FROM Employees
WHERE Department = 'Management'
FETCH FIRST 1 ROW ONLY;
```

### Explanation

- Returns only one matching record from the Management department.

---

# Comparison of TOP, LIMIT, and FETCH FIRST

| Feature | TOP | LIMIT | FETCH FIRST |
| --- | --- | --- | --- |
| SQL Server | Yes | No | Yes |
| MySQL | No | Yes | No |
| PostgreSQL | No | Yes | Yes |
| Oracle | No | No | Yes |
| Supports Percentage | Yes | No | No |
| Supports Offset | Through OFFSET-FETCH | Yes | Yes |

---

# Common Use Cases

## Display Top 5 Products

```sql
SELECT *
FROM Products
ORDER BY Price DESC
LIMIT 5;
```

## Display Latest 10 Orders

```sql
SELECT *
FROM Orders
ORDER BY OrderDate DESC
LIMIT 10;
```

## Display Highest Paid Employee

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC
LIMIT 1;
```

---

# Best Practices

- Always use ORDER BY when retrieving top records.
- Use LIMIT and OFFSET for pagination.
- Avoid fetching unnecessary rows.
- Use indexes on sorted columns for better performance.
- Prefer FETCH FIRST when working with SQL-standard databases.

---

# Important Points

- TOP, LIMIT, and FETCH FIRST serve the same purpose.
- Their syntax differs across database systems.
- ORDER BY should be used when retrieving highest or lowest values.
- OFFSET helps implement pagination.
- These clauses improve query efficiency by reducing returned data.

---

# Conclusion

The SQL TOP, LIMIT, and FETCH FIRST clauses are essential tools for controlling query output. They help retrieve only the required number of records, improve performance, and support tasks such as pagination, reporting, and ranking. Understanding the differences between these clauses allows developers to write efficient SQL queries across multiple database systems.



###
