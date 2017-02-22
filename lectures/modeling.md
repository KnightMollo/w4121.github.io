---
layout: page
---

## Exercise 

Let's store data for some application

* What application?
* XML/hierarchitacl data
* Relational data

### XML/Hierarchitacl 

Means many things

* Data model -- discuss IMS
* Physical encoding -- that's fine
* "Schema on read": figure out the schema when actually read the data
  (vs schema on write: need to write data that conforms to schema)
  * Just projection on sparse schema

Let's try to model something using XML

        # default option:
        cages --(livesin)-- animals --(cares for)-- keepers

        animals(frog, c1, k1)
        animals(frog, c1, k2)
        animals(toad, c2, k1)

        # in json

        k1:
          cares: 
            1: frog:
              name: bob
              livesin: 
                c1:
                  name: cage 1
                  size: 100 sqft
            2: toad:
              name: jane
              livesin:
                c2:
                  name: cage 2
                  size: 10 sqft
        k2:
          cares: 
            1: frog:
              name: bob
              livesin: 
                c1:
                  name: cage 1
                  size: 100 sqft
        
            

* In general, not that many options:

          keepers --> animals --> cages
          keepers --> cages --> animals
          .. and other combinations ...

* Let's query it
  * propose some normal queries and try to write the query
    * find keeprs that care for frogs
* Dive deeper -- how do you STORE and process hierarchical data?
  * how do we actually store the tree above?
* What's the problem?
  * schema changes?
  * redundancy issues
    * update consistency (change c1's name)
    * insert anomaly (add animal without cage/keeper?)
    * delete anomaly (if we delete frog, then does k2 disappear? what if I delete k2?)

* Other issues:
  * Guarantees (constraints) you would like to have
    * node types
    * attribute types
    * foreign keys
    * cardinality constraints?
    * redundancy?
* mention Document Type Definitions (DTDs)


History

* used to be called XML, now JSON
*  Some hypotheses
  * The boiling toad: 
    * easy to think about for simple data, hen data get's complex over time
    * fast to write programs
  * Compatibility
    * Lots of important programs take trees as input: browsers
    * Querying node types (e.g., CSS selectors) is not terrible (but it's an impoverished language)


### Relational Model

Walk through example app


What do data models offer above and beyond .csv files?

* access language: relational model has things like sql
* relationships: how do different types of data relate to one another (e.g., employees in a department)?
* constraints/consistency: how do you enforce certain things that are true about the data (e.g., parents older than kids, etc.)


Data independence

* idea: change the representation of data w/o changing programs that operate on it.
* Physical data independence: I can change the layout of data on disk and my programs won't change
  * index the data
  * partition/distribute/replicate the data
  * compress the data
  * sort the data
* Logical data independence: I should be able to change the schema without changing my model.  Add a field.  Delete a field.  Etc..
  * This is accomplished using views in sql

Some history

* IMS (hierarchical)
  * 1968
  * for apollo program (saturn V) to manage the supplies/parts
  * schema chancges --> program changse --> most time spent maintaining the app code
    * but schemas change _all the time!_  note twitter and hashtags.
  * only runs on z?os
  * top 5 european and top 5 US banks run IMS,
* Network model (1970) -- even more complicated
  * programmers wrote low level optimized app code (no physical independenc)
* Relational model (1970) drawbacks:
  * Ted Codd@IBM
  * people didn't know if you could take relational model (theory), throw a declarative language on top of it, and provide a high-performance implementation.
  * optimizers won out -- don't bet against compilers!


        IBM’s signal that it was deadly serious about relational
        systems was a watershed moment. First, it ended once-and-for-all
        “the great debate”. Since IBM held vast marketplace power
        at the time, they effectively announced that relational
        systems had won and CODASYL and hierarchical systems had
        lost. Soon after, Cullinaine and IDMS went into a marketplace
        swoon. Second, they effectively declared that SQL was the
        de facto standard relational language. Other (substantially
        better) query languages, such as QUEL, were immediately
        dead. For a scathing critique of the semantics of SQL,
        consult [DATE84].

        # note project eagle: SQl interface on IMS is the obvious
        # way to go.  IBM actually tried this, but it failed, so they went
        # the dual database strategy with DB/2

        Lesson 9: Technical debates are usually settled by the elephants of the 
        marketplace, and often for reasons that have little to do with the technology.


How to represent the data as relations?  Three tables:

        animals(name, cid, kid)
        keeper(kid, name)
        cages(cid, size)

        # is this enough? no fkeys

Relational is not perfect

* schema up front -- sometimes not realistic (see twitter)
* change schemas is painful (why? does it have to be?)
* set oriented may not always be good -- streaming, scientific


## Twitter Unified Logging Infrastructure

Now to argue for the value of shared schemas.

Problem

* ~100 TB uncompressed/day
* 10Ks production servers
* originally logging was write optimized
  * each team made up their thrift schema and used it -- fast dev cycles
  * reads (esp across teams -- for a data scientist) is very hard!  (walk through example)
* Extract a common schema from twitters many teams
* Allow extensibility

Overall analysis pipeline

                twitter page ---------> group by session ------------> analysis
                               click                       compress
                              view pg

Scribe

* Similar to flume, kafka.  logging system.  Not realtime aka Heron/Storm
  * it logs to HDFS and batch processes logs later
* message:  [ category (metadata) | message string ]
  * categories allocated by groups/apps/teams.  
  * `geoIPhoneV7 | { Time: ..., UserName: ..., id: ..., action: 'click link', linkurl: ...,  }`
  * why is this dangerous?  teams change, schemas evolve.  No one remembers why the schema is what it is.
    * multiply by # teams
  * What's a team?
    * Geo, home page, side bar, ios, search, etc
* Zookeeper tracks aggregator locations
  * ZooKeeper has a file system abstraction
  * an aggregator is basically a client session's server that receives log messages
  * aggregate lists itself in the file system, and Scribe daemons find live aggregators and read from them
* Aggregator takes all streams  for same category, merges, compresses, and stores on staging HDFS
  * eventually bulk moved to main hadoop data warehouse
  * files in warehouse are ordered, but contents within files are potentially arbitrary
* Hadoop/Pig jobs on Hadoop logged data


                Scribe daemons --(read from)--> Aggregator ----> HDFS ----------> Hadoop data warehouse
                                                                        per hr   /logs/cat/YYYY/MM/DD/HH
                                                                        window
* Data scientists

                Devs ---> logs --> HDFS  <------------------- Data scientists
                                           find useful data
                                            interpret data


Challenges

* Simple queries "# events of each type yesterday" is hard
  * no consistent timestamp schema
  * what's an event type?  not consistent
* Any error (say, different delimiters) could result in garbage or no results (long debug cycle)
* even common primitives (tstamps) were named differendly
  * Stylistically: CamelCase, smallCamelCase, snake_case, camel_Snake)
  * Syntactically: uid, userid, UserId
  * tab/space/colon/delimters
* Each team uses a custom schema
  * Across N teams, up to N^2 schema-schema xforms possible
* Resource discovery problem -- categories named adhoc
* Format differences -- Thrift, json, mix
  * JSON: which fields are required, what types, nullable? How to query?
    * used for rich event info: tweet impressions, link click-throughs, etc.
  * Analysts often need to read front-end code to understand the schema!
* Documentation always out of date
  * other developers (including future you) don't understand
  * new employees can't figure out where to find data or how to use it (rely on emailing around)

Core issue

* Goal is actually to analyze sessions
* Even if found all scribe categories (message types), joining them into a SINGLE user session is impossibl
  * e.g., user searched, scrolled two pages of results, clicked on a link.
  * JOIN on user_id, GROUP BY <grouping of interest> ORDER BY time
  * what if a team forgot an attribute?

Note!

* Relational vs JSON does not solve this issue
* If relational, still have O(# teams) different schemas to find and understand

Solution

* Centralized mandate for consistency by enforcing schema at library/API level
* Contrast with DBMS where data and schema always together
* Enables a common denominator dashboard for non-tech users

Unified Naming

* hierarchical event naming `(client, page, section, component, element, action)`
  * e.g., `web:home:mentions:stream:avatar:profile click`
  * analyze via query: (android, ALL, ALL, ALL, ALL, click)
* Common set of fields
  * client, server, user, app, event_name, uid, sessionid, ip, tstamp
* Catch all *event_details* field

Session Sequences

* most analyses were on sessions, so every new dataset would generate many jobs to group by session/uid to create the sequences (redundant)
* created a unified copy of session sequence data
  * key: session id + uid
  * val: oredered sequence of event names
  * drop the message payload
* compress the heck out of it
* good enough for most analytics, CTR, follow-through rate, and funnel analysis


