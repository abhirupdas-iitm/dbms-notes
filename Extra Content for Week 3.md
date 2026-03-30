## CS2001 – Week 3, Extra Lecture 1
### 1. INTRODUCTION
Focus:
→ Understanding **Triggers in DBMS**  
→ Trade-off between **Functionality vs Performance**
#### Goal
> Know when to use triggers — and more importantly, when NOT to

### 2. WHAT ARE TRIGGERS
#### Definition:
Triggers are **automatic procedures** that execute:
- On INSERT  
- On UPDATE  
- On DELETE  
#### Key Insight
> Triggers run **automatically** — not manually

### 3. FUNCTIONALITY vs PERFORMANCE
#### Functionality:
- Automates tasks  
- Enforces rules  
- Reduces manual effort  
#### Performance:
- Can slow down system  
- Adds overhead  
- Hard to control execution  
#### Key Insight
> More automation ≠ better system

### CASE STUDY 1
### 4. SCENARIO
Organization wants to:
- Identify employees eligible for **vaccination reimbursement**
#### Conditions:
- Vaccinated  
- Salary < 35,000  
- Age > 50  
- Lives in containment zone  
#### Tables:
- Employee_Professional  
- Employee_Personal  
- Containment_zones  
- Vaccination  

### 5. TRIGGER LOGIC
- When a row is inserted into **Vaccination**
- AFTER INSERT trigger executes  
#### Task:
- Check conditions  
- Join 3 tables  
- Copy eligible employee data  

### 6. PROBLEM
- Trigger runs for **every insert**
- Even if employee is NOT eligible  
#### Result:
- Every insert → 3-table JOIN  
- High computation cost  
#### Impact:
- Reduced throughput  
- Poor system performance  

### 7. CONCLUSION
> Triggers should be used only for **simple operations**
#### Important Rule
>Avoid complex joins inside triggers  

### CASE STUDY 2
### 8. SCENARIO
- Bank sends email when KYC is updated  
#### Trigger:
- AFTER UPDATE trigger sends email  

### 9. PROBLEM
- Clerk makes mistake  
- Corrects using ROLLBACK  
#### Issue:
- Email already sent  
- Cannot undo email  
#### Impact:
- Customer confusion  
- Inconsistent system behavior  

### 10. CONCLUSION
> External actions (email, files) cannot be rolled back  
#### Important Rule
>Avoid triggers for **external side effects**

###  CASE STUDY 3
### 11. SCENARIO
- Company gives vouchers to vaccinated employees + family  
#### Tables:
- Employee_details  
- Family  
- Vaccination  
- Voucher  

### 12. TRIGGER LOGIC
- Insert into Voucher  
- Automatically insert for family members  

### 13. PROBLEM
- If 2 family members are employees:
Trigger flow:
```
Employee A → triggers B  
Employee B → triggers A  
```
#### Result:
- Infinite loop  
- Recursive inserts  
#### Impact:
- System crash  
- Uncontrolled execution  

### 14. CONCLUSION
> Triggers can cause **infinite recursion**
#### Important Rule
> Always consider **chain reactions**

### FINAL INSIGHTS
### 15. CORE PROBLEMS WITH TRIGGERS
- Hidden execution  
- Performance overhead  
- Difficult debugging  
- Risk of recursion  
- External inconsistency  

### 16. WHEN TO USE TRIGGERS
- Simple validation  
- Logging  
- Small automatic updates  

### 17. WHEN NOT TO USE

- Complex joins  
- External actions  
- Multi-table dependencies  
- Recursive scenarios  
#### BIG PICTURE
Triggers are:
- Powerful  
- Dangerous  
#### Key Insight
> Triggers are like automation without visibility

####  FINAL TAKEAWAY
You now understand:
- How triggers work  
- Why they can fail  
- How to use them safely  
#### Mental Model
Trigger = Automatic reaction  
Good → small, controlled  
Bad → complex, unpredictable  

---