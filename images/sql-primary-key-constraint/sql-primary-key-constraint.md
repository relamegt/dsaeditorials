# SQL PRIMARY KEY Constraint

## Introduction

The SQL `PRIMARY KEY` constraint uniquely identifies each record in a table. It ensures that every row can be distinguished from all other rows by using one or more columns containing unique, non-NULL values.

A primary key is one of the most important constraints in relational databases because it maintains data integrity and establishes relationships between tables.

## Why Use a PRIMARY KEY?

A PRIMARY KEY helps:

- Uniquely identify each row in a table.
- Prevent duplicate records.
- Prevent NULL values in key columns.
- Improve query performance through indexing.
- Establish relationships with foreign keys.
- Maintain data consistency and integrity.

## Key Characteristics of PRIMARY KEY

- Values must be unique.
- Values cannot be NULL.
- A table can have only one PRIMARY KEY.
- A PRIMARY KEY can consist of one or multiple columns.
- An index is automatically created for the PRIMARY KEY.

---

## Types of Primary Keys

### 1. Simple Primary Key

A primary key that consists of a single column.

Example:

```sql
EmployeeID INT PRIMARY KEY
```

### 2. Composite Primary Key

A primary key that consists of multiple columns.

Example:

```sql
PRIMARY KEY (StudentID, CourseID)
```

A combination of values from both columns must be unique.

---

## Syntax

### Creating a PRIMARY KEY During Table Creation

```sql
CREATE TABLE table_name (
    column_name data_type PRIMARY KEY
);
```

### Creating a Composite PRIMARY KEY

```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    PRIMARY KEY (column1, column2)
);
```

### Adding a PRIMARY KEY to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
PRIMARY KEY (column_name);
```

---

# Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

# Creating a Table with PRIMARY KEY

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

---

# Inserting Records

```sql
INSERT INTO Employees
VALUES
(101, 'Akash', 'Management', 85000),
(102, 'Mohit', 'Content', 55000),
(103, 'Abhiram', 'Technical', 72000);
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department | Salary |
| --- | --- | --- | --- |
| 101 | Akash | Management | 85000 |
| 102 | Mohit | Content | 55000 |
| 103 | Abhiram | Technical | 72000 |

### Explanation

- EmployeeID is the PRIMARY KEY.
- Each value is unique.
- No value is NULL.

---

# Example 1: Duplicate PRIMARY KEY Value

```sql
INSERT INTO Employees
VALUES
(101, 'Sai', 'Technical', 92000);
```

### Error

```text
Duplicate entry '101' for PRIMARY KEY
```

### Explanation

- EmployeeID 101 already exists.
- PRIMARY KEY values must be unique.
- SQL rejects the insertion.

---

# Example 2: NULL PRIMARY KEY Value

```sql
INSERT INTO Employees
VALUES
(NULL, 'Hemesh', 'Database', 68000);
```

### Error

```text
Cannot insert NULL into PRIMARY KEY column
```

### Explanation

- PRIMARY KEY columns cannot contain NULL values.
- The insertion fails.

---

# Example 3: PRIMARY KEY with AUTO_INCREMENT

Many databases allow automatic key generation.

### MySQL Example

```sql
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    StudentName VARCHAR(100)
);
```

Insert records:

```sql
INSERT INTO Students (StudentName)
VALUES
('Akash'),
('Sai'),
('Abhiram');
```

### Output

| StudentID | StudentName |
| --- | --- |
| 1 | Akash |
| 2 | Sai |
| 3 | Abhiram |

### Explanation

- StudentID values are generated automatically.
- No need to manually provide IDs.

---

# Example 4: Composite PRIMARY KEY

Create a table where one student can enroll in multiple courses.

```sql
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID)
);
```

Insert records:

```sql
INSERT INTO StudentCourses
VALUES
(1, 101, '2025-01-10'),
(1, 102, '2025-01-15'),
(2, 101, '2025-01-20');
```

### Explanation

- StudentID alone is not unique.
- CourseID alone is not unique.
- The combination of StudentID and CourseID must be unique.

---

# Example 5: Adding PRIMARY KEY to an Existing Table

Create a table without a primary key:

```sql
CREATE TABLE Departments (
    DepartmentID INT,
    DepartmentName VARCHAR(100)
);
```

Add a primary key later:

```sql
ALTER TABLE Departments
ADD CONSTRAINT PK_Department
PRIMARY KEY (DepartmentID);
```

### Explanation

- DepartmentID now uniquely identifies each department.
- Duplicate and NULL values are no longer allowed.

---

# Example 6: PRIMARY KEY and FOREIGN KEY Relationship

Create a parent table:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

Create a child table:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID)
    REFERENCES Departments(DepartmentID)
);
```

### Explanation

- DepartmentID is the PRIMARY KEY in Departments.
- Employees references that key using a FOREIGN KEY.
- This maintains referential integrity.

---

# PRIMARY KEY vs UNIQUE

| Feature | PRIMARY KEY | UNIQUE |
| --- | --- | --- |
| Allows Duplicate Values | No | No |
| Allows NULL Values | No | Yes (depends on DBMS) |
| Number Allowed Per Table | One | Multiple |
| Automatically Indexed | Yes | Yes |
| Used for Record Identification | Yes | No |

---

# Benefits of PRIMARY KEY

## Ensures Uniqueness

```sql
PRIMARY KEY (EmployeeID)
```

Prevents duplicate employee IDs.

## Prevents NULL Values

Every record must contain a valid key value.

## Improves Query Performance

The database automatically creates an index.

## Supports Relationships

Foreign keys reference primary keys to connect tables.

## Maintains Data Integrity

Each row can be uniquely identified.

---

# Common Use Cases

### Employee Table

```sql
EmployeeID INT PRIMARY KEY
```

### Customer Table

```sql
CustomerID INT PRIMARY KEY
```

### Product Table

```sql
ProductID INT PRIMARY KEY
```

### Order Table

```sql
OrderID INT PRIMARY KEY
```

### Student Enrollment Table

```sql
PRIMARY KEY (StudentID, CourseID)
```

---

# Best Practices

- Always define a PRIMARY KEY for every table.
- Use numeric identifiers when possible.
- Keep primary keys small and stable.
- Avoid frequently changing primary key values.
- Use composite keys only when necessary.
- Use AUTO_INCREMENT or IDENTITY columns for surrogate keys.

---

# Important Points

- PRIMARY KEY uniquely identifies each record.
- It automatically prevents NULL values.
- It automatically prevents duplicate values.
- Each table can have only one PRIMARY KEY.
- A PRIMARY KEY may contain multiple columns.
- An index is automatically created.
- PRIMARY KEY is commonly referenced by FOREIGN KEY constraints.

---

# Conclusion

The SQL `PRIMARY KEY` constraint is a fundamental component of relational database design. It uniquely identifies every record, prevents duplicate and NULL values, improves performance through indexing, and serves as the foundation for relationships between tables. Proper use of primary keys ensures data integrity, consistency, and efficient database operations.



###
