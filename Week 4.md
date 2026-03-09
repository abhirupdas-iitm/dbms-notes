## CS2001 – Week 4, Lecture 1
### 1. Week Recap
In the previous week, several features of the SQL language were discussed and practiced.
Topics covered include:
SQL query fundamentals:
- Basic query structure
- Nested subqueries

SQL data management:
- Data modification statements
- SQL expressions for joins and views

Database system features:
- Transactions
- Integrity constraints
- Additional SQL data types
- Authorization

Advanced SQL features:
- Functions and procedures
- Triggers
With that, the initial discussion of SQL concludes. The course now transitions toward **database modeling and database design**, beginning with **formal relational query languages**.

### 2. Module Objective
Primary objective:
- Understand **formal query languages** through relational algebra.

Relational algebra provides a **mathematical foundation for querying relational databases**, which is essential for understanding database design.

### 3. Formal Relational Query Languages

There are three formal relational query language frameworks:
1. Relational Algebra  
2. Tuple Relational Calculus  
3. Domain Relational Calculus  

Key distinctions:
Relational Algebra:
- Procedural
- Algebra-based

Tuple Relational Calculus:
- Non-procedural
- Predicate calculus-based

Domain Relational Calculus:
- Non-procedural
- Predicate calculus-based

Important idea:
Procedural languages describe **how to compute the result**, while non-procedural languages describe **what result is desired**.

### 4. Relational Algebra Overview
Relational algebra was introduced by **Edgar F. Codd at IBM in 1970**.
Important properties:
- It is a **procedural query language**
- Queries are written as **expressions composed of operators**
- Operators take one or two relations as input
- The result of every operation is **a new relation**

Six fundamental relational algebra operators:
- Selection (σ)
- Projection (Π)
- Union (∪)
- Set Difference (−)
- Cartesian Product (×)
- Rename (ρ)
These operators form the **core algebraic system of relational queries**.

### 5. Selection Operation (σ)
The selection operator retrieves tuples that satisfy a specified condition.
Notation:
σₚ(r)
Where:
- r is a relation
- p is the **selection predicate**

Formal definition:
σₚ(r) = { t | t ∈ r and p(t) }

The predicate p is a logical formula constructed using:

Logical operators:
- ∧ (AND)
- ∨ (OR)
- ¬ (NOT)

Each predicate term can be:
```
<attribute> op <attribute>  
<attribute> op <constant>
```
Comparison operators:
= , ≠ , > , ≥ , < , ≤
Example:
Select instructors belonging to the Physics department.
`σ dept_name = 'Physics' (instructor)`
This operation filters tuples satisfying the specified condition.

### 6. Projection Operation (Π)
Projection extracts **specific columns** from a relation.
Notation:
Π A<sub>1</sub>,A<sub>2</sub>,...,A<sub>k</sub> (r)

Where:
- A<sub>1</sub>,A<sub>2</sub>,...,A<sub>k</sub> are attribute names
- r is the relation

Operation behavior:
- Only the specified attributes are retained
- All other attributes are removed

Important property:
Since relations are **sets**, duplicate rows are automatically removed.
Example:
Remove the department name attribute from the instructor relation.
Π <sub>ID, name, salary (instructor)</sub>
Result:
A relation containing only the attributes ID, name, and salary.

### 7. Union Operation (∪)
Union combines tuples from two relations.
Notation:
`r ∪ s`
Formal definition:
`r ∪ s = { t | t ∈ r or t ∈ s }`
Conditions for union compatibility:
1. Both relations must have **the same arity** (same number of attributes)
2. Corresponding attributes must have **compatible domains**

Example:

Find course IDs of courses taught in Fall 2009 or Spring 2010.
Π <sub>course_id</sub> (σ semester = 'Fall' ∧ year = 2009 (section))
∪
Π <sub>course_id</sub> (σ semester = 'Spring' ∧ year = 2010 (section))
Union returns all tuples appearing in either relation.

### 8. Difference Operation (−)
The difference operator returns tuples present in one relation but not in another.
Notation:
`r − s`
Formal definition:
`r − s = { t | t ∈ r and t ∉ s }`

Requirements:
- Both relations must have the same arity
- Corresponding attributes must be compatible

Example:
Find courses taught in Fall 2009 but not in Spring 2010.
Π <sub>course_id</sub> (σ semester = 'Fall' ∧ year = 2009 (section))
−
Π <sub>course_id</sub> (σ semester = 'Spring' ∧ year = 2010 (section))

### 9. Intersection Operation (∩)
Intersection retrieves tuples common to both relations.
Notation:
`r ∩ s`
Definition:
`r ∩ s = { t | t ∈ r and t ∈ s }`

Conditions:
- Same arity
- Compatible attribute domains

Important identity:
`r ∩ s = r − (r − s)`
Thus intersection can be expressed using the difference operator.

### 10. Cartesian Product (×)
The Cartesian product pairs every tuple in one relation with every tuple in another relation.
Notation:
`r × s`
Formal definition:
`r × s = { t q | t ∈ r and q ∈ s }`
Assumption:
Attributes of r and s must be **disjoint**.
If attributes overlap, **renaming must be used**.
Example:
If relation r has m tuples and relation s has n tuples:
`|r × s| = m × n`
The result includes all possible tuple combinations.

### 11. Rename Operation (ρ)
The rename operator assigns a new name to a relation or its attributes.
Purpose:
- Refer to relations multiple times
- Avoid attribute name conflicts
- Improve readability

Basic notation:
`ρ X (E)`

Meaning:
Expression E is renamed to relation X.
Attribute renaming:
`ρ X(A1, A2, ..., An) (E)`

Conditions:
If E has arity n, exactly n attribute names must be provided.
Result:
A relation with renamed attributes and relation name.

### 12. Division Operation (÷)
Division is an advanced relational algebra operator.
It is applied to two relations:
`R(Z) ÷ S(X)`
Where:
`X ⊆ Z`
Define:
`Y = Z − X`
Then the result is a relation:
`T(Y)`
Definition:
A tuple t appears in the result T if:
`tR[Y] = t`
and
`tR[X] = ts`
for **every tuple `ts` in relation S**.
Interpretation:
For a tuple t to appear in the result:
- It must appear in relation R
- In combination with **every tuple of relation S**
Thus division expresses a **“for all” condition**.

### 13. Example Interpretation of Division
Example scenario:
Customer accounts across bank branches.
Account relation:
Account(customer, branch)
Branch relation:
Branch(branch)
Query:
Find customers who have accounts in **all branches**.
Relational algebra:
Account ÷ Branch
Result:
Customers who are associated with **every branch in the bank**.

### 14. Division as a Derived Operation
Division is **not a primitive operator**.
It can be expressed using other relational algebra operations.
Equivalent expression:
```
r ÷ s ≡ Π R−S (r)
       −
       Π R−S ((Π R−S (r) × s) − Π R−S,S (r))
```
Meaning:
Division can be implemented using:
- Projection
- Cartesian product
- Difference
However, having the division operator simplifies query writing.

### 15. Join as a Derived Operation
Join combines tuples from two relations based on a condition.
Conceptually:
Join = Selection + Cartesian Product
General form (Theta Join):
`r ⋈θ s`
Equivalent expression:
`σθ (r × s)`
Types of joins:
Theta Join:
- Condition uses any comparison operator
Equi Join:
- Condition uses equality
Natural Join:
- Equality applied to attributes with the same name
Join is considered a **derived operation** since it can be constructed from primitive relational algebra operators.

### 16. Module Summary
Concepts discussed in this module:
Relational algebra fundamentals:
- Selection (σ)
- Projection (Π)
- Union (∪)
- Difference (−)
- Cartesian Product (×)
- Rename (ρ)
Additional relational algebra operations:
- Intersection
- Division
- Join
These operations provide the **mathematical foundation for relational database queries and database design**.

### Notes taken from Activity Questions 4.1
Nothing! Got all of them correct!

---
## CS2001 – Week 4, Lecture 2
### 1. Module Recap
In the previous module, the foundational mathematics of relational databases was introduced.
Key topic covered:
- Relational Algebra and its operators.
Relational algebra provided a **procedural mathematical framework** for querying relational databases.
This module continues the discussion of **formal query languages**, introducing the **calculus-based query languages** and their relationship with relational algebra.

### 2. Module Objective
Primary objective:
- Introduce **calculus-based relational query languages**.
- Understand their relationship with **relational algebra**.
Important note:
The course will **not go deeply into relational calculus** because:
1. It requires deeper knowledge of **predicate calculus**.
2. Relational calculus is **equivalent to relational algebra**.
Since SQL and most practical database implementations follow the **relational algebra model**, the focus will remain there.
However, it is important to understand that **multiple formal models exist and are mathematically equivalent**.

### 3. Formal Relational Query Language Models
Three formal query frameworks exist:
1. Relational Algebra  
2. Tuple Relational Calculus  
3. Domain Relational Calculus  
These models differ mainly in **how queries are expressed**, but they are **equivalent in expressive power**.

Relational Algebra:
- Procedural
- Describes **how to compute results**

Relational Calculus:
- Non-procedural
- Describes **what result is desired**

### 4. Predicate Logic Foundation
Before understanding relational calculus, we need some basic ideas from **predicate logic**.
Predicate logic (or predicate calculus) is an **extension of propositional logic**.
Propositional logic is essentially **Boolean algebra**.
In Boolean algebra:
We have **Boolean variables (propositions)**.
Each variable can take only two values:
- True
- False

Logical operators used:
- AND ( ∧ )
- OR ( ∨ )
- NOT ( ¬ )

Example structure:
A ∧ B  
A ∨ B  
¬A  
When truth values are assigned to variables, the logical expression evaluates to a **final truth value**.

### 5. Extension to Predicate Calculus
Predicate calculus extends propositional logic by introducing two additional concepts:
- Predicates
- Quantifiers

This allows logical statements to describe **properties of variables**, not just simple true/false variables.
Thus predicate calculus can represent more complex statements than propositional logic.

### 6. Predicates
A **predicate** represents a property applied to a variable.
Example statement:
`x > 3`
This contains two components:
1. Variable: x  
2. Property: greater than 3
The **property** is the predicate.
We represent predicates as:
`P(x)`
Where:
- P = predicate
- x = variable

Example:
`P(x) = x > 3`
Once a value is assigned to x, the predicate becomes a **proposition**.
Examples:
```
P(5) → 5 > 3 → True  
P(2) → 2 > 3 → False  
```
Thus a predicate behaves like a **function returning a truth value**.
Predicates can be combined using logical operators:
- AND
- OR
- NOT
These combinations form **predicate calculus expressions**.

### 7. Multiple Variables in Predicates
Predicates are not limited to one variable.
Example:
`P(x, y)`
A predicate can contain **multiple variables**.
Once specific values are substituted for the variables, the predicate evaluates to a **true or false proposition**.

### 8. Quantifiers
Predicate logic introduces **quantifiers**, which express statements about **entire domains of values**.
A domain of discourse refers to the **set of values a variable can take**.
Example domain:
Natural numbers.
Quantifiers specify **how a predicate applies across that domain**.
Two main quantifiers exist:
1. Universal quantifier  
2. Existential quantifier

### 9. Universal Quantifier (∀)
The universal quantifier represents **“for all”**.
Notation:
`∀x P(x)`
Meaning:
The predicate **P(x) must be true for every element in the domain**.
Example predicate:
`P(x) : x + 2 > x`
If x belongs to real numbers:
`x + 2 > x is always true.`
Therefore:
`∀x P(x) is true.`
Another example:
Let:
`M(x) : x is mortal`
If the domain is **all human beings**, then:
`∀x M(x)`
means:
“All humans are mortal.”
Example where universal quantification is false:
`P(x) : x > 3  
Domain: natural numbers
This is false because:
1, 2, 3 do not satisfy the predicate.
Therefore:
`∀x P(x) is false.`
However, if the domain changes to:
All numbers with two or more digits,
then:
`∀x (x > 3)`
becomes true.
Thus truth depends on the **domain of discourse**.

### 10. Existential Quantifier (∃)
The existential quantifier means **“there exists”**.
Notation:
`∃x P(x)`
Meaning:
There exists **at least one value in the domain** for which the predicate is true.
Example:
`P(x) : x > 3  `
Domain: natural numbers
Here:
`∃x P(x)`
is true because values such as:
4, 5, 6 ...
satisfy the predicate.
Thus existential quantification requires **only one satisfying value**.

### 11. Tuple Relational Calculus (TRC)
Tuple Relational Calculus is a **non-procedural query language** based on predicate calculus.
General form:
`{ t | P(t) }`
Meaning:
The result is a **set of tuples t such that predicate P(t) is true**.
Components of predicate expressions may include:
- Attributes
- Constants
- Comparison operators
- Logical connectives (AND, OR, NOT)
- Implication
- Quantifiers
The predicate defines the **conditions a tuple must satisfy to appear in the result**.

### 12. Example: Students Older Than 21
Problem:
Find the **first names of students whose age is greater than 21**.
Predicate logic formulation:
Let:
t = tuple from Student relation.
Condition:
`Student(t) ∧ t.age > 21`
Result expression:
`{ t.first_name | Student(t) ∧ t.age > 21 }`
Interpretation:
Return the first name attribute of tuples in the **Student relation** whose age is greater than 21.

### 13. Example: Students Taking DBMS
Problem:
Find names of students who have taken the course **DBMS**.
Logical interpretation:
For each student s:
There must exist a course c such that:
- s.course_id = c.course_id
- c.course_name = DBMS
Predicate expression conceptually states:
Return student names where a matching course with name DBMS exists.

### 14. Example: Pilot Certification Database
Relations:
```
Employees  
Aircraft  
Certified  
Flights
```
Query:
Find employee IDs of **pilots certified to fly Boeing aircraft**.
Logical reasoning:
1. Identify aircraft with name Boeing.
2. Identify certification records linking employees to aircraft.
3. Match aircraft IDs with certification entries.
Tuple calculus formulation:
Return employee IDs from Certified relation such that:
- There exists an Aircraft tuple
- Aircraft name = Boeing
- Aircraft ID matches certification record.
Thus the predicate connects **Certified and Aircraft relations**.

### 15. Safety of Expressions
Tuple relational calculus requires **safe expressions**.
A safe expression guarantees that the result set is **finite**.
Example of unsafe expression:
`{ t | t ∉ r }`
This expression attempts to retrieve all tuples **not in relation r**.
Since the universe of possible tuples is infinite, the result could become infinite.
Therefore:
Queries must be written so that the resulting set is **bounded by existing relations**.
In practical systems like SQL, safety constraints are **automatically enforced**.

### 16. Domain Relational Calculus (DRC)
Domain relational calculus is similar to tuple relational calculus.
Key difference:
Tuple Relational Calculus:
- Variables represent **entire tuples**.
Domain Relational Calculus:
- Variables represent **individual attributes**.

Example:
Tuple relational calculus:
t
Domain relational calculus:
`x1, x2, ..., xn`
Thus each attribute becomes a separate variable.
Conceptually both models are **equivalent**.
The difference is only **syntactic notation**.

### 17. Equivalence of Algebra and Calculus
Relational Algebra and Relational Calculus are **equivalent in expressive power**.
This means:
`Any query written in relational algebra can be written in relational calculus.`
Similarly:
Any relational calculus expression can be expressed using relational algebra.
Equivalence is shown by demonstrating that each relational algebra operator has an equivalent calculus expression.

Examples include:
```
Selection  
Projection  
Union  
Difference  
Cartesian Product  
Join
```
Each operator can be expressed through predicate calculus formulations.
Formal proofs of equivalence exist in database theory literature.

### 18. Module Summary
Concepts covered in this module:
Predicate logic fundamentals:
- Propositional logic
- Predicates
- Quantifiers

Relational calculus models:
- Tuple Relational Calculus
- Domain Relational Calculus

Important ideas:
- Relational calculus is **non-procedural**
- Queries specify **what result is desired**
- Relational algebra and relational calculus are **mathematically equivalent**
In practice, database systems rely primarily on **relational algebra concepts**, while relational calculus provides a **logical theoretical foundation**.
