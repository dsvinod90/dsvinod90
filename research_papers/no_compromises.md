---
title: No Compromises 
layout: default
filename: no_compromises
--- 
[back](/dsvinod90/tech)

## No Compromises: distributed transactions with consistency, availability and performance

**Authors:** Aleksandar Dragojevic ́, Dushyanth Narayanan, Edmund B. Nightingale, Matthew Renzelmann, Alex Shamis, Anirudh Badam, Miguel Castro

**[Link to Paper](https://dl.acm.org/doi/10.1145/2815400.2815425)**

Transactions with strong consistency and high availability simplify building and reasoning about  distributed systems. But these implementations performed poorly which forced designers to avoid transactions completely. As a result, consistency guarantees were weakened. No Compromises demonstrates a software that eliminates the need to compromise this trade-off by using a main memory distributed computing platform called Farm which can provide distributed transactions with strict serializability, high performance, durability and high availability. FaRM achieves a peak throughput of 140 million TATP transactions per second on 90 machines with a 4.9 TB database and it recovers from a failure in less than 50ms.

**Here is how FaRM contributed to resolving the challenges:**
1. By providing distributed ACID transactions with strict serializability, high availability, high throughput and low latency.
2. Addressing CPU bottlenecks by: 
	1. Reducing message counts
	2. Using one-sided RDMA reads and writes instead of messages
	3. Exploiting parallelism effectively
3. Providing lock-free reads in the FaRM API which are optimized single-object read only transactions
4. Using Zookeeper as coordination service but handling fault tolerance by using implementations that leverage RDMA to recover fast
5. Using leases to detect failures

**The paper backs up its claims in the following way:**
1. *TATP:* FaRM performed 140 million TATP transactions per second with 58micro seconds median latency and 645 microseconds 99th percentile latency. FaRM outperforms TATP results for Hekaton by a factor of 33.
2. *TPC-C:* FaRM performs up to 4.5 million TPC-C  "new order" transactions per second with median latency of 808 microseconds and 99th percentile latency of 1.9ms. FaRM's throughput was 17x higher than Silo without logging and it's latency at this throughput level is 128x better than Silo with logging
3. *Read performance:* Even though the focus of this paper was on transactional performance and failure recovery, the read-only performance was significantly improved too. A throughput of 790 million lookups/second with median latency of 23 microseconds and 99th percentile latency of 73 microseconds was observed. This is a 20% improvement on the previously reported per-machine throughput for the same benchmark