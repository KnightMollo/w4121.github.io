---
layout: page
---




## Twitter Unified Logging Infrastructure

* ~100 TB uncompressed/day
* 10Ks production servers
* Extract a common schema from twitters many teams
* Allow extensibility

Overall analysis pipeline

                twitter page ---------> group by session ------------> analysis
                               click                       compress
                              view pg

Scribe

* Similar to flume, kafka.  logging system.  Not realtime aka Heron/Storm
* message:  [ category (metadata) | message string ]
  * categories allocated by groups/apps/teams.  
* Zookeeper tracks aggregator locations
* Aggregator takes all streams  for same category, merges and stores on HDFS
* Hadoop/Pig jobs on Hadoop logged data


                Scribe daemons ---> Aggregator ----> HDFS ----------> Hadoop data warehouse
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
* Any error could result in garbage or no results (long debug cycle)
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
  * Often need to read the code to understand the schema!
* Documentation always out of date
  * other developers (including future you) don't understand

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


