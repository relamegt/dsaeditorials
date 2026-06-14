# SQL Logical Operators

## Introduction

SQL Logical Operators are used to combine, compare, and negate conditions in SQL queries. They help filter records based on multiple criteria and return results that evaluate to TRUE, FALSE, or UNKNOWN.

Logical operators are commonly used with the `WHERE`, `HAVING`, and `JOIN` clauses to perform advanced data filtering and decision-making.

## Why Use Logical Operators?

Logical operators help you:

- Combine multiple conditions in a query.
- Filter data more precisely.
- Build complex search criteria.
- Compare values against subquery results.
- Improve query flexibility and readability.

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
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(100),
    EmpCity VARCHAR(50),
    EmpCountry VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

## Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(101, 'Akash', 'London', 'UK', 85000),
(102, 'Mohit', 'Rome', 'Italy', 55000),
(103, 'Abhiram', 'Madrid', 'Spain', 72000),
(104, 'Hemesh', 'London', 'UK', 68000),
(105, 'Sai', 'New York', 'USA', 92000),
(106, 'Rahul', 'Rome', 'Italy', 61000);
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmpID | EmpName | EmpCity | EmpCountry | Salary |
| --- | --- | --- | --- | --- |
| 101 | Akash | London | UK | 85000 |
| 102 | Mohit | Rome | Italy | 55000 |
| 103 | Abhiram | Madrid | Spain | 72000 |
| 104 | Hemesh | London | UK | 68000 |
| 105 | Sai | New York | USA | 92000 |
| 106 | Rahul | Rome | Italy | 61000 |

---

## AND Operator

The `AND` operator returns records only when all specified conditions are TRUE.

### Example 1: Employees from London and UK

```sql
SELECT *
FROM Employees
WHERE EmpCity = 'London'
AND EmpCountry = 'UK';
```

### Output

| EmpID | EmpName |
| --- | --- |
| 101 | Akash |
| 104 | Hemesh |

### Explanation

- Both conditions must be satisfied.
- Only employees from London in the UK are returned.

---

## OR Operator

The `OR` operator returns records when at least one condition is TRUE.

### Example 2: Employees from UK or USA

```sql
SELECT *
FROM Employees
WHERE EmpCountry = 'UK'
OR EmpCountry = 'USA';
```

### Output

| EmpID | EmpName |
| --- | --- |
| 101 | Akash |
| 104 | Hemesh |
| 105 | Sai |

### Explanation

- Records matching either condition are returned.
- Employees from both countries appear in the result.

---

## NOT Operator

The `NOT` operator reverses the result of a condition.

### Example 3: Cities Not Starting with 'S'

```sql
SELECT *
FROM Employees
WHERE EmpCity NOT LIKE 'S%';
```

### Explanation

- Excludes cities beginning with the letter S.
- Returns all remaining employees.

---

## IN Operator

The `IN` operator checks whether a value exists in a specified list.

### Example 4: Employees from London or Rome

```sql
SELECT *
FROM Employees
WHERE EmpCity IN ('London', 'Rome');
```

### Output

| EmpID | EmpName |
| --- | --- |
| 101 | Akash |
| 102 | Mohit |
| 104 | Hemesh |
| 106 | Rahul |

### Explanation

- IN simplifies multiple OR conditions.
- Returns employees from either city.

---

## LIKE Operator

The `LIKE` operator performs pattern matching.

### Example 5: Cities Starting with M

```sql
SELECT *
FROM Employees
WHERE EmpCity LIKE 'M%';
```

### Output

| EmpID | EmpName |
| --- | --- |
| 103 | Abhiram |

### Explanation

- `%` represents any number of characters.
- Matches all city names beginning with M.

---

## BETWEEN Operator

The `BETWEEN` operator checks whether a value falls within a specified range.

### Example 6: Employee IDs Between 102 and 105

```sql
SELECT *
FROM Employees
WHERE EmpID BETWEEN 102 AND 105;
```

### Output

| EmpID |
| --- |
| 102 |
| 103 |
| 104 |
| 105 |

### Explanation

- BETWEEN includes both boundary values.
- IDs 102 and 105 are included.

---

## ALL Operator

The `ALL` operator compares a value against all values returned by a subquery.

### Example 7: IDs Greater Than All London Employees

```sql
SELECT *
FROM Employees
WHERE EmpID > ALL (
    SELECT EmpID
    FROM Employees
    WHERE EmpCity = 'London'
);
```

### Explanation

- Compares EmpID with every value returned by the subquery.
- Returns only IDs greater than all London employee IDs.

---

## ANY Operator

The `ANY` operator returns TRUE if the condition matches at least one value from a subquery.

### Example 8: Match Any Employee ID from Rome

```sql
SELECT *
FROM Employees
WHERE EmpID = ANY (
    SELECT EmpID
    FROM Employees
    WHERE EmpCity = 'Rome'
);
```

### Output

| EmpID | EmpName |
| --- | --- |
| 102 | Mohit |
| 106 | Rahul |

### Explanation

- Returns rows matching any value from the subquery result.

---

## EXISTS Operator

The `EXISTS` operator checks whether a subquery returns any rows.

### Example 9: Check If London Employees Exist

```sql
SELECT EmpName
FROM Employees
WHERE EXISTS (
    SELECT *
    FROM Employees
    WHERE EmpCity = 'London'
);
```

### Explanation

- EXISTS returns TRUE if the subquery produces at least one row.
- Since London employees exist, all employee names are returned.

---

## SOME Operator

The `SOME` operator works similarly to ANY and checks whether a condition is TRUE for at least one value.

### Example 10: IDs Less Than Some London Employee IDs

```sql
SELECT *
FROM Employees
WHERE EmpID < SOME (
    SELECT EmpID
    FROM Employees
    WHERE EmpCity = 'London'
);
```

### Explanation

- Returns employees whose IDs are less than at least one London employee ID.

---

## Comparison of Logical Operators

| Operator | Purpose |
| --- | --- |
| AND | All conditions must be TRUE |
| OR | At least one condition must be TRUE |
| NOT | Reverses a condition |
| IN | Matches values from a list |
| LIKE | Pattern matching |
| BETWEEN | Checks a range of values |
| ALL | Must satisfy comparison with all values |
| ANY | Must satisfy comparison with at least one value |
| EXISTS | Checks if rows exist |
| SOME | Similar to ANY |

---

## Common Use Cases

### Filter Employees by Multiple Conditions

```sql
SELECT *
FROM Employees
WHERE Salary > 60000
AND EmpCountry = 'UK';
```

### Search Using Patterns

```sql
SELECT *
FROM Employees
WHERE EmpName LIKE 'A%';
```

### Retrieve Values from a List

```sql
SELECT *
FROM Employees
WHERE EmpCity IN ('London', 'Rome');
```

---

## Best Practices

- Use AND and OR carefully with parentheses.
- Prefer IN over multiple OR conditions.
- Use EXISTS for efficient subquery checks.
- Use BETWEEN for range-based filtering.
- Ensure subqueries used with ALL, ANY, and SOME return appropriate results.

---

## Important Points

- Logical operators control how conditions are evaluated.
- AND requires all conditions to be TRUE.
- OR requires at least one condition to be TRUE.
- NOT reverses a condition.
- EXISTS checks for the presence of rows.
- ANY and SOME behave similarly in most databases.
- BETWEEN includes both lower and upper boundaries.

---

## Conclusion

SQL Logical Operators are fundamental tools for filtering and controlling query results. They allow developers to combine conditions, perform pattern matching, evaluate ranges, and work with subqueries efficiently. Mastering logical operators helps create more powerful, flexible, and accurate SQL queries.



###
