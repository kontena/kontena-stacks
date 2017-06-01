RabbitMQ Cluster on Kontena
===========================

[RabbitMQ](https://www.rabbitmq.com) is the most widely deployed open source message broker

(based on [harbur/rabbitmq-cluster](https://github.com/harbur/docker-rabbitmq-cluster))

## Install

Prerequisites: You need to have working Kontena Container Platform installed. If you are new to Kontena, check quick start guide.

$ kontena stack install kontena/harbur-rabbitmq-cluster

This will deploy stateful RabbitMQ cluster to your grid. Other services can connect to it with amqp://harbur-rabbitmq-cluster.${GRID}.kontena.local address

Note: Replace ${GRID} with your grid name.
