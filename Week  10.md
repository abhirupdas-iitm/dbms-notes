## CS2001 – Week 10, Lecture 1
## TRANSACTION CONCEPT, ACID PROPERTIES, STATES & SCHEDULES

### 1. CONTEXT
#### Recap
- Completed indexing, hashing, and physical design
#### Shift
- From data organization → data operations
#### Focus
- Transactions
- Concurrency issues
#### Insight
- Transactions define how databases are actually used

### 2. WHAT IS A TRANSACTION
#### Definition
- A transaction is a unit of program execution that accesses and possibly updates data
#### Components
- Read operations
- Write operations
- Computation
#### Example
Transfer $50 from A → B:
1. read(A)
2. A = A − 50
3. write(A)
4. read(B)
5. B = B + 50
6. write(B)
#### Key Insight
- Transaction = logical unit of work

### 3. PROBLEMS IN TRANSACTIONS
#### Failures
- Hardware failure
- Software failure
- System crash
#### Concurrency
- Multiple transactions executing simultaneously
#### Key Insight
- DBMS must handle both failures and concurrency safely

### 4. ACID PROPERTIES OVERVIEW
#### Definition
- Properties that ensure reliable transaction execution
#### Components
- Atomicity
- Consistency
- Isolation
- Durability

### 5. ATOMICITY
#### Definition
- All or nothing execution
#### Problem Example
- A debited but B not credited → inconsistency
#### Requirement
- Partial updates must not be reflected
#### Insight
- Either complete transaction OR rollback everything

### 6. CONSISTENCY
#### Definition
- Database must move from one valid state to another
#### Example Constraint
- A + B must remain constant
#### Types
- Explicit constraints (PK, FK)
- Implicit constraints (business rules)
#### Insight
- Transaction preserves invariants 

### 7. ISOLATION
#### Definition
- Concurrent transactions should not interfere
#### Problem Example
- T2 reads partially updated data of T1
#### Solution
- Execute transactions as if serial
#### Insight
- Concurrent execution must appear sequential

### 8. DURABILITY
#### Definition
- Once committed, changes persist
#### Requirement
- Survive crashes and failures
#### Insight
- Committed data is permanent 

### 9. ACID QUICK RECALL
#### Atomicity
- All or nothing
#### Consistency
- Valid state maintained
#### Isolation
- Transactions independent
#### Durability
- Changes never lost

### 10. TRANSACTION STATES
#### Active
- Transaction executing
#### Partially Committed
- Final statement executed
#### Failed
- Error detected
#### Aborted
- Rolled back
#### Committed
- Successfully completed
#### Terminated
- Finished (commit or abort)
#### Insight
- Similar to process states in OS

### 11. STATE TRANSITIONS
#### Active → Partially Committed
- After last statement
#### Partially Committed → Committed
- If no failure
#### Active/Partial → Failed
- On error
#### Failed → Aborted
- Rollback executed
#### Aborted → Active
- Restart possible
#### Aborted → Terminated
- Kill transaction
#### Committed → Terminated
- Normal completion
#### Key Insight
- Only root split equivalent: commit defines success

### 12. CONCURRENT EXECUTION
#### Definition
- Multiple transactions executed simultaneously
#### Advantages
- Better CPU utilization
- Better disk utilization
- Reduced response time
#### Insight
- Improves throughput significantly

### 13. CONCURRENCY CONTROL
#### Purpose
- Prevent conflicts between transactions
#### Goal
- Maintain isolation and consistency
#### Insight
- Required for safe parallel execution

### 14. SCHEDULE
#### Definition
- Sequence of operations from multiple transactions
#### Properties
- Contains all instructions
- Preserves order within each transaction
#### End Condition
- Commit → success
- Abort → failure
#### Insight
- Schedule defines execution order

### 15. SERIAL SCHEDULE
#### Definition
- Transactions executed one after another
#### Property
- Always consistent
#### Example
- T1 → then T2
#### Insight
- Baseline for correctness

### 16. NON-SERIAL SCHEDULE
#### Definition
- Interleaved execution of transactions
#### Possibility
- Can be correct OR incorrect
#### Insight
- Needs validation

### 17. SERIALIZABLE SCHEDULE
#### Definition
- Equivalent to some serial schedule
#### Property
- Produces same final result
#### Example
- Schedule 3 equivalent to Schedule 1
#### Insight
- Key correctness condition

### 18. INCONSISTENT SCHEDULE
#### Definition
- Violates database invariants
#### Example
- A + B not preserved
#### Cause
- Improper interleaving
#### Insight
- Not all concurrent schedules are valid

### 19. EXAMPLE INSIGHT
#### Observation
- Schedule 1, 2 → serial → consistent
- Schedule 3 → non-serial but equivalent → valid
- Schedule 4 → non-serializable → invalid
#### Key Insight
- Final state consistency matters

### 20. FINAL TAKEAWAYS
#### Core Ideas
- Transaction = unit of execution
- ACID ensures correctness
- Concurrency improves performance
- Schedule defines execution
- Serializability ensures correctness

### MEMORY LINES
#### Quick Recall
- Transaction → logical unit
- ACID → reliability
- States → lifecycle
- Schedule → execution order
- Serializable → correctness
---
## CS2001 – Week 10, Lecture 2
## SERIALIZABILITY & CONFLICT SERIALIZABILITY

### 1. CONTEXT
#### Recap
- Transactions ensure correctness using ACID
- Concurrent execution improves performance
#### Problem
- Not all concurrent schedules are correct
#### Goal
- Identify when concurrent execution is safe
#### Insight
- Need formal correctness condition → Serializability

### 2. SERIALIZABILITY
#### Assumption
- Each transaction individually preserves consistency
#### Definition
- A schedule is serializable if it is equivalent to a serial schedule
#### Meaning
- Produces same final result as some serial execution
#### Types
- Conflict Serializability
- View Serializability
#### Insight
- Serializability ensures correctness in concurrency :contentReference[oaicite:2]{index=2}

### 3. KEY IDEA
#### Serial Execution
- Always consistent
#### Concurrent Execution
- May or may not be consistent
#### Requirement
- Concurrent schedule must behave like serial
#### Insight
- Equivalence to serial execution is sufficient

### 4. SIMPLIFIED MODEL
#### Assumption
- Only consider read and write operations
#### Ignore
- Computation steps (local)
#### Reason
- Only read/write affect database state
#### Insight
- Simplifies analysis without losing correctness :contentReference[oaicite:3]{index=3}

### 5. CONFLICTING INSTRUCTIONS
#### Definition
- Two instructions conflict if:
  - They access same data item
  - At least one is a write
#### Cases
- Read–Read → No conflict
- Read–Write → Conflict
- Write–Read → Conflict
- Write–Write → Conflict
#### Insight
- Conflicts define execution order constraints :contentReference[oaicite:4]{index=4}

### 6. NON-CONFLICTING INSTRUCTIONS
#### Property
- Can be swapped without affecting result
#### Meaning
- Order does not matter
#### Insight
- Swapping is key to proving serializability

### 7. CONFLICT EQUIVALENCE
#### Definition
- Two schedules are conflict equivalent if:
  - One can be obtained from other
  - By swapping non-conflicting instructions
#### Insight
- Equivalent schedules produce same result :contentReference[oaicite:5]{index=5}

### 8. CONFLICT SERIALIZABILITY
#### Definition
- Schedule is conflict serializable if:
  - It is conflict equivalent to a serial schedule
#### Process
- Repeatedly swap non-conflicting instructions
#### Goal
- Transform into serial order
#### Insight
- Practical method to verify serializability :contentReference[oaicite:6]{index=6}

### 9. EXAMPLE: SERIALIZABLE SCHEDULE
#### Observation
- Some non-serial schedules can be rearranged
#### Method
- Swap operations that do not conflict
#### Result
- Convert into serial schedule
#### Insight
- Non-serial ≠ incorrect

### 10. EXAMPLE: NON-SERIALIZABLE
#### Problem
- Conflicts prevent swapping
#### Result
- Cannot transform into serial schedule
#### Insight
- Such schedules are unsafe

### 11. BAD SCHEDULE EXAMPLE
#### Scenario
- T1: Withdraw 100 from A
- T2: Add interest (1.005 × balance)
#### Problem
- Incorrect interleaving
#### Result
- Final balance becomes incorrect
#### Insight
- Violates correctness despite valid individual transactions :contentReference[oaicite:7]{index=7}

### 12. SERIAL SCHEDULE COMPARISON
#### Valid Orders
- T1 → T2
- T2 → T1
#### Property
- Both produce consistent results
#### Insight
- Multiple valid serial outcomes possible

### 13. NON-SERIAL BUT SERIALIZABLE
#### Example
- Mixed execution but still correct
#### Reason
- Can be rearranged to serial order
#### Insight
- Concurrency is safe if serializable

### 14. IMPORTANT RESULT
#### Statement
- Conflict serializable ⇒ Serializable
#### But
- Serializable ⇏ Conflict serializable
#### Insight
- Conflict serializability is sufficient but not necessary :contentReference[oaicite:8]{index=8}

### 15. SPECIAL CASE
#### Observation
- Some schedules:
  - Not conflict serializable
  - Still serializable
#### Reason
- No read dependency on overwritten values
#### Insight
- Rare but important edge case

### 16. PRECEDENCE GRAPH
#### Definition
- Directed graph representing conflicts
#### Nodes
- Transactions
#### Edge Ti → Tj
- If Ti’s operation conflicts and occurs before Tj
#### Insight
- Captures dependency between transactions :contentReference[oaicite:9]{index=9}

### 17. GRAPH CONSTRUCTION
#### Rule 1
- For write(X), add edge to future read/write on X
#### Rule 2
- For read(X), add edge to future write on X
#### Insight
- Edges represent ordering constraints

### 18. TEST FOR SERIALIZABILITY
#### Condition
- Graph must be acyclic
#### If Acyclic
- Schedule is conflict serializable
#### If Cyclic
- Not conflict serializable
#### Insight
- Cycle = contradiction in ordering :contentReference[oaicite:10]{index=10}

### 19. TOPOLOGICAL SORT
#### Definition
- Linear ordering of nodes in DAG
#### Purpose
- Gives equivalent serial schedule
#### Insight
- Extract execution order from graph

### 20. EXAMPLE ANALYSIS
#### Steps
- Build graph from schedule
- Add edges based on conflicts
- Check for cycles
#### Result
- If no cycle → valid schedule
#### Insight
- Systematic method replaces manual swapping

### 21. FINAL TAKEAWAYS
#### Core Ideas
- Serializability = correctness condition
- Conflict defines constraints
- Swapping proves equivalence
- Graph method gives efficient test

### MEMORY LINES
#### Quick Recall
- Serializable → behaves like serial
- Conflict → same data + write
- Swap → only non-conflicting
- Graph → cycle check
- DAG → safe schedule
---
