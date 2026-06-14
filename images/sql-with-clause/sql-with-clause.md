# SQL WITH Clause

## Introduction

The SQL `WITH` clause, also known as a **Common Table Expression (CTE)**, is used to create a temporary named result set that exists only during the execution of a query. It helps simplify complex SQL statements by breaking them into smaller, more readable sections.

A CTE can be referenced multiple times within the same query, making SQL code easier to understand and maintain.

## Why Use the WITH Clause?

The `WITH` clause helps you:

- Simplify complex queries.
- Improve query readability.
- Avoid repeating the same subquery multiple times.
- Organize multi-step calculations.
- Create recursive queries.
- Improve query maintenance.

## Basic Syntax

```sql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT *
FROM cte_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| WITH | Starts the Common Table Expression |
| cte_name | Name assigned to the temporary result set |
| AS | Associates the CTE name with the query |
| SELECT Statement | Generates the temporary result set |
| Main Query | Uses the CTE as a virtual table |

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 80000),
(2, 'Mohit Chandaluri', 'Content', 45000),
(3, 'Abhiram Gopisetti', 'Technical', 70000),
(4, 'Adapa Hemesh', 'Database', 55000),
(5, 'Kiran Kumar', 'Technical', 65000);
```

View the data:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | Salary |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 80000 |
| 2 | Mohit Chandaluri | Content | 45000 |
| 3 | Abhiram Gopisetti | Technical | 70000 |
| 4 | Adapa Hemesh | Database | 55000 |
| 5 | Kiran Kumar | Technical | 65000 |

## Example 1: Finding Employees with Above-Average Salary

The following query calculates the average salary using a CTE and then retrieves members whose salary is greater than the average.

```sql
WITH AverageSalary AS (
    SELECT AVG(Salary) AS AvgSalary
    FROM TeamMembers
)
SELECT MemberID,
       MemberName,
       Salary
FROM TeamMembers
WHERE Salary >
(
    SELECT AvgSalary
    FROM AverageSalary
);
```

### Output

| MemberID | MemberName | Salary |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | 80000 |
| 3 | Abhiram Gopisetti | 70000 |
| 5 | Kiran Kumar | 65000 |

### Explanation

- The CTE calculates the average salary.
- The main query compares each salary against that value.
- Only members earning above the average salary are returned.

## Example 2: Finding Members with the Lowest Salary

This example identifies the member with the minimum salary.

```sql
WITH MinimumSalary AS (
    SELECT MIN(Salary) AS LowestSalary
    FROM TeamMembers
)
SELECT MemberID,
       MemberName,
       Salary
FROM TeamMembers
WHERE Salary =
(
    SELECT LowestSalary
    FROM MinimumSalary
);
```

### Output

| MemberID | MemberName | Salary |
| --- | --- | --- |
| 2 | Mohit Chandaluri | 45000 |

### Explanation

- The CTE calculates the minimum salary.
- The main query retrieves members whose salary matches that value.

## Example 3: Department Salary Summary

A CTE can be used to calculate departmental statistics.

```sql
WITH DepartmentSummary AS (
    SELECT Department,
           AVG(Salary) AS AverageSalary
    FROM TeamMembers
    GROUP BY Department
)
SELECT *
FROM DepartmentSummary;
```

### Output

| Department | AverageSalary |
| --- | --- |
| Management | 80000 |
| Content | 45000 |
| Technical | 67500 |
| Database | 55000 |

## Example 4: Using Multiple CTEs

Multiple CTEs can be defined within a single query.

```sql
WITH DepartmentAverage AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM TeamMembers
    GROUP BY Department
),
HighSalaryMembers AS (
    SELECT *
    FROM TeamMembers
    WHERE Salary > 60000
)
SELECT h.MemberName,
       h.Department,
       d.AvgSalary
FROM HighSalaryMembers h
JOIN DepartmentAverage d
ON h.Department = d.Department;
```

### Benefits

- Separates logic into manageable sections.
- Improves readability.
- Makes complex queries easier to maintain.

## Example 5: Ranking Members by Salary

CTEs work well with window functions.

```sql
WITH RankedMembers AS (
    SELECT MemberID,
           MemberName,
           Department,
           Salary,
           RANK() OVER (
               ORDER BY Salary DESC
           ) AS SalaryRank
    FROM TeamMembers
)
SELECT *
FROM RankedMembers;
```

### Output

| MemberName | Salary | SalaryRank |
| --- | --- | --- |
| Akash Dangudubiyyapu | 80000 | 1 |
| Abhiram Gopisetti | 70000 | 2 |
| Kiran Kumar | 65000 | 3 |
| Adapa Hemesh | 55000 | 4 |
| Mohit Chandaluri | 45000 | 5 |

## Chained CTE Example

One CTE can use another CTE.

```sql
WITH DepartmentAverage AS (
    SELECT Department,
           AVG(Salary) AS AvgSalary
    FROM TeamMembers
    GROUP BY Department
),
AboveDepartmentAverage AS (
    SELECT t.*
    FROM TeamMembers t
    JOIN DepartmentAverage d
    ON t.Department = d.Department
    WHERE t.Salary > d.AvgSalary
)
SELECT *
FROM AboveDepartmentAverage;
```

### Explanation

- First CTE calculates departmental averages.
- Second CTE uses those averages.
- Final query returns members earning above their department average.

## Recursive CTE Example

Recursive CTEs are useful for hierarchical data.

```sql
WITH NumberSeries AS (
    SELECT 1 AS NumberValue

    UNION ALL

    SELECT NumberValue + 1
    FROM NumberSeries
    WHERE NumberValue < 5
)
SELECT *
FROM NumberSeries;
```

### Output

| NumberValue |
| --- |
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |

## WITH Clause vs Subquery

| Feature | WITH Clause (CTE) | Subquery |
| --- | --- | --- |
| Readability | High | Lower for complex queries |
| Reusability | Yes | Usually No |
| Maintenance | Easier | Harder |
| Complex Logic | Better | Less Suitable |
| Recursive Support | Yes | No |

## Advantages of the WITH Clause

- Improves query readability.
- Reduces repeated code.
- Simplifies complex SQL operations.
- Supports recursive queries.
- Makes debugging easier.

## Best Practices

- Use meaningful CTE names.
- Keep CTEs focused on a single task.
- Use multiple CTEs to simplify complex logic.
- Avoid excessive nesting.
- Consider performance when working with very large datasets.

## Important Points

- A CTE exists only during query execution.
- It is not stored permanently in the database.
- Multiple CTEs can be defined in a single query.
- CTEs can reference previous CTEs.
- Recursive CTEs support hierarchical and tree-structured data.
- CTEs improve readability and maintainability.

## Conclusion

The SQL `WITH` clause provides a powerful way to create temporary result sets that simplify complex queries. By organizing logic into reusable and readable sections, Common Table Expressions improve code quality, maintainability, and understanding. Whether calculating aggregates, ranking records, chaining multiple operations, or working with recursive structures, the `WITH` clause is an essential SQL feature for modern database development.



###
