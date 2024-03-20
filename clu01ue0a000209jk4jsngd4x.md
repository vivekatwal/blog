---
title: "Mappings"
datePublished: Wed Mar 20 2024 17:00:13 GMT+0000 (Coordinated Universal Time)
cuid: clu01ue0a000209jk4jsngd4x
slug: mappings

---

# Introduction

A ***schema*** is a description of one or more fields that describes the document type and how to handle the different fields of a document.

Similarly, the purpose of mapping is to define a `data type` for a field. which will then dictate how date in that fields are stored.

Each document is a collection of fields, each field is assigned a data type.

A data type is defined, depending on the operation we need to perform on those data types.

For example below table

| **Subject** | **Marks** |
| --- | --- |
| Maths | 50 |
| Science | 50 |
| History | 50 |

Subject as text and can be of text or string type, while Marks can be of int or float type.

we can assign `Marks` column a string type. but in that case we wont be able to perform numerical operation on string type.

modelling is important becasue it impacts , indexing and search for example If we store numeric and float data as strings, we will not be able to perform addition, subtraction, multiplication, division, min, max, avg, range, and other complex operations, Hence we chose numeric or float data-type.

Some exceptions in numeric data that can be stored as text are id, phone number, PANCARD

[https://xeraa.net/blog/2020\_elasticsearch-coerce-float-to-integer-or-long/](https://xeraa.net/blog/2020_elasticsearch-coerce-float-to-integer-or-long/)[https://stackoverflow.com/questions/54926346/elasticsearch-float-double-field-type-precision](https://stackoverflow.com/questions/54926346/elasticsearch-float-double-field-type-precision)

Example of how does mapping or defining data type in mysql and elasticsearch looks like

* mysql syntax
    

```json
CREATE TABLE employees(
id INT AUTO_INCREMENT PRIMARY KEY,
first_name VARCHAR(255) NOT NULL,
last_name VARCHAR(255) NOT NULL,
dob DATE,
description TEXT,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

* Equivalent elasticsearch syntax
    

```json
PUT /employee
{
  "mappings": {
    "properties": {
      "id": {
        "type": "integer"
      },
      "first_name": {
        "type": "text"
      },
      "last_name": {
        "type": "text"
      },
      "dob": {
        "type": "date"
      },
      "description": {
        "type": "text"
      },
      "created_at": {
        "type": "date"
      }
    }
  }
}
​
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687891489666/757dcbd9-6957-4d35-adfe-12b1b8e02738.png align="center")

Elasticsearch has provided a good list of data types [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-types.html)

**What is the data type and why do we need it?**

Let us take an analogy.

Imagine the scenario when you go to see a doctor to get some prescription for an illness that you are suffering with. Now, the doctor must first identify the disease that you might have and then prescribe the medicines appropriately. He would also, probably, ask for any allergies that you might have and modify the prescription accordingly.

In the case of programming languages, you can consider your body as data, the disease as your data type, the medicines as the operators/functions, or anything that can work on data, and of course you, a programmer, would be the doctor. Now, on the very basic level, you need to know what ***type*** of data are you working on. Without that, it wouldn't be easy and in some cases nigh impossible to determine how to approach towards a solution.

We can substitute a compiler/interpreter as the doctor as well. In that case, the significance of the exact type of data is even more as the compiler/interpreter must know if the program that is being fed as the input is valid or not. To be more precise, it must check if the operations that you are trying to perform are compliant with the ***data type*** of the data. It doesn't make sense to perform addition on two data points: an integer (say 893) and a string (say "programming").

**Table showing Data-Type and Operation**

| **Data-Types** | **Operations** |
| --- | --- |
| text | full text search |
| keyword | aggregation |
| Numeric | addition, subtraction, multiplication, division, min, max, avg, range |
| Date | Add, subtract, get date, get time, date range |
| Geo Datapoint (Latitude, Longitude) | a. Distance between 2 places b. Nearby places for a given lat-long |
| Vector | Calculate distance similarity Cosine similarity |
|  |  |

This table show what operations can be done a particular data-type

We define data type based on operation, first you figure out what operations has to be done to fullfill business logic and then you specify the data type.

# Data Structure

An index can be thought of as an optimized collection of documents and each document is a collection of fields, which are the key-value pairs that contain your data. By default, Elasticsearch indexes all data in every field and each indexed field has a dedicated, optimized data structure. For example, text fields are stored in inverted indices, and numeric and geo fields are stored in BKD trees. The ability to use the per-field data structures to assemble and return search results is what makes Elasticsearch so fast. [more here](https://www.elastic.co/guide/en/elasticsearch/reference/current/documents-indices.html)

It’s often useful to index the same field in different ways for different purposes. For example, you might want to index a string field as both a text field for full-text search and as a keyword field for sorting or aggregating your data. Or, you might choose to use more than one language analyzer to process the contents of a string field that contains user input.

Similarly numeric and date fields are stored in BKD as well doc\_values.

| **Type of data** | **Data Structure** |
| --- | --- |
| String | Inverted Index |
| Geo | Doc values |
| numeric, date | BKD Tree |

**What does elasticsearch do on reading the field mapping**

Elasticsearch does 2 things on basis of mappings:

* processes data according to data-type
    
* store data into different data structure depending upon the field type. We use different data structure to make different operations faster and be able to access data faster while searching.
    

Application of datatype

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687891619356/b2db2efb-2175-4fb6-9516-f2430aa15158.png align="center")

| **Data Type** | **blogs** | **Restaurant** | **Movie** | **logs** | **ecommerce** |
| --- | --- | --- | --- | --- | --- |
| text | title, article | restaurant name, menu | movie name, theatre name |  | product name, product description |
| keyword | tags |  |  | email address, hostnames, status code, tags | brand, color |
| numeric |  |  |  |  | price |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

# Different ways to do mappings

* Guessed by Elasticsearch at ingest time.
    
* Explicit mapping
    
* Dynamic Templates: [https://logz.io/blog/the-top-5-elasticsearch-mistakes-how-to-avoid-them/](https://logz.io/blog/the-top-5-elasticsearch-mistakes-how-to-avoid-them/) 5ht point Oversized template
    

## **Dynamic Mappings (Automatic, Guessed by elasticsearch)**

Elasticsearch has the ability to be schema-less, which means that documents can be indexed without explicitly providing a schema.

1. Explore
    

**Challenges or When to Specify a Custom Mapping**

1. Detected types might not be correct.
    
    For example, a timestamp is often represented in JSON as a `long`, but Elasticsearch will be unable to detect the field as a date field, preventing date filters and facets such as [**the date histogram facet**](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/search-aggregations-bucket-datehistogram-aggregation.html) from working properly.
    
2. Uses default analyzers and settings for indexing and searching.
    

> By explicitly specifying the schema, we can avoid these problems.

* It is good practice to define the [settings](https://opster.com/elasticsearch-glossary/elasticsearch-settings/) and [mapping](https://opster.com/elasticsearch-glossary/elasticsearch-mapping/) of an Index wherever possible because if this is not done, Elasticsearch tries to automatically guess the data type of fields at the time of [indexing](https://opster.com/elasticsearch-glossary/elasticsearch-indexing/). This automatic process may have disadvantages, such as [mapping](https://opster.com/elasticsearch-glossary/elasticsearch-mapping/) conflicts, duplicate data and incorrect data types being set in the index. If the fields are not known in advance, it’s better to use dynamic index [templates](https://opster.com/elasticsearch-glossary/elasticsearch-template/).
    

## **Explicit Mappings**

* skim through the **structure** and **naming** of the fields in the documents.
    
* Locate the part of the documents that you are interested to assign a mapping.
    
* Find the pattern either by **structure** or by **name** and create a expression for it.
    
* And iterate 1-3 steps untill you have mapped all the portion of the document.
    

If you are not using entire document for your application then dont index all the fields, use below snippet inside `dynamic templates` to exclude fields from indexing

```json
{
        "disable_all_else": {
          "path_match": "*",
          "path_unmatch": "*.*",
          "mapping": {
            "index": false
          }
        }
}
```

How to verify dynamic templates mappings?

1. Put dynamic templates.
    
2. Insert one sample document.
    
3. use `<index>/_mapping` to verify mapping.
    

## **Dynamic Templates (Pattern Matching)**

Pattern Matching to perform explicit matching rather than manually specifying mappings for each field manually.

Dynamic templates are specified as an array of named objects:

When to use?

1. Long documents with 100's of fields : It doesnt make sense to assign mapping to each field manually when your document has 100's of field.
    
2. you have the objects that share the same properties
    
3. You are aware of the name patterns.
    
4. Document has objects of objects that is documents are nested to 2 or more degree.
    

Pattern Matching to perform explicit matching rather than manually specifying mappings for each field manually.

Dynamic templates are specified as an array of named objects:

When to use?

1. Long documents with 100's of fields : It doesnt make sense to assign mapping to each field manually when your document has 100's of field.
    
2. you have the objects that share the same properties
    
3. You are aware of the name patterns.
    
4. Document has objects of objects that is documents are nested to 2 or more degree.
    

How to create pattern ?

* skim through the **structure** and **naming** of the fields in the documents.
    
* Locate the part of the documents that you are interested to assign a mapping.
    
* Find the pattern either by **structure** or by **name** and create a expression for it.
    
* And iterate 1-3 steps untill you have mapped all the portion of the document.
    

If you are not using entire document for your application then dont index all the fields, use below snippet inside `dynamic templates` to exclude fields from indexing

```json
{
        "disable_all_else": {
          "path_match": "*",
          "path_unmatch": "*.*",
          "mapping": {
            "index": false
          }
        }
}
```

How to verify dynamic templates mappings?

1. Put dynamic templates.
    
2. Insert one sample document.
    
3. use `<index>/_mapping` to verify mapping.
    

References:

* [https://acloudguru.com/hands-on-labs/define-elasticsearch-index-templates-and-dynamic-mappings](https://acloudguru.com/hands-on-labs/define-elasticsearch-index-templates-and-dynamic-mappings)
    
* [https://ikeptwalking.com/elasticsearch-dynamic-templates-using-match\_mapping\_type/](https://ikeptwalking.com/elasticsearch-dynamic-templates-using-match_mapping_type/)
    
* [https://stackoverflow.com/questions/31280683/create-elasticsearch-dynamic-template-to-ensure-all-fields-are-set-to-not-analyz](https://stackoverflow.com/questions/31280683/create-elasticsearch-dynamic-template-to-ensure-all-fields-are-set-to-not-analyz)
    

Dynamic mapping → Explicit Mapping → Well define Explicit mapping

[**The Workflow**](https://www.elastic.co/blog/found-mapping-workflow#the-workflow)**in Practice**

Without further ado, the workflow is a simple six-step process that may be loosely described like this:

1. Extract a sufficiently large set of example JSON documents from the data set.
    
2. Index the documents.
    
3. Run a few sample queries.
    
4. Look at the automatically generated mapping.
    
5. Refine the generated mapping.
    
6. Repeat steps 2 to 5 until I'm satisfied with the result.
    

**Note**: It takes a couple of iterations to fix the structure/type of the document fields

# Mapping Parameters

These parameters help perform different actions on data like:

* enabling/disabling indexing on particular field
    
* formating of date
    

[https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-params.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-params.html)

* copy\_to
    
* field
    
* enable
    
* position\_increment\_gap
    
* doc\_values
    
* [https://stackoverflow.com/questions/50836504/elasticsearch-mapping-parameters-index-vs-enabled](https://stackoverflow.com/questions/50836504/elasticsearch-mapping-parameters-index-vs-enabled)
    

# Research and Learning

**Random Data Generation**

Let's say if you fall into any of the cases below,

1. want to practice mapping
    
2. you are working on a new problem set
    
3. you know about that project but you don't have data and you don't have to wait for the data to and want to start the mapping process
    

The solutions are:

1. Random Data Generation [here](https://www.json-generator.com/)
    
2. Download relevant data from Kaggle
    
3. Download open-source data
    
4. Scrape Data
    

**How to Update Mappings**

One of the drawbacks of Elasticsearch is the lack of mapping updates to existing fields There are 2 ways to update mappings:

* Delete and recreate index
    
* You can add new field to existing mapping. Eg: If you have 10 fields in mappings you cannot update the mapping for those 10 fields, But you can add 11th field to mapping.
    
* Once a field has been mapped, it can not be modified unless it has been re-indexed.