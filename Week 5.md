## CS2001 – Week 5, Lecture 1
### 1. Module Recap
Previously learned concepts include:
- Relational algebra and relational calculus  
- Equivalence of algebra and calculus  
- Database design process  
- Requirement analysis  
- Entity-Relationship (E-R) model  
- ER diagrams and notation  
- Translation of ER model to relational schema  
- Extended ER features and design considerations  

### 2. Module Objective
Primary objectives:
- Understand what constitutes a good relational database design  
- Introduce normalization concepts  
- Learn First Normal Form (1NF)  

Key idea:
Design quality directly affects redundancy, efficiency, and correctness.

### 3. Good Relational Design
A good relational design should:
- Reflect real-world structure  
- Represent all expected future data  
- Avoid redundant data storage  
- Provide efficient data access  
- Maintain data integrity  
- Be clean, consistent, and understandable  

Important insight:
These goals can sometimes conflict (e.g., efficiency vs redundancy).

### 4. What is a Good Schema?
Example:

Bad design:
instructor_with_department(ID, name, dept_name, salary, building, budget)
Issue:
- building and budget repeat for same department → redundancy  

Observation:
- ID → key  
- building, budget → redundant  
- name, salary → non-redundant  
Good design:
```
instructor(ID, name, dept_name, salary)  
department(dept_name, building, budget)
```

### 5. Redundancy
Definition:
Redundancy = storing the same data multiple times.
Cause:
Occurs when database is not normalized.

### 6. Anomalies
Redundancy leads to anomalies:

#### 6.1 Insertion Anomaly
Cannot insert data without unrelated information.
Example:
Cannot insert instructor without department building/budget.

#### 6.2 Deletion Anomaly
Deleting a record removes unrelated information.
Example:
Deleting last instructor deletes department info.

#### 6.3 Update Anomaly
Same data must be updated in multiple places.
Example:
Updating department budget requires multiple updates → inconsistency risk

### 7. Key Insight
- Redundancy ⇒ Anomaly  
- Dependency ⇒ Redundancy  
Example:
dept_name → building, budget  
Meaning:
Department uniquely determines building and budget.

### 8. Functional Dependency
Definition:
X → Y  
Meaning:
If two rows have same X, they must have same Y.
Example:
`dept_name → building, budget  `

### 9. Decomposition
Goal:
Break large tables into smaller ones to reduce redundancy.
Good decomposition should:
- Preserve information  
- Preserve dependencies  
- Be efficient  
Key idea:
Normalization helps achieve good decomposition.

### 10. Lossy Decomposition
Example:
`employee(ID, name, street, city, salary)`

Decomposed into:
```
employee1(ID, name)  
employee2(name, street, city, salary)
```
Problem:
- name is not unique  
- joining creates incorrect extra tuples  
Result:
Loss of correctness → lossy decomposition

### 11. Lossless-Join Decomposition
Definition:
A decomposition is lossless if:
`R1 ⋈ R2 = R ` 
Conditions:
- R1 ∪ R2 = R  
- R1 ∩ R2 ≠ ∅  
- Join reconstructs original relation  
Example:
```
R(A, B, C)  
R1(A, B)  
R2(B, C)
```
This is lossless.

### 12. Atomic Domains
Definition:
A domain is atomic if values are indivisible.
Non-atomic examples:
- Names (first, middle, last)  
- Roll numbers (CS101 → CS + 101)  

Important rule:
Avoid encoding meaning inside attributes.

### 13. First Normal Form (1NF)
Definition:
A relation is in 1NF if:
- All attributes are atomic  
- All attributes are single-valued  

### 14. Violations of 1NF
Example:
Customer(ID, Name, PhoneNumbers)
Problems:
- PhoneNumbers is multi-valued  
- Phone number may be composite  

### 15. Incorrect Fix Attempt
Customer(ID, Name, Phone1, Phone2)
Issues:
- Arbitrary limit  
- Query confusion  
- Not scalable  

### 16. Another Incorrect Approach
Customer(ID, Name, Phone)  (multiple rows)
Problems:
- Redundancy  
- ID no longer unique  
- Key becomes (ID, Phone)  

### 17. Correct Solution
Decompose into:
```
Customer(ID, Name)  
CustomerPhone(ID, Phone)
```

Properties:
- Removes redundancy  
- Maintains 1NF  
- Models one-to-many relationship  
Key insight:
Whenever one-to-many exists within a table → decompose

### 18. Key Concept
Pattern:
- One entity → multiple values → separate table  
Example:
Customer → multiple phone numbers  

### 19. Overall Flow
Normalization pipeline:
- Dependency → causes redundancy  
- Redundancy → causes anomalies  
- Decomposition → removes redundancy  
- Normalization → guides decomposition  

### 20. Module Summary
Concepts covered:
- Good relational design principles  
- Redundancy and anomalies  
- Functional dependencies  
- Decomposition (lossy vs lossless)  
- Atomic domains  
- First Normal Form (1NF)  
Key takeaway:
Good database design = minimal redundancy + no anomalies + proper normalization

### Notes taken from Activity Questions 5.1
1. In DBMS, we assume that all the relations are in 1NF, by default. (Question: 6)
---
## CS2001 – Week 5, Lecture 2

### 1. Module Recap
Previously covered:
- Good relational design principles  
- Redundancy and anomalies  
- Decomposition (lossy vs lossless)  
- Atomic domains  
- First Normal Form (1NF)  
Key takeaway:
Normalization is required to reduce redundancy and anomalies.

### 2. Module Objective
Primary objective:
- Introduce **Functional Dependencies (FDs)**  
Purpose:
To build a **formal mathematical framework** for good relational design.

### 3. Why Functional Dependencies?
Goals of relational design:
- Determine whether a relation is in good form  
- If not → decompose into smaller relations  

Requirements of decomposition:
- Each resulting relation must be in good form  
- Decomposition must be **lossless-join**  

Foundation of theory:
- Functional dependencies  
- (Later) multivalued dependencies and others  

### 4. Functional Dependencies (FD)
Definition:
A functional dependency is written as:
α → β  
Where:
- α ⊆ R (set of attributes)  
- β ⊆ R  
Condition:
For any valid instance r of relation R:
```
If
t₁[α] = t₂[α]
Then
t₁[β] = t₂[β]
```
Meaning:
If two tuples match on α → they must match on β.

### 5. Intuition of FD
Example:
`dept_name → building, budget  `

Meaning:
If two rows have same department name → they must have same building and budget.
Important:
FDs come from **real-world constraints (business rules)**, not just data observation.

### 6. Important Observation
From data:
- You can disprove an FD  
- But you cannot always prove an FD  

Example:
If:
(1,4), (1,5)
Then:
`A → B is false`
But:
Even if B values are unique, B → A cannot be assumed unless guaranteed by rules.

### 7. Superkey using FD
Definition:
K is a superkey if:
K → R  
Meaning:
K uniquely determines all attributes in the relation.

### 8. Candidate Key using FD
Definition:
K is a candidate key if:
- K → R  
- No subset of K determines R  
Meaning:
Minimal superkey.

### 9. Example Functional Dependencies
Given:
`inst_dept(ID, name, salary, dept_name, building, budget)`
Valid FDs:
```
- dept_name → building  
- dept_name → budget  
- ID → building (via dept_name)  
```
Invalid FD:
`- dept_name → salary  `

### 10. Set of Functional Dependencies
We consider a **set F of FDs**.
Definition:
F holds on R if:
All valid instances of R satisfy all FDs in F.
Important insight:
FDs are **constraints**, not just observations from sample data.

### 11. Trivial Functional Dependency
Definition:
```
α → β is trivial if:
β ⊆ α  
```
Examples:
- (ID, name) → ID  
- name → name  
Reason:
Left side already contains right side.

### 12. Example Functional Dependencies
```
- StudentID → Semester  
- StudentID, Lecture → TA  
- {StudentID, Lecture} → {TA, Semester}  
```
```
- EmployeeID → EmployeeName  
- EmployeeID → DepartmentID  
- DepartmentID → DepartmentName  
```

### 13. Armstrong’s Axioms
These are rules to infer new FDs.
#### 13.1 Reflexivity
If:
`β ⊆ α  `
Then:
`α → β  `

#### 13.2 Augmentation
If:
`α → β  `
Then:
`αγ → βγ`
(Add same attributes to both sides)

#### 13.3 Transitivity
If:
```
α → β  
β → γ
```  
Then:
`α → γ`  

### 14. Closure of Functional Dependencies
Definition:
Closure of F (denoted F⁺):
Set of all FDs that can be inferred from F using axioms.

### 15. Example of Closure
Given:
`F = { A → B, B → C }`
Using transitivity:
`A → C`
So:
`F⁺ = { A → B, B → C, A → C }`  

### 16. Properties of Axioms
Two important properties:
#### 16.1 Soundness
All inferred FDs must be correct.
#### 16.2 Completeness
All valid FDs can be derived using these axioms.

### 17. Key Insight
Functional Dependencies:
- Capture real-world constraints  
- Help identify keys  
- Help guide normalization  
- Help design good schemas  

### 18. Module Summary
Concepts covered:
- Functional dependency definition  
- Relation between FD and keys  
- Super-key and candidate key (formalized)  
- Trivial dependencies  
- Armstrong’s axioms  
- Closure of FDs  
Key takeaway:
Functional dependencies provide a **formal foundation for normalization and database design**.

### Notes taken from Activity Questions 5.2
1. Given a set of functional dependencies F and its closure F<sup>+</sup>, F<sup>+</sup> *cannot* be infinite even for a finite relation R. (Question: 8)
2. 