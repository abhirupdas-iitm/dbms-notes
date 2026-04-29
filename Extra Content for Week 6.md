## CS2001 – Week 6, Extra Lecture 1
### 1. INTRODUCTION TO NORMAL FORMS
Goal:
→ Determine highest normal form of a relation  
#### Given:
- Relation R  
- Functional Dependencies  
#### Steps:
1. Find candidate keys  
2. Check 1NF  
3. Check 2NF  
4. Check 3NF  
5. Check BCNF  
#### Key Insight
> Follow strict order: 1NF → 2NF → 3NF → BCNF  

### 2. FIRST NORMAL FORM (1NF)
#### Definition:
- All attributes must be atomic  
#### Meaning:
- No multivalued attributes  
- No repeating groups  
#### Note:
- Usually assumed satisfied  
#### Key Insight
> Atomic attributes ⇒ 1NF satisfied  

### 3. SECOND NORMAL FORM (2NF)
#### Definition:
- Must be in 1NF  
- No partial dependency  
#### Partial Dependency:
A → B  
Where:
- A ⊂ Candidate Key  
- B = Non-prime attribute  
#### Meaning:
- Non-key depends on full key  
#### Key Insight
> Exists only if composite key exists  

### 4. THIRD NORMAL FORM (3NF)
#### Definition:
For FD A → B:
- A is superkey OR B is prime  
#### Meaning:
- No transitive dependency  
#### Key Insight
> Non-key should not depend on non-key  

### 5. BOYCE-CODD NORMAL FORM (BCNF)
#### Definition:
For FD A → B:
- A must be a superkey  
#### Meaning:
- Stronger than 3NF  
#### Key Insight
> Every determinant must be a superkey  

### 6. EXAMPLE 1
#### Given:
R(A,B,C,D)  
F={B→C,D→A}  
#### Candidate Key:
BD  
#### 1NF:
Satisfied  
#### 2NF:
B→C, B ⊂ BD, C non-prime  
→ Partial dependency  
#### Result:
→ NOT in 2NF  
→ Highest = 1NF  

### 7. EXAMPLE 2
#### Given:
R(A,B,C,D,E,F)  
F={BCD→E,BCE→F,DE→A,D→C,CE→A}  
#### Candidate Keys:
BCD,BDE  
#### 2NF:
DE→A, DE ⊂ BDE, A non-prime  
→ Partial dependency  
#### Result:
→ NOT in 2NF  
→ Highest = 1NF  

### 8. EXAMPLE 3
#### Given:
R(B,W,X,Y,Z)  
F={B→W,W→XYZ,X→Y}  
#### Candidate Key:
B  
#### 2NF:
No composite key → no partial dependency  
→ In 2NF  
#### 3NF:
W→XYZ, W not superkey, RHS non-prime  
→ Violates 3NF  
#### Result:
→ Highest = 2NF  

### 9. EXAMPLE 4
#### Given:
R(X,Y,W,Z,B)  
F={XY→WZB,Z→X}  
#### Candidate Keys:
XY,YZ  
#### 2NF:
Z→X, Z ⊂ YZ, X prime  
→ OK  
#### 3NF:
Z→X, RHS prime  
→ OK  
#### BCNF:
Z not superkey  
→ Violates BCNF  
#### Result:
→ Highest = 3NF  

### 10. EXAMPLE 5
#### Given:
R(A,B,C,D)  
F={A→B,B→C,C→D,D→A}  
#### Candidate Keys:
A,B,C,D  
#### 2NF:
No composite key  
→ OK  
#### 3NF:
All attributes prime  
→ OK  
#### BCNF:
All determinants are keys  
→ OK  
#### Result:
→ BCNF  

### 11. SYSTEMATIC METHOD
#### Steps:
1. Find candidate keys  
2. Identify prime/non-prime  
3. Check partial dependency  
4. Check transitive dependency  
5. Check superkey condition  
#### Shortcut:
> LHS not superkey ⇒ violation  

### 12. COMMON MISTAKES
- Skipping candidate key  
- Confusing prime/non-prime  
- Missing partial dependency  
- Misapplying BCNF condition  

### 13. FINAL TAKEAWAY
You now understand:
- How to find highest normal form  
- Differences: 2NF vs 3NF vs BCNF  
- Proper solving sequence  
#### Mental Model
Find Key → Check Partial → Check Transitive → Check Superkey  

---
## CS2001 – Week 6, Extra Lecture 2
### 1. INTRODUCTION
Goal:
→ Find highest normal form of a relation  
#### Given:
- Relation R  
- Functional Dependencies  
#### Steps:
1. Find candidate keys  
2. Check 1NF  
3. Check 2NF  
4. Check 3NF  
5. Check BCNF  
#### Key Insight
> Always start with candidate key  

### 2. EXAMPLE 1
#### Given:
R(A,B,C,D)  
F={B→C,D→A}  
#### Candidate Key:
BD  
#### 1NF:
- Atomic values assumed  
→ In 1NF  
#### 2NF:
- B→C  
- B ⊂ BD  
- C non-prime  
→ Partial dependency  
#### Result:
→ NOT in 2NF  
→ Highest = 1NF  

### 3. EXAMPLE 2
#### Given:
R(A,B,C,D,E,F)  
F={BCD→E,BCE→F,DE→A,D→C,CE→A}  
#### Candidate Keys:
BCD,BDE  
#### 1NF:
- Atomic  
→ In 1NF  
#### 2NF:
- DE→A  
- DE ⊂ BDE  
- A non-prime  
→ Partial dependency  
#### Result:
→ NOT in 2NF  
→ Highest = 1NF  

### 4. EXAMPLE 3
#### Given:
R(B,W,X,Y,Z)  
F={B→W,W→XYZ,X→Y}  
#### Candidate Key:
B  
#### 1NF:
- Atomic  
→ In 1NF  
#### 2NF:
- No composite key  
→ No partial dependency  
→ In 2NF  
#### 3NF:
- W→XYZ  
- W not superkey  
- RHS non-prime  
→ Violates 3NF  
#### Result:
→ Highest = 2NF  

### 5. EXAMPLE 4
#### Given:
R(X,Y,W,Z,B)  
F={XY→WZB,Z→X}  
#### Candidate Keys:
XY,YZ  
#### 1NF:
- Atomic  
→ In 1NF  
#### 2NF:
- Z→X  
- Z ⊂ YZ  
- X prime  
→ No partial dependency  
→ In 2NF  
#### 3NF:
- Z→X  
- RHS prime  
→ Satisfied  
#### BCNF:
- Z not superkey  
→ Violates BCNF  
#### Result:
→ Highest = 3NF  

### 6. EXAMPLE 5
#### Given:
R(A,B,C,D)  
F={A→B,B→C,C→D,D→A}  
#### Candidate Keys:
A,B,C,D  
#### 1NF:
- Atomic  
→ In 1NF  
#### 2NF:
- No composite key  
→ In 2NF  
#### 3NF:
- All attributes prime  
→ In 3NF  
#### BCNF:
- Every determinant is key  
→ In BCNF  
#### Result:
→ BCNF  

### 7. SYSTEMATIC METHOD
#### Steps:
1. Find candidate keys  
2. Identify prime/non-prime  
3. Check partial dependency  
4. Check transitive dependency  
5. Check BCNF condition  
#### Shortcut:
> LHS not superkey ⇒ violation  

### 8. FINAL TAKEAWAY
You now understand:
- How to find highest normal form  
- Step-by-step evaluation  
- Difference between 2NF,3NF,BCNF  
#### Mental Model
Find Key → Check Partial → Check Transitive → Check Superkey  

---
