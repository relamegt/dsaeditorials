# Finding the Highest Normal Form of a Relation

Determining the highest normal form that a database relation satisfies is a core task in schema optimization. Normalization structures table attributes to minimize data redundancies and prevent update, insertion, and deletion anomalies. By identifying the highest satisfied normal form (1NF, 2NF, 3NF, or BCNF), designers assess structural quality and ensure transaction safety.

## Process of Normal Form Evaluation

To evaluate a database table, administrators assume the relation is at least in the First Normal Form (1NF), meaning all column cells store atomic, indivisible values. From there, designers systematically test the schema against higher levels of constraint validation.

## Steps to Find the Highest Normal Form

To systematically identify a schema's highest normal form, database engineers follow a structured six-step checklist:

### Step 1: Find All Candidate Keys

Identify the complete set of candidate keys for the relation using the defined functional dependencies. This requires calculating the attribute closures of various combinations. If the closure of an attribute set contains all attributes in the relation, and no proper subset of that set does the same, the set is a candidate key.

### Step 2: Classify Prime and Non-Prime Attributes

- **Prime Attributes**: Any attribute that is a member of at least one candidate key in the relation.
- **Non-Prime Attributes**: Attributes that are not part of any candidate key.

### Step 3: Verify First Normal Form (1NF)

Ensure that all attributes contain only atomic values. If a single cell contains a set, list, or nested row of values, the relation violates 1NF.

### Step 4: Verify Second Normal Form (2NF)

Confirm that the relation is in 1NF and contains no partial dependencies. A partial dependency occurs when a non-prime attribute is functionally determined by a proper subset of a composite candidate key. If any partial dependency exists, the relation is not in 2NF.

### Step 5: Verify Third Normal Form (3NF)

Confirm that the relation is in 2NF and contains no transitive dependencies, meaning non-prime attributes do not depend on other non-prime attributes. To satisfy 3NF, every non-trivial functional dependency `X -> Y` must meet at least one of these criteria:

1. The determinant `X` is a super key of the relation.
2. The dependent `Y` is a prime attribute.

### Step 6: Verify Boyce-Codd Normal Form (BCNF)

Confirm that the relation is in 3NF and check if every determinant is a super key. For every non-trivial functional dependency `X -> Y`, the determinant `X` must be a super key.

## Detailed Analytical Case Studies

Database engineers **Mohit** and **Akash** evaluate the following relations to determine their highest satisfied normal form.

### Case Study 1: Schema violating 2NF

Given a relation **R(P, Q, R, S, T)** and a set of functional dependencies:
**F** = `{ P -> S, Q -> P, QR -> S, PR -> QT }`

#### Step 1: Find Candidate Keys

- Calculate the closure of **{P, R}**:
- Initialize: `{P, R}`
- Apply `PR -> QT`: `{P, R, Q, T}`
- Apply `P -> S`: `{P, R, Q, T, S}`
- The closure **(PR)⁺** contains all attributes, so **PR** is a candidate key.
- Since `Q -> P` is an active dependency, replace `P` with `Q` in the key to test **{Q, R}**:
- Initialize: `{Q, R}`
- Apply `QR -> S`: `{Q, R, S}`
- Apply `Q -> P`: `{Q, R, S, P}`
- Apply `PR -> QT`: `{Q, R, S, P, T}`
- The closure **(QR)⁺** contains all attributes, so **QR** is a candidate key.
- Candidate Keys = `{PR, QR}`

#### Step 2: Classify Attributes

- Prime Attributes = `{P, Q, R}`
- Non-Prime Attributes = `{S, T}`

#### Step 3: Check Normal Forms

- **1NF**: Satisfied (all attributes contain atomic values).
- **2NF**: Look at the dependency `P -> S`. The determinant `P` is a proper subset of the candidate key `PR`, and the dependent `S` is a non-prime attribute. This represents a partial dependency, violating 2NF rules.
- **Conclusion**: The highest normal form satisfied is **1NF**.

### Case Study 2: Schema violating 3NF

Given a relation **R(P, Q, R, S, T)** and a set of functional dependencies:
**F** = `{ QR -> S, PR -> QT, Q -> T }`

#### Step 1: Find Candidate Keys

- Calculate the closure of **{P, R}**:
- Initialize: `{P, R}`
- Apply `PR -> QT`: `{P, R, Q, T}`
- Apply `QR -> S`: `{P, R, Q, T, S}`
- The closure **(PR)⁺** contains all attributes, so **PR** is the candidate key.
- Candidate Keys = `{PR}`

#### Step 2: Classify Attributes

- Prime Attributes = `{P, R}`
- Non-Prime Attributes = `{Q, S, T}`

#### Step 3: Check Normal Forms

- **1NF**: Satisfied.
- **2NF**: The proper subsets of the candidate key `PR` are `{P}` and `{R}`. Neither `P` nor `R` acts as a determinant in the dependency set **F**. Therefore, no partial dependencies exist, and the relation is in 2NF.
- **3NF**: Check the dependency `Q -> T`. The determinant `Q` is not a super key (since its closure is `{Q, T}`), and the dependent `T` is a non-prime attribute. This represents a transitive dependency, violating 3NF rules.
- **Conclusion**: The highest normal form satisfied is **2NF**.

## Crucial Evaluation Guidelines

- **Sequential Evaluation**: Always verify normal forms in order: 1NF -&gt; 2NF -&gt; 3NF -&gt; BCNF.
- **First Failure Rule**: The normal form immediately preceding the first failed validation check represents the highest normal form that the relation satisfies.

## Normal Form Verification Checklist

| Normal Form | Primary Condition to Check | Violation Trigger | Highest Satisfied if Violated |
| --- | --- | --- | --- |
| **1NF** | Column values must be atomic | Presence of multi-valued or composite cells | None (Not in 1NF) |
| **2NF** | No partial dependencies on composite keys | A proper subset of a candidate key determines a non-prime attribute | **1NF** |
| **3NF** | Every determinant is a super key OR every dependent is a prime attribute | A non-prime attribute determines another non-prime attribute | **2NF** |
| **BCNF** | Every determinant in a functional dependency must be a super key | A prime attribute depends on a non-super key | **3NF** |

# Summary

To find the highest normal form of a relational database table, designers calculate candidate keys and systematically evaluate dependencies starting from 1NF through BCNF. A relation is in 1NF if all attributes contain atomic values, in 2NF if it contains no partial dependencies, in 3NF if it contains no transitive dependencies, and in BCNF if every determinant is a super key. The normal form immediately preceding the first failed check determines the highest structural classification the relation satisfies. Performing these checks allows database administrators to identify schema anomalies and secure data consistency.




