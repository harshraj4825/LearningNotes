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
BIND(DNS Server) - Berkeley Internet Name Domain is a software of tools including the world's most widely used DNS server software.  
**Why diificult to implement?**  
Because one user can be more intense user so round robin wont work.  
**How to solve session management if you have multiple server?**  
set the session data into centralized storage. but this is the weekness in network topology. **so how will you fix this?**  
instead of hard drive Use RAID - Redundant array of independent discs.  
RAID0, RAID1, RAID5, RAID10 etc.  
RAID0 - write chunck of data to multiple drive to improve performnace
RAID1 - same data will be written into two drive  
This will reduce dedency for session data or share state like this.  
Sticky Session  
- Shared Storage?
  FC, iSCSI, MySQL, NFS (Network file system)
- Cokees?

Load Balancers:  
Software - ELB, HAProxy, LVS
Hardware - Barracuda, Cisco, Citrix

#### Sticky Sessions  
Even if you visit same website multiple time. still you will be endup will same session.  
  - Shared Storage like FC, iSCSI, NySQL, NFS, etc. storing session, user id.
  - Cookies?
    Storing information cookies like storing server id into cookies. Problem: what if your ip is changing also you do not want to reviel youe ip address to the world.
    PHP way create a big number that load balancer will remember.

#### PHP Accelerators  


## Step 2: Review the scalability article  
#### Scalability for Dummies  
###### Part 1: Clones  
Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers.  
That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory.  
Sessions need to be stored in a centralized data store (Database/Redis) which is accessible to all your application servers.  

###### Part 2: Databases  
your servers can now horizontally scale and you can already serve thousands of concurrent requests. But somewhere down the road your application gets slower and slower and finally breaks down. The reason: your database. It’s MySQL, isn’t it?  
you can choose from 2 paths:  
**Path #1** is to stick with MySQL and keep the “beast” running. Hire a database administrator (DBA,) tell him to do master-slave replication (read from slaves, write to master) and upgrade your master server by adding RAM, RAM and more RAM. In some months, your DBA will come up with words like “sharding”, “denormalization” and “SQL tuning” and will look worried about the necessary overtime during the next weeks. At that point every new action to keep your database running will be more expensive and time consuming than the previous one.  

**Path #2** means to denormalize right from the beginning and include no more Joins in any database query. You can stay with MySQL, and use it like a NoSQL database, or you can switch to a better and easier to scale NoSQL database like MongoDB or CouchDB. Joins will now need to be done in your application code. The sooner you do this step the less code you will have to change in the future. But even if you successfully switch to the latest and greatest NoSQL database and let your app do the dataset-joins, soon your database requests will again be slower and slower. You will need to introduce a cache.
###### Part 3: Cache  
you now have a scalable database solution. You have no fear of storing terabytes anymore and the world is looking fine. But just for you. Your users still have to suffer slow page requests when a lot of data is fetched from the database. The solution is the implementation of a cache.  
With “cache” I always mean in-memory caches like Memcached or Redis. Please never do file-based caching, it makes cloning and auto-scaling of your servers just a pain.   

But back to in-memory caches. A cache is a simple key-value store and it should reside as a buffering layer between your application and your data storage. Whenever your application has to read data it should at first try to retrieve the data from your cache. Only if it’s not in the cache should it then try to get the data from the main data source. Why should you do that? Because a cache is lightning-fast. It holds every dataset in RAM and requests are handled as fast as technically possible. For example, Redis can do several hundreds of thousands of read operations per second when being hosted on a standard server. Also writes, especially increments, are very, very fast. Try that with a database!  
There are 2 patterns of caching your data. An old one and a new one:  
**#1 - Cached Database Queries**  
That’s still the most commonly used caching pattern. Whenever you do a query to your database, you store the result dataset in cache. A hashed version of your query is the cache key. The next time you run the query, you first check if it is already in the cache. The next time you run the query, you check at first the cache if there is already a result. This pattern has several issues. The main issue is the expiration. It is hard to delete a cached result when you cache a complex query (who has not?). When one piece of data changes (for example a table cell) you need to delete all cached queries who may include that table cell. You get the point?  

**#2 - Cached Objects**  
That’s my strong recommendation and I always prefer this pattern. In general, see your data as an object like you already do in your code (classes, instances, etc.). Let your class assemble a dataset from your database and then store the complete instance of the class or the assembed dataset in the cache. Sounds theoretical, I know, but just look how you normally code. You have, for example, a class called “Product” which has a property called “data”. It is an array containing prices, texts, pictures, and customer reviews of your product. The property “data” is filled by several methods in the class doing several database requests which are hard to cache, since many things relate to each other. Now, do the following: when your class has finished the “assembling” of the data array, directly store the data array, or better yet the complete instance of the class, in the cache! This allows you to easily get rid of the object whenever something did change and makes the overall operation of your code faster and more logical.

And the best part: it makes asynchronous processing possible! Just imagine an army of worker servers who assemble your objects for you! The application just consumes the latest cached object and nearly never touches the databases anymore!  



