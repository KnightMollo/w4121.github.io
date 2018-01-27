---
layout: page
---

## W4121: Non-graded Quiz,  Wu's Lectures

Answers will be posted around end of February.

<a name="lec2"></a>
### Lec2: Data Modeling

The point of data modeling is to think about what characteristics of the data you will need for your application.

#### Q1: Data Independence

1. What is data independence and why does it matter?
1. What are the main two reasons why hierarchical data model is a bad idea?
  1. Give an example that illustrates the bad idea.
  1. When could it make sense to use a hierarchical data model?
1. What did the graph model try to solve?  What limitations did it still have?


#### Q2: Queries


Suppose our data adheres to the following schema

        animals(id, species, name, gender, keeper_id)
        keepers(id, name, birthday)
        feedings(keeper_id, animal_id, date, time, food, pounds)

Describe in english what each of the following operations will do:

* filter(feedings, time < 12pm)
* filter(feedings, time < 12pm and pounds > 10)
* project(animals, [name])
* project(animals, [species])
* join(feedings, keepers, keeper_id = id)
* join(animals, feedings, keeper_id = id)
* groupby(feedings, [food], SUM(pounds), COUNT(pounds))

What are the operator symbols (greek symbols) for the above operations?

Describe in english what the following operations do:

* Π<sub>food</sub> σ<sub>time=12pm</sub>(feedings)
* Π<sub>name</sub> (σ<sub>time=12pm</sub>(feedings) ⋈<sub>id=animal_id</sub> σ<sub>species=gorilla</sub>(animals))


#### Q3: Logging

We have seen that having a schema is helpful because then data can be easily queried.  Before the solution described in the paper, Twitter's event messages DID adhere to a schema of `(category, message)`.  

1. Even though the events had a schema, why did data scientists still have trouble analyzing logging data?  
  * What was the source of this trouble?
  * Why do you think Twitter let this happen?  Couldn't they have prevented it from the very beginning?
1. What was the main solution to address the above troubles?