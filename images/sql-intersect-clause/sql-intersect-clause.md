# SQL INTERSECT Clause

## Introduction

The SQL `INTERSECT` operator is used to return only the rows that are present in the result sets of both SELECT queries. It works like the mathematical intersection of two sets and helps identify common records between tables or query results.

The `INTERSECT` operator automatically removes duplicate rows and returns only unique matching records.

## Why Use INTERSECT?

The `INTERSECT` operator helps you:

- Find common records between two tables.
- Compare datasets efficiently.
- Remove duplicate matching rows automatically.
- Identify overlapping data across multiple sources.
- Simplify complex comparison queries.

## Syntax

```sql
SELECT column1, column2, ...
FROM table1

INTERSECT

SELECT column1, column2, ...
FROM table2;
```

### Syntax Components

| Component | Description |
| --- | --- |
| INTERSECT | Returns common rows from both queries |
| SELECT | Retrieves data from tables |
| table1, table2 | Tables being compared |
| column1, column2 | Columns to compare |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating Sample Tables

### Customers Table

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    City VARCHAR(50)
);
```

### Orders Table

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT
);
```

## Inserting Sample Records

### Customers

```sql
INSERT INTO Customers
VALUES
(1, 'Akash', 'Vijayawada'),
(2, 'Mohit', 'Hyderabad'),
(3, 'Abhiram', 'Guntur'),
(4, 'Sai', 'Vijayawada'),
(5, 'Hemesh', 'Hyderabad');
```

### Orders

```sql
INSERT INTO Orders
VALUES
(101, 2),
(102, 3),
(103, 5),
(104, 2),
(105, 3);
```

Display the Customers table:

```sql
SELECT * FROM Customers;
```

### Output

| CustomerID | FirstName | City |
| --- | --- | --- |
| 1 | Akash | Vijayawada |
| 2 | Mohit | Hyderabad |
| 3 | Abhiram | Guntur |
| 4 | Sai | Vijayawada |
| 5 | Hemesh | Hyderabad |

Display the Orders table:

```sql
SELECT * FROM Orders;
```

### Output

| OrderID | CustomerID |
| --- | --- |
| 101 | 2 |
| 102 | 3 |
| 103 | 5 |
| 104 | 2 |
| 105 | 3 |

---

## Example 1: Basic INTERSECT Query

Retrieve CustomerIDs that exist in both Customers and Orders tables.

```sql
SELECT CustomerID
FROM Customers

INTERSECT

SELECT CustomerID
FROM Orders;
```

### Output

| CustomerID |
| --- |
| 2 |
| 3 |
| 5 |

### Explanation

- The first query returns all customer IDs.
- The second query returns customer IDs that placed orders.
- INTERSECT returns only IDs found in both results.

---

## Example 2: INTERSECT with WHERE Clause

Retrieve customers from Hyderabad who have placed orders.

```sql
SELECT CustomerID
FROM Customers
WHERE City = 'Hyderabad'

INTERSECT

SELECT CustomerID
FROM Orders;
```

### Output

| CustomerID |
| --- |
| 2 |
| 5 |

### Explanation

- The first query selects Hyderabad customers.
- The second query selects customers with orders.
- INTERSECT returns customers satisfying both conditions.

---

## Example 3: INTERSECT with BETWEEN

Retrieve customers whose IDs are between 2 and 5 and who have placed orders.

```sql
SELECT CustomerID
FROM Customers
WHERE CustomerID BETWEEN 2 AND 5

INTERSECT

SELECT CustomerID
FROM Orders;
```

### Output

| CustomerID |
| --- |
| 2 |
| 3 |
| 5 |

### Explanation

- BETWEEN filters customer IDs within the specified range.
- INTERSECT returns only customers who also appear in Orders.

---

## Example 4: INTERSECT with LIKE

Retrieve customers whose names start with 'M' and who have placed orders.

```sql
SELECT CustomerID
FROM Customers
WHERE FirstName LIKE 'M%'

INTERSECT

SELECT CustomerID
FROM Orders;
```

### Output

| CustomerID |
| --- |
| 2 |

### Explanation

- The first query finds customers whose names begin with M.
- The second query returns customers with orders.
- INTERSECT returns the common customer.

---

## Example 5: INTERSECT with Multiple Columns

Retrieve common customer records using multiple columns.

```sql
SELECT CustomerID, FirstName
FROM Customers

INTERSECT

SELECT CustomerID, FirstName
FROM ArchivedCustomers;
```

### Explanation

- INTERSECT compares both columns together.
- Only rows matching all selected columns are returned.

---

# Rules for INTERSECT

- Both SELECT statements must return the same number of columns.
- Corresponding columns must have compatible data types.
- Duplicate rows are automatically removed.
- Column names in both queries do not need to match.
- The final result contains only common records.

---

# INTERSECT vs UNION vs EXCEPT

| Feature | INTERSECT | UNION | EXCEPT |
| --- | --- | --- | --- |
| Common Rows | Yes | No | No |
| Combines Results | No | Yes | No |
| Removes Duplicates | Yes | Yes | Yes |
| Returns Rows in First Query Only | No | No | Yes |
| Returns Rows in Both Queries | Yes | No | No |

---

## Common Use Cases

### Find Customers Who Placed Orders

```sql
SELECT CustomerID
FROM Customers

INTERSECT

SELECT CustomerID
FROM Orders;
```

### Find Common Products

```sql
SELECT ProductID
FROM CurrentProducts

INTERSECT

SELECT ProductID
FROM PreviousProducts;
```

### Compare Employee Records

```sql
SELECT EmployeeID
FROM CurrentEmployees

INTERSECT

SELECT EmployeeID
FROM FormerEmployees;
```

### Compare Two Query Results

```sql
SELECT City
FROM Customers

INTERSECT

SELECT City
FROM Suppliers;
```

---

## Best Practices

- Ensure both queries return the same number of columns.
- Use compatible data types in corresponding columns.
- Create indexes for better performance on large datasets.
- Use INTERSECT when you specifically need common records.
- Consider JOINs if your database does not support INTERSECT.

---

## Important Points

- INTERSECT returns only rows present in both queries.
- Duplicate rows are removed automatically.
- Both queries must have matching column structures.
- NULL values are treated as equal during comparison.
- INTERSECT is useful for comparing datasets and finding overlaps.
- Some databases such as MySQL do not support INTERSECT directly.

---

## Conclusion

The SQL `INTERSECT` operator is a powerful set operator used to retrieve only the common rows shared by two query results. It automatically removes duplicates and simplifies the process of comparing datasets. By understanding how INTERSECT works and when to use it, developers can efficiently identify matching records across tables and build more effective SQL queries.



###
