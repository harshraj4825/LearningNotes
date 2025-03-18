## Step 1: [Scalability from Scalability Lecture at Harvard](https://www.youtube.com/watch?v=-W9F__D3oY4)  
- Virtical scaling
- Horizontal scaling
- Caching
- Load balancing
- Database replication
- Database partitioning
  
Q. What kind fo feature you are looking for or expecting minimally in a any web hosting company that you choose?  

- Accessibility  
- SFTP - secure file transfer, data encripted(username/password)  
- Unlimited bandwith, Unlimited storage  
- Shared hosting/VPS - Vitual Private Servers
  
**VPS** - Company takes superfast server with lots of RAM of CPU, lots of disk space and they chop it up into the illusion of multiple servers using Hypervisor.  
System Admin can acess your file etc. So you are not sucure.  
If you need complete privacy than you are probably going private own setup.  
**Amazon web services VPS (EC2)** 
Elastic Compute Cloud that essentially let you self-service and spawn as many virtual machines. You can automate the process of spawning more web servers more database servers if you happen to suddenly get popular even overnight.  

**Q. Suppose you website has been super populer and this website has maybe static web content HTML, files, gifs and like dynamic content like PHP code, database like mysql. How do you go about scaling your site so that it can handle more users well?**  
Straightforward approach: Virtical Scaling   
Get more resources like RAM, DISK space or equivalently money  
**Q Why is virtical scaling not necessatily a full solution? **  
Real world constraints: At some point you are either going to exhaust your own financial resources or just the state-of-the-art in technology because world has not made a machine that has as many resources as you need.  
CPU intelligent : machine has 4 core CPU in a machine that is truly parallel. then each core can spawn multiple processes/threads.

  
## Step 2: Review the scalability article  
#### Scalability for Dummies  
###### Part 1: Clones  
Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers.  
That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory.  
Sessions need to be stored in a centralized data store (Database/Redis) which is accessible to all your application servers.  



