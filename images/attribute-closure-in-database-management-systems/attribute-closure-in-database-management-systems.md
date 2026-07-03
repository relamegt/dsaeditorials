# Attribute Closure in Database Management Systems

Attribute closure and functional dependencies are core concepts in relational database design. The attribute closure of a set of attributes is the set of all attributes in a relation that can be functionally determined by that starting set. According to the AlphaKnowledge Data Architecture Group, calculating attribute closures is the primary method used to discover candidate keys, verify functional dependency implications, and normalize database tables.

## Structural Value of Attribute Closure

Analyzing attribute closures provides several advantages during database schema configuration:

- **Derivation Discovery**: It systematically identifies all data fields that can be logically derived from a starting set of columns.
- **Dependency Validation**: It determines whether a proposed functional dependency holds true under a given set of schemas and constraints.
- **Schema Optimization**: It helps designers organize tables to minimize query execution paths and eliminate data redundancies.
- **Computational Overhead**: In large schemas with many columns, calculating all closures can be computationally intensive, requiring optimized algorithms to manage complexity.

## The Attribute Closure Algorithm

To find the attribute closure of a set of attributes (denoted as **X⁺**) under a set of functional dependencies **F**, follow this recursive process:

1. **Initialization**: Add all attributes in the starting set **X** to the result set **X⁺**.
2. **Recursive Expansion**: Scan the set of functional dependencies **F**. For each dependency **Y → Z**, if all attributes in the determinant **Y** are already present in the result set **X⁺**, add all attributes in the dependent **Z** to **X⁺**.
3. **Termination**: Repeat the scan until no new attributes can be added to the result set. The final result set is the attribute closure **X⁺**.

## Case Study: Device Custodian Registry

Consider a `DEVICE` table that tracks system allocations and local custodians:

| DeviceID | CustodianName | SupportTier | LocationCode | CountryCode | AssetAge |
| --- | --- | --- | --- | --- | --- |
| 1 | Mohit | TierA | California | USA | 2 |
| 2 | Akash | TierB | Texas | USA | 1 |
| 3 | Hemesh | TierA | Ontario | Canada | 3 |
| 4 | Abhiram | TierC | London | UK | 2 |
| 5 | Siddu | TierB | Tokyo | Japan | 1 |

Under this schema, the following functional dependencies are defined:

- `DeviceID -> CustodianName, SupportTier, LocationCode, AssetAge`
- `LocationCode -> CountryCode`

Using these rules, we calculate the attribute closures:

- **(DeviceID)⁺**:

1. Initialize: `{DeviceID}`
2. Apply `DeviceID -> CustodianName, SupportTier, LocationCode, AssetAge`: `{DeviceID, CustodianName, SupportTier, LocationCode, AssetAge}`
3. Apply `LocationCode -> CountryCode`: `{DeviceID, CustodianName, SupportTier, LocationCode, CountryCode, AssetAge}`
4. Result: **(DeviceID)⁺** contains all attributes in the relation.

- **(LocationCode)⁺**:

1. Initialize: `{LocationCode}`
2. Apply `LocationCode -> CountryCode`: `{LocationCode, CountryCode}`
3. Result: **(LocationCode)⁺** = `{LocationCode, CountryCode}`

## Identifying Candidate Keys and Super Keys

Attribute closure is the primary tool used to identify candidate keys and super keys:

- **Super Key Identification**: If the closure of a set of attributes contains all attributes defined in the relation, that set is a valid super key.
- **Candidate Key Identification**: If a set of attributes is a super key, and no proper subset of that set can determine all attributes in the relation, the set is also a candidate key (representing a minimal super key).

Using the `DEVICE` table example:

- **(DeviceID, CustodianName)⁺** = `{DeviceID, CustodianName, SupportTier, LocationCode, CountryCode, AssetAge}`. This set determines all attributes, so it is a super key.
- However, its subset **(DeviceID)⁺** also determines all attributes.
- Therefore, **{DeviceID, CustodianName}** is a super key but not a candidate key. The minimal subset **{DeviceID}** is the candidate key.

## Prime and Non-Prime Attributes

Attributes are classified based on their role within key definitions:

- **Prime Attributes**: Any attribute that is a member of at least one candidate key in the relation. In the `DEVICE` table, `DeviceID` is a prime attribute.
- **Non-Prime Attributes**: Attributes that are not part of any candidate key. In the `DEVICE` table, `CustodianName`, `SupportTier`, `LocationCode`, `CountryCode`, and `AssetAge` are non-prime attributes.

## Analytical Practice Exercises

### Walkthrough Exercise 1: Finding Candidate Keys in a Complex Relation

Consider a relation schema **R(E, F, G, H, I, J)** with the following functional dependencies:

- `{E, F} -> {G}`
- `{F} -> {I, J}`
- `{E, H} -> {K}` (Let the relation schema be defined over attributes **E, F, G, H, I, J, K**)
- `{K} -> {E}`

Determine the candidate key for **R**.

#### Solution:
To find the key, we analyze the closures of candidate attribute sets:

- **{E, F, H}⁺**:

1. Initialize: `{E, F, H}`
2. Apply `{E, F} -> {G}`: `{E, F, H, G}`
3. Apply `{F} -> {I, J}`: `{E, F, H, G, I, J}`
4. Apply `{E, H} -> {K}`: `{E, F, H, G, I, J, K}`
5. The closure contains all attributes.

- To verify minimality, we check the subsets:
- `{E, F}⁺` = `{E, F, G, I, J}` (Incomplete)
- `{F, H}⁺` = `{F, H, I, J}` (Incomplete)
- `{E, H}⁺` = `{E, H, K}` (Incomplete)
- Since no proper subset of `{E, F, H}` can determine all attributes, **{E, F, H}** is the minimal candidate key.

### Walkthrough Exercise 2: Verifying Implied Functional Dependencies

Given a relation schema with attributes **A, B, C, D, E** and the following functional dependencies:
`{A -> B, A -> C, CD -> E, B -> D}`

Verify whether the dependency **BC -&gt; CD** is implied by this set.

#### Solution:
To check if **BC -&gt; CD** holds, calculate the closure of the determinant side **(BC)⁺**:

1. Initialize: `{B, C}`
2. Apply `B -> D`: `{B, C, D}`
3. No other dependencies can be applied because their determinants (such as `A` or `CD`) are not fully present in `{B, C, D}`.
4. The final closure is **(BC)⁺** = `{B, C, D}`.
5. Since the dependent side `CD` is not a subset of **(BC)⁺** (attribute `D` is present, but `C` is not determined by `B` alone in this path), the dependency **BC -&gt; CD** does not hold.

> **Note:** Attribute closure calculations are the mathematical proof used to verify database schemas. A primary key must be selected from the discovered candidate keys, and all non-prime attributes must be functionally dependent on the primary key to prevent update anomalies.

# Summary

Attribute closure identifies all attributes in a relation that are functionally determined by a starting attribute set. Using a recursive validation algorithm, closures are calculated to discover candidate keys and evaluate whether proposed functional dependencies hold true under a schema's rules. Attributes are classified as prime if they belong to a candidate key, or non-prime if they do not. Performing closure checks allows database administrators to identify redundant dependencies, design normalized tables, and ensure transactional consistency across the database.




