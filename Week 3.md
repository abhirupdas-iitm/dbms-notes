## CS2001 – Week 3, Lecture 1
### 1. Module Recap
Previously learned foundational relational database and SQL concepts include:
Relational database fundamentals:
- Attributes and attribute types  
- Schema and instance  
- Primary keys  
- Foreign keys  

Relational algebra operations:
- Selection  
- Projection  
- Cartesian product  
- Join  

SQL basics:
- Data Definition Language (DDL)  
- Data Manipulation Language (DML)  
- Basic query structure (select–from–where)  
- Set operations  
- Aggregate functions  
This module focuses on strengthening SQL query writing through practical examples.

### 2. Module Objective

Primary objective:
- Reinforce core SQL features through example-based learning.

Secondary objectives:
- Develop ability to write correct SQL queries  
- Understand SQL query execution behavior  
- Build intuition for relational query formulation  

Key principle:
SQL is a declarative language.
You specify what result you want, not how to compute it.

### 3. SELECT Statement (Selection and Projection)

Example problem:
Find names of buildings where classroom capacity is less than 100.

Query:
```
select distinct building  
from classroom  
where capacity < 100;
```

Explanation:
- from classroom → selects classroom relation  
- where capacity < 100 → filters rows  
- select building → chooses building column  
- distinct → removes duplicate values  

Important rule:
Default behavior of select returns duplicates (multiset).
To explicitly retain duplicates:

```
select all building  
from classroom  
where capacity < 100;
```

### 4. Cartesian Product and Join Condition

Example problem:
Find students whose department budget is less than 100000.

Query:

```
select name, budget  
from student, department  
where student.dept_name = department.dept_name  
and budget < 100000;
```
Execution steps:
Step 1: Cartesian product generates all combinations.
Step 2: Join condition filters matching department names.
Step 3: Budget condition filters valid rows.
Step 4: select projects required columns.

Key insight:
Cartesian product + condition = join.

### 5. Renaming Using AS (Alias)

Same query using aliases:
```
select S.name as studentname, D.budget as deptbudget  
from student as S, department as D  
where S.dept_name = D.dept_name  
and D.budget < 100000;
```
Purpose of alias:
- Simplifies query writing  
- Improves readability  
- Required when same relation appears multiple times  

Example aliases:
student → S  
department → D  

Attribute aliases:
name → studentname  
budget → deptbudget  

### 6. WHERE Clause with AND / OR

Example problem:
Find instructors whose department is Finance OR whose building is Watson or Taylor.
Query:
```
select name  
from instructor I, department D  
where D.dept_name = I.dept_name  
and (  
    I.dept_name = 'Finance'  
    or building in ('Watson', 'Taylor')  
);
```
Explanation:
Join condition ensures instructor matches correct department.
Selection condition applies logical OR filtering.
Important rule:
Always use parentheses when combining AND and OR.

### 7. String Matching (LIKE Operator)

Example problem:
Find course titles where course_id starts with exactly 3 characters followed by a hyphen.
Query:
```
select title  
from course  
where course_id like '___-%';
```
Wildcard symbols:
- _ matches exactly one character  
- % matches any number of characters  

Pattern ___-% means:
- exactly 3 characters  
- followed by hyphen  
- followed by anything  

### 8. ORDER BY Clause

Example problem:
Sort students by department name ascending and total credits descending.
Query:
```
select name, dept_name, tot_cred  
from student  
order by dept_name asc, tot_cred desc;
```
Sorting logic:
Primary sorting:
`dept_name ascending`
Secondary sorting:
`tot_cred descending within same department`

### 9. IN Operator

Example problem:
Find course IDs taught in Fall or Spring 2018.
Query:
```
select course_id  
from teaches  
where semester in ('Fall', 'Spring')  
and year = 2018;
```
Equivalent form:
```
select course_id  
from teaches  
where (semester = 'Fall' or semester = 'Spring')  
and year = 2018;
```

Purpose of IN:
Simplifies multiple OR comparisons.

### 10. UNION Operation

Example problem:
Find all courses taught in Fall or Spring 2018.
Query:
```
select course_id  
from teaches  
where semester = 'Fall' and year = 2018  

union  

select course_id  
from teaches  
where semester = 'Spring' and year = 2018;
```
Important property:
union removes duplicates.
To retain duplicates:
union all

### 11. INTERSECT Operation

Example problem:
Find instructors in Comp. Sci. or Finance with salary less than 80000.
Query:
```
select name  
from instructor  
where dept_name in ('Comp. Sci.', 'Finance')  

intersect  

select name  
from instructor  
where salary < 80000;
```
Equivalent logical query:
```
select name  
from instructor  
where dept_name in ('Comp. Sci.', 'Finance')  
and salary < 80000;
```

### 12. EXCEPT Operation

Example problem:
Find instructors in Comp. Sci. or Finance excluding those with salary between 70000 and 90000.
Query:
```
select name  
from instructor  
where dept_name in ('Comp. Sci.', 'Finance')  

except  

select name  
from instructor  
where salary < 90000 and salary > 70000;
```
Equivalent logical query:
```
select name  
from instructor  
where dept_name in ('Comp. Sci.', 'Finance')  
and (salary >= 90000 or salary <= 70000);
```

### 13. Aggregate Functions Overview

Aggregate functions compute a single value from multiple rows.
Functions include:
- avg  
- min  
- max  
- count  
- sum  

### 14. AVG Function

Example problem:
Find average classroom capacity per building greater than 25.
Query:
```
select building, avg(capacity)  
from classroom  
group by building  
having avg(capacity) > 25;
```
Execution logic:
group by forms building groups.
avg computes average per group.
having filters groups.

### 15. MIN Function

Example problem:
Find minimum instructor salary.
Query:
```
select min(salary)  
from instructor;
```

### 16. MAX Function

Example problem:
Find maximum student credits.
Query:
```
select max(tot_cred)  
from student;
```

### 17. COUNT Function

Example problem:
Find number of courses per building.
Query:
```
select building, count(course_id)  
from section  
group by building;
```
count counts number of rows per group.

### 18. SUM Function

Example problem:
Find total credits per department.
Query:
```
select dept_name, sum(credits)  
from course  
group by dept_name;
```
sum computes total credits per department.

### 19. Logical Execution Order of SQL

Actual logical execution order:
1. from  
2. where  
3. group by  
4. having  
5. select  
6. distinct  
7. order by  
Understanding this order is essential for correct query writing.

### 20. Module Summary

Concepts practiced:
- select and distinct  
- Cartesian product  
- alias using as  
- filtering using where  
- logical operators and, or  
- string matching using like  
- sorting using order by  
- filtering using in  
- set operations union, intersect, except  
- aggregate functions avg, min, max, count, sum  
- grouping using group by and having  
This module establishes the operational foundation for SQL querying.

---
---
## CS2001 – Week 3, Lecture 2
### 1. Module Recap

Previous module covered:
- Basic SQL query structure
- SELECT–FROM–WHERE queries
- Joins
- Set operations (union, intersect, except)
- Aggregation functions

Current module builds on these foundations to introduce:
- Nested subqueries
- Database modification operations
These features enable writing more powerful and flexible SQL queries.

### 2. Module Objectives

Primary objectives:
- Understand nested subqueries in SQL
- Understand data modification operations

These include:
- DELETE
- INSERT
- UPDATE

### 3. Nested Subqueries: Definition

A nested subquery is a SELECT–FROM–WHERE query embedded inside another SQL query.
General form:
```
select A1, A2, ..., An  
from r1, r2, ..., rm  
where P
```
Where any of the following can be replaced by a subquery:
- Attributes in SELECT clause
- Relations in FROM clause
- Conditions in WHERE clause

Key principle:
Output of any SQL query is always a relation.
Therefore, the output of one query can be used as input to another query.

### 4. Subqueries in the WHERE Clause

Typical uses:
- Set membership testing
- Set comparison
- Set cardinality testing

### 5. Set Membership Using IN

Example problem:
Find courses offered in Fall 2009 and Spring 2010.
Query:
```
select distinct course_id  
from section  
where semester = 'Fall' and year = 2009  
and course_id in (  
    select course_id  
    from section  
    where semester = 'Spring' and year = 2010  
);
```
Explanation:
Outer query selects Fall 2009 courses.
Subquery selects Spring 2010 courses.
IN checks if course exists in both sets.

### 6. Set Difference Using NOT IN

Example problem:
Find courses offered in Fall 2009 but not Spring 2010.
Query:
```
select distinct course_id  
from section  
where semester = 'Fall' and year = 2009  
and course_id not in (  
    select course_id  
    from section  
    where semester = 'Spring' and year = 2010  
);
```
Explanation:
NOT IN removes courses present in Spring 2010.

### 7. Tuple Membership Subquery

Example problem:
Count number of students taught by instructor ID 10101.
Query:
```
select count(distinct ID)  
from takes  
where (course_id, sec_id, semester, year) in (  
    select course_id, sec_id, semester, year  
    from teaches  
    where teaches.ID = 10101  
);
```
Explanation:
Subquery returns courses taught by instructor.
Outer query counts students enrolled in those courses.

### 8. Set Comparison Using SOME

Example problem:
Find instructors whose salary is greater than at least one Biology instructor.
Query:
```
select name  
from instructor  
where salary > some (  
    select salary  
    from instructor  
    where dept_name = 'Biology'  
);
```
Definition:
F > some r
means:
There exists at least one tuple in relation r satisfying condition.
Logical interpretation:
Existential quantification.
Meaning:
At least one value satisfies condition.

### 9. Set Comparison Using ALL

Example problem:
Find instructors whose salary is greater than all Biology instructors.
Query:
```
select name  
from instructor  
where salary > all (  
    select salary  
    from instructor  
    where dept_name = 'Biology'  
);
```
Definition:
F > all r
means:
Condition must be true for every tuple in relation.
Logical interpretation:
Universal quantification.
Meaning:
Condition must hold for entire set.

### 10. Testing for Empty Relations Using EXISTS

Definition:
exists r → true if relation r is not empty  
not exists r → true if relation r is empty  

Example problem:
Find courses offered in Fall 2009 and Spring 2010.
Query:
```
select course_id  
from section as S  
where semester = 'Fall' and year = 2009  
and exists (  
    select *  
    from section as T  
    where semester = 'Spring' and year = 2010  
    and S.course_id = T.course_id  
);
```
Explanation:
Subquery checks if matching Spring course exists.
If exists, course selected.

### 11. Using NOT EXISTS

Example problem:
Find students who have taken all Biology courses.
Query:
```
select distinct S.ID, S.name  
from student as S  
where not exists (  
    (select course_id  
     from course  
     where dept_name = 'Biology')  

    except  

    (select T.course_id  
     from takes as T  
     where S.ID = T.ID)  
);
```
Explanation:
Checks if student is missing any Biology course.
If none missing, student selected.

### 12. UNIQUE Clause

Purpose:
Tests whether subquery result contains duplicate tuples.
Example problem:
Find courses offered at most once in 2009.
Query:
```
select T.course_id  
from course as T  
where unique (  
    select R.course_id  
    from section as R  
    where T.course_id = R.course_id  
    and R.year = 2009  
);
```
If duplicates exist, UNIQUE returns false.

### 13. Subqueries in FROM Clause

Example problem:
Find average salary of departments where average salary > 42000.
Query:
```
select dept_name, avg_salary  
from (  
    select dept_name, avg(salary) as avg_salary  
    from instructor  
    group by dept_name  
)  
where avg_salary > 42000;
```
Explanation:
Subquery creates temporary relation.
Outer query filters result.

### 14. WITH Clause (Temporary Relations)

Purpose:
Creates temporary relation usable in query.
Example problem:
Find departments with maximum budget.
Query:
```
with max_budget(value) as (  
    select max(budget)  
    from department  
)  
select department.name  
from department, max_budget  
where department.budget = max_budget.value;
```
Explanation:
Temporary relation created using WITH.

### 15. Scalar Subqueries in SELECT Clause

Definition:
Subquery returning single value.
Example problem:
List departments with number of instructors.
Query:
```
select dept_name,  
(  
    select count(*)  
    from instructor  
    where department.dept_name = instructor.dept_name  
) as num_instructors  
from department;
```
Important rule:
Subquery must return single value.

### 16. Database Modification Operations Overview
Three types:
- DELETE
- INSERT
- UPDATE

### 17. DELETE Operation

`Delete all instructors:`
`delete from instructor;`

`Delete Finance instructors:`

```
delete from instructor  
where dept_name = 'Finance';
```

Delete instructors in Watson building:
```
delete from instructor  
where dept_name in (  
    select dept_name  
    from department  
    where building = 'Watson'  
);
```
Delete instructors with below-average salary:
```
delete from instructor  
where salary < (  
    select avg(salary)  
    from instructor  
);
```
Important behavior:
Average computed first, then deletion performed.

### 18. INSERT Operation

Insert new course:
```
insert into course  
values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```
Insert specifying attributes:
```
insert into course (course_id, title, dept_name, credits)  
values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```
Insert student with null credits:
```
insert into student  
values ('3003', 'Green', 'Finance', null);
```
Insert using SELECT:
```
insert into student  
select ID, name, dept_name, 0  
from instructor;
```

### 19. UPDATE Operation

Increase salaries conditionally:
```
update instructor  
set salary = salary * 1.03  
where salary > 100000;
```

```
update instructor  
set salary = salary * 1.05  
where salary <= 100000;
```
Better approach using CASE:
```
update instructor  
set salary = case  
    when salary <= 100000 then salary * 1.05  
    else salary * 1.03  
end;
```

### 20. UPDATE Using Scalar Subquery

Example problem:
Recompute total credits for students.
Query:
```
update student S  
set tot_creds = (  
    select sum(credits)  
    from takes, course  
    where takes.course_id = course.course_id  
    and S.ID = takes.ID  
    and takes.grade <> 'F'  
    and takes.grade is not null  
);
```

### 21. Module Summary

Key concepts introduced:
Nested subqueries:
- IN
- NOT IN
- SOME
- ALL
- EXISTS
- NOT EXISTS
- UNIQUE

Subqueries in:
- WHERE clause
- FROM clause
- SELECT clause

Temporary relations:
- WITH clause

Database modification:
- DELETE
- INSERT
- UPDATE
These features enable advanced querying and database manipulation.

---
---
## CS2001 – Week 3, Lecture 3
### 1. Module Recap

Previous module covered:
- Nested subqueries
- Data modification operations:
  - delete
  - insert
  - update

These features allow advanced querying and database manipulation.
This module introduces:
- Join expressions
- Views
These enable combining data from multiple relations and creating virtual relations.

### 2. Module Objectives

Primary objectives:
- Learn SQL join expressions
- Learn SQL view definitions and usage

### 3. Join Expressions: Definition

Join operation:
- Takes two relations as input
- Produces one relation as output

Core mechanism:
Join = Cartesian product + matching condition
Cartesian product produces all combinations.
Join condition filters meaningful matches.
Join expressions are typically used in the FROM clause.
General form:
```
select attributes  
from relation1 join relation2  
on join_condition;
```

### 4. Cross Join

Definition:
Produces Cartesian product of two relations.
If relation A has m rows and relation B has n rows:
Result contains m × n rows.
Explicit form:
```
select *  
from employee cross join department;
```
Implicit form:
```
select *  
from employee, department;
```
Result:
All possible combinations of rows.

### 5. Inner Join

Definition:
Returns only tuples that satisfy join condition.
Unmatched tuples are discarded.
Example:
```
select *  
from course inner join prereq  
on course.course_id = prereq.course_id;
```
Result:
Only courses present in both relations.
Inner join corresponds to set intersection.

### 6. Natural Join

Definition:
Join automatically performed using common attribute names.
Duplicate columns removed.
Example:
```
select *  
from course natural join prereq;
```
Difference from inner join:
- Inner join keeps duplicate join columns
- Natural join removes duplicate join columns

### 7. Outer Join: Definition

Outer join preserves unmatched tuples.
Missing values filled using null.
Purpose:
Avoid loss of information.
Types:
- Left outer join
- Right outer join
- Full outer join

### 8. Left Outer Join

Definition:
All tuples from left relation included.
Matching tuples from right relation included.
Non-matching right attributes set to null.
Example:
```
select *  
from course left outer join prereq  
on course.course_id = prereq.course_id;
```
Result:
All course tuples preserved.
Missing prerequisite values become null.

### 9. Right Outer Join

Definition:
All tuples from right relation included.
Matching tuples from left relation included.
Non-matching left attributes set to null.
Example:
```
select *  
from course right outer join prereq  
on course.course_id = prereq.course_id;
```
Result:
All prerequisite tuples preserved.
Missing course values become null.

### 10. Full Outer Join

Definition:
All tuples from both relations included.
Matching tuples joined.
Non-matching attributes filled with null.
Example:
```
select *  
from course full outer join prereq  
on course.course_id = prereq.course_id;
```
Result:
Complete combination of both relations.
No data loss.

### 11. Join Using USING Clause

Definition:
Specifies join attribute explicitly.
Example:
```
select *  
from course full outer join prereq  
using (course_id);
```
Condition:
Attribute must exist in both relations.
Duplicate attribute automatically removed.

### 12. Join with Additional Conditions (Theta Join)

Definition:
Join with predicate condition.
Example:
```
select *  
from course join prereq  
on course.course_id = prereq.course_id  
and dept_name = 'Biology';
```
Allows filtering during join.

### 13. Join Performance Insight

Join internally computes Cartesian product.
Example:
Relation A: 1,000,000 rows  
Relation B: 1,000,000 rows  
Cartesian product:
1,000,000 × 1,000,000 = 10¹² rows
Filtering reduces result size.
Join optimization is critical.

### 14. Views: Definition

View is a virtual relation.
Defined using query expression.
View does not store data physically.
Definition syntax:
```
create view view_name as  
select attributes  
from relation  
where condition;
```
View behaves like a table.

### 15. Purpose of Views

Views used to:
- Hide sensitive information
- Simplify queries
- Provide abstraction
- Restrict access

Example:
```
create view faculty as  
select ID, name, dept_name  
from instructor;
```
Salary column hidden.

### 16. Using Views

Example:
```
select name  
from faculty  
where dept_name = 'Biology';
```
Database executes underlying query dynamically.
View behaves like relation.

### 17. Views with Computed Values

Example:
```
create view departments_total_salary(dept_name, total_salary) as  
select dept_name, sum(salary)  
from instructor  
group by dept_name;
```
Creates virtual relation with computed values.

### 18. Views Defined Using Other Views

Example:
```
create view physics_fall_2009 as  
select course.course_id, sec_id, building, room_number  
from course, section  
where course.course_id = section.course_id  
and course.dept_name = 'Physics'  
and section.semester = 'Fall'  
and section.year = '2009';
```
Create second view using first view:
```
create view physics_fall_2009_watson as  
select course_id, room_number  
from physics_fall_2009  
where building = 'Watson';
```

### 19. View Expansion

Definition:
View definition expanded into underlying query.
Process:
Replace view name with its defining query.
Repeat until base relations reached.
Ensures correct evaluation.

### 20. View Dependencies

Definition:
View v1 depends on view v2 if v2 used in definition.
Dependency can be indirect.
Recursive view:
View depending on itself.
Usually avoided.

### 21. Updating Views

Example:
`insert into faculty values ('30765', 'Green', 'Music');`
System converts into:
`insert into instructor values ('30765', 'Green', 'Music', null);`
Salary set to null.
Conditions for updatable views:
- Single base relation
- No aggregates
- No group by
- No distinct
- No joins

### 22. Views That Cannot Be Updated

Example:
```
create view instructor_info as  
select ID, name, building  
from instructor, department  
where instructor.dept_name = department.dept_name;
```
Insert:
`insert into instructor_info values ('69987', 'White', 'Taylor');`
Problem:
Department unknown.
Update cannot be uniquely translated.

### 23. Materialized Views

Definition:
View stored physically as table.
Syntax conceptually:
```
create materialized view view_name as  
select query;
```
Difference from normal view:

Normal view:
- Virtual
- Computed dynamically

Materialized view:
- Physically stored
- Faster access
- Needs maintenance

Problem:
Underlying data changes → materialized view becomes outdated.
Requires update.

### 24. Logical vs Physical View Distinction

Normal view:
- Logical abstraction
- No storage

Materialized view:
- Physical storage
- Requires synchronization

### 25. Module Summary

Join expressions:
- cross join
- inner join
- natural join
- left outer join
- right outer join
- full outer join
- join using clause
- join with conditions

Views:
- create view
- view abstraction
- view expansion
- view dependencies
- updating views
- materialized views

Join enables combining relations.
Views enable virtual relations and abstraction.
These are core intermediate SQL features.

---
---
## CS2001 – Week 3, Lecture 4
### 1. Module Recap

Previous module covered:
- Join expressions
- Inner join, outer join, natural join
- Views and virtual relations

This module introduces:
- Transactions
- Integrity constraints
- SQL data types and schemas
- Authorization and privileges

### 2. Module Objectives

Objectives:
- Understand transactions in SQL
- Learn integrity constraints
- Understand additional SQL data types
- Understand authorization and access control

### 3. Transactions

Definition:
A transaction is a unit of work performed on a database.
Examples:
- Bank money transfer
- Student course registration
- Updating employee salary

## 4. Atomicity Property

Atomicity means:
Transaction is executed fully or not at all.

Two outcomes:
- Commit → transaction permanently saved
- Rollback → transaction undone completely

Example:
transfer money:
`update account set balance = balance - 500 where id = 'A';`
`update account set balance = balance + 500 where id = 'B';`
If error occurs between statements:
rollback restores original state.

### 5. Isolation Property

Definition:
Transactions execute independently.
Concurrent transactions do not interfere with each other.
Ensures database consistency.

### 6. Transaction Control Commands

Commit transaction:
`commit;`

Rollback transaction:
`rollback;`

Explicit transaction block (SQL standard):
```
begin atomic
    SQL statements
end;
```
Note:
Many databases auto-commit by default.

### 7. Integrity Constraints: Definition

Integrity constraints enforce correctness and consistency of database.
Examples:
- Minimum bank balance
- Employee salary constraints
- Non-null phone number
Prevent invalid data entry.

### 8. Types of Integrity Constraints

Single relation constraints:
- not null
- primary key
- unique
- check

### 9. NOT NULL Constraint

Definition:
Prevents null values.
Example:
`name varchar(20) not null;`
`budget numeric(12,2) not null;`
Null insertion not allowed.

### 10. UNIQUE Constraint

Definition:
Ensures attribute combination is unique.
Example:
unique(ID, email);
Prevents duplicate combinations.
Note:
Unique allows null values.
Primary key does not allow null.

### 11. CHECK Constraint

Definition:
Ensures attribute values satisfy condition.
Example:
```
create table section (
    course_id varchar(8),
    sec_id varchar(8),
    semester varchar(6),
    year numeric(4,0),
    primary key (course_id, sec_id, semester, year),
    check (semester in ('Fall', 'Winter', 'Spring', 'Summer'))
);
```
Invalid values rejected.

### 12. Referential Integrity

Definition:
Ensures foreign key value exists in referenced relation.

Example:
Instructor table:
dept_name = 'Biology'
Department table must contain:
dept_name = 'Biology'

### 13. Foreign Key Definition

Example:
```
create table course (
    course_id char(5) primary key,
    title varchar(20),
    dept_name varchar(20),
    foreign key (dept_name) references department
);
```
Foreign key maintains consistency between tables.

### 14. Cascading Actions

Definition:
Specifies action when referenced value changes.
Example:
```
create table course (
    dept_name varchar(20),
    foreign key (dept_name)
    references department
    on delete cascade
    on update cascade
);
```
Cascade actions:
- delete cascade → delete dependent rows
- update cascade → update dependent rows

Alternative options:
- no action
- set null
- set default

### 15. Constraint Violation Example

Person table referencing itself:
```
create table person (
    ID char(10),
    name char(40),
    mother char(10),
    father char(10),
    primary key(ID),
    foreign key(father) references person,
    foreign key(mother) references person
);
```

Insertion strategies:
Option 1:
Insert parents first.
Option 2:
Insert null temporarily.
Option 3:
Defer constraint checking.

### 16. SQL Built-in Data Types

Date type:
date '2025-01-19'
Time type:
time '09:00:30'
Timestamp type:
timestamp '2025-01-19 09:00:30'
Interval type:
interval '1' day
Supports date arithmetic.

### 17. Index

Definition:
Data structure that speeds up search.
Example:
```
create table student (
    ID varchar(5),
    name varchar(20),
    primary key(ID)
);
```
create index studentID_index on student(ID);
Query using index:
```
select *
from student
where ID = '12345';
```
Index improves performance.

### 18. User Defined Types (UDT)

Definition:
Custom type alias.
Example:
`create type Dollars as numeric(12,2);`
Use:
```
create table department (
    dept_name varchar(20),
    budget Dollars
);
```
Improves readability.

### 19. Domains

Definition:
User defined type with constraints.
Example:
`create domain person_name varchar(20) not null;`

Domain with check constraint:
```
create domain degree_level varchar(10)
check (value in ('Bachelors', 'Masters', 'Doctorate'));
```

Reusable constrained type.

### 20. Large Object Types

Types:
blob → binary large object
clob → character large object
Used for:
- Images
- Videos
- Documents

Example:
photo blob
Database stores reference.
Actual data stored externally.

### 21. Authorization

Definition:
Controls access to database.
Authorization types:
- select
- insert
- update
- delete

Schema authorization:
- create index
- create table
- alter table
- drop table

### 22. Grant Privilege

Syntax:
```
grant privilege_list
on relation_name
to user_list;
```
Example:
`grant select on instructor to Amit;`
Grant all privileges:
`grant all privileges on instructor to Amit;`

### 23. Revoke Privilege

Syntax:
```
revoke privilege_list
on relation_name
from user_list;
```
Example:
`revoke select on instructor from Amit;`
Revoke all privileges:
`revoke all privileges on instructor from Amit;`

### 24. Grant with Grant Option

Definition:
Allows user to grant privileges to others.
Example:
`grant select on department to Amit with grant option;`
Amit can grant privilege further.

### 25. Roles

Definition:
Group of privileges assigned together.
Create role:
`create role instructor;`
Grant role to user:
`grant instructor to Amit;`
Grant privilege to role:
`grant select on takes to instructor;`
User inherits privileges.

### 26. Role Hierarchy

Example:
```
create role teaching_assistant;
grant teaching_assistant to instructor;
create role dean;
grant instructor to dean;
grant dean to Satoshi;
```
Satoshi inherits all privileges.

### 27. Authorization on Views

Create view:
```
create view geo_instructor as
select *
from instructor
where dept_name = 'Geology';
```
Grant privilege:
`grant select on geo_instructor to geo_staff;`

`geo_staff` can query view.
Even without base table access.

### 28. Reference Privilege

Allows creation of foreign key.
Example:
```
grant reference(dept_name)
on department
to Mariano;
```
Required for foreign key creation.

### 29. Privilege Revocation Options

Cascade revoke:
`revoke select on department from Amit cascade;`
Restrict revoke:
`revoke select on department from Amit restrict;`
Cascade removes dependent privileges.
Restrict prevents revoke if dependencies exist.

### 30. Module Summary

Topics covered:
Transactions:
- commit
- rollback
- atomicity
- isolation

Integrity constraints:
- not null
- unique
- check
- foreign key
- cascade actions

SQL data types:
- date
- time
- timestamp
- interval
- index
- user defined types
- domains
- blob
- clob

Authorization:
- grant
- revoke
- roles
- privileges
- authorization on views
These features ensure database consistency, performance, and security.

---
---
## CS2001 – Week 3, Lecture 5
### Functions and Procedural Constructs

SQL was originally a **declarative language**, but since SQL:1999, it includes **procedural features** like:
- Functions
- Procedures
- Variables
- Loops
- Conditionals
- Exception handling
These allow SQL to perform more complex logic inside the database itself.

Functions and procedures can be written in:
- SQL itself
- External languages like C, Java, Python

External languages are useful for:
- Complex algorithms
- Specialized data processing (images, geometry)
- Better performance in some cases

### SQL Functions

Functions:
- Accept parameters
- Return a value
- Can be used inside SQL queries
- Behave like parameterized views

Example:
```
create function dept_count(dept_name varchar(20))
returns integer
begin
    declare d_count integer;
    select count(*) into d_count
    from instructor
    where instructor.dept_name = dept_name;
    return d_count;
end;
```
Usage:
```
select dept_name, budget
from department
where dept_count(dept_name) > 12;
```

### Table-Valued Functions

These functions return an entire table instead of a single value.
Example:
```
create function instructor_of(dept_name char(20))
returns table (
    ID varchar(5),
    name varchar(20),
    dept_name varchar(20),
    salary numeric(8,2)
)
returns table
(
    select ID, name, dept_name, salary
    from instructor
    where instructor.dept_name = instructor_of.dept_name
);
```
Usage:
```
select *
from table(instructor_of('Music'));
```

### SQL Procedures

Procedures:
- Do NOT return values directly
- Use input and output parameters
- Called using CALL

Example:
```
create procedure dept_count_proc(
    in dept_name varchar(20),
    out d_count integer
)
begin
    select count(*) into d_count
    from instructor
    where instructor.dept_name = dept_count_proc.dept_name;
end;
```
Calling procedure:
```
declare d_count integer;
call dept_count_proc('Physics', d_count);
```

### Functions vs Procedures

Functions:
- Return a value
- Can be used inside queries

Procedures:
- Do not return a value directly
- Use output parameters
- Called explicitly using CALL
Functions can be used inside SELECT, WHERE, etc.
Procedures cannot.

### Procedural Language Constructs in SQL

SQL supports programming constructs similar to other languages.

#### Compound Statement
```
begin
    SQL statements
end;
```

#### While Loop
```
while condition do
    statements
end while;
```

#### Repeat Loop
```
repeat
    statements
until condition
end repeat;
```

#### For Loop
`declare total integer default 0;`

```
for r as
    select budget from department
do
    set total = total + r.budget;
end for;
```

#### If-Then-Else
```
if condition then
    statements;
elseif condition then
    statements;
else
    statements;
end if;
```

#### Case Statement

Simple case:
```
case variable
    when value1 then statements;
    when value2 then statements;
    else statements;
end case;
```
Searched case:
```
case
    when condition then statements;
    when condition then statements;
    else statements;
end case;
```

### Exception Handling

Used to handle errors.
Example:
`declare out_of_seats condition;`

```
declare exit handler for out_of_seats
begin
    -- handle exception
end;
signal out_of_seats;
```

### External Language Functions and Procedures

SQL allows functions written in other languages.
Example:
```
create procedure dept_count_proc(
    in dept_name varchar(20),
    out count integer
)
language C
external name '/usr/bin/dept_count_proc';
```
Benefits:
- Higher performance
- More flexibility

Risks:
- Security issues
- Possible database corruption

Safer approaches:
- Sandbox execution
- Separate process execution

### Triggers

A trigger is an automatic action performed when certain database events occur.
Events include:
- INSERT
- UPDATE
- DELETE

Triggers help:
- Enforce integrity
- Maintain consistency
- Log changes
- Perform automatic updates

### Trigger Structure

```
create trigger trigger_name
before | after insert | update | delete
on table_name
for each row
begin
    statements;
end;
```

### BEFORE Triggers

Executed before modification.
Uses:
- Validate data
- Modify values before storing

Example:
```
create trigger set_null_trigger
before update on takes
referencing new row as nrow
for each row
when (nrow.grade = '')
begin
    set nrow.grade = null;
end;
```

### AFTER Triggers

Executed after modification.
Uses:
- Update other tables
- Maintain logs
- Enforce consistency

Example:
```
create trigger credits_earned
after update of grade on takes
referencing new row as nrow
referencing old row as orow
for each row
when nrow.grade <> 'F'
and nrow.grade is not null
and (orow.grade = 'F' or orow.grade is null)
begin
    update student
    set tot_cred = tot_cred +
        (select credits
         from course
         where course.course_id = nrow.course_id)
    where student.id = nrow.id;
end;
```

### Row-Level vs Statement-Level Triggers

Row-level trigger:
- Executes once per row affected
Statement-level trigger:
- Executes once per SQL statement

Example:
Updating 100 rows:
Row trigger → executes 100 times  
Statement trigger → executes once

### Uses of Triggers

Recommended uses:
- Logging changes
- Auditing user actions
- Automatic updates
- Maintaining integrity
- Adding system values (timestamp, username)

### When NOT to Use Triggers

Avoid triggers when:
- Too many triggers exist
- Trigger logic is complex
- Triggers call other triggers
- Recursive triggers are used
- Triggers include loops
- Triggers call external procedures frequently

Triggers should be:
- Simple
- Efficient
- Minimal

### Summary

Functions:
- Return values
- Used inside queries

Procedures:
- Perform actions
- Use input/output parameters

Procedural constructs:
- Loops
- Conditionals
- Exceptions

Triggers:
- Automatic response to database events
- Used for integrity, automation, logging
Triggers are powerful but must be used carefully to avoid performance and maintenance problems.

---
---
