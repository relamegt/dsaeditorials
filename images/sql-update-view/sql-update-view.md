# SQL UPDATE VIEW

## Introduction

The SQL UPDATE VIEW statement is used to modify data displayed through a view or to change the definition of an existing view. Views are virtual tables created from SQL queries, and updating them allows you to manage how data is presented without directly modifying the underlying table structure.

A view can be updated in two ways:

- Using the `UPDATE` statement to modify data through a simple view.
- Using `CREATE OR REPLACE VIEW` to change the structure or definition of the view.

---

## Why Update a View?

Updating a view helps you:

- Modify data through a virtual table.
- Simplify data management.
- Change view definitions without dropping them.
- Restrict access to specific data.
- Maintain reusable query structures.

---

## Syntax

### Updating Data Through a View

```sql
UPDATE view_name
SET column_name = value
WHERE condition;
```

### Updating the View Definition

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Syntax Components

| Component | Description |
| --- | --- |
| UPDATE | Modifies data through a view |
| SET | Specifies new values |
| WHERE | Filters rows to update |
| CREATE OR REPLACE VIEW | Updates the view definition |
| SELECT | Defines the data displayed in the view |

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
CREATE TABLE Students (
    RollNo INT PRIMARY KEY,
    StudentName VARCHAR(100),
    Subject VARCHAR(50),
    Marks INT
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Students VALUES
(1, 'Akash', 'SQL', 85),
(2, 'Akhil', 'Java', 78),
(3, 'Hemanth', 'SQL', 90),
(4, 'Mohit', 'Python', 88),
(5, 'Abhiram', 'Java', 72);
```

Display the table:

```sql
SELECT * FROM Students;
```

### Output

| RollNo | StudentName | Subject | Marks |
| --- | --- | --- | --- |
| 1 | Akash | SQL | 85 |
| 2 | Akhil | Java | 78 |
| 3 | Hemanth | SQL | 90 |
| 4 | Mohit | Python | 88 |
| 5 | Abhiram | Java | 72 |

---

## Creating a View

```sql
CREATE VIEW StudentView AS
SELECT RollNo, StudentName, Marks
FROM Students;
```

Display the view:

```sql
SELECT * FROM StudentView;
```

---

## Example 1: Updating a View Using UPDATE Statement

Update marks for specific students.

```sql
UPDATE StudentView
SET Marks = 95
WHERE RollNo IN (3, 5);
```

Display the updated view:

```sql
SELECT * FROM StudentView;
```

### Output

| RollNo | StudentName | Marks |
| --- | --- | --- |
| 1 | Akash | 85 |
| 2 | Akhil | 78 |
| 3 | Hemanth | 95 |
| 4 | Mohit | 88 |
| 5 | Abhiram | 95 |

### Explanation

- The UPDATE statement modifies data through the view.
- Only rows with RollNo 3 and 5 are updated.
- Changes are reflected in the underlying table.

---

## Example 2: Updating Values Using Arithmetic Operations

Increase marks by 5%.

```sql
UPDATE StudentView
SET Marks = Marks * 1.05;
```

Display the updated view:

```sql
SELECT * FROM StudentView;
```

### Output

| RollNo | StudentName | Marks |
| --- | --- | --- |
| 1 | Akash | 89.25 |
| 2 | Akhil | 81.90 |
| 3 | Hemanth | 99.75 |
| 4 | Mohit | 92.40 |
| 5 | Abhiram | 99.75 |

### Explanation

- Arithmetic expressions can be used during updates.
- Each student's marks increase by 5%.
- The calculation is applied to every row.

---

## Example 3: Updating a View Using Aggregate Functions

Replace the view definition to show total marks by subject.

```sql
CREATE OR REPLACE VIEW StudentView AS
SELECT Subject, SUM(Marks) AS TotalMarks
FROM Students
GROUP BY Subject;
```

Display the view:

```sql
SELECT * FROM StudentView;
```

### Output

| Subject | TotalMarks |
| --- | --- |
| SQL | 175 |
| Java | 150 |
| Python | 88 |

### Explanation

- The original view structure is replaced.
- The new view displays subject-wise totals.
- Aggregate functions require redefining the view.

---

## Example 4: Updating a View Using a Subquery

Replace the view using a subquery.

```sql
CREATE OR REPLACE VIEW StudentView AS
SELECT StudentName,
(
    SELECT SUM(Marks)
    FROM Students s
    WHERE s.Subject = Students.Subject
) AS TotalSubjectMarks
FROM Students;
```

Display the view:

```sql
SELECT * FROM StudentView;
```

### Output

| StudentName | TotalSubjectMarks |
| --- | --- |
| Akash | 175 |
| Akhil | 150 |
| Hemanth | 175 |
| Mohit | 88 |
| Abhiram | 150 |

### Explanation

- The subquery calculates total marks for each subject.
- Students belonging to the same subject receive the same total.
- The view definition is replaced using CREATE OR REPLACE VIEW.

---

## Best Practices

- Use UPDATE only on simple views whenever possible.
- Verify affected rows before executing updates.
- Use CREATE OR REPLACE VIEW when changing view definitions.
- Avoid updating complex views containing joins and aggregates.
- Test updates in a development environment first.

---

## Important Points

- Views are virtual tables based on SQL queries.
- UPDATE can modify data through simple views.
- CREATE OR REPLACE VIEW changes the view structure.
- Changes through updatable views affect underlying tables.
- Aggregate and complex views usually require view redefinition.

---

## Conclusion

The SQL UPDATE VIEW statement allows developers to modify data displayed through views and redefine view structures when requirements change. By using UPDATE for simple views and CREATE OR REPLACE VIEW for structural changes, database administrators can efficiently manage virtual tables while keeping queries organized, reusable, and secure.



###
