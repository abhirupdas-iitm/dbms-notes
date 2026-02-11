#### Lecture 1

# CS2001 – Week 1, Lecture 1

## 1. Course prerequisites (desirable)

- Need basic background in C programming and algorithms.
- Sorting algorithms you are expected to know:
  - Merge sort
  - Quick sort
- Searching algorithms you are expected to know:
  - Linear search
  - Binary search
  - Interpolation search
- If these are weak, revise using MOOCs like:
  - “Design and Analysis of Algorithms”
  - “Introduction to Programming in C”

---

## 2. Course prerequisites (essential)

- Solid understanding of basic data structures is assumed:
  - Array
  - List
  - Binary Search Tree (BST)
  - Balanced tree idea
  - B-tree
  - Hash table / map
- Recommended revision source: algorithm / data-structure MOOCs (Design and Analysis, Fundamental Algorithms).

---

## 3. University database example

- Typical operations in a university database:
  - Add new students, instructors, and courses.
  - Register students for courses and generate class rosters.
  - Store grades, compute GPA, and generate transcripts.
- Historically, such applications were written directly on top of the file system (no DBMS layer).

---

## 4. Drawbacks of using file systems to store data

- **Data redundancy and inconsistency**
  - Same piece of information appears in multiple files and formats.
  - Updates may not be applied everywhere → inconsistent data.
- **Difficulty in accessing data**
  - For every new type of query, a new program has to be written.
- **Data isolation**
  - Data is spread over many files with different formats.
  - Hard to combine and process data from multiple files together.
- **Integrity problems**
  - Integrity constraints (e.g., account_balance > 0) are hidden inside program code.
  - Difficult to add new constraints or modify existing ones cleanly.

---

## 5. What is a Database Management System (DBMS)?

- A DBMS stores information about a particular enterprise (organization).
- It consists of:
  - A collection of interrelated data.
  - A set of programs to access and manipulate that data.
  - An environment that makes data access both convenient and efficient.
- Common database application areas:
  - Banking: transactions.
  - Airlines: reservations, schedules.
  - Universities: registration, grades.
  - Sales / online retail: customers, products, purchases, order tracking, recommendations.
  - Manufacturing: production, inventory, orders, supply chain.
  - Human resources: employee records, salaries, tax details.
- Databases can be very large and they appear in almost every aspect of modern life.


# CS2001 – Week 1, Lecture 2

## 1. History of database systems

### 1950s and early 1960s
- Data processing using magnetic tapes for storage.
- Tapes provided only sequential access.
- Punched cards used for input.

### Late 1960s and 1970s
- Hard disks allowed direct (random) access to data.
- Network and hierarchical data models became widespread.
- Ted Codd defines the relational data model.
  - Would win the ACM Turing Award for this work.
  - IBM Research begins System R prototype.
  - UC Berkeley begins Ingres prototype.
- High-performance (for the era) transaction processing.

### 1980s
- Research relational prototypes evolved into commercial systems → SQL becomes industrial standard.
- Parallel and distributed database systems.
- Object-oriented database systems.

### 1990s
- Large decision support and data-mining applications.
- Large multi-terabyte data warehouses.
- Emergence of Web commerce.

### Early 2000s
- XML and XQuery standards.
- Automated database administration.

### Later 2000s
- Giant data storage systems: Google BigTable, Yahoo PNuts, Amazon (implied).

---

## 2. Evolution of data models

**Timeline (oldest → newest):**

1. **Pioneering DBMS technologies** (1960s)
2. **The Relational Empire** (1970s-1980s)
3. **Multidimensional** (1990s)
4. **Graph** (2000s)
5. **NoSQL** (2000s onwards)

---

## 3. Why leave filesystems?

### Lack of efficiency in meeting growing needs

- As data scales up → operations take significantly more time.
- Spreadsheet files have upper limits on row count.
- Ensuring data consistency becomes a major challenge.
- No way to check constraint violations when multiple processes access data concurrently.
- Cannot give different permissions to different people in a centralized manner.
- System crash could be catastrophic.

**Bottom line:** These filesystem limitations motivated the need for a comprehensive, dedicated platform → **Database Management Systems**.

---

## 4. Spreadsheet files – a better solution?

**Spreadsheet software (e.g., Google Sheets)** was adopted by organizations dealing with large data because of disadvantages with book keeping.

**Advantages of spreadsheets:**

- **Durability:** Computer applications → data less prone to physical damage (vs. physical registers).
- **Scalability:** Easier to search, insert, modify records compared to book ledgers.
- **Security:** Can be password-protected.
- **Ease of Use:** Computer applications reduce manpower needed for routine computations.
- **Consistency:** Not guaranteed but spreadsheets are less prone to mistakes than registers.

**Limitation:** Mostly useful for single user or small enterprise applications.

---

## 5. Book keeping

**Historical context:** Shop owners maintained book registers to track:
- Amount received from customers.
- Amount due for any customer.
- Inventory details.
- And other account information.

**Problems with physical book-keeping:**

- **Durability:** Physical damage from rodents, humidity, wear and tear.
- **Scalability:** Very difficult to maintain over many years; some shops have numerous registers spanning years.
- **Security:** Susceptible to tampering by outsiders.
- **Retrieval:** Time-consuming process to search for a previous entry.
- **Consistency:** Prone to human errors.

**Note:** Not only small shops but large organizations also used to maintain transactions in book registers.

---

## 6. Electronic data management parameters

Managing electronic data or records depends on various parameters:

- **Durability:** Persistence without physical degradation.
- **Scalability:** Ability to handle growing data volumes.
- **Security:** Protection and access control.
- **Retrieval:** Speed and ease of finding records.
- **Ease of Use:** Intuitive interfaces and operations.
- **Consistency:** Data accuracy and integrity.
- **Efficiency:** Performance and resource optimization.
- **Cost:** Budget constraints for implementation and maintenance.
- *... (and others)*

---

## 7. Data management: Electronic

Electronic data/records management evolves with advances in technology → especially memory, storage, computing, and networking.

**1950s:** Computer programming started.

**1960s:** Data management with punch cards / tapes and magnetic tapes.

**1970s:**
- COBOL and CODASYL approach introduced in 1971.
- October 14, 1979 → Apple II shipped VisiCalc, marking the birth of the spreadsheet.
- Magnetic disks became prevalent.

**1980s:** RDBMS (Relational Database Management Systems) changed the face of data management.

**1990s:** Internet → data management started becoming global.

**2000s:** e-Commerce boomed; NoSQL introduced for unstructured data management.

**2010s:** Data Science started riding high.

---

## 8. Data management: Physical

Physical data or records management, more formally known as **Book Keeping**, has been using physical ledgers and journals for centuries.

**Historical milestones:**

- Most significant development: Henry Brown, an American inventor, patented a **"receptacle for storing and preserving papers"** on November 2, 1886.
- Herman Hollerith adapted the punch cards used for weaving looms to act as memory for a mechanical tabulating machine in 1890.

---

## 9. Management of data or records – general

Management of data or records is a basic need for human society:

- **Storage:** Preserving information.
- **Retrieval:** Finding information when needed.
- **Transaction:** Recording changes and updates.
- **Audit:** Tracking who did what and when.
- **Archival:** Long-term preservation.

**For:**
- Individuals
- Small / Big enterprises
- Global organizations

**Two major approaches historically:**
- **Physical:** Book keeping, ledgers (historical).
- **Electronic:** Computerized systems (modern).

---


# CS2001 – Week 1, Lecture 3  
## File Handling via Python vs DBMS

---

## 1. Case study: a banking transaction system

- Simple banking system where a user can:
  - Open a new account.
  - Transfer funds to an existing account.
  - View history of all transactions.
- Application checks:
  - If balance is not enough → block transfer.
  - If account numbers are invalid → show error and terminate transaction.
  - If transaction succeeds → print confirmation message.
- Used to compare:
  - File-based implementation (CSV / spreadsheets).
  - DBMS-based implementation (tables).

**Storage choices:**

- Account details:
  - `Accounts.csv` for file-based implementation.
  - `Accounts` table for DBMS implementation.
- Transaction details:
  - `Ledger.csv` file for file-based implementation.
  - `Ledger` table for DBMS implementation.

---

## 2. Costs and complexity

### File handling via Python

- File systems are cheaper to install and use.
- No specialized hardware, software, or personnel needed to maintain file systems.

### DBMS

- Large databases need dedicated database servers with large storage and processing power.
- DBMS software is expensive, must be installed and updated regularly.
- Databases are inherently complex and need specialized people (DBA) to manage them.
- Overall: high cost of implementation and maintenance.

---

## 3. Programmer’s productivity

### File handling via Python

- **Building the file handler:**
  - All constraints (within and across entities) must be enforced manually in code.
  - Effort to build such an application is large.
- **Maintenance:**
  - To maintain data consistency, the programmer must regularly check the sanity of data and relationships during inserts, updates, and deletes.
- **Handling huge data:**
  - As data grows beyond the file handler’s capacity, more manual code and effort are needed.

### DBMS

- **Configuring the database:**
  - Installation and configuration is the DBA’s specialized job, not the application programmer’s.
- **Maintenance:**
  - DBMS has built-in mechanisms to maintain consistency and sanity of data during insert / update / delete.
  - Programmer does not write these checks manually.
- **Handling huge data:**
  - DBMS can handle very large datasets (even terabytes); programmer does not have to worry about low-level scaling logic.

---

## 4. Persistence, robustness, security

### File handling via Python

- **Persistence:**
  - Data lives in in-memory structures during processing.
  - After updates, programmer must manually write data back to disk files.
- **Robustness:**
  - Ensuring consistency and reliability is manual, using multiple checks.
  - On a system crash, a partially done transaction can cause inconsistency or data loss.
- **Security:**
  - Very hard to implement fine-grained security in file systems.
  - Typically only OS-level authentication is available.

### DBMS

- **Persistence:**
  - Persistence ensured by automatic, system-level mechanisms (logging, commit, etc.).
  - Programmer does not worry about data loss due to manual mistakes.
- **Robustness:**
  - Backup, recovery, and restore need minimal manual intervention.
  - Recovery plans allow automatic recovery after crashes.
- **Security:**
  - User-specific access at database level.
  - Can restrict users to view-only or specific operations.

---

## 5. Scalability

### File handling via Python

- **Number of records:**
  - As number of records increases, flat-file efficiency drops:
    - More time spent searching for the right records.
    - OS limitations in handling huge files.
- **Structural change:**
  - To add an attribute:
    - Programmer must initialize the new attribute for every record (often with a default value) via code.
  - Hard to detect and maintain relationships between entities when attributes are added or removed.

### DBMS

- **Number of records:**
  - Databases are designed to scale as record count grows.
  - In-built mechanisms (e.g., indexing) support quick access to the right data.
- **Structural change:**
  - Adding an attribute column:
    - Can specify a default value; DBMS auto-initializes existing rows.
  - During deletion of attributes:
    - Constraints can prevent unsafe removal or enforce safe cleanup.

---

## 6. Parameter-wise comparison (summary)

- **Scalability w.r.t amount of data:**
  - File handling via Python: very difficult for insert, update, query at scale.
  - DBMS: in-built features for high scalability on large record sets.
- **Scalability w.r.t structure changes:**
  - Python files: extremely difficult to change structure (add/remove attributes).
  - DBMS: simple SQL commands to add/remove attributes.
- **Time of execution:**
  - Python files: operations often in seconds.
  - DBMS: typically in milliseconds.
- **Persistence:**
  - Python: temporary data structures must be manually flushed to files.
  - DBMS: automatic, system-induced persistence.
- **Robustness:**
  - Python: robustness ensured manually by programmer.
  - DBMS: backup/recovery mechanisms with minimal manual effort.
- **Security:**
  - Python: difficult to implement; mostly OS-level.
  - DBMS: user-specific database-level security.
- **Programmer’s productivity:**
  - Python: heavy coding effort for persistence, robustness, security.
  - DBMS: standard, simple queries reduce coding; improves throughput.
- **Arithmetic operations:**
  - Python: easy to implement arbitrary arithmetic in code.
  - DBMS: usually only a limited set of built-in arithmetic operations.
- **Costs:**
  - Python + files: low hardware/software/human costs.
  - DBMS: higher costs for hardware, software, and specialized staff.

---

## 7. Bank transaction: Python vs SQL (implementation glimpse)

> High-level idea only; exact code is not required for the notes.

### File-based Python implementation

- Opens CSV files:
  - `Accounts.csv` for accounts.
  - `Ledger.csv` for transaction log.
- Reads records using `csv.DictReader`, writes using `csv.DictWriter`.
- Steps:
  - Check sufficient balance for debit account.
  - Locate sender and receiver records by account number.
  - Update balances for debit and credit.
  - Append a ledger entry describing the transaction.
  - Rewrite updated records.
- Many manual steps:
  - Explicit loops over records.
  - Manual consistency handling.
  - Manual error handling and rollback logic.

### SQL / DBMS implementation

- Uses SQL block (transaction):
  - Read balance of sender account.
  - If balance < amount → raise notice “Insufficient balance”.
  - Else:
    - Update sender balance (debit).
    - Insert ledger entry for debit.
    - Update receiver balance (credit).
    - Insert ledger entry for credit.
  - Commit transaction.
- Most of the work (locking, atomicity, persistence) is handled by DBMS engine.

## 11. Data Manipulation Language (DML)

- Language for accessing and manipulating the data organized by the appropriate data model.
- **Two classes of query languages:**
  - **Procedural** = Relational algebra (focus on computational power and optimization).
  - **Non-procedural** = Tuple relational calculus (focus in this course).
- **Commercial** = used in commercial systems.
  - **SQL** is the most widely used commercial language.

---

## 12. SQL

- **SQL is NOT a Turing complete language** (equivalent to C programming language).
- Cannot be used to solve all problems that a C program, for example, can solve.
- **Higher-level language** for complex functions; SQL is usually embedded in some higher-level language.
- **Language extensions** for general access to embedded SQL through one of:
  - Application Programming Interface (API) (e.g., ODBC/JDBC) which allows SQL queries to be sent to database.

---

## 13. Data Definition Language (DDL)

- Specification notation for defining the database schema.
- **Example:**

```
create table Dept (  
dept_name varchar(20),  
building varchar(15),  
budget numeric(12,2)  
);
```

- DDL compiler generates a set of table templates stored in a **data dictionary**.
- **Data dictionary schema contains metadata** (that is, data about data).
- **Primary constraints** (ID uniquely identifies tuples).
- **Authorization** (Who can access what).

---

## 14. Relational model

- All data stored in tables in the relational model.
- **Example tabular data in relational model:**

| ID    | name       | salary | dept_name | budget |
| ----- | ---------- | ------ | --------- | ------ |
| 1223  | Watson     | 80000  | Physics   | 70000  |
| 3233  | Wu         | 90000  | Finance   | 50000  |
| 3231  | Franklin   | 60000  | Biology   | 80000  |
| 45565 | Katz       | 75000  | Comp.Sci. | 100000 |
| 98321 | Srinivasan | 65000  | Comp.Sci. | 100000 |
| 15151 | Brandt     | 92000  | Music     | 80000  |
| 76453 | Singh      | 87000  | Physics   | 120000 |

*(c) Instructor table*

---

## 15. Data models

- **Collection of tools** for describing:
- Data
- Data semantics
- **Relational semantics** (focus in this course).
- **Other data models:**
- Object-oriented and Object-relational.
- Network model or semi-structured relational model.
- **Converted to easily manageable unstructured data descriptors:**
- XML format.
- Content Addressable Storage (CAS) with metadata descriptors.
- RDBMS which support BLOBs.

---

## 16. Schema and instances

- **Physical data independence:** Ability to modify the physical schema without changing the logical schema.
- **Logical data independence:** Ability to modify the logical schema without changing the application programs.
- Applications depend on the logical schema.
- In general, changes in some parts do not seriously influence other components.

---

## 17. Schemas and instances (continued)

- **Instance:** Content of the database at a particular point in time.
- **Schema:** Analogue to the type of a variable at a particular point in time.

**Example customer instance:**

| name        | CustomerID | Account# | Adhaar ID | Mobile # |
| ----------- | ---------- | -------- | --------- | -------- |
| Pavan Laha  | 6728       | 91723    | 182708937 | 93010293 |
| Nand Prabhu | 6917       | 82713    | 18290429  | 78820928 |

**Account # | Account Type | Interest Rate | Min.Bal. | Balance**

| 37172 | Savings     | 4.0% | 5000 | 27912 |
| 82713 | Term Deposit| 6.75%| 10000| 10000 |

---

## 18. Schemas and instances (continued)

- **Schema:** Analogous to type of a variable and value of the variable at run-time in programming.
- **Logical schema:** Overall logical structure of the database.
- **Example:** Database consists of information about a set of customers and accounts in a bank.

| name        | CustomerID | Account# | Adhaar ID | Mobile # |
| ----------- | ---------- | -------- | --------- | -------- |
| Pavan Laha  | 6728       | 91723    | 182708937 | 93010293 |
| Nand Prabhu | 6917       | 82713    | 18290429  | 78820928 |

**Customer Schema | Account Schema**

| Account # | Account Type | Interest Rate | Min.Bal. | Balance |
|-----------|--------------|---------------|----------|---------|

- **Physical schema:** Overall physical structure of the database.

---

## 19. View of data

**An architecture for a database system:**

```
┌─────────────────────────────────┐  
│ view level │  
├─────────────────────────────────┤  
│ view 1 │ view 2 │ ... │ view n │  
└────────┼────────┼─────┼────────┘  
│ │ │  
▼ ▼ ▼  
┌─────────────┐  
│ logical │  
│ level │  
└─────────────┘  
│  
▼  
┌─────────────┐  
│ physical │  
│ level │  
└─────────────┘
```


---

# CS2001 – Week 1, Lecture 4
## 1. Levels of abstraction

- **Physical level:** Describes how data (for example, instructor) is actually stored.
- **Logical level:** Describes what data is recorded in the database, and the relationships among data.

```
type instructor = record  
ID: string;  
name: string;  
dept_name: string;  
salary: integer;  
end;
```

- **View level:** Application programs hide details of data types.
- Views can also hide information (such as an employee's salary) for security purposes.

---

## 2. Database design (2)

**Is there any problem with this relation?**

| ID    | name       | salary | dept_name | budget |
| ----- | ---------- | ------ | --------- | ------ |
| 1223  | Watson     | 80000  | Physics   | 70000  |
| 3233  | Wu         | 90000  | Finance   | 50000  |
| 3231  | Franklin   | 60000  | Biology   | 80000  |
| 45565 | Katz       | 75000  | Comp.Sci. | 100000 |
| 98321 | Srinivasan | 65000  | Comp.Sci. | 100000 |
| 15151 | Brandt     | 92000  | Music     | 80000  |
| 76453 | Singh      | 87000  | Physics   | 120000 |

---

## 3. Database design

**Logical design:** Deciding on the database schema.
- Database design requires that we find a **good collection of relation schemas**.
- Business decision: What attributes should we record in the database?
- Computer science decision: What relations should the attributes be distributed among?

**Physical design:** Deciding on the physical layout of the database.


# CS2001 – Week 1, Lecture 5 

## 1. Database architecture

The architecture of a database system is greatly influenced by the underlying computer system on which the database is running:

- Centralized
- Client-server (multi-processor)
- Parallel (multi-processor)
- Distributed
- Cloud

---

## 2. DBMS2 management

### Transaction management

- What if more than one user is concurrently updating the same data?
- **Transaction:** Collection of operations that performs a single logical function in a DBMS.
- **Transaction management component** ensures that the database remains in a consistent state despite system crashes (e.g., power failures) and operating system failures.
- **Concurrency control manager** controls the interaction among the concurrent transactions, to ensure the consistency of the database.

---

## 3. Query processing (2)

- **Equivalent ways of evaluating a given query.**
- **Difference between a good and a bad way of evaluating a query can be enormous.**
- Depends critically on **statistical information** about relations which the database must maintain.
- **Must estimate statistics** about relations and intermediate results to compute cost of complex expressions.

---

## 4. Query processing

```
a) Parsing and translation b) Optimization  
c) Evaluation

query ──→ [parser and translator] ──→ relational-algebra expression ──→ [optimizer] ──→ execution plan  
│ │  
└────────────── [evaluation engine] ───────────────┘  
│  
query output  
│  
[ data ] [ statistics about data ]
```


---

##
