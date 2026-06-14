# Date Functions in SQL

## Introduction

SQL Date Functions are built-in functions used to work with date and time values stored in a database. They help retrieve the current date and time, extract specific date components, perform date calculations, and format date values for reporting and analysis.

Date functions are commonly used in applications involving scheduling, sales reporting, attendance tracking, billing systems, and event management.

---

## Why Use Date Functions?

Date functions help you:

- Retrieve the current date and time.
- Extract year, month, day, or time values.
- Calculate date differences.
- Add or subtract date intervals.
- Format dates for reports and dashboards.
- Analyze trends over specific periods.

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
CREATE TABLE StudentRegistrations (
    RegistrationID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    CourseName VARCHAR(100),
    RegistrationDate DATETIME
);
```

---

## Inserting Sample Records

```sql
INSERT INTO StudentRegistrations
VALUES
(101, 'Akash', 'SQL Fundamentals', '2025-01-10 10:15:00'),
(102, 'Mohit', 'Python Programming', '2025-02-15 09:30:00'),
(103, 'Abhiram', 'Java Development', '2025-03-12 11:45:00'),
(104, 'Hemesh', 'Web Development', '2025-04-05 14:20:00'),
(105, 'Hemanth', 'Data Analytics', '2025-05-08 16:10:00'),
(106, 'Akhil', 'Machine Learning', '2025-06-20 13:00:00');
```

Display all records:

```sql
SELECT * FROM StudentRegistrations;
```

### Output

| RegistrationID | StudentName | CourseName | RegistrationDate |
| --- | --- | --- | --- |
| 101 | Akash | SQL Fundamentals | 2025-01-10 10:15:00 |
| 102 | Mohit | Python Programming | 2025-02-15 09:30:00 |
| 103 | Abhiram | Java Development | 2025-03-12 11:45:00 |
| 104 | Hemesh | Web Development | 2025-04-05 14:20:00 |
| 105 | Hemanth | Data Analytics | 2025-05-08 16:10:00 |
| 106 | Akhil | Machine Learning | 2025-06-20 13:00:00 |

---

## Syntax

### Current Date and Time

```sql
SELECT NOW();
```

### Extract Date Components

```sql
SELECT EXTRACT(YEAR FROM date_column);
```

### Add Date Intervals

```sql
SELECT DATE_ADD(date_column, INTERVAL 7 DAY);
```

### Calculate Date Difference

```sql
SELECT DATEDIFF(date1, date2);
```

---

## Example 1: Using NOW()

Retrieve the current system date and time.

### Query

```sql
SELECT NOW() AS CurrentDateTime;
```

### Sample Output

| CurrentDateTime |
| --- |
| 2026-06-14 10:45:30 |

### Explanation

- Returns the current date and time.
- Useful for logging and timestamp generation.
- Includes both date and time values.

---

## Example 2: Using CURDATE()

Retrieve today's date.

### Query

```sql
SELECT CURDATE() AS CurrentDate;
```

### Sample Output

| CurrentDate |
| --- |
| 2026-06-14 |

### Explanation

- Returns only the current date.
- Time information is not included.
- Useful for date-based filtering.

---

## Example 3: Using CURTIME()

Retrieve the current system time.

### Query

```sql
SELECT CURTIME() AS CurrentTime;
```

### Sample Output

| CurrentTime |
| --- |
| 10:45:30 |

### Explanation

- Returns the current time.
- Excludes date information.
- Useful for scheduling operations.

---

## Example 4: Extracting the Date Portion

Retrieve only the date from a datetime value.

### Query

```sql
SELECT
    StudentName,
    DATE(RegistrationDate) AS RegistrationOnlyDate
FROM StudentRegistrations;
```

### Output

| StudentName | RegistrationOnlyDate |
| --- | --- |
| Akash | 2025-01-10 |
| Mohit | 2025-02-15 |
| Abhiram | 2025-03-12 |
| Hemesh | 2025-04-05 |
| Hemanth | 2025-05-08 |
| Akhil | 2025-06-20 |

### Explanation

- Removes the time portion.
- Returns only the date value.
- Useful for reporting and grouping.

---

## Example 5: Using EXTRACT()

Extract the year from the registration date.

### Query

```sql
SELECT
    StudentName,
    EXTRACT(YEAR FROM RegistrationDate) AS RegistrationYear
FROM StudentRegistrations;
```

### Output

| StudentName | RegistrationYear |
| --- | --- |
| Akash | 2025 |
| Mohit | 2025 |
| Abhiram | 2025 |
| Hemesh | 2025 |
| Hemanth | 2025 |
| Akhil | 2025 |

### Explanation

- Extracts the year component.
- Useful for yearly reports.
- Can also extract month, day, hour, etc.

---

## Example 6: Using DATE_ADD()

Add 30 days to the registration date.

### Query

```sql
SELECT
    StudentName,
    DATE_ADD(RegistrationDate, INTERVAL 30 DAY) AS ExtendedDate
FROM StudentRegistrations;
```

### Output

| StudentName | ExtendedDate |
| --- | --- |
| Akash | 2025-02-09 |
| Mohit | 2025-03-17 |
| Abhiram | 2025-04-11 |
| Hemesh | 2025-05-05 |
| Hemanth | 2025-06-07 |
| Akhil | 2025-07-20 |

### Explanation

- Adds 30 days to each registration date.
- Returns future dates.
- Useful for subscription and expiry calculations.

---

## Example 7: Using DATE_SUB()

Subtract 7 days from the registration date.

### Query

```sql
SELECT
    StudentName,
    DATE_SUB(RegistrationDate, INTERVAL 7 DAY) AS PreviousDate
FROM StudentRegistrations;
```

### Output

| StudentName | PreviousDate |
| --- | --- |
| Akash | 2025-01-03 |
| Mohit | 2025-02-08 |
| Abhiram | 2025-03-05 |
| Hemesh | 2025-03-29 |
| Hemanth | 2025-05-01 |
| Akhil | 2025-06-13 |

### Explanation

- Subtracts days from a date.
- Returns earlier dates.
- Useful for historical calculations.

---

## Example 8: Using DATEDIFF()

Calculate the number of days between today and the registration date.

### Query

```sql
SELECT
    StudentName,
    DATEDIFF(CURDATE(), DATE(RegistrationDate)) AS DaysPassed
FROM StudentRegistrations;
```

### Output

| StudentName | DaysPassed |
| --- | --- |
| Akash | 520 |
| Mohit | 484 |
| Abhiram | 459 |
| Hemesh | 435 |
| Hemanth | 402 |
| Akhil | 359 |

### Explanation

- Calculates the difference between two dates.
- Result is returned in days.
- Useful for duration calculations.

---

## Example 9: Using DATE_FORMAT()

Display registration dates in a readable format.

### Query

```sql
SELECT
    StudentName,
    DATE_FORMAT(
        RegistrationDate,
        '%W, %M %d, %Y'
    ) AS FormattedDate
FROM StudentRegistrations;
```

### Output

| StudentName | FormattedDate |
| --- | --- |
| Akash | Friday, January 10, 2025 |
| Mohit | Saturday, February 15, 2025 |
| Abhiram | Wednesday, March 12, 2025 |
| Hemesh | Saturday, April 05, 2025 |
| Hemanth | Thursday, May 08, 2025 |
| Akhil | Friday, June 20, 2025 |

### Explanation

- Converts dates into a readable format.
- Useful for reports and dashboards.
- Supports multiple formatting patterns.

---

## Example 10: Using ADDDATE()

Add 15 days to the registration date.

### Query

```sql
SELECT
    StudentName,
    ADDDATE(RegistrationDate, 15) AS NewDate
FROM StudentRegistrations;
```

### Output

| StudentName | NewDate |
| --- | --- |
| Akash | 2025-01-25 |
| Mohit | 2025-03-02 |
| Abhiram | 2025-03-27 |
| Hemesh | 2025-04-20 |
| Hemanth | 2025-05-23 |
| Akhil | 2025-07-05 |

### Explanation

- Adds a specified number of days.
- Similar to DATE_ADD().
- Useful for deadline calculations.

---

## Example 11: Using ADDTIME()

Add a time interval to a given time.

### Query

```sql
SELECT ADDTIME('10:30:00', '02:15:00') AS UpdatedTime;
```

### Output

| UpdatedTime |
| --- |
| 12:45:00 |

### Explanation

- Adds two time values.
- Returns the resulting time.
- Useful for scheduling calculations.

---

## Common Date Functions

| Function | Purpose |
| --- | --- |
| NOW() | Returns current date and time |
| CURDATE() | Returns current date |
| CURTIME() | Returns current time |
| DATE() | Extracts date portion |
| EXTRACT() | Extracts specific date parts |
| DATE_ADD() | Adds intervals to dates |
| DATE_SUB() | Subtracts intervals from dates |
| DATEDIFF() | Calculates date differences |
| DATE_FORMAT() | Formats date values |
| ADDDATE() | Adds days to dates |
| ADDTIME() | Adds time values |

---

## Best Practices

- Store dates using DATE, DATETIME, or TIMESTAMP data types.
- Use built-in date functions instead of manual calculations.
- Format dates only when displaying results.
- Use indexes on frequently queried date columns.
- Validate date values before inserting records.

---

## Important Points

- Date functions simplify date and time calculations.
- They improve reporting and data analysis.
- Different functions serve different purposes.
- Date arithmetic can be performed using DATE_ADD() and DATE_SUB().
- Formatting functions improve result readability.

---

## Conclusion

SQL Date Functions provide powerful tools for managing and analyzing date and time values. Whether retrieving the current date, calculating differences, extracting components, or formatting output, these functions simplify database operations and make reporting more efficient. Mastering date functions is essential for working with real-world business applications and time-sensitive data.



###
