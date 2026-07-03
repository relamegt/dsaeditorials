# Lossless Decomposition in DBMS

In relational database systems, lossless decomposition is a database design process that decomposes a relation schema into multiple smaller relations in a way that preserves all information. A decomposition is considered lossless if joining the decomposed tables using a natural join yields exactly the original table without generating missing or spurious (extra) rows.

## Principles of Information-Preserving Decomposition

During database normalization, tables are split to eliminate redundancy. If a decomposition is lossy, joining the decomposed tables generates invalid, merged records that did not exist in the original database, which compromises data integrity. A lossless decomposition ensures that the physical table splits remain completely reversible, allowing the database engine to reconstruct the original state on demand.

## Three Necessary Conditions for Losslessness

For a decomposition of a relation **R** into sub-relations **R1** and **R2** to be lossless under a set of functional dependencies **F**, it must satisfy three structural conditions:

### 1. Attribute Union Check

The union of the attributes in the decomposed sub-relations must equal the attributes of the original relation:
**R1 ∪ R2 = R**

### 2. Common Attribute Intersection Check

The decomposed sub-relations must share at least one attribute in common, meaning their intersection is not empty:
**R1 ∩ R2 ≠ ∅**

### 3. Super Key Closure Check

The common attribute must act as a super key for at least one of the decomposed sub-relations. This is verified by checking if the attribute closure of the intersection determines either all attributes in **R1** or all attributes in **R2**:
**(R1 ∩ R2)⁺ ⊇ R1** or **(R1 ∩ R2)⁺ ⊇ R2**

## Detailed Analytical Case Study

Consider a database relation tracking device deployments and custodians, managed by database administrators **Mohit** and **Akash**:

`DeviceAllocation (DeviceID, CustodianName, AssetAge, LocationCode, LocationName)`

Under this schema, the following functional dependencies hold:

- `DeviceID -> CustodianName, AssetAge, LocationCode`
- `LocationCode -> LocationName`

The designers decompose `DeviceAllocation` into two sub-relations:

- **R1**: `DeviceDescription (DeviceID, CustodianName, AssetAge, LocationCode)`
- **R2**: `LocationDescription (LocationCode, LocationName)`

We verify whether this decomposition is lossless:

### Step 1: Attribute Union Check

- **R1 ∪ R2** = `{DeviceID, CustodianName, AssetAge, LocationCode} ∪ {LocationCode, LocationName}`
- Union result = `{DeviceID, CustodianName, AssetAge, LocationCode, LocationName}` = **R**
- *Status: Passed*

### Step 2: Common Attribute Intersection Check

- **R1 ∩ R2** = `{DeviceID, CustodianName, AssetAge, LocationCode} ∩ {LocationCode, LocationName}`
- Intersection result = `{LocationCode}` (Not empty)
- *Status: Passed*

### Step 3: Super Key Closure Check

Compute the attribute closure of the intersection set `{LocationCode}` under the functional dependencies:

- Initialize: `{LocationCode}`
- Apply `LocationCode -> LocationName`: `{LocationCode, LocationName}`
- The closure **(LocationCode)⁺** = `{LocationCode, LocationName}`
- Since the closure **(LocationCode)⁺** is equal to the attributes of **R2**, the common attribute is a super key of **R2** (i.e., **(R1 ∩ R2)⁺ ⊇ R2**).
- *Status: Passed*

Because all three conditions are satisfied, the decomposition is guaranteed to be lossless.

## The Role of Armstrong's Axioms in Lossless Analysis

Armstrong's Axioms are logical inference rules used to discover all functional dependencies implied by a given set. While they do not directly prove losslessness, they are the tools used to calculate attribute closures during super key checks. The three core axioms are:

### Reflexivity Rule

If a set of attributes **Y** is a subset of **X**, then **X** functionally determines **Y** (written as `X -> Y`).

### Augmentation Rule

If `X -> Y` holds, then adding attributes **Z** to both sides creates a valid dependency `XZ -> YZ`.

### Transitivity Rule

If `X -> Y` and `Y -> Z` hold, then `X -> Z` is also a valid dependency.

Using these rules, database designers compute closures to evaluate the super key status of the shared attributes.

## BCNF and 3NF Lossless Decomposition Algorithms

Not all schema decompositions are guaranteed to be lossless. Relational systems use specific normalization algorithms to ensure that table splits preserve data integrity:

- **BCNF Decomposition Algorithm**: Recursively splits a relation on dependencies that violate BCNF rules, guaranteeing that each resulting sub-relation is lossless.
- **3NF Synthesis Algorithm**: Synthesizes a set of tables from a canonical cover of dependencies, ensuring that the final schema is both dependency preserving and lossless.

## Structural Benefits of Lossless Decompositions

Designing database tables using lossless decompositions provides several operational benefits:

- **Redundancy Reduction**: Splitting tables removes repetitive values, optimizing storage efficiency.
- **Simplified Write Operations**: Smaller tables are easier to update and maintain, reducing locking overhead during transactions.
- **Guaranteed Data Integrity**: Ensuring that joins only produce original rows prevents the creation of duplicate or incorrect records.
- **Schema Flexibility**: Administrators can modify or scale individual tables without affecting the rest of the database schema.

# Summary

Lossless decomposition splits a database relation into smaller tables in a way that guarantees the original table can be reconstructed exactly through join operations without producing missing or spurious rows. The process relies on verifying three key conditions: the union of sub-attributes must equal the original set, the sub-relations must share a non-empty set of attributes, and the shared attributes must act as a super key for at least one of the decomposed tables. Relational systems use 3NF and BCNF algorithms alongside Armstrong's inference axioms to synthesize lossless schemas, reducing data redundancy while protecting data consistency.




