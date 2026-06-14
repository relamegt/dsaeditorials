# SQL SELECT Statement

## Introduction

The SQL `SELECT` statement is one of the most frequently used commands in SQL. It is used to retrieve data from one or more tables and display the results in a structured format.

Whether you need to view specific columns, filter records, sort data, perform calculations, or summarize information, the `SELECT` statement serves as the foundation for data retrieval in SQL.

## Why Use SELECT?

The `SELECT` statement helps you:

- Retrieve specific information from a table.
- Display all records or selected columns.
- Filter records using conditions.
- Sort data in ascending or descending order.
- Group and summarize data.
- Work with multiple tables using joins.

## Basic Syntax

```sql
SELECT column_name
FROM table_name;
```

### Selecting Multiple Columns

```sql
SELECT column1, column2, column3
FROM table_name;
```

### Selecting All Columns

```sql
SELECT *
FROM table_name;
```

## Creating a Sample Table

```sql
CREATE TABLE TeamMembers (
    MemberID INT PRIMARY KEY,
    MemberName VARCHAR(100),
    Department VARCHAR(50),
    ExperienceYears INT
);
```

## Inserting Sample Data

```sql
INSERT INTO TeamMembers
VALUES
(1, 'Akash Dangudubiyyapu', 'Management', 5),
(2, 'Mohit Chandaluri', 'Content', 3),
(3, 'Abhiram Gopisetti', 'Technical', 4),
(4, 'Adapa Hemesh', 'Database', 2),
(5, 'Kiran Kumar', 'Technical', 4);
```

## Selecting Specific Columns

To retrieve only selected columns:

```sql
SELECT MemberName, Department
FROM TeamMembers;
```

### Output

| MemberName | Department |
| --- | --- |
| Akash Dangudubiyyapu | Management |
| Mohit Chandaluri | Content |
| Abhiram Gopisetti | Technical |
| Adapa Hemesh | Database |
| Kiran Kumar | Technical |

## Selecting All Columns

To retrieve every column from a table:

```sql
SELECT *
FROM TeamMembers;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |
| 2 | Mohit Chandaluri | Content | 3 |
| 3 | Abhiram Gopisetti | Technical | 4 |
| 4 | Adapa Hemesh | Database | 2 |
| 5 | Kiran Kumar | Technical | 4 |

## Using SELECT with WHERE

The `WHERE` clause is used to filter records based on specified conditions.

### Example

Retrieve all members from the Technical department.

```sql
SELECT MemberName
FROM TeamMembers
WHERE Department = 'Technical';
```

### Output

| MemberName |
| --- |
| Abhiram Gopisetti |
| Kiran Kumar |

## Using SELECT with DISTINCT

The `DISTINCT` keyword removes duplicate values from the result set.

### Example

Retrieve unique departments.

```sql
SELECT DISTINCT Department
FROM TeamMembers;
```

### Output

| Department |
| --- |
| Management |
| Content |
| Technical |
| Database |

## Using SELECT with ORDER BY

The `ORDER BY` clause sorts the result set.

### Ascending Order

```sql
SELECT *
FROM TeamMembers
ORDER BY ExperienceYears ASC;
```

### Descending Order

```sql
SELECT *
FROM TeamMembers
ORDER BY ExperienceYears DESC;
```

## Using SELECT with GROUP BY

The `GROUP BY` clause groups records that have the same values.

### Example

Count the number of members in each department.

```sql
SELECT Department, COUNT(*) AS TotalMembers
FROM TeamMembers
GROUP BY Department;
```

### Output

| Department | TotalMembers |
| --- | --- |
| Management | 1 |
| Content | 1 |
| Technical | 2 |
| Database | 1 |

## Using SELECT with HAVING

The `HAVING` clause filters grouped results.

### Example

Display departments having more than one member.

```sql
SELECT Department, COUNT(*) AS TotalMembers
FROM TeamMembers
GROUP BY Department
HAVING COUNT(*) > 1;
```

### Output

| Department | TotalMembers |
| --- | --- |
| Technical | 2 |

## Using SELECT with LIMIT

The `LIMIT` clause restricts the number of rows returned.

### Example

Display only the first three records.

```sql
SELECT *
FROM TeamMembers
LIMIT 3;
```

### Output

| MemberID | MemberName | Department | ExperienceYears |
| --- | --- | --- | --- |
| 1 | Akash Dangudubiyyapu | Management | 5 |
| 2 | Mohit Chandaluri | Content | 3 |
| 3 | Abhiram Gopisetti | Technical | 4 |

## Common SELECT Clauses

| Clause | Purpose |
| --- | --- |
| SELECT | Retrieves data |
| FROM | Specifies the source table |
| WHERE | Filters records |
| DISTINCT | Removes duplicates |
| ORDER BY | Sorts results |
| GROUP BY | Groups rows |
| HAVING | Filters grouped data |
| LIMIT | Restricts returned rows |

## Important Points

- `SELECT` is used to retrieve data from database tables.
- Specific columns or all columns can be selected.
- The `WHERE` clause filters records before grouping.
- The `HAVING` clause filters records after grouping.
- `DISTINCT` removes duplicate values.
- `ORDER BY` sorts the result set.
- `LIMIT` restricts the number of returned rows.

## Conclusion

The SQL `SELECT` statement is the foundation of data retrieval in relational databases. By combining it with clauses such as `WHERE`, `DISTINCT`, `ORDER BY`, `GROUP BY`, and `HAVING`, users can efficiently query, filter, organize, and analyze data according to their requirements.



###
