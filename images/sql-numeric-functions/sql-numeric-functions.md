# SQL Numeric Functions

## Introduction

SQL Numeric Functions are built-in functions used to perform mathematical calculations and operations on numeric data. These functions simplify calculations involving integers, decimals, percentages, powers, logarithms, and random number generation.

Numeric functions are widely used in financial applications, reporting systems, analytics dashboards, and scientific calculations.

### Why Use Numeric Functions?

SQL Numeric Functions help you:

- Perform mathematical calculations directly in SQL.
- Round and format numeric values.
- Calculate percentages and growth rates.
- Generate random numbers.
- Analyze business and financial data.
- Simplify complex mathematical operations.

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
CREATE TABLE StudentScores (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Marks DECIMAL(8,2)
);
```

---

## Inserting Sample Records

```sql
INSERT INTO StudentScores
VALUES
(1, 'Akash', 85.75),
(2, 'Mohit', 92.45),
(3, 'Abhiram', 78.90),
(4, 'Hemesh', 88.25),
(5, 'Hemanth', 95.80),
(6, 'Akhil', 81.35);
```

Display all records:

```sql
SELECT * FROM StudentScores;
```

### Output

| StudentID | StudentName | Marks |
| --- | --- | --- |
| 1 | Akash | 85.75 |
| 2 | Mohit | 92.45 |
| 3 | Abhiram | 78.90 |
| 4 | Hemesh | 88.25 |
| 5 | Hemanth | 95.80 |
| 6 | Akhil | 81.35 |

---

## Example 1: ABS() – Absolute Value

Returns the positive value of a number.

```sql
SELECT ABS(-250) AS AbsoluteValue;
```

### Output

| AbsoluteValue |
| --- |
| 250 |

### Explanation

- Converts negative numbers into positive numbers.
- Positive numbers remain unchanged.

---

## Example 2: CEIL() / CEILING()

Rounds a number upward to the nearest integer.

```sql
SELECT CEIL(12.34) AS RoundedValue;
```

### Output

| RoundedValue |
| --- |
| 13 |

### Explanation

- Always rounds upward.
- Decimal values are ignored after rounding.

---

## Example 3: FLOOR()

Rounds a number downward to the nearest integer.

```sql
SELECT FLOOR(12.98) AS RoundedValue;
```

### Output

| RoundedValue |
| --- |
| 12 |

### Explanation

- Always rounds downward.
- Removes the decimal portion.

---

## Example 4: ROUND()

Rounds a number to a specified number of decimal places.

```sql
SELECT ROUND(15.6789, 2) AS RoundedNumber;
```

### Output

| RoundedNumber |
| --- |
| 15.68 |

### Explanation

- Rounds the value to two decimal places.
- Commonly used in financial calculations.

---

## Example 5: TRUNCATE()

Removes decimal places without rounding.

```sql
SELECT TRUNCATE(12.98765, 2) AS TruncatedValue;
```

### Output

| TruncatedValue |
| --- |
| 12.98 |

### Explanation

- Simply removes extra decimal digits.
- Does not perform rounding.

---

## Example 6: MOD()

Returns the remainder after division.

```sql
SELECT MOD(25, 4) AS Remainder;
```

### Output

| Remainder |
| --- |
| 1 |

### Explanation

- Divides 25 by 4.
- Returns the remainder value.

---

## Example 7: POWER()

Raises a number to a specified power.

```sql
SELECT POWER(2, 5) AS Result;
```

### Output

| Result |
| --- |
| 32 |

### Explanation

- Calculates 2⁵.
- Useful in growth and compound interest calculations.

---

## Example 8: SQRT()

Returns the square root of a number.

```sql
SELECT SQRT(144) AS SquareRoot;
```

### Output

| SquareRoot |
| --- |
| 12 |

### Explanation

- Returns the square root of the supplied number.

---

## Example 9: EXP()

Returns e raised to a given power.

```sql
SELECT EXP(1) AS ExponentialValue;
```

### Output

| ExponentialValue |
| --- |
| 2.718281828 |

### Explanation

- Calculates e¹.
- e is approximately 2.71828.

---

## Example 10: LOG()

Returns the natural logarithm of a number.

```sql
SELECT LOG(100) AS LogValue;
```

### Output

| LogValue |
| --- |
| 4.605170 |

### Explanation

- Returns the natural logarithm (base e).
- Commonly used in analytics and statistics.

---

## Example 11: RAND()

Generates a random number.

```sql
SELECT RAND() AS RandomNumber;
```

### Output

| RandomNumber |
| --- |
| 0.472381 |

### Explanation

- Generates a random value between 0 and 1.
- Output changes each execution.

---

## Example 12: ROUND() with Student Marks

Round student marks to the nearest whole number.

```sql
SELECT StudentName,
       ROUND(Marks, 0) AS RoundedMarks
FROM StudentScores;
```

### Output

| StudentName | RoundedMarks |
| --- | --- |
| Akash | 86 |
| Mohit | 92 |
| Abhiram | 79 |
| Hemesh | 88 |
| Hemanth | 96 |
| Akhil | 81 |

### Explanation

- Rounds marks to the nearest integer.
- Useful for reports and summaries.

---

## Example 13: CEIL() with Student Marks

Round marks upward.

```sql
SELECT StudentName,
       CEIL(Marks) AS CeilingMarks
FROM StudentScores;
```

### Output

| StudentName | CeilingMarks |
| --- | --- |
| Akash | 86 |
| Mohit | 93 |
| Abhiram | 79 |
| Hemesh | 89 |
| Hemanth | 96 |
| Akhil | 82 |

### Explanation

- Always rounds marks upward.
- Even small decimals increase the value.

---

## Example 14: FLOOR() with Student Marks

Round marks downward.

```sql
SELECT StudentName,
       FLOOR(Marks) AS FloorMarks
FROM StudentScores;
```

### Output

| StudentName | FloorMarks |
| --- | --- |
| Akash | 85 |
| Mohit | 92 |
| Abhiram | 78 |
| Hemesh | 88 |
| Hemanth | 95 |
| Akhil | 81 |

### Explanation

- Removes the decimal portion.
- Always rounds downward.

---

## Example 15: Calculate Percentage Increase

Calculate marks after adding a 10% bonus.

```sql
SELECT StudentName,
       ROUND(Marks * 1.10, 2) AS BonusMarks
FROM StudentScores;
```

### Output

| StudentName | BonusMarks |
| --- | --- |
| Akash | 94.33 |
| Mohit | 101.70 |
| Abhiram | 86.79 |
| Hemesh | 97.08 |
| Hemanth | 105.38 |
| Akhil | 89.49 |

### Explanation

- Multiplies marks by 1.10.
- Adds a 10% increase.

---

## Common Use Cases

### Calculate Discounted Price

```sql
SELECT ROUND(5000 * 0.90, 2) AS DiscountedPrice;
```

### Find Square Root

```sql
SELECT SQRT(625);
```

### Generate Random Values

```sql
SELECT RAND();
```

### Find Remainder

```sql
SELECT MOD(50, 7);
```

### Calculate Powers

```sql
SELECT POWER(5, 3);
```

---

## Best Practices

- Use ROUND() for financial calculations.
- Use TRUNCATE() when exact decimal removal is required.
- Avoid excessive use of RAND() in large datasets.
- Validate inputs before applying logarithmic functions.
- Use numeric functions inside aggregate reports when needed.

---

## Important Points

- ABS() returns the absolute value.
- CEIL() rounds numbers upward.
- FLOOR() rounds numbers downward.
- ROUND() rounds values to specified decimals.
- TRUNCATE() removes decimal places without rounding.
- MOD() returns the remainder.
- POWER() calculates exponents.
- SQRT() returns square roots.
- EXP() calculates exponential values.
- LOG() calculates logarithms.
- RAND() generates random numbers.

---

## Conclusion

SQL Numeric Functions provide powerful mathematical capabilities directly within SQL queries. They simplify calculations, improve reporting accuracy, and help perform complex numeric operations without requiring external tools. Mastering these functions is essential for database developers, analysts, and anyone working with numerical data in SQL.



###
