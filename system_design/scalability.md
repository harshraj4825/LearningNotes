## Step 1: [Scalability from Scalability Lecture at Harvard](https://www.youtube.com/watch?v=-W9F__D3oY4)
  
## Step 2: Review the scalability article  
#### Scalability for Dummies  
###### Part 1: Clones  
Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers.  
That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory.  
Sessions need to be stored in a centralized data store (Database/Redis) which is accessible to all your application servers.  



