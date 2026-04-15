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

### Notes taken from Activity Questions 9.1
1. 
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

### Notes taken from Activity Questions 9.2
1. 
---
## CS2001 – Week 9, Lecture 3
### 1. CONTEXT
#### Recap
- 2-3-4 trees provide a balanced multi-way search structure
- They are a precursor to external indexing structures
#### Goal
- Understand B+ Tree index files
- Understand basic B-Tree idea
- See why B+ Trees are widely used in databases

### 2. INTRO TO B+ TREE
#### Definition
- B+ Tree is a balanced multi-level search tree
- It generalizes the 2-3-4 tree idea
#### Core Properties
- All leaf nodes are at the same height
- Leaf nodes contain actual data pointers
- Leaf nodes are linked for sequential access
#### Key Insight
- B+ Tree supports both random access and sequential access

### 3. WHY B+ TREE IS NEEDED
#### Problem with Indexed Sequential Files
- Performance degrades as file grows
- Overflow blocks increase
- Periodic reorganization becomes necessary

#### B+ Tree Advantage
- Reorganizes itself locally
- Avoids full file reorganization
- Maintains efficient access as data grows

### 4. NODE STRUCTURE OF B+ TREE
#### Internal Nodes
- Store search keys
- Store pointers to child nodes
#### Leaf Nodes
- Store search keys
- Store pointers to records or buckets
- Store pointer to next leaf node
#### Ordering
- Keys inside every node are sorted

### 5. FILLING CONDITIONS
#### Internal Node
- At least ceil(n / 2) children
- At most n children
- Root is an exception
#### Leaf Node
- At least ceil((n - 1) / 2) values
- At most n - 1 values
#### Root Special Cases
- If root is not a leaf, it must have at least 2 children
- If root is also a leaf, it can have between 0 and n - 1 values
#### Key Insight
- Every non-root node is at least half full

### 6. LEAF NODE PROPERTIES
#### Record Pointers
- Pointer Pi points to a file record with search-key value Ki
#### Ordering Across Leaves
- Search keys in left leaf are less than or equal to those in right leaf
#### Sequential Link
- Last pointer in leaf points to next leaf node
#### Key Insight
- Linked leaves make range queries efficient

### 7. NON-LEAF NODE PROPERTIES
#### Role
- Act as multi-level sparse index over leaf nodes
#### Search Range Rules
- P1 points to values less than K1
- Pi points to values between Ki-1 and Ki
- Last pointer points to values greater than or equal to last key
#### Insight
- Internal nodes guide search, leaf nodes hold actual access information

### 8. SEARCH IN B+ TREE
#### Process
1. Start at root
2. Compare search key with keys in current node
3. Follow the appropriate child pointer
4. Repeat until a leaf is reached
5. Search within the leaf
#### Example Idea
- To search 55:
  - Follow branch between 50 and 75
  - Reach the relevant leaf
  - Do final search inside that leaf
#### Key Insight
- Search always ends at a leaf

### 9. QUERY ALGORITHM IDEA
#### Rule
- At internal node, find the least i such that V ≤ Ki
#### Cases
- If no such i exists, follow last non-null pointer
- If V = Ki, move to Pi+1
- Else move to Pi
#### Final Step
- At leaf, if Ki = V, follow record pointer
- Otherwise record does not exist

### 10. PERFORMANCE OF B+ TREE
#### Height Bound
- Height is at most log base ceil(n / 2) of K
#### Typical Case
- Node size ≈ disk block
- n is often around 100
#### Example
- 1 million keys
- n = 100
- At most about 4 node accesses
#### Comparison
- Balanced binary tree for 1 million keys needs around 20 accesses
#### Key Insight
- B+ Tree drastically reduces disk I/O

### 11. HANDLING DUPLICATES
#### Problem
- Duplicate search keys break strict inequality
#### New Rule
- Keys satisfy K1 ≤ K2 ≤ K3 ...
#### Consequence
- Search subtree conditions become non-strict
#### Modified Search
- Traverse Pi even if V = Ki
- At leaf, if all keys are still less than V, move to right sibling
- Continue to find first occurrence
#### Procedure Idea
- Find first occurrence
- Traverse consecutive leaves to find all matches

### 12. INSERTION IN B+ TREE
#### Step 1
- Find the leaf where key should appear
#### If Key Already Exists
- Add record to file
- Add pointer to bucket if needed
#### If Key Does Not Exist
- Insert into leaf if space is available
- Otherwise split the leaf

### 13. LEAF SPLIT
#### Process
- Take all key-pointer pairs including new one
- Sort them
- Keep first ceil(n / 2) in original leaf
- Put remaining in new leaf
#### Promotion
- Let k be least key in new leaf
- Insert (k, pointer-to-new-leaf) into parent
#### Key Insight
- Parent stores separator for new leaf

### 14. NON-LEAF SPLIT
#### Condition
- Parent is already full while inserting promoted key
#### Process
- Copy node into temporary space
- Insert new key-pointer pair
- Split entries into two nodes
- Promote middle separator upward
#### Propagation
- Split may continue upward
#### Worst Case
- Root splits
- Height increases by 1

### 15. DELETION IN B+ TREE
#### Step 1
- Locate record
- Remove from file and bucket if present
#### Step 2
- Remove key-pointer entry from leaf if needed
#### If Underflow Happens
- Check sibling

### 16. MERGING DURING DELETION
#### Condition
- Entries in node and sibling fit in one node
#### Action
- Merge both into one node
- Delete corresponding separator entry from parent
- Apply recursively upward if needed

### 17. REDISTRIBUTION DURING DELETION
#### Condition
- Node and sibling together do not fit in one node
#### Action
- Redistribute entries between siblings
- Update separator key in parent
#### Key Insight
- Merge reduces nodes, redistribution preserves nodes

### 18. ROOT CHANGE DURING DELETION
#### Condition
- Root left with only one child
#### Action
- Delete root
- Sole child becomes new root
#### Key Insight
- Height can decrease only through root collapse

### 19. B+ TREE FILE ORGANIZATION
#### Idea
- B+ Tree can organize entire data file, not just index file
#### Difference
- In file organization, leaf nodes store actual records
- In index organization, leaf nodes store pointers to records
#### Common Rule
- Leaf nodes still must remain at least half full

### 20. NON-UNIQUE KEYS
#### Problem
- Many records may share same key
#### Possible Handling
- Use bucket blocks
- Use list of tuple pointers
- Add record identifier to make search key unique
#### Practical Insight
- Making key unique simplifies insertion and deletion handling

### 21. RELOCATION AND SECONDARY INDICES
#### Problem
- If records relocate, stored record pointers become invalid
#### Difficulty
- Updating many secondary index pointers is expensive
#### Practical Solution
- Use primary index search key instead of raw record pointer
#### Trade-off
- Slightly more traversal cost
- Much easier maintenance

### 22. STRING KEYS
#### Problem
- Strings are variable length
- Fan-out becomes variable
#### Practical Technique
- Prefix compression
- Use distinguishing prefix as index key
#### Example Idea
- Similar strings can be separated using useful prefixes

### 23. B-TREE INTRO
#### Core Difference from B+ TREE
- In B-Tree, a search key appears only once
- Keys need not be repeated all the way to leaf level
#### Consequence
- Some record pointers may appear in internal nodes

### 24. B+ TREE VS B-TREE
#### B+ Tree
- Leaf nodes contain data pointers
- Internal nodes guide search only
- Keys may appear multiple times
- Better for sequential access because leaves are linked
#### B-Tree
- Keys appear only once
- Internal nodes may also store record pointers
- Can sometimes find record before reaching leaf
#### Practical Insight
- B+ Tree is generally preferred in database indexing

### 25. ADVANTAGES OF B+ TREE
#### Benefits
- Balanced structure
- Efficient search, insert, delete
- Good for both point queries and range queries
- Self-organizing
- Scales well for disk-based storage

### 26. DISADVANTAGES OF B+ TREE
#### Costs
- Extra insertion overhead
- Extra deletion overhead
- Additional space overhead
- More maintenance than simple sequential files

### 27. FINAL TAKEAWAYS
#### Core Ideas
- B+ Tree is a balanced external indexing structure
- Internal nodes form sparse multi-level index
- Leaf nodes hold actual access layer and are linked
- Splits handle insertion overflow
- Merge or redistribution handles deletion underflow
- B+ Tree solves degradation problems of indexed sequential files

### 28. MEMORY LINES
#### Quick Recall
- B+ Tree → balanced + linked leaves
- Search → root to leaf
- Insert → split upward
- Delete → merge or redistribute
- B-Tree → key appears once

### Notes taken from Activity Questions 9.3
1. 
---
## CS2001 – Week 9, Lecture 4
### 1. CONTEXT
#### Recap
- Previously studied B+ Trees (ordered indexing)
- Now shifting to **hash-based indexing**
#### Objective
- Faster **exact-match retrieval**
- Avoid tree traversal overhead
As highlighted in the lecture intro, hashing directly maps keys to locations instead of navigating levels like B+ trees

### 2. WHAT IS HASHING?
#### Core Idea
- Map large domain → small range using a function
#### Definition
- Hash function:  
  `h : D → [0, N]`
- Given key `k`, output = `h(k)`
#### Important Terms
- Hash value / hash code / digest
- Collision: when `k1 ≠ k2` but `h(k1) = h(k2)`
Hashing compresses a huge search space into manageable buckets

### 3. HASH FUNCTION PROPERTIES
#### Good Hash Function Should Be:
- Fast
- Uniform (even distribution)
- Minimize collisions
#### Bad Case
- All keys → same bucket → O(n) search
#### Ideal Case
- Each bucket gets equal records
Uniform distribution is critical for performance

### 4. STATIC HASHING
#### Structure
- Fixed number of buckets
- Each bucket = disk block
#### Working
1. Compute `h(k)`
2. Go to bucket `h(k)`
3. Search inside bucket
#### Key Insight
- Direct access → no tree traversal
Buckets store multiple records → need linear scan inside bucket

### 5. COLLISIONS
#### Why They Happen
- Domain >> number of buckets
#### Example
- Different keys → same hash value
#### Handling
- Search within bucket
Collisions are unavoidable, must be managed efficiently

### 6. BUCKET OVERFLOW
#### Causes
- Too few buckets
- Skewed data
- Poor hash function
#### Solution: Overflow Buckets
##### Overflow Chaining
- Extra buckets linked like a list
##### Types
- Closed hashing → uses overflow buckets
- Open hashing → not used in DBMS
Overflow increases disk I/O → performance degradation

### 7. HASH FILE ORGANIZATION
#### Concept
- Records stored directly using hash(key)
#### Example (from slides)
- `h(dept_name) = sum(char values) mod 10`
- Example outputs:
  - Music → 1
  - Physics → 3
  - Elec Eng → 3 (collision)
Same bucket → sequential search required

### 8. HASH INDICES
#### Idea
- Hashing used for index instead of file
#### Key Points
- Usually **secondary index**
- Stores:
  - search key
  - pointer to record
Speeds up equality search queries significantly

### 9. LIMITATIONS OF STATIC HASHING
#### Major Problems
1. Fixed bucket count
2. Database growth → overflow chains
3. Space wastage if over-allocated
4. Rehashing required (expensive)
Static hashing fails in dynamic environments

### 10. DYNAMIC HASHING (EXTENDABLE HASHING)
#### Motivation
- Handle growing/shrinking databases
#### Key Idea
- Use **prefix bits of hash value**
#### Structure
- Hash gives large binary value (e.g., 32 bits)
- Use only first `i` bits
#### Bucket Table Size
- `2^i`
#### Flexibility
- Increase/decrease `i` dynamically
No need to change hash function — only use more bits

### 11. KEY CONCEPTS
#### Global Depth (i)
- Number of bits used
#### Local Depth (ij)
- Bits used by a bucket
#### Important
- Multiple table entries can point to same bucket
Actual buckets < 2^i possible

### 12. SEARCH IN DYNAMIC HASHING
#### Steps
1. Compute `h(k)`
2. Take first `i` bits
3. Go to bucket table
4. Follow pointer
5. Search inside bucket
Same simplicity as static hashing, but flexible

### 13. INSERTION
#### Case 1: Space Available
- Insert directly
#### Case 2: Bucket Full → Split
##### If i > ij
- Split bucket
- Redistribute entries
##### If i = ij
- Increase `i`
- Double table
- Then split
Table doubling is expensive but rare

### 14. DELETION
#### Steps
1. Locate record
2. Delete from bucket
#### Optimization
- Merge (coalesce) buckets
- Reduce table size (rare)
Coalescing only possible with “buddy” buckets

### 15. ADVANTAGES OF DYNAMIC HASHING
- No performance degradation with growth
- Flexible bucket management
- Efficient equality queries

### 16. DISADVANTAGES
- Extra indirection (directory lookup)
- Directory may grow large
- Splitting & doubling cost
Trade-off: flexibility vs overhead

### 17. HASHING vs ORDERED INDEXING
#### Hashing
- Best for: exact match queries
- Weak for: range queries
#### B+ Tree
- Best for: range queries
- Slightly slower for exact match
Real-world DBs often prefer B+ trees

### 18. BITMAP INDICES
#### Use Case
- Attributes with few distinct values
  - gender
  - state
  - income levels
#### Structure
- One bitmap per value
- Each bit = record presence
Example shown on page 35: bitmaps represent attribute values across records

### 19. BITMAP OPERATIONS
#### Supported Operations
- AND
- OR
- NOT
#### Example
- Male AND Income=L1 → bitwise AND
Extremely fast due to bit-level parallelism

### 20. EFFICIENCY OF BITMAPS
#### Benefits
- Very compact
- Fast logical operations
- Efficient counting
#### Example
- 1M bits processed in ~31K operations
Much faster than tuple scanning

### 21. ADVANCED NOTES
#### Deletion Handling
- Use existence bitmap
#### NULL Handling
- Maintain bitmap for NULL values
#### Hybrid Use
- Combine with B+ Trees
Useful when many records share same value

### 22. FINAL TAKEAWAYS
#### Big Picture
- Hashing → direct access (O(1) average)
- B+ Tree → ordered access (O(log n))
- Bitmap → analytical queries
#### When to Use What
- Exact match → Hashing
- Range queries → B+ Tree
- Multi-condition filters → Bitmap

### 23. MEMORY LINES
- Hashing → Direct bucket access  
- Static → Fixed, Dynamic → Flexible  
- Extendable hashing → prefix bits  
- Bitmap → bitwise filtering powerhouse

### Notes taken from Activity Questions 9.4
1. 
---
## CS2001 – Week 9, Lecture 5
### 1. CONTEXT
#### Recap
- Covered B+ Trees, Hashing, Bitmap Indexing
#### Focus
- Creating indexes in SQL
- Designing indexes effectively
#### Key Insight
- Shift from theory → practical optimization

### 2. INDEX CREATION IN SQL
#### Basic Syntax
`CREATE INDEX <index-name> ON <table-name> (attribute-list);`
#### Example
`CREATE INDEX b_index ON branch(branch_name);`
#### Drop Index
`DROP INDEX index_name;`
#### Insight
- Index is a schema object for faster access

### 3. UNIQUE INDEX
#### Definition
- Ensures no duplicate values
#### Purpose
- Enforces candidate key constraint
#### Note
- Prefer SQL UNIQUE constraint if available

### 4. TYPES OF INDEXES
#### Single Column Index
- Index on one attribute
#### Composite Index
- Index on multiple attributes
#### Function-Based Index
- Index on computed value
#### Example
CREATE INDEX idx ON emp(UPPER(name));
#### Insight
- Useful when queries apply functions

### 5. STORAGE OPTIONS
#### Parameters
- TABLESPACE → storage location
- INITIAL → initial size
- NEXT → next allocation
- PCTINCREASE → growth rate
- PCTFREE → reserved free space
#### Insight
- Controls physical storage behavior

### 6. BITMAP INDEX IN SQL
#### Syntax
`CREATE BITMAP INDEX idx ON table(column);`
#### Use Case
- Low distinct values (gender, semester)
#### Query Example
`SELECT * FROM Student WHERE Gender = 'F' AND Semester = 4;`
#### Execution
- Bitwise AND operation
#### Insight
- Very fast filtering

### 7. MULTIPLE-KEY ACCESS
#### Problem
- Queries with multiple conditions
#### Strategies
- Use one index and filter
- Use another index and filter
- Use both indices and intersect results
#### Insight
- Intersection reduces search space

### 8. COMPOSITE INDEX
#### Definition
- Index on multiple attributes
#### Example
`CREATE INDEX idx ON instructor(dept_name, salary);`
#### Advantage
- Efficient multi-condition queries
#### Key Insight
- Column order matters

### 9. ORDERING RULE
#### Lexicographic Rule
```
(a1, a2) < (b1, b2) if:
- a1 < b1 OR
- a1 = b1 AND a2 < b2
```
#### Insight
- First column dominates search

### 10. COMPOSITE INDEX BEHAVIOR
#### Efficient For
- dept = 'Finance' AND salary = 80000
- dept = 'Finance' AND salary < 80000
#### Inefficient For
- dept < 'Finance' AND salary = 80000
#### Insight
- First attribute drives filtering

### 11. PRIVILEGES REQUIRED
#### Requirements
- INDEX privilege on table
- Tablespace quota
#### Advanced
- CREATE ANY INDEX for other schemas
- QUERY REWRITE for function-based index
#### Insight
- Index creation is controlled

### 12. WHY INDEX DESIGN MATTERS
#### Observation
- Normalization is static
- Indexing is dynamic
#### Requirement
- Adapt based on usage
#### Insight
- Performance evolves over time

### 13. NO FIXED THEORY
#### Fact
- No universal best indexing strategy
#### Depends On
- Data distribution
- Query patterns
#### Insight
- Use heuristics (rules)

### 14. GROUND RULES FOR INDEXING
#### Rule 0: Trade-off
- Faster queries
- Slower updates
- More storage
#### Rule 1: Correct Tables
- Index large tables
- Use when <15% rows retrieved
- Index join columns
- Avoid small tables
#### Rule 2: Correct Columns
- High uniqueness → normal index
- Low uniqueness → bitmap index
- Avoid many nulls
- Avoid large data types
#### Rule 3: Limit Indexes
- More indexes → slower updates
- Balance read vs write
#### Rule 4: Column Order
- Most selective column first
#### Rule 5: Gather Statistics
- Helps optimizer
- Use COMPUTE STATISTICS
#### Rule 6: Drop Unused Indexes
- Remove if not used
- Improves performance

### 15. FINAL TAKEAWAYS
#### Core Idea
- Indexing is a performance optimization tool
#### Strategy
- Design based on workload, not assumptions
#### Mental Model
- Read speed vs write cost trade-off

### 16. MEMORY LINES
#### Quick Recall
- Index → speed vs cost
- Composite → order matters
- Bitmap → bitwise filtering
- Stats → optimizer support
- Drop unused → efficiency

### Notes taken from Activity Questions 9.5
1. 
---
