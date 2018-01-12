---
layout: index
title: Overview
---

<p class="message" align="center">
  <i>Note: This entire website is still under construction. 
  <br/>Anything can change until the beginning
of the semester, so check again soon. </i>
</p>


## Class Overview


An introduction to large-scale distributed systems with an emphasis on big-data processing and storage infrastructures. Topics include fundamental tradeoffs in distributed systems, techniques for exploiting parallelism, big-data computation and storage models, design and implementation of various well-known distributed systems infrastructures, and concrete exposure to programming big-data applications on top popular, open-source infrastructures for data processing and storage systems.  

The course is co-taught by Roxana Geambasu (Assistant Prof. in CS), Sambit Sahu (IBM TJ Watson researcher and CS affiliated faculty), and Eugene Wu (Assistant Prof. in CS). Geambasu will teach fundamental concepts of distributed systems, along with the tradeoffs that arise. Sahu will teach various distributed computation models, along with concrete examples of open-source big-data technologies and how they can be programmed. Wu will teach concepts of data modeling, storage, and visualization, along with the tradeoffs they raise.





## Schedule

* 1/16: [Introduction](./lectures/lec1.pdf)    (all)
  * Why not single machine? 
  * Big-data challenges, datacenter structure, typical use cases and their requirements. 
  * Course overview. 
* 1/23:  Data Models and Cleaning  (Wu)
  * Why the relational data model? Why schemas? The ins and outs.
  * Readings: [What goes around comes around](https://github.com/w4111/syllabus/blob/master/reading/goesaroundcomesaround.pdf)     
    [Unified Logging@Twitter](https://cs.uwaterloo.ca/~jimmylin/publications/Lee_etal_VLDB2012.pdf) 
* 1/30:  Cleaning and Integration (Wu)
  * Readings: [Truth finding on the deep web](http://www.vldb.org/pvldb/vol6/p97-li.pdf)     
    [Data Wrangler](http://vis.stanford.edu/papers/wrangler) 
* 2/06: [Classic Query Processing and Fast Query Processing](https://w4121.github.io/lectures/qproc-primer) (Wu)
  * Reading: [C-Store](http://db.csail.mit.edu/projects/cstore/vldb.pdf)        
    [Col vs Row Stores](http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf), <br/> [OLTP](http://nms.csail.mit.edu/~stavros/pubs/OLTP_sigmod08.pdf) 
* 2/13: Potourri(Wu)
  * Graph analysis/Scalable vis/ML 
  * Readings: [ML](http://www.cs.stanford.edu/people/chrismre/papers/bismarck.pdf) [in DBs](http://db.cs.berkeley.edu/papers/vldb09-madskills.pdf)   
    [Graphs in DBs](http://pages.cs.wisc.edu/~jignesh/publ/Grail.pdf)      
    [Viz in DBs](http://sirrice.github.io/files/papers/ermac-vldb14.pdf) 
* 2/20:  
* 2/27: 
* 3/06: 
* 3/13: NO CLASS.  Spring Break!
* 3/20:
* 3/27: 
* 4/05: Basics (Sahu)
  * HDFS, Hadoop basics 
* 4/10: Batch Processing (Sahu)
  * MapReduce: 
* 4/17: Batch Processing (Sahu)
  * Map Reduce additional details with more complex examples, HBase, Hive 
* 4/24:  Iterative Processing  (Sahu)
  * Intro to Spark, Spark programming 
