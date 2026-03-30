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
## CS2001 – Week 4, Lecture 3
### 1. INTRODUCTION
Focus:
→ Converting **ER Diagrams → Relational Schema**
#### Goal
> Translate ER components into tables while preserving:
- Constraints  
- Relationships  
- Minimal redundancy  

### 2. STRONG ENTITY SET
#### Definition:
Entity with:
- Independent existence  
- Primary key  
#### Conversion Rule:
- Create one table  
- Include all attributes  
- Primary key → becomes table PK  
#### Example:
`Student(enrollmentNo, name, contact)`
#### Key Insight
> Strong entity → direct table mapping  

### 3. COMPOSITE ATTRIBUTE
#### Definition:
Attribute composed of smaller attributes  
Example:
```
Name → (Fname, Mname, Lname)
```
#### Conversion Rule:
- Break into components  
- Store each as separate column  
#### Result:
```
Student(enrollmentNo, Fname, Mname, Lname, contact)
```
#### Key Insight
> Composite attributes are flattened  

### 4. MULTIVALUED ATTRIBUTE
#### Problem:
One attribute → multiple values  
Example:
```
contact = {123, 456}
```
#### Wrong Approach
- Store as comma-separated values  
#### Issue:
- Difficult queries  
- Poor design  
#### Correct Approach
Create separate table:
```
Student(enrollmentNo, Fname, ...)
Contact(enrollmentNo, contact)
```
#### Key Insight
> Multivalued attribute → separate relation  

### 5. DERIVED ATTRIBUTE
#### Example:
- Age derived from DOB  
#### Rule:
- Do NOT store derived attributes  
- Store base attribute instead  
#### Result:
```
Store: DOB  
Do not store: Age
```
#### Key Insight
> Derived attributes are computed, not stored  

### RELATIONSHIP CONVERSION

### 6. MANY-TO-MANY (M:N)
#### Example:
Student ↔ Course  
#### Rule:
- Create new table for relationship  
#### Result:
```
Student(sid, name)
Course(cid, cname)
Enroll(sid, cid)
```
#### If relationship has attributes:
Add them to relationship table  
#### Example:
```
Enroll(sid, cid, enrollmentDate)
```
#### Key Insight
> M:N → always create new relation  

### 7. ONE-TO-MANY (1:N)
#### Example:
Course → Student  
#### Rule:
- Add primary key of “1 side” to “N side”  
#### Result:
```
Course(cid, cname)
Student(sid, name, cid)
```
#### Special Case:
If optional:
- Foreign key can be NULL  
#### Key Insight
> 1:N → no new table needed  

### 8. MANY-TO-ONE (N:1)
Same as 1:N but reversed  
#### Rule:
- Add primary key of “1 side” into “many side”  

### 9. ONE-TO-ONE (1:1)
#### Options:
1. Add FK in either table  
2. Merge both tables  
#### Special Case
If **full participation on both sides**:
→ Merge into single table  
#### Result:
```
ManagerDept(mid, mname, did, dname)
```
#### Key Insight
> 1:1 + full participation → merge tables  

### 10. PARTICIPATION CONSTRAINT
#### Types:
- Partial → optional  
- Total → mandatory  
#### Rule:
- Total participation → NOT NULL constraint  
- Partial → allow NULL  
#### Key Insight
> Participation controls NULL constraints  

### WEAK ENTITY SET
### 11. DEFINITION
- Depends on strong entity  
- Has partial key  
#### Rule:
- Include:
  - Partial key  
  - Primary key of strong entity  
#### Result:
```
Section(courseId, sectionId, semester, year)
```
#### Primary Key:
```
(courseId + sectionId + semester + year)
```
#### Key Insight
> Weak entity PK = strong PK + partial key  

### TERNARY RELATIONSHIP
### 12. DEFINITION
Relationship among 3 entities  
#### Rule:
- Create new table  
- Include PKs of all entities  
#### Example:
```
ProjectGuide(tid, sid, pid, hours)
```
#### Primary Key:
```
(tid, sid, pid)
```
#### Key Insight
> Ternary → always new relation  
### AGGREGATION
### 13. DEFINITION
Relationship between:
- Entity  
- AND another relationship  
#### Rule:
- Treat relationship as entity  
- Create table including:
  - All involved keys  
#### Key Insight
> Aggregation = relationship over relationship  

### SPECIALIZATION
### 14. TYPES
#### 1. Overlapping
- Entity can belong to multiple subclasses  
#### 2. Disjoint
- Entity belongs to only one subclass  
#### 3. Partial
- Some entities may not belong to any subclass  
#### 4. Total
- Every entity must belong to some subclass  

### 15. IMPLEMENTATION
#### Option 1:
Separate tables:
```
Person(id, name)
Faculty(id, salary)
Student(id, grade)
```
#### Option 2 (Optimization):
Add redundancy:
```
Faculty(id, name, salary)
Student(id, name, grade)
```
#### Trade-off:
- Less joins → better performance  
- More redundancy  
#### Key Insight
> Design = balance between redundancy and efficiency  

### 16. COMPLETE SPECIALIZATION
#### Rule:
- No need for parent table  
#### Example:
```
PurchasePart(pid, pname, price)
ManufacturePart(pid, pname, dept)
```
#### Key Insight
> Total specialization → remove parent table  

### FINAL SUMMARY
### 17. CONVERSION RULES

| ER Component          | Relational Mapping |
| --------------------- | ------------------ |
| Strong Entity         | Table              |
| Composite Attribute   | Split columns      |
| Multivalued Attribute | New table          |
| Derived Attribute     | Do not store       |
| M:N Relationship      | New table          |
| 1:N Relationship      | FK in N side       |
| 1:1 Relationship      | FK or merge        |
| Weak Entity           | Add owner key      |
| Ternary               | New table          |
| Aggregation           | Treat as entity    |

### BIG PICTURE
ER Diagram → Logical Design  
Relational Schema → Physical Structure  
#### Key Insight
> Good schema design = correct mapping + minimal redundancy  
### FINAL TAKEAWAY
You now understand:
- How to systematically convert ER → Tables  
- How constraints affect schema  
- How relationships translate into structure  
#### Mental Model
ER Diagram = Idea  
Schema = Implementation  

---
