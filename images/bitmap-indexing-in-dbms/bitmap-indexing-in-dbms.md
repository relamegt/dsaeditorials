# Bitmap Indexing in DBMS

Bitmap indexing is a database indexing technique designed to optimize read-heavy queries on columns containing only a few unique values (known as low-cardinality columns). Instead of storing full column values or row locator pointers, bitmap indexing uses arrays of bits (1s and 0s) to map data rows to their corresponding column values, enabling query processors to resolve filters using fast bitwise operations.

## Principles of Bitmap Indexing

In database tables containing columns with low cardinality (such as `Gender`, `Region`, or `Status`), traditional indexes (like B+ Trees) can be highly inefficient due to duplicate values. Bitmap indexing solves this by creating a separate bit vector (bitmap) for each unique key value. In these vectors, the bit at position `i` is set to `1` if the `i-th` row of the table matches the key value, and `0` otherwise.

## Mechanics of Bitmap Operations

When queries apply boolean filters (such as `AND`, `OR`, or `NOT`), the database engine retrieves the matching bitmaps and executes bitwise logical operations directly in memory. Since hardware processors run bitwise operations (like logical AND/OR) in a single instruction cycle, bitmap indexing provides extremely fast query execution times.

## Database Table Case Study

Consider a device registry database with five rows tracking warranty status and hardware categories:

### Table: DeviceRegistry

| RowNumber | CustodianName | IsWarrantyActive | DeviceType |
| --- | --- | --- | --- |
| 1 | Mohit | Yes | Router |
| 2 | Akash | No | Switch |
| 3 | Hemesh | No | Router |
| 4 | Abhiram | Yes | Firewall |
| 5 | Siddu | No | Switch |

We construct bitmap indexes for both low-cardinality columns:

### Bitmap Indexes for IsWarrantyActive

Since this column has only two unique values (`Yes` and `No`), the index creates two 5-bit vectors:

- **Yes** = `10010` (indicating Row 1 and Row 4 are active)
- **No** = `01101` (indicating Rows 2, 3, and 5 are inactive)

### Bitmap Indexes for DeviceType

This column has three unique values (`Router`, `Switch`, and `Firewall`), resulting in three 5-bit vectors:

- **Router** = `10100` (indicating Row 1 and Row 3 contain routers)
- **Switch** = `01001` (indicating Row 2 and Row 5 contain switches)
- **Firewall** = `00010` (indicating Row 4 contains a firewall)

## Query Execution Using Bitwise Operations

Suppose we want to find all devices where the warranty is inactive and the device type is a switch:

### The Query Scenario

```Sql
SELECT *
FROM DeviceRegistry
WHERE IsWarrantyActive = 'No' AND DeviceType = 'Switch';
```

### Execution Path and Logical AND

1. The database engine retrieves the bitmap for `IsWarrantyActive = 'No'`: **01101**.
2. The engine retrieves the bitmap for `DeviceType = 'Switch'`: **01001**.
3. It performs a bitwise AND operation on the two bit vectors:

- **01101** (Warranty = No)
- **AND 01001** (DeviceType = Switch)
- **= 01001** (Result Vector)

1. The result vector **01001** indicates that Row 2 (**Akash**) and Row 5 (**Siddu**) satisfy both conditions, and the database engine retrieves only those two records.

## Creating a Bitmap Index in SQL

Relational database systems that support bitmap indexing (such as Oracle) use the following syntax to create indexes:

```Sql
CREATE BITMAP INDEX Index_Name
ON Table_Name (Column_Name);
```

To create a bitmap index on the `IsWarrantyActive` column of our case study table:

```Sql
CREATE BITMAP INDEX index_IsWarrantyActive
ON DeviceRegistry (IsWarrantyActive);
```

## Performance Trade-Offs of Bitmap Indexing

Adopting bitmap indexing requires balancing search speed on low-cardinality fields against write locks:

### Advantages of Bitmap Indexing

- **Boolean Processing Speed**: Bitwise operations run directly in CPU registers, enabling rapid query execution.
- **Low Storage Overhead**: Bit vectors require significantly less disk storage compared to bulk pointer-based B+ Trees.
- **Efficient Joins**: Simplifies joining tables in star schemas (common in data warehouses).

### Disadvantages of Bitmap Indexing

- **Write Lock Contention**: Modifying a record requires locking the entire bitmap block, which blocks concurrent write operations on other rows.
- **Inefficient for High Cardinality**: Columns with many unique values (e.g., primary keys or phone numbers) generate too many bitmaps, causing high storage overhead.
- **Poor Update Suitability**: Inserting or updating records requires re-indexing the bit vectors, which degrades performance in transaction-heavy OLTP databases.

## Comparison of B+ Tree and Bitmap Indexing

| Feature | B+ Tree Indexing | Bitmap Indexing |
| --- | --- | --- |
| **Column Cardinality** | High-cardinality columns (many unique values like Primary Keys) | Low-cardinality columns (few unique values like Gender or Status) |
| **Storage Consumption** | High (stores key values and row pointer addresses) | Low (stores compact binary strings) |
| **Write Performance** | High (supports fast inserts/updates without block locks) | Low (modifying a row locks the entire bitmap vector block) |
| **Logical Query Speed** | Slower (requires traversing tree branches) | Extremely fast (resolves filters via hardware bitwise AND/OR) |
| **Best-Fit Databases** | Transaction-heavy OLTP systems | Analytical data warehouses (OLAP) |

> *!NOTE:* The primary trade-off of bitmap indexing is write concurrency versus read speed. While bitmap indexes are highly space-efficient and provide fast query execution for read-heavy data warehouses, they suffer from high write lock contention, making them unsuitable for transaction-heavy OLTP systems.

# Summary

Bitmap indexing optimizes query performance in database management systems by using binary bit vectors to index low-cardinality columns. By mapping table records to arrays of 1s and 0s, the query engine can resolve complex boolean search criteria using fast, CPU-level bitwise operations. While this approach minimizes storage footprints and accelerates data reads, updates can cause write lock contention, making bitmap indexing best suited for read-heavy OLAP systems rather than write-heavy OLTP relational databases.




