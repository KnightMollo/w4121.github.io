---
layout: page
---

## W4121: Non-graded Quiz Solutions


<a name="lec2"></a>
### Lec2: Data Modeling


#### Q1: Data Independence

1. data independence separates how data is stored (csv, binary, row oriented, col oriented, json, etc) from how users/application access, query, and manipulate the data.
1. in very common situations, there is no way to store the data without redundancy. Redundancy is bad because data can easily become inconsistent.  The hierarchical model also made it difficult to query the dat: in IMS, programmers had to write low-level programs to "walk" the hierarchical data structure.
  1. the animals, cages, feeders example from lecture.
  1. if the data is fundamentally hierarchical in nature, where the hierarchy can be deep   e.g., the browser DOM.
1. the graph model tried to solve the redundancy problem in the hierarchical model.  it didn't solve the need to write low-level programs. In fact, it became HARDER to write querying programs because now they needed to walk a complex graph!


#### Q2: Queries

Queries in english

* get feeding records (all columns) where feeding time was before noon
* get feeding records (all columns) where feeding time was before noon and the amount fed was larger than 10 pounds
* get names of all animals (note they will be unique since relational algebra is set oriented)
* get species of all animals (note they will be unique since relational algebra is set oriented)
* get all keeper and feeding attributes where the id of the keeper that performed the feeding is the same as the keeper's id.
* get all keeper and animal attributes where the id of the keeper that performed the feeding is the same as the animal's id.  (it is kind of non-sensical)
* get the total pounds and number of feedings for each food in `feedings`.

Note: relational algebra is a language over **sets**, which is why I emphasized uniqueness.  In practice, SQL is a language over bags (sets that allow duplicates), which is why when you run `SELECT name FROM animals`, you may see the same name twice.


Operator symbols

* filter: sigma
* project: pi
* join: bowtie
* groupby: gamma


Describe in english

* get all foods that have been fed to animals at exactly noon
* get the name of all gorillas that have been fed at exactly noon


#### Q3

1. Even though the events had a schema, why did data scientists still have trouble analyzing logging data?  
  * Every organization created their own schema.  Although each event contained the same data, they were named and represented differently.  In other words, there was no global schema.  From the perspective of the data scientist trying to "query" over all of the event data throughout twitter, there was no physical independence between the event data (and how they were stored), and how the event data was accessed.
  * It wasn't clear from the very beginning what data scientists would even want to analyze.  This data integration problem could have been trivially solved by not building features and going out of business.
1. *Automatically* enforce a global schema that addresses what most data scientists want, while making it easy to continue to customize event data, so that teams can continue to make progress.




