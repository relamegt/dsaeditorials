# Inner Join vs Outer Join

In relational database systems, a Join is an SQL operation used to combine rows from two or more tables based on a related column between them. Joins link data stored across normalized relations, allowing users to query and retrieve meaningful information from the database. The two primary categories of joins are Inner Join and Outer Join.

## Principles of Relational Joins

When databases are normalized, columns are distributed into separate tables to minimize redundancy. To query across these boundaries, SQL joins use matching key fields (typically primary keys and foreign keys) to temporarily consolidate records.

## Component Database Tables Case Study

To analyze joins, we define two database tables tracking custodians and device allocations:

### Table 1: CUSTODIAN

| CustodianID | CustodianName | CustodianAge |
| --- | --- | --- |
| 101 | Mohit | 28 |
| 102 | Akash | 32 |
| 103 | Hemesh | 27 |
| 104 | Abhiram | 30 |
| 105 | Siddu | 22 |

### Table 2: ALLOCATION

| AllocationID | CustodianID | DeviceModel |
| --- | --- | --- |
| 1 | 101 | RouterA |
| 2 | 101 | SwitchB |
| 3 | 102 | RouterA |
| 4 | 103 | FirewallC |
| 5 | 106 | ServerD |

In this dataset, custodians `104` (**Abhiram**) and `105` (**Siddu**) have no devices allocated, and device allocation `5` (`ServerD`) is associated with `CustodianID` `106` (which does not exist in the `CUSTODIAN` table).

## The Inner Join Operation

An Inner Join returns only the matching rows between two tables based on a specified join condition. If a row in the first table does not have a corresponding match in the second table, it is completely excluded from the result set.

### Syntax

```Sql
SELECT Table1.Column1, Table2.Column2
FROM Table1
INNER JOIN Table2
ON Table1.CommonColumn = Table2.CommonColumn;
```

### Case Study Query

The following query retrieves the names of custodians and the device models allocated to them:

```Sql
SELECT CUSTODIAN.CustodianName, ALLOCATION.DeviceModel
FROM CUSTODIAN
INNER JOIN ALLOCATION
ON CUSTODIAN.CustodianID = ALLOCATION.CustodianID;
```

### Result Table

- **Mohit** appears twice since he has two allocations.
- **Akash** and **Hemesh** appear once.
- **Abhiram**, **Siddu**, and **ServerD** are excluded because they do not have matching rows in both tables.

| CustodianName | DeviceModel |
| --- | --- |
| Mohit | RouterA |
| Mohit | SwitchB |
| Akash | RouterA |
| Hemesh | FirewallC |

## The Outer Join Operation

An Outer Join returns all matching rows from both tables, plus the non-matching rows from one or both tables. When a row has no match in the opposing table, the query fills those missing columns with `NULL` values. Outer joins are divided into Left, Right, and Full Joins:

### 1. Left Outer Join

A Left Outer Join returns all rows from the left table and the matching rows from the right table. If a row in the left table has no match on the right, the right table's columns in the result set contain `NULL`.

#### Case Study Query

```Sql
SELECT CUSTODIAN.CustodianName, ALLOCATION.DeviceModel
FROM CUSTODIAN
LEFT JOIN ALLOCATION
ON CUSTODIAN.CustodianID = ALLOCATION.CustodianID;
```

#### Result Table

- Includes all custodians.
- **Abhiram** (104) and **Siddu** (105) are included in the output, with `NULL` for the `DeviceModel` column since they have no device allocations.
- **ServerD** is excluded.

| CustodianName | DeviceModel |
| --- | --- |
| Mohit | RouterA |
| Mohit | SwitchB |
| Akash | RouterA |
| Hemesh | FirewallC |
| Abhiram | NULL |
| Siddu | NULL |

### 2. Right Outer Join

A Right Outer Join returns all rows from the right table and the matching rows from the left table. If a row in the right table has no match on the left, the left table's columns in the result set contain `NULL`.

#### Case Study Query

```Sql
SELECT CUSTODIAN.CustodianName, ALLOCATION.DeviceModel
FROM CUSTODIAN
RIGHT JOIN ALLOCATION
ON CUSTODIAN.CustodianID = ALLOCATION.CustodianID;
```

#### Result Table

- Includes all device allocations.
- **ServerD** is included, with `NULL` for the `CustodianName` column because its `CustodianID` (106) does not match any custodian.
- **Abhiram** and **Siddu** are excluded.

| CustodianName | DeviceModel |
| --- | --- |
| Mohit | RouterA |
| Mohit | SwitchB |
| Akash | RouterA |
| Hemesh | FirewallC |
| NULL | ServerD |

### 3. Full Outer Join

A Full Outer Join combines the results of both the Left and Right Outer Joins, returning all rows from both tables. When a match is missing, the corresponding columns contain `NULL`.

#### Case Study Query

```Sql
SELECT CUSTODIAN.CustodianName, ALLOCATION.DeviceModel
FROM CUSTODIAN
FULL JOIN ALLOCATION
ON CUSTODIAN.CustodianID = ALLOCATION.CustodianID;
```

#### Result Table

- Includes all custodians and all allocations.
- Both **Abhiram** and **Siddu** (with `NULL` device) and **ServerD** (with `NULL` custodian) are preserved.

| CustodianName | DeviceModel |
| --- | --- |
| Mohit | RouterA |
| Mohit | SwitchB |
| Akash | RouterA |
| Hemesh | FirewallC |
| Abhiram | NULL |
| Siddu | NULL |
| NULL | ServerD |

## Evaluation of Join Performance and Trade-Offs

Choosing the appropriate join category requires balancing transaction accuracy and speed:

### Inner Join Trade-Offs

- **Advantages**:
- *Data Consistency*: Excludes unmatched records, preventing `NULL` value complications.
- *Performance Speed*: Database engines process matched rows faster than unmatched sets.
- *Reduced Duplicate Data*: Avoids unnecessary repeating rows.
- **Disadvantages**:
- *Possible Data Loss*: Unmatched rows are completely ignored, which may hide incomplete entries.

### Outer Join Trade-Offs

- **Advantages**:
- *Complete Data Retrieval*: Preserves all records from target tables, preventing information loss.
- *Data Quality Auditing*: Quickly identifies orphaned child records or missing associations.
- **Disadvantages**:
- *Query Latency*: Scanning and organizing unmatched rows with `NULL` fields increases query processing times.
- *Data Duplication*: Can cause row proliferation when tables have multiple matching columns.

## Comparison of Inner Join and Outer Join

| Feature | Inner Join | Outer Join |
| --- | --- | --- |
| **Row Matching Rule** | Only returns rows with matching values in both tables | Returns matching rows plus unmatched rows from one or both tables |
| **Handling of Unmatched Data** | Filters out and discards unmatched records | Preserves unmatched records, inserting `NULL` values |
| **Subtypes Available** | Single standard inner matching type | Three types: Left Outer Join, Right Outer Join, Full Outer Join |
| **Query Performance** | Faster execution (processes matching rows only) | Slower execution (requires additional table scans for NULLs) |

# Summary

SQL Joins combine rows from two or more tables based on common matching columns. An Inner Join retrieves only the matching tuples from both tables, discarding unmatched data to optimize query performance and reduce redundancy. In contrast, Outer Joins preserve all records from one or both relations, using Left, Right, or Full Join variations to populate missing columns with NULL values when matches are absent. Relational databases use Inner Joins for fast matching lookups, while Outer Joins are preferred for data auditing and reporting where no information should be omitted.




