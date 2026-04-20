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
- Transaction = logical unit of work :contentReference[oaicite:2]{index=2}

### 3. PROBLEMS IN TRANSACTIONS
#### Failures
- Hardware failure
- Software failure
- System crash
#### Concurrency
- Multiple transactions executing simultaneously
#### Key Insight
- DBMS must handle both failures and concurrency safely :contentReference[oaicite:3]{index=3}

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
- Either complete transaction OR rollback everything :contentReference[oaicite:4]{index=4}

### 6. CONSISTENCY
#### Definition
- Database must move from one valid state to another
#### Example Constraint
- A + B must remain constant
#### Types
- Explicit constraints (PK, FK)
- Implicit constraints (business rules)
#### Insight
- Transaction preserves invariants :contentReference[oaicite:5]{index=5}

### 7. ISOLATION
#### Definition
- Concurrent transactions should not interfere
#### Problem Example
- T2 reads partially updated data of T1
#### Solution
- Execute transactions as if serial
#### Insight
- Concurrent execution must appear sequential :contentReference[oaicite:6]{index=6}

### 8. DURABILITY
#### Definition
- Once committed, changes persist
#### Requirement
- Survive crashes and failures
#### Insight
- Committed data is permanent :contentReference[oaicite:7]{index=7}

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
- Similar to process states in OS :contentReference[oaicite:8]{index=8}

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
- Improves throughput significantly :contentReference[oaicite:9]{index=9}

### 13. CONCURRENCY CONTROL
#### Purpose
- Prevent conflicts between transactions
#### Goal
- Maintain isolation and consistency
#### Insight
- Required for safe parallel execution :contentReference[oaicite:10]{index=10}

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
- Schedule defines execution order :contentReference[oaicite:11]{index=11}

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