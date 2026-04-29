## CS2001 – Week 11, Lecture 1
## BACKUP & RECOVERY – CONCEPTS AND STRATEGIES

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
---
## CS2001 – Week 11, Lecture 2
## FAILURE CLASSIFICATION, STORAGE & LOG-BASED RECOVERY

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
---
