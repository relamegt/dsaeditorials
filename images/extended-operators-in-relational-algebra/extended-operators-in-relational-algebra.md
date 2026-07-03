# Extended Operators in Relational Algebra

Extended operators in relational algebra are derived operations that go beyond the basic fundamental set of relational operations. They are called derived operators because they do not add new expressive power to the language; instead, they are constructed from combinations of basic operators (such as selection, projection, and Cartesian product) to simplify complex database queries.

## Principles of Derived Relational Algebra Operations

By combining basic operations, derived operators allow database administrators to express complex relationships — such as matching keys, calculating common intersections, or evaluating universal sets — in a compact, readable algebraic notation.

## Component Database Tables Case Study

To analyze the extended operators, we define a device custodian registry schema:

### Table R: REGISTRY

This table tracks allocated device IDs and custodian names:

| DeviceID | CustodianName |
| --- | --- |
| 1 | Mohit |
| 2 | Akash |
| 3 | Hemesh |

### Table S: SPECIFICATIONS

This table tracks spec allocations by custodian:

| CustodianName | SpecCode |
| --- | --- |
| Mohit | S10 |
| Akash | S20 |
| Siddu | S30 |

## Join Operators

Join operators combine data from two or more relations based on matching attribute values, allowing users to query related tables. Joins are divided into Inner Joins and Outer Joins.

### 1. Inner Join

An inner join combines rows from two tables only when their attributes satisfy a matching condition. Unmatched rows on either side are discarded.

#### 1.1 Conditional Join (⋈θ)
A conditional join (or Theta join) combines rows based on a comparison condition (using operators like `=`, `>`, `<`, or `≠`).

- **Operation**: Join `REGISTRY` and `SPECIFICATIONS` where the names match and the `DeviceID` is greater than 1:

  **REGISTRY ⋈ (REGISTRY.CustodianName = SPECIFICATIONS.CustodianName ∧ REGISTRY.DeviceID &gt; 1) SPECIFICATIONS**

- **Result Table**:

| DeviceID | REGISTRY.CustodianName | SPECIFICATIONS.CustodianName | SpecCode |
| --- | --- | --- | --- |
| 2 | Akash | Akash | S20 |

#### 1.2 Equi Join
An equi join is a subset of conditional join where the comparison condition is strictly equality (`=`). Since the join columns are identical, the output displays the matching column values.

- **Operation**: Join `REGISTRY` and `SPECIFICATIONS` on Custodian Name equality:

  **REGISTRY ⋈ (REGISTRY.CustodianName = SPECIFICATIONS.CustodianName) SPECIFICATIONS**

- **Result Table**:

| DeviceID | REGISTRY.CustodianName | SPECIFICATIONS.CustodianName | SpecCode |
| --- | --- | --- | --- |
| 1 | Mohit | Mohit | S10 |
| 2 | Akash | Akash | S20 |

#### 1.3 Natural Join (⋈)
A natural join automatically matches tables based on columns with identical names and data types, removing duplicate matching columns from the result.

- **Operation**: Natural join `REGISTRY` and `SPECIFICATIONS` on the common attribute `CustodianName`:

  **REGISTRY ⋈ SPECIFICATIONS**

- **Result Table**:

| DeviceID | CustodianName | SpecCode |
| --- | --- | --- |
| 1 | Mohit | S10 |
| 2 | Akash | S20 |

### 2. Outer Join

An outer join returns all records from one or both tables even if no matching row exists in the opposing table, filling missing columns with `NULL` placeholders.

#### 2.1 Left Outer Join (⟕)
A left outer join returns all rows from the left table and the matching rows from the right table. If no match is found, the right table's attributes contain `NULL`.

- **Operation**: Left join `REGISTRY` and `SPECIFICATIONS` on Custodian Name:

  **REGISTRY ⟕ SPECIFICATIONS**

### **Result Table:**

| DeviceID | REGISTRY.CustodianName | SPECIFICATIONS.CustodianName | SpecCode |
| --- | --- | --- | --- |
| 1 | Mohit | Mohit | S10 |
| 2 | Akash | Akash | S20 |
| 3 | Hemesh | NULL | NULL |

#### 2.2 Right Outer Join (⟖)
A right outer join returns all rows from the right table and the matching rows from the left table. If no match is found, the left table's attributes contain `NULL`.

- **Operation**: Right join `REGISTRY` and `SPECIFICATIONS` on Custodian Name:

  **REGISTRY ⟖ SPECIFICATIONS**

- **Result Table**:

| DeviceID | REGISTRY.CustodianName | SPECIFICATIONS.CustodianName | SpecCode |
| --- | --- | --- | --- |
| 1 | Mohit | Mohit | S10 |
| 2 | Akash | Akash | S20 |
| NULL | NULL | Siddu | S30 |

#### 2.3 Full Outer Join (⟗)
A full outer join returns all records when there is a match in either the left or right table, filling missing attributes on both sides with `NULL` where matches are absent.

- **Operation**: Full join `REGISTRY` and `SPECIFICATIONS` on Custodian Name:

  **REGISTRY ⟗ SPECIFICATIONS**

- **Result Table**:

| DeviceID | REGISTRY.CustodianName | SPECIFICATIONS.CustodianName | SpecCode |
| --- | --- | --- | --- |
| 1 | Mohit | Mohit | S10 |
| 2 | Akash | Akash | S20 |
| 3 | Hemesh | NULL | NULL |
| NULL | NULL | Siddu | S30 |

## Set Intersection (∩)

The set intersection operator retrieves only the rows that are present in both tables. To perform an intersection, the two relations must be union-compatible.

### Table: TEAM_A

- 1, Mohit
- 2, Akash
- 3, Hemesh

### Table: TEAM_B

- 1, Mohit
- 2, Akash
- **Operation**: Find the students common to both teams:

  `TEAM_A ∩ TEAM_B` 

- **Result Table**:

| DeviceID | CustodianName |
| --- | --- |
| 1 | Mohit |
| 2 | Akash |

## Division Operator (÷)

The division operator is used to solve "for all" queries, identifying rows in a dividend table that are associated with all rows in a divisor table. The divisor's attributes must be a proper subset of the dividend's attributes.

### Table: DEPLOYMENTS

This table tracks device deployments to custodians:

| DeviceID | CustodianName |
| --- | --- |
| 1 | Mohit |
| 1 | Akash |
| 2 | Mohit |
| 2 | Akash |
| 3 | Hemesh |

### Table: REQUIRED_CUSTODIANS

This table represents the target list of custodians:

| CustodianName |
| --- |
| Mohit |
| Akash |

- **Operation**: Find the devices deployed to all custodians in `REQUIRED_CUSTODIANS`:

  **DEPLOYMENTS ÷ REQUIRED_CUSTODIANS**

- **Result Table**:

| DeviceID |
| --- |
| 1 |
| 2 |

## Comparison of Extended Operators

| Operator Class | Algebraic Notation | Logical Operation | Output Objective |
| --- | --- | --- | --- |
| **Inner Join** | ⋈ | Combines matching rows based on a comparison condition | Merges related columns from multiple relations |
| **Outer Join** | ⟕, ⟖, ⟗ | Combines matching rows while preserving unmatched tuples | Ensures no information is lost, using NULL placeholders |
| **Intersection** | ∩ | Identifies rows common to both union-compatible relations | Retrieves the shared subset of tuples |
| **Division** | ÷ | Finds dividend tuples associated with all divisor tuples | Resolves universal "for all" query conditions |

# Summary

Extended operators in relational algebra are derived query operations constructed by combining basic algebraic primitives to simplify data retrieval. Joins combine attributes from multiple relations through inner matching conditions or outer joins that preserve unmatched records using NULL values. Set intersection extracts common rows between union-compatible schemas, and division satisfies complex universal queries by identifying records linked to all tuples in a divisor table. Relational databases rely on these extended expressions to organize query logic and optimize physical database searches.




