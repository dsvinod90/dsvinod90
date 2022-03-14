---
title: Google File System 
layout: default
filename: gfs
--- 
[back](/dsvinod90/tech)

## The Google File System

**Authors:** Sanjay Ghemawat, Howard Gobioff, and Shun-Tak Leung 

**[Link to Paper](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)**

The Google File System shares the same goals as the previous distributed file system such as scalability, reliability, high performance and availability. However, these systems were not efficient to cater to the current and anticipated application workloads and technological environment. Hence, Google had to come up with their own file system that can cater to their specific needs. Google achieves this by implementing the following in its design of the file system:
1. Treat component failures as a norm rather than an exception. The file system is made up of thousands of storage machines that are commodity parts and there is no guarantee that some of them are not functional at any point of time. Hence, constant monitoring, error detection, fault tolerance and automatic recovery were incorporated into the GFS.
2. Revisit design assumptions and parameters such as I/O operation and block sizes as now-a-days files are traditionally huge in size. It is common to have multi GB files. It is not practical in today's world to manage billions of KB-sized files when its typical to have TBs worth of file capacity.
3. Mutate files by appending new data instead of overwriting existing data. Random writes within a file to be non-existent. After the write operation is complete the file is just read only and that too sequentially. This access pattern on huge files ensures performance optimizations and atomicity guarantees.
4. Co-designing the applications and the file system API benefits the overall system by increasing the flexibility.

**Here is how GFS contributed to resolving the challenges:**
1. By designing of the interface in a way that provided a familiar file system interface by providing hierarchically organized files in directories and identifying them by pathnames.
2. By implementing a single master and multiple chunk-servers architecture with shadow master where each of these is a commodity Linux machine running a user level server process.
3. By having a relaxed consistency and high availability model
4. By reducing overhead on master by caching metadata at the client side and having the client communicate directly with the chunk-servers
5. By decoupling the flow of data from the flow of control between the client and the replicas to manage network efficiently
6. By implementing snapshots (creating a copy of file or directory tree at low cost) and record appends (multiple clients append to the same file concurrently while atomicity is maintained)
7. Lazy garbage collection, allowing for simpler and more reliable system
8. Checksumming feature to detect corruption of stored data.

**The paper backs up its claims in the following way:**

Two clusters were used within Google, Cluster A with 342 chunk-servers was used regularly for R&D by hundreds of engineers and Cluster B with 227 chunk-servers was used for production data processing. Following observations were made:
1. *Storage:* A and B store 18 TB and 52 TB of data respectively showing that the clusters had many chunks as the files were large.
2. *Metadata:* Each individual master server in the clusters had only 50 to 100 MB of metadata. This showed that data recovery is very fast.
3. *Read and Write Rates:* The average read rate in cluster A was 580 MB/s and in cluster B it was 380 MB/s even though B had heavy write traffic on its network too. The average write rate was 1.5 MB/s for A and about 110 MB/s for B.
4. *Master Load:* The master load was around 300 Ops/sec for A and about 500 Ops/sec for B. The master was easily able to keep up this rate and was not a bottleneck for these workloads
5. *Recovery Time:* In one experiment one chunk-server was killed in B which had 15,000 chunks containing 600 GB of data. All chunks were restored in 23.2 minutes at an effective replication rate of 440 MB/s. In another experiment, two chunk-servers were killed each with roughly 16,000 chunks and 660 GB of data. They were cloned at high priority and restored in under 2 minutes.