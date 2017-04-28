---
title: Elasticsearch-Quick-Start
date: 2017-04-12
tags:
- Elasticsearch
categories:
- Elasticsearch
---

Elasticsearch是一个 实时的 分布式搜索和分析引擎。
ElasticSearch基于Lucene的搜索服务器, 它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。

<!-- more -->

安装 Elasticsearch

Elasticsearch requires at least Java 8. 
Specifically as of this writing, it is recommended that you use the Oracle JDK version 1.8.0_73. 

$ java -version
java version "1.8.0"
Java(TM) SE Runtime Environment (build 1.8.0-b132)
Java HotSpot(TM) 64-Bit Server VM (build 25.0-b70, mixed mode)


```
$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.3.0.tar.gz
$ tar zxf elasticsearch-5.3.0.tar.gz 
$ cd elasticsearch-5.3.0 
$ bin/elasticsearch

$ curl http://localhost:9200/
{
    name: "xdkVW67",
    cluster_name: "elasticsearch",
    cluster_uuid: "To-C3m1kQpyMLX8suLxK7g",
    version: {
        number: "5.3.0",
        build_hash: "3adb13b",
        build_date: "2017-03-23T03:31:50.652Z",
        build_snapshot: false,
        lucene_version: "6.4.1"
    },
    tagline: "You Know, for Search"
}
```


## 参考链接   
 


## 更新记录

 
[END]