## CS2001 – Week 8, Extra Lecture
### 1. INTRODUCTION TO MAGNETIC DISK
Magnetic Disk:
→ Secondary storage device  
→ Used for reading and writing data  
#### Characteristics:
- Bulk storage  
- Persistent data  
#### Key Insight
> Magnetic disk = primary secondary storage in DBMS

### 2. STRUCTURE OF MAGNETIC DISK
#### Components:
- Platters:
  - Circular disks  
  - Magnetic coating  
- Spindle:
  - Rotates platters  
- Read/Write Head:
  - Reads and writes data  
- Arm Assembly:
  - Moves heads  

#### Key Insight
> Each platter surface has its own read/write head

### 3. DISK ORGANIZATION
#### Tracks:
- Circular rings on platter  
#### Sectors:
- Division of tracks  
- Smallest unit of read/write  

``Sector size = 512 bytes``

#### Cylinder:
- Same track across all platters  

#### Key Insight
> Cylinder = aligned tracks across platters

### 4. DISK ACCESS MECHANISM
- Head moves inward/outward  
- All heads move together  
- Same track across platters accessed  

#### Key Insight
> Movement of arm determines access position

### 5. PERFORMANCE METRICS
#### 1. Capacity:
- Total storage size  

#### 2. Access Time:
Time from request → start of data transfer  

``Access Time = Seek Time + Rotational Latency``

#### Seek Time:
- Time to position head  

#### Rotational Latency:
- Time for sector to reach head  

#### 3. Data Transfer Rate:
- Speed of reading/writing  

#### 4. Reliability:
- Mean Time To Failure (MTTF)  

#### Key Insight
> Access time dominates performance

### 6. NUMERICAL 1 (CAPACITY)
#### Given:
- 5 double-sided platters  
- 50 tracks/surface  
- 32 sectors/track  
- 64 bytes/sector  

#### Steps:
``Total surfaces = 5 × 2 = 10``  
``Total tracks = 50 × 10 = 500``  
``Total sectors = 500 × 32 = 16000``  
``Capacity = 16000 × 64 bytes = 1024000 bytes``  

``1 KB = 1024 bytes``  
→ Capacity = 1000 KB  

#### Cylinders:
``Cylinders = tracks per surface = 50``

#### Key Insight
> Capacity = sectors × sector size

### 7. NUMERICAL 2 (ACCESS TIME)
#### Given:
``Seek Time = S ms``  
``Rotational Latency = R ms``  

#### Formula:
``Access Time = S + R``  

#### Key Insight
> Access time is additive

### 8. NUMERICAL 3 (TRANSFER RATE)
#### Given:
- 30000 RPM  
- 200 sectors/track  
- 512 bytes/sector  

#### Step 1: Time per rotation
``Time = 1 / 30000 min``  
``= 60 / 30000 sec = 2 ms``  

#### Step 2: Data per track
``Data = 200 × 512 = 102400 bytes = 100 KB``  

#### Step 3: Transfer Rate
``Transfer Rate = Data / Time``  
``= 100 KB / 2 ms = 50 KB/ms``  

#### Key Insight
> Transfer rate depends on rotation speed + data per track

### 9. BIG PICTURE
Magnetic Disk defines:
- Storage structure  
- Access cost  
- Performance limits  

#### Key Insight
> Disk performance directly impacts DB query speed

### 10. FINAL TAKEAWAY
You now understand:
- Disk structure (platters, tracks, sectors)  
- Access mechanism  
- Performance metrics  
- Numerical problem solving  

#### Mental Model
Structure → Movement → Access Time → Performance

---
