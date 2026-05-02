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
## CS2001 – Week 12, Lecture 2
### 1. INTRODUCTION
Focus:
→ Query Optimization (Deep Dive)
#### Context:
- Multiple ways to execute same query
- Goal: choose cheapest execution
#### Core Idea
> Same query → many equivalent expressions → pick best plan

### 2. QUERY OPTIMIZATION BASICS
#### Definition:
- Finding most efficient execution strategy
#### Key Components:
- Equivalent expressions
- Different algorithms per operation
- Cost comparison
#### Evaluation Plan:
- Specifies:
  - Order of operations
  - Algorithm used
  - Execution coordination
#### Key Insight
> Evaluation plan = fully annotated execution tree :contentReference[oaicite:0]{index=0}

### 3. COST-BASED OPTIMIZATION
#### Steps:
1. Generate equivalent expressions
2. Create alternative plans
3. Estimate cost
4. Choose minimum cost plan
#### Cost Depends On:
- Number of tuples
- Distinct values
- Intermediate result size
- Algorithm cost
#### Key Insight
> Cost difference can be massive (seconds vs days) :contentReference[oaicite:1]{index=1}

### 4. RELATIONAL EXPRESSION TRANSFORMATION
#### Definition:
Two expressions are equivalent if:
``Same output for all valid database instances``
#### Notes:
- Order of tuples ignored
- SQL uses multisets (duplicates matter)
#### Key Insight
> Equivalence enables optimization flexibility

### 5. EQUIVALENCE RULES (CORE)
#### Rule 1: Selection Decomposition
``σθ1∧θ2(E) = σθ1(σθ2(E))``

#### Rule 2: Selection Commutativity
``σθ1(σθ2(E)) = σθ2(σθ1(E))``

#### Rule 3: Projection Simplification
``πL1(πL2(...(E))) = πL1(E)``

#### Rule 4: Selection + Join
``σθ(E1 × E2) = E1 ⋈θ E2``
``σθ1(E1 ⋈θ2 E2) = E1 ⋈(θ1∧θ2) E2``

#### Key Insight
> Break, reorder, combine operations freely

### 6. JOIN EQUIVALENCE RULES
#### Commutativity:
``E1 ⋈ E2 = E2 ⋈ E1``

#### Associativity:
``(E1 ⋈ E2) ⋈ E3 = E1 ⋈ (E2 ⋈ E3)``

#### Conditional Associativity:
- Valid when conditions apply only to relevant relations

#### Key Insight
> Join order ≠ fixed → optimize based on size

### 7. SELECTION PUSHING (VERY IMPORTANT)
#### Rule:
``σθ(E1 ⋈ E2) = (σθ(E1)) ⋈ E2`` (if θ only uses E1)

#### Extended:
``σθ1∧θ2(E1 ⋈ E2) = (σθ1(E1)) ⋈ (σθ2(E2))``

#### Benefit:
- Reduces relation size early
- Speeds up joins

#### Key Insight
> Filter early → smaller joins → faster queries :contentReference[oaicite:2]{index=2}

### 8. PROJECTION PUSHING
#### Rule:
``πL(E1 ⋈ E2) = πL1(E1) ⋈ πL2(E2)``

#### Condition:
- Keep attributes needed for join
#### Extended:
- Include join attributes:
``πL1∪L2(E1 ⋈ E2) = πL1∪L2(πL1∪L3(E1) ⋈ πL2∪L4(E2))``

#### Key Insight
> Remove unused attributes early

### 9. SET OPERATION RULES
#### Commutative:
``E1 ∪ E2 = E2 ∪ E1``
``E1 ∩ E2 = E2 ∩ E1``

#### Associative:
``(E1 ∪ E2) ∪ E3 = E1 ∪ (E2 ∪ E3)``

#### Selection Distribution:
``σθ(E1 − E2) = σθ(E1) − σθ(E2)``

#### Projection Distribution:
``πL(E1 ∪ E2) = πL(E1) ∪ πL(E2)``

#### Key Insight
> Operations can be rearranged safely

### 10. PRACTICAL OPTIMIZATION STRATEGY
#### Step 1:
Push selections down
#### Step 2:
Push projections down
#### Step 3:
Choose join order
#### Step 4:
Select best algorithm

#### Example Insight:
- Filter "dept = Music" before join
- Filter "year = 2009" before join
→ Smaller intermediate relations :contentReference[oaicite:3]{index=3}

### 11. JOIN ORDERING
#### Example:
``(r1 ⋈ r2) ⋈ r3 ≠ r1 ⋈ (r2 ⋈ r3) (in cost)``
#### Strategy:
- Perform smaller joins first
#### Reason:
- Intermediate size matters
#### Key Insight
> Always minimize intermediate result size

### 12. ENUMERATION OF PLANS
#### Brute Force:
- Generate all equivalent expressions
- Apply all rules repeatedly
#### Problem:
- Exponential complexity

#### Solution:
- Heuristics
- Dynamic programming

#### Key Insight
> Don’t explore everything → prune smartly

### 13. OPTIMIZATION TECHNIQUES
#### Space Optimization:
- Share common sub-expressions
- Avoid duplication

#### Time Optimization:
- Dynamic programming
- Prune bad plans early

#### Key Insight
> Optimization itself must be efficient

### 14. BIG PICTURE
Pipeline:
Query → Expressions → Transformations → Plans → Cost → Best Plan

#### Core Principle
> Reduce data early, join smartly, compute less

### 15. FINAL TAKEAWAY
You now understand:
- Equivalent expressions
- Transformation rules
- Selection & projection pushing
- Join ordering strategy
- Plan generation

#### Mental Model
Rewrite → Reduce → Reorder → Evaluate → Choose best

---
