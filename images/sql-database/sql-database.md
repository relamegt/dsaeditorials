# SQL Database

In the world of data management, handling databases efficiently requires a precise understanding of how to manipulate the environment. This guide explores the fundamental commands used to manage databases and their contents.

## Quick Reference Matrix

| Command | Category | Primary Function | Criticality Level |
| --- | --- | --- | --- |
| **CREATE** | DDL | Establishes a new database or table. | Low |
| **USE** | Session | Sets the active database for the current session. | None |
| **SELECT** | DQL | Retrieves and views data from tables. | None |
| **ALTER/RENAME** | DDL | Changes the name of an existing database. | Medium |
| **DROP** | DDL | Permanently deletes a database and all data. | **High** |

---

## 1. Establishing the Foundation: CREATE DATABASE

The `CREATE DATABASE` statement is the first step in any project. It creates a logical container that can hold tables, views, and stored procedures.

### Syntax

```sql
CREATE DATABASE database_name;
-- Best practice: Use IF NOT EXISTS to prevent errors
CREATE DATABASE IF NOT EXISTS database_name;
```

### Example

```sql
CREATE DATABASE AlphaKnowledge;
```

**Output:**

> `Query OK, Database 'AlphaKnowledge' created.`

---

## 2. Setting the Context: USE

Before you can create tables, you must tell the system which database you want to work with. The `USE` command sets the active context for your current session.

### Syntax

```sql
USE database_name;
```

### Example

```sql
USE AlphaKnowledge;
```

**Output:**

> `Database changed.`

---

## 3. Data Retrieval: SELECT

Once your database is populated data, the `SELECT` command is the most powerful tool in your analytical arsenal. It allows you to extract specific information from tables without altering the underlying data.

### A. Retrieving All Data

Using the asterisk (`*`) wildcard fetches every column and every row in a table.

```sql
SELECT * FROM Employees;
```

### B. Retrieving Specific Columns

To improve performance and readability, it is best to select only the columns you actually need.

```sql
SELECT Name, Salary FROM Employees;
```

**Example Output:**

| Name | Salary |
| --- | --- |
| Alice Vance | 95000 |
| Bob Smith | 72000 |
| Charlie Day | 85000 |

---

## 4. Structural Evolution: RENAME / ALTER

Requirements often change. If a database needs to be renamed for clarity or organizational standards, use the `ALTER` command (specifically in SQL Server).

### Syntax (SQL Server Standard)

```sql
ALTER DATABASE old_name MODIFY NAME = new_name;
```

### Example

```sql
ALTER DATABASE AlphaKnowledge MODIFY NAME = KnowledgeBase;
```

**Output:**

> `Commands OK, 0 rows affected. (Database renamed successfully)`

---

## 5. The Final Action: DROP

The `DROP` command is irreversible. It removes the database structure, all associated tables, and all stored data from the system. **Use this command with extreme caution.**

### Syntax

```sql
DROP DATABASE database_name;
-- Safety-first approach: Use IF EXISTS to avoid errors if the DB is already gone
DROP DATABASE IF EXISTS database_name;
```

### Example

```sql
DROP DATABASE KnowledgeBase;
```

**Output:**

> `Query OK, 0 rows affected. (Database 'KnowledgeBase' dropped)`



###
