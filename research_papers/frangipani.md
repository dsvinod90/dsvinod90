---
title: Frangipani 
layout: default
filename: frangipani
--- 
[back](/dsvinod90/tech)

## Frangipani: A Scalable Distributed File System

**Author:** Chandramohan A. Thekkath, Timothy Mann, Edward K. Lee

**[Link to Paper](https://dl.acm.org/citation.cfm?id=266694)**

Frangipani is a distributed file system that tries to get as close as possible to the ideal distributed file system which has the following characteristics:
1. Provide all its users with coherent shared access to the same set of files
2. Would be scalable to provide more storage space
3. Provides higher performance to a growing user community
Frangipani achieves its success by providing a very simple internal structure that enables programmers to handle system recovery, reconfiguration and load balancing with little machinery.

**Here are the key contributions of the paper:**
1. Providing all the users with a consistent view of the same set of files
2. Easy addition of more servers to an existing Frangipani installation to increate throughput and storage capacity
3. Hassle free addition of new users by the system administrators without concern about which machine will store and manage the new data
4. Ability by the admin to make full and consistent backup of the entire file system without bringing the node down. 
5. Ability to have online backups allowing users to quickly access accidentally deleted files
6. A file system that can tolerate and recover from machine, network and disk failures without operator intervention.

**The paper backs up its claims in the following way:**
1. *Single Machine Performance:* Frangipani was compared to Unix's AdvFS and it was found that Frangipani had throughput of 15.3 MB/s compared to AdvFS's 13.3 MB/s for writes and 10.3 MB/s vs 13.2 MB/s for reads. The CPU utilization for Frangipani was found to be 42% compared to AdvFS's 80% for writes and 25% vs 50% for reads.
2. *Scaling:* Frangipani 's scaling on Uncached Read was found to have negligible variation in the steady -state throughput. The scaling on write also observed little variation in the steady-state throughput during this interval. 
