---
title: "Path to Cypher Query tuning"
datePublished: Thu Oct 27 2022 11:08:04 GMT+0000 (Coordinated Universal Time)
cuid: cldr998ei026uxunvh2v9g9m4
slug: path-to-cypher-query-tuning

---

What are the things to learn to be able to tune cypher queries

1. Preparing for Query Tuning
    
2. How queries work in Neo4j [here](https://neo4j.com/graphacademy/training-cqt-40/01-cqt-40-how-queries-work-in-neo4j/)
    
3. Controlling Row Cardinality
    
4. Neo4j Behind the Scenes
    
5. Optimizing Property Access
    
6. Node Degree Shortcuts
    
7. Monitoring Running Queries
    

you should be able to:

* Define the terms row and DB hit in the context of Cypher querying [cypher-cardinality](https://neo4j.com/developer/kb/understanding-cypher-cardinality/)
    
* Use EXPLAIN and PROFILE to identify weaknesses in a query plan
    
* Use Cypher tools to minimize the number of rows processed in a query
    
* Use best practices for minimizing property access
    
* Use monitoring tools to identify the underlying causes of a long-running query [1](https://neo4j.com/labs/halin/) [2](https://github.com/moxious/halin)
    

Resources to get learn the above topics

* [Lesser Known Features in Cypher](https://www.youtube.com/watch?v=BN5T8IimB78)
    
* [Tuning Cypher](https://www.youtube.com/watch?v=QnozzFP_fPo)
    
* [Best practices for queries that can take hours to complete](https://community.neo4j.com/t5/neo4j-graph-platform/best-practices-for-queries-that-can-take-hours-to-complete/m-p/27305)
    
* [5 Secrets to More Effective Neo4j 2.2 Query Tuning](https://neo4j.com/blog/neo4j-2-2-query-tuning/)