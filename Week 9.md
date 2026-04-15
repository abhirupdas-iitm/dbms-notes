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
## CS2001 – Week 9, Lecture 2
### 1. CONTEXT
#### Recap
- Indexing improves search performance
- Ordered indices introduced
#### Problem
- Need efficient structure for large data
- Must work for disk-based systems
#### Goal
- Build scalable search structures

### 2. SEARCH DATA STRUCTURES
#### Linear Search
- Time → O(n)
- Used for unsorted data
#### Binary Search
- Time → O(log n)
- Requires sorted data
#### Binary Search Tree (BST)
- Search → O(h)
- h = height of tree
#### Key Insight
- Performance depends on height

### 3. PROBLEM WITH BST
#### Worst Case
- Tree becomes skewed
- Height → O(n)
#### Result
- Search becomes O(n)
#### Cause
- Inserting sorted data

### 4. BALANCED BST
#### Definition
- Tree where height h ≈ O(log n)
#### Benefit
- Guarantees efficient search
#### Key Insight
- Balance ensures performance

### 5. TYPES OF BALANCING
#### Worst-case Guarantee
- AVL Tree
- |hL − hR| ≤ 1
#### Randomized
- Randomized BST
- Skip List
#### Amortized
- Splay Tree
#### Insight
- Different strategies ensure balance

### 6. LIMITATION OF BALANCED BST
#### Issues
- Complex rotations
- High overhead
#### Limitation
- Not suitable for disk-based systems
#### Reason
- Designed for in-memory structures

### 7. NEED FOR NEW STRUCTURE
#### Requirement
- Efficient for large datasets
- Works with disk storage
- Avoid complex balancing
#### Solution
- 2-3-4 Tree

### 8. INTRO TO 2-3-4 TREE
#### Definition
- Balanced multi-way search tree
#### Key Property
- All leaves at same depth
#### Result
- Height → O(log n)

### 9. NODE TYPES
#### 2-Node
- 1 key
- 2 children
#### 3-Node
- 2 keys
- 3 children
#### 4-Node
- 3 keys
- 4 children
#### Key Insight
- Nodes can store multiple values

### 10. ORDERING PROPERTY
#### Rule
- Left subtree < key(s)
- Right subtree > key(s)
#### For 3-node
- Values split into 3 regions
#### For 4-node
- Values split into 4 regions

### 11. SEARCH IN 2-3-4 TREE
#### Process
- Compare with multiple keys
- Choose correct subtree
#### Insight
- Generalized BST search

### 12. INSERTION OVERVIEW
#### Step 1
- Locate correct position via search
#### Step 2
- Insert based on node type

### 13. INSERT CASES
#### Case 1: 2-Node
- Convert to 3-node
#### Case 2: 3-Node
- Convert to 4-node
#### Case 3: 4-Node
- Split required

### 14. NODE SPLITTING
#### Given Node
- [S, M, L]
#### Action
- M moves to parent
- S becomes left child
- L becomes right child
#### Insight
- Maintains sorted order

### 15. SPLITTING CASES
#### Root Split
- New root created
- Height increases
#### Parent is 2-Node
- Parent becomes 3-node
#### Parent is 3-Node
- Parent becomes 4-node

### 16. SPLITTING STRATEGIES
#### Early Split
- Split while traversing down
#### Late Split
- Split during insertion
#### Insight
- Both have same complexity O(log n)

### 17. HEIGHT PROPERTY
#### Key Rule
- Height increases only at root split
#### Result
- Height always O(log n)

### 18. EXAMPLE INSERTION
#### Sequence
- 10, 30 → 3-node
- 60 → 4-node
- Insert 20 → split root
#### Observation
- Tree grows upward only when needed

### 19. KEY ADVANTAGES
#### Properties
- Always balanced
- Efficient search, insert, delete
- Sorted data maintained
- Scales well

### 20. DISADVANTAGES
#### Issues
- Multiple node types
- Complex implementation

### 21. OPTIMIZATION IDEA
#### Approach
- Use fixed-size nodes
#### Benefit
- Simpler implementation
#### Insight
- Leads to B-Trees

### 22. GENERALIZATION
#### Property
- Nodes can have multiple keys
#### Rule
- At least half full
#### Insight
- Improves space efficiency

### 23. CONNECTION TO DATABASES
#### Use
- External storage structures
#### Extension
- 2-3-4 Tree → B-Tree → B+ Tree
#### Key Insight
- Foundation of database indexing

### 24. FINAL TAKEAWAYS
#### Core Ideas
- BST fails without balance
- Balanced BST not suitable for disk
- 2-3-4 tree ensures balance
- Multi-key nodes reduce height

### 25. MEMORY LINES
#### Key Reminders
- BST → height dependent
- Balance → log n
- 2-3-4 → multi-key nodes
- Split → upward push
- Root split → height change
---
