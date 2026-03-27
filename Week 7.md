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

---
## CS2001 – Week 7, Lecture 2
### 1. INTRODUCTION TO WEB APPLICATIONS
Focus:
→ Understanding the **Web fundamentals** behind applications
Goal:
- Understand how web works
- Learn communication between client and server
- Learn scripting concepts

### 2. WORLD WIDE WEB (WWW)
The Web is a:
- Distributed system
- Based on **hypertext**
#### Key Features:
- Documents are written in **HTML**
- Contains:
  - Text + formatting
  - Hyperlinks
  - Forms (user input)
#### Key Insight
> Web = interconnected documents + user interaction

### 3. URL (UNIFORM RESOURCE LOCATOR)
Used to **locate resources on the Web**
#### Structure of URL:
```
protocol://machine/path
```
#### Example:
```
http://www.google.com/search?q=dbms
```
#### Components:
- Protocol → `http`
- Machine → `www.google.com`
- Path → `/search?q=dbms`
#### Key Insight
> URL tells:
- **How to access**
- **Where to access**
- **What to access**

### 4. URI vs URL vs URN
- URI → General identifier
- URL → Location (address)
- URN → Name (identity)
#### Analogy:
- URN → Person’s name  
- URL → Person’s address  

### 5. HTML AND HTTP
#### HTML:
- Used for:
  - Formatting
  - Display
  - Input forms
#### HTTP:
- Communication protocol between:
  - Browser ↔ Server
#### Key Insight
> HTML = Structure  
> HTTP = Communication  

### 6. HTTP PROTOCOL (VERY IMPORTANT 🔴)
#### Property:
- **Connectionless**
#### Meaning:
- Request sent → Response received → Connection closed
#### Problem:
- No memory of previous requests
#### Example:
- Login → Server forgets next request user identity

### 7. SESSIONS AND COOKIES
#### Need:
Maintain user state across requests
#### Solution: Cookies
- Small data sent by server
- Stored in browser
- Sent back with every request
#### Session:
- Time period during which user is active
#### Key Insight 🔥
> HTTP is stateless  
> Cookies make it **stateful**

### 8. WEB BROWSER
#### Role:
- Fetch web pages
- Render HTML into UI
#### Functions:
- Takes URL input
- Sends HTTP request
- Displays response
#### Key Concept:
Rendering engine:
- Converts HTML → Visual output

### 9. WEB SERVER
#### Role:
- Accepts HTTP requests
- Sends responses
#### Functioning:
- Request received
- Processed (may involve DB)
- Response returned (HTML)
#### Special Case:
- Can execute programs (dynamic content)

### 10. WEB ARCHITECTURE
Flow:
User → Browser → Server → Database/File → Server → Browser
#### Key Insight
> Web architecture = Practical implementation of 3-tier architecture

### 11. SCRIPTING (CORE CONCEPT)
#### Definition:
- Scripts = small programs executed dynamically
#### Characteristics:
- Interpreted (not compiled separately)
- Embedded in web systems
- Used for dynamic behavior
#### Common Languages:
- JavaScript
- PHP
- JSP
- Python

### 12. TYPES OF SCRIPTING
#### 1. Client-Side Scripting
- Runs in browser
- Example: JavaScript
##### Features:
- Input validation
- UI updates
- Faster interaction
##### Advantage:
- Reduces server load
- Faster response
##### Limitation:
- Security restricted
#### 2. Server-Side Scripting
- Runs on server
##### Features:
- Database interaction
- Business logic
- Generates HTML
#### Key Insight 🔴
> Client-side → Speed  
> Server-side → Power  

### 13. JAVASCRIPT (CLIENT SIDE)
#### Uses:
- Input validation
- Modify page dynamically
- AJAX (no page reload)
#### Example:
- Validate form input before submission
#### Key Insight
> JavaScript makes web pages **interactive**

### 14. SERVER-SIDE SCRIPTING
#### Function:
- Connect frontend with database
#### Process:
- Receive request
- Execute logic
- Generate HTML
- Send response
#### Languages:
- JSP
- PHP
- Python

### 15. SERVLETS
##### Definition:
- Java-based server-side programs
#### Features:
- Handle requests
- Generate dynamic content
- Run on server
#### Working:
- Request → Servlet → DB → HTML → Response
#### Important:
- Each request handled as a thread

### 16. JSP (JAVA SERVER PAGES)
#### Concept:
- HTML + Embedded Java
#### Advantage:
- Easier than servlets
- Cleaner code
#### Key Insight
> JSP = Simplified Servlet

### 17. PHP
#### Features:
- Widely used scripting language
- Strong DB support
#### Use:
- Dynamic web pages
- Server-side processing

### 18. FINAL INSIGHTS
##### 1.
> Web apps = DB + Network + UI
##### 2.
> HTTP alone is stateless → Cookies fix it
##### 3.
> Scripts bring **dynamic behavior**
#### 4.
> 3-tier architecture becomes real through web systems

### 19. FINAL TAKEAWAY
You now understand:
- How web works internally
- How browser ↔ server communicate
- How applications become dynamic
#### Mental Model:
Browser = Interface  
Server = Processor  
Database = Storage  

---
