# SQL UNION Operator

## Introduction

The SQL `UNION` operator is used to combine the results of two or more SELECT statements into a single result set.

The UNION operator removes duplicate rows and returns only unique records from all combined queries. It is commonly used when data needs to be retrieved from multiple tables or multiple queries and displayed together.

## Why Use UNION?

The `UNION` operator helps you:

- Combine results from multiple queries.
- Merge data from different tables.
- Eliminate duplicate records automatically.
- Create consolidated reports.
- Simplify data retrieval from multiple sources.

## Syntax

```sql
SELECT column1, column2, ...
FROM table1

UNION

SELECT column1, column2, ...
FROM table2;
```

### Syntax Components

| Component | Description |
| --- | --- |
| UNION | Combines result sets and removes duplicates |
| SELECT | Retrieves data from tables |
| table1, table2 | Tables participating in the UNION |
| column1, column2 | Columns being combined |

## Rules for Using UNION

- Each SELECT statement must have the same number of columns.
- Corresponding columns must have compatible data types.
- Column names in the final result are taken from the first SELECT statement.
- UNION automatically removes duplicate rows.
- ORDER BY can only be used at the end of the combined query.

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating Sample Tables

### Employees2024

```sql
CREATE TABLE Employees2024 (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Country VARCHAR(50)
);
```

### Employees2025

```sql
CREATE TABLE Employees2025 (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Country VARCHAR(50)
);
```

## Inserting Sample Records

### Employees2024

```sql
INSERT INTO Employees2024
VALUES
(1, 'Akash', 'India'),
(2, 'Mohit', 'USA'),
(3, 'Abhiram', 'Germany'),
(4, 'Hemesh', 'India');
```

### Employees2025

```sql
INSERT INTO Employees2025
VALUES
(5, 'Sai', 'India'),
(6, 'Rahul', 'Canada'),
(7, 'Kiran', 'Germany'),
(8, 'Nikhil', 'Australia');
```

Display the records:

```sql
SELECT * FROM Employees2024;
```

```sql
SELECT * FROM Employees2025;
```

### Output

#### Employees2024

| EmployeeID | EmployeeName | Country |
| --- | --- | --- |
| 1 | Akash | India |
| 2 | Mohit | USA |
| 3 | Abhiram | Germany |
| 4 | Hemesh | India |

#### Employees2025

| EmployeeID | EmployeeName | Country |
| --- | --- | --- |
| 5 | Sai | India |
| 6 | Rahul | Canada |
| 7 | Kiran | Germany |
| 8 | Nikhil | Australia |

---

## Example 1: Basic UNION

Retrieve unique countries from both tables.

```sql
SELECT Country
FROM Employees2024

UNION

SELECT Country
FROM Employees2025;
```

### Output

| Country |
| --- |
| India |
| USA |
| Germany |
| Canada |
| Australia |

### Explanation

- UNION combines countries from both tables.
- Duplicate values such as India and Germany appear only once.
- The final result contains only unique countries.

---

## Example 2: UNION with ORDER BY

Retrieve unique countries and sort them alphabetically.

```sql
SELECT Country
FROM Employees2024

UNION

SELECT Country
FROM Employees2025

ORDER BY Country;
```

### Output

| Country |
| --- |
| Australia |
| Canada |
| Germany |
| India |
| USA |

### Explanation

- UNION combines and removes duplicate countries.
- ORDER BY sorts the final result set.

---

## Example 3: UNION on Multiple Columns

Retrieve employee names and countries from both tables.

```sql
SELECT EmployeeName, Country
FROM Employees2024

UNION

SELECT EmployeeName, Country
FROM Employees2025;
```

### Output

| EmployeeName | Country |
| --- | --- |
| Akash | India |
| Mohit | USA |
| Abhiram | Germany |
| Hemesh | India |
| Sai | India |
| Rahul | Canada |
| Kiran | Germany |
| Nikhil | Australia |

### Explanation

- Both queries return two columns.
- UNION combines the results into one output.
- Duplicate rows would be removed automatically.

---

## Example 4: UNION ALL

Retrieve all countries including duplicates.

```sql
SELECT Country
FROM Employees2024

UNION ALL

SELECT Country
FROM Employees2025;
```

### Output

| Country |
| --- |
| India |
| USA |
| Germany |
| India |
| India |
| Canada |
| Germany |
| Australia |

### Explanation

- UNION ALL does not remove duplicates.
- Every matching row from both tables is returned.
- UNION ALL is generally faster than UNION because duplicate checking is skipped.

---

## Example 5: UNION with WHERE Clause

Retrieve employees from India from both tables.

```sql
SELECT EmployeeName, Country
FROM Employees2024
WHERE Country = 'India'

UNION

SELECT EmployeeName, Country
FROM Employees2025
WHERE Country = 'India';
```

### Output

| EmployeeName | Country |
| --- | --- |
| Akash | India |
| Hemesh | India |
| Sai | India |

### Explanation

- Each SELECT statement applies its own WHERE condition.
- UNION combines the filtered results.

---

## Example 6: UNION with Different Tables

Create another table:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);
```

Insert records:

```sql
INSERT INTO Customers
VALUES
(1, 'Ravi'),
(2, 'Suresh');
```

Retrieve names from both tables.

```sql
SELECT EmployeeName AS PersonName
FROM Employees2024

UNION

SELECT CustomerName
FROM Customers;
```

### Output

| PersonName |
| --- |
| Akash |
| Mohit |
| Abhiram |
| Hemesh |
| Ravi |
| Suresh |

### Explanation

- UNION can combine data from completely different tables.
- The number of columns and data types must match.

---

## Example 7: UNION with Aggregate Functions

Retrieve countries from both tables and count unique countries.

```sql
SELECT COUNT(*)
FROM
(
    SELECT Country
    FROM Employees2024

    UNION

    SELECT Country
    FROM Employees2025
) AS UniqueCountries;
```

### Output

| COUNT(*) |
| --- |
| 5 |

### Explanation

- UNION first creates a unique list of countries.
- COUNT() calculates the total number of unique countries.

---

## UNION vs UNION ALL

| Feature | UNION | UNION ALL |
| --- | --- | --- |
| Removes Duplicates | Yes | No |
| Returns Unique Records | Yes | No |
| Performance | Slower | Faster |
| Duplicate Checking | Yes | No |
| Most Common Use | Reporting | Large Data Processing |

---

## Common Use Cases

### Combine Employee Records

```sql
SELECT EmployeeName
FROM Employees2024

UNION

SELECT EmployeeName
FROM Employees2025;
```

### Combine Product Lists

```sql
SELECT ProductName
FROM Electronics

UNION

SELECT ProductName
FROM Furniture;
```

### Merge Customer Data

```sql
SELECT CustomerName
FROM OnlineCustomers

UNION

SELECT CustomerName
FROM OfflineCustomers;
```

### Retrieve Unique Cities

```sql
SELECT City
FROM Customers

UNION

SELECT City
FROM Suppliers;
```

---

## Best Practices

- Ensure both queries return the same number of columns.
- Use compatible data types across queries.
- Use UNION ALL when duplicate removal is unnecessary.
- Apply filtering before UNION whenever possible.
- Use ORDER BY only at the end of the UNION query.

---

## Important Points

- UNION combines results from multiple SELECT statements.
- Duplicate rows are automatically removed.
- UNION ALL keeps all rows including duplicates.
- Corresponding columns must have compatible data types.
- ORDER BY is applied to the final combined result.
- UNION is commonly used for reporting and data consolidation.

---

## Conclusion

The SQL `UNION` operator is a powerful tool for combining results from multiple queries into a single result set. By automatically removing duplicate records, it helps generate clean and meaningful outputs. Understanding the difference between UNION and UNION ALL allows developers to choose the most efficient approach for reporting, analytics, and data integration tasks.



###
