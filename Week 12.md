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
## CS2001 – Week 12, Lecture 3
### 1. INTRODUCTION
Focus:
→ RDBMS Performance, Architecture, and Scaling
#### Goal:
- Understand system-level performance
- Understand how databases scale
#### Core Idea
> Performance + Architecture + Scaling = Real-world DB systems :contentReference[oaicite:0]{index=0}

### 2. WHAT DBMS APPLICATIONS NEED
#### Key Requirements:
- Throughput (transactions/sec)
- Response Time (latency)
- Availability (uptime)
#### Definitions:
``Throughput = Transactions per second``
``Response Time = Time from request → result``
``Availability = Mean time to failure``
#### Also Required:
- Correctness (ACID)
- Scalability
#### Key Insight
> High throughput + low latency + high availability = good system :contentReference[oaicite:1]{index=1}

### 3. PERFORMANCE FACTORS
#### Transaction-Level:
- Concurrency control
- Query optimization

#### System-Level:
- System architecture
- Database architecture
- Performance tuning

#### Tuning Methods:
- Hardware: faster CPU, more memory, faster disks
- DB parameters: buffer size, checkpointing
- Design: schema, indexes

#### Key Insight
> Bottlenecks decide performance

### 4. SCALABILITY
#### Definition:
- Ability to handle growth without performance loss
#### Growth Dimensions:
- Data size
- Number of users
- Services
- Geographic spread
#### Key Insight
> Scaling ≠ just more data, it’s sustained performance :contentReference[oaicite:2]{index=2}

### 5. RDBMS ARCHITECTURE TYPES
#### Types:
- Centralized
- Client-Server
- Parallel
- Distributed

### 6. CENTRALIZED ARCHITECTURE
#### Characteristics:
- Single system
- No network interaction
#### Use Case:
- Small systems
#### Key Insight
> Simple but not scalable

### 7. CLIENT-SERVER ARCHITECTURE
#### Structure:
- Clients → send requests
- Server → processes queries
#### Components:
- Front-end:
  - UI, forms, reports
- Back-end:
  - Query processing
  - Optimization
  - Concurrency
#### Interface:
- SQL / APIs (ODBC, JDBC)
#### Key Insight
> Separation improves scalability :contentReference[oaicite:3]{index=3}

### 8. SERVER SYSTEM TYPES
#### 1. Transaction Server:
- Executes queries
- Returns results
#### Flow:
Client → SQL → Server → Execute → Return

#### 2. Data Server:
- Handles data-intensive tasks
- Used in high-speed environments

#### Issues:
- Caching
- Locking
- Data transfer

#### Key Insight
> Execution and data handling can be separated

### 9. PARALLEL DATABASE SYSTEMS
#### Definition:
- Multiple CPUs + disks + network
#### Types:
- Coarse-grained → few powerful processors
- Fine-grained → many small processors

#### Metrics:
``Throughput = tasks per unit time``
``Response Time = time per task``

#### Key Insight
> Parallelism improves performance

### 10. SPEEDUP
#### Formula:
``Speedup = Time_small / Time_large``

#### Ideal:
``Speedup = N``

#### Reality:
- Sublinear

### 11. SCALEUP
#### Formula:
``Scaleup = Time_small_problem / Time_large_problem``

#### Ideal:
``Scaleup = 1``

#### Key Insight
> Perfect scaling is rare :contentReference[oaicite:4]{index=4}

### 12. WHY SCALING IS SUBLINEAR
#### Reasons:
- Startup cost
- Resource contention
- Skew (uneven workloads)

#### Key Insight
> Slowest task limits performance

### 13. INTERCONNECTION NETWORKS
#### Types:
1. Bus:
   - Simple
   - Poor scalability

2. Mesh:
   - Better scaling
   - More connections

3. Hypercube:
   - Best communication
   - ``Max hops = log(n)``

#### Key Insight
> Network design impacts DB performance

### 14. PARALLEL ARCHITECTURE MODELS
#### Types:
- Shared Memory
- Shared Disk
- Shared Nothing
- Hybrid

#### Key Insight
> Shared nothing scales best

### 15. DISTRIBUTED DATABASE SYSTEMS
#### Definition:
- Data spread across multiple machines
#### Features:
- Network-connected nodes
- Shared data access

#### Types:
- Homogeneous (same system)
- Heterogeneous (different systems)

#### Transactions:
- Local
- Global

#### Key Insight
> Distribution increases reach but adds complexity

### 16. DISTRIBUTED SYSTEM PROS & CONS
#### Advantages:
- Data sharing
- Fault tolerance
- Availability

#### Disadvantages:
- Complexity
- Bugs
- Overhead

### 17. SCALING DATABASES
#### Problem:
- Single machine limits
#### Solutions:
- Vertical scaling
- Horizontal scaling

### 18. VERTICAL SCALING
#### Definition:
- Increase machine power
#### Pros:
- Simpler
- Less maintenance
#### Cons:
- Single point of failure
- Limited growth

### 19. HORIZONTAL SCALING
#### Definition:
- Add more machines
#### Pros:
- Better fault tolerance
- High scalability
#### Cons:
- Complex system design

#### Key Insight
> Modern systems prefer horizontal scaling :contentReference[oaicite:5]{index=5}

### 20. SCALING TECHNIQUES
#### 1. Master-Slave:
- Writes → master
- Reads → slaves
- Issue: replication delay

#### 2. Sharding:
- Split data across nodes
- No cross-shard joins

#### Other Approaches:
- Multi-master
- No joins (denormalization)
- In-memory DB

#### Key Insight
> Scaling trades consistency for performance

### 21. BIG PICTURE
System Evolution:
Centralized → Client-Server → Parallel → Distributed → Scaled Systems

### 22. FINAL TAKEAWAY
You now understand:
- Performance metrics
- Architecture types
- Parallel & distributed systems
- Scaling strategies

#### Mental Model
Optimize → Architect → Parallelize → Distribute → Scale

---
## CS2001 – Week 12, Lecture 4
### 1. INTRODUCTION
Focus:
→ Big Data + NOSQL + CAP Theorem
#### Goal:
- Understand why RDBMS is not enough
- Understand NOSQL systems
#### Core Idea
> Scale changes everything :contentReference[oaicite:0]{index=0}

### 2. WHAT IS BIG DATA
#### Definition:
- Data too large and complex for traditional systems
#### Challenges:
- Storage
- Processing
- Analysis
- Querying
- Visualization
#### Key Insight
> Problem is not just size, but complexity :contentReference[oaicite:1]{index=1}

### 3. CHARACTERISTICS OF BIG DATA (5 V’s)
- Volume → size of data
- Variety → types (text, image, video, etc.)
- Velocity → speed of generation
- Variability → inconsistency
- Veracity → data quality

#### Key Insight
> Big Data = unpredictable + massive + fast

### 4. WHAT IS NOSQL
#### Definition:
- Non-relational database systems
- Data not stored in tables
#### Meaning:
- “Not Only SQL”
#### Key Features:
- No fixed schema
- Horizontal scalability
- Distributed storage

#### Key Insight
> Flexibility over structure :contentReference[oaicite:2]{index=2}

### 5. WHY NOSQL EMERGED
#### Reasons:
- Big data explosion
- Web-scale applications
- Need for real-time systems

#### “Perfect Storm”:
- Large data
- New requirements
- Flexible data types

#### Key Insight
> NOSQL is not replacement, but extension of RDBMS :contentReference[oaicite:3]{index=3}

### 6. NOSQL VS RDBMS
#### NOSQL Advantages:
- Scalable
- Flexible schema
- High performance (writes)
- Fault tolerant

#### NOSQL Disadvantages:
- No joins
- Weak consistency
- No standard query language

#### Key Insight
> Trade structure for scalability

### 7. CAP THEOREM
#### Three Properties:
- Consistency (C)
- Availability (A)
- Partition Tolerance (P)

#### Definitions:
- Consistency → same data everywhere
- Availability → always respond
- Partition tolerance → survive network failure

### 8. CAP THEOREM RULE
#### Statement:
> Cannot achieve all three simultaneously

#### Conclusion:
``Pick any two: C, A, P``

#### Key Insight
> Trade-offs are unavoidable :contentReference[oaicite:4]{index=4}

### 9. CAP DECISIONS
#### Traditional RDBMS:
- CA (Consistency + Availability)

#### NOSQL Systems:
- AP (Availability + Partition)
- CP (Consistency + Partition)

#### Key Insight
> Large systems prioritize availability

### 10. CONSISTENCY MODELS
#### Strong Consistency:
- ACID
#### Weak Consistency:
- BASE

#### ACID:
- Atomicity
- Consistency
- Isolation
- Durability

#### BASE:
- Basically Available
- Soft State
- Eventual Consistency

#### Key Insight
> BASE enables scalability

### 11. EVENTUAL CONSISTENCY
#### Definition:
- Updates propagate over time
- All nodes become consistent eventually

#### Example:
- Write on one node
- Other nodes update later

#### Key Insight
> Immediate correctness is sacrificed for speed :contentReference[oaicite:5]{index=5}

### 12. GOSSIP PROTOCOL
#### Idea:
- Nodes randomly share updates
#### Analogy:
- Like spreading rumors

#### Result:
- Eventually all nodes sync

#### Key Insight
> Random propagation ensures scalability

### 13. TYPES OF NOSQL DATABASES
#### 1. Key-Value Stores
- Data = key → value
- Very fast
#### Example:
- Redis, DynamoDB

#### 2. Document Stores
- Data stored as JSON/XML documents
- Nested structure
#### Example:
- MongoDB, CouchDB

#### 3. Column Stores
- Data stored in column families
- Efficient for large datasets
#### Example:
- Cassandra, BigTable

#### 4. Graph Stores
- Nodes + edges
- Relationship-focused
#### Example:
- Neo4j

#### Key Insight
> Different models for different problems :contentReference[oaicite:6]{index=6}

### 14. KEY-VALUE MODEL
#### Operations:
``get(key)``
``put(key, value)``
``delete(key)``

#### Features:
- Simple
- Fast
- Scalable

#### Limitation:
- Cannot model complex relations

### 15. DOCUMENT MODEL
#### Structure:
- JSON-like
- Nested objects

#### Features:
- Flexible schema
- Complex data support

#### Key Insight
> Best for semi-structured data

### 16. COLUMN MODEL
#### Structure:
- Column families
- Sparse storage

#### Features:
- Efficient reads
- Data locality

#### Key Insight
> Optimized for large-scale analytics

### 17. GRAPH MODEL
#### Structure:
- Nodes + edges
#### Features:
- Relationship queries
- Traversals

#### Key Insight
> Best for interconnected data

### 18. RELATIONAL VS NON-RELATIONAL
#### Relational:
- Structured data
- Strong consistency
- SQL-based

#### Non-Relational:
- Flexible data
- Scalable
- Eventual consistency

#### Key Insight
> Choose based on problem, not trend

### 19. BIG PICTURE
Evolution:
RDBMS → Scaling issues → NOSQL → Distributed systems

### 20. FINAL TAKEAWAY
You now understand:
- Big data challenges
- NOSQL fundamentals
- CAP theorem trade-offs
- Types of NOSQL systems

#### Mental Model
Big Data → Break RDBMS → Relax guarantees → Scale horizontally

---
## CS2001 – Week 12, Lecture 5
### 1. INTRODUCTION
Final lecture of DBMS  
Focus:
→ Real-world databases + full course consolidation  
Goal:
> Understand database ecosystem + connect everything learned

### 2. RELATIONAL DATABASE MODEL
- Data stored in tables (rows + columns)
- Each row uniquely identified (Primary Key)
- Relations via Foreign Keys
- Query using SQL  

#### Why RDBMS dominates:
- Simplicity  
- Reliability  
- Performance  
- Flexibility  
- Enterprise adoption  

#### Key Insight
> RDBMS = foundation of modern data systems

### 3. TYPES OF DATABASE SYSTEMS
#### Commercial / Proprietary
- Oracle  
- IBM Db2  
- Microsoft SQL Server  
- Sybase  
- Teradata  

#### Open Source
- PostgreSQL  
- MySQL  
- SQLite  
- MariaDB  

#### Object-Relational
- Combines relational + object concepts  

#### Key Insight
> Industry uses both proprietary and open-source systems

### 4. MARKET OVERVIEW
- Oracle → dominant (~45–48%)  
- Microsoft → ~19%  
- IBM → ~15%  

#### Insight:
> Enterprise world heavily relies on Oracle

### 5. DBMS RANKING
Top systems:
1. Oracle  
2. MySQL  
3. SQL Server  
4. PostgreSQL  
5. Db2  

#### Trend:
- PostgreSQL rising  
- Open-source adoption increasing  

#### Key Insight
> Open-source is catching up fast

### 6. MAJOR DATABASE SYSTEMS
#### Oracle
- Multi-model DB  
- OLTP + analytics  
- Uses SQL + PL/SQL  

#### IBM Db2
- Strong enterprise analytics  

#### SQL Server
- Microsoft DB  
- Uses Transact-SQL  

#### PostgreSQL
- Powerful open-source  
- Handles large-scale systems  

#### MySQL
- Lightweight  
- Popular for web apps  

#### SQLite
- Embedded DB  
- No server required  

#### Key Insight
> DB choice depends on use-case, not popularity

### 7. OBJECT-RELATIONAL DB
- Combines:
  - Relational model  
  - Object-oriented concepts  
- Uses pointers → faster access  
- Reduces joins  

#### Limitation:
- Less used compared to NOSQL rise

### 8. COMPARISON FACTORS
Databases compared on:
- ACID compliance  
- Indexing  
- Partitioning  
- Security  
- OS support  

#### Key Insight
> Core features same, implementation differs

### 9. INDUSTRY REALITY
- RDBMS still dominant  
- NOSQL growing  

#### Why RDBMS still strong:
- Strong consistency  
- Transactions  
- Reliability  

#### Key Insight
> NOSQL complements RDBMS, doesn’t replace it

### 10. FULL COURSE RECAP
Week 1:
- DBMS basics  

Week 2–3:
- Relational model  
- SQL  

Week 4:
- Advanced SQL  
- Transactions  

Week 5–6:
- Functional dependencies  
- Normalization  

Week 7:
- Application architecture  

Week 8–9:
- Storage  
- Indexing (B+ Trees, Hashing)  

Week 10:
- Query processing  
- Optimization  

Week 11:
- Transactions  
- Concurrency  
- Recovery  

Week 12:
- Big Data  
- NOSQL  
- CAP theorem  
- DB ecosystem  

#### Key Insight
> You now understand the entire DB pipeline

### 11. FINAL TAKEAWAY
You now know:
- Design databases  
- Write efficient queries  
- Optimize performance  
- Understand real systems  

### Mental Model:
``Design → Query → Optimize → Scale → Choose DB``

### 12. FINAL MESSAGE
- Every system uses data  
- Every company depends on DB  
- DBMS knowledge = long-term value  

#### Key Insight
> Databases are permanent in tech

### 13. STRATEGIC NEXT STEPS
- Master SQL deeply  
- Practice with:
  - PostgreSQL  
  - SQLite  
- Focus on:
  - Indexing  
  - Transactions  
  - Query optimization  

Then move to:
→ Distributed systems  
→ Big Data  
→ System design  

---
