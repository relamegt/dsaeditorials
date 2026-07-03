# SQL Queries on Clustered and Non-Clustered Indexes

In relational database systems, SQL indexes optimize data retrieval by allowing the query processor to locate records without performing a slow, resource-intensive full-table scan. Database engines use two primary index types to accelerate search and join operations: Clustered Index and Non-Clustered Index.

## Principles of SQL Indexing

An index functions similarly to the index section at the back of a reference manual. By storing selected key columns alongside pointer addresses, the query optimizer can jump directly to targeted disk blocks, minimizing physical disk I/O.

## Clustered Indexing in SQL

A clustered index determines the physical storage order of a table's data rows on disk. Data is physically stored in the sorted order of the indexed column(s). Because a table's records can only be stored in a single physical sequence, each table is restricted to exactly one clustered index. By default, defining a primary key automatically creates a clustered index on that column.

### Database Table Creation and Default Clustered Index

We create a custom database table `DeviceRegistry` using the primary key `DeviceID` to enforce a default clustered index:

```Sql
CREATE TABLE DeviceRegistry
(
DeviceID INT PRIMARY KEY,
CustodianName VARCHAR(50),
DepartmentName VARCHAR(50)
);

INSERT INTO DeviceRegistry (DeviceID, CustodianName, DepartmentName) VALUES
(103, 'Hemesh', 'Security'),
(102, 'Akash', 'Support'),
(101, 'Mohit', 'Research');

SELECT * FROM DeviceRegistry;
```

#### Result Table
Even though data was inserted in a different order, the default clustered index physically sorts the table by the primary key:

| DeviceID | CustodianName | DepartmentName |
| --- | --- | --- |
| 101 | Mohit | Research |
| 102 | Akash | Support |
| 103 | Hemesh | Security |

### Dropping and Re-creating Clustered Indexes

To create a clustered index on a different column (e.g., sorting the table alphabetically by custodian name), we must first drop the primary key constraint or the pre-existing clustered index:

```Sql
-- Drop existing clustered index (assuming index name is PK_DeviceRegistry)
ALTER TABLE DeviceRegistry DROP CONSTRAINT PK_DeviceRegistry;

-- Create custom clustered index on CustodianName
CREATE CLUSTERED INDEX IX_DeviceRegistry_CustodianName
ON DeviceRegistry (CustodianName ASC);
```

## Non-Clustered Indexing in SQL

A non-clustered index is stored in a separate physical structure from the actual table data. It contains selected column keys and virtual pointer addresses (or row locators) referencing the actual data rows. This separate layout is similar to a book's table of contents, which lists topics and page numbers without changing the physical text layout of the pages.

### Database Table Creation without Primary Key

We create the table without a primary key so that no default clustered index is applied:

```Sql
CREATE TABLE DeviceRegistry
(
DeviceID INT,
CustodianName VARCHAR(50),
DepartmentName VARCHAR(50)
);

INSERT INTO DeviceRegistry (DeviceID, CustodianName, DepartmentName) VALUES
(103, 'Hemesh', 'Security'),
(102, 'Akash', 'Support'),
(101, 'Mohit', 'Research');

SELECT * FROM DeviceRegistry;
```

#### Result Table
Without a clustered index, rows are stored on disk in their insertion sequence:

| DeviceID | CustodianName | DepartmentName |
| --- | --- | --- |
| 103 | Hemesh | Security |
| 102 | Akash | Support |
| 101 | Mohit | Research |

### Creating Non-Clustered Index

We create a non-clustered index on the `CustodianName` column to speed up name searches:

```Sql
CREATE NONCLUSTERED INDEX IX_DeviceRegistry_CustodianName
ON DeviceRegistry (CustodianName ASC);
```

#### Index Output Mapping
The index structure stores sorted keys alongside their logical physical addresses:

| CustodianName | RowAddress |
| --- | --- |
| Akash | Row 2 |
| Hemesh | Row 1 |
| Mohit | Row 3 |

## Query Optimization and Execution Scenarios

We analyze execution mechanics under different indexing configurations:

### 1. SELECT Queries with WHERE Clauses

- **Clustered Index**: When querying the primary key, the engine uses the clustered index to jump directly to the target block:

`````Sql
SELECT *
  FROM DeviceRegistry
  WHERE DeviceID = 102;
```

*Result*: Returns Akash's record quickly with minimal disk reads.

- **Non-Clustered Index**: If we query by name after creating the non-clustered index:

`````Sql
SELECT *
  FROM DeviceRegistry
  WHERE CustodianName = 'Mohit';
```

*Result*: The engine scans the index file, locates Mohit, extracts `Row 3`, and reads the third row from the primary table.

### 2. UPDATE Queries

- **Clustered Index**: Updating a non-indexed attribute (e.g., department location) for a specific ID is highly efficient because the database quickly locates the target record using the clustered key:

`````Sql
UPDATE DeviceRegistry
  SET DepartmentName = 'Operations'
  WHERE DeviceID = 103;
```

- **Non-Clustered Index**: If the update modifies a column that is part of a non-clustered index, the engine must write the update to the primary table and update the sorted index file, adding execution overhead:

`````Sql
UPDATE DeviceRegistry
  SET CustodianName = 'H. Agarwal'
  WHERE DeviceID = 101;
```

### 3. JOIN Queries

- **Clustered Index**: When joining two tables, using a clustered index on the join columns allows the query engine to perform efficient merge joins:

`````Sql
-- Create secondary join table
  CREATE TABLE DepotAllocation (
      DeviceID INT,
      DepotName VARCHAR(50)
  );

  INSERT INTO DepotAllocation VALUES
  (101, 'DepotAlpha'),
  (102, 'DepotBeta'),
  (103, 'DepotGamma');

  -- Join query
  SELECT r.DeviceID, r.CustodianName, d.DepotName
  FROM DeviceRegistry r
  JOIN DepotAllocation d
  ON r.DeviceID = d.DeviceID;
```

*Result*: Using the clustered index on `DeviceID` accelerates the match speed.

## Comparison of Clustered and Non-Clustered Indexes

| Aspect | Clustered Index | Non-Clustered Index |
| --- | --- | --- |
| **Data Storage Order** | Dictates the physical sort order of data rows on disk | Does not alter the physical storage order of the data |
| **Max Indexes Allowed** | Exactly one per table | Multiple indexes (e.g., 999+ in SQL Server) |
| **Index Structure** | The index is the table itself (data stored in leaf blocks) | Stored as a separate file containing pointers to data rows |
| **Query Performance** | Faster for range queries and sorting scans | Faster for point lookups on specific non-primary columns |
| **Primary Key Relationship** | Automatically created on primary keys by default | Created on any column, independent of key status |
| **Design Flexibility** | Low (constrained by a single sorting path) | High (can build multiple indexes to optimize queries) |

> !NOTE: The primary difference between clustered and non-clustered indexes lies in their physical storage design. A clustered index is the table itself, physically sorting the actual data rows on disk. A non-clustered index is a separate index file containing sorted key values and virtual pointer addresses that map to the unsorted table rows.

# Summary

Clustered and non-clustered indexes are critical tools used to optimize SQL queries and minimize disk I/O. A clustered index defines the physical sorting sequence of data rows on disk, making it ideal for primary keys and range scans. A non-clustered index maintains a separate logical file of keys and row pointers, allowing databases to support multiple indexes on non-primary columns to speed up point lookups. Choosing between these indexing types requires balancing database write overhead against the search requirements of select, update, and join statements.




