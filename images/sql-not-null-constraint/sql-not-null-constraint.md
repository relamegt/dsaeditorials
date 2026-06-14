# SQL NOT NULL Constraint

## Introduction

The SQL `NOT NULL` constraint ensures that a column cannot store NULL values. It is used to enforce mandatory fields and guarantees that every record contains a valid value for the specified column.

Unlike a PRIMARY KEY, which enforces both uniqueness and non-nullability, the NOT NULL constraint only ensures that data is present.

## Why Use NOT NULL?

The `NOT NULL` constraint helps you:

- Enforce mandatory fields.
- Prevent missing or incomplete data.
- Improve data integrity.
- Ensure important columns always contain values.
- Reduce data validation issues.

## Syntax

### During Table Creation

```sql
CREATE TABLE table_name (
    column_name data_type NOT NULL
);
```

### Adding NOT NULL to an Existing Column

```sql
ALTER TABLE table_name
MODIFY column_name data_type NOT NULL;
```

### Syntax Components

| Component | Description |
| --- | --- |
| NOT NULL | Prevents a column from storing NULL values |
| CREATE TABLE | Applies the constraint during table creation |
| ALTER TABLE | Adds the constraint to an existing table |
| MODIFY | Modifies an existing column definition |

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
    StudentID INT NOT NULL,
    StudentName VARCHAR(100),
    City VARCHAR(50)
);
```

## Inserting Valid Records

```sql
INSERT INTO Students (StudentID, StudentName, City)
VALUES
(101, 'Akash', 'Vijayawada'),
(102, 'Mohit', 'Hyderabad'),
(103, 'Abhiram', 'Guntur');
```

Display all records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | City |
| --- | --- | --- |
| 101 | Akash | Vijayawada |
| 102 | Mohit | Hyderabad |
| 103 | Abhiram | Guntur |

### Explanation

- StudentID is defined as NOT NULL.
- All inserted rows contain valid StudentID values.
- Therefore, the records are inserted successfully.

---

## Example 1: Inserting NULL into a NOT NULL Column

```sql
INSERT INTO Students (StudentID, StudentName, City)
VALUES
(NULL, 'Sai', 'Vijayawada');
```

### Error

```text
ERROR: Column 'StudentID' cannot be NULL
```

### Explanation

- StudentID is defined as NOT NULL.
- SQL rejects the insertion because NULL values are not allowed.
- The record is not inserted into the table.

---

## Example 2: Applying NOT NULL During Table Creation

```sql
CREATE TABLE Employees (
    EmployeeID INT NOT NULL,
    EmployeeName VARCHAR(100) NOT NULL,
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

### Explanation

- EmployeeID must always contain a value.
- EmployeeName must always contain a value.
- Department and Salary can contain NULL values because they do not have the NOT NULL constraint.

---

## Example 3: Multiple NOT NULL Columns

```sql
CREATE TABLE Customers (
    CustomerID INT NOT NULL,
    CustomerName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) NOT NULL,
    Phone VARCHAR(20)
);
```

### Explanation

- CustomerID, CustomerName, and Email are mandatory fields.
- Phone is optional because it does not use NOT NULL.

---

## Example 4: Adding NOT NULL to an Existing Column

Assume the following table already exists:

```sql
CREATE TABLE Courses (
    CourseID INT,
    CourseName VARCHAR(100)
);
```

Add the NOT NULL constraint:

```sql
ALTER TABLE Courses
MODIFY CourseID INT NOT NULL;
```

### Explanation

- CourseID can no longer store NULL values.
- Future INSERT and UPDATE operations must provide a value for CourseID.

---

## Example 5: NOT NULL with PRIMARY KEY

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100) NOT NULL
);
```

### Explanation

- PRIMARY KEY automatically includes NOT NULL.
- DepartmentID cannot contain NULL values.
- DepartmentName is explicitly marked as NOT NULL.

---

## Example 6: NOT NULL with UPDATE

Consider the following query:

```sql
UPDATE Students
SET StudentID = NULL
WHERE StudentID = 101;
```

### Error

```text
ERROR: Column 'StudentID' cannot be NULL
```

### Explanation

- NOT NULL applies to both INSERT and UPDATE operations.
- SQL prevents updating the column to NULL.

---

## NOT NULL vs NULL

| Feature | NOT NULL | NULL |
| --- | --- | --- |
| Allows Missing Values | No | Yes |
| Mandatory Data Entry | Yes | No |
| Improves Data Integrity | Yes | No |
| Used for Required Fields | Yes | No |

---

## Common Use Cases

### Mandatory Employee ID

```sql
CREATE TABLE Employees (
    EmployeeID INT NOT NULL
);
```

### Mandatory Email Address

```sql
CREATE TABLE Users (
    Email VARCHAR(100) NOT NULL
);
```

### Mandatory Product Name

```sql
CREATE TABLE Products (
    ProductName VARCHAR(100) NOT NULL
);
```

### Mandatory Order Date

```sql
CREATE TABLE Orders (
    OrderDate DATE NOT NULL
);
```

---

## Best Practices

- Use NOT NULL for all mandatory fields.
- Apply NOT NULL to identifiers and key business attributes.
- Avoid allowing NULL values in critical columns.
- Combine NOT NULL with PRIMARY KEY and UNIQUE constraints where appropriate.
- Design tables carefully before applying constraints.

---

## Important Points

- NOT NULL prevents a column from storing NULL values.
- It ensures that data is always present.
- The constraint can be added during table creation or later using ALTER TABLE.
- NOT NULL does not enforce uniqueness.
- PRIMARY KEY columns are automatically NOT NULL.
- The constraint applies to both INSERT and UPDATE operations.

---

## Conclusion

The SQL `NOT NULL` constraint is one of the most fundamental data integrity constraints. It ensures that important columns always contain valid values and prevents incomplete records from being stored in the database. Proper use of NOT NULL helps create reliable, consistent, and high-quality databases.



###
