# Conversion Function in SQL

## Introduction

SQL Conversion Functions are used to convert data from one data type to another. These functions help ensure compatibility between different data types and enable accurate data processing, comparison, formatting, and reporting.

Conversion functions are commonly used when working with dates, numbers, and character strings. They provide better control over data representation and query results.

---

## Why Use Conversion Functions?

Conversion functions help you:

- Convert data between different data types.
- Format dates and numbers for display.
- Ensure compatibility during comparisons.
- Improve readability of query results.
- Handle user input effectively.
- Avoid data type mismatch errors.

---

## Types of Data Type Conversion

SQL supports two types of data type conversion:

### 1. Implicit Data Type Conversion

Implicit conversion occurs automatically when SQL converts one data type into another during query execution.

Examples:

| From | To |
| --- | --- |
| CHAR / VARCHAR | NUMBER |
| CHAR / VARCHAR | DATE |
| DATE | VARCHAR |
| NUMBER | VARCHAR |

### 2. Explicit Data Type Conversion

Explicit conversion is performed manually using SQL conversion functions when precise control is required.

Common conversion functions include:

| Function | Purpose |
| --- | --- |
| TO_CHAR() | Converts numbers or dates to text |
| TO_NUMBER() | Converts text to a numeric value |
| TO_DATE() | Converts text to a date value |

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
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2),
    HireDate DATE
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Employees
VALUES
(1, 'Akash', 25000.50, '2023-05-10'),
(2, 'Abhiram', 18000.75, '2022-11-15'),
(3, 'Hemesh', 32000.00, '2021-03-20'),
(4, 'Sai', 15000.25, '2024-01-08');
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Salary | HireDate |
| --- | --- | --- | --- |
| 1 | Akash | 25000.50 | 2023-05-10 |
| 2 | Abhiram | 18000.75 | 2022-11-15 |
| 3 | Hemesh | 32000.00 | 2021-03-20 |
| 4 | Sai | 15000.25 | 2024-01-08 |

---

# Implicit Data Type Conversion

Implicit conversion happens automatically without requiring conversion functions.

---

## Example 1: Numeric Comparison

```sql
SELECT EmployeeID,
       EmployeeName,
       Salary
FROM Employees
WHERE Salary > 20000;
```

### Output

| EmployeeID | EmployeeName | Salary |
| --- | --- | --- |
| 1 | Akash | 25000.50 |
| 3 | Hemesh | 32000.00 |

### Explanation

- Salary is compared directly as a numeric value.
- SQL automatically handles the comparison.

---

## Example 2: String Converted to Number Automatically

```sql
SELECT EmployeeID,
       EmployeeName,
       Salary
FROM Employees
WHERE Salary > '20000';
```

### Output

| EmployeeID | EmployeeName | Salary |
| --- | --- | --- |
| 1 | Akash | 25000.50 |
| 3 | Hemesh | 32000.00 |

### Explanation

- The value `'20000'` is supplied as text.
- SQL automatically converts it into a number.
- This process is known as implicit conversion.

---

# Explicit Data Type Conversion

Explicit conversion is performed using conversion functions.

---

## TO_CHAR() Function

The TO_CHAR() function converts dates or numbers into character strings.

### Syntax

```sql
TO_CHAR(expression, 'format_model')
```

---

## Example 3: Convert Date to Text

```sql
SELECT EmployeeName,
       TO_CHAR(HireDate, 'DD-MM-YYYY') AS FormattedDate
FROM Employees;
```

### Output

| EmployeeName | FormattedDate |
| --- | --- |
| Akash | 10-05-2023 |
| Abhiram | 15-11-2022 |
| Hemesh | 20-03-2021 |
| Sai | 08-01-2024 |

### Explanation

- Converts DATE values into text.
- Controls the display format.
- Useful in reports and dashboards.

---

## Common Date Format Elements

| Format | Description |
| --- | --- |
| YYYY | Four-digit year |
| YY | Two-digit year |
| MM | Month number |
| MONTH | Full month name |
| MON | Month abbreviation |
| DD | Day of month |
| DAY | Full day name |
| DY | Day abbreviation |

---

## Common Time Format Elements

| Format | Description |
| --- | --- |
| HH | Hour |
| HH24 | 24-hour format |
| MI | Minutes |
| SS | Seconds |
| AM / PM | Meridian indicator |

---

## Example 4: Convert Number to Text

```sql
SELECT EmployeeName,
       TO_CHAR(Salary, '$99,999.99') AS FormattedSalary
FROM Employees;
```

### Output

| EmployeeName | FormattedSalary |
| --- | --- |
| Akash | $25,000.50 |
| Abhiram | $18,000.75 |
| Hemesh | $32,000.00 |
| Sai | $15,000.25 |

### Explanation

- Converts numeric data into formatted text.
- Currency symbols and commas can be added.
- Useful for financial reports.

---

## Number Format Elements

| Format | Description |
| --- | --- |
| 9 | Displays a digit |
| 0 | Displays zero if needed |
| $ | Currency symbol |
| L | Local currency symbol |
| . | Decimal point |
| , | Thousand separator |

---

## TO_NUMBER() Function

The TO_NUMBER() function converts character data into numeric values.

### Syntax

```sql
TO_NUMBER(character_value, 'format_model')
```

---

## Example 5: Convert Text to Number

```sql
SELECT TO_NUMBER('15000') AS ConvertedNumber;
```

### Output

| ConvertedNumber |
| --- |
| 15000 |

### Explanation

- Converts text into a numeric value.
- Useful when numeric calculations are required.

---

## TO_DATE() Function

The TO_DATE() function converts character data into date values.

### Syntax

```sql
TO_DATE(character_value, 'format_model')
```

---

## Example 6: Convert Text to Date

```sql
SELECT TO_DATE(
'15 June 2024',
'DD Month YYYY'
) AS ConvertedDate;
```

### Output

| ConvertedDate |
| --- |
| 2024-06-15 |

### Explanation

- Converts a text string into a DATE value.
- Format model specifies how SQL interprets the text.

---

## Example 7: Using TO_DATE() in a Query

```sql
SELECT EmployeeName,
       HireDate
FROM Employees
WHERE HireDate =
      TO_DATE(
      '10 May 2023',
      'DD Month YYYY'
      );
```

### Output

| EmployeeName | HireDate |
| --- | --- |
| Akash | 2023-05-10 |

### Explanation

- Converts the supplied text into a date.
- Enables accurate date comparisons.

---

## Common Use Cases

### Convert Salary for Reporting

```sql
SELECT TO_CHAR(Salary, '$99,999.99')
FROM Employees;
```

### Convert User Input to Date

```sql
SELECT TO_DATE(
'01-01-2025',
'DD-MM-YYYY'
);
```

### Convert Text Number to Integer

```sql
SELECT TO_NUMBER('500');
```

---

## Best Practices

- Use explicit conversion when precision is required.
- Avoid relying heavily on implicit conversion.
- Validate date formats before conversion.
- Use appropriate format models.
- Keep data stored in proper native data types.
- Use TO_CHAR() mainly for display purposes.

---

## Important Points

- SQL supports both implicit and explicit conversion.
- Implicit conversion is performed automatically.
- Explicit conversion uses functions like TO_CHAR(), TO_NUMBER(), and TO_DATE().
- TO_CHAR() converts numbers and dates into text.
- TO_NUMBER() converts text into numeric values.
- TO_DATE() converts text into date values.
- Proper formatting improves readability and accuracy.

---

## Conclusion

SQL Conversion Functions provide a reliable way to transform data between different formats such as text, numbers, and dates. Functions like TO_CHAR(), TO_NUMBER(), and TO_DATE() allow precise control over how data is displayed, compared, and processed. Understanding both implicit and explicit conversion techniques helps create accurate, efficient, and user-friendly SQL queries.



###
