# SQL LIKE Operator

## Introduction

The SQL `LIKE` operator is used to search for specific patterns within text data stored in a column. It is commonly used with the `WHERE` clause to filter records based on partial matches rather than exact values.

The LIKE operator works with wildcard characters, making it a powerful tool for searching and filtering textual data.

## Why Use the LIKE Operator?

The `LIKE` operator helps you:

- Search for partial text matches.
- Find records based on patterns.
- Filter data using wildcards.
- Perform flexible text searches.
- Improve data retrieval without requiring exact values.

## Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name LIKE pattern;
```

### Syntax Components

| Component | Description |
| --- | --- |
| column_name | Column to be searched |
| LIKE | Pattern matching operator |
| pattern | Text pattern containing optional wildcards |

## Wildcards Used with LIKE

Wildcards allow pattern matching within strings.

| Wildcard | Description |
| --- | --- |
| % | Represents zero or more characters |
| _ | Represents exactly one character |
| [] | Represents any single character within brackets (SQL Server) |
| - | Represents a range inside brackets |

### Common Patterns

| Pattern | Meaning |
| --- | --- |
| 'A%' | Starts with A |
| '%A' | Ends with A |
| 'A%T' | Starts with A and ends with T |
| '%SQL%' | Contains SQL |
| '_A%' | A is the second character |
| 'A__%' | Starts with A and contains at least 3 characters |

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
CREATE TABLE Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100),
    City VARCHAR(50),
    Address VARCHAR(150)
);
```

## Inserting Sample Records

```sql
INSERT INTO Suppliers
VALUES
(1, 'Cafe Delight', 'Madrid', 'Kungsgatan 15'),
(2, 'Central Foods', 'London', 'Baker Street'),
(3, 'Capital Traders', 'Madrid', 'Kungsgatan 24'),
(4, 'Golden Supplies', 'Rome', 'Main Road'),
(5, 'Coffee House', 'Madrid', 'Central Avenue'),
(6, 'Fresh Market', 'Paris', 'River Street');
```

Display all records:

```sql
SELECT * FROM Suppliers;
```

### Output

| SupplierID | SupplierName | City | Address |
| --- | --- | --- | --- |
| 1 | Cafe Delight | Madrid | Kungsgatan 15 |
| 2 | Central Foods | London | Baker Street |
| 3 | Capital Traders | Madrid | Kungsgatan 24 |
| 4 | Golden Supplies | Rome | Main Road |
| 5 | Coffee House | Madrid | Central Avenue |
| 6 | Fresh Market | Paris | River Street |

---

## Example 1: Names Starting with 'Ca'

Retrieve suppliers whose names start with "Ca".

```sql
SELECT SupplierID,
       SupplierName,
       Address
FROM Suppliers
WHERE SupplierName LIKE 'Ca%';
```

### Output

| SupplierID | SupplierName |
| --- | --- |
| 1 | Cafe Delight |
| 3 | Capital Traders |

### Explanation

- `Ca%` matches values beginning with "Ca".
- Any number of characters may follow after "Ca".

---

## Example 2: Address Contains 'Kungsgatan'

Retrieve suppliers whose address contains the word "Kungsgatan".

```sql
SELECT *
FROM Suppliers
WHERE Address LIKE '%Kungsgatan%';
```

### Output

| SupplierID | SupplierName |
| --- | --- |
| 1 | Cafe Delight |
| 3 | Capital Traders |

### Explanation

- `%` before and after the text allows matching anywhere within the string.
- The word can appear at the beginning, middle, or end.

---

## Example 3: Second Character Pattern

Retrieve suppliers whose names have "a" as the second character.

```sql
SELECT SupplierID,
       SupplierName
FROM Suppliers
WHERE SupplierName LIKE '_a%';
```

### Output

| SupplierID | SupplierName |
| --- | --- |
| 1 | Cafe Delight |
| 3 | Capital Traders |

### Explanation

- `_` represents exactly one character.
- The second character must be "a".

---

## Example 4: LIKE with AND

Retrieve suppliers located in Madrid whose names start with "C".

```sql
SELECT SupplierID,
       SupplierName,
       City
FROM Suppliers
WHERE City = 'Madrid'
AND SupplierName LIKE 'C%';
```

### Output

| SupplierID | SupplierName | City |
| --- | --- | --- |
| 1 | Cafe Delight | Madrid |
| 3 | Capital Traders | Madrid |
| 5 | Coffee House | Madrid |

### Explanation

- The city must be Madrid.
- The supplier name must begin with C.
- Both conditions must be satisfied.

---

## Example 5: NOT LIKE Operator

Retrieve suppliers whose names do not contain "Co".

```sql
SELECT SupplierID,
       SupplierName
FROM Suppliers
WHERE SupplierName NOT LIKE '%Co%';
```

### Output

| SupplierID | SupplierName |
| --- | --- |
| 1 | Cafe Delight |
| 2 | Central Foods |
| 3 | Capital Traders |
| 4 | Golden Supplies |
| 6 | Fresh Market |

### Explanation

- `NOT LIKE` reverses the pattern match.
- Records containing "Co" are excluded.

---

## Example 6: Names Ending with 's'

Retrieve suppliers whose names end with "s".

```sql
SELECT SupplierID,
       SupplierName
FROM Suppliers
WHERE SupplierName LIKE '%s';
```

### Output

| SupplierID | SupplierName |
| --- | --- |
| 2 | Central Foods |

### Explanation

- `%s` matches any text ending with the letter "s".
- Characters before "s" can be anything.

---

## Example 7: Exact Character Length Pattern

Retrieve suppliers whose names start with "C" and contain exactly five characters.

```sql
SELECT SupplierName
FROM Suppliers
WHERE SupplierName LIKE 'C____';
```

### Explanation

- Each underscore represents one character.
- The pattern matches names beginning with C and containing exactly five characters.

---

## LIKE vs = Operator

| Feature | LIKE | = |
| --- | --- | --- |
| Exact Match | No | Yes |
| Pattern Matching | Yes | No |
| Supports Wildcards | Yes | No |
| Flexible Searching | Yes | No |

---

## Common Use Cases

### Search Employees by Name

```sql
SELECT *
FROM Employees
WHERE EmployeeName LIKE 'A%';
```

### Search Products Containing a Word

```sql
SELECT *
FROM Products
WHERE ProductName LIKE '%Laptop%';
```

### Find Customers Ending with a Specific Letter

```sql
SELECT *
FROM Customers
WHERE CustomerName LIKE '%n';
```

---

## Best Practices

- Use LIKE for pattern-based searches.
- Use = when exact matches are required.
- Avoid leading wildcards (`%text`) when possible for better performance.
- Create indexes on frequently searched columns.
- Use NOT LIKE when excluding patterns.

---

## Important Points

- LIKE is used for pattern matching.
- `%` represents zero or more characters.
- `_` represents exactly one character.
- NOT LIKE excludes matching patterns.
- LIKE is commonly used with the WHERE clause.
- Case sensitivity depends on the database system.

---

## Conclusion

The SQL `LIKE` operator is a powerful pattern-matching tool that allows flexible searching of text data. By using wildcards such as `%` and `_`, developers can efficiently retrieve records based on partial matches, making LIKE an essential operator for filtering and searching data in SQL databases.



###
