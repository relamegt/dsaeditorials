# SQL Comments

This is where **SQL Comments** come in. Comments are notes you leave inside your code that the database engine completely ignores. They are for humans (you and your teammates), making the code easier to read, maintain, and debug.

---

## 1. Single-Line Comments

Shorter-line comments are best for quick notes. In SQL, you start these comments with a double dash (`--`). Everything written after the dashes on that specific line will be ignored by the database.

**Syntax:**
`-- Your comment here`

**Example:**

```sql
SELECT * FROM Students; -- This query fetches all records from the students table
SELECT name FROM Students WHERE grade = 'A'; -- Only get top performing students
```

---

## 2. Multi-Line Comments

If you need to write a long explanation or want to comment out a large block of code, multi-line comments are the solution. You start with `/*` and end with `*/`. 

**Syntax:**

```sql
/* 
This is a multi-line comment.
It can span across many lines
as you need. 
*/
```

**Example:**

```sql
/* 
The following query calculates the total 
sales for the year 2023 and filters 
by the North region.
*/
SELECT SUM(amount) FROM Sales WHERE year = 2023;
```

---

## 3. In-Line Comments

In-line comments are used when you want to place a note right in the middle of a SQL statement. This is incredibly helpful for "disabling" a specific part of a query while testing without deleting it.

**Syntax:**
`/* comment */`

**Example:**

```sql
SELECT student_name, /* age, */ email 
FROM Students;
-- In this example, the age column is temporarily ignored.
```

---

## Quick Reference Table

| Comment Type | Syntax | Best Used For |
| --- | --- | --- |
| **Single-Line** | `--` | Quick notes on one line of code. |
| **Multi-Line** | `/* ... */` | Long explanations or disabling blocks of code. |
| **In-Line** | `/* ... */` | Adding notes inside the middle of a query. |

---

## Why are comments important?

1. **Readability:** It helps others understand your logic.
2. **Maintenance:** It helps "future self" remember why a specific filter or join was used later.
3. **Debugging:** You can quickly "comment out" lines of code to find which specific part is causing an error.



###
