---
layout: page
title: Lectures
---


<style>
.lecture tr td:first-child {
  width: 15%;
  font-weight: bold;
}
.lecture tr:first-child {
  font-weight: bold;
}
.lecture tr td:nth-child(2) {
  width: 20%;
}
</style>

{: .table  .lecture :}
|        |  Title   |  Description | Instructor |
| Week 1 |  Introduction   |  Why not single machine? Big-data challenges, datacenter structure, typical use cases and their requirements. Course overview. | All
| Week 2 |  Batch Processing |  MapReduce: architecture, components, programming model. | Sahu
| Week 3 |  Batch Processing (cont) | Storage side: HDFS, HBASE.  | Sahu
| Week 4 |  Iterative Processing |  Spark, RDD abstractions for in-memory computation; Spark Tachyon, a memory-centric distributed file system. | Sahu
| Week 5 |  Iterative (continued) + Stream Processing |  |   Sahu
| Week 6 |  Machine Learning Systems & Examples | Introduction to MLLib and/or other ML processing systems. | Industry guest.
| Week 7 |  Google's Storage Stack  | How core problems in distributed systems are solved in the real world. Design of Chubby, Bigtable, two fundamental components of a google cluster. High-level architecture of a Google cluster. | Sahu
| Week 8 |  Data Models and Cleaning |  Why the relational data model? Why schemas? The ins and outs. | Wu
|        |                           |  Readings: [What goes around comes around](https://github.com/w4111/syllabus/blob/master/reading/goesaroundcomesaround.pdf),  [Unified Logging@Twitter](https://cs.uwaterloo.ca/~jimmylin/publications/Lee_etal_VLDB2012.pdf) |
| Week 9 |  Cleaning and Integration  | Readings: [Truth finding on the deep web](http://www.vldb.org/pvldb/vol6/p97-li.pdf), [Data Wrangler](http://vis.stanford.edu/papers/wrangler) | Wu
| Week 10 |  Classic Query Processing and Fast Query Processing  | Reading: [C-Store](http://db.csail.mit.edu/projects/cstore/vldb.pdf), [Col vs Row Stores](http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf), [OLTP](http://nms.csail.mit.edu/~stavros/pubs/OLTP_sigmod08.pdf) | Wu
| Week 11 | Potourri  | Mixture of ideas: Graph analysis. Scalable visualization. Distributed transactions. | Wu
| Week 12 |  Distributed Systems Primer ([notes](http://columbia.github.io/systems-bigdata-class/lectures/ds-primer.txt))  | Challenges and principles, failure modes, inherent tradeoffs. | Sahu 
| Week 13 |  Communication and Synchronization Building Blocks | [Remote procedure calls, clock synchronization, logical clocks -- all building blocks for distributed algorithms.](http://columbia.github.io/systems-bigdata-class/2-lectures/)  | Sahu
|        |  (Notes: [RPC](http://columbia.github.io/systems-bigdata-class/lectures/rpc.txt), [clocks](http://columbia.github.io/systems-bigdata-class/lectures/clocks.txt), [mutual exclusion example](http://columbia.github.io/systems-bigdata-class/lectures/mutual-exclusion-example.pdf) (slides by Dave Andersen))  | |
| Week 14 |  Hard problems in Distributed Systems  |  Consistency, consensus, known impossibility results, approaches to navigate the challenges. | Sahu

