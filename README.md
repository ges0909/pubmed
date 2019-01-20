# Bulk Uploader

## PubMed

_PubMed_ comprises more than 29 million citations for biomedical literature from MEDLINE, life science journals, and online books. Citations may include links to full-text content from PubMed Central and publisher web sites.

The _PubMed_ Database available on the NCBI FTP site under the `baseline` and `updatefiles` directories. It consists of set of citation records in XML format for download on an annual basis. The annual baseline is released in December of each year. Further for each day, update files that include new, revised and deleted citations, are produced. For more details see the file _README.txt_ in the root of the download directory.

## Elasticsearch

* REST interface

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

1. [NCBI FTP site](ftp://ftp.ncbi.nlm.nih.gov/pubmed/) incl.
   1. [PubMed Baseline Directory](ftp://ftp.ncbi.nlm.nih.gov/pubmed/baseline)
   1. [PubMed Updatefiles Directory](ftp://ftp.ncbi.nlm.nih.gov/pubmed/updatefiles)
1. [Elasticsearch](https://www.elastic.co/de/downloads/elasticsearch#ga-release), GA release
1. [Elasticsearch, Bulk Uploading and the High-Level Java REST Client - Part 1](http://www.compose.com/articles/compose-elasticsearch-bulk-uploading-and-the-high-level-java-rest-client-part-1/)
1. [Elasticsearch, Bulk Uploading and the High-Level Java REST Client - Part 2](http://www.compose.com/articles/elasticsearch-bulk-uploading-and-the-high-level-java-rest-client-part-2/)
