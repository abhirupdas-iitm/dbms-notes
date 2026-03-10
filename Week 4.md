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

### Notes taken from Activity Questions 4.2
1. Considering the relations **R**(A,B,C) and **P**(B,X,Y), the following expression will result in (A,B,C,X,Y): `R⋈P`. (Question: 7)
2. TRC is a *non-procedural* query language. (Question: 9)
---
## CS2001 – Week 4, Lecture 3
### 1. Module Recap
In the previous modules:
Topics covered include:
- Relational Algebra and its operators  
- Relational Calculus and predicate-based query formulation  
Both of these form the **formal mathematical foundation of relational databases**.
Going forward, these ideas will be used **interchangeably** while designing databases and writing queries.
From this module onward, the course transitions to **database design**.

### 2. Module Objective
Primary objective:
- Understand **how to design a database system for a real-world application**
Key tool introduced:
- **Entity–Relationship (E-R) Model**
The E-R model is used for **representing real-world systems in a structured conceptual form** before implementation.

### 3. Design Process Overview
Design always begins with a **requirement specification**.
Steps involved:
1. Understand the **functional specification**
2. Identify **stakeholders**
3. Identify **business rules and constraints**
4. Design a system that satisfies these requirements

Examples of possible applications:
- Academic systems (students, instructors, courses)
- Banking systems
- Financial systems
- Distributed systems such as national-scale applications

Important design considerations include:
- Performance requirements  
- Resource usage  
- Concurrency requirements  
- Response time requirements  
- Distribution of the system  

Example scenarios:
- A small store database might run on a **single PC**  
- A banking system requires **high concurrency and fast response time**  
- Nationwide systems (e.g., large public systems) require **distributed infrastructure**
Thus, database design must balance **requirements, resources, and system limitations**.

### 4. Key Components of the Design Process
At the beginning of database design, two important concepts are required:
1. **Abstraction**
2. **Modeling**
These help manage the complexity of real-world systems.

### 5. Abstraction
Abstraction means representing information at **different levels of detail**.
Human cognition has limitations:
- Short-term memory typically handles **5–7 items at a time**

Therefore abstraction helps by:
- Simplifying information
- Reducing complexity
- Ignoring irrelevant details
Example:
Consider a binary string:
```
110010101001
```
This is difficult to remember.
If grouped into **octal representation**:
```
6251
```
It becomes easier to remember.
Similarly, using **hexadecimal representation**:
```
CA9
```
Both representations contain the **same information**, but the abstraction level is different.
Thus abstraction allows us to:
- Handle complex information efficiently
- Focus only on relevant aspects
Example in database context:
When working with **student course data**, relevant attributes may include:
- Course
- Grades
- Attendance

Attributes like:
- Instructor salary
- Student date of birth
may not be relevant for that specific task.
Abstraction allows focusing only on **relevant attributes**.

### 6. Models
While abstraction simplifies information, **models represent real-world systems mathematically or logically**.
A model is a representation that allows reasoning about real-world behavior.
Examples from other fields:
Physics:
```
S = ut + (1/2)at²
```
Where:
- S = distance
- u = initial velocity
- t = time
- a = acceleration
This formula models **motion in the real world**.
Other examples:
Physics:
- Newton's laws
- Quantum mechanics models
Chemistry:
- Molecular structure models
Geography:
- Map projections
Electrical engineering:
- Circuit diagrams
- Transistor models
- Kirchhoff’s laws
These models represent the same real-world system from **different perspectives**.
Similarly, database systems require **models of real-world information systems**.

### 7. Database Design Approach
The overall database design process can be divided into three stages:
1. **Requirement Analysis**
2. **Database Design**
3. **Implementation**
#### Requirement Analysis
- Gather system requirements
- Define system functionality
- Identify stakeholders and constraints
#### Database Design
Two levels:
1. **Logical Design (Conceptual Model)**
2. **Physical Design**

Logical design focuses on:
- Structure of the data
- Relationships between data

Physical design focuses on:
- Storage structures
- Indexes
- Pages
- Data organization
In this module, the focus is on **logical design**.

### 8. Entity-Relationship (E-R) Model
The **Entity-Relationship model** is used to represent the conceptual design of a database.
Key idea:
Represent real-world objects and their relationships.
Two primary components:
1. **Entities**
2. **Relationships**

An **entity** is anything that can be distinguished as a separate object.
Example:
- Instructor
- Student
- Course
A **collection of similar entities** forms an **entity set**.
Example:
- All instructors → Instructor entity set
- All students → Student entity set
Entities are described using **attributes**.

### 9. Attributes
An attribute is a **property associated with an entity set**.
Example attributes:
Student:
- Student_ID
- Name
- Age

Instructor:
- Instructor_ID
- Name
- Salary
Each entity must be **uniquely identifiable** using attribute values.

### 10. Types of Attributes
Attributes can be categorized into different types.
#### Simple Attribute
A simple attribute contains a **single value**.
Examples:
- Age
- Salary
- Course_ID

#### Composite Attribute
A composite attribute consists of **multiple sub-attributes**.
Example:
Name
Components:
- First Name
- Middle Name
- Last Name

Example:
Address
Components:
- Street
- City
- State
- Postal Code
Even a **date** may be considered composite:
- Day
- Month
- Year
However, if a database system supports a **date data type**, it may be treated as a simple attribute.

#### Multi-Valued Attribute
A multi-valued attribute can have **multiple values for one entity**.
Example:
Phone numbers of a person.
A person may have:
- Personal number
- Work number
- Messaging number
Thus phone number is **multi-valued**.

#### Derived Attribute
A derived attribute is **computed from another attribute**.
Example:
Age.
Age changes every day, so it should not be stored directly.
Instead store:
```
Date_of_birth
```
Age is then computed when required.

### 11. Attribute Domain
Each attribute has a **domain**, which is the set of permitted values.
Example:
Age domain:

```
0 – 150
```

Course_ID domain:

```
valid course identifiers
```
Domains restrict allowed attribute values.

### 12. Entity Sets
An **entity set** is a collection of entities that share the same attributes.
Example:
Instructor entity set:
```
Instructor(ID, Name, Salary)
```
Student entity set:
```
Student(ID, Name)
```
Primary keys are used to uniquely identify entities.
Primary keys are usually **underlined** in schema notation.
Example:
```
Instructor(_ID_, Name, Salary)
```

### 13. Relationships
Relationships represent **associations between entity sets**.
Example:
Instructor — teaches — Course
This relationship indicates:
- Which instructor teaches which course.
Relationships may also have **attributes**.
Example:
Advisor relationship:
Student — advisor — Instructor
Possible relationship attribute:
```
Advisor_Start_Date
```
This stores when the instructor became the student's advisor.

### 14. Degree of Relationship
Relationships may involve multiple entity sets.
Binary relationship:
Between **two entity sets**.
Example:
`Student — takes — Course`
Ternary relationship:
Between **three entity sets**.

Example:
`Instructor — guides — Student — in Project`

Here we need:
- Instructor
- Student
- Project
Such relationships represent **three-way associations**.
However, database designs often try to **reduce higher-degree relationships into binary relationships** when possible.

### 15. Redundant Attributes
Sometimes attributes become **redundant due to relationships**.
Example:
Instructor entity:
```
Instructor(ID, Name, Dept_Name)
```
Department entity:
```
Department(Dept_Name, Details)
```
Relationship:
```
Instructor — works_for — Department
```
Since the relationship identifies the department of an instructor, the attribute `Dept_Name` in Instructor may become redundant.
However, redundancy decisions depend on the **overall schema design**.
Sometimes redundant attributes may still appear later during **relational table conversion**.

### 16. Cardinality Constraints
Cardinality constraints describe **how many entities from one set can relate to entities in another set**.
Types include:

#### One-to-One (1:1)
Each entity in set A is related to **exactly one entity in set B**.
Example:
Passport — Person

#### One-to-Many (1:N)
One entity in set A relates to **many entities in set B**.
Example:
Father → Children
One father may have multiple children.
But each child has one father.

#### Many-to-One (N:1)
Reverse of one-to-many.
Example:
Many employees work in **one department**.

#### Many-to-Many (M:N)
Entities in both sets may have multiple associations.
Example:
Students — take — Courses
- One student takes many courses
- One course has many students

### 17. Weak Entity Sets
Normally entity sets must have a **primary key**.
Such entity sets are called **strong entity sets**.
However, some entities cannot be uniquely identified using their own attributes.
These are called **weak entity sets**.
Weak entities rely on **another entity set for identification**.

### 18. Example of Weak Entity Set
Consider:
Building entity set:
```
Building(Building_Number, Building_Name, Address)
```
Primary key:
```
Building_Number
```
Apartment entity set:
```
Apartment(Door_Number, Floor)
```
Door_Number alone cannot uniquely identify apartments because:
```
Door_Number 201
```
may exist in many buildings.
Thus Apartment is a **weak entity set**.
Relationship:
```
Building — contains — Apartment
```
Every apartment belongs to **one building**.
A building may have **many apartments**.

### 19. Identifying Relationship
The relationship connecting a weak entity to a strong entity is called an **identifying relationship**.
Example:
```
Building — BA — Apartment
```
Rules:
1. Weak entity must have **total participation** in this relationship.
2. The weak entity key is formed by:
```
Primary Key of Strong Entity + Weak Entity Discriminator
```
Example:
```
Primary Key = (Building_Number, Door_Number)
```
Thus the weak entity borrows identity from the strong entity.

### 20. Module Summary
Topics discussed in this module:
Database design foundations:
- Requirement analysis
- Abstraction
- Modeling
Conceptual design using **Entity-Relationship model**:
- Entities
- Attributes
- Entity sets
- Relationships
Additional concepts:
- Types of attributes
- Cardinality constraints
- Weak entity sets
- Identifying relationships
These concepts form the **foundation of logical database design**, which will later be converted into relational tables and normalized schemas.

### Notes taken from Activity Questions 4.3
1. An attribute is a set of descriptive properties possessed by all members of an entity set. (Question: 2)
2. The relationship associating the weak entity set with the identifying entity set is called *identifying relationship*. (Question: 8)
---
## CS2001 – Week 4, Lecture 4
### 1. Module Recap
In the previous module, the **database design process** was introduced.
Key points discussed:
- Database design begins with **conceptual modeling**.
- The **Entity–Relationship (E-R) Model** is used for representing real-world requirements.
- The E-R model includes:
  - Entity sets
  - Attributes
  - Relationships
In this module, we move forward to:
1. Represent E-R models using **E-R diagrams**.
2. Convert E-R models into **relational schemas (tables)**.

### 2. Module Objective
Primary objectives:
- Understand **E-R diagram notation**
- Learn how to **translate E-R models into relational schemas**
Thus, this module bridges the gap between:
```
Conceptual design → Relational database implementation
```

### 3. E-R Diagram
An **E-R diagram** is a graphical representation of the E-R model.
It visually represents:
- Entity sets
- Attributes
- Relationships
- Cardinality constraints
- Participation constraints
These diagrams were introduced in the early days of database design and later became standardized, especially with the development of **Unified Modeling Language (UML)**.

### 4. Representation of Entity Sets
Entity sets are represented using **rectangles**.
Inside the rectangle:
- The **entity set name** is written
- Attributes are listed
Primary key attributes are **underlined**.
Example representation:
```
Instructor
---------
ID
name
salary
Student
---------
ID
name
tot_cred
```
This notation indicates that **ID is the primary key** for both entity sets.

### 5. Representation of Relationship Sets
Relationships between entity sets are represented using **diamonds**.
Example:
```
Instructor  — advisor — Student
```
Diagram structure:
```
Instructor ◇ advisor ◇ Student
```
Meaning:
- The relationship **advisor** connects Instructor and Student.
- By default, the relationship connects the **primary keys of the participating entity sets**.
Thus the relationship contains:
```
(instructor_id, student_id)
```

### 6. Relationships with Attributes
Sometimes relationships themselves may have attributes.
Example:
Advisor relationship may include:
```
date
```
representing when advising started.
Graphical notation:
- Relationship attribute is connected with a **dashed line** to the relationship diamond.
Example:
```
Instructor — advisor — Student
                  |
                 date
```
Important distinction:
- **Dashed line → attribute of relationship**
- **Solid line → relationship with another entity set**
Thus the relationship becomes:
```
(instructor_id, student_id, date)
```

### 7. Roles in Relationships
An entity set may participate **multiple times in the same relationship**.
Example:
Course prerequisite relationship.
```
Course — prereq — Course
```
Since both sides refer to the same entity set, **roles** are used.
Example roles:
```
course_id
prereq_id
```
Meaning:
- course_id → the course
- prereq_id → its prerequisite course
Thus roles help distinguish **different functions of the same entity set** in a relationship. 

### 8. Cardinality Constraints
Cardinality constraints specify **how many entities can participate in a relationship**.
In E-R diagrams:
- **Arrow → one**
- **Plain line → many**
Example:
#### One-to-One (1:1)
Each instructor advises at most one student, and vice versa.
```
Instructor → advisor → Student
```

#### One-to-Many (1:N)
One instructor may advise many students.
```
Instructor → advisor — Student
```
Meaning:
- Instructor → many students
- Each student → one instructor

#### Many-to-One (N:1)
Many students may have the same instructor.
```
Instructor — advisor → Student
```

#### Many-to-Many (M:N)
Multiple students may have multiple advisors.
```
Instructor — advisor — Student
```
No arrows appear on either side.

### 9. Participation Constraints
Participation constraints describe **whether participation is mandatory or optional**.
Two types:
#### Total Participation
Represented by **double lines**.
Meaning:
Every entity must participate in the relationship.
Example:
```
Student == advisor
```
Meaning:
Every student must have an advisor.

#### Partial Participation
Represented by **single line**.
Meaning:
Participation is optional.
Example:
```
Instructor — advisor
```
Meaning:
Some instructors may not advise any students.
Thus:
```
Student → total participation
Instructor → partial participation
```

### 10. Cardinality Bounds
More detailed constraints may be expressed using **minimum..maximum notation**.
Example:
```
0..*
```
Meaning:
- Minimum = 0
- Maximum = unlimited
Example relationship:
Instructor advising students:
```
Instructor 0..* → advisor → Student 1..1
```
Interpretation:
- Instructor may advise **0 or more students**
- Each student must have **exactly one advisor**. :contentReference[oaicite:2]{index=2}

### 11. Complex Attributes in E-R Diagrams
E-R diagrams can represent different attribute types.
#### Composite Attributes
Example:
```
Name
 ├ first_name
 ├ middle_initial
 └ last_name
```
Example:
```
Address
 ├ street
 │   ├ street_number
 │   ├ street_name
 │   └ apt_number
 ├ city
 ├ state
 └ zip
```

#### Multivalued Attributes
Multivalued attributes are shown using **curly braces**.
Example:
```
{phone_number}
```
Meaning:
An instructor may have multiple phone numbers.

#### Derived Attributes
Derived attributes are computed from other attributes.
Example:
```
age()
```
Age is derived from:
```
date_of_birth
```
Thus derived attributes are written using **function notation**.

### 12. Weak Entity Sets in E-R Diagrams
Weak entities are represented using **double rectangles**.
Example:
```
Course → Section
```
Section depends on Course.
Diagram rules:
1. Weak entity → **double rectangle**
2. Identifying relationship → **double diamond**
3. Discriminator → **dashed underline**

Example:
```
Section(sec_id, semester, year)
```
Discriminator:
```
(sec_id, semester, year)
```
Primary key becomes:
```
(course_id, sec_id, semester, year)
```
Thus the weak entity borrows part of its identity from the strong entity.

### 13. E-R Model to Relational Schema
After creating the E-R diagram, the next step is **converting it into relational tables**.
This process is called:
```
Reduction to relational schema
```
Each:
- Entity set
- Relationship set
becomes a **relation schema**.
A database corresponding to an E-R diagram is represented as a **collection of schemas**. 

### 14. Representing Entity Sets
For **strong entity sets**:
The relation contains the same attributes.
Example:
```
student(ID, name, tot_cred)
```
For **weak entity sets**:
Include the **primary key of the identifying strong entity set**.
Example:
```
section(course_id, sec_id, semester, year)
```

### 15. Representing Relationship Sets
A relationship set becomes a relation containing:
- Primary keys of participating entity sets
- Relationship attributes
Example:
Advisor relationship:
```
advisor(s_id, i_id)
```
Where:
- s_id → student ID
- i_id → instructor ID
If relationship had attribute date:
```
advisor(s_id, i_id, date)
```

### 16. Handling Composite Attributes
Composite attributes are handled by **flattening**.
Example:
Instead of:
```
name(first_name, last_name)
```
Use separate attributes:
```
first_name
last_name
```
Example schema:
```
instructor(
 ID,
 first_name,
 middle_initial,
 last_name,
 street_number,
 street_name,
 apt_number,
 city,
 state,
 zip_code,
 date_of_birth
)
```

### 17. Handling Multivalued Attributes
Multivalued attributes require **separate relations**.
Example:
Instructor has multiple phone numbers.
Create new schema:
```
inst_phone(ID, phone_number)
```
Each phone number becomes a separate tuple.
Example:
Instructor 22222 with two numbers:
```
(22222, 4567890)
(22222, 1234567)
```
Thus multivalued attributes are modeled using **separate relations**.

### 18. Redundancy in Schema
Some relationships may be redundant.
Example:
Relationship:
```
inst_dept
```
between Instructor and Department.
Instead of creating a separate table:
```
inst_dept(i_id, dept_name)
```
We can add attribute directly:
```
Instructor(ID, name, salary, dept_name)
```
This works when:
- Relationship is **many-to-one**
- Participation on the many side is **total**
This reduces the need for joins.
However if participation is partial, replacing relationships with attributes may introduce **NULL values**.

### 19. Redundancy with Weak Entities
The identifying relationship of a weak entity may also become redundant.
Example:
Section depends on Course.
Instead of keeping:
```
sec_course
```
relationship separately,
the schema already contains:
```
section(course_id, sec_id, semester, year)
```
Thus the identifying relationship may not require a separate table.

### 20. Module Summary
Topics covered:
E-R diagram representation:
- Entity sets
- Relationship sets
- Relationship attributes
- Roles
- Cardinality constraints
- Participation constraints
- Cardinality bounds

Advanced E-R concepts:
- Composite attributes
- Multivalued attributes
- Derived attributes
- Weak entity sets
Implementation step:
- Conversion of **E-R models into relational schemas**
This step transforms conceptual database design into **actual relational table structures**.

### Notes taken from Activity Questions 4.4
1. In E-R diagrams, a weak entity set is represented by double rectangle. (Question: 3)
---
## CS2001 – Week 4, Lecture 5

### 1. Introduction
This module concludes the discussion on **logical database design using the Entity–Relationship (ER) model**.
Previously discussed topics:
- ER diagrams
- Translation of ER models to relational schema
In this module we explore:
1. **Extended ER features**
2. **Important design considerations in ER modeling**

### 2. Extended ER Features
Extended ER features expand the basic ER model to handle **more complex real-world scenarios**.
Key topics include:
- Non-binary relationships
- Specialization (ISA hierarchy)
- Generalization
- Aggregation

### 3. Non-Binary Relationship Sets
Most relationships in database design are **binary relationships** (between two entity sets).
However, sometimes relationships naturally involve **more than two entities**.
Example: **Ternary Relationship**
Entities involved:
- Project
- Instructor
- Student

Relationship:
```
proj_guide(student, instructor, project)
```
Meaning:
A **student works on a project under the guidance of an instructor**.
The ER diagram for this relationship shows a **ternary relationship connecting the three entities**. 

# 4. Cardinality Constraints in Ternary Relationships
Cardinality constraints become more complex for ternary relationships.
Example:
If an arrow points to **Instructor**, it means:
> For a given student and project, there is **at most one instructor**.
However, if arrows appear toward multiple entities, ambiguity arises.
Possible interpretations:
1. Each **A entity uniquely determines B and C**
2. Each **pair (A,B)** determines C
3. Each **pair (A,C)** determines B
Because of this ambiguity:
**Rule:**  
For ternary relationships, **only one arrow is allowed** to indicate a cardinality constraint.

### 5. Specialization (ISA Relationship)
Specialization represents **hierarchical relationships between entities**.
It follows a **top-down design approach**.
Example hierarchy:
```
Person
│
├── Student
│     └── tot_credits
│
└── Employee
      └── salary
          ├── Instructor (rank)
          └── Secretary (hours_per_week)
```
Interpretation:
- **Student IS A Person**
- **Employee IS A Person**
- **Instructor IS A Employee**
Key property:

### Attribute Inheritance
Lower-level entities inherit:
- All attributes of the higher-level entity
- Participation in relationships
Example:
Instructor inherits:
```
Person attributes
+ Employee attributes
+ rank
```

### 6. Types of Specialization
#### 1. Overlapping Specialization
An entity may belong to **multiple subclasses**.
Example:
```
Person → Student
Person → Employee
```
A person can be both:
- Student
- Employee
Example: Teaching assistant.

#### 2. Disjoint Specialization
Entities belong to **only one subclass**.
Example:
```
Employee → Instructor
Employee → Secretary
```
An employee cannot be both instructor and secretary.

### 7. Completeness Constraints
Specialization may also be classified as:
#### Total Specialization
Every entity in the higher-level set **must belong to a subclass**.
Example:
```
Student → UG
Student → PG
```

Every student must be either:
- Undergraduate
- Postgraduate
Thus specialization is **total**.

#### Partial Specialization
Entities in the higher-level set **may or may not belong to subclasses**.
Example:
```
Person → Student
Person → Employee
```
A person might be neither.

### 8. Representing Specialization in Relational Schema
There are two major approaches.
#### Method 1: Separate Tables
Create:
```
Person(ID, name, street, city)

Student(ID, tot_credits)

Employee(ID, salary)
```
Key of Person becomes key of lower-level entities.
#### Advantage
- No redundancy.
#### Disadvantage
- Requires **joins** to obtain complete information.
Example:
To find student name and credits:
```
JOIN Student with Person
```

#### Method 2: Flattened Tables
Each subclass stores all attributes.
Example:
```
Student(ID, name, street, city, tot_credits)

Employee(ID, name, street, city, salary)
```
#### Advantage
- No joins required.
#### Disadvantage
- Redundant data if entity belongs to multiple subclasses.
Example:
If a person is both student and employee → duplicated attributes.

### 9. Generalization
Generalization is the **reverse of specialization**.
Instead of top-down design:
```
Top-down → Specialization
Bottom-up → Generalization
```
Example:
Start with:
```
Instructor
Secretary
```
Identify common attributes:
```
Person
```
Thus:
```
Instructor IS A Person
Secretary IS A Person
```
Generalization combines entity sets with similar properties into a **higher-level entity set**.

### 10. Aggregation
Aggregation is used when we need **relationships between relationships**.
Example scenario:
We have a ternary relationship:
```
proj_guide(student, instructor, project)
```
Now suppose we want to record:
```
evaluation of a student by instructor for a project
```
If we directly add another ternary relationship, redundancy occurs.
Instead:
Treat the relationship **proj_guide as an entity**.
This abstraction is called **aggregation**.
Result:
```
proj_guide → aggregated entity
eval_for → relationship with evaluation entity
```
Meaning:
A **student–project–instructor combination may have an evaluation**.
Aggregation eliminates redundancy and improves modeling clarity.

### 11. Representing Aggregation in Relational Schema
Schema includes:
- Primary key of aggregated relationship
- Key of related entity
- Additional attributes
Example schema:
```
eval_for(student_id, project_id, instructor_id, evaluation_id)
```
Here:
```
(student_id, project_id, instructor_id)
```
comes from the **aggregated relationship**.

### 12. Design Issues in ER Modeling
Several modeling decisions must be made during database design.
These choices depend on:
- Application requirements
- Data characteristics
- Query patterns
#### 12.1 Entities vs Attributes
Example: Phone number.
Option 1:
```
Instructor(ID, name, salary, phone_number)
```
Phone number is an **attribute**.
Option 2:
```
Instructor(ID, name, salary)

Phone(phone_number, location)

inst_phone(Instructor_ID, phone_number)
```
Phone is treated as an **entity set**.
Advantages:
- Allows multiple phone numbers
- Can store additional details (location, type)

#### 12.2 Entities vs Relationship Sets
Sometimes it is unclear whether a concept should be:
- Entity
- Relationship
Guideline:
Relationships often represent **actions between entities**.
Example:
```
Student — registration — Section
```
But sometimes the relationship itself may become an entity.

#### 12.3 Binary vs Non-Binary Relationships
Any non-binary relationship can theoretically be replaced by binary relationships.
Example:
Ternary relationship:
```
R(A, B, C)
```
Convert to:
```
E (artificial entity)
RA(E, A)
RB(E, B)
RC(E, C)
```
Each relationship stores part of the information.
However:
Some constraints involving all three entities may become harder to enforce.

### 13. Key Design Decisions
Important ER modeling decisions include:
1. Attribute vs Entity representation
2. Entity vs Relationship modeling
3. Binary vs Ternary relationships
4. Strong vs Weak entity sets
5. Use of specialization/generalization
6. Use of aggregation
These decisions influence:
- Data redundancy
- Query complexity
- Integrity constraints
- System performance

### 14. ER Notation
Standard ER notation symbols include:

| Symbol               | Meaning                       |
| -------------------- | ----------------------------- |
| Rectangle            | Entity set                    |
| Diamond              | Relationship set              |
| Double rectangle     | Weak entity                   |
| Underlined attribute | Primary key                   |
| Dashed underline     | Discriminator                 |
| Triangle (ISA)       | Specialization/generalization |
| Double line          | Total participation           |
These symbols are standardized and commonly used in database design tools.
### 15. Module Summary
This module completed the discussion of **Extended ER Modeling**.
Topics covered:
- Non-binary relationships
- Specialization (ISA hierarchy)
- Generalization
- Aggregation
- Schema representation
- Design issues in ER modeling
These concepts help create **accurate conceptual database models** that reflect real-world systems before implementation.

### Notes taken from Activity Questions 4.5
Nothing! Got all of them right!

---
