# SQL Composite Key

## Introduction

A Composite Key in SQL is a primary key that consists of two or more columns used together to uniquely identify each record in a table. Individually, the columns may contain duplicate values, but their combined values must be unique.

Composite keys are commonly used when a single column cannot uniquely identify records and multiple columns are required to establish uniqueness.

## Why Use a Composite Key?

A Composite Key helps you:

- Uniquely identify records using multiple columns.
- Prevent duplicate combinations of data.
- Maintain data integrity.
- Support many-to-many relationships.
- Avoid creating unnecessary surrogate keys.

## Key Characteristics of Composite Key

- Consists of two or more columns.
- The combination of values must be unique.
- Individual columns can contain duplicate values.
- Composite key columns cannot contain NULL values.
- A table can have only one PRIMARY KEY, which may be composite.

## Syntax

### Creating a Composite Key During Table Creation

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    PRIMARY KEY (column1, column2)
);
```

### Adding a Composite Key to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
PRIMARY KEY (column1, column2);
```

### Syntax Components

| Component | Description |
| --- | --- |
| PRIMARY KEY | Defines the primary key |
| column1, column2 | Columns that form the composite key |
| CONSTRAINT | Optional name assigned to the key |
| ALTER TABLE | Adds the key to an existing table |

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
CREATE TABLE Orders (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10,2),
    PRIMARY KEY (OrderID, ProductID)
);
```

## Inserting Sample Records

```sql
INSERT INTO Orders
VALUES
(101, 1, 2, 150.00),
(101, 2, 1, 250.00),
(102, 1, 3, 150.00);
```

Display all records:

```sql
SELECT * FROM Orders;
```

### Output

| OrderID | ProductID | Quantity | Price |
| --- | --- | --- | --- |
| 101 | 1 | 2 | 150.00 |
| 101 | 2 | 1 | 250.00 |
| 102 | 1 | 3 | 150.00 |

### Explanation

- OrderID alone is not unique.
- ProductID alone is not unique.
- The combination of OrderID and ProductID uniquely identifies each row.

---

## Example 1: Student Enrollment Table Using Composite Key

Create the table:

```sql
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    StudentName VARCHAR(100),
    PRIMARY KEY (StudentID, CourseID)
);
```

Insert records:

```sql
INSERT INTO StudentCourses
VALUES
(101, 1, 'Akash'),
(102, 1, 'Mohit'),
(103, 2, 'Abhiram'),
(104, 2, 'Hemesh'),
(105, 3, 'Akhil');
```

Display records:

```sql
SELECT * FROM StudentCourses;
```

### Output

| StudentID | CourseID | StudentName |
| --- | --- | --- |
| 101 | 1 | Akash |
| 102 | 1 | Mohit |
| 103 | 2 | Abhiram |
| 104 | 2 | Hemesh |
| 105 | 3 | Akhil |

### Explanation

- Multiple students can enroll in the same course.
- A student can enroll in multiple courses.
- StudentID and CourseID together uniquely identify an enrollment.

---

## Example 2: Duplicate Composite Key Value

```sql
INSERT INTO StudentCourses
VALUES
(101, 1, 'Akash');
```

### Error

```text
PRIMARY KEY constraint violation:
Duplicate composite key value detected.
```

### Explanation

- The combination (101, 1) already exists.
- Composite key values must remain unique.
- SQL rejects the insertion.

---

## Example 3: NULL Value in Composite Key

```sql
INSERT INTO StudentCourses
VALUES
(NULL, 4, 'Mohit');
```

### Error

```text
PRIMARY KEY constraint violation:
NULL values are not allowed.
```

### Explanation

- Composite key columns cannot contain NULL values.
- The insertion fails because StudentID is part of the primary key.

---

## Example 4: Adding a Composite Key to an Existing Table

Create a table without a primary key:

```sql
CREATE TABLE ProjectAssignments (
    EmployeeID INT,
    ProjectID INT,
    AssignedDate DATE
);
```

Add the composite key:

```sql
ALTER TABLE ProjectAssignments
ADD CONSTRAINT PK_ProjectAssignments
PRIMARY KEY (EmployeeID, ProjectID);
```

### Explanation

- The composite key is added after table creation.
- EmployeeID and ProjectID together uniquely identify each assignment.

---

## Rules for Composite Keys

- A composite key consists of two or more columns.
- The combined values must be unique.
- Individual columns may contain duplicate values.
- Composite key columns cannot contain NULL values.
- A table can have only one PRIMARY KEY.
- Composite keys automatically create an index.

---

## Composite Key vs Simple Primary Key

| Feature | Simple Primary Key | Composite Key |
| --- | --- | --- |
| Number of Columns | One | Multiple |
| Uniqueness Based On | Single Column | Combination of Columns |
| Complexity | Simple | More Complex |
| Storage Requirement | Lower | Higher |
| Typical Use Case | Single Identifier | Multiple Identifiers |

---

## Common Use Cases

### Student Course Enrollment

```sql
PRIMARY KEY (StudentID, CourseID)
```

### Order Details

```sql
PRIMARY KEY (OrderID, ProductID)
```

### Employee Project Assignment

```sql
PRIMARY KEY (EmployeeID, ProjectID)
```

### Customer Product Purchases

```sql
PRIMARY KEY (CustomerID, ProductID)
```

---

## Best Practices

- Use composite keys only when necessary.
- Keep the number of key columns minimal.
- Avoid frequently changing key columns.
- Ensure all composite key columns are mandatory.
- Use meaningful business identifiers whenever possible.

---

## Important Points

- A composite key uses multiple columns to uniquely identify records.
- Individual columns can contain duplicate values.
- The combined values must always be unique.
- Composite key columns cannot contain NULL values.
- Composite keys are commonly used in junction tables.
- Composite keys automatically create an index.

---

## Conclusion

The SQL `Composite Key` is a powerful mechanism for uniquely identifying records when a single column is not sufficient. By combining multiple columns into a single primary key, composite keys help maintain data integrity, enforce uniqueness, and accurately model real-world relationships in relational databases.



###
