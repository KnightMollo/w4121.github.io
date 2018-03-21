---
layout: index
title: Overview
---

## Class Overview

An introduction to large-scale distributed systems with an emphasis on big-data processing and storage infrastructures. Topics include fundamental tradeoffs in distributed systems, techniques for exploiting parallelism, big-data computation and storage models, design and implementation of various well-known distributed systems infrastructures, and concrete exposure to programming big-data applications on top popular, open-source infrastructures for data processing and storage systems.  

The course is co-taught by Roxana Geambasu (Associate Prof. in CS), Sambit Sahu (IBM TJ Watson researcher and CS affiliated faculty), and Eugene Wu (Assistant Prof. in CS). Geambasu will teach fundamental concepts of distributed systems, along with the tradeoffs that arise. Sahu will teach various distributed computation models, along with concrete examples of open-source big-data technologies and how they can be programmed. Wu will teach concepts of data modeling, storage, and visualization, along with the tradeoffs they raise.


## Updates

* Added student-written lecture notes for:
  * [relational model](./files/notes/lecture_notes_1.pptx). Direct your thanks to Kathy Lin (kl2615), Xiaohui Guo (xg2225), Aria Kumar (sk4345)
  * [query processing + optimization](./lecture_notes_2.pdf).  Direct your thanks to Yijia Chen (yc3425), Haotian Zeng (hz2494), Yiwen Zhang (yz3310)
* Added [non-graded quiz solutions](./quiz_sol)
* Added link to [non-graded quiz](./quiz)

## Schedule

{:.schedule}
* 1/16: [Introduction](./lectures/lec1.pdf)    (all)
  * Why not single machine? 
  * Big-data challenges, datacenter structure, typical use cases and their requirements. 
  * Course overview. 
* 1/23:  Data Models and Cleaning  (Wu)
  * Why the relational data model? Why schemas? The ins and outs.
  * Optional Readings: <small>Will introduce these in class</small> 
    * [What goes around comes around](https://github.com/w4111/syllabus/blob/master/reading/goesaroundcomesaround.pdf)     
    * [Unified Logging@Twitter](https://cs.uwaterloo.ca/~jimmylin/publications/Lee_etal_VLDB2012.pdf) 
  * [Non-graded Quiz](./quiz#lec2)
* 1/30:  Cleaning and Integration (Wu)
  * Optional Readings:<small>Will introduce these in class</small> 
    * [Truth finding on the deep web](http://www.vldb.org/pvldb/vol6/p97-li.pdf)     
    * [Data Wrangler](http://vis.stanford.edu/papers/wrangler) 
* 2/06: Classic Query Processing and Fast Query Processing (Wu)
  * Optional Reading:<small>Will introduce these in class</small> 
    * [C-Store](http://db.csail.mit.edu/projects/cstore/vldb.pdf)        
    * [Col vs Row Stores](http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf)
    * [OLTP](http://nms.csail.mit.edu/~stavros/pubs/OLTP_sigmod08.pdf) 
    * [Code Generation in Spark](https://databricks.com/blog/2016/05/23/apache-spark-as-a-compiler-joining-a-billion-rows-per-second-on-a-laptop.html)
* 2/13: Potourri (Wu)
  * Graph analysis/Scalable vis/ML 
  * Optional Readings:<small>Will introduce these in class</small> 
    * [ML](http://www.cs.stanford.edu/people/chrismre/papers/bismarck.pdf) [in DBs](http://db.cs.berkeley.edu/papers/vldb09-madskills.pdf)   
    * [Graphs in DBs](http://pages.cs.wisc.edu/~jignesh/publ/Grail.pdf)      
    * [Viz in DBs](http://sirrice.github.io/files/papers/ermac-vldb14.pdf) 

* 2/20: [Scaling and fault tolerance: challenges and techniques](./lectures/ds-primer.pdf) (Geambasu)
  * Failure models in large-scale distributed systems, consistency and coherence challenges, scaling challenges
  * Sharding and replication as the key techniques for scaling and fault tolerance.
  * Assigned reading: [RFC 667](https://columbia.github.io/ds2-class/papers/johnson-rfc677.pdf), 1975
* 2/27: [Distributed transactions on sharded databases](./lectures/transactions-primer.pdf) (Geambasu)
  * Two-phase locking, write-ahead logs
  * Two-phase commit
* 3/06: Replication architectures and protocols (Geambasu)
  * Primary-secondary architectures, chain replication, leader election protocols
  * Consistency and the ordering of events in a distributed system. Importance of time.
* 3/13: NO CLASS.  Spring Break!
* 3/20: The design and implementation of a scalable, fault tolerant storage system: Google's Spanner (Geambasu)
  * Reading/video: [Spanner](https://research.google.com/archive/spanner.html)

* 3/27: Distributed computing models (Sahu)
  * HDFS, Hadoop basics
  * MapReuce Programming Model
  * AWS EMR and MapReduce
* 4/03: Batch processing (Sahu)
  * MapReduce programming with more complex examples
  * HBase, Hive 
* 4/10: Iterative and Stream Processing  (Sahu)
  * Intro to Spark, Big Data Architecture and Spark
  * Spark programming
* 4/17: FINAL QUIZ
* 4/24: Advanced Spark Programming (Sahu)
  * Advanced Spark Programming
  * SparkQL, Spark Streaming, Machine Learning with Spark
  * End-to-end Intelligent System design with Spark
