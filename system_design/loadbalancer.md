## Load Balancer
Load balancers distribute incoming client requests to computing resources such as application server and databases. In each case load balancer returns the resourse from the computing resource to the appropriate client.  
Load balancer are effective at:
- Preventing requests from going to unhealthy servers.
- Preventing overloading resources
- Helping to eliminate a sigle point of failure.

Load balancers can be implemented with hardware(expensive) or with software such as HAProxy.  
Additional benifits include:
- **SSL termination** - Decrypt incoming requests to encrypt server responsed to backend servers do not have to perform these potentially expensive operations
   - Removes the need to install X.509 certificates on each server
- **Session persistence** - Issue cookies and route a specific clients request to same instance if the web apps do not keep track of sessions.


To protect against failure, it's common to set up multiple load balacers, either in active-passvie or active-active mode.  
**Type of load balanceer routing policy**
- Random
- Least loaded
- Session/Cookies
- Round robin or wrighted round robin
- Layer 4
- Layer 7

#### Horizonatal scaling
Load balancer can also help with horizontal scaling, improving performace and availablity. Scaling out using commodity machines is more cost efficent and results in higher availability than scaling up a single server on more expensive hardware, called **Virtual Scalling**.  
Disdantage(s): horizontal scalling  
- Scaling horizontally introduces complexity and involves cloning servers.
  - Server should be stateless
  - Sessions can be stored in a centralized data store such as a db, redis
- Downstream servers such as caches and databases need to handle more simultaneous connections as upstream server scale out.

#### Disadvantage(s): Load balancer
- The load balancer can become a performace bottleneck if it does not have enough resources or if it is not configured properly.
- Introducing a laod balancer to help eliminate single point of failure results incresed complexity.

#### Round robin or wrighted round robin
