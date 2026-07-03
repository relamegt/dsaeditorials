# Dependency Preserving Decomposition in DBMS

In relational database systems, dependency preservation is an essential property of schema decomposition. A decomposition of a relation **R** into sub-relations **R1, R2, ..., Rn** is dependency preserving if the union of the functional dependencies projected onto the decomposed sub-relations is logically equivalent to the original set of functional dependencies **F**.

## Principles of Dependency Preservation

When decomposing a large table into smaller tables to achieve higher normal forms (such as 3NF or BCNF), designers must ensure that the constraints of the original database are not lost. Preserving these dependencies provides several key architectural benefits:

- **Constraint Enforcement**: It allows the database engine to enforce integrity constraints within individual tables without executing expensive join operations across multiple tables.
- **Lossless Reconstruction**: Working alongside lossless join properties, it ensures that the original relation can be reconstructed without data loss.
- **Improved Data Integrity**: It reduces data redundancy and prevents update anomalies while preserving data logic.

## Mathematical Formulation of Preservation Coverage

A decomposition **D** = **{R1, R2, ..., Rn}** of a relation **R** is dependency preserving with respect to a set of functional dependencies **F** if the closure of the union of the projected dependencies equals the closure of the original set:

**`(F1 ∪ F2 ∪ ... ∪ Fn)⁺ = F⁺`** 

When a relation is decomposed into two sub-relations (**R1** with projected dependencies **F1** and **R2** with projected dependencies **F2**), the relationship between the union of the projected dependencies and the original set falls into three scenarios:

- **F1 ∪ F2 = F**: The decomposition preserves all functional dependencies.
- **F1 ∪ F2 ⊂ F**: The union is a strict subset of the original set, indicating the decomposition does not preserve dependencies.
- **F1 ∪ F2 ⊃ F**: This scenario is mathematically impossible.

## Worked Case Studies of Dependency Preservation

During schema normalization, database designers **Mohit** and **Akash** evaluate whether the following decompositions preserve the system's functional dependencies.

### Case Study 1: Verifying a Dependency-Preserving Decomposition

Given a relation **R(P, Q, R)** with the functional dependencies **F** = `{ P -> Q, Q -> R }` and a proposed decomposition **R1(P, Q)** and **R2(Q, R)**, determine if the decomposition is dependency preserving.

#### Step 1: Project the Functional Dependencies

- On **R1(P, Q)**: The projected dependency is `P -> Q`.
- On **R2(Q, R)**: The projected dependency is `Q -> R`.
- The union of the projected dependencies is: **F'** = `{ P -> Q, Q -> R }`.

#### Step 2: Find the Closure of the Projected Set
Using the dependencies in **F'**, we calculate the closure **F'⁺**:

- From `P -> Q` and `Q -> R`, we derive `P -> R`.
- Therefore, **F'⁺** = `{ P -> Q, Q -> R, P -> R }`.

#### Step 3: Compare with the Original Closure
Because **F'⁺** is identical to the original closure **F⁺**, the decomposition is dependency preserving.

### Case Study 2: Verifying a Non-Preserving Decomposition

Given a relation **R(P, Q, R, S)** with the functional dependencies **F** = `{ PQ -> R, R -> S, S -> P }` and a proposed decomposition **R1(P, Q, R)** and **R2(R, S)**, determine if the decomposition is dependency preserving.

#### Step 1: Project the Functional Dependencies

- On **R1(P, Q, R)**:
- `PQ -> R` is present.
- From `R -> S` and `S -> P`, we transitively derive `R -> P`.
- The projected dependencies are: **F1** = `{ PQ -> R, R -> P }`.
- On **R2(R, S)**:
- `R -> S` is present.
- The projected dependency is: **F2** = `{ R -> S }`.

#### Step 2: Calculate the Union of the Projected Dependencies

- The union of the projected dependencies is: **F1 ∪ F2** = `{ PQ -> R, R -> P, R -> S }`.

#### Step 3: Verify the Original Dependencies under the Union Set
We check if each original dependency in **F** can be derived from **F1 ∪ F2**:

- `PQ -> R`: Present in the union set.
- `R -> S`: Present in the union set.
- `S -> P`: To verify this dependency, compute the attribute closure of **{S}** using the rules of the union set **F1 ∪ F2**:

1. Initialize: `{S}`
2. No dependencies in `{ PQ -> R, R -> P, R -> S }` have a determinant composed of `S` alone.
3. The final closure is **(S)⁺** = `{S}`.

- Since the dependent `P` is not a member of **(S)⁺** under the union set, the dependency `S -> P` cannot be derived.
- Therefore, the decomposition is not dependency preserving.

## 

# Summary

Dependency preserving decomposition ensures that a relation's functional dependencies can be enforced within individual tables after schema decomposition, avoiding costly join operations. A decomposition is dependency preserving if the closure of the union of the projected sub-relation dependencies is equivalent to the closure of the original dependency set. When all original rules can be derived from the decomposed tables, the database maintains its integrity constraints; if any dependency cannot be derived, the decomposition is not preserving, which may introduce inconsistencies during transactions.




