# Equivalence of Functional Dependencies

In relational database design, two sets of functional dependencies (FDs) are considered equivalent if they enforce the exact same integrity constraints on a relation. Equivalence indicates that every functional dependency in the first set can be logically derived from the second set, and every functional dependency in the second set can be derived from the first set using relational inference rules (such as Armstrong's axioms).

## Principles of Semantic Equivalence in Database Schemas

When two sets of functional dependencies are equivalent, they produce the same set of valid relation instances and preserve the same data integrity constraints. Analyzing equivalence helps database designers optimize schema definitions and eliminate redundant dependencies during normalization.

### Determining Relationships between Dependency Sets

Let **FD1** and **FD2** be two separate sets of functional dependencies defined over a relation **R**. We determine their relationship by checking their mutual coverage:

- **FD2 Covers FD1**: If every functional dependency in **FD1** can be derived using the dependencies in **FD2**, then **FD2** is a superset of or covers **FD1** (denoted as **FD2 ⊃ FD1** or **FD1 ⊆ FD2**).
- **FD1 Covers FD2**: If every functional dependency in **FD2** can be derived using the dependencies in **FD1**, then **FD1** is a superset of or covers **FD2** (denoted as **FD1 ⊃ FD2** or **FD2 ⊆ FD1**).
- **Equivalence**: If both coverage conditions are true (**FD1 ⊆ FD2** and **FD2 ⊆ FD1**), then the sets are equivalent (**FD1 = FD2**).

## The Administrative Need for Equivalence Verification

During the database design process, schema definitions are often created by different team members. For example, suppose two database engineers, **Mohit** and **Akash**, are tasked with defining the functional dependencies for a shared company registry database:

- **Mohit** proposes a set of functional dependencies based on direct attribute lookups.
- **Akash** proposes a different set of functional dependencies aimed at query minimization.

As the database administrator, you must verify that both sets enforce the same semantic constraints. Determining equivalence ensures that the schema selected for production does not lose any critical business rules and does not introduce database anomalies.

## Trade-Offs of Dependency Equivalence Analysis

Verifying dependency equivalence involves several design trade-offs:

- **Advantages**:
- *Redundancy Elimination*: It identifies redundant functional dependencies, allowing designers to simplify the schema and improve transaction speed.
- *Design Interchangeability*: It establishes equivalent candidate sets that can be used interchangeably based on query performance needs.
- *Data Consistency Assurance*: It verifies that all possible combinations of attributes follow the same structural rules.
- **Disadvantages**:
- *Algorithmic Complexity*: The process of calculating closures for every attribute combination becomes computationally expensive as the number of columns grows.
- *Time-Consuming Validation*: Testing multiple candidate sets requires running multiple attribute closure loops.
- *Semantic Limitations*: Logical equivalence checks verify only the mathematical structure of the dependencies, not the real-world meaning of the data.

## Worked Analytical Cases

### Case 1: Proving Equivalence between Two Sets

Consider a relation **R(P, Q, R, S)** with two functional dependency sets:

- **FD1** = `{P -> Q, Q -> R, PQ -> S}`
- **FD2** = `{P -> Q, Q -> R, P -> R, P -> S}`

#### Step 1: Check if FD2 covers FD1 (FD1 ⊆ FD2)

- `P -> Q` is present directly in **FD2**.
- `Q -> R` is present directly in **FD2**.
- To check `PQ -> S`, calculate the attribute closure of **{P, Q}** under the rules of **FD2**:

1. Initialize: `{P, Q}`
2. Apply `P -> Q`: `{P, Q}`
3. Apply `Q -> R`: `{P, Q, R}`
4. Apply `P -> S`: `{P, Q, R, S}`
5. Since the dependent `S` is a subset of **(PQ)⁺** under **FD2**, the dependency `PQ -> S` can be derived from **FD2**.

- Therefore, **FD2 covers FD1** (**FD1 ⊆ FD2**).

#### Step 2: Check if FD1 covers FD2 (FD2 ⊆ FD1)

- `P -> Q` is present directly in **FD1**.
- `Q -> R` is present directly in **FD1**.
- To check `P -> R`, calculate the closure of **{P}** under the rules of **FD1**:

1. Initialize: `{P}`
2. Apply `P -> Q`: `{P, Q}`
3. Apply `Q -> R`: `{P, Q, R}`
4. Since the dependent `R` is a subset of **(P)⁺** under **FD1**, the dependency `P -> R` can be derived.

- To check `P -> S`, calculate the closure of **{P}** under the rules of **FD1**:

1. Initialize: `{P}`
2. Apply `P -> Q`: `{P, Q}`
3. Apply `Q -> R`: `{P, Q, R}`
4. Apply `PQ -> S` (since both `P` and `Q` are present in the set): `{P, Q, R, S}`
5. Since the dependent `S` is a subset of **(P)⁺** under **FD1**, the dependency `P -> S` can be derived.

- Therefore, **FD1 covers FD2** (**FD2 ⊆ FD1**).

#### Conclusion
Since **FD1 ⊆ FD2** and **FD2 ⊆ FD1** are both true, the two sets are equivalent (**FD1 = FD2**).

### Case 2: Proving Non-Equivalence and One-Way Coverage

Consider a relation **R(P, Q, R, S)** with two functional dependency sets:

- **FD1** = `{P -> Q, Q -> R, P -> R}`
- **FD2** = `{P -> Q, Q -> R, P -> S}`

#### Step 1: Check if FD2 covers FD1 (FD1 ⊆ FD2)

- `P -> Q` is present directly in **FD2**.
- `Q -> R` is present directly in **FD2**.
- To check `P -> R`, calculate the closure of **{P}** under **FD2**:

1. Initialize: `{P}`
2. Apply `P -> Q`: `{P, Q}`
3. Apply `Q -> R`: `{P, Q, R}`
4. Apply `P -> S`: `{P, Q, R, S}`
5. Since `R` is a subset of **(P)⁺** under **FD2**, the dependency `P -> R` can be derived.

- Therefore, **FD2 covers FD1** (**FD1 ⊆ FD2**).

#### Step 2: Check if FD1 covers FD2 (FD2 ⊆ FD1)

- `P -> Q` is present directly in **FD1**.
- `Q -> R` is present directly in **FD1**.
- To check `P -> S`, calculate the closure of **{P}** under **FD1**:

1. Initialize: `{P}`
2. Apply `P -> Q`: `{P, Q}`
3. Apply `Q -> R`: `{P, Q, R}`
4. No other dependencies apply. The final closure is **(P)⁺** = `{P, Q, R}`.
5. Since the dependent `S` is not a subset of **(P)⁺** under **FD1**, the dependency `P -> S` cannot be derived from **FD1**.

- Therefore, **FD1 does not cover FD2** (**FD2 ⊄ FD1**).

#### Conclusion
Since **FD1 ⊆ FD2** is true but **FD2 ⊆ FD1** is false, the two dependency sets are not equivalent.

> **Note:** Verifying dependency equivalence is a core task in database administration. Equivalence checks confirm whether different schemas enforce identical business rules. If a dependency cannot be derived from an alternative set, adopting that set will result in a loss of constraints, potentially introducing data anomalies.

# Summary

Equivalence of functional dependencies determines whether two separate sets of FDs enforce the same constraints on a database schema. Designers evaluate equivalence by checking if each set can cover (derive) all dependencies in the other set through recursive attribute closure calculations. If mutual coverage is proven, the sets are semantically equivalent and can be used interchangeably to optimize physical table layouts. If coverage is one-way or absent, the sets are not equivalent, and choosing the weaker set will result in a loss of database constraints.




