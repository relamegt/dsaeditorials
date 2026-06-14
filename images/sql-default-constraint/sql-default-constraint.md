# SQL DEFAULT Constraint

## Introduction

The SQL `DEFAULT` constraint is used to automatically assign a predefined value to a column when no value is provided during an INSERT operation.

It helps maintain consistency, reduces manual data entry, and ensures that columns always receive meaningful values when data is inserted.

## Why Use a DEFAULT Constraint?

The `DEFAULT` constraint helps you:

- Automatically assign values when no value is specified.
- Reduce repetitive data entry.
- Maintain data consistency.
- Prevent unnecessary NULL values.
- Simplify INSERT statements.

## Key Characteristics of DEFAULT Constraint

- Provides a predefined value for a column.
- Applied only when no value is specified.
- Can be used with most data types.
- Can be defined during table creation.
- Can be added later using ALTER TABLE.
- Does not affect explicitly provided values.

## Syntax

### Creating a DEFAULT Constraint During Table Creation

```sql
CREATE TABLE table_name (
    column_name datatype DEFAULT default_value
);
```

### Using DEFAULT for Multiple Columns

```sql
CREATE TABLE table_name (
    column1 datatype DEFAULT value1,
    column2 datatype DEFAULT value2
);
```

### Adding a DEFAULT Constraint to an Existing Table

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
SET DEFAULT default_value;
```

### Syntax Components

| Component | Description |
| --- | --- |
| DEFAULT | Assigns a predefined value |
| default_value | Value automatically inserted |
| ALTER TABLE | Adds a default value to an existing table |
| column_name | Column receiving the default value |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Table with DEFAULT Constraint

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    City VARCHAR(50) DEFAULT 'Vijayawada'
);
```

### Explanation

- If no city is provided, SQL automatically inserts 'Vijayawada'.
- Explicitly provided values override the default value.

---

## Inserting Records Using DEFAULT Values

```sql
INSERT INTO Students (StudentID, StudentName)
VALUES
(101, 'Akash'),
(102, 'Mohit');
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | City |
| --- | --- | --- |
| 101 | Akash | Vijayawada |
| 102 | Mohit | Vijayawada |

### Explanation

- No city values were supplied.
- SQL automatically inserted the default value.

---

## Example 1: Overriding the DEFAULT Value

```sql
INSERT INTO Students
VALUES
(103, 'Abhiram', 'Hyderabad');
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | City |
| --- | --- | --- |
| 101 | Akash | Vijayawada |
| 102 | Mohit | Vijayawada |
| 103 | Abhiram | Hyderabad |

### Explanation

- Since a city value was explicitly provided, SQL uses that value instead of the default.

---

## Example 2: DEFAULT Constraint for Department

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Department VARCHAR(50) DEFAULT 'Technical'
);
```

Insert records:

```sql
INSERT INTO Employees (EmployeeID, EmployeeName)
VALUES
(1, 'Akash'),
(2, 'Mohit');
```

Display records:

```sql
SELECT * FROM Employees;
```

### Output

| EmployeeID | EmployeeName | Department |
| --- | --- | --- |
| 1 | Akash | Technical |
| 2 | Mohit | Technical |

### Explanation

- Department was not specified.
- SQL automatically assigned the default department.

---

## Example 3: Using DEFAULT with Numeric Values

```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Quantity INT DEFAULT 0
);
```

Insert records:

```sql
INSERT INTO Products (ProductID, ProductName)
VALUES
(101, 'Keyboard'),
(102, 'Mouse');
```

Display records:

```sql
SELECT * FROM Products;
```

### Output

| ProductID | ProductName | Quantity |
| --- | --- | --- |
| 101 | Keyboard | 0 |
| 102 | Mouse | 0 |

### Explanation

- Quantity was not provided.
- SQL inserted the default value 0.

---

## Example 4: Using DEFAULT with Current Date

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    OrderDate DATE DEFAULT CURRENT_DATE
);
```

Insert records:

```sql
INSERT INTO Orders (OrderID, CustomerName)
VALUES
(1, 'Akash'),
(2, 'Mohit');
```

### Explanation

- The current system date is automatically stored.
- No need to manually enter the date.

---

## Example 5: Adding a DEFAULT Constraint Using ALTER TABLE

Create a table:

```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

Add a default value:

```sql
ALTER TABLE Departments
ALTER COLUMN DepartmentName
SET DEFAULT 'General';
```

### Explanation

- Future records automatically receive 'General' when no department name is specified.

---

## Example 6: Removing a DEFAULT Constraint

```sql
ALTER TABLE Departments
ALTER COLUMN DepartmentName
DROP DEFAULT;
```

### Explanation

- The default value is removed.
- Future inserts will no longer receive automatic values.

---

## Example 7: DEFAULT with NOT NULL

```sql
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    Status VARCHAR(20) NOT NULL DEFAULT 'Active'
);
```

Insert records:

```sql
INSERT INTO Courses (CourseID, CourseName)
VALUES
(101, 'SQL'),
(102, 'Java');
```

Display records:

```sql
SELECT * FROM Courses;
```

### Output

| CourseID | CourseName | Status |
| --- | --- | --- |
| 101 | SQL | Active |
| 102 | Java | Active |

### Explanation

- Status cannot be NULL.
- DEFAULT automatically assigns 'Active'.

---

## Rules for DEFAULT Constraint

- Used when no value is specified during insertion.
- Explicit values override the default value.
- Can be used with strings, numbers, and dates.
- Can be combined with NOT NULL.
- Can be added or removed later.

---

## DEFAULT vs NULL

| Feature | DEFAULT | NULL |
| --- | --- | --- |
| Automatically assigns value | Yes | No |
| Requires user input | No | No |
| Improves consistency | Yes | No |
| Represents missing data | No | Yes |
| Can be customized | Yes | No |

---

## Common Use Cases

### Default City

```sql
City VARCHAR(50) DEFAULT 'Vijayawada'
```

### Default Department

```sql
Department VARCHAR(50) DEFAULT 'Technical'
```

### Default Quantity

```sql
Quantity INT DEFAULT 0
```

### Default Status

```sql
Status VARCHAR(20) DEFAULT 'Active'
```

### Default Current Date

```sql
OrderDate DATE DEFAULT CURRENT_DATE
```

---

## Best Practices

- Use DEFAULT values for commonly repeated data.
- Combine DEFAULT with NOT NULL when appropriate.
- Choose meaningful default values.
- Avoid misleading default data.
- Document business-related default values clearly.

---

## Important Points

- DEFAULT automatically inserts predefined values.
- It is used only when no value is provided.
- Explicit values always override the default.
- DEFAULT can be applied to numeric, text, and date columns.
- Constraints can be added or removed later.
- DEFAULT improves consistency and simplifies data entry.

---

## Conclusion

The SQL `DEFAULT` constraint is a useful feature that automatically assigns predefined values when no value is provided during data insertion. It helps maintain consistency, reduce manual input, and simplify database operations. When used appropriately with other constraints such as NOT NULL and CHECK, DEFAULT contributes to more reliable and efficient database design.



###
