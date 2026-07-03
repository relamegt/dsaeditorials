# Tuple Relational Calculus in DBMS

Tuple Relational Calculus (TRC) is a non-procedural, declarative query language used to retrieve data from relational databases. Instead of specifying a step-by-step procedure to retrieve data, TRC describes the logical properties that the desired data must satisfy. It is based on first-order predicate logic and uses tuple variables to represent rows of database tables.

## Principles of Declarative Query Design

In a declarative query language like Tuple Relational Calculus, the user defines what data is required rather than how to retrieve it. This logical definition is abstract and serves as the mathematical foundation for SQL's filtering and projection conditions.

## Syntax and Logical Operators

A TRC query defines a set of tuples that satisfy a given logical condition.

### Formal Syntax

The basic syntax of a TRC query is expressed as:

`{ t | P(t) }`

- **t**: A tuple variable representing a row placeholder.
- **P(t)**: The predicate condition or logical formula that must evaluate to true for a tuple to be included in the result.
- **{ }**: Denotes the set of result tuples returned by the query.

### Logical Operators and Quantifiers

Predicate expressions are constructed by combining conditions using standard logical operators and quantifiers:

- **∧ (AND)**: Both conditions must evaluate to true.
- **∨ (OR)**: At least one condition must evaluate to true.
- **¬ (NOT)**: Negates the following condition.
- **∃ (Existential Quantifier)**: Denotes "there exists" a tuple in a relation that satisfies the condition (e.g., `∃ t ∈ r (Q(t))`).
- **∀ (Universal Quantifier)**: Denotes "for all" tuples in a relation, the condition holds true (e.g., `∀ t ∈ r (Q(t))`).
- **∈ (Membership)**: Denotes that a tuple belongs to a specific relation.

## Domain Relational Calculus (DRC) Overview

Domain Relational Calculus is similar to TRC, but it uses domain variables (attributes) instead of tuple variables (rows) as the basis for filtering:

`{ <a1, a2, ..., an> | P(a1, a2, ..., an) }`

where `a1, a2, ..., an` represent attributes of the relation and `P` represents the logical predicate condition.

## Component Database Tables Case Study

To analyze TRC queries, we define a custom system operations log database:

### Table: OPERATOR

| OperatorName | OperatingSystem | OfficeLocation |
| --- | --- | --- |
| Mohit | Linux | Chicago |
| Akash | Windows | Boston |
| Hemesh | macOS | Dallas |
| Abhiram | Linux | Chicago |

### Table: FACILITY

| FacilityName | FacilityCity |
| --- | --- |
| FAC1 | Chicago |
| FAC2 | Dallas |
| FAC3 | Boston |

### Table: ALLOCATION

| AllocationNumber | FacilityName | DeviceAge |
| --- | --- | --- |
| 9001 | FAC1 | 4 |
| 9002 | FAC2 | 3 |
| 9003 | FAC3 | 2 |
| 9004 | FAC1 | 1 |

### Table: DEVICE_LOG

| LogID | FacilityName | ResponseTime |
| --- | --- | --- |
| G71 | FAC1 | 45 |
| G75 | FAC2 | 120 |
| G82 | FAC3 | 85 |
| G90 | FAC2 | 210 |

### Table: LOG_ASSIGNMENT

| OperatorName | LogID |
| --- | --- |
| Mohit | G71 |
| Akash | G82 |
| Abhiram | G90 |

### Table: REGISTRY

| OperatorName | AllocationNumber |
| --- | --- |
| Mohit | 9001 |
| Akash | 9003 |
| Hemesh | 9004 |

## Tuple Relational Calculus Examples

Using the system log tables, we analyze the logical structure of TRC queries:

### Example 1: Filtering Rows Based on a Range

Find the log ID, facility name, and response time of device logs where the response time is greater than or equal to 100 milliseconds:

`{ t | t ∈ device_log ∧ t[ResponseTime] >= 100 }`

#### Result Table
The query filters the `DEVICE_LOG` table, returning all attributes for matching rows:

| LogID | FacilityName | ResponseTime |
| --- | --- | --- |
| G75 | FAC2 | 120 |
| G90 | FAC2 | 210 |

### Example 2: Projecting Specific Attributes

Find the log ID for each log where the response time is greater than or equal to 100 milliseconds:

`{ t[LogID] | t ∈ device_log ∧ t[ResponseTime] >= 100 }`

#### Result Table
The query returns only the projected attribute `LogID` for the matching tuples:

| LogID |
| --- |
| G75 |
| G90 |

### Example 3: Joining Relations with Existential Quantifiers

Find the names of all operators who have both a log assignment and a registry record:

`{ t | ∃ s ∈ log_assignment (t.operator_name = s.operator_name) ∧ ∃ u ∈ registry (t.operator_name = u.operator_name) }`

#### Result Table
The query returns names that exist in both the `LOG_ASSIGNMENT` and `REGISTRY` tables:

| OperatorName |
| --- |
| Mohit |
| Akash |

### Example 4: Sub-query Matching over a Specific Attribute

Find the names of all operators who have a log assignment at the "FAC1" facility:

`{ t | ∃ s ∈ log_assignment (t.operator_name = s.operator_name ∧ ∃ l ∈ device_log (s.log_id = l.log_id ∧ l.facility_name = 'FAC1')) }`

#### Result Table

- **Mohit** is returned because he is linked to log `G71`, which is recorded at facility `FAC1`.
- **Akash** is excluded because his log `G82` is at facility `FAC3`.
- **Abhiram** is excluded because his log `G90` is at facility `FAC2`.

| OperatorName |
| --- |
| Mohit |

## Comparison of Tuple Relational Calculus and Relational Algebra

| Feature | Tuple Relational Calculus | Relational Algebra |
| --- | --- | --- |
| **Language Type** | Declarative / Non-procedural | Procedural |
| **Primary Focus** | What data to retrieve | How to retrieve the data step-by-step |
| **Expression Style** | Logical predicates and quantifiers | Set-based operators and mappings |
| **Execution** | Abstract, requires translation before execution | Directly executable by relational query engines |
| **DBMS Role** | Serves as the mathematical basis for SQL syntax | Serves as the internal algebra for query optimization |

# Summary

Tuple Relational Calculus is a declarative, non-procedural query language based on first-order predicate logic that retrieves data from relational databases by specifying the logical properties the results must satisfy. Using tuple variables, logical operators, and existential or universal quantifiers, TRC defines query outcomes without detailing the physical execution steps. While relational algebra defines procedural sequences for query optimization, TRC provides the declarative foundation for SQL statements, ensuring database consistency and transactional accuracy.




