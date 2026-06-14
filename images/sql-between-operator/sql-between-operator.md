# SQL BETWEEN Operator

## Introduction

The SQL `BETWEEN` operator is used to filter records that fall within a specified range of values. It can be used with numeric values, dates, and text values.

The `BETWEEN` operator includes both the starting and ending values of the specified range, making it an inclusive operator.

## Why Use BETWEEN?

The `BETWEEN` operator helps you:

- Retrieve values within a specific range.
- Simplify range-based filtering.
- Improve query readability.
- Work with numbers, dates, and strings.
- Reduce the need for multiple comparison operators.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Syntax Components

| Component | Description |
| --- | --- |
| BETWEEN | Checks whether a value falls within a range |
| value1 | Starting value of the range |
| value2 | Ending value of the range |
| column_name | Column being evaluated |

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
    Age INT,
    Salary DECIMAL(10,2),
    HireDate DATE
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(1, 'Akash', 'Management', 28, 85000, '2020-03-15'),
(2, 'Mohit', 'Content', 24, 55000, '2021-07-20'),
(3, 'Abhiram', 'Technical', 31, 72000, '2019-09-10'),
(4, 'Hemesh', 'Database', 38, 68000, '2022-01-05'),
(5, 'Sai', 'Technical', 42, 92000, '2018-11-12'),
(6, 'Rahul', 'Content', 26, 50000, '2020-06-25');
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Age | Salary | HireDate |
| --- | --- | --- | --- | --- | --- |
| 1 | Akash | Management | 28 | 85000 | 2020-03-15 |
| 2 | Mohit | Content | 24 | 55000 | 2021-07-20 |
| 3 | Abhiram | Technical | 31 | 72000 | 2019-09-10 |
| 4 | Hemesh | Database | 38 | 68000 | 2022-01-05 |
| 5 | Sai | Technical | 42 | 92000 | 2018-11-12 |
| 6 | Rahul | Content | 26 | 50000 | 2020-06-25 |

---

## Example 1: BETWEEN with Numeric Values

Retrieve employees whose age is between 25 and 35.

```sql
SELECT EmployeeName, Age
FROM Employees
WHERE Age BETWEEN 25 AND 35;
```

### Output

| EmployeeName | Age |
| --- | --- |
| Akash | 28 |
| Abhiram | 31 |
| Rahul | 26 |

### Explanation

- The query checks whether Age falls between 25 and 35.
- Both boundary values are included.
- Only matching employees are returned.

---

## Example 2: BETWEEN with Salary Range

Retrieve employees whose salary is between 60000 and 90000.

```sql
SELECT EmployeeName, Salary
FROM Employees
WHERE Salary BETWEEN 60000 AND 90000;
```

### Output

| EmployeeName | Salary |
| --- | --- |
| Akash | 85000 |
| Abhiram | 72000 |
| Hemesh | 68000 |

### Explanation

- Salaries within the specified range are selected.
- Employees outside the range are excluded.

---

## Example 3: BETWEEN with Dates

Retrieve employees hired between January 1, 2020 and December 31, 2021.

```sql
SELECT EmployeeName, HireDate
FROM Employees
WHERE HireDate BETWEEN '2020-01-01' AND '2021-12-31';
```

### Output

| EmployeeName | HireDate |
| --- | --- |
| Akash | 2020-03-15 |
| Mohit | 2021-07-20 |
| Rahul | 2020-06-25 |

### Explanation

- BETWEEN works with date values.
- Both start and end dates are included.
- Employees hired during the specified period are returned.

---

## Example 4: NOT BETWEEN

Retrieve employees whose age is not between 25 and 35.

```sql
SELECT EmployeeName, Age
FROM Employees
WHERE Age NOT BETWEEN 25 AND 35;
```

### Output

| EmployeeName | Age |
| --- | --- |
| Mohit | 24 |
| Hemesh | 38 |
| Sai | 42 |

### Explanation

- NOT BETWEEN reverses the condition.
- Employees whose age falls outside the range are returned.

---

## Example 5: BETWEEN with Text Values

Retrieve employees whose names are alphabetically between 'A' and 'M'.

```sql
SELECT EmployeeName
FROM Employees
WHERE EmployeeName BETWEEN 'A' AND 'M';
```

### Output

| EmployeeName |
| --- |
| Abhiram |
| Akash |
| Hemesh |

### Explanation

- SQL compares text values alphabetically.
- Names falling within the specified alphabetical range are returned.

---

## Example 6: BETWEEN with AND Condition

Retrieve employees whose salary is between 50000 and 80000 and belong to the Technical department.

```sql
SELECT EmployeeName, Salary, Department
FROM Employees
WHERE Salary BETWEEN 50000 AND 80000
AND Department = 'Technical';
```

### Output

| EmployeeName | Salary | Department |
| --- | --- | --- |
| Abhiram | 72000 | Technical |

### Explanation

- BETWEEN filters salaries within the specified range.
- The AND condition further filters by department.

---

## Example 7: BETWEEN with ORDER BY

Retrieve employees aged between 25 and 40 and display them in ascending order of age.

```sql
SELECT EmployeeName, Age
FROM Employees
WHERE Age BETWEEN 25 AND 40
ORDER BY Age;
```

### Output

| EmployeeName | Age |
| --- | --- |
| Rahul | 26 |
| Akash | 28 |
| Abhiram | 31 |
| Hemesh | 38 |

### Explanation

- BETWEEN filters the records.
- ORDER BY sorts the result based on age.

---

## Example 8: Using BETWEEN for Product Prices

```sql
SELECT ProductName, Price
FROM Products
WHERE Price BETWEEN 1000 AND 5000;
```

### Explanation

- Retrieves products priced within the specified range.
- Commonly used in e-commerce applications.

---

## Example 9: Using BETWEEN for Date Reports

```sql
SELECT *
FROM Orders
WHERE OrderDate BETWEEN '2025-01-01' AND '2025-12-31';
```

### Explanation

- Retrieves orders placed during a specific year.
- Useful for generating reports and analytics.

---

## BETWEEN vs Comparison Operators

### Using BETWEEN

```sql
SELECT *
FROM Employees
WHERE Age BETWEEN 25 AND 35;
```

### Using Comparison Operators

```sql
SELECT *
FROM Employees
WHERE Age >= 25
AND Age <= 35;
```

### Comparison

| Feature | BETWEEN | Comparison Operators |
| --- | --- | --- |
| Readability | High | Moderate |
| Includes Boundaries | Yes | Yes |
| Requires Less Code | Yes | No |
| Supports Numbers | Yes | Yes |
| Supports Dates | Yes | Yes |
| Supports Text | Yes | Yes |

---

## Common Use Cases

### Find Employees Within an Age Range

```sql
SELECT *
FROM Employees
WHERE Age BETWEEN 25 AND 35;
```

### Find Orders Within a Date Range

```sql
SELECT *
FROM Orders
WHERE OrderDate BETWEEN '2025-01-01' AND '2025-12-31';
```

### Find Products Within a Price Range

```sql
SELECT *
FROM Products
WHERE Price BETWEEN 1000 AND 5000;
```

### Find Students Within a Score Range

```sql
SELECT *
FROM Students
WHERE Marks BETWEEN 70 AND 90;
```

---

## Best Practices

- Use BETWEEN for readable range-based filtering.
- Remember that BETWEEN is inclusive.
- Ensure the lower value appears before the higher value.
- Use date formats supported by your database.
- Combine BETWEEN with other conditions when needed.

---

## Important Points

- BETWEEN checks whether a value lies within a range.
- The operator includes both boundary values.
- Works with numbers, dates, and text.
- NOT BETWEEN excludes values within the range.
- BETWEEN improves query readability compared to multiple comparisons.
- Frequently used in reporting, filtering, and analytics queries.

---

## Conclusion

The SQL `BETWEEN` operator provides a simple and readable way to filter records within a specified range. Whether working with numeric values, dates, or text, BETWEEN helps simplify queries while improving readability. Its inclusive nature and versatility make it one of the most commonly used operators for range-based filtering in SQL.



###
