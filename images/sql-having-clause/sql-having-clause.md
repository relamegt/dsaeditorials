# SQL HAVING Clause

## Introduction

The SQL `HAVING` clause is used to filter grouped data after the `GROUP BY` operation has been performed. Unlike the `WHERE` clause, which filters individual rows before grouping, the `HAVING` clause filters groups based on aggregate values such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.

The `HAVING` clause is commonly used in reports, analytics, and data summaries where filtering is required on aggregated results.

## Why Use the HAVING Clause?

The `HAVING` clause helps you:

- Filter grouped records.
- Apply conditions to aggregate functions.
- Analyze summarized data.
- Generate meaningful reports.
- Retrieve only groups that satisfy specific criteria.

## HAVING vs WHERE

| Feature | WHERE | HAVING |
| --- | --- | --- |
| Filters | Individual Rows | Groups |
| Executes | Before GROUP BY | After GROUP BY |
| Works with Aggregate Functions | No | Yes |
| Common Usage | Row Filtering | Group Filtering |

## Basic Syntax

```sql
SELECT column_name,
       AGGREGATE_FUNCTION(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| SELECT | Columns to display |
| AGGREGATE_FUNCTION | Functions such as COUNT(), SUM(), AVG() |
| GROUP BY | Creates groups of rows |
| HAVING | Filters groups based on aggregate values |

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    ExperienceYears INT
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 80000, 5),
(2, 'Mohit Chandaluri', 'Content', 45000, 3),
(3, 'Abhiram Gopisetti', 'Technical', 70000, 4),
(4, 'Adapa Hemesh', 'Database', 55000, 2),
(5, 'Kiran Kumar', 'Technical', 65000, 5),
(6, 'Sai Kumar', 'Content', 50000, 4);
```

Display the data:

```sql
SELECT * FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | Salary | ExperienceYears |
| --- | --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 80000 | 5 |
| 2 | Mohit Chandaluri | Content | 45000 | 3 |
| 3 | Abhiram Gopisetti | Technical | 70000 | 4 |
| 4 | Adapa Hemesh | Database | 55000 | 2 |
| 5 | Kiran Kumar | Technical | 65000 | 5 |
| 6 | Sai Kumar | Content | 50000 | 4 |

## Example 1: Filtering Groups Using COUNT()

Find departments having more than one member.

```sql
SELECT Department,
       COUNT(*) AS MemberCount
FROM TeamMembers
GROUP BY Department
HAVING COUNT(*) > 1;
```

### Output

| Department | MemberCount |
| --- | --- |
| Content | 2 |
| Technical | 2 |

### Explanation

- Records are grouped by department.
- COUNT() calculates the number of members in each department.
- HAVING filters only departments with more than one member.

## Example 2: Filtering Total Salary

Display departments whose total salary exceeds 100000.

```sql
SELECT Department,
       SUM(Salary) AS TotalSalary
FROM TeamMembers
GROUP BY Department
HAVING SUM(Salary) > 100000;
```

### Output

| Department | TotalSalary |
| --- | --- |
| Technical | 135000 |
| Content | 95000 |

Depending on the condition, only qualifying departments are displayed.

## Example 3: Filtering Average Salary

Retrieve departments where the average salary is greater than 60000.

```sql
SELECT Department,
       AVG(Salary) AS AverageSalary
FROM TeamMembers
GROUP BY Department
HAVING AVG(Salary) > 60000;
```

### Output

| Department | AverageSalary |
| --- | --- |
| Management | 80000 |
| Technical | 67500 |

### Explanation

- AVG() calculates average salary per department.
- HAVING filters departments based on the calculated average.

## Example 4: Filtering Maximum Salary

Display departments whose highest salary exceeds 70000.

```sql
SELECT Department,
       MAX(Salary) AS HighestSalary
FROM TeamMembers
GROUP BY Department
HAVING MAX(Salary) > 70000;
```

### Output

| Department | HighestSalary |
| --- | --- |
| Management | 80000 |

## Example 5: Filtering Minimum Experience

Display departments where the minimum experience is less than 3 years.

```sql
SELECT Department,
       MIN(ExperienceYears) AS MinimumExperience
FROM TeamMembers
GROUP BY Department
HAVING MIN(ExperienceYears) < 3;
```

### Output

| Department | MinimumExperience |
| --- | --- |
| Database | 2 |

## Example 6: Multiple HAVING Conditions

Retrieve departments where:

- Total salary is greater than 100000.
- Average salary is greater than 60000.

```sql
SELECT Department,
       SUM(Salary) AS TotalSalary,
       AVG(Salary) AS AverageSalary
FROM TeamMembers
GROUP BY Department
HAVING SUM(Salary) > 100000
AND AVG(Salary) > 60000;
```

### Output

| Department | TotalSalary | AverageSalary |
| --- | --- | --- |
| Technical | 135000 | 67500 |

## HAVING Without GROUP BY

When `GROUP BY` is omitted, the entire table is treated as a single group.

### Example

Display the total salary only if it exceeds 300000.

```sql
SELECT SUM(Salary) AS TotalSalary
FROM TeamMembers
HAVING SUM(Salary) > 300000;
```

### Output

| TotalSalary |
| --- |
| 365000 |

## HAVING with COUNT()

Find departments containing at least two members.

```sql
SELECT Department,
       COUNT(*) AS MemberCount
FROM TeamMembers
GROUP BY Department
HAVING COUNT(*) >= 2;
```

### Output

| Department | MemberCount |
| --- | --- |
| Content | 2 |
| Technical | 2 |

## Combining WHERE and HAVING

`WHERE` filters rows first, while `HAVING` filters groups afterward.

### Example

Find departments where the average salary of members earning more than 50000 exceeds 65000.

```sql
SELECT Department,
       AVG(Salary) AS AverageSalary
FROM TeamMembers
WHERE Salary > 50000
GROUP BY Department
HAVING AVG(Salary) > 65000;
```

### Execution Order

1. WHERE filters rows.
2. GROUP BY creates groups.
3. Aggregate functions are calculated.
4. HAVING filters the grouped results.

## Common Aggregate Functions Used with HAVING

| Function | Description |
| --- | --- |
| COUNT() | Counts records |
| SUM() | Calculates total |
| AVG() | Calculates average |
| MIN() | Finds smallest value |
| MAX() | Finds largest value |

## Common Use Cases

| Scenario | Usage |
| --- | --- |
| Department Reports | Filter departments by employee count |
| Sales Analysis | Filter products by total sales |
| Performance Reports | Filter teams by average performance |
| Financial Analysis | Filter groups by revenue totals |

## Best Practices

- Use `WHERE` for row-level filtering.
- Use `HAVING` for aggregate filtering.
- Avoid using HAVING when WHERE can perform the same task.
- Combine WHERE and HAVING for better performance.
- Use meaningful aliases for aggregate columns.

## Important Points

- HAVING filters grouped data.
- It is commonly used with aggregate functions.
- It executes after GROUP BY.
- It can be used without GROUP BY when treating the entire table as one group.
- Multiple conditions can be combined using AND and OR.
- WHERE and HAVING serve different purposes.

## Conclusion

The SQL `HAVING` clause is an essential tool for filtering aggregated data after grouping operations. By working alongside `GROUP BY` and aggregate functions such as `COUNT()`, `SUM()`, and `AVG()`, it enables powerful reporting, analysis, and data summarization capabilities. Understanding the difference between `WHERE` and `HAVING` is crucial for writing efficient and accurate SQL queries.



###
