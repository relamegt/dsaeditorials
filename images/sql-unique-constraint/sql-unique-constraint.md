# SQL UNIQUE Constraint

## Introduction

The SQL `UNIQUE` constraint ensures that all values in a column or a group of columns are distinct. It prevents duplicate values from being stored while allowing NULL values (depending on the DBMS).

The UNIQUE constraint is commonly used to maintain data accuracy and ensure that specific fields such as email addresses, usernames, phone numbers, or registration numbers remain unique.

## Why Use a UNIQUE Constraint?

The `UNIQUE` constraint helps you:

- Prevent duplicate values in a column.
- Maintain data accuracy and consistency.
- Enforce business rules.
- Ensure uniqueness without making a column a PRIMARY KEY.
- Create reliable identifiers such as emails and usernames.

## Key Characteristics of UNIQUE Constraint

- Prevents duplicate values.
- Can be applied to one or multiple columns.
- Multiple UNIQUE constraints can exist in a table.
- NULL values are generally allowed (DBMS dependent).
- May automatically create an index.

## Syntax

### Creating a UNIQUE Constraint During Table Creation

```sql
CREATE TABLE table_name (
    column_name datatype UNIQUE
);
```

### Creating a Composite UNIQUE Constraint

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    UNIQUE (column1, column2)
);
```

### Adding a UNIQUE Constraint to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
UNIQUE (column_name);
```

### Syntax Components

| Component | Description |
| --- | --- |
| UNIQUE | Prevents duplicate values |
| column_name | Column that must contain unique values |
| CONSTRAINT | Optional name assigned to the constraint |
| ALTER TABLE | Adds the constraint to an existing table |
| UNIQUE(column1,column2) | Creates a multi-column unique constraint |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Table with UNIQUE Constraint

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    City VARCHAR(50)
);
```

## Inserting Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 'akash@gmail.com', 'Vijayawada'),
(102, 'Mohit', 'mohit@gmail.com', 'Hyderabad'),
(103, 'Abhiram', 'abhiram@gmail.com', 'Guntur');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | City |
| --- | --- | --- | --- |
| 101 | Akash | [akash@gmail.com](mailto:akash@gmail.com) | Vijayawada |
| 102 | Mohit | [mohit@gmail.com](mailto:mohit@gmail.com) | Hyderabad |
| 103 | Abhiram | [abhiram@gmail.com](mailto:abhiram@gmail.com) | Guntur |

### Explanation

- Email is defined as UNIQUE.
- Every email value must be different.
- No duplicate email addresses are allowed.

---

## Example 1: Duplicate UNIQUE Value

```sql
INSERT INTO Students
VALUES
(104, 'Hemesh', 'akash@gmail.com', 'Vijayawada');
```

### Error

```text
UNIQUE constraint violation:
Duplicate value detected.
```

### Explanation

- The email  [akash@gmail.com](mailto:akash@gmail.com)  already exists.
- UNIQUE columns cannot contain duplicate values.
- SQL rejects the insertion.

---

## Example 2: UNIQUE Column with NULL Values

```sql
INSERT INTO Students
VALUES
(104, 'Hemesh', NULL, 'Vijayawada'),
(105, 'Akhil', NULL, 'Hyderabad');
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | City |
| --- | --- | --- | --- |
| 104 | Hemesh | NULL | Vijayawada |
| 105 | Akhil | NULL | Hyderabad |

### Explanation

- Most DBMSs allow multiple NULL values in UNIQUE columns.
- NULL is treated as an unknown value rather than a duplicate value.

---

## Example 3: UNIQUE Constraint on Multiple Columns

Create a table:

```sql
CREATE TABLE CourseEnrollments (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    UNIQUE (StudentID, CourseID)
);
```

Insert records:

```sql
INSERT INTO CourseEnrollments
VALUES
(101, 1, '2026-01-10'),
(101, 2, '2026-01-15'),
(102, 1, '2026-01-20');
```

Display records:

```sql
SELECT * FROM CourseEnrollments;
```

### Output

| StudentID | CourseID | EnrollmentDate |
| --- | --- | --- |
| 101 | 1 | 2026-01-10 |
| 101 | 2 | 2026-01-15 |
| 102 | 1 | 2026-01-20 |

### Explanation

- StudentID values can repeat.
- CourseID values can repeat.
- The combination of StudentID and CourseID must remain unique.

---

## Example 4: Violating a Multi-Column UNIQUE Constraint

```sql
INSERT INTO CourseEnrollments
VALUES
(101, 1, '2026-02-01');
```

### Error

```text
UNIQUE constraint violation:
Duplicate combination detected.
```

### Explanation

- The combination (101, 1) already exists.
- The UNIQUE constraint prevents duplicate combinations.

---

## Example 5: Adding a UNIQUE Constraint to an Existing Table

Create a table:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    PhoneNumber VARCHAR(15)
);
```

Add a UNIQUE constraint:

```sql
ALTER TABLE Employees
ADD CONSTRAINT UQ_Phone
UNIQUE (PhoneNumber);
```

### Explanation

- PhoneNumber must now contain unique values.
- Duplicate phone numbers will not be allowed.

---

## Rules for UNIQUE Constraint

- Duplicate values are not allowed.
- Multiple UNIQUE constraints can exist in a table.
- UNIQUE can be applied to one or more columns.
- NULL values are generally allowed.
- UNIQUE helps maintain data consistency.
- UNIQUE may create an index automatically.

---

## UNIQUE vs PRIMARY KEY

| Feature | UNIQUE | PRIMARY KEY |
| --- | --- | --- |
| Allows Duplicate Values | No | No |
| Allows NULL Values | Yes (DBMS dependent) | No |
| Number Allowed Per Table | Multiple | One |
| Uniquely Identifies Records | No | Yes |
| Automatically Indexed | Usually | Yes |

---

## Common Use Cases

### Email Addresses

```sql
Email VARCHAR(100) UNIQUE
```

### Usernames

```sql
Username VARCHAR(50) UNIQUE
```

### Mobile Numbers

```sql
PhoneNumber VARCHAR(15) UNIQUE
```

### Registration Numbers

```sql
RegistrationNo VARCHAR(20) UNIQUE
```

### Multi-Column Uniqueness

```sql
UNIQUE (StudentID, CourseID)
```

---

## Best Practices

- Use UNIQUE for fields that should not repeat.
- Use PRIMARY KEY for record identification.
- Keep UNIQUE columns meaningful and stable.
- Avoid unnecessary UNIQUE constraints.
- Use multi-column UNIQUE constraints when business rules require unique combinations.

---

## Important Points

- UNIQUE prevents duplicate values.
- Multiple UNIQUE constraints can exist in a table.
- UNIQUE can be applied to one or multiple columns.
- Most DBMSs allow multiple NULL values.
- UNIQUE helps maintain data quality and consistency.
- UNIQUE is often used for emails, usernames, and phone numbers.

---

## Conclusion

The SQL `UNIQUE` constraint is an essential database feature used to prevent duplicate values and maintain data accuracy. It can be applied to individual columns or combinations of columns, making it flexible for enforcing business rules. By ensuring uniqueness while still allowing NULL values in most database systems, the UNIQUE constraint plays a vital role in maintaining reliable and consistent data.



###
