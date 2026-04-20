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
## CS2001 – Week 10, Lecture 3
## RECOVERABILITY, TCL & VIEW SERIALIZABILITY

### 1. CONTEXT
#### Recap
- Serializability ensures Isolation & Consistency
#### Problem
- Failures can still break Atomicity
#### Goal
- Ensure database can recover to consistent state
#### Insight
- Need recovery mechanisms beyond serializability

### 2. WHAT IS RECOVERY
#### Definition
- Process of restoring database to consistent state after failure
#### Problem Example
- Transfer A → B interrupted mid-way
- A updated, B not updated
#### Result
- Inconsistent database
#### Solution
- Rollback partial changes
#### Insight
- Recovery ensures atomicity under failures :contentReference[oaicite:2]{index=2}

### 3. RECOVERABLE SCHEDULE
#### Definition
- If Tj reads value written by Ti
- Then commit(Ti) must occur before commit(Tj)
#### Reason
- Prevent using uncommitted data
#### Insight
- Read-after-write dependency must be respected :contentReference[oaicite:3]{index=3}

### 4. IRRECOVERABLE SCHEDULE
#### Problem
- Tj commits before Ti
- But Tj read Ti’s data
#### Failure Scenario
- If Ti aborts → Tj becomes invalid
#### Result
- Cannot rollback safely
#### Insight
- Such schedules must be avoided

### 5. CASCADING ROLLBACK
#### Definition
- One failure causes multiple rollbacks
#### Cause
- Transactions depend on uncommitted data
#### Chain Effect
- T1 fails → T2 rollback → T3 rollback
#### Problem
- Large amount of work lost
#### Insight
- Expensive and undesirable :contentReference[oaicite:4]{index=4}

### 6. CASCADELESS SCHEDULE
#### Definition
- Transactions read only committed data
#### Condition
- commit(Ti) before read(Tj)
#### Advantage
- No cascading rollback
#### Insight
- Stronger than recoverable schedules :contentReference[oaicite:5]{index=5}

### 7. RELATION BETWEEN TYPES
#### Order of Strength
- Cascadeless ⊂ Recoverable ⊂ All schedules
#### Insight
- Cascadeless automatically recoverable

### 8. EXAMPLE INSIGHT
#### Irrecoverable
- Commit happens too early
#### Recoverable with cascading
- Rollback possible but expensive
#### Cascadeless
- Safe and efficient
#### Insight
- Best practice → cascadeless schedules

### 9. TRANSACTIONS IN SQL
#### Start
- Implicitly begins
#### End
- COMMIT or ROLLBACK
#### Default Behavior
- Auto-commit after each statement
#### Control
- Can disable auto-commit
#### Insight
- SQL manages transactions automatically :contentReference[oaicite:6]{index=6}

### 10. TCL (TRANSACTION CONTROL LANGUAGE)
#### Commands
- COMMIT
- ROLLBACK
- SAVEPOINT
- SET TRANSACTION
#### Scope
- Works with INSERT, UPDATE, DELETE
#### Insight
- Controls transaction execution

### 11. COMMIT
#### Definition
- Makes changes permanent
#### Effect
- Writes data to database
#### Property
- Cannot be undone after commit
#### Insight
- Marks successful completion :contentReference[oaicite:7]{index=7}

### 12. ROLLBACK
#### Definition
- Undo uncommitted changes
#### Scope
- Only after last commit
#### Effect
- Restores previous state
#### Insight
- Ensures atomicity :contentReference[oaicite:8]{index=8}

### 13. SAVEPOINT
#### Definition
- Intermediate checkpoint in transaction
#### Purpose
- Partial rollback
#### Syntax
- SAVEPOINT name
#### Rollback
- ROLLBACK TO name
#### Insight
- Fine-grained control over transactions :contentReference[oaicite:9]{index=9}

### 14. RELEASE SAVEPOINT
#### Definition
- Removes savepoint
#### Effect
- Cannot rollback to it anymore
#### Insight
- Frees resources

### 15. SET TRANSACTION
#### Purpose
- Define transaction properties
#### Options
- READ ONLY
- READ WRITE
#### Insight
- Controls behavior of transaction

### 16. VIEW SERIALIZABILITY
#### Motivation
- Conflict serializability too restrictive
#### Goal
- Allow more valid schedules
#### Insight
- Weaker but more flexible condition :contentReference[oaicite:10]{index=10}

### 17. VIEW EQUIVALENCE
#### Two schedules are equivalent if:
#### (1) Initial Read
- Same transaction reads initial value
#### (2) Read-Write Pair
- Reads same value written by same transaction
#### (3) Final Write
- Same transaction performs last write
#### Insight
- Based on data flow, not ordering :contentReference[oaicite:11]{index=11}

### 18. VIEW SERIALIZABLE
#### Definition
- Equivalent to a serial schedule under view equivalence
#### Insight
- More schedules qualify compared to conflict serializable

### 19. KEY RELATION
#### Property
- Conflict serializable ⇒ View serializable
#### But
- View serializable ⇏ Conflict serializable
#### Insight
- View is more general

### 20. BLIND WRITE
#### Definition
- Write without prior read
#### Role
- Enables view serializability without conflict serializability
#### Insight
- Key concept in weaker schedules

### 21. TESTING VIEW SERIALIZABILITY
#### Difficulty
- No simple graph-based method
#### Complexity
- NP-complete problem
#### Meaning
- No efficient general solution
#### Insight
- Harder than conflict serializability :contentReference[oaicite:12]{index=12}

### 22. PRACTICAL APPROACH
#### Strategy
- Check sufficient conditions
#### Limitation
- May miss valid schedules
#### Insight
- Trade-off between accuracy and efficiency

### 23. EXAMPLE STRATEGY
#### Step 1
- List all possible serial schedules
#### Step 2
- Apply final write condition
#### Step 3
- Apply initial read condition
#### Step 4
- Apply read-write pairing
#### Result
- Identify equivalent serial schedule

### 24. COMPLEX SERIALIZABILITY
#### Observation
- Some schedules:
  - Not conflict serializable
  - Not view serializable
  - Still produce correct result
#### Reason
- Depends on actual computations
#### Insight
- Beyond read-write analysis :contentReference[oaicite:13]{index=13}

### 25. FINAL TAKEAWAYS
#### Core Ideas
- Recovery ensures atomicity after failure
- Cascadeless schedules are safest
- TCL controls transaction lifecycle
- View serializability expands valid schedules
- Testing view serializability is computationally hard

### MEMORY LINES
#### Quick Recall
- Recovery → rollback inconsistency
- Cascading → chain rollback
- Cascadeless → safest execution
- COMMIT → permanent
- ROLLBACK → undo
- View → weaker than conflict
---
## CS2001 – Week 10, Lecture 4
## CONCURRENCY CONTROL & LOCK-BASED PROTOCOLS

### 1. CONTEXT
#### Recap
- Serializability ensures correctness
- Recovery ensures atomicity
#### Problem
- Designing correct schedules manually is hard
#### Goal
- Automatically ensure safe concurrent execution
#### Insight
- Need concurrency control mechanisms

### 2. CONCURRENCY CONTROL
#### Definition
- Mechanism to ensure correct concurrent execution
#### Requirements
- Conflict serializability
- Recoverability (preferably cascadeless)
#### Problem
- Serial execution → poor performance
#### Insight
- Balance between correctness and performance :contentReference[oaicite:2]{index=2}

### 3. KEY IDEA
#### Approach
- Control access to shared data
#### Method
- Allow only safe interleavings
#### Insight
- Prevent conflicts instead of fixing later

### 4. LOCKING CONCEPT
#### Definition
- Lock = permission to access data item
#### Rule
- Must acquire lock before accessing data
#### Insight
- Ensures mutual exclusion

### 5. TYPES OF LOCKS
#### Shared Lock (S)
- Read only
- Multiple transactions allowed
#### Exclusive Lock (X)
- Read + Write
- Only one transaction allowed
#### Insight
- Reads can share, writes need exclusivity :contentReference[oaicite:3]{index=3}

### 6. LOCK COMPATIBILITY
#### Rules
- S + S → Allowed
- S + X → Not allowed
- X + X → Not allowed
#### Insight
- Prevents inconsistent reads/writes :contentReference[oaicite:4]{index=4}

### 7. LOCK OPERATIONS
#### lock-S(Q)
- Request shared lock
#### lock-X(Q)
- Request exclusive lock
#### unlock(Q)
- Release lock
#### Insight
- Transactions must explicitly manage locks

### 8. LOCKING PROTOCOL
#### Definition
- Rules for acquiring and releasing locks
#### Purpose
- Restrict unsafe schedules
#### Insight
- Ensures serializability indirectly

### 9. LOCK REQUEST PROCESS
#### Steps
- Transaction requests lock
- If compatible → granted
- Else → wait
#### Insight
- Waiting ensures correctness

### 10. HOLDING LOCKS
#### Rule
- Must hold lock while accessing data
#### Important
- Releasing too early is dangerous
#### Insight
- Timing of unlock is critical :contentReference[oaicite:5]{index=5}

### 11. EXAMPLE: SERIAL EXECUTION
#### Scenario
- T1 transfers money
- T2 calculates total
#### Result
- Always correct output
#### Insight
- Serial execution is safe baseline

### 12. BAD CONCURRENT SCHEDULE
#### Problem
- Early unlock of data item
#### Result
- Other transaction reads partial update
#### Example Result
- Incorrect total (250 instead of 300)
#### Insight
- Intermediate state exposed → inconsistency :contentReference[oaicite:6]{index=6}

### 13. GOOD CONCURRENT SCHEDULE
#### Fix
- Delay unlocking until safe point
#### Result
- Other transaction waits
#### Outcome
- Correct result (300)
#### Insight
- Proper lock duration ensures correctness :contentReference[oaicite:7]{index=7}

### 14. DEADLOCK
#### Definition
- Two or more transactions waiting indefinitely
#### Example
- T1 holds A, needs B
- T2 holds B, needs A
#### Result
- Circular waiting
#### Insight
- System stuck permanently :contentReference[oaicite:8]{index=8}

### 15. DEADLOCK HANDLING
#### Solution
- Abort one transaction
- Release locks
#### Insight
- Break circular dependency

### 16. TRADEOFF
#### Without Locks
- Inconsistent data
#### With Locks
- Deadlocks possible
#### Insight
- Deadlocks preferable over inconsistency :contentReference[oaicite:9]{index=9}

### 17. TWO-PHASE LOCKING (2PL)
#### Purpose
- Ensure conflict serializability
#### Phases
#### Growing Phase
- Acquire locks
- No releases
#### Shrinking Phase
- Release locks
- No new locks
#### Insight
- Enforces disciplined locking :contentReference[oaicite:10]{index=10}

### 18. LOCK POINT
#### Definition
- Point where last lock is acquired
#### Property
- Determines serialization order
#### Insight
- Basis for correctness

### 19. LIMITATION OF 2PL
#### Issue
- Cannot generate all serializable schedules
#### But
- Ensures correctness
#### Insight
- Practical compromise

### 20. LOCK CONVERSIONS
#### Upgrade
- S → X (during growing phase)
#### Downgrade
- X → S (during shrinking phase)
#### Insight
- Flexible locking improves efficiency :contentReference[oaicite:11]{index=11}

### 21. AUTOMATIC LOCKING (READ)
#### Process
- If no X-lock → grant S-lock
- Else → wait
#### Insight
- DBMS can handle locking internally

### 22. AUTOMATIC LOCKING (WRITE)
#### Process
- Need X-lock
- Upgrade if holding S-lock
- Else request X-lock
#### Insight
- Writes require stricter control

### 23. DEADLOCK IN 2PL
#### Observation
- Even 2PL allows deadlocks
#### Insight
- Serializability ≠ deadlock-free :contentReference[oaicite:12]{index=12}

### 24. STARVATION
#### Definition
- Transaction waits indefinitely
#### Causes
- Continuous priority to others
- Repeated rollbacks
#### Insight
- Fairness issue in scheduling :contentReference[oaicite:13]{index=13}

### 25. CASCADING ROLLBACK
#### Cause
- Reading uncommitted data
#### Effect
- Multiple rollbacks
#### Insight
- Still possible under 2PL :contentReference[oaicite:14]{index=14}

### 26. STRICT TWO-PHASE LOCKING
#### Rule
- Hold X-locks till commit/abort
#### Advantage
- Prevent cascading rollback
#### Insight
- Safer than basic 2PL :contentReference[oaicite:15]{index=15}

### 27. RIGOROUS 2PL
#### Rule
- Hold ALL locks till commit/abort
#### Advantage
- Strongest guarantee
#### Tradeoff
- Lower concurrency
#### Insight
- Maximum safety, minimum parallelism

### 28. LOCK MANAGER
#### Role
- Handles lock requests
- Grants/denies locks
#### Communication
- Transactions send requests
#### Insight
- Central control system :contentReference[oaicite:16]{index=16}

### 29. LOCK TABLE
#### Structure
- Tracks:
  - Granted locks
  - Waiting requests
#### Implementation
- In-memory hash table
#### Behavior
- Queue for requests
- Grant if compatible
#### Insight
- Core data structure for locking :contentReference[oaicite:17]{index=17}

### 30. FINAL TAKEAWAYS
#### Core Ideas
- Concurrency control ensures correctness
- Locks enforce isolation
- 2PL ensures serializability
- Deadlocks are unavoidable
- Tradeoff: safety vs concurrency

### MEMORY LINES
#### Quick Recall
- Lock → control access
- S → read, X → write
- 2PL → grow then shrink
- Deadlock → circular wait
- Strict 2PL → safer execution
---
## CS2001 – Week 10, Lecture 5
## DEADLOCK HANDLING & TIMESTAMP-BASED PROTOCOLS

### 1. CONTEXT
#### Recap
- Locking ensures isolation
- Two-phase locking ensures serializability
#### Problem
- Deadlocks occur frequently
#### Goal
- Handle, prevent, or avoid deadlocks
#### Insight
- Need systematic deadlock management

### 2. DEADLOCK
#### Definition
- Set of transactions waiting on each other
#### Condition
- Circular waiting
#### Example
- T1 waits for T2
- T2 waits for T1
#### Insight
- System gets stuck indefinitely :contentReference[oaicite:2]{index=2}

### 3. DEADLOCK HANDLING STRATEGIES
#### Categories
- Prevention
- Detection
- Recovery
#### Insight
- Trade-off between complexity and performance

### 4. DEADLOCK PREVENTION
#### Goal
- Ensure deadlock never occurs
#### Methods
- Pre-declare all locks
- Impose ordering on data items
#### Drawback
- Reduced concurrency
#### Insight
- Avoid cycle formation :contentReference[oaicite:3]{index=3}

### 5. TIMESTAMP
#### Definition
- Unique identifier assigned to transaction
#### Meaning
- Represents relative start time
#### Rule
- Smaller timestamp → older transaction
#### Insight
- Used to enforce ordering :contentReference[oaicite:4]{index=4}

### 6. WAIT-DIE SCHEME
#### Type
- Non-preemptive
#### Rule
- Older transaction → wait
- Younger transaction → rollback (die)
#### Condition
- If TS(Ti) < TS(Tj) → Ti waits
- Else → Ti dies
#### Insight
- Older transactions get priority :contentReference[oaicite:5]{index=5}

### 7. WAIT-DIE CHARACTERISTICS
#### Behavior
- Younger transactions repeatedly restart
#### Advantage
- Prevents deadlock
#### Drawback
- More rollbacks
#### Insight
- Conservative approach

### 8. WOUND-WAIT SCHEME
#### Type
- Preemptive
#### Rule
- Older transaction → preempts (wounds)
- Younger transaction → waits
#### Condition
- If TS(Ti) < TS(Tj) → Tj is rolled back
- Else → Ti waits
#### Insight
- Aggressive strategy :contentReference[oaicite:6]{index=6}

### 9. WOUND-WAIT CHARACTERISTICS
#### Advantage
- Fewer rollbacks compared to wait-die
#### Behavior
- Older transactions dominate
#### Insight
- More efficient in practice

### 10. COMMON PROPERTY
#### Rule
- Restart with same timestamp
#### Purpose
- Maintain priority order
#### Insight
- Prevent starvation :contentReference[oaicite:7]{index=7}

### 11. TIMEOUT SCHEME
#### Idea
- Wait only for fixed time
#### If timeout
- Rollback and restart
#### Advantage
- Simple implementation
#### Drawback
- Starvation possible
#### Insight
- Not very reliable :contentReference[oaicite:8]{index=8}

### 12. DEADLOCK DETECTION
#### Approach
- Use Wait-For Graph
#### Nodes
- Transactions
#### Edge Ti → Tj
- Ti waiting for Tj
#### Insight
- Captures dependency structure :contentReference[oaicite:9]{index=9}

### 13. DEADLOCK CONDITION
#### Rule
- Cycle in graph ⇒ deadlock
#### No cycle ⇒ safe
#### Insight
- Same principle as precedence graph

### 14. DETECTION PROCESS
#### Steps
- Build wait-for graph
- Periodically check for cycles
#### Insight
- Dynamic monitoring required

### 15. DEADLOCK RECOVERY
#### Action
- Rollback one or more transactions
#### Goal
- Break cycle
#### Insight
- Must sacrifice some work :contentReference[oaicite:10]{index=10}

### 16. VICTIM SELECTION
#### Criteria
- Minimum cost
#### Factors
- Work done
- Resources used
- Number of rollbacks
#### Insight
- Optimize rollback impact :contentReference[oaicite:11]{index=11}

### 17. ROLLBACK STRATEGIES
#### Full Rollback
- Abort entire transaction
#### Partial Rollback
- Rollback to safe point
#### Insight
- Partial rollback is more efficient

### 18. STARVATION IN RECOVERY
#### Problem
- Same transaction repeatedly chosen
#### Solution
- Increase cost of repeated rollbacks
#### Insight
- Fairness must be ensured :contentReference[oaicite:12]{index=12}

### 19. TIMESTAMP-BASED PROTOCOL
#### Idea
- Use timestamps instead of locks
#### Goal
- Ensure serializability
#### Advantage
- No waiting → no deadlock
#### Insight
- Different approach to concurrency :contentReference[oaicite:13]{index=13}

### 20. DATA ITEM TIMESTAMPS
#### Maintain for each item Q
- W-timestamp(Q): last write time
- R-timestamp(Q): last read time
#### Insight
- Tracks data usage history :contentReference[oaicite:14]{index=14}

### 21. READ RULE
#### If TS(Ti) < W-timestamp(Q)
- Reject read → rollback
#### Else
- Allow read
- Update R-timestamp(Q)
#### Insight
- Prevent reading obsolete data :contentReference[oaicite:15]{index=15}

### 22. WRITE RULE (CASE 1)
#### If TS(Ti) < R-timestamp(Q)
- Reject write → rollback
#### Reason
- Value already used by newer transaction
#### Insight
- Prevent inconsistency

### 23. WRITE RULE (CASE 2)
#### If TS(Ti) < W-timestamp(Q)
- Reject write → rollback
#### Reason
- Writing obsolete value
#### Insight
- Maintain correct ordering

### 24. WRITE RULE (CASE 3)
#### Otherwise
- Allow write
- Update W-timestamp(Q)
#### Insight
- Valid operation

### 25. KEY PROPERTY
#### Result
- Operations follow timestamp order
#### Outcome
- Conflict serializability ensured
#### Insight
- Implicit ordering replaces locks :contentReference[oaicite:16]{index=16}

### 26. NO DEADLOCK
#### Reason
- Transactions never wait
#### Behavior
- Immediate rollback instead
#### Insight
- Eliminates circular wait :contentReference[oaicite:17]{index=17}

### 27. LIMITATIONS
#### Issues
- May not be recoverable
- May not be cascadeless
#### Insight
- Trade-off for deadlock freedom :contentReference[oaicite:18]{index=18}

### 28. FINAL TAKEAWAYS
#### Core Ideas
- Deadlocks are inevitable in locking
- Prevention uses ordering or timestamps
- Detection uses wait-for graph
- Recovery requires rollback
- Timestamp protocol avoids deadlock

### MEMORY LINES
#### Quick Recall
- Deadlock → circular wait
- Wait-die → younger dies
- Wound-wait → older kills
- Detection → cycle check
- Timestamp → no locks, no deadlock
---
