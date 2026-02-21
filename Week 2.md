# CS2001 – Week 2, Lecture 1
## Module 06 – Introduction to Relational Model
### 1. Week Recap
- DBMS widely used across domains → motivation for study.
- File-system based applications are limited compared to DBMS.
- Basic notions of DBMS introduced previously.
- Now moving toward the relational model in detail.
### 2. Lecture Objectives
- Understand attributes and their types.
- Understand mathematical structure of relational model:
  - Schema
  - Instance
  - Keys
- Familiarize with relational query languages.
### 3. Example of a Relation
- A relation is represented as a table.
- Columns → attributes.
- Rows → tuples (records).
- Order of columns does not matter; attribute names matter.
- Each row corresponds to a specific entity occurrence.
Example:
instructor(ID, name, dept_name, salary)

Each row:
(ID value, name value, dept_name value, salary value)
### 4. Attributes
#### 4.1 Definition
- Attributes describe properties of an entity.
- Only relevant attributes are chosen (business decision).
- Each attribute has:
  - A name
  - A domain (set of allowed values)
  - An atomic type
#### 4.2 Example: Students Relation
Students = (Roll#, FirstName, LastName, DoB, Passport#, Aadhaar#, Department)

Domains:
- Roll# → Alphanumeric string
- FirstName, LastName → Alpha string
- DoB → Date
- Passport# → String (Letter + 7 digits), nullable
- Aadhaar# → 12-digit number
- Department → Alpha string
#### 4.3 Domain
- Domain = set of allowed values for an attribute.
- Every attribute value must belong to its domain.
- Example:
  - If DoB is of type Date, cannot store "27th March 1997" as free text.
  - If Roll# is alphanumeric, it must match that format.
#### 4.4 Atomicity
- Attribute values are atomic (indivisible).
- Cannot combine multiple logical values into one attribute.
  - FirstName and LastName should not be merged.
- Relational model assumes atomic attributes.
#### 4.5 Null Value
- Null ∈ every domain.
- Indicates:
  - Value unknown
  - Value not applicable
- Example:
  - Passport# can be null.
- Null creates complications in certain operations.
### 5. Schema and Instance
#### 5.1 Relation Schema
- Let A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> be attributes.
- Relation schema:
R = (A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>)

Example:
instructor = (ID, name, dept_name, salary)

Schema specifies:
- Attribute names
- Their domains
- Their types
- No actual data
#### 5.2 Formal Definition
Let D<sub>1</sub>, D<sub>2</sub>, ..., D<sub>n</sub> be domains of A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>.

A relation r is a subset of:
D<sub>1</sub> x D<sub>2</sub> x ... x D<sub>n</sub>

Thus:
r ⊆ D<sub>1</sub> x D<sub>2</sub> x ... x D<sub>n</sub>

Each tuple:
t = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>)
where ai ∈ Di

A relation is a set of n-tuples.
#### 5.3 Relation Instance
- Actual data stored in table form.
- A snapshot of data at a given time.
- Instance changes; schema remains fixed.

Example:
instructor ≡ String(5) × String × String × Number+
#### 5.4 Properties of Relations
- Order of tuples is irrelevant.
- Relations are sets → no ordering.
- No two tuples can be identical.
- Every tuple must be unique.
### 6. Keys
#### 6.1 Superkey
Let K ⊆ R (R = set of attributes).

K is a superkey if:
Values of K uniquely identify each tuple in every possible relation instance.

Example:
For instructor:
- {ID} is a superkey.
- {ID, name} is also a superkey.
#### 6.2 Candidate Key
A superkey K is a candidate key if:
- K is minimal.
- No proper subset of K is a superkey.

Example:
- {ID} is a candidate key.
- {ID, name} is not minimal → not a candidate key.
#### 6.3 Primary Key
- One candidate key chosen as primary key.
- Used for tuple identification in practice.
#### 6.4 Example: Students Relation

Students = (Roll#, FirstName, LastName, DoB, Passport#, Aadhaar#, Department)

Superkeys:
- {Roll#}
- {Roll#, DoB}

Candidate Keys:
- {Roll#}
- {FirstName, LastName}
- {Aadhaar#}

Passport# cannot be a key because:
- It is nullable.
- Null cannot uniquely identify tuples.

Primary Key:
- Roll#

Reason:
Roll# encodes useful information:
Example: 14CS92P01
- 14 → Admission year
- CS → Department
- 92 → Category
- P → Type of admission
- 01 → Serial number

Thus Roll# is both unique and semantically meaningful.
#### 6.5 Types of Keys

Secondary / Alternate Key:
- Candidate keys not chosen as primary.
- Example: {FirstName, LastName}, Aadhaar#

Simple Key:
- Single attribute key.
- Example: Roll#

Composite Key:
- More than one attribute.
- Example: {FirstName, LastName}

Compound Key:
- Multiple attributes, each individually a simple key.
- Example: {Roll#, Course#}
#### 6.6 Surrogate Key
- Artificially generated unique identifier.
- Not derived from application data.
- Example: Order number in an e-commerce system.
- Used when natural attributes cannot uniquely identify tuples.

Difference:
- Natural key → derived from real-world data (Roll#, Aadhaar#).
- Surrogate key → system-generated (OrderID).
#### 6.7 Foreign Key
Foreign key constraint:
- Value in one relation must appear in another.

Referencing relation:
- Enrolment(Roll#, Course#)

Referenced relations:
- Students(Roll#)
- Courses(Course#)

Foreign key enforces referential integrity.
### 7. Relational Query Languages
#### 7.1 Procedural vs Declarative
Procedural:
- Specify how to compute.
- Example languages: C, C++, Java, Python.
- Programmer provides algorithm.

Example: Square root of n
1. Guess x<sub>0</sub>
2. x<sub>i</sub>+1 = (x<sub>i</sub> + n/x<sub>i</sub>)/2
3. Repeat until convergence

Declarative:
- Specify what result is required.
- Not how to compute it.

Example:
Find m such that:
m<sup>2</sup> = n

#### 7.2 Relational Query Paradigm
Relational model uses declarative style.

Pure relational languages:
- Relational Algebra
- Tuple Relational Calculus
- Domain Relational Calculus

Properties:
- Equivalent in expressive power.
- Not Turing-complete.
- Relational Algebra:
  - Not Turing-machine equivalent.
  - Has 6 basic operations.
  - Will be focus of study.

### 8. Lecture Summary
- Defined attributes and domains.
- Understood atomicity and null.
- Defined relation schema and instance formally.
- Relations are unordered sets of unique tuples.
- Introduced:
  - Superkey
  - Candidate key
  - Primary key
  - Composite key
  - Surrogate key
  - Foreign key
- Introduced procedural vs declarative paradigms.
- Previewed relational query languages.

---
---
# CS2001 – Week 2, Lecture 2
## Module 07 – Relational Algebra
### 1. Module Recap
- Relational model basics introduced:
  - Attributes and domains
  - Schema and instance
  - Keys (superkey, candidate key, primary key, foreign key)
- Relational query languages introduced at a high level.
- Now focus on relational algebra and its operators.
### 2. Module Objectives
- Understand relational algebra.
- Learn core relational algebra operators.
- Understand aggregation operators.
- Understand limitations of relational algebra.
### 3. Basic Properties of Relations
- A relation is a set.
- Therefore:
  - Ordering of tuples is irrelevant.
  - No duplicate tuples allowed.
- Example:
  - If (a1, b1) appears twice → invalid.
  - Relations must contain distinct tuples only.
- These properties affect behavior of projection, union, join, etc.
### 4. Relational Operators
#### 4.1 Selection (σ) – Row Filtering
- Syntax:
  σ_condition(r)
- Returns:
  - Subset of tuples in r satisfying condition.
- Example:
  σA=B ∧ D>5 (r)
- Logical operators allowed:
  - ∧ (AND)
  - ∨ (OR)
  - Comparison operators (=, >, <, etc.)
- Output:
  - Relation with same schema as r.
  - Fewer or equal tuples.
#### 4.2 Projection (π) – Column Selection
- Syntax:
  πA,C (r)
- Keeps only specified attributes.
- Removes other attributes entirely.
- Important:
  - Duplicate tuples generated after projection are eliminated.
- Example:
  πA(r)
  → Only attribute A.
  → If values repeat, duplicates removed.
- Output:
  - Relation with fewer attributes.
  - Possibly fewer tuples due to duplicate removal.
#### 4.3 Union (∪)
- Syntax:
  r ∪ s
- Requirement:
  - r and s must have identical schemas (same attributes, same domains).
- Result:
  - All tuples from both.
  - Duplicate tuples removed (set semantics).
#### 4.4 Set Difference (−)
- Syntax:
  r − s
- Requirement:
  - r and s must have identical schemas.
- Result:
  - Tuples in r that are not in s.
#### 4.5 Intersection (∩)
- Syntax:
  r ∩ s
- Result:
  - Tuples common to both r and s.
- Not independent:
  r ∩ s = r − (r − s)
#### 4.6 Cartesian Product (×)
- Syntax:
  r × s
- Result:
  - All possible pairings of tuples from r and s.
- If:
  - |r| = m
  - |s| = n
- Then:
  - |r × s| = m × n
- Schema:
  - Attributes of r followed by attributes of s.
##### Naming Issue
- If r and s share attribute names:
  - Cannot have duplicate attribute names in result.
  - Use qualification:
    r.B and s.B
- Necessary especially for self-product.
#### 4.7 Renaming (ρ)
- Syntax:
  ρX(E)
- Returns:
  - Expression E under name X.
- Used for:
  - Self joins.
  - Disambiguation.
- Example:
  r × ρs(r)
#### 4.8 Composition of Operations
- Operators can be nested.
- Example:
  σA=C (r × s)
- Process:
  1. Compute r × s.
  2. Apply selection.
- Output always a relation.
### 5. Natural Join (⋈)
#### 5.1 Definition
- Let r and s be relations on schemas R and S.
- Natural join:
  r ⋈ s
- Result schema:
  R ∪ S
- For each pair (tr, ts):
  - If values match on attributes in R ∩ S,
    include combined tuple.
#### 5.2 Key Characteristics
- Only tuples agreeing on common attribute names are combined.
- Duplicate columns from R ∩ S removed in output.
- Stronger than Cartesian product.
#### 5.3 Equivalent Expression
r ⋈ s =
πA,r.B,C,r.D,E (σr.B=s.B ∧ r.D=s.D (r × s))

Steps:
1. Cartesian product.
2. Select tuples where common attributes match.
3. Project to remove duplicate columns.

- Natural join is widely used in query processing.
- Core operation in relational querying.
### 6. Aggregate Operators
#### 6.1 Purpose
- Compute summary values.
- Examples:
  - SUM
  - AVG
  - MAX
  - MIN
#### 6.2 Behavior
- Input:
  - A relation.
- Output:
  - A single value (not a relation).
- Example:
  SUM(B)
  MAX(salary)
#### 6.3 Difference from Relational Operators
Relational operators:
- Input: relation(s)
- Output: relation

Aggregate operators:
- Input: relation
- Output: single scalar value

- Aggregates are not part of pure relational algebra.
- Used in practical query languages (e.g., SQL).
### 7. Notes on Relational Languages
- Each query input:
  - One or more relations.
- Each query output:
  - A relation.
- Output values must originate from input relations.
- Relational algebra is not Turing complete.
  - Cannot express all possible computations.
  - Requires host programming language for general algorithms.
### 8. Summary of Core Operators
Unary Operators:
- σ (Selection)
- π (Projection)
- ρ (Renaming)

Binary Operators:
- ∪ (Union)
- − (Difference)
- ∩ (Intersection)
- × (Cartesian Product)
- ⋈ (Natural Join)

Aggregate Operators:
- SUM
- AVG
- MAX
- MIN
### 9. Module Summary
- Introduced relational algebra.
- Studied:
  - Selection
  - Projection
  - Union
  - Difference
  - Intersection
  - Cartesian Product
  - Renaming
  - Natural Join
- Understood aggregate operators.
- Noted that relational algebra:
  - Is declarative.
  - Is not Turing complete.
  - Always returns relations (except aggregates).

---
---
