# SQL Alternate Key

## Introduction

An Alternate Key in SQL is a candidate key that is not selected as the PRIMARY KEY but can still uniquely identify a record in a table.

When multiple columns are capable of uniquely identifying rows, one column is chosen as the PRIMARY KEY, while the remaining candidate keys become Alternate Keys.

Alternate Keys are typically implemented using the `UNIQUE` constraint.

## Why Use an Alternate Key?

An Alternate Key helps you:

- Uniquely identify records using alternative columns.
- Prevent duplicate values.
- Maintain data integrity.
- Provide additional unique identifiers.
- Support business requirements such as unique email addresses, phone numbers, or registration numbers.

## Key Characteristics of Alternate Key

- Must contain unique values.
- Usually implemented using the UNIQUE constraint.
- A table can have multiple Alternate Keys.
- One candidate key becomes the PRIMARY KEY.
- Remaining candidate keys become Alternate Keys.
- Can be used for searching and identifying records.

## Relationship Between Candidate Key, Primary Key, and Alternate Key

Consider a table containing:

- EmployeeID
- Email
- PhoneNumber

If all three columns contain unique values, they are candidate keys.

Suppose EmployeeID is selected as the PRIMARY KEY.

Then:

- EmployeeID → Primary Key
- Email → Alternate Key
- PhoneNumber → Alternate Key

## Syntax

### Creating Alternate Keys During Table Creation

```sql
CREATE TABLE table_name (
    primary_column datatype PRIMARY KEY,
    alternate_column1 datatype UNIQUE,
    alternate_column2 datatype UNIQUE
);
```

### Adding an Alternate Key to an Existing Table

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
UNIQUE (column_name);
```

### Syntax Components

| Component | Description |
| --- | --- |
| PRIMARY KEY | Main unique identifier of the table |
| UNIQUE | Creates an Alternate Key |
| CONSTRAINT | Optional name for the key |
| ALTER TABLE | Adds an Alternate Key to an existing table |
| Candidate Key | A column eligible to become a PRIMARY KEY |

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

## Creating a Table with Alternate Keys

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    PhoneNumber VARCHAR(15) UNIQUE,
    City VARCHAR(50)
);
```

### Explanation

- StudentID is the PRIMARY KEY.
- Email is an Alternate Key.
- PhoneNumber is an Alternate Key.
- Both Email and PhoneNumber uniquely identify records.

---

## Inserting Records

```sql
INSERT INTO Students
VALUES
(101, 'Akash', 'akash@gmail.com', '9876543210', 'Vijayawada'),
(102, 'Mohit', 'mohit@gmail.com', '9876543211', 'Hyderabad'),
(103, 'Abhiram', 'abhiram@gmail.com', '9876543212', 'Guntur');
```

Display records:

```sql
SELECT * FROM Students;
```

### Output

| StudentID | StudentName | Email | PhoneNumber | City |
| --- | --- | --- | --- | --- |
| 101 | Akash | [akash@gmail.com](mailto:akash@gmail.com) | 9876543210 | Vijayawada |
| 102 | Mohit | [mohit@gmail.com](mailto:mohit@gmail.com) | 9876543211 | Hyderabad |
| 103 | Abhiram | [abhiram@gmail.com](mailto:abhiram@gmail.com) | 9876543212 | Guntur |

### Explanation

- StudentID uniquely identifies each student.
- Email values are unique.
- Phone numbers are unique.
- Email and PhoneNumber function as Alternate Keys.

---

## Example 1: Duplicate Alternate Key Value

```sql
INSERT INTO Students
VALUES
(104, 'Hemesh', 'akash@gmail.com', '9876543213', 'Guntur');
```

### Error

```text
UNIQUE constraint violation:
Duplicate value detected.
```

### Explanation

- [akash@gmail.com](mailto:akash@gmail.com)  already exists.
- Alternate Keys must remain unique.
- SQL rejects the insertion.

---

## Example 2: Duplicate Phone Number

```sql
INSERT INTO Students
VALUES
(105, 'Akhil', 'akhil@gmail.com', '9876543211', 'Hyderabad');
```

### Error

```text
UNIQUE constraint violation:
Duplicate value detected.
```

### Explanation

- Phone number 9876543211 already exists.
- Alternate Key values cannot be duplicated.

---

## Example 3: Adding an Alternate Key to an Existing Table

Create a table:

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Email VARCHAR(100)
);
```

Add an Alternate Key:

```sql
ALTER TABLE Employees
ADD CONSTRAINT UQ_Email
UNIQUE (Email);
```

### Explanation

- Email becomes an Alternate Key.
- Duplicate email addresses are no longer allowed.

---

## Example 4: Multiple Alternate Keys

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    AadhaarNumber VARCHAR(20) UNIQUE,
    PhoneNumber VARCHAR(15) UNIQUE
);
```

### Explanation

- CustomerID is the PRIMARY KEY.
- Email is an Alternate Key.
- AadhaarNumber is an Alternate Key.
- PhoneNumber is an Alternate Key.
- The table contains three Alternate Keys.

---

## Example 5: Alternate Key with Product Information

```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductCode VARCHAR(20) UNIQUE,
    ProductName VARCHAR(100)
);
```

Insert records:

```sql
INSERT INTO Products
VALUES
(1, 'PRD101', 'Laptop'),
(2, 'PRD102', 'Keyboard'),
(3, 'PRD103', 'Mouse');
```

### Explanation

- ProductID is the PRIMARY KEY.
- ProductCode is an Alternate Key.
- ProductCode can uniquely identify products.

---

## Rules for Alternate Keys

- Alternate Keys must contain unique values.
- Multiple Alternate Keys can exist in a table.
- One candidate key becomes the PRIMARY KEY.
- Remaining candidate keys become Alternate Keys.
- Alternate Keys are commonly implemented using UNIQUE constraints.
- Alternate Keys help maintain data integrity.

---

## Alternate Key vs Primary Key

| Feature | Primary Key | Alternate Key |
| --- | --- | --- |
| Must Be Unique | Yes | Yes |
| Allows NULL Values | No | Yes (DBMS dependent) |
| Number Allowed Per Table | One | Multiple |
| Identifies Records | Yes | Yes |
| Implemented Using | PRIMARY KEY | UNIQUE |
| Candidate Key Selected | Yes | No |

---

## Common Use Cases

### Email Address

```sql
Email VARCHAR(100) UNIQUE
```

### Phone Number

```sql
PhoneNumber VARCHAR(15) UNIQUE
```

### Aadhaar Number

```sql
AadhaarNumber VARCHAR(20) UNIQUE
```

### PAN Number

```sql
PANNumber VARCHAR(20) UNIQUE
```

### Product Code

```sql
ProductCode VARCHAR(20) UNIQUE
```

---

## Best Practices

- Choose a stable column as the PRIMARY KEY.
- Use Alternate Keys for other unique business attributes.
- Apply UNIQUE constraints carefully.
- Avoid unnecessary Alternate Keys.
- Use meaningful columns such as email, phone number, or registration number.

---

## Important Points

- An Alternate Key is a candidate key that is not selected as the PRIMARY KEY.
- Alternate Keys are implemented using UNIQUE constraints.
- A table can have multiple Alternate Keys.
- Alternate Keys help prevent duplicate data.
- They provide additional methods of uniquely identifying records.
- Alternate Keys improve data consistency and integrity.

---

## Conclusion

The SQL Alternate Key is a candidate key that is not chosen as the PRIMARY KEY but still uniquely identifies records within a table. Implemented using the UNIQUE constraint, Alternate Keys help maintain data integrity, prevent duplicate values, and provide additional unique identifiers for business operations. They play an important role in designing efficient and reliable relational databases.



###
