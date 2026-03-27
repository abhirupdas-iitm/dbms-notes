## CS2001 – Week 7, Lecture 1
### 1. INTRODUCTION TO APPLICATION ARCHITECTURE
After designing databases, the next step is:
→ **Building applications that use these databases**
Goal:
- Efficient
- Scalable
- Secure
- Real-world usable systems

### 2. APPLICATION PROGRAMS
Applications exist across multiple domains:
- Financial (Banking, UPI, Trading)
- Travel (IRCTC, Airlines, Hotels)
- Communication (WhatsApp, Zoom)
- E-commerce (Amazon, Flipkart)
- Education (SWAYAM, Coursera)
- Health (Telemedicine, `CoWIN`)
- ERP Systems (Institutions, Hospitals)
#### Key Insight
Despite diversity:
> All applications are **data-intensive systems using DBMS**

### 3. CHARACTERISTICS OF APPLICATIONS
#### 1. Diversity
Applications differ in:
- Domain
- Scale
- Users
- Response time
#### 2. Unity (VERY IMPORTANT 🔴)
All applications share:
- Use of **RDBMS**
- Use of **SQL**
- Similar **architecture**

### 4. THREE-TIER ARCHITECTURE (CORE CONCEPT 🔥)
All major applications follow:
#### 1. Presentation Layer (Frontend)
- User Interface
- Browser / Mobile App
- Handles:
  - Input
  - Display
  - Interaction
#### 2. Business Logic Layer (Middle Layer)
- Core functionality
- Decision making
- Workflow handling
Examples:
- Authentication
- Payment processing
- Order management
#### 3. Data Access Layer (Backend)
- Database interaction
- Storage & retrieval
- Security
#### FLOW:
User → Frontend → Logic → Database → Logic → Frontend

### 5. PRESENTATION LAYER (MVC MODEL)
Uses **MVC Architecture**
#### Components:
##### 1. Model
- Represents data + partial logic
##### 2. View
- User interface (UI)
##### 3. Controller
- Handles input
- Connects View ↔ Model
#### Flow:
User → Controller → Model → View → User

### 6. BUSINESS LOGIC LAYER
#### Responsibilities:
- Implements **business rules**
- Controls workflows
- Processes user actions
#### Example Rule:
Student can enroll only if:
- Fees paid
- Prerequisites completed
#### Key Insight
> Database stores data  
> Business logic decides **what is allowed**

### 7. OBJECT-RELATIONAL MAPPING (ORM)
#### Problem:
- Business layer → Object-oriented
- Database → Relational
#### Solution:
**ORM maps objects ↔ tables**
Example:
- Java Class `Student` ↔ Table `Student`
#### Benefits:
- Easier coding
- Better abstraction
- Seamless data handling

### 8. DATA ACCESS LAYER
#### Role:
- Interface between logic and DB
Handles:
- SQL queries
- Data retrieval
- Data updates
#### Key Challenge:
- Bridging:
  - Programming languages (Java, Python)
  - SQL (Relational model)

### 9. ARCHITECTURE CLASSIFICATION
Based on tiers:
- 1-Tier
- 2-Tier
- 3-Tier
- n-Tier

### 10. ARCHITECTURE EVOLUTION
#### 1. Mainframe Era (1960–70)
- Centralized system
#### 2. PC Era (1980s)
- Local networks (LAN)
#### 3. Web/Mobile Era (1990s → present)
- Internet-based systems

### 11. 1-TIER ARCHITECTURE
#### Definition:
All components in **single system**
- UI
- Logic
- Database
#### Pros:
- Simple
#### Cons:
- Not scalable
- Not practical

### 12. 2-TIER ARCHITECTURE
#### Definition:
Client ↔ Server
- Client: UI + some logic
- Server: Database
#### Features:
- Direct communication
- No intermediate layer
#### Limitation:
- Poor scalability
- Weak separation of concerns

### 13. 3-TIER ARCHITECTURE (MOST IMPORTANT)

#### Structure:
- Presentation Layer
- Business Logic Layer
- Data Access Layer
#### Advantages:
- Scalability
- Security
- Maintainability
#### Fact:
> Most widely used architecture in real-world systems

### 14. N-TIER ARCHITECTURE
#### Definition:
Extension of 3-tier
- Multiple servers
- Distributed components
#### Purpose:
- Load balancing
- Scalability
- Performance optimization

### 15. SAMPLE APPLICATION BREAKDOWN
#### Example: Web Mail

| Layer         | Function                  |
| ------------- | ------------------------- |
| Presentation  | Login, Inbox, Compose     |
| Logic         | Authentication, SMTP/IMAP |
| Data          | Mail storage              |
| Functionality | Send/Receive mail         |

### 16. KEY INSIGHTS 🔥
#### 1.
> Database design ≠ application design
#### 2.
> Every real system =  
Frontend + Logic + Database
#### 3.
> Separation of concerns = scalability
#### 4.
> Business logic is the brain of the system

### 17. FINAL TAKEAWAY
You’ve now moved from:
Database Design → Application Systems
#### Mental Model:
Database = Storage  
Logic = Brain  
Frontend = Face  
