---
title: Dremel 
layout: default
filename: dremel 
--- 
[back](/dsvinod90/tech)

## Dremel: Interactive Analysis of Web-Scale Datasets

**Authors:** Sergey Melnik, Andrey Gubarev, Jing Jing Long, Geoffrey Romer, Shiva Shivakumar, Matt Tolton, Theo Vassilakis

**[Link to Paper](https://ai.google/research/pubs/pub36632/)**

Dremel supports interactive analysis of large datasets over shared clusters of commodity machines. 
Unlike traditional databases, it is capable of accessing data in place for nested data.  Dremel can execute many queries over such data that would otherwise require a large sequence of MapReduce jobs and would take a fraction of the execution time as well.

**Here are some of the key contributions of the paper:**
1. Columnar storage format for nested data.
2. Algorithms for dissecting nested records into columns and then restructuring them
3. Efficient Dremel query language and execution that operates on column-striped nested data and does not require restructuring of nested records
4. Application of execution trees in database processing just like it is implemented in web search systems

Experiments were performed on trillion-record multi terabyte datasets conducted on system instances running 1000-4000 nodes. It was observed that 
On local disk it was observed that when few columns are read, the gains of columnar representation are about an order of magnitude. Retrieval time for columnar nested data grew linearly with number of fields.
On comparing MapReduce and Dremel, it was observed that Dremel tool significantly less execution time compared to MR-record and MR-columns
Other experimental observation supporting the claims can be found in Section 7 and 8 of the research paper.