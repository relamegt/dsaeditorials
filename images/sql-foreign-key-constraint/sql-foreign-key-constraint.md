# SQL FOREIGN KEY Constraint

## Introduction

The SQL `FOREIGN KEY` constraint is used to create and enforce relationships between two tables. It ensures that values in a child table correspond to existing values in a parent table, thereby maintaining referential integrity.

A FOREIGN KEY prevents invalid references between tables and helps keep related data consistent across the database.

## Why Use a FOREIGN KEY?

A FOREIGN KEY helps:

- Establish relationships between tables.
- Maintain referential integrity.
- Prevent invalid data references.
- Ensure consistency between related records.
- Restrict actions that would break table relationships.
- Support cascading updates and deletions.

## Key Characteristics of FOREIGN KEY

- References a PRIMARY KEY or UNIQUE column in another table.
- Maintains relationships between parent and child tables.
- Prevents insertion of invalid reference values.
- Prevents deletion of referenced parent records unless allowed.
- Supports actions such as CASCADE, SET NULL, and RESTRICT.
- Multiple FOREIGN KEY constraints can exist in a table.

---

## Parent Table and Child Table

### Parent Table

The table containing the referenced PRIMARY KEY or UNIQUE key.

Example:

```sql
Students
```

### Child Table

The table containing the FOREIGN KEY column.

Example:

```sql
Courses
```

In a FOREIGN KEY relationship:

```text
Parent Table (Students)
        |
        |
        v
Child Table (Courses)
```

---

## Syntax

### Creating a FOREIGN KEY During Table Creation

```sql
CREATE TABLE table_name (
    column_name datatype,
    CONSTRAINT constraint_name
    FOREIGN KEY (column_name)
    REFERENCES parent_table(parent_column)
);
```

### Creating a Composite FOREIGN KEY

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    FOREIGN KEY (column1, column2)
    REFERENCES parent_table(column1, column2)
);
```

### Adding a FOREIGN KEY to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
FOREIGN KEY (column_name)
REFERENCES parent_table(parent_column);
```

### Syntax Components

| Component | Description |
| --- | --- |
| FOREIGN KEY | Creates a relationship between tables |
| REFERENCES | Specifies the parent table and column |
| CONSTRAINT | Optional name for the foreign key |
| parent_table | Table containing the referenced key |
| parent_column | Referenced PRIMARY KEY or UNIQUE column |
| ALTER TABLE | Adds a foreign key to an existing table |

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

## Creating Parent and Child Tables

### Parent Table

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50)
);
```

### Child Table

```sql
CREATE TABLE Courses (
    CourseName VARCHAR(50),
    Instructor VARCHAR(100),
    ReferenceID INT,
    CONSTRAINT FK_Student
    FOREIGN KEY (ReferenceID)
    REFERENCES Students(StudentID)
);
```

---

## Inserting Records

Insert records into the parent table:

```sql
INSERT INTO Students
VALUES
(1, 'Akash', 'Vijayawada'),
(2, 'Sai', 'Hyderabad');
```

Insert records into the child table:

```sql
INSERT INTO Courses
VALUES
('Mathematics', 'Dr. Sharma', 1),
('Biology', 'Dr. Reddy', 2);
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | City |
| --- | --- | --- |
| 1 | Akash | Vijayawada |
| 2 | Sai | Hyderabad |

```sql
SELECT * FROM Courses;
```

### Output

| CourseName | Instructor | ReferenceID |
| --- | --- | --- |
| Mathematics | Dr. Sharma | 1 |
| Biology | Dr. Reddy | 2 |

### Explanation

- ReferenceID references StudentID.
- Every ReferenceID value must exist in the Students table.
- The relationship is successfully established.

---

## Example 1: Inserting a Valid Foreign Key Value

```sql
INSERT INTO Courses
VALUES
('Physics', 'Dr. Kumar', 1);
```

### Explanation

- StudentID 1 exists in the Students table.
- The insertion succeeds.

---

## Example 2: Inserting an Invalid Foreign Key Value

```sql
INSERT INTO Courses
VALUES
('Chemistry', 'Dr. Rao', 5);
```

### Error

```text
FOREIGN KEY constraint violation:
Referenced key does not exist.
```

### Explanation

- StudentID 5 does not exist.
- The insertion fails.
- FOREIGN KEY prevents invalid references.

---

## Example 3: Deleting a Referenced Parent Record

```sql
DELETE FROM Students
WHERE StudentID = 1;
```

### Error

```text
Cannot delete or update a parent row:
A FOREIGN KEY constraint fails.
```

### Explanation

- StudentID 1 is referenced in the Courses table.
- Deleting it would create orphan records.
- SQL blocks the deletion.

---

## Example 4: Adding FOREIGN KEY to an Existing Table

Create tables:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT
);
```

Add the FOREIGN KEY:

```sql
ALTER TABLE Employees
ADD CONSTRAINT FK_Department
FOREIGN KEY (DepartmentID)
REFERENCES Departments(DepartmentID);
```

### Explanation

- Employees.DepartmentID now references Departments.DepartmentID.
- Invalid department references are prevented.

---

## Example 5: FOREIGN KEY with ON DELETE CASCADE

Create tables:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID)
    REFERENCES Departments(DepartmentID)
    ON DELETE CASCADE
);
```

### Explanation

- If a department is deleted,
- All related employee records are automatically deleted.
- Useful when child records should not exist without the parent.

---

## Example 6: FOREIGN KEY with ON UPDATE CASCADE

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID)
    REFERENCES Departments(DepartmentID)
    ON UPDATE CASCADE
);
```

### Explanation

- If DepartmentID changes in the parent table,
- The change automatically updates related child records.

---

## Example 7: Composite FOREIGN KEY

Parent table:

```sql
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID)
);
```

Child table:

```sql
CREATE TABLE ExamResults (
    StudentID INT,
    CourseID INT,
    Marks INT,
    FOREIGN KEY (StudentID, CourseID)
    REFERENCES StudentCourses(StudentID, CourseID)
);
```

### Explanation

- Both columns together form the FOREIGN KEY.
- The combination must exist in the parent table.

---

## FOREIGN KEY Actions

### CASCADE

Automatically updates or deletes related child records.

```sql
ON DELETE CASCADE
```

### RESTRICT

Prevents deletion or updates when related records exist.

```sql
ON DELETE RESTRICT
```

### SET NULL

Sets foreign key values to NULL when the parent row is deleted.

```sql
ON DELETE SET NULL
```

### NO ACTION

Rejects the operation if dependent records exist.

```sql
ON DELETE NO ACTION
```

---

## FOREIGN KEY vs PRIMARY KEY

| Feature | PRIMARY KEY | FOREIGN KEY |
| --- | --- | --- |
| Uniquely identifies rows | Yes | No |
| Allows NULL values | No | Yes (unless restricted) |
| Prevents duplicate values | Yes | No |
| Maintains relationships | No | Yes |
| Referenced by other tables | Yes | No |
| Number allowed per table | One | Multiple |

---

## Benefits of FOREIGN KEY

### Maintains Referential Integrity

Ensures relationships remain valid.

### Prevents Invalid References

Only existing parent records can be referenced.

### Improves Data Consistency

Related data remains synchronized.

### Supports Cascading Operations

Automatically updates or deletes dependent records.

### Simplifies Database Design

Makes relationships clear and enforceable.

---

## Common Use Cases

### Students and Courses

```sql
FOREIGN KEY (StudentID)
REFERENCES Students(StudentID)
```

### Employees and Departments

```sql
FOREIGN KEY (DepartmentID)
REFERENCES Departments(DepartmentID)
```

### Orders and Customers

```sql
FOREIGN KEY (CustomerID)
REFERENCES Customers(CustomerID)
```

### Order Items and Products

```sql
FOREIGN KEY (ProductID)
REFERENCES Products(ProductID)
```

---

## Best Practices

- Always reference a PRIMARY KEY or UNIQUE column.
- Use meaningful constraint names.
- Index frequently used foreign key columns.
- Use CASCADE carefully.
- Avoid unnecessary cascading deletes.
- Validate relationships before inserting data.

---

## Important Points

- FOREIGN KEY creates relationships between tables.
- Referenced values must exist in the parent table.
- Multiple foreign keys can exist in a table.
- FOREIGN KEY supports CASCADE, RESTRICT, SET NULL, and NO ACTION.
- Helps maintain referential integrity.
- Prevents orphaned records.
- Commonly references PRIMARY KEY columns.

---

## Conclusion

The SQL `FOREIGN KEY` constraint is essential for maintaining relationships between tables and enforcing referential integrity. It ensures that child table records always reference valid parent records, prevents inconsistent data, and supports advanced actions such as cascading updates and deletions. Proper use of FOREIGN KEY constraints leads to reliable, consistent, and well-structured relational databases.



###
