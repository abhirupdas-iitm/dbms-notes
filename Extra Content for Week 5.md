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
