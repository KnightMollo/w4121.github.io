---
layout: page
title: Lectures
---

<p class="message" align="right">
  <i>Note: This schedule is in flux at the moment! </i>
</p>


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
| Week 1 1/18 |  [Introduction](./lectures/lec1.pdf)   |  Why not single machine? Big-data challenges, datacenter structure, typical use cases and their requirements. Course overview. | All
| Week 2 1/25 |  Basics |  HDFS, Hadoop basics  | Sahu
| Week 3 2/01 |  Batch Processing | MapReduce | Sahu
| Week 4 2/08 |  Batch Processing ctd |  Map Reduce additional details with more complex examples, HBase, Hive | Sahu
| Week 5 2/15 |  Iterative Processing | Intro to Spark, Spark programming |   Sahu
| Week 6 2/22 |  Data Models and Cleaning |  Why the relational data model? Why schemas? The ins and outs. | Wu
|        |                           |  Readings: <br/>[What goes around comes around](https://github.com/w4111/syllabus/blob/master/reading/goesaroundcomesaround.pdf), <br/> [Unified Logging@Twitter](https://cs.uwaterloo.ca/~jimmylin/publications/Lee_etal_VLDB2012.pdf) |
| Week 7 3/01 |  Cleaning and Integration  | Readings: <br/>[Truth finding on the deep web](http://www.vldb.org/pvldb/vol6/p97-li.pdf), <br/> [Data Wrangler](http://vis.stanford.edu/papers/wrangler) | Wu
| Week 8 3/08 |  [Classic Query Processing and Fast Query Processing](https://w4121.github.io/lectures/qproc-primer)  | Reading: <br/>[C-Store](http://db.csail.mit.edu/projects/cstore/vldb.pdf), <br/> [Col vs Row Stores](http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf), <br/> [OLTP](http://nms.csail.mit.edu/~stavros/pubs/OLTP_sigmod08.pdf) | Wu
| Week 9 3/15 | NO CLASS.  Spring Break!
| Week 10 3/22 | Potourri  | Wu's goodbye tour: Graph analysis. Scalable visualization. ML. Distributed transactions(?) | Wu
|        |                           |  Readings: <br/>[ML in DBs](http://vldb.org/pvldb/vol5/p1700_joehellerstein_vldb2012.pdf), <br/> [Graphs in DBs](http://pages.cs.wisc.edu/~jignesh/publ/Grail.pdf)<br/>[Viz in DBs](http://sirrice.github.io/files/papers/ermac-vldb14.pdf) |
| Week 11 3/29 |   | | Sahu
| Week 12 4/05 |   | | Sahu 
| Week 13 4/12 |   | | Sahu
| Week 14 4/19 |   | | Sahu
| Week 15 4/26 |   | | Sahu
| Week 16 5/03 | [Poster Presentation](./proposals#poster) + [Submit Writups](./proposals#report)  | | Sahu

<!--
| Week 11 |  Google's Storage Stack  | How core problems in distributed systems are solved in the real world. Design of Chubby, Bigtable, two fundamental components of a google cluster. High-level architecture of a Google cluster. | Sahu
| Week 12 |  Distributed Systems Primer ([notes](http://columbia.github.io/systems-bigdata-class/lectures/ds-primer.txt))  | Challenges and principles, failure modes, inherent tradeoffs. | Sahu 
| Week 13 |  Communication and Synchronization Building Blocks | [Remote procedure calls, clock synchronization, logical clocks -- all building blocks for distributed algorithms.](http://columbia.github.io/systems-bigdata-class/2-lectures/)  | Sahu
|        |  (Notes: [RPC](http://columbia.github.io/systems-bigdata-class/lectures/rpc.txt), [clocks](http://columbia.github.io/systems-bigdata-class/lectures/clocks.txt), [mutual exclusion example](http://columbia.github.io/systems-bigdata-class/lectures/mutual-exclusion-example.pdf) (slides by Dave Andersen))  | |
| Week 14 |  Hard problems in Distributed Systems  |  Consistency, consensus, known impossibility results, approaches to navigate the challenges. | Sahu
-->
