---
title: "Installation of ELK"
datePublished: Sat Jun 10 2023 16:33:40 GMT+0000 (Coordinated Universal Time)
cuid: cliq7ubla00040aml0h4temlr
slug: installation-of-elk
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686675813985/a899e0b6-70e8-4bdc-a018-cb1b80e7bdf3.png
tags: elasticsearch

---

Install Java

```markdown
sudo apt install default-jre -y              # version 2:1.11-72
sudo apt install openjdk-8-jre-headless -y
```

[Download](https://www.java.com/en/) [Official Java Installation guide](https://www.java.com/en/download/help/download_options.html)

## **Elasticsearch**

Elasticsearch is available for different platforms [Elasticsearch](https://www.elastic.co/downloads/past-releases/elasticsearch-7-10-0) [Kibana](https://www.elastic.co/downloads/past-releases/kibana-7-10-0) [Logstash](https://www.elastic.co/downloads/past-releases/logstash-7-10-0) . If you are looking for a particular version of elasticsearch find [here](https://www.elastic.co/downloads/past-releases) , In this article, we will go ahead with ELK 7.10 for Ubuntu.

1. Download and run elasticsearch
    

```markdown
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.0-linux-x86_64.tar.gz
​
tar -xzf elasticsearch-7.10.0-linux-x86_64.tar.gz
​
cd elasticsearch-7.10.1/
```

1. Start elasticsearch
    

```markdown
./bin/elasticsearch
```

1. Once elasticsearch is started, Let's test by hitting [`localhost:9200`](http://localhost:9200)
    

## **Kibana**

1. Download and unzip kibana
    

```markdown
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.10.0-linux-x86_64.tar.gz
​
tar -xzf kibana-7.10.0-linux-x86_64.tar.gz
​
cd kibana-7.10.0-linux-x86_64/
```

1. start kibana
    

```markdown
./bin/kibana
```

## **Tips**

* To run elasticsearch as a daemon in the background `./bin/elasticsearch -d -p pid` and to shut down Elasticsearch, kill the process ID recorded in the PID file: `pkill -F pid`
    

## **What few commands to check on starting elasticsearch**

* Getting information about clusters and nodes
    
    ```markdown
    GET _API/parameter
    ```
    
* GET info about cluster
    
    ```markdown
    GET _cluster/health
    ```
    
* Get info about nodes in a cluster
    
    ```markdown
    GET _nodes/stats
    ```
    

---

## Uploading data to elasticsearch

This code can be used to generate ndjson from json for fast insertion of data in elasticsearch for experiments

```markdown
Json to ndjson
jq -c -r ".[]" input.json | while read line; do echo '{"index":{}}'; echo $line; done > bulk.json
​
curl -XPOST localhost:9200/your_index/your_type/_bulk -H "Content-Type: application/x-ndjson" --data-binary @bulk.json
​
```