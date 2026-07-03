# Relational Database Keys

Keys are fundamental elements of the relational database model that ensure structural uniqueness, enforce data integrity, and optimize search access. By defining rules for individual columns or combinations of columns, keys establish how rows are identified within a table and how relationships are mapped across different tables.

## Structural Importance of Keys in Database Schemas

Without structured database keys, managing large relational tables becomes slow and error-prone. Keys serve three primary functions:

- **Enforcing Row Uniqueness**: They ensure that every record in a table is distinct and can be identified without ambiguity.
- **Enforcing Data Integrity**: They prevent duplicate entries and maintain database consistency across insertions and updates.
- **Establishing Logical Relationships**: They connect separate tables using referenced keys, allowing the database engine to perform efficient join operations.

## Taxonomy of Relational Keys

The relational model classifies keys into ten distinct categories based on their design and functionality:

### 1. Candidate Key

A candidate key is a minimal set of attributes that can uniquely identify each tuple in a relation. It is a super key containing no redundant attributes.

- Every table must define at least one candidate key.
- Candidate keys must contain unique values, and no two rows can share the same candidate key value.
- A table can contain multiple candidate keys, from which a single primary key is selected.

### 2. Super Key

A super key is a set of one or more attributes that can uniquely identify a tuple in a relation.

- Unlike candidate keys, a super key can include additional, redundant attributes that are not strictly necessary for unique identification.
- For example, if a system serial number uniquely identifies a record, combining that serial number with a description field still forms a valid super key, even though the description is redundant.

### 3. Alternate Key

An alternate key is any candidate key in a table that was not selected to be the primary key. It is also referred to as a secondary candidate key.

- Alternate keys can uniquely identify records just like the primary key, but they are not used as the main identifier for relationship mappings.

### 4. Foreign Key

A foreign key is an attribute in one table that references the primary key of another table, establishing a logical link between the two relations.

- The table containing the foreign key is the referencing table, and the table being pointed to is the referenced table.
- Unlike primary keys, foreign keys can contain duplicate values and can be set to `NULL` if the relationship is optional.

### 5. Partial Key

A partial key is an attribute in a weak entity set that helps identify records but cannot uniquely identify them by itself.

- A partial key must be combined with the primary key of its identifying strong entity set to form a composite key that uniquely identifies each weak entity instance.
- It cannot contain `NULL` values because it is needed to distinguish records within the weak entity set.

### 6. Primary Key

A primary key is a single candidate key selected by the database designer to uniquely identify each row in a table.

- A primary key cannot contain duplicate values and can never be `NULL`.
- Database engines automatically organize the physical storage layout around the primary key index to accelerate search operations.

### 7. Secondary Key

A secondary key is an attribute or combination of attributes used to search and retrieve records, but it does not guarantee row uniqueness.

- The DBMS uses secondary keys to build non-unique search indexes, speeding up query execution for common search fields (such as filtering assets by manufacturer).

### 8. Unique Key

A unique key constraint guarantees that all values in a specific column or combination of columns are unique across all rows in a table.

- Unlike a primary key, a unique key column allows `NULL` values, although standard relational databases typically restrict this to a single `NULL` entry per column.

### 9. Composite Key

A composite key is a key that is formed by combining two or more columns to uniquely identify a record.

- Composite keys are used when a single column is insufficient to guarantee uniqueness, such as in junction tables where combinations of two foreign keys represent relationships.

### 10. Surrogate Key

A surrogate key is an artificial, system-generated identifier added to a table when no suitable natural key exists.

- It is typically implemented as an auto-incremented integer value.
- A surrogate key carries no real-world meaning and is used solely to simplify database indexing and relationship mapping.

## Structural Layouts and Examples

To illustrate these concepts, consider a device inventory schema containing tables designed around various key types.

### Example A: Secondary Key Indexing Structure

The following `DEVICE_LOG` table uses the `SerialNo` column as its primary key, while the `ModelName` column acts as a secondary key. The database build index paths over `ModelName` to speed up search queries, even though model names are duplicated.

| SerialNo | ModelName | PurchaseYear | TargetDepot |
| --- | --- | --- | --- |
| SN101 | CoreV1 | 2024 | North |
| SN102 | SwitchX | 2025 | South |
| SN103 | CoreV1 | 2024 | North |
| SN104 | AccessTerminal | 2026 | East |
| SN105 | SwitchX | 2025 | West |

### Example B: Unique Key Constraints

In this `DEVICE_CONTACTS` table, the `SerialNo` column is the primary key. The `SupportContactEmail` column is configured as a unique key, ensuring that no two devices share the same support contact email.

| SerialNo | SupportContactEmail | ModelName |
| --- | --- | --- |
| SN101 | support1@alphaknowledge.org | CoreV1 |
| SN102 | support2@alphaknowledge.org | SwitchX |
| SN103 | support3@alphaknowledge.org | CoreV1 |
| SN104 | support4@alphaknowledge.org | AccessTerminal |
| SN105 | support5@alphaknowledge.org | SwitchX |

Here, if a device has no assigned support contact, the `SupportContactEmail` field can store a `NULL` value, but any non-null email addresses must remain unique.

> **Note:** Correctly classifying keys is essential for relational database normalization. Primary keys enforce structural uniqueness, foreign keys maintain referential relationships across tables, and unique keys prevent duplicate values in optional columns. Misconfiguring these keys can lead to data duplication, orphan records, and slow query execution.

# Summary

Database keys are essential tools in the relational model for enforcing row uniqueness, maintaining data integrity, and linking related tables. They span ten different categories, including primary keys for absolute identification, candidate keys that represent potential primary keys, and foreign keys that map relationships to other tables. While surrogate keys provide system-generated identifiers and composite keys combine multiple columns for uniqueness, unique keys prevent duplicates in columns that allow NULL values. Selecting the appropriate key types allows designers to construct normalized schemas that scale efficiently and prevent data inconsistencies.




