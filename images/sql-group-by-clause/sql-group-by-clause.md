# SQL GROUP BY Clause

## Introduction

The SQL `GROUP BY` clause is used to organize rows that contain the same values into groups. It is commonly used with aggregate functions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()` to perform calculations on each group of data.

Instead of calculating results for an entire table, `GROUP BY` allows calculations to be performed separately for each category or group.

## Why Use GROUP BY?

The `GROUP BY` clause helps you:

- Summarize large datasets.
- Calculate totals for different categories.
- Generate reports and analytics.
- Count records within groups.
- Find averages, minimums, and maximums for specific categories.

## Syntax

```sql
SELECT column_name,
       aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| SELECT | Retrieves data from a table |
| aggregate_function | Performs calculations such as SUM(), COUNT(), AVG() |
| WHERE | Filters rows before grouping |
| GROUP BY | Creates groups based on column values |

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

Display the records:

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

## How GROUP BY Works

The GROUP BY clause collects rows with identical values in the specified column and treats them as a single group.

For each group, aggregate functions perform calculations independently.

### Example

```sql
SELECT Department
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department |
| --- |
| Management |
| Content |
| Technical |
| Database |

## Example 1: Counting Records in Each Group

Find the number of members in each department.

```sql
SELECT Department,
       COUNT(*) AS MemberCount
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | MemberCount |
| --- | --- |
| Management | 1 |
| Content | 2 |
| Technical | 2 |
| Database | 1 |

### Explanation

- Records are grouped by department.
- COUNT() counts members in each group.
- Each department receives its own count.

## Example 2: Calculating Total Salary

Find the total salary paid by each department.

```sql
SELECT Department,
       SUM(Salary) AS TotalSalary
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | TotalSalary |
| --- | --- |
| Management | 80000 |
| Content | 95000 |
| Technical | 135000 |
| Database | 55000 |

### Explanation

- GROUP BY creates department groups.
- SUM() calculates total salary for each group.

## Example 3: Calculating Average Salary

Find the average salary in each department.

```sql
SELECT Department,
       AVG(Salary) AS AverageSalary
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | AverageSalary |
| --- | --- |
| Management | 80000 |
| Content | 47500 |
| Technical | 67500 |
| Database | 55000 |

## Example 4: Finding Highest Salary

Display the highest salary in each department.

```sql
SELECT Department,
       MAX(Salary) AS HighestSalary
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | HighestSalary |
| --- | --- |
| Management | 80000 |
| Content | 50000 |
| Technical | 70000 |
| Database | 55000 |

## Example 5: Finding Lowest Salary

Display the lowest salary in each department.

```sql
SELECT Department,
       MIN(Salary) AS LowestSalary
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | LowestSalary |
| --- | --- |
| Management | 80000 |
| Content | 45000 |
| Technical | 65000 |
| Database | 55000 |

## Example 6: GROUP BY Multiple Columns

The GROUP BY clause can group data using more than one column.

### Example

```sql
SELECT Department,
       ExperienceYears,
       COUNT(*) AS MemberCount
FROM TeamMembers
GROUP BY Department,
         ExperienceYears;
```

### Output

| Department | ExperienceYears | MemberCount |
| --- | --- | --- |
| Management | 5 | 1 |
| Content | 3 | 1 |
| Content | 4 | 1 |
| Technical | 4 | 1 |
| Technical | 5 | 1 |
| Database | 2 | 1 |

### Explanation

Rows are grouped using both Department and ExperienceYears.

## Using WHERE with GROUP BY

The WHERE clause filters rows before grouping.

### Example

Display departments where salary is greater than 50000 before grouping.

```sql
SELECT Department,
       COUNT(*) AS MemberCount
FROM TeamMembers
WHERE Salary > 50000
GROUP BY Department;
```

### Explanation

- WHERE removes unwanted rows first.
- Remaining rows are grouped afterward.

## Using HAVING with GROUP BY

The HAVING clause filters groups after grouping has been completed.

### Example

Display departments having more than one member.

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

- GROUP BY creates department groups.
- HAVING filters only groups that satisfy the condition.

## GROUP BY with Multiple Aggregate Functions

You can calculate multiple values simultaneously.

### Example

```sql
SELECT Department,
       COUNT(*) AS TotalMembers,
       SUM(Salary) AS TotalSalary,
       AVG(Salary) AS AverageSalary,
       MAX(Salary) AS HighestSalary,
       MIN(Salary) AS LowestSalary
FROM TeamMembers
GROUP BY Department;
```

### Output

A summarized report for every department containing:

- Total members
- Total salary
- Average salary
- Highest salary
- Lowest salary

## Common Aggregate Functions Used with GROUP BY

| Function | Description |
| --- | --- |
| COUNT() | Counts records |
| SUM() | Calculates total value |
| AVG() | Calculates average value |
| MAX() | Finds highest value |
| MIN() | Finds lowest value |

## Common Use Cases

| Scenario | Usage |
| --- | --- |
| Employee Reports | Count employees per department |
| Sales Analysis | Calculate sales per product category |
| Student Reports | Count students per course |
| Financial Reports | Calculate department expenses |
| Analytics Dashboards | Summarize business metrics |

## Best Practices

- Always use aggregate functions with grouped data.
- Use meaningful aliases for calculated columns.
- Apply WHERE before grouping when possible.
- Use HAVING only for filtering grouped results.
- Group only by columns that are necessary.

## Important Points

- GROUP BY combines rows with identical values.
- Aggregate functions perform calculations on each group.
- WHERE filters rows before grouping.
- HAVING filters groups after grouping.
- Multiple columns can be used in GROUP BY.
- GROUP BY is widely used in reporting and analytics.

## Conclusion

The SQL `GROUP BY` clause is one of the most powerful tools for data analysis and reporting. By organizing records into groups and applying aggregate functions, it enables meaningful summaries and insights from large datasets. When combined with aggregate functions, WHERE, and HAVING clauses, GROUP BY becomes an essential feature for building efficient and informative SQL queries.



###
