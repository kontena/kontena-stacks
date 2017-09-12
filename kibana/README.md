# Kibana on Kontena

[Kibana](https://www.elastic.co/products/kibana) Kibana lets you visualize your Elasticsearch data and navigate the Elastic Stack.

## Install

> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start). You also need to have working installation of `kontena/elasticsearch` stack.

Install Kontena Load Balancer stack (optional)
`$ kontena stack install kontena/ingress-lb`

Install Kibana stack
`$ kontena stack install kontena/kibana`

This will deploy Kibana and connect it to Elasticsearch.


