# SQL UNION ALL Operator

## Introduction

The SQL `UNION ALL` operator combines the result sets of two or more SELECT statements into a single output.

Unlike `UNION`, the `UNION ALL` operator does not remove duplicate rows. It returns all records from every SELECT statement, making it faster and more efficient when duplicate values are acceptable.

## Why Use UNION ALL?

The `UNION ALL` operator helps you:

- Combine results from multiple queries.
- Retain duplicate records.
- Improve performance compared to UNION.
- Merge large datasets efficiently.
- Consolidate information from multiple tables.

## Syntax

```sql
SELECT column1, column2, ...
FROM table1

UNION ALL

SELECT column1, column2, ...
FROM table2;
```

### Syntax Components

| Component | Description |
| --- | --- |
| UNION ALL | Combines result sets including duplicates |
| SELECT | Retrieves records from a table |
| table1, table2 | Tables participating in the operation |
| column1, column2 | Columns being combined |

## Rules for Using UNION ALL

- Every SELECT statement must return the same number of columns.
- Corresponding columns must have compatible data types.
- Column names in the final output are taken from the first SELECT statement.
- Duplicate records are not removed.
- ORDER BY can only be used at the end of the entire query.

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating Sample Tables

### Students

```sql
CREATE TABLE Students (
    RollNo INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT,
    Country VARCHAR(50)
);
```

### TripDetails

```sql
CREATE TABLE TripDetails (
    RollNo INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT,
    Country VARCHAR(50)
);
```

## Inserting Sample Records

### Students

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 21, 'India'),
(2, 'Mohit', 20, 'USA'),
(3, 'Abhiram', 22, 'India'),
(4, 'Hemesh', 19, 'Canada');
```

### TripDetails

```sql
INSERT INTO TripDetails
VALUES
(5, 'Sai', 22, 'India'),
(6, 'Akash', 21, 'India'),
(7, 'Rahul', 24, 'Germany'),
(8, 'Mohit', 20, 'USA');
```

Display the records:

```sql
SELECT * FROM Students;
```

```sql
SELECT * FROM TripDetails;
```

### Output

#### Students

| RollNo | Name | Age | Country |
| --- | --- | --- | --- |
| 1 | Akash | 21 | India |
| 2 | Mohit | 20 | USA |
| 3 | Abhiram | 22 | India |
| 4 | Hemesh | 19 | Canada |

#### TripDetails

| RollNo | Name | Age | Country |
| --- | --- | --- | --- |
| 5 | Sai | 22 | India |
| 6 | Akash | 21 | India |
| 7 | Rahul | 24 | Germany |
| 8 | Mohit | 20 | USA |

---

## Example 1: UNION ALL on a Single Column

Combine all names from both tables.

```sql
SELECT Name
FROM Students

UNION ALL

SELECT Name
FROM TripDetails;
```

### Output

| Name |
| --- |
| Akash |
| Mohit |
| Abhiram |
| Hemesh |
| Sai |
| Akash |
| Rahul |
| Mohit |

### Explanation

- Records from both tables are combined.
- Duplicate names are preserved.
- Akash and Mohit appear twice.

---

## Example 2: UNION ALL on Multiple Columns

Combine names and countries from both tables.

```sql
SELECT Name, Country
FROM Students

UNION ALL

SELECT Name, Country
FROM TripDetails;
```

### Output

| Name | Country |
| --- | --- |
| Akash | India |
| Mohit | USA |
| Abhiram | India |
| Hemesh | Canada |
| Sai | India |
| Akash | India |
| Rahul | Germany |
| Mohit | USA |

### Explanation

- Both queries return the same number of columns.
- Duplicate rows are included in the final result.

---

## Example 3: Using Aliases with UNION ALL

Combine Roll Numbers from both tables using a common column name.

```sql
SELECT RollNo AS Identifier
FROM Students

UNION ALL

SELECT RollNo AS Identifier
FROM TripDetails;
```

### Output

| Identifier |
| --- |
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |
| 6 |
| 7 |
| 8 |

### Explanation

- Aliases make the final column name consistent.
- UNION ALL combines all values without duplicate checking.

---

## Example 4: UNION ALL with WHERE Clause

Retrieve students older than 20 years from both tables.

```sql
SELECT Name, Age
FROM Students
WHERE Age > 20

UNION ALL

SELECT Name, Age
FROM TripDetails
WHERE Age > 20;
```

### Output

| Name | Age |
| --- | --- |
| Akash | 21 |
| Abhiram | 22 |
| Sai | 22 |
| Akash | 21 |
| Rahul | 24 |

### Explanation

- Each SELECT statement applies its own filtering.
- UNION ALL combines the filtered results.
- Duplicate rows remain in the output.

---

## Example 5: UNION ALL with ORDER BY

Combine all countries and sort them alphabetically.

```sql
SELECT Country
FROM Students

UNION ALL

SELECT Country
FROM TripDetails

ORDER BY Country;
```

### Output

| Country |
| --- |
| Canada |
| Germany |
| India |
| India |
| India |
| India |
| USA |
| USA |

### Explanation

- UNION ALL preserves duplicates.
- ORDER BY sorts the final combined result.

---

## Example 6: Counting Records Using UNION ALL

Count all countries from both tables including duplicates.

```sql
SELECT COUNT(*)
FROM
(
    SELECT Country
    FROM Students

    UNION ALL

    SELECT Country
    FROM TripDetails
) AS CombinedCountries;
```

### Output

| COUNT(*) |
| --- |
| 8 |

### Explanation

- UNION ALL combines all rows.
- COUNT(*) includes duplicate values in the total count.

---

## Example 7: UNION vs UNION ALL

### Using UNION

```sql
SELECT Country
FROM Students

UNION

SELECT Country
FROM TripDetails;
```

### Output

| Country |
| --- |
| India |
| USA |
| Canada |
| Germany |

### Using UNION ALL

```sql
SELECT Country
FROM Students

UNION ALL

SELECT Country
FROM TripDetails;
```

### Output

| Country |
| --- |
| India |
| USA |
| India |
| Canada |
| India |
| India |
| Germany |
| USA |

### Explanation

- UNION removes duplicates.
- UNION ALL retains duplicates.
- UNION ALL generally executes faster because duplicate elimination is not required.

---

## UNION ALL vs UNION

| Feature | UNION ALL | UNION |
| --- | --- | --- |
| Removes Duplicates | No | Yes |
| Includes Duplicate Rows | Yes | No |
| Performance | Faster | Slower |
| Memory Usage | Lower | Higher |
| Duplicate Checking | No | Yes |
| Best Use Case | Large datasets | Unique results |

---

## Common Use Cases

### Combine Student Lists

```sql
SELECT Name
FROM Students

UNION ALL

SELECT Name
FROM Alumni;
```

### Combine Customer Records

```sql
SELECT CustomerName
FROM OnlineCustomers

UNION ALL

SELECT CustomerName
FROM OfflineCustomers;
```

### Merge Product Data

```sql
SELECT ProductName
FROM Electronics

UNION ALL

SELECT ProductName
FROM Furniture;
```

### Consolidate Sales Records

```sql
SELECT SaleAmount
FROM Sales2024

UNION ALL

SELECT SaleAmount
FROM Sales2025;
```

---

## Best Practices

- Use UNION ALL when duplicate values are acceptable.
- Ensure all SELECT statements return compatible columns.
- Apply filtering before UNION ALL whenever possible.
- Use ORDER BY only at the end of the combined query.
- Prefer UNION ALL for large datasets to improve performance.

---

## Important Points

- UNION ALL combines results from multiple SELECT statements.
- Duplicate rows are retained.
- It is faster than UNION because duplicate checking is skipped.
- Corresponding columns must have compatible data types.
- ORDER BY is applied only to the final combined result.
- Frequently used in reporting and data consolidation tasks.

---

## Conclusion

The SQL `UNION ALL` operator is an efficient way to combine result sets from multiple queries while preserving duplicate records. Because it does not perform duplicate elimination, it generally provides better performance than UNION. It is particularly useful when working with large datasets, historical records, logs, and reporting systems where every record must be retained.



###
