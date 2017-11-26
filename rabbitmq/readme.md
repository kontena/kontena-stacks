RabbitMQ Cluster on Kontena
===========================

[RabbitMQ](https://www.rabbitmq.com) is the most widely deployed open source message broker

(based on [harbur/rabbitmq-cluster](https://github.com/harbur/docker-rabbitmq-cluster))

## Install

Prerequisites: You need to have working Kontena Container Platform installed. If you are new to Kontena, check quick start guide.

RabbitMQ is a stateful service, therefore you must first create a Kontena volume.  For a local volume run the following command:

```
$ kontena volume create --scope instance --driver local harbur-rabbitmq-cluster-seed-data
$ kontena volume create --scope instance --driver local harbur-rabbitmq-cluster-node-data
```

$ kontena stack install kontena/harbur-rabbitmq-cluster

This will deploy stateful RabbitMQ cluster to your grid. Other services can connect to it with amqp://harbur-rabbitmq-cluster.${GRID}.kontena.local address.

Note: Replace ${GRID} with your grid name.

## Event Bus

This stack will create a new VHost called "eventbus" as well as an associated user and password. This can be used by applications instead of having to give out access to the default VHost and admin user.  To connect to this VHost, just link to the Vault secret `harbur-rabbitmq-cluster-eventbus-uri`.


## Admin UI

The admin UI will be enabled, but is only available after opening a VPN connection to the Grid.  After that you should be able to connect via the URL `http://node.harbur-rabbitmq-cluster.${GRID}.kontena.local:15672`.