# SQL LIMIT Clause

## Introduction

The SQL `LIMIT` clause is used to restrict the number of rows returned by a query. Instead of displaying all records from a table, LIMIT allows you to retrieve only a specific number of rows.

This feature is particularly useful when working with large datasets, generating reports, implementing pagination, or displaying top-performing records.

The LIMIT clause is commonly supported in MySQL, PostgreSQL, SQLite, and several other database systems.

## Why Use LIMIT?

The `LIMIT` clause helps you:

- Retrieve only a specific number of records.
- Improve query performance on large tables.
- Implement pagination in applications.
- Display top or bottom records.
- Reduce unnecessary data transfer.

## Syntax

### Basic Syntax

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT row_count;
```

### Syntax with OFFSET

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT row_count OFFSET offset_value;
```

### Alternative MySQL Syntax

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT offset_value, row_count;
```

### Syntax Components

| Component | Description |
| --- | --- |
| row_count | Number of rows to return |
| offset_value | Number of rows to skip before retrieving data |

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
(5, 'Kiran Kumar', 'Technical', 85000, 6),
(6, 'Sai Kumar', 'Content', 50000, 4),
(7, 'Ravi Teja', 'Support', 40000, 2),
(8, 'Nikhil Reddy', 'Technical', 75000, 5);
```

Display all records:

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
| 5 | Kiran Kumar | Technical | 85000 | 6 |
| 6 | Sai Kumar | Content | 50000 | 4 |
| 7 | Ravi Teja | Support | 40000 | 2 |
| 8 | Nikhil Reddy | Technical | 75000 | 5 |

## Example 1: Retrieve the First Few Records

Display only the first three rows.

```sql
SELECT *
FROM TeamMembers
LIMIT 3;
```

### Output

| MemberID | MemberName | Department |
| --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management |
| 2 | Mohit Chandaluri | Content |
| 3 | Abhiram Gopisetti | Technical |

### Explanation

- LIMIT restricts the output to three rows.
- Only the first three records are returned.

## Example 2: Using LIMIT with ORDER BY

Display the top three highest-paid team members.

```sql
SELECT MemberName,
       Salary
FROM TeamMembers
ORDER BY Salary DESC
LIMIT 3;
```

### Output

| MemberName | Salary |
| --- | --- |
| Kiran Kumar | 85000 |
| Akash Dangudubiyyapu | 80000 |
| Nikhil Reddy | 75000 |

### Explanation

- ORDER BY sorts salaries from highest to lowest.
- LIMIT returns only the first three records.

## Example 3: Using LIMIT with OFFSET

Skip the first two records and retrieve the next three records.

```sql
SELECT *
FROM TeamMembers
LIMIT 3 OFFSET 2;
```

### Output

| MemberID | MemberName |
| --- | --- |
| 3 | Abhiram Gopisetti |
| 4 | Adapa Hemesh |
| 5 | Kiran Kumar |

### Explanation

- OFFSET skips the first two rows.
- LIMIT retrieves the next three rows.

## Example 4: MySQL OFFSET Syntax

The same query can be written in MySQL as:

```sql
SELECT *
FROM TeamMembers
LIMIT 2, 3;
```

### Explanation

- 2 indicates rows to skip.
- 3 indicates rows to retrieve.

## Example 5: Finding the Highest Salary

Retrieve the employee with the highest salary.

```sql
SELECT MemberName,
       Salary
FROM TeamMembers
ORDER BY Salary DESC
LIMIT 1;
```

### Output

| MemberName | Salary |
| --- | --- |
| Kiran Kumar | 85000 |

## Example 6: Finding the Lowest Salary

Retrieve the employee with the lowest salary.

```sql
SELECT MemberName,
       Salary
FROM TeamMembers
ORDER BY Salary ASC
LIMIT 1;
```

### Output

| MemberName | Salary |
| --- | --- |
| Ravi Teja | 40000 |

## Example 7: Finding the Third Highest Salary

Retrieve the third highest salary.

```sql
SELECT MemberName,
       Salary
FROM TeamMembers
ORDER BY Salary DESC
LIMIT 1 OFFSET 2;
```

### Output

| MemberName | Salary |
| --- | --- |
| Nikhil Reddy | 75000 |

### Explanation

- ORDER BY sorts salaries from highest to lowest.
- OFFSET skips the first two records.
- LIMIT retrieves the next record.

## Example 8: Using LIMIT with WHERE

Display two technical team members.

```sql
SELECT MemberName,
       Department
FROM TeamMembers
WHERE Department = 'Technical'
LIMIT 2;
```

### Output

| MemberName | Department |
| --- | --- |
| Abhiram Gopisetti | Technical |
| Kiran Kumar | Technical |

### Explanation

- WHERE filters rows first.
- LIMIT restricts the final result.

## Using LIMIT for Pagination

Pagination is commonly used in web applications.

### Page 1

```sql
SELECT *
FROM TeamMembers
LIMIT 5 OFFSET 0;
```

### Page 2

```sql
SELECT *
FROM TeamMembers
LIMIT 5 OFFSET 5;
```

### Explanation

- Page 1 shows records 1–5.
- Page 2 shows records 6–10.
- Useful when displaying large datasets.

## LIMIT vs TOP vs FETCH

Different database systems use different keywords.

| Database | Clause |
| --- | --- |
| MySQL | LIMIT |
| PostgreSQL | LIMIT |
| SQLite | LIMIT |
| SQL Server | TOP / OFFSET FETCH |
| Oracle | FETCH FIRST |

### SQL Server Example

```sql
SELECT TOP 5 *
FROM TeamMembers;
```

### Oracle Example

```sql
SELECT *
FROM TeamMembers
FETCH FIRST 5 ROWS ONLY;
```

## Common Use Cases

| Scenario | Usage |
| --- | --- |
| Pagination | Display data page by page |
| Dashboards | Show top records |
| Reports | Limit report size |
| Analytics | Retrieve top-performing entries |
| Testing | View sample records |

## Best Practices

- Use ORDER BY with LIMIT for predictable results.
- Apply WHERE before LIMIT whenever possible.
- Use OFFSET carefully on very large datasets.
- Avoid retrieving more records than required.
- Use pagination for large result sets.

## Important Points

- LIMIT restricts the number of returned rows.
- OFFSET skips a specified number of rows.
- ORDER BY should be used when result order matters.
- LIMIT improves performance by reducing result size.
- Syntax may vary across database systems.

## Conclusion

The SQL `LIMIT` clause is a simple yet powerful feature that helps control the size of query results. It is widely used for pagination, reporting, analytics, and retrieving top or bottom records. When combined with ORDER BY, WHERE, and OFFSET, LIMIT provides precise control over the data returned from a database query.



###
