# SQL Aggregate Functions

## Introduction

SQL Aggregate Functions are used to perform calculations on multiple rows of data and return a single summarized result. They help analyze large datasets by calculating totals, averages, counts, minimum values, maximum values, and more.

Aggregate functions are widely used in reporting, data analysis, and business intelligence applications.

## Why Use Aggregate Functions?

Aggregate functions help you:

- Summarize large amounts of data.
- Calculate totals and averages.
- Find minimum and maximum values.
- Count records efficiently.
- Generate reports and analytical insights.

## Common Aggregate Functions

The most frequently used aggregate functions in SQL are:

1. COUNT()
2. SUM()
3. AVG()
4. MIN()
5. MAX()

## Syntax

```sql
AGGREGATE_FUNCTION(column_name)
```

### Syntax Components

| Component | Description |
| --- | --- |
| AGGREGATE_FUNCTION | Function such as COUNT, SUM, AVG, MIN, or MAX |
| column_name | Column on which the calculation is performed |

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
INSERT INTO Employees
VALUES
(1, 'Akash', 'Management', 85000),
(2, 'Mohit', 'Content', 55000),
(3, 'Abhiram', 'Technical', 72000),
(4, 'Hemesh', 'Database', 68000),
(5, 'Sai', 'Technical', 92000),
(6, 'Rahul', 'Content', NULL);
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
| 6 | Rahul | Content | NULL |

---

## COUNT() Function

The `COUNT()` function returns the number of rows that match a specified condition.

### Types of COUNT()

- `COUNT(*)` → Counts all rows.
- `COUNT(column_name)` → Counts non-NULL values.
- `COUNT(DISTINCT column_name)` → Counts unique non-NULL values.

### Example 1: Count All Records

```sql
SELECT COUNT(*) AS TotalEmployees
FROM Employees;
```

### Output

| TotalEmployees |
| --- |
| 6 |

### Explanation

- Counts every row in the table.
- NULL values are also included because rows are counted.

---

### Example 2: Count Non-NULL Salaries

```sql
SELECT COUNT(Salary) AS EmployeesWithSalary
FROM Employees;
```

### Output

| EmployeesWithSalary |
| --- |
| 5 |

### Explanation

- Counts only rows where Salary is not NULL.
- The NULL salary value is ignored.

---

### Example 3: Count Unique Departments

```sql
SELECT COUNT(DISTINCT Department) AS UniqueDepartments
FROM Employees;
```

### Output

| UniqueDepartments |
| --- |
| 4 |

### Explanation

- Duplicate department values are counted only once.
- Useful for identifying unique categories.

---

## SUM() Function

The `SUM()` function calculates the total of a numeric column.

### Example 4: Calculate Total Salary

```sql
SELECT SUM(Salary) AS TotalSalary
FROM Employees;
```

### Output

| TotalSalary |
| --- |
| 372000 |

### Explanation

- Adds all non-NULL salary values.
- NULL values are ignored.

---

### Example 5: Sum of Distinct Salaries

```sql
SELECT SUM(DISTINCT Salary) AS DistinctSalaryTotal
FROM Employees;
```

### Output

| DistinctSalaryTotal |
| --- |
| 372000 |

### Explanation

- Adds only unique salary values.
- Duplicate values are excluded.

---

## AVG() Function

The `AVG()` function calculates the average of numeric values.

### Example 6: Average Salary

```sql
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
```

### Output

| AverageSalary |
| --- |
| 74400 |

### Explanation

- Adds all non-NULL salaries.
- Divides by the number of non-NULL salary records.

---

### Example 7: Average of Distinct Salaries

```sql
SELECT AVG(DISTINCT Salary) AS DistinctAverageSalary
FROM Employees;
```

### Output

| DistinctAverageSalary |
| --- |
| 74400 |

### Explanation

- Uses only unique salary values.
- Duplicate salaries are ignored.

---

## MIN() Function

The `MIN()` function returns the smallest value in a column.

### Example 8: Lowest Salary

```sql
SELECT MIN(Salary) AS LowestSalary
FROM Employees;
```

### Output

| LowestSalary |
| --- |
| 55000 |

### Explanation

- Finds the smallest non-NULL salary.
- NULL values are ignored.

---

## MAX() Function

The `MAX()` function returns the largest value in a column.

### Example 9: Highest Salary

```sql
SELECT MAX(Salary) AS HighestSalary
FROM Employees;
```

### Output

| HighestSalary |
| --- |
| 92000 |

### Explanation

- Finds the largest salary value.
- NULL values are ignored.

---

## Aggregate Functions with GROUP BY

Aggregate functions are commonly used with the `GROUP BY` clause.

### Example 10: Average Salary by Department

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

- Employees are grouped by department.
- Average salary is calculated for each department.

---

## Aggregate Functions with HAVING

The `HAVING` clause filters grouped results.

### Example 11: Departments with Average Salary Above 70000

```sql
SELECT Department,
       AVG(Salary) AS AverageSalary
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 70000;
```

### Output

| Department | AverageSalary |
| --- | --- |
| Management | 85000 |
| Technical | 82000 |

### Explanation

- HAVING filters groups after aggregation.
- Only departments with average salary above 70000 are displayed.

---

## Aggregate Functions and NULL Values

Most aggregate functions ignore NULL values.

Consider the following query:

```sql
SELECT
COUNT(Salary),
SUM(Salary),
AVG(Salary),
MIN(Salary),
MAX(Salary)
FROM Employees;
```

### Explanation

- NULL values are ignored by COUNT(column), SUM(), AVG(), MIN(), and MAX().
- COUNT(*) is the only aggregate function that counts all rows regardless of NULL values.

---

## Aggregate Functions vs Scalar Functions

| Feature | Aggregate Functions | Scalar Functions |
| --- | --- | --- |
| Operate on multiple rows | Yes | No |
| Return one result | Yes | No |
| Used for summarization | Yes | No |
| Example | COUNT(), SUM() | UPPER(), LOWER() |

---

## Common Use Cases

### Count Total Customers

```sql
SELECT COUNT(*) AS TotalCustomers
FROM Customers;
```

### Calculate Total Sales

```sql
SELECT SUM(Amount) AS TotalSales
FROM Orders;
```

### Find Average Marks

```sql
SELECT AVG(Marks) AS AverageMarks
FROM Students;
```

### Find Highest Product Price

```sql
SELECT MAX(Price) AS HighestPrice
FROM Products;
```

### Find Lowest Product Price

```sql
SELECT MIN(Price) AS LowestPrice
FROM Products;
```

---

## Best Practices

- Use aggregate functions for summarizing data.
- Combine GROUP BY with aggregate functions when analyzing categories.
- Use HAVING to filter aggregated results.
- Understand how NULL values affect calculations.
- Use DISTINCT when unique values are required.

---

## Important Points

- Aggregate functions operate on multiple rows and return a single result.
- Common aggregate functions are COUNT(), SUM(), AVG(), MIN(), and MAX().
- Most aggregate functions ignore NULL values.
- Aggregate functions are frequently used with GROUP BY and HAVING.
- DISTINCT can be combined with aggregate functions.
- They are essential for reporting and data analysis.

---

## Conclusion

SQL Aggregate Functions provide powerful tools for summarizing and analyzing data. Functions such as COUNT(), SUM(), AVG(), MIN(), and MAX() help transform large datasets into meaningful insights. When combined with GROUP BY and HAVING clauses, aggregate functions become essential for reporting, business intelligence, and decision-making applications.



###
