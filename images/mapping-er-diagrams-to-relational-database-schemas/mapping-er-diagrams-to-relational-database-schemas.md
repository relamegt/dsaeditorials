# Mapping ER Diagrams to Relational Database Schemas

Converting an Entity-Relationship (ER) diagram to a relational model is a key step in database design. The ER model represents the high-level conceptual structure of the data, while the relational model provides the physical layout that can be directly implemented using a relational database management system (RDBMS) like Oracle SQL or MySQL.

## Principles of Schema Translation

The conversion process maps entities and relationships to logical tables. The total number of tables required to represent the design without redundancy depends on the relationship cardinalities and participation constraints.

## Case 1: Binary 1:1 Cardinality with Total Participation

This case occurs when each entity in the first set relates to at most one entity in the second set, and at least one entity set exhibits total participation in the relationship.

### Conceptual Example

A user account is associated with zero or one profile setting record, but every profile setting record must belong to exactly one user account. This represents a 1:1 relationship with total participation on the profile settings side.

### Conversion and Consolidation Process

1. Create a `USER_ACCOUNT` table with primary key `UserID`.
2. Create a `PROFILE_SETTINGS` table with primary key `SettingsID`.
3. Create an association table containing `UserID` and `SettingsID` to represent the relationship.

Because every settings record corresponds to exactly one user account, all three tables can be merged into a single table with `UserID` as the primary key.

### Required Tables

A minimum of 1 table is required.

---

## Case 2: Binary 1:1 Cardinality with Partial Participation on Both Ends

This case occurs when each entity in both sets can associate with at most one instance in the opposing set, but participation is optional on both sides.

### Conceptual Example

An employee can rent at most one reserved parking space, and each parking space is leased to at most one employee. Some employees do not rent parking, and some parking spaces remain unassigned.

### Conversion and Consolidation Process

1. Create an `EMPLOYEE` table with primary key `EmpID`.
2. Create a `PARKING_SPACE` table with primary key `SpaceID`.
3. Create a relationship table containing `EmpID` and `SpaceID`.

Merging all three tables into one would create columns with many `NULL` values for employees without parking or unassigned spaces. To prevent this, the relationship is merged into the `EMPLOYEE` table by adding the `SpaceID` as a foreign key, while the `PARKING_SPACE` table remains separate.

### Required Tables

A minimum of 2 tables are required.

---

## Case 3: Binary N:1 Cardinality Relationships

This case occurs when multiple entity instances in the first set can relate to a single entity instance in the second set, but each instance in the first set connects to only one instance in the second.

### Conceptual Example

Multiple devices can be allocated to a single department, but each device belongs to exactly one department.

### Conversion and Consolidation Process

1. Create a `DEVICE` table with primary key `DeviceID`.
2. Create a `DEPARTMENT` table with primary key `DeptID`.
3. Create a relationship table containing `DeviceID` and `DeptID`.

Since each device links to only one department, the `DeviceID` does not repeat in the relationship table. Therefore, the relationship can be merged directly into the `DEVICE` table by adding `DeptID` as a foreign key. The `DEPARTMENT` table remains separate.

### Required Tables

A minimum of 2 tables are required.

---

## Case 4: Binary M:N Cardinality Relationships

This case occurs when multiple entity instances on both sides of the relationship can associate with multiple instances in the opposing set.

### Conceptual Example

A developer can contribute to multiple code repositories, and each repository can receive contributions from multiple developers.

### Conversion and Consolidation Process

1. Create a `DEVELOPER` table with primary key `DevID`.
2. Create a `REPOSITORY` table with primary key `RepoID`.
3. Create an association table containing `DevID` and `RepoID` to track contributions.

Because both IDs repeat in the association records, the tables cannot be merged without causing severe data duplication. The relationship must be kept as a separate junction table with a composite primary key composed of `(DevID, RepoID)`.

### Required Tables

A minimum of 3 tables are required.

---

## Case 5: Relationships Involving Weak Entities

This case occurs when a child entity set cannot exist without a parent identifying entity, meaning it has no unique key attributes of its own.

### Conceptual Example

An employee has dependent records representing family members. A dependent cannot exist in the system without the corresponding employee. The dependent is a weak entity, and its participation is total.

### Conversion and Consolidation Process

1. Create an `EMPLOYEE` table with primary key `EmpID`.
2. Create a `DEPENDENTS` table. Because a weak entity has no primary key of its own, its key is formed by combining the identifying parent key (`EmpID`) with its own partial key (`DependentName`).
3. Create a relationship table containing `EmpID` and `DependentName`.

Because the primary keys of the relationship and the weak entity are identical, the relationship table is merged directly into the `DEPENDENTS` table.

### Sample Table Structure: DEPENDENTS

The resulting `DEPENDENTS` table uses the primary key of the parent employee alongside the names of the family members:

| DependentName | EmpID | RelationshipType |
| --- | --- | --- |
| Mohit | E101 | Child |
| Akash | E101 | Spouse |
| Hemesh | E102 | Child |
| Abhiram | E103 | Parent |
| Siddu | E103 | Child |

The schema is reduced to exactly two tables: the parent `EMPLOYEE` table and this merged `DEPENDENTS` table.

### Required Tables

A minimum of 2 tables are required.

> **Note:** Analyzing cardinality and participation constraints is essential when mapping ER models to physical databases. One-to-one relationships with total participation allow complete table merging, whereas partial participation and many-to-many relationships require separate tables to prevent NULL values and data redundancy.

# Summary

Mapping ER models to relational schemas translates conceptual entities and relationships into physical tables. Binary 1:1 relationships require only 1 table if at least one entity exhibits total participation, but demand 2 tables if participation is partial on both ends to avoid NULL values. Many-to-one relationships merge the relationship into the "many" side table, requiring 2 tables, while many-to-many relationships must use a separate junction table to prevent redundancy, requiring a minimum of 3 tables. Finally, weak entities are merged with their identifying relationship, using a composite key built from the parent entity's primary key and their own partial key, requiring exactly 2 tables.




