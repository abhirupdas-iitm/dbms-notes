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
