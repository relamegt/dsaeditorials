# Basic Operators in Relational Algebra

The relational database model organizes data using relations, which are structured collections of tuples (rows) sharing the same attributes (columns). Relational algebra is a formal procedural query language that operates on these relations, taking one or more tables as input and returning a new relation as its output.

## Procedural Query Languages and the Relational Model

In a procedural query language like relational algebra, the user instructs the system to perform a sequence of algebraic operations to retrieve the desired data. RDBMS engines compile these expressions to execute queries efficiently.

## Component Database Tables Case Study

To analyze the basic operators, we define three database tables tracking custodians, contractors, and spare parts:

### Table 1: DEVICE_SPARE

This table tracks allocated spare parts associated with serial numbers:

| SerialNumber | SparePart |
| --- | --- |
| 101 | Battery |
| 102 | Screen |
| 102 | Battery |
| 104 | Keyboard |

### Table 2: CONTRACTOR

This table lists third-party contractors and their details:

| ContractorID | CustodianName | LocationCity | ContactPhone | CustodianAge |
| --- | --- | --- | --- | --- |
| 101 | Mohit | New York | 9123456780 | 28 |
| 105 | Akash | Chicago | 9234567891 | 32 |
| 106 | Hemesh | Boston | 9345678912 | 27 |
| 104 | Abhiram | New York | 9456789123 | 30 |

### Table 3: STAFF

This table lists internal staff members and their details:

| StaffID | CustodianName | LocationCity | ContactPhone | CustodianAge |
| --- | --- | --- | --- | --- |
| 101 | Mohit | New York | 9123456780 | 28 |
| 102 | Siddu | Los Angeles | 9234512345 | 18 |
| 103 | Hemesh | Houston | 9345612345 | 20 |
| 104 | Abhiram | New York | 9456789123 | 30 |

## Detailed Analysis of Basic Operators

Relational algebra relies on six basic operators to query and modify tables:

### 1. Selection Operator (σ)

The selection operator filters rows from a relation based on a specified logical condition.

- **Syntax**: **σ(Condition)(RelationName)**
- **Operation**: Extracts staff members from `STAFF` whose age is greater than 18:

  **σ(CustodianAge &gt; 18)(STAFF)**

- **Result Table**:

| StaffID | CustodianName | LocationCity | ContactPhone | CustodianAge |
| --- | --- | --- | --- | --- |
| 101 | Mohit | New York | 9123456780 | 28 |
| 103 | Hemesh | Houston | 9345612345 | 20 |
| 104 | Abhiram | New York | 9456789123 | 30 |

### 2. Projection Operator (π)

The projection operator filters columns from a relation, returning only the specified columns and discarding all others. Duplicate rows in the output are automatically removed.

- **Syntax**: **π(Column1, Column2, ..., ColumnN)(RelationName)**
- **Operation**: Extracts unique staff IDs and names from the `STAFF` relation:

  **π(StaffID, CustodianName)(STAFF)**

- **Result Table**:

| StaffID | CustodianName |
| --- | --- |
| 101 | Mohit |
| 102 | Siddu |
| 103 | Hemesh |
| 104 | Abhiram |

### 3. Cartesian Product (×)

The Cartesian product operator combines every row of the first relation with every row of the second relation, generating all possible combinations.

- **Syntax**: **Relation1 × Relation2**
- **Operation**: Cross-joins `STAFF` (4 tuples) and `DEVICE_SPARE` (4 tuples), resulting in `4 * 4 = 16` tuples:

  **STAFF × DEVICE_SPARE**

- **Result Table**:

| StaffID | CustodianName | LocationCity | ContactPhone | CustodianAge | SerialNumber | SparePart |
| --- | --- | --- | --- | --- | --- | --- |
| 101 | Mohit | New York | 9123456780 | 28 | 101 | Battery |
| 101 | Mohit | New York | 9123456780 | 28 | 102 | Screen |
| 101 | Mohit | New York | 9123456780 | 28 | 102 | Battery |
| 101 | Mohit | New York | 9123456780 | 28 | 104 | Keyboard |
| 102 | Siddu | Los Angeles | 9234512345 | 18 | 101 | Battery |
| 102 | Siddu | Los Angeles | 9234512345 | 18 | 102 | Screen |
| 102 | Siddu | Los Angeles | 9234512345 | 18 | 102 | Battery |
| 102 | Siddu | Los Angeles | 9234512345 | 18 | 104 | Keyboard |
| 103 | Hemesh | Houston | 9345612345 | 20 | 101 | Battery |
| 103 | Hemesh | Houston | 9345612345 | 20 | 102 | Screen |
| 103 | Hemesh | Houston | 9345612345 | 20 | 102 | Battery |
| 103 | Hemesh | Houston | 9345612345 | 20 | 104 | Keyboard |
| 104 | Abhiram | New York | 9456789123 | 30 | 101 | Battery |
| 104 | Abhiram | New York | 9456789123 | 30 | 102 | Screen |
| 104 | Abhiram | New York | 9456789123 | 30 | 102 | Battery |
| 104 | Abhiram | New York | 9456789123 | 30 | 104 | Keyboard |

### 4. Union Operator (∪)

The union operator combines rows from two relations into a single result. To perform a union, both tables must be union-compatible, meaning they share the same number of attributes with matching data domains. Duplicate rows are removed.

- **Syntax**: **Relation1 ∪ Relation2**
- **Operation**: Combines `STAFF` with `CONTRACTOR` after renaming the key column to match:

  **STAFF ∪ ρ(StaffID / ContractorID)(CONTRACTOR)**

- **Result Table**:

| StaffID | CustodianName | LocationCity | ContactPhone | CustodianAge |
| --- | --- | --- | --- | --- |
| 101 | Mohit | New York | 9123456780 | 28 |
| 102 | Siddu | Los Angeles | 9234512345 | 18 |
| 103 | Hemesh | Houston | 9345612345 | 20 |
| 104 | Abhiram | New York | 9456789123 | 30 |
| 105 | Akash | Chicago | 9234567891 | 32 |
| 106 | Hemesh | Boston | 9345678912 | 27 |

### 5. Set Difference Operator (−)

The set difference operator retrieves rows that exist in the first relation but do not exist in the second. The two relations must be union-compatible.

- **Syntax**: **Relation1 − Relation2**
- **Operation**: Finds individuals who are internal staff but not contractors:

  **STAFF − ρ(StaffID / ContractorID)(CONTRACTOR)**

- **Result Table**:

| StaffID | CustodianName | LocationCity | ContactPhone | CustodianAge |
| --- | --- | --- | --- | --- |
| 102 | Siddu | Los Angeles | 9234512345 | 18 |
| 103 | Hemesh | Houston | 9345612345 | 20 |

### 6. Rename Operator (ρ)

The rename operator applies a temporary label to a relation or its columns to prevent name conflicts.

- **Syntax**: **ρ(NewRelationName, OriginalRelation)**
- **Operation**: Renames `STAFF` to `STAFF1`:

  **ρ(STAFF1, STAFF)**

To project specific columns and rename the resulting table:
**ρ(STAFF_NAMES, π(StaffID, CustodianName)(STAFF))**

## Basic Relational Algebra Operators Summary

| Operator | Notation | Input Type | Output Objective |
| --- | --- | --- | --- |
| **Selection** | σ | Unary | Filters rows matching a specific logical condition |
| **Projection** | π | Unary | Retrieves specific columns and removes duplicate rows |
| **Cartesian Product** | × | Binary | Generates all possible combinations of rows |
| **Union** | ∪ | Binary | Combines rows from two union-compatible relations |
| **Set Difference** | − | Binary | Returns rows in the first table that are missing from the second |
| **Rename** | ρ | Unary | Re-labels relations or attributes temporarily |

# Summary

Basic operators in relational algebra provide the fundamental tools needed to query and manipulate relational tables in a DBMS. Through unary operations like selection and projection, developers filter rows and columns to focus on specific records, while binary operations like Cartesian product, union, and set difference combine or exclude rows across tables. These basic operations are combined to build advanced query processes, ensuring that database management engines can execute declarative commands while preserving data consistency.




