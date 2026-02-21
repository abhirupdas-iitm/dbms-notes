# CS2001 – Week 2, Lecture 1
### 1. Week Recap
- DBMS widely used across domains → motivation for study.
- File-system based applications are limited compared to DBMS.
- Basic notions of DBMS introduced previously.
- Now moving toward the relational model in detail.
### 2. Lecture Objectives
- Understand attributes and their types.
- Understand mathematical structure of relational model:
  - Schema
  - Instance
  - Keys
- Familiarize with relational query languages.
### 3. Example of a Relation
- A relation is represented as a table.
- Columns → attributes.
- Rows → tuples (records).
- Order of columns does not matter; attribute names matter.
- Each row corresponds to a specific entity occurrence.
Example:
instructor(ID, name, dept_name, salary)

Each row:
(ID value, name value, dept_name value, salary value)
### 4. Attributes
#### 4.1 Definition
- Attributes describe properties of an entity.
- Only relevant attributes are chosen (business decision).
- Each attribute has:
  - A name
  - A domain (set of allowed values)
  - An atomic type
#### 4.2 Example: Students Relation
Students = (Roll#, FirstName, LastName, DoB, Passport#, Aadhaar#, Department)

Domains:
- Roll# → Alphanumeric string
- FirstName, LastName → Alpha string
- DoB → Date
- Passport# → String (Letter + 7 digits), nullable
- Aadhaar# → 12-digit number
- Department → Alpha string
#### 4.3 Domain
- Domain = set of allowed values for an attribute.
- Every attribute value must belong to its domain.
- Example:
  - If DoB is of type Date, cannot store "27th March 1997" as free text.
  - If Roll# is alphanumeric, it must match that format.
#### 4.4 Atomicity
- Attribute values are atomic (indivisible).
- Cannot combine multiple logical values into one attribute.
  - FirstName and LastName should not be merged.
- Relational model assumes atomic attributes.
#### 4.5 Null Value
- Null ∈ every domain.
- Indicates:
  - Value unknown
  - Value not applicable
- Example:
  - Passport# can be null.
- Null creates complications in certain operations.
### 5. Schema and Instance
#### 5.1 Relation Schema
- Let A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub> be attributes.
- Relation schema:
R = (A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>)

Example:
instructor = (ID, name, dept_name, salary)

Schema specifies:
- Attribute names
- Their domains
- Their types
- No actual data
#### 5.2 Formal Definition
Let D<sub>1</sub>, D<sub>2</sub>, ..., D<sub>n</sub> be domains of A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>.

A relation r is a subset of:
D<sub>1</sub> x D<sub>2</sub> x ... x D<sub>n</sub>

Thus:
r ⊆ D<sub>1</sub> x D<sub>2</sub> x ... x D<sub>n</sub>

Each tuple:
t = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>)
where ai ∈ Di

A relation is a set of n-tuples.
#### 5.3 Relation Instance
- Actual data stored in table form.
- A snapshot of data at a given time.
- Instance changes; schema remains fixed.

Example:
instructor ≡ String(5) × String × String × Number+
#### 5.4 Properties of Relations
- Order of tuples is irrelevant.
- Relations are sets → no ordering.
- No two tuples can be identical.
- Every tuple must be unique.
### 6. Keys
#### 6.1 Superkey
Let K ⊆ R (R = set of attributes).

K is a superkey if:
Values of K uniquely identify each tuple in every possible relation instance.

Example:
For instructor:
- {ID} is a superkey.
- {ID, name} is also a superkey.
#### 6.2 Candidate Key
A superkey K is a candidate key if:
- K is minimal.
- No proper subset of K is a superkey.

Example:
- {ID} is a candidate key.
- {ID, name} is not minimal → not a candidate key.
#### 6.3 Primary Key
- One candidate key chosen as primary key.
- Used for tuple identification in practice.
#### 6.4 Example: Students Relation

Students = (Roll#, FirstName, LastName, DoB, Passport#, Aadhaar#, Department)

Superkeys:
- {Roll#}
- {Roll#, DoB}

Candidate Keys:
- {Roll#}
- {FirstName, LastName}
- {Aadhaar#}

Passport# cannot be a key because:
- It is nullable.
- Null cannot uniquely identify tuples.

Primary Key:
- Roll#

Reason:
Roll# encodes useful information:
Example: 14CS92P01
- 14 → Admission year
- CS → Department
- 92 → Category
- P → Type of admission
- 01 → Serial number

Thus Roll# is both unique and semantically meaningful.
#### 6.5 Types of Keys

Secondary / Alternate Key:
- Candidate keys not chosen as primary.
- Example: {FirstName, LastName}, Aadhaar#

Simple Key:
- Single attribute key.
- Example: Roll#

Composite Key:
- More than one attribute.
- Example: {FirstName, LastName}

Compound Key:
- Multiple attributes, each individually a simple key.
- Example: {Roll#, Course#}
#### 6.6 Surrogate Key
- Artificially generated unique identifier.
- Not derived from application data.
- Example: Order number in an e-commerce system.
- Used when natural attributes cannot uniquely identify tuples.

Difference:
- Natural key → derived from real-world data (Roll#, Aadhaar#).
- Surrogate key → system-generated (OrderID).
#### 6.7 Foreign Key
Foreign key constraint:
- Value in one relation must appear in another.

Referencing relation:
- Enrolment(Roll#, Course#)

Referenced relations:
- Students(Roll#)
- Courses(Course#)

Foreign key enforces referential integrity.
### 7. Relational Query Languages
#### 7.1 Procedural vs Declarative
Procedural:
- Specify how to compute.
- Example languages: C, C++, Java, Python.
- Programmer provides algorithm.

Example: Square root of n
1. Guess x<sub>0</sub>
2. x<sub>i</sub>+1 = (x<sub>i</sub> + n/x<sub>i</sub>)/2
3. Repeat until convergence

Declarative:
- Specify what result is required.
- Not how to compute it.

Example:
Find m such that:
m<sup>2</sup> = n

#### 7.2 Relational Query Paradigm
Relational model uses declarative style.

Pure relational languages:
- Relational Algebra
- Tuple Relational Calculus
- Domain Relational Calculus

Properties:
- Equivalent in expressive power.
- Not Turing-complete.
- Relational Algebra:
  - Not Turing-machine equivalent.
  - Has 6 basic operations.
  - Will be focus of study.

### 8. Lecture Summary
- Defined attributes and domains.
- Understood atomicity and null.
- Defined relation schema and instance formally.
- Relations are unordered sets of unique tuples.
- Introduced:
  - Superkey
  - Candidate key
  - Primary key
  - Composite key
  - Surrogate key
  - Foreign key
- Introduced procedural vs declarative paradigms.
- Previewed relational query languages.

---
---
# CS2001 – Week 2, Lecture 2
### 1. Module Recap
- Relational model basics introduced:
  - Attributes and domains
  - Schema and instance
  - Keys (superkey, candidate key, primary key, foreign key)
- Relational query languages introduced at a high level.
- Now focus on relational algebra and its operators.
### 2. Module Objectives
- Understand relational algebra.
- Learn core relational algebra operators.
- Understand aggregation operators.
- Understand limitations of relational algebra.
### 3. Basic Properties of Relations
- A relation is a set.
- Therefore:
  - Ordering of tuples is irrelevant.
  - No duplicate tuples allowed.
- Example:
  - If (a1, b1) appears twice → invalid.
  - Relations must contain distinct tuples only.
- These properties affect behavior of projection, union, join, etc.
### 4. Relational Operators
#### 4.1 Selection (σ) – Row Filtering
- Syntax:
  `σ<sub>condition</sub>(r)`
- Returns:
  - Subset of tuples in r satisfying condition.
- Example:
  `σ<sub>A=B ∧ D>5</sub>(r)`
- Logical operators allowed:
  - ∧ (AND)
  - ∨ (OR)
  - Comparison operators (=, >, <, etc.)
- Output:
  - Relation with same schema as r.
  - Fewer or equal tuples.
#### 4.2 Projection (π) – Column Selection
- Syntax:
  `π<sub>A,C</sub>(r)`
- Keeps only specified attributes.
- Removes other attributes entirely.
- Important:
  - Duplicate tuples generated after projection are eliminated.
- Example:
  `π<sub>A</sub>(r)`
  → Only attribute A.
  → If values repeat, duplicates removed.
- Output:
  - Relation with fewer attributes.
  - Possibly fewer tuples due to duplicate removal.
#### 4.3 Union (∪)
- Syntax:
  `r ∪ s`
- Requirement:
  - r and s must have identical schemas (same attributes, same domains).
- Result:
  - All tuples from both.
  - Duplicate tuples removed (set semantics).
#### 4.4 Set Difference (−)
- Syntax:
  `r − s`
- Requirement:
  - r and s must have identical schemas.
- Result:
  - Tuples in r that are not in s.
#### 4.5 Intersection (∩)
- Syntax:
  `r ∩ s`
- Result:
  - Tuples common to both r and s.
- Not independent:
  `r ∩ s = r − (r − s)`
#### 4.6 Cartesian Product (×)
- Syntax:
  `r × s`
- Result:
  - All possible pairings of tuples from r and s.
- If:
  - |r| = m
  - |s| = n
- Then:
  - |r × s| = m × n
- Schema:
  - Attributes of r followed by attributes of s.
##### Naming Issue
- If r and s share attribute names:
  - Cannot have duplicate attribute names in result.
  - Use qualification:
    `r.B` and `s.B`
- Necessary especially for self-product.
#### 4.7 Renaming (ρ)
- Syntax:
   ρ<sub>X</sub>(E)
- Returns:
  - Expression E under name X.
- Used for:
  - Self joins.
  - Disambiguation.
- Example:
  r × ρ<sub>s</sub>(r)
#### 4.8 Composition of Operations
- Operators can be nested.
- Example:
  σ<sub>A=C (r × s)</sub>
- Process:
  1. Compute r × s.
  2. Apply selection.
- Output always a relation.
### 5. Natural Join (⋈)
#### 5.1 Definition
- Let r and s be relations on schemas R and S.
- Natural join:
  `r ⋈ s`
- Result schema:
  `R ∪ S`
- For each pair (t<sub>r</sub>, t<sub>s</sub>):
  - If values match on attributes in `R ∩ S`,
    include combined tuple.
#### 5.2 Key Characteristics
- Only tuples agreeing on common attribute names are combined.
- Duplicate columns from `R ∩ S` removed in output.
- Stronger than Cartesian product.
#### 5.3 Equivalent Expression
r ⋈ s =
π<sub>A,r.B,C,r.D,E</sub>(σ<sub>r.B=s.B ∧ r.D=s.D (r × s)</sub>)
Steps:
1. Cartesian product.
2. Select tuples where common attributes match.
3. Project to remove duplicate columns.

- Natural join is widely used in query processing.
- Core operation in relational querying.
### 6. Aggregate Operators
#### 6.1 Purpose
- Compute summary values.
- Examples:
  - SUM
  - AVG
  - MAX
  - MIN
#### 6.2 Behavior
- Input:
  - A relation.
- Output:
  - A single value (not a relation).
- Example:
  SUM(B)
  MAX(salary)
#### 6.3 Difference from Relational Operators
Relational operators:
- Input: relation(s)
- Output: relation

Aggregate operators:
- Input: relation
- Output: single scalar value

- Aggregates are not part of pure relational algebra.
- Used in practical query languages (e.g., SQL).
### 7. Notes on Relational Languages
- Each query input:
  - One or more relations.
- Each query output:
  - A relation.
- Output values must originate from input relations.
- Relational algebra is not Turing complete.
  - Cannot express all possible computations.
  - Requires host programming language for general algorithms.
### 8. Summary of Core Operators
Unary Operators:
- σ (Selection)
- π (Projection)
- ρ (Renaming)

Binary Operators:
- ∪ (Union)
- − (Difference)
- ∩ (Intersection)
- × (Cartesian Product)
- ⋈ (Natural Join)

Aggregate Operators:
- SUM
- AVG
- MAX
- MIN
### 9. Module Summary
- Introduced relational algebra.
- Studied:
  - Selection
  - Projection
  - Union
  - Difference
  - Intersection
  - Cartesian Product
  - Renaming
  - Natural Join
- Understood aggregate operators.
- Noted that relational algebra:
  - Is declarative.
  - Is not Turing complete.
  - Always returns relations (except aggregates).

---
---
# CS2001 – Week 2, Lecture 3
### 1. Module Recap
- Relational algebra introduced.
- Studied operators: selection, projection, union, difference, Cartesian product, natural join.
- Now moving to practical relational query language: SQL.
### 2. Module Objectives
- Understand relational query language (SQL).
- Understand Data Definition Language (DDL).
- Understand Data Manipulation Language (DML) basic query structure.
### 3. History of SQL
#### 3.1 Origin
- Developed by IBM (San Jose Research Lab).
- Originally called SEQUEL (Structured English Query Language).
- Later renamed Structured Query Language (SQL).
- Still pronounced “sequel”.
#### 3.2 Standardization
- SQL-86 → First ANSI standard.
- SQL-89 → Added integrity constraints.
- SQL-92 → Major ISO standard (ISO/IEC 9075). Became de facto industry standard.
#### 3.3 Major Revisions
- SQL:1999
  - Regular expressions
  - Recursive queries (transitive closure)
  - Triggers
  - Procedural/control flow support
  - Arrays and structured types
  - SQL embedding in Java (SQL/OLB)
  - Java embedding in SQL (SQL/JRT)
- SQL:2003
  - XML support (SQL/XML)
  - Window functions
  - Identity columns
- SQL:2006
  - Full XML integration
- SQL:2008
  - ORDER BY outside cursors
  - INSTEAD OF triggers
  - TRUNCATE
- SQL:2011
  - Temporal data
- SQL:2016
  - JSON support
  - Row pattern matching
- SQL:2019
  - Multidimensional arrays (MDarray)
#### 3.4 Compliance
- SQL is de facto standard for relational databases.
- Most systems comply at least with SQL-92.
- Many support SQL-2003 or later.
- Syntax differences may exist across systems.
- Always consult system documentation.
#### 3.5 Alternatives and Derivatives
- No real alternative protocol to SQL for relational databases.
- Frontend alternatives exist:
  - LINQ (.NET)
  - ScalaQL
  - ActiveRecord (Ruby)
  - HaskellDB
- Derivative language:
  - SPARQL (for RDF / Graph databases)
  - Standardized by W3C
  - Used in semantic web and graph DBs
### 4. Data Definition Language (DDL)
#### 4.1 Purpose
DDL specifies:
- Relation schema
- Attribute domains
- Integrity constraints
- Indices
- Security
- Storage structure
#### 4.2 Domain Types in SQL
- char(n) → fixed-length string
- varchar(n) → variable-length string (max n)
- int → integer
- smallint → small integer
- numeric(p, d) → fixed-point number
  - p = total digits
  - d = digits after decimal
- real, double precision → floating point
- float(n) → floating point with precision
Example:
numeric(8,2)
→ up to 8 digits total
→ 2 digits after decimal
### 5. CREATE TABLE
#### 5.1 General Form
create table r (
A<sub>1</sub> D<sub>1</sub>,
A<sub>2</sub> D<sub>2</sub>,
...
A<sub>n</sub> D<sub>n</sub>,
integrity-constraint1,
...
integrity-constraint<sub>k</sub>
);
- r → relation name
- A<sub>i</sub> → attribute
- D<sub>i</sub> → data type
#### 5.2 Example: Instructor Table
```create table instructor (
ID char(5),
name varchar(20),
dept_name varchar(20),
salary numeric(8,2)
);
```
#### 5.3 Integrity Constraints
- not null
- primary key (A<sub>1</sub>,...,A<sub>n</sub>)
- foreign key (...) references r
Example:
```
create table instructor (
ID char(5),
name varchar(20) not null,
dept_name varchar(20),
salary numeric(8,2),
primary key (ID),
foreign key (dept_name) references department
);
```
Notes:
- primary key automatically implies not null.
- foreign key enforces referential integrity.
### 6. University Schema Examples
#### 6.1 Student Table
```
create table student (
ID varchar(5),
name varchar(20) not null,
dept_name varchar(20),
tot_cred numeric(3,0),
primary key (ID),
foreign key (dept_name) references department
);
```
#### 6.2 Course Table
```
create table course (
course_id varchar(8),
title varchar(50),
dept_name varchar(20),
credits numeric(2,0),
primary key (course_id),
foreign key (dept_name) references department
);
```
#### 6.3 Takes Table (Composite Key)
```
create table takes (
ID varchar(5),
course_id varchar(8),
sec_id varchar(8),
semester varchar(6),
year numeric(4,0),
grade varchar(2),
primary key (ID, course_id, sec_id, semester, year),
foreign key (ID) references student,
foreign key (course_id, sec_id, semester, year)
references section
);
```
- Composite primary key.
- Multiple foreign keys possible.
### 7. Updating Tables
#### 7.1 Insert (DML)
`insert into instructor values ('10211','Smith','Biology',66000);`
#### 7.2 Delete (DML)
`delete from student;`
- Removes all tuples.
- Table structure remains.
#### 7.3 Drop Table (DDL)
`drop table r;`
- Removes table completely.
#### 7.4 Alter Table (DDL)
Add attribute:
`alter table r add A D;`
- Existing tuples get NULL for new attribute.

Drop attribute:
`alter table r drop A;`
- Removes attribute (not supported in some systems).
### 8. Data Manipulation Language (DML)
#### 8.1 Basic Query Structure
select A<sub>1</sub>, A<sub>2</sub>, ... , A<sub>n</sub>
from r<sub>1</sub>, r<sub>2</sub>, ..., r<sub>m</sub>
where P;
- A<sub>i</sub> → attributes
- r<sub>i</sub> → relations
- P → predicate (Boolean condition)
- Result → relation
Structure:
- select → projection
- from → Cartesian product
- where → selection
### 9. Select Clause
#### 9.1 Basic Form
`select name from instructor;`
- Case-insensitive.
- Corresponds to projection.
#### 9.2 Duplicates
- SQL allows duplicates by default.
- Use distinct to remove duplicates:
`select distinct dept_name from instructor;`
- Use all to explicitly allow duplicates:
`select all dept_name from instructor;`
#### 9.3 Special Forms
Select all attributes:
`elect * from instructor;`

Literal without from:
`select '437';`

Literal with alias:
`select '437' as FOO;`

Literal with from:
`select 'A' from instructor;`
- Produces N rows with value 'A'.
#### 9.4 Arithmetic Expressions
`select ID, name, salary/12 from instructor;`
Rename column:
`select ID, name, salary/12 as monthly_salary from instructor;`
### 10. Where Clause
- Specifies condition.
- Corresponds to selection.
Example:
```
select name
from instructor
where dept_name = 'Comp. Sci.';
```
Compound condition:
```
select name
from instructor
where dept_name = 'Comp. Sci.' and salary > 80000;
```
Logical operators:
- and
- or
- not
Arithmetic expressions allowed in conditions.
### 11. From Clause
- Lists relations in query.
- Corresponds to Cartesian product.
Example:
`select * from instructor, teaches;`
- Produces Cartesian product.
- Common attribute names qualified:
  instructor.ID
  teaches.ID

Cartesian product alone is rarely useful.
Combined with where clause:
```
select *
from instructor, teaches
where instructor.ID = teaches.ID;
```
- Produces meaningful join-like result.
### 12. Conceptual Mapping to Relational Algebra
- select clause → projection (π)
- where clause → selection (σ)
- from clause → Cartesian product (×)
- select + from + where together → equivalent to relational algebra expression.
### 13. Module Summary
- Introduced SQL history and evolution.
- Understood DDL:
  - create table
  - integrity constraints
  - alter, drop
- Understood DML basic query structure:
  - select
  - from
  - where
- Understood duplicates behavior.
- Understood relation to relational algebra.

---
---
# CS2001 – Week 2, Lecture 4
### 1. Module Recap
- We introduced SQL.
- We discussed DDL and basic query structure.
- We studied the select–from–where form.
- We now complete our understanding of the basic query structure.
### 2. Module Objectives
- To complete the understanding of basic query structure.
- To study additional basic SQL operations:
  - Cartesian Product
  - Rename (AS)
  - String Operations
  - Order By
  - Select Top / Fetch
  - Where Clause Predicates
  - Duplicates
### 3. Cartesian Product
#### 3.1 Basic Form
`select * from instructor, teaches;`
- Produces the Cartesian product of instructor × teaches.
- Every instructor tuple is paired with every teaches tuple.
- All attributes from both relations appear in the result.
- If attribute names are common (e.g., ID), they are qualified:
  - instructor.ID
  - teaches.ID
#### 3.2 Why Cartesian Product Alone Is Not Useful
- It produces many meaningless tuples.
- Example:
  - instructor.ID ≠ teaches.ID → meaningless pairing.
- Useful only when combined with a where clause (selection).
#### 3.3 Equi-Join Example
Find names of instructors who have taught some course and the course id:
```
select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID;
```
- This performs:
  - Cartesian product
  - Selection on matching IDs
- Equivalent to equi-join / natural join in relational algebra.
#### 3.4 Adding Additional Condition
Find instructors in the Art department who have taught some course:
```
select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID
and instructor.dept_name = 'Art';
```
- First condition → join.
- Second condition → department restriction.
### 4. Rename (AS) Operation
#### 4.1 Syntax
`old_name as new_name`
- Used to rename:
  - Relations
  - Attributes
Keyword as is optional:
instructor as T ≡ instructor T
#### 4.2 Self-Join Example
Find instructors whose salary is higher than some instructor in 'Comp. Sci':
select distinct T.name
from instructor as T, instructor as S
where T.salary > S.salary
  and S.dept_name = 'Comp. Sci.';
- We create two instances of instructor:
  - T
  - S
- Compare T.salary and S.salary.
- Restrict S to Comp. Sci.
This is necessary for self-join operations.
### 5. Cartesian Product and Hierarchies
Given relation emp_super(person, supervisor):
Tasks:
- Find supervisor of "Bob".
- Find supervisor of supervisor of "Bob".
- Find all supervisors (direct and indirect) of "Bob".
Basic query:
```
select supervisor
from emp_super
where person = 'Bob';
```
To find supervisor of supervisor:
- Use self-join via Cartesian product.
- Match supervisor of one row with person of another row.
Recursive hierarchy requires repeated joining or recursive queries (later topic).
### 6. String Operations
#### 6.1 LIKE Operator
Used for pattern matching.
Special characters:
- % → matches any substring (including empty)
- _ → matches any single character
#### 6.2 Example
Find instructors whose name contains "`dar`":
```
select name
from instructor
where name like '%dar%';
```
Matches:
- Darwin
- Majumdar
- Sardar
#### 6.3 Pattern Examples
- 'Intro%' → begins with "Intro"
- '%Comp%' → contains "Comp"
- '___' → exactly 3 characters
- '___%' → at least 3 characters

#### 6.4 Escape Character
To match literal %:
like '100\%' escape '\';
#### 6.5 Case Sensitivity
- Patterns inside quotes are case sensitive.
- SQL keywords are case insensitive.
#### 6.6 Other String Operations
- Concatenation
- Convert to upper/lower case
- String length
- Substring extraction
### 7. Order By Clause
List instructor names alphabetically:
```
select distinct name
from instructor
order by name;
```
- Default: ascending order.
- Descending:
order by name desc;
- Can sort by multiple attributes:
order by dept_name, name;
### 8. Selecting Limited Number of Tuples
#### 8.1 SELECT TOP (SQL Server / MS Access)
`select top 10 distinct name from instructor;`
#### 8.2 FETCH (Oracle / Standard SQL)
```
select distinct name
from instructor
order by name
fetch first 10 rows only;
```
#### 8.3 LIMIT (MySQL)
```
select distinct name
from instructor
order by name
limit 10;
```
Used for:
- Large tables
- Pagination
- Performance control
### 9. Additional WHERE Clause Predicates
#### 9.1 BETWEEN
Find instructors with salary between 90000 and 100000:
```
select name
from instructor
where salary between 90000 and 100000;
```
Equivalent to:
salary >= 90000 and salary <= 100000
#### 9.2 Tuple Comparison
```
select name, course_id
from instructor, teaches
where (instructor.ID, dept_name)
      = (teaches.ID, 'Biology');
```
Compact form of multiple equality comparisons.
#### 9.3 IN Operator
```
select name
from instructor
where dept_name in ('Comp. Sci.', 'Biology');
```
Equivalent to:
`dept_name = 'Comp. Sci.' or dept_name = 'Biology'`
### 10. Duplicates and Multiset Semantics
#### 10.1 Set vs Multiset
- Relational algebra → set semantics (no duplicates).
- SQL → multiset (bag) semantics (duplicates allowed).
#### 10.2 Multiset Operators
Given multiset relations r<sub>1</sub> and r<sub>2</sub>:
a) Selection:
If tuple t appears c<sub>1</sub> times in r<sub>1</sub> and satisfies condition,
then it appears c<sub>1</sub> times in σ<sub>(r1)</sub>.
b) Projection:
If tuple t appears c<sub>1</sub> times in r<sub>1</sub>,
then Π(<sub>t</sub>) appears c<sub>1</sub> times in result.
c) Cartesian Product:
If t<sub>1</sub> appears c<sub>1</sub> times in r<sub>1</sub> and
t<sub>2</sub> appears c<sub>2</sub> times in r<sub>2</sub>,
then (t<sub>1</sub>, t<sub>2</sub>) appears c<sub>1</sub> × c<sub>2</sub> times.
#### 10.3 Example
r<sub>1</sub>(A,B) = {(1,a), (2,a)}
r<sub>2</sub>(C) = {(2), (3), (3)}
Projection:
Π<sub>B</sub>(r1) = {(a), (a)}
Cartesian product:
Π<sub>B</sub>(r1) × r2 =
{(a,2),(a,2),(a,3),(a,3),(a,3),(a,3)}
#### 10.4 SQL Semantics
```
select A1, A2, ..., An
from r1, r2, ..., rm
where P
```
Equivalent to multiset version of:
Π<sub>A<sub>1</sub>,A<sub>2</sub>,...,A<sub>n</sub></sub>
(σP(r<sub>1</sub> × r<sub>2</sub> × ... × r<sub>m</sub>))
### 11. Module Summary
- Completed understanding of basic SQL query structure.
- Studied:
  - Cartesian product
  - Equi-join
  - Rename (AS)
  - String matching (LIKE)
  - Order by
  - Select Top / Fetch
  - BETWEEN, IN, tuple comparison
  - Duplicate (multiset) semantics
- SQL corresponds to relational algebra with multiset extensions.

---
---
