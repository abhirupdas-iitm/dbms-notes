## CS2001 – Week 9, Lecture 1
### 1. WHY INDEXING? (RECAP)
#### Goal
- Speed up data access
- Avoid full table scan
#### Core Idea
Index = (search-key → pointer to record)
#### Key Insight
> Index reduces search time but adds update cost

### 2. TYPES OF INDEXING
#### Ordered Index
- Entries stored in sorted order
- Supports efficient range queries
#### Primary Index
- Defines physical order of file
- Also called clustering index
#### Secondary Index
- Does NOT define physical order
- Always dense

### 3. DENSE VS SPARSE INDEX
#### Dense Index
- Entry for every search-key
- Direct access to record

#### Sparse Index
- Entry for some search-keys (typically one per block)
#### Search Process in Sparse Index
1. Find largest key < K
2. Jump to corresponding block
3. Perform sequential scan
#### Comparison

| Feature     | Dense Index  | Sparse Index |
| ----------- | ------------ | ------------ |
| Entries     | Every record | Some records |
| Speed       | Faster       | Slower       |
| Space       | High         | Low          |
| Update Cost | High         | Lower        |
#### Critical Condition
> Sparse index works ONLY if file is sorted
#### Memory Line
> Dense → speed, Sparse → space

### 4. LIMITATIONS OF BASIC INDEXING
#### Problem
- Large datasets → index may not fit in memory
- Disk access becomes expensive
#### Insight
> Single-level index is not scalable

### 5. MULTILEVEL INDEX
#### Idea
- Build index on top of index
#### Structure
- Inner index → points to data
- Outer index → points to inner index
#### Key Insight
> Reduces search time by hierarchical lookup

### 6. NEED FOR BETTER STRUCTURES
#### Problem with Binary Search Trees (BST)
- Can become skewed → O(n)
- Even balanced trees require rotations
- High maintenance cost
- Not suitable for disk storage
#### Requirement
- Always balanced
- Efficient insert/delete
- Works for large data on disk

### 7. INTRO TO 2-3-4 TREES
#### Definition
A balanced search tree where nodes can have multiple keys
#### Node Types
- 2-node → 1 key, 2 children
- 3-node → 2 keys, 3 children
- 4-node → 3 keys, 4 children

### 8. KEY PROPERTY

> All leaves are at the same depth
#### Result
- Tree is always balanced
- Height = O(log n)

### 9. SEARCH IN 2-3-4 TREE
#### Process
- Compare key with multiple values in node
- Decide correct subtree
#### Insight
> Generalized binary search

### 10. INSERTION IN 2-3-4 TREE
#### Step 1
- Search for correct position
#### Case 1: Node is 2-node
- Convert to 3-node
#### Case 2: Node is 3-node
- Convert to 4-node
#### Case 3: Node is 4-node (FULL)
- Split required

### 11. SPLITTING RULE
Given node:
[S  M  L]
#### Action
- M moves to parent
- S becomes left child
- L becomes right child

### 12. ROOT SPLIT (IMPORTANT)
#### When root is split
- New root is created
- Height increases by 1
#### Key Insight
> Height increases ONLY when root splits

### 13. WHY 2-3-4 TREES WORK
#### Advantages
- Always balanced
- Guaranteed O(log n) search
- Efficient insertion and deletion
#### Disadvantages
- Multiple node types
- Complex implementation

### 14. TRANSITION TO B-TREES
#### Idea
- Generalize 2-3-4 tree
- Allow more keys per node
#### Purpose
- Reduce disk I/O
- Better performance for large datasets

### 15. FINAL TAKEAWAYS
#### Mental Model
- Index → speeds up search
- Multilevel index → scales indexing
- 2-3-4 tree → ensures balance
- B-tree → optimized for disk
### 16. MEMORY LINES

- Dense → speed
- Sparse → space
- Secondary → dense compulsory
- Root split → height change
- All leaves same level → balanced
---
## CS2001 – Week 9, Lecture 2
### 1. CONTEXT
#### Recap
- Indexing improves search performance
- 2-3-4 trees ensure balance
#### Limitation
- Not scalable for disk-based systems
#### Goal
- Efficient disk-based structure
- Fast search, insert, delete

### 2. INTRO TO B+ TREE
#### Definition
B+ Tree is a balanced multi-level search tree:
- Extension of 2-3-4 tree
- Used in database indexing
- Optimized for disk systems
#### Key Insight
- All leaves are at the same depth

### 3. STRUCTURE OF B+ TREE
#### Internal Nodes
- Store keys and pointers to child nodes
#### Leaf Nodes
- Store keys
- Store pointers to actual records
- Contain pointer to next leaf node
#### Key Property
- Leaf nodes are linked for sequential access

### 4. CORE PROPERTIES
#### Balance
- All root-to-leaf paths have equal length
#### Node Capacity
Let n = maximum number of keys
- Internal nodes: [n/2, n]
- Leaf nodes: [n/2, n]
#### Exception
- Root can have fewer entries
#### Key Insight
- Every node is at least half full

### 5. TRADE-OFF IN NODE SIZE
#### More Keys per Node
- Smaller height
- More comparisons per node
#### Fewer Keys per Node
- Faster node-level search
- Larger height
#### Insight
- Optimal fan-out is required

### 6. SEARCH IN B+ TREE
#### Process
1. Start at root
2. Compare sequentially with keys
3. Follow appropriate pointer
4. Repeat until leaf node
5. Search inside leaf
#### Key Insight
- Search always terminates at leaf

### 7. INSERTION IN B+ TREE
#### Step 1
- Locate correct leaf node
#### Step 2
- Insert key in sorted order
#### Case 1: Node Not Full
- Insert directly
#### Case 2: Node Full
- Split required

### 8. SPLITTING
#### Leaf Split
- Divide keys into two halves
- Create new leaf node
- Smallest key of new node goes to parent
#### Internal Node Split
- Split node into two
- Push middle key upward
#### Propagation
- May continue up to root

### 9. ROOT SPLIT
#### Condition
- Root becomes full and splits
#### Result
- New root created
- Height increases by 1
#### Key Insight
- Height increases only via root split

### 10. DELETION IN B+ TREE

#### Step 1
- Locate key in leaf node
#### Step 2
- Delete key
#### Underflow Condition
- Node has fewer than n/2 keys
#### Resolution
- Borrow from sibling OR
- Merge nodes
#### Result
- Height may decrease

### 11. PERFORMANCE ANALYSIS
#### Height
- O(log base fan-out n)
#### Example
- n ≈ 100
- 1 million keys
- Height ≈ 4
#### Comparison
- BST → ~20 levels
- B+ Tree → ~4 levels
#### Key Insight
- Minimizes disk access

### 12. ADVANTAGES
#### Properties
- Always balanced
- Efficient disk I/O
- Supports range queries
- Sequential traversal via leaf links
- Self-organizing

### 13. DISADVANTAGES
#### Costs
- Extra insertion overhead
- Extra deletion overhead
- Additional storage for pointers

### 14. HANDLING DUPLICATES
#### Problem
- Multiple records with same key
#### Solutions
- Use bucket of pointers
- Store list of record pointers
- Append record ID to key
#### Insight
- Unique keys simplify structure

### 15. POINTER ISSUES
#### Problem
- Record relocation invalidates pointers
#### Solution
- Use primary key instead of direct pointer
#### Trade-off
- Extra lookup cost
- Easier maintenance

### 16. STRING INDEXING
#### Problem
- Variable length keys
#### Solution
- Prefix compression
#### Example
- "Silberschatz" → "Silb"

### 17. B+ TREE AS MULTILEVEL INDEX
#### Observation
- Upper levels behave like sparse index
- Lower levels behave like dense index
#### Insight
- Hierarchical indexing structure

### 18. INTRO TO B-TREE
#### Definition
- Variant of B+ Tree without key duplication
#### Key Difference
- Keys stored only once
- Data can appear in internal nodes

### 19. B-TREE PROPERTIES
#### Characteristics
- No repeated keys
- Records may be found before leaf
- Internal nodes store data pointers

### 20. B-TREE VS B+ TREE
#### B+ Tree
- Better for range queries
- Higher fan-out
- Lower height
- Simpler
#### B-Tree
- May find earlier
- Lower fan-out
- More complex
#### Key Insight
- B+ Trees preferred in databases

### 21. FINAL TAKEAWAYS
#### Mental Model
- B+ Tree = disk-optimized balanced index
#### Core Strength
- Reduces disk I/O drastically

### 22. MEMORY LINES
#### Key Reminders
- B+ Tree → data at leaf
- High fan-out → low height
- Split → upward propagation
- Merge → during deletion
- Disk I/O dominates performance
---
