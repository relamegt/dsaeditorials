# SQL IN Operator

## Introduction

The SQL `IN` operator is used to filter records by checking whether a column's value matches any value in a specified list. It provides a cleaner and more readable alternative to writing multiple `OR` conditions.

The IN operator can work with both explicit values and subqueries, making it a powerful tool for filtering data efficiently.

## Why Use the IN Operator?

The `IN` operator helps you:

- Simplify multiple OR conditions.
- Improve query readability.
- Filter records using a list of values.
- Work efficiently with subqueries.
- Reduce query complexity.

## Syntax

### IN with Explicit Values

```sql
SELECT column_name
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

### IN with a Subquery

```sql
SELECT column_name
FROM table_name
WHERE column_name IN (
    SELECT column_name
    FROM another_table
);
```

### Syntax Components

| Component | Description |
| --- | --- |
| IN | Checks whether a value exists in a list |
| value1, value2 | Values to compare against |
| column_name | Column being evaluated |
| subquery | Query returning values for comparison |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Sample Employee Table

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Department VARCHAR(50),
    Address VARCHAR(100)
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(101, 'Akash', 'Kumar', 'Technical', 'Tokyo, Japan'),
(102, 'Mohit', 'Sharma', 'Content', 'Paris, France'),
(103, 'Abhiram', 'Reddy', 'Technical', 'London, UK'),
(104, 'Hemesh', 'Kumar', 'Database', 'Madrid, Spain'),
(105, 'Sai', 'Krishna', 'Management', 'Paris, France');
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | FirstName | LastName | Department | Address |
| --- | --- | --- | --- | --- |
| 101 | Akash | Kumar | Technical | Tokyo, Japan |
| 102 | Mohit | Sharma | Content | Paris, France |
| 103 | Abhiram | Reddy | Technical | London, UK |
| 104 | Hemesh | Kumar | Database | Madrid, Spain |
| 105 | Sai | Krishna | Management | Paris, France |

---

## Example 1: Basic Use of the IN Operator

Retrieve employees whose address is either Tokyo or Paris.

```sql
SELECT FirstName,
       LastName
FROM Employees
WHERE Address IN ('Tokyo, Japan', 'Paris, France');
```

### Output

| FirstName | LastName |
| --- | --- |
| Akash | Kumar |
| Mohit | Sharma |
| Sai | Krishna |

### Explanation

- The IN operator checks whether Address matches any value in the list.
- It replaces multiple OR conditions with a cleaner syntax.

Equivalent query using OR:

```sql
SELECT FirstName,
       LastName
FROM Employees
WHERE Address = 'Tokyo, Japan'
OR Address = 'Paris, France';
```

---

## Example 2: Using NOT IN

Retrieve employees whose address is not Tokyo or London.

```sql
SELECT FirstName
FROM Employees
WHERE Address NOT IN ('Tokyo, Japan', 'London, UK');
```

### Output

| FirstName |
| --- |
| Mohit |
| Hemesh |
| Sai |

### Explanation

- NOT IN excludes specified values.
- Only records with other addresses are returned.

---

## Example 3: IN Operator with Numeric Values

Retrieve employees belonging to departments with IDs 1, 3, and 5.

```sql
SELECT *
FROM Employees
WHERE EmployeeID IN (101, 103, 105);
```

### Output

| EmployeeID | FirstName |
| --- | --- |
| 101 | Akash |
| 103 | Abhiram |
| 105 | Sai |

### Explanation

- IN works with numeric values as well as strings.
- Records matching any listed value are returned.

---

## Creating a Manager Table

```sql
CREATE TABLE Managers (
    EmployeeID INT PRIMARY KEY
);
```

Insert sample records:

```sql
INSERT INTO Managers
VALUES
(101),
(105);
```

Display the table:

```sql
SELECT * FROM Managers;
```

### Output

| EmployeeID |
| --- |
| 101 |
| 105 |

---

## Example 4: IN Operator with a Subquery

Retrieve details of employees who are managers.

```sql
SELECT *
FROM Employees
WHERE EmployeeID IN (
    SELECT EmployeeID
    FROM Managers
);
```

### Output

| EmployeeID | FirstName |
| --- | --- |
| 101 | Akash |
| 105 | Sai |

### Explanation

- The subquery retrieves manager IDs.
- The outer query returns employees whose IDs exist in that list.
- This is a common use of IN with related tables.

---

## Example 5: NOT IN with a Subquery

Retrieve employees who are not managers.

```sql
SELECT *
FROM Employees
WHERE EmployeeID NOT IN (
    SELECT EmployeeID
    FROM Managers
);
```

### Output

| EmployeeID | FirstName |
| --- | --- |
| 102 | Mohit |
| 103 | Abhiram |
| 104 | Hemesh |

### Explanation

- The subquery returns manager IDs.
- NOT IN excludes those employees from the result.

---

## Example 6: IN with Multiple Conditions

Retrieve employees from the Technical or Database departments.

```sql
SELECT *
FROM Employees
WHERE Department IN ('Technical', 'Database');
```

### Output

| EmployeeID | FirstName | Department |
| --- | --- | --- |
| 101 | Akash | Technical |
| 103 | Abhiram | Technical |
| 104 | Hemesh | Database |

### Explanation

- Multiple department values are checked in a single condition.
- This improves readability compared to multiple OR statements.

---

## IN vs OR Operator

| Feature | IN | OR |
| --- | --- | --- |
| Readability | High | Lower with many values |
| Multiple Values | Yes | Yes |
| Query Length | Short | Long |
| Supports Subqueries | Yes | No |

---

## Common Use Cases

### Filter Multiple Departments

```sql
SELECT *
FROM Employees
WHERE Department IN ('Technical', 'Content');
```

### Filter Multiple Cities

```sql
SELECT *
FROM Customers
WHERE City IN ('Hyderabad', 'Vijayawada', 'Guntur');
```

### Filter Records Using a Subquery

```sql
SELECT *
FROM Orders
WHERE CustomerID IN (
    SELECT CustomerID
    FROM Customers
);
```

---

## Best Practices

- Use IN instead of multiple OR conditions whenever possible.
- Use NOT IN carefully when NULL values may exist.
- Prefer subqueries with IN for related table filtering.
- Keep value lists concise and meaningful.
- Ensure data types match between the column and comparison values.

---

## Important Points

- IN checks whether a value exists in a list.
- NOT IN excludes values from a list.
- IN can work with explicit values or subqueries.
- IN improves readability over multiple OR conditions.
- The operator returns TRUE if any listed value matches.
- Subqueries make IN useful for relational filtering.

---

## Conclusion

The SQL `IN` operator is a simple yet powerful filtering tool that allows developers to compare a value against multiple possible matches. It improves query readability, reduces complexity, and works seamlessly with subqueries. By using IN and NOT IN effectively, developers can write cleaner and more maintainable SQL queries.



###
