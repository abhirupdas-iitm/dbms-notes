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
