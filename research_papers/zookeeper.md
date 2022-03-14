---
title: Zookeeper 
layout: default
filename: zookeeper 
--- 
[back](/dsvinod90/tech)

## ZooKeeper: Wait-free coordination for Internet-scale systems

**Authors**: Patrick Hunt, Mahadev Konar, Flavio P. Junqueira and Benjamin Reed

**[Link to Paper](https://www.usenix.org/legacy/event/atc10/tech/full_papers/Hunt.pdf)**

Zookeeper is a service for co-ordinating processes of distributed applications. So far there were services such as Amazon Simple Queue Service, Chubby, VMS etc that approached co-ordination by focussing on very specific aspects such as queueing, locks etc. 
1. Zookeeper, instead of implementing specific primitives on the server side, exposed an API on the client side that enabled developers to implement their own primitives by implementing a co-ordination kernel. By doing so, it enables multiple forms of co-ordination adapted to the requirements of applications instead of constraining developers to a fixed set of primitives. 
2. By removing blocking primitives such as locks, it eliminated slow or faulty clients which impacted the performance of faster clients. 
3. It's wait free data objects improve performance and fault tolerance.
4. Zookeeper also provides an ensemble of servers that use replication to achieve high availability and performance. 
5. Finally, guaranteeing FIFO client order enables clients to submit operations asynchronously thereby significantly reducing the time of initialization of the client.

**Here are the key contributions of the paper:**
1. Providing a wait-free co-ordination service in distributed systems and providing highly available systems
2. Implementing various co-ordination techniques using the co-ordination kernel
3. Linearizable writes: all requests that update Zookeeper's state are serializable and respect precedence
4. FIFO client order: all requests from a given client are executed in the order that they were sent by the client

Evaluation was carried out on a cluster 35 machines to serve 250 simultaneous clients. 
1. *Throughput:* it was observed that Zookeeper achieved high throughput by distributing load across the servers because of the relaxed consistency guarantees. On the other hand, Chubby directed all the requests to the leader and the throughput was found to be much lower as the extra CPU and network load caused by the clients impacted the performance of the leader.
2. *Failure and recovery:* It was observed that the failure of a single follower reduced the throughput slightly. The leader election algorithm was able to recover fast enough to prevent throughput from dropping substantially. Zookeeper took less than 200 ms to elect a new leader. Even if the followers take more time to recover, Zookeeper raises the throughput significantly faster once it starts processing requests.
3. *Latency of requests:* It was found that the average request latency for three Zookeeper workers was 1.2 ms and for nine servers was 1.4 ms which was much higher than Chubby's throughput.
