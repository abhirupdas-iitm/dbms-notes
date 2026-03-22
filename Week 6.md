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
