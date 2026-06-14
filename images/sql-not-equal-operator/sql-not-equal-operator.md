# SQL NOT EQUAL Operator

## Introduction

The SQL `NOT EQUAL` operator is used to compare two values and return records where the values are not equal.

It is commonly used in the `WHERE` clause to exclude specific values from query results. If the compared values are equal, the condition returns FALSE. If either value is NULL, the result is UNKNOWN (NULL).

SQL supports two not-equal operators:

```sql
<>
```

```sql
!=
```

Although both work similarly in many database systems, `<>` is the SQL standard and is generally recommended.

## Why Use the NOT EQUAL Operator?

The NOT EQUAL operator helps you:

- Exclude specific values from query results.
- Filter unwanted records.
- Create negative search conditions.
- Work with both numeric and text values.
- Combine multiple filtering conditions.

## Syntax

### Using the Standard Operator

```sql
SELECT column_name
FROM table_name
WHERE column_name <> value;
```

### Using Alternative Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name != value;
```

### Syntax Components

| Component | Description |
| --- | --- |
| &lt;&gt; | Standard SQL not equal operator |
| != | Alternative not equal operator |
| column_name | Column being compared |
| value | Value to exclude |

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
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50),
    Score INT,
    RankPosition INT,
    CodingStreak INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 'Vijayawada', 98, 3, 150),
(2, 'Mohit', 'Hyderabad', 92, 5, 120),
(3, 'Abhiram', 'Guntur', 100, 1, 180),
(4, 'Hemesh', 'Vijayawada', 89, 6, 95),
(5, 'Sai', 'Hyderabad', 96, 4, 130),
(6, 'Rahul', 'Guntur', 88, 7, 110);
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | City | Score | RankPosition | CodingStreak |
| --- | --- | --- | --- | --- | --- |
| 1 | Akash | Vijayawada | 98 | 3 | 150 |
| 2 | Mohit | Hyderabad | 92 | 5 | 120 |
| 3 | Abhiram | Guntur | 100 | 1 | 180 |
| 4 | Hemesh | Vijayawada | 89 | 6 | 95 |
| 5 | Sai | Hyderabad | 96 | 4 | 130 |
| 6 | Rahul | Guntur | 88 | 7 | 110 |

---

## Example 1: NOT EQUAL with String Values

Retrieve all students whose name is not 'Sai'.

```sql
SELECT *
FROM Students
WHERE StudentName <> 'Sai';
```

### Output

| StudentID | StudentName |
| --- | --- |
| 1 | Akash |
| 2 | Mohit |
| 3 | Abhiram |
| 4 | Hemesh |
| 6 | Rahul |

### Explanation

- The query compares each student's name with 'Sai'.
- Records that do not match are returned.
- The record containing Sai is excluded.

---

## Example 2: NOT EQUAL with Numeric Values

Retrieve students whose score is not 100.

```sql
SELECT *
FROM Students
WHERE Score <> 100;
```

### Output

| StudentName | Score |
| --- | --- |
| Akash | 98 |
| Mohit | 92 |
| Hemesh | 89 |
| Sai | 96 |
| Rahul | 88 |

### Explanation

- Students with a score of 100 are excluded.
- All remaining records are returned.

---

## Example 3: NOT EQUAL with Multiple Conditions

Retrieve students whose score is not 98, rank is not 3, and coding streak is at least 100.

```sql
SELECT *
FROM Students
WHERE Score <> 98
  AND RankPosition <> 3
  AND CodingStreak >= 100;
```

### Output

| StudentName | Score | RankPosition | CodingStreak |
| --- | --- | --- | --- |
| Mohit | 92 | 5 | 120 |
| Abhiram | 100 | 1 | 180 |
| Sai | 96 | 4 | 130 |
| Rahul | 88 | 7 | 110 |

### Explanation

- Students with score 98 are excluded.
- Students with rank 3 are excluded.
- Only students with coding streaks greater than or equal to 100 are included.

---

## Example 4: Using != Operator

Retrieve students whose city is not Hyderabad.

```sql
SELECT *
FROM Students
WHERE City != 'Hyderabad';
```

### Output

| StudentName | City |
| --- | --- |
| Akash | Vijayawada |
| Abhiram | Guntur |
| Hemesh | Vijayawada |
| Rahul | Guntur |

### Explanation

- The `!=` operator performs the same function as `<>`.
- Students from Hyderabad are excluded.

---

## Example 5: NOT EQUAL with GROUP BY

Display the count of students grouped by city where score is not 100.

```sql
SELECT City,
       COUNT(*) AS TotalStudents
FROM Students
WHERE Score <> 100
GROUP BY City;
```

### Output

| City | TotalStudents |
| --- | --- |
| Vijayawada | 2 |
| Hyderabad | 2 |
| Guntur | 1 |

### Explanation

- Records with score 100 are removed first.
- Remaining students are grouped by city.
- COUNT() calculates the number of students in each group.

---

## Example 6: NOT EQUAL with ORDER BY

Retrieve students whose rank is not 1 and sort them by score.

```sql
SELECT *
FROM Students
WHERE RankPosition <> 1
ORDER BY Score DESC;
```

### Output

| StudentName | Score |
| --- | --- |
| Akash | 98 |
| Sai | 96 |
| Mohit | 92 |
| Hemesh | 89 |
| Rahul | 88 |

### Explanation

- The student with rank 1 is excluded.
- Remaining records are sorted by score in descending order.

---

## Example 7: NOT EQUAL with NULL Values

Consider the following records:

```sql
INSERT INTO Students
VALUES
(7, 'Kiran', 'Chennai', NULL, 8, 90);
```

Query:

```sql
SELECT *
FROM Students
WHERE Score <> 100;
```

### Explanation

- NULL cannot be compared directly using `<>` or `!=`.
- Rows containing NULL values are not returned by the condition.
- Use `IS NULL` or `IS NOT NULL` when working with NULL values.

---

## Difference Between &lt;&gt; and !=

| Feature | &lt;&gt; | != |
| --- | --- | --- |
| SQL Standard | Yes | No |
| Supported by Most Databases | Yes | Yes |
| Recommended Usage | Yes | No |
| Functionality | Same | Same |

---

## Common Use Cases

### Exclude a Specific Department

```sql
SELECT *
FROM Employees
WHERE Department <> 'HR';
```

### Exclude a Specific City

```sql
SELECT *
FROM Customers
WHERE City <> 'Mumbai';
```

### Exclude a Particular Status

```sql
SELECT *
FROM Orders
WHERE Status <> 'Cancelled';
```

### Exclude a Specific Product Category

```sql
SELECT *
FROM Products
WHERE Category <> 'Electronics';
```

---

## Best Practices

- Prefer `<>` because it follows the SQL standard.
- Use NOT EQUAL conditions carefully with NULL values.
- Combine with AND and OR for advanced filtering.
- Use meaningful conditions to improve query readability.
- Test queries involving NULL values separately.

---

## Important Points

- NOT EQUAL is used to exclude matching values.
- SQL supports both `<>` and `!=`.
- `<>` is the SQL-standard operator.
- NULL values are not evaluated as equal or not equal.
- The operator works with numbers, strings, and dates.
- NOT EQUAL is commonly used inside WHERE clauses.

---

## Conclusion

The SQL NOT EQUAL operator is a simple but powerful filtering tool used to exclude specific values from query results. Whether working with numbers, text, or dates, it helps create precise conditions and retrieve only the required data. Understanding the difference between `<>` and `!=`, along with proper handling of NULL values, allows developers to write cleaner and more reliable SQL queries.



###
