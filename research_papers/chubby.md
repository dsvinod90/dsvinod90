---
title: Chubby 
layout: default
filename: chubby 
--- 
[back](/dsvinod90/tech)

## The Chubby lock service for loosely-coupled distributed systems

**Author:** Mike Burrows

**[Link to Paper](https://research.google/pubs/pub27897/)**

Chubby lock service provides coarse-grained locking as well as reliable storage for loosely-coupled distributed system. The purpose of the lock service is to allow its clients to synchronize their activities and to agree on basic information about their environment. Before Chubby was deployed, most distributed systems in Google used ad-hoc methods for primary election or required operator intervention . In the former case, Chubby allowed a small saving in computing effort whereas in the latter case, it achieved a significant improvement in availability in systems that no longer required human intervention on failure.

**Here are some of the key contributions of the paper:**
1. Imposing coarse-grained locks rather than fine-grained locks so that they have far less load on the lock server
2. Choosing to provide a lock service instead of a library or service for consensus
3. Implementing a simple file system interface similar to Unix
4. Provisioning a 64-bit file content checksum to check for errors in files
5. Subscription to a range of events by clients when a handle is created
6. Caching mechanism provided by Chubby clients for file data and node meta-data in a consistent and write-through cache held in memory

It was found that Chubby's data fit into RAM which made most of the operations cheap. The mean request latency of production servers was found to be a small fraction of a millisecond regardless of the cell load until the cell approaches overload. RPC read latencies was limited by RPC system and network to be under 1ms for local cells. More details of the implementation and use can be found in section 4 of the research paper.