## CS2001 – Week 2, Extra Lecture 1
### 1. INTRODUCTION
This lecture covers:
- Binary number system  
- Conversion (Binary ↔ Decimal)  
- Character representation basics  
- Binary operations  
#### Goal
> Understand how computers represent and process data using binary  

### 2. BINARY NUMBER SYSTEM
#### Definition:
Binary is a number system with **base = 2**
#### Digits:
- 0  
- 1  
#### Comparison:
- Decimal → Base 10 → digits (0–9)  
- Binary → Base 2 → digits (0, 1)  
#### Key Insight
> Binary uses only two states → perfect for computers

### 3. WHY BINARY IS USED
#### 1. Electronic Representation
- ON → 1  
- OFF → 0  
#### 2. Hardware Compatibility
- Computers use switches (transistors)
- Switches have only 2 states
#### 3. Logical Operations
- TRUE / FALSE  
- YES / NO  
#### Key Insight
> Binary matches BOTH:
- Hardware behavior  
- Logical operations  
#### 4. BASIC UNITS
##### Bit:
- Smallest unit  
- 0 or 1  
##### Byte:
- 8 bits = 1 byte  
#### Key Insight
> All data in computers = sequence of bits


### 5. NUMBER OF VALUES (VERY IMPORTANT 🔴)
#### Rule:
For **n bits**:
```
Total values = 2ⁿ
```
#### Example:
- 1 bit → 2 values  
- 2 bits → 4 values  
- 3 bits → 8 values  
#### Range:
```
0 to (2ⁿ − 1)
```
#### Key Insight
> n bits can represent numbers from 0 to (2ⁿ − 1)

### 6. BINARY COUNTING
Example (3 bits):
```
000 → 0  
001 → 1  
010 → 2  
011 → 3  
100 → 4  
101 → 5  
110 → 6  
111 → 7  
```
#### Key Insight
> Binary counting follows same logic as decimal, but base = 2

### 7. DECIMAL → BINARY (INTEGER)
#### Method:
1. Divide number by 2  
2. Store remainder  
3. Repeat until quotient = 0  
4. Write remainders **bottom → top**
#### Example:
Convert 1729:
```
1729 ÷ 2 → remainder  
Repeat until quotient = 0
```
#### Final Answer:
Binary = remainders (bottom → top)
#### Key Insight
> Order of remainders is CRITICAL

### 8. DECIMAL → BINARY (FRACTION)
#### Method:
1. Multiply fractional part by 2  
2. Extract integer part  
3. Repeat with new fractional part  
4. Stop when:
   - Fraction = 0 OR  
   - Desired precision reached  
#### Example:
0.718 → multiply repeatedly by 2  
#### Result:
Binary fraction = collected integer parts (top → bottom)
#### Key Insight
> Fraction conversion may be **approximate**

### 9. COMPLETE CONVERSION
Example:
```
2.718 (decimal)
```
#### Steps:
- Convert integer part → 2 → 10  
- Convert fractional part separately  
#### Final:
```
2.718 ≈ 10.101101...
```
#### Key Insight
> Integer + Fraction handled separately

### 10. BINARY → DECIMAL (INTEGER)
#### Method:
1. Assign powers of 2 (right → left)
2. Multiply digits
3. Add results
#### Example:
```
Binary → 1011
= 1×2³ + 0×2² + 1×2¹ + 1×2⁰
= 8 + 0 + 2 + 1 = 11
```
#### Key Insight
> Each position = power of 2

### 11. BINARY → DECIMAL (FRACTION)
#### Method:
- Use negative powers of 2  
#### Example:
```
0.101
= 1×2⁻¹ + 0×2⁻² + 1×2⁻³
= 0.5 + 0 + 0.125
= 0.625
```
#### Key Insight
> Fraction uses powers: 2⁻¹, 2⁻², 2⁻³...

### 12. PRECISION ISSUE
- Some decimal numbers cannot be exactly represented in binary  
- Leads to approximation  
#### Example:
0.718 → approximate binary  
#### Key Insight
> Computers often store **approximate values**

### 13. INTERESTING NOTES
- 2.718 → Euler’s number (e)  
- 1729 → Ramanujan’s famous number  

### 14. BIG PICTURE 🔴
Binary enables:
- Data representation  
- Arithmetic operations  
- Logical computation  

### 15. FINAL TAKEAWAY
You now understand:
- Why binary is used  
- How data is stored  
- How conversions work  
#### Mental Model
Binary = Language of computers  
Bits = Letters  
Numbers = Meaning  

---
## CS2001 – Week 2, Extra Lecture 2
### 1. INTRODUCTION
Till now:
- Binary numbers  
- Number representation  
Now:
→ **Character representation + Boolean operations**
#### Goal
> Understand how computers represent text and perform logical operations  

### 2. CHARACTER ENCODING
#### Definition:
Character Encoding maps:
```
Character → Number → Binary
```
#### Storage:
- Stored as **binary bits in memory**
#### Key Insight
> Computers store characters as **numbers**, not symbols

### 3. ASCII (IMPORTANT)
#### Full Form:
American Standard Code for Information Interchange  
#### Features:
- Originally **7-bit**
- Represents **128 characters**
#### Extended ASCII:
- **8-bit**
- Represents **256 characters**
#### Common ASCII Ranges:
- Numbers (0–9) → 48–57  
- Uppercase (A–Z) → 65–90  
- Lowercase (a–z) → 97–122  
#### Example:
Character: `W`
- ASCII → 87  
- Binary → 1010111  
#### Storage:
- Stored as **1 byte (8 bits)**
- Extra bit added → padding  
#### Key Insight
> Every character = fixed binary pattern in memory  

### 4. UNICODE
#### Definition:
- Multilingual character encoding system  
#### Features:
- Supports many languages  
- Uses up to **16 bits (UTF-16)**  
#### Key Insight
> ASCII is limited → Unicode solves global language problem  

### 5. INTRO TO BOOLEAN ALGEBRA
#### Origin:
- Developed by **George Boole**  
#### Purpose:
- Solve logical problems mathematically  
#### Boolean Variable:
- Can take only:
  - 0 (False)  
  - 1 (True)  
#### Key Insight
> Boolean algebra = logic of computers  

### 6. BASIC BOOLEAN OPERATIONS
#### 1. AND ( . )
- Logical multiplication  
#### Rules:
```
0 . 0 = 0  
1 . 0 = 0  
0 . 1 = 0  
1 . 1 = 1  
```
#### Key Insight
> AND → both must be 1  
#### 2. OR ( + )
- Logical addition  
#### Rules:
```
0 + 0 = 0  
1 + 0 = 1  
0 + 1 = 1  
1 + 1 = 1  
```
#### Key Insight
> OR → at least one is 1  
#### 3. NOT ( ¬ )
- Logical negation  
#### Rules:
```
¬0 = 1  
¬1 = 0  
```
#### Key Insight
> NOT → flips the value  

### 7. DERIVED OPERATIONS
- XOR  
- NAND  
- NOR  
- XNOR  
#### Important:
> All can be derived using AND, OR, NOT  

### 8. XOR (IMPORTANT)
#### Definition:
```
A ^ B = A'B + AB'
```
#### Rules:
```
0 ^ 0 = 0  
1 ^ 0 = 1  
0 ^ 1 = 1  
1 ^ 1 = 0  
```
#### Key Insight
> XOR → true when inputs are different  

### 9. LOGIC GATES
- Physical implementation of Boolean operations  
#### Examples:
- AND gate  
- OR gate  
- NOT gate  
- XOR gate  
#### Key Insight
> Hardware = Boolean algebra in action  

### 10. WHY BOOLEAN OPERATIONS MATTER
Applications:
- Memory management  
- Error correction  
- Data recovery  
- Decision making  
#### Key Insight
> All computing = applying logic on binary  

### 11. ADVANCED NOTES
- Complex gates = combination of basic gates  
- Laws exist:
  - Associative  
  - Complementary  
  - De Morgan’s Laws  
#### Important:
> For this course → focus on basic operations  

### 12. BIG PICTURE
You now have:
- Binary → Data  
- Encoding → Meaning  
- Boolean → Processing  

### 13. FINAL TAKEAWAY
You now understand:
- How characters are stored  
- How logic is applied  
- How computation happens  
#### Mental Model
Binary = Language  
Encoding = Meaning  
Boolean = Thinking  

---
