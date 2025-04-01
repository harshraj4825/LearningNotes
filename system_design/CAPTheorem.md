## CAP theorem  
In a distributed system(a collection of interconnected nodes that share data.)
you can only have two out of the following three guarantees across a write/read pair:  
- Consistency
- Availability
- Partition Tolerance  
One of them must be sacrificed.
![image](https://github.com/user-attachments/assets/6e0bf3b4-50a7-4711-9e1a-01151debfa51)
- Consistency - A read is guaranteed to return the most recent write for a given clinet.
- Availability - A non-failing node will return a reasonable response within a reasonable amount of time(no error/timeour).
- Partition Tolerance - The system will continue to function when network partitons occur.


Nerworks aren't reliable, so you will need to support Partition tolerance. You will need to make a software tradeoff between consistency vs availability.  
**CP - Consitency/Partition Tolerance**  
Wait for a response from the partitioned node which could result in timeout error. The system
can also choose to return an error, depending upon scinario you desire.  
-Choose consistency over availability when you business requirement dictate atomic reads/writes.  
**AP - Availability/Partition Tolerance**  
Return most recent version of data you have. This system state will also accept writes the can be processed later when the partition is resolved. Choose Availability over Consistency when your business requirements allow for some flexibility around when the data in the system syschronizes.  
AP is a good choice if the business needs to allow for eventual consistency or when the system needs to continue working despite external errors.  


The design between Consistency and Availability is a software trade off. You can choose what to do in the face of a network partition- the control is in your hands. Network outages, both temporary and permanent, are a fact of life and occure whether you want them to or not - this exists outside of your software.
