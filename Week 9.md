## CS2001 – Week 9, Lecture 1
### 1. MOTIVATION FOR INDEXING
#### Problem
- Searching records in a table requires scanning entire file
- Time complexity → O(n)
#### Example
- Search by Name → need to scan all records
- Search by Phone → again scan all records
#### Limitation
- Cannot sort file on multiple attributes simultaneously
#### Key Insight
- Sorting helps one query but hurts others

### 2. BASIC IDEA OF INDEXING
#### Definition
- Indexing creates a separate structure to speed up search
#### Structure
- search-key → pointer to record
#### Example
- Index on Name → sorted names + pointers
- Index on Phone → sorted phones + pointers
#### Key Insight
- Original file order does not matter
#### Result
- Search becomes O(log n) using binary search

### 3. SEARCH KEY
#### Definition
- Attribute (or set of attributes) used to look up records
#### Examples
- Name
- Phone number
- Department
#### Note
- Does not have to be primary key

### 4. INDEX FILE
#### Definition
- File containing index entries
#### Entry Format
- (search-key, pointer)
#### Property
- Much smaller than original data file
#### Key Insight
- Enables fast lookup with minimal storage

### 5. TYPES OF INDICES
#### Ordered Index
- Entries sorted on search key
#### Hash Index
- Entries distributed using hash function
#### Scope
- This lecture focuses on ordered index

### 6. INDEX EVALUATION METRICS
#### Access Types
- Equality queries
- Range queries
#### Performance Metrics
- Access time
- Insertion time
- Deletion time
- Space overhead
#### Insight
- Indexing is a trade-off system

### 7. ORDERED INDICES
#### Definition
- Index entries stored in sorted order of search key
#### Example
- Library catalog sorted by author
#### Key Insight
- Enables binary search

### 8. PRIMARY INDEX
#### Definition
- Index based on sequential order of file
#### Alternate Name
- Clustering index
#### Property
- Defines physical ordering of data
#### Note
- May or may not be primary key

### 9. SECONDARY INDEX
#### Definition
- Index on attribute not used for file ordering
#### Alternate Name
- Non-clustering index
#### Property
- Does not affect physical order
#### Key Insight
- Used for alternate search paths

### 10. INDEX-SEQUENTIAL FILE
#### Definition
- Sequential file with primary index
#### Insight
- Combines ordering + indexing

### 11. DENSE INDEX
#### Definition
- Index entry for every search-key value
#### Property
- Direct access to records
#### Advantage
- Faster lookup
#### Disadvantage
- Larger size
- Higher maintenance cost

### 12. SPARSE INDEX
#### Definition
- Index entry for only some search-key values
#### Condition
- File must be sorted on search key
#### Search Process
1. Find largest key < K
2. Jump to that location
3. Perform sequential scan
#### Advantage
- Less space
- Lower maintenance
#### Disadvantage
- Slower than dense index

### 13. SPARSE INDEX OPTIMIZATION
#### Strategy
- One index entry per block
#### Method
- Store first key of each block
#### Key Insight
- Quickly locate block, then scan inside

### 14. DENSE VS SPARSE (CORE)
#### Dense
- Fast access
- High space
- High update cost
#### Sparse
- Lower space
- Lower update cost
- Slightly slower access
#### Memory Line
- Dense → speed
- Sparse → space

### 15. SECONDARY INDEX (DETAILED)
#### Problem
- Multiple records may have same key
#### Solution
- Index points to bucket (list of pointers)
#### Key Insight
- One index entry → multiple records
#### Important Rule
- Secondary index must be dense

### 16. COST OF INDEXING
#### Advantage
- Faster search
#### Cost
- Extra storage
- Update overhead
#### Insight
- Every insert/delete must update index

### 17. PRIMARY VS SECONDARY SCAN
#### Primary Index Scan
- Efficient sequential access
#### Secondary Index Scan
- Expensive
- May require multiple disk reads
#### Reason
- Records scattered across disk

### 18. MULTILEVEL INDEX
#### Problem
- Index too large to fit in memory
#### Solution
- Build index on index
#### Structure
- Inner index → original index
- Outer index → index of inner index
#### Extension
- Can have multiple levels
#### Key Insight
- Hierarchical indexing

### 19. INDEX UPDATE – DELETION
#### Case 1: Dense Index
- Delete entry directly
#### Case 2: Sparse Index
- Replace with next key if needed
- If duplicate exists → delete entry
#### Condition
- If last occurrence → remove index entry

### 20. INDEX UPDATE – INSERTION
#### Dense Index
- Insert new key if not present
#### Sparse Index
- No change if within existing block
#### Special Case
- New block created → add index entry

### 21. SECONDARY INDEX USAGE
#### Use Case
- Query on non-primary attribute
#### Examples
- Find by department
- Find by salary
#### Insight
- Avoids full table scan

### 22. FINAL TAKEAWAYS
#### Core Ideas
- Index = search accelerator
- Ordered index enables binary search
- Dense vs sparse = trade-off
- Secondary index enables multiple query paths
- Multilevel index ensures scalability
### 23. MEMORY LINES
#### Key Reminders
- Index → pointer structure
- Dense → fast, costly
- Sparse → compact, slower
- Primary → defines order
- Secondary → alternate search
---
