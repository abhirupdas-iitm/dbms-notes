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
