# SQL Self Join

## Introduction

A SQL `Self Join` is a join in which a table is joined with itself. It is used when rows within the same table need to be compared or related to each other.

A Self Join is commonly used to represent hierarchical relationships such as employee-manager, parent-child, or category-subcategory relationships.

## Why Use a Self Join?

The `Self Join` helps you:

- Compare rows within the same table.
- Find employee-manager relationships.
- Represent hierarchical data.
- Analyze related records stored in a single table.
- Detect duplicates and dependencies.

## Syntax

```sql
SELECT columns
FROM table_name AS alias1
JOIN table_name AS alias2
ON alias1.column_name = alias2.column_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| alias1 | First reference to the table |
| alias2 | Second reference to the same table |
| JOIN | Combines rows from the same table |
| ON | Specifies the matching condition |

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
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    ManagerID INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees VALUES
(1, 'Akash', NULL),
(2, 'Mohit', 1),
(3, 'Abhiram', 1),
(4, 'Hemanth', 2);
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | ManagerID |
| --- | --- | --- |
| 1 | Akash | NULL |
| 2 | Mohit | 1 |
| 3 | Abhiram | 1 |
| 4 | Hemanth | 2 |

---

## Example 1: Employee and Manager Details

Retrieve employees along with their managers.

```sql
SELECT e.EmployeeName AS Employee,
       m.EmployeeName AS Manager
FROM Employees e
JOIN Employees m
ON e.ManagerID = m.EmployeeID;
```

### Output

| Employee | Manager |
| --- | --- |
| Mohit | Akash |
| Abhiram | Akash |
| Hemanth | Mohit |

### Explanation

- The Employees table is joined with itself.
- Alias `e` represents employees.
- Alias `m` represents managers.
- ManagerID is matched with EmployeeID.

---

## Example 2: Finding Employees Managed by Akash

```sql
SELECT e.EmployeeName
FROM Employees e
JOIN Employees m
ON e.ManagerID = m.EmployeeID
WHERE m.EmployeeName = 'Akash';
```

### Output

| EmployeeName |
| --- |
| Mohit |
| Abhiram |

### Explanation

- Retrieves employees whose manager is Akash.
- Uses a Self Join to establish the relationship.

---

## Applications of Self Join

### Employee-Manager Relationships

```sql
SELECT e.EmployeeName, m.EmployeeName
FROM Employees e
JOIN Employees m
ON e.ManagerID = m.EmployeeID;
```

### Parent-Child Relationships

```sql
SELECT c.ChildName, p.ParentName
FROM Family c
JOIN Family p
ON c.ParentID = p.PersonID;
```

### Finding Duplicate Records

```sql
SELECT a.Name, b.Name
FROM Employees a
JOIN Employees b
ON a.Email = b.Email;
```

---

## Self Join vs Regular Join

| Feature | Self Join | Regular Join |
| --- | --- | --- |
| Uses same table | Yes | No |
| Uses aliases | Yes | Optional |
| Compares rows within a table | Yes | No |
| Combines multiple tables | No | Yes |

---

## Best Practices

- Always use aliases when performing a Self Join.
- Use meaningful alias names for readability.
- Ensure proper join conditions to avoid unnecessary results.
- Use Self Joins for hierarchical relationships.

---

## Important Points

- A Self Join joins a table with itself.
- Aliases are required to distinguish table references.
- Commonly used for employee-manager relationships.
- Helps analyze hierarchical and related data.
- It is not a separate join type; it uses standard JOIN operations.

---

## Conclusion

The SQL `Self Join` is used to join a table with itself to compare or relate rows within the same table. It is especially useful for hierarchical structures such as employee-manager relationships, parent-child records, and other scenarios where data within a single table is interconnected.



###
