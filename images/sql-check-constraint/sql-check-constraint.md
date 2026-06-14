# SQL CHECK Constraint

## Introduction

The SQL `CHECK` constraint is used to enforce specific conditions on column values. It ensures that only valid data satisfying a defined rule can be inserted or updated in a table.

If a value violates the CHECK condition, the database rejects the operation and maintains data integrity.

## Why Use a CHECK Constraint?

The `CHECK` constraint helps you:

- Enforce business rules at the database level.
- Prevent invalid data from being stored.
- Improve data consistency and accuracy.
- Restrict values to a valid range.
- Validate data during INSERT and UPDATE operations.

## Key Characteristics of CHECK Constraint

- Validates data against a specified condition.
- Can be applied to a single column or multiple columns.
- Works during INSERT and UPDATE operations.
- Can be defined while creating a table.
- Can be added later using ALTER TABLE.
- Helps maintain data integrity.

## Syntax

### Creating a CHECK Constraint During Table Creation

```sql
CREATE TABLE table_name (
    column_name datatype CHECK (condition)
);
```

### Creating a Table-Level CHECK Constraint

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    CHECK (condition)
);
```

### Adding a CHECK Constraint to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
CHECK (condition);
```

### Syntax Components

| Component | Description |
| --- | --- |
| CHECK | Defines a validation rule |
| condition | Expression that must evaluate to TRUE |
| CONSTRAINT | Optional name for the CHECK constraint |
| ALTER TABLE | Adds a CHECK constraint to an existing table |
| Table-Level CHECK | Validates multiple columns together |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Table with CHECK Constraint

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Age INT CHECK (Age >= 18),
    City VARCHAR(50)
);
```

### Explanation

- StudentID uniquely identifies each student.
- Age must be 18 or greater.
- Any value below 18 will be rejected.

---

## Inserting Valid Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 21, 'Vijayawada'),
(102, 'Mohit', 22, 'Hyderabad'),
(103, 'Abhiram', 20, 'Guntur');
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Age | City |
| --- | --- | --- | --- |
| 101 | Akash | 21 | Vijayawada |
| 102 | Mohit | 22 | Hyderabad |
| 103 | Abhiram | 20 | Guntur |

### Explanation

- All age values satisfy the CHECK condition.
- The records are inserted successfully.

---

## Example 1: Violating a CHECK Constraint

```sql
INSERT INTO Students
VALUES
(104, 'Hemesh', 16, 'Guntur');
```

### Error

```text
CHECK constraint violation:
Age must be greater than or equal to 18.
```

### Explanation

- Age 16 does not satisfy the condition.
- SQL rejects the insertion.

---

## Example 2: CHECK Constraint on Salary

Create a table:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Salary DECIMAL(10,2)
    CHECK (Salary > 0)
);
```

Insert records:

```sql
INSERT INTO Employees
VALUES
(101, 'Akash', 50000),
(102, 'Mohit', 45000);
```

### Explanation

- Salary must be greater than zero.
- Positive salary values are accepted.

---

## Example 3: Invalid Salary Value

```sql
INSERT INTO Employees
VALUES
(103, 'Abhiram', -1000);
```

### Error

```text
CHECK constraint violation:
Salary must be greater than zero.
```

### Explanation

- Negative salary values are not allowed.
- SQL rejects the record.

---

## Example 4: CHECK Constraint with Multiple Columns

```sql
CREATE TABLE EmployeeDetails (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Age INT,
    Salary DECIMAL(10,2),
    CHECK (Age >= 18 AND Salary > 0)
);
```

Insert records:

```sql
INSERT INTO EmployeeDetails
VALUES
(101, 'Akash', 25, 55000),
(102, 'Mohit', 27, 48000);
```

Display records:

```sql
SELECT * FROM EmployeeDetails;
```

### Output

| EmployeeID | EmployeeName | Age | Salary |
| --- | --- | --- | --- |
| 101 | Akash | 25 | 55000 |
| 102 | Mohit | 27 | 48000 |

### Explanation

- Age must be at least 18.
- Salary must be greater than zero.
- Both conditions must be satisfied.

---

## Example 5: Violating a Multi-Column CHECK Constraint

```sql
INSERT INTO EmployeeDetails
VALUES
(103, 'Hemesh', 17, 45000);
```

### Error

```text
CHECK constraint violation:
Age must be greater than or equal to 18.
```

### Explanation

- Age 17 violates the CHECK condition.
- The row is rejected.

---

## Example 6: Adding a CHECK Constraint Using ALTER TABLE

Create a table:

```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2)
);
```

Add a CHECK constraint:

```sql
ALTER TABLE Products
ADD CONSTRAINT CHK_Price
CHECK (Price >= 100);
```

### Explanation

- Product prices must be at least 100.
- Values below 100 will be rejected.

---

## Example 7: Restricting Marks Range

```sql
CREATE TABLE StudentMarks (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Marks INT CHECK (Marks BETWEEN 0 AND 100)
);
```

Insert records:

```sql
INSERT INTO StudentMarks
VALUES
(101, 'Akash', 85),
(102, 'Mohit', 92),
(103, 'Abhiram', 78);
```

### Explanation

- Marks must be between 0 and 100.
- Values outside this range are not accepted.

---

## Rules for CHECK Constraint

- The condition must evaluate to TRUE.
- Invalid values are rejected.
- Can validate one or multiple columns.
- Works with INSERT and UPDATE statements.
- Multiple CHECK constraints can exist in a table.
- Helps enforce business rules.

---

## CHECK Constraint vs NOT NULL

| Feature | CHECK | NOT NULL |
| --- | --- | --- |
| Validates Conditions | Yes | No |
| Prevents NULL Values | Can be combined | Yes |
| Supports Complex Rules | Yes | No |
| Works on Multiple Columns | Yes | No |
| Enforces Business Logic | Yes | No |

---

## Common Use Cases

### Minimum Age Requirement

```sql
CHECK (Age >= 18)
```

### Positive Salary

```sql
CHECK (Salary > 0)
```

### Product Price Validation

```sql
CHECK (Price >= 100)
```

### Marks Validation

```sql
CHECK (Marks BETWEEN 0 AND 100)
```

### Valid Quantity

```sql
CHECK (Quantity > 0)
```

---

## Best Practices

- Use CHECK constraints for business rules.
- Keep validation rules simple and meaningful.
- Combine CHECK with NOT NULL when required.
- Validate important numeric ranges.
- Use descriptive constraint names.

---

## Important Points

- CHECK validates data before insertion or update.
- Invalid values are rejected automatically.
- It can be applied to one or multiple columns.
- CHECK constraints improve data quality.
- Multiple CHECK constraints can exist in a table.
- CHECK is commonly used for age, salary, marks, quantity, and price validation.

---

## Conclusion

The SQL `CHECK` constraint is a powerful validation mechanism that ensures only valid data enters a database table. By enforcing custom rules and business requirements, it improves data quality, consistency, and integrity. Whether validating age, salary, marks, price, or multiple columns together, the CHECK constraint plays an important role in maintaining reliable and accurate database systems.



###
