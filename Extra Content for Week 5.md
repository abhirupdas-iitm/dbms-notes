## CS2001 – Week 5, Extra Lecture 1
### 1. INTRODUCTION
Decomposition:
→ Breaking a relation into smaller relations  
#### Definition:
A decomposition of relation R:
- Produces sub-relations R1, R2, ...  
- Each contains subset of attributes  
- Together they contain all attributes of R  
#### Example:
```
R(A, B, C, D)

→ R1(A, B, D)
→ R2(A, C)
```
#### Goal
> Remove redundancy while preserving information  

### 2. TYPES OF DECOMPOSITION
#### 1. Lossless Join Decomposition
#### Definition:
- No information is lost  
- Joining sub-relations reconstructs original relation  
#### Condition:
```
R1 ⋈ R2 = R
```
#### Meaning:
- Perfect reconstruction  
- No extra or missing tuples  
#### Key Insight
> Always aim for lossless decomposition  
#### 2. Lossy Join Decomposition
#### Definition:
- Information is lost  
- Joining produces extra (spurious) tuples  
#### Condition:
```
R1 ⋈ R2 ≠ R
```
#### Problem:
- Incorrect data after join  
- Leads to anomalies  
#### Key Insight
> Lossy decomposition is unacceptable  

### 3. CONDITIONS FOR LOSSLESS DECOMPOSITION
For decomposition into R1 and R2:
#### Condition 1:
```
R1 ∪ R2 = R
```
(All attributes must be covered)
#### Condition 2:
```
R1 ∩ R2 ≠ ∅
```
(Common attributes must exist)
#### Condition 3 (MOST IMPORTANT):
```
(R1 ∩ R2) → R1
OR
(R1 ∩ R2) → R2
```
#### Interpretation:
- Common attributes must functionally determine at least one relation  
#### Key Insight
> Intersection must act like a key for one side  

### 4. EXAMPLE 1 (LOSSY)
#### Given:
```
D(Course_ID, Course_name, Credit, Dept_ID, Dept_name, Teacher)
```
#### Decomposition:
```
D1(Credit, Dept_name, Teacher)
D2(Course_ID, Course_name, Credit, Dept_ID)
```
#### Analysis:
- Intersection = Credit  
- Credit does NOT determine D1 or D2  
#### Result:
→ Lossy decomposition  
#### Reason:
- No proper key in intersection  

### 5. EXAMPLE 2 (LOSSLESS)
#### Decomposition:
```
D1(Course_ID, Dept_name, Teacher)
D2(Course_ID, Course_name, Credit, Dept_ID)
```
#### Analysis:
- Intersection = Course_ID  
- Course_ID determines D1  
#### Result:
→ Lossless decomposition  
#### Key Insight
> If intersection is a key → safe decomposition  

### 6. FUNCTIONAL DEPENDENCY BASED CHECK
#### Given:
```
R(A, B, C, D, E)

F = { AB → C, C → D, B → E }
```
#### Case 1:
```
R1(A, B, C)
R2(D, E)
```
#### Check:
- Intersection = ∅  
#### Result:
→ Lossy  
#### Case 2:
```
R1(A, B, C, D)
R2(B, E)
```
#### Check:
- Intersection = B  
- B → E ⇒ determines R2  
#### Result:
→ Lossless  

### 7. MULTIPLE RELATION DECOMPOSITION
#### Given:
```
R(A, B, C, D, E, G)

F = { AB → C, AC → B, AD → E, B → D, BC → A, E → G }
```
#### Decomposition:
```
R1(A, B, C)
R2(A, C, D, E)
R3(A, D, G)
```
#### Steps:
1. Check union → all attributes present  
2. Check intersections  
3. Compute closures  
#### Key Checks:
- (R1 ∩ R2) = AC  
- AC → B ⇒ determines R1  

- Combine R1 and R2 → R12  

- (R12 ∩ R3) = AD  
- AD → E → G ⇒ determines R3  
#### Result:
→ Lossless  

### 8. EXAMPLE (LOSSY MULTI-DECOMPOSITION)
#### Decomposition:
```
R1(A, B)
R2(B, C)
R3(A, B, D, E)
R4(E, G)
```
#### Key Check:
- (R1 ∩ R2) = B  
- B does NOT determine R1 or R2  
#### Result:
→ Lossy  

### 9. SYSTEMATIC METHOD
#### Step-by-step:
1. Check attribute coverage  
2. Find intersections  
3. Apply functional dependencies  
4. Compute closure  
5. Verify condition  
#### Shortcut:
> If intersection is a superkey for one relation → lossless  

### 10. COMMON MISTAKES
- Ignoring intersection  
- Not computing closure  
- Assuming union condition is sufficient  
- Confusing key with non-key  

### 11. BIG PICTURE
Decomposition is used for:
- Normalization  
- Removing redundancy  
- Avoiding anomalies  
#### Key Insight
> Normalization relies on correct decomposition  

### 12. FINAL TAKEAWAY
You now understand:
- Lossless vs lossy decomposition  
- How to verify using functional dependencies  
- How to solve exam questions step-by-step  
#### Mental Model
Decompose → Check intersection → Apply FD → Decide  

---
## CS2001 – Week 5, Extra Lecture 2
### 1. INTRODUCTION
Canonical Cover:
→ A simplified set of functional dependencies  
#### Why needed?
- DBMS must check FD violations after updates  
- Large FD sets → expensive checking  
- Reduce FDs without changing meaning  
#### Goal
> Simplify FD set while preserving closure  

### 2. DEFINITION
A canonical cover (or minimal cover):
- Equivalent to original FD set  
- Same closure  
- No redundant dependencies  
- No extraneous attributes  
#### Important Note
Some definitions require:
- Only **single attribute on RHS**
Example:
```
A → BC  (not minimal form)
A → B, A → C  (minimal form)
```
#### Key Insight
> Canonical cover = smallest equivalent FD set  

### 3. STEPS TO FIND CANONICAL COVER
#### Step 1: Make RHS Single Attribute
```
A → BC  ⇒  A → B, A → C
```
#### Step 2: Remove Extraneous Attributes
Check if attribute can be removed **without changing closure**
#### Step 3: Remove Redundant FDs
Check if FD can be derived from others  
#### Key Insight
> Remove unnecessary parts, but preserve meaning  

### 4. EXTRANEOUS ATTRIBUTE
#### Definition:
An attribute is extraneous if:
- It can be removed  
- Closure remains unchanged  
#### Example:
```
B → C  
AB → C
```
Since B alone determines C:
→ A is extraneous  
#### Result:
```
AB → C  ⇒  B → C
```
#### Key Insight
> Stronger FD makes weaker one unnecessary  

### 5. REDUNDANT FUNCTIONAL DEPENDENCY
#### Definition:
FD is redundant if:
- It can be derived from other FDs  
#### Example:
```
A → B  
B → C  
A → C
```
Since:
```
A → B → C
```
→ A → C is redundant  
#### Result:
```
A → B, B → C
```
#### Key Insight
> Use transitivity to detect redundancy  

### 6. EXAMPLE 1
#### Given:
```
A → BC  
A → B  
B → C  
AB → C
```
#### Step 1: Split RHS
```
A → B  
A → C  
A → B  
B → C  
AB → C
```
#### Step 2: Remove Extraneous Attribute
- From AB → C  
- Since B → C  
→ A is extraneous  
#### Step 3: Remove Redundancy
- Duplicate A → B → remove one  
- Duplicate B → C → remove one  
- A → C is derived via A → B → C → remove  
#### Final Canonical Cover:
```
A → B  
B → C
```

### 7. EXAMPLE 2
#### Given:
```
A → BC  
CD → E  
B → D  
E → A
```
#### Step 1: Split RHS
```
A → B  
A → C  
CD → E  
B → D  
E → A
```
#### Step 2: Check Extraneous Attributes
- Only CD → E needs checking  
- Neither C nor D alone determines E  
→ No extraneous attribute  
#### Step 3: Check Redundancy
Compute closures:
```
A⁺ = ABCDE  
(CD)⁺ = ABCDE  
B⁺ = BD  
E⁺ = ABCD
```
#### Observation:
- Removing any FD changes closure  
#### Final Canonical Cover:
```
A → B  
A → C  
CD → E  
B → D  
E → A
```

### 8. EXAMPLE 3
#### Given:
```
A → BCDE  
CD → E
```
#### Step 1: Split RHS
```
A → B  
A → C  
A → D  
A → E  
CD → E
```
#### Step 2: Check Redundancy
- A → C and A → D ⇒ A → CD  
- CD → E ⇒ A → E  
→ A → E is redundant  
#### Final Canonical Cover:
```
A → B  
A → C  
A → D  
CD → E
```

### 9. EXAMPLE 4 (TRICKY)
#### Given:
```
B → A  
D → A  
AB → D
```
#### Step 1: Check Extraneous Attribute
From:
```
B → A  
AB → D
```
Using augmentation:
```
B → A ⇒ BB → AB
AB → D ⇒ B → D
```
→ A is extraneous in AB → D  
#### Step 2: Update FD
```
B → D
```
#### Step 3: Check Redundancy
Now:
```
B → D  
D → A ⇒ B → A
```
→ B → A is redundant  
#### Final Canonical Cover:
```
B → D  
D → A
```

### 10. SYSTEMATIC APPROACH
#### Algorithm:
1. Convert RHS to single attributes  
2. Remove extraneous attributes  
3. Remove redundant FDs  
4. Verify closure remains same  
#### Shortcut
> If removing something does not change closure → remove it  

### 11. COMMON MISTAKES
- Not splitting RHS  
- Missing extraneous attributes  
- Not checking closure properly  
- Removing necessary FD  

### 12. BIG PICTURE
Canonical cover is used in:
- Normalization  
- Schema design  
- Dependency checking  
#### Key Insight
> Smaller FD set = faster validation + cleaner design  
### 13. FINAL TAKEAWAY
You now understand:
- What canonical cover is  
- How to compute it step-by-step  
- How to detect extraneous attributes  
- How to remove redundant dependencies  
#### Mental Model
Split → Simplify → Test → Finalize  

---