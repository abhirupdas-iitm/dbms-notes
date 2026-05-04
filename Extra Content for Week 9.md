## CS2001 – Week 9, Extra Lecture 1
### 1. INTRODUCTION TO B+ TREE
Goal:
→ Understand structure and properties of B+ Trees  
#### Focus:
- Node structure  
- Key-pointer relationship  
- Tree organization  
#### Key Insight
> B+ Tree is used for efficient indexing in DBMS

### 2. BASIC STRUCTURE
#### Components:
- Keys  
- Record Pointers  
- Child Pointers  

#### Node contains:
- Key values  
- Pointer to records  
- Pointer to child nodes  

#### Key Insight
> Each key is associated with a record pointer

### 3. ORDER OF B+ TREE
#### Definition:
- Maximum number of children a node can have  

#### Property:
``Max children = m``  
``Max keys = m - 1``  

#### Key Insight
> Order determines capacity of nodes

### 4. CHILD POINTERS
#### Definition:
- Links to child nodes  

#### Properties:
- Internal nodes store child pointers  
- Leaf nodes store data pointers  

#### Key Insight
> Internal nodes guide search, leaf nodes store actual data

### 5. INTERNAL VS LEAF NODES
#### Internal Node:
- Contains keys  
- Contains child pointers  
- Does NOT store actual data  

#### Leaf Node:
- Contains keys  
- Contains record pointers  
- Stores actual data  

#### Key Insight
> Data exists only at leaf level

### 6. SEARCH PROCESS
#### Steps:
1. Start at root  
2. Compare key values  
3. Follow appropriate child pointer  
4. Reach leaf node  
5. Retrieve data  

#### Key Insight
> Search always ends at leaf node

### 7. NODE CAPACITY
#### Maximum:
``Max children = m``  
``Max keys = m - 1``  

#### Minimum:
``Min children ≈ ⌈m/2⌉``  

#### Key Insight
> Nodes must remain balanced

### 8. BALANCED TREE PROPERTY
- All leaf nodes are at same level  
- Tree height is minimal  

#### Key Insight
> Balanced structure ensures fast access

### 9. INSERTION IDEA
#### Steps:
1. Insert in leaf node  
2. If overflow:
   - Split node  
   - Promote middle key  
3. Adjust parent  

#### Key Insight
> Splitting maintains balance

### 10. POINTER ORGANIZATION
- Left side → smaller values  
- Right side → larger values  

#### Key Insight
> Tree maintains sorted order

### 11. DATA ORGANIZATION
- Sequential storage at leaf level  
- Efficient for range queries  

#### Key Insight
> B+ Tree supports ordered traversal

### 12. PRACTICAL OBSERVATIONS
- High fan-out (many children)  
- Reduced tree height  
- Faster disk access  

#### Key Insight
> B+ Trees minimize disk I/O

### 13. COMMON CONFUSION
- Internal nodes ≠ data storage  
- Data only in leaf nodes  
- Keys guide navigation  

### 14. FINAL TAKEAWAY
You now understand:
- Structure of B+ Trees  
- Node composition  
- Search process  
- Tree properties  

#### Mental Model
Root → Internal Nodes → Leaf → Data

---
## CS2001 – Week 9, Extra Lecture 2
### 1. INTRODUCTION
Goal:
→ Understand construction of B+ Tree  
→ Learn insertion process  
#### Focus:
- Internal node structure  
- Leaf node behavior  
- Splitting logic  
#### Key Insight
> Construction of B+ Tree ensures balance and efficiency :contentReference[oaicite:0]{index=0}

### 2. BASIC RULES OF B+ TREE
#### Order (m):
``Max children = m``  
``Max keys = m - 1``  

#### Properties:
- Keys stored in sorted order  
- All leaves at same level  
- High fan-out  

#### Key Insight
> Order defines structure and limits

### 3. INTERNAL NODE STRUCTURE
Contains:
- Keys  
- Child pointers  

#### Properties:
- Guides search path  
- Does NOT store actual records  

#### Key Insight
> Internal nodes act as routing nodes

### 4. LEAF NODE STRUCTURE
Contains:
- Keys  
- Record pointers  

#### Properties:
- Stores actual data  
- Linked sequentially  

#### Key Insight
> Leaf nodes hold complete data access

### 5. INSERTION PROCESS
#### Step 1:
Insert key in leaf node  

#### Step 2:
Maintain sorted order  

#### Step 3:
If node has space → DONE  

#### Key Insight
> Always insert at leaf first

### 6. OVERFLOW CONDITION
Occurs when:
``Number of keys > m - 1``  

#### Action:
- Split node  
- Divide keys into two nodes  

#### Key Insight
> Overflow triggers structural change

### 7. NODE SPLITTING
#### Steps:
1. Divide keys into two halves  
2. Create new node  
3. Move half keys  

#### Promotion:
- Middle key goes to parent  

#### Key Insight
> Splitting maintains balance

### 8. ROOT SPLIT
If root overflows:
- Create new root  
- Increase tree height  

#### Key Insight
> Only root split increases height

### 9. INSERTION EXAMPLE IDEA
#### Process:
- Start with empty tree  
- Insert values sequentially  
- Split when capacity exceeded  

#### Key Insight
> Tree grows upward via splits

### 10. POINTER DISTRIBUTION
- Left child → smaller keys  
- Right child → larger keys  

#### Key Insight
> Maintains sorted traversal

### 11. TREE GROWTH
- Controlled via splits  
- Height remains low  

#### Key Insight
> High branching factor reduces height

### 12. PERFORMANCE ADVANTAGE
- Fewer disk accesses  
- Efficient search  
- Balanced structure  

#### Key Insight
> B+ Tree optimizes disk-based indexing

### 13. COMMON MISTAKES
- Inserting in internal nodes directly  
- Ignoring sorted order  
- Incorrect split handling  

### 14. FINAL TAKEAWAY
You now understand:
- Construction rules  
- Insertion steps  
- Overflow handling  
- Splitting mechanism  

#### Mental Model
Insert → Check Overflow → Split → Promote → Balance

---
