# SQL Correlated Subqueries

## Introduction

A Correlated Subquery is a subquery that depends on values from the outer query. Unlike a normal subquery, it cannot execute independently because it references columns from the outer query.

The subquery runs once for every row processed by the outer query, making it useful for row-by-row comparisons and advanced filtering.

### Key Features

- Depends on values from the outer query.
- Executes once for each row of the outer query.
- Useful for row-specific calculations.
- Commonly used with EXISTS and NOT EXISTS.
- Helps solve complex filtering conditions.

---

## Why Use Correlated Subqueries?

Correlated subqueries are useful when:

- Comparing a row against other rows in the same table.
- Finding records above or below group averages.
- Checking the existence of related records.
- Performing conditional updates and deletions.
- Working with hierarchical or grouped data.

---

## Syntax

```sql id="corr1"
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
| Correlated Subquery | Query that references the outer query |
| t1 | Alias for the outer table |
| Operator | Comparison operator such as &gt;, &lt;, = |

---

## Creating Sample Table

```sql id="corr2"
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    Salary DECIMAL(10,2)
);
```

---

## Inserting Sample Records

```sql id="corr3"
INSERT INTO Employees VALUES
(1,'Akash',101,50000),
(2,'Rahul',101,60000),
(3,'Sai',102,45000),
(4,'Hemanth',102,70000),
(5,'Abhiram',103,55000);
```

Display the table:

```sql id="corr4"
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | DepartmentID | Salary |
| --- | --- | --- | --- |
| 1 | Akash | 101 | 50000 |
| 2 | Rahul | 101 | 60000 |
| 3 | Sai | 102 | 45000 |
| 4 | Hemanth | 102 | 70000 |
| 5 | Abhiram | 103 | 55000 |

---

# Example 1: Employees Earning Above Department Average

Find employees whose salary is greater than the average salary of their department.

```sql id="corr5"
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
| Rahul | 60000 | 101 |
| Hemanth | 70000 | 102 |

### Explanation

- The subquery calculates the average salary for the current employee's department.
- The outer query compares the employee's salary with that average.
- Only employees earning above their department average are returned.

---

# Example 2: Correlated Subquery with UPDATE

Update salaries of employees in Department 101 to their department average salary.

```sql id="corr6"
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

- The subquery calculates the department average.
- UPDATE assigns that value to matching employees.
- Each row uses its department information dynamically.

---

# Example 3: Correlated Subquery with DELETE

Delete employees whose salary is below their department average.

```sql id="corr7"
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
- Employees earning below the average are deleted.

---

# Example 4: Using EXISTS

Find employees who manage at least one other employee.

Create another table:

```sql id="corr8"
CREATE TABLE Staff (
    EmployeeID INT,
    EmployeeName VARCHAR(50),
    ManagerID INT
);
```

```sql id="corr9"
INSERT INTO Staff VALUES
(1,'John',NULL),
(2,'David',1),
(3,'Emma',1),
(4,'Sophia',2);
```

Query:

```sql id="corr10"
SELECT s1.EmployeeID,
       s1.EmployeeName
FROM Staff s1
WHERE EXISTS
(
    SELECT 1
    FROM Staff s2
    WHERE s2.ManagerID = s1.EmployeeID
);
```

### Output

| EmployeeID | EmployeeName |
| --- | --- |
| 1 | John |
| 2 | David |

### Explanation

- EXISTS checks whether the subquery returns any rows.
- Employees who manage others are returned.

---

# Example 5: Using NOT EXISTS

Find managers who have no employees reporting to them.

```sql id="corr11"
SELECT s1.EmployeeID,
       s1.EmployeeName
FROM Staff s1
WHERE NOT EXISTS
(
    SELECT 1
    FROM Staff s2
    WHERE s2.ManagerID = s1.EmployeeID
);
```

### Output

| EmployeeID | EmployeeName |
| --- | --- |
| 3 | Emma |
| 4 | Sophia |

### Explanation

- NOT EXISTS returns rows where the subquery finds no matching records.
- Employees without subordinates are displayed.

---

## Correlated vs Non-Correlated Subquery

| Non-Correlated Subquery | Correlated Subquery |
| --- | --- |
| Executes once | Executes for every outer row |
| Independent of outer query | Depends on outer query |
| Faster for large datasets | Can be slower |
| Can run separately | Cannot run independently |
| Simpler execution | Dynamic execution |

---

## Performance Considerations

- Correlated subqueries execute multiple times.
- Performance may decrease on large datasets.
- Proper indexing improves execution speed.
- JOINs are often faster alternatives.
- Use correlated subqueries only when necessary.

---

## Best Practices

- Use meaningful table aliases.
- Keep subqueries simple and readable.
- Create indexes on frequently compared columns.
- Consider JOINs for better performance.
- Test correlated queries on large datasets before deployment.

---

## Important Points

- Correlated subqueries reference the outer query.
- They execute once for every row of the outer query.
- Commonly used with EXISTS and NOT EXISTS.
- Useful for row-level comparisons.
- Cannot execute independently.

---

## Conclusion

SQL Correlated Subqueries are powerful tools for solving row-specific problems and advanced filtering requirements. Since they depend on the outer query, they provide dynamic results that standard subqueries cannot. Although they may be slower on large datasets, they are extremely useful when comparing rows within groups, checking existence conditions, and performing conditional updates or deletions.



###
