## Step 1: [Scalability from Scalability Lecture at Harvard](https://www.youtube.com/watch?v=-W9F__D3oY4)  
- Virtical scaling
- Horizontal scaling
- Caching
- Load balancing
- Database replication
- Database partitioning

#### Virtual Scaling  

**Q. What kind fo feature you are looking for or expecting minimally in a any web hosting company that you choose?**  

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

#### Horizontal Scaling  
Intead of one, use bunch of servers.  
We inbound HTTP request we somehow want to distribute that request over all of the verious web serves.  
You have now servers but now how you will decide which server will server your request.  
**Load Balancing**  
Client --> Load balancer(public ips) --> servers(private/public ips) 
 
 **Q What are some alternatives to load balancing the actual load(how busy server is) on the server?**  
1. Using header(url) each types has how server like
   one server will serve html.
   other server will serve gif.
   etc  
what if all server has same content? what is simpler than asking backend server how busy are you right now?  
Hint: When you time something.com into a browser and hit enter what happens?
packet will be send to ip server. but how do you get the ip address.
Using DNS
**DNS** : Domain name system - That server in the world a whole bunch of them is to translate hostname to ips and vise-versa.

So we can use DNS tricks to return backend server ips. So this blackbox(load balancer) is jsut a fancy DNS setup where by instead of returning the IP address of load balancer itself maybe instead od DNS server just returns the IP address of backend server using round robin and it is called **Load balancing with BIND.**

#### Load balancing with BIND

## Step 2: Review the scalability article  
#### Scalability for Dummies  
###### Part 1: Clones  
Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers.  
That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory.  
Sessions need to be stored in a centralized data store (Database/Redis) which is accessible to all your application servers.  



