---
title: Resilient Distributed Datasets 
layout: default
filename: rdd
--- 
[back](/dsvinod90/tech)

## Resilient Distributed Datasets: A Fault Tolerant Abstraction For In-Memory Cluster Computing

**Authors**: Matei Zaharia, Mosharaf Chowdhury, Tathagata Das, Ankur Dave, Justin Ma, Murphy McCauley, Michael J. Franklin, Scott Shenker, Ion Stoica 

**[Link to Paper](https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf)**

While cluster computing frameworks such as MapReduce and Dryad have been widely adopted for large scale data analytics, they lack abstractions for leveraging distributed memory. For instance, intermediate results between two MapReduce jobs have to be written to the storage disk and then accessed from the disk in order to be fault tolerant. This brings down the execution time by a large order of magnitude when working with big data. While some solutions for in-memory data abstractions were provided such as HaLoop and Pregel, their use cases were very narrow focussed and the scope of such in-memory abstractions could be applied in a more general way. RDDs solve this problem by providing a programming interface that can be fault tolerant with very fast execution times. This was achieved by implementing coarse-grained transformations to many data items and providing a lineage instead of granular data. If a partition of the RDD is lost, then it can be rebuilt just for the lost partition using the lineage. This process has proven to be much faster than performing Disk I/O at every intermediate stage.

**Here is how RDDs contributed to resolving the challenges:**
1. By providing the concept of lineage which is used to recompute the lost partition of an RDD instead of performing I/O operations on disk. This ensured fault tolerance while maintaining quick recovery times.
2. By providing the Spark programming interface and an interactive shell from where RDDs can be created.
3. By implementing the concept of dependencies which allow new child RDDs to be created from parent RDDs using transformations and actions
4. By being lazy: this means that a transformation will only be acted upon if an action is performed on the RDD. This saves compute time.
5. By incorporating controlled partitioning based on narrow and wide dependencies. This allows programmers to custom partition based on the use case thereby resulting in very fast execution times.
6. By implementing a DAG scheduler which takes the lineage as input and chalks out the Directed Acyclic Graph which is the synonymous with an execution plan for the cluster manager. The cluster manager then distributes this execution plan to the workers where the tasks are run and outputted.

**The paper backs up its claims in the following way:**
1. *Iterative machine learning applications:*
    1. Implemented logistic regression and k-means to compare performance of Hadoop, HadoopBinMem and Spark
    2. Both algorithms were run for 10  iterations on 100GB datasets using 25-100 machines.
    3. Spark, HadoopBM and Hadoop took 3s, 62s and 76s respectively for Logistic regression and 33s, 87s and 106s respectively for k-means for a cluster of 100 machines
2. *Fault recovery during k-means:*
    1. Running times for 10 iterations of k-means on a 75 node cluster were compared.
    2. There were 400 tasks working on 100GB data per iteration
    3. One node was failed in the 6th iteration
    4. RDD was re-created using the lineage by taking an addition 30s only
    5. The average time then resumed to what it originally was i.e. 58s from the 7th iteration onwards
3. Page Rank was performed using Hadoop, Spark and Spark with Controlled Partition. While Hadoop took 171s to complete the task, Basic Spark took 72s and Spark with Controlled Partitioning took 23s
4. *Interactive Data Mining:*
    1. Analyzed 1TB of Wikipedia page view logs(~2years of data)
    2. Used 100 large EC2 instances with 8cores and 68GB RAM each
    3. Ran queries to find total view of:
        1. all pages
        2. pages with titles exactly matching a given word
        3. pages with titles partially matching a word
    4. Maximum time taken for Spark was 7s while disk querying took 170s