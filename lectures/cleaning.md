# Lecture 2: Cleaning and Integration

## Data Integration

Data prep/cleaning/integration is hard.  Why?

* highly domain specific in actual techniques
* ref zia's paper
* It's hard to even know what "cleaned" or "correct" even means

### History lesson

* 1990: retailers want to do market basket analysis
* consolidate sales, HR, products systems into a single reprresentation (global schema)
* load into warehouse to generat CFO/marketing reports
* Analysts run queries, learn customer preferences -- pet rocks are out, pogs are in
  * know to buy pogs and discount pet rocks
  * what kinds of queries are these?
* Pays for itself within a year through better buying and stock rotation decisions: 
  * everyone gets in on this late 90s early 00s
* OK, everyone wants data in their "data warehouse", and industry grows around this need (ETL)
* Does ETL work?
  1. Create global schema in advance (need to know what table you're dumping data into)
    * Remember the pain of creating a single table's schema?
  2. Send programmer to each data source (often different groups or companies!) to manually write connectors
    * everyone has their own "unique" data format: salary is in dollars vs pounds vs "wage".  Fixed vs per hour.
  3. write cleaning/transform scripts to convert before importing.  
* Scalability limitations (human scalability, not compute scalability) (crowdsourcing)
  1. Defining a global schema can take years -- by then, 2 years out of date
    * will never work unless schema stops changing. (is this realistic?) 
  2. Programmer per data source hard to scale.  
    * who does this job??
  3. fundamentally hard -- easy to underestimate data dirtiness
    * rule of thumb: ~10% of your data is incorrect
      * nicknames, codes, stale addresses (out of date), nulls, inconsistencies due to redundancy in schema design
    * dedup is contextual (contextual == hard)
      * ewu == Eugene Wu the billionaire == eugene wu@columbia == eugene wu at UBC?
      * Restaurants may have same address: but be in a foodcourt vs restaurant that took over an old one vs a moving restaurant (how can a global schema anticipate all this)
* Result? warehousing projects in 1990’s factor of two over budget and a factor of two late
* Still, fundamentally a win, so all CEOs want to add data sources
  * avg large enterprise has 5k data stores, only handful in warehouse

Beer vignette

         He had a typical data warehouse of sales of his products
         by brand, by distributor, by time period, etc. I told the
         analysts that El Nino was widely predicted to occur that
         winter and it would be wetter than normal on the west coast
         and warmer than normal in the Northeast. I then asked if
         beer sales are correlated to temperature or precipitation.
         They replied “I wish we could answer that question, but
         weather data is not in our warehouse”. Supporting data
         source scalability is very difficult using ETL technology.

But why not mandate a common schema?  That should be easy to do

* 2000s.  called Master data management

Mike's informix story

* New CEO asked HR VP "how many employees do we have?"
* She returned in a week "I don't know, and no way to find out".  Why?
* Informix operates in 58 countries, each with diff labor laws.
  * What does an employee _mean_?  Semantics matter, we will see in truthfinding
  * no golden database, would need to integrate all 58 data sources
  * informix doesn't even control all of them (partners, subsidiaries)
  * If master database not done early (not possible), may be impossible later

Why does this happen?

* Business agility: master databases and upfront schemas are not agile
  * If they said "here is the master database, conform", then they would spend months on that than making money
* Make $$ first.  Global schemas don't matter if you're broke
* This is not even the only reason!

Acquisitions

* Decentralized company -- 300 business units with their own purchasing systems
* Clearly, global system more efficient
  * enable global analysis -- supply chain
  * negotiate widgets as a large company than as individual units -- could save billions.
* Where do these "units" come from?  Acquisitions
* Godaddy purchased friend's startup
  * 2 years to get customer databases to match so a godaddy customer can _purchase their product_
  * it's exhausting work, and no one enjoys it :(


Lessons and Connections

* If you hear "integration", run
* Nature of the firm: Ronald Coase
  * Q: "Why and under what conditions should we expect firms to emerge?"
  * Why hire when you can contract?
  * A: transaction costs.
* Data on the ground moves faster than the global model.  What does this say about organizations?
  * Orders flow downward and can get lost/misinterpreted
  * Information flows up, but may not

### What is traditional integration?
 
What it is

* Ingest: find and dl data.  Parse into known structure 
* Transform: Euros to dollars, codes to names (naive rules, syntactic)
* Clean: find and fix errors (nulls, outliers, missing, wrong, etc)
  * how do people even know what's an error?
* Schema integration: wage == salary.  Not always a clean mapping
* Deduplication

Twitter unified logging paper

* ingest: removed parsing needs that broke analyses and created common format.
* transform: not needed with global schema.  Theri global schema was "learned".  Easier within a single hadoop system/company.
* clean: --
* integration: --
* deduplication: --

Ingest

* mainly parse and convert between file formats
* underappreciated!!  current analysis toolchains require using mulitple systems -- transforming for each tool is painful!
  * think about work to turn CSV or Excel into a dataframe
* hadoop used to write to disk as csv (3x replication), then read into next stage/system.
  * apache arrow standardizes for in-memory data structure 
  * yarn, etc systems working hard so next job can read in-memory data structures from previous job (containers)
* Protobuf/thrift standardize format within a company
* This is just formatting -- no semantics.  

Transforms

* Data wrangler/potter's wheel
  * simple structural transforms and extraction (regex)
  * current research focus is "interactive extraction"
* extraction, value filling
* no data semantics still

Cleaning

* are values _correct_?  What does that mean?
  * activeclean says correct is if the ML model improves
  * billing says correct means the value is exactly what it should be (debatable.  Customer may not agree)
* functional dependencies and automatic repairs
* outlier detection and pattern finding
  * hard -- domain specific
* explanation
* humans

Schema matching 

* Two data sources, how to combine into a single schema?

Dedup: clustering in high dimensions

* N^2 algorithm or worse

These are not complete, not disconnected, and can happen in any order.  But helpful categorization.



# Data Transformation

Wrangler

* descendant of potter's wheel work from databases
  * pretty much coined/popularized the term "data wrangling".
* tool for cleaning and reformatting datasets
* don't need to write code to clean data
  * you are a business analyst that can use Excel, not python.
  * you want to get things done, not wait for IT
* direct manipulation
  * click on line of text, select what you want, Wrangler learns a template for transforms to apply to make it happen
  * "programming by example"
* Key ideas
  * interactivity

            data cleaning requires LOOKING at the data,
            hard to do if relying on scripts and print statements
            bring (lift) the scripting into the visual domain, 
            so users can do what they do best.
  
  * preview what actions will do (so you can decide quickly)
  * recommendations/synthesis

            multiple ways ofsaying "heavy rain": HEAVY rain, Heavy Rain, Moderate RAIN
            just provide examples, let system figure it out


  * transformation language.  Synthesis == generate program in the language
* Languages are good.

### 3 core operator types

Map: take X, convert to X'

* **cut** some text from a string
* **edit** convert text to other text
* **delete** cut data with a condition
* **extract, split, merge**

Restructure: change structure of data

* **transpose**: table value Aij becomes Aji

          A B      A | 1
          ---  -->
          1 2      B | 2

* **Drop** column
* **wrap** formatting
* **fold**: data turns into attributes (confusing)

          city1 | 2001 | 56
          city1 | 2002 | 70 
          city2 | 2001 | 45
          city2 | 2002 | 20

          # fold year onto city

                2001  2002
          city1  56    70
          city2  45    20

* **unfold** attributes turn into data

Position operators (non tranditional from DB perspective)

* **fill** copy data from one cell to others
* **translate** shift row left or right
* **promote** turn a row into the schema
* **sort** reorder

Once done wrangling, export the wrangled data, or a script to run on larger dataset (trifacta's value prop)

Homework was to play with it and form opinions

* what does it make easy?
  * simple pattern extraction
* What is hard to do?
  * complex conditions, multi-structural-step transforms
* is the interface "discoverable"?
* what do you think it's most useful for?
  * simple parsing scripts


Given your homework, what tools _would_ you like?


# Data Source Integration

Truth finding on the deep web

What do we know?

* aggregating data from sources on the web is nice but hard.  But _how hard_?  Unclear in terms of quantifying before this paper
* What is the "deep web"?
  * HTML is not written by hand anymore, generated from data.
  * DBMS -> webapp -> HTML string -> browser
  * a webpage is a "view" over a database.
  * We see the browser, but deepweb is the dbms
* Luna looks at 2 domains that you would think would be clean: flights and stocks
  * search on google/yahoo for keywords (e.g., flights, stocks)
  * pikcs top pages, extracts their sources via crawling
    * federal aviation administration, AA website

The setup

* data model
  * object: a flight, a stock
  * attr/data item: takeoff time, duration, departure gate, etc
  * for given object's attr, single true value (debatable!  but fair assumption)
* Sources provide subset of objects and attributes
* sources can differ in three ways
  * schema: structure/attrs differ
  * instance: objects identified (pkeys) using different attrs (id vs name+company)
  * value: true values, diff value, diff format, wrong, missing, etc
* too  many issues! paper fixes schema and instance, only focus on value

### The Sources

Stock

* 55 sources
  * search "stock price quotes", "AAPL quotes" and find deep-web sources of top 200 results
  * 89 sources total, 76 use GET methods, 55 crawlable (others use JS/reject crawling)
  * 1000 stocks: 30 from dow, 100 from nasdaq, 873 random from russel 3000
  * crawl once a day during July after market close
  * object: stock on day X
* attrs
  * 3-71 attrs per source; 333 total (local attrs); 153 after manual matching (global attrs)
  * distribution follows zipf's law
  * (21) 13% provided by 1/3 of source; picked 16 of them to study.
* Performed data cleaning e.g., 6.7M = 6700000 = 6,700,000
* picked 5 popular sources, voted to pick gold standard values for 200 symbols

Flight dataset

* 38 sources, 1200 flights from AA, UA, Continental hub airports
* crawl every day in Dec
* object: flight on day X
* 43 local, 15 global, 4-15 attrs per source
* 6 (40%) attrs in 50% of sources; used those
* 3 airline websites on 100 flights as gold

### The Data

Redundancy

* Stocks have high coverage
  * all sources provide 90% of stocks
  *  50% sources have all stocks 
* Flights
  * 36% sources cover 90% flights; 50% flights in 60% sources
  * 28% sources provide 50% attrs; 29% attrs in 50% sources
* small # extremely common/rare attrs, most are found in small number of sources (fat tail)

Are values consistent?

* What are possible metrics?
  * # values
  * entropy: higher entropy --> higher inconsistency
  * dominant value D: val found in most sources
  * deviation from dominant value (std, but use dominant instead of mean. why?)
  * how dominant: % sources with dominant val D
  * are dominant values == gold?
* fundamentally what are these metrics measuring?
  * disagreement!  variety and spread of values
  * f(distribution of values)
* stocks
  * 3.7 vals/attr
  * 17% attrs have 1 value (37% if exclude a bad data source); 30% have 2 values.
  * valuues seem to be similar
    * low deviation and entropy.  
    * Suggests data is pretty similar. (one would hope so for stocks!)
  * realtime values have less inconsistency than statistics -- more semantic ambiguity with statistics (see below)
* flights
  * 1.45 vals/attr
  * 61% attrs have 1 val; 93% have <= 2 vals
  * large deviation in some attrs such as departure times (~15minutes off)

Why the inconsistency?

* Semantics (46% cases): dividend computed for year or quarter?  Market cap? Yield?
* Instance ambiguity (6%): stock symbol interpreted incorrectly (stock was terminated)
* Out of date (34%) stale data
* Data units (1 error): 76"B" instead of 76"M"  (billion instead of million!)
* Wrong data (11%)
* Stock data saw all types of inconsistency, flights saw semantic, out of date, and pure errors (56% cases)

### Does dominance work?  Can I take majority vote and call it a day?

Stock

* 42% attrs of dominant vals supported by >90% sources 
* dominance factor seems correlated with precision: 90% if in 50% sources
* 90% overall

Flight

* lower inconsistency (higher dominance factor), lower precision
* 80% prec at 60% dominance factor.  Big dip at 50% due to copying
* 85% overall

Very high dominance is usually correct.  Precision quickly drops when dominance decreases

Are sources accurate?  (% of its values are gold) (Figure 7)

* stocks: 
  * 86% average
  * 35% have 90% acc.
  * authoratative sources: 83-90%
* flight
  * 80% avg
  * 40% sources > 90% acc
  * authoratative sources: 71-90%

Data copying

* why is this bad?  skews voting scheme. ballot stuffing 
* copynig everywhere:
  * partnerships
  * redirect queries to third party
  * iframes
  * objects/attrs almost identical
* accuracy of copied source varies!
  * stock 75-92% 
  * flight 50-90%
* copying from bad sources?  why?
* removing copied sources helps dominant values (majority vote) a lot!


### Data Fusion

Compare 15 approaches from research to majority vote scheme. Categories

* Web-link based: page rank on source 
  * (node = source, edge if share a value)
* Information retrieval: similarity measures
  * each value is 1,0,-1 vector.  one val for each source
  * 1 if source provides the value, -1 if it provides different value, 0 otherwise
  * seed with set of true values
* Bayesian
  * accuXXX methods.  fancy
* copy-aware: discount copying

All variations of voting basically

* iterative algorithms
  * source quality proportional to agreement with others
  * weigh in majority vote is the quality
  * iterate between source quality and majority vote until converge
* taking into account
  * trustworthiness (bootstrap by labeling some sources with quality)
  * difficulty of attributes
  * similarity and formatting of values (recall values were preprocessed for this paper)
  * copying (identified manually)

High level results

* majority vote < best source < best fusion
  * having best sources important (50% flight errors due to trustworthiness)
  * picking fusion method matters [not a promising result :( ]
* table 9:
  * stock:  vote: 92%;  accuformatter: 94%;  accucopy: 88%
  * flight: vote: 88%;  accuformatter: 95%;  accucopy: 98%
  * accucopy bad for stock, best for flight
* trustworthiness: learning a bayesian prior on which source is best is helpful 
* bias: learning which sources copy from one another is helpful 
* most accurate methods are slowest by factor of 1000x (fig 12)
* no one fusion method that wins 
* fusing small number of good sources >> fusing all sources

Takeaways

* unique slowflake: every ource has its own attriutes of interest.  has its own values for those attributes
* learning the best source matters
  * why nielson/bloomberg/reuters make money
* combining sources, even simple majority vote, helps
* trade off improved accuracy for algorithmic efficiency
* no best algorithm (recall the data cleaning challenges from beginning of lecture?)
* small number of good sources usually good enough! (positive result)


