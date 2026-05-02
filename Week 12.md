## CS2001 – Week 12, Lecture 1
### 1. INTRODUCTION
Focus:
→ Query Processing & Optimization
#### Context:
- Previous: Backup, Recovery, RAID
- Now: Efficient query execution
#### Goal
> Execute queries with minimum cost

### 2. QUERY PROCESSING OVERVIEW
#### Flow:
SQL Query → Parser → Relational Algebra → Optimizer → Execution Plan → Output
#### Steps:
1. Parsing & Translation
2. Optimization
3. Evaluation
#### Key Insight
> Same query → multiple execution plans

### 3. PARSING & TRANSLATION
#### Function:
- Syntax check
- Relation verification
- SQL → Relational Algebra
#### Example:
``SELECT salary FROM instructor WHERE salary < 75000``
Equivalent:
``σ(salary<75000)(Π(salary(instructor)))``
``Π(salary)(σ(salary<75000(instructor)))``
#### Key Insight
> Equivalent expressions ≠ same cost

### 4. QUERY OPTIMIZATION
#### Definition:
- Select best execution plan
#### Based on:
- Data statistics
- Relation size
- Tuple count
#### Output:
→ Execution plan
#### Key Insight
> Optimization = cost minimization

### 5. QUERY COST
#### Definition:
- Total execution cost
#### Components:
- Disk I/O (dominant)
- CPU
- Network
#### Metrics:
- Block transfers (b)
- Seeks (S)
#### Formula:
``Cost = b × tT + S × tS``
#### Key Insight
> Disk I/O dominates

### 6. COST FACTORS
- Write cost > Read cost
- Buffering reduces I/O
- Memory may be limited
- Worst-case assumptions used
#### Key Insight
> Assume minimal memory availability

### 7. SELECTION OPERATION
#### Goal:
→ Retrieve tuples satisfying condition
#### Methods:
A1: Linear Search
- Cost: ``tS + br × tT``
A1 (Key):
- Avg: ``tS + (br/2) × tT``
A2: Primary Index (Key)
- Cost: ``(hi+1)(tT+tS)``
A3: Primary Index (Non-key)
- Cost: ``hi(tT+tS) + b×tT``
A4: Secondary Index (Key)
- Same as A2
A4: Secondary Index (Non-key)
- Cost: ``(hi+n)(tT+tS)``
#### Key Insight
> Index reduces search cost drastically

### 8. COMPLEX SELECTION
#### AND:
- Use best index first
- Apply remaining conditions in memory
#### OR:
- Use union of index results
- Else linear scan
#### NOT:
- Linear scan
#### Key Insight
> AND reduces, OR expands search

### 9. SORTING
#### Methods:
- Index-based
- In-memory
- External sort-merge
#### External Sort:
Step 1: Create sorted runs
Step 2: Merge runs
#### Key Insight
> Used when data > memory

### 10. EXTERNAL SORT-MERGE
#### Phase 1:
- Read M blocks
- Sort in memory
- Write runs
#### Phase 2:
- Merge runs
- Multi-way merge
#### Key Insight
> Reduce runs iteratively

### 11. JOIN OPERATION
#### Types:
- Nested Loop
- Block Nested Loop
- Indexed Nested Loop
- Merge Join
- Hash Join
#### Nested Loop Cost:
``nr × bs + br``
#### Key Insight
> Brute force = expensive

### 12. BLOCK NESTED LOOP
#### Idea:
- Use blocks instead of tuples
#### Cost:
``br × bs + br``
#### Key Insight
> Reduces I/O compared to basic nested loop

### 13. INDEXED NESTED LOOP
#### Condition:
- Index on join attribute
#### Cost:
``br × (tT+tS) + nr × c``
#### Key Insight
> Very efficient with index

### 14. OTHER OPERATIONS
#### Duplicate Elimination:
- Sorting or hashing
#### Projection:
- Remove unnecessary attributes
#### Aggregation:
- count, sum, min, max
- avg = ``sum/count``
#### Key Insight
> Combine operations to reduce cost

### 15. BIG PICTURE
Query Processing:
- Translate → Optimize → Execute
#### Core Idea:
> Same query → different costs → choose minimum

### 16. FINAL TAKEAWAY
You now understand:
- Query pipeline
- Cost estimation
- Selection, sorting, join methods
#### Mental Model
Query → Algebra → Plan → Cost → Best Plan → Execute

---
