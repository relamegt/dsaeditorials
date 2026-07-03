# Canonical Cover of Functional Dependencies

In relational database systems, managing a large, unoptimized set of functional dependencies creates unnecessary processing overhead during transaction validation. To address this issue, database administrators use the concept of a canonical cover.

A canonical cover is a simplified, minimal set of functional dependencies that is equivalent to the original set. It contains no redundant dependencies and no extraneous attributes. It is also referred to as the minimal cover or the irreducible form of a functional dependency set.

## Principles of Irreducible Coverings

A functional dependency set is in its canonical form if it satisfies the following structural properties:

- Every dependency has a unique left-hand side, meaning no two dependencies share the same determinant.
- The right-hand side of each dependency contains only atomic attributes.
- There are no redundant dependencies that can be inferred from other rules in the set.
- There are no extraneous attributes on either the left-hand or right-hand side of any dependency.
- **Extraneous Attribute**: An attribute in a functional dependency is extraneous if its removal does not alter the overall attribute closure of the dependency set.

## Step-by-Step Algorithm for Finding Canonical Cover

To find the canonical cover (**Fc**) of a set of functional dependencies **F**, system designers like **Hemesh** and **Abhiram** follow a structured five-step reduction process:

### Step 1: Decompose the Functional Dependencies

If a dependency has multiple attributes on its right-hand side (e.g., `X -> YZ`), split it into separate dependencies, each with a single attribute on the right-hand side (e.g., `X -> Y` and `X -> Z`).

### Step 2: Eliminate Extraneous Attributes

For each dependency in the set, analyze whether any attribute on the left-hand side (LHS) or right-hand side (RHS) is extraneous:

- **Checking LHS Extraneous Attributes**: In a dependency `XY -> Z`, check if `X` or `Y` can be removed.

1. Remove `X` to form a modified dependency `Y -> Z`.
2. Compute the attribute closure of `Y` under the remaining dependencies.
3. If the closure shows that `Y` can still determine `Z` without using the `X` attribute, then `X` is extraneous and can be removed.

- **Checking RHS Extraneous Attributes**: In a dependency `X -> YZ`, check if any attribute in the dependent set can be removed.

1. Remove an attribute `Z` to form `X -> Y`.
2. Compute the closure of `X` under the modified dependency set.
3. If the closure remains unchanged, then `Z` is extraneous on the right-hand side and can be removed.

### Step 3: Remove Redundant Dependencies

A dependency is redundant if it can be derived from the other dependencies in the set.

1. Temporarily remove the dependency (e.g., `X -> Y`) from the set.
2. Calculate the attribute closure of `X` using only the remaining dependencies.
3. If the dependent `Y` is still a member of the calculated closure, the removed dependency is redundant and can be permanently deleted from the set.

### Step 4: Consolidate Dependencies with Identical Determinants

If two or more dependencies share the same left-hand side (e.g., `X -> Y` and `X -> Z`), combine them into a single dependency by taking the union of their right-hand sides (e.g., `X -> YZ`).

### Step 5: Verify the Final Cover

Ensure that the final set **Fc** contains no extraneous attributes, no redundant dependencies, and shares the exact same closure properties as the original set **F**.

## Detailed Analytical Walkthroughs

### Case 1: Reducing a Redundant Set

Consider a relation **R(P, Q, R)** with the functional dependency set:
**F** = `{P -> QR, Q -> R, PQ -> R}`

#### Step 1: Decompose Right-Hand Sides
Decompose the multi-attribute dependent `P -> QR` into single attributes:
**F** = `{P -> Q, P -> R, Q -> R, PQ -> R}`

#### Step 2: Eliminate Extraneous Attributes
Analyze `PQ -> R` to check if `P` or `Q` is extraneous on the left-hand side:

- Check if `Q` is extraneous:

1. Temporarily remove `Q` to form `P -> R`.
2. Calculate the closure of **{P}** under the other dependencies: `{P, Q, R}`.
3. Since `R` is in **(P)⁺**, the attribute `Q` is extraneous in the dependency `PQ -> R` and can be removed, leaving `P -> R`.

- The dependency set becomes: `{P -> Q, P -> R, Q -> R}` (duplicate instances of `P -> R` are consolidated).

#### Step 3: Remove Redundant Dependencies
Check if `P -> R` is redundant:

1. Temporarily remove `P -> R` from the set: `{P -> Q, Q -> R}`.
2. Calculate the closure of the determinant **(P)⁺** using the remaining dependencies:

- Initialize: `{P}`
- Apply `P -> Q`: `{P, Q}`
- Apply `Q -> R`: `{P, Q, R}`

1. Since the dependent `R` is present in **(P)⁺**, the dependency `P -> R` is redundant and can be removed.

#### Step 4: Consolidate Determinants
The remaining dependencies are: `{P -> Q, Q -> R}`.
Since no two dependencies share the same left-hand side, no consolidation is needed.

#### Conclusion
The final canonical cover is: **Fc** = `{P -> Q, Q -> R}`.

### Case 2: Evaluating a Non-Redundant Set

Consider a relation **R(P, Q, R, S, T)** with the functional dependency set:
**F** = `{P -> QR, RS -> T, Q -> S, T -> P}`

#### Step 1: Decompose and Analyze

- Decompose `P -> QR` into `P -> Q` and `P -> R`.
- The set becomes: `{P -> Q, P -> R, RS -> T, Q -> S, T -> P}`.
- Check LHS extraneous attributes in `RS -> T`:
- If we remove `R`, we check if `S⁺` can determine `T`. Under this set, `S⁺` = `{S}`, which does not determine `T`. So `R` is not extraneous.
- If we remove `S`, we check if `R⁺` can determine `T`. Under this set, `R⁺` = `{R}`, which does not determine `T`. So `S` is not extraneous.
- Check redundancies:
- If we remove `P -> R`, the remaining dependencies do not allow us to derive `R` from `P`. So `P -> R` is not redundant.
- No other dependencies are redundant or contain extraneous attributes.

#### Conclusion
The canonical cover is: **Fc** = `{P -> QR, RS -> T, Q -> S, T -> P}`.

## Verification Process for Canonical Coverage

To verify whether a simplified set of dependencies **F** canonically covers another set **G**, database administrator **Abhiram** follows these verification steps:

1. **Calculate Closures**: Compute the attribute closures under both dependency sets.
2. **Verify Equivalent Closure**: For the sets to be equivalent, the closure of **F** must be equal to the closure of **G**.
3. **Verify G can be derived from F**:

- For each dependency `X -> Y` in **G**, calculate **(X)⁺** under **F**.
- Confirm that `Y` is a subset of **(X)⁺**.

1. **Verify F can be derived from G**:

- For each dependency `X -> Y` in **F**, calculate **(X)⁺** under **G**.
- Confirm that `Y` is a subset of **(X)⁺**.

1. **Verify Minimality**: Confirm that the covering set **F** has no extraneous attributes or redundant dependencies. If both coverage steps are valid and **F** is minimal, then **F** canonically covers **G**.

## Structural Benefits of Minimal Coverings

Utilizing a canonical cover provides several advantages:

- **Minimal Footprint**: It represents the smallest possible set of dependencies required to enforce the schema's constraints.
- **Lossless Representation**: It simplifies the dependency set without losing any structural constraints or data rules.
- **Improved Performance**: It improves transaction execution speed by reducing the number of redundant checks the database engine must run during updates.
- **Simplified Maintenance**: Minimizing dependencies makes it easier to modify tables and update columns without violating database integrity.

# Summary

A canonical cover is a minimal, irreducible set of functional dependencies equivalent to the original set, containing no redundant dependencies or extraneous attributes. Database designers calculate the canonical cover by decomposing multi-attribute dependents, eliminating extraneous attributes on the left and right sides of each dependency, and deleting redundant rules. The resulting cover preserves all structural constraints while reducing verification overhead. Verifying that one set of dependencies canonically covers another requires proving mutual coverage through attribute closure checks, ensuring that database updates remain consistent and performant.




