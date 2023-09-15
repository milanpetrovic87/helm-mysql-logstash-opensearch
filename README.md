This helm repo makes the installation of Logstash for Opensearch. If you try to install Logstash helm for elk and try to implement it in Opensearch you probably see issues in implementation. 

The repo for Logstash in ELK is not compatible with Opensearch.

**Why do we need Logstash?**

Logstash is an agent that collects logs from Elastic/Opensearch cluster. 

In this scenario, we made one example of SQL database (mysql) which will contain some data. That data will be input for Logstash, then after processing data will be output to Opensearch. 

**How does it work?**

Prerequisite: You will need to have running Opensearch cluster accessible in cluster at port 9200

Here we have a 3 repos

1\.[mysql-opensearch](https://github.com/milanpetrovic87/helm-mysql-logstash-opensearch/tree/main/mysql-opensearch) which creates base mysql without persistence storage. This is for the purpose of testing only, in production, we will have pv and pvc. Once when you create db you need to make database, table and populate data. Example used in this scenario is given here:
<https://www.elastic.co/guide/en/cloud/current/ec-getting-started-search-use-cases-db-logstash.html>

2\. [Logstash-helm](https://github.com/milanpetrovic87/helm-mysql-logstash-opensearch/tree/main/logstash-helm) this repo creates helm deployment for logstash in opensearch.

3\. [Logstash-with-pvc](https://github.com/milanpetrovic87/helm-mysql-logstash-opensearch/tree/main/logstash-with-pvc) creates logstash with configuration for mysql and opensearch connection. 

- Here you will need to create pv and pvc beforehand because you will need a driver for mysql connection to be included in deployment.
- Download jdbc.jar driver from official mysql web site

You need to use kubectl to create persistent volume (pv) and persistent volume claim (pvc) in your cluster. So there are two files in repo [pod-file-share.yaml](https://github.com/milanpetrovic87/helm-mysql-logstash-opensearch/blob/main/pod-file-share.yaml) which creates pv and [pvc.yaml](https://github.com/milanpetrovic87/helm-mysql-logstash-opensearch/blob/main/pvc.yaml) which creates pvc. Note this is an example of Azure storage creation.

The end result is index created in Opensearch

![](Aspose.Words.b5cc3e24-b648-4371-a94f-ba1e15bede55.001.png)
