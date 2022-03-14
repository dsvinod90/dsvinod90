---
title: Megastore 
layout: default
filename: megastore
--- 
[back](/dsvinod90/tech)

## Megastore: Providing Scalable, Highly Available Storage for Interactive Services

**Authors:** Jason Baker, Chris Bond, James C. Corbett, JJ Furman, Andrey Khorlin, James Larson, Jean-Michel Le ́on, Yawei Li, Alexander Lloyd, Vadim Yushprakh

**[Link to Paper](https://research.google/pubs/pub36971/)**

Megastore is a storage system that blends the scalability of a NoSQL datastore with the convenience of a traditional RDBMS in a novel way, and provides both strong consistency guarantees and high availability. Relational databases provide a rich set of features for easily building applications, but they are difficult to scale to hundreds of millions of users. NoSQL datastores such as Bigtable, HBase or Cassandra are highly scalable, but their limited API and loose consistency models complicate application development. Megastore bridges this gap.

**The key contributions of the paper are:**
1. Design of a data model and storage system that allows rapid development of interactive applications where high availability and scalability are built-in from the start
2. Implementation of Paxos replication and consensus algorithm optimized for low-latency operation across geographically distributed datacenters to ensure high availability

Megastore was deployed at Google for more than 100 production applications to be used as their storage service. It was found that the level of availability was found to be extremely high despite a steady stream of machine failures. Average read latencies were tens of milliseconds depending on the amount of data. Most reads were local. Average write latencies were found to be in the order of 100-400 milliseconds depending on the distance between datacenters.