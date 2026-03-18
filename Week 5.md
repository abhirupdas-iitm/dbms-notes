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
---
## CS2001 – Week 5, Lecture 3
### 1. Module Recap
Previously covered:
- Functional Dependencies (FDs)  
- Armstrong’s Axioms:
  - Reflexivity  
  - Augmentation  
  - Transitivity  
- Closure of FDs (F⁺)  
Key idea:
New functional dependencies can be derived systematically using axioms.

### 2. Module Objective
- Extend **Functional Dependency Theory**  
- Learn **closure computation techniques**  
- Apply FDs for **schema decomposition**  
- Introduce **BCNF and 3NF**

### 3. Closure of Functional Dependencies (F⁺)
Definition:
Closure F⁺ is the set of all FDs that can be inferred from F using Armstrong’s axioms.
Example:
`F = { A → B, B → C }  `
Then:
`F⁺ = { A → B, B → C, A → C }`

### 4. Example: Deriving New Functional Dependencies
Given:
```
R = (A, B, C, G, H, I)  
F = {  
A → B  
A → C  
CG → H  
CG → I  
B → H  
}
```
Derived FDs:
- A → H (via transitivity: A → B and B → H)  
- AG → I (augment A → C with G → AG → CG, then CG → I)  
- CG → HI (combine CG → H and CG → I)  

### 5. Algorithm to Compute F⁺
Procedure:
1. Initialize:
   F⁺ ← F  
2. Repeat:
   - Apply **reflexivity and augmentation** on each FD  
   - Apply **transitivity** on FD pairs  
   - Add newly generated FDs  
1. Stop when:
   No new FDs are generated  
Key insight:
Since attributes are finite → process terminates.

### 6. Derived Rules (From Armstrong’s Axioms)
These are not primitive but derived:
#### 6.1 Union
If:
```
α → β  
α → γ  
```
Then:
`α → βγ  `

#### 6.2 Decomposition
If:
`α → βγ  `
Then:
```
α → β  
α → γ  
```
#### 6.3 Pseudotransitivity
If:
```
α → β  
γβ → δ  
```
Then:
`αγ → δ  `

### 7. Closure of Attribute Sets (α⁺)
Definition:
α⁺ = set of attributes functionally determined by α using F.

### 8. Algorithm to Compute α⁺
1. Initialize:
   `result ← α ` 
2. Repeat:
   For each FD β → γ in F:
   - `If β ⊆ result → add γ to result  `
1. Stop when:
   No changes occur  

### 9. Example: Computing (AG)⁺
Given:
```
R = (A, B, C, G, H, I)  
F = { A → B, A → C, CG → H, CG → I, B → H }
```
Steps:
- Start: AG  
- Add B, C (A → B, A → C) → ABCG  
- Add H (CG → H) → ABCGH  
- Add I (CG → I) → ABCGHI  
Thus:
(AG)⁺ = {A, B, C, G, H, I}  

### 10. Testing for Candidate Key
Check:
#### Step 1: Super-key
If:
α⁺ = all attributes → α is super-key  
Here:
AG⁺ = R → super-key  
#### Step 2: Minimality
Check subsets:
- A⁺ ≠ R  
- G⁺ ≠ R  
Therefore:
AG is a **candidate key**

### 11. Uses of Attribute Closure
1. **Check Superkey**
   - α⁺ contains all attributes → superkey  
1. **Check FD**
   - `β ⊆ α⁺ → α → β` holds  
1. **Compute F⁺ efficiently**
   - Use closures instead of brute-force  

### 12. BCNF (Boyce-Codd Normal Form)
Definition:
A relation R is in BCNF if for every FD α → β:
- Either:
  - β ⊆ α (trivial)  
  - α is a super-key  

### 13. Example: Not in BCNF
Relation:
`instr_dept(ID, name, salary, dept_name, building, budget)`
FD:
`dept_name → building, budget  `
Problem:
- Non-trivial  
- dept_name is NOT a superkey  
Therefore:
Not in BCNF  

### 14. BCNF Decomposition Rule
If α → β violates BCNF:
Decompose R into:
```
1. R₁ = α ∪ β  
2. R₂ = R − (β − α)  
```

### 15. Example Decomposition
Given:
```
α = dept_name  
β = building, budget  
```
Result:
```
- R₁ = (dept_name, building, budget)  
- R₂ = (ID, name, salary, dept_name)  
```
Both are in BCNF  

### 16. Lossless Join Property
A decomposition is lossless if:
```
1. R₁ ∪ R₂ = R  
2. R₁ ∩ R₂ ≠ ∅  
3. (R₁ ∩ R₂) → R₁ or R₂  
```

### 17. Dependency Preservation
Definition:
A decomposition is dependency-preserving if:
All FDs can be checked without joining relations.

### 18. BCNF vs Dependency Preservation
Important result:
- BCNF ensures **lossless join**  
- BUT may **NOT preserve dependencies**  

### 19. Example: Dependency Not Preserved
Given:
```
R = (C, S, Z)  
F = { CS → Z, Z → C }
```
Decomposition:
- R₁ = (Z, C)  
- R₂ = (S, Z)  
Properties:
- Lossless join ✔  
- Cannot check CS → Z without join ❌  

### 20. Third Normal Form (3NF)
Definition:
A relation R is in 3NF if for every FD α → β:
At least one holds:
1. β ⊆ α (trivial)  
2. α is a superkey  
3. Each attribute in (β − α) is part of some candidate key  

### 21. BCNF vs 3NF
- `BCNF ⊆ 3NF  `
- 3NF allows slight redundancy  
- Ensures **dependency preservation**  

### 22. Goals of Normalization
For relation R:
- Check if R is in good form  
- If not → decompose into R₁, R₂, ..., Rₙ  
Requirements:
- Each relation in good form  
- Lossless join  
- Prefer dependency preservation  

### 23. Problems with Decomposition
1. Loss of information (lossy join)  
2. Expensive dependency checking (requires joins)  
3. Increased query cost  
Trade-off:
Normalization vs performance  

### 24. Limitation of BCNF
Example:
`inst_info(ID, child_name, phone)`
Observations:
- No non-trivial FD → already BCNF  
- Still has redundancy  
Problem:
- Multiple children × multiple phones → duplication  

### 25. Solution Beyond BCNF
Decompose into:
```
- inst_child(ID, child_name)  
- inst_phone(ID, phone)  
```
Result:
- Removes redundancy  
- Eliminates anomalies  

### 26. Key Insight
BCNF is strong, but not always sufficient.  
Leads to higher normal forms:
→ Fourth Normal Form (4NF)

### 27. Module Summary
Concepts covered:
- Closure of FDs (F⁺)  
- Closure of attribute sets (α⁺)  
- Derived rules of FDs  
- BCNF definition and decomposition  
- Lossless join and dependency preservation  
- Introduction to 3NF  
- Limitations of BCNF  
Final takeaway:
Functional dependencies provide a **complete mathematical framework** for:
- Designing schemas  
- Detecting redundancy  
- Performing normalization

### Notes taken from Activity Questions 5.3
1. A set of all functional dependencies implied by the original set of dependencies is called a closure set of functional dependencies. (Question: 1)
2. If a relation is in BCNF, then it is also in 3NF. (Question: 9)
---
## CS2001 – Week 5, Lecture 4
### 1. Module Recap
Previously covered:
- Functional Dependencies (FDs)  
- Closure of attributes (α⁺)  
- Closure of FDs (F⁺)  
- BCNF and 3NF basics  

### 2. Module Objective
- Learn **algorithms for functional dependencies**
- Compute:
  - Attribute closure  
  - Extraneous attributes  
  - Equivalent FD sets  
  - Canonical (minimal) cover  

### 3. Attribute Closure (α⁺)
Definition:
α⁺ = set of attributes functionally determined by α using F.

### 4. Uses of Attribute Closure
1. **Check Superkey**
   - α⁺ = all attributes ⇒ superkey  
1. **Check Candidate Key**
   - Superkey + minimal  
1. **Check Functional Dependency**
   - α → β holds if β ⊆ α⁺  
1. **Compute F⁺**
   - Use closure of different subsets  

### 5. Extraneous Attributes
Definition:
An attribute is **extraneous** if removing it does NOT change the meaning of FDs.

### 6. Types of Extraneous Attributes
#### 6.1 Left-Hand Side (LHS)
A ∈ α is extraneous if:
(α − A) → β can still be derived from F  
Effect:
FD becomes **stronger**

#### 6.2 Right-Hand Side (RHS)
A ∈ β is extraneous if:
α → (β − A) still implies original F  
Effect:
FD becomes **weaker**

### 7. Example: Extraneous Attribute (LHS)
Given:
`F = { A → C, AB → C }`
Check:
Is B extraneous in AB → C?
Yes:
Because A → C already exists  
So:
`AB → C ⇒ A → C  `
Thus:
B is extraneous  

### 8. Example: Extraneous Attribute (RHS)
Given:
`F = { A → C, AB → CD }`
Check:
Is C extraneous in AB → CD?
Yes:
- A → C  
- So AB → C  
- Hence AB → D is sufficient  
Thus:
C is extraneous  

### 9. Tests for Extraneous Attributes
#### 9.1 Test for LHS
To check if A ∈ α is extraneous:
1. Compute (α − A)⁺ using F  
2. If β ⊆ (α − A)⁺ → A is extraneous  

#### 9.2 Test for RHS
To check if A ∈ β is extraneous:
1. Define:
   `F' = (F − {α → β}) ∪ {α → (β − A)}`  
2. Compute α⁺ using F'  
3. If A ∈ α⁺ → A is extraneous  

### 10. Equivalent Sets of Functional Dependencies
Definition:
F and G are equivalent if:
F⁺ = G⁺  

### 11. Checking Equivalence
F and G are equivalent if:
- F covers G (F⁺ ⊇ G)  
- G covers F (G⁺ ⊇ F)  
Cases:
- Both true → Equivalent  
- One true → One stronger  
- Both false → Independent  

### 12. Canonical Cover (Minimal Cover)
Definition:
A canonical cover F<sub>c</sub> of F satisfies:
1. F<sub>c</sub> ≡ F (same closure)  
2. No extraneous attributes  
3. Unique LHS for each FD  

### 13. Properties of Canonical Cover
- Minimal set of FDs  
- No redundancy  
- No unnecessary attributes  
- Also called:
  - Minimal cover  
  - Irreducible set  

### 14. Example: Removing Redundant FD
Given:
`F = { A → B, B → C, A → C }`
Observation:
A → C is redundant  
Because:
`A → B and B → C ⇒ A → C  `

### 15. Example: RHS Reduction
Given:
`{ A → B, B → C, A → CD }`
Steps:
```
- A → CD ⇒ A → C and A → D  
- A → B, B → C ⇒ A → C  
```
Thus:
C is redundant  
Final:
`{ A → B, B → C, A → D }`

### 16. Example: LHS Reduction
Given:
`{ A → B, B → C, AC → D }`
Steps:
```
- A → B, B → C ⇒ A → C  
- AC → D ⇒ A → D  
```
Final:
`{ A → B, B → C, A → D }`

### 17. Algorithm: Canonical Cover
Repeat until no change:
1. **Apply Union Rule**
   - Combine FDs with same LHS  
1. **Remove Extraneous Attributes**
   - From LHS and RHS  
1. **Repeat**
   - Because new simplifications may arise  
Termination:
- Each step reduces size  
- Finite → algorithm stops  

### 18. Example: Full Reduction
Given:
`F = { A → BC, B → C, A → B, AB → C }`
Steps:
1. Combine:
   A → BC  
2. Remove extraneous:
   - A extraneous in AB → C → remove FD  
1. Reduce RHS:
   - C extraneous in A → BC  
Final:
F<sub>c</sub> = { A → B, B → C }

### 19. Key Insight
Canonical cover = **most efficient representation of constraints**

### 20. Practice Problems Overview
#### 20.1 FD Checking
Check if:
α → β holds using α⁺  
#### 20.2 Super-keys
Find α such that:
α⁺ = R  
#### 20.3 Candidate Keys
- Super-key  
- Minimal  
#### 20.4 Prime Attributes
- Attributes in any candidate key  
#### 20.5 Non-Prime Attributes
- Not in any candidate key  
#### 20.6 Equivalence
Check if:
F⁺ = G⁺  
#### 20.7 Canonical Cover
Reduce FD set to minimal form  

### 21. Important Concepts
- Closure → core computational tool  
- Extraneous attributes → redundancy removal  
- Equivalence → comparison of FD sets  
- Canonical cover → minimal representation  

### 22. Module Summary
Concepts covered:
- Attribute closure algorithm  
- Extraneous attribute detection  
- Equivalent FD sets  
- Canonical cover computation  
Final takeaway:
Functional dependency algorithms enable:
- Efficient schema design  
- Reduction of redundancy  
- Preparation for normalization  
