# Elasticsearch on Kontena

[Elasticsearch](https://www.elastic.co/products/elasticsearch) is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases.


### Prerequisites

You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start). You also need to have working installation of `kontena/elasticsearch` stack.

Elasticsearch is a bit memory hungry, so your nodes should have plenty of mem available.

The default operating system limits on mmap counts is likely to be too low, which may result in out of memory exceptions. So increase the `max_map_count`on the hosts. This can be done for example with:
```
kontena node ssh node-1 sudo sysctl -w vm.max_map_count=262144
```


## Install

Install Elasticsearch stack
`$ kontena stack install kontena/elasticsearch`

This will deploy Elasticsearch. If you've specified more than one instance, Elasticsearch will automatically clusterize itself. Before connecting any apps to it it's probably good idea to wait until the cluster status goes green. See https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-health.html how to check cluster status.


