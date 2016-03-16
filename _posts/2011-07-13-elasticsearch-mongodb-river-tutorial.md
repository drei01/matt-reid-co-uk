---
layout: post
title: elasticsearch mongodb river tutorial
---

[Elasticsearch](http://www.elasticsearch.org/) is a distributed,
scalable nosql search server built on
[lucene](http://lucene.apache.org/java/docs/index.html). It can use
plugins(rivers) to hook into changes made on other databases such
as[couchdb](http://www.elasticsearch.org/blog/2010/09/28/the_river_searchable_couchdb.html). 








There is currently no "official" river for mongodb and elasticsearch but
aparo has written one and it is available on hit g[ithub
repo](https://github.com/aparo/elasticsearch/blob/master/plugins/river/mongodb/src/main/java/org/elasticsearch/river/mongodb/MongoDBRiver.java).










Here is how to go about installing it.










-   Download the mongodb river
    [HERE](http://www63.zippyshare.com/v/44146885/file.html)
-   unzip into $ES_HOME/plugins/mongodb_river/
-   restart elasticsearch
-   run the following to index a collection on elasticsearch:



    !/bin/bash
    curl -X PUT localhost:9200/_river/mongodb/_meta -d '{
            "type":"mongodb",
            "mongodb":{
                    "db":"DATABASE_NAME",
                    "collection":"COLLECTION",
            "index":"ES_INDEX_NAME"
            }
    }'





 









