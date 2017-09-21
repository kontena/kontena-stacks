HA Kafka cluster on Kontena
===========================

[Kafka](https://kafka.apache.org/) is used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, wicked fast, and runs in production in thousands of companies.

(based on Kafka stack used in [HHypermap BOP -- Harvard Hypermap, Billion Object Platform](https://github.com/cga-harvard/hhypermap-bop))

## Install

Prerequisites: You need to have working Kontena Container Platform installed. If you are new to Kontena, check quick start guide.  You also need a running Zookeeper cluster.  For the simplest installation, use the Kontena provided stack `kontena/zookeeper-cluster`.

Kafka is a stateful service, therefore you must first create a Kontena volume.  For a local volume run the following command:

```
$ kontena volume create --scope instance --driver local kafka-cluster-data
```

For local development purposes you can skip volume creation by using the `SKIP_VOLUMES` variable.

Next install the stack itself.  There are multiple options available, configured with environment variables or interactively via prompts:

| Option | Description |
| -------| ------------|
| `LINK_ZOOKEEPER` | Boolean, if true use a Zookeeper Kontena service, otherwise specify an external URI.  Defaults to true. |
| `ZOOKEEPER_LINK` | If `LINK_ZOOKEEPER` is true, this is the service to link to. |
| `ZOOKEEPER_URI` | If `LINK_ZOOKEEPER` is false, this is the URI of Zookeeper to use. |
| `NUM_INSTANCES` | Number of instances of Kafka broker.  Default is 3. |
| `EXPOSE_KAFKA_PORT` | Boolean, if true the Kafka port 9092 will be exposed to the host node.  Defaults to `false` |
| `SKIP_VOLUMES` | Boolean, if true no volumes are mapped.  Useful for local development.  Defaults to `false` |
| `KAFKA_VARIABLES` | Comma delimited list of Kafka config variables.  Of the form `KAFKA_SOME_VAR=value`, which is transformed into the Kafka config form `some.var=value`.  Any variable containing `replication.factor` will never be set to a value greater than `NUM_INSTANCES` (`offsets.topic.replication.factor`, `transaction.state.log.replication.factor`, `default.replication.factor`, `config.storage.replication.factor`, `offset.storage.replication.factor`, `status.storage.replication.factor`). |

Generally, the default values are good for a basic cluster setup.

To initially install:

```
$ kontena stack install
```

To upgrade:

```
$ kontena stack upgrade kafka-cluster
```

Other services inside your Kontena Grid can now connect to Kafka using the address `kafka.kafka-cluster.${GRID}.kontena.local:9092`.

## Local Development
The `kafka-cluster` stack is also very useful if you are developing systems that use Kafka even when your development environment itself is not running inside Kontena.  To run a local development setup, make sure to do the following steps (examples assume a Kontena Grid named `dev`):

1. Create a local Zookeeper stack: `NUM_INSTANCES=1 SKIP_VOLUMES=true kontena stack install kontena/zookeeper-cluster`
2. Create a local Kafka stack: `NUM_INSTANCES=1 SKIP_VOLUMES=true EXPOSE_KAFKA_PORT=true kontena stack install kontena/kafka-cluster`
3. Add an `/etc/hosts` file entry (assuming here our Kontena grid name is `dev`) `127.0.0.1  kafka.kafka-cluster.dev.kontena.local` (for Vagrant development setups you may want to change 127.0.0.1 to the address of your Vagrant VM).

Now services outside of the Kontena grid can connect to Kafka using the address `kafka.kafka-cluster.dev.kontena.local:9092`.

## Configuration
Thanks to Kontena's `service exec` feature, it's fairly easy to run the various management tools Kafka provides without having to have direct `ssh` access to Kafka.

Examples:

- List all topics:

```
$ kontena service exec kafka-cluster/kafka /usr/bin/kafka-topics --list --zookeeper zookeeper.zookeeper-cluster.dev.kontena.local:2181
```


- Creating a single partition, single replica topic:

```
$ kontena service exec kafka-cluster/kafka /usr/bin/kafka-topics --create --zookeeper zookeeper.zookeeper-cluster.dev.kontena.local:2181 --replication-factor 1 --partitions 1 --topic mytopic
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