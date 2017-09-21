# EFK Stack

EFK stack sets up log storage and analytics stack using Elasticsearch, Fluentd and Kibana.

Currently Kontena EFK setup is actually using multiple stacks to make all the parts highly re-usable.

Following chapters describe how to set up EFK using ready made stacks. It's advised to install the stacks in the order defined here.

## Elasticsearch

Set up Elasticsearch using [`kontena/elasticsearch`](https://github.com/kontena/kontena-stacks/tree/master/elasticsearch) stack. It needs volumes to store Elasticsearch data persistently. Those volumes should be `instance` scoped as Elasticsearch itself replicates the data.

The initial setup of Elasticsearch stack creates new passwords in Kontena secrets vault for the default users in Elasticsearch and configures Elasticsearch to use those. The same secrets are also automatically used when installing Kibana and Fluentd stacks.

## Fluentd

Fluentd is used to receive the log data and to store it in Elasticsearch.

Fluentd can be set up using [`kontena/fluentd-elasticsearch`](https://github.com/kontena/kontena-stacks/tree/master/fluentd/elasticsearch) stack. You need to configure the elasticsearch hostname where fluentd will store the data.


## Kibana

Kibana is used to query and visualize the logs stored and indexed in Elasticsearch.

Kibana can be setup easily with [`kontena/kibana`](https://github.com/kontena/kontena-stacks/tree/master/kibana) stack.


## TODO

With upcoming Kontena 1.4 stack dependency mechanism it will be possible to create "top-level" EFK stack that uses these other stacks as building blocks.

So when 1.4 is generally available, there shall be a top level EFK stack created. :)