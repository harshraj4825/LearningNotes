## Consistency Patterns
With the copy of same data, we are faced with options on how to syschronize them so clinets have consistent view of data.  
From CAP theorem : Every read receives the most recent write or an error.  

1. Week Consistency
2. Eventual Consistency
3. Strong Consistency
<!-- Reset numbering -->
1. Week Consistency  
After write, reads may or may not see it. A best effort approach is taken.
This approch is seen in systems such as memecached. Week consistency works in real time use cases such as VoIP, video chat, and runtime multiplayer games.
For Example, If you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

2. Eventual Consistency  
After a write, read will eventually see it(typically within milliseconds). Data is replicated async.
This approach is seen in system such as DNS and email. Eventual consistency works well in high available systems.

3. Strong consistency  
After a write, read will see it. Data is replicated syschronously.
This approach is seen in file systems and RDBMS. Strong consistencey works well in systems that need transactions.

##### Notes from Google I/O 2009- Transaction across datacenters  
Multihoming (n): Operating from multiple data centers.  

**Why across datacenters** :  
- Catastrophic failiues
- Expected failures
- Routine maintenance
- Geolocality : CDNs, edge caching  

**Why dot across datacenters** :  
- Within a datacenter
  - High bandwidth: 1-100Gbps interconnects
  - Low latency: <1ms within rack, 1-5ms across
  - Little to no cost
- Between datacenters
  - Low bandwidth : 10Mbps-1Gbps
  - High Latency: 50-150ms
  - $$$ for fiber

**Multihoming**  
- Hard problem
- consistently ? Harder.
- with real time writes? Hardest/
- What to do?

Option 1: Don't  
- instead, bunkerize
- Bad at catastrophic failure
- No great for serving
Option 2 : Primary with hot failover(s)  
- Better but not ideal
  - Mefiocre at catastropbic failure
  - Window of lost data
  - Failover data may be inconsistent
- Amazon Web Services
- Banks, Brokerages, etc
- Geolocated for reads, not for writes  

Options 3: True multihoming  
- Simultaneous write in different DCs
- Two way: hard
- N way: harder
- Handle catastrophic failure, geolocallity
- but pay fro it in latency for fibers

#### Techniques and tradeoffs
![image](https://github.com/user-attachments/assets/92d139d8-39e9-4d74-9b4f-ab8dd49fc0ad)  
M/S - Master/Slave replication  
![image](https://github.com/user-attachments/assets/e01274ca-33cb-4fe9-bb03-843ce73a06e6)
Multi-master replication   
![image](https://github.com/user-attachments/assets/133b8cb5-bd32-47cf-9393-061cf43d8aa6)  
Two Phase Commit  
![image](https://github.com/user-attachments/assets/e45729c7-f806-445b-82a4-1aaa27aeae4b)  
Paxos  
![image](https://github.com/user-attachments/assets/cee3203c-e949-49d4-9c2c-540aa6469bc9)



