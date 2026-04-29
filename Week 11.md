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
