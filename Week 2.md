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
1. Guess x0
2. xi+1 = (xi + n/xi)/2
3. Repeat until convergence

Declarative:
- Specify what result is required.
- Not how to compute it.

Example:
Find m such that:
m^2 = n

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
