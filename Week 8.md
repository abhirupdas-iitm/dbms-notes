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
