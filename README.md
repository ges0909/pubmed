# Java Bulk Uploader

## PubMed

_PubMed_ comprises more than 29 million citations for biomedical literature from [MEDLINE](http://www.nlm.nih.gov/bsd/pmresources.html), life science journals, and online books. Citations may include links to full-text content from _PubMed Central_ and publisher web sites.

The _PubMed_ Database is available on the NCBI FTP site under the `baseline` and `updatefiles` directories. It consists of set of citation records in **XML format** for download on an annual basis. The annual baseline is released in December of each year. Further for each day, update files that include new, revised and deleted citations, are produced. For details see the _README.txt_ file in the root of the download directory.

TODO: In Eschborn nachfragen, welche PubMed-Version für TRIP bereitgestellt wurde. Welche Attribute wurden übernommen, etc.?

## Elasticsearch

TODO: Was ist Elasticsearch?

TODO: RDBMS -> Table - Column / ES -> Index -> Type

TODO: REST Interface?

TODO: Bulk Data API? Layout JSON Records?

There are a few concepts that are core to Elasticsearch.

A **cluster** is a collection of one or more nodes (servers) that together holds the entire data and provides indexing and search capabilities across all nodes. It is valid to have a cluster with only a single node in it.

A **node** is a single server that is part of a cluster. It stores the data and participates in the cluster’s indexing and search capabilities.

An **index** is a collection of documents that have somewhat similar characteristics. An index is identified by a name whih is used to refer to the it when performing indexing, search, update, and delete operations against the documents in it. In a single cluster, you can define as many indexes as you want.

A **type** is used to be a logical category/partition of your index to allow you to store different types of documents in the same index. The concept of types will be removed in a later Elasticsearch version.

A **document** is a basic unit of information that can be indexed. A document is expressed in **JSON** (JavaScript Object Notation) format. Within an index, many documents as wanted can be stored.

An index can potentially store a large amount of data that can exceed the hardware limits of a single node. To solve this problem, Elasticsearch provides the ability to subdivide an index into multiple pieces called **shards**. When creating an index, the number of shards may be defined. Each shard is a fully-functional and independent "index" that can be hosted on any node in the cluster. Sharding allows to split/scale horizontally the content volume and distribute and parallelize operations across shards (potentially on multiple nodes) to **increase performance/throughput**. The mechanics of how a shard is distributed and how its documents are aggregated back into search requests are completely managed by Elasticsearch.

In cases where a shard/node somehow goes offline, Elasticsearch allows to make one or more copies of index’s shards into what are called **replicas**. Replicas provide high availability and allow to **scale out the search volume/throughput** since searches can be executed on all replicas in parallel.

### Summary

Each index can be split into multiple shards. An index can also be replicated zero (meaning no replicas) or more times. Once replicated, each index will have primary shards (the original shards that were replicated from) and replica shards (the copies of the primary shards).

**As result until here remains to recorded, that the number of shards and replicas are suiteable to affect the search performance.**

### Installation

Current version at time of writing is 6.5.4 (GA release) from December 19, 2018.

Requires Java 8, _Oracle JDK version 1.8.0\_131_ is recommended.

* `wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.4.zip`
* `unzip elasticsearch-6.5.4.zip`
* `rm elasticsearch-6.5.4.zip`
* `cd elasticsearch-6.5.4/`

### Running

* `bin\elasticsearch`

### Bulk Data Upload

* `wget https://download.elastic.co/demos/kibana/gettingstarted/shakespeare.json`
* `curl -H "Content-Type: application/json" -X POST "localhost:9200/shakespeare/_bulk?pretty" --data-binary @shakespeare.json`

### Java API

* low-level API close to raw REST requests
* high-level API since release 6, based on low-level API

#### Implementation

* `gradle init --type java-application`

## References

* [NCBI FTP site](ftp://ftp.ncbi.nlm.nih.gov/pubmed/) incl.
  * [PubMed Baseline Directory](ftp://ftp.ncbi.nlm.nih.gov/pubmed/baseline)
  * [PubMed Updatefiles Directory](ftp://ftp.ncbi.nlm.nih.gov/pubmed/updatefiles)
* [Elasticsearch](https://www.elastic.co/de/downloads/elasticsearch#ga-release), GA release
* [Elasticsearch Reference [6.5] » Getting Started » Basic Concepts](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-concepts.html#getting-started-concepts)
* [Elasticsearch Reference [6.5] » Document APIs » Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html)
* [Elasticsearch, Bulk Uploading and the High-Level Java REST Client - Part 1](http://www.compose.com/articles/compose-elasticsearch-bulk-uploading-and-the-high-level-java-rest-client-part-1/)
* [Elasticsearch, Bulk Uploading and the High-Level Java REST Client - Part 2](http://www.compose.com/articles/elasticsearch-bulk-uploading-and-the-high-level-java-rest-client-part-2/)
* [JMH Java Microbenchmarking Harness](https://openjdk.java.net/projects/code-tools/jmh/)
* [JMH Gradle Plugin](https://github.com/melix/jmh-gradle-plugin)

## Open Ponits

TODO: Architektübersichtsdiagramm

TODO: XML-nach-JSON Konvertierung

TODO: Warum JMH?

TODO: Welche Metriken werden gemessen? Response-Time?

