# SQL RENAME VIEW

## Introduction

The SQL RENAME VIEW operation is used to change the name of an existing view without affecting its structure, underlying data, or functionality. Renaming views helps maintain clarity and consistency when business requirements or naming conventions change.

Benefits of renaming a view:

- Improves database readability.
- Aligns view names with business requirements.
- Maintains existing view logic.
- Avoids recreating views unnecessarily.
- Keeps database objects organized.

---

## Why Rename a View?

Renaming a view helps you:

- Follow updated naming conventions.
- Improve schema organization.
- Make view names more descriptive.
- Reflect changes in business terminology.
- Maintain a clean database structure.

---

## Syntax

### SQL Server

```sql
EXEC sp_rename 'old_view_name', 'new_view_name';
```

### Syntax Components

| Component | Description |
| --- | --- |
| sp_rename | SQL Server system procedure used for renaming objects |
| old_view_name | Existing view name |
| new_view_name | New view name |

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

## Creating a Sample Table

```sql
CREATE TABLE Sales (
    ProductID INT,
    ProductName VARCHAR(100),
    Quantity INT
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Sales VALUES
(101, 'Laptop', 15),
(102, 'Keyboard', 25),
(101, 'Laptop', 10),
(103, 'Mouse', 30),
(102, 'Keyboard', 20);
```

Display the table:

```sql
SELECT * FROM Sales;
```

### Output

| ProductID | ProductName | Quantity |
| --- | --- | --- |
| 101 | Laptop | 15 |
| 102 | Keyboard | 25 |
| 101 | Laptop | 10 |
| 103 | Mouse | 30 |
| 102 | Keyboard | 20 |

---

## Example 1: Creating a View

Create a view that displays total quantity sold for each product.

```sql
CREATE VIEW SalesReport AS
SELECT ProductID,
       SUM(Quantity) AS TotalQuantity
FROM Sales
GROUP BY ProductID;
```

Display the view:

```sql
SELECT * FROM SalesReport;
```

### Output

| ProductID | TotalQuantity |
| --- | --- |
| 101 | 25 |
| 102 | 45 |
| 103 | 30 |

### Explanation

- The view groups records by ProductID.
- SUM() calculates the total quantity sold.
- The view acts as a virtual table.

---

## Example 2: Renaming the View

Rename the view from SalesReport to MonthlySalesReport.

```sql
EXEC sp_rename 'SalesReport', 'MonthlySalesReport';
```

### Explanation

- The view name changes.
- The view definition remains unchanged.
- Underlying table data is unaffected.

---

## Example 3: Verifying the Renamed View

Retrieve data using the new view name.

```sql
SELECT * FROM MonthlySalesReport;
```

### Output

| ProductID | TotalQuantity |
| --- | --- |
| 101 | 25 |
| 102 | 45 |
| 103 | 30 |

### Explanation

- The renamed view works exactly like the original view.
- Only the view name has changed.
- All calculations and logic remain intact.

---

## Example 4: Renaming a Student View

Create a student view.

```sql
CREATE VIEW StudentMarksView AS
SELECT
    RollNo,
    StudentName,
    Marks
FROM Students;
```

Rename the view.

```sql
EXEC sp_rename 'StudentMarksView', 'StudentPerformanceView';
```

Display the renamed view.

```sql
SELECT * FROM StudentPerformanceView;
```

### Explanation

- StudentMarksView is renamed.
- Student data remains unchanged.
- Queries must use the new view name.

---

## Best Practices

- Use meaningful and descriptive view names.
- Follow consistent naming conventions.
- Verify dependent applications after renaming.
- Rename views during maintenance windows when possible.
- Document renamed database objects.

---

## Important Points

- Renaming a view does not modify underlying data.
- View definitions remain unchanged.
- SQL Server uses the sp_rename procedure.
- Existing queries must use the new view name.
- Renaming improves database maintainability.

---

## Conclusion

The SQL RENAME VIEW operation allows database administrators and developers to update view names without recreating views or affecting underlying data. It improves readability, maintains consistency, and helps keep database schemas organized while preserving existing functionality.



###
