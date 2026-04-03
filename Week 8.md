## CS2001 – Week 8, Lecture 1
### 1. INTRODUCTION TO PHYSICAL DATABASE DESIGN
After understanding application architecture:
→ Focus shifts to **efficient storage and access of data**
Two major aspects:
- Logical Design (already covered)
- Physical Design (current focus)
Goal:
- Efficient storage
- Fast access
- Optimized performance

### 2. RECAP: LOGICAL VS PHYSICAL DESIGN
#### Logical Design
- Entities
- Relationships
- Constraints
- Abstract representation
#### Physical Design
- How data is stored on disk
- File structures
- Indexing mechanisms
#### Key Insight
> Logical = WHAT  
> Physical = HOW

### 3. NEED FOR PHYSICAL DESIGN
Why required?
- Large-scale data handling
- Performance optimization
- Efficient querying
#### Key Factors:
- Access time
- Storage space
- Data organization

### 4. ALGORITHMS VS PROGRAMS
#### Algorithm
- Finite sequence of steps
- Must terminate
- Solves a problem
#### Program
- Implementation of algorithm
- May or may not terminate
Examples:
- OS → never terminates
- DBMS → continuously running
#### Key Insight
> Algorithms → Always terminate  
> Programs → May run indefinitely

### 5. ANALYSIS OF ALGORITHMS
Core Questions:
- Why analyze?
- What to analyze?
- How to analyze?
- Where to analyze?

### 6. WHY ANALYZE?
Reasons:
- Limited resources
- Avoid performance issues
- Compare algorithms
Goals:
- Predict performance
- Provide guarantees
- Optimize systems

### 7. WHAT TO ANALYZE?
Focus on:
#### 1. Time Complexity
- Execution time
#### 2. Space Complexity
- Memory usage
Other factors:
- Power
- Bandwidth
- Processor usage
#### Key Insight
> In databases → Time & Space are critical

### 8. INPUT COMPLEXITY
Defined by:
- Size of input (n)
Examples:
- Number of elements
- Length of string
#### Key Idea
> Larger input → Higher cost

### 9. COUNTING MODEL
Approach:
- Identify key operation
- Count frequency
Example:
- Sum of n numbers → n additions
Time:
- T(n) = n
Space:
- Constant

### 10. ALGORITHM OPTIMIZATION INSIGHT
Example:
Searching in string
Naive:
- Recomputing length → O(n²)
Optimized:
- Store length once → O(n)
#### Key Insight
> Small changes → Huge performance gains

### 11. TIME VS SPACE TRADEOFF
Example:
Factorial
#### Recursive
- Time: O(n)
- Space: O(n)
#### Iterative
- Time: O(n)
- Space: O(1)
#### Key Insight
> Iteration saves memory

### 12. FUNCTION APPROXIMATION
Problem:
- Exact time depends on hardware
Solution:
→ Compare **growth rate**

### 13. BIG-O NOTATION
Used to represent:
- Growth of algorithm
Examples:
- O(1) → constant
- O(log n) → logarithmic
- O(n) → linear
- O(n log n) → efficient
- O(n²) → slow
- O(2ⁿ) → very slow
#### Key Insight
> Focus on dominant term

### 14. DOMINANT TERM RULE
Example:
T(n) = n² + n
→ Ignore smaller term
Final:
- O(n²)
#### Key Insight
> Highest power dominates

### 15. GROWTH COMPARISON
Order of efficiency:
- O(1) → best
- O(log n)
- O(n)
- O(n log n)
- O(n²)
- O(n³)
- O(2ⁿ) → worst

### 16. TYPES OF ANALYSIS
#### 1. Worst Case
- Maximum time
#### 2. Average Case
- Expected time
#### Key Insight
> Databases mostly consider worst-case

### 17. FINAL TAKEAWAY
You are now entering:
Database Systems → Performance Optimization
#### Mental Model:
Algorithm = Process  
Data Structure = Organization  
Complexity = Cost

---
## CS2001 – Week 8, Lecture 2
### 1. INTRODUCTION TO DATA STRUCTURES
Focus:
→ Data structures for **efficient storage and access**
Context:
- Used in physical database design
- Foundation for indexing and storage optimization
Definition:
- A data structure organizes and stores data in memory
- Enables efficient:
  - Access
  - Modification
#### Key Insight
> Data Structure = Storage + Operations

### 2. DATA STRUCTURE VS DATABASE
#### Data Structure
- In-memory
- Temporary
- Exists during program execution
#### Database
- Persistent storage
- Exists beyond program execution
#### Key Insight
> Data Structure → Temporary  
> Database → Permanent

### 3. CLASSIFICATION OF DATA STRUCTURES
Two types:
- Linear Data Structures
- Non-Linear Data Structures
Focus of this lecture:
→ Linear Data Structures

### 4. DESIGN PERSPECTIVE
A data structure consists of:
#### 1. Container
- Stores data
#### 2. Operations
- Create
- Insert
- Delete
- Search
- Close
#### Key Insight
> Efficiency depends on operations, not just storage

### 5. LINEAR DATA STRUCTURES
Definition:
- Elements arranged sequentially
Property:
- Given one element → next element is identifiable

### 6. TWO FUNDAMENTAL MEMORY MODELS
#### 1. Indexed (Sequential)
- Data stored in contiguous memory
- Access using index
- Random access possible
#### 2. Referential (Pointer-based)
- Data stored non-contiguously
- Each element stores address of next
- Access via pointers
#### Key Insight
> All data structures are built on:
- Indexing
- Referencing

### 7. TYPES OF LINEAR DATA STRUCTURES
- Array (Indexed)
- Linked List (Referential)
- Stack
- Queue

### 8. ARRAY
#### Properties:
- Contiguous memory
- Fixed size
- Random access
#### Complexity:
- Access → O(1)
- Insert → O(n)
- Delete → O(n)
#### Reason:
- Shifting elements required
#### Key Insight
> Fast access, slow modification

### 9. LINKED LIST
#### Properties:
- Non-contiguous memory
- Each node:
  - Data
  - Pointer
- Uses header node
#### Complexity:
- Access → O(n)
- Insert → O(1) (if position known)
- Delete → O(1) (if position known)
#### Key Insight
> Flexible size, slow access

### 10. ARRAY VS LINKED LIST

| Operation | Array | Linked List |
| --------- | ----- | ----------- |
| Access    | O(1)  | O(n)        |
| Insert    | O(n)  | O(1)        |
| Delete    | O(n)  | O(1)        |
#### Key Insight
> Trade-off between access and modification

### 11. STACK
Definition:
- Last In First Out (LIFO)
Operations:
- Push
- Pop
- Top
#### Key Insight
> Only top element accessible

### 12. QUEUE
Definition:
- First In First Out (FIFO)
Operations:
- Insert (Enqueue)
- Delete (Dequeue)
- Front
#### Key Insight
> Oldest element removed first

### 13. IMPORTANT NOTE
Stack and Queue:
- Defined by operations
- Not by storage
Can be implemented using:
- Array
- Linked List

### 14. SEARCHING
Two types:
#### 1. Linear Search
- Works on:
  - Array (ordered/unordered)
  - Linked list
- Complexity:
  - O(n)
#### 2. Binary Search
Condition:
- Data must be sorted
Process:
- Divide into halves
- Eliminate half each step
#### Complexity:
- O(log n)
#### Key Insight
> Divide and conquer

### 15. BINARY SEARCH LIMITATION
- Works only on arrays
- Requires random access
Cannot be used efficiently on:
- Linked lists
Reason:
- No direct access to middle element

### 16. SEARCH COMPARISON
#### Array
- Linear Search → O(n)
- Binary Search → O(log n) (if sorted)
#### Linked List
- Linear Search → O(n)
- Binary Search → Not efficient

### 17. INSERT & DELETE SUMMARY
#### Array
- Insert:
  - O(n) (ordered)
  - O(1) (unordered, at end)
- Delete:
  - O(n)
#### Linked List
- Insert → O(1)
- Delete → O(1)
(If position known)

### 18. FINAL INSIGHT
Linear data structures have:
- Efficient operations in some areas
- Inefficient in others
#### Problem:
> No structure supports fast:
- Search
- Insert
- Delete together
### 19. FINAL TAKEAWAY
You now understand:
- Arrays vs Linked Lists
- Stack and Queue fundamentals
- Search techniques
#### Mental Model:
Array → Fast access  
Linked List → Fast modification  
Binary Search → Fast search (with sorting)
Next step:
→ Non-linear data structures (to overcome limitations)

---
## CS2001 – Week 8, Lecture 3
### 1. INTRODUCTION TO NON-LINEAR DATA STRUCTURES
Focus:
→ Move beyond limitations of linear data structures
Goal:
- Improve:
  - Search
  - Insert
  - Delete performance

### 2. RECAP OF LINEAR DATA STRUCTURES
Observations:
- Space complexity → O(n)
- Trade-offs exist:
Array:
- Fast access
- Slow insert/delete
Linked List:
- Fast insert/delete
- Slow access/search
#### Key Insight
> No linear structure optimizes all operations

### 3. NEED FOR NON-LINEAR STRUCTURES
Problem:
- Cannot achieve efficient:
  - Search
  - Insert
  - Delete together
Solution:
→ Use hierarchical / network structures

### 4. NON-LINEAR DATA STRUCTURE
Definition:
- Data organized in non-sequential form
- Multiple relationships possible
Properties:
- Multiple paths between elements
- Hierarchical or graph-based structure

### 5. TYPES OF NON-LINEAR DATA STRUCTURES
- Graph
- Tree
- Hash Table
- Skip List (advanced)

### 6. GRAPH
Definition:
- Collection of:
  - Vertices (nodes)
  - Edges (connections)
Types:
- Directed / Undirected
- Weighted / Unweighted
- Cyclic / Acyclic
- Connected / Disconnected
Applications:
- Networks (electric, water)
- Social networks
- Knowledge graphs
- ER diagrams

### 7. TREE
Definition:
- Special type of graph
Properties:
- Connected
- Acyclic
Structure:
- Hierarchical
Types:
- Rooted / Unrooted
- Binary / n-ary
- Balanced / Unbalanced

### 8. TREE TERMINOLOGY
#### Root
- Node with no parent
#### Parent
- Predecessor node
#### Child
- Successor node
#### Leaf Node
- No children
#### Internal Node
- At least one child
#### Subtree
- Tree rooted at a node
#### Path
- Sequence of nodes
#### Siblings
- Same parent
#### Arity
- Number of children
#### Height
- Maximum level

### 9. TREE PROPERTIES
- Nodes = n
- Edges = n - 1
Binary Tree:
- Max nodes at level l → 2^l
- Max nodes in tree → 2^(h+1) - 1
Height bounds:
- Minimum → O(log n)
- Maximum → O(n)
#### Key Insight
> Balanced tree → log n height  
> Unbalanced tree → linear height

### 10. HASH TABLE
Concept:
- Use hash function
Process:
- Key → Hash function → Index
Storage:
- Array-based
#### Key Insight
> Fast access using computation
(Note: Detailed later)

### 11. BINARY SEARCH TREE (BST)
Goal:
- Combine:
  - Fast search (like binary search)
  - Efficient insert/delete (like linked list)

### 12. BST PROPERTY
For every node X:
- Left subtree → values < X
- Right subtree → values > X
Condition:
- Must hold for every node
#### Key Insight
> Ordering maintained at every node

### 13. BST CONSTRUCTION
Process:
- Insert elements one by one
- Compare and place:
  - Left if smaller
  - Right if larger
#### Key Insight
> Structure depends on insertion order

### 14. BST SEARCH
Process:
- Start at root
- Compare:
  - Equal → Found
  - Smaller → Go left
  - Larger → Go right
Repeat until:
- Found
- Or NULL reached

### 15. SEARCH COMPLEXITY
Depends on height (h)
- Best case → O(log n)
- Worst case → O(n)
#### Key Insight
> Performance depends on tree shape

### 16. INSERT & DELETE IN BST
Insert:
- Search position
- Insert node
Delete:
- Search node
- Adjust pointers
Complexity:
- O(h)
#### Key Insight
> Insert/Delete = Search + Adjustment

### 17. BALANCED VS UNBALANCED
#### Balanced Tree
- Height → O(log n)
- Efficient operations
#### Unbalanced Tree
- Height → O(n)
- Degrades to linked list

### 18. ADVANTAGE OF BST
If balanced:
- Search → O(log n)
- Insert → O(log n)
- Delete → O(log n)
#### Key Insight
> Achieves overall efficiency

### 19. LINEAR VS NON-LINEAR
#### Linear
- Sequential
- Single path
- Easier
#### Non-Linear
- Hierarchical
- Multiple paths
- More complex

### 20. FINAL TAKEAWAY
Non-linear structures solve:
- Trade-offs of linear structures
BST provides:
- Balanced efficiency (if maintained properly)
#### Mental Model:
Linear → Simple but limited  
Non-linear → Complex but powerful  
Next step:
→ Advanced trees (Red-Black, B-Tree)

---
## CS2001 – Week 8, Lecture 4
### 1. INTRODUCTION TO PHYSICAL STORAGE
Focus:
→ Move from in-memory structures to **persistent storage**
Requirement:
- Data must survive:
  - Program termination
  - Power failure
  - System crashes
#### Key Insight
> Databases require permanent storage

### 2. STORAGE REQUIREMENTS
Key needs:
- Large data volume
- Persistence
- Reliability
- Efficient access

### 3. CLASSIFICATION OF STORAGE
Two types:
#### 1. Volatile Storage
- Data lost on power failure
#### 2. Non-Volatile Storage
- Data persists

### 4. PERFORMANCE FACTORS
Storage evaluated based on:
- Speed
- Cost per unit data
- Reliability
#### Key Insight
> Trade-off between speed and cost

### 5. VOLATILE STORAGE
#### Cache
- Fastest memory
- Very expensive
- Very small
#### Main Memory (RAM)
- Fast access
- Larger than cache
- Still volatile
#### Key Insight
> Used for active computation only

### 6. FLASH MEMORY
Properties:
- Non-volatile
- Faster than disk
- Slower than RAM
Limitations:
- Limited write cycles
- Requires erase before rewrite
#### Key Insight
> Bridge between RAM and disk

### 7. MAGNETIC DISK
Main storage for databases
Properties:
- Non-volatile
- Large capacity
- Direct access
#### Key Insight
> Backbone of database storage

### 8. DISK ORGANIZATION
Components:
- Platters (disks)
- Spindle (rotation)
- Read/Write heads
#### Key Insight
> Data accessed via rotating disks

### 9. TRACKS AND SECTORS
#### Track
- Circular path on disk
#### Sector
- Subdivision of track
#### Block (Cluster)
- Group of sectors
#### Key Insight
> Block = unit of read/write

### 10. CYLINDER
Definition:
- Set of tracks aligned vertically across disks
#### Key Insight
> Same position across all platters

### 11. DISK ACCESS MECHANISM
Steps:
1. Move head to track → Seek
2. Wait for sector → Rotation
3. Read/write data

### 12. ACCESS TIME
Components:
#### Seek Time
- Time to locate track
#### Rotational Latency
- Time to locate sector
#### Key Insight
> Access time = Seek + Rotation

### 13. DATA TRANSFER RATE
Definition:
- Speed of data transfer
Factors:
- Disk speed
- Track position
#### Key Insight
> Outer tracks → faster transfer

### 14. RELIABILITY (MTTF)
Definition:
- Mean Time To Failure
Typical:
- Several years
#### Key Insight
> Lower failure probability is critical

### 15. OPTICAL STORAGE
Examples:
- CD
- DVD
- Blu-ray
Properties:
- Write once, read many
- Used for archival

### 16. MAGNETIC TAPE
Properties:
- Sequential access
- Very high capacity
- Low cost
Limitation:
- Slow access
#### Key Insight
> Best for backup and archival

### 17. STORAGE HIERARCHY
Order:
- Cache
- Main Memory
- Flash
- Magnetic Disk
- Optical Disk
- Tape
#### Key Insight
> Top → Fast, Expensive  
> Bottom → Slow, Cheap

### 18. DISK CONTROLLER
Function:
- Manages disk operations
- Controls:
  - Seek
  - Rotation
  - Read/Write
Ensures:
- Error detection
- Data integrity

### 19. CLOUD STORAGE
Examples:
- Google Drive
- Amazon Drive
- OneDrive
Advantages:
- Scalable
- Accessible anywhere
- Backup handled
#### Key Insight
> Growing trend in databases

### 20. FLASH DRIVES & SD CARDS
Properties:
- Portable
- Non-volatile
- Limited cycles
Usage:
- Small-scale storage

### 21. SOLID STATE DRIVE (SSD)
Properties:
- No moving parts
- Very fast
- Expensive
Comparison with HDD:
- Faster access
- Higher cost
#### Key Insight
> SSD replaces HDD in performance-critical systems

### 22. FUTURE STORAGE
#### DNA Storage
- Extremely high density
- Experimental
#### Quantum Storage
- Based on qubits
- Future technology

### 23. FINAL TAKEAWAY
You now understand:
- Storage types
- Disk structure
- Performance factors
#### Mental Model:
Memory → Speed  
Disk → Capacity  
Tape → Archival  
Next step:
→ Database storage structures and indexing

---
