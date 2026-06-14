# SQL DISTINCT Clause

## Introduction

The SQL `DISTINCT` clause is used to eliminate duplicate values from query results and return only unique records. It is commonly used when a table contains repeated data and you want to view only distinct values.

The DISTINCT keyword can be applied to a single column or multiple columns. When used with multiple columns, it returns unique combinations of those column values.

## Why Use DISTINCT?

The `DISTINCT` clause helps you:

- Remove duplicate values from query results.
- Display only unique records.
- Generate cleaner reports.
- Count unique values in a dataset.
- Analyze data without repetition.

## Syntax

### DISTINCT on a Single Column

```sql
SELECT DISTINCT column_name
FROM table_name;
```

### DISTINCT on Multiple Columns

```sql
SELECT DISTINCT column1, column2
FROM table_name;
```

### Syntax Components

| Component | Description |
| --- | --- |
| DISTINCT | Removes duplicate rows from the result |
| column_name | Column whose unique values are required |
| table_name | Table from which data is retrieved |

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
    RollNo INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50),
    Age INT
);
```

## Inserting Sample Records

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 'Vijayawada', 21),
(2, 'Mohit', 'Hyderabad', 22),
(3, 'Abhiram', 'Vijayawada', 21),
(4, 'Hemesh', 'Guntur', 23),
(5, 'Akash', 'Vijayawada', 21),
(6, 'Sai', 'Hyderabad', 22);
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| RollNo | StudentName | City | Age |
| --- | --- | --- | --- |
| 1 | Akash | Vijayawada | 21 |
| 2 | Mohit | Hyderabad | 22 |
| 3 | Abhiram | Vijayawada | 21 |
| 4 | Hemesh | Guntur | 23 |
| 5 | Akash | Vijayawada | 21 |
| 6 | Sai | Hyderabad | 22 |

---

## Example 1: DISTINCT on a Single Column

Retrieve unique city names.

```sql
SELECT DISTINCT City
FROM Students;
```

### Output

| City |
| --- |
| Vijayawada |
| Hyderabad |
| Guntur |

### Explanation

- Duplicate city values are removed.
- Each city appears only once in the result.

---

## Example 2: DISTINCT on Student Names

Retrieve unique student names.

```sql
SELECT DISTINCT StudentName
FROM Students;
```

### Output

| StudentName |
| --- |
| Akash |
| Mohit |
| Abhiram |
| Hemesh |
| Sai |

### Explanation

- Although Akash appears multiple times, DISTINCT returns it only once.

---

## Example 3: DISTINCT on Multiple Columns

Retrieve unique combinations of city and age.

```sql
SELECT DISTINCT City, Age
FROM Students;
```

### Output

| City | Age |
| --- | --- |
| Vijayawada | 21 |
| Hyderabad | 22 |
| Guntur | 23 |

### Explanation

- DISTINCT considers both columns together.
- Duplicate City–Age combinations are removed.

---

## Example 4: DISTINCT with ORDER BY

Display unique cities in alphabetical order.

```sql
SELECT DISTINCT City
FROM Students
ORDER BY City;
```

### Output

| City |
| --- |
| Guntur |
| Hyderabad |
| Vijayawada |

### Explanation

- DISTINCT removes duplicates.
- ORDER BY sorts the unique values.

---

## Example 5: Counting Unique Values

Count the number of unique cities.

```sql
SELECT COUNT(DISTINCT City) AS TotalCities
FROM Students;
```

### Output

| TotalCities |
| --- |
| 3 |

### Explanation

- DISTINCT identifies unique cities.
- COUNT calculates how many unique cities exist.

---

## Example 6: DISTINCT with WHERE Clause

Retrieve unique cities where age is greater than 21.

```sql
SELECT DISTINCT City
FROM Students
WHERE Age > 21;
```

### Output

| City |
| --- |
| Hyderabad |
| Guntur |

### Explanation

- WHERE filters rows first.
- DISTINCT removes duplicate city names from the filtered result.

---

## Example 7: DISTINCT with Multiple Conditions

Retrieve unique ages for students living in Hyderabad.

```sql
SELECT DISTINCT Age
FROM Students
WHERE City = 'Hyderabad';
```

### Output

| Age |
| --- |
| 22 |

---

## DISTINCT and NULL Values

Consider the following records:

```sql
INSERT INTO Students
VALUES
(7, 'Rahul', 'Chennai', NULL),
(8, 'Kiran', 'Mumbai', NULL);
```

Retrieve unique ages:

```sql
SELECT DISTINCT Age
FROM Students;
```

### Output

| Age |
| --- |
| 21 |
| 22 |
| 23 |
| NULL |

### Explanation

- DISTINCT treats all NULL values as the same.
- Multiple NULL values appear only once.

---

## DISTINCT vs GROUP BY

Both DISTINCT and GROUP BY can return unique values, but their purposes differ.

### Using DISTINCT

```sql
SELECT DISTINCT City
FROM Students;
```

### Using GROUP BY

```sql
SELECT City
FROM Students
GROUP BY City;
```

### Comparison

| Feature | DISTINCT | GROUP BY |
| --- | --- | --- |
| Removes duplicates | Yes | Yes |
| Supports aggregate functions | No | Yes |
| Simpler syntax | Yes | No |
| Used for grouping calculations | No | Yes |

---

## Common Use Cases

### Find Unique Departments

```sql
SELECT DISTINCT Department
FROM Employees;
```

### Find Unique Countries

```sql
SELECT DISTINCT Country
FROM Customers;
```

### Count Unique Customers

```sql
SELECT COUNT(DISTINCT CustomerID)
FROM Orders;
```

### Find Unique Product Categories

```sql
SELECT DISTINCT Category
FROM Products;
```

---

## Best Practices

- Use DISTINCT only when necessary.
- Avoid using DISTINCT to hide poor table design.
- Create proper keys and constraints to prevent duplicate data.
- Combine DISTINCT with WHERE for better performance.
- Use COUNT(DISTINCT column) when counting unique values.

---

## Important Points

- DISTINCT removes duplicate rows from query results.
- It can be applied to one or multiple columns.
- Multiple columns return unique combinations.
- NULL values appear only once in DISTINCT results.
- DISTINCT operates on the final result set after filtering.

---

## Conclusion

The SQL `DISTINCT` clause is a simple and effective way to eliminate duplicate values from query results. It helps produce cleaner reports, perform accurate analysis, and retrieve unique records from a database. When combined with clauses such as WHERE, ORDER BY, and COUNT(), DISTINCT becomes a powerful tool for data retrieval and reporting.



###
