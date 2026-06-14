# SQL NOT Operator

## Introduction

The SQL `NOT` operator is used to reverse the result of a condition. It returns records that do not satisfy the specified condition.

The NOT operator is commonly used in the `WHERE` clause to exclude unwanted records from query results. It can also be combined with operators such as `IN`, `LIKE`, `BETWEEN`, and `IS NULL` to create more powerful filtering conditions.

## Why Use the NOT Operator?

The `NOT` operator helps you:

- Exclude specific records from query results.
- Reverse Boolean conditions.
- Create negative filtering conditions.
- Improve query flexibility.
- Combine with other SQL operators for advanced filtering.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE NOT condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| NOT | Reverses the result of a condition |
| condition | Expression to evaluate |
| WHERE | Filters records based on conditions |

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
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    Country VARCHAR(50),
    PostalCode VARCHAR(20)
);
```

## Inserting Sample Records

```sql
INSERT INTO Customers
VALUES
(1, 'Akash', 'India', '520010'),
(2, 'Mohit', 'UK', 'SW1A1AA'),
(3, 'Abhiram', 'USA', '10001'),
(4, 'Hemesh', 'India', NULL),
(5, 'Sai', 'Canada', 'M5V2T6'),
(6, 'Manoj', 'UK', 'EC1A1BB');
```

Display all records:

```sql
SELECT * FROM Customers;
```

### Output

| CustomerID | CustomerName | Country | PostalCode |
| --- | --- | --- | --- |
| 1 | Akash | India | 520010 |
| 2 | Mohit | UK | SW1A1AA |
| 3 | Abhiram | USA | 10001 |
| 4 | Hemesh | India | NULL |
| 5 | Sai | Canada | M5V2T6 |
| 6 | Manoj | UK | EC1A1BB |

---

## Example 1: Excluding a Specific Value

Retrieve customers who are not from the UK.

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'UK';
```

### Output

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 1 | Akash | India |
| 3 | Abhiram | USA |
| 4 | Hemesh | India |
| 5 | Sai | Canada |

### Explanation

- The condition `Country = 'UK'` is evaluated first.
- The NOT operator reverses the result.
- Customers from the UK are excluded from the output.

---

## Example 2: Using NOT with IN

Retrieve customers who are not from the USA or UK.

```sql
SELECT *
FROM Customers
WHERE NOT Country IN ('USA', 'UK');
```

### Output

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 1 | Akash | India |
| 4 | Hemesh | India |
| 5 | Sai | Canada |

### Explanation

- The IN operator checks for matching countries.
- NOT reverses the result.
- Customers from USA and UK are excluded.

---

## Example 3: Using NOT with LIKE

Retrieve customers whose names do not start with the letter 'M'.

```sql
SELECT *
FROM Customers
WHERE NOT CustomerName LIKE 'M%';
```

### Output

| CustomerID | CustomerName |
| --- | --- |
| 1 | Akash |
| 3 | Abhiram |
| 4 | Hemesh |
| 5 | Sai |

### Explanation

- `LIKE 'M%'` finds names starting with M.
- NOT removes those matching records.
- Only customers whose names do not begin with M are displayed.

---

## Example 4: Using NOT with IS NULL

Retrieve customers whose postal code is not NULL.

```sql
SELECT *
FROM Customers
WHERE NOT PostalCode IS NULL;
```

### Output

| CustomerID | CustomerName | PostalCode |
| --- | --- | --- |
| 1 | Akash | 520010 |
| 2 | Mohit | SW1A1AA |
| 3 | Abhiram | 10001 |
| 5 | Sai | M5V2T6 |
| 6 | Manoj | EC1A1BB |

### Explanation

- `IS NULL` identifies NULL values.
- NOT reverses the condition.
- Only rows with valid postal codes are returned.

---

## Example 5: Using NOT with AND

Retrieve customers who are neither from the USA nor from the UK.

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'USA'
AND NOT Country = 'UK';
```

### Output

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 1 | Akash | India |
| 4 | Hemesh | India |
| 5 | Sai | Canada |

### Explanation

- The first condition excludes USA customers.
- The second condition excludes UK customers.
- Only customers from other countries are displayed.

---

## Example 6: Using NOT with BETWEEN

Retrieve customers whose IDs are not between 2 and 5.

```sql
SELECT *
FROM Customers
WHERE CustomerID NOT BETWEEN 2 AND 5;
```

### Output

| CustomerID | CustomerName |
| --- | --- |
| 1 | Akash |
| 6 | Manoj |

### Explanation

- BETWEEN checks values within the specified range.
- NOT excludes values inside that range.
- Only records outside the range are returned.

---

## Example 7: Using NOT with Multiple Conditions

Retrieve customers who are not from India and whose names do not start with M.

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'India'
AND NOT CustomerName LIKE 'M%';
```

### Output

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 3 | Abhiram | USA |
| 5 | Sai | Canada |

### Explanation

- Records must satisfy both negative conditions.
- Customers from India are excluded.
- Names beginning with M are also excluded.

---

## Common Use Cases

### Exclude Specific Countries

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'USA';
```

### Exclude Multiple Categories

```sql
SELECT *
FROM Products
WHERE Category NOT IN ('Electronics', 'Furniture');
```

### Exclude Names Starting with a Letter

```sql
SELECT *
FROM Employees
WHERE EmployeeName NOT LIKE 'A%';
```

### Exclude NULL Values

```sql
SELECT *
FROM Orders
WHERE NOT DeliveryDate IS NULL;
```

---

## Best Practices

- Use NOT only when it improves readability.
- Prefer NOT IN when excluding multiple values.
- Use NOT LIKE for pattern exclusion.
- Be careful when combining NOT with NULL values.
- Use parentheses when working with complex logical conditions.

---

## Important Points

- NOT reverses the result of a condition.
- It is commonly used with WHERE clauses.
- NOT can be combined with IN, LIKE, BETWEEN, and IS NULL.
- It helps exclude unwanted records from query results.
- Complex filtering conditions can be created using NOT with logical operators.

---

## Conclusion

The SQL `NOT` operator is a powerful filtering tool that allows developers to exclude records based on specific conditions. By reversing Boolean expressions, it provides greater flexibility in data retrieval and works effectively with operators such as IN, LIKE, BETWEEN, and IS NULL. Proper use of NOT helps create cleaner, more precise, and easier-to-maintain SQL queries.



###
