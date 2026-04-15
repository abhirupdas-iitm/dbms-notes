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