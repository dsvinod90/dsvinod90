---
title: Pastry 
layout: default
filename: pastry
--- 
[back](/dsvinod90/tech)

## Pastry: Scalable, decentralized object location and routing for large scale peer-to-peer systems

**Authors**: Antony Rowstron and Peter Druschel

**[Link to Paper](http://rowstron.azurewebsites.net/PAST/pastry.pdf)**

Peer-to-peer systems can be characterized as distributed systems in which all nodes have identical capabilities and responsibilities and all communication is symmetric. There are currently many projects aimed at constructing peer-to-peer applications and understanding more of the issues and requirements of such applications and systems. One of the key problems in large-scale peer-to-peer applications is to provide efficient algorithms for object location and routing within the network. This paper presents Pastry, a generic peer-to-peer object location and routing scheme, based on a self-organizing overlay network of nodes connected to the Internet. Pastry is completely decentralized, fault-resilient, scalable, and reliable. Moreover, Pastry has good route locality properties. 

**Here are some of the key contributions of the paper:**
1. Each node in the Pastry network has a unique numeric identifier (nodeId). When presented with a message and a numeric key, a Pastry node efficiently routes the message to the node with a nodeId that is numerically closest to the key, among all currently live Pastry nodes.
2. Pastry takes into account network locality; it seeks to minimize the distance messages travel, according to a scalar proximity metric like the number of IP routing hops
3. Pastry's simple API
4. Pastry’s protocols for handling the arrival and departure of nodes in the Pastry network 
5. Ability to locate nearest node in over 75% and one of two nearest nodes in over 91% of all queries

A network emulation environment was implemented permitting experiments with upto 100,000 Pastry Nodes. All experiments were performed on a quad-processor Compaq AlphaServer ES40 (500MHz 21264 Alpha CPUs) with 6GBytes of main memory, running True64 UNIX, version 4.0F. The Pastry node software was implemented in Java and executed using Compaq’s Java 2 SDK, version 1.2.2-6 and the Compaq FastVM, version 1.2.2-4. 
1. *Routing performance:* The results showed that the number of route hops scaled with the size of the network. The routing throughput, in messages per second, of a Pastry node which had unoptimized Java implementation was found to be over 3000 messages per second.
2. *Maintaining the network:* The results show that Pastry’s method of node integration is highly effective in initializing the routing tables with good locality. On average, less than 1 entry per level of the routing able is not the best choice
3. *Replica routing:* The results show that Pastry is effective in locating a node near the client in the vast majority of cases, and that the use of the heuristic is effective. 
4. *Node failures:* The results show that Pastry recovers all missing table entries, and that the quality of the entries with respect to locality (fraction of optimal entries) approaches that before the failures.