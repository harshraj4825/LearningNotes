## Availability Pattern
Availability patterns are architectural strategies used in system design to ensure high availability (HA) by minimizing downtime and improving fault tolerance. These patterns help systems handle failures gracefully while maintaining continuous service.  

- Active-Passive(Standby) pattern
- Active-Active pattern
- Load balancing pattern
- Failover patter
- Circuit Breaker Pattern
- Retry and Timeout pattern
- Multi-resion deployment pattern


### Fail-over  
Failover is a mechanisum that ensure a system remains operational by automatically switching to a backup/redundant system when primary system fails.  
It is a critical aspect of high availability and fault tolerance in distributed systems.  
Systems use heartbeat mechanisms (e.g., pings, probes) to check if components are alive.  
#### Active-passive  
One system is active, while the backup remains idle until needed.

hot-standby: passive server is already running.  
Warm Standby: The passive system runs but takes some time to take over.
culd-standby: passive server needs to startup.  
Downtime is determinced by whether it hot or cold. Only active server handles the traffic.  
Active server failover also referred as master-slave failover.  
#### Active-active
In active-active, both server are serving traffic.  
If the server is public facing , the DNS would need to know about the public IPs of both servers. If the servers 
are internal facing, application logic need to know about both servers.  

Active-active failover also know as master-master failover.  
#### Disavatages: failover
- failover adds more hardware and additional complexity.
- There is potential for data loss if active system fails before any newly written date can be replicated to the passive.


## Availability in numbers
Availability is calculated as the percentage of time a system is operational and accessible over given periold.
**Availability=( Uptime/(Downtime+Uptime))×100**  
### Availability Levels(Nines concept)
High availability is often measured in "nines" (e.g., 99.9%(3's nine), 99.99%(4's nines)).  

|Availability|Downtime per Year|Downtime per month|Downtime per weel|
|-----------|--------|------------|-------------|
|99% (2 nines)|3.65 days|7.2 hrs|1.68 hrs|
|99.9% (3 nines)|8.76 hrs|43.2min|10.1min|
99.99% (4 nince)|52.6 mins|4.32 min|1.01min|

### Availability in parallel vs in sequence
If a service consists of multiple components prone to failure, the service's overall availability depends on whether the components are in sequence or in parallel.  
#### In sequence
Overall availability decreases when two components with availability < 100% are in sequence:  
```Availability (Total) = Availability (Foo) * Availability (Bar)```
#### In Parellel
Overall availability increases when two components with availability < 100% are in parallel:  
``` Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar)) ```   

## Availability Revist
Availability patterns are architectural strategies used in system design to ensure high availability (HA) by minimizing downtime and improving fault tolerance. These patterns help systems handle failures gracefully while maintaining continuous service.  

---

### **Key Availability Patterns**
#### **1. Active-Passive (Standby) Pattern**
   - **Concept**: A primary (active) system serves requests, while a secondary (passive) system remains on standby. If the primary system fails, the secondary system takes over.
   - **Example**:  
     - **Database Replication**: PostgreSQL with a standby replica.  
     - **Cloud HA**: AWS RDS Multi-AZ deployment.
   - **Pros**:  
     - Reliable failover mechanism.  
     - Reduces downtime.  
   - **Cons**:  
     - Delayed failover (switching takes time).  
     - Idle resources in the passive system.  

---

#### **2. Active-Active Pattern**
   - **Concept**: Multiple active nodes handle requests, balancing the load. If one node fails, traffic is redistributed to healthy nodes.
   - **Example**:  
     - Load-balanced microservices behind **AWS ELB, HAProxy, or NGINX**.  
     - **Kubernetes Pods** running across multiple nodes.  
   - **Pros**:  
     - No single point of failure (SPOF).  
     - Efficient resource utilization.  
   - **Cons**:  
     - More complex consistency management.  
     - Requires strong **synchronization and conflict resolution**.

---

#### **3. Load Balancing Pattern**
   - **Concept**: Distributes traffic across multiple instances to prevent overloading and ensure availability.
   - **Example**:  
     - **Round-robin, Least Connections, or Weighted Load Balancing** with NGINX, HAProxy, or AWS ALB.  
   - **Pros**:  
     - Reduces downtime due to overloading.  
     - Improves scalability.  
   - **Cons**:  
     - Requires **session stickiness** for stateful applications.  
     - If the load balancer fails, traffic routing stops.

---

#### **4. Failover Pattern**
   - **Concept**: Automatic switching to a backup system when the primary system fails.
   - **Example**:  
     - DNS failover using **Route 53 health checks**.  
     - Multi-region deployment in **AWS, GCP, or Azure**.  
   - **Pros**:  
     - Ensures system continuity.  
   - **Cons**:  
     - Failover switching time varies.  
     - Split-brain scenarios can occur.

---

#### **5. Circuit Breaker Pattern**
   - **Concept**: Prevents system overload by stopping calls to a failing service and retrying later.
   - **Example**:  
     - **Netflix Hystrix**, **Resilience4j** for handling service failures in microservices.  
   - **Pros**:  
     - Prevents cascading failures.  
   - **Cons**:  
     - Might block legitimate traffic during temporary failures.

---

#### **6. Retry and Timeout Pattern**
   - **Concept**: Retries failed requests with an exponential backoff strategy to avoid overwhelming the system.
   - **Example**:  
     - **AWS SDK retry mechanism**, **Spring Retry**.  
   - **Pros**:  
     - Improves resilience.  
   - **Cons**:  
     - Can increase latency if misconfigured.

---

#### **7. Multi-Region Deployment Pattern**
   - **Concept**: Deploys systems in multiple geographic regions to handle failures in one region.
   - **Example**:  
     - **AWS Global Accelerator, Azure Traffic Manager**.  
   - **Pros**:  
     - Reduces latency for global users.  
     - Increases fault tolerance.  
   - **Cons**:  
     - Expensive and requires complex synchronization.  

---
