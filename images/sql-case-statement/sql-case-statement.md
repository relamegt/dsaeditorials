# SQL CASE Statement

## Introduction

The SQL `CASE` statement is used to add conditional logic to SQL queries. It evaluates conditions sequentially and returns a value when the first matching condition is found.

The CASE statement works similarly to an IF-THEN-ELSE structure in programming languages and is commonly used for categorizing data, transforming values, and creating dynamic outputs.

## Why Use CASE?

The `CASE` statement helps you:

- Add conditional logic within SQL queries.
- Categorize data into meaningful groups.
- Transform values dynamically.
- Create custom sorting rules.
- Improve reporting and data presentation.

## Types of CASE Statements

SQL supports two forms of CASE expressions:

1. Simple CASE Expression
2. Searched CASE Expression

## Syntax

### Simple CASE Expression

```sql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ELSE result
END
```

### Searched CASE Expression

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END
```

### Syntax Components

| Component | Description |
| --- | --- |
| CASE | Starts the conditional expression |
| WHEN | Specifies a value or condition to evaluate |
| THEN | Value returned when condition is true |
| ELSE | Default value if no condition matches |
| END | Ends the CASE statement |

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
    Age INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Customers
VALUES
(1, 'Akash', 'India', 21),
(2, 'Mohit', 'United Kingdom', 22),
(3, 'Abhiram', 'Australia', 24),
(4, 'Hemesh', 'Japan', 23),
(5, 'Sai', 'Spain', 26);
```

Display all records:

```sql
SELECT * FROM Customers;
```

### Output

| CustomerID | CustomerName | Country | Age |
| --- | --- | --- | --- |
| 1 | Akash | India | 21 |
| 2 | Mohit | United Kingdom | 22 |
| 3 | Abhiram | Australia | 24 |
| 4 | Hemesh | Japan | 23 |
| 5 | Sai | Spain | 26 |

---

## Example 1: Simple CASE Expression

Classify customers based on their country.

```sql
SELECT CustomerName,
       Country,
       CASE Country
           WHEN 'India' THEN 'Indian'
           WHEN 'Japan' THEN 'Japanese'
           WHEN 'Australia' THEN 'Australian'
           WHEN 'Spain' THEN 'Spanish'
           ELSE 'Other'
       END AS Nationality
FROM Customers;
```

### Output

| CustomerName | Country | Nationality |
| --- | --- | --- |
| Akash | India | Indian |
| Mohit | United Kingdom | Other |
| Abhiram | Australia | Australian |
| Hemesh | Japan | Japanese |
| Sai | Spain | Spanish |

### Explanation

- The CASE expression compares Country values.
- The corresponding nationality is returned.
- ELSE handles unmatched countries.

---

## Example 2: CASE with Multiple Conditions

Display age categories for customers.

```sql
SELECT CustomerName,
       Age,
       CASE
           WHEN Age < 22 THEN 'Young Adult'
           WHEN Age BETWEEN 22 AND 25 THEN 'Adult'
           WHEN Age > 25 THEN 'Senior Adult'
           ELSE 'Unknown'
       END AS AgeGroup
FROM Customers;
```

### Output

| CustomerName | Age | AgeGroup |
| --- | --- | --- |
| Akash | 21 | Young Adult |
| Mohit | 22 | Adult |
| Abhiram | 24 | Adult |
| Hemesh | 23 | Adult |
| Sai | 26 | Senior Adult |

### Explanation

- Conditions are evaluated from top to bottom.
- The first matching condition determines the output.
- ELSE acts as a default value.

---

## Example 3: CASE with ORDER BY

Display customers by giving priority to customers from Japan.

```sql
SELECT CustomerName,
       Country,
       CASE
           WHEN Country = 'Japan' THEN 0
           ELSE 1
       END AS SortPriority
FROM Customers
ORDER BY SortPriority, Country;
```

### Output

| CustomerName | Country | SortPriority |
| --- | --- | --- |
| Hemesh | Japan | 0 |
| Abhiram | Australia | 1 |
| Akash | India | 1 |
| Sai | Spain | 1 |
| Mohit | United Kingdom | 1 |

### Explanation

- CASE generates a custom sorting value.
- Japanese customers appear first.
- Remaining records are sorted alphabetically.

---

## Example 4: CASE with Aggregate Functions

Count customers based on age groups.

```sql
SELECT
CASE
    WHEN Age < 23 THEN 'Below 23'
    ELSE '23 and Above'
END AS AgeCategory,
COUNT(*) AS TotalCustomers
FROM Customers
GROUP BY
CASE
    WHEN Age < 23 THEN 'Below 23'
    ELSE '23 and Above'
END;
```

### Output

| AgeCategory | TotalCustomers |
| --- | --- |
| Below 23 | 2 |
| 23 and Above | 3 |

### Explanation

- CASE creates dynamic categories.
- GROUP BY groups records based on those categories.
- COUNT calculates the total records in each group.

---

## Example 5: CASE with UPDATE

Increase customer age based on conditions.

```sql
UPDATE Customers
SET Age =
CASE
    WHEN Age < 23 THEN Age + 1
    ELSE Age + 2
END;
```

### Explanation

- Customers below age 23 receive an increment of 1 year.
- Others receive an increment of 2 years.
- CASE applies different updates based on conditions.

---

## Example 6: CASE for Calculated Output

Display customer discount categories.

```sql
SELECT CustomerName,
       CASE
           WHEN Age < 22 THEN '5% Discount'
           WHEN Age BETWEEN 22 AND 25 THEN '10% Discount'
           ELSE '15% Discount'
       END AS DiscountCategory
FROM Customers;
```

### Output

| CustomerName | DiscountCategory |
| --- | --- |
| Akash | 5% Discount |
| Mohit | 10% Discount |
| Abhiram | 10% Discount |
| Hemesh | 10% Discount |
| Sai | 15% Discount |

### Explanation

- CASE creates dynamic discount categories.
- Different values are returned based on age.

---

## CASE vs IF

| Feature | CASE | IF |
| --- | --- | --- |
| ANSI SQL Standard | Yes | No |
| Multiple Conditions | Yes | Limited |
| Supported Across Databases | Yes | Depends on DBMS |
| Used in SELECT Queries | Yes | Limited |

---

## Common Use Cases

### Categorize Employees

```sql
SELECT EmployeeName,
CASE
    WHEN Salary > 80000 THEN 'High Salary'
    ELSE 'Standard Salary'
END
FROM Employees;
```

### Generate Grade Labels

```sql
SELECT StudentName,
CASE
    WHEN Marks >= 90 THEN 'A'
    WHEN Marks >= 75 THEN 'B'
    ELSE 'C'
END
FROM Students;
```

### Custom Sorting

```sql
ORDER BY
CASE
    WHEN Department = 'Management' THEN 1
    ELSE 2
END;
```

### Dynamic Reports

```sql
SELECT ProductName,
CASE
    WHEN Stock = 0 THEN 'Out of Stock'
    ELSE 'Available'
END
FROM Products;
```

---

## Best Practices

- Use CASE for readable conditional logic.
- Keep conditions simple and well organized.
- Place more specific conditions before general ones.
- Always include an ELSE clause when possible.
- Use meaningful aliases for CASE results.

---

## Important Points

- CASE adds conditional logic to SQL queries.
- Conditions are evaluated sequentially.
- The first matching condition is returned.
- ELSE executes when no conditions match.
- CASE can be used in SELECT, WHERE, ORDER BY, GROUP BY, UPDATE, and HAVING clauses.
- CASE is ANSI SQL compliant and supported by most databases.

---

## Conclusion

The SQL `CASE` statement is a powerful feature that allows developers to incorporate conditional logic directly into SQL queries. It helps categorize data, create dynamic outputs, customize sorting, and simplify complex reporting requirements. By mastering CASE expressions, you can build more flexible, readable, and efficient SQL queries.



###
