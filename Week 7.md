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
#### 2. Unity (VERY IMPORTANT)
All applications share:
- Use of **RDBMS**
- Use of **SQL**
- Similar **architecture**

### 4. THREE-TIER ARCHITECTURE (CORE CONCEPT)
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

### 16. KEY INSIGHTS
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

### Notes taken from Activity Questions 7.1
1. 
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

### 6. HTTP PROTOCOL (VERY IMPORTANT)
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
#### Key Insight
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
#### Key Insight
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

### Notes taken from Activity Questions 7.2
1. 
---
## CS2001 – Week 7, Lecture 3
### 1. INTRODUCTION
Focus:
→ How **programming languages interact with databases**
#### Core Problem:
Application (Java/Python)  
→ Needs data  
→ Database understands only **SQL**
#### Key Question
> How do we connect **high-level programs ↔ SQL databases?**

### 2. OVERALL APPROACH
Applications use **APIs (Application Programming Interfaces)**
#### Tasks performed:
- Connect to database
- Send SQL queries
- Fetch results
- Close connection
#### Key Insight
> API acts as a **bridge between program and database**

### 3. TWO APPROACHES (VERY IMPORTANT)
#### 1. Connectionist Approach
- Uses APIs/drivers
#### 2. Embedded SQL Approach
- SQL written inside program
#### Key Insight
> Connectionist = External communication  
> Embedded = Internal integration  

### 4. CONNECTIONIST APPROACH
#### Concept:
Program ↔ API ↔ Database
#### Components:
- High-level language (Java, Python)
- SQL queries
- Connection library
#### Flow:
Program → API → SQL → Database → Result → Program

### 5. ODBC (OPEN DATABASE CONNECTIVITY)
#### Definition:
- Standard API for database access
#### Features:
- DBMS independent
- OS independent
- Portable
#### Functions:
- Open connection
- Execute queries
- Fetch results
#### Key Insight
> Write once → Run across multiple databases

### 6. ODBC WORKFLOW (PYTHON EXAMPLE)
Steps:
1. Connect to database
2. Create cursor
3. Execute SQL
4. Fetch results
#### Key Concept: Cursor
- Acts like **iterator/pointer**
- Traverses result rows
#### Flow:
- Execute query  
- Fetch one row at a time  
- Process  

### 7. JDBC (JAVA DATABASE CONNECTIVITY)
#### Definition:
- Java-specific database API
#### Features:
- Object-oriented
- Platform independent
- Exception handling
#### Workflow:
1. Establish connection
2. Create Statement object
3. Execute query
4. Process ResultSet
#### Key Insight
> Statement = handle to communicate with DB  
> `ResultSet` = table returned from DB  

### 8. JDBC FLOW
```
Connection → Statement → Execute → ResultSet → Iterate
```
#### Result Handling:
- Use `.next()` to iterate rows
- Extract values using column names
#### Key Insight
> ResultSet behaves like a **table iterator**

### 9. BRIDGE DRIVERS
#### Problem:
- Different systems support different APIs
#### Solution:
Bridge drivers
#### Types:
- ODBC ↔ JDBC
- JDBC ↔ ODBC
- OLEDB ↔ ODBC
- ADO.NET ↔ ODBC
#### Key Insight
> Bridges ensure **interoperability**

### 10. EMBEDDED SQL APPROACH
#### Concept:
- SQL written directly inside program
#### Syntax:
```
EXEC SQL <SQL statement>
```
#### Key Idea:
- SQL becomes part of program code

### 11. HOST LANGUAGE & VARIABLES
#### Host Language:
- C, Java, Python, etc.
#### Variable Usage:
- Prefix with `:`
Example:
```
:credit_amount
```
#### Key Insight
> Host variables allow data exchange between:
Program ↔ SQL

### 12. CURSORS (VERY IMPORTANT)
#### Purpose:
- Handle multi-row query results
#### Steps:
1. Declare cursor
2. Open cursor
3. Fetch rows
4. Close cursor
#### Example:
```
DECLARE c CURSOR FOR SELECT ...
```
#### Flow:
```
OPEN → FETCH → PROCESS → CLOSE
```
### Key Insight
> Cursor = bridge for handling multiple tuples

### 13. FETCH OPERATION
#### Function:
- Retrieves one row at a time
#### Syntax:
```
FETCH c INTO :var1, :var2
```
#### Behavior:
- Repeated fetch → next row
- Ends when no more data

### 14. UPDATE USING CURSOR
#### Concept:
- Modify rows using cursor
#### Example:
```
WHERE CURRENT OF c
```
#### Use:
- Update specific row in iteration

### 15. EMBEDDED SQL FLOW
```
Connect → Declare → Open → Fetch → Process → Close
```

### 16. KEY DIFFERENCE

| Feature      | Connectionist   | Embedded SQL   |
| ------------ | --------------- | -------------- |
| SQL Location | Outside program | Inside program |
| Flexibility  | High            | Moderate       |
| Control      | API-based       | Language-based |

### 17. BIG PICTURE
Now full system is complete:
Frontend → Backend Logic → API → SQL → Database

### 18. FINAL INSIGHTS
#### 1.
> SQL alone is not enough → needs integration
#### 2.
> APIs make communication possible
#### 3.
> Cursors are essential for handling results
#### 4.
> Embedded SQL gives tighter integration

### 19. FINAL TAKEAWAY
You now understand:
- How programs talk to databases
- How SQL is executed from code
- How results flow back into applications
#### Mental Model:
Program = Brain  
API = Translator  
Database = Storage  

### Notes taken from Activity Questions 7.3
1. 
---
## CS2001 – Week 7, Lecture 4
### 1. INTRODUCTION
Focus:
→ Building **real applications using Python + PostgreSQL**
### Goal
> Move from theory → **actual working system**

### 2. OBJECTIVES
- Access PostgreSQL using Python
- Build a **web application**
- Integrate frontend + backend

### 3. BIG PICTURE
```
Frontend (HTML)
        ↓
Flask (Python backend)
        ↓
psycopg2 (API)
        ↓
PostgreSQL (Database)
```
#### Key Insight
> This is a **complete application pipeline**

### 4. PYTHON + POSTGRESQL
Python uses modules to interact with PostgreSQL.
#### Common Modules:
- psycopg2 (MOST IMPORTANT)
- pg8000
- PyGreSQL
- SQLAlchemy

### 5. WHY psycopg2?
- Most popular
- Stable
- Thread-safe
- Widely used in frameworks
#### Install:
```
pip install psycopg2
```

### 6. CORE WORKFLOW (VERY IMPORTANT)
From *diagram on page 8*:
Steps:
1. Create connection  
2. Create cursor  
3. Execute query  
4. Commit / rollback  
5. Close cursor  
6. Close connection  
#### Key Insight
> This is SAME pattern as ODBC/JDBC — just Python version

### 7. CONNECTION
```
psycopg2.connect(database, user, password, host, port)
```
#### Returns:
→ Connection object

### 8. CURSOR
```
conn.cursor()
```
#### Purpose:
- Executes SQL
- Fetches results
#### Key Insight
> Cursor = control handle for DB operations

### 9. EXECUTING SQL
```
cursor.execute(SQL, parameters)
```
#### Example:
```
INSERT INTO table VALUES (%s, %s)
```
#### Important
- `%s` = placeholder
- Prevents SQL injection

### 10. FETCH METHODS
- `fetchone()` → 1 row  
- `fetchmany()` → multiple rows  
- `fetchall()` → all rows  

### 11. COMMIT & ROLLBACK
```
conn.commit()
conn.rollback()
```
#### Meaning:
- Commit → save changes
- Rollback → undo changes
### Key Insight
> Without commit → changes NOT saved

### 12. FULL EXECUTION FLOW
```
Connect → Cursor → Execute → Fetch → Commit → Close
```

### 13. SQL OPERATIONS FROM PYTHON
#### CREATE TABLE
- Execute SQL using cursor
- Commit
#### INSERT
- Use parameterized query
- Check rowcount
#### DELETE
- Condition-based removal
- rowcount shows affected rows
#### UPDATE
- Modify existing rows
#### SELECT
- Fetch results into list
- Iterate and print
#### Key Insight
> All SQL operations follow SAME pattern

### 14. WEB DEVELOPMENT WITH PYTHON
Python supports frameworks:
- Django (large)
- Flask (lightweight)
- Pyramid
- Bottle

### 15. FLASK FRAMEWORK
#### Definition:
- Lightweight web framework
#### Features:
- Easy to start
- Flexible
- Scalable
- Uses templates
#### Install:
```
pip install Flask
```

### 16. SIMPLE FLASK APP
```
@app.route("/")
def hello():
    return "Hello World"
```
#### Run:
```
app.run()
```
#### Output:
- Runs server at `127.0.0.1:5000`
### Key Insight
> Flask handles web server logic automatically

### 17. ROUTING (VERY IMPORTANT)
```
@app.route("/path")
```
#### Meaning:
- URL → function mapping
#### Example:
- `/` → homepage  
- `/add` → add page  
- `/viewall` → view page  

### 18. TEMPLATE RENDERING
```
render_template("file.html")
```
#### Purpose:
- Converts HTML → browser view
#### Key Insight
> Flask reduces frontend effort significantly

### 19. FULL APPLICATION EXAMPLE
(Table: Candidate)
Columns:
- cno
- name
- email

### 20. FRONTEND (HTML)
#### index.html
- Home page
- Links:
  - Add Email
  - View Email
#### add.html
- Form:
  - `cno`
  - `name`
  - `email`
#### viewall.html
- Displays table data

### 21. BACKEND (FLASK)
#### ROUTE: HOME
```
@app.route("/")
```
→ Shows index page
#### ROUTE: ADD
```
@app.route("/add")
```
→ Shows form
#### ROUTE: SAVE DETAILS
```
@app.route("/savedetails", methods=["POST"])
```
#### Flow:
1. Get form data  
2. Connect DB  
3. Insert record  
4. Commit  
5. Show success page  
#### Key Insight
> Form → Python → SQL → Database

### 22. VIEW ALL DATA
```
@app.route("/viewall")
```
### Flow:
1. Execute SELECT  
2. Fetch all rows  
3. Pass to HTML  
4. Render table  
#### Key Insight
> Data flows back to frontend via templates

### 23. FINAL FLOW
```
User → Form → Flask → psycopg2 → PostgreSQL
                         ↓
                 Result → Flask → HTML → User
```

### 24. WHAT YOU JUST BUILT
- Full-stack mini application:
  - Frontend (HTML)
  - Backend (Python Flask)
  - Database (PostgreSQL)

### 25. FINAL INSIGHTS
#### 1.
> psycopg2 = Python DB connector
#### 2.
> Flask = Web interface builder
#### 3.
> Templates = bridge to UI
#### 4.
> Commit is critical

### 26. FINAL TAKEAWAY
You now understand:
- How real apps connect to DB
- How frontend interacts with backend
- How data flows end-to-end
#### Mental Model
HTML = Face  
Flask = Brain  
psycopg2 = Messenger  
Database = Memory  

### Notes taken from Activity Questions 7.4
1. 
---
## CS2001 – Week 7, Lecture 5
### 1. INTRODUCTION
This lecture focuses on:
- Rapid Application Development (RAD)
- Application Performance
- Application Security
- Mobile Applications
#### Goal
> Understand how real-world systems are built **fast, scalable, and secure**

### 2. RAPID APPLICATION DEVELOPMENT (RAD)
#### Definition:
RAD is an **agile development approach** that focuses on:
- Fast prototyping  
- Continuous feedback  
- Iterative improvement  
#### Key Idea
> Build → Test → Feedback → Improve (repeat)

### 3. WHY RAD?
Traditional model (Waterfall):
```
Requirements → Design → Implementation → Testing → Delivery
```
RAD model:
```
Small iterations + continuous feedback
```
#### Key Insight
> Customer is involved throughout (customer-in-loop)

### 4. RAD PHASES
1. Business Modeling  
2. Data Modeling  
3. Process Modeling  
4. Testing & Turnover  
#### Explanation:
##### 1. Business Modeling
- What problem are we solving?
##### 2. Data Modeling
- Entities, attributes, relationships
##### 3. Process Modeling
- Workflows (e.g., order → payment → delivery)
##### 4. Testing & Turnover
- Validate + deploy
#### Key Insight
> All phases happen **in parallel & iteratively**

### 5. RAD TECHNIQUES
To speed development:
- UI libraries
- Drag-and-drop IDEs
- Auto code generation
#### Examples:
- Java Server Faces (JSF)
- Ruby on Rails (CRUD automation)

### 6. RAD PLATFORMS
- Google App Engine  
- Microsoft Azure  
- AWS EC2  
- AWS Elastic Beanstalk  
#### Key Insight
> Industry EXPECTS you to know at least one platform

### 7. APPLICATION PERFORMANCE
#### Problem:
- Millions of users
- Thousands of requests per second
#### Solution: CACHING
#### Types of Caching:
##### 1. Server-Side
- Connection pooling  
- Query result caching  
- HTML caching  
##### 2. Client-Side
- Browser caching  
- Proxy caching  
#### Key Insight
> Avoid re-computation → reuse results
#### Important
Cached data can become **stale** (outdated)

### 8. APPLICATION SECURITY
#### 8.1 SQL INJECTION
##### Problem:
User input alters SQL query
Example:
```
Input: X' OR 'Y'='Y
```
#### Result:
```
SELECT * FROM table WHERE name='X' OR 'Y'='Y'
```
→ Always TRUE → security breach
#### Solution:
- Use parameterized queries
- Prepared statements
#### Key Insight
> NEVER directly concatenate user input into SQL
#### 8.2 PASSWORD SECURITY
#### Problems:
- Storing passwords in plain text
- Backup files leaking data
#### Solutions:
- Encrypt passwords
- Restrict file access
- Limit DB access by IP
#### Key Insight
> Security failure = system failure
#### 8.3 AUTHENTICATION
#### Weak Method:
- Password only
#### Strong Method:
- Two-Factor Authentication (2FA)
Examples:
- Password + OTP  
- Password + device token  
#### Key Insight
> Identity must be VERIFIED, not assumed
#### 8.4 AUTHORIZATION (VERY IMPORTANT)
#### Problem:
SQL supports:
- Table-level access  
- Column-level access  
BUT NOT:
- Row-level access  
#### Example:
> Student should see ONLY their grades
#### Issue:
- DB doesn’t know user identity  
- Cannot restrict per row  
#### Solution:
- Implement in application layer  
- Use views / filters  
#### Key Insight
> Authorization logic = application responsibility
#### 8.5 AUDIT TRAILS
##### Definition:
Logs of:
- Who did what  
- When  
- On which data  
#### Purpose:
- Detect attacks  
- Fix issues  
- Trace responsibility  
#### Required at:
- Database level  
- Application level  
#### Key Insight
> If you can't track it, you can't secure it

### 9. CHALLENGES IN WEB APPLICATIONS
- UI/UX complexity  
- Scalability  
- Performance  
- Security  
- Framework knowledge  

### 10. MOBILE APPLICATIONS
#### Definition:
Apps designed for:
- Smartphones  
- Tablets  
#### Constraints:
- Limited memory  
- Limited power  
- Limited bandwidth  
- Small screen  
#### Advantages:
- Sensors (accelerometer)  
- Touch interface  
- Mobility  
#### Key Insight
> Mobile ≠ Web (different constraints)

### 11. MOBILE vs WEB
##### Mobile Website:
- Runs in browser  
- Uses HTML  
- Needs internet  
##### Mobile App:
- Installed on device  
- Can work offline  
- Uses device features  

### 12. MOBILE ARCHITECTURE
From *diagram on page 22*:
#### Layers:
1. Presentation  
2. Business  
3. Data  
#### Data Layer Split:
- Local Data (fast)  
- Remote Data (large)  
#### Key Insight
> Mobile apps balance speed vs connectivity

### 13. TYPES OF MOBILE APPS
#### 1. Native Apps
- Platform-specific  
- High performance  
#### 2. Web Apps
- Browser-based  
- Cross-platform  
#### 3. Hybrid Apps
- Mix of both  
#### Key Insight
> Trade-off: performance vs portability

### 14. DESIGN CONSIDERATIONS
- Device type  
- Resources  
- Bandwidth  
- UI/UX  
- Navigation  
- Flow  

### 15. FINAL TAKEAWAY
You now understand:
- How applications are developed rapidly  
- How performance is optimized  
- How systems are secured  
- How mobile systems differ  
#### Mental Model
RAD = Speed  
Caching = Efficiency  
Security = Protection  
Mobile = Constraint-aware design  

### Notes taken from Activity Questions 7.5
1. 
---
