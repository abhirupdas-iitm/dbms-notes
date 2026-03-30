## CS2001 – Week 4, Extra Lecture 1
### 1. INTRODUCTION
Focus:
→ Understanding **Division Operation in Relational Algebra**
### Goal
> Identify queries of the form:  
   “Find X such that it is related to ALL values of Y”

### 2. DIVISION OPERATION
#### Definition:
Division is a **binary operation**:
```
r(X) ÷ s(B)
```
Where:
- r has attributes (A, B)
- s has attribute (B)
- B ⊆ X
#### Output:
- Result contains attributes:
```
A = X − B
```
#### Key Insight
> Division finds values in A that are associated with **ALL values in s**

### 3. INTUITION (MOST IMPORTANT)
Division answers:
> “Which A values are paired with **every B value in s**?”
#### Think like this:
For each candidate A:
- Check ALL B in s  
- If ANY B is missing → reject  
#### Key Insight
> Division = “FOR ALL” condition  

### 4. BASIC EXAMPLE
Given:
```
r(A, B)
s(B)
```
#### Condition:
Include A if:
```
For every b ∈ s,
(a, b) exists in r
```
#### Result:
Only those A values that satisfy the condition

### 5. CASE ANALYSIS
#### Case 1:
s = {b2}
#### Result:
All A that appear with b2 in r
#### Case 2:
s = {b2, b3}
#### Result:
Only A values that appear with BOTH:
- b2  
- b3  
#### Key Insight
> More elements in s → stricter condition → fewer results  

### 6. FORMAL UNDERSTANDING
Let:
- X = attributes of r  
- B = attributes of s  
- A = X − B  
#### Then:
Result = `set of all tuples t[A]` such that:
```
For every tuple ts in s,
there exists tuple tr in r
with:
tr[A] = t
and tr[B] = ts
```
#### Key Insight
> You are filtering A based on **complete coverage of s**
### EXAMPLE 1 (SHOP – ITEM)
### 7. TABLES
#### Shop(counter, name, quantity)
#### Item(name, quantity)
#### Task:
```
Shop ÷ Item
```
#### Meaning:
Find counters that have **ALL items listed in Item**
#### Step-by-step:
- Check each counter  
- Verify if it has:
  - pen (40)  
  - notebook (20)  
#### Result:
```
c2, c3
```
#### Key Insight
> Only those counters that satisfy ALL item conditions survive
### EXAMPLE 2 (EMPLOYEE)
### 8. TABLES
#### `DepartmentLocation(department, location)`
#### `EmployeeDepartment(employee, department)`
#### Task:
Find employees working in:
```
ALL departments located in Campus2
```
#### Step 1:
Extract departments in Campus2:
```
T1 = π department (σ location = 'Campus2')
```
#### Step 2:
Divide:
```
EmployeeDepartment ÷ T1
```
#### Result:
Employees who work in ALL those departments
#### Example Result:
```
Jairaj, Ananya
```
#### Key Insight 🔥
> Division converts multi-condition requirement into one operation
### WHEN TO USE DIVISION
Use when question contains:
- “for all”  
- “in all”  
- “every”  
- “complete set”  
#### Examples:
- Students who took ALL courses  
- Employees in ALL departments  
- Shops selling ALL items  

### IMPORTANT PROPERTIES
### 9. CHARACTERISTICS
- Not commutative  
- Reduces attributes  
- Produces subset of A  

### 10. COMMON MISTAKE
- Checking “exists” instead of “for all”
#### Wrong thinking:
> If A appears with ANY B → include  
#### Correct thinking:
> A must appear with EVERY B  
### BIG PICTURE
Division = inverse of Cartesian product (conceptually)
#### Key Insight
> Division is the only operation that naturally expresses  
   “FOR ALL” in relational algebra  

### FINAL TAKEAWAY
You now understand:
- What division does  
- How to interpret it  
- When to apply it  
#### Mental Model 🧠
Selection → filters rows  
Join → combines tables  
Division → enforces **completeness constraint**  

---
## CS2001 – Week 4, Extra Lecture 2
### 1. INTRODUCTION
Focus:
→ Understanding **Tuple Relational Calculus (TRC)**
#### Goal
> Learn how to write queries using **logic instead of procedures**

### 2. NON-PROCEDURAL QUERY LANGUAGE
TRC is:
- **Non-procedural**
- You specify:
  - WHAT you want  
- Not:
  - HOW to compute it  
#### Key Insight
> TRC focuses on **result conditions**, not execution steps  

### 3. BASIC FORM
Every TRC query is of the form:
```
{ t | P(t) }
```
#### Where:
- `t` → tuple (result)  
- `P(t)` → predicate (condition)  
#### Meaning:
> Return all tuples `t` such that condition `P(t)` is TRUE  
#### Key Insight
> TRC = “Find all t such that P(t) holds”

### 4. LOGICAL OPERATORS
Predicates can use:
- AND ( ∧ )  
- OR ( ∨ )  
- NOT ( ¬ )  
#### Example:
```
t.age > 21 ∧ t.course = 'DBMS'
```

### 5. QUANTIFIERS (VERY IMPORTANT)
#### 1. EXISTS (∃)
```
∃ t ∈ R (P(t))
```
Meaning:
> There exists at least ONE tuple satisfying P(t)

#### 2. FOR ALL (∀)
```
∀ t ∈ R (P(t))
```
Meaning:
> P(t) must be TRUE for ALL tuples
#### Key Insight
> ∃ = at least one  
> ∀ = for every  
### BASIC EXAMPLE
### 6. QUERY
Find first names of students with:
```
age > 21
```
#### TRC:
```
{ t.Fname | t ∈ Student ∧ t.age > 21 }
```
#### Alternative form:
```
{ t | ∃ s ∈ Student (s.age > 21 ∧ t.Fname = s.Fname) }
```
#### Key Insight
> You can express same query in multiple equivalent forms  

### 🔴 JOIN-LIKE QUERIES
### 7. SCHEMA
- student(rollNo, name, year, courseId)  
- course(courseId, cname, teacher)  
#### QUERY:
Find names of students who took:
```
'DBMS'
```
#### TRC:
```
{ s.name |
  s ∈ student ∧
  ∃ c ∈ course (
    s.courseId = c.courseId ∧
    c.cname = 'DBMS'
  )
}
```
#### Key Insight
> Join in TRC = linking variables using conditions  
### MULTIPLE ATTRIBUTES
### 8. QUERY
Find:
- name  
- rollNo  
#### TRC:
```
{ s.name, s.rollNo |
  s ∈ student ∧
  ∃ c ∈ course (
    s.courseId = c.courseId ∧
    c.cname = 'DBMS'
  )
}
```
#### Key Insight
> Output attributes must be explicitly mentioned  
### COMPLEX EXAMPLE (AIRCRAFT)
### 9. SCHEMA
- Aircraft(`aid, aname, cruisingrange`)  
- Certified(`eid, aid`)  
- Employees(`eid, ename, salary`)  
#### QUERY
Find:
```
eids of pilots certified for Boeing aircraft
```
#### TRC:
```
{ C.eid |
  C ∈ Certified ∧
  ∃ A ∈ Aircraft (
    A.aid = C.aid ∧
    A.aname = 'Boeing'
  )
}
```
#### Key Insight
> Always match foreign keys explicitly  

### COMBINED CONDITIONS
### 10. QUERY
Find:
- names  
- salaries  
of certified pilots for Boeing  
#### TRC:
```
{ E.ename, E.salary |
  E ∈ Employees ∧
  ∃ C ∈ Certified ∧
  ∃ A ∈ Aircraft (
    E.eid = C.eid ∧
    C.aid = A.aid ∧
    A.aname = 'Boeing'
  )
}
```
#### Key Insight
> Multiple tables → multiple existential conditions  

###  ADVANCED QUERY
### 11. QUERY
Find flights that can be piloted by:
```
every pilot with salary > 100,000
```
#### Logic:
- Pilot must:
  - Be certified  
  - Have aircraft with range > flight distance  
#### TRC (Conceptual):
```
{ F.flno |
  F ∈ Flights ∧
  ∀ E ∈ Employees (
    E.salary > 100000 →
    ∃ C ∈ Certified ∧
    ∃ A ∈ Aircraft (
      E.eid = C.eid ∧
      C.aid = A.aid ∧
      A.cruisingrange > F.distance
    )
  )
}
```
#### Key Insight
> Division-like queries in TRC use **∀ (for all)**  

###  COMMON PATTERNS
### 12. MAPPING

| Concept    | TRC Pattern       |
| ---------- | ----------------- |
| Selection  | t ∈ R ∧ condition |
| Projection | { t.attribute }   |
| Join       | match attributes  |
| Division   | use ∀             |

### COMMON MISTAKES
### 13.
- Forgetting to bind variables  
- Missing join conditions  
- Confusing ∃ and ∀  
#### Correct Thinking:
- Always define:
  - Source relation  
  - Conditions  
  - Output attributes  

### BIG PICTURE
TRC is equivalent to:
- Relational Algebra  
- SQL  
#### Difference:
- RA → procedural  
- TRC → declarative  
#### Key Insight
> TRC = logic-based view of queries  

### FINAL TAKEAWAY
You now understand:
- TRC syntax  
- Quantifiers  
- How joins work in TRC  
- How to express complex queries  
#### Mental Model
SQL = Practical  
RA = Step-by-step  
TRC = Pure logic  

---