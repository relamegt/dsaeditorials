# SQL Statistical Functions

## Introduction

SQL Statistical Functions are built-in functions that help analyze numeric data by performing calculations such as averages, totals, counts, variances, and standard deviations. These functions are widely used in reporting, business intelligence, financial analysis, and data analytics.

Statistical functions allow users to summarize large datasets and extract meaningful insights directly from a database.

## Why Use Statistical Functions?

SQL Statistical Functions help you:

- Calculate averages and totals quickly.
- Count records efficiently.
- Find minimum and maximum values.
- Measure data spread and variability.
- Analyze relationships between datasets.
- Generate business reports and dashboards.

---

## Common Statistical Functions in SQL

| Function | Description |
| --- | --- |
| AVG() | Calculates the average value |
| SUM() | Calculates the total sum |
| COUNT() | Counts rows or values |
| MIN() | Returns the minimum value |
| MAX() | Returns the maximum value |
| VARIANCE() | Calculates variance |
| STDDEV() | Calculates standard deviation |
| PERCENTILE_CONT() | Calculates percentile values |
| CORR() | Calculates correlation coefficient |
| COVAR_POP() | Calculates population covariance |

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
CREATE TABLE StudentDetails (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Marks DECIMAL(5,2)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO StudentDetails
VALUES
(1, 'Akash', 85),
(2, 'Mohit', 92),
(3, 'Abhiram', 78),
(4, 'Hemesh', 88),
(5, 'Hemanth', 95),
(6, 'Akhil', 81);
```

Display all records:

```sql
SELECT * FROM StudentDetails;
```

### Output

| StudentID | StudentName | Marks |
| --- | --- | --- |
| 1 | Akash | 85 |
| 2 | Mohit | 92 |
| 3 | Abhiram | 78 |
| 4 | Hemesh | 88 |
| 5 | Hemanth | 95 |
| 6 | Akhil | 81 |

---

## Example 1: AVG() Function

Calculate the average marks of all students.

```sql
SELECT AVG(Marks) AS AverageMarks
FROM StudentDetails;
```

### Output

| AverageMarks |
| --- |
| 86.50 |

### Explanation

- AVG() calculates the arithmetic mean.
- It adds all marks and divides by the total number of records.

---

## Example 2: SUM() Function

Calculate the total marks scored by all students.

```sql
SELECT SUM(Marks) AS TotalMarks
FROM StudentDetails;
```

### Output

| TotalMarks |
| --- |
| 519 |

### Explanation

- SUM() returns the total of all numeric values.
- Useful for financial and reporting calculations.

---

## Example 3: COUNT() Function

Count the total number of students.

```sql
SELECT COUNT(*) AS TotalStudents
FROM StudentDetails;
```

### Output

| TotalStudents |
| --- |
| 6 |

### Explanation

- COUNT(*) counts all rows in the table.
- Frequently used for summary reports.

---

## Example 4: MAX() Function

Find the highest marks.

```sql
SELECT MAX(Marks) AS HighestMarks
FROM StudentDetails;
```

### Output

| HighestMarks |
| --- |
| 95 |

### Explanation

- MAX() returns the largest value in a column.
- Useful for identifying top performers.

---

## Example 5: MIN() Function

Find the lowest marks.

```sql
SELECT MIN(Marks) AS LowestMarks
FROM StudentDetails;
```

### Output

| LowestMarks |
| --- |
| 78 |

### Explanation

- MIN() returns the smallest value.
- Helps identify minimum values in datasets.

---

## Example 6: VARIANCE() Function

Calculate the variance of student marks.

```sql
SELECT VARIANCE(Marks) AS MarksVariance
FROM StudentDetails;
```

### Output

| MarksVariance |
| --- |
| 35.58 |

### Explanation

- Variance measures how spread out values are from the average.
- Larger variance indicates greater data dispersion.

---

## Example 7: STDDEV() Function

Calculate the standard deviation of marks.

```sql
SELECT STDDEV(Marks) AS MarksStandardDeviation
FROM StudentDetails;
```

### Output

| MarksStandardDeviation |
| --- |
| 5.96 |

### Explanation

- Standard deviation measures the amount of variation in data.
- Lower values indicate more consistent results.

---

## Example 8: AVG() with WHERE Clause

Calculate the average marks of students scoring above 80.

```sql
SELECT AVG(Marks) AS AverageMarks
FROM StudentDetails
WHERE Marks > 80;
```

### Output

| AverageMarks |
| --- |
| 88.20 |

### Explanation

- WHERE filters the records first.
- AVG() calculates the average on the filtered data.

---

## Example 9: COUNT() with Condition

Count students who scored above 85.

```sql
SELECT COUNT(*) AS StudentsAbove85
FROM StudentDetails
WHERE Marks > 85;
```

### Output

| StudentsAbove85 |
| --- |
| 3 |

### Explanation

- Counts only rows satisfying the condition.
- Useful for performance-based analysis.

---

## Example 10: MAX() and MIN() Together

Display the highest and lowest marks in one query.

```sql
SELECT
MAX(Marks) AS HighestMarks,
MIN(Marks) AS LowestMarks
FROM StudentDetails;
```

### Output

| HighestMarks | LowestMarks |
| --- | --- |
| 95 | 78 |

### Explanation

- Multiple aggregate functions can be used together.
- Helps summarize data efficiently.

---

## Creating Another Sample Table

```sql
CREATE TABLE StudentPerformance (
    StudentID INT,
    StudyHours INT,
    Marks INT
);
```

---

## Inserting Sample Records

```sql
INSERT INTO StudentPerformance
VALUES
(1, 5, 70),
(2, 6, 75),
(3, 7, 82),
(4, 8, 88),
(5, 9, 94),
(6, 10, 98);
```

---

## Example 11: PERCENTILE_CONT()

Find the median marks.

```sql
SELECT PERCENTILE_CONT(0.5)
WITHIN GROUP (ORDER BY Marks) AS MedianMarks
FROM StudentDetails;
```

### Output

| MedianMarks |
| --- |
| 86.50 |

### Explanation

- 0.5 represents the 50th percentile.
- Returns the median value of the dataset.

---

## Example 12: CORR() Function

Calculate the correlation between study hours and marks.

```sql
SELECT CORR(StudyHours, Marks) AS CorrelationValue
FROM StudentPerformance;
```

### Output

| CorrelationValue |
| --- |
| 0.98 |

### Explanation

- Measures the relationship between two numeric columns.
- Values close to 1 indicate a strong positive relationship.

---

## Example 13: COVAR_POP() Function

Calculate population covariance.

```sql
SELECT COVAR_POP(StudyHours, Marks) AS PopulationCovariance
FROM StudentPerformance;
```

### Output

| PopulationCovariance |
| --- |
| 15.67 |

### Explanation

- Measures how two variables change together.
- Positive values indicate both variables tend to increase together.

---

## Common Use Cases

### Calculate Average Salary

```sql
SELECT AVG(Salary)
FROM Employees;
```

### Count Customers

```sql
SELECT COUNT(*)
FROM Customers;
```

### Find Maximum Revenue

```sql
SELECT MAX(Revenue)
FROM Sales;
```

### Find Minimum Product Price

```sql
SELECT MIN(Price)
FROM Products;
```

---

## Best Practices

- Use aggregate functions with WHERE clauses whenever possible.
- Handle NULL values carefully.
- Use aliases for better readability.
- Combine statistical functions for comprehensive reporting.
- Validate data before performing advanced calculations.

---

## Important Points

- AVG() calculates average values.
- SUM() calculates totals.
- COUNT() counts rows or values.
- MIN() returns the smallest value.
- MAX() returns the largest value.
- VARIANCE() measures data spread.
- STDDEV() measures deviation from the average.
- PERCENTILE_CONT() calculates percentile values.
- CORR() measures correlation between columns.
- COVAR_POP() calculates covariance.

---

## Conclusion

SQL Statistical Functions provide powerful tools for analyzing and summarizing data directly within a database. Functions such as AVG(), SUM(), COUNT(), MIN(), MAX(), VARIANCE(), and STDDEV() help generate valuable insights, while advanced functions like CORR() and COVAR_POP() enable deeper analytical reporting. Mastering these functions is essential for effective data analysis and decision-making in SQL.



###
