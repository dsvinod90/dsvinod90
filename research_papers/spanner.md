---
title: Spanner 
layout: default
filename: spanner
--- 
[back](/dsvinod90/tech)

## Spanner: Google’s Globally Distributed Database

**Authors**: JAMES C. CORBETT, JEFFREY DEAN, MICHAEL EPSTEIN, ANDREW FIKES, CHRISTOPHER FROST, J. J. FURMAN, SANJAY GHEMAWAT, ANDREY GUBAREV, CHRISTOPHER HEISER, PETER HOCHSCHILD, WILSON HSIEH, SEBASTIAN KANTHAK, EUGENE KOGAN, HONGYI LI, ALEXANDER LLOYD, SERGEY MELNIK, DAVID MWAURA, DAVID NAGLE, SEAN QUINLAN, RAJESH RAO, LINDSAY ROLIG, YASUSHI SAITO, MICHAL SZYMANIAK, CHRISTOPHER TAYLOR, RUTH WANG, and DALE WOODFORD, Google, Inc. 

**[Link to Paper](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/65b514eda12d025585183a641b5a9e096a3c4be5.pdf)**

Spanner is a scalable, globally distributed database. It shards shards data across global datacenters and is migrates data across machines to balance load and in response to failures. Applications use Spanner for high availability. It can even handle wide area network partitions.  Spanner's main focus is managing cross-datacenter replicated data. However there are other platforms like BigTable that have been designed and implemented on top of Google's distributed-systems infrastructure. It was found that using Bigtable can be difficult for applications that have complex evolving schemas or those that want strong consistencies in the presence of wide-area replication. Because of this many applications at Google chose Megastore despite it poor write throughput. This is where Spanner comes in and bridges that gap.

**Here are some of the key contributions of the paper:**
1. The replication configurations for data can be dynamically controlled at a fine grain by applications.
2. Provision of externally consistent reads and writes
3. Provision of globally consistent reads across the database at a timestamp
4. Ensuring the above two points by implementing the concept of TrueTime API

**The paper backs up its claims in the following way:**
1. *Microbenchmark measurements:* were taken on timeshared machines: each spanserver ran on scheduling units of 4GB RAM and 4 cores. Each zone contained one spanserver. Clients and zones were placed in a set of datacenters with network distances of less than 1ms. The test database was created with 50 Paxos groups with 2500 directories. Operations were standalone reads and writes of 4KB.
2. *Latency:*  It was found the clients used sufficiently few operations to avoid queuing at the servers.
Throughput: It was found that the clients used sufficiently many operations to saturate the servers' CPUs. Scaling upto 50 participants in a two phase commit was found to be reasonable in both mean and 99th percentile. At 100 participants, latencies start to rise noticably.
3. *Availability:* It was found that shorter lease times would re- duce the effect of server deaths on availability, but would require greater amounts of lease-renewal network traffic 
4. *True Time:* Google's machine statistics show that bad CPU are 6 times more likely than bad clocks i.e. clock issues are extremely infrequent relative to much more serious hardware problem and it was indeed found that True Time's implementation was trustworthy.