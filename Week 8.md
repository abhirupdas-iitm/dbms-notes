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
