# DBMS NOTES — MODULE 26: NORMAL FORMS

## 1. INTRODUCTION TO NORMALIZATION
Normalization (Schema Refinement) is a systematic technique used to organize data in a relational database by decomposing tables to eliminate redundancy and undesirable characteristics.

### Goals:
- Eliminate redundancy
- Ensure logical data dependencies

### Why normalization?
Redundancy leads to anomalies:
- **Insertion Anomaly**
- **Update Anomaly**
- **Deletion Anomaly**

---

## 2. ANOMALIES

### 1. Update Anomaly
Same data appears multiple times → difficult to update consistently.

### 2. Insertion Anomaly
Cannot insert data without presence of other dependent data.

### 3. Deletion Anomaly
Deleting a tuple may unintentionally remove useful information.

---

## 3. DECOMPOSITION PROPERTIES

When decomposing relations, two properties must be ensured:

### 1. Lossless Join Property
- Original relation can be reconstructed from decomposed relations.

### 2. Dependency Preservation
- Functional dependencies remain enforceable without performing joins.

---

## 4. NORMAL FORMS

Normal Forms define rules/constraints for good schema design.

### Common Normal Forms:
- 1NF (First Normal Form)
- 2NF (Second Normal Form)
- 3NF (Third Normal Form)

A database is considered "normalized" if it is in **3NF**.

---

## 5. FIRST NORMAL FORM (1NF)

### Definition:
A relation is in 1NF if all attributes contain **atomic (indivisible) values**.

### Key Idea:
- No multivalued attributes (MVA)

### Example:
STUDENT(SID, Sname, Cname)

If a student has multiple courses in one row → NOT 1NF  
Solution → split into multiple rows

---

### Limitation of 1NF:
Even after achieving 1NF, redundancy may still exist.

### Example:
Supplier(SID, Status, City, PID, Qty)

Problems:
- Deletion anomaly
- Insertion anomaly
- Update anomaly

---

### Key Insight:
If a functional dependency **X → Y** exists and:
- X is NOT a superkey → redundancy exists
- X is a superkey → no redundancy

---

## 6. SECOND NORMAL FORM (2NF)

### Definition:
A relation is in 2NF if:
1. It is in 1NF
2. It has **no partial dependency**

---

### Partial Dependency:
Let:
- X = Candidate Key
- Y = Proper subset of X
- A = Non-prime attribute

If:
Y → A  
→ Then it is a partial dependency

---

### Prime vs Non-Prime Attribute:
- Prime: part of any candidate key
- Non-prime: not part of any candidate key

---

### Example:
STUDENT(SID, Sname, Cname)

FDs:
- {SID, Cname} → Sname
- SID → Sname  (Partial dependency)

Problem:
- Sname repeats → redundancy

---

### Decomposition:
R1(SID, Sname)  
R2(SID, Cname)

Result:
- Lossless Join ✔
- Dependency Preserved ✔
- No partial dependency ✔

---

## 7. 2NF LIMITATION

Even after 2NF, redundancy may still exist due to **transitive dependencies**.

Example:
Supplier(SID, Status, City, PID, Qty)

FDs:
- SID → City
- City → Status

Thus:
SID → Status (transitive)

---

## 8. THIRD NORMAL FORM (3NF)

### Definition:
A relation is in 3NF if:
1. It is in 2NF
2. It has **no transitive dependency**

---

### Alternative Formal Definition:
For every FD X → A:
At least one must be true:
- A ⊆ X (trivial FD)
- X is a superkey
- A is a prime attribute

---

## 9. TRANSITIVE DEPENDENCY

If:
- A → B
- B → C
- B does NOT determine A

Then:
A → C is a **transitive dependency**

---

### Example:
Book → Author  
Author → Nationality  
⇒ Book → Nationality (Transitive)

Cause:
Non-key attribute determining another non-key attribute

---

## 10. 3NF DECOMPOSITION

Example:
Sup_City(SID, Status, City)

FDs:
- SID → City
- City → Status

Transitive:
SID → Status

---

### Decomposition:
SC(SID, City)  
CS(City, Status)

Result:
- Lossless Join ✔
- Dependency Preserved ✔
- No transitive dependency ✔

---

## 11. IMPORTANT OBSERVATIONS

- 3NF removes most anomalies
- 3NF is widely used in practice
- Higher normal forms exist (BCNF, 4NF, etc.), but are more complex

---

## 12. FINAL HIERARCHY

- 1NF → Atomic values
- 2NF → No partial dependency
- 3NF → No transitive dependency

---

## 13. KEY TAKEAWAY

Normalization is a progressive refinement process:

Original Schema  
→ 1NF (remove MVA)  
→ 2NF (remove partial dependency)  
→ 3NF (remove transitive dependency)

Goal:
- Minimal redundancy
- No anomalies
- Logical data structure

---
# DBMS NOTES — MODULE 27: DECOMPOSITION (3NF & BCNF)

## 1. MOTIVATION

Even though BCNF removes more redundancy, it **may not preserve dependencies**.

### Problem:
- BCNF → Lossless ✔ but Dependency Preservation ❌ (sometimes)

### Solution:
Use **3NF decomposition**
- Slight redundancy allowed
- Dependency preservation guaranteed

---

## 2. 3NF RECAP

A relation is in 3NF if for every FD X → A:

At least one holds:
- A ⊆ X (trivial)
- X is a superkey
- A is a prime attribute (part of some candidate key)

---

## 3. TESTING FOR 3NF

To check if a relation is in 3NF:

- Check only F (not F⁺) ✔
- For each FD α → β:
  - If α is a superkey → OK
  - Else check: β attributes must be part of some candidate key

⚠️ Issue:
- Finding candidate keys is expensive
- Testing 3NF is **NP-hard** :contentReference[oaicite:0]{index=0}

---

## 4. 3NF DECOMPOSITION ALGORITHM

Given:
- Relation R
- Functional Dependencies F

### Steps:

### Step 1: Compute Canonical Cover (Fc)
- Remove redundant dependencies
- Minimize FDs

---

### Step 2: Create Relations
For each FD X → Y in Fc:
- Create relation Ri = X ∪ Y

---

### Step 3: Ensure Key Presence
- If no Ri contains a candidate key K:
  - Add one relation with K

---

### Step 4 (Optional Optimization):
- Remove redundant relations (subset relations)

---

## 5. PROPERTIES OF 3NF DECOMPOSITION

After decomposition:
- Each relation is in 3NF ✔
- Lossless Join ✔
- Dependency Preserving ✔

---

## 6. 3NF DECOMPOSITION EXAMPLE

Relation:
(customer_id, employee_id, branch_name, type)

FDs:
- customer_id, employee_id → type
- employee_id → branch_name
- customer_id, branch_name → employee_id

---

### Step 1: Canonical Cover
Remove redundancy:
- branch_name is extraneous

Fc:
- customer_id, employee_id → type
- employee_id → branch_name
- customer_id, branch_name → employee_id

---

### Step 2: Create Relations
- (customer_id, employee_id, type)
- (employee_id, branch_name)
- (customer_id, branch_name, employee_id)

---

### Step 3: Remove Redundancy
- (employee_id, branch_name) is subset → remove

---

### Final 3NF:
- (customer_id, employee_id, type)
- (customer_id, branch_name, employee_id)

---

## 7. BCNF (BOYCE-CODD NORMAL FORM)

### Definition:
A relation is in BCNF if for every FD α → β:
- α is a superkey OR
- dependency is trivial

---

## 8. TESTING FOR BCNF

### Method:
For each FD α → β:
- Compute α⁺ (closure)
- If α⁺ ≠ R → violation

---

### Optimization:
- Only check F (not F⁺) for original relation ✔

⚠️ But:
- For decomposed relations → must consider F⁺ :contentReference[oaicite:1]{index=1}

---

## 9. BCNF DECOMPOSITION ALGORITHM

If FD α → β violates BCNF:

### Step:
- R1 = α ∪ β
- R2 = R − (β − α)

Repeat until all relations are in BCNF

---

### Property:
- Always Lossless Join ✔
- Dependency Preservation ❌ (not guaranteed)

---

## 10. BCNF EXAMPLE

R(A, B, C)  
F = {A → B, B → C}

Key = A

---

### Problem:
B → C violates BCNF (B not superkey)

---

### Decomposition:
- R1 = (B, C)
- R2 = (A, B)

---

## 11. IMPORTANT PITFALL

While checking BCNF on decomposed relation:

- Checking only F may mislead ❌
- Must consider F⁺

---

### Example Insight:
Even if FD not visible in F:
- It may exist in F⁺
- Can violate BCNF

---

## 12. DEPENDENCY PRESERVATION IN BCNF

Two methods:

### 1. Using F⁺ (Exponential Algorithm)
- Always correct ✔
- Expensive ❌

---

### 2. Using Direct F (Polynomial Algorithm)
- Faster ✔
- May give false negative ❌

---

### Key Insight:
- Polynomial method is **safe but conservative**
- May say "not preserved" even when it is

---

## 13. COMPARISON: 3NF vs BCNF

| Feature | 3NF | BCNF |
|--------|-----|------|
| Focus | Primary Key | Candidate Keys |
| Redundancy | Some | Minimal |
| Dependency Preservation | Always ✔ | Not guaranteed ❌ |
| Lossless Join | ✔ | ✔ |
| Condition | X superkey OR Y prime | X must be superkey |

---

## 14. FINAL UNDERSTANDING

### 3NF:
- Practical
- Dependency preserving
- Slight redundancy

### BCNF:
- Cleaner design
- No redundancy
- May lose dependencies

---

## 15. BIG PICTURE

You always have:

- 3NF → Lossless ✔ + Dependency Preserving ✔
- BCNF → Lossless ✔ + Minimal Redundancy ✔

But:
- You **cannot always get both BCNF + Dependency Preservation**

---

## 16. STRATEGY FOR EXAMS

- If question asks:
  - "Preserve dependencies" → go for 3NF
  - "Remove redundancy completely" → go for BCNF

---

## 17. KEY FLOW

R  
→ Check 3NF  
→ If not → Apply 3NF decomposition  
→ If stricter needed → Apply BCNF decomposition  

---
# DBMS NOTES — MODULE 28: CASE STUDY (LIBRARY INFORMATION SYSTEM)

## 1. OBJECTIVE

Apply normalization + FD theory to **real-world database design**

Goal:
- Convert specification → ER Model → Relational Schema → Refined Design

---

## 2. DESIGN PIPELINE

1. Identify **Entity Sets**
2. Identify **Relationships**
3. Create **Initial Schema**
4. Apply **Schema Refinement (FDs + Normalization)**
5. Optimize for **Queries**
6. Finalize Schema

---

## 3. SYSTEM OVERVIEW (LIS)

Library system manages:
- Books
- Members
- Issue/Return process

Key constraints:
- Multiple copies of same book
- Members have quotas
- Issue rules enforced

:contentReference[oaicite:0]{index=0}

---

## 4. ENTITY SETS

### 4.1 BOOKS
Attributes:
- title
- author (fname, lname)
- publisher
- year
- ISBN (unique per publication)
- accession_no (unique per copy)

---

### 4.2 STUDENTS
Attributes:
- member_no (unique)
- name
- roll_no (unique)
- department
- gender
- mobile (nullable)
- dob
- degree

---

### 4.3 FACULTY
Attributes:
- member_no (unique)
- name
- id (unique)
- department
- gender
- mobile
- doj

---

### 4.4 MEMBERS
Attributes:
- member_no
- member_type (ug, pg, rs, fc)

---

### 4.5 QUOTA
Attributes:
- member_type
- max_books
- max_duration

---

### 4.6 STAFF (Derived / Assumed)
Attributes:
- name
- id
- gender
- mobile
- doj

---

## 5. RELATIONSHIP

### BOOK ISSUE

Between:
- members (member_no)
- books (accession_no)

Attributes:
- doi (date of issue)

Type:
- Many-to-One (many books → one member)

---

## 6. INITIAL RELATIONAL SCHEMA

- books(title, author_fname, author_lname, publisher, year, ISBN, accession_no)
- book_issue(member_no, accession_no, doi)
- members(member_no, member_type)
- quota(member_type, max_books, max_duration)
- students(member_no, ..., roll_no, ...)
- faculty(member_no, ..., id, ...)
- staff(...)

---

## 7. SCHEMA REFINEMENT

### 7.1 BOOKS — PROBLEM

FDs:
- ISBN → title, author, publisher, year
- accession_no → ISBN

Key:
- accession_no

❌ Redundancy:
- Same book info repeated across copies

---

### 7.2 BOOKS — DECOMPOSITION

Split into:

1. **book_catalogue**
   - (ISBN, title, author, publisher, year)
   - Key: ISBN

2. **book_copies**
   - (ISBN, accession_no)
   - Key: accession_no

✔ BCNF  
✔ Lossless  
✔ Dependency Preserved

---

### 7.3 BOOK ISSUE

FD:
- (member_no, accession_no) → doi

Key:
- (member_no, accession_no)

✔ Already BCNF

---

### 7.4 QUOTA

FD:
- member_type → max_books, max_duration

Key:
- member_type

✔ BCNF

---

### 7.5 MEMBERS

FD:
- member_no → member_type

Key:
- member_no

✔ BCNF

---

### 7.6 STUDENTS

FDs:
- roll_no → all attributes
- member_no ↔ roll_no

Keys:
- roll_no, member_no

✔ BCNF  
⚠ Problem:
- member_no duplicated unnecessarily

---

### 7.7 FACULTY

FDs:
- id → all attributes
- member_no ↔ id

✔ BCNF  
⚠ Same issue as students

---

## 8. REAL-WORLD PROBLEM (VERY IMPORTANT)

Query:
> Find name of member who issued a book

Problem:
- member_no exists
- BUT:
  - Is member student?
  - Or faculty?

❌ Cannot decide which table to query

---

## 9. DESIGN FIX (CRITICAL INSIGHT)

Introduce **GENERALIZATION**

### New MEMBERS Schema:

members(
- member_no
- member_class (student / faculty)
- member_type
- roll_no (nullable)
- id (nullable)
)

FDs:
- member_no → everything
- member_type → member_class

---

### Relationship:
- student IS-A member
- faculty IS-A member

---

## 10. UPDATED SCHEMA

### STUDENTS (Simplified)
- roll_no → all attributes
- No member_no

---

### FACULTY (Simplified)
- id → all attributes
- No member_no

---

## 11. FINAL SCHEMA

- book_catalogue(title, author_fname, author_lname, publisher, year, ISBN)
- book_copies(ISBN, accession_no)
- book_issue(member_no, accession_no, doi)
- quota(member_type, max_books, max_duration)
- members(member_no, member_class, member_type, roll_no, id)
- students(student_fname, student_lname, roll_no, department, gender, mobile, dob, degree)
- faculty(faculty_fname, faculty_lname, id, department, gender, mobile, doj)
- staff(staff_fname, staff_lname, id, gender, mobile, doj)

---

## 12. KEY TAKEAWAYS

### 1. Theory ≠ Complete Design
- Even BCNF schemas may fail in practice

---

### 2. Query Efficiency Matters
- Design must support real queries

---

### 3. Hidden Information Exists
- Not all constraints are explicitly given
- Must infer from problem

---

### 4. Generalization is Powerful
- Helps unify multiple entity types

---

## 13. FINAL FLOW (VERY IMPORTANT)

Specification  
→ Extract Entities  
→ Build ER Model  
→ Convert to Schema  
→ Apply Normalization (3NF / BCNF)  
→ Check Queries  
→ Refine Design  

---

## 14. CORE INSIGHT 🔴

> A "perfect" normalized schema is useless if queries become impractical.

---
# DBMS NOTES — MODULE 29: MVD & 4NF

## 1. MOTIVATION

Even after BCNF:
- Redundancy can still exist ❌

Reason:
- Functional Dependencies (FDs) are **not sufficient**

New concept needed:
→ **Multivalued Dependencies (MVDs)**

:contentReference[oaicite:0]{index=0}

---

## 2. MULTIVALUED DEPENDENCY (MVD)

### Idea:
An attribute can determine **multiple independent values**

Notation:
- X → Y (FD)
- X ↠ Y (MVD)

---

## 3. INTUITION

Example:
Person(Man, Phones, Dogs_Like)

- A man can have:
  - Multiple phones
  - Multiple dogs he likes

So:
- Man ↠ Phones
- Man ↠ Dogs_Like

---

### Key Insight:
Phones and Dogs are **independent**

But in table:
→ All combinations appear (Cartesian Product)

Example:
| Man | Phone | Dog |
|-----|------|-----|
| M1 | P1 | D1 |
| M1 | P1 | D2 |
| M1 | P2 | D1 |
| M1 | P2 | D2 |

---

### Problem:
- Massive redundancy
- Still satisfies BCNF ❗

---

## 4. WHY BCNF FAILS

- No non-trivial FD exists
- Whole relation is candidate key

→ BCNF satisfied  
→ But redundancy exists

🔥 This is the limitation of BCNF

---

## 5. FORMAL DEFINITION

MVD: X ↠ Y holds if:

For tuples t1, t2:
- If t1[X] = t2[X]

Then:
- We must have tuples combining values:
  - t3[Y] = t1[Y]
  - t3[rest] = t2[rest]
  - and vice versa

---

### Simple Meaning:
- Values of Y are independent of rest of attributes

---

## 6. KEY PROPERTY

If:
X → Y (FD)

Then:
X ↠ Y (MVD)

✔ Every FD is an MVD  
❌ Not every MVD is FD

---

## 7. WHEN MVD OCCURS

### Case:
Two independent relationships stored together

Example:
- Student(SID, Name)
- Course(CID, Name)

If merged:
→ Student_Course

Then:
- SID ↠ CID
- SID ↠ Cname

---

## 8. ANOTHER CLASSIC EXAMPLE

Instructor(ID, Child, Phone)

- ID ↠ Child
- ID ↠ Phone

Combining both → redundant combinations

---

## 9. TRIVIAL MVD

MVD X ↠ Y is trivial if:
- Y ⊆ X OR
- X ∪ Y = R

Else:
→ Non-trivial MVD (problematic)

---

## 10. MVD INFERENCE RULES

### Important ones:

- Complementation:
  - X ↠ Y ⇒ X ↠ (R − X − Y)

- Augmentation:
  - WX ↠ YZ

- Transitivity:
  - X ↠ Y and Y ↠ Z ⇒ X ↠ (Z − Y)

- Replication:
  - X → Y ⇒ X ↠ Y

---

## 11. USE OF MVD

- Detect redundancy beyond FDs
- Define constraints on relations
- Ensure correct data representation

---

## 12. FOURTH NORMAL FORM (4NF)

### Definition:

A relation is in 4NF if for every MVD X ↠ Y:

At least one holds:
- MVD is trivial OR
- X is a superkey

---

### Key Insight:
4NF = BCNF + MVD control

---

## 13. IMPORTANT RESULT

If a relation is in 4NF:
→ It is automatically in BCNF

---

## 14. 4NF DECOMPOSITION ALGORITHM

### Step 1:
Find MVD X ↠ Y where:
- X is NOT a superkey

---

### Step 2:
Decompose:

- R1 = X ∪ Y
- R2 = R − (Y − X)

---

### Step 3:
Repeat until all relations satisfy 4NF

---

### Property:
- Lossless Join ✔
- Dependency Preservation ❌ (not guaranteed)

---

## 15. MAIN EXAMPLE

Relation:
Person(Man, Phones, Dogs_Like, Address)

Dependencies:
- Man ↠ Phones
- Man ↠ Dogs_Like
- Man → Address

---

### Problem:
- None of LHS are superkeys
→ Violates 4NF

---

### Decomposition:

1. Person_Phones(Man, Phones)
2. Person_Dogs(Man, Dogs_Like)
3. Person_Address(Man, Address)

---

### Result:
✔ All in 4NF  
✔ No redundancy  
✔ Lossless

---

## 16. ADVANCED EXAMPLE FLOW

R(A, B, C, G, H, I)

FDs:
- A ↠ B
- B ↠ HI
- CG ↠ H

---

### Decomposition Steps:
- R1(A, B)
- R2(A, C, G, H, I)
- R3(C, G, H)
- R4(A, C, G, I)
- R5(A, I)
- R6(A, C, G)

Final:
→ All in 4NF

---

## 17. KEY DIFFERENCE

| Concept | FD | MVD |
|--------|----|-----|
| Meaning | Single value | Multiple independent values |
| Redundancy type | Partial / Transitive | Cartesian explosion |
| Fix | 3NF / BCNF | 4NF |

---

## 18. BIG PICTURE 🔴

1NF → Atomic  
2NF → No partial dependency  
3NF → No transitive dependency  
BCNF → Strong FD control  
4NF → Remove MVD redundancy  

---

## 19. CORE INSIGHT 🔥

> Even a perfectly normalized BCNF table can be horribly redundant due to independent multivalued attributes.

---

## 20. PRACTICAL NOTE

- 4NF is **rarely needed in practice**
- Most systems stop at:
  → 3NF or BCNF

Reason:
- MVD situations are limited (phones, emails, etc.)

---

## 21. FINAL FLOW

FD-based Normalization → 3NF → BCNF  
Then:
MVD-based Normalization → 4NF  

---
# DBMS NOTES — MODULE 30: DESIGN SUMMARY & TEMPORAL DATABASES

## 1. OVERALL OBJECTIVE

This module concludes:
- Database Design Process
- Practical Design Trade-offs
- Introduction to Temporal Databases

:contentReference[oaicite:0]{index=0}

---

## 2. DESIGN GOALS (VERY IMPORTANT 🔴)

Ideal database design should achieve:

- BCNF / 4NF
- Lossless Join
- Dependency Preservation

---

### Reality Check:

You **cannot always achieve all three simultaneously**

So we compromise:

- Use **3NF** → allow redundancy
- Or lose dependency preservation

---

### Practical Limitation:
- SQL **cannot enforce general FDs**
- Only enforces **keys (superkeys)**

---

## 3. HIGHER NORMAL FORMS (FOR COMPLETENESS)

- 5NF (Join Dependency)
- 6NF
- DKNF

⚠️ Rarely used because:
- Too complex
- No strong inference systems

---

## 4. DATABASE DESIGN PROCESS

### Starting Point:

Schema R comes from:
- ER model conversion
- Universal relation
- Ad-hoc design

---

### Process Flow:

1. Identify entities & relationships
2. Convert to relational schema
3. Apply normalization
4. Ensure:
   - Minimal redundancy
   - No anomalies
5. Refine for queries

---

## 5. ER MODEL vs NORMALIZATION

### Ideal Case:
- Good ER design → No normalization needed

---

### Real Case:
- Hidden dependencies exist

Example:
- department_name → building

Fix:
- Create separate **Department entity**

---

### Insight:
Normalization cannot fix **bad conceptual modeling**

---

## 6. DENORMALIZATION (VERY IMPORTANT 🔴)

### Why?
- Improve query performance

---

### Example:
Course + Prerequisite

Instead of:
- Two tables + JOIN

Use:
- Single combined table

---

### Trade-off:

| Benefit | Cost |
|--------|------|
| Faster queries | Redundancy |
| No joins | Update overhead |
| Simple retrieval | More storage |

---

### Alternative:
- Materialized Views

---

### CORE INSIGHT 🔥

> Perfect normalization ≠ best performance

---

## 7. BAD DESIGN PATTERNS

### ❌ Year-wise Tables:
earnings_2004, earnings_2005...

Problem:
- Hard to query across years

---

### ❌ Crosstab Design:
(company_id, earnings_2004, earnings_2005...)

Problem:
- Not scalable
- Difficult queries

---

### ✔ Correct Design:
(company_id, year, earnings)

---

## 8. LIS EXAMPLE (4NF EXTENSION)

From *page 12–14 diagrams*:
- book_title has:
  - multiple authors
  - multiple editions :contentReference[oaicite:1]{index=1}

---

### MVDs:
- book_title ↠ author
- book_title ↠ edition

---

### Problem:
- BCNF satisfied
- But NOT 4NF

---

### Decomposition:

- book_author(book_title, author)
- book_edition(book_title, edition)

✔ Removes redundancy  
✔ Achieves 4NF  

---

## 9. TEMPORAL DATABASES (NEW CONCEPT)

### Motivation:
Some data is **time-dependent**

Examples:
- Medical records
- Stock prices
- Exchange rates

---

### Problem:
Traditional DB stores only **current state**

---

### Need:
Store:
- Value + Time Interval

---

## 10. TEMPORAL DATA

Each tuple has:
- Valid Time Interval

---

### Concepts:

- Snapshot → value at a point
- Interval → value over time

---

### Example:
course(course_id, title, start, end)

---

### Constraint:
- No overlapping intervals

⚠️ Hard to enforce efficiently

---

## 11. TYPES OF TIME

### 1. VALID TIME
- When fact is true in real world

---

### 2. TRANSACTION TIME
- When fact is stored in DB

---

## 12. UNI vs BI TEMPORAL

### Uni-Temporal:
- Only one time dimension

---

### Bi-Temporal:
- Both:
  - Valid Time
  - Transaction Time

---

## 13. EXAMPLE (JOHN CASE)

From *page 21–23 tables* :contentReference[oaicite:2]{index=2}

---

### Problem (Non-temporal DB):
- Only latest address stored
- History lost

---

### Uni-Temporal Solution:

Person(Name, City, Valid_From, Valid_Till)

Example:
- Chennai → (1992 to 2015)
- Mumbai → (2015 to ∞)

---

### Bi-Temporal Solution:

Person(Name, City, Valid_From, Valid_Till, Entered, Superseded)

---

### Insight:
- Valid Time = real-world truth
- Transaction Time = database history

---

## 14. ADVANTAGES OF TEMPORAL DB

- Historical queries possible
- Rollback support
- Better real-world modeling

---

## 15. DISADVANTAGES

- More storage
- Complex queries
- Difficult maintenance

---

## 16. BIG PICTURE 🔴

Database Design is about balance:

- Theory (Normalization)
- Practice (Performance)
- Reality (Time-based data)

---

## 17. FINAL TAKEAWAY 🔥

> A good database designer knows when to normalize, when to denormalize, and when to rethink the model entirely.

---

## 18. COMPLETE NORMALIZATION JOURNEY

1NF → Atomic  
2NF → No partial dependency  
3NF → No transitive dependency  
BCNF → Strong FD rules  
4NF → Handle MVD  

---

## 19. FINAL FLOW

ER Model  
→ Relational Schema  
→ Normalize (3NF / BCNF / 4NF)  
→ Optimize (Denormalization if needed)  
→ Extend (Temporal if required)  

---
