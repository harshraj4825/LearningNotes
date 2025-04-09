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

### Load Balancing Algorithms
#### Random 
Distribute the request evenly.
#### Round robin
Load balancer will still distribute requests equally. in cyclic way.
#### Weighted Round Robin
The weighted round robin is similar to the round robin in that the way request are assigned to the nodes is still cyclic, albeit with a twist. The node with the higher specs will be apportioned a greater number of requests.  
How would the load balancer know which node has higher capacity?
      You tell it beforeheand, and assign weights to each node.
      ![image](https://www.jscape.com/hubfs/images/weighted_round_robin.png)

#### Least Connections
Algorithm takes into consideration the number of current connections each server has. When a client attemps to connect, the load balancer will try to determine which server has the least number of connections and then assign the new connection to that server.
#### Weighted Least connections
It consider number of clients currently connected to each server.
#### Layer 4 load balancing
Layer 4 load balancers look at into at the transport layer to decide how to distribute requests. Generally, this involves the source, distination IP addresses, and ports in the header, but not the contents of the packet. Layer 4 load balancers forward network packets to and from the upstream, performing Network Address Translation (NAT).

#### Layer 7 load balancing
Layer 7 load balancers look at the application layer to decide how to distribute requests, This involve contents of the header, message, and cookies. Layer 7 load balancers terminate network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server. For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.  

At the cost of flexibility, layer 4 load balancing requires less time and computing resources than layer 7, although the performace impact can be minmal on modern commodity hardware.  
