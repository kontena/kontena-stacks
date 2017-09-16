HA Kafka cluster on Kontena
===========================

[Kafka](https://kafka.apache.org/) is used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, wicked fast, and runs in production in thousands of companies.

(based on Kafka stack used in [HHypermap BOP -- Harvard Hypermap, Billion Object Platform](https://github.com/cga-harvard/hhypermap-bop))

## Install

Prerequisites: You need to have working Kontena Container Platform installed. If you are new to Kontena, check quick start guide.


Kafka and Zookeeper are stateful services, therefore you must first create a Kontena volume.  For a local volume run the following commands:

```
$ kontena volume create --scope instance --driver local kafka-cluster-zookeeper-data
$ kontena volume create --scope instance --driver local kafka-cluster-kafka-data
```

Next install the stack itself.  There are 3 options available, configured with environment variables or interactively via prompts:

| Option | Description |
| -------| ------------|
| `ZOOKEEPER_URI` | URI of Zookeeper cluster.  Default value if using Kontena Zookeeper stack in the same grid |
| `NUM_INSTANCES` | Number of instances of Kafka broker.  Default is 3. |
| `EXPOSE_KAFKA_PORT` | Boolean, if true the Kafka port 9092 will be exposed to the host node.  Defaults to `false` |
| `SKIP_VOLUMES` | Boolean, if true no volumes are mapped.  Useful for local development.  Defaults to `false` |

Generally, the default values are good for a basic cluster setup.

To initially install:

```
$ kontena stack install
```

To upgrade:

```
$ kontena stack upgrade kafka-cluster
```

Other services can now connect to Kafka using the address `kafka.kafka-cluster.${GRID}.kontena.local:9092`.

## Local Development
The `kafka-cluster` stack is also very useful if you are developing systems that use Kafka even when your development environment itself is not running inside Kontena.  To run a local development setup, make sure to do the following steps:

1. Make sure you also create local Zookeeper stack
2. Set `NUM_KAFKA_INSTANCES` to 1
3. Set `EXPOSE_KAFKA_PORT` to `true` (this will make port 9092 on your development machine connect to Kafka inside Kontena)
4. Optionally set `SKIP_VOLUMES` to `true` 
5. Add an `/etc/hosts` file entry (assuming here our Kontena grid name is `dev`) `127.0.0.1  kafka.kafka-cluster.dev.kontena.local` (for Vagrant development setups you may want to change 127.0.0.1 to the address of your Vagrant VM).

Now services outside of the Kontena grid can connect to Kafka using the address `kafka.kafka-cluster.dev.kontena.local:9092`.

## Configuration
Thanks to Kontena's `service exec` feature, it's fairly easy to run the various management tools Kafka provides without having to have direct `ssh` access to Kafka.

Examples:

- Creating a single partition, single replica topic:

```
$ kontena service exec kafka-cluster/kafka /usr/bin/kafka-topics --create --zookeeper zookeeper.zookeeper-cluster.dev.kontena.local:2181 --replication-factor 1 --partitions 1 --topic mytopic
```

- List all topics:

```
$ kontena service exec kafka-cluster/kafka /usr/bin/kafka-topics --list --zookeeper zookeeper.zookeeper-cluster.dev.kontena.local:2181
```

- Interactively listen for all events on a topic from the beginning:

```
$ kontena service exec -it kafka-cluster/kafka sh
$ /usr/bin/kafka-console-consumer --bootstrap-server kafka:9092 --topic mytopic --from-beginning
```

- Interactively publish events to a topic:

```
$ kontena service exec -it kafka-cluster/kafka sh
$ /usr/bin/kafka-console-producer --broker-list kafka:9092 --topic mytopic
```