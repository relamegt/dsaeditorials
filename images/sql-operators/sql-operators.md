# SQL Operators

In SQL, **operators** are special symbols used to perform operations on data. They are the "verbs" of your queries, allowing you to calculate, compare, and filter information. 

This guide covers the six major types of operators with practical examples.

![SQL Operators](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/sql-operators/1781438127508-sql_operator.png)

---

## 1. Arithmetic Operators

These are used to perform mathematical calculations on numeric columns.

**Sample Table: `Employees`**

| ID | Name | Salary | Bonus |
| --- | --- | --- | --- |
| 1 | Alice | 5000 | 500 |
| 2 | Bob | 6000 | 700 |
| 3 | Charlie | 4500 | 200 |

| Operator | Description | Example Query |
| --- | --- | --- |
| `+` | Addition | `SELECT Salary + Bonus AS TotalPay FROM Employees;` |
| `-` | Subtraction | `SELECT Salary - Bonus AS NetPay FROM Employees;` |
| `*` | Multiplication | `SELECT Salary * 1.1 AS RaiseAmount FROM Employees;` |
| `/` | Division | `SELECT Salary / 2 AS HalfSalary FROM Employees;` |
| `%` | Modulus (Remainder) | `SELECT Salary % 100 AS Remainder FROM Employees;` |

**Output for `Salary + Bonus`:**

| TotalPay |
| --- |
| 5500 |
| 6700 |
| 4700 |

---

## 2. Comparison Operators

These are used to compare two values. They always return **True** or **False**, and are usually used in `WHERE` clauses to filter data.

**Sample Table: `Products`**

| Product | Price | Stock |
| --- | --- | --- |
| Laptop | 1200 | 10 |
| Mouse | 25 | 50 |
| Monitor | 200 | 15 |

| Operator | Description | Example Query | Result |
| --- | --- | --- | --- |
| `=` | Equal to | `SELECT * FROM Products WHERE Price = 200;` | Monitor |
| `!=` | Not equal to | `SELECT * FROM Products WHERE Product != 'Mouse';` | Laptop, Monitor |
| `>` | Greater than | `SELECT * FROM Products WHERE Stock > 20;` | Mouse, Monitor |
| `<` | Less than | `SELECT * FROM Products WHERE Stock < 20;` | Laptop, Monitor |
| `>=` | Greater or equal | `SELECT * FROM Products WHERE Price >= 200;` | Laptop, Monitor |
| `<=` | Less or equal | `SELECT * FROM Products WHERE Stock <= 15;` | Laptop, Monitor |

---

## 3. Logical Operators

These are used to combine two or more conditions in a single query.

**Sample Table: `Users`**

| Name | City | Age |
| --- | --- | --- |
| John | New York | 25 |
| Sarah | London | 30 |
| Mike | New York | 20 |
| Anna | Paris | 25 |

| Operator | Description | Example Query | Result |
| --- | --- | --- | --- |
| `AND` | True if BOTH conditions are true | `SELECT * FROM Users WHERE City='New York' AND Age > 22;` | John |
| `OR` | True if AT LEAST one is true | `SELECT * FROM Users WHERE City='Paris' OR Age < 22;` | Mike, Anna |
| `NOT` | Reverse the result | `SELECT * FROM Users WHERE NOT City='New York';` | Sarah, Anna |

---

## 4. Compound Operators

Compound operators perform an arithmetic operation and assign the result back to the same column. They are typically used with `UPDATE` statements.

**Example: Give everyone a 1000 salary raise.**

```sql
UPDATE Employees 
SET Salary = Salary + 1000;
```

**Updated `Employees` Table:**

| ID | Name | Salary |
| --- | --- | --- |
| 1 | Alice | 6000 |
| 2 | Bob | 7000 |
| 3 | Charlie | 5500 |

---

## 5. Special Operators

These provide specialized tools for filtering based on ranges, lists, or pattern matching.

**Sample Table: `Students`**

| Name | Score | Grade |
| --- | --- | --- |
| Rahul | 85 | A |
| Priya | 72 | B |
| Amit | 95 | A |
| Sara | 60 | C |

| Operator | Description | Example Query | Result |
| --- | --- | --- | --- |
| `BETWEEN` | Within a range | `SELECT * FROM Students WHERE Score BETWEEN 70 AND 90;` | Rahul, Priya |
| `IN` | Match any in list | `SELECT * FROM Students WHERE Grade IN ('B', 'C');` | Priya, Sara |
| `LIKE` | Pattern matching | `SELECT * FROM Students WHERE Name LIKE 'R%';` | Rahul, Sara |
| `IS NULL` | Checks for empty values | `SELECT * FROM Students WHERE Grade IS NULL;` | (None) |
| `EXISTS` | Checks if subquery has rows | `SELECT 'Yes' WHERE EXISTS (SELECT * FROM Students WHERE Score > 90);` | Yes |

---

### Summary Table

| Category | Primary Use | Key Symbols |
| --- | --- | --- |
| **Arithmetic** | Math | `+`, `-`, `*`, `/`, `%` |
| **Comparison** | Filtering | `=`, `!=`, `>`, `<`, `>=`, `<=` |
| **Logical** | Combining Filters | `AND`, `OR`, `NOT` |
| **Compound** | Updating | `+=`, `-=`, `*=` |
| **Special** | Searching | `BETWEEN`, `IN`, `LIKE`, `IS NULL` |



###
