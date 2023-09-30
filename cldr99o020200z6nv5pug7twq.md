---
title: "DynamoDB Expressions"
datePublished: Thu Sep 09 2021 19:28:00 GMT+0000 (Coordinated Universal Time)
cuid: cldr99o020200z6nv5pug7twq
slug: dynamodb-expressions

---



As almost every developer has worked with Relational (Mysql,Postgres,etc) and No-SQL (MongoDB) databases, and over the time has developed the intuition for writing and execution of CRUD operations queries for these databases. DynamoDB breaks this intuition in many ways.

 

Lately, I have been working on a project which has DynamoDB as its Database. And like most of the developers, I searched for insert, update and delete queries and started writing the DynamoDB queries with the intuition of  Mysql, Postgres, MongoDB. 

I was able to write basic queries but slowly I started to realise that I am struggling to understand the execution of queries. And then I found the need to go back to Basics of query writing in DynamoDB and that was **Expressions**.



Before Moving to Expression Let understand the Jargons in Dynamodb

**Item**:  Refers to row, record, Document in other databases.

**Attribute**: Refer to column in Mysql, Postgres and Field in MongoDB and Elasticsearch.




[Expressions](https://www.dynamodbguide.com/expression-basics/#condition-expressions) are an integral part of using DynamoDB

- Expressions are rules for simple and complex CRUD operations.

- You have to follow strict syntax to write expressions

- This strict nature of expression enables DynamoDB for faster execution of queries even on millions of records/Items.

- The size of the table doesn't matter latency remains constant i.e  <10ms  for small(1 GB) or big (100 GB) tables 

| Types Of Expression       | Read | Insert | Update |
| :------------------------ | ---- | ------ | ------ |
| Projection expressions    | 1    |        |        |
| Key condition expressions | 1    |        |        |
| Condition expressions     |      | 1      | 1      |
| Update expressions        |      |        | 1      |
| Filter expressions        |      |        |        |

These Tables show the need of Expression for different Database operations.



## Condition expressions

DynamoDB write operations are unconditional, Each operation overwrites an existing item with same primary key.

Many time need arises that you only want to *insert new Item(row/documents) if it does not already exist in the table*. Which means you need some condition to be satisfied, before write operation takes place. `ConditionExpression` enables you to write your such conditions. 

**Sequence of query Execution**

1. DynamoDB retrieve the Item for given primary key. Atmost only 1 Item is retrieved as it is mandatory to specify the  primary key.
2. Then verifies that the retrieved Item satisfies the User condition (Specified in ConditionExpression) or not.
3. If User condition is satisfied then write operation is executed or else the execution fails.

**Condition expressions** always operate on an **individual item** ~~not multiple items~~  **when certain conditions are true**.

On first run, this Item is inserted successfully. If you try inserting the same Item again, you'll get an error:

```
An error occurred (ConditionalCheckFailedException) when calling the PutItem operation: The conditional request failed

```

[Alex](https://www.alexdebrie.com/posts/dynamodb-condition-expressions/) has explained ConditionExpression in detail, For example you can also refer [AWS Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html), [WorkingWithItems.ConditionalUpdate](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.ConditionalUpdate), [ConditionExpresion PutItem and UpdateItem example](https://amazon-dynamodb-labs.workshop.aws/hands-on-labs/explore-cli/cli-writing-data.html)



## Update expression

- **[Update expressions](https://www.dynamodbguide.com/expression-basics/updating-deleting-items#updating-items)** are used to update a particular attribute in an existing Item.
- This is same as `Update set column_name='value'`in mysql.
- DynamoDB Syntax


```
UpdateExpression: 'SET attributeToEdit = :newValue REMOVE attributeToDelete'
```



## Projection expressions 

- Project expressions are used to specify a subset of attributes you want to receive when reading Items. 
- We used these in our GetItem calls.
- GetItem calls are same as select queries in mysql.
- We specify column name in select queries such as `Select column1, column2, column3 from tablename` in the same way we use ProjectionExpressions to specify attributes that we want to retireve in query.



## Key condition expressions

- [**Key condition expressions**](https://www.dynamodbguide.com/expression-basics/querying#using-key-expressions) are used when querying a table with a composite primary key to limit the items selected.



## Filter expressions

- [**Filter expressions**](https://www.dynamodbguide.com/expression-basics/filtering) allow you to filter the results of queries and scans to allow for more efficient responses.



**DynamoDB limitations**

- [400kb record size](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Limits.html#limits-items)
- [Request has limitation of 1 mb](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Limits.html#limits-api)




