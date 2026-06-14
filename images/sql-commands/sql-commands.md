# SQL Commands

SQL commands are the fundamental building blocks used to interact with databases. They allow you to create structures, manage data, and control security. 

Before diving into the command types, understand these basic terms:

- **Database:** An organized collection of data.
- **Table:** Data stored in rows and columns.
- **Row (Record):** A single entry in a table.
- **Column (Field):** A specific attribute or property of the data.
- **Primary Key:** A unique identifier for each record.
- **Constraint:** A rule applied to data to ensure its accuracy.

SQL commands are categorized into five main groups:

![SQL Commands](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/mastering-sql-commands-a-complete-guide/1781438516356-ccommands.png)

---

## 1. DDL (Data Definition Language)

DDL commands are used to define, alter, or delete the **structure** of the database (tables, indexes, and schemas).

| Command | Description | Syntax |
| --- | --- | --- |
| **CREATE** | Creates a new table or index. | `CREATE TABLE table_name (...);` |
| **DROP** | Deletes an entire table object. | `DROP TABLE table_name;` |
| **ALTER** | Changes the structure of an existing table. | `ALTER TABLE table_name ADD...` |
| **TRUNCATE** | Removes all records from a table but keeps the structure. | `TRUNCATE TABLE table_name;` |
| **COMMENT** | Adds descriptions to the data dictionary. | `COMMENT ON table_name IS '...';` |
| **RENAME** | Renames an existing object. | `RENAME TABLE old TO new;` |

**Example:**

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50),
    hire_date DATE
);
```

*This creates a new table called "Employees" to hold information for our team.*

---

## 2. DQL (Data Query Language)

DQL is used to fetch and retrieve data from the database. The primary command is **SELECT**.

| Command/Clause | Description | Syntax/Usage |
| --- | --- | --- |
| **SELECT** | Retrieves specific columns from the database. | `SELECT col1, col2` |
| **FROM** | Specifies the table to retrieve data from. | `FROM table_name` |
| **WHERE** | Filters rows before grouping occurs. | `WHERE condition` |
| **GROUP BY** | Groups rows that have the same values. | `GROUP BY column_name` |
| **HAVING** | Filters results created by GROUP BY. | `HAVING condition` |
| **DISTINCT** | Removes duplicate rows from the result set. | `SELECT DISTINCT col1` |
| **ORDER BY** | Sorts the result set (ASC or DESC). | `ORDER BY col1 DESC` |
| **LIMIT** | Restricts the number of rows returned. | `LIMIT number` |

**Example:**

```sql
SELECT first_name, last_name, hire_date
FROM Employees
WHERE department = 'Sales'
ORDER BY hire_date DESC;
```

*This retrieves the names and hire dates of everyone in Sales, showing the newest first.*

---

## 3. DML (Data Manipulation Language)

DML commands are used to manage the **data stored inside** the tables. You use these to add, update, or delete records.

| Command | Description | Syntax |
| --- | --- | --- |
| **INSERT** | Adds new records to a table. | `INSERT INTO table (cols) VALUES (vals);` |
| **UPDATE** | Modifies existing data within a table. | `UPDATE table SET col=val WHERE;` |
| **DELETE** | Removes specific records from a table. | `DELETE FROM table WHERE cond;` |

**Example:**

```sql
INSERT INTO Employees (first_name, last_name, department) 
VALUES ('Akash', 'Dangudubiyyapu', 'Sales');

INSERT INTO Employees (first_name, last_name, department) 
VALUES ('Mohit', 'Chandaluri', 'IT');

INSERT INTO Employees (first_name, last_name, department) 
VALUES ('Abhiram', 'Gopisetty', 'HR');
```

---

## 4. DCL (Data Control Language)

DCL deals with **security and permissions**. These commands control who is allowed to access the data.

| Command | Description | Syntax |
| --- | --- | --- |
| **GRANT** | Assigns new privileges to a user. | `GRANT privilege ON table TO user;` |
| **REVOKE** | Takes away previously granted privileges. | `REVOKE privilege ON table FROM user;` |

**Example:**

```sql
GRANT SELECT, UPDATE ON Employees TO Mohit_Chandaluri;
```

*This gives Mohit permission to view and update records in the Employees table.*

---

## 5. TCL (Transaction Control Language)

TCL groups a set of tasks into a single execution unit. If one part of the group fails, the whole transaction fails.

| Command | Description | Syntax |
| --- | --- | --- |
| **BEGIN** | Starts a new transaction. | `BEGIN TRANSACTION;` |
| **COMMIT** | Saves all changes made during the transaction. | `COMMIT;` |
| **ROLLBACK** | Undoes changes if an error occurs. | `ROLLBACK;` |
| **SAVEPOINT** | Creates a point to return to later. | `SAVEPOINT point_name;` |

**Example:**

```sql
BEGIN TRANSACTION;

-- Update Akash's department
UPDATE Employees SET department = 'Marketing' WHERE first_name = 'Akash';

-- Create a checkpoint
SAVEPOINT before_update;

-- Try to update Abhiram's department
UPDATE Employees SET department = 'IT' WHERE first_name = 'Abhiram';

-- If we made a mistake, go back to the checkpoint
ROLLBACK TO before_update;

-- If everything looks good, save the Akash update permanently
COMMIT;
```



###
