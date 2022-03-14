---
title: Naiad 
layout: default
filename: naiad
--- 
[back](/dsvinod90/tech)

## Naiad: A Timely Dataflow System

**Author:** Derek G. Murray, Frank McSherry, Rebecca Isaacs, Michael Isard, Paul Barham, Martin Abadi (Microsoft Research Silicon Valley)

**[Link to Paper](https://sigops.org/s/conferences/sosp/2013/papers/p439-murray.pdf)**

There was no existing system that could satisfy all three requirements of many data processing tasks i.e. low-latency interactive access to results, iterative sub-computations and consistent intermediate outputs in order for sub-computations to be nested and composed. Naiad is a general purpose system that fulfills all of these requirements and also support a variety of high-level programming models while being performant. In order to be able to do so, the following features were adopted:
1. structured loops that allowed feedback in the dataflow
2. stateful data flow vertices that were capable of consuming and producing records without global coordination 
3. notifications for vertices once they have received all records for a given round of input or loop iteration

**Here is how Naiad contributed to contributing to resolving challenges:**
1. By implementing of timely dataflow that resulted in concurrent execution of different epochs and iterations and explicit vertex notification after all messages of a certain timestamp were delivered.
2. By relying on data parallelism to increate the aggregate computation, memory and bandwidth available to applications.
3. By deploying workers which are responsible for delivering messages and notifications to the vertices in the partition of timely dataflow graph.
4. By using distributed progress tracking to track the status of any outstanding events of a worker in the system with a pointstamp that could result in the pointstamp of the notification. 
5. By providing for fault tolerance by implementing Checkpoint and Restore interface.

**The paper backs up its claims in the following way:**

The Hardware setup was 2 racks of 32 computers, each with 2 quad-core 2.1GHz AMD Opteron processors, 16GB memory and an Nvidia NForce Gigabit Ethernet NIC. Each rack switch has 40Gbps uplink to the core switch.
1. *Throughput:* It was found that Naiad achieves a throughput that scales linearly though opportunities exist to improve its absolute performance.
2. *Latency:* The median time per iteration for 100K iterations was found to be 753microseconds for 64 computers. However, the 95th percentile showed the adverse impacts of micro-stragglers with increase in the number of computers.
3. *Protocol optimizations:* The optimizations were found to reduce the volume of protocol traffic by one or two orders of magnitude depending on whether it was a LocalAccumulation or GlobalAccumulation.
4. *Scaling:* WCC was found to scale more slowly at 24 computers and reaches a max speedup of 38x on 64 computers. WordCount was found to scale linearly with 46x speedup on 64 computers.
