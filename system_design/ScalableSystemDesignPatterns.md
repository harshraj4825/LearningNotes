## Scalable System Design Patterns
1. Load balancer  
   In this model, there is dispatcher that determines which worker instance will handle the request based on different policies. The application should best be in
   stateless so any worker instance can handle the request.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgs7yGseA2JblV-s_vw5HoRkfsQ4WM9fBOprJByra9VPXiUxXCYf-D4NWqqVdJKJrYd3xDUgOiPIccV9JNc_32ph9MnmgDKjeAlceNKsR3JT7kiYFwWW6i2ySTa8Kj3FwU2ceWhd4P04CGA/s400/p1.png)

2. Scatter and Gatter  
   In this model, the dispatcher multicast the request to all workers of the pool. Each worker will compute a local result and send it back to the dispatcher, who will consolidate them into a single response and then send back to the client.
   This model is used in Search engine like: Yahoo, Google to handle user's keyword search request... etc.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjVT7xapK-hUwJ3w8BfYihr5zsGX9tPVhoGzjMSzHF4hc_EsYohSvj_3nfMhD0c2uIco1Bg92ZLUrrERRM6SICWJT4fp2j4775IH7RthavMdBSOmJz1yWC4vWrprRix-EZfHwNgaTYf3irh/s1600/P2.png)
3. Result cache  
   In this model, the dispatcher will first lookup is the request has been made before and try to find the previous result to return, In order to save the actual execution.
   This pattern is commonly used in large enterprise application. Memecached is a very commonly deployed cache server.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFqHcngyxv_0yf4AnQhxkS96UlsM-W48GnLe8KYRKDO6QgkSqK9GhnpuzrG8Fthn870OerRpY-p9L2pl180pr8ohCrnvd_R5rUhQp_DKuMxb0GENhqWxM1yqBBnWN8mOA9Q7z07SPPTl4x/s400/P3.png)
4. Shared Space  
   This model also known as "Blackboard"; all worker monitor information from the shared space and contributes parial knowledge back to the blackboard. This information is continuously enriched until a solution is reached.
   This pattern is used in JavaSpace and also commercial product GigaSpace.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjODXfMYS0n8ClctxFLT_uiWFQwNfctdCvDGKT2-CWpRmfuMtCTG1D8V8pavsporz_DlbH8-c00-XzzLic6yBUqwchCiFjn7t853hBG264s1zF6w4ced-Sto3nVl4sNJXoiuD6j8o3EwfmP/s1600/P4.png)
5. Pipe and Filter  
   This model also known as "Data Flow Processing"; All workers connected by pipes where data is flow across.
   This pattern is very common EAI pattern
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgaZl7AMJhO2bje3VBYsVIS6re_l2p3M1XsF9FJ4xR_MIJfiwwGvQFgnvNctokR09C1PuMAzl6qd6lGSex46VLl6OsUbMAS55T1DyPQIkc6HV5B4nO6IRvL-XRxN_b9GlQBOVGsJA3mhE1w/s1600/P5.png)
6. Map Reduce:  
   This model is targetting batch jobs where disk I/O is the major bottleneck. It use a distributed file system so that disk I/O can be done in parallel.
   This pattern is used in many of Google's internal application, as well as implemented in open source Hadoop parallel processing framwork.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8o6Kw2cwTXE0HvzfCY1-Fm3fYz3JsC3T8On7sZ0Ts3q6iWeh7zn887be9sUcNcEtkaoRdpf0GoSYoXQ-Yh59ZvxA3l3x9S0Xt9etDFugaNYQALVYrI7LqBDnl9s0YoYPNcla8Q54zRfLI/s1600/P7.png)
7. Bulk Syschronous Parellel  
   This model is based on lock-step execution across all workers, coordinated by a master. Each worker repeat the following steps until the exit condition is reached, when there is no more active workers.
   1. Each worker read data from input.
   2. Each worker perform local processing based on the read data.
   3. Each worker push local result along its direct connection.
   ![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjUUwz1xF9WP1MmcZCIUSmc2jOG0u_aN105HNR3aX0Zj0Yvyv4BBDFhYwJYaSfTgOD8jm3kwFxhei_9IRkaKIf0BoU_NF0g8Xh1QxK8wD51lUVIWg6zRVKTEV6IT6FD3wbm1E5fjH0jBSbO/s1600/P8.png)

8. Execution Orchestrator
   This model is based on an instelligent scheduler/orchestrator to schedule ready-to-run tasks (based on a dependency graph) across a clusters of dumb workers.
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqaEyJWVci394vQjOLzWDqGB4PPJqoMXZNLE9guoDTBkBBd_R6RVRY2T3OJEh61JyIxjisc8M3QcWMxEq-wDU6owoBrdmTwQPyo6zH-U0sHtsXfxokuJiU_6vt7TGI9WRX9nyjsAo3DlUM/s1600/P8.png)
   
