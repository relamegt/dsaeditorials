# SQL PRIMARY KEY Constraint

## Introduction

The SQL `PRIMARY KEY` constraint uniquely identifies each record in a table and ensures strong data integrity. It prevents duplicate and NULL values, making it one of the most important constraints in relational database design.

A PRIMARY KEY helps maintain data consistency, improves query performance through indexing, and serves as the foundation for relationships between tables.

## Why Use a PRIMARY KEY?

A PRIMARY KEY helps:

- Uniquely identify each row in a table.
- Prevent duplicate records.
- Prevent NULL values.
- Improve query performance through automatic indexing.
- Establish relationships between tables.
- Maintain data integrity and consistency.

## Key Characteristics of PRIMARY KEY

- Values must be unique.
- Values cannot be NULL.
- A table can have only one PRIMARY KEY.
- A PRIMARY KEY can contain one or multiple columns.
- An index is automatically created.
- Frequently referenced by FOREIGN KEY constraints.

---

## Types of Primary Keys

### 1. Simple Primary Key

A simple primary key consists of a single column.

Example:

```sql
EmployeeID INT PRIMARY KEY
```

### 2. Composite Primary Key

A composite primary key consists of multiple columns.

Example:

```sql
PRIMARY KEY (StudentID, CourseID)
```

The combination of values from all columns must be unique.

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

### Syntax Components

| Component | Description |
| --- | --- |
| PRIMARY KEY | Uniquely identifies each row in a table |
| column_name | Column used as the primary key |
| CONSTRAINT | Optional name assigned to the constraint |
| ALTER TABLE | Adds a primary key to an existing table |
| Composite Key | Primary key created using multiple columns |

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

## Creating a Table with PRIMARY KEY

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50),
    Department VARCHAR(50)
);
```

---

## Inserting Records

```sql
INSERT INTO Employees (EmpID, EmpName, Department)
VALUES
(101, 'Bob', 'Sales'),
(102, 'Lucas', 'HR');
```

Display all records:

```sql
SELECT * FROM Employees;
```

### Output

| EmpID | EmpName | Department |
| --- | --- | --- |
| 101 | Bob | Sales |
| 102 | Lucas | HR |

### Explanation

- EmpID is the PRIMARY KEY.
- Each value must be unique.
- NULL values are not allowed.

---

## Example 1: Duplicate PRIMARY KEY Value

```sql
INSERT INTO Employees
VALUES
(101, 'Alice', 'IT');
```

### Error

```text
PRIMARY KEY constraint violation:
Duplicate key value detected.
```

### Explanation

- EmpID 101 already exists.
- PRIMARY KEY values must be unique.
- SQL rejects the insertion.

---

## Example 2: NULL PRIMARY KEY Value

```sql
INSERT INTO Employees
VALUES
(NULL, 'Emma', 'Finance');
```

### Error

```text
PRIMARY KEY constraint violation:
NULL values are not allowed.
```

### Explanation

- PRIMARY KEY columns cannot contain NULL values.
- The insertion fails.

---

## Example 3: Creating a PRIMARY KEY in a New Table

```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    LastName VARCHAR(255),
    FirstName VARCHAR(255),
    Age INT
);
```

Insert records:

```sql
INSERT INTO Persons VALUES
(1, 'Johnson', 'Emily', 25),
(2, 'Walker', 'James', 30);
```

Display records:

```sql
SELECT * FROM Persons;
```

### Output

| PersonID | LastName | FirstName | Age |
| --- | --- | --- | --- |
| 1 | Johnson | Emily | 25 |
| 2 | Walker | James | 30 |

### Explanation

- PersonID is the PRIMARY KEY.
- Each row contains a unique identifier.
- Duplicate values are not allowed.

---

## Example 4: Composite PRIMARY KEY

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
INSERT INTO StudentCourses VALUES
(1, 101, '2025-01-10'),
(1, 102, '2025-01-15'),
(2, 101, '2025-01-20');
```

Display records:

```sql
SELECT * FROM StudentCourses;
```

### Output

| StudentID | CourseID | EnrollmentDate |
| --- | --- | --- |
| 1 | 101 | 2025-01-10 |
| 1 | 102 | 2025-01-15 |
| 2 | 101 | 2025-01-20 |

### Explanation

- StudentID alone is not unique.
- CourseID alone is not unique.
- The combination of StudentID and CourseID must be unique.

---

## Example 5: Adding PRIMARY KEY to an Existing Table

Create a table without a primary key:

```sql
CREATE TABLE Person (
    PersonID INT,
    LastName VARCHAR(255),
    FirstName VARCHAR(255),
    Age INT
);
```

Add a primary key:

```sql
ALTER TABLE Person
ADD CONSTRAINT PK_Person
PRIMARY KEY (PersonID);
```

Display table structure:

```sql
DESCRIBE Person;
```

### Output

| Field | Type | Key |
| --- | --- | --- |
| PersonID | INT | PRI |
| LastName | VARCHAR(255) |  |
| FirstName | VARCHAR(255) |  |
| Age | INT |  |

### Explanation

- PersonID now uniquely identifies each row.
- Duplicate values are prohibited.
- NULL values are prohibited.

---

## Example 6: PRIMARY KEY with AUTO_INCREMENT

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
- Every generated value remains unique.

---

## Example 7: PRIMARY KEY and FOREIGN KEY Relationship

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
- Employees references DepartmentID using a FOREIGN KEY.
- This relationship maintains referential integrity.

---

## PRIMARY KEY vs UNIQUE

| Feature | PRIMARY KEY | UNIQUE |
| --- | --- | --- |
| Allows Duplicate Values | No | No |
| Allows NULL Values | No | Yes (depends on DBMS) |
| Number Allowed Per Table | One | Multiple |
| Automatically Indexed | Yes | Yes |
| Used for Record Identification | Yes | No |

---

## Benefits of PRIMARY KEY

### Ensures Uniqueness

```sql
PRIMARY KEY (EmpID)
```

Prevents duplicate record identifiers.

### Prevents NULL Values

Every record must contain a valid key value.

### Improves Query Performance

The database automatically creates an index.

### Supports Relationships

Foreign keys reference primary keys to establish table relationships.

### Maintains Data Integrity

Each record can be uniquely identified.

---

## Common Use Cases

### Employee Table

```sql
EmpID INT PRIMARY KEY
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

## Best Practices

- Always define a PRIMARY KEY for every table.
- Prefer numeric identifiers when possible.
- Keep primary key values small and stable.
- Avoid updating primary key values frequently.
- Use composite keys only when necessary.
- Use AUTO_INCREMENT or IDENTITY for surrogate keys.

---

## Important Points

- PRIMARY KEY uniquely identifies each record.
- PRIMARY KEY values must be unique.
- PRIMARY KEY columns cannot contain NULL values.
- A table can have only one PRIMARY KEY.
- A PRIMARY KEY can contain one or multiple columns.
- PRIMARY KEY automatically creates an index.
- PRIMARY KEY is commonly referenced by FOREIGN KEY constraints.

---

## Conclusion

The SQL `PRIMARY KEY` constraint is a fundamental component of relational database design. It uniquely identifies every record in a table, prevents duplicate and NULL values, improves query performance through indexing, and serves as the foundation for relationships between tables. Proper use of primary keys ensures data integrity, consistency, and efficient database operations.



###
