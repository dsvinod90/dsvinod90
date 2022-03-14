---
title: Big Table 
layout: default
filename: big_table 
--- 
[back](/dsvinod90/tech)

## Bigtable: A Distributed Storage System for Structured Data

**Authors:** Fay Chang, Jeffrey Dean, Sanjay Ghemawat, Wilson C. Hsieh, Deborah A. Wallach Mike Burrows, Tushar Chandra, Andrew Fikes, Robert E. Gruber

**[Link to Paper](https://research.google/pubs/pub27898/)**

Bigtable was designed in late 2003 to manage large amounts of distributed data in Google. It was designed to reliably scale petabytes of data to thousands of machines. Bigtable resembles a database as it shares many implementation strategies with databases. Compared to Parallel databases and main-memory databases Bigtable provides a different interface. It does not support a full relational data model but provides a simple data model that supports dynamic control over data layout and format and allows clients to reason about the locality properties of the data represented in the storage.

**The key contributions of the paper are:**
1. Tables in Bigtable are sparse, distributed, persistent multi-dimensional sorted map
2. Rows maintained in lexicographic order and grouped into tablets
3. Columns grouped and stored as column families
4. The Bigtable API that provides functions for creating and deleting tables and column families
5. Using GFS to store log and data files
6. Use of controlled compression by clients for SSTables
7. Caching for read performance
8. Use of bloom filters

The tablet servers were configured to use 1GB of memory and to write to a GFS cell consisting of 1786 machines with two 400GB IDE hard drives each. For single tablet server performance, it was found that the server executes 1200 reads/second or 75MB/s of data from GFS. Random reads from memory was faster. Sequential reads were found to be faster than random reads and scans were faster than sequential reads. Writes were found to perform better than reads.
It was found that as they scaled from 1 to 500 severs  the aggregate throughput increases dramatically by over a factor of 100.