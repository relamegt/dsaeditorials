# Anomalies in the Relational Model

Database anomalies are operational irregularities that occur when data is poorly organized in a database schema. These anomalies are primarily caused by storing multiple independent entities within a single unnormalized table, leading to data redundancy, inconsistent updates, and improper enforcement of integrity constraints.

## Structural Causes of Database Anomalies

Anomalies occur when a database schema forces designers to mix independent conceptual attributes in a single table. This flat design leads to data redundancy, which degrades performance and compromises data accuracy:

- **Redundant Storage**: The same piece of information is repeated across multiple rows.
- **Dependency Issues**: Changes to one attribute require updates to other, unrelated attributes.
- **Key Constraints**: The database cannot enforce primary or foreign keys without generating empty or invalid fields.

## Classification of Relational Anomalies

Database administrators classify transaction anomalies into three distinct categories based on their operational impact:

### 1. Insertion Anomaly

An insertion anomaly occurs when a new record cannot be added to the database because some unrelated, mandatory information is missing. In a flat schema where two independent concepts are combined, inserting a row for one concept requires providing information for the other concept. If that information does not exist yet, the insertion fails.

### 2. Deletion Anomaly

A deletion anomaly occurs when removing a record to delete specific information unintentionally deletes unrelated, critical information. Because the database design combines multiple concepts in one table, deleting a row to remove one concept also deletes the only copy of another concept stored in that same row.

### 3. Update Anomaly

An update anomaly occurs when modifying duplicate data leads to inconsistencies because the same information is stored in multiple rows. If the database administrator updates the value in one row but fails to update it in all other rows where the value is repeated, the database enters an inconsistent state, causing incorrect calculations and reports.

## Tabular Case Study of Database Anomalies

To analyze how anomalies occur, consider a device management database.

### Table: DEVICE_CUSTODIAN

This table combines device allocations, custodian details, and department budgets:

| DeviceID | CustodianName | DepartmentCode | DepartmentBudget |
| --- | --- | --- | --- |
| 1 | Mohit | DEP1 | 50000 |
| 2 | Akash | DEP2 | 60000 |
| 3 | Hemesh | DEP1 | 50000 |
| 4 | Abhiram | DEP3 | 75000 |
| 5 | Siddu | DEP2 | 60000 |

### Table: DEVICE_ALLOCATION

This table associates device keys with location codes under a foreign key constraint:

| DeviceID | AllocationID | LocationName |
| --- | --- | --- |
| 1 | A501 | ServerRoom |
| 2 | A502 | TechLab |
| 1 | A503 | TechLab |

## Explaining the Anomalies through the Case Study

Using the device tables, we can demonstrate the operational mechanics of each anomaly:

### Insertion Anomaly Example

Suppose the organization establishes a new department named 'Finance' with `DepartmentCode` 'DEP4' and a budget of 80000. Under the current `DEVICE_CUSTODIAN` schema, we cannot insert this new department record into the database until the department is assigned a device and a custodian. Because the table's primary key requires a `DeviceID`, we cannot store the department details alone.

### Deletion Anomaly Example

If the device assigned to `DeviceID` 4 (with custodian **Abhiram**) is retired and its record is deleted, the system removes the entire row. Consequently, we also lose the existence of the `DEP3` department and its budget of 75000. Deleting the device record unintentionally deletes the department's structural information.

### Update Anomaly Example

If the budget for `DEP1` is updated from 50000 to 55000, this modification must be applied to every row representing a custodian in `DEP1`. In this case, the database engine must locate and update both **Mohit's** row (Device 1) and **Hemesh's** row (Device 3). If only one row is updated, the database will report conflicting budgets for the same department.

## Elimination of Anomalies through Normalization

Database anomalies are resolved using normalization. Normalization is a systematic schema design process that decomposes complex, redundant tables into smaller, well-structured relations.

According to E.F. Codd, the creator of the relational model, normalization:

- **Reduces Data Redundancy**: It separates independent entity sets into their own tables.
- **Eliminates Anomalies**: It ensures that insertion, deletion, and update operations only affect the targeted entity set.
- **Establishes Clear Relationships**: It links tables using foreign key constraints to maintain referential integrity.

For example, normalizing the `DEVICE_CUSTODIAN` table involves decomposing it into two separate tables:

1. A `DEPARTMENT` table (`DepartmentCode`, `DepartmentBudget`)
2. A `CUSTODIAN` table (`DeviceID`, `CustodianName`, `DepartmentCode`, with `DepartmentCode` acting as a foreign key).

After this decomposition, we can insert new departments without needing device assignments, delete device records without losing department details, and update a department's budget in a single row.

> **Note:** Enforcing referential integrity constraints is key to preventing data anomalies. When a referencing table contains foreign keys, the database engine prevents operations that would leave orphan records, ensuring data consistency across all tables.

# Summary

Database anomalies occur due to redundant data storage in flat, unnormalized tables, causing inconsistencies during insertion, update, and deletion operations. Insertion anomalies prevent adding new records when required key details are missing, deletion anomalies result in the unintentional loss of related data, and update anomalies create data inconsistencies when duplicate fields are not modified uniformly. Relational systems eliminate these anomalies through normalization, which decomposes large tables into smaller entities linked by foreign key constraints. This design ensures that transactions only modify the intended data fields, maintaining referential integrity across the system.




