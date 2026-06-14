# SQL Correlated Subqueries

## Introduction

A Correlated Subquery is a subquery that depends on values from the outer query. Unlike a regular subquery, a correlated subquery cannot execute independently because it references columns from the outer query.

The subquery executes once for each row processed by the outer query, making it useful for row-by-row comparisons, filtering, and conditional operations.

### Why Use Correlated Subqueries?

- Compare rows within the same table.
- Perform row-specific calculations.
- Filter data based on group averages.
- Check the existence of related records.
- Perform conditional updates and deletions.

## Syntax

```sql
SELECT column1, column2
FROM table1 t1
WHERE column_name operator
(
    SELECT column_name
    FROM table2
    WHERE table2.column = t1.column
);
```

### Syntax Components

| Component | Description |
| --- | --- |
| Outer Query | Main query being executed |
| Correlated Subquery | Subquery that references the outer query |
| Operator | Comparison operator such as =, &gt;, &lt; |
| Alias | Temporary table name used for reference |

---

## Creating Sample Tables

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);
```

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    Salary DECIMAL(10,2),
    ManagerID INT
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Departments VALUES
(101, 'IT'),
(102, 'HR'),
(103, 'Finance'),
(104, 'Marketing');
```

```sql
INSERT INTO Employees VALUES
(1, 'Akash', 101, 50000, NULL),
(2, 'Rahul', 101, 65000, 1),
(3, 'Sai', 102, 45000, 1),
(4, 'Abhiram', 102, 70000, 2),
(5, 'Hemanth', 103, 55000, 2);
```

Display all employees:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID | Salary | ManagerID |
| --- | --- | --- | --- | --- |
| 1 | Akash | 101 | 50000 | NULL |
| 2 | Rahul | 101 | 65000 | 1 |
| 3 | Sai | 102 | 45000 | 1 |
| 4 | Abhiram | 102 | 70000 | 2 |
| 5 | Hemanth | 103 | 55000 | 2 |

## Example 1: Employees Earning Above Department Average

Retrieve employees whose salary is greater than the average salary of their department.

```sql
SELECT EmployeeName,
       Salary,
       DepartmentID
FROM Employees e
WHERE Salary >
(
    SELECT AVG(Salary)
    FROM Employees
    WHERE DepartmentID = e.DepartmentID
);
```

### Output

| EmployeeName | Salary | DepartmentID |
| --- | --- | --- |
| Rahul | 65000 | 101 |
| Abhiram | 70000 | 102 |

### Explanation

- The subquery calculates the average salary for each department.
- The outer query compares each employee's salary with that average.
- Employees earning above the department average are returned.

## Example 2: Correlated Subquery with UPDATE

Update salaries of employees in Department 101 to the department average salary.

```sql
UPDATE Employees
SET Salary =
(
    SELECT AVG(Salary)
    FROM Employees e2
    WHERE e2.DepartmentID = Employees.DepartmentID
)
WHERE DepartmentID = 101;
```

### Explanation

- The subquery calculates the average salary for Department 101.
- UPDATE modifies the matching employee records.
- Each row uses its department value dynamically.

## Example 3: Correlated Subquery with DELETE

Delete employees whose salary is below their department average.

```sql
DELETE FROM Employees e
WHERE Salary <
(
    SELECT AVG(Salary)
    FROM Employees
    WHERE DepartmentID = e.DepartmentID
);
```

### Explanation

- The subquery calculates the average salary for each department.
- Employees earning less than the average are removed.

## Example 4: Using EXISTS with Correlated Subqueries

Find employees who manage at least one other employee.

```sql
SELECT e.EmployeeID,
       e.EmployeeName
FROM Employees e
WHERE EXISTS
(
    SELECT 1
    FROM Employees sub
    WHERE sub.ManagerID = e.EmployeeID
);
```

### Output

| EmployeeID | EmployeeName |
| --- | --- |
| 1 | Akash |
| 2 | Rahul |

### Explanation

- EXISTS checks whether the subquery returns any rows.
- Employees who have subordinates are returned.

## Example 5: Using NOT EXISTS with Correlated Subqueries

Find departments that do not have any employees.

```sql
SELECT d.DepartmentID,
       d.DepartmentName
FROM Departments d
WHERE NOT EXISTS
(
    SELECT 1
    FROM Employees e
    WHERE e.DepartmentID = d.DepartmentID
);
```

### Output

| DepartmentID | DepartmentName |
| --- | --- |
| 104 | Marketing |

### Explanation

- NOT EXISTS returns rows where the subquery finds no matching records.
- Departments without employees are displayed.

---

## Correlated Subquery vs Normal Subquery

| Normal Subquery | Correlated Subquery |
| --- | --- |
| Executes once | Executes for every outer row |
| Independent of outer query | Depends on outer query |
| Faster for large datasets | Can be slower |
| Can execute separately | Cannot execute independently |
| Simpler execution | Dynamic execution |

---

## Performance Considerations

- Correlated subqueries execute repeatedly for each row.
- Large datasets may experience slower performance.
- Indexing can improve execution speed.
- JOIN operations may sometimes provide better performance.
- Use correlated subqueries only when row-level processing is required.

---

## Best Practices

- Use meaningful table aliases.
- Keep correlated subqueries simple.
- Create indexes on frequently filtered columns.
- Consider JOINs for better optimization.
- Test query performance before deployment.

---

## Important Points

- Correlated subqueries depend on the outer query.
- They execute once for every row of the outer query.
- Commonly used with EXISTS and NOT EXISTS.
- Useful for row-level comparisons and calculations.
- Cannot run independently without the outer query.

---

## Conclusion

SQL Correlated Subqueries are powerful tools for performing row-specific comparisons and advanced filtering. Since they reference the outer query, they provide dynamic results that regular subqueries cannot. Although they may be slower on large datasets, they are highly effective for solving complex business and reporting requirements.



###
