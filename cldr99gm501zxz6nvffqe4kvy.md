---
title: "How _refresh work in ES in practice"
datePublished: Mon Jan 03 2022 17:43:42 GMT+0000 (Coordinated Universal Time)
cuid: cldr99gm501zxz6nvffqe4kvy
slug: how-refresh-work-in-es-in-practice

---

## Learning By doing 



Many Processes in elasticsearch are automated and help a new developer to start the journey faster and easily. But later instead of digging deeper, we rely on default setting, this restricts us from exploring and getting a deeper understanding and also limits our visualisation on the flow of working , it also make us poor in troubleshooting.  



Create a index with 2 shard and set `refresh_interval` to 1 minute. We are setting the environment with this setting

```
PUT my-index
{
  "settings": {
    "index": {
      "number_of_shards": "2",
      "refresh_interval": "1m"
    }
  }
}
```



Execute to see no documents exists

```
GET my-index/_search
```

run _stats 

```
GET my-index/_stats/refresh,flush
```

Before moving ahead its important to understand the structure of stats output, Look at `primaries.refresh.total`value and `primaries.flush.total`, these values are of use to us.

Now lets insert a document

```
POST my-index/_doc/1
{
  "description": "inspecting index stats"
}
```

and lets query for a document `GET my-index/_search` you will not find any document, the documents are only visible after **refresh** operation takes place. (default refresh interval is 30s, we have to set it to 1 min for experiment purpose).

lets refresh the index manually, using below command

```
POST my-index/_refresh
```

now check the refresh count using `GET my-index/_stats/refresh,flush` and document using `GET my-index/_search` .

Lets Repeat same for deletion of document.

1. `DELETE my-index/_doc/1`
2. Check the refresh count using `GET my-index/_stats/refresh,flush` 
3. Perform manual refresh for operation to reflect `POST my-index/_refresh`
4. After refresh , go to step 2.

What we saw in this article was, 

- changes are reflected after _refresh takes place.
- How to check total number of refresh operation using _stats API.



These same steps can be performed for `_flush` and `_forcemerge`









