## CS2001 – Week 11, Lecture 1
### BACKUP & RECOVERY – CONCEPTS AND STRATEGIES
### 1. CONTEXT
#### Recap
- Transactions ensure ACID properties
- Concurrency introduces serializability issues
- Locking ensures isolation but causes deadlocks
#### Shift
- From transaction correctness → data safety
#### Focus
- Backup and recovery mechanisms
#### Insight
- Even correct systems can fail → need recovery

### 2. WHAT IS BACKUP
#### Definition
- A representative copy of database contents
#### Includes
- Data files
- Control files
- Logs
#### Purpose
- Protect against unexpected failures
#### Types
- Physical backup → full system copy
- Logical backup → extracted data (tables, views, etc.)
#### Insight
- Backup = insurance for data

### 3. WHAT IS RECOVERY
#### Definition
- Process of restoring database to last consistent state
#### Mechanism
- Uses database logs
#### Log Contains
- Transaction sequence
- State changes
- Modified values
#### Insight
- Recovery replays or undoes operations

### 4. WHY BACKUP IS NECESSARY
#### Disaster Recovery
- Hardware failure
- Malware
- Natural causes
#### Client Requirements
- Restore previous versions
#### Auditing
- Historical data inspection
#### Downtime Reduction
- Faster system restoration
#### Insight
- Backup supports both safety and business continuity

### 5. TYPES OF BACKUP DATA
#### Business Data
- Core application data (users, transactions)
#### System Data
- Configurations, logs, dependencies
#### Media Data
- Images, videos, audio
#### Insight
- All layers must be backed up

### 6. BACKUP STRATEGY OVERVIEW
#### Key Questions
- What to backup?
- How often?
- How much?
#### Goal
- Balance performance, cost, and safety
#### Insight
- Strategy depends on system requirements

### 7. FULL BACKUP
#### Definition
- Complete copy of entire database
#### Includes
- Tables, indexes, procedures, everything
#### Requirement
- Must be done at least once
#### Frequency
- Depends on system type
#### Insight
- Baseline for all backups

### 8. FULL BACKUP ADVANTAGES
#### Simple Recovery
- Single backup needed
#### Independence
- No dependency on other backups
#### Reliability
- Loss of one backup doesn’t affect others
#### Insight
- Easiest restore mechanism

### 9. FULL BACKUP DISADVANTAGES
#### High Time
- Long backup duration
#### High Storage
- Large space required
#### Downtime
- System may be unavailable
#### Insight
- Not scalable for large systems

### 10. INCREMENTAL BACKUP
#### Definition
- Backup only changed data since last backup
#### Example
- 2TB DB → only 5% change → backup 5%
#### Usage
- Full backup once, then incremental daily
#### Insight
- Efficient for large systems

### 11. INCREMENTAL ADVANTAGES
#### Less Storage
- Only changed data stored
#### Faster Backup
- Smaller data size
#### Reduced Downtime
- Minimal system interruption
#### Insight
- Highly efficient for daily operations

### 12. INCREMENTAL DISADVANTAGES
#### Complex Recovery
- Need full + all incrementals
#### Dependency Chain
- Missing one → recovery fails
#### Insight
- Recovery cost increases

### 13. DIFFERENTIAL BACKUP
#### Definition
- Backup changes since last full backup
#### Behavior
- Accumulates changes over time
#### Insight
- Middle ground between full and incremental

### 14. DIFFERENTIAL ADVANTAGES
#### Faster Recovery
- Only full + latest differential needed
#### Fewer Backup Sets
- Reduced dependency chain
#### Insight
- Better recovery efficiency

### 15. DIFFERENTIAL DISADVANTAGES
#### Larger Size
- Grows over time
#### Storage Cost
- Higher than incremental
#### Insight
- Trade-off between speed and storage

### 16. COMPARISON
#### Full
- Large, simple, slow
#### Incremental
- Small, fast, complex recovery
#### Differential
- Medium size, faster recovery
#### Insight
- Choose based on workload

### 17. BACKUP SCHEDULE (MONTHLY)
#### Pattern
- Full backup once
- Weekly differential
- Daily incremental
#### Recovery Requirement
- 1 full + 1 differential + few incrementals
#### Insight
- Optimizes recovery time

### 18. COLD BACKUP
#### Definition
- Backup when system is offline
#### Property
- Consistent state guaranteed
#### Limitation
- System unavailable
#### Insight
- Safe but not always practical

### 19. HOT BACKUP
#### Definition
- Backup while system is running
#### Requirement
- High availability systems
#### Examples
- Banking systems
- Stock trading systems
#### Insight
- Real-time backup

### 20. HOT BACKUP ADVANTAGES
#### Availability
- No downtime
#### Point-in-time Recovery
- More precise restoration
#### Efficiency
- Works well with dynamic data
#### Insight
- Essential for 24×7 systems

### 21. HOT BACKUP DISADVANTAGES
#### Complexity
- Hard to implement
#### Cost
- High maintenance
#### Risk
- Errors during process affect backup
#### Insight
- Trade-off for availability

### 22. TRANSACTION LOGGING
#### Definition
- Recording all database operations
#### Purpose
- Enable recovery
#### Content
- Transactions, states, changes
#### Insight
- Core mechanism for recovery

### 23. ROLE OF LOGS IN BACKUP
#### Function
- Restore consistency after failure
#### Usage
- Replay or undo transactions
#### Insight
- Logs complement backups

### 24. FINAL TAKEAWAYS
#### Core Ideas
- Backup protects against data loss
- Recovery restores consistency
- Full, incremental, differential → trade-offs
- Hot backup enables real-time systems
- Logs are essential for recovery

### MEMORY LINES
#### Quick Recall
- Backup → copy
- Recovery → restore
- Full → everything
- Incremental → changes since last
- Differential → changes since full
- Logs → recovery backbone

### Notes taken from Activity Questions 11.1
1. 
---
## CS2001 – Week 11, Lecture 2
### FAILURE CLASSIFICATION, STORAGE & LOG-BASED RECOVERY

### 1. CONTEXT
#### Recap
- Backup strategies ensure data availability
#### Problem
- Failures still occur during execution
#### Goal
- Recover database while preserving ACID
#### Assumption
- Single transaction (no concurrency yet)
#### Insight
- Recovery ensures Atomicity & Durability

### 2. ROLE IN ACID
#### Atomicity
- Recovery system ensures all-or-nothing
#### Durability
- Ensures committed changes persist
#### Consistency
- Supported indirectly
#### Isolation
- Handled by concurrency control
#### Insight
- Recovery subsystem = A + D backbone

### 3. FAILURE CLASSIFICATION
#### Transaction Failure
- Logical errors
- System errors (deadlock, abort)
#### System Crash
- Power failure
- OS crash
- Memory loss
#### Disk Failure
- Head crash
- Data loss on disk
#### Insight
- Different failures → different strategies

### 4. FAIL-STOP ASSUMPTION
#### Definition
- Disk data not corrupted on crash
#### Meaning
- Only memory lost
#### Insight
- Simplifies recovery model

### 5. RECOVERY PROBLEM
#### Example
- Transfer A → B
#### Issue 1
- A updated, B not updated → inconsistency
#### Issue 2
- Commit done but not written to disk → lost update
#### Insight
- Need controlled recovery mechanism

### 6. RECOVERY ALGORITHM STRUCTURE
#### Part 1
- Actions during normal execution (logging)
#### Part 2
- Actions after failure (recovery)
#### Insight
- Must record before failure to recover later

### 7. STORAGE TYPES
#### Volatile Storage
- Lost on crash
- Example: RAM
#### Non-Volatile Storage
- Survives crash
- Example: disk, SSD
#### Stable Storage
- Ideal (never fails)
- Implemented via replication
#### Insight
- Recovery depends on storage reliability

### 8. STABLE STORAGE IMPLEMENTATION
#### Method
- Maintain multiple copies of data
#### Strategy
1. Write first copy
2. If success → write second copy
3. Complete only after both succeed
#### Insight
- Redundancy ensures safety

### 9. FAILURE DURING WRITE
#### Cases
- Successful write
- Partial failure (corrupt)
- Total failure (not written)
#### Insight
- Must detect inconsistencies

### 10. RECOVERY OF COPIES
#### Method
- Use checksum to detect errors
#### Fix
- Replace bad copy with correct one
#### If both valid but different
- Choose one as correct
#### Insight
- Data integrity maintained via comparison

### 11. DATA ACCESS MODEL
#### Blocks
- Physical blocks → disk
- Buffer blocks → memory
#### Operations
- input(B): disk → memory
- output(B): memory → disk
#### Insight
- DBMS controls data movement

### 12. TRANSACTION WORK AREA
#### Concept
- Each transaction has local copy
#### Notation
- xi = local copy of X
#### Insight
- Isolation at memory level

### 13. READ & WRITE OPERATIONS
#### read(X)
- Copy from buffer → local
#### write(X)
- Copy local → buffer
#### Important
- Disk write (output) can be delayed
#### Insight
- Buffering improves performance

### 14. CORE IDEA OF RECOVERY
#### Rule
- Log changes BEFORE applying them
#### Reason
- Enables undo/redo
#### Insight
- Logging = foundation of recovery

### 15. LOG-BASED RECOVERY
#### Definition
- Maintain log of all updates
#### Stored in
- Stable storage
#### Insight
- Sequential history of operations

### 16. LOG RECORD FORMAT
#### Start
- < Ti start >
#### Update
- < Ti, X, V1, V2 >
  - V1 = old value
  - V2 = new value
#### Commit
- < Ti commit >
#### Insight
- Full trace of transaction

### 17. WRITE-AHEAD LOGGING (WAL)
#### Rule
- Log must be written before database write
#### Reason
- Ensures recoverability
#### Insight
- Critical DBMS rule

### 18. DATABASE MODIFICATION SCHEMES
#### Immediate Modification
- Write before commit allowed
#### Deferred Modification
- Write only after commit
#### Focus
- Immediate modification used here
#### Insight
- Trade-off between simplicity and performance

### 19. TRANSACTION COMMIT
#### Condition
- Commit log written to stable storage
#### Requirement
- All previous logs must be written
#### Note
- Data may still be in buffer
#### Insight
- Commit ≠ disk write completion

### 20. UNDO OPERATION
#### Definition
- Restore old value (V1)
#### Direction
- Backward scan
#### Logging
- Compensation log written
#### Insight
- Used for rollback

### 21. REDO OPERATION
#### Definition
- Apply new value (V2)
#### Direction
- Forward scan
#### Logging
- No extra log needed
#### Insight
- Used to reapply committed changes

### 22. WHEN TO UNDO / REDO
#### Undo if
- < Ti start > exists
- No commit/abort
#### Redo if
- < Ti commit > exists
#### Special Case
- Even aborted transactions may be redone (repeat history)
#### Insight
- Ensures consistency

### 23. NORMAL ROLLBACK
#### Steps
- Scan log backward
- Undo each operation
- Write compensation logs
- Write < Ti abort >
#### Insight
- Complete reversal of transaction

### 24. RECOVERY AFTER FAILURE
#### Undo
- Incomplete transactions
#### Redo
- Completed transactions
#### Insight
- Restore correct final state

### 25. CHECKPOINTING
#### Problem
- Full log scan is expensive
#### Solution
- Periodic checkpoints
#### Insight
- Reduces recovery time

### 26. CHECKPOINT PROCESS
#### Steps
1. Stop updates
2. Flush logs to disk
3. Flush buffers to disk
4. Write < checkpoint L >
#### Insight
- Snapshot of system state

### 27. RECOVERY WITH CHECKPOINT
#### Ignore
- Transactions before checkpoint (completed)
#### Redo
- Transactions committed after checkpoint
#### Undo
- Transactions active at failure
#### Insight
- Limits recovery scope

### 28. CHECKPOINT TRADEOFF
#### Frequent
- Faster recovery
- Lower performance
#### Rare
- Better performance
- Slower recovery
#### Insight
- Balance required

### 29. FINAL TAKEAWAYS
#### Core Ideas
- Failures are inevitable
- Logging enables recovery
- Undo restores old state
- Redo restores committed state
- Checkpoints optimize recovery

### MEMORY LINES
#### Quick Recall
- Log → history
- V1 = old, V2 = new
- Undo → rollback
- Redo → reapply
- Checkpoint → shortcut recovery

### Notes taken from Activity Questions 11.2
1. 
---
## CS2001 – Week 11, Lecture 3
## TRANSACTIONAL LOGGING, HOT BACKUP & CONCURRENT RECOVERY

### 1. CONTEXT
#### Recap
- Failures unavoidable
- Log-based recovery ensures ACID
#### Focus
- Hot backup + concurrent recovery
#### Insight
- Real systems ≠ serial → concurrency matters

### 2. HOT BACKUP
#### Definition
- Backup while DB is running
#### Use Cases
- Banking systems
- Stock trading
- Real-time systems
#### Problem
- Data keeps changing during backup
#### Insight
- Backup may become inconsistent

### 3. TRANSACTION LOGGING AS HOT BACKUP
#### Key Idea
- Backup logs instead of full data
#### Why
- Logs are small
- Faster backup
#### Strategy
- Cold backup → data
- Hot backup → logs
#### Insight
- Logs bridge gap between backup and failure

### 4. WRITE ORDER RULE (CRITICAL)
#### Mandatory Order
1. Write to log
2. Write to database
#### Reason
- Enables recovery if crash occurs
#### Insight
- This is WAL in action

### 5. CRASH SCENARIO LOGIC
#### Case
- Crash before DB write
#### Result
- Backup inconsistent
#### Solution
1. Recover backup
2. Replay logs
#### Insight
- Logs restore missing updates

### 6. RECOVER vs RESTORE
#### Recover
- Load data + logs from backup
#### Restore
- Apply logs to reach consistent state
#### Insight
- Recover = fetch, Restore = fix

### 7. LOG REPLAY STRATEGY
#### Approach
- Replay ALL logs (usually)
#### Reason
- Simpler than selective replay
#### Insight
- Slight redundancy > complexity

### 8. CONCURRENT TRANSACTIONS
#### Reality
- Multiple transactions execute together
#### Shared Components
- Same log
- Same buffer
#### Insight
- Logs interleaved across transactions

### 9. CRITICAL ASSUMPTION
#### Rule
- No transaction updates item modified by uncommitted transaction
#### Implementation
- Strict Two-Phase Locking
#### Reason
- Enables correct undo
#### Insight
- Prevents cascading rollback

### 10. DATA ACCESS (CONCURRENT)
#### Structure
- Shared buffer
- Private workspace per transaction
#### Behavior
- Read → buffer → local
- Write → local → buffer
#### Insight
- Isolation via private copies

### 11. LOG STRUCTURE (SAME AS BEFORE)
#### Entries
- < Ti start >
- < Ti, X, V1, V2 >
- < Ti commit >
#### Insight
- Logging unchanged, complexity ↑

### 12. ROLLBACK (NORMAL)
#### Steps
1. Scan log backward
2. Undo each update
3. Write CLR (compensation log)
4. Write < Ti abort >
#### Insight
- Same as serial case

### 13. CHECKPOINT RECAP (CONCURRENT)
#### Categories
- Ta: commit before checkpoint → ignore
- Tb: start before, commit after → redo
- Tc: start after, commit → redo
- Td: incomplete → undo
#### Insight
- Checkpoint limits recovery scope

### 14. CORE RECOVERY STRATEGY
#### Step 1
- Redo everything after checkpoint
#### Step 2
- Undo incomplete transactions
#### Insight
- “Redo first, then undo”

### 15. CRITICAL CONCEPT (VERY IMPORTANT)
#### Problem
- Incomplete transactions lost after crash
#### Solution
- Redo them first
- Then undo them
#### Insight
- Must reach failure state before rollback

### 16. REDO-UNDO PHASES
#### Redo Phase
- Apply ALL updates (committed + uncommitted)
#### Undo Phase
- Undo only incomplete transactions
#### Insight
- Known as “Repeating History”

### 17. REDO PHASE ALGORITHM
#### Steps
1. Find last checkpoint
2. Initialize undo-list
3. Scan forward:
   - Update → redo (write V2)
   - Start → add to undo-list
   - Commit/Abort → remove from undo-list
#### Insight
- Builds undo-list dynamically

### 18. REDO OPERATIONS
#### Based on Log
- INSERT → insert again
- DELETE → delete again
- UPDATE → apply V2
#### Insight
- Reconstruct state at failure

### 19. UNDO PHASE ALGORITHM
#### Steps
1. Scan backward
2. For each Ti in undo-list:
   - Write V1 (undo)
   - Write CLR
3. On < Ti start >:
   - Write < Ti abort >
   - Remove from undo-list
4. Stop when list empty
#### Insight
- Full rollback of incomplete transactions

### 20. UNDO OPERATIONS
#### Based on Log
- INSERT → delete
- DELETE → insert
- UPDATE → restore V1
#### Insight
- Reverse effect completely

### 21. COMPLETE FLOW
#### After Crash
1. Recover backup
2. Redo phase
3. Undo phase
4. Resume system
#### Insight
- Deterministic recovery pipeline

### 22. FINAL TAKEAWAYS
#### Key Ideas
- Logs = hot backup backbone
- Redo everything after checkpoint
- Undo incomplete transactions
- Redo first, undo later

### MEMORY LINES
#### Quick Recall
- Log first → DB later
- Recover → load
- Restore → replay
- Redo → forward
- Undo → backward
- Redo ALL, Undo SOME

### Notes taken from Activity Questions 11.3
1. 
---
## CS2001 – Week 11, Lecture 4
### EARLY LOCK RELEASE, LOGICAL UNDO & ADVANCED RECOVERY
### 1. CONTEXT
#### Recap
- Log-based recovery handles concurrency
- Redo → then Undo
#### Problem
- Real systems use early lock release
#### Goal
- Handle recovery when locks are released before commit
#### Insight
- Traditional undo no longer works directly

### 2. EARLY LOCK RELEASE
#### Definition
- Locks released before transaction completes
#### Used In
- B+ trees (indexes)
- System data structures
#### Reason
- Improve concurrency
#### Insight
- Breaks strict 2PL assumption

### 3. PROBLEM WITH EARLY LOCK RELEASE
#### Scenario
- T1 inserts (V1, R1)
- Lock released
- T2 inserts (V2, R2)
#### Issue
- Node structure changes
#### Result
- Cannot revert to old value safely
#### Insight
- Physical undo becomes incorrect

### 4. WHY PHYSICAL UNDO FAILS
#### Traditional Undo
- Replace new value with old value
#### Problem
- Also removes changes by other transactions
#### Example
- Undo T1 → accidentally undo T2
#### Insight
- Violates correctness

### 5. SOLUTION: LOGICAL UNDO
#### Idea
- Undo operation logically, not physically
#### Example
- Insert → undo by delete
- Delete → undo by insert
#### Insight
- Reverse effect, not state

### 6. LOGICAL UNDO LOGGING
#### Definition
- Log contains undo operation (not just old value)
#### Type
- Logical operations
#### Contrast
- Physical logging → values
- Logical logging → actions
#### Insight
- Needed for early lock release

### 7. PHYSICAL REDO (IMPORTANT)
#### Rule
- Redo is always physical
#### Reason
- Logical redo is complex
#### Insight
- Hybrid system:
  - Redo → physical
  - Undo → logical

### 8. OPERATION LOGGING
#### Structure
- < Ti, Oj, operation-begin >
- Physical update logs
- < Ti, Oj, operation-end, U >
#### U
- Logical undo operation
#### Insight
- Combines physical + logical logging

### 9. OPERATION LOGGING FLOW
#### Step 1
- Log operation begin
#### Step 2
- Log physical updates (V1 → V2)
#### Step 3
- Log operation end with undo info
#### Insight
- Full trace of operation lifecycle

### 10. EXAMPLE (INDEX INSERT)
#### Operation
- Insert (K5, RID7) into index
#### Logs
- operation-begin
- physical updates
- operation-end (delete K5, RID7)
#### Insight
- Undo = delete operation

### 11. CRASH BEFORE OPERATION END
#### Condition
- operation-end not found
#### Action
- Use physical undo
#### Reason
- Operation incomplete
#### Insight
- Treat as normal rollback

### 12. CRASH AFTER OPERATION END
#### Condition
- operation-end exists
#### Action
- Use logical undo
#### Ignore
- Physical undo logs
#### Insight
- Operation already applied

### 13. KEY RULE
#### If operation incomplete
- Use physical undo
#### If operation complete
- Use logical undo
#### Insight
- Decision depends on log state

### 14. TRANSACTION ROLLBACK (LOGICAL UNDO)
#### Process
- Scan log backward
#### Case 1
- < Ti, X, V1, V2 > → physical undo
#### Case 2
- operation-end → logical undo
#### Case 3
- operation-abort → skip
#### Case 4
- redo-only → ignore
#### Insight
- Mixed undo strategy

### 15. LOGICAL UNDO EXECUTION
#### Steps
- Execute undo operation (U)
- Log actions normally
- Write operation-abort
#### Insight
- Undo itself is logged

### 16. SKIPPING LOG RECORDS
#### When
- operation-abort found
#### Action
- Skip to operation-begin
#### Reason
- Avoid duplicate undo
#### Insight
- Prevents inconsistency

### 17. END OF ROLLBACK
#### Condition
- < Ti start > found
#### Action
- Write < Ti abort >
#### Insight
- Transaction fully undone

### 18. FAILURE RECOVERY WITH LOGICAL UNDO
#### Same High-Level Steps
1. Redo phase
2. Undo phase
#### Difference
- Undo uses logical + physical
#### Insight
- Extension of previous algorithm

### 19. REDO PHASE (UNCHANGED)
#### Rule
- Redo all updates
#### Includes
- Committed
- Uncommitted
#### Insight
- Repeat history principle

### 20. UNDO PHASE (MODIFIED)
#### Process
- Backward scan
#### Use
- Logical undo for completed operations
- Physical undo for incomplete ones
#### Insight
- Hybrid undo mechanism

### 21. FINAL RECOVERY MODEL
#### Flow
1. Recover backup
2. Redo all updates
3. Undo incomplete transactions
   - logical or physical
#### Insight
- Fully general recovery system

### 22. WHERE EARLY LOCK RELEASE USED
#### Systems
- Index structures (B+ trees)
- Free space management
- Block tracking
#### Insight
- High-frequency structures

### 23. PLANNING BACKUP & RECOVERY
#### Factors
#### Data Importance
- Critical data → more backups
#### Frequency of Change
- Frequent updates → frequent backup
#### Recovery Speed
- Business downtime constraints
#### Equipment
- Hardware + software capability
#### Employees
- Skilled personnel required
#### Storage
- Onsite vs offsite backups
#### Insight
- Technical + business decision

### 24. FINAL TAKEAWAYS
#### Core Ideas
- Early lock release improves concurrency
- Physical undo fails in such systems
- Logical undo solves the issue
- Redo always physical
- Recovery becomes hybrid

### MEMORY LINES
#### Quick Recall
- Early release → logical undo
- Insert → delete
- Delete → insert
- Redo → always physical
- Undo → depends on state

### Notes taken from Activity Questions 11.4
1. 
---
## CS2001 – Week 11, Lecture 5
## RAID (REDUNDANT ARRAY OF INDEPENDENT DISKS)

### 1. WHAT IS RAID?
#### Definition
- Multiple disks combined → appear as a single disk
#### Goals
- High capacity
- High speed (parallelism)
- High reliability (redundancy)
#### Insight
- Parallel disks = performance + fault tolerance

### 2. WHY RAID IS NEEDED
#### Problem
- More disks → higher chance of failure
#### Example
- 100 disks → failure likely within ~41 days
#### Solution
- Add redundancy
#### Insight
- Reliability comes from redundancy, not fewer failures

### 3. THREE CORE TECHNIQUES
#### (A) MIRRORING
- Duplicate data across disks
- Writes → both disks
- Reads → any disk
##### Pros
- Very high reliability
- Fast reads
##### Cons
- 50% storage efficiency
#### (B) STRIPING
- Split data across disks
##### Types
1. Bit-level
2. Byte-level
3. Block-level (most used)
##### Pros
- High parallelism
- Faster reads/writes
##### Cons
- No redundancy (alone)
#### (C) PARITY
- Extra bit/block for error detection + correction
- Uses XOR
##### Idea
- Missing data = XOR of remaining + parity
##### Pros
- Storage efficient
- Enables recovery
##### Cons
- Computation overhead

### 4. RAID LEVELS OVERVIEW
#### Important
- Numbers ≠ ranking
- Just identifiers
#### Common Levels
- RAID 0 → Striping
- RAID 1 → Mirroring
- RAID 5 → Distributed parity
- RAID 6 → Dual parity
- RAID 10 → Hybrid

### 5. RAID 0 (STRIPING)
#### Features
- No redundancy
- 100% storage utilization
- Highest performance
#### Problem
- One disk failure → total data loss
#### Use Case
- Temporary / non-critical data

### 6. RAID 1 (MIRRORING)
#### Features
- Duplicate data
- Excellent fault tolerance
- Parallel reads
#### Cost
- 50% storage efficiency
#### Insight
- Data survives single disk failure

### 7. RAID 2 (HAMMING CODE)
#### Features
- Bit-level striping
- Error correction using Hamming code
#### Problem
- Complex
- Not used in practice

### 8. RAID 3 (BYTE STRIPING + PARITY)
#### Features
- Byte-level striping
- Single parity disk
#### Problem
- Cannot handle multiple requests
- All disks accessed together

### 9. RAID 4 (BLOCK STRIPING + PARITY)
#### Features
- Block-level striping
- Dedicated parity disk
#### Pros
- Good read performance
#### Cons
- Parity disk bottleneck
- Write performance low
#### Limit
- Handles only 1 disk failure

### 10. RAID 5 (DISTRIBUTED PARITY)
#### Features
- Block striping
- Parity distributed across disks
#### Pros
- No bottleneck disk
- Good read performance
#### Cons
- Write overhead (parity updates)
#### Limit
- Survives 1 disk failure

### 11. RAID 6 (DUAL PARITY)
#### Features
- Two parity blocks (P + Q)
- Uses Reed-Solomon codes
#### Pros
- Survives 2 disk failures
#### Cons
- Slow writes
- Higher computation

### 12. HYBRID RAID
#### Idea
- Combine RAID levels

### 13. RAID 01 (0 + 1)
#### Structure
- Mirror of stripes
#### Flow
- First stripe → then mirror
#### Issue
- Less reliable than RAID 10

### 14. RAID 10 (1 + 0)
#### Structure
- Stripe of mirrors
#### Flow
- First mirror → then stripe
#### Pros
- High performance
- High reliability
#### Insight
- Best for databases

### 15. RAID TRADE-OFF TRIANGLE
#### Three Factors
- Speed
- Cost
- Fault tolerance
#### Examples
- RAID 0 → fast + cheap
- RAID 5 → cheap + safe
- RAID 10 → fast + safe

### 16. PRACTICAL USAGE
#### RAID 0
- Logging, rendering
- Temporary data
#### RAID 1
- OS, transactional DB
#### RAID 5
- Data warehouse, web servers
#### RAID 6
- Archival systems
#### RAID 10
- Databases, high-performance apps

### 17. CHOOSING RAID LEVEL
#### Factors
- Cost
- Performance
- Failure handling
- Rebuild time

### 18. IMPORTANT INSIGHTS
#### RAID 0
- Not fault tolerant
#### RAID 2/3/4
- Rarely used
#### RAID 5
- Best balance
#### RAID 1
- Better for frequent writes

### 19. PERFORMANCE NOTE
#### RAID 1 vs RAID 5
- RAID 1 → faster writes
- RAID 5 → better storage efficiency

### 20. WHAT RAID DOES NOT DO
#### DOES NOT
- Guarantee uptime
- Replace backups
- Prevent human errors
- Protect from malware
- Protect from disasters
#### Insight
- RAID ≠ Backup

### 21. FINAL TAKEAWAYS
#### Core Ideas
- RAID = performance + redundancy
- Uses:
  - Mirroring
  - Striping
  - Parity
- Trade-offs always exist

### MEMORY LINES
- Striping → speed
- Mirroring → safety
- Parity → balance
- RAID ≠ Backup

### Notes taken from Activity Questions 11.5
1. 
---
---
