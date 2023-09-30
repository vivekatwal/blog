---
title: "Update Mapping without downtime"
datePublished: Sat Jun 10 2023 16:24:10 GMT+0000 (Coordinated Universal Time)
cuid: cliq7i3w900010al31rd97peb
slug: update-mapping-without-downtime
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686676032533/32676f0d-5cb2-48f0-b191-2f379f2b07e1.png
tags: elasticsearch

---

  
Imagine you have the application ready and up in production, all the stakeholders are celebrating and after a month you get a request for some minor changes to change the data type of a field string to a number.

many times Post Production and maintenance becomes cumbersome, hectic and takes most of your time and energy. for Years developers, the OPS Team and other stakeholders of a product have gone through these problems, and many have built out-of-the-box solutions, but this out-of-the-box solution had always been an overhead to solve one problem and unknowingly introduced another.

Slowly the industry and community felt the need to incorporate post-maintenance features within the product.

Elasticsearch has some of tools that ease the process and offload the maintainer task.

And some of the features that we will discuss are \_reindex and alias.

Elasticsearch has two types of index-level settings [static and dynamic settings](https://www.elastic.co/guide/en/elasticsearch/reference/master/index-modules.html#index-modules-settings) , `dynamic` settings can be changed on a live index, while `static` settings can only be set at **Index Creation** or **on a closed index**

For Settings that require a closed index

1. close the index
    
    ```markdown
    POST my-index/_close
    ```
    
2. Apply the settings.
    
3. Open the index
    
    ```markdown
    POST my-index/_open
    ```
    

---

## **Update Mapping without downtime**

Once the documents are indexed with existing mapping, there is no way to go back and update the mapping, Let's understand why.

Mapping contains data type for fields and other parameters, and this data type and setting tells Elasticsearch to store data in respective data structures and these data structures are stored in segments. so updating the data type for a field in mapping means re-processing the data and storing the data in a new data structure and writing this data structure back to segments.

But Segments are immutable. which means once segments are written for the first time, they cannot be updated or modified. and Hence updating mapping is not straightforward.

Now there must be an obvious question, Why do the simple feature updation of segments is not allowed?

Search Engines are expected to be a low latency even for millions of documents. And they have to be designed from a read-heavy perspective.

The reason that segments are immutable is about `Caching`

Lucene is designed to leverage the underlying OS for caching in-memory data structures. Lucene segments are stored in individual files. Because segments are immutable, these files never change. This makes them very cache friendly, and the underlying OS will happily keep hot segments resident in memory for faster access. These segments include both the inverted index (for full-text search) and doc values (for aggregations).

OK, so does it mean elasticsearch users cannot update the mapping of an index?

Yes, you cannot update the mapping of an existing index, but instead, create a new index with updated/modified mapping. but hang on, you don't have to run the same script that you have used to upload documents for the first time or go through the same process.

Elasticsearch has a very simple solution to it.

1. Create an index with updated mappings
    

1. Use [Reindex](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-reindex.html) API to copy all the documents from the old index to a new index.
    

```markdown
POST _reindex
{
  "source": {
    "index": "my-index"
  },
  "dest": {
    "index": "my-new-index"
  }
}
```

and if you have a huge volume of data, the request may timeout, so use the below syntax

```markdown
POST _reindex?wait_for_completion=false
{
  "source": {
    "index": "my-index"
  },
  "dest": {
    "index": "my-new-index"
  }
}
```

In response you get a [task](https://www.elastic.co/guide/en/elasticsearch/reference/current/tasks.html) id, you can use that task id to check the status,

```markdown
GET /_tasks/<task_id>
```

Cool, re-indexing is done, and you have a new index with updated mappings.

OK wait I just realized that either

* I will have to update the new\_index name in the code.
    
* Inform different Team using the index using kibana
    
* Update the documents
    

in short, I have to inform all the stake holders accessing, and if elastic search is used by a small team who closely coordinate than this information can be passed, But if this index is used by multiple people at multiple places, then every time you make any changes using reindex without any downtime, you have to inform each and every user.

So to overcome this challenge Elasticsearch provides with alias API, you can maintain an alias for the index and always share the alias with all the stakeholders.

```markdown
POST _aliases
{
  "actions": [
    {
      "remove": {
        "index": "my-index",
        "alias": "latest-index"
      }
    },
    {
      "add": {
        "index": "my-new-index",
        "alias": "latest-index"
      }
    }
  ]
}
```

And now If you don't need the old index, delete it to free up the space.

```markdown
DELETE my-index
```

Ready to take action? Start implementing these tips and techniques today!