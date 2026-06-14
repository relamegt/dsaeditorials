# SQL Subquery

## Introduction

A SQL Subquery is a query nested inside another SQL query. The inner query executes first, and its result is used by the outer query. Subqueries help perform complex filtering, comparisons, calculations, and data manipulation operations.

Subqueries are commonly used to:

- Filter data using results from another query.
- Perform dynamic comparisons.
- Use aggregate functions such as AVG(), MAX(), and SUM().
- Update or delete records based on query results.
- Simplify complex SQL statements.

---

## Why Use Subqueries?

Subqueries help you:

- Break complex queries into smaller parts.
- Improve query readability.
- Retrieve data based on dynamic conditions.
- Perform advanced filtering and comparisons.
- Work with aggregated data efficiently.

---

## Syntax

### Subquery in WHERE Clause

```sql id="w8h4nk"
SELECT column_name
FROM table_name
WHERE column_name operator
(
    SELECT column_name
    FROM table_name
    WHERE condition
);
```

### Subquery in FROM Clause

```sql id="nywqyt"
SELECT *
FROM
(
    SELECT column_name
    FROM table_name
) AS subquery_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| Outer Query | Main query executed after the subquery |
| Subquery | Query inside another query |
| Operator | Comparison operator such as =, &gt;, &lt;, IN |
| Alias | Temporary name for a derived table |

---

## Creating a Sample Database

```sql id="7qmqe8"
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql id="m4tfo6"
USE AlphaKnowledgeDB;
```

---

## Creating a Sample Table

```sql id="ayxk81"
CREATE TABLE Students (
    RollNo INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50),
    Score INT
);
```

---

## Inserting Sample Records

```sql id="j89k7u"
INSERT INTO Students VALUES
(1, 'Akash', 'Vijayawada', 85),
(2, 'Akhil', 'Hyderabad', 70),
(3, 'Hemanth', 'Guntur', 95),
(4, 'Mohit', 'Vijayawada', 78),
(5, 'Abhiram', 'Hyderabad', 88);
```

Display all records:

```sql id="fd8u3u"
SELECT * FROM Students;
```

### Output

| RollNo | StudentName | City | Score |
| --- | --- | --- | --- |
| 1 | Akash | Vijayawada | 85 |
| 2 | Akhil | Hyderabad | 70 |
| 3 | Hemanth | Guntur | 95 |
| 4 | Mohit | Vijayawada | 78 |
| 5 | Abhiram | Hyderabad | 88 |

---

## Types of Subqueries

### Single-Row Subquery

Returns exactly one row.

```sql id="e0nv1u"
SELECT *
FROM Students
WHERE Score =
(
    SELECT MAX(Score)
    FROM Students
);
```

### Multi-Row Subquery

Returns multiple rows.

```sql id="i81mbd"
SELECT *
FROM Students
WHERE City IN
(
    SELECT City
    FROM Students
    WHERE Score > 80
);
```

### Correlated Subquery

Depends on values from the outer query.

```sql id="9e50uk"
SELECT s1.StudentName, s1.Score
FROM Students s1
WHERE s1.Score >
(
    SELECT AVG(s2.Score)
    FROM Students s2
    WHERE s2.City = s1.City
);
```

---

## Example 1: Subquery with WHERE Clause

Find students whose score is greater than the average score.

```sql id="1blotm"
SELECT *
FROM Students
WHERE Score >
(
    SELECT AVG(Score)
    FROM Students
);
```

### Output

| RollNo | StudentName | Score |
| --- | --- | --- |
| 1 | Akash | 85 |
| 3 | Hemanth | 95 |
| 5 | Abhiram | 88 |

### Explanation

- The subquery calculates the average score.
- The outer query retrieves students scoring above that average.

---

## Example 2: Single-Row Subquery

Find the student with the highest score.

```sql id="y8cd7i"
SELECT *
FROM Students
WHERE Score =
(
    SELECT MAX(Score)
    FROM Students
);
```

### Output

| RollNo | StudentName | Score |
| --- | --- | --- |
| 3 | Hemanth | 95 |

### Explanation

- MAX() returns the highest score.
- The outer query finds the matching student.

---

## Example 3: Multi-Row Subquery

Find students belonging to cities where at least one student scored above 85.

```sql id="bbqzz7"
SELECT *
FROM Students
WHERE City IN
(
    SELECT City
    FROM Students
    WHERE Score > 85
);
```

### Output

| RollNo | StudentName | City |
| --- | --- | --- |
| 2 | Akhil | Hyderabad |
| 3 | Hemanth | Guntur |
| 5 | Abhiram | Hyderabad |

### Explanation

- The subquery returns cities meeting the condition.
- The outer query retrieves all students from those cities.

---

## Example 4: Subquery with UPDATE

Increase scores of students from Hyderabad.

```sql id="tgm3r4"
UPDATE Students
SET Score = Score + 5
WHERE City IN
(
    SELECT City
    FROM Students
    WHERE City = 'Hyderabad'
);
```

Display updated records:

```sql id="75mb2h"
SELECT * FROM Students;
```

### Explanation

- The subquery identifies Hyderabad.
- The UPDATE statement modifies matching records.

---

## Example 5: Subquery with DELETE

Delete students whose score is below the average score.

```sql id="7z20h8"
DELETE FROM Students
WHERE Score <
(
    SELECT AVG(Score)
    FROM Students
);
```

### Explanation

- The subquery calculates the average score.
- Students scoring below average are removed.

---

## Example 6: Subquery in FROM Clause

Use a subquery as a temporary table.

```sql id="df6xki"
SELECT StudentName, Score
FROM
(
    SELECT StudentName, Score
    FROM Students
    WHERE Score > 80
) AS HighScorers;
```

### Output

| StudentName | Score |
| --- | --- |
| Akash | 85 |
| Hemanth | 95 |
| Abhiram | 88 |

### Explanation

- The subquery creates a temporary result set.
- The outer query retrieves selected columns.

---

## Example 7: Subquery with JOIN

Combine subqueries and joins.

```sql id="m1vqwn"
SELECT s.StudentName, s.City
FROM Students s
INNER JOIN
(
    SELECT RollNo
    FROM Students
    WHERE Score > 80
) h
ON s.RollNo = h.RollNo;
```

### Output

| StudentName | City |
| --- | --- |
| Akash | Vijayawada |
| Hemanth | Guntur |
| Abhiram | Hyderabad |

### Explanation

- The subquery retrieves high-scoring students.
- INNER JOIN combines matching records.

---

## Best Practices

- Keep subqueries simple and readable.
- Use JOINs when they provide better performance.
- Avoid deeply nested subqueries.
- Use aliases for derived tables.
- Test subqueries separately before embedding them.

---

## Important Points

- A subquery is a query inside another query.
- Subqueries can be used in SELECT, WHERE, FROM, and HAVING clauses.
- Single-row subqueries return one value.
- Multi-row subqueries return multiple values.
- Correlated subqueries execute once for each outer query row.

---

## Conclusion

SQL Subqueries are powerful tools for performing advanced filtering, calculations, and data manipulation. They allow one query to use the result of another query, making complex database operations easier to write and understand. By combining subqueries with clauses such as WHERE, FROM, UPDATE, DELETE, and JOIN, developers can create flexible and efficient SQL solutions.



###
