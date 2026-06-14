# Recursive Join in SQL

## Introduction

A Recursive Join in SQL is used to retrieve hierarchical or parent-child data from a table. It is commonly implemented using a Recursive Common Table Expression (CTE), where a query repeatedly joins a table with itself until all related records are retrieved.

Recursive joins are useful for representing organizational structures, category hierarchies, reporting relationships, and tree-like data.

## Why Use Recursive Joins?

Recursive joins help you:

- Retrieve hierarchical data.
- Work with parent-child relationships.
- Traverse tree structures.
- Generate employee-manager hierarchies.
- Simplify recursive data retrieval.

## Syntax

```sql
WITH RECURSIVE cte_name AS (
    -- Anchor Query
    SELECT columns
    FROM table_name
    WHERE condition

    UNION ALL

    -- Recursive Query
    SELECT t.columns
    FROM table_name t
    JOIN cte_name c
    ON t.column_name = c.column_name
)
SELECT *
FROM cte_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| WITH RECURSIVE | Creates a recursive CTE |
| Anchor Query | Starting point of recursion |
| UNION ALL | Combines anchor and recursive results |
| Recursive Query | Retrieves related records repeatedly |
| CTE | Temporary result set used recursively |

---

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
(4, 'Hemanth', 2),
(5, 'Akhil', 2);
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
| 5 | Akhil | 2 |

---

## Example 1: Employee Hierarchy

Display all employees reporting to Akash.

```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT EmployeeID, EmployeeName, ManagerID
    FROM Employees
    WHERE EmployeeID = 1

    UNION ALL

    SELECT e.EmployeeID, e.EmployeeName, e.ManagerID
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh
    ON e.ManagerID = eh.EmployeeID
)
SELECT *
FROM EmployeeHierarchy;
```

### Output

| EmployeeID | EmployeeName | ManagerID |
| --- | --- | --- |
| 1 | Akash | NULL |
| 2 | Mohit | 1 |
| 3 | Abhiram | 1 |
| 4 | Hemanth | 2 |
| 5 | Akhil | 2 |

### Explanation

- Akash is the root employee.
- Mohit and Abhiram report directly to Akash.
- Hemanth and Akhil report to Mohit.
- Recursive processing continues until no more employees are found.

---

## Example 2: Find Direct Subordinates

Display employees reporting directly to Mohit.

```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT EmployeeID, EmployeeName, ManagerID
    FROM Employees
    WHERE EmployeeID = 2

    UNION ALL

    SELECT e.EmployeeID, e.EmployeeName, e.ManagerID
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh
    ON e.ManagerID = eh.EmployeeID
)
SELECT *
FROM EmployeeHierarchy;
```

### Output

| EmployeeID | EmployeeName | ManagerID |
| --- | --- | --- |
| 2 | Mohit | 1 |
| 4 | Hemanth | 2 |
| 5 | Akhil | 2 |

### Explanation

- Mohit is selected as the starting employee.
- Hemanth and Akhil are found through recursion.

---

## Applications of Recursive Joins

### Employee-Manager Hierarchy

```sql
WITH RECURSIVE EmployeeHierarchy AS (...)
```

Used to display reporting structures.

### Category and Subcategory Systems

```sql
WITH RECURSIVE CategoryTree AS (...)
```

Used in e-commerce applications.

### Parent-Child Relationships

```sql
WITH RECURSIVE FamilyTree AS (...)
```

Used to traverse hierarchical relationships.

### Organization Charts

```sql
WITH RECURSIVE OrgStructure AS (...)
```

Used to display complete organizational structures.

## Recursive Join vs Self Join

| Feature | Recursive Join | Self Join |
| --- | --- | --- |
| Handles multiple hierarchy levels | Yes | No |
| Uses recursion | Yes | No |
| Uses CTE | Yes | No |
| Suitable for tree structures | Yes | Limited |
| Suitable for direct relationships | Yes | Yes |

---

## Best Practices

- Use recursive joins only when hierarchical data is involved.
- Define a clear anchor query.
- Avoid infinite recursion by ensuring proper relationships.
- Use indexing on parent and child columns.
- Test recursion depth for large datasets.

---

## Important Points

- Recursive joins are implemented using recursive CTEs.
- They repeatedly join a table with itself.
- Useful for hierarchical and tree-structured data.
- Consist of an anchor query and recursive query.
- Continue execution until no additional matching rows exist.

---

## Conclusion

Recursive joins in SQL provide an efficient way to retrieve hierarchical and parent-child data. By using recursive CTEs, complex structures such as employee hierarchies, category trees, and organizational charts can be queried easily while maintaining readable and scalable SQL code.



###
