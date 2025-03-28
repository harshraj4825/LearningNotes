## Performance vs scalability  
A service is scalable if it results in increased performace in a manner perportional to resources added.
- If you have a proformance problem, your system is slow for a single user.  
- If you have a scalability problem, your system is fast for a single user but slow under heavy load.

**What is it that we really mean by scalability?** A service is said to be scalable if when we increase the resources in a system, it results in increased performace in a manner perportional to resources added. Increasing performace in manner
 perportiinal to resource adeed.  

 **Why is scalability so hard?**  
 Because scalability cannot be an after-thought. It requires applications and platforms to be designed with scaling in mind, such that adding resources actually results in improving the performance or that if redundancy is introduced the system performance is not adversely affected. Many algorithms that perform reasonably well under low load and small datasets can explode in cost if either requests rates increase, the dataset grows or the number of nodes in the distributed system increases.

 **Is achieving good scalability possible?**  
 Absolutely, but only if we architect and engineer our systems to take scalability into account. For the systems we build we must carefully inspect along which axis we expect the system to grow, where redundancy is required, and how one should handle heterogeneity in this system, and make sure that architects are aware of which tools they can use for under which conditions, and what the common pitfalls are.

 
